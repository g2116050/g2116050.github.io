### AESの並列化による暗号処理の高速化

白勢研究室
  
1012104  吉田 努  
  
2015/08/10  

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
- 背景
- 暗号の概要
- 関連研究
- 目的
- 研究課題
- スケジュール
- まとめ
- 参考文献

---
## 背景(1/2)
- 公開鍵暗号の登場
- ハイブリッド暗号
    - 電子商取引など
  
## ↓<!-- .element: class="fragment" data-fragment-index="1" -->
### 暗号は必要不可欠<!-- .element: class="fragment" data-fragment-index="1" -->

---
## 背景(2/2)
- 暗号研究において高速化は重要
    - 時間が掛かりすぎると使い物にならない
    - 出来るだけ短時間で済ませたい
- デジタルコンテンツの多様化
    - 動画
    - 音楽
    - 画像

---
## そもそも暗号とは
- 情報を第3者に分からないような変換を施すこと
- 大きく分けて2種類
    - 共通鍵暗号
        - データ自体の暗号化
    - 公開鍵暗号
        - 共通鍵暗号で使う鍵の暗号化

---
## 共通鍵暗号方式
<center>![Block](/home/b1012104/Pictures/Study/presentation/key2.png)</center>
- 暗号化と復号の鍵が同じ暗号

---
## ブロック暗号
- AES
- DES
- 3DES
- ブロックごとに暗号処理を行う
<center>![Block](/home/b1012104/Pictures/Study/presentation/block.png)</center>
- 固定長(block size)のデータの暗号化<!-- .element: class="fragment" data-fragment-index="1" -->

---
## AES(Advanced Encryption Standard)
- アメリカ国立標準技術研究所(NIST)
- DESの後継
- 128bit単位で暗号処理を施す
<center>![Block](/home/b1012104/Pictures/Study/presentation/128bit.png)</center>
- ブロック長: 128 bit
- 鍵長      : 128 bit, 192 bit, 256 bit

---
## 暗号利用モード
- ブロック暗号のアルゴリズムを利用して暗号化を行う
- ECB mode
- CBC mode
- CTR mode
### ブロック暗号と暗号利用モードを組み合わせて暗号化を行う<!-- .element: class="fragment" data-fragment-index="1" -->

--
## ECB mode
<center>![ecb block](/home/b1012104/Pictures/Study/presentation/ecbblock.png)</center>

### ↓

<center>![mode](/home/b1012104/Pictures/Study/presentation/ecb.png)</center>

---
## ブロック暗号と暗号利用モード
<center>![mode](/home/b1012104/Pictures/Study/presentation/mode2.png)</center>
- 任意のブロック暗号で利用可能
- アルゴリズムの入れ替えが可能  

--
## 例
<center>![3des_cbc](/home/b1012104/Pictures/Study/presentation/mode_3des_cbc.png)</center>

### <center>↓</center><!-- .element: class="fragment" data-fragment-index="1" -->

<center>![aes_cbc](/home/b1012104/Pictures/Study/presentation/mode_aes_cbc.png)</center><!-- .element: class="fragment" data-fragment-index="1" -->

---
## 関連研究
- メニーコア・コプロセッサXeon Phiでの並列暗号実装[2]
    - ファイル単位で暗号処理を並列化
    - Xeon Phi vs Xeon

--
## 課題
- コア数が多いはずのXeon Phiの方が遅い

---
## 目的
### 並列化による暗号処理の高速化

---
## 準備状況
- 共通鍵暗号
- AESのアルゴリズムの理解
- AESのプログラミング

---
## 課題
- どう並列化するか

---
## 並列化
- ブロック単位の並列化
<center>![parallel1](/home/b1012104/Pictures/Study/presentation/parallel1.png)</center>

--
- AESの内部処理の並列化
<center>![parallel2](/home/b1012104/Pictures/Study/presentation/parallel2.png)</center>

--
- ファイル単位の並列化
    - 複数ファイルを処理する場合に限る
<center>![parallel3](/home/b1012104/Pictures/Study/presentation/parallel3.png)</center>

---
## 並列化対象
- どの部分の並列化を行うか検討中

---
## 並列化手法
- OpenMP
- Pthread
- その他の並列化基盤も検討

---
## OpenMP
- C, C++, FORTRAN
- Cの場合
    - \#pragma omp parallel for でforループを簡単に並列化可能
    - 比較的簡単

---
## Pthread
- POSIX thread
- 前述したOpenMPよりも複雑だが細かい指示が可能

---
## 今後の日程
<center>![schedule](/home/b1012104/Pictures/Study/presentation/schedule.png)</center>

---
## まとめ
- 共通鍵暗号はもっとも基本的な暗号方式で情報社会において必要不可欠
- AESの並列化を行い暗号処理にかかる時間を短縮する
- 並列化手法
    - OpenMP
    - Pthread

---
## 参考文献
[1] J.A.ブーフマン, 暗号理論入門, シュプリンガー・ジャパン株式会社(2007)  
[2] 白勢政明, メニーコア・コプロセッサXeon Phiでの並列暗号実装, 情報処理学会研究報告. マルチメディア通信と分散処理研究会報告 2015-DPS-162(27), 1-8 (2015)
