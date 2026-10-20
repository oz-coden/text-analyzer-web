# 文字数カウント

[ブラウザで使う](https://tools.oz-coden.com/text-analyzer/)

文字数・行数・段落数・文章数・句読点数・読了時間・原稿用紙枚数を入力に合わせて集計します。Escキーで入力をクリアできます。

## 実行方法

1. このリポジトリをクローンまたはダウンロードし、フォルダ構成を保ちます。
2. リポジトリのルートで `python -m http.server 8000` を実行します（Python 3が必要です）。
3. ブラウザで `http://localhost:8000/` を開きます。

実行時は静的なHTML・CSS・JavaScriptだけを使います。Node.jsやAPIサーバー、ビルド工程は不要です。入力内容の処理はブラウザ内で行います。

## 仕様

文字数はUnicodeコードポイント単位です。改行を含めず、空白を含む値と除く値を表示します。読了時間は500字/分、原稿用紙は20字×20行を目安とした概算です。

## 共通UI

`vendor/ui/` は [oz-coden.com-ui-web](https://github.com/oz-coden/oz-coden.com-ui-web) の配布用コピーです。利用するコミットとファイルハッシュは `shared-ui.json` に記録しています。個別のレイアウトは `style.css` で管理します。

共通UIを更新する場合は、共通UIリポジトリの `scripts/sync-ui.mjs` を使い、取り込んだファイルとメタデータをコミットしてください。配布用コピーを同梱しているため、実行時に共通UIリポジトリへアクセスする必要はありません。

## ソースの来歴

初期実装は [oz-coden.github.io](https://github.com/oz-coden/oz-coden.github.io) のコミット `dfc7c0a29396e2114d73e99dd17d494f7ab1c5ee` にあるツールを元にしています。このリポジトリで単独実行・変更できます。
