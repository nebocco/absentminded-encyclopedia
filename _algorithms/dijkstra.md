---
layout: entry
changelog:
  - summary: 見出し作成
    authors: kimiyuki
    reviewers: kuretchi
    date: 2021-02-12T00:00:00+09:00
  - summary: Fibonacci Heap の計測の注釈を変更
    authors: noshi91
    reviewers:
    date: 2021-04-03T18:05:57+09:00
algorithm:
  input: >
    非負の辺重み $c : E \to \lbrace x \in \mathbb{R} \mid x \ge 0 \rbrace$ 付き有向グラフ $G = (V, E)$ および頂点 $s \in V$
  output: >
    各頂点 $t \in V$ に対し $s$-$t$ 最短路長
  time_complexity: $O(\vert V \vert ^ 2)$ や $O(\vert E \vert \log \vert V \vert)$ など
  space_complexity:
  aliases:
  level: green
description: >
  Dijkstra 法とは、単一始点最短経路問題を解くアルゴリズムのひとつ。グラフに負の辺があると動作しない。辺が非負という仮定をもとに動的計画法を利用して高速に動作し、計算量は $O(\vert V \vert ^ 2)$ や $O(\vert E \vert \log \vert V \vert)$ などである。
---

# Dijkstra 法

## 概要

Dijkstra 法とは、単一始点最短経路問題を解くアルゴリズムのひとつである。グラフに負の辺があると動作しない。辺が非負という仮定をもとに動的計画法を利用する。
計算量は、単純な実装では $O(\vert V \vert ^ 2)$ である。優先度付きキューを用いる実装では、優先度付きキューに何を使うかに依存し、Binary Heap を用いた場合は $O(\vert E \vert \log \vert V \vert)$ である。

単一始点最短経路問題を解くとは、辺に重みが付いた有向グラフ $G$ と頂点 $s$ が与えられたとき、$s$ を始点とする $s$-$t$ 最短経路をすべての頂点 $t$ に対して求めるということである。

## 詳細

(省略)

## その他

-   高速化のためには優先度付きキューへの push の前の枝刈りが重要である[^yosupo-speedup]。
-   Dijkstra 法は辺の重みが整数でかつ最大値が小さいときは優先度付きキューの持ち方を工夫することで計算量を落とせる。この手法は Dial's algorithm と呼ばれる。また特に、辺の重みが $0$ か $1$ のみである場合は 0-1 BFS と呼ばれる[^yosupo-speedup]。
-   辺を逆向きにして終点から Dijkstra 法をするとうまくいくことがある。また、始点と終点の両側からの Dijkstra 法がうまくいくこともある。
-   入力されたグラフを拡張して作った別のグラフ上で Dijkstra 法をするとうまくいくことがよくある。これは「拡張グラフでのダイクストラ法」などと呼ばれる。省略して「拡張ダイクストラ」と呼ばれることもあるが、これは不適切な呼び方であると批判されることが多い[^evima-extended-graph]。
-   Fibonacci heap を用いて適切に実装すると計算量が $O(\vert E \vert + \vert V \vert \log \vert V \vert)$ に落ちる。これは競技プログラミングの範囲内でもグラフによっては速いことがある[^rsk0315-fibonacci][^noshi91-fibonacci]。

## 参考文献

-   Dijkstra, E.W. A note on two problems in connexion with graphs. Numer. Math. 1, 269–271 (1959). <https://doi.org/10.1007/BF01386390>
    -   Dijkstra による提案論文。再発明された Prim 法の紹介も含んでいる。

## 関連項目

-   [動的計画法](/algorithm-encyclopedia/dynamic-programming)
    -   Dijkstra 法は動的計画法のひとつである。
-   Prim 法
    -   Prim 法は最小全域木を求めるアルゴリズムのひとつであるが、Dijkstra 法と類似している。
-   [Bellman-Ford 法](/algorithm-encyclopedia/bellman-ford)
    -   Bellman-Ford 法は Dijkstra 法と並ぶ単一始点最短経路問題を解くアルゴリズムのひとつである。Dijkstra 法より遅いが、Dijkstra 法とは違って負辺があっても動作する。
-   [Shortest Path Faster Algorithm](/algorithm-encyclopedia/spfa)
    -   Dijkstra 法を優先度付きキューでなく普通のキューを使うように修正するとほとんど SPFA になる。
-   [Warshall-Floyd 法](/algorithm-encyclopedia/warshall-floyd)
    -   Warshall-Floyd 法は全点対間最短経路問題を解くアルゴリズムのひとつである。Dijkstra 法を $\vert V \vert$ 回実行したいような場合には、代わりに Warshall-Floyd 法を使うとよい。
-   [Dial's algorithm](/algorithm-encyclopedia/dial)
    -   与えられるグラフの辺の重みが整数でかつ最大値が $k$ のとき、この仮定を使って優先度付きキューの持ち方を工夫することで、Dijkstra 法を修正して計算量は $O(k \vert V \vert + \vert E \vert)$ に落とせる。そのように修正したものが Dial's algorithm である。

## 外部リンク

-   [色々なダイクストラ高速化 - SlideShare](https://www.slideshare.net/yosupo/ss-46612984)<sup>[archive.org](https://web.archive.org/web/20210212144246/https://www.slideshare.net/yosupo/ss-46612984)</sup>
    -   <a class="handle">yosupo</a> によるスライド。必須の高速化テクニック (単純な枝刈り) や、辺の重みの整数性を利用した高速化テクニック (Dial's algorithm) などが紹介されている。
-   [ダイクストラ法のよくあるミスと落し方 - あなたは嘘つきですかと聞かれたら「YES」と答えるブログ](https://snuke.hatenablog.com/entry/2021/02/22/102734)<sup>[archive.org](https://web.archive.org/web/20210222035858/https://snuke.hatenablog.com/entry/2021/02/22/102734)</sup>
    -   <a class="handle">snuke</a> によるブログ記事。実装ミスをしている Dijkstra 法を撃墜するケースがまとめられている。

## 注釈

[^yosupo-speedup]: [色々なダイクストラ高速化 - SlideShare](https://www.slideshare.net/yosupo/ss-46612984)<sup>[archive.org](https://web.archive.org/web/20210212144246/https://www.slideshare.net/yosupo/ss-46612984)</sup>
[^evima-extended-graph]: <https://twitter.com/evima0/status/334678901521530880><sup>[archive.org](https://web.archive.org/web/20210212131916/https://twitter.com/evima0/status/334678901521530880)</sup>
[^rsk0315-fibonacci]: <a class="handle">rsk0315</a> の計測によると [AtCoder Regular Contest 064: E - Cosmic Rays](https://atcoder.jp/contests/arc064/tasks/arc064_c)<sup>[archive.org](https://web.archive.org/web/20201101135215/https://atcoder.jp/contests/arc064/tasks/arc064_c)</sup> (完全グラフ) では binary heap より Fibonacci heap の方が速い[^fibonacci-vs-naive]。(<https://twitter.com/rsk0315_h4x/status/1188898280459005954><sup>[archive.org](https://web.archive.org/web/20210212142947/https://twitter.com/rsk0315_h4x/status/1188898280459005954)</sup>)
[^noshi91-fibonacci]: <a class="handle">noshi91</a> の計測によると、Fibonacci Heap が Binary Heap と $O(\lvert V \rvert ^ 2)$ の実装のいずれよりも高速になるようなグラフが存在する。[Binary Heap を用いた Dijkstra 法の最悪ケースと Fibonacci Heap の計測](https://github.com/noshi91/blog/blob/master/pages/dijkstra_experiment.pdf) <sup>[archive.org](https://web.archive.org/web/20210301113825/https://raw.githubusercontent.com/noshi91/blog/master/pages/dijkstra_experiment.pdf)</sup>
[^fibonacci-vs-naive]: これは binary heap を用いた一般的な $O(\vert E \vert \log \vert V \vert)$ の実装との比較であり、密グラフでは Fibonacci heap を用いた実装より単純な $O(\vert V \vert ^ 2)$ の実装の方が速い場合が多いことに注意せよ。
