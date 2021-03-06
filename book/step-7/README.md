# 低レイヤガイドブック
- 筆者がやったことあるもの、ないものも載せています。
- 僕の推しを載せています
- なにかこれいいぞ！という教材あったらどなたでもMatterMostに書き込んでください。
- 以下はminicamp環境に入っているツールです。 https://github.com/uta8a/minicamp-env でansibleで公開しています。

```
- ltrace
- strace
- vim
- gdb
- git
- file
- curl
- wget
- binutils
- libssl-dev
- build-essential
- netcat
- nasm
- python3
- python3-pip
- python3-dev
- ghex
- radare2
- docker.io
- checksec
- rp++
- Rust
- VSCode
- socat
- pwntools (pip3)
- gdb-peda
```

## OS
- blog_os
  - https://github.com/phil-opp/blog_os
  - (unsafeを使うけど)RustでOSを書く。完結はまだで現在もアップデートが頻繁に行われるが、Rust自体もアップデートされているのでそれに合わせてメンテされているのはよい。
  - legacy BIOSを使っているが、UEFIに変えるRoadmapもあり、rust-osdevで進行しているので今後に期待。

## エミュレータ
- Writing a RISC-V Emulator from Scratch in 10 Steps
  - https://book.rvemu.app/
  - 64bit RISC-V emulatorを作る
  - 初回の Setup and Implement Two Instructions は仕様書を読みながらコード書いていく流れなのでとてもよいなと思いました

## Security
- Exploitation Fundamentals
  - https://github.com/rung/training-exploit-fundamentals
  - goのセキュリティにも触れられている
  - Pwn形式で学べる

## 言語処理系
- 低レイヤを知りたい人のためのCコンパイラ作成入門
  - https://www.sigbus.info/compilerbook
  - 今回の講義を受けておそらくスタック構造に慣れたと思うので分割コンパイルとリンクの手前まではすぐに行けると思います
- Crafting Interpreters
  - https://craftinginterpreters.com/contents.html
  - 自作言語のインタプリタを作る教材。とても丁寧です。
  - ガベージコレクションも作るようです。

## LLVM
- 怖くないLLVM入門
  - https://qiita.com/Anko_9801/items/df4475fecbddd0d91ccc
  - 軽めの記事です
  - LLVMって何？という人はまずここから入るといいと思っています
- ミニキャン言語を作ろう
  - https://flattsecurity.hatenablog.com/entry/2019/10/28/103000
  - Yuka Ikarashiさんの2019年山梨ミニキャンプの講義
  - 公開されているので、取り組みながら自作言語を作ってLLVMについても学べます
  - 筆者が参加した最初のミニキャンプでとてもおもしろかったのでぜひ
- maekawatoshiki/cilk
  - https://github.com/maekawatoshiki/cilk
  - これは教材ではないのですが、LLVMのようなコンパイラ基盤を作っている人のリポジトリです(Rust製)
  - `docs-ja` や `cilkcc` (独自のLLVMのような基盤の上でCコンパイラのサブセットを書いている) を読んでみると面白いです
  - maekawatoshikiさんは ブラウザ([naglfar](https://github.com/maekawatoshiki/naglfar))やJavaScriptの処理系([rapidus](https://github.com/maekawatoshiki/rapidus))を開発されていたことがあり、「こんなでかいソフトウェアのサブセットって作れるんだ」という気持ちになるので一度見てみるとよいです
