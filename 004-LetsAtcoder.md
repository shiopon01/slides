---
marp: true
---

<!--
theme: gaia
_footer: © 2020 shion.ueda
_class: lead
-->

# 今日から始めるAtCoder

2020-2-00（WIP）
shion.ueda

---

## 目次

- 競技プログラミングとは
- 例題
- なんか
- 幅優先探索（BFS）

---

<!--_class: lead -->

## 競技プログラミングとは

---

hogehoge

---

<!--_class: lead -->

## 例題

---

## ABC086A - Product

### 問題

2つの整数値 **a**, **b** が与えられます。
**a** と **b** の積が偶数か奇数か判定してください。
（偶数なら `Even`、奇数なら `Odd` と出力する。）

### 制約

- 1 ≤ a,b ≤ 10000

https://atcoder.jp/contests/abc086/tasks/abc086_a

---

### 入出力例1

```txt
3 4
```

```txt
Even
```

### 入出力例2

```txt
1 21
```

```txt
Odd
```

---

### 解答例

```go
// Go言語
package main

import "fmt"

func main() {
	var a, b int
	fmt.Scan(&a, &b)

	if a*b%2 == 0 {
		fmt.Println("Even")
	} else {
		fmt.Println("Odd")
	}
}
```

---

<!--_class: lead -->

## 最短路問題

---

## 例

### 問題

上下左右に移動できる2次元盤面上の迷路のスタート地点からゴール地点への最短距離を求めます。迷路の行数 **R** と列数 **C**、スタート座標 **sy**, **sx** とゴール座標 **gy**, **gx**、迷路の情報（空きマス **.** と壁マス **#**）が与えられます。

### 制約

- 盤面は 1 ≦ R ≦ 50 かつ 1 ≦ C ≦ 50
- スタート、ゴール地点は 1 ≦ sy,gy ≦ R かつ 1 ≦ sx,gx ≦ C

---

### 入出力例1

```txt
7 8
2 2
4 5
########
#......#
#.######
#..#...#
#..##..#
##.....#
########
```

```txt
11
```

---

<!--_class: lead -->

最短路問題
↓
## 幅優先探索（BFS）

---

## 幅優先探索（BFS）とは

> 幅優先探索（はばゆうせんたんさく、英: breadth first search）はグラフ理論（Graph theory）において **木構造（tree structure）やグラフ（graph）の探索に用いられるアルゴリズム**。（略）...幅優先探索は解を探すために、**グラフの全てのノードを網羅的に展開・検査** する。

- 最短路や最小手数を求めるためのアルゴリズム
  - 迷路の最短路
  - パズルの最小手数
  - SNSでの、ある人からある人への友人関係最小ステップ数
- 似たものに、深さ優先探索（DFS）がある

---

## 深さ優先

![bg 50%](images/004/dfs.png)

---

## 幅優先

![bg 50%](images/004/bfs.png)

---

## 最短路を求めるアルゴリズム

### 準備

1. **座標を記録するQueue** と、**最短路を記録する配列** を準備する
2. 開始地点の頂点の座標をQueueに入れる

### 探索（Queueの中が空になるまで 3〜5 繰り返し）

3. Queueから頂点をひとつ取り出す
4. 辺で繋がる頂点を調べ、配列に最短路を記録する
5. 調べた頂点をQueueに入れる

---

### 最長路例：アローダイアグラムのクリティカルパス

経路が正の数のみと決まっている場合などは、経路の数値を負の値として考えることで最大値（クリティカルパス）を割り出すこともできる。

![w:800px](images/004/cretical-path.png)

(応用情報技術者平成24年秋期 午前問52 の有向グラフ）

---

<!--_class: lead -->

## 迷路の最短路を求める - 図解

迷路は巨大な無向グラフと言える。

---

迷路は
`[行][列]` の
2次元配列で
表すことが
できる。

ここでは
**S** が `[0][0]`
**G** が `[2][3]`
<br>

答え：
**G** の最短距離は **11**

![bg 50%](images/004/meiro.png)

---

### 事前準備

1. **迷路の配列**（道は `.` 壁は `#` の文字で表現）と、
  同じサイズの **最短路を保存する配列** と、
  十分なサイズの **Queue** を用意する。（**y,x** のペアを保存）
2. スタート地点の頂点の **y,x** をQueueに保存する。

![w:1150px](images/004/setup.png)

---

### 探索準備

開始地点の座標をQueueに入れて、開始地点の座標を **0** に設定

![w:1150px](images/004/bfs-1.png)

---

### 探索①：Queueから頂点を1つ取り出して処理

隣接する頂点の最短路を **現在地の最短路+1** して座標をQueueに追加。

![w:1140px](images/004/bfs-2.png)

---

### 探索②：Queueから頂点を1つ取り出して処理

隣接する頂点の最短路を **現在地の最短路+1** して座標をQueueに追加。

![w:1140px](images/004/bfs-3.png)

---

### 探索③：Queueから頂点を1つ取り出して処理

隣接する頂点の最短路を **現在地の最短路+1** して座標をQueueに追加。

![w:1140px](images/004/bfs-4.png)

---

### 探索④：Queueから頂点を1つ取り出して処理

隣接する頂点の最短路を **現在地の最短路+1** して座標をQueueに追加。

![w:1140px](images/004/bfs-5.png)

---

<!--_class: lead -->

## ・・・・

---

### 最後の探索：Queueから頂点を1つ取り出して処理

隣接する頂点が無く、Queueが空なので終了。最短路は **11**。

![w:1140px](images/004/bfs-6.png)

---

### 注意する点

隣接する頂点を処理する際、先に対象の頂点が探索済みかどうかを判定する必要がある。

探索済みの頂点だった際、その回の処理は **スキップ** する。

（BFSでは、最初に設定された
移動数が後からきた移動数より大きくなることはない。）

![bg right 80%](images/004/bfs-etc.png)

---

<!--_class: lead -->

## 最短路問題 例題

---

## ABC007C - 幅優先探索

### 問題

上下左右に移動できる2次元盤面上の迷路のスタート地点からゴール地点への最短距離を求めます。迷路の行数 **R** と列数 **C**、スタート座標 **sy**, **sx** とゴール座標 **gy**, **gx**、迷路の情報（空きマス **.** と壁マス **#**）が与えられます。

### 制約

- 盤面は 1 ≦ R ≦ 50 かつ 1 ≦ C ≦ 50
- スタート、ゴール地点は 1 ≦ sy,gy ≦ R かつ 1 ≦ sx,gx ≦ C

https://atcoder.jp/contests/abc007/tasks/abc007_3

---

### 入出力例1

```txt
7 8
2 2
4 5
########
#......#
#.######
#..#...#
#..##..#
##.....#
########
```

```txt
11
```

---

## 解答例