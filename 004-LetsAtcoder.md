---
marp: true
---

<!--
theme: gaia
_footer: © 2020 shion.ueda
_class: lead
-->

# 今日から始めるAtCoder

2020-00-00（WIP）
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

## 幅優先探索（BFS）

---

## ABC007C - 幅優先探索

### 問題

上下左右に移動できる2次元盤面上の迷路のスタート地点からゴール地点への最短距離を求めましょう。迷路の行数 **R** と列数 **C**、スタート座標 **sy**, **sx** とゴール座標 **gy**, **gx**、迷路の情報（空きマス **.** と壁マス **#**）が与えられます。

### 制約

- 盤面は 1 ≦ R ≦ 50 かつ 1 ≦ C ≦ 50
- スタート、ゴール地点は 1 ≦ sy,gy ≦ R かつ 1 ≦ sx,gx ≦ C

https://atcoder.jp/contests/abc007/tasks/abc007_3

---

## あ