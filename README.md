![Kube](https://cdn.rawgit.com/uptownhr/kube/master/src/containers/Home/cube.svg)

# Kube
Universal React Express middleware package. A universal react dev environment provided through `npm install`


## What's included?
Kube comes with with a middleware that will,

1. render your components `react-router/routes` component serverside
2. webpack dev server
3. webpack hot module reloader server
4. webpack module loaders from the server

## Webpack module loaders for the server
Webpack module loaders are awesome and brings lot of value to your react development. You can now compose a package with all it's depedencies together. However, problems rise when you attempt to use module loaders for server side rendering purposes. Normal implementations of SSR uses the React-DOMServer to render a component to string. When the DOMServer attempts to require in a file(like an image) normally handled by a webpack loader, it will error out. Node's require expects all loaded files to be a JSON. 
 
 Using Kube, components rendered from the server are also prebuilt using webpack. Meaning all the module loaders have parsed through the require statements already. This results in a clean translation between client/server, allowing you to easily use module loaders on react universally. 


## Use as a standalone server
`npm install -g kube`

New Project

1. `kube init testing-kube`
2. `cd testing-kube`
3. `kube up`

Existing Project

1. `cd your-project`
2. `kube init`
3. `kube up`

Visit localhost:3000

## Use as a Middleware
`npm install --save-dev kube`

### Express App - Server side rendering
```js
// /index.js
const express = require('express');
const app = express()

/*
Loads middleware and provides
1. the webpack dev server
2. the webpack hot moldule reloader
3. res.kube.render
*/
require('kube')(app, {
  src_path: "src",
  public_path: "public",
  debug: false
})

app.get('/', function(req,res){
  let state = { ssr: 'server state' }
  res.kube.render(state)
})
```
