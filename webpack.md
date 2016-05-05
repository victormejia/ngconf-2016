## Core Concepts: entry

(http://thelarkinn.github.io/angular2-webpack-lite/)[http://thelarkinn.github.io/angular2-webpack-lite/]

Tells webpack what files to load

```javascript
module.exports = {
  entry: './browser/main.ts'
}

// or

module.exports = {
  entry: [...]
}
```

## Core Concepts: Output

```javascript
module.exports = {
  entry: 'main.js',
  output: {
    path: './dist',
    filename: '/bundle.js'
  }
}
```

## Core Concepts: Loaders

tells webpack how to interpret files, and transforms them

```javascript
module: {
  loaders: [
    {test: /\.ts$/, loader: 'ts', include: 'regex', exclude: 'regex'}
  ]
}
```


## Core Concepts: Plugins
an ES5 class, apply functionality at the compilation level

## Webpack 2
  * native es2015 module support
  * tree shaking
  * faster compilation
  * optimizations
