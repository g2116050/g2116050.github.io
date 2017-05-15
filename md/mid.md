## IDベース鍵共有システムの実用性の検討

白勢研究室  
1012104 吉田 努  
2015/11/16  

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
## 背景
- そもそも暗号とは
    - 情報を第3者に分からないように変換を施すこと

---
## 共通鍵暗号
- 基本的な暗号
- 暗号と聞いて一番初めにイメージする?
- 比較的高速
<center>![Block](/home/b1012104/Pictures/Study/presentation/key2.png)</center>

--
## 代表例
- AES
- 3DES  
など

---
## 鍵配送問題

--
## 鍵配送問題(1/2)
<center>![Block](/home/b1012104/Pictures/Study/presentation/common key cryptosystem.png)</center>


--
## 鍵配送問題(2/2)
<center>![Block](/home/b1012104/Pictures/Study/presentation/key sharing.png)</center>

---
## 公開鍵暗号
- 暗号化と復号に用いる鍵が異なる
- 鍵配送問題の解決
- 認証や電子署名などの応用
- 比較的低速
<center>![Block](/home/b1012104/Pictures/Study/presentation/pkc.png)</center>

--
## 代表例
- RSA暗号
- エルガマル暗号
- <span style="color:red">楕円曲線暗号</span>  
など

---
## 楕円曲線
<center>![Block](/home/b1012104/tex/gradrepo/midterm/ec.png)</center>

--
## 楕円曲線暗号
- 数学的計算困難性を安全性の根拠としている
- 短い鍵長
- ~~次世代暗号~~
    - RSA暗号から移行が行われている

---
## 新しい暗号方式の誕生

--
## ペアリング
## (Pairing)

--
## ペアリングとは
- 楕円曲線上で定義される双線形写像
- 2入力1出力
    - 楕円曲線上の2点がある値に変換される
- 双線形性
    - $f(lP, Q) = f(P, lQ)= f(P, Q)^l$

---
## ペアリングを利用した暗号方式はまだ普及していない

---
## 関連研究

--
## IDベース鍵共有

--
## DH鍵共有(1/2)
- ある値$g$を二人で決める
- AliceとBobは乱数を各々用意する
    - Aliceの乱数: A
    - Bobの乱数: B

--
## DH鍵共有(2/2)
<center>![Block](/home/b1012104/Pictures/Study/presentation/easy DH key sharing.png)</center>

--
## IDベース鍵共有(1/3)
- ID情報は公開されているものとする
    - ID情報とはメールアドレスなどを言う
- 鍵生成センターが必要
- ID情報と個人の秘密鍵で鍵を作る


--
## IDベース鍵共有(2/3)
<center>![Block](/home/b1012104/Pictures/Study/presentation/easy ID-based key sharing.png)</center>

--
## IDベース鍵共有(3/3)
- $f(S\_A, ID\_B) = K\_{AB}$
- $f(ID\_A, S\_B) = K\_{BA}$
- 特徴
    - ID情報のみで鍵共有を行える
    - 2者間で通信が不要
    - ユーザの乱数生成が不要

---
## 目的
IDベース鍵共有システムを構築し,  
実用に耐えうるかどうかの評価を行う

--
## TEPLA
- 筑波大学が開発
- 数少ないペアリング演算ライブラリ
    - TEPLA(University of Tsukuba Elliptic Curve and Pairing Library)
    - PBC(Pairing-Based Cryptography Library)

--
## 評価
- 時間
    - 公開鍵暗号との比較
    - 実用的な時間に収まるかどうか
- システム
    - 改竄
    - なりすまし

---
## まとめ
- 暗号技術は情報社会で必要不可欠
- ペアリングを利用した暗号方式は日常的に利用されていない
- IDベース鍵共有システムを構築
- システムの実用性の評価を行う

---
## 参考文献
1.  J.A.ブーフマン, "暗号理論入門", シュプリンガー・ジャパン株式会社, 2007
2.  有田正剛, 境隆一, 只木孝太郎, 趙晋輝, 松尾和人, "暗号理論と楕円曲線-数学的土壌に花開く暗号技術-", 森北出版株式会社, 2008

---
## 楕円曲線
<center>![Block](/home/b1012104/tex/gradrepo/midterm/ec.png)</center>

--
## 楕円曲線の加算
<center>![Block](/home/b1012104/tex/gradrepo/midterm/ecadd5.png)</center>
### $P\ +\ Q\ =\ R$

--
## 楕円曲線のスカラー倍
- 点      : $P$
- スカラー: $l$
- $lP\ =\ \underbrace{P\ +\ P\ +\ \cdots\ +\ P }_{l個のP}$

--
## 楕円離散対数問題
### $lP\ =\ Q$
#### 2点$P, Q$が与えられたとき
#### スカラー倍の$l$を求めること

---
## IDベース鍵共有(1/4)
- ID情報は公開されているものとする
- 鍵生成センター
    - ID情報を楕円曲線上の点に変換する関数を公開しておく
    - この暗号システムで利用する秘密鍵$s$を設定

--
## IDベース鍵共有(2/4)
- ユーザ Alice, Bob
- パラメータ
    - ID情報: $ID_A, ID_B$
    - 公開鍵: $P_A, P_B$
    - 秘密鍵: $S_A, S_B$
        - $S_A = sP_A, S_B = sP_B$


--
## IDベース鍵共有(3/4)
<center>![Block](/home/b1012104/Pictures/Study/presentation/ID-based key sharing.png)</center>

--
## IDベース鍵共有(4/4)
- 正当性
    - $K_\{AB\} = e_n(S_A, P_B) = e_n(sP_A, P_B)\\\\ = e_n(P_A, P_B)^s$
    - $K_\{BA\} = e_n(P_A, S_B) = e_n(P_A, sP_B)\\\\ = e_n(P_A, P_B)^s$

---
## ペアリングとは
- 楕円曲線上で定義される双線形写像
- 2入力1出力
    - 楕円曲線上の2点が, ある有限体の元に対応する
- 双線形性
    - $e_n(lP, Q) = e_n(P, lQ)= e_n(P, Q)^l$
