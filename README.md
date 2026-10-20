# Text Analyzer

日本語の説明は[目次](#目次)から読めます。

## Table of Contents

1. [Summary](#summary)
2. [Background of Development](#background-of-development)
3. [Features](#features)
4. [Requirements, Dependencies](#requirements-dependencies)
5. [Installation](#installation)
6. [LICENSE](#license)
7. [CREDIT](#credit)

## Summary

A browser-based text counter that updates character, line, paragraph and sentence counts as you type. It also estimates reading time and the number of Japanese manuscript pages.

[Playground Is Here!](https://tools.oz-coden.com/text-analyzer/)

## Background of Development

The aim is to check the size and basic structure of a piece of writing in one place, using transparent counting rules and simple estimates.

## Features

- Live counts  
  Update character, line, paragraph, sentence and punctuation counts as the input changes.
- Character counts with and without whitespace  
  Count Unicode code points, excluding newlines in both totals. Supplementary characters such as `😀` count as one; combining marks and multi-code-point emoji are counted separately.
- Reading time estimate  
  Estimate reading time at 500 non-whitespace characters per minute, rounded up to whole seconds.
- Manuscript page estimate  
  Estimate 20-column, 20-line manuscript pages while accounting for input line breaks.
- Keyboard clearing and shared themes  
  Press Esc in the text area to clear it, and switch between the common light and dark themes.

## Requirements, Dependencies

- A current web browser with JavaScript enabled.

The user interface is in Japanese. Shared UI assets are included in this repository. Python 3 is only needed for the example local server command below; an equivalent static HTTP server can also be used.

## Installation

1. Clone or download this repository, keeping the directory structure intact.
2. Start a static HTTP server from the repository root. For example, with Python 3:

   ```sh
   python -m http.server 8000
   ```

3. Open `http://localhost:8000/` in your browser.

The application files are at the repository root. Running the application requires only static HTML, CSS and JavaScript; no Node.js runtime, API server or build step is required.

Text analysis runs entirely in the browser. The application does not upload the input text or save it for restoration after reloading.

### Usage

1. Type or paste text into **解析するテキスト**.
2. Read the counters below the input. They update automatically.
3. Press Esc while the text area is focused to clear the input and reset the counters.

The counters use the following rules:

- **Characters:** the total with whitespace excludes newline characters; the total without whitespace removes JavaScript `\s` whitespace, including spaces, tabs and newlines.
- **Lines:** split the input at newlines, including empty lines and a final empty line after a trailing newline.
- **Paragraphs:** count nonempty parts separated by one or more newlines.
- **Sentences:** count nonempty parts separated by `。` or `.`; this is delimiter-based counting, not natural-language sentence analysis.
- **Punctuation:** count `、`, `。`, `，`, `．`, `,` and `.`.
- **Manuscript pages:** wrap each input line at 20 code points, count each empty line as one line, then round the total up to 20-line pages. Japanese typesetting rules are not applied.

An empty input sets all counts to zero. Reading time and manuscript pages are estimates.

### Development and publication

Application-specific behavior and layout are in `script.js` and `style.css`. Shared styles, navigation and themes are bundled in `vendor/ui/` from [oz-coden.com-ui-web](https://github.com/oz-coden/oz-coden.com-ui-web). The source commit and file hashes are recorded in `shared-ui.json`, so the application does not fetch the shared UI repository at runtime.

To update the bundled UI, clone the shared UI repository alongside this repository. From this application's root, run `node ../oz-coden.com-ui-web/scripts/sync-ui.mjs . COMMIT_SHA`, replacing `COMMIT_SHA` with the full 40-character commit SHA to use. Commit the updated `vendor/ui/` files and `shared-ui.json`. This maintenance command requires Node.js 22 or later and an internet connection.

This repository checks JavaScript syntax on push and pull requests. With Node.js 22 or later, run the same checks locally:

```sh
node --check script.js
node --check vendor/ui/ui.js
```

The hosted application is assembled and published through [tools.oz-coden.com](https://github.com/oz-coden/tools.oz-coden.com). Its publication workflow applies the shared UI to all tools and runs browser integration checks. See that repository for deployment instructions.

## LICENSE

This project is released under the [MIT License](LICENSE).

## CREDIT

Shared styles, navigation and themes: [oz-coden.com-ui-web](https://github.com/oz-coden/oz-coden.com-ui-web).

---

# 文字数カウント

## 目次

1. [概要](#概要)
2. [開発背景](#開発背景)
3. [機能](#機能)
4. [前提・依存](#前提依存)
5. [導入方法](#導入方法)
6. [ライセンス](#ライセンス)
7. [クレジット](#クレジット)

## 概要

入力に合わせて文字数・行数・段落数・文章数などを集計するブラウザ用ツールです。読了時間や原稿用紙の枚数の目安も表示します。

[Playgroundはこちら！](https://tools.oz-coden.com/text-analyzer/)

## 開発背景

文章の分量や基本的な構成をひとつの画面で確認し、計数ルールを把握したうえで、読了時間や原稿用紙の枚数の目安を利用できることを目的としています。

## 機能

- 入力に合わせた集計  
  文字数・行数・段落数・文章数・句読点数を、入力の変更に合わせて更新します。
- 空白を含む文字数と除く文字数  
  どちらも改行を除き、Unicodeコードポイント単位で数えます。`😀`のような補助文字は1文字ですが、結合文字や複数コードポイントで構成される絵文字は、それぞれのコードポイントを数えます。
- 読了時間の目安  
  空白を除いた文字数を1分500字として計算し、秒単位で切り上げます。
- 原稿用紙の枚数の目安  
  入力の改行を考慮し、20字×20行の原稿用紙の枚数を概算します。
- キーボードでの消去と共通テーマ  
  入力欄でEscを押すと消去できます。共通のライト・ダークテーマも利用できます。

## 前提・依存

- JavaScriptが有効な最新のWebブラウザ。

画面の言語は日本語です。共通UIのファイルはこのリポジトリに同梱しています。Python 3は下記のローカルサーバーのコマンドを使う場合に必要で、同等の静的HTTPサーバーでも実行できます。

## 導入方法

1. このリポジトリをクローンまたはダウンロードし、フォルダ構成を保ちます。
2. リポジトリのルートで静的HTTPサーバーを起動します。Python 3を利用する場合は、次のコマンドを実行します。

   ```sh
   python -m http.server 8000
   ```

3. ブラウザで`http://localhost:8000/`を開きます。

アプリ本体はリポジトリのルートにあります。実行には静的なHTML・CSS・JavaScriptだけを使い、Node.jsの実行環境・APIサーバー・ビルド工程は不要です。

文章の集計はブラウザ内で行います。入力した文章をアップロードしたり、再読み込み後に復元するために保存したりする処理はありません。

### 使い方

1. **解析するテキスト**に文章を入力または貼り付けます。
2. 入力欄の下にある集計結果を確認します。結果は自動で更新されます。
3. 入力欄にフォーカスがある状態でEscを押すと、入力と集計結果をクリアします。

集計には、次のルールを使います。

- **文字数：** 空白を含む値は改行を除きます。空白を除く値は、スペース・タブ・改行など、JavaScriptの`\s`に該当する文字を除きます。
- **行数：** 改行で区切り、空行や末尾の改行の後の空行も数えます。
- **段落数：** 1つ以上の改行で区切られた、空でない部分を数えます。
- **文章数：** `。`または`.`で区切られた、空でない部分を数えます。区切り文字に基づく集計で、自然言語としての文の解析は行いません。
- **句読点数：** `、`・`。`・`，`・`．`・`,`・`.`を数えます。
- **原稿用紙：** 入力の各行を20コードポイントで折り返し、空行は1行として数え、合計を20行単位で切り上げます。禁則処理などの日本語の組版規則は適用しません。

入力が空の場合は、すべての値を0にします。読了時間と原稿用紙の枚数は目安です。

### 開発と公開

アプリ固有の処理は`script.js`、レイアウトは`style.css`で管理します。共通のスタイル・ナビゲーション・テーマ切り替えは、[oz-coden.com-ui-web](https://github.com/oz-coden/oz-coden.com-ui-web)から`vendor/ui/`へ同梱しています。取得元のコミットとファイルハッシュは`shared-ui.json`に記録しており、実行時に共通UIリポジトリへアクセスする必要はありません。

同梱の共通UIを更新するには、このリポジトリと同じ親フォルダに共通UIリポジトリをクローンします。このアプリのルートで`node ../oz-coden.com-ui-web/scripts/sync-ui.mjs . COMMIT_SHA`を実行し、`COMMIT_SHA`を取り込む版の40桁のコミットSHAに置き換えてください。更新された`vendor/ui/`のファイルと`shared-ui.json`をコミットします。この保守用コマンドには、Node.js 22以降とインターネット接続が必要です。

このリポジトリでは、pushとプルリクエスト時にJavaScriptの構文を検査します。Node.js 22以降を利用すると、同じ検査をローカルでも実行できます。

```sh
node --check script.js
node --check vendor/ui/ui.js
```

公開用のアプリは、[tools.oz-coden.com](https://github.com/oz-coden/tools.oz-coden.com)で組み立てて配信します。公開処理では、全ツールに共通UIを適用し、ブラウザでの統合検査を行います。公開手順は同リポジトリを参照してください。

## ライセンス

This project is released under the [MIT License](LICENSE).

## クレジット

共通のスタイル・ナビゲーション・テーマ：[oz-coden.com-ui-web](https://github.com/oz-coden/oz-coden.com-ui-web)。
