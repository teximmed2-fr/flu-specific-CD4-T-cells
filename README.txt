Heatmaps were generated with R Studio for Windows 10.

The following information is provided:

Versions of used Software and packages.
Links for download of software versions and packages.
R Scripts for Heatmap generation.
2 Excel files that were used as input data.


RStudio Version 1.2.5033 
link for download:
https://www.npackd.org/p/rstudio/1.2.5033

scource code download here:
https://github.com/rstudio/rstudio/releases/tag/v1.2.5033


R version 3.6.3 (2020-02-29)
link for download:
https://cran.r-project.org/bin/windows/base/old/3.6.3/


Install neccessary packages as listed in the script below.

install package ‘readxl’ version 1.3.1
https://github.com/tidyverse/readxl/releases/tag/v1.3.1

Install package ‘ComplexHeatmap’ version 2.2.0 
https://www.bioconductor.org/packages/release/bioc/html/ComplexHeatmap.html
download link: https://anaconda.org/bioconda/bioconductor-complexheatmap/2.0.0/download/noarch/bioconductor-complexheatmap-2.0.0-r36_1.tar.bz2

The following R code generates heatmaps from data contained in excel files.

R Script for heatmap with clustering and dendrograms from excel files:
library(readxl)
library(ComplexHeatmap)

# path
#enter your path here
#example path
path<-"C:/Users/yourpath/filename.xlsx"

# read excel table and create dataframe
df<-read_excel(path)

#df to matrix
matrix<-scale(df[,-c(1,2,3)])

Heatmap(matrix,
        column_order = NULL,
        right_annotation=rowAnnotation(years=(df$years),
                                       col=list(years=c("unknown"="#6d7678",
                                                        "no vacc"="#ff0d05",
                                                        "1"="#0591ff","2"="#4bfbe3",
                                                        "10"= "#4bfbe3")),
                                       simple_anno_size = unit(2, "mm"), 
                                       donor=anno_text(df$donor,rot = 10, 
                                      gp = gpar(fontsize =8))),
        left_annotation=rowAnnotation(activation=(df$activation),
                                      col=list(activation=c("early"="#07B24F","late"="#000000")), 
                                      simple_anno_size = unit(2, "mm")),
        column_names_gp = gpar(fontsize = 8),
        show_row_names = FALSE,
        show_column_names = TRUE,row_names_gp = gpar(fontsize = 8),
        
        show_row_dend = TRUE,
        show_column_dend = FALSE,
        cluster_rows = TRUE,
        name=" ")