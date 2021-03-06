# アセンブリを書く

- この章では、アセンブリの読み書きの「書き」パートを通して慣れていきましょう。比較的簡単なので、終わった人は自由にアセンブリを書いて、Mattermostに「こんなことできたよ！」と報告してくれると嬉しいです。

## 単純な足し算

- `~/minicamp-files/step-1-1/main.s` の空欄を埋めて足し算をしてください。
- 以下のようにして確かめることができます

```bash
$ gcc main.s -o main # mainという名前の実行ファイル生成
$ ./main # ここでeaxに最後に入っている値がステータスコードとしてreturnされる
$ echo $? # eaxに入っている値を確認
```

- `echo $?` で最後に実行したプログラムの終了ステータスコードを得られるのでそれを使っています。

## RPN電卓

- 四則演算とスタック構造に慣れてもらいたいので電卓を作ってもらいます
- 大部分作ってあるので、アセンブリ出力部分を作ってください
- (逆ポーランド記法は以下のように演算子を後ろに置くような表記の仕方を言います。スタックと相性がよいです)

```bash
1 1 + # -> 2
1 2 + 3 4 - + # -> 3 -1 + -> 2
```

- `~/minicamp-files/step-1-2/rpncalc.c` の空欄を埋めて逆ポーランド記法での引き算、掛け算、割り算を入力したときにそれに対応するアセンブリを出力してください

```bash
$ gcc rpncalc.c -o rpncalc
$ ./rpncalc
1 2 + 3 4 + +
# ここでCtrl+dすると計算結果が出てくる
.intel_syntax noprefix
.globl main
main:
  push 1
  ...
  ret
[10] # <- これはstderrに出る

$ ./rpncalc > rpn.s
1 2 + 3 4 + +
# Ctrl+d
[10]
$ cat rpn.s
# アセンブリが生成されている
$ gcc rpn.s
$ ./rpn
$ echo $? # 値が確認できる
```

- 解答の例 https://github.com/uta8a/code-playground/blob/master/rpn/src/x86_64.c
  - 割り算が少しむずかしいかもしれません。
  - 仕様書が大事！とはいえ、仕様書だけではどう進めばいいかわからなくなることがあります。そのときは、実際に書いてコンパイルした結果を眺めてみると手がかりがつかめるかもしれません。仕様書を眺める、手を動かして実物を調べる、この2点が分かればOKです。(このへんが、実機が大事と言われる理由なのかなと思っています。)

## 終わったら...？

- いろいろ書いてみることが大事なので、アセンブリをいろいろ書いてみてください。こんなことできました！みたいなのをMattermostで報告してみてください。
- 例
  - RPN電卓に新しい演算子(xorとか)を導入してみる
  - writeシステムコールを呼び出して、値を出力できないか考えてみる
