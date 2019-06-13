[![CircleCI](https://circleci.com/gh/mozilla/extension-workshop/tree/master.svg?style=svg)](https://circleci.com/gh/mozilla/extension-workshop/tree/master)

# Extension Workshop

Launchpad for why and how to build Firefox extensions.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

- [Ruby 2.6.1](https://www.ruby-lang.org/en/downloads/), a dynamic open-source programming language
- [Jekyll](https://jekyllrb.com) site generator for [Github Pages](https://pages.github.com)
- [Yarn](https://yarnpkg.com/en/) Package Manager

Once you have Jekyll and yarn insalled you'll need to install the dependencies:

```
bundle install
yarn install
```

Then to run locally in devlopment run:

```
yarn start
```

Note: Running locally will show unpublished content that uses the `published: false` convention in frontmatter. Content with `published: false` will not be available on stage or production.

### Available yarn commands

| Command             | Description                                                                             |
| ------------------- | --------------------------------------------------------------------------------------- |
| yarn clean          | Clears the output directly and cleans the .jekyll-cache.                                |
| yarn build          | Builds the site.                                                                        |
| yarn start          | Starts jekyll and includes unpublished content. (Note the first run is slow!)           |
| yarn start-prodlike | Starts jekyll and doesn't include unpublished content for a production-like experience. |

## Content Updates

This site has three templates: a full-width page, a sidebar page for documentation, and a Content Guidelines page

### How to add a Content Guidelines page

#### Create a new page

1. Create new file
2. Add header (see example below)
3. Copy 'modules' needed from `content-guidelines/master-template.md` and paste in new file
4. Save as markdown: `content-guidelines/page-name.md`

```
---
layout: guides
title: Page Name
permalink: /content-guidelines/page-name/
published: false
---
```

Note: `published: false` will withhold this content from stage and production, to publish content, remove this line.

#### Upload media

1. Add the image files to `_assets/img/`
2. In your page, link to images using this page structure:

This tag will output an entire `img` element. Note: that using `@optim` enables the jekyll asset pipeline to optimize the image. This is always recommended unless you see an issue with the output.

```
{% asset "image.jpg" @optim %}
```

For finer control you can use:

```html
<img src="{% asset "image.jpg" @path @optim %}" someattr="whatever" />
```

Here's an example using markdown - note you need to add `@path` and `@optim`.

```markdown
![Remembear subtitle screenshot]({% asset "content-guidelines/remembear-subtitle.png" @path @optim %} "Remembear subtitle text")
```

#### Add the page to the menu

Go to `_data/content-guidelines-pages.yaml` and add a new entry for your page:

```
- title: "Page Name"
  url: "/content-guidelines/page-name/"
  draft-label: true
```

#### Controlling draft labelling

If you don't want the page to be labelled as a draft, as and when it's ready remove `draft-label: true` from the relevant entry in `_data/content-guidelines.yaml`

## Deployment

The site is auto-deployed on commits to master to https://extensionworkshop.allizom.org/

Tagged commits will be auto deployed to production.
