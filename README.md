はじめに
======

対象者
------

卒論か修論をLaTeXで書きたい人

趣旨・目標
----------

なんかテンプレートとかネット上に落ちてるけど、いきなり見てもわかんないし、あんまり長い文章に適していない気がするので、わかるように説明する。

OSはWindowsベースで説明しています。MacでもLinuxでも基本的には同じなので参考にはなるかと思います。Macの方は、[泉富士夫先生の作成したマニュアル](http://fujioizumi.verse.jp/download/TeXShop_Japanese.pdf)を参考にするとよいです。

LaTeXってなに？って人へ
-----------------------

こんなん書けるようになるやつです。

<div align="center"><http://www.slideshare.net/ssuserbd0784/ss-57672851:embed:cite></div>


準備
==========================

インストール
----------
http://did2memo.net/2014/03/06/easy-latex-install-windows-8-2014-03/

Macの人はこちら（<http://fujioizumi.verse.jp/download/TeXShop_Japanese.pdf>／<http://osksn2.hep.sci.osaka-u.ac.jp/~taku/osx/install_ptex.html:title>）を参考にインストールしてください。

エディタを決める
------------------
TeXworksで充分。

適当にプリアンブルを書く
--------------------------
`\documentclass`から`\begin{document}`の間に書きます。例えばこんな感じです。

```
\documentclass{jsarticle}
\usepackage{amsmath}
\usepackage{bm}
\usepackage{overcite}
\usepackage{wrapfig}
\usepackage[dvipdfmx]{graphicx}
\newcommand{\FRAC}[2]{\leavevmode\kern.1em
 \raise.5ex\hbox{\the\scriptfont0 #1}\kern-.1em
 /\kern-.15em\lower.25ex\hbox{\the\scriptfont0 #2}}
\begin{document}
あいうえお
$\FRAC{1}{2}$
\end{document}
```

`\usepackage`で指定したパッケージが使えるようになるわけですが、上の例ではデフォルトで入っていないパッケージを導入しているので、皆さんが使おうとするとエラーが出るはずです。なのでパッケージを入れてやる必要があります。[ここ](https://texwiki.texjp.org/?LaTeX%E5%85%A5%E9%96%80%2F%E5%90%84%E7%A8%AE%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E5%88%A9%E7%94%A8)などを参考に入れてみましょう。例えば、上の例のoverciteを入れてみましょう。[こちら](http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/overcite.html)からダウンロード可能です。エラーが出なくなれば、プリアンブルで指定したパッケージがすべて入っていることになります。

あとで好きなパッケージ入れるからとりあえずいいわ、って人は、エラーに該当する`\usepackage`の行を消してしまい、先に進みましょう。それでもOKです。

`\newcommand`はマクロの指定です。とりあえず必要ない。

図を入れる
========

フォーマットはpdf安定
---------------------

黙ってpdfにする。余白のカットをしたいときは[PDF slim](http://www.forest.impress.co.jp/library/software/pdfslim/)とか使う。
```
\begin{figure}[htbp]
\centering
\includegraphics[height=80mm]{foo.pdf}
\caption{nanntoka}
\label{fig:hogehoge}
\end{figure}
```

ラベルを必ずつけよう
--------------------

コマンドは`\label{}`。[こちら](http://www.clas.kitasato-u.ac.jp/~fujiwara/infoScienceB/TeX/ref/labelAndRef.html)を参考にして、数式にラベルを付けてみましょう。

ちょっとしたコツとしては、

- 図: `\label{fig:foo}`
- 表: `\label{tab:foo}`
- 式: `\label{eq:foo}`
- 節: `\label{sec:foo}`

のように種類によってラベル名を系統だてておくと混乱を防げます。

参考文献を付ける
==============

文献情報を自分で書く方法
------------------------

LaTeXでは参考文献を付け、文献番号をコマンドで呼び出すことができます。[こちら](http://www.latex-cmd.com/struct/thebibliography.html)を見ながらやってみましょう。

予備知識： コマンドライン(非情報系の方向け)
------------------------
- http://techacademy.jp/magazine/5318
- http://www.atmarkit.co.jp/ait/articles/0708/30/news137.html

Mendeleyと連携しよう
--------------------

Mendeleyと連携する方法は[こちら](http://pioneerboy.hatenablog.com/entry/2014/01/18/214446）をそのままマネすればOKです。リンク先ではDropboxを利用していますが、別に無くてもおｋ。

またこの方法だと、一度文献データをコンパイルする必要があります。[こちら](http://akita-nct.jp/yamamoto/comp/latex/bibtex/bibtex.html）も参考にしてください。

一度短いレポートをつくってみよう
=======================

ここまでの知識をできるだけ使って短いレポートでも作ってみましょう。

全体の構成
=========

jsbookにしよう
--------------

卒論・修論ぐらいの長い文章を書くときはjsbookがベストだと思いますので変えましょう。ヘッダーに章番号と章タイトルが入ってかっちょええです。

```
\documentclass[a4paper,10pt,oneside,openany]{jsbook}
```
 

複数章の長い文章を書くときの構成
--------------------------------

冒頭で言いましたが、web上に落ちているテンプレートには、長い文章を書くのに適しているものは少ないように感じます。というのも、普通LaTeXで何章にもわたる長い文章を書くときにはそれ相応の手法があるのです。図示するとこんな感じ。

TODO
\[f:id:kichiku\_kikuchi:20160130222427j:plain\]

ひとつのファイルに何万字も書いて図を入れて数式入れて。。。ってのは無理があります。なので、<b>各チャプターごとにtexファイルを分割</b>し書いていきます。\\input{}を使えば、複数のtexファイルをひとつにまとめることができます。ですが、最後に一気にタイプセットして細かい調整をしていくというのは大変ですね。<b>タイプセットも各チャプターごと</b>にできた方が絶対便利です。[こちら](http://khmtvx.hatenablog.com/entry/2013/08/19/223003）を参考に。

上図のような構成にして、各チャプターのtexファイルとparent.texをタイプセットしてみてください。どちらもタイプセットできればOKです。

図は別フォルダへ
----------------

挿入する図（画像）を別ディレクトリに分けます。[ここ](http://homepage.seesaa.net/article/25260276.html）を参考にして、やってみましょう。別ディレクトに置いた図を挿入してparent.texがタイプセットできればOKです！

表紙はLaTeXで作らなくてもいい
-----------------------------

何で作っても構いませんが、サイズをA4用紙と全く同じにしましょう。210×297mmです。そして、[こちら](http://did2.blog64.fc2.com/blog-entry-483.html）にそって画像位置の調整を行うだけです。こちらではepsを使用していますが、黙ってpdfを使いましょう。
powerpointで作った場合、上のサイト通りにやると少しずれたのでちょっとだけ変えています。

```
\enlargethispage{\paperwidth}
\thispagestyle{empty}
\vspace*{-1truein}
\vspace*{-\topmargin}
\vspace*{-\headheight}
\vspace*{-\headsep}
\vspace*{-\topskip}
\noindent\hspace{-0.7in}\hspace*{-\oddsidemargin}
\includegraphics{cover.pdf}
```

また、表紙のtexファイルは個別に作成して上述の\\input{}で取り込むのが良いと思います。最終的なディレクトリ構成は下図のようになるでしょう。

TODO
\[f:id:kichiku\_kikuchi:20160130234205j:plain\]

目次をつくろう
--------------
http://www.latex-cmd.com/struct/contents.html


Advanced編
==========

markdownで書いて変換する方法
----------------------------

これ

http://mizchi.hatenablog.com/entry/2014/01/20/090957

http://qiita.com/mountcedar/items/e7603c2eb65661369c3b

リアルタイムプレビューする方法
------------------------------

これ

http://webmem.hatenablog.com/entry/sublime-text-markdown

参考文献のスタイルを変えたい
----------------------------

これ。

http://www.ketsuago.com/entry/2015/03/16/231806

その他
=====

図などを思い通りの位置に入れるコツ
----------------------------------

とにかく`\vspace`、`\hspace`でいじくれば解決できることが多いです。

便利ツール
----------

あんまりつかったことないですが色々あります。私が使ったことあるのは、MyScript MathPadというiOSのアプリぐらいですかね。手書きで書いた数式をTeX形式に変換してくれるアプリです。コマンドを覚えるまでは便利ですが、覚えたら要らなくなります。

https://itunes.apple.com/jp/app/myscript-mathpad-jeneretalatexno/id674996719?mt=8&uo=4

各種変換ツールはこちら。

https://texwiki.texjp.org//?%E5%A4%89%E6%8F%9B%E3%83%84%E3%83%BC%E3%83%AB


その他のリンク集
----------------
TODO

http://webmem.hatenablog.com/entry/how-to-write-a-modern-latex-for-academic-papers
http://qiita.com/amayaw9/items/01d626ce1ae18c27df8b
http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/011.html
http://osksn2.hep.sci.osaka-u.ac.jp/~naga/miscellaneous/tex/tex-tips1.html#Anchor-1.-42085
http://ichiro-maruta.blogspot.jp/2013/03/latex.html
http://joker.hatenablog.com/entry/2012/07/09/153537
http://dayinthelife.at.webry.info/201401/article_2.html
http://hnsn1202.hateblo.jp/entry/2012/06/07/030443

参考書
------

一応、参考書がなくても書けるようになることを目標にしていましたが、やはり一冊本があると安心します。超名著なので無駄にはならないはず。
TODO

http://www.amazon.co.jp/%E6%94%B9%E8%A8%82%E7%AC%AC6%E7%89%88-LaTeX2%CE%B5%E7%BE%8E%E6%96%87%E6%9B%B8%E4%BD%9C%E6%88%90%E5%85%A5%E9%96%80-%E5%A5%A5%E6%9D%91-%E6%99%B4%E5%BD%A6/dp/4774160458/ref=sr_1_1?ie=UTF8&qid=1454910053&sr=8-1&keywords=latex

http://www.amazon.co.jp/%E6%94%B9%E8%A8%82%E7%AC%AC5%E7%89%88-LaTeX2e-%E7%BE%8E%E6%96%87%E6%9B%B8%E4%BD%9C%E6%88%90%E5%85%A5%E9%96%80-%E5%A5%A5%E6%9D%91-%E6%99%B4%E5%BD%A6/dp/4774143197/ref=sr_1_8?ie=UTF8&qid=1454910053&sr=8-8&keywords=latex
