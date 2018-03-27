# makeのビルド

## 要件

- `git` (`choco install git`)
- `sed` (`choco install gnuwin32-sed.install`)
  - `build_w32.bat`で`sed`コマンドが使用されているため必須です。
- Visual Studio (Community 2017でテスト済み)
- Windows x64（Windows 10でテスト済み）

## ビルド

- x64 Native Tools Command Prompt for Visual Studioを起動
- コマンドプロンプトを起動し、`vcvarsall x64`を実行
- コマンドプロンプトを起動し、`vcinit x64`を実行（[vcinit](https://github.com/retorillo/vcinit))

上記いずれかの方法でコマンドプロンプトを起動し、以下のコマンドを実行してください。

```
git clone https://git.savannah.gnu.org/git/make.git
cd make
git reset --hard HEAD 4.2.1
build_w32.bat
```

`4.2.1`にリセットしていますが、必要に応じて最新のタグに書き換えてください。最新のタグは`git describe`で確認できます。
