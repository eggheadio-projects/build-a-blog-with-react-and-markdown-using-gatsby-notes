# [08. Build Gatsby Page Slugs Dynamically from Markdown with gatsby-node.js](https://egghead.io/lessons/gatsby-build-gatsby-page-slugs-dynamically-from-markdown-with-gatsby-node-js)

Gatsby includes several Node APIs for building sites. In this lesson, we’ll use the `createPages` API to dynamically build a page for each of our posts, by using the URL path in the front matter of each Markdown doc found via a GraphQL query.

## 📕 Notes

## Page template

Create a folder in the `/src` directory of your Gatsby application called templates. Now create a `blogTemplate.js` inside it with the following content:

```js
import React from "react"
import { graphql } from "gatsby"

export default function Template({
  data, // this prop will be injected by the GraphQL query below.
}) {
  const { markdownRemark } = data // data.markdownRemark holds your post data
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post-container">
      <div className="blog-post">
        <h1>{frontmatter.title}</h1>
        <h2>{frontmatter.date}</h2>
        <div
          className="blog-post-content"
          dangerouslySetInnerHTML={{ __html: html }}
        />
      </div>
    </div>
  )
}

export const pageQuery = graphql`
  query($slug: String!) {
    markdownRemark(frontmatter: { slug: { eq: $slug } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        slug
        title
      }
    }
  }
`
```

## `createPage` API

Use the graphql to query Markdown file data as below. Next, use the createPage action creator to create a page for each of the Markdown files using the blogTemplate.js you created in the previous step.

```js
exports.createPages = async ({ actions, graphql, reporter }) => {
  const { createPage } = actions

  const blogPostTemplate = require.resolve(`./src/templates/blogTemplate.js`)

  const result = await graphql(`
    {
      allMarkdownRemark(
        sort: { order: DESC, fields: [frontmatter___date] }
        limit: 1000
      ) {
        edges {
          node {
            frontmatter {
              slug
            }
          }
        }
      }
    }
  `)

  // Handle errors
  if (result.errors) {
    reporter.panicOnBuild(`Error while running GraphQL query.`)
    return
  }

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.slug,
      component: blogPostTemplate,
      context: {
        // additional data can be passed via context
        slug: node.frontmatter.slug,
      },
    })
  })
}
```

Gatsby calls the `createPages` API (if present) at build time with injected parameters, `actions` and `graphql`.

## ⚠️ Important

If you're following the video lesson. The `graphql` call returns a promise, so we can just return that directly. No need to call it again. 

## ⚙️ Resources
