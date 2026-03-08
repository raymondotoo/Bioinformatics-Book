# Chapter 18: Interactive Visualization with R Shiny

## 18.1 Why R Shiny?

In the previous chapter, we performed complex analyses on the ADNI-ADRC datasets. However, static plots and tables are often insufficient for exploring high-dimensional proteomic data.

**R Shiny** is a powerful framework that allows data scientists to build interactive web applications straight from R. It bridges the gap between statistical analysis and user-friendly visualization, allowing clinicians to explore the data without writing a single line of code.

## 18.2 App Architecture

A Shiny app has two main components:

1.  **UI (User Interface):** Defines how the app looks (layout, inputs, outputs).
2.  **Server:** Defines how the app works (the R code that runs the analysis and generates plots).

For our clinical proteomics app, we used `shinydashboard` to create a professional, modular layout.
The app reads the processed data and statistical results generated in Chapter 17.

## 18.3 Key Modules

### Module 1: Cohort Explorer
This module provides a high-level overview of the study population. We used `ggplot2` and `plotly` to create dynamic pie charts and histograms. Users can filter by age, sex, and diagnosis to understand the demographics of specific sub-cohorts.

### Module 2: Protein Query Engine
The core of the app allows users to query specific proteins (e.g., "APOE", "CLU").
*   **Reactive Filtering:** When a user selects a protein, the server instantly subsets the massive dataset.
*   **Visualization:** The app generates boxplots showing expression levels across disease groups (CN, MCI, AD) and Volcano plots highlighting differential expression.

### Module 3: Survival Analysis Interface
This advanced module integrates the `survival` and `survminer` packages. Users can define "High" vs. "Low" expression groups (e.g., based on a median split) and generate Kaplan-Meier curves on the fly to assess prognostic value.

## 18.4 Deployment and Reproducibility

To ensure the app is robust and shareable:
*   **Containerization:** We used **Docker** to package the app, R installation, and all required libraries into a single container. This guarantees the app runs identically on any server.
*   **Shiny Server:** The app is hosted on a Shiny Server, allowing multiple users to access it simultaneously via a web browser.

## 18.5 Bioinformatics in Action: A Simple Shiny App
## 18.5 Bioinformatics in Action: Building the Dashboard

Here is a minimal example of a Shiny app that allows a user to select a dataset and view a histogram.
Here is a simplified structure of the actual `app.R` file used for the ADNI-ADRC viewer.

```r
library(shiny)
library(shinydashboard)
library(ggplot2)

# 1. Define UI
ui <- fluidPage(
  titlePanel("Simple Data Viewer"),
# 1. UI Definition
ui <- dashboardPage(
  dashboardHeader(title = "ADNI-ADRC Proteomics"),
  
  sidebarLayout(
    sidebarPanel(
      selectInput("dataset", "Choose a dataset:", 
                  choices = c("pressure", "cars")),
      sliderInput("bins", "Number of bins:",
                  min = 1, max = 50, value = 30)
    ),
    
    mainPanel(
      plotOutput("distPlot")
  dashboardSidebar(
    sidebarMenu(
      menuItem("Cohort Explorer", tabName = "cohort", icon = icon("users")),
      menuItem("Protein Query", tabName = "query", icon = icon("search"))
    )
  ),
  
  dashboardBody(
    tabItems(
      # Tab 1: Cohort Explorer
      tabItem(tabName = "cohort",
              h2("Cohort Demographics"),
              plotOutput("age_dist_plot")),
      
      # Tab 2: Protein Query
      tabItem(tabName = "query",
              h2("Differential Expression"),
              selectInput("protein_select", "Select Protein:", choices = c("APOE", "CLU", "PTK2B")),
              plotOutput("boxplot"))
    )
  )
)

# 2. Define Server Logic
# 2. Server Logic
server <- function(input, output) {
  
  output$distPlot <- renderPlot({
    # Select data based on user input
    if (input$dataset == "pressure") {
      x <- pressure$temperature
    } else {
      x <- cars$speed
    }
  # Reactive plot for Protein Query
  output$boxplot <- renderPlot({
    req(input$protein_select)
    # In the real app, 'data' comes from the loaded datasets
    # ggplot(data, aes(x=Diagnosis, y=.data[[input$protein_select]], fill=Diagnosis)) +
    #   geom_boxplot() +
    #   theme_minimal()
    
    # Draw the histogram with the specified number of bins
    hist(x, breaks = input$bins, col = 'darkgray', border = 'white',
         main = paste("Histogram of", input$dataset))
    # Placeholder for demonstration
    plot(1:10, main = paste("Expression of", input$protein_select))
  })
}

# 3. Run the App
# shinyApp(ui = ui, server = server)
```

## Summary

By building an R Shiny app, we transformed static analysis results into a dynamic tool for discovery. This allows domain experts to interact with the data directly, fostering better collaboration between bioinformaticians and clinicians.