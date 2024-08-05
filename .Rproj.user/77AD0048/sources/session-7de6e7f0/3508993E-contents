# AutoStruct Dynamics: Organizational Chart Visualization

## Introduction

In the complex and globally interconnected automobile industry, visual clarity on organizational structures is crucial for strategic operations. Stephen Elvis Ampah has crafted "AutoStruct Dynamics," a cutting-edge tool built in R, designed to map and visualize these structures with precision, focusing on a fictional yet illustrative global automobile company.

## Background

The automobile sector operates through a network of intricate relationships spanning various geographical and functional divisions. Each division from design, production, to sales holds vital importance. "AutoStruct Dynamics" is designed to delineate these structures, facilitating a deeper understanding of interdepartmental interactions and hierarchies.

## The Dataset

The core of "AutoStruct Dynamics" is powered by a dataset represented in the R `data.table` object, `dt`. This table succinctly encapsulates the hierarchical structure of a large, multinational automobile company:

- **Top Level (CAR)**: Represents the corporate entity, under which two major geographical divisions are categorized: German and America.
- **Second Level (German, America)**: These nodes branch out into specific brands or subsidiaries. German covers European operations with brands like AUDI, BMW, and Opel. America represents operations in the USA with brands such as RAM, GMC, and Jeep.
- **Leaf Nodes (Brands)**: The terminal points of the chart, representing individual brands that operate under their respective geographical divisions.

This dataset is structured to reflect the complex, multi-layered relationships within the company, showcasing how corporate directives flow down to regional divisions and further into specific brands.

## The Tool

Using libraries like `highcharter`, `dplyr`, and `data.table`, the "AutoStruct Dynamics" tool visualizes these relationships within a highly interactive framework. Users can explore the corporate hierarchy from the top level down to individual brands, with tooltips and dynamic data labels providing detailed insights into each division's scale and operations.

## Features

- **Interactive Visualization**: By interacting with the chart, users can uncover the specifics of each division and subsidiary, including strategic roles and output capacities.
- **Real-Time Data Integration**: The tool supports updates with real-time data, reflecting organizational changes as they happen.
- **Customizable Detail Levels**: Users can adjust the visualization to show varying levels of detail, suitable for different analytical needs.

## Implementation

The implementation of this visualization involves setting up the data table `dt`, configuring the Highcharts organization chart options, and enhancing interactivity with custom JavaScript functions for tooltips and data labels. This setup ensures a user-friendly interface and a deeply informative visualization experience.

## Impact and Future Directions

"AutoStruct Dynamics" helps stakeholders in the automobile industry to visualize and understand corporate structures for better strategic decision-making. Future updates may include adaptable frameworks for different industries and advanced predictive models to forecast organizational changes.

## Conclusion

"AutoStruct Dynamics" serves as a strategic visualization tool that simplifies the complexity of corporate hierarchies in the automobile industry, providing actionable insights and fostering a comprehensive understanding of internal and competitive dynamics.


Mr Stephen Elvis Ampah 
05.08.2024

``` r
library(highcharter)
```

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

    ## Highcharts (www.highcharts.com) is a Highsoft software product which is

    ## not free for commercial and Governmental use

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(data.table)
```

    ## 
    ## Attaching package: 'data.table'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     between, first, last

``` r
library(webshot2)
library(htmlwidgets)
```

``` r
XY <- c(24015319, 480442671, 57765129, 6772172, 9401538, 57940350)
MN <- c(17945543, 300517552, 31052000, 2798460, 8626025, 1894563)

dt <- data.table(
  from = c("CAR", "CAR", "German", "German", "German", "America", "America", "America"),
  to = c("German", "America", "AUDI", "BMW", "Opel", "RAM", "GMC", "Jeep")
)

# Customize tooltip to show XY and MN values for links and nodes
Tooltip <- JS(
  "function() {
      let total_xy = 0;
      let total_mn = 0;
      if (this.point.id === 'German') {
        ['AUDI', 'BMW', 'Opel'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Total: ' + total_xy.toLocaleString('de-DE') + '<br>Change: ' + total_mn.toLocaleString('de-DE');
      } else if (this.point.id === 'America') {
        ['RAM', 'GMC', 'Jeep'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Total: ' + total_xy.toLocaleString('de-DE') + '<br>Change: ' + total_mn.toLocaleString('de-DE');
      } else if (this.point.id === 'AUDI' || this.point.id === 'BMW' || this.point.id === 'Opel' || this.point.id === 'RAM' || this.point.id === 'GMC' || this.point.id === 'Jeep') {
        return this.point.name + '<br>Total: ' + this.point.xy.toLocaleString('de-DE') + '<br>Change: ' + this.point.mn.toLocaleString('de-DE');
      } else if (this.point.id === 'CAR') {
        ['AUDI', 'BMW', 'Opel', 'RAM', 'GMC', 'Jeep'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Total: ' + total_xy.toLocaleString('de-DE') + '<br>Change: ' + total_mn.toLocaleString('de-DE');
      } else {
        return this.point.name;
      }
    }"
)

Datalabel <- JS(
  "function() {
      let total_xy = 0;
      let total_mn = 0;
      if (this.point.id === 'German') {
        ['AUDI', 'BMW', 'Opel'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Ist: ' + Highcharts.numberFormat(total_xy/1000000, 2, ',', '.') + ' Mio.<br>Δ: ' + Highcharts.numberFormat(total_mn/1000000, 2, ',', '.') + ' Mio.';
      } else if (this.point.id === 'America') {
        ['RAM', 'GMC', 'Jeep'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Ist: ' + Highcharts.numberFormat(total_xy/1000000, 2, ',', '.') + ' Mio.<br>Δ: ' + Highcharts.numberFormat(total_mn/1000000, 2, ',', '.') + ' Mio.';
      } else if (this.point.id === 'AUDI' || this.point.id === 'BMW' || this.point.id === 'Opel' || this.point.id === 'RAM' || this.point.id === 'GMC' || this.point.id === 'Jeep') {
        return this.point.name + '<br>Ist: ' + Highcharts.numberFormat(this.point.xy/1000000, 2, ',', '.') + ' Mio.<br>Δ: ' + Highcharts.numberFormat(this.point.mn/1000000, 2, ',', '.') + ' Mio.';
      } else if (this.point.id === 'CAR') {
        ['AUDI', 'BMW', 'Opel', 'RAM', 'GMC', 'Jeep'].forEach(function(id) {
          let node = this.series.nodes.find(node => node.id === id);
          if (node) {
            total_xy += node.xy;
            total_mn += node.mn;
          }
        }, this);
        return this.point.name + '<br>Ist: ' + Highcharts.numberFormat(total_xy/1000000, 2, ',', '.') + ' Mio.<br>Δ: ' + Highcharts.numberFormat(total_mn/1000000, 2, ',', '.') + ' Mio.';
      } else {
        return this.point.name;
      }
    }"
)


hc <- highchart() %>%
  
  hc_chart(inverted = TRUE,
           backgroundColor = "#343A40"
  ) %>%
  
  ## The plotOptions is a wrapper object for the configuration of objects for each series type
  hc_plotOptions(organization = list(
    linkColor = "#f8f9fa",
    nodeWidth = 70,
    height = 70
  )) %>%
  
  hc_add_series(data = dt,
                type = "organization",
                colorByPoint = FALSE,
                color = list(
                  linearGradient = list(x1 = 0, y1 = 0, x2 = 1, y2 = 0),
                  stops = list(
                    c(0, "#6F201A"),
                    c(1, "#FFC3B3"))),
                dataLabels = list(
                  enabled = TRUE,
                  useHTML = TRUE,
                  style = list(
                    color = "#f8f9fa",
                    fontSize = "12px",
                    fontWeight = "bold",
                    textOutline = FALSE
                  ),
                  # crop = FALSE,
                  # allowOverlap = TRUE,
                  nodeFormatter = Datalabel
                ),
                
                nodes = list(
                  list(id = "AUDI", xy = XY[1], mn = MN[1]), 
                  list(id = "RAM", xy = XY[2], mn = MN[2]),
                  list(id = "BMW", xy = XY[3], mn = MN[3]),
                  list(id = "GMC", xy = XY[4], mn = MN[4]),
                  list(id = "Opel", xy = XY[5], mn = MN[5]),
                  list(id = "Jeep", xy = XY[6], mn = MN[6]),
                  list(id = "CAR"),
                  list(id = "German"),
                  list(id = "America")
                )
                
  ) %>%
  
  # Tooltip enables the hovering effect to take place
  hc_tooltip(
    enabled = TRUE,
    useHTML = TRUE,
    className = NULL,
    formatter = Tooltip
  )

  # Save the widget as an HTML file
  saveWidget(hc, "plot.html", selfcontained = FALSE)

  # Use webshot to convert it to an image
  webshot2::webshot("plot.html", "plot.png", delay = 5)
```

![](AutoStruct_Dynamics_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->
