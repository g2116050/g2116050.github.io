## Git

吉田 努  
  
白勢研ゼミ 2016/06/28  

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
- 群(部分群)
- 部分群

---
## 今回
- Git
	- VCS
	- gitとは

---
## VCS
- Vesion Contol System(VCS)
	- 版管理
	- 前のバージョンに戻したい
	- いつバグが混入したか探る
	- いろいろな場面で利用できそう
		- 卒論
		- システム開発
		- 社会人

---
## Gitとは
- DVCSの一種
	- Distributed VCS
	- 分散型のVCS
- リーナスさんが開発
- 昔は集中管理していた
	- Concurrent Versions System
	- Subversion

---
## Git用語

---
## リポジトリ
- 施された変更をVCSが追跡する場所
- git initで作成する
	- .git ディレクトリ
- 分散型リポジトリ
	- プロジェクト全体の履歴を保持
	- 全員がリポジトリを持つ

--
## 集中型リポジトリ
<center>![Block](/home/b1012104/Pictures/Study/seminar/VCS.png)</center>
- リポジトリを集中管理
- 厳格なロック

--
## 分散型リポジトリ
<center>![Block](/home/b1012104/Pictures/Study/seminar/DVCS.png)</center>
- 各人がリポジトリを持つ
- リモートリポジトリにプッシュとプル
- ロックではないがプッシュを拒否されることがある

---
## コミット
- ある時点でのスナップショット
	- 変更を記録する
	- ある区切りでコミットを行う
- リポジトリにコミットが置かれる
- 多分親と子を持つ
- SHA-1ハッシュ値を持つ

--
## どんなときにコミットをするか
- 機能が完成したとき
- 区切りがついたとき
- 後でまとめればいいや…
	- いつでもok

--
## コミットのコメント
- コミットごとにコメントを書くことができる
- そのコミットで何を変更したか, 追加したか
- 自明すぎることは書かない
- 後日見たときにわかりやすいコメントを

---
## データを保持する場所(1/2)
1. 作業ツリー
	- ディレクトリの中身
	- 自分から見えるリポジトリの現在の姿
2. インデックス or ステージングエリア
	- リポジトリと作業ツリーの間
	- キャッシュ
3. リポジトリ
	- 最終的な保管場所

--
## データを保持する場所(2/2)
<center>![Block](/home/b1012104/Pictures/Study/seminar/place.png)</center>

---
## 基本的な使い方
- add
	- 変更したファイルをステージングする
	- ステージングエリアに登録後コミットする
- commit
	- 変更を確定する
	- 変更を履歴として残す
- branch
	- ブランチを作る
	- ブランチを削除する
- merge
	- ブランチ間の変更履歴を統合する

---
## ブランチ
- branch(枝)
- 変更の異なる歴史
- 最初にできるブランチはmaster
<center>![Block](/home/b1012104/Pictures/Study/seminar/branch.png)</center>

--
## なぜブランチを使うか
- 変更の履歴が一つでは不便
- 機能毎に開発ラインを分けたい
- 試しに作ってみたい

--
## ブランチ間で変更を統合したい
- マージする
	- 直接マージ
	- 圧縮マージ
	- チェリーピック

---
## 差分を見る
- 今回の変更を知りたい
- あの時何を変更したか知りたい


	$ git diff // ステージングエリアと作業ツリー
	$ git diff --cached // ステージングエリアとリポジトリ
	$ git diff HEAD // 作業ツリーとリポジトリ

---
## 使ってみての感想
- 結構便利?
	- 一区切り毎にコミット
	- 過去のバージョンに戻せる
- 慣れないと果てしなく使い辛い
	- 過去のコミットの修正
	- システムの理解

---
## おまけ
- ログ


	* commit 2bfa44215832eae8b4fd8623e62cdef08a9fe6ef
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Sun Jun 26 19:03:14 2016 +0900
	|
	|     add omake
	|
	* commit 0f1c2e0ee62bfb24e7115fe226eb0512a68ef712
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Sun Jun 26 16:51:49 2016 +0900
	|
	|     add commit
	|
	* commit 303447a37fdabbce8c993bfb2fea3ce9b29bfcd1
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Fri Jun 24 17:49:03 2016 +0900
	|
	|     add branch
	|
	* commit a13fd2e3c9c98606310c212cf5dd516bd9dd295c
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Fri Jun 24 22:18:43 2016 +0900
	|
	|     add git-diff
	|
	* commit f6da15929da7dc664d0398bd7227ccbe00ba2b92
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Fri Jun 24 00:21:12 2016 +0900
	|
	|     add basic usage
	|
	* commit f848107905b67a01bd2607b873efabd319dc6f25
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Thu Jun 23 23:45:38 2016 +0900
	|
	|     add data structure
	|
	* commit 6e26c7c5aba2e3b3c387961e694ac7e93563e2f5
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Thu Jun 23 23:17:55 2016 +0900
	|
	|     add ripository
	|
	* commit 556e495af7503ae6e221bd9095e3a11ba817035c
	| Author: b1012104 <b1012104@fun.ac.jp>
	| Date:   Thu Jun 23 22:18:28 2016 +0900
	|
	|     add VCS and What is Git?
	|
	* commit a2ef1c29da9d29d3e57c6102ec05e23207e73e14
	  Author: b1012104 <b1012104@fun.ac.jp>
	    Date:   Thu Jun 23 21:36:04 2016 +0900

		first commit
