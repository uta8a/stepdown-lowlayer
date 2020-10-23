# ELFを書く

- ここではトレーニングとして、ELFを手打ちで書いてもらいます。一度やっておくと「バイナリを手で打ち込めます」と言えるようになります。

## 書き方

- 基本的にはELFを読んだときと同じことをすればよいです。
- `man elf` とコマンドラインで打って `elf.h` を見たり、仕様書( https://refspecs.linuxfoundation.org/elf/gabi4+/contents.html )を読んでください。
- elfのヘッダーの一部がかけたら、readelfが認識してくれるようになるので、readelfが「これはELFファイルですね」と判定するくらいまでELFの手打ちにチャレンジしてみてください
- 確かめ方は以下の通りです。

```bash
$ readelf -h handmade # handmadeが自分で作ったファイルです
# ヘッダの一部を出力したらOK 完全なELFではないのでエラーが出るが気にしない
```
