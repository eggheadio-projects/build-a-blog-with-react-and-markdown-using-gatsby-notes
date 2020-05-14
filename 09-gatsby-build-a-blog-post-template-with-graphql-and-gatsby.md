# [09. Build a Blog Post Template with GraphQL and Gatsby](https://egghead.io/lessons/gatsby-build-a-blog-post-template-with-graphql-and-gatsby)

In order to display the generated HTML from a Markdown post, we will build a GraphQL query and pass its data into a Template component that makes use of React’s `dangerouslySetInnerHTML` API to add a DOM element.

## Template Query

In our `blogPost.js` template write the following:

```js
export const query = graphql`
  query($pathSlug: String!) {
    markdownRemark(frontmatter: { path: { eq: $pathSlug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`
```


## `dangerouslySetInnerHTML` API

We're going to use React's `dangerouslySetInnerHTML` API. We pass in an object of `__html`. Its value will be `html`. 

```js
const Template = (props) => {
  console.log(props)
  const title = props.data.markdownRemark.frontmatter.title
  const html = props.data.markdownRemark.html
  return (
    <div>
      <div className='blogpost'
      dangerouslySetInnerHTML={{__html: html}}
      />
    </div>
  )
}
```

This is going to render the HTML from the query

Let's add a title. We have our title and our post showing up. We can click back to the home page. We see that all of our posts have pages now. Added a little bit of style. We're good to go.

```js
const Template = ({data}) => {
  const {markdownRemark} = data
  const title = markdownRemark.frontmatter.title
  const html = markdownremark.html
  return (
    <div>
      <h1 style={{fontFamily: 'avenir'}}>{title}</h1>
      <div className='blogpost' 
        dangerouslySetInnerHTML={{__html: html}} style={{
          fontFamily: 'avenir'
        }}
      />
    </div>
  )
}
```