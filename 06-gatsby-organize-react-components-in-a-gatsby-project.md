# [06. Organize React Components in a Gatsby Project](https://egghead.io/lessons/gatsby-organize-react-components-in-a-gatsby-project)

In this lesson, the Header component is extracted out of the main page layout and into its own file in a new components directory.

## Header.js

Inside of your `src` folder create a new folder called `components`.


Inside the components folder create a new file called `Header.js`. Go ahead and copy the Header component that we defined in our index.js file into the Header.js file.

```js
// components/Header.js

import React from "react"
import { StaticQuery, graphql } from 'gatsby'

const TitleAndDescription = ({data}) => {
  const title = data.site.siteMetadata.title
  const description = data.site.siteMetadata.description

  return (
    <div style={{
      display: 'flex',
      flexDirection: 'column',
      alignItems: 'center',
      fontFamily: 'avenir'
    }}>
      <h2 style={{marginBottom: 0}}>{title}</h2>
      <p style={{
        marginTop: 0,
        opacity: 0.5
      }}>
        {description}
      </p>
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
      render={data => <TitleAndDescription data={data} />}
    />
  )
}

export default Header
```

## Index.js

Now you can import our Header inside our `index.js` file. 

```js
import React from "react"
import { StaticQuery, graphql } from 'gatsby'
import Header from '../components/Header'

const Layout = () => {
  return (
    <div>
      <Header />
    </div>
  )
}

export default Layout 
```

Now if you check your page it should still work as expected.