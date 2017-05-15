## 電子署名とプロキシ暗号

吉田 努  
  
白勢研ゼミ 2016/10/04  

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
- ペアリングの基本
- ペアリングを使った電子署名

---
## 今日の内容
- ペアリングの種類
- 前回の改良
- プロキシ暗号
- 今後の予定

---
## ペアリング
- 楕円曲線上で定義される双線形写像
- 双線形性
	- $e(aP, bQ) = e(P, Q)^{ab}$
	- 恐らくこれが一番重要

---
## ディストーション写像
- $\psi(P)$
- ある$P \in E[n]$に対して以下を満たす凖同型写像
	- $\psi(P) \in E[n]$
	- $\psi(P) \notin \langle P \rangle $

---
## ペアリングの種類
- $e'(aP, bP) = e(aP, \psi(bP))$ <!--' -->

1. type $I$
	- $e'(aP, bP) = e'(bP, aP)$ <!-- ' -->
	が成り立つ  <!--' -->
1. type $I\hspace{-.2em}I$
	- ディストーション写像は存在するが逆向きの写像を計算するのは困難
1. type $I\hspace{-.2em}I\hspace{-.2em}I$
	- ディストーション写像が存在しない

- type $I$は対称ペアリング, type$I\hspace{-.2em}I$, $I\hspace{-.2em}I\hspace{-.2em}I$は非対称ペアリングと呼ばれている

---
## これがなんなの？
- 多くは対称ペアリング
	- パラメータが少なくて済む

---
## Bonehの電子署名
- $H$: 楕円曲線への埋め込み関数
- $e: G_1 \times G_2 \to G_3$
	- 正確には違う
- M: messageのM

--
## Bonehの電子署名
- 秘密鍵
	- $s$
- 公開鍵
	- $P, sP$

- 署名
	- $sH(M)$

- 検証
	- $e(sP, H(M))\ \overset{?}{=}\ e(P, sH(M))$


---
## 自分のアイディア
- 秘密鍵
	- $P, s$
- 公開鍵
	- $S = e(P, H(M))^s$

- 署名
	- $sP$

- 検証
	- $e(sP, H(M))\ \overset{?}{=}\ S$

---
## 改良1
- $h: \\{0, 1\\}^* \to \mathbb{Z}$
- h(M) = m

--

- 秘密鍵
	- $s \in \mathbb{Z}, P \in G_1$
- 公開鍵
	- $Q \in G_2, e(P, Q)^s$

- 署名
	- $\frac{s}{m}P$

- 検証
	- $e(P, Q)^s \overset{?}{=} e(\frac{s}{m}P, m'Q)$ <!-- ' -->

--
## 失敗
- 誰でも署名できる
	- $(\frac{s}{m}P) m = sP$
	- $h$が点へ移すハッシュ関数ではない
- $m$を隠すにはスカラー倍ではなく足す必要がある


---
## 改良2
- 秘密鍵
	- $s \in \mathbb{Z}, P \in G_1$
- 公開鍵
	- $Q \in G_2, e(P, Q)^s$

- 署名
	- $(s + m)P$

- 検証
	- e((s + m)P, Q) = e(sP, Q)e(mP, Q)
	- しっくりくる検証がない

---
## 改良3
- 秘密鍵
	- $s \in \mathbb{Z}, P \in G_1$
- 公開鍵
	- $Q \in G_2, e(P, Q)^s, e(P, Q)^r$

- 署名
	- $(sm + r)P$

- 検証
	- $(e(P, Q)^s)^{m'} \overset{?}{=} e((sm+r)P, Q) / e(P, Q)^r$

--
### あまり良くないかもしれない
- 検証に一回のペアリングと一回の冪乗
- 上手く言ったと思っても穴があることが多い

---
## プロキシ暗号
- 代理人暗号や再暗号化など呼ばれる
- 英語だとProxy re-encryption
- Aさんに向けて暗号化した暗号文をBさんに向けた暗号文に変換できる暗号
- $e: E \times E \to G$
- $g = e(P, P) \in G$
- $p, g$を公開する

--
## プロキシ暗号
- 鍵生成
- Aさん
	- 秘密鍵: $a \in Z$
	- 公開鍵: $aP$

- Bさん
	- 秘密鍵: $b \in Z$
	- 公開鍵: $bP$

--
## プロキシ暗号
- $r_{A \to B} = (\frac{1}{a})(bP) = (\frac{b}{a})P$

- 暗号化
	- A向けの暗号文
	- $c_a = (mg^r, r(aP))$

- 通常の復号
	- $\frac{mg^r}{e(r(aP), (1/a)P)} = \frac{mg^r}{e(P, P)^r} = \frac{mg^r}{g^r} = m$


--
## プロキシ暗号
- 再暗号化
	- $e(raP, r_{A \to B}) = e(raP, (b/a)P) = e(P, P)^{rb} = g^{rb}$
	- $c_b = (mg^r, g^{rb})$

- 再暗号化の復号
	- $\frac{mg^r}{g^{{rb}^(1/b)}} = \frac{mg^r}{g^r} = m$

---
## 困った点
- 暗号の多くは対称ペアリングでかかれている
	- 非対称ペアリングに変換？
	- 安全性?

---
## 今後の予定
- プロキシ暗号の実装
	- 電子書籍の貸し借りに向いてる
- http://www.scat.or.jp/frontier/frontier79/okamoto.pdf
