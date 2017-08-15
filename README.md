# Webpack installation

During this short tutorial, we will be installing webpack from scratch.

## What do you need?
You will need a computer with Node and NPM installed.

1. Check your version of NPM:

```sh
$ npm -v
```

Note: You need at least the 3.5 version of NPM to avoid any performance issues.

2. Create a new npm package

```sh
$ npm init -y
```

3. Install webpack

```sh
$ npm install --save-dev webpack
```

4. We want to be able to bunble CSS file into our JS bundles, for that we need both the Style and CSS loaders.

```sh
$ npm install --save-dev style-loader css-loader
```

5. We also want to use SCSS (Sass) syntaxt.

```sh
$ npm install sass-loader node-sass webpack --save-dev
```

6. Create a _./src_ directory and a _./public_ directory

The _src/_ directory will contain your source code: javascript and scss.
The _public/_ directory will contain your base HTML and images. All other files will be automatically created by webpack.

7. Create a _webpack.config.js_ file with the following content:

```
  const path = require('path');

  module.exports = {
    entry: './src/index.js',
    output: {
      filename: 'bundle.js',
      path: path.resolve(__dirname, 'public')
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                'style-loader',
                'css-loader'
                ]
            },
            {  //Here we are including the .scss loader to make it transpale Sass to CSS.
                test: /\.scss$/,
                use: [{
                    loader: "style-loader" // creates style nodes from JS strings
                }, {
                    loader: "css-loader" // translates CSS into CommonJS
                }, {
                    loader: "sass-loader" // compiles Sass to CSS
                }]
            }
        ]
    }
  };
```

8. Create a _index.js_ file inside the _./src_ folder with the following content:

```
window.onload=function(){ alert('hello webpack'); }
```

9. Run webpack with the following command:

```sh
$ webpack
```

10. Make sure that webpack created the bundle, you should see an output like this:
```sh
    $ webpack
    
    Hash: 69f7ef42fb105dfe89e9
    Version: webpack 3.5.4
    Time: 115ms
        Asset     Size  Chunks             Chunk Names
    bundle.js  2.52 kB       0  [emitted]  main
       [0] ./src/index.js 50 bytes {0} [built]
```

11. If everything went well, create an _./public/index.html_ file and import the _bundle.js_ script. Run you _index.html_ file and the alert should promt!