---
title: "Wiki"
---
# Basic Usage

The Wiki is written in [Markdown](https://guides.github.com/features/mastering-markdown/). To contribute to the documentation you can checkout the Wiki project from our [GitHub Repo](https://github.com/evannetwork/evannetwork.github.io).

The Markdown flavor used in this wiki is [kramdown](https://kramdown.gettalong.org/). For the differences and for flavor specific syntax see [this guide](https://kramdown.gettalong.org/syntax.html) or the [quickref](https://kramdown.gettalong.org/quickref.html).


## Write and test wiki pages
To create content and test the wiki pages locally you can use [Ruby Jekyll](https://jekyllrb.com/)

```bash
$ gem install jekyll bundler
$ bundle install
```

If ```bundle install``` fails with
```
Installing commonmarker 0.17.9 with native extensions
Gem::Ext::BuildError: ERROR: Failed to build gem native extension.
```

make sure that the package ```ruby-dev``` is installed. For example with:
```bash
sudo apt-get install ruby-dev
```
on Linux distributions, that use the apt package manager.

To start a local wiki jekyll instance and test the created wiki pages you can start jekyll with.
```bash
$ bundle exec jekyll serve --incremental
```

This starts a local http server at `http://127.0.0.1:4000` where you can serve the local version of the wiki.

