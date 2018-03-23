# Basic Usage

The Wiki is written in [Markdown](https://guides.github.com/features/mastering-markdown/). To contribute to the documentation you can checkout the Wiki project from our [GitHub Repo](https://github.com/evannetwork/evannetwork.github.io).

## Write and test wiki pages
To create content and test the wiki pages locally you can use [Ruby Jekyll](https://jekyllrb.com/)

```bash
$ gem install jekyll bundler
$ bundle install
```

To start a local wiki jekyll instance and test the created wiki pages you can start jekyll with.
```bash
$ bundle exec jekyll serve --incremental
```

This starts a local http server at `http://127.0.0.1:4000` where you can serve the local version of the wiki.
