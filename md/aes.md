## AES

吉田 努  
  
白勢研ゼミ 2015/07/31  

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
- 有限体
    - 多項式でも整数のように計算ができる
    - $GF(2^n)$はコンピュータでよく利用されている
- AESを理解するには少しの有限体の知識が必要だったので...

---
## 今日の内容
- 共通鍵暗号
- AESとは
- AESのアルゴリズム
    - AddRoundkey
    - SubBytes
    - ShiftRows
    - MixColumns
- 有限体の乗算

---
## 共通鍵暗号
- 暗号化と複合の鍵が同じ暗号
- 実際には暗号利用モードを選択する必要がある
    - ECB mode
    - CBC mode
    - CTR mode  
    などなど
- ブロックごとに暗号処理をするアルゴリズム
    - AES
    - DES

---
## Confusion と Diffusion
- シャノンの情報理論
- 普通のブロック暗号はこの2つに基づいて設計されている

---
## Confusion
- 混乱
- 暗号文の統計的分布の平文の分布への依存の仕方が非常に複雑なこと

---
## Diffusion
- 拡散
- 平文の個々の各ビットや鍵の各ビットが暗号文の可能な限り多くのビットに影響を及ぼすこと

---
## AES(Advanced Encryption Standard)
- アメリカ国立標準技術研究所(NIST)による選考(1997)
    - "Advanced"というくらいなのでDESの後継として募集された
- ラインダール(Rijndael)暗号が申請される
    - RijmenさんとDaemenさんにちなんだ名称
- ラインダール暗号の特殊な場合をAESとして正式に採用された(2001)
    - AES $\subset$ ラインダール

---
## AESで必要な記号
- Nb
    - 平文ブロックと暗号文ブロックはNb個の32bitの語からなる
    - AESではNb = 4
        - AESのブロック長は128bitである
- Nk
    - 鍵はNk個の32bitの語からなる
    - AESではNk = 4, 6, 8
    - つまり, 鍵長は128bit, 192bit, 256bitの3種類
- Nr
    - 巡回の回数
    - AESではNr = 10(Nk = 4), 12(Nk = 6), 14(Nk = 8)

---
## state
- 平文と暗号文の状態を4行4列の配列で表す
- 1つの要素の大きさはbyte
- Column-major order
    - つまり列から先に数える
- $state : \begin{bmatrix\}s\_\{0,0\} & s\_\{0,1\} & s\_\{0,2\} & s\_\{0,3\} \\\\ s\_\{1,0\} & s\_\{1,1\} & s\_\{1,2\} & s\_\{1,3\} \\\\ s\_\{2,0\} & s\_\{2,1\} & s\_\{2,2\} & s\_\{2,3\} \\\\ s\_\{3,0\} & s\_\{3,1\} & s\_\{3,2\} & s\_\{3,3\} \end\{bmatrix\}$  

こんなこと参考文献には一切書いてませんでした...<!-- .element: class="fragment" data-fragment-index="1" -->

---
## byteとword
- byte
    - 1バイトのデータ構造
- word
    - 4バイトのデータ構造
    - byte4つ分

---
## byteと$GF(2^8)$の元の同一視
- $byte\ b\ =\ (0, 0, 0, 0, 0, 0, 1, 1)$は元$\alpha + 1$に対応する
- $byte\ b\ =\ (1, 0, 0, 0, 0, 0, 0, 0)$は元$\alpha^7$に対応する

---
## AESのアルゴリズム
- KeyExpansion
    - 鍵を伸長鍵に拡張する
- Cipher
    - 暗号化を実行する本体
    - 以下の処理が実行される
        - AddRoundkey
        - SubBytes
        - ShiftRows
        - MixColumns
- InvCipher
    - Cipherの逆変換を行う

---
## KeyExpansion
- 鍵をラウンド数の分だけ拡張する
- 鍵空間を128bitとすると
    - Nr(ラウンド数)=10
    - $128 \times 11$の伸長鍵に拡張される
        - word: $( 1word \times  4) \times 11$
        - byte: $( 1byte \times 16) \times 11$
    - 最初の128bitは入力された鍵その物

---
## KeyExpansionで行う変換
- SubWord
    - SubBytesによる変換をWord全体に行う
    - $(b_0, b_1, b_2, b_3)\ =\ (Ab_0^\{-1\}, Ab_1^\{-1\}, Ab_2^\{-1\}, Ab_3^\{-1\})$
- RotWord
    - Rotate Word(多分)
    - 左に1byteの巡回シフト
    - $(b_0,\ b_1,\ b_2,\ b_3)\ =\ (b_1,\ b_2,\ b_3,\ b_0)$
- Rcon[i]
    - $x ^ \{(i-1)\}$で計算される値
    - AESではiは最高10まで

---
## KeyExpansionの擬似コード

```
KeyExpansion(byte key[4*Nk], word w[Nb*(Nr+1)], Nk)
begin
    word temp
    i = 0
    while (i < Nk)
        w[i] = word(key[4*i], key[4*i+1], key[4*i+2], key[4*i+3])
        i = i + 1
    end while
    i = Nk
    while (i < Nb * (Nr+1)]
        temp = w[i-1]
        if (i mod Nk = 0)
            temp = SubWord(RotWord(temp)) xor Rcon[i/Nk]
        else if (Nk > 6 and i mod Nk = 4)
            temp = SubWord(temp)
        end if
        w[i] = w[i-Nk] xor temp
        i = i + 1
    end while
end
```

---
## Cipher
- 実際に暗号処理を行う
- Cipherで行われる変換
    - AddRoundkey
    - SubBytes
    - ShiftRows
    - MixColumns

---
## AddRoundKey
- 伸長鍵とstateを混ぜる
- stateの縦の列1word分と伸長鍵の1ワード分のxor

---
## SubBytes
- 既約多項式: $m(x)\ =\ x^8+x^4+x^3+x+1$
- S-Boxによる変換をすべてのバイトに適用する
    - state全体に適用するということ
- $b = Ab^\{-1\}+c$

---
## S-Box
- $ b = \begin\{bmatrix\} 1 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \\\\ 1 & 1 & 0 & 0 & 0 & 1 & 1 & 1 \\\\ 1 & 1 & 1 & 0 & 0 & 0 & 1 & 1 \\\\ 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \\\\ 1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\\\ 0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\\\ 0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 \\\\ 0 & 0 & 0 & 1 & 1 & 1 & 1 & 1\end\{bmatrix\} b^\{-1\} \bigoplus \begin{bmatrix\}1 \\\\ 1 \\\\ 0 \\\\ 0 \\\\ 0 \\\\ 1 \\\\ 1 \\\\ 0\end\{bmatrix\}$

---
## 参考文献への批判: S-Box
- 参考文献のS-Boxは間違っていた

---
## ShiftRows
- 各行に対して巡回左シフトを適用する
- 1行目は0, 2行目は1, 3行目は2, 4行目は3

- $\begin{bmatrix\}s\_\{0,0\} & s\_\{0,1\} & s\_\{0,2\} & s\_\{0,3\} \\\\ s\_\{1,0\} & s\_\{1,1\} & s\_\{1,2\} & s\_\{1,3\} \\\\ s\_\{2,0\} & s\_\{2,1\} & s\_\{2,2\} & s\_\{2,3\} \\\\ s\_\{3,0\} & s\_\{3,1\} & s\_\{3,2\} & s\_\{3,3\} \end\{bmatrix\} = \begin{bmatrix\}s\_\{0,0\} & s\_\{0,1\} & s\_\{0,2\} & s\_\{0,3\} \\\\ s\_\{1,1\} & s\_\{1,2\} & s\_\{1,3\} & s\_\{1,0\} \\\\ s\_\{2,2\} & s\_\{2,3\} & s\_\{2,0\} & s\_\{2,1\} \\\\ s\_\{3,3\} & s\_\{3,0\} & s\_\{3,1\} & s\_\{3,2\} \end\{bmatrix\} $

---
## MixColumns
- 文字通り列を混ぜる
    - 多項式との積を混ぜ合わせる
    - $a_i$ はstateの列に対応

- $\begin\{bmatrix\}b_0 \\\\ b_1 \\\\ b_2 \\\\ b_3 \end\{bmatrix\} = \begin{bmatrix\}2 & 3 & 1 & 1 \\\\ 1 & 2 & 3 & 1 \\\\ 1 & 1 & 2 & 3 \\\\ 3 & 1 & 1 & 2 \end\{bmatrix\} \begin{bmatrix\}a_0 \\\\ a_1 \\\\ a_2 \\\\ a_3 \end\{bmatrix\}  $

---
## Cipherの擬似コード
    Cipher(byte in[4, Nb], byte out[4, Nb], word w[Nb*(Nr+1)])
    begin
        byte state[4, Nb]
        state = in
        AddRoundKey(state, w[0, Nb-1])
        for round = 1 step 1 to Nr-1
            SubBytes(state)
            ShiftRows(state)
            MixColumns(state)
            AddRoundKey(state, w[round*Nb, (round+1)*Nb-1])
        end for
        SubBytes(state)
        ShiftRows(state)
        AddRoundKey(state, w[Nr*Nb, (Nr+1)*Nb-1])
        out = state
    end

---
## 有限体の計算
- 有限体の計算を実際に行うのはナンセンス
    - 計算コスト
- 変換テーブルを用意する
    - S-Boxによる変換を先に用意しておく
    - $GF(2^8)$なので元の個数は$2^8$個
    - 256個の要素を持つテーブルを用意すればよい

---
## 掛け算の仕方
- $m(x)\ =\ x^8+x^4+x^3+x+1 = (1, 0 0 0 1, 1 0 1 1)$
    - $\alpha^8\ =\ \alpha^4 + \alpha^3 + \alpha^1 + 1$
    - 8桁を越えたものの指数を落としていけば良い
- 7bit * 7bit は14bit
    - 1byteじゃ足りない
- 例
    - $(1, 0 0 0 0, 0 0 0 1):\ 0x101$
        - $(0 0 0 1, 1 0 1 1)\ xor\ (0 0 0 0, 0 0 0 1)$<!-- .element: class="fragment" data-fragment-index="1" -->
        - $(0 0 0 1, 1 0 1 0)$<!-- .element: class="fragment" data-fragment-index="2" -->
        - 0x1a<!-- .element: class="fragment" data-fragment-index="3" -->

---
## 皆さんはどう計算しますか?

---
## 実例1
    byte↲
    mul(byte a, byte b)↲
    {↲
        unsigned int i, j, x = 0;↲
        for (i = 0, j = 1; i < 8; i++, j <<= 1) {↲
            if (b & j)↲
                x ^= a << i;↲
        }↲
        while (x >> 8) {↲
            for (i = 8, j = 256; i < 16; i++, j <<= 1) {↲
                if (x & j) {↲
                    x ^= j;↲
                    x ^= (0x1b << (i - 8));↲
                }↲
            }↲
        }↲
        return (byte)x;↲
    }


---
## 実例2
    byte
    mul(byte a, byte b)
    {
        unsigned short int i, j, val = 0;
        for (i = 0, j = 1; i < 8 ; i++, j <<= 1)
            if (b & j)
                val ^= (a << i);

        if (val >> 8) {
            if (val & 0x0100U)
                val ^= 0x1b;
            if (val & 0x0200U)
                val ^= 0x36;
            if (val & 0x0400U)
                val ^= 0x6c;↲
            if (val & 0x0800U)
                val ^= 0xd8;↲
            if (val & 0x1000U)
                val ^= 0xab;↲
            if (val & 0x2000U)
                val ^= 0x4d;
            if (val & 0x4000U)
                val ^= 0x9a;
        }
        return (byte)val;
    }

---
## 逆元計算
- 有限体でも整数と同様に逆元計算をすることができる
    - 拡張ユークリッド互助法
- しかし面倒くさい
    - 256個しか元がない
    - 掛けて1になったら逆元
##    
  
### 手抜きが可能!<!-- .element: class="fragment" data-fragment-index="1" -->

---
## 手抜きで逆元テーブル作成
    int
    main()
    {
        unsigned int i, j;

        printf("0x00, ");
        for (i = 1; i < 256; i++) {
            for (j = 1; j < 256; j++) {
                if (mul(i, j) == 0x01) {
                    printf("0x%02x,%c", j, (i+1) % 8 == 0 ? '\n' : ' ');
                    break;
                }
            }
        }
    }

---
## 逆元テーブル
    byte inv[] = {
        0x00, 0x01, 0x8d, 0xf6, 0xcb, 0x52, 0x7b, 0xd1,
        0xe8, 0x4f, 0x29, 0xc0, 0xb0, 0xe1, 0xe5, 0xc7,
        0x74, 0xb4, 0xaa, 0x4b, 0x99, 0x2b, 0x60, 0x5f,
        0x58, 0x3f, 0xfd, 0xcc, 0xff, 0x40, 0xee, 0xb2,
        0x3a, 0x6e, 0x5a, 0xf1, 0x55, 0x4d, 0xa8, 0xc9,
        0xc1, 0x0a, 0x98, 0x15, 0x30, 0x44, 0xa2, 0xc2,
        0x2c, 0x45, 0x92, 0x6c, 0xf3, 0x39, 0x66, 0x42,
        0xf2, 0x35, 0x20, 0x6f, 0x77, 0xbb, 0x59, 0x19,
        0x1d, 0xfe, 0x37, 0x67, 0x2d, 0x31, 0xf5, 0x69,
        0xa7, 0x64, 0xab, 0x13, 0x54, 0x25, 0xe9, 0x09,
        0xed, 0x5c, 0x05, 0xca, 0x4c, 0x24, 0x87, 0xbf,
        0x18, 0x3e, 0x22, 0xf0, 0x51, 0xec, 0x61, 0x17,
        0x16, 0x5e, 0xaf, 0xd3, 0x49, 0xa6, 0x36, 0x43,
        0xf4, 0x47, 0x91, 0xdf, 0x33, 0x93, 0x21, 0x3b,
        0x79, 0xb7, 0x97, 0x85, 0x10, 0xb5, 0xba, 0x3c,
        0xb6, 0x70, 0xd0, 0x06, 0xa1, 0xfa, 0x81, 0x82,
        0x83, 0x7e, 0x7f, 0x80, 0x96, 0x73, 0xbe, 0x56,
        0x9b, 0x9e, 0x95, 0xd9, 0xf7, 0x02, 0xb9, 0xa4,
        0xde, 0x6a, 0x32, 0x6d, 0xd8, 0x8a, 0x84, 0x72,
        0x2a, 0x14, 0x9f, 0x88, 0xf9, 0xdc, 0x89, 0x9a,
        0xfb, 0x7c, 0x2e, 0xc3, 0x8f, 0xb8, 0x65, 0x48,
        0x26, 0xc8, 0x12, 0x4a, 0xce, 0xe7, 0xd2, 0x62,
        0x0c, 0xe0, 0x1f, 0xef, 0x11, 0x75, 0x78, 0x71,
        0xa5, 0x8e, 0x76, 0x3d, 0xbd, 0xbc, 0x86, 0x57,
        0x0b, 0x28, 0x2f, 0xa3, 0xda, 0xd4, 0xe4, 0x0f,
        0xa9, 0x27, 0x53, 0x04, 0x1b, 0xfc, 0xac, 0xe6,
        0x7a, 0x07, 0xae, 0x63, 0xc5, 0xdb, 0xe2, 0xea,
        0x94, 0x8b, 0xc4, 0xd5, 0x9d, 0xf8, 0x90, 0x6b,
        0xb1, 0x0d, 0xd6, 0xeb, 0xc6, 0x0e, 0xcf, 0xad,
        0x08, 0x4e, 0xd7, 0xe3, 0x5d, 0x50, 0x1e, 0xb3,
        0x5b, 0x23, 0x38, 0x34, 0x68, 0x46, 0x03, 0x8c,
        0xdd, 0x9c, 0x7d, 0xa0, 0xcd, 0x1a, 0x41, 0x1c
    }

---
## 他の部分
- S-Boxのテーブルも作成可能
- MixColumnsの掛け算もテーブルで用意可能
- AddRoundKeyは展開可能
- byte order  
<center>などなど結構考える事が多い...</center>

---
## 教訓
- 一つの情報に対して, 複数のソースを確認する
- 情報源が書籍だからと言って信じすぎない

---
## 参考文献
- 暗号理論入門
- Wikipedia AES
