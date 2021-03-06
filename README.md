# Webpack Builder π¦
`babel`, `webpack`λ‘ λΉλνκ²½ κ΅¬μ±

## 1. λ²λ€ μ§μ νμ πΎ
- `.js`
- `.css` `.scss` `.sass`
- `.jpeg` `.jpg` `.png` `.gif` `.bmp` `.svg`


## 2. κ°λ° νκ²½ μ€μ  βοΈ 

### webpack-dev-server
- `npm install webpack-dev-server --save-dev`
- `npm run build` 
- `npm start`

>[dev-server options](https://webpack.js.org/configuration/dev-server/)
```javascript
// webpack.dev.js
	devServer: {
		static: {
			directory: path.join(__dirname, 'dist'),
		},
		compress: true,
		port: 9000,
		historyApiFallback: true,
	},
```

### webpack-dev-middleware
- `npm install --save-dev express webpack-dev-middleware
`
```javascript
const express = require('express');
const webpack = require('webpack');
const webpackDevMiddleware = require('webpack-dev-middleware');

const app = express();
const config = require('./webpack.config.js');
const compiler = webpack(config);

// κΈ°λ³Έ μ€μ  νμΌ
app.use(
  webpackDevMiddleware(compiler, {
    publicPath: config.output.publicPath,
  })
);

// ν¬νΈ 3000μμ νμΌ μ κ³΅
app.listen(3000, function () {
  console.log('Example app listening on port 3000!\n');
});
```

```javascript
// webpack.common.js
...
output: {
	...
	publicPath: '/',  // http://localhost:3000 μ μ
	...	
},
```

## μμ  μ¬ν­
- CSSμ `background-image: url('')` μμ μ΄λ―Έμ§κ° μ λλ‘ μΆλ ₯λμ§ μμ.
- μ΄λ―Έμ§λ ν°νΈκ°μ μμλ€μ μΉν©μ λ΄μ₯λμ΄μλ λ‘λλ₯Ό μ¬μ©νλλ‘ μμ 
> [Webpack 5 - Asset Modules](https://webpack.js.org/guides/asset-modules/)
```javascript
module: {
	rules: [
		...
		{
			test: /\.(jpe?g|png|gif|bmp|svg)$/,
			type: 'asset/resource',
			exclude: /node_modules/,
		},
		{
			test: /\.(woff|woff2|eot|ttf|otf)$/i,
			type: 'asset/resource',
			exclude: /node_modules/,
		},
	],
},

```