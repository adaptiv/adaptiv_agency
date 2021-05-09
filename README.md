# Web site for Adaptiv Sthlm AB

## Jekyll

This site is based on the [Jekyll](https://jekyllrb.com/) static site generator.
Jekyll uses the [Liquid](https://shopify.github.io/liquid/) template language.

## Agency

We use the Agency theme based on [Agency bootstrap theme ](https://startbootstrap.com/template-overviews/agency/)

## GitHub Pages

We host our repo on GitHub and publish the site on [GitHub Pages](https://docs.github.com/en/pages).

## How to use

### Start

The index.html is the start page. It uses its own layout, which includes the sections.
It contains sections on our offerings, the team, about Adaptiv, and contact information.

### Articles

Articles and blog posts is on a separate page. Posts are written in
[Markdown](https://www.markdownguide.org/) and placed in the _posts directory.

Articles are listed on the 'posts.html' page.

Individual articles use the 'post.html' layout.

### Sustainability

Sustainability is a separate page. Content is found in '_includes/sustainability.html'.

### Team

Team members and info are in global configuration file '_config.yml'

Images are in '/img/team/'

### About

Images are in '/img/about/'

## Run locally

```bash
gem install jekyll
make start
```
