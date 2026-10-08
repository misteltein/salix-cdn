# salix-cdn

`salix` のチェックアウト用ブラウザ成果物だけを配信する公開リポジトリです。

このリポジトリには、次のビルド済みファイルだけを置きます。

- `salix.js`
- `salix-fonts.js`
- `LICENSE-NOTO.txt`

`salix-fonts.js` には Noto Sans JP と Noto Serif JP が埋め込まれています。両フォントは SIL Open Font License 1.1 で提供されているため、著作権表示とライセンス本文を含む `LICENSE-NOTO.txt` を必ず同梱します。ソースコード、Google Apps Script、設定用の認証情報、開発用ファイルは含めません。

## 配信

futureshopの注文手続き画面では、ショップ配下の外部scriptがWebスキミング対策で削除されます。そのため、タグで固定したjsDelivr URLを使用します。

```html
<script src="https://cdn.jsdelivr.net/gh/misteltein/salix-cdn@v1.0.0/salix-fonts.js" integrity="sha384-DJRv3I/1FCpiA88jA2cyEcaCj8o1u6zhxQb/9e0ba3LtkKwbVFyzhkNdbcq8skK2" crossorigin="anonymous" data-salix-pdf-fonts></script>
<script src="https://cdn.jsdelivr.net/gh/misteltein/salix-cdn@v1.0.0/salix.js" integrity="sha384-igoQ4Dwuvo5Y2KGSWJ9MOtU2Lr/zG7PCyyId43vIwPuzsqlDJ9ecpToOEPkBpAK0" crossorigin="anonymous" data-salix-mode="checkout"></script>
```

`@main` は使わず、リリースタグまたはコミットSHAで固定してください。

## 更新手順

1. 非公開の `salix` リポジトリで `npm run build` を実行する。
2. `dist/salix.js`、`dist/salix-fonts.js`、`dist/LICENSE-NOTO.txt` だけをこのリポジトリのルートへコピーする。
3. 内容を確認してコミットし、新しいタグを作成してpushする。
4. 非公開リポジトリの `scripts/build.mjs` にあるCDNタグを新しいタグへ更新して再ビルドし、生成された `dist/checkout-embed.html` をfutureshopへ登録する。
