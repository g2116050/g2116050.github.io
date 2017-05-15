## Proxy Re-Encryption

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
## Proxy Re-Encryption(PRE)
- 簡潔に言うと復号権の委任を行う
	- Alice向けの暗号文をBob向けの暗号文に変換する
	- Aliceの秘密鍵はBobには渡さない
- Dodis and Ivan曰く
	- 復号権の委任 = 異なる秘密鍵を用いた2段階の復号手続きを持つ暗号システム作ること
	- つまりAliceとBobの秘密鍵を用いる暗号

---
## Identity-based Encryption(IBE)
- ID情報(任意の文字列)を公開鍵として扱うことができる公開鍵暗号の一種
	- RSA方式でも実現可能だが実用的ではない
	- ペアリングが登場して流行?
- 鍵配送問題の
- 鍵生成局が持つマスターシークレットをシステム全体の秘密鍵とする

--
## 普通の公開鍵暗号
- EC Elgamal方式
- 秘密鍵生成は受信者
- 公開鍵は$sP$だと送信する必要がある
<center>![Block](/home/b1012104/Pictures/Study/IBE/PKC.png)</center>

--
## IBE
<center>![Block](/home/b1012104/Pictures/Study/IBE/IBE.png)</center>

--
## IBE
- 秘密鍵生成は鍵生成局
- マスターシークレットを含んだ情報を共有することで受信者が秘密鍵を作る必要はなくなり、一つの秘密情報で困難性を確保している
- $P_A$はAliceのIDに対応している
	- Map to Pointによって任意の文字列を楕円曲線上の一点に対応付けることができる

---
## 電子書籍
- LCP
	- 著作権管理のための規格
	- 出版社は重いDRMでユーザに負担をかけるかノーガードで著作権管理を諦めるかの板ばさみ状態だった
	- 妥協点として軽いDRMを開発: LCP

---
## LCPの暗号に関する規程
- 最低一段階のファイルに対する暗号化は必要
	- おそらく共通鍵暗号をさしている
	- ここでは, 以降コンテンツ保護のための共通鍵をコンテンツキーと呼ぶ
- 最低AES 128bitを使え(つまり256でも可)
- コンテンツキーの暗号化に公開鍵暗号もほぼ必須扱い(RSA-1024ぐらい安価でECC-NIST-256くらい効率的なものが求められる)
- key hidingは実装者依存
- 鍵の失効はサポートされません

---
## EPUB LCPの問題点
- 暗号に関する規程が曖昧過ぎる
	- 実装者依存
	- とにかく暗号化しろ?
- 貸し借りや共有が貧弱
	- パスワードを渡すことで解決?
	- 本当に解決してるのか?
	- 現実的なのか？
- 頭を悩ます事が多い

---
## 今回の研究
- 新たなPREの応用
	- LCPに基づいた電子書籍の貸し借り
	- PREの性質から安全なコンテンツの受け渡しも実現できる
- コンテンツキーが分からないという状況に置いてはPREは貸し借りに向いている

---
## 必要なPREの性質
- Single-use
	- 一つの暗号文に対して一度のみの再暗号化を許す
- Unidirectionality
	- 単方向性
- non-Interactivity
	- 非対話性: 再暗号化鍵は一人で作れる

---
## 今後の予定
- PREを使った貸し借りシステムの実装
- 論文の執筆
