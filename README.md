# 物工卒論
物理工学科卒論を書くためのlatex関連のファイルをまとめています。

# ファイル構成
- main : メインのlatexファイル
- lst.sty : 読み込むスタイルファイル一覧を書き込んだstyファイル（個人的な設定も多い）
- number_section.tex : 分割コンパイルのためのファイルたち
- fig : figureを入れる場所
- bib : bibliography用のbibtexファイル置き場

というかんじです。

# 使い方
基本的には章ごとに number_section.tex をはやして使う感じが良いと思います。その際、ファイル冒頭に `% !TEX root = main.tex` とかく事によって、子ファイルでコンパイルを通したときに親ファイルからコンパイルしてくれるようになります。
また、完全に僕の好みで余計なスタイルファイルも多数読み込んでいるので、必要に応じて削ってください。必要ないコマンドも多分結構定義されています。
あと、「physics」パッケージと「siunitx」パッケージが `\qty` で競合して居るのでエラーが出ますが、「physics」をあとに読み込んでいるので数式内で普通に `\qtu` が使えます。単位を表示したいときには `\si` を使ってください。

# Overleaf などで使う人向け
コンパイルをuplatexで行うように指定していることに注意してください。もともとローカルで動作させることを前提にしているので、エラーを吐くかもしれないですがggってなんとかしましょう。
Overleafなどに対して使用する場合は、このリポジトリ内にある.zipファイルをダウンロードして解凍、それをアップロードして使用してください。

# VScode を使う人向け
まずはlatexを導入しましょう。[この記事](https://zenn.dev/e_chan1007/articles/8029f3f9dff2be)が参考になるかと思います。導入したら、そのままではエラーを吐くので、以下のようにsettings.jsonのlatex-workshopのところを書き直してください。
```
// Latex 関連
  "[latex]": {
    "editor.wordWrap": "on",
    "editor.wordSeparators": "./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}`~?。．、，（）「」『』［］｛｝《》てにをはがのともへでや ",
    "editor.tabSize": 2,
    "editor.insertSpaces": true,
    "editor.detectIndentation": false,
    "editor.suggestSelection": "recentlyUsedByPrefix",
    "editor.suggest.snippetsPreventQuickSuggestions": false,
    "editor.quickSuggestions": {
      "other": true,
      "comments": false,
      "strings": false
    },
    "editor.bracketPairColorization.enabled": true,
    "editor.unicodeHighlight.invisibleCharacters": true,
    "editor.unicodeHighlight.allowedCharacters": {
      "，": true,
      "．": true,
      "！": true,
      "？": true,
      "［": true,
      "］": true,
      "｛": true,
      "｝": true,
      "＜": true,
      "＞": true,
    },
    "editor.stickyScroll.enabled": true,
  },
    "latex-workshop.latex.recipe.default": "with biber",
    "latex-workshop.latex.clean.enabled": true,
    "latex-workshop.latex.clean.fileTypes": [
  "*.aux",
  "*.bbl",
  "*.blg",
  "*.idx",
  "*.ind",
  "*.lof",
  "*.lot",
  "*.out",
  "*.toc",
  "*.acn",
  "*.acr",
  "*.alg",
  "*.glg",
  "*.glo",
  "*.gls",
  "*.ist",
  "*.fls",
  "*.log",
  "*.fdb_latexmk",
  "*.dvi",
  "*.synctex.gz"
],
       "latex-workshop.latex.recipes": [
      {
        "name": "without bib",
        "tools": ["uplatex", "uplatex", "dvipdfmx"]
      }, {
        "name": "with bib",
        "tools": ["uplatex","pbibtex","uplatex","uplatex", "dvipdfmx"]
      },{
        "name": "with biber",
        "tools": ["uplatex","biber","uplatex","uplatex", "dvipdfmx"]
      }
    ],
    "latex-workshop.latex.tools": [
      {
        "name": "platex",
        "command": "platex",
        "args": [
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "uplatex",
        "command": "uplatex",
        "args": [
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
      },
      {
        "name": "pbibtex",
        "command": "pbibtex",
        "args": [
            "%DOCFILE%"
        ]
    },
      {
        "name": "dvipdfmx",
        "command": "dvipdfmx",
        "args": ["%DOCFILE%.dvi"]
      },

      {
        "name": "biber",
        "command": "biber",
        "args": [
          "%DOCFILE%"
      ]
      }
    ],

```
設定としては、
- 余分なファイルをコンパイル時に削除する
- コンパイル時に uplatex → pbibtex → uplatex → dvipdfmx と通すようにする
- エディタの見た目をいい感じに
というような内容です。好みもあるのでカスタマイズできる人はやってみてください。

git が入っている人はテンプレート使ってリポジトリを作ってクローンしてくれればいいですし、そうでない人は.zipをローカルに保存してそこで作業してください。
因みに僕はgit素人なのでなんか問題あったら言ってください。
