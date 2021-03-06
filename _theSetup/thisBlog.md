---
layout: default
title: This Blog
hook: How to setup this Site.
published: true
---
{::comment} This is the special Kramdown way of having an HTML comment. {:/comment}

{::comment} The actual header for "Table of Contents" should be excluded from the actual calculation of the Table-of-Content, so hit it with the "no_toc" {:/comment}
## Table of Contents
{:.no_toc} 

{::comment}
	Should the TOC be bullets or numbered items?  

	You tell the TOC "macro" that by binding/affixing it to either an unordered list "*" or an ordered list "1." 

	It will then replace the list entry with the auto-generated html table of contents.
{:/comment}

1. Sacrificial uordered list for the toc "macro" to bind to
{:toc}

---

## High level

* Inpiration but dated, and I did not want to just start with a fork : [smashingmagazine article](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)
    * got lost running Ruby and whatnot locally (sitting number 1)
* Read the [Jekyll docs](https://jekyllrb.com/).
* Examined / cribbed [routley.io/](https://routley.io/) since he had a nice and simple site that looks like it was using GitHub to run Jekyll.
* How to get [a Jekyll Collection working](https://www.sitepoint.com/getting-started-jekyll-collections/)

Two be fair it took me two and a half full "sittings" to get this working.   I first tried to get Jekyll working locally, and got lost.  My second attempt was to do it all on Github.

## Jekyll In a Nutshell

Jekyll is a Ruby based tool that combines the following :
* Code "stuff"
	* A templating language called [Liquid](https://jekyllrb.com/docs/templates/)
    * Directory scanning logic
    * Markdown -> Html logic
    * Yaml parser used to control and feed data into the templating language
* Convention "stuff"
	* a top level config file of "_config.yml".
    * a directory structure of where to find posts, includes etc
    * a "header" section of each of your files/posts to define "variables" that the templating engine can reference.
       
In Practice this means Jekyll :
* scans the directories and loads all the "documents" into memory
	* or at this point just the "metadata" of the files: filename and the yaml headers 
* once it has a "holistic" view of all the data, it can do the Markdown to Html rendering
	* the "top level" pages tend to to have the "templating logic" in them
	* a standard blog post typically doesn't have any "templage" language in it
* thus the actual building of "the page" that lists all the blog items is template logic that loops over all the "posts" found off the filesystem

```html
Example page that builds the list of all the blog entries.

{% raw %}Blog Entries
<ul>
  {% for post in site.posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>{% endraw %}
```
* the "prettiness" of the HTML is generally by controlling the CSS in the "_includes" directory.

## What Jekyll Doesn't Do

Any of the html prettiness.   Dealing with CSS or Bootstrap. etc   
That is where Jekyll themes come in.

So ...
1. get it so that you can author the content, then 
2. make it pretty.

## Editing

Github is awesome.  It can run Jekyll automatically for you to generate the pages.
* [https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)
* things you can and can not change [https://help.github.com/articles/configuring-jekyll/](https://help.github.com/articles/configuring-jekyll/)

Editing : Well I can edit with Intellij and do the whole edit/commit/push cycle OR I can just edit markdown in a nice tool : [prose.io](http://prose.io/#about).

## Authoring

- Table of Contents : 
	- Did not work :( - [http://www.seanbuscay.com/blog/jekyll-toc-markdown/](http://www.seanbuscay.com/blog/jekyll-toc-markdown/)
    - Did work but annoying - [https://ecotrust-canada.github.io/markdown-toc/](https://ecotrust-canada.github.io/markdown-toc/)
- KramDown Docs :  [https://kramdown.gettalong.org/quickref.html](https://kramdown.gettalong.org/quickref.html)
- How to escape liquid template tags?
	- So that I can put example stuff in a code block
    - [https://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags](https://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags)
