---
title: "Getting started with Jekyll and GitHub Pages"
date: 2024-02-27
layout: post
category: applied
tags: [jekyll, gh-pages]
---
The 
Best is to start with a working template, for example, the same that was used for this project, [template](https://github.com/jsanz/gh-pages-minima-starter/). This template also includes a very nice tutorial, [setup](https://jsanz.github.io/gh-pages-minima-starter/2020/03/22/get-code.html).

However a few side notes;
You maybe need to export the path to your ruby installation (GNU+Linux)
```bash
export PATH=/home/<USERDIR>/.local/share/gem/ruby/<ruby version, eg: 3.0.0>/bin:$PATH
export GEM_HOME=$(ls -t -U | ruby -e 'puts Gem.user_dir')
```
It might be that the live preview has a missing json dependency.
In that cas just add it to the Gemfile.
```ruby
gem "json", "~> 2.7"
```
If you intend to do something with tags, keep the following in mind 
- GitHub Pages comes with fixed plugins if you want Github to take care of building
- Tag overview pages cant be created programmatically without a plugin
