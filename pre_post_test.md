# 事前・事後テスト内容

事前テストには**知識問題**と**診断問題**の2種類用意し，事前・事後テストにて同じ問題を使用した．

---

## 知識問題

ソートアルゴリズムの基礎知識に対する理解度を測る問題を用意した．

#### 問1.1
<div align="center">
    <img src="pictures\knowledge\exp1.png" border="1px">
</div>

#### 問1.2
<div align="center">
    <img src="pictures\knowledge\exp2.png" border="1px">
</div>

#### 問2
<div align="center">
    <img src="pictures\knowledge\exp3.png" border="1px">
</div>

#### 問3
<div align="center">
    <img src="pictures\knowledge\exp4.png" border="1px">
</div>

#### 問4
<div align="center">
    <img src="pictures\knowledge\exp5.png" border="1px">
</div>

#### 問5
<div align="center">
    <img src="pictures\knowledge\exp6.png" border="1px">
</div>

---

## 診断問題

意図的に誤りを含ませた問題を提示し，問題を診断させることにより，診断能力を測る設問を用意した．

```
以下の文章は，「ソートアルゴリズム」を題材にした問題となっています．
あなたは「診断者」として以下の問題を診断してください．
```

### 問題文
```
テスト結果を整理するために，N人の**学生の名前**(Name)と**テスト結果**(Score)を管理します．
このとき，点数の**大きい順**(降順)に整列したときの配列を出力するプロフラムを作成してください．
ただし，ソートアルゴリズムは自分で実走し，Pythonの組み込み関数は使用しないでください．

--入出力形式--
[入力]
 N
 Name_1 Score_1
 Name_2 Score_2
       :
 Name_N Score_N

[出力]
N人目の名前とスコアを入力した直後に，"[Result of sort]"という文字列を1度だけ表示した後，[Name Score]という形式で整列済みの配列を出力

--入出力例--
[入力例 1] [出力例 1]
 5         [Result of sort]
 田中 40    佐藤 90
 渡辺 80    渡辺 80
 佐藤 90    小島 70
 小島 70    安田 65
 安田 65    田中　40

[入力例 2] [出力例 2]
 3         スコアは0~100の範囲です
 田中 40
 渡辺 101

[入力例 3] [出力例 3]
 10        スコアの入力が不適切です
 田中 40
 渡辺 サ

[入力例 4] [出力例 4]
 -2        人数は0以上の整数です

[入力例 5] [出力例 5]
 0         [Result of sort]
```

### 解答
```
def bubble_sort_by_score(items):
    n = len(items)
        for i in range(n - 1):
        swapped = False
        for j in range(n - 1 - i):
            if items[j][1] < items[j + 1][1]:
                items[j], items[j + 1] = items[j + 1], items[j]
                swapped = True
        if not swapped:
            break

def main():
    # 受験者の数 N の入力（エラー処理を含む）
    try:
        N = int(input().strip())
        if N < 0:
            print("人数は0以上の整数です")
            return
    except ValueError:
        print("人数の入力が不適切です")
        return

    items = []
    for _ in range(N):
        line = input().split()
         Name = line[0]
        # 点数が0〜100の範囲外かどうかをチェック
        try:
            Score = int(line[1])
            if Score < 0 or Score > 100:
                print("スコアは0~100の範囲です")
                return
        except ValueError:
            print("スコアの入力が不適切です")
            return
        items.append((Name, Score))
    bubble_sort_by_score(items)

    # ソート後の結果を出力（N=0の場合は[Result of sort]）
    if N > 0:
        for Name, Score in items:
            print("[Result of sort]")
            print(Name, Score)

if __name__ == "__main__":
    main()
```

### 解説文
```
入力Nが膨大なデータ量になる場面ではないため，比較的実装が容易なバブルソートアルゴリズムを選択する．
"bubble_sort()"は，リストの隣接要素(Score)を比較し，要素を交換することの繰り返しを行うことで整列が行われる，
この繰り返しをN-1回の外ループ "for i in range()" で実現している．このループは，リスト全体をスキャンするものである．
各繰り返しの中で，隣接要素の比較・交換を，内ループ "for j in range()" によって実現している．
items[j]とitems[j+1]を比較し，小さい方を後ろに移動させる，これを，リストの先頭から末尾まで探索することで，1番小さい要素が末尾に移動される．
また，小さい数字が末尾に並び始めていくため，外ループが完了すると，小さい数字が後ろから並ぶ．つまり，要素が降順になる．
"main"を定義し， if __name__ == "__main__": main() の形にすることで，スクリプトを直接実行したときだけ，mainが呼ばれる構造になっている，
"int(input().strip())"で標準入力から整数を受け取り，空白文字を削除している．
Nが0未満の場合と，整数化できない文字列が入力された場合は，対応するエラー文を出力して処理を終了する．
次に，NameとScoreを取得するためのリスト"items"を定義する．ここで，N回だけループし，各行を"sprit()"で分割し，NameとScoreを取り出す．
ここでも，Scoreが0以上100以下の整数でない場合と，整数化できない入力が与えられた場合は，対応するエラー文を出力して処理を終了する．
その後は，入力によって得た配列をソートする，出力部分では，まず "[Result of sort]" という文字列を表示した後，配列した"items"から「Name Score」の順になるよう，要素を取り出して出力している．
なお，N=0のときは，ループが回らず何も出力されない．
```

### 診断内容
<div align="center">
    <img src="pictures\assessment\exp12.png" border="1px">
</div>
<div align="center">
    <img src="pictures\assessment\exp13.png" border="1px">
</div>