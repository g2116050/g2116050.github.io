## 株式会社HARP 一次選考<br>プレゼンテーション

吉田 努  
  
2017/05/17  

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
## 目次
- 自己紹介
- エピソード
	- 大学生
	- 大学院生
- 志望動機
- 将来の展望

---
## 自己紹介
- 吉田 努
- 学歴
	- 北海道石狩南高等学校 卒業
	- 公立はこだて未来大学 卒業
	- 公立はこだて未来大学大学院 卒業見込み
- 研究
	- 高機能暗号の応用
- 趣味
	- 将棋
	- 筋力トレーニング

---
## エピソード

---
## 大学生時代
- 1, 2年生を漠然と過ごす
	- 漠然とSEになるものかと思っていた
	- 進学も考えていなかった
	- 元々セキュリティ関連をやりたいと考えていた
- 3年次
	- Linuxをメインで使い始める
	- O'Reillyなどの技術書を読み始める <!--' -->
		- C, Shell script, Linuxなど
	- PBLにおいて素因数分解プロジェクト
- 4年次
	- 卒業研究

---
<section data-background="/images/ecmnet.png" style="font-size:40px">
## 素因数分解プロジェクト
- 目的
	- 巨大な素因数を発見し、ランキングに掲載される
	- RSA暗号の安全性評価にもなる
- 設立初年度
	- ノウハウなどがない
-  理論班とプログラミング班

---
## 素因数分解プロジェクト
- 前半
	- 基礎学習
- 後半
	- プロトタイプ作成
	- 素因数分解プログラム作成
	- プログラムの並列化
	- プログラムの稼働
- プログラミング班のリーダ的立場
	- 他に出来る人がいなかった

--
## プロトタイプ作成
- 動機
	- 貢献したいという気持ちが強かった
	- 純粋に楽しかった
- とりあえず動作するプログラムを作成
- 不完全な実装
- メンバーには喜んでもらえた
<center>![Block](/images/funecm.png)</center>

--
## 素因数分解プログラム作成
- 素因数分解アルゴリズムの実装
	- Linux | C言語 | GMP Library | OpenMP
- インターンシップで学んだ経験を反映
	- 仕様書
	- コーディング規約
- ペアプログラミング
	- 不慣れな人もいたため
- アルゴリズムの資料作成
	- 情報共有

--
## プロジェクトの学び
- 学習コスト
	- 有期的なプロジェクトにおいては致命的になる
	- 勉強だけで終わってしまう
- 協働作業の難しさ
	- モチベーションのギャップ
	- 意外と積極的に動いてはくれない

---
<section data-background="/images/ec.png">
## 卒業研究(4年次)
- 白勢研究室を選択
	- 暗号がテーマ
	- 公開鍵暗号, 楕円曲線
- 理由
	- PBLが楽しかった
	- 純粋な興味
	- 素因数分解で学んだことを活かせそう

---
## 卒業研究(4年次)
- 数学の基礎が足りない
	- 代数学
	- 楕円曲線</br>などを学び始める
- 基本的な暗号を学ぶ
	- 共通鍵暗号(AES, DESなど)
	- 公開鍵暗号(RSA, DH鍵共有など)

---
## 卒業研究
- 基本的に一人
- 方針が立たない
- 新規性が必要
- 学んでいるだけでは研究にはならない

--
## 共通鍵暗号の並列化
<center>![Block](/images/parallel1.png)</center>

--
## IDベース鍵共有の実用性の検討
### $e: E[n] \times E[n] \rightarrow \mu_n$
### $e(aP, bQ) = e(P, Q)^{ab}$
- ペアリングについて学ぶ
- 結果的に納得のいく研究は出来なかった

---
## 大学院
- 不安を抱えながら進学
	- 卒業研究の失敗
- 苦労したものの何とか一本論文を投稿
	- Proxy Re-Encryptionを用いたデジタルコンテンツの共有法
- 現在もう一つの研究を進めている
	- ペアリング逆計算問題に基づく電子署名の構成可能性の検討

--
## 学部・大学院での学び
- 自発的に行動する力
	- 論文
	- 不十分な点を学習
- 継続することの重要性

---
## 志望動機

--
## HARPとの関わり
- 平成26年度 戦略的基盤技術高度化支援事業(サポイン事業)
	- HARP
	- テクノフェイス
	- 流研
- 公立はこだて未来大学にて行われた会議に出席
- 白勢先生から内情を少し聞いたりする

--
## 志望動機
- 安全で便利な電子自治体の実現に暗号技術が貢献できる
	- タイムスタンプ
	- 高機能暗号による新たなサービス
- 個人の裁量が大きい
	- Grucco
	- Pepper
- 札幌での勤務希望

---
## 将来の展望

--
## 短期的な展望
- タイムスタンプの調査
	- 技術仕様
	- 自治体の需要
	- 日本データ通信協会の認定基準
- 暗号のみならず様々な技術を身につけていきたい
	- javascript? Ruby? Python? 現場で必要なもの

--
## 長期的な展望
- 自治体向けの新たなサービスの創出
- 技術の進歩に取り残されないようにする
