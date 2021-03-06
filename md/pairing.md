## PAIRING

吉田 努  
  
白勢研ゼミ 2015/10/21  

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
- ペアリング
    - 分かった部分のみ
    - あまり理解してない

---
## ペアリングとは
- 2入力1出力の写像
- 双線形写像(bilinear  map)
- 楕円曲線上の2点$aP$と$bQ$が有限体の元$g^{ab}$に変換される

---
## ペアリングの種類
- ヴェイユペアリング
    - 最初のペアリング?
- テイトペアリング
    - より早い?

---
## 楕円離散対数

<center>$y^2\ =\ x^3\ +\ ax\ +\ b \\\ (a,\ b\ \in\ F_q,\ (x,y)\ \in\ F_q\ \times\ F_q)$</center>
- 楕円曲線上の2点$P, Q$が既知とする  
    <center>$P\ =\ lQ$</center>
    を満たす$l$を求める問題を楕円離散対数問題(ECDLP)という

--
- $f:\ E(F\_q)\ \to\ F\_\{q^\{m\}\}$
    - が存在するとする
    - $f(P)^l\ =\ f(lP)\ =\ f(Q)$  
    が成立する
- $F(P)\ =\ \alpha,\ F(Q)\ =\ \beta(\alpha,\ \beta\ \in\ F\_\{q^m\})$  
とすれば, $\alpha^l\ =\ \beta$と表すことができる

--
- 通常の有限体での離散対数問題を計算することで楕円離散対数の計算を行うことができる
- $E/F\_p$におけるECDLPよりも$F\_{q^m}$のDLPの方が計算が容易である場合に有効

---
## 代数的閉包
- 体$K$の代数的閉包を$\overline{K}$と表す
- $K$の代数的閉包
    - 体$K$上の変数多項式の根すべてを$K$に加えた体である
- 例
    - 実数体$R$の代数的閉包は$C$である

--
## 有限体の代数的閉包
$\overline{F\_q}\ =\ \cup\_{k \gt 1}F\_{q^k}$
- 体$K$上で定義された楕円曲線$E/K$を考える

---
## $n$ねじれ群
- ある整数について楕円曲線上の点の位数が$n$となる集合
    - $E[n]\ :=\ \\{P\ \in\ E(\overline{K})\ |\ nP\ =\ O\\}$
    - $n$ねじれ群という
    - この群の元を$n$ねじれ点という
    - これらの点は全部で$n^2$個ある


---
## ヴェイユペアリング
- 2つの$n$ねじれ点からの1の$n$乗根への写像
- $P,Q\ \in\ E[n]$に対して, $e_n(P,\ Q)$と記述される  
<center>$E[n]\ \times\ E[n]\ \to\ \mu_n\ \subset\ \overline{K}$</center>
<center>$(P,\ Q)\ \mapsto\ e_n(P,\ Q)$</center>

---
## ヴェイユペアリングの性質
- $P, P_1, P_2, Q, Q_1, Q_2, \in E[n]$

 1. 双線形

    - $e_n(P_1\ +\ P_2,\ Q)\ =\ e_n(P_1,\ Q)e_n(P_2,\ Q)$
    - $e_n(P,\ Q_1\ +\ Q_2)\ =\ e_n(P,\ Q_1)e_n(P,\ Q_2)$

 1. 同一性

    - $e_n(P,\ P)\ =\ 1$

 1. 非退化

    - $\forall Q\ \in\ E[n]$に対して, $e_n(P,\ Q)\ =\ 1$ならば$P\ =\ O$

---
## 因子
- このあたりから難しいので...
- 大まかな流れ
-> 因子を求める  
-> 関数を求める  
-> ヴェイユペアリング

---
## ペアリングの原点
- MOV攻撃のために考案された?
- 楕円曲線離散対数を通常の有限体での離散対数で考えたい


---
## 参考文献
- 暗号理論と楕円曲線
