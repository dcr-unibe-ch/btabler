# Using \`btabler\`

``` r
library(btabler)
#> Loading required package: xtable
```

`btabler` is a wrapper for the `xtable` package which adds some new
functionality for merging headers, adding footers etc.

To demonstrate how `btabler`

``` r
df <- data.frame(name = c("", "Row 1", "Row2"),
                 out_t = c("Total", "t1", "t1"),
                 out_1 = c("Group 1", "g11", "g12"), 
                 out_2 = c("Group 2", "g21", "g22"))
```

``` r
btable(df, nhead = 1, nfoot = 0, caption = "Table1")
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{longtable}{lccc}
#> \caption{Table1} \\ 
#>   \toprule
#>  \multicolumn{1}{l}{} & \multicolumn{1}{c}{Total} & \multicolumn{1}{c}{Group 1} & \multicolumn{1}{c}{Group 2} \\ 
#>    \hline 
#>  \endhead 
#>  \hline 
#> \multicolumn{4}{l}{\textit{continued on next page}} 
#>  \endfoot 
#>  \endlastfoot 
#> Row 1 & t1 & g11 & g21 \\ 
#>   Row2 & t1 & g12 & g22 \\ 
#>    \bottomrule
#> \end{longtable}
#> \endgroup
```

In the compiled PDF, this looks substantially better of course…

![](fig/basic.png)

## Templates

`btabler` requires that a few specific LaTeX packages are included in
the header of your `Rmd` or `Rnw`/\`tex’ file:

    # .tex
    \usepackage{longtable}
    \usepackage{booktabs}
    \usepackage{float}
    \usepackage{array}

    # .Rmd
    header-includes:
      - \usepackage{longtable}
      - \usepackage{booktabs}
      - \usepackage{float}
      - \usepackage{array}

For convenience, `btabler` provides templates for each which can be
accessed via `use_btabletemplate`:

``` r
use_btabletemplate("report")             # creates report.Rmd in the working directory
use_btabletemplate("report", "Rnw")      # creates report.Rnw in the working directory
use_btabletemplate("code/report", "Rnw") # creates report.Rnw in the code directory
```

## Headers and footers

Where there are multiple header lines, the `nhead` argument can be used
and any neighboring cells in those first rows will be merged.

``` r
df <- data.frame(name = c("", "", "Row 1", "Row2"),
                 out_t = c("Total", "mean (sd)", "t1", "t1"),
                 out_1 = c("Group 1", "mean (sd)", "g11", "g12"),
                 out_2 = c("Group 2", "mean (sd)", "g21", "g22"))
btable(df, nhead = 2, nfoot = 0, caption = "Table1")
```

![](fig/header.png)

`btable` italicizes the second row of the header by default. This can be
changed via the `head_it` argument:

``` r
btable(df, nhead = 2, nfoot = 0, caption = "Table1", 
       head_it = NA)
```

![](fig/head_it.png)

Likewise, aggregation of the header can also be turned of

``` r
btable(df, nhead = 2, nfoot = 0, caption = "Table1", 
       head_it = NA, aggregate = FALSE)
```

![](fig/aggregate.png)

Footers included in the dataframe can also be added:

``` r
df <- data.frame(name = c("", "Row 1", "Row2", "*Footer"),
                 out_t = c("Total", "t1", "t1", ""),
                 out_1 = c("Group 1", "g11", "g12", ""),
                 out_2 = c("Group 2", "g21", "g22", ""))
btable(df, nhead=1, nfoot=1, caption="Table1", 
       rulelength = "6cm")
```

![](fig/footer.png)

## Alignment

Alignment can be changed via the `aligntot` argument. For example, we
could specify that the first column be left aligned and all other
columns should be centered aligned:

``` r
btable(df, nhead = 1, nfoot = 0, caption = "Table1", aligntot = "lccc")
```

![](fig/align.png)

### Custom column types

It’s possible to create new column types in LaTeX and use them in
`btabler`.

The following creates a new column type if put in the LaTeX or Rmd
header

    # .tex
    \newcolumntype{P}[1]{>{\centering\arraybackslash}p{#1}}

    # .Rmd
    header-includes:
      ... # other requirements
      - \newcolumntype{P}[1]{>{\centering\arraybackslash}p{#1}}

This can then be used in btable in the `aligntot` argument (note that
`xtable` warns about non-standard, adding `warning = FALSE` to the chunk
header might be useful…)

``` r
btable(df, nhead = 1, nfoot = 0, 
       caption = "Table1", 
       aligntot = "P{3cm}P{1.5cm}P{1.5cm}P{1.5cm}")
```

![](fig/customcols.png)
