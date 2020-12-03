会社で使う用
OS: Windows 10

USBメモリ等に入れてどこでも使えるVSCodeとJS開発環境を用意する方法
インストール不要
Windowsの場合、VSCode等のアップデートは手動

参考リンク
https://code.visualstudio.com/docs/editor/portable

# 必要なソフトをダウンロード

インストーラでなく圧縮形式のやつ
  - [VSCode](https://code.visualstudio.com/download) zip 64bit
  - [Git](https://git-scm.com/download/win) 64-bit Git for Windows Portable
  - [Node.js](https://nodejs.org/ja/download/) Windows Binary (.zip) 64bit

VSCodeとNode.jsは.zip
Gitだけ自己解凍形式の.exe

# VSCodeをポータブルモードにする
VSCodeのフォルダに「data」を作成するだけ
設定がすべてそこに保存されるようになる

# VSCodeのsettings.jsonをいじる

```js
{
    "terminal.integrated.env.windows": {
        "PATH": "${workspaceRoot}\\node_modules\\.bin;${execPath}\\..\\..\\node;${env:PATH}",
    },
    "terminal.integrated.shell.windows": "${execPath}\\..\\..\\git\\bin\\bash.exe",

    //ここだけVSCodeの定数を使えないので、フォルダを移動した際は手動で変更しなければいけない
    "git.path": "C:\\Users\\inarb\\Desktop\\dev\\apps\\git\\bin\\git.exe", 
}
```

フォルダ名は適宜変える
シェルはGitについでに入ってるbashにする (Next.jsのチュートリアルでWindowsの場合はそう推奨されてる) ほんとはWSLとか使いたい

# Gitの設定

```
git config --system user.name "xxx"
git config --system user.email "xxx@xxx.xxx"
```

普通は`--global`だけど`--system`にすると`/etc/gitconfig`に保存される
git bashの場合、etcはGitがあるフォルダ直下にあるので、フォルダまるごと移動できる

おわり

# 参考
https://code.visualstudio.com/docs/editor/portable
https://code.visualstudio.com/docs/editor/variables-reference
https://medium.com/@arimgibson/supercharged-portable-vscode-with-git-and-node-js-34afad8f661b
https://www.atmarkit.co.jp/ait/articles/1807/20/news023.html