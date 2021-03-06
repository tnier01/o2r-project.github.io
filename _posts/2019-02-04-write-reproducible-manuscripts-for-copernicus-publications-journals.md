---
layout: post
title: How to increase reproducibility and transparency in your research
categories:
  - "open science"
  - "reproducible research"
  - "Copernicus"
  - "Copernicus Publications"
  - "EGU"
  - "preproducibility"
  - "suppdata"
  - "rticles"
author: 'Daniel Nüst'
---

_[This article is cross posted-on the [EGU GeoLog](https://blogs.egu.eu/geolog/2019/02/01/reproducibility-and-transparency-in-research/).]_

Contemporary science faces many challenges in publishing results that are reproducible.
This is due to increased usage of data and digital technologies as well as heightened demands for scholarly communication.
These challenges have led to widespread [calls](#munafo) for more research transparency, accessibility, and reproducibility from the science community.
This article presents current findings and solutions to these problems, including recent new software that makes writing submission-ready manuscripts for journals of _[Copernicus Publications](https://www.copernicus.org/)_ a lot easier.
<!--more-->
While it can be debated if science really faces a [reproducibility](#baker) [crisis](#fanelli), the challenges of computer-based research have sparked numerous articles on new [good](#wilson) [research](#gil) [practices](#sandve) and their [evaluation](#hardwicke).
The challenges have also driven researchers to develop infrastructure and tools to help scientists effectively write articles, publish data, share code for computations, and communicate their findings in a reproducible way, for example [Jupyter](#jupyter), [ReproZip](#reprozip) and [research compendia](https://research-compendium.science/).

[Recent](#konkol) [studies](#nuest) [showed](#ostermann) that the geosciences and geographic information science are not beyond issues with reproducibility, just like other domains.
Therefore, more and more [journals](https://www.nature.com/authors/policies/availability.html) have [adopted policies](#stodden) on sharing data and code.
However, it is equally important that scientists foster an [open research culture](#nosek) and teach researchers how they adopt more transparent and reproducible workflows, for example at skill-building workshops at conferences offered by fellow researchers, such as the EGU short courses, community-led non-profit organisations such as the [Carpentries](https://carpentries.org/), [open courses for students](#toelch), small discussion groups at research labs, or individual efforts of self-learning.
In the light of prevailing [issues of a common definition](#barba) of reproducibility, [Philip Stark](#stark), a statistics professor and associate dean of mathematical and physical sciences at the University of California, Berkeley, recently coined the term [_preproducibility_](#stark): _"An experiment or analysis is preproducible if it has been described in adequate detail for others to undertake it."_
The neologism intends to reduce confusion and also to embrace a positive attitude for more openness, honesty, and helpfulness in scholarly communication processes.

<!-- image here! -->
[![](/public/images/2018-11_showme-nottrustme-nature.png)](https://twitter.com/NatureNews/status/999715421208104960)

In the spirit of these activities, this article describes a modern workflow made possible by recent software releases.
The new features allow the EGU community to write preproducible manuscripts for submission to the large variety of academic journals published by [_Copernicus Publications_](https://www.copernicus.org/).
The new workflow might require hard-earned adjustments for some researchers, but it pays off because of an increase in transparency and effectivity.
This is especially the case for early career scientists.
An open and reproducible workflow enables researchers to build on others' and own previous work and better collaborate on solving the societal challenges of today.

## Reproducible research manuscripts

[Open](https://en.wikipedia.org/wiki/Open-notebook_science) digital [notebooks](https://arxiv.org/abs/1804.05492), which [interweave data and code](https://en.wikipedia.org/wiki/Literate_programming) and can be exported to different output formats such as PDF, are powerful means to improve transparency and preproducibility of research.
[Jupyter Notebook](https://jupyter.org/), [Stencila](http://stenci.la/) and [R Markdown](https://rmarkdown.rstudio.com/) let researchers combine long-form text of a publication and source code for analysis and visualisation in a single document.
Having text and code side-by-side makes them easier to grasp and ensures consistency, because each rendering of the document executes the whole workflow using the original data.
Caching for long-lasting computations is possible, and researchers working with supercomputing infrastructures or huge datasets may limit the executed code to purposes of visualisation using processed data as input.
Authors can transparently expose specific code snippets to readers but also publish the complete source code of the document openly for collaboration and review.

The popular notebook formats are plain text-based, like [Markdown](https://en.wikipedia.org/wiki/Markdown) in case of R Markdown.
Therefore an R Markdown document can be managed with [version control software](https://en.wikipedia.org/wiki/Version_control), which are programs for managing multiple versions and contributions, even by different people, to the same documents.
Version control provides traceability of authorship, a time machine for going back to any previous "working" version, and online collaboration such as on [GitLab](https://en.wikipedia.org/wiki/GitLab).
This kind of workflow also stops [the madness of using file names for versions](http://phdcomics.com/comics/archive_print.php?comicid=1531) yet still lets authors use [awesome file names](https://speakerdeck.com/jennybc/how-to-name-files) and apply domain-specific [guidelines for packaging research](#marwick).

<blockquote class="twitter-tweet" data-lang="de"><p lang="en" dir="ltr">Final.doc <a href="https://t.co/YXJaSacHWu">https://t.co/YXJaSacHWu</a> <a href="https://t.co/4bBDzn7TXt">pic.twitter.com/4bBDzn7TXt</a></p>&mdash; PHD Comics (@PHDcomics) <a href="https://twitter.com/PHDcomics/status/826861642507882496?ref_src=twsrc%5Etfw">1. Februar 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

R Markdown supports [different programming languages](https://rmarkdown.rstudio.com/lesson-5.html) besides the popular namesake [R](https://www.r-project.org/) and is a sensible solution even if you do not analyse data with scripts nor have any code in your scholarly manuscript.
It is easy to write, allows you to [manage your bibliography](https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html) effectively, can be used for websites, [books](https://bookdown.org/) or [blogs](https://bookdown.org/yihui/blogdown/), but most importantly _it does not fall short when it is time to submit a manuscript article to a journal_.

The [`rticles`](https://cran.r-project.org/package=rticles) extension package for R provides a number of templates for popular journals and publishers.
Since version `0.6` ([published Oct 9 2018](https://github.com/rstudio/rticles/releases/tag/v0.6)) these [templates include](https://github.com/rstudio/rticles/pull/172) the [Copernicus Publications Manuscript preparations guidelines for authors](https://publications.copernicus.org/for_authors/manuscript_preparation.html).
The Copernicus Publications staff was kind enough to give a test document a quick review and all seems in order, though of course any problems and questions shall be directed to the software's vibrant community and not the publishers.

The following code snippet and screen shot demonstrate the workflow.
Lines starting with `#` are code comments and explain the steps.
Code examples provided here are ready to use and only lack the installation commands for required packages.

~~~
# load required R extension packages:
library("rticles")
library("rmarkdown")

# create a new document using a template:
rmarkdown::draft(file = "MyArticle.Rmd",
                 template = "copernicus_article",
                 package = "rticles", edit = FALSE)

# render the source of the document to the default output format:
rmarkdown::render(input = "MyArticle/MyArticle.Rmd")
~~~
{: .language-r}

![](/public/images/2018-10_rmd-pdf-example.png)

The commands created a directory with the Copernicus Publications template's files, including an R Markdown (`.Rmd`) file ready to be edited by you (left-hand side of the screenshot), a [LaTeX](https://en.wikipedia.org/wiki/LaTeX) (`.tex`) file for submission to the publisher, and a `.pdf` file for inspecting the final results and sharing with your colleagues (right-hand side of the screenshot).
You can see how simple it is to format text, insert citations, chemical formulas or equations, and add figures, and how they are rendered into a high-quality output file.

All of these steps may also be completed with user-friendly forms when using [RStudio](https://en.wikipedia.org/wiki/RStudio), a popular development and authoring environment available for all operating systems.
The left-hand side of the following screenshot shows the form for creating a new document based on a template, and the right-hand shows side the menu for rendering, called "knitting" with R Markdown because code and text are combined into one document like threads in a garment.

![](/public/images/2018-10_rstudio-ui-example.png)

And in case you decide last minute to submit to a different journal, [`rticles` supports many publishers](https://github.com/rstudio/rticles#overview) so you only have to adjust the template while the whole content stays the same.

## Sustainable access to supplemental data

Data published today [should](http://www.copdess.org/enabling-fair-data-project/commitment-to-enabling-fair-data-in-the-earth-space-and-environmental-sciences/) be published and properly cited using appropriate [research data repositories](https://www.re3data.org/) following the [FAIR data](https://en.wikipedia.org/wiki/FAIR_data) [principles](https://www.force11.org/group/fairgroup/fairprinciples).
Journals require authors to follow these principles, see for example the [Copernicus Publications data policy](https://publications.copernicus.org/services/data_policy.html) or a recent [announcement by _Nature_](#nature).
Other publishers required, or still do today, to store supplemental information (SI), such as dataset files, extra figures, or extensive descriptions of experimental procedures, as part of the article.
Usually only the article itself receives a digital object identifier ([DOI](https://en.wikipedia.org/wiki/Digital_object_identifier)) for long-term identification and availability.
The DOI [minted](https://www.helmholtz-berlin.de/zentrum/locations/bibliothek/dokumentationhaupt/veroeffentlichungsverzeichnis-kopie/doi-vergabe_en.html) by the publisher is not suitable for direct access to supplemental files, because it points to a [landing](https://support.crossref.org/hc/en-us/articles/214669863-Your-landing-page) [page](https://support.datacite.org/docs/datacite-doi-display-guidelines#section-applying-the-guidelines) about the identified object.
This landing page is designed to be read by humans but not by computers.

The R package [`suppdata`](https://github.com/ropensci/suppdata) [closes this gap](#pearse).
It supports downloading supplemental information using the article's DOI.
This way `suppdata` enables long-term reproducible data access when data was published as SI in the past or in exceptional cases today, for example if you write about a reproduction of a published article.
In the latest version available [from GitHub](https://github.com/ropensci/suppdata/blob/master/README.md) (suppdata is [on its way](https://github.com/ropensci/suppdata/issues/31) to [CRAN](https://cran.r-project.org/package=suppdata)) the [supported publishers](https://github.com/ropensci/suppdata#supported-publishers-and-repositories) include Copernicus Publications.
The following example code downloads a data file for the article ["Divergence of seafloor elevation and sea level rise in coral reef ecosystems"](https://doi.org/10.5194/bg-14-1739-2017) by Yates et al. published in _Biogeosciences_ in 2017.
The code then creates a mostly meaningless plot shown below.

~~~
# load required R extension package:
library("suppdata")

# download a specific supplemental information (SI) file
# for an article using the article's DOI:
csv_file <- suppdata::suppdata(
  x = "10.5194/bg-14-1739-2017",
  si = "Table S1 v2 UFK FOR_PUBLICATION.csv")
supplemental

# read the data and plot it (toy example!):
my_data <- read.csv(file = csv_file, skip = 3)
plot(x = my_data$NAVD88_G03, y = my_data$RASTERVALU,
     xlab = "Historical elevation (NAVD88 GEOID03))",
     ylab = "LiDAR elevation (NAVD88 GEOID03)",
     main = "A data plot for article 10.5194/bg-14-1739-2017",
     pch = 20, cex = 0.5)
~~~
{: .language-r}

<!--
png(file = "public/images/2018-10_suppdata-example-plot.png", width = 512, height = 512, bg = "white")
plot(x = my_data$NAVD88_G03, y = my_data$RASTERVALU,
  xlab = "Historical elevation (NAVD88 GEOID03))",
  ylab = "LiDAR elevation (NAVD88 GEOID03)",
  main = "A silly plot for article 10.5194/bg-14-1739-2017",
  pch = 20, cex = 0.5)
dev.off()
-->

![](/public/images/2018-10_suppdata-example-plot.png)

## Main takeaways

Authoring submission-ready manuscripts for journals of Copernicus Publications just got a lot easier.
Everybody who can write manuscripts with a word processor can learn quickly R Markdown and benefit from a preproducible data science workflow.
Digital notebooks not only improve day-to-day research habits, but the same workflow is suitable for authoring high-quality scholarly manuscripts and graphics.
The interaction with the publisher is smooth thanks to the LaTeX submission format, but you never have to write any LaTeX.
The workflow is based on an established [Free and Open Source](https://en.wikipedia.org/wiki/Free_and_Open-Source_Software) software stack and embraces the idea of preproducibility and the principles of [Open Science](https://en.wikipedia.org/wiki/Open_science).
The software is maintained by an [active](https://stackoverflow.com/questions/tagged/r), [growing](https://stackoverflow.blog/2017/10/10/impressive-growth-r/), and welcoming community of researchers and developers with a [strong connection](https://www.r-spatial.org/) to [the](https://gis.stackexchange.com/questions/tagged/r) [geospatial](https://geocompr.github.io/) [sciences](https://asdar-book.org/).
Because of the complete and consistent notebook, [you](#markowetz), a colleague, or a student can easily pick up the work at a later time.
The road to effective and transparent research begins with a first step - [take it](https://vickysteeves.gitlab.io/repro-papers/)!

## Acknowledgements

The software updates were contributed by [Daniel Nüst](https://orcid.org/0000-0002-0024-5046) from the project [Opening Reproducible Research](https://o2r.info) (o2r) at the Institute for Geoinformatics, University of Münster, Germany, but would not be able without the support of Copernicus Publications, the software maintainers most notably [Yihui Xie](https://yihui.name/) and [Will Pearse](http://www.pearselab.com/), and the general awesomeness of the R, R-spatial, Open Science, and Reproducible Research communities.
The blog text was greatly improved with feedback by EGU's [Olivia](http://oliviatrani.org/) [Trani](https://twitter.com/oliviatrani) and Copernicus Publications' [Xenia](https://twitter.com/XeniavanEdig) [van Edig](https://www.copernicus.org/contact_us.html).
Thank you!

## References

<!-- https://crosscite.org/ has a style "copernicus-publications" -->

- <a name="nature"></a>[Announcement: FAIR data in Earth science](https://doi.org/10.1038/d41586-019-00075-3), Nature, 565(7738), 134–134, doi:10.1038/d41586-019-00075-3, 2019.
- <a name="baker"></a>Baker, M.: [1,500 Scientists Lift the Lid on Reproducibility](https://doi.org/10.1038/533452a), Nature, 533(7604), 452–454, doi:10.1038/533452a, 2016.
- <a name="barba"></a>Barba, L.&nbsp;A.: [Terminologies for Reproducible Research](http://arxiv.org/abs/1802.03311), ArXiv:1802.03311 [Cs], February 9, 2018.
- <a name="fanelli"></a>Fanelli, D.: [Opinion: Is Science Really Facing a Reproducibility Crisis, and Do We Need It To?](https://doi.org/10.1073/pnas.1708272114), Proceedings of the National Academy of Sciences, 115(11), 2628–2631, doi:10.1073/pnas.1708272114, 2018.
- <a name="gil"></a>Gil, Y., David, C.&nbsp;H., Demir, I., Essawy, B.&nbsp;T., Fulweiler, R.&nbsp;W., Goodall, J.&nbsp;L., Karlstrom, L., Lee, H., Mills, H.&nbsp;J., Oh, J.-H., Pierce, S.&nbsp;A., Pope, A., Tzeng, M.&nbsp;W., Villamizar, S.&nbsp;R.&nbsp;and Yu, X.: [Towards the Geoscience Paper of the Future: Best Practices for Documenting and Sharing Research from Data to Software to Provenance](https://doi.org/10.1002/2015EA000136), Earth and Space Science, 3(10), 388–415, doi:10.1002/2015ea000136, 2016.
- <a name="hardwicke"></a>Hardwicke, T.&nbsp;E., Mathur, M.&nbsp;B., MacDonald, K., Nilsonne, G., Banks, G.&nbsp;C., Kidwell, M.&nbsp;C., Hofelich Mohr, A., Clayton, E., Yoon, E.&nbsp;J., Henry Tessler, M., Lenne, R.&nbsp;L., Altman, S., Long, B. and Frank, M.&nbsp;C.: [Data availability, reusability, and analytic reproducibility: evaluating the impact of a mandatory open data policy at the journal Cognition](https://doi.org/10.1098/rsos.180448), Royal Society Open Science, 5(8), 180448, doi:10.1098/rsos.180448, 2018.
- <a name="konkol-cgis"></a>Konkol, M. and Kray, C.: [In-depth examination of spatiotemporal figures in open reproducible research](https://doi.org/10.1080/15230406.2018.1512421), Cartography and Geographic Information Science, 1–16, doi:10.1080/15230406.2018.1512421, 2018.
- <a name="konkol-ijgis"></a>Konkol, M., Kray, C. and Pfeiffer, M.: [Computational reproducibility in geoscientific papers: Insights from a series of studies with geoscientists and a reproduction study](https://doi.org/10.1080/13658816.2018.1508687), International Journal of Geographical Information Science, 1–22, doi:10.1080/13658816.2018.1508687, 2018.
- <a name="markowetz"></a>Markowetz, F.: [Five selfish reasons to work reproducibly](https://doi.org/10.1186/s13059-015-0850-7), Genome Biology, 16(1), doi:10.1186/s13059-015-0850-7, 2015.
- <a name="marwick"></a>Marwick, B., Boettiger, C. and Mullen, L.: [Packaging Data Analytical Work Reproducibly Using R (and Friends)](https://doi.org/10.1080/00031305.2017.1375986), The American Statistician, 72(1), 80–88, doi:10.1080/00031305.2017.1375986, 2017.
- <a name="munafo"></a>Munafò, M.&nbsp;R., Nosek, B.&nbsp;A., Bishop, D.&nbsp;V.&nbsp;M., Button, K.&nbsp;S., Chambers, C.&nbsp;D., Percie du Sert, N., Simonsohn, U., Wagenmakers, E.-J., Ware, J.&nbsp;J. and Ioannidis, J.&nbsp;P.&nbsp;A.: [A manifesto for reproducible science, Nature Human Behaviour](https://doi.org/10.1038/s41562-016-0021), 1(1), 21, doi:10.1038/s41562-016-0021, 2017.
- <a name="nuest"></a>Nüst, D., Granell, C., Hofer, B., Konkol, M., Ostermann, F.&nbsp;O., Sileryte, R. and Cerutti, V.: [Reproducible research and GIScience: an evaluation using AGILE conference papers](https://doi.org/10.7717/peerj.5072), PeerJ, 6, e5072, doi:10.7717/peerj.5072, 2018.
- <a name="ostermann"></a>Ostermann, F.&nbsp;O. and Granell, C.: [Advancing Science with VGI: Reproducibility and Replicability of Recent Studies using VGI](https://doi.org/10.1111/tgis.12195), Transactions in GIS, 21(2), 224–237, doi:10.1111/tgis.12195, 2016.
- <a name="pearse"></a>Pearse, W.&nbsp;D. and A Chamberlain, S.: [Suppdata: Downloading Supplementary Data from Published Manuscripts](https://doi.org/10.21105/joss.00721), Journal of Open Source Software, 3(25), 721, doi:10.21105/joss.00721, 2018.
- <a name="repozip"></a>[ReproZip: Computational Reproducibility With Ease](https://osf.io/vc72z/), F. Chirigati, R. Rampin, D. Shasha, and J. Freire. In Proceedings of the 2016 ACM SIGMOD International Conference on Management of Data (SIGMOD), pp. 2085-2088, 2016
- <a name="sandve"></a>Sandve, G.&nbsp;K., Nekrutenko, A., Taylor, J. and Hovig, E.: [Ten Simple Rules for Reproducible Computational Research](https://doi.org/10.1371/journal.pcbi.1003285), edited by P.&nbsp;E. Bourne, PLoS Computational Biology, 9(10), e1003285, doi:10.1371/journal.pcbi.1003285, 2013.
- <a name="stark"></a>Stark, P.&nbsp;B.: [Before reproducibility must come preproducibility](https://doi.org/10.1038/d41586-018-05256-0), Nature, 557(7707), 613–613, doi:10.1038/d41586-018-05256-0, 2018.
- <a name="toelch"></a>Toelch, U. and Ostwald, D.: [Digital open science—Teaching digital tools for reproducible and transparent research](https://doi.org/10.1371/journal.pbio.2006022), PLOS Biology, 16(7), e2006022, doi:10.1371/journal.pbio.2006022, 2018.
- <a name="jupyter"></a>Jupyter, P., Bussonnier, M., Forde, J., Freeman, J., Granger, B., Head, T., Holdgraf, C., Kelley, K., Nalvarte, G., Osheroff, A., Pacer, M., Panda, Y., Perez, F., Ragan-Kelley, B. and Willing, C.: [Binder 2.0 - Reproducible, interactive, sharable environments for science at scale](http://conference.scipy.org/proceedings/scipy2018/pdfs/project_jupyter.pdf), in Proceedings of the 17th Python in Science Conference, SciPy., 2018.
- <a name="wilson"></a>Wilson, G., Bryan, J., Cranston, K., Kitzes, J., Nederbragt, L. and Teal, T.&nbsp;K.: [Good enough practices in scientific computing](https://doi.org/10.1371/journal.pcbi.1005510), PLOS Computational Biology, 13(6), e1005510, doi:10.1371/journal.pcbi.1005510, 2017.
- <a name="yates"></a>Yates, K.&nbsp;K., Zawada, D.&nbsp;G., Smiley, N.&nbsp;A. and Tiling-Range, G.: [Divergence of seafloor elevation and sea level rise in coral reef ecosystems](https://doi.org/10.5194/bg-14-1739-201), Biogeosciences, 14(6), 1739–1772, doi:10.5194/bg-14-1739-2017, 2017.
