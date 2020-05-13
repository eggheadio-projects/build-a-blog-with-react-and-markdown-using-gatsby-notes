# [02. Install Plugins for Transforming Markdown with Gatsby](https://egghead.io/lessons/gatsby-install-plugins-for-transforming-markdown-with-gatsby)

Gatsby makes use of various plugins for building static sites. Here we will install `gatsby-source-filesystem` and `gatsby-transformer-remark` to work with locally stored Markdown files.

## Install `gatsby-source-filesystem`

The `gatsby-source-filesytem` is what is known as a Source Plugin. Data in Gatsby sites can come from anywhere: APIs, databases, CMSs, local files etc.

```bash
npm i gatsby-source-filesystem@2.0.1-beta.10
```

## Install `gatsby-transformer-remark`

The `gatsby-transformer-remark` is what is known as a Transformer Plugin. Transformer plugins take raw content from source plugins and transforms it into something more usable.

```bash
npm i gatsby-transformer-remark@2.1.1-beta.5
```

##  Create `gatsby-conifg.js`

```js
module.exports = {
  siteMetadata: {
    title: 'My Blog',
    description: 'This is my cool blog.'
  },
  plugins: [
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `pages`,
        path: `${__dirname}/src/pages`
      }
    }
  ]
}
```