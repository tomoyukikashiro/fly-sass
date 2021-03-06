# fly-sass [![][travis-badge]][travis-link] [![npm package][npm-ver-link]][npm-pkg-link]

> Compile SASS (via [node-sass](https://github.com/sass/node-sass)) with Fly

## Install

```
npm install --save-dev fly-sass
```

## Usage

The globs within `source()` should always point to individual files. 

#### Basic

```js
exports.styles = function * (fly) {
  yield fly.source('src/styles/style.scss').sass().target('dist')
}
```

#### Multiple Bundles

Simply create an array of individual file paths.

```js
exports.styles = function * (fly) {
  yield fly.source([
    'src/styles/client.scss',
    'src/styles/admin.scss'
  ]).sass().target('dist')
}
```

#### SASS vs SCSS

There is no need to set [`indentedSyntax`](https://github.com/sass/node-sass#indentedsyntax) -- the SASS parser will intelligently decipher if you are using the SASS syntax.

```js
exports.styles = function * (fly) {
  yield fly.source([
    'src/styles/client.sass', // SASS
    'src/styles/admin.scss' // SCSS
  ]).sass().target('dist')
}
```

#### Sourcemaps

You may create source maps for your bundles. Simply provide the desired file path as `outFile` or `sourceMap`.

> **Important:** It is _recommended_ that you provide `sourceMap` your desired path. However, if `sourceMap` is a `true`, you **must** then provide `outFile` your file path string.

```js
exports.styles = function * (fly) {
  yield fly.source('src/app.sass')
    .sass({sourceMap: 'dist/css/app.css.map'})
    .target('dist');
}

// OR

exports.styles = function * (fly) {
  yield fly.source('src/app.sass')
    .sass({sourceMap: true, outFile: 'dist/css/app.css.map'})
    .target('dist');
}
```

## API

### .sass(options)

This plugin does not have any custom options. Please visit [`node-sass` options](https://github.com/sass/node-sass#options) for a full list of available options.

> **Note:** You will _not_ be able to set the `file` or `data` options. These are done for you & cannot be changed.

## License

MIT © Fly

> A big thanks to [Tomoyuki Kashiro](http://tomoyukikashiro.me) for donating the plugin to Fly!

[npm-pkg-link]: https://www.npmjs.org/package/fly-sass
[npm-ver-link]: https://img.shields.io/npm/v/fly-sass.svg?style=flat-square
[travis-link]:  https://travis-ci.org/flyjs/fly-sass
[travis-badge]: http://img.shields.io/travis/flyjs/fly-sass.svg?style=flat-square
