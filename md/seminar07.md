## 群(部分群)

吉田 努  
  
白勢研ゼミ 2016/06/20  

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
## 前回
- Tepla

---
## 今回
- 群(部分群)
- 部分群

---
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
## 部分群
- 群$G$の部分集合$H$が群$G$の演算$\cdot$に関して群になる時、$H$は群$G$の部分群である

--
## 部分群
- 群$G$の部分集合$H$が以下の2つを満たすとき
	1. $a \in H \Rightarrow a^\{-1\} \in H$
	1. $a, b \in H \Rightarrow ab \in H$  
部分群という

--
## 部分群
- まとめたら
	- $a, b \in H \Rightarrow a^\{-1\}b \in H$
- 証明

---
## 同値関係
-  ある集合Sにおいて二項関係$\sim$が以下を満たすとき$\sim$は$S$の同値関係である
	1. 反射律
		- $a \sim a$
	1. 対称律
		- $a \sim b \Rightarrow b \sim a$
	1. 推移律
		- $a \sim b \land b \sim c \Rightarrow a \sim c$

---
## 同値類
- 集合$S$
- $a \in S$
- $a$と同値な元の集合を  
$\overline{a} = \\{x (\in S)| x \sim a\\}$  
と表し同値類という
- $S_a, C(a)$でも可

---
## 商集合
- $S/\sim\ =\ \\{S\_a | a \in S\\}$
	- 集合が元の集合
- $S/\sim$の和集合は$S$になる
- 同値関係の定義から  
$S_a \neq S_b \Rightarrow S_a \cap S_b = \phi$  
となる

---
## 剰余群
- $G$を群, $H$をその部分群とする
- $a, b \in G$
- $a^\{-1\}b\ \in H$は同値関係
	- 証明
- この同値関係による商集合が剰余群

---
## 剰余類
- $aH = \\{ah | h \in H\\}$
	- ただの$a$の同値類
- $aH$が$a$の同値類である証明
	- 剰余類から
	- $a \sim b \Leftrightarrow a^\{-1\}b \in H$から

---
## 他にも
- 正規部分群
- 群の演算の遺伝
- 結構面白いが不要？

---
## 余り
- gitはIT業界の常識らしい
	- 勉強しませんか？
	- 何かを作る？
