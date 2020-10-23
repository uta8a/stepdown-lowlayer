#　ELFファイルを読む

- fileコマンドを打つと、以下のように表示されます

```
 file a.out 
a.out: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=0c3abc6e723c194f04a4efd55b6b6cbe3e53c421, for GNU/Linux 3.2.0, not stripped
```
- `ELF`と書いてあるのがわかるでしょうか？fileコマンドはELF形式のファイルだと判断しているようです。
- それでは、このELFについて見ていきます。
- 少しファイルがでかいので、小さいものを見ていきます。
- elf.cを見ていく
- (elfの仕様に沿ってヘッダを解説)
