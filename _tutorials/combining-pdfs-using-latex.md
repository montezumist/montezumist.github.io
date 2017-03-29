---
title: "Combining several PDF files into one using LaTeX"
tags: [LaTeX, template]
excerpt: "A small template to combine several PDF files into one"
---

I often need to put a few PDF files into one and do not always have the most available tools for the job:
* I don't have a license for Adobe Reader Professional
* I do not run a variant of Linux that has a nice tool like `pdfunite` or `convert`.

However, I am able to get the merged PDF file using LaTeX as shown below:

{% highlight tex linenos %}
\documentclass[11pt]{article} 

\usepackage{geometry} 
\geometry{a4paper} 

\usepackage{grffile,pdfpages}

\begin{document}
\includepdf[pages={1,2,3,5,7,9,11}]{folder/fileA.pdf}
\includepdf[angle=180]{folder 2/file B.pdf}

\end{document}
{% endhighlight %}

- Line 1 to 4: define the overall size of the document
- Line 6: the package `grffile` allows you to have spaces in the names of the PDF files you're going to use; the package `pdfpages` is what we use to include PDFs in our document
- Line 9: select the given pages of the document `folder/fileA.pdf`
- Line 10: insert all of `folder 2/file B.pdf` after flipping the pages 180 degrees (if it's upside down)

And you're done!
