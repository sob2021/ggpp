
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ggpextra <img src="man/figures/logo-ggpextra.png" align="right" width="150" />

[![cran
version](https://www.r-pkg.org/badges/version/ggpextra)](https://cran.r-project.org/package=ggpextra)
[![R build
status](https://github.com/aphalo/ggpextra/workflows/R-CMD-check/badge.svg)](https://github.com/aphalo/ggpextra/actions)

## Purpose

Package ‘**ggpextra**’ (Grammar Extensions to ‘ggplot2’) is a set of
extensions to R package ‘ggplot2’ (&gt;= 3.0.0). New geoms support
insets plots, tables and grobs as insets using a syntax consistent with
the grammar of graphics. The grammar is also extended to support native
plot coordinates (npc) so that annotations can be easily positioned
using new geometries and scales. New position functions facilitate the
labelling of observations by nudging labels away or towards curves or a
focal virtual centre. New variations of `"outward"` and `"inward"`
justification complement the new types of nudge.

## Extended Grammar of graphics

The position of annotations within the plotting area depends in most
cases on graphic design considerations rather than on properties such as
the range of values in the data being plotted. In particular, the
location within the plotting area of large annotation objects like
model-fit summaries, location maps, plots, and tables needs usually to
be set independently of the `x` and `y` scales, re-scaling or any
transformations. To acknowledge this, the Grammar of Graphics is here
expanded by supporting *x* and *y* positions expressed in ‘grid’ “npc”
units in the range 0..1. This is implemented with new
(pseudo-)aesthetics *npcx* and *npcy* and their corresponding scales,
plus geometries and a revised `annotate()` function. The new aesthetics
function in “parallel” with the *x* and *y* aesthetics used for plotting
data. The advantage of this approach is that the syntax used for
annotations becomes identical to that used for plotting data and that
these geoms *cleanly* support facets in a way consistent with the rest
of the grammar.

## Aesthetics and scales

Scales `scale_npcx_continuous()` and `scale_npcy_continuous()` and the
corresponding new aesthetics `npcx` and `npcy` make it possible to add
graphic elements and text to plots using coordinates expressed in `npc`
units for the location within the plotting area.

Scales `scale_x_logFC()` and `scale_y_logFC()` are suitable for plotting
of log fold change data. Scales `scale_x_Pvalue()`, `scale_y_Pvalue()`,
`scale_x_FDR()` and `scale_y_FDR()` are suitable for plotting *p*-values
and adjusted *p*-values or false discovery rate (FDR). Default arguments
are suitable for volcano and quadrant plots as used for transcriptomics,
metabolomics and similar data.

Scales `scale_colour_outcome()`, `scale_fill_outcome()` and
`scale_shape_outcome()` and functions `outome2factor()`,
`threshold2factor()`, `xy_outcomes2factor()` and
`xy_thresholds2factor()` used together make it easy to map ternary
numeric outputs and logical binary outcomes to color, fill and shape
aesthetics. Default arguments are suitable for volcano, quadrant and
other plots as used for genomics, metabolomics and similar data.

## Geometries

Geometries `geom_table()`, `geom_plot()` and `geom_grob()` make it
possible to add inset tables, inset plots, and arbitrary ‘grid’
graphical objects including bitmaps and vector graphics as layers to a
ggplot using native coordinates for `x` and `y`.

Geometries `geom_text_npc()`, `geom_label_npc()`, `geom_table_npc()`,
`geom_plot_npc()` and `geom_grob_npc()`, `geom_text_npc()` and
`geom_label_npc()` are versions of geometries that accept positions on
*x* and *y* axes using aesthetics `npcx` and `npcy` values expressed in
“npc” units.

Geometries `geom_x_margin_arrow()`, `geom_y_margin_arrow()`,
`geom_x_margin_grob()`, `geom_y_margin_grob()`, `geom_x_margin_point()`
and `geom_y_margin_point()` make it possible to add marks along the *x*
and *y* axes. `geom_vhlines()` and `geom_quadrant_lines()` draw vertical
and horizontal reference lines within a single layer.

Geometry `geom_linked_text()` connects text drawn at a nudged position
to the original position, usually that of a point being labelled.

## Statistics

Statistic `stat_fmt_tb()` helps with the formatting of tables to be
plotted with `geom_table()`.

Four statistics, `stat_dens2d_filter()`, `stat_dens2d_label()`,
`stat_dens1d_filter()` and `stat_dens1d_label()`, implement tagging or
selective labelling of observations based on the local 2D density of
observations in a panel. Another two statistics,
`stat_dens1d_filter_g()` and `stat_dens1d_filter_g()` compute the
density by group instead of by plot panel. These six stats are designed
to work well together with `geom_text_repel()` and `geom_label_repel()`
from package ‘ggrepel’.

The statistics `stat_apply_panel()` and `stat_apply_group()` can be
useful for applying arbitrary functions returning numeric vectors. They
are specially useful with functions lime `cumsum()`, `cummax()` and
`diff()`.

## Position functions

New position functions implementing different flavours of nudging are
provided: `position_nudge_keep()`, `position_nudge_to()`,
`position_nudge_center()` and `position_nudge_line()`. These last two
functions make it possible to apply nudging that varies automatically
according to the relative position of points with respect to arbitrary
points or lines, or with respect to a polynomial or smoothing spline
fitted on-the-fly to the the observations. In contrast to
`ggplot2::position_nudge()` all these functions return the repositioned
and original *x* and *y* coordinates.

## History

This package is a “spin-off” from package ‘ggpmisc’ containing
extensions to the grammar originally written for use wihtin ‘ggpmisc’
but which are of general usefulness. As ‘ggpmisc’ has grown in size,
spliting it into two packages seems the best option. Package ‘ggpmisc’
will remain as a “loader” of the packages into which it is being split.

## Examples

``` r
library(ggpextra)
library(ggrepel)
```

A plot with an inset plot.

``` r
p <- ggplot(mtcars, aes(factor(cyl), mpg, colour = factor(cyl))) +
  stat_boxplot() +
  labs(y = NULL) +
  theme_bw(9) + theme(legend.position = "none")

ggplot(mtcars, aes(wt, mpg, colour = factor(cyl))) +
  geom_point() +
  annotate("plot_npc", npcx = "left", npcy = "bottom", label = p) +
  expand_limits(y = 0, x = 0)
```

![](man/figures/README-readme-06-1.png)<!-- -->

## Installation

Installation of the most recent stable version from CRAN:

``` r
install.packages("ggpextra")
```

Installation of the current unstable version from GitHub:

``` r
# install.packages("devtools")
devtools::install_github("aphalo/ggpextra")
```

## Documentation

HTML documentation is available at
(<https://docs.r4photobiology.info/ggpextra/>), including a *User
Guide*.

News about updates are regularly posted at
(<https://www.r4photobiology.info/>).

## Contributing

Please report bugs and request new features at
(<https://github.com/aphalo/ggpextra/issues>). Pull requests are welcome
at (<https://github.com/aphalo/ggpextra>).

## Citation

If you use this package to produce scientific or commercial
publications, please cite according to:

``` r
citation("ggpextra")
```

## License

© 2016-2021 Pedro J. Aphalo (<pedro.aphalo@helsinki.fi>). Released under
the GPL, version 2 or greater. This software carries no warranty of any
kind.
