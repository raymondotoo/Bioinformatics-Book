# Chapter 19: Interactive Visualization of WGCNA Results


<div class="download-slides">
📥 <a href="../slides/chapter-18.pptx" download>Download Lecture Slides (PPTX)</a>
</div>

## 19.1 Visualizing WGCNA Results

While static plots are useful, WGCNA generates a wealth of data that is best explored interactively. In this chapter, we build a Shiny dashboard to explore the network analysis results from Chapter 18.

## 19.2 Dashboard Structure

<p align="center">
  <img src="../assets/illustrations/shiny-dashboard.svg" alt="Illustration of Shiny Dashboard">
</p>

Try the interactive module-trait heatmap demo here: [Interactive WGCNA Heatmap](../interactive/wgcna.html)

We will use `shinydashboard` to organize the results into three main tabs:
1.  **Network Topology:** Visualizing the soft thresholding and scale-free fit.
2.  **Module Detection:** Exploring the dendrogram and module assignment.
3.  **Module-Trait Relationships:** An interactive heatmap correlating modules with clinical variables.

## 19.3 Bioinformatics in Action: The Shiny App

Here is the structure of the `app.R` file designed to visualize WGCNA outputs.

```r
library(shiny)
library(shinydashboard)
library(WGCNA)
library(gplots)

# 1. UI Definition
ui <- dashboardPage(
  dashboardHeader(title = "WGCNA Results Viewer"),
  
  dashboardSidebar(
    sidebarMenu(
      menuItem("Network Topology", tabName = "topology", icon = icon("chart-line")),
      menuItem("Dendrogram", tabName = "dendro", icon = icon("tree")),
      menuItem("Module-Trait Heatmap", tabName = "heatmap", icon = icon("th"))
    )
  ),
  
  dashboardBody(
    tabItems(
      # Tab 1: Topology
      tabItem(tabName = "topology",
              h2("Scale-Free Topology Fit"),
              plotOutput("sftPlot")),
      
      # Tab 2: Dendrogram
      tabItem(tabName = "dendro",
              h2("Clustering Dendrogram"),
              plotOutput("dendroPlot", height = "600px")),
      
      # Tab 3: Heatmap
      tabItem(tabName = "heatmap",
              h2("Module-Trait Relationships"),
              plotOutput("heatmapPlot", height = "800px"))
    )
  )
)

# 2. Server Logic
server <- function(input, output) {
  
  # In a real deployment, load the pre-computed RData from the pipeline
  # load("wgcna_results.RData")
  
  output$sftPlot <- renderPlot({
    # Placeholder for the Scale-Free Topology Plot generated in Step 2
    plot(1:10, type="n", xlab="Soft Threshold (power)", ylab="Scale Free Topology Model Fit,signed R^2", main = "Scale independence")
    text(1:10, 1:10, labels=1:10, col="red")
    abline(h=0.90, col="red")
  })
  
  output$dendroPlot <- renderPlot({
    # Placeholder for the Dendrogram generated in Step 3
    # plotDendroAndColors(geneTree, dynamicColors, "Dynamic Tree Cut", dendroLabels = FALSE, hang = 0.03, addGuide = TRUE, guideHang = 0.05)
    plot(1:10, main = "Gene Dendrogram and Module Colors")
  })
  
  output$heatmapPlot <- renderPlot({
    # Placeholder for the Heatmap generated in Step 4
    # labeledHeatmap(Matrix = moduleTraitCor, xLabels = names(clinical_traits), yLabels = names(MEs), ySymbols = names(MEs), colorLabels = FALSE, colors = blueWhiteRed(50), textMatrix = textMatrix, setStdMargins = FALSE, cex.text = 0.5, zlim = c(-1,1), main = paste("Module-trait relationships"))
    image(1:10, 1:10, matrix(1:100, nrow=10), main = "Module-Trait Correlation Heatmap")
  })
}
```

## Summary

By building an R Shiny app, we transformed static analysis results into a dynamic tool for discovery. This allows domain experts to interact with the data directly, fostering better collaboration between bioinformaticians and clinicians.

## 19.4 Deployment and Packaging Options

Options for making interactive results accessible:

- **Shiny Server / shinyapps.io:** Host Shiny apps for live, server-rendered interactivity (requires active R session).
- **Static HTML widgets:** Use `htmlwidgets` (e.g., `plotly`, `DT`) embedded in R Markdown HTML reports for zero-dependency sharing.
- **Pre-computed RData:** Package pre-computed `.RData` or `.rds` files so the app loads instantly without re-running analyses.

Choose the approach that fits your audience; for broad dissemination, static HTML reports with embedded widgets are often easiest to share.