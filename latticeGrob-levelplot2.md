latticeGrob levelplot2
================
Dongdong Kong
2020/5/25

``` r
library(latticeGrob)
```

    ## 
    ## Attaching package: 'latticeGrob'

    ## The following objects are masked from 'package:Ipaper':
    ## 
    ##     check_dir, contain, file_ext, file_name, fprintf, melt_list,
    ##     melt_tree, reorder_name, rm_empty

``` r
load("data_latticeGrob.rda")

stat = list(show = FALSE)
pars = list(title = list(x = -180, y = 90, cex = 1.4))

latticeGrob::init_lattice()
# load_all("../latticeGrob")
stat = list(show = TRUE, name = "u", loc = c(-30, -60), digit = 1, include.sd = TRUE, FUN = matrixStats::weightedMean)

brks <- c(-Inf, 10, 20, 50, 100, 150, 200, 300, 400, 500, 800, 1000, 1500, Inf)
# brks <- {c(2, 5, 10, 20, 50)} %>% c(-Inf, -rev(.), 0, ., Inf)
ncol <- length(brks) - 1
# cols <- rcolors::get_color("amwg256", ncol) %>% rev()

p <- levelplot2(mean ~ s1+s2 | band,
                df,
                grid5,
                colors = cols, brks = brks,
                layout = c(2, 2),
                pars = pars,
                stat = stat, 
                unit = "(mm)", unit.adj = 0.5,
                yticks = seq(0, 0.2, 0.1),
                ylim = c(-72, 99),
                xlim = c(-190, 240),
                aspect = 0.5,
                show_signPerc = FALSE,
                prob_z = 0.98, 
                # unit = "km2", unit.adj = 0.5,
                legend.num2factor = TRUE,
                colorkey = list(width = 1.4, height = 0.96, labels = list(cex = 1)),
                # sp.layout = list(sp_layout), # , sp_poly
                interpolate = FALSE
) + 
    theme_lattice(key.margin = c(0, 1.5, 0, 0),
                  plot.margin = c(0, 3, -1.5, 1))
write_fig(p, "latticeGrob_levelplot2 (2003-2017).svg", 11.4, 5.2)
```

![Image Title](./latticeGrob_levelplot2%20\(2003-2017\).svg)
