# [01. Install the Latest Version of Gatsby](https://egghead.io/lessons/gatsby-install-the-latest-version-of-gatsby)

## Important ⚠️

> To follow the course, install the `gatsby@2.0.0-rc.28`. But take into account that `gatsby@2.0.0-rc.28` is no longer maintained and not recommended for usage. 

## Install the Gatsby CLI

```bash
npm i gatsby@2.0.0-rc.28
```

Insure that you are running the Gatsby `2.0.0-rc.28` version: 

```bash
gatsby -v
```

Create a new site:

```bash
gatsby new gatsby-site
```

## Course repo

An alternative, and recommended way to successfully follow the course is to `git clone` the course repo:

```bash
git clone git@github.com:eggheadio-projects/build-a-blog-with-react-and-markdown-using-gatsby-code.git
```

Install dependencies:

```bash
npm install
```

Change directories into site folder and start development server.

```bash
cd build-a-blog-with-react-and-markdown-using-gatsby-code
```

```bash
gatsby develop
```

Gatsby will start a hot-reloading development environment accessible by default at http://localhost:8000.

## Start development server

Try editing the JavaScript pages in `src/pages`. Saved changes will live reload in the browser.
