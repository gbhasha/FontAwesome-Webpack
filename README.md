FontAwesome-webpack
====================

Font awesome configuration and loading package for webpack, using font-awesome (SCSS).

Based on font-awesome-webpack (less) by Gowrav Shekar (@gowravshekar).

Usage
-----

```bash
$ npm i FontAwesome-webpack font-awesome
```

To properly load font-awesome fonts, you need to configure loaders in your `webpack.config.js`. Example:

``` javascript
module.exports = {
  module: {
    loaders: [
      // the url-loader uses DataUrls.
      // the file-loader emits files.
      { test: /\.woff(2)?(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: "url-loader?limit=10000&mimetype=application/font-woff" },
      { test: /\.(ttf|eot|svg)(\?v=[0-9]\.[0-9]\.[0-9])?$/, loader: "file-loader" }
    ]
  }
};
```

Font awesome font urls are of the format `[dot][extension]?=[version-number]`, for example `.woff?v=4.2.0`

The Regex for font types are adjusted to support these formats. Regex also support urls ending with .woff, .ttf, .eot and .svg (Used by Bootstrap).

### Complete Font-Awesome

To use the complete font-awesome package including all styles with the default settings:

``` javascript
require("FontAwesome-webpack");
```

The `require` statement should be present in your application code(Entry file or any other file required in entry file) and not in webpack.config.js.

### Custom configuration

You can configurate FontAwesome-webpack with two configuration files:

* `font-awesome.config.js`
* `font-awesome.config.scss`

Add both files *next to each other* in your project. Then:

``` javascript
require("FontAwesome-webpack!./path/to/font-awesome.config.js");
```

Or simple add it as entry point to your `webpack.config.js`:

``` javascript
module.exports = {
  entry: [
    "FontAwesome-webpack!./path/to/font-awesome.config.js",
    "your-existing-entry-point"
  ]
};
```

#### `font-awesome.config.js`

Example:

``` javascript
module.exports = {
  styles: {
    "mixins": true,

    "core": true,
    "icons": true,

    "larger": true,
    "path": true,
  }
};
```

#### `font-awesome.config.scss`

Imported after Font-Awesome's default variables, but before anything else.

You may customize Font-Awesome here.

Example:

``` scss
$fa-inverse: #eee;
$fa-border-color: #ddd;
```

### extract-text-webpack-plugin

Configure style loader in `font-awesome.config.js`.

Example:

``` javascript
module.exports = {
  styleLoader: require('extract-text-webpack-plugin').extract('style-loader', 'css-loader!sass-loader'),
  styles: {
    ...
  }
};
```

Install `extract-text-webpack-plugin` before using this configuration.
