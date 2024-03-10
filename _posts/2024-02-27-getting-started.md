---
title: "Getting started with Jekyll and GitHub Pages"
modified_date: 2024-03-10
date: 2024-02-27
layout: post
category: applied
tags: [jekyll, gh-pages]
---
A brief overview of how to get things started quickly and some not so obvious Jekyll and Markdown features.

##### Table of Contents
{:.no_toc}
* A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}

### Getting Started
The best is to start with a working template, for example, the same that was used for this project, [template](https://github.com/jsanz/gh-pages-minima-starter/). This template also includes a very nice tutorial, [setup](https://jsanz.github.io/gh-pages-minima-starter/2020/03/22/get-code.html).

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

### Not so obvious Markdown and Jekyll features

For a complete list of all github flavoured markdown features head to the official [^docs]

Github Pages can be configured among other tools to use kramdown as converter. The docs for this can be found here [^kramdowndocs].
#### Footnotes
You can use footnotes in conjunction with the markdown parser kramdown. Kramdown is one of default github markdown parsers for gh-pages.

The announcement was in 2021[^footnotes] <== footnote example.
Some additional resources: 
- [Official Docs: footnotes](https://docs.github.com/en/enterprise-cloud@latest/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#footnotes)
- Jake Lee has written a nice summary (with edgecases) about the syntax in this [blog post](https://blog.jakelee.co.uk/footnote-experiments-on-github-and-jekyll/).

#### Table of Contents
To create a toc 2 steps are necessary.
First use kramdown as markdown converter, for this add 'markdown: kramdown' to your _config.yml file.

Secondly, use something like the following snippet to your posts [kramdown: html#toc](https://kramdown.gettalong.org/converter/html.html#toc):
```markdown
#### Table of Contents
{:.no_toc}
* A markdown unordered list which will be replaced with the ToC, excluding the "Contents header" from above
{:toc}
```
#### Ensure Links open in new Tabs
[See this Jeyll discussion](https://talk.jekyllrb.com/t/how-can-i-ensure-my-links-open-in-a-new-tab/4318){:target="_blank"}

Or copy paste this example:
```markdown
[link text](the link){:target="_blank"}
```

#### test
bla
{: .block-tip }

### References

[^footnotes]: [https://github.blog/changelog/2021-09-30-footnotes-now-supported-in-markdown-fields/](https://github.blog/changelog/2021-09-30-footnotes-now-supported-in-markdown-fields/)
[^docs]: [https://docs.github.com/en/enterprise-cloud@latest/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/en/enterprise-cloud@latest/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
[^kramdowndocs]: [https://kramdown.gettalong.org/converter/html.html](https://kramdown.gettalong.org/converter/html.html)

