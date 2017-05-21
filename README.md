<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Build Status](https://travis-ci.org/osmdatar/osmdata.svg?branch=master)](https://travis-ci.org/osmdatar/osmdata) [![Build status](https://ci.appveyor.com/api/projects/status/github/osmdatar/osmdata?svg=true)](https://ci.appveyor.com/project/osmdatar/osmdata) [![codecov](https://codecov.io/gh/osmdatar/osmdata/branch/master/graph/badge.svg)](https://codecov.io/gh/osmdatar/osmdata) [![Project Status: WIP](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/osmdata)](http://cran.r-project.org/web/packages/osmdata) [![CRAN Downloads](http://cranlogs.r-pkg.org/badges/grand-total/osmdata?color=orange)](http://cran.r-project.org/package=osmdata)

![](./fig/title.png)

`osmdata` is an R package for accessing OpenStreetMap (OSM) data using the [Overpass API](http://wiki.openstreetmap.org/wiki/Overpass_API). The Overpass API (or OSM3S) is a read-only API that serves up custom selected parts of the OSM map data. Map data can be returned either as [Simple Features (`sf`)](https://cran.r-project.org/package=sf) or [Spatial (`sp`)](https://cran.r-project.org/package=sp) objects.

### Installation

``` r
devtools::install_github("osmdatar/osmdata")
```

### Usage

[Overpass API](http://wiki.openstreetmap.org/wiki/Overpass_API) queries can be built from a base query constructed with `opq` followed by `add_feature`. The corresponding OSM objects are then downloaded and converted to `R Simple Features (sf)` objects with `osmdata_sf()` or to `R Spatial (sp)` objects with `osmdata_sp()`. For example,

``` r
q0 <- opq(bbox = c(-0.27, 51.47, -0.20, 51.50)) # Chiswick Eyot in London, U.K.
q1 <- add_feature(q0, key = 'name', value = "Thames", exact = FALSE)
x <- osmdata_sf(q1)
x
```

    #>  Object of class 'osmdata' with:
    #>                   $bbox : 51.47,-0.27,51.5,-0.2
    #>          $overpass_call : The call submitted to the overpass API
    #>              $timestamp : [ Tue Mar  7 22:17:27 2017 ]
    #>             $osm_points : 'sf' Simple Features Collection with 21305 points
    #>              $osm_lines : 'sf' Simple Features Collection with 1891 linestrings
    #>           $osm_polygons : 'sf' Simple Features Collection with 22 polygons
    #>         $osm_multilines : 'sf' Simple Features Collection with 5 multilinestrings
    #>      $osm_multipolygons : 'sf' Simple Features Collection with 3 multipolygons

OSM data can also be downloaded in OSM XML format with `osmdata_xml()` and saved for use with other software.

``` r
osmdata_xml(q1, "data.xml")
```

The `XML` document is returned silently and may be passed directly to `osmdata_sp()` or `osmdata_sf()`

``` r
doc <- osmdata_xml(q1, "data.xml")
x <- osmdata_sf(q1, doc)
```

Or data can be read from a previously downloaded file:

``` r
x <- osmdata_sf(q1, "data.xml")
```

For more details, see the [website](https://osmdatar.github.io/osmdata/)

### Style guide

We appreciate any contributions; those that comply with our general coding style even more. In four short points:

1.  `<-` not `=`
2.  Indent with four spaces
3.  Be generous with other white spaces - you've got plenty of real estate on that big screen of yours.
4.  Code is much easier to read when braces are vertically aligned, so please put `{` in the same vertical position as `}`.

### Code of Conduct

Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.
