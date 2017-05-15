### タイムリリース暗号を利用した  
### デジタルコンテンツのための  
### 事前配信システムの提案
<!-- A Proposal of Pre-distribution System for Digital Contents Using Timed-release Cryptography -->

白勢研究室
  
2116050  吉田 努  
  
2016/7/28  

<style type="text/css">
	.reveal table {
		font-size: 80%;
	}?
</style>

<style type="text/css">
.reveal section img {
  margin: 15px 0px;
  border: 0px;
  box-shadow: 0 0 0px rgba(0, 0, 0, 0);
}
</style>

---
## 目次
- 背景
- 目的
- 関連研究
- 研究手段
- 研究経過
- スケジュール
- まとめ
- 参考文献

---
## 背景(1/2)
- PCやタブレットの普及
- デジタルコンテンツ
	- 電子書籍
	- ゲーム
	- 映像
	- 音楽

--
## 背景(2/2)
<img src="/home/b1012104/Pictures/Study/TRE/server.png" width="50%" height="50%">
- コンテンツリリース時
	- サーバの負荷増
	- ユーザの負担増

--
## タイムリリース暗号によって解決できるのでは

---
## タイムリリース暗号
- タイムリリース暗号とは
	- 時間指定(未来)で暗号文を復号することができる暗号
- 普及していない暗号の一つ

---
## 具体例
- AさんからBさんにタイムリリース暗号を用いて暗号文を送信したい
<center>![Block](/home/b1012104/Pictures/Study/TRE/TRE1.png)</center>

--
## 具体例
<center>![Block](/home/b1012104/Pictures/Study/TRE/TRE2.png)</center>

---
## 目的
- タイムリリース暗号でデジタルコンテンツを暗号化
- デジタルコンテンツの事前配信
	- コンテンツリリース時のサーバの負担を減少させる
	- ユーザの負担を削減

---
## 関連研究
- タイムリリース暗号
	- time-lock puzzle
	- trusted server
	- pairing<!-- .element: class="fragment highlight-blue"-->

---
## Time-lock puzzle
- 数学的に計算時間がかかる問題を送信
	- 素因数分解など
- 受信者は計算することで復号可能

--
## Time-lock puzzle
<center>![Block](/home/b1012104/Pictures/Study/TRE/time-lock puzzle.png)</center>

--
## Time-lock puzzle
- 非実用的なシステム
	- 正確な復号時刻
	- 計算資源

---
## Trusted Server
- 公開鍵と共通鍵のペアを利用
- サーバを介してメッセージを暗号化
- タイムサーバ
	- 共通鍵暗号の鍵を定期的に送信

--
## Trusted Server
<center>![Block](/home/b1012104/Pictures/Study/TRE/trusted server2.png)</center>

--
## Trusted Server
<center>![Block](/home/b1012104/Pictures/Study/TRE/trusted server.png)</center>

---
## Pairing
- 楕円曲線上で定義される双線形写像
	- 公開鍵暗号を拡張したような暗号を構成可能
	- pairingを用いた高機能暗号が数多く考案されている
	- pairingを用いたタイムリリース暗号もその一つ
- 送信者とタイムサーバとの間でやりとりを一度行う
- スケーラビリティと匿名性と言う点で優れている

--
## Pairing
<center>![Block](/home/b1012104/Pictures/Study/TRE/pairing.png)</center>

---
## 研究手段
- ペアリングを用いたタイムリリース暗号
- システムの設計
	- セキュリティパラメータなどの決定
- タイムサーバ/クライアントの構築
- Pairingライブラリ
	- Tepla
	- PBC

---
## 研究経過
- Pairingの学習
- タイムリリース暗号の学習
- TeplaやPBCの習得

---
## スケジュール
- 8 - 9月 システム設計
- 10 - 12月 プロトタイプを実装
- 12月- 発表準備

---
## まとめ
- デジタルコンテンツの普及
- デジタルコンテンツの事前配信の需要があるのでは
	- サーバの負荷軽減
	- ユーザの負担を解消
- pairingを利用したタイムリリース暗号

---
## 参考文献
- Chan, AC-F., and Ian F. Blake. "Scalable, server-passive, user-anonymous timed release cryptography." 25th IEEE International Conference on Distributed Computing Systems (ICDCS'05). IEEE, 2005.<!-- ' -->
- 光成 滋生, "クラウドを支えるこれからの暗号技術." 秀和システム, 2015

---
### ご清聴ありがとうございました
