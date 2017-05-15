## ペアリングを用いた暗号方式

吉田 努  
  
白勢研ゼミ 2016/09/26  

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
- ペアリングの基本
- 電子署名
- ペアリングの使われ方

---
## ペアリング
- 楕円曲線上で定義される双線形写像
- 双線形性
	- $e(aP, bQ) = e(P, Q)^{ab}$
	- 恐らくこれが一番重要

---
## 電子署名
- 公開鍵暗号の逆を行うイメージ？
	- そうでなくてもよい

- 3つの機能？
	- なりすまし防止
	- 改竄検出
	- 否認防止

- 公開鍵と署名から得られる情報から秘密鍵が漏洩してはいけない

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
