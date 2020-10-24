# バッファオーバーフローしてみる
- この章では、C言語で書かれたプログラムの脆弱性を通して、1章で見たメモリの構造のうち、スタックについての理解を深めます。

## 用語説明
- Pwn
  - セキュリティのコンテスト、CTFの分野のひとつ。バイナリに関わる脆弱性の問題が出題される。
- checksec
  - https://github.com/slimm609/checksec.sh
  - 実行ファイルの(主に)セキュリティ機構がどのような状態か調べるbash script
- pwntools
  - Pwnを行うときに使う便利なツール(Pythonライブラリ)

## 各セキュリティ機構
- おそらく `checksec` コマンドが使えるようになっていると思います。
- すこし遊んでみましょう。
```bash
$ checksec --file=./bof
$ checksec --file=/usr/bin/ls
$ checksec --kernel
```

<!-- TODO -->
<!-- http://sig.tsg.ne.jp/sig-ctf-2017/pwn/2017/05/26/Easy-Pwn.html -->
<!-- https://miso-24.hatenablog.com/entry/2019/10/16/021321 -->
## 主なセキュリティ機構の説明
- RELRO
  - RELocation Read Only
  - GOT領域を読み込みOnlyにする
    - GOT領域を書き換えると嬉しい
    - GOT領域とは？
      - 共有ライブラリ関数のアドレス一覧表。
      - ここを書き換えると任意関数へのアドレスに変更して任意関数を実行できる
- STACK CANARY
  - 関数内でスタックのオーバーフローを検知する
- NX
  - RIPが変なところに飛ばないようにする(text領域だけのはず)
- PIE
  - プログラムの配置をランダムにする -> text領域もランダムになる
  - `lea	rdi, .LC0[rip]` と関連している
  - https://qiita.com/0yoyoyo/items/85122f31ba8d14332e3d
- RPATH, RUNPATHはなにか？
  - https://security.stackexchange.com/questions/161799/why-does-checksec-sh-highlight-rpath-and-runpath-as-security-issues
- Symbols
- FORTIFY
- Fortified
- Fortifiable
- FILE
  - ファイルへのパス
- ASLR
  - OSの持つセキュリティ機構
  - スタックやヒープのアドレスをランダムにする

```
# ASLRをOFFにする
$ sudo sysctl -w kernel.randomize_va_space=0
# ASLRをONにする(演習が終わったら必ずONに戻してください)
$ sudo sysctl -w kernel.randomize_va_space=2
```

### セキュリティ機構 goとの違い

- goはコンパイラオプションをデフォルトにすると以下のようになる

```
$ checksec --file=main
RELRO           STACK CANARY      NX            PIE             RPATH      RUNPATH	Symbols		FORTIFY	Fortified	Fortifiable	FILE
No RELRO        No canary found   NX enabled    No PIE          No RPATH   No RUNPATH   2695 Symbols	  No	0		0		main
```

- RELRO, STACK CANARY, PIEがオフ
- これは、言語の方でメモリ周りの脆弱性が起こらないようにしているのでバイナリに保護機能はつけなくてよい、というgoの戦略に基づいたもの(goは脆弱！というわけではないことに注意)
- しかし、cgo(C言語を使えるgolang), unsafe(rawポインタ操作を許す構文)を使った上でコンパイラオプションをそのままにしていると...？

## pwntools
- おそらくPython3で `import pwn` が使えるようになっていると思います。
- pwntoolsは様々な機能がありますが、今回使うのは以下です。
- 使う機能
  - context 最初の設定
  - process プロセスを生成。実行ファイルを実行する
  - p64 アドレスをpayload向けに変換してくれる
  - sendline バイト列を送り込む
  - interactive 対話環境に入る。シェルをとったあとに使う。
- documentは https://pwntools.readthedocs.io/en/latest/index.html です。

## 簡単なバッファオーバーフローをやってみよう
```
ASLRオフ
gdbの使い方
RSPの書き換え
skip rbp https://qiita.com/ssssssssok1/items/b8ffca6b68149812c335
ret2esp http://www.intellilink.co.jp/article/column/ctf01.html
16byte align https://uchan.hateblo.jp/entry/2018/02/16/232029
```