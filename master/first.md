## ツールを使いこなす

吉田 努  
  
白勢研ゼミ 2016/04/18  

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
- linux
- git
- pari/gp

---
## linux (1/2)
- あると便利
- terminalが使える
- プログラミング環境として良い?
	- IDE vs Editor

---
## linux (2/2)
- 親しみのあるコマンドラインプログラム
	- ls
	- cat
	- ecm
	- git
	- tex
	- gp

---
## Git とは
- VCS (Version Control System)
- Linux開発者リーナス・トーバルズ氏が核となる部分を開発
- バザール方式で開発される

---
## Git の意味
- (英俗)馬鹿者, ろくでなし(Weblioより)
- Git: Global Information Tracker
    - 後付けの意味

---
## なぜ版管理が必要か
- 版管理
    - 変更日時, 変更箇所などを保存し, 変更内容の確認や変更前の状態に復元することができる
    - オープンソースでは複数の人間が複数のファイルを編集する
    - プログラム開発には必要不可欠なものとなっている

---
## Git 活用
- 文章ならOK
    - ソースコード
    - texファイル  
    などなど

---
## 基本的な使い方
- 追跡したいファイルを 'add' して登録する
    - add することで, index にステージされる
- 変更を 'commit' して確定する
    - commitすることで変更が記録される

---
## Git の特徴
- ファイル名を追跡しない
    - ファイルのハッシュ値のみを追跡する!
    - gitはファイルの内容のみを気にする

---
## ブランチ
- 開発ライン
    - デフォルトブランチがmasterブランチ
    - masterブランチから新たなブランチを作成する

---
## Git と暗号
- Git はファイルの内容のハッシュ値でファイルを追跡している
    - ハッシュの性質をうまく利用!
    - SHA-1
- ファイルが同じならばハッシュは一致する

---
