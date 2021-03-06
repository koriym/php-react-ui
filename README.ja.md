# php-reactjs-ui

[English](README.md)

**php-reactjs-ui**はPHPプロジェクトとReactJS UIを統合するためのアプリケーションフレームワークアグノスティックなボイラープレートです。

 * [React](https://facebook.github.io/react/) UI framework
 * [Gulp](http://gulpjs.com/) Build system
 * [Webpack](https://webpack.github.io/) Moudle bundler
 * [Babel](https://babeljs.io/) JS transpiler
 * [Karma](https://karma-runner.github.io/0.13/index.html) Test Runner
 * [Mocha](http://mochajs.org/) Test framework
 * [Chai](http://chaijs.com/) BDD / TDD assertion framework 
 * [Enzyme](https://github.com/airbnb/enzyme) JavaScript Testing utilities for React
 * [Eslint](http://eslint.org/) Linting utility for JS and JSX
 * [Phantomjs](http://phantomjs.org/) Scriptable Headless WebKit
 * [react-php-v8js](https://github.com/reactjs/react-php-v8js) PHP library that renders React components on the server

 
## 前提条件

 * [Node](https://nodejs.org/en/)
 * [V8Js PHP extension](https://github.com/phpv8/v8js)  (オプション)
 
## インストール

このパッケージをダウンロードまたはクローンして、`ui`フォルダと`package.json`をPHPプロジェクトのルートに設置します。

```
git clone https://github.com/koriym/php-reactjs-ui.git
cp -r php-reactjs-ui/ui /path/to/yourapp
cp php-reactjs-ui/package.json /path/to/yourapp
```

次にモジュールをインストールします。

```
cd /path/to/yourapp
npm install
```

ReactでSSR（サーバーサイドレンダリング）をする場合は`react-php-v8js`をインストールします。
[V8Js PHP extension](https://github.com/phpv8/v8js)が必要です。

```
composer require reactjs/react-php-v8js
```
 
### ディレクトリ構造
 
```
├── src                  # php
├── tests                # php
├── composer.json
├── package.json          # JS
├── node_modules          # JS
├── ui
│   ├── .babelrc
│   ├── .eslintrc
│   ├── .babelrc
│   ├── .babelrc
│   ├── entry.js
│   ├── gulpfile.js
│   ├── karma.conf.js
│   ├── src               # JS
│   ├── test              # JS
│   ├── ui.config.js
│   └── webpack.config.js
└── vendor
```

既存のPHPプロジェクトへの追加が容易です。

## 設定

`ui/ui.js`と`ui/entry.js`で設定します。

`ui/ui.js` アプリケーション

```javascript
module.exports = {
  // project root directory
  projectDir: projectDir,
  // web root directory
  publicDir: projectDir + 'var/www',
  // webpack.outout.publicPath
  publicPath: '/build/',
  // watch directory for browsersync
  watchDir: [
    projectDir + 'src/**/*.php',
    projectDir + 'var/www/*.php',             // add more dirs
  ],
  // cleared directory in each run
  clearDir: [
    projectDir + 'var/tmp/*',                 // add more dirs
  ],
};
```

`ui/entry.js`

```javascript
module.exports = {
  react: 'src/react.js',
  helloworld: [
    'webpack-hot-middleware/client',
    'src/testing_examples/helloworld.jsx',
  ],
  ssr: [
    'webpack-hot-middleware/client',
    'src/testing_examples/ssr.js',
  ]
};
```

## 起動

http://127.0.0.0:8080/ で起動します。

```
npm start
```

## Browsersync + HMR

PHPやJS、Twigのテンプレートファイル等が更新された時にブラウザを自動で再読みます。

```
npm run dev
```
込みさせるためには`start-hot`コマンドで使用します。


## テスト

```
npm test      
```

JSのテストを`Karma`+`Mocha`+`Chai`で実行監視します。`karma.conf.js`で設定します。

## リント

```
npm run lint
```

[Eslint](http://eslint.org/)を実行します。ルールは[Airbnb](http://mitsuruog.github.io/javascript-style-guide/)です。変更するには`.eslintrc`を編集します。

## PHP QA

[phpcs](https://github.com/squizlabs/PHP_CodeSniffer)と[phpmd](https://phpmd.org/)の監視を行います。

```
npm run phpqa
```

注意）監視を行う`test`や`php`は別のターミナルで開いておくといいでしょう。

## デモ

```
git clone https://github.com/koriym/php-reactjs-ui.git
cd php-reactjs-ui
npm install
composer install # optional for SSR
npm run lint
npm test
[^C]
npm start
```

 * `http://127.0.0.1/`        client side rendering (CSR)
 * `http://127.0.0.1/ssr.php` server side rendering (SSR)

