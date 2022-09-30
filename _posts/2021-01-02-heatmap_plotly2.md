---
layout: post
title: "Heatmap using R Plotly (Colorscale, borders and subplot)"
author: "Zikai Lin"
date: "1/2/2021"
classes: wide
categories:
  - blog
tags:
  - R
  - Plotly
  - heatmap
  - visualization
---



## Basics

In **plotly**, the heatmap can be plotted by the **plot_ly** function. You can specify the type of plot as **heatmap**.

```r
library(plotly)
fig <- plot_ly(z = volcano, type = "heatmap")

fig
```

![Basic heatmap in plotly](/ziklin/assets/images/2020-01-02-heatmap/fig1.png)

Now plotly creates a beautiful interactive heatmap visualization for you. However, this is just a simple example without further customization. Sometimes, you might need to specify optional arguments to make your heatmap visualization cleaner and more publishable.

## Colors
First let's start with the color scale. The default color scale in plotly is the **Viridis** style. But you can either specify a color scheme using the name listed in <https://colorbrewer2.org>, or a customized colorscale in R. Here are some available color schemes that you can directly use in plotly:

### Continuous color scale

Multi-hue colorscale:

- Blue-Green colorscale (**BuGn**)
- Blue-Purple colorscale (**BuPu**)
- Green-Blue colorscale (**GnBu**)
- Orange-Red colorscale (**OrRd**)
- Purple-Blue colorscale (**PuBu**)
- Purple-Blue-Green colorscale (**PuBuGn**)
- Purple-Red colorscale (**PuRd**)
- Red-Purple colorscale (**RdPu**)
- Yellow-Green colorscale (**YlGn**)
- Yellow-Green-Blue colorscale (**YlGnBu**)
- Yellow-Orange-Bright colorscale (**YlOrBr**)
- Yellow-Orange-Red colorscale (**YlOrRd**)

Single hue colorscale:

- Blues (**Blues**)
- Greens (**Greens**)
- Greys (**Greys**)
- Oranges (**Oranges**)
- Purples (**Purples**)
- Reds (**Reds**)

***Example*** - Blues

```r
library(plotly)
fig <- plot_ly(z = volcano, type = "heatmap", colors = "Blues")
fig
```

![Example - Continuous colorscale](/ziklin/assets/images/2020-01-02-heatmap/fig2.png)



### Diverging colorscale

Diverging colorscales are often useful when you want to visualize the "sign" in your dataset, e.g. negative-positive. Some existing diverging colorscales available in plotly are as follow:

- Brown-Bright-Green (**BrBG**)
- Pink-Yellow-Green (**PiYG**)
- Purple-Green (**PRGn**)
- Purple-Orange (**PuOr**)
- Red-Blue (**RdBu**)
- Red-Grey (**RdGy**)
- Red-Yellow-Blue (**RdYlBu**)
- Red-Yellow-Green (**RdYlGn**)
- Spectral (**Spectral**)

***Example*** - the red-blue color scale to display your heatmap. But a reverse scale, which is Blue-Red colorscheme are more often used, so you might want to specify **reversescale = TRUE**

```r
library(plotly)
fig <- plot_ly(z = volcano, type = "heatmap",
               colors = "RdBu", reversescale =T)
fig
```

![Example - Red-blue colorscale](/ziklin/assets/images/2020-01-02-heatmap/fig3.png)



### Qualitative colorscale

Qualitative is useful when you want to disply categorical data. The available qualitative colorscales in plotly are:

- Accent
- Dark2
- Paired
- Pastel1
- Pastel2
- Set1
- Set2
- Set3

For more details, please take a look at <https://colorbrewer2.org/#type=qualitative&scheme=Set1&n=3>.


## Scale

Sometimes users might found themselves in such pain when they try to adjust the range of colorscale in plotly, because it is not well-documented on the official website. For instance, in the volcano dataset, the temperature is usually considered to be greater than 0F. Therefore, it will be misleading if we plot it in blue color when temperature is greater than 0. 

Fortunately, it is possible to adjust the range of your colorscale by specifying two arguments in plot_ly function.

- **zauto**: if you specify this option to FALSE, then plotly won't automatically adjust the colorscale in your heatmap.
- **zmax**: the upper bound of your colorscale.
- **zmim**: the lower bound of your colorscale.


```r
# Expanding the range of the colorscale
fig <- plot_ly(z = volcano, type = "heatmap",
               colors = "RdBu", reversescale =T,
               zauto = FALSE, zmax = 200, zmin = 0)
fig
```

![Example - Customize colorscale range](/ziklin/assets/images/2020-01-02-heatmap/fig4.png)



## Borders and axis

Sometimes, it will be useful to add a border to your heatmap, especially when the boundary is not clear. A way to do it is to configure and customize the axis. Here's an example of how to add borders to your heatmap:


```r
ax <- list(
  zeroline = TRUE,
  showline = TRUE,
  mirror = "ticks",
  gridcolor = toRGB("gray50"),
  gridwidth = 2,
  zerolinecolor = toRGB("red"),
  zerolinewidth = 4,
  linecolor = toRGB("black"),
  linewidth = 6,
  titlefont=list(
  family = "Roman",
  size = 25
  )
)

ay <- list(
  zeroline = TRUE,
  showline = TRUE,
  mirror = "ticks",
  gridcolor = toRGB("gray50"),
  gridwidth = 2,
  zerolinecolor = toRGB("red"),
  zerolinewidth = 4,
  linecolor = toRGB("black"),
  linewidth = 6
)

fig <- plot_ly(z = volcano, type = "heatmap",
               colors = "RdBu", reversescale =T,
               zauto = FALSE, zmax = 200, zmin = 0) %>%
  layout(xaxis = ax, yaxis = ay)
fig
```

![Add border to your heatmaps](/ziklin/assets/images/2020-01-02-heatmap/fig5.png)



## Subplot

**subplot()** is a very handy function to gather plotly objects. 

```r
fig_rb <- plot_ly(z = volcano, type = "heatmap",
                  colors = "RdBu", reversescale =T,
                  zauto = FALSE, zmax = 200, zmin = 0)
fig_gry <- plot_ly(z = volcano, type = "heatmap",
                   colors = "Greys", reversescale =T,
                   zauto = FALSE, zmax = 200, zmin = 0)
fig_grn <- plot_ly(z = volcano, type = "heatmap",
                   colors = "Greens", reversescale =T,
                   zauto = FALSE, zmax = 200, zmin = 0)
subplot(fig_rb, fig_gry, fig_grn)
```

![Subplot in plotly](/ziklin/assets/images/2020-01-02-heatmap/fig6.png)

