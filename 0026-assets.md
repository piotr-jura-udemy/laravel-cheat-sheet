### Laravel Mix

Laravel Mix is a tool on top of [Webpack](https://webpack.js.org/).
It's main purpose is to make life of Laravel developer much easier and does not require you to know Webpack to get started.

#### What is Webpack?

Webpack is a module bundler for JavaScript applications.

The simplest explanation - it converts some input files into output files.

The input files are one or more JavaScript files, like librariries (React/Vue.js/jQuery and plugins) and your own code. Webpack will then let you to generate a single JavaScript file in a smart way (it will create a dependency graph to know what is used and where).

#### Installing Node and NPM

To use Laravel Mix and thus Webpack, you need Node and NPM.
 
[Download Node](https://nodejs.org/en/)
 
NPM is bundled together with Node. Installation is as easy as it gets (on Windows and Mac), it comes with a UI installer.

#### What is Node?

Node.js is a JavaScript runtime environment. It's everything you need to run a JavaScript program outside the browser.

#### Installing Laravel Mix

All dependencies are defined inside the `package.json` file. You just need to run

```
npm install
```

The `package.json` contains all JavaScript and CSS libraries your app needs along with their desired version.

It creates a file called `package-lock.json`. It contains all the libraries that were installed and their version. This file should be included in your project (in GIT repository).

The difference is simple:

- You edit `package.json` to say what you need
- `package-lock.json` is auto-generated and describes the versions of libraries installed, and let's every other environment on which your project runs install them using the same exact versions that you have

`package.json` is like `composer.json` in PHP
`package-lock.json` is like `composer.lock` in PHP

All the libraries are installed into the `node_modules` folder.
 
#### webpack.mix.js

Laravel Mix configuration file is called `webpack.mix.js`.

By default it is configured to bundle your application JavaScript and CSS files.

The main JavaScript file is `resources/js/app.js`
The main CSS file is `resources/sass/app.scss`

