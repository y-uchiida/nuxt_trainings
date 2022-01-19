# axios-module
Nuxt.js 用にカスタマイズされたaxios モジュールが公式から提供されている

## インストールコマンド
以下のコマンドでインストールする
```
$ yarn add @nuxtjs/axios
```

## 設定ファイルの編集
`nuxt.config.js` から、axios をインポートする

```JavaScript
/* 以下の記述を追加する */

  modules: [
    '@nuxtjs/axios', /* import axios module */
  ],
  axios: {},
```

## axios モジュールの利用
`this.$axios` にaxiosのオブジェクトが格納される  
各種メソッドも、`$` のプレフィックスを付けて利用できる  
`this.$axios.$get('https://~~~')` のようにして、APIにアクセスできる

## token(API キー) を利用する
アクセスのたびに手動でAPI キーを追加するのは手間なので、  
axios-module のリクエストをフックして、リクエスト前にトークンを追加する  
```JavaScript
/* plugins/axios.js */
export default function({$axios}) {
  $axios.onRequest( (config) => {
    console.log(config)
    if (process.env.QIITA_TOKEN) {
      config.headers.common['Authorization'] = process.env.QIITA_TOKEN
    }
    return config
  })
}
```

次に、作成したプラグインを`nuxt.config.js` でインポートする  
```JavaScript
/* nuxt.config.js */
plugins: [
  '~/plugins/axios.js'
],
env: {
  config.headers.common['Authorization'] = 'Bearer ' + process.env.QIITA_TOKEN
},
```
