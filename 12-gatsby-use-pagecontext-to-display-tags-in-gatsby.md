# [12. Use PageContext to Display Tags in Gatsby](https://egghead.io/lessons/gatsby-use-pagecontext-to-display-tags-in-gatsby)

Gatsby uses PageContext to pass additional information into a React component. In this lesson we will update our Tag page templates to display data.

## Individual URL for Tags

Our component will be `singleTagIndexTemplate`. Our context will be the `posts` and the `tagName`.

```js
// singleTagIndex.js

import React from "react"
import { graphql, Link } from 'gatsby'

const SingleTagTemplate = ({data, pageContext}) => {
  const { posts, tagName } = pageContext
  return (
    <div style={{fontFamily: 'avenir'}}>
      <div>
        Posts about {`${tagName}`}
      </div>
      <div>
        <ul>
          {posts.map((post, index) => {
            return (
              <li key={index}>
                <Link to={post.frontmatter.path}>
                  {post.frontmatter.title}
                </Link>
              </li>
            )
          })}
        </ul>
      </div>
    </div>
  )
}

export default SingleTagTemplate

```

And we'll add a key that will be our `index`. We will add `Link` and pass our props `post.frontmatter.path`:

```js
// singleTagsIndex.js

import React from "react"
import { graphql, Link } from 'gatsby'

const SingleTagTemplate = ({data, pageContext}) => {
  const { posts, tagName } = pageContext
  return (
    <div style={{fontFamily: 'avenir'}}>
      <div>
        Posts about {`${tagName}`}
      </div>
      <div>
        <ul>
          {posts.map((post, index) => {
            return (
              <li key={index}>
                <Link to={post.frontmatter.path}>
                  {post.frontmatter.title}
                </Link>
              </li>
            )
          })}
        </ul>
      </div>
    </div>
  )
}

export default SingleTagTemplate
```

## Browse by Tag link

We got to browse by `Tag link`, click it, and we get to `/tags`.

```js
<div>
  <Link to='/tags'>Browse by Tag</Link>
</div>
```

And finally, go back to our `allTagsIndex`, and add a leading slash.

```js
<li key={index}>
  <Link to={`/tags/${tagName}`}>
    {tagName}
  </Link>
</li>
```