# [11. Expose Post Tag Data for a Gatsby Blog](https://egghead.io/lessons/gatsby-expose-post-tag-data-for-a-gatsby-blog)

In this lesson we will prepare Tag browsing templates, and update `gatsby-node.js` to use GraphQL to query for tags in our Markdown posts.

## Query to get all tags


```js
import React form "react"
import { graphql, links } from 'gatsby'

const AllTagsTemplates = ({data}) => {
  return (
    <div>
     <div>
       tags here
    </div>
  )
}

export defualt AllTagsTemplate
```

Go to `gatsby-node.js` and create a new function called `createTagPages`. And `createTagPages` will take in `createPage` and the list of posts. 

```js
const createTagPages = (createPage, posts) => {
  const allTagIndexTemplate = path.resolve('src/templates/allTagsIndex.js')
  const singleTagIndexTemplate = path.resolve('src/templates/singleTagIndex.js')
}
```

```js
const postByTag = {}

posts.forEach(({node}) => {
  if (node.frontmatter.tags) {
    node.frontmatter.tags.forEach(tag => {
      if(!postsByTag[tag]) {
        postsByTag[tag] = []
      }
      postsByTag[tag].push(node)
    })
  }
})
```

## Dynamically create a key

We are dynamically creating a key for each of our tags. Each of those keys will have an array of the posts that use that tag. 

Now call createPage. Our path will be `'/tags'`. The component will be the `allTagsIndexTemplate`. The context that we're going to pass will be called tags and it will be `tags.sort`, so this will be a sorted list of all of our tags.

```js
const tags = Object.keys(postsByTag)

createPage({
  path: '/tags'
  component: allTagsIndexTemplate,
  context: {
  tags: tags.sort()
  }
})
```

## Process each `Post`

We're going to call our `createTagPages` function with our `createPage` action and all the posts that we created.

```js
const posts = result.data.allMarkdownRemark.edges

createTagPages(createPage, posts)
```

Now on our `/tags` page, hit reload, and we see that our `/tags` page is being created.

```js
import React from "react"
import { graphql, Link } from 'gatsby'

const AllTagsTemplate = ({data, pageContext}) => {
 console.log(pageContext)
  return (
    <div style={{fontFamily: 'avenir'}}>
      <div>
        tags here
      </div>
    </div>
  )
}

export default AllTagsTemplate
```

Data is what's used for a query that would be inside of this template and `pageContext` is what gets passed from `gatsby-node.js`.

In your query be sure to include the tags key:

```js
  edges {
    node {
      frontmatter {
        path
        title
        tags
      }
    }
  }
```
