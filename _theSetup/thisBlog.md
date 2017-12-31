---
layout: default
title: The Blog
hook: How to setup this Site.
published: true
---


## High level

* Read the [Jekyll docs](https://jekyllrb.com/).
* Examined / cribbed https://routley.io/ since it simple.
* How to get [a Jekyll Collection working](https://www.sitepoint.com/getting-started-jekyll-collections/)

Two be fair it took me two full "sitting" to get this working.

## Jekyll In a Nutshell

* A Ruby based tool that combines the following
   * Code "stuff"
	   * A templating language
       * Directory scanning logic
       * Markdown -> Html logic
       * Yaml parser used to control and feed data into the templating language
   * Convention "stuff"
	   * a top level config file of "_config.yml".
       * a directory structure of where to find posts, includes etc
       * a "header" section of each of your files/posts to define "variables" that the templating engine can reference.
       
In Practice this means Jekyll
* scans the directories and loads all the "documents" into memory
	* or at this point just the "metadata" of the files: filename and the yaml headers 
* once it has a "holistic" view of all the data, it can do the Markdown to Html rendering
	* the "top level" pages tend to to have the "templating logic" in them
	* a standard blog post typically doesn't have any "templage" language in it
* thus the actuall building of "the page" that lists all the blog items is template logic that loops over all the "posts" found off the filesystem


	{% for post in site.posts %}
	   [{{ post.title }}]({{ post.url }}) 
    {% endfor %}

* the "prettiness" of the HTML is generally by controlling the CSS in the "_includes" directory.

## Github




