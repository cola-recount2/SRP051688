cola Report for recount2:SRP051688
==================

**Date**: 2019-12-26 00:43:09 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 16000    56
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:hclust](#SD-hclust)     |          6| 1.000|           1.000|       1.000|** |2,5        |
|[SD:skmeans](#SD-skmeans)   |          6| 1.000|           0.992|       0.982|** |2,5        |
|[SD:pam](#SD-pam)           |          6| 1.000|           1.000|       1.000|** |2          |
|[SD:mclust](#SD-mclust)     |          6| 1.000|           1.000|       1.000|** |4,5        |
|[CV:hclust](#CV-hclust)     |          6| 1.000|           1.000|       1.000|** |3,4,5      |
|[CV:mclust](#CV-mclust)     |          6| 1.000|           0.998|       0.995|** |2,3,4,5    |
|[MAD:hclust](#MAD-hclust)   |          6| 1.000|           1.000|       1.000|** |5          |
|[MAD:skmeans](#MAD-skmeans) |          6| 1.000|           0.989|       0.975|** |2,5        |
|[MAD:pam](#MAD-pam)         |          6| 1.000|           1.000|       1.000|** |5          |
|[MAD:mclust](#MAD-mclust)   |          6| 1.000|           1.000|       1.000|** |3,4,5      |
|[ATC:hclust](#ATC-hclust)   |          6| 1.000|           0.993|       0.985|** |2,3,4      |
|[ATC:kmeans](#ATC-kmeans)   |          3| 1.000|           0.998|       0.983|** |2          |
|[ATC:pam](#ATC-pam)         |          6| 1.000|           0.999|       0.999|** |2,3,4,5    |
|[ATC:mclust](#ATC-mclust)   |          6| 1.000|           1.000|       1.000|** |4,5        |
|[ATC:NMF](#ATC-NMF)         |          3| 1.000|           0.986|       0.992|** |2          |
|[SD:NMF](#SD-NMF)           |          6| 0.951|           0.856|       0.921|** |4,5        |
|[MAD:NMF](#MAD-NMF)         |          6| 0.948|           0.907|       0.945|*  |2,5        |
|[CV:NMF](#CV-NMF)           |          6| 0.925|           0.839|       0.874|*  |2          |
|[CV:skmeans](#CV-skmeans)   |          6| 0.917|           0.970|       0.941|*  |2,5        |
|[CV:pam](#CV-pam)           |          6| 0.917|           0.975|       0.940|*  |2,4,5      |
|[ATC:skmeans](#ATC-skmeans) |          6| 0.917|           0.979|       0.974|*  |2,3        |
|[MAD:kmeans](#MAD-kmeans)   |          2| 0.584|           0.933|       0.938|   |           |
|[SD:kmeans](#SD-kmeans)     |          4| 0.574|           0.774|       0.768|   |           |
|[CV:kmeans](#CV-kmeans)     |          2| 0.252|           0.862|       0.831|   |           |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 0.537           0.707       0.888          0.386 0.584   0.584
#&gt; CV:NMF      2 0.938           0.969       0.969          0.497 0.501   0.501
#&gt; MAD:NMF     2 1.000           0.979       0.989          0.501 0.501   0.501
#&gt; ATC:NMF     2 1.000           1.000       1.000          0.250 0.751   0.751
#&gt; SD:skmeans  2 1.000           1.000       1.000          0.499 0.501   0.501
#&gt; CV:skmeans  2 1.000           0.997       0.998          0.499 0.501   0.501
#&gt; MAD:skmeans 2 1.000           0.998       0.999          0.499 0.501   0.501
#&gt; ATC:skmeans 2 1.000           1.000       1.000          0.499 0.501   0.501
#&gt; SD:mclust   2 0.751           0.936       0.959          0.479 0.501   0.501
#&gt; CV:mclust   2 1.000           0.984       0.988          0.497 0.501   0.501
#&gt; MAD:mclust  2 0.584           0.939       0.946          0.494 0.501   0.501
#&gt; ATC:mclust  2 0.501           0.804       0.837          0.417 0.584   0.584
#&gt; SD:kmeans   2 0.335           0.900       0.885          0.418 0.501   0.501
#&gt; CV:kmeans   2 0.252           0.862       0.831          0.413 0.501   0.501
#&gt; MAD:kmeans  2 0.584           0.933       0.938          0.456 0.501   0.501
#&gt; ATC:kmeans  2 1.000           1.000       1.000          0.250 0.751   0.751
#&gt; SD:pam      2 1.000           0.989       0.990          0.256 0.751   0.751
#&gt; CV:pam      2 1.000           0.998       0.997          0.496 0.501   0.501
#&gt; MAD:pam     2 0.454           0.757       0.850          0.401 0.501   0.501
#&gt; ATC:pam     2 1.000           1.000       1.000          0.250 0.751   0.751
#&gt; SD:hclust   2 1.000           1.000       1.000          0.250 0.751   0.751
#&gt; CV:hclust   2 0.501           0.959       0.931          0.460 0.501   0.501
#&gt; MAD:hclust  2 0.751           0.924       0.960          0.499 0.501   0.501
#&gt; ATC:hclust  2 1.000           1.000       1.000          0.250 0.751   0.751
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.795           0.921       0.942          0.545 0.731   0.573
#&gt; CV:NMF      3 0.792           0.911       0.885          0.233 0.875   0.751
#&gt; MAD:NMF     3 0.861           0.941       0.965          0.192 0.886   0.778
#&gt; ATC:NMF     3 1.000           0.986       0.992          1.335 0.668   0.557
#&gt; SD:skmeans  3 0.709           0.944       0.903          0.192 0.917   0.834
#&gt; CV:skmeans  3 0.875           0.951       0.959          0.266 0.875   0.751
#&gt; MAD:skmeans 3 0.709           0.809       0.837          0.218 1.000   1.000
#&gt; ATC:skmeans 3 0.917           0.951       0.963          0.166 0.917   0.834
#&gt; SD:mclust   3 0.834           0.924       0.949          0.327 0.668   0.431
#&gt; CV:mclust   3 1.000           0.996       0.997          0.335 0.751   0.541
#&gt; MAD:mclust  3 1.000           1.000       1.000          0.179 0.584   0.377
#&gt; ATC:mclust  3 0.834           0.967       0.981          0.424 0.834   0.716
#&gt; SD:kmeans   3 0.501           0.658       0.758          0.429 0.948   0.896
#&gt; CV:kmeans   3 0.294           0.745       0.721          0.376 1.000   1.000
#&gt; MAD:kmeans  3 0.584           0.780       0.799          0.327 1.000   1.000
#&gt; ATC:kmeans  3 1.000           0.998       0.983          1.267 0.668   0.557
#&gt; SD:pam      3 0.782           0.918       0.960          1.326 0.668   0.557
#&gt; CV:pam      3 0.792           0.910       0.859          0.214 0.875   0.751
#&gt; MAD:pam     3 0.782           0.910       0.958          0.488 0.917   0.834
#&gt; ATC:pam     3 1.000           1.000       1.000          1.328 0.668   0.557
#&gt; SD:hclust   3 0.792           0.869       0.939          1.423 0.626   0.502
#&gt; CV:hclust   3 1.000           0.999       0.998          0.357 0.875   0.751
#&gt; MAD:hclust  3 0.792           0.921       0.960          0.190 0.917   0.834
#&gt; ATC:hclust  3 1.000           1.000       1.000          1.328 0.668   0.557
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.975           0.947       0.978         0.1903 0.881   0.707
#&gt; CV:NMF      4 0.834           0.954       0.930         0.1544 0.917   0.779
#&gt; MAD:NMF     4 0.880           0.916       0.963         0.1928 0.881   0.707
#&gt; ATC:NMF     4 0.794           0.885       0.901         0.1982 0.875   0.702
#&gt; SD:skmeans  4 0.834           0.928       0.889         0.1931 0.875   0.702
#&gt; CV:skmeans  4 0.834           0.923       0.901         0.1234 0.917   0.779
#&gt; MAD:skmeans 4 0.834           0.871       0.822         0.1649 0.792   0.585
#&gt; ATC:skmeans 4 0.834           0.939       0.913         0.1144 0.958   0.901
#&gt; SD:mclust   4 1.000           1.000       1.000         0.1123 0.958   0.876
#&gt; CV:mclust   4 1.000           1.000       1.000         0.0655 0.958   0.876
#&gt; MAD:mclust  4 1.000           1.000       1.000         0.2139 0.875   0.702
#&gt; ATC:mclust  4 1.000           1.000       1.000         0.1909 0.875   0.702
#&gt; SD:kmeans   4 0.574           0.774       0.768         0.1492 0.823   0.616
#&gt; CV:kmeans   4 0.626           0.762       0.710         0.1999 0.792   0.585
#&gt; MAD:kmeans  4 0.532           0.770       0.772         0.1335 0.792   0.585
#&gt; ATC:kmeans  4 0.709           0.802       0.788         0.2328 0.834   0.602
#&gt; SD:pam      4 0.823           0.912       0.957         0.1908 0.875   0.702
#&gt; CV:pam      4 1.000           0.998       0.998         0.1729 0.917   0.779
#&gt; MAD:pam     4 0.849           0.942       0.968         0.1864 0.875   0.702
#&gt; ATC:pam     4 1.000           0.936       0.975         0.2535 0.850   0.641
#&gt; SD:hclust   4 0.834           0.873       0.939         0.1663 0.917   0.779
#&gt; CV:hclust   4 1.000           0.997       0.995         0.1336 0.917   0.779
#&gt; MAD:hclust  4 0.834           0.928       0.960         0.1902 0.875   0.702
#&gt; ATC:hclust  4 1.000           0.985       0.990         0.2190 0.875   0.702
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.978           0.937       0.953         0.1073 0.922   0.730
#&gt; CV:NMF      5 0.878           0.962       0.947         0.1095 0.917   0.717
#&gt; MAD:NMF     5 0.933           0.936       0.957         0.1003 0.902   0.673
#&gt; ATC:NMF     5 0.779           0.918       0.834         0.0753 0.917   0.717
#&gt; SD:skmeans  5 0.917           0.964       0.967         0.1120 0.917   0.717
#&gt; CV:skmeans  5 0.917           0.957       0.953         0.1097 0.917   0.717
#&gt; MAD:skmeans 5 0.958           0.973       0.974         0.1148 0.917   0.717
#&gt; ATC:skmeans 5 0.834           0.915       0.909         0.1578 0.875   0.669
#&gt; SD:mclust   5 1.000           1.000       1.000         0.1175 0.917   0.717
#&gt; CV:mclust   5 1.000           0.994       0.994         0.1175 0.917   0.717
#&gt; MAD:mclust  5 1.000           1.000       1.000         0.1175 0.917   0.717
#&gt; ATC:mclust  5 1.000           0.987       0.989         0.1175 0.917   0.717
#&gt; SD:kmeans   5 0.522           0.692       0.689         0.0804 1.000   1.000
#&gt; CV:kmeans   5 0.522           0.560       0.529         0.0786 0.834   0.504
#&gt; MAD:kmeans  5 0.605           0.759       0.684         0.0900 0.917   0.717
#&gt; ATC:kmeans  5 0.699           0.757       0.747         0.0922 1.000   1.000
#&gt; SD:pam      5 0.892           0.859       0.921         0.1186 0.893   0.647
#&gt; CV:pam      5 1.000           0.991       0.996         0.1168 0.897   0.660
#&gt; MAD:pam     5 0.927           0.904       0.956         0.1203 0.912   0.701
#&gt; ATC:pam     5 1.000           0.973       0.981         0.0947 0.918   0.700
#&gt; SD:hclust   5 0.917           0.907       0.941         0.1175 0.917   0.717
#&gt; CV:hclust   5 1.000           1.000       1.000         0.1175 0.917   0.717
#&gt; MAD:hclust  5 0.917           0.983       0.985         0.1175 0.917   0.717
#&gt; ATC:hclust  5 0.875           0.872       0.905         0.1129 0.917   0.717
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.951           0.856       0.921         0.0588 0.953   0.778
#&gt; CV:NMF      6 0.925           0.839       0.874         0.0625 0.918   0.635
#&gt; MAD:NMF     6 0.948           0.907       0.945         0.0630 0.948   0.756
#&gt; ATC:NMF     6 0.824           0.908       0.855         0.0493 1.000   1.000
#&gt; SD:skmeans  6 1.000           0.992       0.982         0.0532 0.958   0.802
#&gt; CV:skmeans  6 0.917           0.970       0.941         0.0552 0.958   0.802
#&gt; MAD:skmeans 6 1.000           0.989       0.975         0.0531 0.958   0.802
#&gt; ATC:skmeans 6 0.917           0.979       0.974         0.1028 0.917   0.670
#&gt; SD:mclust   6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; CV:mclust   6 1.000           0.998       0.995         0.0522 0.958   0.802
#&gt; MAD:mclust  6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; ATC:mclust  6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; SD:kmeans   6 0.636           0.892       0.734         0.0676 0.875   0.575
#&gt; CV:kmeans   6 0.626           0.680       0.688         0.0683 0.844   0.429
#&gt; MAD:kmeans  6 0.647           0.890       0.700         0.0598 0.958   0.802
#&gt; ATC:kmeans  6 0.768           0.909       0.719         0.0570 0.917   0.670
#&gt; SD:pam      6 1.000           1.000       1.000         0.0483 0.945   0.744
#&gt; CV:pam      6 0.917           0.975       0.940         0.0533 0.949   0.762
#&gt; MAD:pam     6 1.000           1.000       1.000         0.0486 0.954   0.781
#&gt; ATC:pam     6 1.000           0.999       0.999         0.0406 0.948   0.753
#&gt; SD:hclust   6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; CV:hclust   6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; MAD:hclust  6 1.000           1.000       1.000         0.0526 0.958   0.802
#&gt; ATC:hclust  6 1.000           0.993       0.985         0.0525 0.958   0.802
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2501 0.751   0.751
#> 3 3 0.792           0.869       0.939         1.4230 0.626   0.502
#> 4 4 0.834           0.873       0.939         0.1663 0.917   0.779
#> 5 5 0.917           0.907       0.941         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     1       0          1  1  0
#&gt; SRR1740039     1       0          1  1  0
#&gt; SRR1740040     1       0          1  1  0
#&gt; SRR1740041     1       0          1  1  0
#&gt; SRR1740042     1       0          1  1  0
#&gt; SRR1740043     1       0          1  1  0
#&gt; SRR1740044     1       0          1  1  0
#&gt; SRR1740045     1       0          1  1  0
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     1       0          1  1  0
#&gt; SRR1740067     1       0          1  1  0
#&gt; SRR1740068     1       0          1  1  0
#&gt; SRR1740069     1       0          1  1  0
#&gt; SRR1740070     1       0          1  1  0
#&gt; SRR1740071     1       0          1  1  0
#&gt; SRR1740072     1       0          1  1  0
#&gt; SRR1740073     1       0          1  1  0
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1740034     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740035     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740036     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740037     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740038     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740039     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740040     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740041     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740042     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740043     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740044     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740045     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740050     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740051     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740052     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740054     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740053     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740056     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740055     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740057     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740058     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740059     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740060     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740061     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740062     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740063     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740064     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740065     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740066     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740067     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740068     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740069     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740070     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740071     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740072     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740073     2   0.000      0.800 0.000 1.000  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740078     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740079     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740080     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740081     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740082     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740083     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740084     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740085     2   0.621      0.479 0.428 0.572  0
#&gt; SRR1740086     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740087     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740088     1   0.000      1.000 1.000 0.000  0
#&gt; SRR1740089     1   0.000      1.000 1.000 0.000  0
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4
#&gt; SRR1740034     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740035     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740036     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740037     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740038     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740039     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740040     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740041     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740042     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740043     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740044     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740045     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740050     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740051     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740052     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740054     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740053     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740056     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740055     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740057     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740058     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740059     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740060     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740061     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740062     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740063     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740064     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740065     4   0.492      1.000 0.428 0.000  0 0.572
#&gt; SRR1740066     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740067     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740068     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740069     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740070     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740071     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740072     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740073     2   0.492      0.818 0.000 0.572  0 0.428
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1 0.000
#&gt; SRR1740078     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740079     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740080     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740081     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740082     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740083     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740084     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740085     2   0.000      0.479 0.000 1.000  0 0.000
#&gt; SRR1740086     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740087     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740088     1   0.492      1.000 0.572 0.428  0 0.000
#&gt; SRR1740089     1   0.492      1.000 0.572 0.428  0 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5
#&gt; SRR1740034     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740035     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740036     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740037     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740038     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740039     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740040     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740041     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740042     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740043     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740044     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740045     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740046     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740048     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740047     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740049     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740050     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740051     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740052     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740054     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740053     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740056     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740055     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740057     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740058     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740059     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740060     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740061     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740062     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740063     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740064     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740065     4   0.000       1.00 0.000  0  0  1 0.000
#&gt; SRR1740066     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740067     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740068     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740069     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740070     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740071     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740072     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740073     2   0.000       1.00 0.000  1  0  0 0.000
#&gt; SRR1740074     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740075     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740076     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740077     3   0.000       1.00 0.000  0  1  0 0.000
#&gt; SRR1740078     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740079     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740080     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740081     5   0.000       0.73 0.000  0  0  0 1.000
#&gt; SRR1740082     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740083     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740084     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740085     1   0.000       1.00 1.000  0  0  0 0.000
#&gt; SRR1740086     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740087     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740088     5   0.422       0.62 0.416  0  0  0 0.584
#&gt; SRR1740089     5   0.422       0.62 0.416  0  0  0 0.584
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.335           0.900       0.885         0.4182 0.501   0.501
#> 3 3 0.501           0.658       0.758         0.4293 0.948   0.896
#> 4 4 0.574           0.774       0.768         0.1492 0.823   0.616
#> 5 5 0.522           0.692       0.689         0.0804 1.000   1.000
#> 6 6 0.636           0.892       0.734         0.0676 0.875   0.575
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.541      0.883 0.876 0.124
#&gt; SRR1740035     1   0.541      0.883 0.876 0.124
#&gt; SRR1740036     1   0.541      0.883 0.876 0.124
#&gt; SRR1740037     1   0.541      0.883 0.876 0.124
#&gt; SRR1740038     2   0.909      0.880 0.324 0.676
#&gt; SRR1740039     2   0.909      0.880 0.324 0.676
#&gt; SRR1740040     2   0.909      0.880 0.324 0.676
#&gt; SRR1740041     2   0.909      0.880 0.324 0.676
#&gt; SRR1740042     2   0.904      0.882 0.320 0.680
#&gt; SRR1740043     2   0.904      0.882 0.320 0.680
#&gt; SRR1740044     2   0.904      0.882 0.320 0.680
#&gt; SRR1740045     2   0.904      0.882 0.320 0.680
#&gt; SRR1740046     2   0.552      0.799 0.128 0.872
#&gt; SRR1740048     2   0.552      0.799 0.128 0.872
#&gt; SRR1740047     2   0.552      0.799 0.128 0.872
#&gt; SRR1740049     2   0.552      0.799 0.128 0.872
#&gt; SRR1740050     1   0.000      0.954 1.000 0.000
#&gt; SRR1740051     1   0.000      0.954 1.000 0.000
#&gt; SRR1740052     1   0.000      0.954 1.000 0.000
#&gt; SRR1740054     1   0.118      0.949 0.984 0.016
#&gt; SRR1740053     1   0.000      0.954 1.000 0.000
#&gt; SRR1740056     1   0.118      0.949 0.984 0.016
#&gt; SRR1740055     1   0.118      0.949 0.984 0.016
#&gt; SRR1740057     1   0.118      0.949 0.984 0.016
#&gt; SRR1740058     1   0.000      0.954 1.000 0.000
#&gt; SRR1740059     1   0.000      0.954 1.000 0.000
#&gt; SRR1740060     1   0.000      0.954 1.000 0.000
#&gt; SRR1740061     1   0.000      0.954 1.000 0.000
#&gt; SRR1740062     1   0.541      0.883 0.876 0.124
#&gt; SRR1740063     1   0.541      0.883 0.876 0.124
#&gt; SRR1740064     1   0.541      0.883 0.876 0.124
#&gt; SRR1740065     1   0.541      0.883 0.876 0.124
#&gt; SRR1740066     2   0.909      0.880 0.324 0.676
#&gt; SRR1740067     2   0.909      0.880 0.324 0.676
#&gt; SRR1740068     2   0.909      0.880 0.324 0.676
#&gt; SRR1740069     2   0.909      0.880 0.324 0.676
#&gt; SRR1740070     2   0.904      0.882 0.320 0.680
#&gt; SRR1740071     2   0.904      0.882 0.320 0.680
#&gt; SRR1740072     2   0.904      0.882 0.320 0.680
#&gt; SRR1740073     2   0.904      0.882 0.320 0.680
#&gt; SRR1740074     2   0.552      0.799 0.128 0.872
#&gt; SRR1740075     2   0.552      0.799 0.128 0.872
#&gt; SRR1740076     2   0.552      0.799 0.128 0.872
#&gt; SRR1740077     2   0.552      0.799 0.128 0.872
#&gt; SRR1740078     1   0.000      0.954 1.000 0.000
#&gt; SRR1740079     1   0.000      0.954 1.000 0.000
#&gt; SRR1740080     1   0.000      0.954 1.000 0.000
#&gt; SRR1740081     1   0.000      0.954 1.000 0.000
#&gt; SRR1740082     1   0.118      0.949 0.984 0.016
#&gt; SRR1740083     1   0.118      0.949 0.984 0.016
#&gt; SRR1740084     1   0.118      0.949 0.984 0.016
#&gt; SRR1740085     1   0.118      0.949 0.984 0.016
#&gt; SRR1740086     1   0.000      0.954 1.000 0.000
#&gt; SRR1740087     1   0.000      0.954 1.000 0.000
#&gt; SRR1740088     1   0.000      0.954 1.000 0.000
#&gt; SRR1740089     1   0.000      0.954 1.000 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1   0.245      0.665 0.924 0.076 0.000
#&gt; SRR1740035     1   0.245      0.665 0.924 0.076 0.000
#&gt; SRR1740036     1   0.245      0.665 0.924 0.076 0.000
#&gt; SRR1740037     1   0.245      0.665 0.924 0.076 0.000
#&gt; SRR1740038     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740039     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740040     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740041     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740042     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740043     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740044     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740045     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740046     2   0.631     -0.954 0.000 0.508 0.492
#&gt; SRR1740048     2   0.631     -0.954 0.000 0.508 0.492
#&gt; SRR1740047     2   0.631     -0.954 0.000 0.508 0.492
#&gt; SRR1740049     2   0.631     -0.954 0.000 0.508 0.492
#&gt; SRR1740050     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740051     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740052     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740054     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740053     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740056     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740055     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740057     1   0.880      0.761 0.564 0.152 0.284
#&gt; SRR1740058     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740059     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740060     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740061     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740062     1   0.268      0.665 0.920 0.076 0.004
#&gt; SRR1740063     1   0.268      0.665 0.920 0.076 0.004
#&gt; SRR1740064     1   0.268      0.665 0.920 0.076 0.004
#&gt; SRR1740065     1   0.268      0.665 0.920 0.076 0.004
#&gt; SRR1740066     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740067     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740068     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740069     2   0.175      0.779 0.048 0.952 0.000
#&gt; SRR1740070     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740071     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740072     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740073     2   0.141      0.779 0.036 0.964 0.000
#&gt; SRR1740074     3   0.630      1.000 0.000 0.472 0.528
#&gt; SRR1740075     3   0.630      1.000 0.000 0.472 0.528
#&gt; SRR1740076     3   0.630      1.000 0.000 0.472 0.528
#&gt; SRR1740077     3   0.630      1.000 0.000 0.472 0.528
#&gt; SRR1740078     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740079     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740080     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740081     1   0.713      0.791 0.544 0.024 0.432
#&gt; SRR1740082     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740083     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740084     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740085     1   0.885      0.759 0.560 0.156 0.284
#&gt; SRR1740086     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740087     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740088     1   0.670      0.810 0.648 0.024 0.328
#&gt; SRR1740089     1   0.670      0.810 0.648 0.024 0.328
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4  0.6049      0.974 0.200 0.044 0.044 0.712
#&gt; SRR1740035     4  0.6049      0.974 0.200 0.044 0.044 0.712
#&gt; SRR1740036     4  0.6049      0.974 0.200 0.044 0.044 0.712
#&gt; SRR1740037     4  0.6049      0.974 0.200 0.044 0.044 0.712
#&gt; SRR1740038     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740039     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740040     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740041     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740042     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740043     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740044     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740045     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740046     3  0.4699      0.949 0.000 0.320 0.676 0.004
#&gt; SRR1740048     3  0.4699      0.949 0.000 0.320 0.676 0.004
#&gt; SRR1740047     3  0.4699      0.949 0.000 0.320 0.676 0.004
#&gt; SRR1740049     3  0.4699      0.949 0.000 0.320 0.676 0.004
#&gt; SRR1740050     1  0.0188      0.573 0.996 0.004 0.000 0.000
#&gt; SRR1740051     1  0.0188      0.573 0.996 0.004 0.000 0.000
#&gt; SRR1740052     1  0.0188      0.573 0.996 0.004 0.000 0.000
#&gt; SRR1740054     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740053     1  0.0188      0.573 0.996 0.004 0.000 0.000
#&gt; SRR1740056     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740055     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740057     1  0.9326      0.484 0.444 0.164 0.172 0.220
#&gt; SRR1740058     1  0.6972      0.539 0.600 0.004 0.172 0.224
#&gt; SRR1740059     1  0.6972      0.539 0.600 0.004 0.172 0.224
#&gt; SRR1740060     1  0.6972      0.539 0.600 0.004 0.172 0.224
#&gt; SRR1740061     1  0.6972      0.539 0.600 0.004 0.172 0.224
#&gt; SRR1740062     4  0.4800      0.974 0.196 0.044 0.000 0.760
#&gt; SRR1740063     4  0.4800      0.974 0.196 0.044 0.000 0.760
#&gt; SRR1740064     4  0.4800      0.974 0.196 0.044 0.000 0.760
#&gt; SRR1740065     4  0.4800      0.974 0.196 0.044 0.000 0.760
#&gt; SRR1740066     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740067     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740068     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740069     2  0.0592      0.948 0.016 0.984 0.000 0.000
#&gt; SRR1740070     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740071     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740072     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740073     2  0.2522      0.948 0.016 0.908 0.000 0.076
#&gt; SRR1740074     3  0.6478      0.949 0.000 0.336 0.576 0.088
#&gt; SRR1740075     3  0.6478      0.949 0.000 0.336 0.576 0.088
#&gt; SRR1740076     3  0.6516      0.949 0.000 0.332 0.576 0.092
#&gt; SRR1740077     3  0.6516      0.949 0.000 0.332 0.576 0.092
#&gt; SRR1740078     1  0.0895      0.573 0.976 0.004 0.020 0.000
#&gt; SRR1740079     1  0.0895      0.573 0.976 0.004 0.020 0.000
#&gt; SRR1740080     1  0.0895      0.573 0.976 0.004 0.020 0.000
#&gt; SRR1740081     1  0.0895      0.573 0.976 0.004 0.020 0.000
#&gt; SRR1740082     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740083     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740084     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740085     1  0.9354      0.484 0.440 0.168 0.172 0.220
#&gt; SRR1740086     1  0.6963      0.539 0.600 0.004 0.168 0.228
#&gt; SRR1740087     1  0.6963      0.539 0.600 0.004 0.168 0.228
#&gt; SRR1740088     1  0.6963      0.539 0.600 0.004 0.168 0.228
#&gt; SRR1740089     1  0.6963      0.539 0.600 0.004 0.168 0.228
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.5574      0.922 0.076 0.028 0.064 0.748 0.084
#&gt; SRR1740035     4  0.5574      0.922 0.076 0.028 0.064 0.748 0.084
#&gt; SRR1740036     4  0.5574      0.922 0.076 0.028 0.064 0.748 0.084
#&gt; SRR1740037     4  0.5574      0.922 0.076 0.028 0.064 0.748 0.084
#&gt; SRR1740038     2  0.3890      0.836 0.012 0.736 0.000 0.000 0.252
#&gt; SRR1740039     2  0.3890      0.836 0.012 0.736 0.000 0.000 0.252
#&gt; SRR1740040     2  0.3890      0.836 0.012 0.736 0.000 0.000 0.252
#&gt; SRR1740041     2  0.3890      0.836 0.012 0.736 0.000 0.000 0.252
#&gt; SRR1740042     2  0.0000      0.836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740043     2  0.0000      0.836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740044     2  0.0000      0.836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740045     2  0.0000      0.836 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740046     3  0.6039      0.923 0.000 0.192 0.660 0.056 0.092
#&gt; SRR1740048     3  0.6026      0.923 0.000 0.192 0.660 0.052 0.096
#&gt; SRR1740047     3  0.6026      0.923 0.000 0.192 0.660 0.052 0.096
#&gt; SRR1740049     3  0.6039      0.923 0.000 0.192 0.660 0.056 0.092
#&gt; SRR1740050     1  0.5900      0.483 0.468 0.008 0.000 0.076 0.448
#&gt; SRR1740051     1  0.5855      0.483 0.468 0.008 0.000 0.072 0.452
#&gt; SRR1740052     1  0.5855      0.483 0.468 0.008 0.000 0.072 0.452
#&gt; SRR1740054     1  0.8700      0.390 0.484 0.160 0.104 0.112 0.140
#&gt; SRR1740053     1  0.5900      0.483 0.468 0.008 0.000 0.076 0.448
#&gt; SRR1740056     1  0.8700      0.390 0.484 0.160 0.104 0.112 0.140
#&gt; SRR1740055     1  0.8700      0.390 0.484 0.160 0.104 0.112 0.140
#&gt; SRR1740057     1  0.8700      0.390 0.484 0.160 0.104 0.112 0.140
#&gt; SRR1740058     1  0.3203      0.459 0.820 0.012 0.000 0.168 0.000
#&gt; SRR1740059     1  0.3203      0.459 0.820 0.012 0.000 0.168 0.000
#&gt; SRR1740060     1  0.3203      0.459 0.820 0.012 0.000 0.168 0.000
#&gt; SRR1740061     1  0.3203      0.459 0.820 0.012 0.000 0.168 0.000
#&gt; SRR1740062     4  0.2548      0.921 0.072 0.028 0.004 0.896 0.000
#&gt; SRR1740063     4  0.2548      0.921 0.072 0.028 0.004 0.896 0.000
#&gt; SRR1740064     4  0.2548      0.921 0.072 0.028 0.000 0.896 0.004
#&gt; SRR1740065     4  0.2548      0.921 0.072 0.028 0.000 0.896 0.004
#&gt; SRR1740066     2  0.4044      0.836 0.012 0.732 0.000 0.004 0.252
#&gt; SRR1740067     2  0.4044      0.836 0.012 0.732 0.000 0.004 0.252
#&gt; SRR1740068     2  0.4044      0.836 0.012 0.732 0.000 0.004 0.252
#&gt; SRR1740069     2  0.4044      0.836 0.012 0.732 0.000 0.004 0.252
#&gt; SRR1740070     2  0.0324      0.836 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740071     2  0.0324      0.836 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740072     2  0.0324      0.836 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740073     2  0.0324      0.836 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740074     3  0.3866      0.918 0.004 0.192 0.780 0.024 0.000
#&gt; SRR1740075     3  0.3866      0.918 0.004 0.192 0.780 0.024 0.000
#&gt; SRR1740076     3  0.3710      0.918 0.000 0.192 0.784 0.000 0.024
#&gt; SRR1740077     3  0.3710      0.918 0.000 0.192 0.784 0.000 0.024
#&gt; SRR1740078     1  0.6085      0.483 0.468 0.008 0.004 0.080 0.440
#&gt; SRR1740079     1  0.6085      0.483 0.468 0.008 0.004 0.080 0.440
#&gt; SRR1740080     1  0.6042      0.483 0.468 0.008 0.004 0.076 0.444
#&gt; SRR1740081     1  0.6042      0.483 0.468 0.008 0.004 0.076 0.444
#&gt; SRR1740082     1  0.8662      0.390 0.484 0.160 0.092 0.108 0.156
#&gt; SRR1740083     1  0.8662      0.390 0.484 0.160 0.092 0.108 0.156
#&gt; SRR1740084     1  0.8662      0.390 0.484 0.160 0.092 0.108 0.156
#&gt; SRR1740085     1  0.8662      0.390 0.484 0.160 0.092 0.108 0.156
#&gt; SRR1740086     1  0.3693      0.459 0.804 0.012 0.016 0.168 0.000
#&gt; SRR1740087     1  0.3693      0.459 0.804 0.012 0.016 0.168 0.000
#&gt; SRR1740088     1  0.3693      0.459 0.804 0.012 0.016 0.168 0.000
#&gt; SRR1740089     1  0.3693      0.459 0.804 0.012 0.016 0.168 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4   0.643      0.912 0.152 0.004 0.036 0.592 0.028 0.188
#&gt; SRR1740035     4   0.651      0.912 0.152 0.004 0.036 0.592 0.036 0.180
#&gt; SRR1740036     4   0.643      0.912 0.152 0.004 0.036 0.592 0.028 0.188
#&gt; SRR1740037     4   0.655      0.912 0.152 0.004 0.040 0.592 0.036 0.176
#&gt; SRR1740038     2   0.104      0.770 0.008 0.964 0.000 0.004 0.024 0.000
#&gt; SRR1740039     2   0.104      0.770 0.008 0.964 0.000 0.004 0.024 0.000
#&gt; SRR1740040     2   0.104      0.770 0.008 0.964 0.000 0.004 0.024 0.000
#&gt; SRR1740041     2   0.104      0.770 0.008 0.964 0.000 0.004 0.024 0.000
#&gt; SRR1740042     2   0.577      0.770 0.008 0.644 0.000 0.116 0.180 0.052
#&gt; SRR1740043     2   0.577      0.770 0.008 0.644 0.000 0.116 0.180 0.052
#&gt; SRR1740044     2   0.577      0.770 0.008 0.644 0.000 0.116 0.180 0.052
#&gt; SRR1740045     2   0.577      0.770 0.008 0.644 0.000 0.116 0.180 0.052
#&gt; SRR1740046     3   0.605      0.908 0.032 0.120 0.684 0.028 0.088 0.048
#&gt; SRR1740048     3   0.599      0.908 0.028 0.120 0.684 0.028 0.100 0.040
#&gt; SRR1740047     3   0.599      0.908 0.028 0.120 0.684 0.028 0.100 0.040
#&gt; SRR1740049     3   0.605      0.908 0.032 0.120 0.684 0.028 0.088 0.048
#&gt; SRR1740050     5   0.558      0.929 0.172 0.000 0.000 0.016 0.604 0.208
#&gt; SRR1740051     5   0.595      0.929 0.180 0.000 0.008 0.020 0.584 0.208
#&gt; SRR1740052     5   0.595      0.929 0.180 0.000 0.008 0.020 0.584 0.208
#&gt; SRR1740054     1   0.209      0.989 0.908 0.072 0.004 0.012 0.004 0.000
#&gt; SRR1740053     5   0.558      0.929 0.172 0.000 0.000 0.016 0.604 0.208
#&gt; SRR1740056     1   0.209      0.989 0.908 0.072 0.004 0.012 0.004 0.000
#&gt; SRR1740055     1   0.209      0.989 0.908 0.072 0.004 0.012 0.004 0.000
#&gt; SRR1740057     1   0.209      0.989 0.908 0.072 0.004 0.012 0.004 0.000
#&gt; SRR1740058     6   0.317      0.965 0.256 0.000 0.000 0.000 0.000 0.744
#&gt; SRR1740059     6   0.317      0.965 0.256 0.000 0.000 0.000 0.000 0.744
#&gt; SRR1740060     6   0.317      0.965 0.256 0.000 0.000 0.000 0.000 0.744
#&gt; SRR1740061     6   0.317      0.965 0.256 0.000 0.000 0.000 0.000 0.744
#&gt; SRR1740062     4   0.468      0.910 0.136 0.004 0.000 0.724 0.012 0.124
#&gt; SRR1740063     4   0.468      0.910 0.136 0.004 0.000 0.724 0.012 0.124
#&gt; SRR1740064     4   0.490      0.910 0.136 0.004 0.016 0.724 0.008 0.112
#&gt; SRR1740065     4   0.490      0.910 0.136 0.004 0.016 0.724 0.008 0.112
#&gt; SRR1740066     2   0.133      0.770 0.008 0.952 0.000 0.012 0.000 0.028
#&gt; SRR1740067     2   0.133      0.770 0.008 0.952 0.000 0.012 0.000 0.028
#&gt; SRR1740068     2   0.133      0.770 0.008 0.952 0.000 0.012 0.000 0.028
#&gt; SRR1740069     2   0.133      0.770 0.008 0.952 0.000 0.012 0.000 0.028
#&gt; SRR1740070     2   0.581      0.770 0.008 0.644 0.000 0.148 0.148 0.052
#&gt; SRR1740071     2   0.581      0.770 0.008 0.644 0.000 0.148 0.148 0.052
#&gt; SRR1740072     2   0.581      0.770 0.008 0.644 0.000 0.148 0.148 0.052
#&gt; SRR1740073     2   0.581      0.770 0.008 0.644 0.000 0.148 0.148 0.052
#&gt; SRR1740074     3   0.230      0.909 0.000 0.120 0.872 0.008 0.000 0.000
#&gt; SRR1740075     3   0.230      0.909 0.000 0.120 0.872 0.008 0.000 0.000
#&gt; SRR1740076     3   0.230      0.909 0.000 0.120 0.872 0.000 0.008 0.000
#&gt; SRR1740077     3   0.230      0.909 0.000 0.120 0.872 0.000 0.008 0.000
#&gt; SRR1740078     5   0.696      0.929 0.180 0.000 0.036 0.040 0.500 0.244
#&gt; SRR1740079     5   0.696      0.929 0.180 0.000 0.036 0.040 0.500 0.244
#&gt; SRR1740080     5   0.717      0.929 0.188 0.000 0.044 0.044 0.480 0.244
#&gt; SRR1740081     5   0.717      0.929 0.188 0.000 0.044 0.044 0.480 0.244
#&gt; SRR1740082     1   0.144      0.989 0.928 0.072 0.000 0.000 0.000 0.000
#&gt; SRR1740083     1   0.144      0.989 0.928 0.072 0.000 0.000 0.000 0.000
#&gt; SRR1740084     1   0.144      0.989 0.928 0.072 0.000 0.000 0.000 0.000
#&gt; SRR1740085     1   0.144      0.989 0.928 0.072 0.000 0.000 0.000 0.000
#&gt; SRR1740086     6   0.451      0.965 0.264 0.000 0.016 0.016 0.016 0.688
#&gt; SRR1740087     6   0.451      0.965 0.264 0.000 0.016 0.016 0.016 0.688
#&gt; SRR1740088     6   0.451      0.965 0.264 0.000 0.016 0.016 0.016 0.688
#&gt; SRR1740089     6   0.451      0.965 0.264 0.000 0.016 0.016 0.016 0.688
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4992 0.501   0.501
#> 3 3 0.709           0.944       0.903         0.1918 0.917   0.834
#> 4 4 0.834           0.928       0.889         0.1931 0.875   0.702
#> 5 5 0.917           0.964       0.967         0.1120 0.917   0.717
#> 6 6 1.000           0.992       0.982         0.0532 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     2       0          1  0  1
#&gt; SRR1740039     2       0          1  0  1
#&gt; SRR1740040     2       0          1  0  1
#&gt; SRR1740041     2       0          1  0  1
#&gt; SRR1740042     2       0          1  0  1
#&gt; SRR1740043     2       0          1  0  1
#&gt; SRR1740044     2       0          1  0  1
#&gt; SRR1740045     2       0          1  0  1
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     2       0          1  0  1
#&gt; SRR1740067     2       0          1  0  1
#&gt; SRR1740068     2       0          1  0  1
#&gt; SRR1740069     2       0          1  0  1
#&gt; SRR1740070     2       0          1  0  1
#&gt; SRR1740071     2       0          1  0  1
#&gt; SRR1740072     2       0          1  0  1
#&gt; SRR1740073     2       0          1  0  1
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740035     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740036     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740037     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740046     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740048     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740047     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740049     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740050     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740051     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740052     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740054     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740053     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740056     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740055     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740057     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740058     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740059     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740060     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740061     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740062     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740063     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740064     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740065     1  0.4291      0.861 0.820 0.000 0.180
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR1740074     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740075     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740076     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740077     3  0.5291      1.000 0.000 0.268 0.732
#&gt; SRR1740078     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740079     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740080     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740081     1  0.0000      0.928 1.000 0.000 0.000
#&gt; SRR1740082     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740083     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740084     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740085     1  0.3587      0.890 0.892 0.020 0.088
#&gt; SRR1740086     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740087     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740088     1  0.0892      0.928 0.980 0.000 0.020
#&gt; SRR1740089     1  0.0892      0.928 0.980 0.000 0.020
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740046     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740048     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740047     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740049     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740050     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740051     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740052     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740054     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740053     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740056     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740055     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740057     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740058     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740059     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740060     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740061     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000 0.000 1.000
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740074     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740075     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740076     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740077     3   0.112      1.000 0.000 0.036 0.964 0.000
#&gt; SRR1740078     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740079     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740080     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740081     1   0.375      0.865 0.800 0.000 0.004 0.196
#&gt; SRR1740082     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740083     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740084     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740085     1   0.121      0.789 0.964 0.000 0.032 0.004
#&gt; SRR1740086     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740087     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740088     1   0.419      0.840 0.732 0.000 0.000 0.268
#&gt; SRR1740089     1   0.419      0.840 0.732 0.000 0.000 0.268
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1740034     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740035     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740036     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740037     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740038     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740039     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740040     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740041     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740042     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740043     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740044     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740045     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740050     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740051     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740052     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740054     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740053     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740056     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740055     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740057     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740058     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740059     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740060     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740061     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740062     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740063     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740064     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740065     4  0.0290      1.000 0.000 0.000  0 0.992 0.008
#&gt; SRR1740066     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740067     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740068     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740069     2  0.0451      0.995 0.004 0.988  0 0.008 0.000
#&gt; SRR1740070     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740071     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740072     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740073     2  0.0000      0.995 0.000 1.000  0 0.000 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740078     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740079     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740080     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740081     5  0.0000      0.885 0.000 0.000  0 0.000 1.000
#&gt; SRR1740082     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740083     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740084     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740085     1  0.0162      1.000 0.996 0.000  0 0.000 0.004
#&gt; SRR1740086     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740087     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740088     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
#&gt; SRR1740089     5  0.3804      0.875 0.160 0.000  0 0.044 0.796
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5    p6
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740038     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740039     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740040     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740041     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740042     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740043     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740044     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740045     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740050     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740051     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740052     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740054     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740053     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740056     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740055     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740057     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740058     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740059     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740060     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740061     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000  0  1 0.000 0.000
#&gt; SRR1740066     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740067     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740068     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740069     2  0.0000      0.972 0.000 1.000  0  0 0.000 0.000
#&gt; SRR1740070     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740071     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740072     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740073     2  0.1500      0.972 0.012 0.936  0  0 0.052 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1  0 0.000 0.000
#&gt; SRR1740078     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740079     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740080     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740081     5  0.1141      1.000 0.000 0.000  0  0 0.948 0.052
#&gt; SRR1740082     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740083     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740084     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740085     1  0.0363      1.000 0.988 0.000  0  0 0.000 0.012
#&gt; SRR1740086     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740087     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740088     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
#&gt; SRR1740089     6  0.0000      1.000 0.000 0.000  0  0 0.000 1.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.989       0.990         0.2559 0.751   0.751
#> 3 3 0.782           0.918       0.960         1.3264 0.668   0.557
#> 4 4 0.823           0.912       0.957         0.1908 0.875   0.702
#> 5 5 0.892           0.859       0.921         0.1186 0.893   0.647
#> 6 6 1.000           1.000       1.000         0.0483 0.945   0.744
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740035     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740036     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740037     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740038     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740039     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740040     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740041     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740042     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740043     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740044     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740045     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740046     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740048     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740047     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740049     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740050     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740054     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740053     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740056     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740055     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740057     1  0.0376      0.988 0.996 0.004
#&gt; SRR1740058     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740062     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740063     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740064     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740065     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740066     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740067     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740068     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740069     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740070     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740071     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740072     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740073     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740074     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740075     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740076     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740077     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740078     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740082     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740083     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740084     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740085     1  0.1633      0.987 0.976 0.024
#&gt; SRR1740086     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.988 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.988 1.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1740034     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740035     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740036     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740037     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740042     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740043     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740044     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740045     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740050     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740051     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740052     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740054     1   0.593      0.559 0.644 0.356  0
#&gt; SRR1740053     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740056     1   0.455      0.775 0.800 0.200  0
#&gt; SRR1740055     1   0.593      0.559 0.644 0.356  0
#&gt; SRR1740057     1   0.455      0.775 0.800 0.200  0
#&gt; SRR1740058     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740059     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740060     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740061     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740062     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740063     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740064     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740065     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740070     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740071     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740072     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740073     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740078     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740079     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740080     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740081     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740082     1   0.593      0.559 0.644 0.356  0
#&gt; SRR1740083     1   0.593      0.559 0.644 0.356  0
#&gt; SRR1740084     1   0.455      0.775 0.800 0.200  0
#&gt; SRR1740085     1   0.455      0.775 0.800 0.200  0
#&gt; SRR1740086     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740087     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740088     1   0.000      0.920 1.000 0.000  0
#&gt; SRR1740089     1   0.000      0.920 1.000 0.000  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740042     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740043     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740044     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740045     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740050     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740051     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740052     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740054     1   0.488      0.484 0.592 0.408  0  0
#&gt; SRR1740053     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740056     1   0.361      0.772 0.800 0.200  0  0
#&gt; SRR1740055     1   0.488      0.484 0.592 0.408  0  0
#&gt; SRR1740057     1   0.361      0.772 0.800 0.200  0  0
#&gt; SRR1740058     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740059     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740060     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740061     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740070     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740071     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740072     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740073     2   0.000      1.000 0.000 1.000  0  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740078     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740079     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740080     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740081     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740082     1   0.488      0.484 0.592 0.408  0  0
#&gt; SRR1740083     1   0.488      0.484 0.592 0.408  0  0
#&gt; SRR1740084     1   0.361      0.772 0.800 0.200  0  0
#&gt; SRR1740085     1   0.361      0.772 0.800 0.200  0  0
#&gt; SRR1740086     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740087     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740088     1   0.000      0.878 1.000 0.000  0  0
#&gt; SRR1740089     1   0.000      0.878 1.000 0.000  0  0
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740038     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740039     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740040     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740041     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740042     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740043     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740044     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740045     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740050     5   0.342      0.752 0.240 0.000  0  0 0.760
#&gt; SRR1740051     5   0.000      0.829 0.000 0.000  0  0 1.000
#&gt; SRR1740052     5   0.000      0.829 0.000 0.000  0  0 1.000
#&gt; SRR1740054     5   0.440      0.718 0.252 0.036  0  0 0.712
#&gt; SRR1740053     5   0.351      0.741 0.252 0.000  0  0 0.748
#&gt; SRR1740056     1   0.368      0.335 0.720 0.000  0  0 0.280
#&gt; SRR1740055     2   0.551      0.458 0.252 0.632  0  0 0.116
#&gt; SRR1740057     1   0.304      0.500 0.808 0.000  0  0 0.192
#&gt; SRR1740058     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740059     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740060     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740061     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0  1 0.000
#&gt; SRR1740066     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740067     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740068     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740069     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740070     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740071     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740072     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740073     2   0.000      0.976 0.000 1.000  0  0 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1  0 0.000
#&gt; SRR1740078     5   0.167      0.839 0.076 0.000  0  0 0.924
#&gt; SRR1740079     5   0.161      0.840 0.072 0.000  0  0 0.928
#&gt; SRR1740080     5   0.000      0.829 0.000 0.000  0  0 1.000
#&gt; SRR1740081     5   0.000      0.829 0.000 0.000  0  0 1.000
#&gt; SRR1740082     1   0.497      0.234 0.588 0.376  0  0 0.036
#&gt; SRR1740083     1   0.326      0.561 0.840 0.124  0  0 0.036
#&gt; SRR1740084     1   0.218      0.591 0.888 0.000  0  0 0.112
#&gt; SRR1740085     1   0.218      0.591 0.888 0.000  0  0 0.112
#&gt; SRR1740086     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740087     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740088     1   0.351      0.749 0.748 0.000  0  0 0.252
#&gt; SRR1740089     1   0.351      0.749 0.748 0.000  0  0 0.252
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.751           0.936       0.959         0.4787 0.501   0.501
#> 3 3 0.834           0.924       0.949         0.3275 0.668   0.431
#> 4 4 1.000           1.000       1.000         0.1123 0.958   0.876
#> 5 5 1.000           1.000       1.000         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 4 5
```

There is also optional best $k$ = 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740035     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740036     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740037     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740038     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740039     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740040     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740041     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740042     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740043     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740044     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740045     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740046     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740048     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740047     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740049     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740050     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740051     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740052     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740054     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740053     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740056     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740055     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740057     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740058     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740059     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740060     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740061     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740062     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740063     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740064     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740065     1  0.0938      0.907 0.988 0.012
#&gt; SRR1740066     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740067     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740068     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740069     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740070     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740071     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740072     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740073     2  0.0000      0.990 0.000 1.000
#&gt; SRR1740074     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740075     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740076     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740077     1  0.0000      0.907 1.000 0.000
#&gt; SRR1740078     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740079     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740080     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740081     2  0.1633      0.984 0.024 0.976
#&gt; SRR1740082     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740083     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740084     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740085     2  0.0938      0.989 0.012 0.988
#&gt; SRR1740086     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740087     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740088     1  0.7883      0.781 0.764 0.236
#&gt; SRR1740089     1  0.7883      0.781 0.764 0.236
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1 p2   p3
#&gt; SRR1740034     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740035     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740036     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740037     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740038     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740039     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740040     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740041     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740042     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740043     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740044     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740045     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740046     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740048     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740047     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740049     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740050     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740051     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740052     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740054     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740053     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740056     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740055     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740057     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740058     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740059     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740060     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740061     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740062     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740063     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740064     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740065     3   0.595      0.700 0.36  0 0.64
#&gt; SRR1740066     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740067     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740068     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740069     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740070     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740071     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740072     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740073     2   0.000      1.000 0.00  1 0.00
#&gt; SRR1740074     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740075     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740076     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740077     3   0.000      0.767 0.00  0 1.00
#&gt; SRR1740078     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740079     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740080     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740081     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740082     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740083     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740084     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740085     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740086     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740087     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740088     1   0.000      1.000 1.00  0 0.00
#&gt; SRR1740089     1   0.000      1.000 1.00  0 0.00
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1740034     4       0          1  0  0  0  1
#&gt; SRR1740035     4       0          1  0  0  0  1
#&gt; SRR1740036     4       0          1  0  0  0  1
#&gt; SRR1740037     4       0          1  0  0  0  1
#&gt; SRR1740038     2       0          1  0  1  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0
#&gt; SRR1740048     3       0          1  0  0  1  0
#&gt; SRR1740047     3       0          1  0  0  1  0
#&gt; SRR1740049     3       0          1  0  0  1  0
#&gt; SRR1740050     1       0          1  1  0  0  0
#&gt; SRR1740051     1       0          1  1  0  0  0
#&gt; SRR1740052     1       0          1  1  0  0  0
#&gt; SRR1740054     1       0          1  1  0  0  0
#&gt; SRR1740053     1       0          1  1  0  0  0
#&gt; SRR1740056     1       0          1  1  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0
#&gt; SRR1740058     1       0          1  1  0  0  0
#&gt; SRR1740059     1       0          1  1  0  0  0
#&gt; SRR1740060     1       0          1  1  0  0  0
#&gt; SRR1740061     1       0          1  1  0  0  0
#&gt; SRR1740062     4       0          1  0  0  0  1
#&gt; SRR1740063     4       0          1  0  0  0  1
#&gt; SRR1740064     4       0          1  0  0  0  1
#&gt; SRR1740065     4       0          1  0  0  0  1
#&gt; SRR1740066     2       0          1  0  1  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0
#&gt; SRR1740075     3       0          1  0  0  1  0
#&gt; SRR1740076     3       0          1  0  0  1  0
#&gt; SRR1740077     3       0          1  0  0  1  0
#&gt; SRR1740078     1       0          1  1  0  0  0
#&gt; SRR1740079     1       0          1  1  0  0  0
#&gt; SRR1740080     1       0          1  1  0  0  0
#&gt; SRR1740081     1       0          1  1  0  0  0
#&gt; SRR1740082     1       0          1  1  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0
#&gt; SRR1740086     1       0          1  1  0  0  0
#&gt; SRR1740087     1       0          1  1  0  0  0
#&gt; SRR1740088     1       0          1  1  0  0  0
#&gt; SRR1740089     1       0          1  1  0  0  0
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5
#&gt; SRR1740034     4       0          1  0  0  0  1  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1
#&gt; SRR1740051     5       0          1  0  0  0  0  1
#&gt; SRR1740052     5       0          1  0  0  0  0  1
#&gt; SRR1740054     1       0          1  1  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1
#&gt; SRR1740056     1       0          1  1  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0
#&gt; SRR1740058     5       0          1  0  0  0  0  1
#&gt; SRR1740059     5       0          1  0  0  0  0  1
#&gt; SRR1740060     5       0          1  0  0  0  0  1
#&gt; SRR1740061     5       0          1  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1
#&gt; SRR1740079     5       0          1  0  0  0  0  1
#&gt; SRR1740080     5       0          1  0  0  0  0  1
#&gt; SRR1740081     5       0          1  0  0  0  0  1
#&gt; SRR1740082     1       0          1  1  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0
#&gt; SRR1740086     5       0          1  0  0  0  0  1
#&gt; SRR1740087     5       0          1  0  0  0  0  1
#&gt; SRR1740088     5       0          1  0  0  0  0  1
#&gt; SRR1740089     5       0          1  0  0  0  0  1
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.537           0.707       0.888         0.3861 0.584   0.584
#> 3 3 0.795           0.921       0.942         0.5453 0.731   0.573
#> 4 4 0.975           0.947       0.978         0.1903 0.881   0.707
#> 5 5 0.978           0.937       0.953         0.1073 0.922   0.730
#> 6 6 0.951           0.856       0.921         0.0588 0.953   0.778
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 4 5
```

There is also optional best $k$ = 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740035     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740036     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740037     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740038     1  0.9710      0.147 0.600 0.400
#&gt; SRR1740039     1  0.9661      0.176 0.608 0.392
#&gt; SRR1740040     1  0.9710      0.147 0.600 0.400
#&gt; SRR1740041     1  0.9635      0.189 0.612 0.388
#&gt; SRR1740042     2  0.9933      0.395 0.452 0.548
#&gt; SRR1740043     2  0.9909      0.416 0.444 0.556
#&gt; SRR1740044     2  0.9881      0.434 0.436 0.564
#&gt; SRR1740045     2  0.9933      0.395 0.452 0.548
#&gt; SRR1740046     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740048     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740047     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740049     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740050     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740054     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740053     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740056     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740055     1  0.0672      0.879 0.992 0.008
#&gt; SRR1740057     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740058     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740062     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740063     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740064     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740065     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740066     1  0.9710      0.147 0.600 0.400
#&gt; SRR1740067     1  0.9710      0.147 0.600 0.400
#&gt; SRR1740068     1  0.9635      0.189 0.612 0.388
#&gt; SRR1740069     1  0.9608      0.201 0.616 0.384
#&gt; SRR1740070     2  0.8386      0.646 0.268 0.732
#&gt; SRR1740071     2  0.8813      0.624 0.300 0.700
#&gt; SRR1740072     2  0.9427      0.562 0.360 0.640
#&gt; SRR1740073     2  0.9661      0.516 0.392 0.608
#&gt; SRR1740074     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740075     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740076     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740077     2  0.0000      0.745 0.000 1.000
#&gt; SRR1740078     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740082     1  0.0376      0.882 0.996 0.004
#&gt; SRR1740083     1  0.0376      0.882 0.996 0.004
#&gt; SRR1740084     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740085     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740086     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.886 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.886 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740035     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740036     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740037     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740038     2  0.0000     0.9431 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000     0.9431 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000     0.9431 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0424     0.9358 0.000 0.992 0.008
#&gt; SRR1740042     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740043     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740044     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740045     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740046     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740048     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740047     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740049     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740050     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740051     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740052     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740054     1  0.2165     0.9053 0.936 0.064 0.000
#&gt; SRR1740053     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740056     1  0.0424     0.9415 0.992 0.008 0.000
#&gt; SRR1740055     2  0.6309     0.0208 0.496 0.504 0.000
#&gt; SRR1740057     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740058     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740059     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740060     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740061     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740062     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740063     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740064     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740065     1  0.5500     0.8542 0.816 0.084 0.100
#&gt; SRR1740066     2  0.0000     0.9431 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000     0.9431 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0237     0.9441 0.000 0.996 0.004
#&gt; SRR1740069     2  0.0237     0.9441 0.000 0.996 0.004
#&gt; SRR1740070     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740071     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740072     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740073     2  0.0747     0.9439 0.000 0.984 0.016
#&gt; SRR1740074     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740075     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740076     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740077     3  0.2959     1.0000 0.000 0.100 0.900
#&gt; SRR1740078     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740079     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740080     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740081     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740082     1  0.1643     0.9252 0.956 0.044 0.000
#&gt; SRR1740083     1  0.1753     0.9218 0.952 0.048 0.000
#&gt; SRR1740084     1  0.1289     0.9287 0.968 0.032 0.000
#&gt; SRR1740085     1  0.0747     0.9377 0.984 0.016 0.000
#&gt; SRR1740086     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740087     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740088     1  0.0000     0.9447 1.000 0.000 0.000
#&gt; SRR1740089     1  0.0000     0.9447 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1740034     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740035     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740036     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740037     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740038     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740039     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740040     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740041     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740042     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740043     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740044     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740045     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740046     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740048     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740047     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740049     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740050     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740051     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740052     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740054     1  0.2868     0.8558 0.864 0.136 0.000  0
#&gt; SRR1740053     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740056     1  0.0707     0.9551 0.980 0.020 0.000  0
#&gt; SRR1740055     2  0.5151     0.0337 0.464 0.532 0.004  0
#&gt; SRR1740057     1  0.0592     0.9574 0.984 0.016 0.000  0
#&gt; SRR1740058     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740059     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740060     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740061     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740062     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740063     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740064     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740065     4  0.0000     1.0000 0.000 0.000 0.000  1
#&gt; SRR1740066     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740067     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740068     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740069     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740070     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740071     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740072     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740073     2  0.0000     0.9625 0.000 1.000 0.000  0
#&gt; SRR1740074     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740075     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740076     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740077     3  0.0188     1.0000 0.000 0.004 0.996  0
#&gt; SRR1740078     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740079     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740080     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740081     1  0.0188     0.9646 0.996 0.000 0.004  0
#&gt; SRR1740082     1  0.3219     0.8234 0.836 0.164 0.000  0
#&gt; SRR1740083     1  0.3764     0.7503 0.784 0.216 0.000  0
#&gt; SRR1740084     1  0.2149     0.9014 0.912 0.088 0.000  0
#&gt; SRR1740085     1  0.1022     0.9470 0.968 0.032 0.000  0
#&gt; SRR1740086     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740087     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740088     1  0.0000     0.9647 1.000 0.000 0.000  0
#&gt; SRR1740089     1  0.0000     0.9647 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1740034     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740035     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740036     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740037     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740038     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740039     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740040     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740041     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740042     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740043     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740044     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740045     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740046     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740048     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740047     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740049     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740050     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740051     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740052     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740054     1  0.4818     0.0448 0.520 0.460  0  0 0.020
#&gt; SRR1740053     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740056     1  0.3413     0.8124 0.832 0.124  0  0 0.044
#&gt; SRR1740055     2  0.2561     0.8952 0.144 0.856  0  0 0.000
#&gt; SRR1740057     1  0.3242     0.8659 0.852 0.076  0  0 0.072
#&gt; SRR1740058     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740059     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740060     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740061     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740062     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740063     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740064     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740065     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740066     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740067     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740068     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740069     2  0.0290     0.9478 0.000 0.992  0  0 0.008
#&gt; SRR1740070     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740071     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740072     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740073     2  0.2017     0.9513 0.080 0.912  0  0 0.008
#&gt; SRR1740074     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740075     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740076     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740077     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740078     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740079     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740080     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740081     5  0.0510     1.0000 0.016 0.000  0  0 0.984
#&gt; SRR1740082     1  0.1197     0.8563 0.952 0.048  0  0 0.000
#&gt; SRR1740083     1  0.0703     0.8695 0.976 0.024  0  0 0.000
#&gt; SRR1740084     1  0.0510     0.8720 0.984 0.016  0  0 0.000
#&gt; SRR1740085     1  0.0693     0.8780 0.980 0.012  0  0 0.008
#&gt; SRR1740086     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740087     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740088     1  0.1732     0.8977 0.920 0.000  0  0 0.080
#&gt; SRR1740089     1  0.1732     0.8977 0.920 0.000  0  0 0.080
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5    p6
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740038     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740039     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740040     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740041     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740042     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740043     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740044     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740045     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740050     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740051     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740052     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740054     6  0.4565     -0.875 0.432 0.036  0  0  0 0.532
#&gt; SRR1740053     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740056     6  0.1753      0.226 0.084 0.004  0  0  0 0.912
#&gt; SRR1740055     1  0.4650      0.958 0.488 0.040  0  0  0 0.472
#&gt; SRR1740057     6  0.0713      0.426 0.028 0.000  0  0  0 0.972
#&gt; SRR1740058     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740059     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740060     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740061     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740066     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740067     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740068     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740069     2  0.0363      1.000 0.000 0.988  0  0  0 0.012
#&gt; SRR1740070     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740071     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740072     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740073     1  0.4941      0.995 0.492 0.064  0  0  0 0.444
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740078     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740079     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740080     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740081     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740082     6  0.1196      0.379 0.040 0.008  0  0  0 0.952
#&gt; SRR1740083     6  0.0790      0.460 0.032 0.000  0  0  0 0.968
#&gt; SRR1740084     6  0.1007      0.340 0.044 0.000  0  0  0 0.956
#&gt; SRR1740085     6  0.0547      0.447 0.020 0.000  0  0  0 0.980
#&gt; SRR1740086     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740087     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740088     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
#&gt; SRR1740089     6  0.3854      0.703 0.464 0.000  0  0  0 0.536
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.501           0.959       0.931         0.4595 0.501   0.501
#> 3 3 1.000           0.999       0.998         0.3568 0.875   0.751
#> 4 4 1.000           0.997       0.995         0.1336 0.917   0.779
#> 5 5 1.000           1.000       1.000         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 3 4 5
```

There is also optional best $k$ = 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1   p2
#&gt; SRR1740034     1   0.000      0.859 1.00 0.00
#&gt; SRR1740035     1   0.000      0.859 1.00 0.00
#&gt; SRR1740036     1   0.000      0.859 1.00 0.00
#&gt; SRR1740037     1   0.000      0.859 1.00 0.00
#&gt; SRR1740038     2   0.000      1.000 0.00 1.00
#&gt; SRR1740039     2   0.000      1.000 0.00 1.00
#&gt; SRR1740040     2   0.000      1.000 0.00 1.00
#&gt; SRR1740041     2   0.000      1.000 0.00 1.00
#&gt; SRR1740042     2   0.000      1.000 0.00 1.00
#&gt; SRR1740043     2   0.000      1.000 0.00 1.00
#&gt; SRR1740044     2   0.000      1.000 0.00 1.00
#&gt; SRR1740045     2   0.000      1.000 0.00 1.00
#&gt; SRR1740046     2   0.000      1.000 0.00 1.00
#&gt; SRR1740048     2   0.000      1.000 0.00 1.00
#&gt; SRR1740047     2   0.000      1.000 0.00 1.00
#&gt; SRR1740049     2   0.000      1.000 0.00 1.00
#&gt; SRR1740050     1   0.634      0.951 0.84 0.16
#&gt; SRR1740051     1   0.634      0.951 0.84 0.16
#&gt; SRR1740052     1   0.634      0.951 0.84 0.16
#&gt; SRR1740054     1   0.634      0.951 0.84 0.16
#&gt; SRR1740053     1   0.634      0.951 0.84 0.16
#&gt; SRR1740056     1   0.634      0.951 0.84 0.16
#&gt; SRR1740055     1   0.634      0.951 0.84 0.16
#&gt; SRR1740057     1   0.634      0.951 0.84 0.16
#&gt; SRR1740058     1   0.634      0.951 0.84 0.16
#&gt; SRR1740059     1   0.634      0.951 0.84 0.16
#&gt; SRR1740060     1   0.634      0.951 0.84 0.16
#&gt; SRR1740061     1   0.634      0.951 0.84 0.16
#&gt; SRR1740062     1   0.000      0.859 1.00 0.00
#&gt; SRR1740063     1   0.000      0.859 1.00 0.00
#&gt; SRR1740064     1   0.000      0.859 1.00 0.00
#&gt; SRR1740065     1   0.000      0.859 1.00 0.00
#&gt; SRR1740066     2   0.000      1.000 0.00 1.00
#&gt; SRR1740067     2   0.000      1.000 0.00 1.00
#&gt; SRR1740068     2   0.000      1.000 0.00 1.00
#&gt; SRR1740069     2   0.000      1.000 0.00 1.00
#&gt; SRR1740070     2   0.000      1.000 0.00 1.00
#&gt; SRR1740071     2   0.000      1.000 0.00 1.00
#&gt; SRR1740072     2   0.000      1.000 0.00 1.00
#&gt; SRR1740073     2   0.000      1.000 0.00 1.00
#&gt; SRR1740074     2   0.000      1.000 0.00 1.00
#&gt; SRR1740075     2   0.000      1.000 0.00 1.00
#&gt; SRR1740076     2   0.000      1.000 0.00 1.00
#&gt; SRR1740077     2   0.000      1.000 0.00 1.00
#&gt; SRR1740078     1   0.634      0.951 0.84 0.16
#&gt; SRR1740079     1   0.634      0.951 0.84 0.16
#&gt; SRR1740080     1   0.634      0.951 0.84 0.16
#&gt; SRR1740081     1   0.634      0.951 0.84 0.16
#&gt; SRR1740082     1   0.634      0.951 0.84 0.16
#&gt; SRR1740083     1   0.634      0.951 0.84 0.16
#&gt; SRR1740084     1   0.634      0.951 0.84 0.16
#&gt; SRR1740085     1   0.634      0.951 0.84 0.16
#&gt; SRR1740086     1   0.634      0.951 0.84 0.16
#&gt; SRR1740087     1   0.634      0.951 0.84 0.16
#&gt; SRR1740088     1   0.634      0.951 0.84 0.16
#&gt; SRR1740089     1   0.634      0.951 0.84 0.16
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740035     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740036     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740037     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740038     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740042     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740043     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740044     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740045     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740046     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740048     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740047     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740049     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740050     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740051     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740052     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740054     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740053     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740056     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740055     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740057     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740058     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740059     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740060     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740061     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740062     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740063     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740064     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740065     3  0.0424      1.000 0.008 0.000 0.992
#&gt; SRR1740066     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740070     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740071     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740072     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740073     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR1740074     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740075     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740076     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740077     2  0.0424      0.995 0.000 0.992 0.008
#&gt; SRR1740078     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740079     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740080     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740081     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740082     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740083     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740084     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740085     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740086     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740087     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740088     1  0.0000      1.000 1.000 0.000 0.000
#&gt; SRR1740089     1  0.0000      1.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740046     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740048     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740047     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740049     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740050     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740051     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740052     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740054     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740053     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740056     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740055     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740057     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740058     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740059     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740060     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740061     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740074     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740075     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740076     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740077     3  0.0592      1.000 0.000 0.016 0.984  0
#&gt; SRR1740078     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740079     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740080     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740081     1  0.0592      0.990 0.984 0.000 0.016  0
#&gt; SRR1740082     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740083     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740084     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740085     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740086     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740087     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740088     1  0.0000      0.995 1.000 0.000 0.000  0
#&gt; SRR1740089     1  0.0000      0.995 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5
#&gt; SRR1740034     4       0          1  0  0  0  1  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1
#&gt; SRR1740051     5       0          1  0  0  0  0  1
#&gt; SRR1740052     5       0          1  0  0  0  0  1
#&gt; SRR1740054     1       0          1  1  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1
#&gt; SRR1740056     1       0          1  1  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0
#&gt; SRR1740058     1       0          1  1  0  0  0  0
#&gt; SRR1740059     1       0          1  1  0  0  0  0
#&gt; SRR1740060     1       0          1  1  0  0  0  0
#&gt; SRR1740061     1       0          1  1  0  0  0  0
#&gt; SRR1740062     4       0          1  0  0  0  1  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1
#&gt; SRR1740079     5       0          1  0  0  0  0  1
#&gt; SRR1740080     5       0          1  0  0  0  0  1
#&gt; SRR1740081     5       0          1  0  0  0  0  1
#&gt; SRR1740082     1       0          1  1  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0
#&gt; SRR1740086     1       0          1  1  0  0  0  0
#&gt; SRR1740087     1       0          1  1  0  0  0  0
#&gt; SRR1740088     1       0          1  1  0  0  0  0
#&gt; SRR1740089     1       0          1  1  0  0  0  0
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.252           0.862       0.831         0.4131 0.501   0.501
#> 3 3 0.294           0.745       0.721         0.3760 1.000   1.000
#> 4 4 0.626           0.762       0.710         0.1999 0.792   0.585
#> 5 5 0.522           0.560       0.529         0.0786 0.834   0.504
#> 6 6 0.626           0.680       0.688         0.0683 0.844   0.429
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.671      0.742 0.824 0.176
#&gt; SRR1740035     1   0.671      0.742 0.824 0.176
#&gt; SRR1740036     1   0.671      0.742 0.824 0.176
#&gt; SRR1740037     1   0.671      0.742 0.824 0.176
#&gt; SRR1740038     2   0.584      0.912 0.140 0.860
#&gt; SRR1740039     2   0.584      0.912 0.140 0.860
#&gt; SRR1740040     2   0.584      0.912 0.140 0.860
#&gt; SRR1740041     2   0.584      0.912 0.140 0.860
#&gt; SRR1740042     2   0.574      0.913 0.136 0.864
#&gt; SRR1740043     2   0.574      0.913 0.136 0.864
#&gt; SRR1740044     2   0.574      0.913 0.136 0.864
#&gt; SRR1740045     2   0.574      0.913 0.136 0.864
#&gt; SRR1740046     2   0.224      0.842 0.036 0.964
#&gt; SRR1740048     2   0.224      0.842 0.036 0.964
#&gt; SRR1740047     2   0.224      0.842 0.036 0.964
#&gt; SRR1740049     2   0.224      0.842 0.036 0.964
#&gt; SRR1740050     1   0.689      0.868 0.816 0.184
#&gt; SRR1740051     1   0.689      0.868 0.816 0.184
#&gt; SRR1740052     1   0.689      0.868 0.816 0.184
#&gt; SRR1740054     1   0.781      0.876 0.768 0.232
#&gt; SRR1740053     1   0.689      0.868 0.816 0.184
#&gt; SRR1740056     1   0.781      0.876 0.768 0.232
#&gt; SRR1740055     1   0.781      0.876 0.768 0.232
#&gt; SRR1740057     1   0.781      0.876 0.768 0.232
#&gt; SRR1740058     1   0.697      0.880 0.812 0.188
#&gt; SRR1740059     1   0.697      0.880 0.812 0.188
#&gt; SRR1740060     1   0.697      0.880 0.812 0.188
#&gt; SRR1740061     1   0.697      0.880 0.812 0.188
#&gt; SRR1740062     1   0.671      0.742 0.824 0.176
#&gt; SRR1740063     1   0.671      0.742 0.824 0.176
#&gt; SRR1740064     1   0.671      0.742 0.824 0.176
#&gt; SRR1740065     1   0.671      0.742 0.824 0.176
#&gt; SRR1740066     2   0.584      0.912 0.140 0.860
#&gt; SRR1740067     2   0.584      0.912 0.140 0.860
#&gt; SRR1740068     2   0.584      0.912 0.140 0.860
#&gt; SRR1740069     2   0.584      0.912 0.140 0.860
#&gt; SRR1740070     2   0.574      0.913 0.136 0.864
#&gt; SRR1740071     2   0.574      0.913 0.136 0.864
#&gt; SRR1740072     2   0.574      0.913 0.136 0.864
#&gt; SRR1740073     2   0.574      0.913 0.136 0.864
#&gt; SRR1740074     2   0.224      0.842 0.036 0.964
#&gt; SRR1740075     2   0.224      0.842 0.036 0.964
#&gt; SRR1740076     2   0.224      0.842 0.036 0.964
#&gt; SRR1740077     2   0.224      0.842 0.036 0.964
#&gt; SRR1740078     1   0.689      0.868 0.816 0.184
#&gt; SRR1740079     1   0.689      0.868 0.816 0.184
#&gt; SRR1740080     1   0.689      0.868 0.816 0.184
#&gt; SRR1740081     1   0.689      0.868 0.816 0.184
#&gt; SRR1740082     1   0.781      0.876 0.768 0.232
#&gt; SRR1740083     1   0.781      0.876 0.768 0.232
#&gt; SRR1740084     1   0.781      0.876 0.768 0.232
#&gt; SRR1740085     1   0.781      0.876 0.768 0.232
#&gt; SRR1740086     1   0.697      0.880 0.812 0.188
#&gt; SRR1740087     1   0.697      0.880 0.812 0.188
#&gt; SRR1740088     1   0.697      0.880 0.812 0.188
#&gt; SRR1740089     1   0.697      0.880 0.812 0.188
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1740034     1   0.797      0.590 0.560 0.068 NA
#&gt; SRR1740035     1   0.797      0.590 0.560 0.068 NA
#&gt; SRR1740036     1   0.797      0.590 0.560 0.068 NA
#&gt; SRR1740037     1   0.797      0.590 0.560 0.068 NA
#&gt; SRR1740038     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740039     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740040     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740041     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740042     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740043     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740044     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740045     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740046     2   0.186      0.716 0.052 0.948 NA
#&gt; SRR1740048     2   0.186      0.716 0.052 0.948 NA
#&gt; SRR1740047     2   0.186      0.716 0.052 0.948 NA
#&gt; SRR1740049     2   0.186      0.716 0.052 0.948 NA
#&gt; SRR1740050     1   0.584      0.726 0.768 0.036 NA
#&gt; SRR1740051     1   0.584      0.726 0.768 0.036 NA
#&gt; SRR1740052     1   0.584      0.726 0.768 0.036 NA
#&gt; SRR1740054     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740053     1   0.584      0.726 0.768 0.036 NA
#&gt; SRR1740056     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740055     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740057     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740058     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740059     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740060     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740061     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740062     1   0.777      0.590 0.560 0.056 NA
#&gt; SRR1740063     1   0.777      0.590 0.560 0.056 NA
#&gt; SRR1740064     1   0.777      0.590 0.560 0.056 NA
#&gt; SRR1740065     1   0.777      0.590 0.560 0.056 NA
#&gt; SRR1740066     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740067     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740068     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740069     2   0.925      0.786 0.164 0.480 NA
#&gt; SRR1740070     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740071     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740072     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740073     2   0.846      0.815 0.156 0.612 NA
#&gt; SRR1740074     2   0.301      0.716 0.052 0.920 NA
#&gt; SRR1740075     2   0.301      0.716 0.052 0.920 NA
#&gt; SRR1740076     2   0.301      0.716 0.052 0.920 NA
#&gt; SRR1740077     2   0.301      0.716 0.052 0.920 NA
#&gt; SRR1740078     1   0.546      0.726 0.768 0.016 NA
#&gt; SRR1740079     1   0.546      0.726 0.768 0.016 NA
#&gt; SRR1740080     1   0.546      0.726 0.768 0.016 NA
#&gt; SRR1740081     1   0.546      0.726 0.768 0.016 NA
#&gt; SRR1740082     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740083     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740084     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740085     1   0.183      0.794 0.956 0.036 NA
#&gt; SRR1740086     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740087     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740088     1   0.300      0.791 0.916 0.016 NA
#&gt; SRR1740089     1   0.300      0.791 0.916 0.016 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4   0.112      0.969 0.000 0.036 0.000 0.964
#&gt; SRR1740035     4   0.112      0.969 0.000 0.036 0.000 0.964
#&gt; SRR1740036     4   0.112      0.969 0.000 0.036 0.000 0.964
#&gt; SRR1740037     4   0.112      0.969 0.000 0.036 0.000 0.964
#&gt; SRR1740038     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740039     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740040     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740041     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740042     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740043     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740044     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740045     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740046     3   0.510      0.947 0.004 0.368 0.624 0.004
#&gt; SRR1740048     3   0.510      0.947 0.004 0.368 0.624 0.004
#&gt; SRR1740047     3   0.510      0.947 0.004 0.368 0.624 0.004
#&gt; SRR1740049     3   0.510      0.947 0.004 0.368 0.624 0.004
#&gt; SRR1740050     1   0.814      0.505 0.500 0.028 0.240 0.232
#&gt; SRR1740051     1   0.814      0.505 0.500 0.028 0.240 0.232
#&gt; SRR1740052     1   0.814      0.505 0.500 0.028 0.240 0.232
#&gt; SRR1740054     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740053     1   0.814      0.505 0.500 0.028 0.240 0.232
#&gt; SRR1740056     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740055     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740057     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740058     1   0.642      0.607 0.620 0.032 0.036 0.312
#&gt; SRR1740059     1   0.642      0.607 0.620 0.032 0.036 0.312
#&gt; SRR1740060     1   0.642      0.607 0.620 0.032 0.036 0.312
#&gt; SRR1740061     1   0.642      0.607 0.620 0.032 0.036 0.312
#&gt; SRR1740062     4   0.274      0.968 0.000 0.036 0.060 0.904
#&gt; SRR1740063     4   0.274      0.968 0.000 0.036 0.060 0.904
#&gt; SRR1740064     4   0.285      0.968 0.004 0.036 0.056 0.904
#&gt; SRR1740065     4   0.285      0.968 0.004 0.036 0.056 0.904
#&gt; SRR1740066     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740067     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740068     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740069     2   0.000      0.840 0.000 1.000 0.000 0.000
#&gt; SRR1740070     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740071     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740072     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740073     2   0.448      0.828 0.064 0.812 0.120 0.004
#&gt; SRR1740074     3   0.698      0.947 0.072 0.368 0.540 0.020
#&gt; SRR1740075     3   0.698      0.947 0.072 0.368 0.540 0.020
#&gt; SRR1740076     3   0.698      0.947 0.072 0.368 0.540 0.020
#&gt; SRR1740077     3   0.698      0.947 0.072 0.368 0.540 0.020
#&gt; SRR1740078     1   0.824      0.505 0.480 0.028 0.260 0.232
#&gt; SRR1740079     1   0.824      0.505 0.480 0.028 0.260 0.232
#&gt; SRR1740080     1   0.824      0.505 0.480 0.028 0.260 0.232
#&gt; SRR1740081     1   0.824      0.505 0.480 0.028 0.260 0.232
#&gt; SRR1740082     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740083     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740084     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740085     1   0.624      0.638 0.604 0.076 0.000 0.320
#&gt; SRR1740086     1   0.658      0.607 0.612 0.032 0.044 0.312
#&gt; SRR1740087     1   0.658      0.607 0.612 0.032 0.044 0.312
#&gt; SRR1740088     1   0.658      0.607 0.612 0.032 0.044 0.312
#&gt; SRR1740089     1   0.658      0.607 0.612 0.032 0.044 0.312
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.2828      0.940 0.000 0.020 0.004 0.872 0.104
#&gt; SRR1740035     4  0.2828      0.940 0.000 0.020 0.004 0.872 0.104
#&gt; SRR1740036     4  0.2828      0.940 0.000 0.020 0.004 0.872 0.104
#&gt; SRR1740037     4  0.2890      0.939 0.004 0.016 0.004 0.872 0.104
#&gt; SRR1740038     3  0.5817     -0.120 0.000 0.384 0.544 0.028 0.044
#&gt; SRR1740039     3  0.5817     -0.120 0.000 0.384 0.544 0.028 0.044
#&gt; SRR1740040     3  0.5817     -0.120 0.000 0.384 0.544 0.028 0.044
#&gt; SRR1740041     3  0.5817     -0.120 0.000 0.384 0.544 0.028 0.044
#&gt; SRR1740042     2  0.4228      0.987 0.000 0.748 0.216 0.004 0.032
#&gt; SRR1740043     2  0.4228      0.987 0.000 0.748 0.216 0.004 0.032
#&gt; SRR1740044     2  0.4228      0.987 0.000 0.748 0.216 0.004 0.032
#&gt; SRR1740045     2  0.4228      0.987 0.000 0.748 0.216 0.004 0.032
#&gt; SRR1740046     3  0.6041      0.380 0.204 0.120 0.644 0.032 0.000
#&gt; SRR1740048     3  0.5885      0.380 0.204 0.120 0.652 0.024 0.000
#&gt; SRR1740047     3  0.5885      0.380 0.204 0.120 0.652 0.024 0.000
#&gt; SRR1740049     3  0.6041      0.380 0.204 0.120 0.644 0.032 0.000
#&gt; SRR1740050     5  0.2322      0.500 0.028 0.036 0.008 0.008 0.920
#&gt; SRR1740051     5  0.2322      0.500 0.028 0.036 0.008 0.008 0.920
#&gt; SRR1740052     5  0.2322      0.500 0.028 0.036 0.008 0.008 0.920
#&gt; SRR1740054     5  0.8523      0.257 0.200 0.212 0.004 0.216 0.368
#&gt; SRR1740053     5  0.2322      0.500 0.028 0.036 0.008 0.008 0.920
#&gt; SRR1740056     5  0.8523      0.257 0.200 0.212 0.004 0.216 0.368
#&gt; SRR1740055     5  0.8523      0.257 0.200 0.212 0.004 0.216 0.368
#&gt; SRR1740057     5  0.8523      0.257 0.200 0.212 0.004 0.216 0.368
#&gt; SRR1740058     1  0.6665      0.976 0.536 0.020 0.000 0.180 0.264
#&gt; SRR1740059     1  0.6665      0.976 0.536 0.020 0.000 0.180 0.264
#&gt; SRR1740060     1  0.6665      0.976 0.536 0.020 0.000 0.180 0.264
#&gt; SRR1740061     1  0.6665      0.976 0.536 0.020 0.000 0.180 0.264
#&gt; SRR1740062     4  0.4908      0.940 0.032 0.092 0.004 0.768 0.104
#&gt; SRR1740063     4  0.4908      0.940 0.032 0.092 0.004 0.768 0.104
#&gt; SRR1740064     4  0.4908      0.940 0.032 0.092 0.004 0.768 0.104
#&gt; SRR1740065     4  0.4908      0.940 0.032 0.092 0.004 0.768 0.104
#&gt; SRR1740066     3  0.6718     -0.120 0.040 0.392 0.496 0.028 0.044
#&gt; SRR1740067     3  0.6718     -0.120 0.040 0.392 0.496 0.028 0.044
#&gt; SRR1740068     3  0.6718     -0.120 0.040 0.392 0.496 0.028 0.044
#&gt; SRR1740069     3  0.6718     -0.120 0.040 0.392 0.496 0.028 0.044
#&gt; SRR1740070     2  0.4393      0.987 0.000 0.748 0.208 0.012 0.032
#&gt; SRR1740071     2  0.4393      0.987 0.000 0.748 0.208 0.012 0.032
#&gt; SRR1740072     2  0.4393      0.987 0.000 0.748 0.208 0.012 0.032
#&gt; SRR1740073     2  0.4393      0.987 0.000 0.748 0.208 0.012 0.032
#&gt; SRR1740074     3  0.6627      0.379 0.320 0.128 0.524 0.028 0.000
#&gt; SRR1740075     3  0.6627      0.379 0.320 0.128 0.524 0.028 0.000
#&gt; SRR1740076     3  0.6425      0.379 0.332 0.128 0.524 0.016 0.000
#&gt; SRR1740077     3  0.6425      0.379 0.332 0.128 0.524 0.016 0.000
#&gt; SRR1740078     5  0.0324      0.499 0.004 0.004 0.000 0.000 0.992
#&gt; SRR1740079     5  0.0324      0.499 0.004 0.004 0.000 0.000 0.992
#&gt; SRR1740080     5  0.0290      0.499 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1740081     5  0.0290      0.499 0.000 0.008 0.000 0.000 0.992
#&gt; SRR1740082     5  0.8505      0.257 0.180 0.228 0.004 0.220 0.368
#&gt; SRR1740083     5  0.8505      0.257 0.180 0.228 0.004 0.220 0.368
#&gt; SRR1740084     5  0.8505      0.257 0.180 0.228 0.004 0.220 0.368
#&gt; SRR1740085     5  0.8505      0.257 0.180 0.228 0.004 0.220 0.368
#&gt; SRR1740086     1  0.7162      0.976 0.504 0.048 0.000 0.180 0.268
#&gt; SRR1740087     1  0.7162      0.976 0.504 0.048 0.000 0.180 0.268
#&gt; SRR1740088     1  0.7162      0.976 0.504 0.048 0.000 0.180 0.268
#&gt; SRR1740089     1  0.7162      0.976 0.504 0.048 0.000 0.180 0.268
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4   0.201      0.917 0.000 0.004 0.000 0.892 0.000 0.104
#&gt; SRR1740035     4   0.201      0.917 0.000 0.004 0.000 0.892 0.000 0.104
#&gt; SRR1740036     4   0.201      0.917 0.000 0.004 0.000 0.892 0.000 0.104
#&gt; SRR1740037     4   0.240      0.916 0.000 0.004 0.008 0.880 0.004 0.104
#&gt; SRR1740038     1   0.450      0.996 0.552 0.424 0.008 0.000 0.004 0.012
#&gt; SRR1740039     1   0.445      0.996 0.552 0.424 0.012 0.000 0.000 0.012
#&gt; SRR1740040     1   0.450      0.996 0.552 0.424 0.008 0.000 0.004 0.012
#&gt; SRR1740041     1   0.445      0.996 0.552 0.424 0.012 0.000 0.000 0.012
#&gt; SRR1740042     2   0.135      0.600 0.024 0.952 0.000 0.000 0.008 0.016
#&gt; SRR1740043     2   0.135      0.599 0.024 0.952 0.000 0.008 0.000 0.016
#&gt; SRR1740044     2   0.135      0.600 0.024 0.952 0.000 0.000 0.008 0.016
#&gt; SRR1740045     2   0.135      0.600 0.024 0.952 0.000 0.000 0.008 0.016
#&gt; SRR1740046     3   0.358      0.895 0.004 0.244 0.740 0.012 0.000 0.000
#&gt; SRR1740048     3   0.351      0.895 0.000 0.248 0.740 0.004 0.008 0.000
#&gt; SRR1740047     3   0.351      0.895 0.000 0.248 0.740 0.004 0.008 0.000
#&gt; SRR1740049     3   0.358      0.895 0.004 0.244 0.740 0.012 0.000 0.000
#&gt; SRR1740050     5   0.399      0.930 0.000 0.000 0.000 0.024 0.676 0.300
#&gt; SRR1740051     5   0.399      0.930 0.000 0.000 0.000 0.024 0.676 0.300
#&gt; SRR1740052     5   0.399      0.930 0.000 0.000 0.000 0.024 0.676 0.300
#&gt; SRR1740054     6   0.311      0.639 0.024 0.036 0.000 0.076 0.004 0.860
#&gt; SRR1740053     5   0.420      0.930 0.004 0.000 0.000 0.028 0.668 0.300
#&gt; SRR1740056     6   0.311      0.639 0.024 0.036 0.000 0.076 0.004 0.860
#&gt; SRR1740055     6   0.311      0.639 0.024 0.036 0.000 0.076 0.004 0.860
#&gt; SRR1740057     6   0.311      0.639 0.024 0.036 0.000 0.076 0.004 0.860
#&gt; SRR1740058     6   0.590      0.655 0.240 0.000 0.024 0.028 0.096 0.612
#&gt; SRR1740059     6   0.593      0.655 0.240 0.000 0.024 0.032 0.092 0.612
#&gt; SRR1740060     6   0.593      0.655 0.240 0.000 0.024 0.032 0.092 0.612
#&gt; SRR1740061     6   0.590      0.655 0.240 0.000 0.024 0.028 0.096 0.612
#&gt; SRR1740062     4   0.551      0.916 0.084 0.004 0.040 0.716 0.052 0.104
#&gt; SRR1740063     4   0.551      0.916 0.084 0.004 0.040 0.716 0.052 0.104
#&gt; SRR1740064     4   0.551      0.916 0.084 0.004 0.044 0.716 0.048 0.104
#&gt; SRR1740065     4   0.549      0.916 0.088 0.004 0.036 0.716 0.052 0.104
#&gt; SRR1740066     2   0.629     -0.748 0.428 0.452 0.056 0.024 0.028 0.012
#&gt; SRR1740067     2   0.629     -0.748 0.428 0.452 0.056 0.024 0.028 0.012
#&gt; SRR1740068     2   0.629     -0.748 0.428 0.452 0.056 0.024 0.028 0.012
#&gt; SRR1740069     2   0.629     -0.748 0.428 0.452 0.056 0.024 0.028 0.012
#&gt; SRR1740070     2   0.131      0.604 0.000 0.952 0.000 0.004 0.028 0.016
#&gt; SRR1740071     2   0.131      0.604 0.000 0.952 0.000 0.004 0.028 0.016
#&gt; SRR1740072     2   0.131      0.604 0.000 0.952 0.000 0.004 0.028 0.016
#&gt; SRR1740073     2   0.131      0.604 0.000 0.952 0.000 0.004 0.028 0.016
#&gt; SRR1740074     3   0.650      0.895 0.060 0.252 0.564 0.028 0.096 0.000
#&gt; SRR1740075     3   0.650      0.895 0.060 0.252 0.564 0.028 0.096 0.000
#&gt; SRR1740076     3   0.642      0.895 0.056 0.252 0.564 0.020 0.108 0.000
#&gt; SRR1740077     3   0.642      0.895 0.056 0.252 0.564 0.020 0.108 0.000
#&gt; SRR1740078     5   0.635      0.930 0.032 0.000 0.064 0.056 0.548 0.300
#&gt; SRR1740079     5   0.635      0.930 0.032 0.000 0.064 0.056 0.548 0.300
#&gt; SRR1740080     5   0.634      0.930 0.028 0.000 0.068 0.056 0.548 0.300
#&gt; SRR1740081     5   0.637      0.929 0.036 0.000 0.060 0.056 0.548 0.300
#&gt; SRR1740082     6   0.294      0.639 0.004 0.036 0.016 0.076 0.000 0.868
#&gt; SRR1740083     6   0.294      0.639 0.004 0.036 0.016 0.076 0.000 0.868
#&gt; SRR1740084     6   0.294      0.639 0.004 0.036 0.016 0.076 0.000 0.868
#&gt; SRR1740085     6   0.294      0.639 0.004 0.036 0.016 0.076 0.000 0.868
#&gt; SRR1740086     6   0.609      0.655 0.180 0.000 0.060 0.028 0.096 0.636
#&gt; SRR1740087     6   0.609      0.655 0.180 0.000 0.060 0.028 0.096 0.636
#&gt; SRR1740088     6   0.611      0.655 0.176 0.000 0.064 0.028 0.096 0.636
#&gt; SRR1740089     6   0.611      0.655 0.176 0.000 0.064 0.028 0.096 0.636
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.997       0.998         0.4992 0.501   0.501
#> 3 3 0.875           0.951       0.959         0.2661 0.875   0.751
#> 4 4 0.834           0.923       0.901         0.1234 0.917   0.779
#> 5 5 0.917           0.957       0.953         0.1097 0.917   0.717
#> 6 6 0.917           0.970       0.941         0.0552 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740035     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740036     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740037     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740046     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740048     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740047     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740049     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740050     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740054     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740053     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740056     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740055     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740057     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740058     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740062     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740063     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740064     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740065     1  0.0938      0.991 0.988 0.012
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740074     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740075     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740076     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740077     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740078     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740082     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740083     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740084     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740085     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740086     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.997 1.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1   p2    p3
#&gt; SRR1740034     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740035     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740036     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740037     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740038     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740039     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740040     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740041     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740042     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740043     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740044     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740045     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740046     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740048     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740047     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740049     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740050     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740051     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740052     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740054     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740053     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740056     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740055     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740057     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740058     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740059     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740060     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740061     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740062     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740063     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740064     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740065     3   0.141      1.000 0.036 0.00 0.964
#&gt; SRR1740066     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740067     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740068     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740069     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740070     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740071     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740072     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740073     2   0.000      0.972 0.000 1.00 0.000
#&gt; SRR1740074     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740075     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740076     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740077     2   0.254      0.942 0.000 0.92 0.080
#&gt; SRR1740078     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740079     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740080     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740081     1   0.355      0.896 0.868 0.00 0.132
#&gt; SRR1740082     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740083     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740084     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740085     1   0.000      0.939 1.000 0.00 0.000
#&gt; SRR1740086     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740087     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740088     1   0.141      0.934 0.964 0.00 0.036
#&gt; SRR1740089     1   0.141      0.934 0.964 0.00 0.036
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740035     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740036     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740037     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740038     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740039     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740040     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740041     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740042     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740043     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740044     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740045     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740046     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740048     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740047     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740049     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740050     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740051     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740052     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740054     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740053     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740056     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740055     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740057     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740058     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740059     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740060     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740061     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740062     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740063     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740064     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740065     4  0.0188      1.000 0.004 0.000 0.000 0.996
#&gt; SRR1740066     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740067     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740068     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740069     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR1740070     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740071     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740072     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740073     2  0.0336      0.994 0.000 0.992 0.008 0.000
#&gt; SRR1740074     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740075     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740076     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740077     3  0.4584      1.000 0.000 0.300 0.696 0.004
#&gt; SRR1740078     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740079     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740080     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740081     1  0.5883      0.730 0.648 0.000 0.288 0.064
#&gt; SRR1740082     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740083     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740084     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740085     1  0.0592      0.871 0.984 0.000 0.016 0.000
#&gt; SRR1740086     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740087     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740088     1  0.0469      0.872 0.988 0.000 0.000 0.012
#&gt; SRR1740089     1  0.0469      0.872 0.988 0.000 0.000 0.012
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740038     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740039     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740040     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740041     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740042     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740043     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740044     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740045     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740046     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740048     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740047     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740049     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740050     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740051     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740052     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740054     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740053     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740056     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740055     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740057     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740058     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740059     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740060     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740061     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740066     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740067     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740068     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740069     2  0.0000      0.973 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740070     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740071     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740072     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740073     2  0.1469      0.973 0.000 0.948 0.036 0.000 0.016
#&gt; SRR1740074     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740075     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740076     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740077     3  0.0963      1.000 0.000 0.036 0.964 0.000 0.000
#&gt; SRR1740078     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740079     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740080     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740081     5  0.0510      1.000 0.016 0.000 0.000 0.000 0.984
#&gt; SRR1740082     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740083     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740084     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740085     1  0.0162      0.880 0.996 0.000 0.000 0.000 0.004
#&gt; SRR1740086     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740087     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740088     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
#&gt; SRR1740089     1  0.4586      0.872 0.780 0.000 0.036 0.056 0.128
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740038     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740039     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740040     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740041     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740042     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740043     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740044     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740045     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740050     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740051     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740052     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740054     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740053     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740056     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740055     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740057     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740058     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740059     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740060     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740061     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740066     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740067     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740068     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740069     2  0.3390      0.896 0.152 0.808 0.000 0.000 0.032 0.008
#&gt; SRR1740070     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740071     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740072     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740073     2  0.0713      0.895 0.000 0.972 0.028 0.000 0.000 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740078     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740079     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740080     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740081     5  0.0790      1.000 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR1740082     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740083     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740084     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740085     1  0.2378      1.000 0.848 0.000 0.000 0.000 0.000 0.152
#&gt; SRR1740086     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740087     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740088     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
#&gt; SRR1740089     6  0.0260      1.000 0.000 0.000 0.000 0.008 0.000 0.992
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.997         0.4965 0.501   0.501
#> 3 3 0.792           0.910       0.859         0.2138 0.875   0.751
#> 4 4 1.000           0.998       0.998         0.1729 0.917   0.779
#> 5 5 1.000           0.991       0.996         0.1168 0.897   0.660
#> 6 6 0.917           0.975       0.940         0.0533 0.949   0.762
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 4 5
```

There is also optional best $k$ = 2 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740035     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740036     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740037     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740038     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740039     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740040     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740041     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740042     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740043     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740044     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740045     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740046     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740048     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740047     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740049     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740050     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740051     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740052     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740054     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740053     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740056     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740055     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740057     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740058     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740059     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740060     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740061     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740062     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740063     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740064     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740065     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740066     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740067     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740068     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740069     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740070     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740071     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740072     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740073     2  0.0938      0.996 0.012 0.988
#&gt; SRR1740074     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740075     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740076     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740077     2  0.0000      0.992 0.000 1.000
#&gt; SRR1740078     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740079     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740080     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740081     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740082     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740083     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740084     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740085     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740086     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740087     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740088     1  0.0000      1.000 1.000 0.000
#&gt; SRR1740089     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740035     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740036     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740037     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740038     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740039     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740040     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740041     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740042     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740043     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740044     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740045     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740046     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740048     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740047     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740049     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740050     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740051     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740052     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740054     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740053     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740056     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740055     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740057     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740058     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740059     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740060     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740061     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740062     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740063     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740064     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740065     3   0.630      1.000 0.484 0.000 0.516
#&gt; SRR1740066     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740067     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740068     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740069     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740070     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740071     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740072     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740073     2   0.668      0.851 0.008 0.508 0.484
#&gt; SRR1740074     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740075     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740076     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740077     2   0.000      0.670 0.000 1.000 0.000
#&gt; SRR1740078     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740079     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740080     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740081     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740082     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740083     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740084     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740085     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740086     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740087     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740088     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740089     1   0.000      1.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3 p4
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740046     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740048     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740047     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740049     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740050     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740051     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740052     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740054     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740053     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740056     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740055     1  0.0336      0.991 0.992 0.008 0.000  0
#&gt; SRR1740057     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740058     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740059     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740060     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740061     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000 0.000  1
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000 0.000  0
#&gt; SRR1740074     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740075     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740076     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740077     3  0.0336      1.000 0.000 0.008 0.992  0
#&gt; SRR1740078     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740079     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740080     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740081     1  0.0336      0.995 0.992 0.000 0.008  0
#&gt; SRR1740082     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740083     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740084     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740085     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740086     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740087     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740088     1  0.0000      0.997 1.000 0.000 0.000  0
#&gt; SRR1740089     1  0.0000      0.997 1.000 0.000 0.000  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740038     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740039     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740040     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740041     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740042     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740043     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740044     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740045     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740050     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740051     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740052     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740054     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740053     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740056     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740055     2   0.314      0.740 0.204 0.796  0  0  0
#&gt; SRR1740057     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740058     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740059     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740060     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740061     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0  1  0
#&gt; SRR1740066     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740067     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740068     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740069     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740070     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740071     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740072     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740073     2   0.000      0.985 0.000 1.000  0  0  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1  0  0
#&gt; SRR1740078     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740079     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740080     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740081     5   0.000      1.000 0.000 0.000  0  0  1
#&gt; SRR1740082     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740083     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740084     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740085     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740086     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740087     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740088     1   0.000      1.000 1.000 0.000  0  0  0
#&gt; SRR1740089     1   0.000      1.000 1.000 0.000  0  0  0
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5    p6
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740038     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740039     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740040     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740041     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740042     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740043     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740044     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740045     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740050     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740051     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740052     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740054     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740053     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740056     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740055     1  0.0146      0.994 0.996 0.000  0  0  0 0.004
#&gt; SRR1740057     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740058     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740059     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740060     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740061     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740066     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740067     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740068     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740069     2  0.0000      0.913 0.000 1.000  0  0  0 0.000
#&gt; SRR1740070     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740071     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740072     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740073     2  0.2697      0.913 0.000 0.812  0  0  0 0.188
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740078     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740079     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740080     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740081     5  0.0000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740082     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740083     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740084     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740085     1  0.0000      0.999 1.000 0.000  0  0  0 0.000
#&gt; SRR1740086     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740087     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740088     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
#&gt; SRR1740089     6  0.2697      1.000 0.188 0.000  0  0  0 0.812
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2     1           0.984       0.988         0.4971 0.501   0.501
#> 3 3     1           0.996       0.997         0.3345 0.751   0.541
#> 4 4     1           1.000       1.000         0.0655 0.958   0.876
#> 5 5     1           0.994       0.994         0.1175 0.917   0.717
#> 6 6     1           0.998       0.995         0.0522 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4 5
```

There is also optional best $k$ = 2 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740035     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740036     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740037     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740038     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740039     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740040     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740041     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740042     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740043     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740044     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740045     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740046     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740048     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740047     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740049     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740050     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740054     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740053     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740056     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740055     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740057     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740058     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740062     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740063     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740064     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740065     1  0.2778      0.963 0.952 0.048
#&gt; SRR1740066     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740067     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740068     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740069     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740070     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740071     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740072     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740073     2  0.0376      0.991 0.004 0.996
#&gt; SRR1740074     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740075     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740076     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740077     2  0.1633      0.982 0.024 0.976
#&gt; SRR1740078     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740082     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740083     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740084     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740085     1  0.0376      0.986 0.996 0.004
#&gt; SRR1740086     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.987 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.987 1.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1740034     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740035     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740036     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740037     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740038     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740046     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740048     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740047     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740049     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740050     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740051     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740052     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740054     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740053     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740056     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740055     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740057     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740058     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740059     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740060     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740061     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740062     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740063     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740064     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740065     3   0.103      0.986 0.024  0 0.976
#&gt; SRR1740066     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740074     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740075     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740076     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740077     3   0.000      0.986 0.000  0 1.000
#&gt; SRR1740078     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740079     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740080     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740081     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740082     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740083     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740084     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740085     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740086     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740087     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740088     1   0.000      1.000 1.000  0 0.000
#&gt; SRR1740089     1   0.000      1.000 1.000  0 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1740034     4       0          1  0  0  0  1
#&gt; SRR1740035     4       0          1  0  0  0  1
#&gt; SRR1740036     4       0          1  0  0  0  1
#&gt; SRR1740037     4       0          1  0  0  0  1
#&gt; SRR1740038     2       0          1  0  1  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0
#&gt; SRR1740048     3       0          1  0  0  1  0
#&gt; SRR1740047     3       0          1  0  0  1  0
#&gt; SRR1740049     3       0          1  0  0  1  0
#&gt; SRR1740050     1       0          1  1  0  0  0
#&gt; SRR1740051     1       0          1  1  0  0  0
#&gt; SRR1740052     1       0          1  1  0  0  0
#&gt; SRR1740054     1       0          1  1  0  0  0
#&gt; SRR1740053     1       0          1  1  0  0  0
#&gt; SRR1740056     1       0          1  1  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0
#&gt; SRR1740058     1       0          1  1  0  0  0
#&gt; SRR1740059     1       0          1  1  0  0  0
#&gt; SRR1740060     1       0          1  1  0  0  0
#&gt; SRR1740061     1       0          1  1  0  0  0
#&gt; SRR1740062     4       0          1  0  0  0  1
#&gt; SRR1740063     4       0          1  0  0  0  1
#&gt; SRR1740064     4       0          1  0  0  0  1
#&gt; SRR1740065     4       0          1  0  0  0  1
#&gt; SRR1740066     2       0          1  0  1  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0
#&gt; SRR1740075     3       0          1  0  0  1  0
#&gt; SRR1740076     3       0          1  0  0  1  0
#&gt; SRR1740077     3       0          1  0  0  1  0
#&gt; SRR1740078     1       0          1  1  0  0  0
#&gt; SRR1740079     1       0          1  1  0  0  0
#&gt; SRR1740080     1       0          1  1  0  0  0
#&gt; SRR1740081     1       0          1  1  0  0  0
#&gt; SRR1740082     1       0          1  1  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0
#&gt; SRR1740086     1       0          1  1  0  0  0
#&gt; SRR1740087     1       0          1  1  0  0  0
#&gt; SRR1740088     1       0          1  1  0  0  0
#&gt; SRR1740089     1       0          1  1  0  0  0
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1 p2 p3 p4   p5
#&gt; SRR1740034     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740035     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740036     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740037     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740038     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740039     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740040     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740041     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740042     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740043     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740044     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740045     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740046     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740048     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740047     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740049     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740050     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740051     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740052     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740054     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740053     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740056     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740055     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740057     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740058     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740059     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740060     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740061     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740062     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740063     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740064     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740065     4   0.000      1.000 0.00  0  0  1 0.00
#&gt; SRR1740066     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740067     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740068     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740069     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740070     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740071     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740072     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740073     2   0.000      1.000 0.00  1  0  0 0.00
#&gt; SRR1740074     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740075     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740076     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740077     3   0.000      1.000 0.00  0  1  0 0.00
#&gt; SRR1740078     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740079     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740080     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740081     5   0.000      0.978 0.00  0  0  0 1.00
#&gt; SRR1740082     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740083     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740084     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740085     1   0.000      1.000 1.00  0  0  0 0.00
#&gt; SRR1740086     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740087     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740088     5   0.104      0.978 0.04  0  0  0 0.96
#&gt; SRR1740089     5   0.104      0.978 0.04  0  0  0 0.96
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4   p5    p6
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740038     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740039     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740040     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740041     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740042     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740043     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740044     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740045     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740050     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740051     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740052     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740054     1  0.0000      0.998 1.000 0.000  0  0 0.00 0.000
#&gt; SRR1740053     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740056     1  0.0000      0.998 1.000 0.000  0  0 0.00 0.000
#&gt; SRR1740055     1  0.0000      0.998 1.000 0.000  0  0 0.00 0.000
#&gt; SRR1740057     1  0.0260      0.996 0.992 0.000  0  0 0.00 0.008
#&gt; SRR1740058     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740059     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740060     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740061     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000  0  1 0.00 0.000
#&gt; SRR1740066     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740067     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740068     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740069     2  0.0000      0.995 0.000 1.000  0  0 0.00 0.000
#&gt; SRR1740070     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740071     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740072     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740073     2  0.0363      0.995 0.000 0.988  0  0 0.00 0.012
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1  0 0.00 0.000
#&gt; SRR1740078     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740079     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740080     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740081     5  0.0000      1.000 0.000 0.000  0  0 1.00 0.000
#&gt; SRR1740082     1  0.0260      0.996 0.992 0.000  0  0 0.00 0.008
#&gt; SRR1740083     1  0.0000      0.998 1.000 0.000  0  0 0.00 0.000
#&gt; SRR1740084     1  0.0000      0.998 1.000 0.000  0  0 0.00 0.000
#&gt; SRR1740085     1  0.0260      0.996 0.992 0.000  0  0 0.00 0.008
#&gt; SRR1740086     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740087     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740088     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
#&gt; SRR1740089     6  0.0547      1.000 0.000 0.000  0  0 0.02 0.980
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.938           0.969       0.969         0.4968 0.501   0.501
#> 3 3 0.792           0.911       0.885         0.2335 0.875   0.751
#> 4 4 0.834           0.954       0.930         0.1544 0.917   0.779
#> 5 5 0.878           0.962       0.947         0.1095 0.917   0.717
#> 6 6 0.925           0.839       0.874         0.0625 0.918   0.635
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740035     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740036     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740037     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740038     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740039     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740040     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740041     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740042     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740043     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740044     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740045     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740046     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740048     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740047     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740049     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740050     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740051     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740052     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740054     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740053     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740056     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740055     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740057     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740058     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740062     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740063     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740064     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740065     1  0.4562      0.934 0.904 0.096
#&gt; SRR1740066     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740067     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740068     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740069     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740070     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740071     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740072     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740073     2  0.2043      0.981 0.032 0.968
#&gt; SRR1740074     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740075     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740076     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740077     2  0.2603      0.962 0.044 0.956
#&gt; SRR1740078     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740079     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740080     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740081     1  0.0672      0.975 0.992 0.008
#&gt; SRR1740082     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740083     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740084     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740085     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740086     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.976 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.976 1.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740035     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740036     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740037     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740038     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740042     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740043     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740044     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740045     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740046     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740048     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740047     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740049     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740050     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740051     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740052     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740054     1  0.6252      0.984 0.648 0.008 0.344
#&gt; SRR1740053     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740056     1  0.6081      0.986 0.652 0.004 0.344
#&gt; SRR1740055     1  0.6962      0.944 0.648 0.036 0.316
#&gt; SRR1740057     1  0.6081      0.986 0.652 0.004 0.344
#&gt; SRR1740058     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740059     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740060     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740061     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740062     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740063     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740064     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740065     3  0.0747      1.000 0.000 0.016 0.984
#&gt; SRR1740066     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740070     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740071     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740072     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740073     2  0.0000      0.865 0.000 1.000 0.000
#&gt; SRR1740074     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740075     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740076     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740077     2  0.7885      0.693 0.352 0.580 0.068
#&gt; SRR1740078     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740079     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740080     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740081     1  0.6081      0.982 0.652 0.004 0.344
#&gt; SRR1740082     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740083     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740084     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740085     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740086     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740087     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740088     1  0.6057      0.988 0.656 0.004 0.340
#&gt; SRR1740089     1  0.6057      0.988 0.656 0.004 0.340
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740035     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740036     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740037     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740038     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740039     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740040     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740041     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740042     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740043     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740044     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740045     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740046     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740048     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740047     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740049     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740050     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740051     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740052     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740054     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740053     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740056     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740055     1  0.0921      0.903 0.972 0.028 0.000 0.000
#&gt; SRR1740057     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740058     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740059     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740060     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740061     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740062     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740063     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740064     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740065     4  0.0336      1.000 0.000 0.008 0.000 0.992
#&gt; SRR1740066     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740067     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740068     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740069     2  0.0188      0.998 0.000 0.996 0.004 0.000
#&gt; SRR1740070     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740071     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740072     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740073     2  0.0000      0.998 0.000 1.000 0.000 0.000
#&gt; SRR1740074     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740075     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740076     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740077     3  0.4364      1.000 0.000 0.220 0.764 0.016
#&gt; SRR1740078     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740079     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740080     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740081     1  0.4228      0.837 0.760 0.000 0.232 0.008
#&gt; SRR1740082     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740083     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740084     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740085     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740086     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740087     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740088     1  0.0000      0.922 1.000 0.000 0.000 0.000
#&gt; SRR1740089     1  0.0000      0.922 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740035     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740036     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740037     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740038     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740039     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740040     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740041     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740042     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740043     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740044     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740045     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740050     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740051     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740052     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740054     1  0.0771      0.949 0.976 0.020 0.000 0.004 0.000
#&gt; SRR1740053     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740056     1  0.0162      0.960 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1740055     1  0.3398      0.706 0.780 0.216 0.000 0.004 0.000
#&gt; SRR1740057     1  0.0162      0.960 0.996 0.000 0.000 0.004 0.000
#&gt; SRR1740058     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740059     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740060     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740061     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740062     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740063     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740064     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740065     4  0.0290      1.000 0.000 0.000 0.008 0.992 0.000
#&gt; SRR1740066     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740067     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740068     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740069     2  0.2806      0.928 0.000 0.844 0.000 0.004 0.152
#&gt; SRR1740070     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740071     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740072     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740073     2  0.0000      0.928 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740078     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740079     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740080     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740081     5  0.2648      1.000 0.152 0.000 0.000 0.000 0.848
#&gt; SRR1740082     1  0.1571      0.915 0.936 0.060 0.000 0.004 0.000
#&gt; SRR1740083     1  0.1430      0.923 0.944 0.052 0.000 0.004 0.000
#&gt; SRR1740084     1  0.0865      0.947 0.972 0.024 0.000 0.004 0.000
#&gt; SRR1740085     1  0.0451      0.957 0.988 0.008 0.000 0.004 0.000
#&gt; SRR1740086     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740087     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740088     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
#&gt; SRR1740089     1  0.0290      0.962 0.992 0.000 0.000 0.000 0.008
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4  0.0260     0.9968 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1740035     4  0.0260     0.9968 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1740036     4  0.0260     0.9968 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1740037     4  0.0260     0.9968 0.008 0.000 0.000 0.992 0.000 0.000
#&gt; SRR1740038     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740039     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740040     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740041     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740042     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740043     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740044     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740045     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740046     3  0.0146     0.9984 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1740048     3  0.0146     0.9984 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1740047     3  0.0146     0.9984 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1740049     3  0.0146     0.9984 0.000 0.000 0.996 0.000 0.004 0.000
#&gt; SRR1740050     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740051     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740052     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740054     1  0.2996    -0.0124 0.772 0.000 0.000 0.000 0.000 0.228
#&gt; SRR1740053     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740056     6  0.3797     0.6588 0.420 0.000 0.000 0.000 0.000 0.580
#&gt; SRR1740055     1  0.1471     0.3423 0.932 0.004 0.000 0.000 0.000 0.064
#&gt; SRR1740057     6  0.3695     0.6944 0.376 0.000 0.000 0.000 0.000 0.624
#&gt; SRR1740058     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740059     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740060     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740061     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740062     4  0.0000     0.9968 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740063     4  0.0000     0.9968 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740064     4  0.0000     0.9968 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740065     4  0.0000     0.9968 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR1740066     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740067     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740068     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740069     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740070     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740071     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740072     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740073     1  0.3774     0.6595 0.592 0.408 0.000 0.000 0.000 0.000
#&gt; SRR1740074     3  0.0000     0.9984 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740075     3  0.0000     0.9984 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740076     3  0.0000     0.9984 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740077     3  0.0000     0.9984 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR1740078     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740079     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740080     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740081     5  0.0146     1.0000 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR1740082     1  0.3854    -0.5557 0.536 0.000 0.000 0.000 0.000 0.464
#&gt; SRR1740083     6  0.3851     0.6071 0.460 0.000 0.000 0.000 0.000 0.540
#&gt; SRR1740084     6  0.3774     0.6709 0.408 0.000 0.000 0.000 0.000 0.592
#&gt; SRR1740085     6  0.3717     0.6897 0.384 0.000 0.000 0.000 0.000 0.616
#&gt; SRR1740086     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740087     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740088     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR1740089     6  0.0000     0.8290 0.000 0.000 0.000 0.000 0.000 1.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.751           0.924       0.960         0.4992 0.501   0.501
#> 3 3 0.792           0.921       0.960         0.1896 0.917   0.834
#> 4 4 0.834           0.928       0.960         0.1902 0.875   0.702
#> 5 5 0.917           0.983       0.985         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 5
```

There is also optional best $k$ = 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1   p2
#&gt; SRR1740034     1   0.000      0.923 1.00 0.00
#&gt; SRR1740035     1   0.000      0.923 1.00 0.00
#&gt; SRR1740036     1   0.000      0.923 1.00 0.00
#&gt; SRR1740037     1   0.000      0.923 1.00 0.00
#&gt; SRR1740038     2   0.000      1.000 0.00 1.00
#&gt; SRR1740039     2   0.000      1.000 0.00 1.00
#&gt; SRR1740040     2   0.000      1.000 0.00 1.00
#&gt; SRR1740041     2   0.000      1.000 0.00 1.00
#&gt; SRR1740042     2   0.000      1.000 0.00 1.00
#&gt; SRR1740043     2   0.000      1.000 0.00 1.00
#&gt; SRR1740044     2   0.000      1.000 0.00 1.00
#&gt; SRR1740045     2   0.000      1.000 0.00 1.00
#&gt; SRR1740046     2   0.000      1.000 0.00 1.00
#&gt; SRR1740048     2   0.000      1.000 0.00 1.00
#&gt; SRR1740047     2   0.000      1.000 0.00 1.00
#&gt; SRR1740049     2   0.000      1.000 0.00 1.00
#&gt; SRR1740050     1   0.000      0.923 1.00 0.00
#&gt; SRR1740051     1   0.000      0.923 1.00 0.00
#&gt; SRR1740052     1   0.000      0.923 1.00 0.00
#&gt; SRR1740054     1   0.855      0.699 0.72 0.28
#&gt; SRR1740053     1   0.000      0.923 1.00 0.00
#&gt; SRR1740056     1   0.855      0.699 0.72 0.28
#&gt; SRR1740055     1   0.855      0.699 0.72 0.28
#&gt; SRR1740057     1   0.855      0.699 0.72 0.28
#&gt; SRR1740058     1   0.000      0.923 1.00 0.00
#&gt; SRR1740059     1   0.000      0.923 1.00 0.00
#&gt; SRR1740060     1   0.000      0.923 1.00 0.00
#&gt; SRR1740061     1   0.000      0.923 1.00 0.00
#&gt; SRR1740062     1   0.000      0.923 1.00 0.00
#&gt; SRR1740063     1   0.000      0.923 1.00 0.00
#&gt; SRR1740064     1   0.000      0.923 1.00 0.00
#&gt; SRR1740065     1   0.000      0.923 1.00 0.00
#&gt; SRR1740066     2   0.000      1.000 0.00 1.00
#&gt; SRR1740067     2   0.000      1.000 0.00 1.00
#&gt; SRR1740068     2   0.000      1.000 0.00 1.00
#&gt; SRR1740069     2   0.000      1.000 0.00 1.00
#&gt; SRR1740070     2   0.000      1.000 0.00 1.00
#&gt; SRR1740071     2   0.000      1.000 0.00 1.00
#&gt; SRR1740072     2   0.000      1.000 0.00 1.00
#&gt; SRR1740073     2   0.000      1.000 0.00 1.00
#&gt; SRR1740074     2   0.000      1.000 0.00 1.00
#&gt; SRR1740075     2   0.000      1.000 0.00 1.00
#&gt; SRR1740076     2   0.000      1.000 0.00 1.00
#&gt; SRR1740077     2   0.000      1.000 0.00 1.00
#&gt; SRR1740078     1   0.000      0.923 1.00 0.00
#&gt; SRR1740079     1   0.000      0.923 1.00 0.00
#&gt; SRR1740080     1   0.000      0.923 1.00 0.00
#&gt; SRR1740081     1   0.000      0.923 1.00 0.00
#&gt; SRR1740082     1   0.855      0.699 0.72 0.28
#&gt; SRR1740083     1   0.855      0.699 0.72 0.28
#&gt; SRR1740084     1   0.855      0.699 0.72 0.28
#&gt; SRR1740085     1   0.855      0.699 0.72 0.28
#&gt; SRR1740086     1   0.000      0.923 1.00 0.00
#&gt; SRR1740087     1   0.000      0.923 1.00 0.00
#&gt; SRR1740088     1   0.000      0.923 1.00 0.00
#&gt; SRR1740089     1   0.000      0.923 1.00 0.00
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1   p2 p3
#&gt; SRR1740034     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740035     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740036     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740037     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740038     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740039     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740040     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740041     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740042     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740043     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740044     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740045     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740046     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740048     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740047     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740049     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740050     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740051     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740052     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740054     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740053     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740056     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740055     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740057     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740058     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740059     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740060     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740061     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740062     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740063     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740064     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740065     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740066     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740067     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740068     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740069     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740070     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740071     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740072     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740073     2    0.00      1.000 0.00 1.00  0
#&gt; SRR1740074     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740075     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740076     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740077     3    0.00      1.000 0.00 0.00  1
#&gt; SRR1740078     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740079     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740080     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740081     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740082     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740083     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740084     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740085     1    0.54      0.699 0.72 0.28  0
#&gt; SRR1740086     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740087     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740088     1    0.00      0.917 1.00 0.00  0
#&gt; SRR1740089     1    0.00      0.917 1.00 0.00  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1   p2 p3 p4
#&gt; SRR1740034     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740035     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740036     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740037     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740038     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740039     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740040     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740041     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740042     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740043     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740044     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740045     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740046     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740048     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740047     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740049     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740050     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740051     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740052     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740054     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740053     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740056     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740055     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740057     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740058     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740059     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740060     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740061     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740062     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740063     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740064     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740065     4   0.000      1.000 0.00 0.00  0  1
#&gt; SRR1740066     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740067     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740068     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740069     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740070     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740071     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740072     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740073     2   0.000      1.000 0.00 1.00  0  0
#&gt; SRR1740074     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740075     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740076     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740077     3   0.000      1.000 0.00 0.00  1  0
#&gt; SRR1740078     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740079     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740080     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740081     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740082     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740083     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740084     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740085     1   0.428      0.729 0.72 0.28  0  0
#&gt; SRR1740086     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740087     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740088     1   0.000      0.884 1.00 0.00  0  0
#&gt; SRR1740089     1   0.000      0.884 1.00 0.00  0  0
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3 p4    p5
#&gt; SRR1740034     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740035     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740036     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740037     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740038     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740050     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740051     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740052     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740054     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740053     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740056     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740055     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740057     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740058     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740059     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740060     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740061     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740062     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740063     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740064     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740065     4   0.000      1.000 0.000  0  0  1 0.000
#&gt; SRR1740066     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000  1  0  0 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000  0  1  0 0.000
#&gt; SRR1740078     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740079     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740080     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740081     5   0.207      0.938 0.104  0  0  0 0.896
#&gt; SRR1740082     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740083     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740084     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740085     1   0.000      1.000 1.000  0  0  0 0.000
#&gt; SRR1740086     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740087     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740088     5   0.000      0.941 0.000  0  0  0 1.000
#&gt; SRR1740089     5   0.000      0.941 0.000  0  0  0 1.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.584           0.933       0.938         0.4564 0.501   0.501
#> 3 3 0.584           0.780       0.799         0.3269 1.000   1.000
#> 4 4 0.532           0.770       0.772         0.1335 0.792   0.585
#> 5 5 0.605           0.759       0.684         0.0900 0.917   0.717
#> 6 6 0.647           0.890       0.700         0.0598 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.000      0.971 1.000 0.000
#&gt; SRR1740035     1   0.000      0.971 1.000 0.000
#&gt; SRR1740036     1   0.000      0.971 1.000 0.000
#&gt; SRR1740037     1   0.000      0.971 1.000 0.000
#&gt; SRR1740038     2   0.662      0.924 0.172 0.828
#&gt; SRR1740039     2   0.662      0.924 0.172 0.828
#&gt; SRR1740040     2   0.662      0.924 0.172 0.828
#&gt; SRR1740041     2   0.662      0.924 0.172 0.828
#&gt; SRR1740042     2   0.662      0.924 0.172 0.828
#&gt; SRR1740043     2   0.662      0.924 0.172 0.828
#&gt; SRR1740044     2   0.662      0.924 0.172 0.828
#&gt; SRR1740045     2   0.662      0.924 0.172 0.828
#&gt; SRR1740046     2   0.000      0.863 0.000 1.000
#&gt; SRR1740048     2   0.000      0.863 0.000 1.000
#&gt; SRR1740047     2   0.000      0.863 0.000 1.000
#&gt; SRR1740049     2   0.000      0.863 0.000 1.000
#&gt; SRR1740050     1   0.000      0.971 1.000 0.000
#&gt; SRR1740051     1   0.000      0.971 1.000 0.000
#&gt; SRR1740052     1   0.000      0.971 1.000 0.000
#&gt; SRR1740054     1   0.443      0.907 0.908 0.092
#&gt; SRR1740053     1   0.000      0.971 1.000 0.000
#&gt; SRR1740056     1   0.443      0.907 0.908 0.092
#&gt; SRR1740055     1   0.443      0.907 0.908 0.092
#&gt; SRR1740057     1   0.443      0.907 0.908 0.092
#&gt; SRR1740058     1   0.000      0.971 1.000 0.000
#&gt; SRR1740059     1   0.000      0.971 1.000 0.000
#&gt; SRR1740060     1   0.000      0.971 1.000 0.000
#&gt; SRR1740061     1   0.000      0.971 1.000 0.000
#&gt; SRR1740062     1   0.000      0.971 1.000 0.000
#&gt; SRR1740063     1   0.000      0.971 1.000 0.000
#&gt; SRR1740064     1   0.000      0.971 1.000 0.000
#&gt; SRR1740065     1   0.000      0.971 1.000 0.000
#&gt; SRR1740066     2   0.662      0.924 0.172 0.828
#&gt; SRR1740067     2   0.662      0.924 0.172 0.828
#&gt; SRR1740068     2   0.662      0.924 0.172 0.828
#&gt; SRR1740069     2   0.662      0.924 0.172 0.828
#&gt; SRR1740070     2   0.662      0.924 0.172 0.828
#&gt; SRR1740071     2   0.662      0.924 0.172 0.828
#&gt; SRR1740072     2   0.662      0.924 0.172 0.828
#&gt; SRR1740073     2   0.662      0.924 0.172 0.828
#&gt; SRR1740074     2   0.000      0.863 0.000 1.000
#&gt; SRR1740075     2   0.000      0.863 0.000 1.000
#&gt; SRR1740076     2   0.000      0.863 0.000 1.000
#&gt; SRR1740077     2   0.000      0.863 0.000 1.000
#&gt; SRR1740078     1   0.000      0.971 1.000 0.000
#&gt; SRR1740079     1   0.000      0.971 1.000 0.000
#&gt; SRR1740080     1   0.000      0.971 1.000 0.000
#&gt; SRR1740081     1   0.000      0.971 1.000 0.000
#&gt; SRR1740082     1   0.443      0.907 0.908 0.092
#&gt; SRR1740083     1   0.443      0.907 0.908 0.092
#&gt; SRR1740084     1   0.443      0.907 0.908 0.092
#&gt; SRR1740085     1   0.443      0.907 0.908 0.092
#&gt; SRR1740086     1   0.000      0.971 1.000 0.000
#&gt; SRR1740087     1   0.000      0.971 1.000 0.000
#&gt; SRR1740088     1   0.000      0.971 1.000 0.000
#&gt; SRR1740089     1   0.000      0.971 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740035     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740036     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740037     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740038     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740039     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740040     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740041     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740042     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740043     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740044     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740045     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740046     2   0.622      0.704 0.000 0.568 0.432
#&gt; SRR1740048     2   0.622      0.704 0.000 0.568 0.432
#&gt; SRR1740047     2   0.622      0.704 0.000 0.568 0.432
#&gt; SRR1740049     2   0.622      0.704 0.000 0.568 0.432
#&gt; SRR1740050     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740051     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740052     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740054     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740053     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740056     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740055     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740057     1   0.625      0.741 0.772 0.144 0.084
#&gt; SRR1740058     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740059     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740060     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740061     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740062     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740063     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740064     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740065     1   0.627      0.684 0.548 0.000 0.452
#&gt; SRR1740066     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740067     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740068     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740069     2   0.158      0.856 0.028 0.964 0.008
#&gt; SRR1740070     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740071     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740072     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740073     2   0.116      0.857 0.028 0.972 0.000
#&gt; SRR1740074     2   0.625      0.704 0.000 0.556 0.444
#&gt; SRR1740075     2   0.625      0.704 0.000 0.556 0.444
#&gt; SRR1740076     2   0.625      0.704 0.000 0.556 0.444
#&gt; SRR1740077     2   0.625      0.704 0.000 0.556 0.444
#&gt; SRR1740078     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740079     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740080     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740081     1   0.226      0.807 0.932 0.000 0.068
#&gt; SRR1740082     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740083     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740084     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740085     1   0.637      0.736 0.764 0.152 0.084
#&gt; SRR1740086     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740087     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740088     1   0.226      0.818 0.932 0.000 0.068
#&gt; SRR1740089     1   0.226      0.818 0.932 0.000 0.068
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4  0.4382      0.984 0.296 0.000 0.000 0.704
#&gt; SRR1740035     4  0.4382      0.984 0.296 0.000 0.000 0.704
#&gt; SRR1740036     4  0.4382      0.984 0.296 0.000 0.000 0.704
#&gt; SRR1740037     4  0.4382      0.984 0.296 0.000 0.000 0.704
#&gt; SRR1740038     2  0.6923      0.919 0.012 0.612 0.252 0.124
#&gt; SRR1740039     2  0.6923      0.919 0.012 0.612 0.252 0.124
#&gt; SRR1740040     2  0.6923      0.919 0.012 0.612 0.252 0.124
#&gt; SRR1740041     2  0.6923      0.919 0.012 0.612 0.252 0.124
#&gt; SRR1740042     2  0.4576      0.918 0.012 0.728 0.260 0.000
#&gt; SRR1740043     2  0.4576      0.918 0.012 0.728 0.260 0.000
#&gt; SRR1740044     2  0.4576      0.918 0.012 0.728 0.260 0.000
#&gt; SRR1740045     2  0.4576      0.918 0.012 0.728 0.260 0.000
#&gt; SRR1740046     3  0.2909      0.951 0.000 0.020 0.888 0.092
#&gt; SRR1740048     3  0.2949      0.951 0.000 0.024 0.888 0.088
#&gt; SRR1740047     3  0.2949      0.951 0.000 0.024 0.888 0.088
#&gt; SRR1740049     3  0.2909      0.951 0.000 0.020 0.888 0.092
#&gt; SRR1740050     1  0.0859      0.604 0.980 0.008 0.004 0.008
#&gt; SRR1740051     1  0.0859      0.604 0.980 0.008 0.004 0.008
#&gt; SRR1740052     1  0.0859      0.604 0.980 0.008 0.004 0.008
#&gt; SRR1740054     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740053     1  0.0859      0.604 0.980 0.008 0.004 0.008
#&gt; SRR1740056     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740055     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740057     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740058     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740059     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740060     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740061     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740062     4  0.5369      0.984 0.296 0.016 0.012 0.676
#&gt; SRR1740063     4  0.5369      0.984 0.296 0.016 0.012 0.676
#&gt; SRR1740064     4  0.5369      0.984 0.296 0.016 0.012 0.676
#&gt; SRR1740065     4  0.5369      0.984 0.296 0.016 0.012 0.676
#&gt; SRR1740066     2  0.6969      0.919 0.012 0.608 0.252 0.128
#&gt; SRR1740067     2  0.6969      0.919 0.012 0.608 0.252 0.128
#&gt; SRR1740068     2  0.6969      0.919 0.012 0.608 0.252 0.128
#&gt; SRR1740069     2  0.6969      0.919 0.012 0.608 0.252 0.128
#&gt; SRR1740070     2  0.4755      0.918 0.012 0.724 0.260 0.004
#&gt; SRR1740071     2  0.4755      0.918 0.012 0.724 0.260 0.004
#&gt; SRR1740072     2  0.4755      0.918 0.012 0.724 0.260 0.004
#&gt; SRR1740073     2  0.4755      0.918 0.012 0.724 0.260 0.004
#&gt; SRR1740074     3  0.0779      0.951 0.000 0.016 0.980 0.004
#&gt; SRR1740075     3  0.0779      0.951 0.000 0.016 0.980 0.004
#&gt; SRR1740076     3  0.0707      0.951 0.000 0.020 0.980 0.000
#&gt; SRR1740077     3  0.0707      0.951 0.000 0.020 0.980 0.000
#&gt; SRR1740078     1  0.0592      0.604 0.984 0.000 0.000 0.016
#&gt; SRR1740079     1  0.0592      0.604 0.984 0.000 0.000 0.016
#&gt; SRR1740080     1  0.0592      0.604 0.984 0.000 0.000 0.016
#&gt; SRR1740081     1  0.0592      0.604 0.984 0.000 0.000 0.016
#&gt; SRR1740082     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740083     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740084     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740085     1  0.7163      0.512 0.576 0.232 0.004 0.188
#&gt; SRR1740086     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740087     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740088     1  0.6198      0.500 0.672 0.152 0.000 0.176
#&gt; SRR1740089     1  0.6198      0.500 0.672 0.152 0.000 0.176
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.6477      0.944 0.292 0.000 0.036 0.564 0.108
#&gt; SRR1740035     4  0.6477      0.944 0.292 0.000 0.036 0.564 0.108
#&gt; SRR1740036     4  0.6477      0.944 0.292 0.000 0.036 0.564 0.108
#&gt; SRR1740037     4  0.6477      0.944 0.292 0.000 0.036 0.564 0.108
#&gt; SRR1740038     2  0.5401      0.805 0.084 0.696 0.000 0.196 0.024
#&gt; SRR1740039     2  0.5401      0.805 0.084 0.696 0.000 0.196 0.024
#&gt; SRR1740040     2  0.5401      0.805 0.084 0.696 0.000 0.196 0.024
#&gt; SRR1740041     2  0.5401      0.805 0.084 0.696 0.000 0.196 0.024
#&gt; SRR1740042     2  0.0324      0.806 0.004 0.992 0.000 0.000 0.004
#&gt; SRR1740043     2  0.0324      0.806 0.004 0.992 0.000 0.000 0.004
#&gt; SRR1740044     2  0.0324      0.806 0.004 0.992 0.000 0.000 0.004
#&gt; SRR1740045     2  0.0324      0.806 0.004 0.992 0.000 0.000 0.004
#&gt; SRR1740046     3  0.3427      0.928 0.012 0.192 0.796 0.000 0.000
#&gt; SRR1740048     3  0.3427      0.928 0.000 0.192 0.796 0.012 0.000
#&gt; SRR1740047     3  0.3427      0.928 0.000 0.192 0.796 0.012 0.000
#&gt; SRR1740049     3  0.3427      0.928 0.012 0.192 0.796 0.000 0.000
#&gt; SRR1740050     5  0.4234      0.328 0.252 0.000 0.004 0.020 0.724
#&gt; SRR1740051     5  0.4167      0.328 0.252 0.000 0.000 0.024 0.724
#&gt; SRR1740052     5  0.4167      0.328 0.252 0.000 0.000 0.024 0.724
#&gt; SRR1740054     5  0.6761      0.512 0.096 0.060 0.104 0.072 0.668
#&gt; SRR1740053     5  0.4234      0.328 0.252 0.000 0.004 0.020 0.724
#&gt; SRR1740056     5  0.6761      0.512 0.096 0.060 0.104 0.072 0.668
#&gt; SRR1740055     5  0.6761      0.512 0.096 0.060 0.104 0.072 0.668
#&gt; SRR1740057     5  0.6808      0.510 0.100 0.060 0.104 0.072 0.664
#&gt; SRR1740058     1  0.3534      0.992 0.744 0.000 0.000 0.000 0.256
#&gt; SRR1740059     1  0.3534      0.992 0.744 0.000 0.000 0.000 0.256
#&gt; SRR1740060     1  0.3534      0.992 0.744 0.000 0.000 0.000 0.256
#&gt; SRR1740061     1  0.3534      0.992 0.744 0.000 0.000 0.000 0.256
#&gt; SRR1740062     4  0.5303      0.943 0.232 0.000 0.000 0.660 0.108
#&gt; SRR1740063     4  0.5303      0.943 0.232 0.000 0.000 0.660 0.108
#&gt; SRR1740064     4  0.5546      0.942 0.228 0.000 0.008 0.656 0.108
#&gt; SRR1740065     4  0.5429      0.943 0.228 0.000 0.004 0.660 0.108
#&gt; SRR1740066     2  0.5385      0.805 0.076 0.692 0.000 0.208 0.024
#&gt; SRR1740067     2  0.5385      0.805 0.076 0.692 0.000 0.208 0.024
#&gt; SRR1740068     2  0.5385      0.805 0.076 0.692 0.000 0.208 0.024
#&gt; SRR1740069     2  0.5385      0.805 0.076 0.692 0.000 0.208 0.024
#&gt; SRR1740070     2  0.0324      0.806 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740071     2  0.0324      0.806 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740072     2  0.0324      0.806 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740073     2  0.0324      0.806 0.000 0.992 0.000 0.004 0.004
#&gt; SRR1740074     3  0.5927      0.929 0.088 0.192 0.668 0.052 0.000
#&gt; SRR1740075     3  0.5927      0.929 0.088 0.192 0.668 0.052 0.000
#&gt; SRR1740076     3  0.5948      0.929 0.080 0.192 0.668 0.060 0.000
#&gt; SRR1740077     3  0.5948      0.929 0.080 0.192 0.668 0.060 0.000
#&gt; SRR1740078     5  0.4321      0.328 0.252 0.000 0.024 0.004 0.720
#&gt; SRR1740079     5  0.4321      0.328 0.252 0.000 0.024 0.004 0.720
#&gt; SRR1740080     5  0.4354      0.328 0.252 0.000 0.020 0.008 0.720
#&gt; SRR1740081     5  0.4354      0.328 0.252 0.000 0.020 0.008 0.720
#&gt; SRR1740082     5  0.6851      0.512 0.096 0.060 0.112 0.072 0.660
#&gt; SRR1740083     5  0.6851      0.512 0.096 0.060 0.112 0.072 0.660
#&gt; SRR1740084     5  0.6851      0.512 0.096 0.060 0.112 0.072 0.660
#&gt; SRR1740085     5  0.6851      0.512 0.096 0.060 0.112 0.072 0.660
#&gt; SRR1740086     1  0.3916      0.992 0.732 0.000 0.012 0.000 0.256
#&gt; SRR1740087     1  0.3916      0.992 0.732 0.000 0.012 0.000 0.256
#&gt; SRR1740088     1  0.3916      0.992 0.732 0.000 0.012 0.000 0.256
#&gt; SRR1740089     1  0.3916      0.992 0.732 0.000 0.012 0.000 0.256
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4  0.2213      0.918 0.100 0.000 0.008 0.888 0.000 0.004
#&gt; SRR1740035     4  0.2170      0.918 0.100 0.000 0.012 0.888 0.000 0.000
#&gt; SRR1740036     4  0.2213      0.918 0.100 0.000 0.008 0.888 0.000 0.004
#&gt; SRR1740037     4  0.2170      0.918 0.100 0.000 0.000 0.888 0.012 0.000
#&gt; SRR1740038     2  0.0547      0.762 0.020 0.980 0.000 0.000 0.000 0.000
#&gt; SRR1740039     2  0.0547      0.762 0.020 0.980 0.000 0.000 0.000 0.000
#&gt; SRR1740040     2  0.0547      0.762 0.020 0.980 0.000 0.000 0.000 0.000
#&gt; SRR1740041     2  0.0547      0.762 0.020 0.980 0.000 0.000 0.000 0.000
#&gt; SRR1740042     2  0.5055      0.750 0.004 0.604 0.000 0.008 0.064 0.320
#&gt; SRR1740043     2  0.5055      0.750 0.004 0.604 0.000 0.008 0.064 0.320
#&gt; SRR1740044     2  0.5055      0.750 0.004 0.604 0.000 0.008 0.064 0.320
#&gt; SRR1740045     2  0.5055      0.750 0.004 0.604 0.000 0.008 0.064 0.320
#&gt; SRR1740046     3  0.2266      0.918 0.000 0.108 0.880 0.000 0.012 0.000
#&gt; SRR1740048     3  0.2358      0.918 0.000 0.108 0.876 0.000 0.000 0.016
#&gt; SRR1740047     3  0.2358      0.918 0.000 0.108 0.876 0.000 0.000 0.016
#&gt; SRR1740049     3  0.2266      0.918 0.000 0.108 0.880 0.000 0.012 0.000
#&gt; SRR1740050     5  0.5622      0.956 0.296 0.000 0.016 0.068 0.596 0.024
#&gt; SRR1740051     5  0.5548      0.956 0.296 0.000 0.016 0.068 0.600 0.020
#&gt; SRR1740052     5  0.5548      0.956 0.296 0.000 0.016 0.068 0.600 0.020
#&gt; SRR1740054     1  0.1007      0.970 0.956 0.044 0.000 0.000 0.000 0.000
#&gt; SRR1740053     5  0.5622      0.956 0.296 0.000 0.016 0.068 0.596 0.024
#&gt; SRR1740056     1  0.1007      0.970 0.956 0.044 0.000 0.000 0.000 0.000
#&gt; SRR1740055     1  0.1007      0.970 0.956 0.044 0.000 0.000 0.000 0.000
#&gt; SRR1740057     1  0.1007      0.970 0.956 0.044 0.000 0.000 0.000 0.000
#&gt; SRR1740058     6  0.7876      0.958 0.188 0.000 0.016 0.180 0.276 0.340
#&gt; SRR1740059     6  0.7876      0.958 0.188 0.000 0.016 0.180 0.276 0.340
#&gt; SRR1740060     6  0.7876      0.958 0.188 0.000 0.016 0.180 0.276 0.340
#&gt; SRR1740061     6  0.7876      0.958 0.188 0.000 0.016 0.180 0.276 0.340
#&gt; SRR1740062     4  0.4880      0.918 0.108 0.000 0.024 0.752 0.056 0.060
#&gt; SRR1740063     4  0.4880      0.918 0.108 0.000 0.024 0.752 0.056 0.060
#&gt; SRR1740064     4  0.4902      0.917 0.104 0.000 0.028 0.752 0.048 0.068
#&gt; SRR1740065     4  0.4877      0.918 0.108 0.000 0.024 0.752 0.052 0.064
#&gt; SRR1740066     2  0.1596      0.762 0.020 0.944 0.000 0.012 0.020 0.004
#&gt; SRR1740067     2  0.1596      0.762 0.020 0.944 0.000 0.012 0.020 0.004
#&gt; SRR1740068     2  0.1596      0.762 0.020 0.944 0.000 0.012 0.020 0.004
#&gt; SRR1740069     2  0.1596      0.762 0.020 0.944 0.000 0.012 0.020 0.004
#&gt; SRR1740070     2  0.3890      0.750 0.004 0.596 0.000 0.000 0.000 0.400
#&gt; SRR1740071     2  0.3890      0.750 0.004 0.596 0.000 0.000 0.000 0.400
#&gt; SRR1740072     2  0.3890      0.750 0.004 0.596 0.000 0.000 0.000 0.400
#&gt; SRR1740073     2  0.3890      0.750 0.004 0.596 0.000 0.000 0.000 0.400
#&gt; SRR1740074     3  0.5570      0.919 0.016 0.108 0.720 0.032 0.060 0.064
#&gt; SRR1740075     3  0.5570      0.919 0.016 0.108 0.720 0.032 0.060 0.064
#&gt; SRR1740076     3  0.5499      0.919 0.016 0.108 0.724 0.028 0.064 0.060
#&gt; SRR1740077     3  0.5499      0.919 0.016 0.108 0.724 0.028 0.064 0.060
#&gt; SRR1740078     5  0.4612      0.955 0.284 0.000 0.000 0.052 0.656 0.008
#&gt; SRR1740079     5  0.4612      0.955 0.284 0.000 0.000 0.052 0.656 0.008
#&gt; SRR1740080     5  0.4507      0.955 0.284 0.000 0.004 0.052 0.660 0.000
#&gt; SRR1740081     5  0.4507      0.955 0.284 0.000 0.004 0.052 0.660 0.000
#&gt; SRR1740082     1  0.2420      0.970 0.904 0.044 0.028 0.000 0.008 0.016
#&gt; SRR1740083     1  0.2420      0.970 0.904 0.044 0.028 0.000 0.008 0.016
#&gt; SRR1740084     1  0.2420      0.970 0.904 0.044 0.028 0.000 0.008 0.016
#&gt; SRR1740085     1  0.2420      0.970 0.904 0.044 0.028 0.000 0.008 0.016
#&gt; SRR1740086     6  0.7522      0.957 0.184 0.000 0.004 0.180 0.232 0.400
#&gt; SRR1740087     6  0.7522      0.957 0.184 0.000 0.004 0.180 0.232 0.400
#&gt; SRR1740088     6  0.7414      0.957 0.188 0.000 0.000 0.180 0.232 0.400
#&gt; SRR1740089     6  0.7414      0.957 0.188 0.000 0.000 0.180 0.232 0.400
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.998       0.999         0.4993 0.501   0.501
#> 3 3 0.709           0.809       0.837         0.2177 1.000   1.000
#> 4 4 0.834           0.871       0.822         0.1649 0.792   0.585
#> 5 5 0.958           0.973       0.974         0.1148 0.917   0.717
#> 6 6 1.000           0.989       0.975         0.0531 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740035     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740036     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740037     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740046     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740048     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740047     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740049     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740050     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740054     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740053     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740056     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740055     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740057     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740058     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740062     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740063     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740064     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740065     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740074     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740075     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740076     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740077     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740078     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740082     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740083     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740084     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740085     1  0.0938      0.990 0.988 0.012
#&gt; SRR1740086     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.997 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.997 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740035     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740036     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740037     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740038     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740042     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740043     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740044     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740045     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740046     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740048     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740047     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740049     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740050     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740051     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740052     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740054     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740053     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740056     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740055     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740057     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740058     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740059     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740060     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740061     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740062     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740063     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740064     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740065     1  0.3752      0.814 0.856 0.000 0.144
#&gt; SRR1740066     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740070     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740071     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740072     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740073     2  0.0000      0.885 0.000 1.000 0.000
#&gt; SRR1740074     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740075     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740076     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740077     2  0.6192      0.753 0.000 0.580 0.420
#&gt; SRR1740078     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740079     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740080     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740081     1  0.0237      0.858 0.996 0.000 0.004
#&gt; SRR1740082     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740083     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740084     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740085     1  0.7453      0.613 0.528 0.036 0.436
#&gt; SRR1740086     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740087     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740088     1  0.0000      0.858 1.000 0.000 0.000
#&gt; SRR1740089     1  0.0000      0.858 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740035     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740036     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740037     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740046     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740048     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740047     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740049     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740050     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740051     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740052     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740054     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740053     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740056     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740055     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740057     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740058     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740059     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740060     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740061     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740062     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740063     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740064     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740065     1  0.6309      0.607 0.588 0.000 0.076 0.336
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740074     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740075     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740076     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740077     3  0.2149      1.000 0.000 0.088 0.912 0.000
#&gt; SRR1740078     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740079     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740080     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740081     1  0.1677      0.736 0.948 0.000 0.012 0.040
#&gt; SRR1740082     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740083     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740084     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740085     4  0.4661      1.000 0.348 0.000 0.000 0.652
#&gt; SRR1740086     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740087     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740088     1  0.0188      0.750 0.996 0.000 0.000 0.004
#&gt; SRR1740089     1  0.0188      0.750 0.996 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3   p4    p5
#&gt; SRR1740034     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740035     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740036     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740037     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740038     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740039     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740040     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740041     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740042     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740043     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740044     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740045     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740050     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740051     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740052     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740054     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740053     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740056     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740055     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740057     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740058     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740059     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740060     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740061     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740062     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740063     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740064     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740065     4  0.0000      1.000 0.000 0.000  0 1.00 0.000
#&gt; SRR1740066     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740067     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740068     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740069     2  0.0290      0.997 0.008 0.992  0 0.00 0.000
#&gt; SRR1740070     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740071     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740072     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740073     2  0.0000      0.997 0.000 1.000  0 0.00 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.00 0.000
#&gt; SRR1740078     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740079     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740080     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740081     5  0.0162      0.911 0.004 0.000  0 0.00 0.996
#&gt; SRR1740082     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740083     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740084     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740085     1  0.0290      1.000 0.992 0.000  0 0.00 0.008
#&gt; SRR1740086     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740087     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740088     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
#&gt; SRR1740089     5  0.3479      0.908 0.084 0.000  0 0.08 0.836
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4   p5    p6
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740038     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740039     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740040     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740041     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740042     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740043     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740044     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740045     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740050     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740051     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740052     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740054     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740053     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740056     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740055     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740057     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740058     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740059     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740060     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740061     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0 1.000 0.00 0.000
#&gt; SRR1740066     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740067     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740068     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740069     2   0.000      0.961 0.000 1.000  0 0.000 0.00 0.000
#&gt; SRR1740070     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740071     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740072     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740073     2   0.166      0.961 0.000 0.912  0 0.000 0.00 0.088
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1 0.000 0.00 0.000
#&gt; SRR1740078     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740079     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740080     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740081     5   0.000      1.000 0.000 0.000  0 0.000 1.00 0.000
#&gt; SRR1740082     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740083     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740084     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740085     1   0.000      1.000 1.000 0.000  0 0.000 0.00 0.000
#&gt; SRR1740086     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740087     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740088     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
#&gt; SRR1740089     6   0.184      1.000 0.004 0.000  0 0.004 0.08 0.912
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.454           0.757       0.850         0.4008 0.501   0.501
#> 3 3 0.782           0.910       0.958         0.4882 0.917   0.834
#> 4 4 0.849           0.942       0.968         0.1864 0.875   0.702
#> 5 5 0.927           0.904       0.956         0.1203 0.912   0.701
#> 6 6 1.000           1.000       1.000         0.0486 0.954   0.781
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 5
```

There is also optional best $k$ = 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.000      0.901 1.000 0.000
#&gt; SRR1740035     1   0.000      0.901 1.000 0.000
#&gt; SRR1740036     1   0.000      0.901 1.000 0.000
#&gt; SRR1740037     1   0.000      0.901 1.000 0.000
#&gt; SRR1740038     2   0.971      0.725 0.400 0.600
#&gt; SRR1740039     2   0.971      0.725 0.400 0.600
#&gt; SRR1740040     2   0.971      0.725 0.400 0.600
#&gt; SRR1740041     2   0.971      0.725 0.400 0.600
#&gt; SRR1740042     2   0.971      0.725 0.400 0.600
#&gt; SRR1740043     2   0.971      0.725 0.400 0.600
#&gt; SRR1740044     2   0.971      0.725 0.400 0.600
#&gt; SRR1740045     2   0.971      0.725 0.400 0.600
#&gt; SRR1740046     2   0.000      0.628 0.000 1.000
#&gt; SRR1740048     2   0.000      0.628 0.000 1.000
#&gt; SRR1740047     2   0.000      0.628 0.000 1.000
#&gt; SRR1740049     2   0.000      0.628 0.000 1.000
#&gt; SRR1740050     1   0.000      0.901 1.000 0.000
#&gt; SRR1740051     1   0.000      0.901 1.000 0.000
#&gt; SRR1740052     1   0.000      0.901 1.000 0.000
#&gt; SRR1740054     1   0.900      0.342 0.684 0.316
#&gt; SRR1740053     1   0.000      0.901 1.000 0.000
#&gt; SRR1740056     1   0.722      0.649 0.800 0.200
#&gt; SRR1740055     1   0.900      0.342 0.684 0.316
#&gt; SRR1740057     1   0.662      0.695 0.828 0.172
#&gt; SRR1740058     1   0.000      0.901 1.000 0.000
#&gt; SRR1740059     1   0.000      0.901 1.000 0.000
#&gt; SRR1740060     1   0.000      0.901 1.000 0.000
#&gt; SRR1740061     1   0.000      0.901 1.000 0.000
#&gt; SRR1740062     1   0.000      0.901 1.000 0.000
#&gt; SRR1740063     1   0.000      0.901 1.000 0.000
#&gt; SRR1740064     1   0.000      0.901 1.000 0.000
#&gt; SRR1740065     1   0.000      0.901 1.000 0.000
#&gt; SRR1740066     2   0.971      0.725 0.400 0.600
#&gt; SRR1740067     2   0.971      0.725 0.400 0.600
#&gt; SRR1740068     2   0.971      0.725 0.400 0.600
#&gt; SRR1740069     2   0.971      0.725 0.400 0.600
#&gt; SRR1740070     2   0.971      0.725 0.400 0.600
#&gt; SRR1740071     2   0.971      0.725 0.400 0.600
#&gt; SRR1740072     2   0.971      0.725 0.400 0.600
#&gt; SRR1740073     2   0.971      0.725 0.400 0.600
#&gt; SRR1740074     2   0.000      0.628 0.000 1.000
#&gt; SRR1740075     2   0.000      0.628 0.000 1.000
#&gt; SRR1740076     2   0.000      0.628 0.000 1.000
#&gt; SRR1740077     2   0.000      0.628 0.000 1.000
#&gt; SRR1740078     1   0.000      0.901 1.000 0.000
#&gt; SRR1740079     1   0.000      0.901 1.000 0.000
#&gt; SRR1740080     1   0.000      0.901 1.000 0.000
#&gt; SRR1740081     1   0.000      0.901 1.000 0.000
#&gt; SRR1740082     1   0.900      0.342 0.684 0.316
#&gt; SRR1740083     1   0.839      0.490 0.732 0.268
#&gt; SRR1740084     1   0.722      0.649 0.800 0.200
#&gt; SRR1740085     1   0.722      0.649 0.800 0.200
#&gt; SRR1740086     1   0.000      0.901 1.000 0.000
#&gt; SRR1740087     1   0.000      0.901 1.000 0.000
#&gt; SRR1740088     1   0.000      0.901 1.000 0.000
#&gt; SRR1740089     1   0.000      0.901 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1740034     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740035     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740036     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740037     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740042     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740043     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740044     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740045     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740050     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740051     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740052     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740054     1   0.610      0.481 0.608 0.392  0
#&gt; SRR1740053     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740056     1   0.455      0.768 0.800 0.200  0
#&gt; SRR1740055     1   0.610      0.481 0.608 0.392  0
#&gt; SRR1740057     1   0.455      0.768 0.800 0.200  0
#&gt; SRR1740058     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740059     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740060     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740061     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740062     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740063     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740064     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740065     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740070     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740071     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740072     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740073     2   0.000      1.000 0.000 1.000  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1
#&gt; SRR1740078     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740079     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740080     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740081     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740082     1   0.610      0.481 0.608 0.392  0
#&gt; SRR1740083     1   0.610      0.481 0.608 0.392  0
#&gt; SRR1740084     1   0.455      0.768 0.800 0.200  0
#&gt; SRR1740085     1   0.455      0.768 0.800 0.200  0
#&gt; SRR1740086     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740087     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740088     1   0.000      0.914 1.000 0.000  0
#&gt; SRR1740089     1   0.000      0.914 1.000 0.000  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette  p1  p2 p3 p4
#&gt; SRR1740034     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740035     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740036     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740037     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740038     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740039     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740040     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740041     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740042     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740043     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740044     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740045     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740046     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740048     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740047     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740049     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740050     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740051     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740052     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740054     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740053     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740056     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740055     1   0.485      0.477 0.6 0.4  0  0
#&gt; SRR1740057     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740058     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740059     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740060     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740061     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740062     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740063     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740064     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740065     4   0.000      1.000 0.0 0.0  0  1
#&gt; SRR1740066     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740067     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740068     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740069     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740070     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740071     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740072     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740073     2   0.000      1.000 0.0 1.0  0  0
#&gt; SRR1740074     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740075     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740076     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740077     3   0.000      1.000 0.0 0.0  1  0
#&gt; SRR1740078     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740079     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740080     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740081     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740082     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740083     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740084     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740085     1   0.361      0.813 0.8 0.2  0  0
#&gt; SRR1740086     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740087     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740088     1   0.000      0.910 1.0 0.0  0  0
#&gt; SRR1740089     1   0.000      0.910 1.0 0.0  0  0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1740034     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740035     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740036     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740037     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740038     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740039     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740040     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740041     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740042     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740043     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740044     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740045     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740046     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740048     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740047     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740049     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740050     5  0.3109     0.7734 0.200 0.000  0  0 0.800
#&gt; SRR1740051     1  0.4219    -0.0391 0.584 0.000  0  0 0.416
#&gt; SRR1740052     5  0.4235     0.4525 0.424 0.000  0  0 0.576
#&gt; SRR1740054     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740053     5  0.3109     0.7734 0.200 0.000  0  0 0.800
#&gt; SRR1740056     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740055     5  0.0162     0.8294 0.000 0.004  0  0 0.996
#&gt; SRR1740057     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740058     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740059     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740060     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740061     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740062     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740063     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740064     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740065     4  0.0000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740066     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740067     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740068     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740069     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740070     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740071     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740072     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740073     2  0.0000     1.0000 0.000 1.000  0  0 0.000
#&gt; SRR1740074     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740075     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740076     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740077     3  0.0000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740078     5  0.3109     0.7734 0.200 0.000  0  0 0.800
#&gt; SRR1740079     5  0.3109     0.7734 0.200 0.000  0  0 0.800
#&gt; SRR1740080     5  0.4182     0.5066 0.400 0.000  0  0 0.600
#&gt; SRR1740081     5  0.4182     0.5066 0.400 0.000  0  0 0.600
#&gt; SRR1740082     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740083     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740084     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740085     5  0.0000     0.8322 0.000 0.000  0  0 1.000
#&gt; SRR1740086     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740087     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740088     1  0.0000     0.9325 1.000 0.000  0  0 0.000
#&gt; SRR1740089     1  0.0000     0.9325 1.000 0.000  0  0 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.584           0.939       0.946         0.4940 0.501   0.501
#> 3 3 1.000           1.000       1.000         0.1785 0.584   0.377
#> 4 4 1.000           1.000       1.000         0.2139 0.875   0.702
#> 5 5 1.000           1.000       1.000         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 3 4 5
```

There is also optional best $k$ = 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.469      0.918 0.900 0.100
#&gt; SRR1740035     1   0.469      0.918 0.900 0.100
#&gt; SRR1740036     1   0.469      0.918 0.900 0.100
#&gt; SRR1740037     1   0.469      0.918 0.900 0.100
#&gt; SRR1740038     2   0.000      0.960 0.000 1.000
#&gt; SRR1740039     2   0.000      0.960 0.000 1.000
#&gt; SRR1740040     2   0.000      0.960 0.000 1.000
#&gt; SRR1740041     2   0.000      0.960 0.000 1.000
#&gt; SRR1740042     2   0.000      0.960 0.000 1.000
#&gt; SRR1740043     2   0.000      0.960 0.000 1.000
#&gt; SRR1740044     2   0.000      0.960 0.000 1.000
#&gt; SRR1740045     2   0.000      0.960 0.000 1.000
#&gt; SRR1740046     1   0.118      0.943 0.984 0.016
#&gt; SRR1740048     1   0.118      0.943 0.984 0.016
#&gt; SRR1740047     1   0.118      0.943 0.984 0.016
#&gt; SRR1740049     1   0.118      0.943 0.984 0.016
#&gt; SRR1740050     2   0.563      0.897 0.132 0.868
#&gt; SRR1740051     2   0.563      0.897 0.132 0.868
#&gt; SRR1740052     2   0.563      0.897 0.132 0.868
#&gt; SRR1740054     2   0.163      0.956 0.024 0.976
#&gt; SRR1740053     2   0.563      0.897 0.132 0.868
#&gt; SRR1740056     2   0.163      0.956 0.024 0.976
#&gt; SRR1740055     2   0.163      0.956 0.024 0.976
#&gt; SRR1740057     2   0.163      0.956 0.024 0.976
#&gt; SRR1740058     1   0.278      0.938 0.952 0.048
#&gt; SRR1740059     1   0.278      0.938 0.952 0.048
#&gt; SRR1740060     1   0.278      0.938 0.952 0.048
#&gt; SRR1740061     1   0.278      0.938 0.952 0.048
#&gt; SRR1740062     1   0.469      0.918 0.900 0.100
#&gt; SRR1740063     1   0.469      0.918 0.900 0.100
#&gt; SRR1740064     1   0.469      0.918 0.900 0.100
#&gt; SRR1740065     1   0.469      0.918 0.900 0.100
#&gt; SRR1740066     2   0.000      0.960 0.000 1.000
#&gt; SRR1740067     2   0.000      0.960 0.000 1.000
#&gt; SRR1740068     2   0.000      0.960 0.000 1.000
#&gt; SRR1740069     2   0.000      0.960 0.000 1.000
#&gt; SRR1740070     2   0.000      0.960 0.000 1.000
#&gt; SRR1740071     2   0.000      0.960 0.000 1.000
#&gt; SRR1740072     2   0.000      0.960 0.000 1.000
#&gt; SRR1740073     2   0.000      0.960 0.000 1.000
#&gt; SRR1740074     1   0.118      0.943 0.984 0.016
#&gt; SRR1740075     1   0.118      0.943 0.984 0.016
#&gt; SRR1740076     1   0.118      0.943 0.984 0.016
#&gt; SRR1740077     1   0.118      0.943 0.984 0.016
#&gt; SRR1740078     2   0.563      0.897 0.132 0.868
#&gt; SRR1740079     2   0.563      0.897 0.132 0.868
#&gt; SRR1740080     2   0.563      0.897 0.132 0.868
#&gt; SRR1740081     2   0.563      0.897 0.132 0.868
#&gt; SRR1740082     2   0.163      0.956 0.024 0.976
#&gt; SRR1740083     2   0.163      0.956 0.024 0.976
#&gt; SRR1740084     2   0.163      0.956 0.024 0.976
#&gt; SRR1740085     2   0.163      0.956 0.024 0.976
#&gt; SRR1740086     1   0.278      0.938 0.952 0.048
#&gt; SRR1740087     1   0.278      0.938 0.952 0.048
#&gt; SRR1740088     1   0.278      0.938 0.952 0.048
#&gt; SRR1740089     1   0.278      0.938 0.952 0.048
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1740034     1       0          1  1  0  0
#&gt; SRR1740035     1       0          1  1  0  0
#&gt; SRR1740036     1       0          1  1  0  0
#&gt; SRR1740037     1       0          1  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0
#&gt; SRR1740039     2       0          1  0  1  0
#&gt; SRR1740040     2       0          1  0  1  0
#&gt; SRR1740041     2       0          1  0  1  0
#&gt; SRR1740042     2       0          1  0  1  0
#&gt; SRR1740043     2       0          1  0  1  0
#&gt; SRR1740044     2       0          1  0  1  0
#&gt; SRR1740045     2       0          1  0  1  0
#&gt; SRR1740046     3       0          1  0  0  1
#&gt; SRR1740048     3       0          1  0  0  1
#&gt; SRR1740047     3       0          1  0  0  1
#&gt; SRR1740049     3       0          1  0  0  1
#&gt; SRR1740050     1       0          1  1  0  0
#&gt; SRR1740051     1       0          1  1  0  0
#&gt; SRR1740052     1       0          1  1  0  0
#&gt; SRR1740054     1       0          1  1  0  0
#&gt; SRR1740053     1       0          1  1  0  0
#&gt; SRR1740056     1       0          1  1  0  0
#&gt; SRR1740055     1       0          1  1  0  0
#&gt; SRR1740057     1       0          1  1  0  0
#&gt; SRR1740058     1       0          1  1  0  0
#&gt; SRR1740059     1       0          1  1  0  0
#&gt; SRR1740060     1       0          1  1  0  0
#&gt; SRR1740061     1       0          1  1  0  0
#&gt; SRR1740062     1       0          1  1  0  0
#&gt; SRR1740063     1       0          1  1  0  0
#&gt; SRR1740064     1       0          1  1  0  0
#&gt; SRR1740065     1       0          1  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0
#&gt; SRR1740067     2       0          1  0  1  0
#&gt; SRR1740068     2       0          1  0  1  0
#&gt; SRR1740069     2       0          1  0  1  0
#&gt; SRR1740070     2       0          1  0  1  0
#&gt; SRR1740071     2       0          1  0  1  0
#&gt; SRR1740072     2       0          1  0  1  0
#&gt; SRR1740073     2       0          1  0  1  0
#&gt; SRR1740074     3       0          1  0  0  1
#&gt; SRR1740075     3       0          1  0  0  1
#&gt; SRR1740076     3       0          1  0  0  1
#&gt; SRR1740077     3       0          1  0  0  1
#&gt; SRR1740078     1       0          1  1  0  0
#&gt; SRR1740079     1       0          1  1  0  0
#&gt; SRR1740080     1       0          1  1  0  0
#&gt; SRR1740081     1       0          1  1  0  0
#&gt; SRR1740082     1       0          1  1  0  0
#&gt; SRR1740083     1       0          1  1  0  0
#&gt; SRR1740084     1       0          1  1  0  0
#&gt; SRR1740085     1       0          1  1  0  0
#&gt; SRR1740086     1       0          1  1  0  0
#&gt; SRR1740087     1       0          1  1  0  0
#&gt; SRR1740088     1       0          1  1  0  0
#&gt; SRR1740089     1       0          1  1  0  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1740034     4       0          1  0  0  0  1
#&gt; SRR1740035     4       0          1  0  0  0  1
#&gt; SRR1740036     4       0          1  0  0  0  1
#&gt; SRR1740037     4       0          1  0  0  0  1
#&gt; SRR1740038     2       0          1  0  1  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0
#&gt; SRR1740048     3       0          1  0  0  1  0
#&gt; SRR1740047     3       0          1  0  0  1  0
#&gt; SRR1740049     3       0          1  0  0  1  0
#&gt; SRR1740050     1       0          1  1  0  0  0
#&gt; SRR1740051     1       0          1  1  0  0  0
#&gt; SRR1740052     1       0          1  1  0  0  0
#&gt; SRR1740054     1       0          1  1  0  0  0
#&gt; SRR1740053     1       0          1  1  0  0  0
#&gt; SRR1740056     1       0          1  1  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0
#&gt; SRR1740058     1       0          1  1  0  0  0
#&gt; SRR1740059     1       0          1  1  0  0  0
#&gt; SRR1740060     1       0          1  1  0  0  0
#&gt; SRR1740061     1       0          1  1  0  0  0
#&gt; SRR1740062     4       0          1  0  0  0  1
#&gt; SRR1740063     4       0          1  0  0  0  1
#&gt; SRR1740064     4       0          1  0  0  0  1
#&gt; SRR1740065     4       0          1  0  0  0  1
#&gt; SRR1740066     2       0          1  0  1  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0
#&gt; SRR1740075     3       0          1  0  0  1  0
#&gt; SRR1740076     3       0          1  0  0  1  0
#&gt; SRR1740077     3       0          1  0  0  1  0
#&gt; SRR1740078     1       0          1  1  0  0  0
#&gt; SRR1740079     1       0          1  1  0  0  0
#&gt; SRR1740080     1       0          1  1  0  0  0
#&gt; SRR1740081     1       0          1  1  0  0  0
#&gt; SRR1740082     1       0          1  1  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0
#&gt; SRR1740086     1       0          1  1  0  0  0
#&gt; SRR1740087     1       0          1  1  0  0  0
#&gt; SRR1740088     1       0          1  1  0  0  0
#&gt; SRR1740089     1       0          1  1  0  0  0
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5
#&gt; SRR1740034     4       0          1  0  0  0  1  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1
#&gt; SRR1740051     5       0          1  0  0  0  0  1
#&gt; SRR1740052     5       0          1  0  0  0  0  1
#&gt; SRR1740054     1       0          1  1  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1
#&gt; SRR1740056     1       0          1  1  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0
#&gt; SRR1740058     5       0          1  0  0  0  0  1
#&gt; SRR1740059     5       0          1  0  0  0  0  1
#&gt; SRR1740060     5       0          1  0  0  0  0  1
#&gt; SRR1740061     5       0          1  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1
#&gt; SRR1740079     5       0          1  0  0  0  0  1
#&gt; SRR1740080     5       0          1  0  0  0  0  1
#&gt; SRR1740081     5       0          1  0  0  0  0  1
#&gt; SRR1740082     1       0          1  1  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0
#&gt; SRR1740086     5       0          1  0  0  0  0  1
#&gt; SRR1740087     5       0          1  0  0  0  0  1
#&gt; SRR1740088     5       0          1  0  0  0  0  1
#&gt; SRR1740089     5       0          1  0  0  0  0  1
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.979       0.989          0.501 0.501   0.501
#> 3 3 0.861           0.941       0.965          0.192 0.886   0.778
#> 4 4 0.880           0.916       0.963          0.193 0.881   0.707
#> 5 5 0.933           0.936       0.957          0.100 0.902   0.673
#> 6 6 0.948           0.907       0.945          0.063 0.948   0.756
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740035     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740036     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740037     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740038     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740039     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740040     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740041     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740042     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740043     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740044     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740045     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740046     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740048     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740047     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740049     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740050     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740051     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740052     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740054     1  0.2948      0.943 0.948 0.052
#&gt; SRR1740053     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740056     1  0.0672      0.976 0.992 0.008
#&gt; SRR1740055     1  0.7528      0.749 0.784 0.216
#&gt; SRR1740057     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740058     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740059     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740060     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740061     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740062     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740063     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740064     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740065     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740066     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740067     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740068     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740069     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740070     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740071     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740072     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740073     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740074     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740075     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740076     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740077     2  0.0000      1.000 0.000 1.000
#&gt; SRR1740078     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740079     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740080     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740081     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740082     1  0.6148      0.837 0.848 0.152
#&gt; SRR1740083     1  0.4815      0.892 0.896 0.104
#&gt; SRR1740084     1  0.2948      0.943 0.948 0.052
#&gt; SRR1740085     1  0.1414      0.967 0.980 0.020
#&gt; SRR1740086     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740087     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740088     1  0.0000      0.981 1.000 0.000
#&gt; SRR1740089     1  0.0000      0.981 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1  0.2680      0.925 0.924 0.068 0.008
#&gt; SRR1740035     1  0.2584      0.927 0.928 0.064 0.008
#&gt; SRR1740036     1  0.2584      0.927 0.928 0.064 0.008
#&gt; SRR1740037     1  0.3129      0.913 0.904 0.088 0.008
#&gt; SRR1740038     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740042     2  0.0592      0.962 0.000 0.988 0.012
#&gt; SRR1740043     2  0.0592      0.962 0.000 0.988 0.012
#&gt; SRR1740044     2  0.0592      0.962 0.000 0.988 0.012
#&gt; SRR1740045     2  0.0592      0.962 0.000 0.988 0.012
#&gt; SRR1740046     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740048     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740047     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740049     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740050     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740051     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740052     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740054     1  0.3816      0.852 0.852 0.148 0.000
#&gt; SRR1740053     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740056     1  0.0424      0.950 0.992 0.008 0.000
#&gt; SRR1740055     2  0.5443      0.609 0.260 0.736 0.004
#&gt; SRR1740057     1  0.0237      0.951 0.996 0.004 0.000
#&gt; SRR1740058     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740059     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740060     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740061     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740062     1  0.3965      0.879 0.860 0.132 0.008
#&gt; SRR1740063     1  0.4099      0.872 0.852 0.140 0.008
#&gt; SRR1740064     1  0.3896      0.883 0.864 0.128 0.008
#&gt; SRR1740065     1  0.4164      0.868 0.848 0.144 0.008
#&gt; SRR1740066     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      0.963 0.000 1.000 0.000
#&gt; SRR1740070     2  0.2066      0.933 0.000 0.940 0.060
#&gt; SRR1740071     2  0.1860      0.939 0.000 0.948 0.052
#&gt; SRR1740072     2  0.1753      0.943 0.000 0.952 0.048
#&gt; SRR1740073     2  0.1529      0.948 0.000 0.960 0.040
#&gt; SRR1740074     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740075     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740076     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740077     3  0.0424      1.000 0.000 0.008 0.992
#&gt; SRR1740078     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740079     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740080     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740081     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740082     1  0.4291      0.848 0.840 0.152 0.008
#&gt; SRR1740083     1  0.3192      0.894 0.888 0.112 0.000
#&gt; SRR1740084     1  0.1753      0.931 0.952 0.048 0.000
#&gt; SRR1740085     1  0.0892      0.946 0.980 0.020 0.000
#&gt; SRR1740086     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740087     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740088     1  0.0000      0.952 1.000 0.000 0.000
#&gt; SRR1740089     1  0.0000      0.952 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740038     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740039     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740040     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740041     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740042     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740043     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740044     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740045     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740050     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740051     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740052     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740054     1   0.478      0.501 0.624 0.376  0  0
#&gt; SRR1740053     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740056     1   0.312      0.802 0.844 0.156  0  0
#&gt; SRR1740055     2   0.241      0.863 0.104 0.896  0  0
#&gt; SRR1740057     1   0.241      0.837 0.896 0.104  0  0
#&gt; SRR1740058     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740059     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740060     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740061     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0  1
#&gt; SRR1740066     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740067     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740068     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740069     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740070     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740071     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740072     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740073     2   0.000      0.992 0.000 1.000  0  0
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1  0
#&gt; SRR1740078     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740079     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740080     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740081     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740082     1   0.497      0.324 0.548 0.452  0  0
#&gt; SRR1740083     1   0.497      0.325 0.548 0.452  0  0
#&gt; SRR1740084     1   0.413      0.691 0.740 0.260  0  0
#&gt; SRR1740085     1   0.353      0.770 0.808 0.192  0  0
#&gt; SRR1740086     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740087     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740088     1   0.000      0.896 1.000 0.000  0  0
#&gt; SRR1740089     1   0.000      0.896 1.000 0.000  0  0
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4    p5
#&gt; SRR1740034     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740035     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740036     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740037     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740038     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740039     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740040     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740041     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740042     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740043     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740044     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740045     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740046     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740048     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740047     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740049     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740050     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740051     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740052     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740054     2   0.430     0.0689 0.476 0.524  0  0 0.000
#&gt; SRR1740053     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740056     1   0.300     0.8468 0.840 0.148  0  0 0.012
#&gt; SRR1740055     2   0.148     0.9334 0.064 0.936  0  0 0.000
#&gt; SRR1740057     1   0.292     0.8599 0.852 0.132  0  0 0.016
#&gt; SRR1740058     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740059     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740060     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740061     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740062     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740063     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740064     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740065     4   0.000     1.0000 0.000 0.000  0  1 0.000
#&gt; SRR1740066     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740067     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740068     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740069     2   0.029     0.9417 0.000 0.992  0  0 0.008
#&gt; SRR1740070     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740071     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740072     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740073     2   0.120     0.9446 0.048 0.952  0  0 0.000
#&gt; SRR1740074     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740075     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740076     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740077     3   0.000     1.0000 0.000 0.000  1  0 0.000
#&gt; SRR1740078     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740079     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740080     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740081     5   0.029     1.0000 0.008 0.000  0  0 0.992
#&gt; SRR1740082     1   0.289     0.8091 0.824 0.176  0  0 0.000
#&gt; SRR1740083     1   0.265     0.8375 0.848 0.152  0  0 0.000
#&gt; SRR1740084     1   0.213     0.8672 0.892 0.108  0  0 0.000
#&gt; SRR1740085     1   0.196     0.8716 0.904 0.096  0  0 0.000
#&gt; SRR1740086     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740087     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740088     1   0.120     0.9004 0.952 0.000  0  0 0.048
#&gt; SRR1740089     1   0.120     0.9004 0.952 0.000  0  0 0.048
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3 p4 p5    p6
#&gt; SRR1740034     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740035     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740036     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740037     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740038     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740039     2   0.120      0.996 0.056 0.944  0  0  0 0.000
#&gt; SRR1740040     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740041     2   0.120      0.996 0.056 0.944  0  0  0 0.000
#&gt; SRR1740042     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740043     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740044     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740045     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740050     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740051     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740052     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740054     1   0.209      0.801 0.876 0.000  0  0  0 0.124
#&gt; SRR1740053     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740056     6   0.386      0.398 0.476 0.000  0  0  0 0.524
#&gt; SRR1740055     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740057     6   0.362      0.586 0.352 0.000  0  0  0 0.648
#&gt; SRR1740058     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740059     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740060     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740061     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740062     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740063     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740064     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740065     4   0.000      1.000 0.000 0.000  0  1  0 0.000
#&gt; SRR1740066     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740067     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740068     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740069     2   0.114      0.999 0.052 0.948  0  0  0 0.000
#&gt; SRR1740070     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740071     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740072     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740073     1   0.000      0.981 1.000 0.000  0  0  0 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1  0  0 0.000
#&gt; SRR1740078     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740079     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740080     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740081     5   0.000      1.000 0.000 0.000  0  0  1 0.000
#&gt; SRR1740082     6   0.386      0.408 0.472 0.000  0  0  0 0.528
#&gt; SRR1740083     6   0.371      0.559 0.380 0.000  0  0  0 0.620
#&gt; SRR1740084     6   0.384      0.450 0.452 0.000  0  0  0 0.548
#&gt; SRR1740085     6   0.375      0.540 0.396 0.000  0  0  0 0.604
#&gt; SRR1740086     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740087     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740088     6   0.000      0.778 0.000 0.000  0  0  0 1.000
#&gt; SRR1740089     6   0.000      0.778 0.000 0.000  0  0  0 1.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2501 0.751   0.751
#> 3 3 1.000           1.000       1.000         1.3280 0.668   0.557
#> 4 4 1.000           0.985       0.990         0.2190 0.875   0.702
#> 5 5 0.875           0.872       0.905         0.1129 0.917   0.717
#> 6 6 1.000           0.993       0.985         0.0525 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4
```

There is also optional best $k$ = 2 3 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     1       0          1  1  0
#&gt; SRR1740039     1       0          1  1  0
#&gt; SRR1740040     1       0          1  1  0
#&gt; SRR1740041     1       0          1  1  0
#&gt; SRR1740042     1       0          1  1  0
#&gt; SRR1740043     1       0          1  1  0
#&gt; SRR1740044     1       0          1  1  0
#&gt; SRR1740045     1       0          1  1  0
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     1       0          1  1  0
#&gt; SRR1740067     1       0          1  1  0
#&gt; SRR1740068     1       0          1  1  0
#&gt; SRR1740069     1       0          1  1  0
#&gt; SRR1740070     1       0          1  1  0
#&gt; SRR1740071     1       0          1  1  0
#&gt; SRR1740072     1       0          1  1  0
#&gt; SRR1740073     1       0          1  1  0
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1740034     1       0          1  1  0  0
#&gt; SRR1740035     1       0          1  1  0  0
#&gt; SRR1740036     1       0          1  1  0  0
#&gt; SRR1740037     1       0          1  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0
#&gt; SRR1740039     2       0          1  0  1  0
#&gt; SRR1740040     2       0          1  0  1  0
#&gt; SRR1740041     2       0          1  0  1  0
#&gt; SRR1740042     2       0          1  0  1  0
#&gt; SRR1740043     2       0          1  0  1  0
#&gt; SRR1740044     2       0          1  0  1  0
#&gt; SRR1740045     2       0          1  0  1  0
#&gt; SRR1740046     3       0          1  0  0  1
#&gt; SRR1740048     3       0          1  0  0  1
#&gt; SRR1740047     3       0          1  0  0  1
#&gt; SRR1740049     3       0          1  0  0  1
#&gt; SRR1740050     1       0          1  1  0  0
#&gt; SRR1740051     1       0          1  1  0  0
#&gt; SRR1740052     1       0          1  1  0  0
#&gt; SRR1740054     1       0          1  1  0  0
#&gt; SRR1740053     1       0          1  1  0  0
#&gt; SRR1740056     1       0          1  1  0  0
#&gt; SRR1740055     1       0          1  1  0  0
#&gt; SRR1740057     1       0          1  1  0  0
#&gt; SRR1740058     1       0          1  1  0  0
#&gt; SRR1740059     1       0          1  1  0  0
#&gt; SRR1740060     1       0          1  1  0  0
#&gt; SRR1740061     1       0          1  1  0  0
#&gt; SRR1740062     1       0          1  1  0  0
#&gt; SRR1740063     1       0          1  1  0  0
#&gt; SRR1740064     1       0          1  1  0  0
#&gt; SRR1740065     1       0          1  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0
#&gt; SRR1740067     2       0          1  0  1  0
#&gt; SRR1740068     2       0          1  0  1  0
#&gt; SRR1740069     2       0          1  0  1  0
#&gt; SRR1740070     2       0          1  0  1  0
#&gt; SRR1740071     2       0          1  0  1  0
#&gt; SRR1740072     2       0          1  0  1  0
#&gt; SRR1740073     2       0          1  0  1  0
#&gt; SRR1740074     3       0          1  0  0  1
#&gt; SRR1740075     3       0          1  0  0  1
#&gt; SRR1740076     3       0          1  0  0  1
#&gt; SRR1740077     3       0          1  0  0  1
#&gt; SRR1740078     1       0          1  1  0  0
#&gt; SRR1740079     1       0          1  1  0  0
#&gt; SRR1740080     1       0          1  1  0  0
#&gt; SRR1740081     1       0          1  1  0  0
#&gt; SRR1740082     1       0          1  1  0  0
#&gt; SRR1740083     1       0          1  1  0  0
#&gt; SRR1740084     1       0          1  1  0  0
#&gt; SRR1740085     1       0          1  1  0  0
#&gt; SRR1740086     1       0          1  1  0  0
#&gt; SRR1740087     1       0          1  1  0  0
#&gt; SRR1740088     1       0          1  1  0  0
#&gt; SRR1740089     1       0          1  1  0  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3    p4
#&gt; SRR1740034     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740035     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740036     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740037     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740038     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740050     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740051     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740052     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740054     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740053     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740056     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740055     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740057     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740058     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740059     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740060     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740061     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740062     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740063     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740064     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740065     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740066     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000  1  0 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000  0  1 0.000
#&gt; SRR1740078     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740079     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740080     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740081     1   0.187      0.946 0.928  0  0 0.072
#&gt; SRR1740082     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740083     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740084     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740085     4   0.000      1.000 0.000  0  0 1.000
#&gt; SRR1740086     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740087     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740088     1   0.000      0.974 1.000  0  0 0.000
#&gt; SRR1740089     1   0.000      0.974 1.000  0  0 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3    p4    p5
#&gt; SRR1740034     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740035     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740036     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740037     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740038     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740039     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740040     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740041     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740042     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740043     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740044     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740045     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740046     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740048     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740047     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740049     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740050     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740051     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740052     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740054     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740053     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740056     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740055     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740057     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740058     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740059     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740060     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740061     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740062     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740063     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740064     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740065     4   0.359      0.571  0  0  0 0.736 0.264
#&gt; SRR1740066     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740067     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740068     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740069     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740070     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740071     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740072     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740073     2   0.000      1.000  0  1  0 0.000 0.000
#&gt; SRR1740074     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740075     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740076     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740077     3   0.000      1.000  0  0  1 0.000 0.000
#&gt; SRR1740078     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740079     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740080     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740081     4   0.393      0.534  0  0  0 0.672 0.328
#&gt; SRR1740082     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740083     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740084     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740085     1   0.000      1.000  1  0  0 0.000 0.000
#&gt; SRR1740086     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740087     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740088     5   0.000      1.000  0  0  0 0.000 1.000
#&gt; SRR1740089     5   0.000      1.000  0  0  0 0.000 1.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2 p3    p4    p5 p6
#&gt; SRR1740034     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740035     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740036     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740037     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740038     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740039     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740040     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740041     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740042     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740043     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740044     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740045     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740046     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740048     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740047     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740049     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740050     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740051     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740052     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740054     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740053     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740056     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740055     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740057     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740058     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740059     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740060     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740061     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740062     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740063     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740064     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740065     4   0.114      1.000  0 0.000  0 0.948 0.052  0
#&gt; SRR1740066     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740067     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740068     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740069     2   0.114      0.977  0 0.948  0 0.052 0.000  0
#&gt; SRR1740070     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740071     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740072     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740073     2   0.000      0.977  0 1.000  0 0.000 0.000  0
#&gt; SRR1740074     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740075     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740076     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740077     3   0.000      1.000  0 0.000  1 0.000 0.000  0
#&gt; SRR1740078     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740079     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740080     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740081     5   0.000      1.000  0 0.000  0 0.000 1.000  0
#&gt; SRR1740082     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740083     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740084     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740085     1   0.000      1.000  1 0.000  0 0.000 0.000  0
#&gt; SRR1740086     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740087     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740088     6   0.000      1.000  0 0.000  0 0.000 0.000  1
#&gt; SRR1740089     6   0.000      1.000  0 0.000  0 0.000 0.000  1
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2501 0.751   0.751
#> 3 3 1.000           0.998       0.983         1.2674 0.668   0.557
#> 4 4 0.709           0.802       0.788         0.2328 0.834   0.602
#> 5 5 0.699           0.757       0.747         0.0922 1.000   1.000
#> 6 6 0.768           0.909       0.719         0.0570 0.917   0.670
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     1       0          1  1  0
#&gt; SRR1740039     1       0          1  1  0
#&gt; SRR1740040     1       0          1  1  0
#&gt; SRR1740041     1       0          1  1  0
#&gt; SRR1740042     1       0          1  1  0
#&gt; SRR1740043     1       0          1  1  0
#&gt; SRR1740044     1       0          1  1  0
#&gt; SRR1740045     1       0          1  1  0
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     1       0          1  1  0
#&gt; SRR1740067     1       0          1  1  0
#&gt; SRR1740068     1       0          1  1  0
#&gt; SRR1740069     1       0          1  1  0
#&gt; SRR1740070     1       0          1  1  0
#&gt; SRR1740071     1       0          1  1  0
#&gt; SRR1740072     1       0          1  1  0
#&gt; SRR1740073     1       0          1  1  0
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740035     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740036     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740037     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740038     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740039     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740040     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740041     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740042     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740043     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740044     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740045     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740046     3   0.000      0.984 0.000 0.000 1.000
#&gt; SRR1740048     3   0.000      0.984 0.000 0.000 1.000
#&gt; SRR1740047     3   0.000      0.984 0.000 0.000 1.000
#&gt; SRR1740049     3   0.000      0.984 0.000 0.000 1.000
#&gt; SRR1740050     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740051     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740052     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740054     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740053     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740056     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740055     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740057     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740058     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740059     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740060     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740061     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740062     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740063     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740064     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740065     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740066     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740067     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740068     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740069     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740070     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740071     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740072     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740073     2   0.175      1.000 0.048 0.952 0.000
#&gt; SRR1740074     3   0.175      0.984 0.000 0.048 0.952
#&gt; SRR1740075     3   0.175      0.984 0.000 0.048 0.952
#&gt; SRR1740076     3   0.175      0.984 0.000 0.048 0.952
#&gt; SRR1740077     3   0.175      0.984 0.000 0.048 0.952
#&gt; SRR1740078     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740079     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740080     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740081     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740082     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740083     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740084     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740085     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740086     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740087     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740088     1   0.000      1.000 1.000 0.000 0.000
#&gt; SRR1740089     1   0.000      1.000 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     4  0.4679      0.670 0.352 0.000 0.000 0.648
#&gt; SRR1740035     4  0.4697      0.667 0.356 0.000 0.000 0.644
#&gt; SRR1740036     4  0.4697      0.667 0.356 0.000 0.000 0.644
#&gt; SRR1740037     4  0.4679      0.670 0.352 0.000 0.000 0.648
#&gt; SRR1740038     2  0.0336      0.929 0.008 0.992 0.000 0.000
#&gt; SRR1740039     2  0.0336      0.929 0.008 0.992 0.000 0.000
#&gt; SRR1740040     2  0.0336      0.929 0.008 0.992 0.000 0.000
#&gt; SRR1740041     2  0.0336      0.929 0.008 0.992 0.000 0.000
#&gt; SRR1740042     2  0.3351      0.929 0.008 0.844 0.000 0.148
#&gt; SRR1740043     2  0.3351      0.929 0.008 0.844 0.000 0.148
#&gt; SRR1740044     2  0.3351      0.929 0.008 0.844 0.000 0.148
#&gt; SRR1740045     2  0.3351      0.929 0.008 0.844 0.000 0.148
#&gt; SRR1740046     3  0.0188      0.969 0.000 0.004 0.996 0.000
#&gt; SRR1740048     3  0.0188      0.969 0.000 0.000 0.996 0.004
#&gt; SRR1740047     3  0.0188      0.969 0.000 0.000 0.996 0.004
#&gt; SRR1740049     3  0.0188      0.969 0.000 0.004 0.996 0.000
#&gt; SRR1740050     1  0.1557      0.720 0.944 0.000 0.000 0.056
#&gt; SRR1740051     1  0.1716      0.716 0.936 0.000 0.000 0.064
#&gt; SRR1740052     1  0.1716      0.716 0.936 0.000 0.000 0.064
#&gt; SRR1740054     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740053     1  0.1716      0.716 0.936 0.000 0.000 0.064
#&gt; SRR1740056     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740055     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740057     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740058     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740059     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740060     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740061     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740062     4  0.4746      0.654 0.368 0.000 0.000 0.632
#&gt; SRR1740063     4  0.4746      0.654 0.368 0.000 0.000 0.632
#&gt; SRR1740064     4  0.4746      0.654 0.368 0.000 0.000 0.632
#&gt; SRR1740065     4  0.4746      0.654 0.368 0.000 0.000 0.632
#&gt; SRR1740066     2  0.0672      0.929 0.008 0.984 0.000 0.008
#&gt; SRR1740067     2  0.0672      0.929 0.008 0.984 0.000 0.008
#&gt; SRR1740068     2  0.0672      0.929 0.008 0.984 0.000 0.008
#&gt; SRR1740069     2  0.0672      0.929 0.008 0.984 0.000 0.008
#&gt; SRR1740070     2  0.3450      0.929 0.008 0.836 0.000 0.156
#&gt; SRR1740071     2  0.3450      0.929 0.008 0.836 0.000 0.156
#&gt; SRR1740072     2  0.3450      0.929 0.008 0.836 0.000 0.156
#&gt; SRR1740073     2  0.3450      0.929 0.008 0.836 0.000 0.156
#&gt; SRR1740074     3  0.2081      0.969 0.000 0.000 0.916 0.084
#&gt; SRR1740075     3  0.2081      0.969 0.000 0.000 0.916 0.084
#&gt; SRR1740076     3  0.2197      0.969 0.000 0.004 0.916 0.080
#&gt; SRR1740077     3  0.2197      0.969 0.000 0.004 0.916 0.080
#&gt; SRR1740078     1  0.1557      0.720 0.944 0.000 0.000 0.056
#&gt; SRR1740079     1  0.1716      0.716 0.936 0.000 0.000 0.064
#&gt; SRR1740080     1  0.1716      0.716 0.936 0.000 0.000 0.064
#&gt; SRR1740081     1  0.1557      0.720 0.944 0.000 0.000 0.056
#&gt; SRR1740082     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740083     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740084     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740085     1  0.3764      0.712 0.784 0.000 0.000 0.216
#&gt; SRR1740086     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740087     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740088     4  0.4955      0.694 0.444 0.000 0.000 0.556
#&gt; SRR1740089     4  0.4955      0.694 0.444 0.000 0.000 0.556
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1    p2    p3    p4    p5
#&gt; SRR1740034     4  0.6482      0.622 NA 0.000 0.000 0.492 0.232
#&gt; SRR1740035     4  0.6482      0.622 NA 0.000 0.000 0.492 0.232
#&gt; SRR1740036     4  0.6482      0.622 NA 0.000 0.000 0.492 0.232
#&gt; SRR1740037     4  0.6482      0.622 NA 0.000 0.000 0.492 0.232
#&gt; SRR1740038     2  0.3932      0.838 NA 0.672 0.000 0.000 0.000
#&gt; SRR1740039     2  0.3932      0.838 NA 0.672 0.000 0.000 0.000
#&gt; SRR1740040     2  0.3932      0.838 NA 0.672 0.000 0.000 0.000
#&gt; SRR1740041     2  0.3932      0.838 NA 0.672 0.000 0.000 0.000
#&gt; SRR1740042     2  0.0992      0.844 NA 0.968 0.000 0.000 0.024
#&gt; SRR1740043     2  0.0992      0.844 NA 0.968 0.000 0.000 0.024
#&gt; SRR1740044     2  0.0992      0.844 NA 0.968 0.000 0.000 0.024
#&gt; SRR1740045     2  0.0992      0.844 NA 0.968 0.000 0.000 0.024
#&gt; SRR1740046     3  0.2511      0.955 NA 0.000 0.892 0.000 0.028
#&gt; SRR1740048     3  0.2482      0.955 NA 0.000 0.892 0.000 0.024
#&gt; SRR1740047     3  0.2482      0.955 NA 0.000 0.892 0.000 0.024
#&gt; SRR1740049     3  0.2511      0.955 NA 0.000 0.892 0.000 0.028
#&gt; SRR1740050     5  0.6398      0.707 NA 0.000 0.000 0.200 0.500
#&gt; SRR1740051     5  0.6410      0.707 NA 0.000 0.000 0.200 0.496
#&gt; SRR1740052     5  0.6410      0.707 NA 0.000 0.000 0.200 0.496
#&gt; SRR1740054     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740053     5  0.6410      0.707 NA 0.000 0.000 0.200 0.496
#&gt; SRR1740056     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740055     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740057     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740058     4  0.0798      0.657 NA 0.000 0.000 0.976 0.016
#&gt; SRR1740059     4  0.0798      0.657 NA 0.000 0.000 0.976 0.016
#&gt; SRR1740060     4  0.0798      0.657 NA 0.000 0.000 0.976 0.016
#&gt; SRR1740061     4  0.0798      0.657 NA 0.000 0.000 0.976 0.016
#&gt; SRR1740062     4  0.6500      0.619 NA 0.000 0.000 0.488 0.236
#&gt; SRR1740063     4  0.6500      0.619 NA 0.000 0.000 0.488 0.236
#&gt; SRR1740064     4  0.6500      0.619 NA 0.000 0.000 0.488 0.236
#&gt; SRR1740065     4  0.6500      0.619 NA 0.000 0.000 0.488 0.236
#&gt; SRR1740066     2  0.4777      0.838 NA 0.680 0.000 0.000 0.052
#&gt; SRR1740067     2  0.4777      0.838 NA 0.680 0.000 0.000 0.052
#&gt; SRR1740068     2  0.4777      0.838 NA 0.680 0.000 0.000 0.052
#&gt; SRR1740069     2  0.4777      0.838 NA 0.680 0.000 0.000 0.052
#&gt; SRR1740070     2  0.0000      0.844 NA 1.000 0.000 0.000 0.000
#&gt; SRR1740071     2  0.0000      0.844 NA 1.000 0.000 0.000 0.000
#&gt; SRR1740072     2  0.0000      0.844 NA 1.000 0.000 0.000 0.000
#&gt; SRR1740073     2  0.0000      0.844 NA 1.000 0.000 0.000 0.000
#&gt; SRR1740074     3  0.0404      0.954 NA 0.000 0.988 0.000 0.012
#&gt; SRR1740075     3  0.0404      0.954 NA 0.000 0.988 0.000 0.012
#&gt; SRR1740076     3  0.0404      0.954 NA 0.000 0.988 0.000 0.000
#&gt; SRR1740077     3  0.0404      0.954 NA 0.000 0.988 0.000 0.000
#&gt; SRR1740078     5  0.6398      0.707 NA 0.000 0.000 0.200 0.500
#&gt; SRR1740079     5  0.6398      0.707 NA 0.000 0.000 0.200 0.500
#&gt; SRR1740080     5  0.6398      0.707 NA 0.000 0.000 0.200 0.500
#&gt; SRR1740081     5  0.6398      0.707 NA 0.000 0.000 0.200 0.500
#&gt; SRR1740082     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740083     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740084     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740085     5  0.2852      0.678 NA 0.000 0.000 0.172 0.828
#&gt; SRR1740086     4  0.0510      0.657 NA 0.000 0.000 0.984 0.016
#&gt; SRR1740087     4  0.0510      0.657 NA 0.000 0.000 0.984 0.016
#&gt; SRR1740088     4  0.0510      0.657 NA 0.000 0.000 0.984 0.016
#&gt; SRR1740089     4  0.0510      0.657 NA 0.000 0.000 0.984 0.016
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR1740034     4  0.2907      0.967 0.028 0.000 0.000 0.860 0.096 0.016
#&gt; SRR1740035     4  0.2858      0.969 0.028 0.000 0.000 0.864 0.092 0.016
#&gt; SRR1740036     4  0.2858      0.969 0.028 0.000 0.000 0.864 0.092 0.016
#&gt; SRR1740037     4  0.2907      0.967 0.028 0.000 0.000 0.860 0.096 0.016
#&gt; SRR1740038     2  0.1682      0.773 0.052 0.928 0.000 0.020 0.000 0.000
#&gt; SRR1740039     2  0.1682      0.773 0.052 0.928 0.000 0.020 0.000 0.000
#&gt; SRR1740040     2  0.1682      0.773 0.052 0.928 0.000 0.020 0.000 0.000
#&gt; SRR1740041     2  0.1682      0.773 0.052 0.928 0.000 0.020 0.000 0.000
#&gt; SRR1740042     2  0.5871      0.771 0.224 0.556 0.000 0.016 0.000 0.204
#&gt; SRR1740043     2  0.5871      0.771 0.224 0.556 0.000 0.016 0.000 0.204
#&gt; SRR1740044     2  0.5871      0.771 0.224 0.556 0.000 0.016 0.000 0.204
#&gt; SRR1740045     2  0.5927      0.771 0.220 0.556 0.000 0.020 0.000 0.204
#&gt; SRR1740046     3  0.3592      0.915 0.124 0.000 0.812 0.044 0.000 0.020
#&gt; SRR1740048     3  0.3664      0.915 0.116 0.000 0.812 0.044 0.000 0.028
#&gt; SRR1740047     3  0.3664      0.915 0.116 0.000 0.812 0.044 0.000 0.028
#&gt; SRR1740049     3  0.3592      0.915 0.124 0.000 0.812 0.044 0.000 0.020
#&gt; SRR1740050     5  0.0146      0.978 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1740051     5  0.1088      0.968 0.024 0.000 0.000 0.000 0.960 0.016
#&gt; SRR1740052     5  0.1088      0.968 0.024 0.000 0.000 0.000 0.960 0.016
#&gt; SRR1740054     1  0.6210      0.995 0.472 0.000 0.000 0.172 0.332 0.024
#&gt; SRR1740053     5  0.1088      0.968 0.024 0.000 0.000 0.000 0.960 0.016
#&gt; SRR1740056     1  0.6210      0.995 0.472 0.000 0.000 0.172 0.332 0.024
#&gt; SRR1740055     1  0.6275      0.992 0.468 0.000 0.000 0.172 0.332 0.028
#&gt; SRR1740057     1  0.6210      0.995 0.472 0.000 0.000 0.172 0.332 0.024
#&gt; SRR1740058     6  0.6153      0.968 0.052 0.000 0.000 0.216 0.164 0.568
#&gt; SRR1740059     6  0.6153      0.968 0.052 0.000 0.000 0.216 0.164 0.568
#&gt; SRR1740060     6  0.6153      0.968 0.052 0.000 0.000 0.216 0.164 0.568
#&gt; SRR1740061     6  0.6153      0.968 0.052 0.000 0.000 0.216 0.164 0.568
#&gt; SRR1740062     4  0.1765      0.971 0.000 0.000 0.000 0.904 0.096 0.000
#&gt; SRR1740063     4  0.1765      0.971 0.000 0.000 0.000 0.904 0.096 0.000
#&gt; SRR1740064     4  0.1765      0.971 0.000 0.000 0.000 0.904 0.096 0.000
#&gt; SRR1740065     4  0.1765      0.971 0.000 0.000 0.000 0.904 0.096 0.000
#&gt; SRR1740066     2  0.0000      0.773 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740067     2  0.0000      0.773 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740068     2  0.0000      0.773 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740069     2  0.0000      0.773 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR1740070     2  0.5529      0.771 0.152 0.560 0.000 0.004 0.000 0.284
#&gt; SRR1740071     2  0.5529      0.771 0.152 0.560 0.000 0.004 0.000 0.284
#&gt; SRR1740072     2  0.5542      0.771 0.156 0.560 0.000 0.004 0.000 0.280
#&gt; SRR1740073     2  0.5542      0.771 0.156 0.560 0.000 0.004 0.000 0.280
#&gt; SRR1740074     3  0.0632      0.913 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1740075     3  0.0632      0.913 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR1740076     3  0.0547      0.913 0.020 0.000 0.980 0.000 0.000 0.000
#&gt; SRR1740077     3  0.0547      0.913 0.020 0.000 0.980 0.000 0.000 0.000
#&gt; SRR1740078     5  0.0146      0.978 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1740079     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740080     5  0.0000      0.978 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR1740081     5  0.0146      0.978 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR1740082     1  0.6068      0.995 0.480 0.000 0.000 0.172 0.332 0.016
#&gt; SRR1740083     1  0.6068      0.995 0.480 0.000 0.000 0.172 0.332 0.016
#&gt; SRR1740084     1  0.6068      0.995 0.480 0.000 0.000 0.172 0.332 0.016
#&gt; SRR1740085     1  0.6068      0.995 0.480 0.000 0.000 0.172 0.332 0.016
#&gt; SRR1740086     6  0.5133      0.968 0.000 0.000 0.000 0.212 0.164 0.624
#&gt; SRR1740087     6  0.5133      0.968 0.000 0.000 0.000 0.212 0.164 0.624
#&gt; SRR1740088     6  0.5133      0.968 0.000 0.000 0.000 0.212 0.164 0.624
#&gt; SRR1740089     6  0.5133      0.968 0.000 0.000 0.000 0.212 0.164 0.624
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000          0.499 0.501   0.501
#> 3 3 0.917           0.951       0.963          0.166 0.917   0.834
#> 4 4 0.834           0.939       0.913          0.114 0.958   0.901
#> 5 5 0.834           0.915       0.909          0.158 0.875   0.669
#> 6 6 0.917           0.979       0.974          0.103 0.917   0.670
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     2       0          1  0  1
#&gt; SRR1740039     2       0          1  0  1
#&gt; SRR1740040     2       0          1  0  1
#&gt; SRR1740041     2       0          1  0  1
#&gt; SRR1740042     2       0          1  0  1
#&gt; SRR1740043     2       0          1  0  1
#&gt; SRR1740044     2       0          1  0  1
#&gt; SRR1740045     2       0          1  0  1
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     2       0          1  0  1
#&gt; SRR1740067     2       0          1  0  1
#&gt; SRR1740068     2       0          1  0  1
#&gt; SRR1740069     2       0          1  0  1
#&gt; SRR1740070     2       0          1  0  1
#&gt; SRR1740071     2       0          1  0  1
#&gt; SRR1740072     2       0          1  0  1
#&gt; SRR1740073     2       0          1  0  1
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3
#&gt; SRR1740034     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740035     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740036     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740037     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740038     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740039     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740040     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740041     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740042     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740043     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740044     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740045     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740046     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740048     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740047     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740049     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740050     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740051     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740052     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740054     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740053     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740056     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740055     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740057     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740058     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740059     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740060     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740061     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740062     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740063     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740064     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740065     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740066     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740067     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740068     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740069     2  0.0000      0.844 0.000 1.000 0.000
#&gt; SRR1740070     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740071     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740072     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740073     2  0.5138      0.819 0.000 0.748 0.252
#&gt; SRR1740074     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740075     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740076     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740077     3  0.0237      1.000 0.000 0.004 0.996
#&gt; SRR1740078     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740079     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740080     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740081     1  0.0237      0.997 0.996 0.000 0.004
#&gt; SRR1740082     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740083     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740084     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740085     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740086     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740087     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740088     1  0.0000      0.999 1.000 0.000 0.000
#&gt; SRR1740089     1  0.0000      0.999 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2    p3    p4
#&gt; SRR1740034     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740035     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740036     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740037     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740042     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740043     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740044     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740045     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740050     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740051     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740052     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740054     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740053     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740056     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740055     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740057     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740058     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740059     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740060     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740061     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740062     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740063     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740064     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740065     1   0.208      0.902 0.916 0.000 0.000 0.084
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR1740070     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740071     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740072     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740073     4   0.520      1.000 0.000 0.264 0.036 0.700
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000 1.000 0.000
#&gt; SRR1740078     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740079     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740080     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740081     1   0.384      0.821 0.776 0.000 0.000 0.224
#&gt; SRR1740082     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740083     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740084     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740085     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740086     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740087     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740088     1   0.000      0.926 1.000 0.000 0.000 0.000
#&gt; SRR1740089     1   0.000      0.926 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1740034     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740035     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740036     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740037     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740038     2   0.051      0.993 0.000 0.984  0 0.000 0.016
#&gt; SRR1740039     2   0.051      0.993 0.000 0.984  0 0.000 0.016
#&gt; SRR1740040     2   0.051      0.993 0.000 0.984  0 0.000 0.016
#&gt; SRR1740041     2   0.051      0.993 0.000 0.984  0 0.000 0.016
#&gt; SRR1740042     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740043     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740044     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740045     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740050     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740051     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740052     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740054     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740053     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740056     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740055     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740057     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740058     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740059     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740060     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740061     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740062     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740063     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740064     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740065     1   0.278      0.712 0.880 0.000  0 0.048 0.072
#&gt; SRR1740066     2   0.000      0.993 0.000 1.000  0 0.000 0.000
#&gt; SRR1740067     2   0.000      0.993 0.000 1.000  0 0.000 0.000
#&gt; SRR1740068     2   0.000      0.993 0.000 1.000  0 0.000 0.000
#&gt; SRR1740069     2   0.000      0.993 0.000 1.000  0 0.000 0.000
#&gt; SRR1740070     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740071     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740072     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740073     4   0.127      1.000 0.000 0.052  0 0.948 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740078     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740079     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740080     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740081     5   0.051      1.000 0.016 0.000  0 0.000 0.984
#&gt; SRR1740082     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740083     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740084     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740085     1   0.340      0.851 0.780 0.000  0 0.004 0.216
#&gt; SRR1740086     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740087     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740088     1   0.331      0.852 0.776 0.000  0 0.000 0.224
#&gt; SRR1740089     1   0.331      0.852 0.776 0.000  0 0.000 0.224
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5    p6
#&gt; SRR1740034     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740035     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740036     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740037     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740038     2  0.1151      0.987 0.012 0.956  0 0.032 0.000 0.000
#&gt; SRR1740039     2  0.1151      0.987 0.012 0.956  0 0.032 0.000 0.000
#&gt; SRR1740040     2  0.1151      0.987 0.012 0.956  0 0.032 0.000 0.000
#&gt; SRR1740041     2  0.1151      0.987 0.012 0.956  0 0.032 0.000 0.000
#&gt; SRR1740042     1  0.0000      0.997 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1740043     1  0.0000      0.997 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1740044     1  0.0000      0.997 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1740045     1  0.0000      0.997 1.000 0.000  0 0.000 0.000 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740050     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740051     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740052     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740054     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740053     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740056     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740055     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740057     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740058     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740059     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740060     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740061     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740062     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740063     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740064     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740065     4  0.0937      1.000 0.000 0.000  0 0.960 0.000 0.040
#&gt; SRR1740066     2  0.0363      0.987 0.012 0.988  0 0.000 0.000 0.000
#&gt; SRR1740067     2  0.0363      0.987 0.012 0.988  0 0.000 0.000 0.000
#&gt; SRR1740068     2  0.0363      0.987 0.012 0.988  0 0.000 0.000 0.000
#&gt; SRR1740069     2  0.0363      0.987 0.012 0.988  0 0.000 0.000 0.000
#&gt; SRR1740070     1  0.0260      0.997 0.992 0.000  0 0.008 0.000 0.000
#&gt; SRR1740071     1  0.0260      0.997 0.992 0.000  0 0.008 0.000 0.000
#&gt; SRR1740072     1  0.0260      0.997 0.992 0.000  0 0.008 0.000 0.000
#&gt; SRR1740073     1  0.0260      0.997 0.992 0.000  0 0.008 0.000 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 0.000
#&gt; SRR1740078     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740079     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740080     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740081     5  0.0000      1.000 0.000 0.000  0 0.000 1.000 0.000
#&gt; SRR1740082     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740083     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740084     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740085     6  0.0000      0.936 0.000 0.000  0 0.000 0.000 1.000
#&gt; SRR1740086     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740087     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740088     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
#&gt; SRR1740089     6  0.2264      0.934 0.000 0.012  0 0.096 0.004 0.888
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2     1           1.000       1.000         0.2501 0.751   0.751
#> 3 3     1           1.000       1.000         1.3280 0.668   0.557
#> 4 4     1           0.936       0.975         0.2535 0.850   0.641
#> 5 5     1           0.973       0.981         0.0947 0.918   0.700
#> 6 6     1           0.999       0.999         0.0406 0.948   0.753
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3 4 5
```

There is also optional best $k$ = 2 3 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     1       0          1  1  0
#&gt; SRR1740039     1       0          1  1  0
#&gt; SRR1740040     1       0          1  1  0
#&gt; SRR1740041     1       0          1  1  0
#&gt; SRR1740042     1       0          1  1  0
#&gt; SRR1740043     1       0          1  1  0
#&gt; SRR1740044     1       0          1  1  0
#&gt; SRR1740045     1       0          1  1  0
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     1       0          1  1  0
#&gt; SRR1740067     1       0          1  1  0
#&gt; SRR1740068     1       0          1  1  0
#&gt; SRR1740069     1       0          1  1  0
#&gt; SRR1740070     1       0          1  1  0
#&gt; SRR1740071     1       0          1  1  0
#&gt; SRR1740072     1       0          1  1  0
#&gt; SRR1740073     1       0          1  1  0
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3
#&gt; SRR1740034     1       0          1  1  0  0
#&gt; SRR1740035     1       0          1  1  0  0
#&gt; SRR1740036     1       0          1  1  0  0
#&gt; SRR1740037     1       0          1  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0
#&gt; SRR1740039     2       0          1  0  1  0
#&gt; SRR1740040     2       0          1  0  1  0
#&gt; SRR1740041     2       0          1  0  1  0
#&gt; SRR1740042     2       0          1  0  1  0
#&gt; SRR1740043     2       0          1  0  1  0
#&gt; SRR1740044     2       0          1  0  1  0
#&gt; SRR1740045     2       0          1  0  1  0
#&gt; SRR1740046     3       0          1  0  0  1
#&gt; SRR1740048     3       0          1  0  0  1
#&gt; SRR1740047     3       0          1  0  0  1
#&gt; SRR1740049     3       0          1  0  0  1
#&gt; SRR1740050     1       0          1  1  0  0
#&gt; SRR1740051     1       0          1  1  0  0
#&gt; SRR1740052     1       0          1  1  0  0
#&gt; SRR1740054     1       0          1  1  0  0
#&gt; SRR1740053     1       0          1  1  0  0
#&gt; SRR1740056     1       0          1  1  0  0
#&gt; SRR1740055     1       0          1  1  0  0
#&gt; SRR1740057     1       0          1  1  0  0
#&gt; SRR1740058     1       0          1  1  0  0
#&gt; SRR1740059     1       0          1  1  0  0
#&gt; SRR1740060     1       0          1  1  0  0
#&gt; SRR1740061     1       0          1  1  0  0
#&gt; SRR1740062     1       0          1  1  0  0
#&gt; SRR1740063     1       0          1  1  0  0
#&gt; SRR1740064     1       0          1  1  0  0
#&gt; SRR1740065     1       0          1  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0
#&gt; SRR1740067     2       0          1  0  1  0
#&gt; SRR1740068     2       0          1  0  1  0
#&gt; SRR1740069     2       0          1  0  1  0
#&gt; SRR1740070     2       0          1  0  1  0
#&gt; SRR1740071     2       0          1  0  1  0
#&gt; SRR1740072     2       0          1  0  1  0
#&gt; SRR1740073     2       0          1  0  1  0
#&gt; SRR1740074     3       0          1  0  0  1
#&gt; SRR1740075     3       0          1  0  0  1
#&gt; SRR1740076     3       0          1  0  0  1
#&gt; SRR1740077     3       0          1  0  0  1
#&gt; SRR1740078     1       0          1  1  0  0
#&gt; SRR1740079     1       0          1  1  0  0
#&gt; SRR1740080     1       0          1  1  0  0
#&gt; SRR1740081     1       0          1  1  0  0
#&gt; SRR1740082     1       0          1  1  0  0
#&gt; SRR1740083     1       0          1  1  0  0
#&gt; SRR1740084     1       0          1  1  0  0
#&gt; SRR1740085     1       0          1  1  0  0
#&gt; SRR1740086     1       0          1  1  0  0
#&gt; SRR1740087     1       0          1  1  0  0
#&gt; SRR1740088     1       0          1  1  0  0
#&gt; SRR1740089     1       0          1  1  0  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3    p4
#&gt; SRR1740034     4  0.0000     0.8937 0.000  0  0 1.000
#&gt; SRR1740035     1  0.4992     0.0208 0.524  0  0 0.476
#&gt; SRR1740036     4  0.4994     0.0217 0.480  0  0 0.520
#&gt; SRR1740037     4  0.2281     0.8257 0.096  0  0 0.904
#&gt; SRR1740038     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740039     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740040     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740041     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740042     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740043     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740044     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740045     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740046     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740048     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740047     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740049     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740050     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740051     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740052     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740054     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740053     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740056     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740055     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740057     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740058     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740059     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740060     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740061     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740062     1  0.0921     0.9494 0.972  0  0 0.028
#&gt; SRR1740063     1  0.0921     0.9494 0.972  0  0 0.028
#&gt; SRR1740064     1  0.0921     0.9494 0.972  0  0 0.028
#&gt; SRR1740065     1  0.0921     0.9494 0.972  0  0 0.028
#&gt; SRR1740066     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740067     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740068     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740069     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740070     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740071     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740072     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740073     2  0.0000     1.0000 0.000  1  0 0.000
#&gt; SRR1740074     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740075     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740076     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740077     3  0.0000     1.0000 0.000  0  1 0.000
#&gt; SRR1740078     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740079     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740080     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740081     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740082     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740083     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740084     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740085     1  0.0000     0.9681 1.000  0  0 0.000
#&gt; SRR1740086     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740087     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740088     4  0.0921     0.9206 0.028  0  0 0.972
#&gt; SRR1740089     4  0.0921     0.9206 0.028  0  0 0.972
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2 p3    p4    p5
#&gt; SRR1740034     4   0.127      0.918 0.052  0  0 0.948 0.000
#&gt; SRR1740035     4   0.342      0.763 0.240  0  0 0.760 0.000
#&gt; SRR1740036     4   0.342      0.763 0.240  0  0 0.760 0.000
#&gt; SRR1740037     4   0.242      0.871 0.132  0  0 0.868 0.000
#&gt; SRR1740038     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740048     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740047     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740049     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740050     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740051     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740052     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740054     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740053     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740056     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740055     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740057     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740058     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740059     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740060     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740061     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740062     1   0.000      0.957 1.000  0  0 0.000 0.000
#&gt; SRR1740063     1   0.000      0.957 1.000  0  0 0.000 0.000
#&gt; SRR1740064     1   0.000      0.957 1.000  0  0 0.000 0.000
#&gt; SRR1740065     1   0.000      0.957 1.000  0  0 0.000 0.000
#&gt; SRR1740066     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000  1  0 0.000 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740075     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740076     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740077     3   0.000      1.000 0.000  0  1 0.000 0.000
#&gt; SRR1740078     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740079     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740080     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740081     5   0.000      1.000 0.000  0  0 0.000 1.000
#&gt; SRR1740082     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740083     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740084     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740085     1   0.127      0.978 0.948  0  0 0.000 0.052
#&gt; SRR1740086     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740087     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740088     4   0.000      0.940 0.000  0  0 1.000 0.000
#&gt; SRR1740089     4   0.000      0.940 0.000  0  0 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4 p5    p6
#&gt; SRR1740034     4  0.0146      0.997 0.000 0.000  0 0.996  0 0.004
#&gt; SRR1740035     4  0.0146      0.997 0.000 0.000  0 0.996  0 0.004
#&gt; SRR1740036     4  0.0146      0.997 0.000 0.000  0 0.996  0 0.004
#&gt; SRR1740037     4  0.0146      0.997 0.000 0.000  0 0.996  0 0.004
#&gt; SRR1740038     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740039     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740040     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740041     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740042     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740043     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740044     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740045     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740050     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740051     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740052     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740054     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740053     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740056     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740055     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740057     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740058     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740059     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740060     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740061     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740062     4  0.0146      0.997 0.004 0.000  0 0.996  0 0.000
#&gt; SRR1740063     4  0.0146      0.997 0.004 0.000  0 0.996  0 0.000
#&gt; SRR1740064     4  0.0146      0.997 0.004 0.000  0 0.996  0 0.000
#&gt; SRR1740065     4  0.0146      0.997 0.004 0.000  0 0.996  0 0.000
#&gt; SRR1740066     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740067     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740068     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740069     2  0.0000      0.998 0.000 1.000  0 0.000  0 0.000
#&gt; SRR1740070     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740071     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740072     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740073     2  0.0146      0.998 0.000 0.996  0 0.004  0 0.000
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.000  0 0.000
#&gt; SRR1740078     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740079     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740080     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740081     5  0.0000      1.000 0.000 0.000  0 0.000  1 0.000
#&gt; SRR1740082     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740083     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740084     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740085     1  0.0000      1.000 1.000 0.000  0 0.000  0 0.000
#&gt; SRR1740086     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740087     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740088     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
#&gt; SRR1740089     6  0.0000      1.000 0.000 0.000  0 0.000  0 1.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.501           0.804       0.837         0.4168 0.584   0.584
#> 3 3 0.834           0.967       0.981         0.4240 0.834   0.716
#> 4 4 1.000           1.000       1.000         0.1909 0.875   0.702
#> 5 5 1.000           0.987       0.989         0.1175 0.917   0.717
#> 6 6 1.000           1.000       1.000         0.0526 0.958   0.802
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 4 5
```

There is also optional best $k$ = 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2
#&gt; SRR1740034     1   0.955      0.746 0.624 0.376
#&gt; SRR1740035     1   0.955      0.746 0.624 0.376
#&gt; SRR1740036     1   0.955      0.746 0.624 0.376
#&gt; SRR1740037     1   0.955      0.746 0.624 0.376
#&gt; SRR1740038     2   0.000      1.000 0.000 1.000
#&gt; SRR1740039     2   0.000      1.000 0.000 1.000
#&gt; SRR1740040     2   0.000      1.000 0.000 1.000
#&gt; SRR1740041     2   0.000      1.000 0.000 1.000
#&gt; SRR1740042     2   0.000      1.000 0.000 1.000
#&gt; SRR1740043     2   0.000      1.000 0.000 1.000
#&gt; SRR1740044     2   0.000      1.000 0.000 1.000
#&gt; SRR1740045     2   0.000      1.000 0.000 1.000
#&gt; SRR1740046     1   0.000      0.697 1.000 0.000
#&gt; SRR1740048     1   0.000      0.697 1.000 0.000
#&gt; SRR1740047     1   0.000      0.697 1.000 0.000
#&gt; SRR1740049     1   0.000      0.697 1.000 0.000
#&gt; SRR1740050     1   0.000      0.697 1.000 0.000
#&gt; SRR1740051     1   0.000      0.697 1.000 0.000
#&gt; SRR1740052     1   0.000      0.697 1.000 0.000
#&gt; SRR1740054     1   0.961      0.743 0.616 0.384
#&gt; SRR1740053     1   0.000      0.697 1.000 0.000
#&gt; SRR1740056     1   0.961      0.743 0.616 0.384
#&gt; SRR1740055     1   0.961      0.743 0.616 0.384
#&gt; SRR1740057     1   0.961      0.743 0.616 0.384
#&gt; SRR1740058     1   0.961      0.743 0.616 0.384
#&gt; SRR1740059     1   0.961      0.743 0.616 0.384
#&gt; SRR1740060     1   0.961      0.743 0.616 0.384
#&gt; SRR1740061     1   0.961      0.743 0.616 0.384
#&gt; SRR1740062     1   0.955      0.746 0.624 0.376
#&gt; SRR1740063     1   0.955      0.746 0.624 0.376
#&gt; SRR1740064     1   0.955      0.746 0.624 0.376
#&gt; SRR1740065     1   0.955      0.746 0.624 0.376
#&gt; SRR1740066     2   0.000      1.000 0.000 1.000
#&gt; SRR1740067     2   0.000      1.000 0.000 1.000
#&gt; SRR1740068     2   0.000      1.000 0.000 1.000
#&gt; SRR1740069     2   0.000      1.000 0.000 1.000
#&gt; SRR1740070     2   0.000      1.000 0.000 1.000
#&gt; SRR1740071     2   0.000      1.000 0.000 1.000
#&gt; SRR1740072     2   0.000      1.000 0.000 1.000
#&gt; SRR1740073     2   0.000      1.000 0.000 1.000
#&gt; SRR1740074     1   0.000      0.697 1.000 0.000
#&gt; SRR1740075     1   0.000      0.697 1.000 0.000
#&gt; SRR1740076     1   0.000      0.697 1.000 0.000
#&gt; SRR1740077     1   0.000      0.697 1.000 0.000
#&gt; SRR1740078     1   0.000      0.697 1.000 0.000
#&gt; SRR1740079     1   0.000      0.697 1.000 0.000
#&gt; SRR1740080     1   0.000      0.697 1.000 0.000
#&gt; SRR1740081     1   0.000      0.697 1.000 0.000
#&gt; SRR1740082     1   0.961      0.743 0.616 0.384
#&gt; SRR1740083     1   0.961      0.743 0.616 0.384
#&gt; SRR1740084     1   0.961      0.743 0.616 0.384
#&gt; SRR1740085     1   0.961      0.743 0.616 0.384
#&gt; SRR1740086     1   0.961      0.743 0.616 0.384
#&gt; SRR1740087     1   0.961      0.743 0.616 0.384
#&gt; SRR1740088     1   0.961      0.743 0.616 0.384
#&gt; SRR1740089     1   0.961      0.743 0.616 0.384
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1 p2    p3
#&gt; SRR1740034     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740035     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740036     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740037     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740038     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740039     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740040     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740041     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740042     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740043     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740044     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740045     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740046     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740048     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740047     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740049     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740050     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740051     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740052     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740054     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740053     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740056     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740055     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740057     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740058     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740059     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740060     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740061     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740062     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740063     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740064     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740065     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740066     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740067     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740068     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740069     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740070     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740071     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740072     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740073     2   0.000      1.000 0.000  1 0.000
#&gt; SRR1740074     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740075     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740076     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740077     3   0.000      1.000 0.000  0 1.000
#&gt; SRR1740078     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740079     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740080     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740081     1   0.362      0.878 0.864  0 0.136
#&gt; SRR1740082     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740083     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740084     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740085     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740086     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740087     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740088     1   0.000      0.963 1.000  0 0.000
#&gt; SRR1740089     1   0.000      0.963 1.000  0 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4
#&gt; SRR1740034     1       0          1  1  0  0  0
#&gt; SRR1740035     1       0          1  1  0  0  0
#&gt; SRR1740036     1       0          1  1  0  0  0
#&gt; SRR1740037     1       0          1  1  0  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0
#&gt; SRR1740048     3       0          1  0  0  1  0
#&gt; SRR1740047     3       0          1  0  0  1  0
#&gt; SRR1740049     3       0          1  0  0  1  0
#&gt; SRR1740050     4       0          1  0  0  0  1
#&gt; SRR1740051     4       0          1  0  0  0  1
#&gt; SRR1740052     4       0          1  0  0  0  1
#&gt; SRR1740054     1       0          1  1  0  0  0
#&gt; SRR1740053     4       0          1  0  0  0  1
#&gt; SRR1740056     1       0          1  1  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0
#&gt; SRR1740058     1       0          1  1  0  0  0
#&gt; SRR1740059     1       0          1  1  0  0  0
#&gt; SRR1740060     1       0          1  1  0  0  0
#&gt; SRR1740061     1       0          1  1  0  0  0
#&gt; SRR1740062     1       0          1  1  0  0  0
#&gt; SRR1740063     1       0          1  1  0  0  0
#&gt; SRR1740064     1       0          1  1  0  0  0
#&gt; SRR1740065     1       0          1  1  0  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0
#&gt; SRR1740075     3       0          1  0  0  1  0
#&gt; SRR1740076     3       0          1  0  0  1  0
#&gt; SRR1740077     3       0          1  0  0  1  0
#&gt; SRR1740078     4       0          1  0  0  0  1
#&gt; SRR1740079     4       0          1  0  0  0  1
#&gt; SRR1740080     4       0          1  0  0  0  1
#&gt; SRR1740081     4       0          1  0  0  0  1
#&gt; SRR1740082     1       0          1  1  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0
#&gt; SRR1740086     1       0          1  1  0  0  0
#&gt; SRR1740087     1       0          1  1  0  0  0
#&gt; SRR1740088     1       0          1  1  0  0  0
#&gt; SRR1740089     1       0          1  1  0  0  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette   p1 p2 p3   p4 p5
#&gt; SRR1740034     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740035     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740036     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740037     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740038     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740039     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740040     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740041     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740042     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740043     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740044     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740045     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740046     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740048     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740047     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740049     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740050     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740051     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740052     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740054     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740053     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740056     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740055     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740057     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740058     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740059     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740060     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740061     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740062     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740063     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740064     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740065     4   0.000      1.000 0.00  0  0 1.00  0
#&gt; SRR1740066     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740067     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740068     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740069     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740070     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740071     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740072     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740073     2   0.000      1.000 0.00  1  0 0.00  0
#&gt; SRR1740074     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740075     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740076     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740077     3   0.000      1.000 0.00  0  1 0.00  0
#&gt; SRR1740078     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740079     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740080     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740081     5   0.000      1.000 0.00  0  0 0.00  1
#&gt; SRR1740082     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740083     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740084     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740085     1   0.000      0.955 1.00  0  0 0.00  0
#&gt; SRR1740086     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740087     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740088     1   0.173      0.954 0.92  0  0 0.08  0
#&gt; SRR1740089     1   0.173      0.954 0.92  0  0 0.08  0
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2 p3 p4 p5 p6
#&gt; SRR1740034     4       0          1  0  0  0  1  0  0
#&gt; SRR1740035     4       0          1  0  0  0  1  0  0
#&gt; SRR1740036     4       0          1  0  0  0  1  0  0
#&gt; SRR1740037     4       0          1  0  0  0  1  0  0
#&gt; SRR1740038     2       0          1  0  1  0  0  0  0
#&gt; SRR1740039     2       0          1  0  1  0  0  0  0
#&gt; SRR1740040     2       0          1  0  1  0  0  0  0
#&gt; SRR1740041     2       0          1  0  1  0  0  0  0
#&gt; SRR1740042     2       0          1  0  1  0  0  0  0
#&gt; SRR1740043     2       0          1  0  1  0  0  0  0
#&gt; SRR1740044     2       0          1  0  1  0  0  0  0
#&gt; SRR1740045     2       0          1  0  1  0  0  0  0
#&gt; SRR1740046     3       0          1  0  0  1  0  0  0
#&gt; SRR1740048     3       0          1  0  0  1  0  0  0
#&gt; SRR1740047     3       0          1  0  0  1  0  0  0
#&gt; SRR1740049     3       0          1  0  0  1  0  0  0
#&gt; SRR1740050     5       0          1  0  0  0  0  1  0
#&gt; SRR1740051     5       0          1  0  0  0  0  1  0
#&gt; SRR1740052     5       0          1  0  0  0  0  1  0
#&gt; SRR1740054     1       0          1  1  0  0  0  0  0
#&gt; SRR1740053     5       0          1  0  0  0  0  1  0
#&gt; SRR1740056     1       0          1  1  0  0  0  0  0
#&gt; SRR1740055     1       0          1  1  0  0  0  0  0
#&gt; SRR1740057     1       0          1  1  0  0  0  0  0
#&gt; SRR1740058     6       0          1  0  0  0  0  0  1
#&gt; SRR1740059     6       0          1  0  0  0  0  0  1
#&gt; SRR1740060     6       0          1  0  0  0  0  0  1
#&gt; SRR1740061     6       0          1  0  0  0  0  0  1
#&gt; SRR1740062     4       0          1  0  0  0  1  0  0
#&gt; SRR1740063     4       0          1  0  0  0  1  0  0
#&gt; SRR1740064     4       0          1  0  0  0  1  0  0
#&gt; SRR1740065     4       0          1  0  0  0  1  0  0
#&gt; SRR1740066     2       0          1  0  1  0  0  0  0
#&gt; SRR1740067     2       0          1  0  1  0  0  0  0
#&gt; SRR1740068     2       0          1  0  1  0  0  0  0
#&gt; SRR1740069     2       0          1  0  1  0  0  0  0
#&gt; SRR1740070     2       0          1  0  1  0  0  0  0
#&gt; SRR1740071     2       0          1  0  1  0  0  0  0
#&gt; SRR1740072     2       0          1  0  1  0  0  0  0
#&gt; SRR1740073     2       0          1  0  1  0  0  0  0
#&gt; SRR1740074     3       0          1  0  0  1  0  0  0
#&gt; SRR1740075     3       0          1  0  0  1  0  0  0
#&gt; SRR1740076     3       0          1  0  0  1  0  0  0
#&gt; SRR1740077     3       0          1  0  0  1  0  0  0
#&gt; SRR1740078     5       0          1  0  0  0  0  1  0
#&gt; SRR1740079     5       0          1  0  0  0  0  1  0
#&gt; SRR1740080     5       0          1  0  0  0  0  1  0
#&gt; SRR1740081     5       0          1  0  0  0  0  1  0
#&gt; SRR1740082     1       0          1  1  0  0  0  0  0
#&gt; SRR1740083     1       0          1  1  0  0  0  0  0
#&gt; SRR1740084     1       0          1  1  0  0  0  0  0
#&gt; SRR1740085     1       0          1  1  0  0  0  0  0
#&gt; SRR1740086     6       0          1  0  0  0  0  0  1
#&gt; SRR1740087     6       0          1  0  0  0  0  0  1
#&gt; SRR1740088     6       0          1  0  0  0  0  0  1
#&gt; SRR1740089     6       0          1  0  0  0  0  0  1
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16000 rows and 56 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.2501 0.751   0.751
#> 3 3 1.000           0.986       0.992         1.3351 0.668   0.557
#> 4 4 0.794           0.885       0.901         0.1982 0.875   0.702
#> 5 5 0.779           0.918       0.834         0.0753 0.917   0.717
#> 6 6 0.824           0.908       0.855         0.0493 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;            class entropy silhouette p1 p2
#&gt; SRR1740034     1       0          1  1  0
#&gt; SRR1740035     1       0          1  1  0
#&gt; SRR1740036     1       0          1  1  0
#&gt; SRR1740037     1       0          1  1  0
#&gt; SRR1740038     1       0          1  1  0
#&gt; SRR1740039     1       0          1  1  0
#&gt; SRR1740040     1       0          1  1  0
#&gt; SRR1740041     1       0          1  1  0
#&gt; SRR1740042     1       0          1  1  0
#&gt; SRR1740043     1       0          1  1  0
#&gt; SRR1740044     1       0          1  1  0
#&gt; SRR1740045     1       0          1  1  0
#&gt; SRR1740046     2       0          1  0  1
#&gt; SRR1740048     2       0          1  0  1
#&gt; SRR1740047     2       0          1  0  1
#&gt; SRR1740049     2       0          1  0  1
#&gt; SRR1740050     1       0          1  1  0
#&gt; SRR1740051     1       0          1  1  0
#&gt; SRR1740052     1       0          1  1  0
#&gt; SRR1740054     1       0          1  1  0
#&gt; SRR1740053     1       0          1  1  0
#&gt; SRR1740056     1       0          1  1  0
#&gt; SRR1740055     1       0          1  1  0
#&gt; SRR1740057     1       0          1  1  0
#&gt; SRR1740058     1       0          1  1  0
#&gt; SRR1740059     1       0          1  1  0
#&gt; SRR1740060     1       0          1  1  0
#&gt; SRR1740061     1       0          1  1  0
#&gt; SRR1740062     1       0          1  1  0
#&gt; SRR1740063     1       0          1  1  0
#&gt; SRR1740064     1       0          1  1  0
#&gt; SRR1740065     1       0          1  1  0
#&gt; SRR1740066     1       0          1  1  0
#&gt; SRR1740067     1       0          1  1  0
#&gt; SRR1740068     1       0          1  1  0
#&gt; SRR1740069     1       0          1  1  0
#&gt; SRR1740070     1       0          1  1  0
#&gt; SRR1740071     1       0          1  1  0
#&gt; SRR1740072     1       0          1  1  0
#&gt; SRR1740073     1       0          1  1  0
#&gt; SRR1740074     2       0          1  0  1
#&gt; SRR1740075     2       0          1  0  1
#&gt; SRR1740076     2       0          1  0  1
#&gt; SRR1740077     2       0          1  0  1
#&gt; SRR1740078     1       0          1  1  0
#&gt; SRR1740079     1       0          1  1  0
#&gt; SRR1740080     1       0          1  1  0
#&gt; SRR1740081     1       0          1  1  0
#&gt; SRR1740082     1       0          1  1  0
#&gt; SRR1740083     1       0          1  1  0
#&gt; SRR1740084     1       0          1  1  0
#&gt; SRR1740085     1       0          1  1  0
#&gt; SRR1740086     1       0          1  1  0
#&gt; SRR1740087     1       0          1  1  0
#&gt; SRR1740088     1       0          1  1  0
#&gt; SRR1740089     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3
#&gt; SRR1740034     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740035     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740036     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740037     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740038     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740039     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740040     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740041     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740042     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740043     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740044     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740045     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740050     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740051     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740052     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740054     1  0.1163      0.969 0.972 0.028  0
#&gt; SRR1740053     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740056     1  0.1031      0.972 0.976 0.024  0
#&gt; SRR1740055     1  0.4605      0.755 0.796 0.204  0
#&gt; SRR1740057     1  0.1031      0.972 0.976 0.024  0
#&gt; SRR1740058     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740059     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740060     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740061     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740062     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740063     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740064     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740065     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740066     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740067     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740068     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740069     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740070     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740071     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740072     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740073     2  0.0237      1.000 0.004 0.996  0
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1
#&gt; SRR1740078     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740079     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740080     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740081     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740082     1  0.1289      0.966 0.968 0.032  0
#&gt; SRR1740083     1  0.1289      0.966 0.968 0.032  0
#&gt; SRR1740084     1  0.1031      0.972 0.976 0.024  0
#&gt; SRR1740085     1  0.1031      0.972 0.976 0.024  0
#&gt; SRR1740086     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740087     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740088     1  0.0000      0.986 1.000 0.000  0
#&gt; SRR1740089     1  0.0000      0.986 1.000 0.000  0
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4
#&gt; SRR1740034     1  0.0336     0.7847 0.992 0.000  0 0.008
#&gt; SRR1740035     1  0.0469     0.7861 0.988 0.000  0 0.012
#&gt; SRR1740036     1  0.0469     0.7824 0.988 0.000  0 0.012
#&gt; SRR1740037     1  0.0336     0.7847 0.992 0.000  0 0.008
#&gt; SRR1740038     2  0.0779     0.9839 0.004 0.980  0 0.016
#&gt; SRR1740039     2  0.0779     0.9839 0.004 0.980  0 0.016
#&gt; SRR1740040     2  0.0895     0.9824 0.004 0.976  0 0.020
#&gt; SRR1740041     2  0.1042     0.9801 0.008 0.972  0 0.020
#&gt; SRR1740042     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740043     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740044     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740045     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740046     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740048     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740047     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740049     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740050     4  0.3428     0.9962 0.144 0.012  0 0.844
#&gt; SRR1740051     4  0.3479     0.9948 0.148 0.012  0 0.840
#&gt; SRR1740052     4  0.3428     0.9962 0.144 0.012  0 0.844
#&gt; SRR1740054     1  0.4961     0.3390 0.552 0.000  0 0.448
#&gt; SRR1740053     4  0.3479     0.9913 0.148 0.012  0 0.840
#&gt; SRR1740056     1  0.4643     0.6211 0.656 0.000  0 0.344
#&gt; SRR1740055     1  0.7771     0.0545 0.420 0.252  0 0.328
#&gt; SRR1740057     1  0.4277     0.7342 0.720 0.000  0 0.280
#&gt; SRR1740058     1  0.3801     0.8048 0.780 0.000  0 0.220
#&gt; SRR1740059     1  0.3610     0.8201 0.800 0.000  0 0.200
#&gt; SRR1740060     1  0.3610     0.8198 0.800 0.000  0 0.200
#&gt; SRR1740061     1  0.3649     0.8177 0.796 0.000  0 0.204
#&gt; SRR1740062     1  0.0592     0.7799 0.984 0.000  0 0.016
#&gt; SRR1740063     1  0.0592     0.7799 0.984 0.000  0 0.016
#&gt; SRR1740064     1  0.0592     0.7799 0.984 0.000  0 0.016
#&gt; SRR1740065     1  0.0592     0.7799 0.984 0.000  0 0.016
#&gt; SRR1740066     2  0.0657     0.9843 0.004 0.984  0 0.012
#&gt; SRR1740067     2  0.0779     0.9839 0.004 0.980  0 0.016
#&gt; SRR1740068     2  0.1042     0.9801 0.008 0.972  0 0.020
#&gt; SRR1740069     2  0.0779     0.9839 0.004 0.980  0 0.016
#&gt; SRR1740070     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740071     2  0.0592     0.9844 0.000 0.984  0 0.016
#&gt; SRR1740072     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740073     2  0.0469     0.9848 0.000 0.988  0 0.012
#&gt; SRR1740074     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740075     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740076     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740077     3  0.0000     1.0000 0.000 0.000  1 0.000
#&gt; SRR1740078     4  0.3479     0.9948 0.148 0.012  0 0.840
#&gt; SRR1740079     4  0.3479     0.9948 0.148 0.012  0 0.840
#&gt; SRR1740080     4  0.3428     0.9962 0.144 0.012  0 0.844
#&gt; SRR1740081     4  0.3428     0.9962 0.144 0.012  0 0.844
#&gt; SRR1740082     1  0.3306     0.8250 0.840 0.004  0 0.156
#&gt; SRR1740083     1  0.3157     0.8240 0.852 0.004  0 0.144
#&gt; SRR1740084     1  0.3266     0.8263 0.832 0.000  0 0.168
#&gt; SRR1740085     1  0.3266     0.8263 0.832 0.000  0 0.168
#&gt; SRR1740086     1  0.3688     0.8175 0.792 0.000  0 0.208
#&gt; SRR1740087     1  0.3569     0.8227 0.804 0.000  0 0.196
#&gt; SRR1740088     1  0.3610     0.8211 0.800 0.000  0 0.200
#&gt; SRR1740089     1  0.3528     0.8213 0.808 0.000  0 0.192
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5
#&gt; SRR1740034     4  0.5184      0.959 0.456 0.004  0 0.508 0.032
#&gt; SRR1740035     4  0.5187      0.953 0.460 0.004  0 0.504 0.032
#&gt; SRR1740036     4  0.5181      0.963 0.452 0.004  0 0.512 0.032
#&gt; SRR1740037     4  0.5181      0.963 0.452 0.004  0 0.512 0.032
#&gt; SRR1740038     2  0.3005      0.923 0.008 0.856  0 0.124 0.012
#&gt; SRR1740039     2  0.2681      0.925 0.004 0.876  0 0.108 0.012
#&gt; SRR1740040     2  0.3543      0.909 0.012 0.828  0 0.136 0.024
#&gt; SRR1740041     2  0.3053      0.921 0.008 0.852  0 0.128 0.012
#&gt; SRR1740042     2  0.1074      0.920 0.016 0.968  0 0.012 0.004
#&gt; SRR1740043     2  0.0798      0.922 0.016 0.976  0 0.008 0.000
#&gt; SRR1740044     2  0.1074      0.920 0.016 0.968  0 0.012 0.004
#&gt; SRR1740045     2  0.0566      0.924 0.012 0.984  0 0.004 0.000
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740050     5  0.2852      0.996 0.172 0.000  0 0.000 0.828
#&gt; SRR1740051     5  0.3048      0.994 0.176 0.000  0 0.004 0.820
#&gt; SRR1740052     5  0.3048      0.994 0.176 0.000  0 0.004 0.820
#&gt; SRR1740054     1  0.4382      0.694 0.760 0.004  0 0.060 0.176
#&gt; SRR1740053     5  0.3086      0.991 0.180 0.000  0 0.004 0.816
#&gt; SRR1740056     1  0.3547      0.791 0.836 0.004  0 0.060 0.100
#&gt; SRR1740055     1  0.6381      0.499 0.640 0.144  0 0.064 0.152
#&gt; SRR1740057     1  0.3504      0.805 0.840 0.004  0 0.064 0.092
#&gt; SRR1740058     1  0.1697      0.859 0.932 0.000  0 0.008 0.060
#&gt; SRR1740059     1  0.1626      0.867 0.940 0.000  0 0.016 0.044
#&gt; SRR1740060     1  0.1579      0.861 0.944 0.000  0 0.024 0.032
#&gt; SRR1740061     1  0.1661      0.862 0.940 0.000  0 0.024 0.036
#&gt; SRR1740062     4  0.5196      0.963 0.428 0.008  0 0.536 0.028
#&gt; SRR1740063     4  0.5002      0.961 0.424 0.004  0 0.548 0.024
#&gt; SRR1740064     4  0.5078      0.963 0.424 0.004  0 0.544 0.028
#&gt; SRR1740065     4  0.5190      0.960 0.424 0.008  0 0.540 0.028
#&gt; SRR1740066     2  0.3005      0.923 0.008 0.856  0 0.124 0.012
#&gt; SRR1740067     2  0.2957      0.923 0.008 0.860  0 0.120 0.012
#&gt; SRR1740068     2  0.2957      0.923 0.008 0.860  0 0.120 0.012
#&gt; SRR1740069     2  0.3059      0.922 0.008 0.856  0 0.120 0.016
#&gt; SRR1740070     2  0.0579      0.924 0.008 0.984  0 0.008 0.000
#&gt; SRR1740071     2  0.0324      0.925 0.004 0.992  0 0.000 0.004
#&gt; SRR1740072     2  0.1299      0.917 0.012 0.960  0 0.020 0.008
#&gt; SRR1740073     2  0.1267      0.917 0.012 0.960  0 0.024 0.004
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.000 0.000
#&gt; SRR1740078     5  0.2852      0.996 0.172 0.000  0 0.000 0.828
#&gt; SRR1740079     5  0.2891      0.995 0.176 0.000  0 0.000 0.824
#&gt; SRR1740080     5  0.2852      0.996 0.172 0.000  0 0.000 0.828
#&gt; SRR1740081     5  0.2852      0.996 0.172 0.000  0 0.000 0.828
#&gt; SRR1740082     1  0.1891      0.827 0.936 0.016  0 0.032 0.016
#&gt; SRR1740083     1  0.1869      0.814 0.936 0.012  0 0.036 0.016
#&gt; SRR1740084     1  0.1186      0.840 0.964 0.008  0 0.020 0.008
#&gt; SRR1740085     1  0.1673      0.847 0.944 0.008  0 0.032 0.016
#&gt; SRR1740086     1  0.1041      0.867 0.964 0.000  0 0.004 0.032
#&gt; SRR1740087     1  0.1485      0.856 0.948 0.000  0 0.032 0.020
#&gt; SRR1740088     1  0.1041      0.865 0.964 0.000  0 0.004 0.032
#&gt; SRR1740089     1  0.1168      0.867 0.960 0.000  0 0.008 0.032
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;            class entropy silhouette    p1    p2 p3    p4    p5 p6
#&gt; SRR1740034     4  0.3810      0.957 0.176 0.008  0 0.780 0.016 NA
#&gt; SRR1740035     4  0.3610      0.952 0.176 0.004  0 0.788 0.012 NA
#&gt; SRR1740036     4  0.3325      0.973 0.152 0.008  0 0.816 0.016 NA
#&gt; SRR1740037     4  0.3532      0.971 0.164 0.012  0 0.800 0.016 NA
#&gt; SRR1740038     2  0.0881      0.843 0.012 0.972  0 0.000 0.008 NA
#&gt; SRR1740039     2  0.0551      0.847 0.004 0.984  0 0.004 0.008 NA
#&gt; SRR1740040     2  0.1604      0.830 0.016 0.944  0 0.008 0.008 NA
#&gt; SRR1740041     2  0.0798      0.844 0.012 0.976  0 0.004 0.004 NA
#&gt; SRR1740042     2  0.3897      0.847 0.016 0.712  0 0.000 0.008 NA
#&gt; SRR1740043     2  0.3897      0.847 0.016 0.712  0 0.000 0.008 NA
#&gt; SRR1740044     2  0.4013      0.847 0.016 0.712  0 0.004 0.008 NA
#&gt; SRR1740045     2  0.3795      0.849 0.012 0.724  0 0.004 0.004 NA
#&gt; SRR1740046     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740048     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740047     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740049     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740050     5  0.2145      0.990 0.076 0.004  0 0.012 0.904 NA
#&gt; SRR1740051     5  0.1843      0.988 0.080 0.004  0 0.004 0.912 NA
#&gt; SRR1740052     5  0.2009      0.984 0.084 0.004  0 0.000 0.904 NA
#&gt; SRR1740054     1  0.4048      0.798 0.788 0.004  0 0.016 0.104 NA
#&gt; SRR1740053     5  0.2062      0.980 0.088 0.004  0 0.000 0.900 NA
#&gt; SRR1740056     1  0.2978      0.863 0.868 0.004  0 0.016 0.060 NA
#&gt; SRR1740055     1  0.6740      0.466 0.536 0.140  0 0.012 0.084 NA
#&gt; SRR1740057     1  0.3383      0.862 0.840 0.000  0 0.032 0.052 NA
#&gt; SRR1740058     1  0.1059      0.904 0.964 0.000  0 0.016 0.016 NA
#&gt; SRR1740059     1  0.0622      0.904 0.980 0.000  0 0.012 0.008 NA
#&gt; SRR1740060     1  0.0820      0.902 0.972 0.000  0 0.016 0.012 NA
#&gt; SRR1740061     1  0.1059      0.901 0.964 0.000  0 0.016 0.016 NA
#&gt; SRR1740062     4  0.3232      0.971 0.140 0.020  0 0.824 0.016 NA
#&gt; SRR1740063     4  0.3275      0.974 0.148 0.012  0 0.820 0.016 NA
#&gt; SRR1740064     4  0.3327      0.973 0.144 0.016  0 0.820 0.016 NA
#&gt; SRR1740065     4  0.3192      0.968 0.136 0.020  0 0.828 0.016 NA
#&gt; SRR1740066     2  0.0810      0.845 0.008 0.976  0 0.004 0.008 NA
#&gt; SRR1740067     2  0.0924      0.843 0.008 0.972  0 0.008 0.004 NA
#&gt; SRR1740068     2  0.0748      0.843 0.016 0.976  0 0.004 0.000 NA
#&gt; SRR1740069     2  0.1026      0.841 0.012 0.968  0 0.008 0.004 NA
#&gt; SRR1740070     2  0.3875      0.848 0.016 0.716  0 0.000 0.008 NA
#&gt; SRR1740071     2  0.3875      0.848 0.016 0.716  0 0.000 0.008 NA
#&gt; SRR1740072     2  0.4119      0.838 0.016 0.692  0 0.004 0.008 NA
#&gt; SRR1740073     2  0.4205      0.838 0.016 0.692  0 0.008 0.008 NA
#&gt; SRR1740074     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740075     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740076     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740077     3  0.0000      1.000 0.000 0.000  1 0.000 0.000 NA
#&gt; SRR1740078     5  0.2089      0.988 0.072 0.004  0 0.012 0.908 NA
#&gt; SRR1740079     5  0.2257      0.990 0.076 0.004  0 0.012 0.900 NA
#&gt; SRR1740080     5  0.2157      0.989 0.076 0.004  0 0.008 0.904 NA
#&gt; SRR1740081     5  0.2145      0.990 0.076 0.004  0 0.012 0.904 NA
#&gt; SRR1740082     1  0.2123      0.886 0.908 0.008  0 0.020 0.000 NA
#&gt; SRR1740083     1  0.2307      0.881 0.900 0.012  0 0.024 0.000 NA
#&gt; SRR1740084     1  0.2728      0.878 0.876 0.004  0 0.024 0.012 NA
#&gt; SRR1740085     1  0.2908      0.873 0.864 0.004  0 0.028 0.012 NA
#&gt; SRR1740086     1  0.0551      0.905 0.984 0.000  0 0.008 0.004 NA
#&gt; SRR1740087     1  0.1007      0.901 0.968 0.004  0 0.016 0.004 NA
#&gt; SRR1740088     1  0.0551      0.906 0.984 0.000  0 0.004 0.008 NA
#&gt; SRR1740089     1  0.0881      0.906 0.972 0.000  0 0.008 0.008 NA
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


