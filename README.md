# Vite Ejs Template

## Node バージョン
`v18` or `v18` 以上

## コマンド

- `npm run dev` 開発モードが立ち上がる
  - ブラウザが自動的に開きます。手動で下記のURLを叩いても表示されます。  
    `http://localhost:5173/pages/index.html`
- `npm run build` - ビルドモード
- `npm run preview` - ビルドされたサイトを確認できます
  - ブラウザが自動的に開きます。手動で下記のURLを叩いても表示されます。  
    `http://localhost:4173/`

## ディレクトリ構造
  - assets
    - images
    - scss
    - js  
  - dist  # ビルドされたファイル 
  - json
  - layout  # ejs テンプレート
  - pages # 各ページ
  - public  # コンパイルを通さないアセットファイル（`dist`のルートに配置されます）
  - main.js  # エントリーポイント
  - vite.config.js  # 設定ファイル

## アセット名にハッシュがいらない場合

`vite.config.js`のoutputの設定にある`[name]-[hash]`の`-[hash]`を削除します。

```js
export default defineConfig({
  ...
  build: {
    rollupOptions: {
      output: {
        assetFileNames: (assetInfo) => {
          let extType = assetInfo.name.split('.').at(1);
          if (/png|jpe?g|svg|gif|tiff|bmp|ico/i.test(extType)) {
            extType = 'img';
          }
          return `assets/${extType}/[name][extname]`;
        },
        entryFileNames: `assets/js/[name].js`,
        chunkFileNames: `assets/js/[name].js`,
      }
    }
  }
})
```