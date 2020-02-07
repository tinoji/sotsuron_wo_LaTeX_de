卒論をLaTeXで。
======

まえがき
------
これは[tinoji](https://github.com/tinoji)が[2016年にブログに書いた記事](https://www.ketsuago.com/entry/2016/01/30/191934)をGitHubに移行したものです。  
古い記事にもかからわず、卒論シーズンになると驚くほど多くのPVがありました。知り合いの学生さんに「参考にしてます」とリプをもらったりもしました。嬉しい:pray:  
しかしリンク切れが出てきてしまったり、あまりに情報が古くなったりしていたので、「自分は最近使ってないから更新できないし困ったなー。GitHubに置いたら誰かメンテしてくれないかなー。」と思い、移行してみました。  

対象者
------
卒論や修論をLaTeXで書きたい人

趣旨・目標
----------
上述の対象者がLaTeXを使用して、
- なんとなく文章を書き、
- どうにか数式と図を入れ、
- 参考文献を付け、
- そこそこきれいなpdfを出力でき、
- 卒論程度の長さの文章を書くためのテンプレートを作ったり構成ができる

ようになることを目標にしています。  
すべて説明するのではなく、いい感じのリンク集として機能すればよいかなーと思っています。

環境
----
OSはWindowsベースで説明しています。MacでもLinuxでも基本的には同じなので参考にはなるかと思います。Macの方は、[泉富士夫先生のマニュアル](http://fujioizumi.verse.jp/download/TeXShop_Japanese.pdf)を参考にするとよいです。

LaTeX is 何
-----------------------
これは[tinoji](https://github.com/tinoji)が[初めてLaTeXで書いたレポート](https://www.slideshare.net/ssuserbd0784/ss-57672851)です。こんな感じのPDFが作れるようになるソフトウェア(というか組版システム)がLaTeXです。

<img src="https://github.com/tinoji/sotsuron_wo_LaTeX_de/blob/master/images/tex_sample.png" width="500px">

今はMicrosoft Wordでも数式がかなりキレイに挿入できるようになったりしているので、ぶっちゃけそれもありかもしれません。好きなものを使いましょう。

<br>

準備
==========================

インストール
----------
古いかもしれませんが、当時は[このインストーラ](http://did2memo.net/2014/03/06/easy-latex-install-windows-8-2014-03/)一択でした。
Macの人は[こちら](http://osksn2.hep.sci.osaka-u.ac.jp/~taku/osx/install_ptex.html:title)を参考にインストールしてください。

インストールができて、説明どおりにPDFを生成できればOKです。


エディタを決める
------------------
最初はデフォルトで入るTeXworksで充分だと思います。慣れてきたら好みのものを探すとよいかと。

適当にプリアンブルを書く
----------------------
ここから実際にLaTexを書いていきます。

LaTeXでは環境設定のひとつとしてプリアンブルというものをいじる必要があります。プリアンブルはパッケージやマクロを定義するもので。`\documentclass`から`\begin{document}`の間に書きます。例えばこんな感じです。

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

`\usepackage`で指定したパッケージが使えるようになるわけですが、上の例ではデフォルトで入っていないパッケージを導入しているので、皆さんが使おうとするとエラーが出るはずです。なのでパッケージを入れてやる必要があります。[こちら](https://texwiki.texjp.org/?LaTeX%E5%85%A5%E9%96%80%2F%E5%90%84%E7%A8%AE%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%AE%E5%88%A9%E7%94%A8)などを参考に入れてみましょう。例えば、上の例のoverciteを入れてみましょう。[ここ](http://www.biwako.shiga-u.ac.jp/sensei/kumazawa/tex/overcite.html)からダウンロード可能です。エラーが出なくなれば、プリアンブルで指定したパッケージがすべて入っていることになります。

あとで好きなパッケージ入れるからとりあえずいい、という人は、エラーに該当する`\usepackage`の行を消してしまい、先に進みましょう。

`\newcommand`はマクロの指定です。とりあえず無視しましょう。

<br>

図を入れる
========

フォーマットはPDF安定
---------------------
次は図を入れてみましょう。[色々ややこしい事情があるらしい](https://qiita.com/zr_tex8r/items/5413a29d5276acac3771)ので黙ってPDFにします。余白のカットをしたいときは[PDF slim](http://www.forest.impress.co.jp/library/software/pdfslim/)などを使うとよいです。

とりあえず何でもよいのでpdfにした画像を用意して入れてみましょう。画像を読み込むときはこんな感じです。画像はとりあえず `*.tex`があるディレクトリの中に入れておけばOKです。※たくさん画像があるとごちゃごちゃしてくるので、後々整理します．
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
数式や図にラベルというものを付けることができます。「式(4)では・・・」のような文を書くときに、ベタ書きしてずれてしまうのを防ぐための機能だと思ってOKです。

コマンドは`\label{}`。[こちら](http://www.clas.kitasato-u.ac.jp/~fujiwara/infoScienceB/TeX/ref/labelAndRef.html)を参考にして、数式にラベルを付けてみましょう。

ちょっとしたコツとしては、

- 図: `\label{fig:foo}`
- 表: `\label{tab:foo}`
- 式: `\label{eq:foo}`
- 節: `\label{sec:foo}`

のように種類によってラベル名を系統だてておくと混乱を防げます。

<br>

参考文献を付ける
==============

文献情報を自分で書く方法
------------------------
LaTeXでは参考文献を付け、文献番号をコマンドで呼び出すことができます。[こちら](http://www.latex-cmd.com/struct/thebibliography.html)を見ながらやってみましょう。

予備知識： コマンドライン(非情報系の方向け)
------------------------
以下のMendelayとの連携で使うので、コマンドラインをちょっと使えるようになっておくとよいです。
- http://techacademy.jp/magazine/5318
- http://www.atmarkit.co.jp/ait/articles/0708/30/news137.html

Mendeleyと連携しよう
--------------------
文献管理に[Mendelay](https://www.mendeley.com/?interaction_required=true)を使ってる人も多いでしょう。LaTexとMendelayを連携すると、文献を引用するためのキーがすぐ取得できて非常に便利です。

Mendeleyと連携する方法は[こちら](http://pioneerboy.hatenablog.com/entry/2014/01/18/214446)をそのままマネすればOKです。リンク先ではDropboxを利用していますが、別にローカルでも問題ありません。

またこの方法だと、一度文献データをコンパイルする必要があります。[こちら](http://akita-nct.jp/yamamoto/comp/latex/bibtex/bibtex.html)も参考にしてください。

<br>

一度短いレポートをつくってみよう
=======================
ここまでの知識をできるだけ使って短いレポートでも作ってみましょう。  
[冒頭に載せたレポートのtexファイルがPCに残っていたので置いておきます](https://github.com/tinoji/sotsuron_wo_LaTeX_de/tree/master/examples/report)。

<br>

全体の構成
=========

jsbookにしよう
--------------
卒論・修論ぐらいの長い文章を書くときはjsbookがベストだと思いますので変えましょう。ヘッダーに章番号と章タイトルが入ってそれっぽくなります。

```
\documentclass[a4paper,10pt,oneside,openany]{jsbook}
```
 
複数章の長い文章を書くときの構成
--------------------------------
複数章に渡る長い文章を書くときは、少し工夫をする必要があります。

ひとつのファイルに何万字も書いて図を入れて数式入れて。。。ってのは無理があります。なので、**各チャプターごとにtexファイルを分割**し書いていきます。`\input{}`を使えば、複数のtexファイルをひとつにまとめることができます。ですが、最後に一気にタイプセットして細かい調整をしていくというのは大変ですね。**タイプセットも各チャプターごと**にできた方が絶対便利です。[こちら](http://khmtvx.hatenablog.com/entry/2013/08/19/223003)を参考に。

<img src="https://github.com/tinoji/sotsuron_wo_LaTeX_de/blob/master/images/chapter.jpg" width="500px">

上図のような構成にして、各チャプターのtexファイルと`parent.tex`をタイプセットしてみてください。どちらもタイプセットできればOKです。

図は別フォルダへ
----------------
挿入する図（画像）を別ディレクトリに分けます。[ここ](http://homepage.seesaa.net/article/25260276.html)を参考にして、やってみましょう。別ディレクトに置いた図を挿入して`parent.tex`がタイプセットできればOKです。

表紙はLaTeXで作らなくてもいい
-----------------------------
表紙ももちろん作れるのですが、なかなかうまくいかない印象があります。他のソフトでサクッと作ってしまうのがおすすめです。  
何で作っても構いませんが、サイズをA4用紙と全く同じにしましょう。210×297mmです。そして、[こちら](http://did2.blog64.fc2.com/blog-entry-483.html)にそって画像位置の調整を行うだけです。リンク先ではEPSを使用していますが、PDFを使いましょう。

PowerPointで作った場合、上のサイト通りにやると少しずれたのでちょっとだけ変えています。

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

また、表紙のtexファイルは個別に作成して`\input{}`で取り込むのが良いと思います。最終的なディレクトリ構成は下図のようになります。

<img src="https://github.com/tinoji/sotsuron_wo_LaTeX_de/blob/master/images/directory_layout.jpg" width="500px">

目次をつくろう
--------------
サクッとできるはずです。  
http://www.latex-cmd.com/struct/contents.html

<br>

ここまでできると、LaTeXの最低限のエッセンスは習得できたんじゃないかと思います。つまり**卒論が書けます**！！！頑張ってください〜〜 :v:

<br>


Advanced編
==========

Markdownで書いて変換する方法
----------------------------
普段からMarkdownを使っている人や、極力TeXのコマンドを打ちたくないという人にお勧めの方法です。とても便利です。
- http://mizchi.hatenablog.com/entry/2014/01/20/090957
- http://qiita.com/mountcedar/items/e7603c2eb65661369c3b

リアルタイムプレビューする方法
------------------------------
- http://webmem.hatenablog.com/entry/sublime-text-markdown

参考文献のスタイルを変えたい
----------------------------
デフォルトのまま参考文献を出力すると、こんな感じになると思います。
```
George M Sheldrick. A short history of SHELX. Acta Crystallographica Section A Foundations of Crystallography, 64:112–22, January 2008.
```

つまり、
```
ファーストネーム　ミドルネームの頭文字　ファミリーネーム．タイトル．出版物名（イタリック），巻数：ページ， 出版月　出版年．
```

という感じです。このスタイルは学問分野によって様々で、研究室によってはこのジャーナルの形式に合わせよ、なんていう決まりがあるかもしれません。結構つらいので、あまりこだわらない人はやめておいた方が身のためです。

- http://www.ketsuago.com/entry/2015/03/16/231806

<br>

その他
=====

図などを思い通りの位置に入れるコツ
----------------------------------
とにかく`\vspace`、`\hspace`でいじって調整するのが手っ取り早い気がします。

便利ツール
----------
あんまりつかったことないですが色々あります。手書きで書いた数式をTeX形式に変換してくれるアプリを使ったことがあるのですが、もうStoreから消えていました。探せば新しいものがあるはずです。

その他のリンク集
----------------
- [卒論/修論/博論のためのモダンなLaTeXの書き方](http://webmem.hatenablog.com/entry/how-to-write-a-modern-latex-for-academic-papers)
- [BibTeXのインストール](http://qiita.com/amayaw9/items/01d626ce1ae18c27df8b)
- [目次の変え方](http://osksn2.hep.sci.osaka-u.ac.jp/~naga/miscellaneous/tex/tex-tips1.html#Anchor-1.-42085)
- [使ってはいけない LaTeX のコマンド・パッケージ・作法](http://ichiro-maruta.blogspot.jp/2013/03/latex.html)
- [TeXのjsarticleで余白設定](http://joker.hatenablog.com/entry/2012/07/09/153537)
- [geometry パッケージによるページレイアウトの設定](http://dayinthelife.at.webry.info/201401/article_2.html)
- [初心者がutf8でLaTeXとBibTeXを使うための一通りの準備](http://hnsn1202.hateblo.jp/entry/2012/06/07/030443)

参考書
------
こちらを買うことをおすすめします。名著です。
- https://www.amazon.co.jp/dp/4774187054/ref=cm_sw_em_r_mt_dp_U_A.xpEbAM24K6H
