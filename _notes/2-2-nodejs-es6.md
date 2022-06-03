

install dev 
```
  npm i --save-dev @babel/core @babel/node @babel/preset-env @babel/plugin-transform-runtime

  npm i @babel/runtime
```

.babelrc
```
{
    "presets": [
        "@babel/preset-env"
    ],
    "plugins": [
        [
            "@babel/plugin-transform-runtime",
            { "regenerator": true }
        ]
    ]
}
```