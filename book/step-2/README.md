# アセンブリを書く
- この章では、アセンブリの読み書きの「書き」パートを通して慣れていきましょう。比較的簡単な問題が多いので、終わった人は自由にアセンブリを書いて、MatterMostに「こんなことできたよ！」と報告してくれると嬉しいです。

## 単純な足し算
- `~/minicamp-files/step-1-1/main.s` の空欄を埋めて足し算をしてください。
- 以下のようにして確かめることができます
```bash
$ gcc main.s -o main # mainという名前の実行ファイル生成
$ ./main # ここでeaxに最後に入っている値がステータスコードとしてreturnされる
$ echo $? # eaxに入っている値を確認
```

## RPN電卓

- 解答の例 https://github.com/uta8a/code-playground/blob/master/rpn/src/x86_64.c
