# [小七的博客](https://summer1914.github.io/)

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/cd4fd74b864245a391d8678f1f458359)](https://www.codacy.com/app/summer1914/summer1914.github.io?utm_source=github.com&utm_medium=referral&utm_content=summer1914/summer1914.github.io&utm_campaign=badger)
<!-- [![Build Status](https://travis-ci.org/summer1914/summer1914.github.io.svg?branch=master)](https://travis-ci.org/summer1914/summer1914.github.io) -->

## Features

The blog is based on mmistakes' contribution for [Minimal Mistakes Jekyll Theme](https://github.com/mmistakes/minimal-mistakes). Besides, I create a new layout `keynote`, to combine nicely HTML Presentation content and your blog post.

**Usage**: a extra `iframe` is used to define the url of your HTML Presentation, the format of `keynote` layout shows below: 

```
---
date: XXXX-XX-XX
layout: keynote
title: THIS IS YOUR ARTICLE TITLE
thread: THREAD ID
categories: CATEGORY
tags: [tag1, tag2]
excerpt: Introduction
iframe: PUT YOUR URL HERE, such as https://summer1914.github.io/slides/s-D3-Basic-Tutorial
---
```

Progressive Web APP Support: TBD

## Serve locally

```
git clone git@github.com:summer1914/summer1914.github.io.git
bundle exec jekyll serve
```

## About

[Create](https://github.com/summer1914/summer1914.github.io/issues/new) a new issue to report bugs or communicate with me about your insights.

This is the source code for my personal website.

Unless stated otherwise, all content is MIT-licensed.

Joe Jiang

2017.2
