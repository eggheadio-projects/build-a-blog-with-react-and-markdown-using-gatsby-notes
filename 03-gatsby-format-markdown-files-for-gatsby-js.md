# [03. Format Markdown Files for Gatsby.js](https://egghead.io/lessons/gatsby-format-markdown-files-for-gatsby-js)

Front matter allows you to keep metadata attached to an instance of a content type—i.e., embedded inside a content file—and is one of the many features that gives Gatsby its strength.

## Format Markdown Files

Go to your `src/pages` directory and add in a few directories with the slug `YYYY-MM-DD-name-of-post`.

Inside the `index.md` file add the Front Matter for the site. 

```yml
---
path: "/first-post"
date: "2018-07-21"
title: "My First Post"
tags: ['this', 'that']
excerpt: "A preview of my first post"
---

Lorem ipsum.
```

Follow this pattern for all of your posts.

## ⚠️ Dealing with Deprecation

You can have multiple instances of this plugin to read source nodes from different locations on your filesystem.
