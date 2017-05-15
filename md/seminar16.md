## Improved Proxy Re-Encryption Schemes with Applications to Secure Distributed Storage

吉田 努  
  
白勢研ゼミ 2016/12/20  

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
- Identity-Based Proxy Re-Encryptionの要約

---
## 今日の内容
- PREとIBE
- 電子書籍への応用

---
## Introduction(1/2)
- PREはproxyがAliceの公開鍵を使って計算された暗号文をBobの秘密鍵で復号できる暗号文に変換を施す
- PREのプリミティブの応用は数多くある
	- Aliceが同僚のBobに一時的に暗号化されたメールを秘密鍵を送ることなく転送したいという状況
	- この場合, 委任者のAliceは彼女の受け取ったメールを被委任者のBobが彼の秘密鍵で復号できるような形式でproxyが再暗号化するのを任せる
	- Aliceは単純に彼女の秘密鍵をproxyに渡すこともできるが, この要件はproxyにおいて非現実的な信用のレベルである

---
## Introduction(2/2)
- 我々は前のアプローチよりも効率的ないくつかのPRE方式を提案する
- Unidirectional が我々の方式の一番の利点である
	- AliceはBobが彼女が委任することなくBobに委任できる
- proxyに再暗号化してもらうために, 委任者は秘密鍵のすべてを誰かに対して晒す必要がない(被委任者にでさえ)
- 限られた信用はproxyに置かれている
	- 再暗号化された暗号文は復号することができない
	- 我々の方式はproxyがすべての知りうる再暗号化の情報を公開しても安全であることを示す
- この方式はプロキシが完全に信用される必要がある場合には実用的ではないアプリケーションを実現させる
- 我々のPRE方式の実用性を示すため, PREを使ったsecure file systemの計測を行
- 我々のシステムは分散されている暗号化されたコンテンツへのアクセスを管理するために, 中央化されたアクセスコントロールサーバを利用している
- PREをアクセスコントロールサーバに復号権限のすべてを渡すことなく, 中央管理のアクセスコントロールを許すために利用している

---
## Background
- 復号権の委任の方法論はMamboとOkamotoが始めて示した
	- 従来の暗号化して復号するというアプローチを向上するものだった?
- Blaze, Bleumer and Straussは原始的proxy暗号を提案した
- BBS scheme
	- Elgamal based Scheme
	- p = 2q + 1
	- delegation key: $b/a \mod q$
	- $(mg^k \mod p, (g^{ak})^{b/a})$
- しかしながら固有の問題がある
	- Bidirectionality(双方向性)
		- b/aはAliceからBobへの暗号文の転換に使われ, その逆も含む(Bob->Alice)
		- それゆえAliceとBobが完全に信頼がおける場合には問題ない
	- Transitivity(推移性)
		- proxyは同意のない委任権が作れてしまう
		- $a/b$ と $b/c$ で$a/c$が作れてしまう
	- collusion(結託)
		- $(a/b) * b = a$

---
## Background
- Jakobsson developed quorum-based protocol
- Proxyは下位要素に分けられる
- 委任者の鍵はproxyが信頼できるならば安全である

---
## Background
- Dodis and Ivanは単方向性をもつElgamal, RSA and IBEベースのPREを実現した
	- ユーザの秘密鍵を二つの団体間で共有することで実現
- Elgamal scheme
	- Aliceの秘密鍵は$s = s_1 + s_2$に分けられる
	- $s_1$: proxy, $s_2$: Bob
	- 与えられた暗号文$(mg^{sk}, g^k)$
	- proxy: $(mg^{sk}/(g^k)^{s_1})$
	- Bob: $(mg/(g^k)^{s_2}) = m$
	- 欠点: 真の意味で暗号文の再暗号化を行わない
		- 追加の秘密情報の保持を求める(i.e. $s^(i)_2$を共有する)
		- 現実的には管理が難しい
	- 結託攻撃には弱い

---
## Background
- key-insulated
- signcryption scheme
