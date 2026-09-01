# NicoNavi web page:
https://tan-furukawa.github.io/niconavi/

# software:
https://github.com/Tan-Furukawa/niconavi_app

# tutorials:
- Tutorial 1: CPO Analysis with the GGG3 Dataset

# ローカルプレビュー (push 前の確認)

```bash
cd nicol_navi
npm run dev     # http://localhost:1313/ を開く
```

- `npm run dev` … 開発用サーバ。`--baseURL http://localhost:1313/` を渡すので、
  画像もローカルの `static/` から配信されます（本番サイトを見に行きません）。
  下書き (`draft = true`) と未来日付の記事も表示します。
- `npm run preview` … 公開時と同じ条件（下書き・未来日付を除外）で確認します。
- `npm run build` … 本番と同じ `--baseURL https://tan-furukawa.github.io/niconavi/` でビルド。
- `npm run build:local` … `public_local/` にローカル用ビルドを出力（`public/` を汚しません）。
- `npm run clean` … 生成物を削除します。

## 画像・動画の書き方

`baseURL` が `https://tan-furukawa.github.io/niconavi/` のため、`<img>` に本番 URL を
直接書くと、ローカルでは未公開の画像が 404 になります。代わりにショートコードを使います。

```
{{< img src="images/page/tutorial/tutorial1/pic1.png" alt="video タブ" width="45%" >}}
```

`src` は `static/` からの相対パスです。`width` は省略すると `100%` になります。
動画などの生 HTML では `{{< url "images/page/acquisition/pic3.mp4" >}}` を使います。
どちらも `relURL` を通すので、ローカルでは `/images/...`、本番では `/niconavi/images/...`
に展開されます。
