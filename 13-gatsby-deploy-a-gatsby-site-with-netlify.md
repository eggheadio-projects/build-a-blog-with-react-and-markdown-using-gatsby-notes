# [13. Deploy a Gatsby Site with Netlify](https://egghead.io/lessons/gatsby-deploy-a-gatsby-site-with-netlify)

There are several options for hosting your Gatsby blog. In this lesson, you'll learn how to deploy your site to Netlify.

## Running `gatsby build`

Now that we're done building our blog, we can run `gatsby build`. While this does its thing, we'll come over to GitHub, and we'll create a new repository. We'll copy our `add origin`. Inside of our `myBlog directory`, we have a new `public directory`.


## Push to Github

```bash
$ git init
$ git remote add origin git@github.com:taylorbeii/gatsby-demo-blog.git
$ git add .
$ git commit -am "initial commit" 
$ git push origin master
```

ow, over Netlify, I've logged in, and I'm going to use the new site from Git, connect to GitHub here, and find our demo blog. Our branch will be `master`. We don't have any build commands or publish directories because we've uploaded it into the route, and clicked the deploy button.

After it's done deploying, we can open it in a new tab, and our blog is live.

## ⚠️ Dealing with Deprecation

It's also possible to deploy the entire Gatsby website to Netlify. Click on the `Deploy site` button and Netlify will start the `build` and `deploy` process you have specified. You can go to the `Deploys tab` and see the process unfold in the `Deploy log`. After a few moments, it will give you the live site URL, e.g., `random-name.netlify.com`.

Remember to add your deploy settings with the below options (if needed):

Branch to deploy: the default is `master`.
Build Command: the default is `npm run build`.
Publish directory: the default is `public`.

## Resources

- [Deploying to Netlify](https://www.gatsbyjs.org/docs/deploying-to-netlify/)