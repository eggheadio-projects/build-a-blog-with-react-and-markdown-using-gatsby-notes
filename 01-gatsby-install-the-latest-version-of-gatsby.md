## 01. Install the Latest Version of Gatsby

### Important Note ⚠️

The `gatsby@2.0.0-rc.28` is no longer maintained and not recommended for usage. To follow the course, install the `gatsby@2.0.0-rc.28` or install the latest Gatsby version. But if you install the latest version, please take into account that it will not match the course content.

## Install the Gatsby CLI

```curl
npm i gatsby@2.0.0-rc.28
```

Insure that you are running the Gatsby `` version: 

```curl
gatsby -v
```

## New site from course repo

```curl
git clone git@github.com:eggheadio-projects/build-a-blog-with-react-and-markdown-using-gatsby-code.git
```

Install dependencies:

```
npm install
```

Change directories into site folder and Start development server.

```
cd build-a-blog-with-react-and-markdown-using-gatsby-code
```

```
gatsby develop
```

Gatsby will start a hot-reloading development environment accessible by default at http://localhost:8000.

Try editing the JavaScript pages in `src/pages`. Saved changes will live reload in the browser.