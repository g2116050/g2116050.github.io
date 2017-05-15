## 暗号で使う数学


吉田 努  
  
白勢研ゼミ 2016/05/09  

<style type="text/css">
	.reveal table {
		font-size: 80%;
	}
</style>

<style type="text/css">
.reveal section img {
  margin: 15px 0px;
  border: 0px;
  box-shadow: 0 0 0px rgba(0, 0, 0, 0);
}
</style>

---
## 今日の内容
- 写像
- 演算
- 群

---
## 写像
- 集合$A$の各元に対して、集合$B$の元がただ一つ対応する規則$f$が定まっているとき、この対応を$A$から$B$への写像という
- $f:A \to B$
<center>![Block](/home/b1012104/Pictures/Study/math/map/mapping.png)</center>

--
## Quiz 1
<center>![Block](/home/b1012104/Pictures/Study/math/map/mapping2.png)</center>

--
## Quiz 2
<center>![Block](/home/b1012104/Pictures/Study/math/map/mapping3.png)</center>

--
## Quiz 3
<center>![Block](/home/b1012104/Pictures/Study/math/map/mapping_undef.png)</center>


---
## 全射・単射
- 写像$f: A \to B$
- 全射
	- $\forall y \in B$に対して  
	$f(x) = y$  
	を満たす$x \in A$が存在する
- 単射
	- $x\_{1}, x\_{2} \in A$が  
	$f(x\_{1}) = f(x\_{2})$  
	ならば$x\_{1} = x\_{2}$となる

--
## 単射
<center>![Block](/home/b1012104/Pictures/Study/math/map/injmap.png)</center>

--
## 全射
<center>![Block](/home/b1012104/Pictures/Study/math/map/surmap.png)</center>

--
## 全単射
<center>![Block](/home/b1012104/Pictures/Study/math/map/surinjmap.png)</center>

---
## 演算
- 演算は実は写像
- $f: A \times A \to A$ のような写像
- $(x\_{1}, x\_{2}) \mapsto f(x\_{1}, x\_{2})$  
(ただし$x\_{1}, x\_{2} \in A$)
- つまり、演算は常に集合$A$に閉じている

---
## 群って何？
1. 単位元が存在する
1. 結合法則が成り立つ
1. 逆元が存在する  
を満たす集合

--
## 群
- 集合$G$が演算$\cdot$に対して以下を満たすとき群という
	1. (結合律)  
	$a, b, c \in G$に対して, $(a \cdot b) \cdot c = a \cdot (b \cdot c)$
	1. (単位元の存在)  
	$\forall a \in G$に対して, $a \cdot e = e \cdot a = a$を満たす$e \in G$が存在する
	1. (逆元の存在)  
	$\forall a \in G$に対して, $a \cdot a' = a' \cdot a = e$を満たす$a' \in G$が存在する

- 集合$G$が演算$\cdot$に対して群であるとき$(G, \cdot)$と表す
<!-- ' -->

--
## 可換群
- 群に加えて
	- (可換律)  
	$a, b \in G$に対して, $a \cdot b = b \cdot a$を満たす
- アーベル群とも呼ぶ

---
## 群の具体例
- $(Z, +)$  
= $\\{\cdots, -2, -1, 0, 1, 2, \cdots\\}$
- 結合法則
	- 自明
- 単位元の存在
	- $a + 0 = 0 + a = a$
- 逆元
	- $a + (-a) = (-a) + a = 0$

---
## 部分群
- 群$G$の部分集合$H$が群$G$の演算$\cdot$に関して群になる時、$H$は群$G$の部分群である

--
## 例1
- $(Z, +)$の部分集合$\\{0\\}$は$Z$の部分群である
	- 結合法則
		- 自明
	- 単位元
		- $0 + 0 = 0$
	- 逆元
		- $0 + (-0) = 0$

--
## 例2
- $(Z, +)$の部分集合$3Z = \\{\cdots, -3, 0, 3, \cdots\\}$は$Z$の部分群である
	- 結合法則
		- 自明
	- 単位元
		- $0 + a = a + 0 = a$
	- 逆元
		- $a + (-a) = (-a) + a = 0$

---
## $Z/nZ$の正体
- 今まで何気なく出てきた
- $Z/5Z = \\{0, 1, 2, 3, 4\\}$?

---
## 剰余群
- 剰余類
	- $G$: 群
	- $H$: $G$の部分群
	- $a \cdot H$の形の部分集合を$G$における剰余類という$(a \in G)$
- 剰余類の全体の集合
	- $G/H = \\{a_i\cdot H\\}$
	- $a \cdot H = \\{a\cdot h | \forall h \in H\\}$

---
## 結局のところ
- $Z/5Z = \\{0+5Z, 1+5Z, 2+5Z, 3+5Z, 4+5Z\\}$

---
## その他
- ラグランジュの定理  
- 環
- 体
- 拡大体
- 楕円曲線

---
## 何の役に立つの？
- 群の性質
- 公開鍵暗号が理解できた気になれる

---
## 群のまとめ
- 群は演算と集合の話
- 演算は何でもよい
- 3つの条件
	- 結合法則
	- 単位元の存在
	- 逆元の存在
- 部分群は意外と重要

---
## 参考文献
- 代数学から学ぶ暗号理論
