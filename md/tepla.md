## AES-NI と Tepla

吉田 努  
  
白勢研ゼミ 2015/10/07  

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
- AES-NI
    - インテルのCPUの拡張命令セット
    - AESの暗号化・復号処理が早くなる
- Tepla
    - 筑波大学が作成したペアリングを計算するためのライブラリ

---
## AES-NIの概要
- NI = New Instructions
- AESアルゴリズムの高負荷な処理の一部をハードウェア実装することで処理を高速化
- ソフトウェア実装によるテーブル参照方式のサイドチャネル攻撃を防ぐ

---
## AES-NIの詳細
- 6つの命令で構成
    - AESENC
    - AESENCLAST
    - AESDEC
    - AESDECLAST
    - AESKEYGENASSIST
    - AESIMC

---
## AESENC
- 暗号化の1ラウンドを行う
- AESの4つのステップが実行される
    - ShiftRows
    - SubBytes
    - MixColumns
    - AddRoundkey

---
## AESENCLAST
- 暗号化の最終ラウンドを行う
- MixColumns無し

---
## AESDEC
- AESENCとほぼ同様
- AddRoundkey以外は先頭にInvが付く
    - ex) InvShiftRows

---
## AESDECLAST
- AESENCLASTとほぼ同様
- 複号の最終ラウンドを行う
- InvMixColumnsが無い

---
## AESKEYGENASSIST
- ラウンド鍵(伸長鍵)を生成する

---
## AESIMC
- 暗号化ラウンド鍵を復号に便利な形に変換する
- ちょっとよく分からない?

---
## OpenSSLとAES-NI
- フォーラムによれば
    - OpenSSLではversion1.0.1からデフォルトでAES-NIが有効であるらしい
    - OpenSSLでAES-NIを無効にするには環境変数を変える必要がある？
        - OPENSSL_ia32cap=”~0×200000200000000″
    - AES-NIの効果は約2倍らしい

---
## Tepla
- 筑波大学が作成したペアリング演算ライブラリ
- University of <span style="color:red">T</span>sukuba <span style="color:red">E</span>lliptic Curve and <span style="color:red">P</span>aring <span style="color:red">L</span>ibr<span style="color:red">a</span>ry
    - 無茶苦茶だと感じるのは自分だけでしょうか
- C言語
- GMPとOpenSSLを必要とする
- 提供する機能
    - 有限体上の演算
    - 楕円曲線の演算
    - ペアリング演算

---
## 想像していたライブラリ
- いくつかのペアリングを利用した暗号が実装されている
- ペアリングを知らない人間でも使える

---
## 実際のTepla
- 暗号処理は提供されていない！
- ただペアリング演算を行う<span style="color:red">だけ</span>
- つまり
    - ペアリングを用いた暗号方式を実装するためのライブラリ
    - ペアリングを用いた暗号方式を扱うにはペアリングの知識が必要
    - 一般向けとは思えない

---
## 思い出してみると…
- 金岡さんの講演
    - 暗号技術は煩わしい、分かり辛い
    - 誰でも利用できる形で提供
    - 大丈夫．暗号は敵じゃない．

---
## PBC library
- Paring-Based Cryptography library
- GMPで構成されたフリーのCライブラリ
- 使用例を公開している
    - Paterson identity-based signatures
    - Joux tripartite Diffie-Hellman
    - Boneh-Lynn-Shacham short signatures

---
## Tepla と PBC
- Teplaは多分開発が止まっている
    - ver1.0
- PBCはまだ続いている
    - ver0.5.14

---
## 参考文献
- AES-NIについて http://stackoverflow.com/questions/25284119/how-can-i-check-if-openssl-is-support-use-the-intel-aes-ni
- PBC library https://crypto.stanford.edu/pbc/news.html
- Tepla http://www.cipher.risk.tsukuba.ac.jp/tepla/index.html
