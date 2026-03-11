# Open a basic template suitable for use with btable

Open a basic template suitable for use with btable

## Usage

``` r
use_btabletemplate(name, fmt = c("Rmd", "Rnw"), ..., open = TRUE)
```

## Arguments

- name:

  name to save the file under

- fmt:

  character defining format (`Rmd` or `Rnw` are accepted)

- ...:

  other options passed to
  [`use_template`](https://usethis.r-lib.org/reference/use_template.html)

- open:

  logical, whether to open the file

## Value

(by default) saves and opens a script of the chosen format

## Examples

``` r
if (FALSE) { # \dontrun{
# Rmd file
use_btabletemplate("foo")
# Rnw file
use_btabletemplate("foo", fmt = "Rnw")
} # }
```
