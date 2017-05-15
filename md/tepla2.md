## Tepla

吉田 努  
  
白勢研ゼミ 2015/11/20  

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
## Tepla
- 筑波大学が作成したペアリング演算ライブラリ
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
## 少し触ってみて...

---
## IDベース鍵共有を構築するのにあたって
- ペアリングさえ計算できれば中身は知らなくてもいい
	- もちろん多少は必要
- TEPLAを使いこなす必要がある

---
## TEPLAの仕様
- オブジェクト指向っぽい作り
	- 構造体と関数へのポインタで実現
	- 内部では, 関数?メソッド？は->(アロー演算子)で呼ぶ
- 楕円曲線上の点への変換関数がある!
	- これはうれしい
- ユーザが使うAPIはドキュメント付き
	- 素晴らしい!

---
## 点の変換
- 文字列
	- point_get_str(char *s, const EC_POINT P)
- バイト列
	- point_to_oct(unsigned char* os, size_t *size, EC_POINT P);
- どっちが良いでしょうか

---
## ペアリングの計算
- EC_PAIRING
	- PairingType type
	- EC_GROUP g1
	- EC_GROUP g2
	- Field    g3
	- これ何ですか...
- pairing_map(Element g, const EC_POINT P, const EC_POINT Q, const EC_PAIRING p)
	- ペアリング値を計算する

---
## 埋め込み
- 文字列を楕円曲線上の点に変換する
- point_map_to_point(EC_POINT P, const *s, size_t slen, int t)

---
## バグ?
- pairing_init()
- point_init()
- 上記の手順で実行すると
	- Segmentation fault
- なぜか

---
## 仕様?
- pairing_clear()の後にsegmentation fault
	- pairing_clear();
	- point_clear();
- point_clear()が怪しい

---
## 原因
- EC_POINTで呼び出されるメソッドがEC_GROUP依存だった
 1. pairing_clear()で, EC_GROUPのmethodを開放
 2. point_clear()で開放済みのmethodを参照
 3. NULL参照
 4. segmentation fault

---
## 考察(1/2)
- 鍵生成センター
	- 公開
		- 楕円曲線
		- 埋め込み関数
	- 非公開
		- 秘密鍵: スカラーs

---
## 考察(2/2)
- ペアリングはEC_PAIRING構造体により管理される
- ペアリングの種類はECBN254のみ
- 鍵生成センターが公開するまでもない?

---
## 誰が何をするか
- 鍵生成センター
	- s倍する
	- 返す
	- 鍵の変更
	- ユーザの認証
- ユーザ
	- 自身の公開鍵を作成
	- 自身の秘密鍵を受け取る
	- 相手の公開鍵を作成
	- ペアリング値の計算

---
## sample.cを読む

---
## 参考文献
- Tepla http://www.cipher.risk.tsukuba.ac.jp/tepla/index.html
