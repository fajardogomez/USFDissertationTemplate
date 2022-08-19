# USFDissertationTemplate
An unofficial template to mostly meet USF's ETD guidelines

The project can be copied (and viewed) from [Overleaf](https://www.overleaf.com/read/qmrvgskkzrmr). Though a lot of time and effort went into making this document meet ETD guidelines in Summer 2022 it is bound to 
* have missed some formatting requirements
* become outdated when requirements change
* produce docuemnts that meet the requirements but still get flagged by ETD reviewers (looking at you, "half empty" spaces that are _less_ than 5.5" long)
It falls on the user to do several checks before submitting. A checklist is provided, though it may not be exhaustive. 

This template was written to be used "right out of the box," with sample files that can be readily modified and code snippets that can be adapted as necessary. Many useful packages have already been loaded, both in the `.cls` file (mostly formatting that may break if messed around with too much) and in the preamble file. Be wary of the order in which you add packages to the preamble. For example, `cleveref` can produce errors when it is not the last package to be loaded. Generally, for the less $\LaTeX$ savvy it may be best to add new macros and packages in the neighborhood of other things in the template that are serving a similar purpose.

Should you run into a problem not easily answered by web searches or the kind people of [stackexchange](https://tex.stackexchange.com/) just submit an issue and I'll see what I can do about it. 
