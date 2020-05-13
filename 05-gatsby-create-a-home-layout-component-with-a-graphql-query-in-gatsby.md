# [05. Create a Home Layout Component with a GraphQL Query in Gatsby](https://egghead.io/lessons/gatsby-create-a-home-layout-component-with-a-graphql-query-in-gatsby)

## Refactor Hello Component

Let's refactor `index.js`. Create a new component called `Header` and let's have it will return our `StaticQuery` component. And one of the props that the `StaticQuery` returns is our actual GraphQL query:

```js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
    />
  )
}
const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}
```

Inside of our query `prop` we're going to pass a tagged templated with the syntax we use to make a GraphQL query:

```js
graphql`
  query {
    ...
  }
`
```

## ⚠️ Dealing with Deprecation

> StaticQuery does not work with raw React.createElement calls; please use JSX, e.g. `<StaticQuery />`

## StaticQuery

The next prop that we pass to `StaticQuery` is what we want to render.

```js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
      render={data => <div>{data.site.siteMetadata.title}}
    />
  )
}
const Layout = () => {
  return (
    <div>
      <Header />
    </div>
  )
}

export default Layout
```


Now we're able to replace our `Hello world!` with our `Header` component.

## New Component

Let's clean up our the our render `prop` by creating a new component:

```js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const TitleAndDescription = ( {data}) => {
  const title = data.site.siteMetadata.title
  const description = data.site.siteMetadata.description

  return (
    <div>
      <h2>{title}</h2>
      <p>{description}</p>
    </div>
  )
}

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
      render={data => <TitleAndDescription data={data}>}
    />
  )
}
const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}

export default Layout
```
