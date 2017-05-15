## Identity-Based Proxy Re-Encryption

吉田 努  
  
白勢研ゼミ 2016/11/2x  

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
- ペアリング
- 電子書籍
	- proxy re-encryptionによる電子書籍の貸出
	- LCP要件

---
## 今日の内容
- Identity-Based Proxy Re-Encryptionの要約

---
## Abstract
- proxy re-encryption(PRE)とは, 半分信頼できる代理人(semi-trusted proxy)が暗号化前の平文を見ずにAlice向けの暗号文をBob向けの暗号文に変換するもの
- 公開鍵の設定で数多くのPREが提案されている
- この論文ではIDベースのPRE(IB-PRE)を取り上げる
	- 我々の方式は現在のIBEと互換性がある
	- 鍵生成局の特別な作業は必要ない
		- 鍵生成と鍵配布のみ
	- 非対話かつ複数の再暗号化を許す
		- 再暗号化鍵生成時に相手との通信が不要
	- ランダムオラクルとDBDH仮定に基づく

--
## 解説
- Identity-based Encryption(IBE)
	- ID情報(任意の文字列)に基づく暗号
	- 文字列を公開鍵として扱えるようになる
		- 相手のIDだけで暗号化可能
		- ただし信頼のおける鍵生成局が必要
- Proxy Re-Encryption(PRE)
	- 日本では代理人暗号やプロキシ暗号
	- その名のとおり代理人が暗号処理を行う
		- 具体的には代理人が再暗号鍵を貰い, 再暗号化を行う
- Identity-based Proxy Re-Encryption(IB-PRE)
	- 二つを組み合わせた暗号
	- IDを元に暗号化, 再暗号が可能

--
## 解説
- ランダムオラクル
	- 完全にランダムなハッシュ関数はないと証明した論文があるらしい
	- ランダムオラクル仮定 = ハッシュ関数が一様に分布するものとする(しないけど)
	- 多分理論的には重要
		- しかしハッシュ関数を攻略するのは難しいのでは?

---
## Introduction
- まずは普通のPREについて
- 代理人(proxy)はAliceの公開鍵を使って暗号化された暗号文をBobに向けたものへと変換できる
	- AliceはBobに秘密鍵を渡す必要がない
- 代理人は完全には信頼できないという基本的な性質がある
	- 代理人は秘密鍵を知らない
	- 変換時に平文が分からない
- 代理人とBobの結託は許さない
	- 少なくとも片方は信頼できる
	- 結託は防げるし検知できる

--
## Introduction
- PREは多数提案されている
- 本論文ではPREをIBEに拡張しますよ
	- IBEは鍵配布問題の解決に役立つと知られている
- またIBEは新しい暗号方式の展開を許している
	- secret handshake
	- public-key searchable encryption
	- CCA2-secure public-key encryption
	- digital signature

--
## Introduction
- IB-PREはIDでPREができますよ
- proxyは平文は見れませんよ
- 秘密鍵はproxy key/re-encryption keyからは分かりませんよ
- 我々の方式はBoneh-Franklin IBEと互換性がありますよ
	- 同じ秘密鍵とパラメータを使用している
- 鍵生成局:PKG(Private Key Generator)が必要
	- 基本的にはproxy keyをPKGが作れる

--
## Introduction
- でも2つの観点から気にしない
	- 理論的な面
		- IB-PREを見つけることを不可能にしてしまう
	- 実践的な面
		- PKGがproxy keyの生成に関わるのは望ましくない

---
## 提案方式の特性
- PREの特性(Atenieseら)
	- 単方向性(Unidirectionality)
		- AがBの暗号文を復号することなく, AがBに復号するのを許す
	- 非対話性(Non-Interactivity)
		- AはB向けの再暗号化鍵をoflineで作ることができる
	- 多重使用性(Multi-use)
		- 一つの暗号文に対して複数回の再暗号化を許す
	- 非推移性(Non-transitivity)
		- 代理人がさらに委任することは許されない
		- 再暗号化鍵$rk\_{A->B}$と$rk\_{B->C}$から$rk\_{A->C}$は作れない
	- Space-optimal(訳し辛い)
		- 再暗号化のための追加の通信が必要なこと

---
## 提案方式の特性
- 単方向性(Unidirectionality)のみに着目する
	- 双方向性 $\subset$ 単方向性
	- Alice -> Bob, Bob -> Aliceとすれば双方向性は実現できる
- 非対話性(Non-Interactivity)は基礎的な性質
	- IDベース系だとシステムに加入する前のユーザにPREを適応できるという面白い事態が起きる
	- IDは証明書にも条件を表すことにも使える
		- "Alice || security-clearance || time-period"
- 多重使用性(Multi-use)を満たすものもある
	- 単方向性と多重使用性を満たす方式を探すことはオープンプロブレム

---
## 定義
- Bilinear Map $e: G_1 \times G_1 \to G_T$
	1. $G_1, G_T$は位数$q$の群
	2. $\forall a, b \in (Z/qZ)^*, g \in G_1, e(g^a, g^b) = e(g, g)^{ab}$
	3. 非退化
	4. eは効率的に計算できる
- 簡潔さのために対称ペアリングで定義されている
	- が二つとも非対称ペアリングで動くよ
	- $e: G_1 \times G_2 \to G_T$

- DBDH
	- 略

---
## IB-PRE
- 定義 非対話のIB-PRE
	- Setup, KeyGen, Encrypt, Decrypt, RKGen, Reencrypt
- Setup($1^k$, MaxLevels)
	- paramsとmskを出力する
- KeyGen(params, msk, id)
	- idに対応する秘密鍵$sk\_{id}$を出力する
- Encrypt(params, id, m)
	- idに向けた暗号文$c\_{id}$を出力
- RKGen(params, $sk\_{id}$, $id_1$, $id_2$)
	- 再暗号化鍵$rk\_{id_1 \to id_2}$を出力
- Reencrypt(params, $rk\_{id\_1 \to id\_2}$, $c\_{id}$)
	- 再暗号化された暗号文$c\_{id_2}$を出力
- Decrypt(params, $sk\_{id}$, $c\_{id}$)
	- mを出力

---
## IB-PRE
