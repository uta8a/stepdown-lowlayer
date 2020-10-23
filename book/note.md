# honkit 使い方
- https://honkit.netlify.app/setup.html
  - installをする
- ディレクトリ構造が大事っぽい
```
.git
book/
  README.md
  SUMMARY.md
  .bookignore
  chapter-1/
    README.md
docs/
  # index.html...
```
- こんな感じで、後はpackage.jsonにいい感じに書いてやると`npm run serve`だけでよくなる
- SUMMARYが左のTOCに対応するので、ここはその都度更新してやらないといけない
- step-1-1のようにナンバリングして、目次ではタイトルを表示させるようにすると、ディレクトリ構造の把握とUIが両立できそう