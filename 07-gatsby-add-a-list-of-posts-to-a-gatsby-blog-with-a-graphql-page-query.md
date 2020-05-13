# [07. Add a List of Posts to a Gatsby Blog with a GraphQL Page Query](https://egghead.io/lessons/gatsby-add-a-list-of-posts-to-a-gatsby-blog-with-a-graphql-page-query)

# Add a List of Posts to a Gatsby Blog with a GraphQL Page Query

We're going to focus on using Page queries. We can use GraphiQL to help us write our queries.

```JS
import React from "react"
import { graphql } from "gatsby"
import Header from "../components/Header"

const Layout = (props) => {
  console.log(props)
  return (
    <div>
     <Header />
    </div>
  )
}

export const query = graphql`
 query HomepageQuery {
   allMarkdownRemark {
     edges {
       node {
         id
         frontmatter {
           title
           path
           date
         }
       }
     }
   }
 }
`
export default Layout
```

Use the console log to see the data that is being brought in by your query. You'll notice that our query is showing up under the `data` key.

```JS
import React from "react"
import { graphql } from "gatsby"
import Header from "../components/Header"

const Layout = ( {data}) => {
 const { edges } = data.allMarkdownRemark
 return (
   <div>
    <Header />
    {
      edges.map(edge => {
        const { id, frontmatter } = edge.node
        return (
          <div key={id}>{frontmatter.title}</div>
        )
      })
    }
   </div>
 )
}

export const query = graphql`
query HomepageQuery {
  allMarkdownRemark {
    edges {
      node {
        id
        frontmatter {
          title
          path
          date
        }
      }
    }
  }
}
`
export default Layout
```


To get our posts to display in the correct order you can go back to GraphiQL and look at the Documentation Explorer and look at `allMarkdownRemark` and see that it can pass it some arguments. 

One of them is `sort`. We can sort on fields in this case it will be `frontmatter___date` and provide it an order of `DESC`.

```JS
export const query = graphql`
query HomepageQuery {
  allMarkdownRemark(sort: {order: DESC, fields: [frontmatter___date]}) {
    edges {
      node {
        id
        frontmatter {
          title
          path
          date
        }
      }
    }
  }
}
`
```

