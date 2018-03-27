# lessのビルド

## 要件

- `make` (v4.2.90でテスト済み）
- Visual Studio (Community 2017でテスト済み)
- Windows x64（Windows 10でテスト済み）

## ソースのダウンロード

[greenwoodsoftware.com](http://www.greenwoodsoftware.com/less/download.html)から最新のtarかzipをダウンロードし展開します。

あるいは`curl`、`7z`、`gpg`がそろっている場合は、コマンドでダウンロード・整合性の確認をすることも可能です。

- `curl` (`choco install curl`)
- `7z` (`choco install 7zip`)
- `gpg` (`choco install gnupg-modern`)

```batch
curl -o less.tar.gz http://www.greenwoodsoftware.com/less/less-530.tar.gz
curl -o less.sig http://www.greenwoodsoftware.com/less/less-530.sig
gpg --keyserver pgp.mit.edu --recv-key 33235259
gpg --verify less.sig less.tar.gz
7z x less.tar.gz
7z x less.tar
```

## Makefile.wnuの変更

`X86`ではなく`I386`になっていることからも、おそらくMakefileがかなり古いままになっているようで現行の環境でビルドするには一部変更が必要でした。

### .SUFFIXES

`.c.obj::`の箇所に`.SUFFIXES: .c .obj`を追加して以下のようにしてください。

```Makefile
.SUFFIXES: .c .obj

.c.obj::
	$(CC) $(CFLAGS) $<
```

### less.exe

ターゲット`less.exe`の`$**`を`$^`に変更します。

```Makefile
less.exe: $(OBJ)
	$(LD) $(LDFLAGS) $^ $(LIBS) /out:$@
# $(LD) $(LDFLAGS) $** $(LIBS) /out:$@
```

### LDFLAGS

`LDFLAGS`の`I386`を`X64`に変更します。

```Makefile
# LDFLAGS = /nologo /subsystem:console /incremental:no /machine:I386
LDFLAGS = /nologo /subsystem:console /incremental:no /machine:X64
```

## ビルド

- x64 Native Tools Command Prompt for Visual Studioを起動
- コマンドプロンプトを起動し、`vcvarsall x64`を実行
- コマンドプロンプトを起動し、`vcinit x64`を実行（[vcinit](https://github.com/retorillo/vcinit))

上記いずれかの方法でコマンドプロンプトを起動し、以下のコマンドを実行してください。

```Makefile
make -f Makefile.wnu 
```
