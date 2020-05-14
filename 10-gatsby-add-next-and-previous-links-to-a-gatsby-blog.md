#  [10. Add Next and Previous Links to a Gatsby Blog](https://egghead.io/lessons/gatsby-add-next-and-previous-links-to-a-gatsby-blog)

Gatsby’s `createPage` action allows for additional data to be passed in via context. In this lesson, we will add a processing step to include links between posts, and update our templates to conditionally display them as appropriate.

## gatsby-node.js

Let's include a new variable for `posts`, because we're going to need to know where we're at in the list in order to link back and forth. We'll do `const posts = result.data.allMarkdownRemark.edges`, and then we can just update the line below to be `posts.forEach`.


```js
).then(result => {
  const posts = result.data.allMarkdownRemark.edges
  
  posts.forEach(({node}) => {
    ...
  })
})
```

Let's also get the index of each post: 

```js
context: {
  pathSlug: path, 
  prev: index === 0 ? null: posts[index - 1].node,
  next: index === (posts.length - 1) ? null : posts[index + 1].node
}
```

## Passing `pageContext`

We need to add a sort parameter to the `allMarkdownRemark` query in `gatsby-node.js`. Inside of `gatsby-node.js`, we're going to add a sort to the `allMarkdownRemark` query. And we'll use the `sort` keyword. `Sort` takes an object. We will `sort` in ascending order, based on `front matter___date`.

```js
query {
  allMarkdownRemark (
    sort: {order: ASC, fields: [frontmatter___date]}
    ...
  )
}
```

## Adding `Link`

Since we now that we're getting next and previous passed through the page context, let's add some links. We'll delete the console.log, and then we will destructure `next` and `prev` from `pageContext`. We'll `import { Link } from Gatsby`.

```js
import { graphql, Link } from 'gatsby'

const Template = ({data, pagecontext}) => {
  const {next, prev} = pagecontext
}
```

We'll do `next && <Link to={next.frontMatter.path}>` and we'll do the same for the previous link:

```js
const Template = ({data, pageContext}) => {
  const {next, prev} = pageContext

  const {markdownRemark} = data
  const title = markdownRemark.frontmatter.title
  const html = markdownRemark.html
  return (
    <div>
      <h1 style={{fontFamily: 'avenir'}}>{title}</h1>
      <div className='blogpost'
        dangerouslySetInnerHTML={{__html: html}}
        style={{
          fontFamily: 'avenir'
        }}
      />

      <div style={{marginBottom: '1rem', fontFamily: 'avenir'}}>
        {next &&
          <Link to={next.frontmatter.path}>
            Next: {`${next.frontmatter.title}`}
          </Link>
        }
      </div>
      <div style={{fontFamily: 'avenir'}}>
        {prev &&
          <Link to={prev.frontmatter.path}>
            Prev: {`${prev.frontmatter.title}`}
          </Link>
        }
      </div>
    </div>
  )
}
```



## Resources

- [Adding Pagination](https://www.gatsbyjs.org/docs/adding-pagination/#other-resources)