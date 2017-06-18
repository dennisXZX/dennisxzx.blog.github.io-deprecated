---
layout: post
title: React Project Set Up
categories: [React]
---

Create-react-app is a popular tool for building a react app as it abstracts away the build configuration. However, it is necessary to know what is happening under the hood in order to become a better web developer.

To create a react app, we first install node.js and NPM to manage our dependencies. We use `npm init` to initialize a `package.json` file.

After that, we need to install a whole bunch of packages for the react project.

```
npm-install --save react react-dom

npm install --save-dev babel-core babel-loader babel-preset-env babel-preset-react css-loader style-loader sass-loader node-sass html-webpack-plugin webpack webpack-dev-server
```

In order to set up an automated build process, we need to config our webpack.

```
const path = require('path');
// a webpac plugin which helps generate an HTML file in the distribution folder
// and also inserts the bundle.js into the generated HTML file 
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	// define the root js file
	entry: './app/index.js',
	// define the name of the output file and where it should be located
	output: {
		path: path.resolve(__dirname, 'dist'),
		filename: 'bundle.js'
	},
	// define what loaders should be applied
	module: {
		rules: [
			// transform js file through babel
			// the babel config file can be found in .babelrc
			{ test: /\.(js)$/, use: 'babel-loader' },
			// style loader adds the CSS to the DOM
			// css loader adds the CSS into the js file 
			// sass-loader loads a SASS file and compiles it to CSS (requires node-sass as peer dependency)
			{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
		]
	},
	plugins: [new HtmlWebpackPlugin({
		template: 'app/index.html'
	})]
}
```

Note: This build process will inject all CSS into the js file. If you would like to have a separate CSS file in the dist folder, you can use the `ExtractTextPlugin` to achieve that.

Now let's look at our `.babelrc` file. Babel would transform all Javascript to browser-compatible. In addition, it would translate all JSX to plain Javascript.

```
// babel-preset-env lets you specify an environment and automatically enables the necessary plugins. The default behavior without options runs all transforms (behaves the same as babel-preset-latest).
{
	"presets": [
		"env",
		"react"
	]
}
```

After the configuration of Webpack and Babel, we set up an NPM script to kick start the project by using `webpack-dev-server`.

```
  "scripts": {
    "start": "webpack-dev-server --open",
		"build": "webpack"
  }
```

Hooray! We have finally set up our own build process. Now you can simply use `npm start` for development and `npm build` for production build.