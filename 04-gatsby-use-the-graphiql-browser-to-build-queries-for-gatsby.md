# [04. Use the GraphiQL Browser to Build Queries for Gatsby](https://egghead.io/lessons/gatsby-use-the-graphiql-browser-to-build-queries-for-gatsby)

GraphiQL is the GraphQL integrated development environment (IDE). It’s a powerful (and all-around awesome) tool you’ll use often while building Gatsby websites.

You can access it when your site’s development server is running—normally at `http://localhost:8000/___graphql`.

## ⚠️ Dealing with Deprecation

This is the new way to query file nodes. It's important to add `query MyQuery`.

```graphql
query MyQuery {
  allFile {
    edges {
      node {
        extension
        dir
        modifiedTime
      }
    }
  }
}
```

## Adding GraphiQL Input

This was the data that was fetched from the gatsby-config.js file.

```graphql
query MyQuery {
  site {
    siteMetadata {
      title
      description
    }
  }
}
```

Make sure to check out the GraphiQL docs in the upper right-hand corner of the IDE. It’s easy to miss them, but they’re worth visiting!

## GraphiQL Output

Let's do the same thing for allMarkdownRemark:

```graphql
query MyQuery {
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          title
          path
          date
          excerpt
        }
      }
    }
  }
}
```

You should expect this to return JSON to return all of the front matter from your different markdown files. Also you can think of edges as the file paths and node as the individual markdown files.
