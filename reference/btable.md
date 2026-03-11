# btable

btable is a wrapper for xtable and produces tables in latex format.

## Usage

``` r
btable(
  dat,
  nhead,
  nfoot,
  caption,
  label = NULL,
  alignp = NA,
  aligntot = NA,
  alignh1 = "l",
  nnewline = 0,
  indent = 1,
  hlines = NA,
  fonts1 = 8,
  fonts2 = 12,
  rulelength = NULL,
  head_it = c(2),
  head_bf = NA,
  foot_it = NULL,
  foot_bf = NA,
  tab.env = "long",
  table.placement = "ht",
  middle_sep = NA,
  aggregate = TRUE,
  rephead = TRUE,
  mergerow = NA,
  sfile = "",
  print = TRUE,
  comment = FALSE,
  include.colnames = FALSE,
  ...
)
```

## Arguments

- dat:

  dataframe

- nhead:

  number of header rows

- nfoot:

  number of footer rows

- caption:

  caption of table

- label:

  label of table for referncing in latex

- alignp:

  optional width of first column, to be entered with unit, e.g. "2cm"

- aligntot:

  alignment of all columns, as string using latex syntax, e.g. "lccc"

- alignh1:

  alignment of header of the first column (all other headers are
  centered)

- nnewline:

  if given, a line break will be introduced for the first column before
  nnewline letters at a space (if possible)

- indent:

  indent of line break

- hlines:

  additional horizontal lines after specified rows

- fonts1:

  font size of text, 8 by default

- fonts2:

  font size of row, 12 by default

- rulelength:

  optional width of footer

- head_it:

  number of the header rows to be shown in italic, NA indicates none

- head_bf:

  number of the header rows to be shown in bold, NA indicates none

- foot_it:

  number of the footer rows to be shown in italic, NA indicates none

- foot_bf:

  number of the footer rows to be shown in bold, NA indicates none

- tab.env:

  tabular environment, "long" or "float", use float to suppress breaking
  across pages

- table.placement:

  table placement if tab.env==float, contain only elements of
  "h","t","b","p","!","H", default value is "ht".

- middle_sep:

  empty_column in table

- aggregate:

  aggregation of header names TRUE/FALSE

- rephead:

  repeating header after page break

- mergerow:

  merge indicated row, show only first entry

- sfile:

  sanitizing file for latex, dataframe with two columns, pattern and
  replacement

- print:

  logical, indicates whether table should be printed, TRUE by default

- comment:

  logical, indicates whether xtable should print it's comment, FALSE by
  default

- include.colnames:

  logical, indicated whether the columns names are printed, FALSE by
  default.

- ...:

  further arguments passed to print.xtable()

## Value

table in latex format

## Details

Required arguments are a data.frame with the table (dat), the number of
header and footer lines (nhead, nfoot) and a caption for the table.

## Examples

``` r
df<-data.frame(name=c("","Row 1","Row2"),out_t=c("Total","t1","t1"),
    out_1=c("Group 1","g11","g12"),out_2=c("Group 2","g21","g22"))
btable(df,nhead=1,nfoot=0,caption="Table1")
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
btable(df,nhead=1,nfoot=0,caption="Table1",aligntot="llll")
#> Warning: The header rows to not respect aligntot if aggregate==TRUE (the default)---use aggregate=FALSE to use aligntot for the headers.
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{longtable}{llll}
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

#two header lines
df<-data.frame(name=c("","","Row 1","Row2"),out_t=c("Total","mean (sd)","t1","t1"),
    out_1=c("Group 1","mean (sd)","g11","g12"),out_2=c("Group 2","mean (sd)","g21","g22"))
btable(df,nhead=2,nfoot=0,caption="Table1")
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{longtable}{lccc}
#> \caption{Table1} \\ 
#>   \toprule
#>  \multicolumn{1}{l}{} & \multicolumn{1}{c}{Total} & \multicolumn{1}{c}{Group 1} & \multicolumn{1}{c}{Group 2} \\ 
#>   \multicolumn{1}{l}{\textit{}} & \multicolumn{3}{c}{\textit{mean (sd)}}   \\ 
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
btable(df,nhead=2,nfoot=0,caption="Table1",head_it=NA)
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{longtable}{lccc}
#> \caption{Table1} \\ 
#>   \toprule
#>  \multicolumn{1}{l}{} & \multicolumn{1}{c}{Total} & \multicolumn{1}{c}{Group 1} & \multicolumn{1}{c}{Group 2} \\ 
#>   \multicolumn{1}{l}{} & \multicolumn{3}{c}{mean (sd)}   \\ 
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
btable(df,nhead=2,nfoot=0,caption="Table1",head_it=NA,aggregate=FALSE)
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{longtable}{lccc}
#> \caption{Table1} \\ 
#>   \toprule
#>   & Total & Group 1 & Group 2 \\ 
#>    & mean (sd) & mean (sd) & mean (sd) \\ 
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

#footer
df<-data.frame(name=c("","Row 1","Row2","*Footer"),out_t=c("Total","t1","t1",""),
    out_1=c("Group 1","g11","g12",""),out_2=c("Group 2","g21","g22",""))
btable(df,nhead=1,nfoot=1,caption="Table1")
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
#>    \specialrule{1pt}{1pt}{1pt} \multicolumn{4}{l}{\textit{*Footer}} \\\end{longtable}
#> \endgroup

#floating table, no page break within table
df<-data.frame(name=c("","Row 1","Row2"),out_t=c("Total","t1","t1"),
    out_1=c("Group 1","g11","g12"),out_2=c("Group 2","g21","g22"))
btable(df,nhead=1,nfoot=1,caption="Table1",tab.env="float",table.placement="H")
#> \begin{table}[H]
#> \centering
#> \caption{Table1} 
#> \begingroup\fontsize{8pt}{12pt}\selectfont
#> \begin{tabular}{lccc}
#>   \toprule
#>  \multicolumn{1}{l}{} & \multicolumn{1}{c}{Total} & \multicolumn{1}{c}{Group 1} & \multicolumn{1}{c}{Group 2} \\ 
#>    \midrule
#> Row 1 & t1 & g11 & g21 \\ 
#>    \specialrule{1pt}{1pt}{1pt} \multicolumn{4}{l}{\textit{Row2}} \\\end{tabular}
#> \endgroup
#> \end{table}

#save table and print later
df<-data.frame(name=c("","Row 1","Row2"),out_t=c("Total","t1","t1"),
    out_1=c("Group 1","g11","g12"),out_2=c("Group 2","g21","g22"))
saved_table<-btable(df,nhead=1,nfoot=1,caption="Table1",print=FALSE)
cat(saved_table)
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
#>    \specialrule{1pt}{1pt}{1pt} \multicolumn{4}{l}{\textit{Row2}} \\\end{longtable}
#> \endgroup
```
