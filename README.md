# Darts Scorer を GitHub Pages で公開する手順

このフォルダには、ビルド不要でそのまま公開できる静的サイト一式が入っています。

- `index.html` … ページ本体（React・Babel・Tailwindを全てCDNから読み込みます）
- `app.jsx` … アプリ本体のコード

## 手順（GitHubのWeb画面だけでOK）

1. https://github.com にログインし、右上の「+」→「New repository」で新しいリポジトリを作成します。
   - 例：リポジトリ名 `darts-scorer`
   - Public を選択（GitHub Pagesの無料利用にはPublicが簡単です）
2. 作成したリポジトリのページで「Add file」→「Upload files」を選び、この `index.html` と `app.jsx` の2つをドラッグ＆ドロップしてアップロードし、「Commit changes」します。
3. リポジトリの「Settings」タブ →左メニューの「Pages」を開きます。
4. 「Build and deployment」の「Source」で **Deploy from a branch** を選択。
5. 「Branch」で `main`（または `master`）、フォルダは `/ (root)` を選んで「Save」。
6. 数十秒〜数分待つと、ページ上部に公開URLが表示されます。
   - 通常は `https://（あなたのユーザー名）.github.io/darts-scorer/` になります。

これだけで公開完了です。ビルドやコマンド操作は不要です。

## gitコマンドを使う場合

```bash
git init
git add index.html app.jsx
git commit -m "Add darts scorer"
git branch -M main
git remote add origin https://github.com/（ユーザー名）/darts-scorer.git
git push -u origin main
```

その後は上記の手順3〜5と同じくSettings→Pagesで公開設定をしてください。

## 補足

- データ保存について：アプリ内の「履歴」は、Claude上で動かしていたときの特別なストレージAPIの代わりに、**ブラウザのlocalStorage**を使うように調整済みです。同じブラウザ・同じ端末でアクセスした場合のみ履歴が残ります（他の端末とは共有されません）。
- `index.html` をパソコン上で直接ダブルクリックして開くと、`app.jsx` の読み込みがブラウザのセキュリティ制限（CORS）で失敗することがあります。動作確認はGitHub Pagesに公開した後、またはローカルサーバー（例：`python3 -m http.server` をこのフォルダで実行し `http://localhost:8000` を開く）経由で行ってください。
- 独自ドメインを使いたい場合は、Pages設定内の「Custom domain」から設定できます。
