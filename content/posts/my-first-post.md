+++ 
draft = false
date = 2022-04-10T17:56:18+02:00
title = "Workshop: Deploy yourself to the cloud"
description = ""
slug = "workshop"
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

# Introduction

Cloud solutions are much like cooking: you need the right ingredients and the expertise to combine them perfectly. With our Cloud Services, we offer both to our customers. Be it as Private Cloud Solutions in our own datacenters or on the Global Public Clouds together with our partners Amazon Web Services (AWS) and Microsoft Azure. In this workshop, you can make your own first steps towards the Cloud by starting your personal blog and right away deploy it to AWS.


# Your personal blog
Alright, let's get started. In the step by step guide below, you will create your first static site based on [hugo](https://gohugo.io/), push it to [GitHub](https://github.com/), and deploy it with [AWS Amplify](https://aws.amazon.com/amplify/).


## Step 1: Setup Hugo

Install Hugo using the guide for your platform (macOS, Windows, Linux, ...)

https://gohugo.io/getting-started/installing

```bash
# Test if everything is alright
$ hugo version
```


## Step 2: Start you first site

After you have successfully installed Hugo, we can use the handy `hug new site` command to start our personal blog project.
Go to a directory you want to work on and simply type the below commands. Replace *yourblog* with your personal project name.

```bash
# Initialize your site
$ hugo new site yourblog

# Change to the newly created directory
$ cd yourblog
```


## Step 3: Choose and configure your theme

In the current workshop we will work with the [hugo-coder](https://github.com/luizdepra/hugo-coder) theme.
However, there are many more themes at https://themes.gohugo.io.
```bash
# Initialize a new git repository
$ git init

# Configure your theme. Find more themes on https://themes.gohugo.io/
git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder
```

Configure your theme by opening `config.toml` file in the root directory of our site.
Start based on the config below and customize the params.

Note: the config below is dependant on the chosen theme. In case you've chosen another theme than hugo-coder, you will have to adapt parts of the config.

```toml
baseURL = "http://www.swisscom.com/"
languageCode = "en-us"
title = "Swisscom Student Day"
theme = "hugo-coder"

paginate = 20

pygmentsStyle = "monokai"
pygmentsCodeFences = true
pygmentsCodeFencesGuessSyntax = true

[taxonomies]
  category = "categories"
  series = "series"
  tag = "tags"
  author = "authors"

[params]
  author = "Swisscom Student Day 2022"
  info = "Deploy yourself to the Cloud!"
  description = "John Doe's personal website"
  keywords = "blog,developer,personal"
  avatarurl = "images/avatar.png"
  #gravatar = "john.doe@example.com"
  since = 2022
  enableTwemoji = true
  colorScheme = "auto"
  hidecolorschemetoggle = false

# Social links
[[params.social]]
  name = "Github"
  icon = "fa fa-github fa-2x"
  weight = 1
  url = "https://github.com/swisscom"
[[params.social]]
  name = "Twitter"
  icon = "fa fa-twitter fa-2x"
  weight = 3
  url = "https://twitter.com/swisscom"

# Menu links
[[menu.main]]
  name = "Blog"
  weight = 1
  url  = "posts/"
[[menu.main]]
  name = "About"
  weight = 2
  url = "about/"

```


## Step 4: Create your first content

Use the `hugo new` command to create your first pages.

```bash
# Create your first post and add some content
$ hugo new posts/my-first-post.md
$ echo "# My First Post" >> content/posts/my-first-post.md

# Create a simple static page 
$ hugo new about.md
$ echo "# About Me" >> content/about.md
```

Note: the echo commands are meant as example. Use your favorite editor or IDE to edit the newly created markdown files.
Learn more about Markdown in the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) or the [Markdown Guide](https://www.markdownguide.org/).


## Step 5: Push your site to GitHub



## Step 5: Deploy to AWS

