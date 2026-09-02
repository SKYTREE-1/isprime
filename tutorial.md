# Let's find prime numbers!

## 素数をみつけよう @showdialog

![素数判定チュートリアル2](https://skytree-1.github.io/isprime/images/img01.png)

## 素数かどうかを調べるアルゴリズム @showdialog

**自分より小さい自然数で割り切れない２以上の自然数が素数。**

例えば、7なら、
  * 7 ÷ 2 → 割り切れない
  * 7 ÷ 3 → 割り切れない
  * 7 ÷ 4 → 割り切れない
  * 7 ÷ 5→ 割り切れない
  * 7 ÷ 6 → 割り切れない

  → 7は素数

つまり、2以上の整数 `n` が素数かどうかを調べる方法の手順は次のように書けます。
素数の判定では、変数 ``||variables: is_prime||`` を使い、n が素数の時１、素数でないときに 0 とすることにします。

**手順**
1.　n を素数と仮定する（is_prime == 1）。
2.　`2` から `n - 1` までの整数 `i` について、次を繰り返す。
   - `n` が `i` で割り切れるか調べる。
   - 割り切れれば、`n` は素数ではない（is_prime == 0）。
3.　どの数でも割り切れなければ、`n` は素数である(is_prime==1)。

実際に、**２以上の整数**が素数かどうかを判定するプログラムを作成しよう！

## STEP1-1 変数の作成
``||variables:変数を追加する||`` から、3個の変数 n,i, is_prime 作成します。

## STEP1-2 仮の数値の代入 
``||input:ボタン A が押されたとき||``を配置して、``||variables:変数 〜 を〜にする||`` ブロックを使って、``||variables:変数 is_prime||`` を 1 ``||variables:変数 i||``を2、``||variables:変数 n を||`` 仮に 7 にします。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
})
```

## STEP1-3 くり返しの設定
``||loops:もし <偽> ならくりかえし||`` を出して、  <偽> の部分に ``||logic: 論理||``にある「くらべるブロック」から ``||logic: ()<()||`` ブロックをセットして ``||logic: (i)<(n)||`` にします。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
    	
    }
})
```


## STEP1-4 素数の判定
``||variables:n||`` が ``||variables:i||`` で割り切れるかどうかの判定をするので、
``||logic: 論理||``の``||logic: もし〜なら||``ブロックを``||loops:くりかえし||``の中に入れます。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (true) {

        }
    }
})
```

## STEP1-4  素数の判定（つづき）
``||variables:n||`` が ``||variables:i||`` で割り切れたら素数ではないので、
``||logic: もし〜なら||`` に比べるブロックを追加して ``||math:n÷iの余り||`` = 0  という条件を設定して、このとき``||variables: is_prime||`` を 0にします。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (n % i == 0) {
            is_prime = 0
        }
    }
})
```

## STEP1-7 i をひとつ増やす
``||loops: くりかえし||``ブロックの一番下に ``||variables: 変数||``から``||variables: 変数iを1増やす||`` をセットします。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (n % i == 0) {
            is_prime = 0
        }
        i += 1
    }
})
```

## STEP1-8 結果の表示
``||loops: くりかえし||``ブロックの下に ``||basic: 基本||``から``||basic: 数を表示||`` を使って、``||variables:変数||``の``||variables:is_prime||``を表示します。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (n % i == 0) {
            is_prime = 0
        }
        i += 1
    }
    basic.showNumber(is_prime)
})
```


## STEP1-9 実行
ここまできたら、ダウンロードして micro:bit で動かしてみよう。できたら、 ``||variables:n||``  の値をいろいろな値に変えて、試してみよう。


```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (n % i == 0) {
            is_prime = 0
        }
        i += 1
    }
    basic.showNumber(is_prime)
})
```

## STEP1-10 ちょっと改善
変数 ``||variables: is_prime||`` は 0 になると、その時点で素数ではないことが確定します。その後の判定は無駄になります。
``||loops:ループ||`` にある``||loops:くりかえしを終わる||``ブロックを使って``||variables:is_prime||``が0になったら、ループを抜けるように変更してください。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i < n) {
        if (n % i == 0) {
            is_prime = 0
            break;
        }
        i += 1
    }
    basic.showNumber(is_prime)
})
```


## さらに効率よく  @showdialog

ここまで、`i` を **2から `n-1` まで** 動かして、`n` が割り切れるかを一つずつチェックしてきました。

でも、ちょっと待ってください。

**本当に `n-1` まで調べる必要があるでしょうか？**

`n` が素数でなければ、`n` は2つの数の積で表すことができます。

例えば、

`36 = 4 × 9`

です。

このとき、2つの数のうち、**少なくとも一方は `√n` 以下** になります。

つまり、`n` が他の数で割り切れるなら、**必ず `√n` 以下のところで、その「割り切れる数」を見つけることができます。**

だったら……

**`n-1` まで調べる必要はありません。**

**2 ～ `√n` まで調べれば十分です！**

この考え方を使って、プログラムを改善しましょう。


## STEP1-11 さらに効率よく
``||loops:くりかえし||`` ブロックの条件 ``||logic : i <  n||`` の不等号と、右辺を変更して√n 以下になるように変更してください。
できたらダウンロードして実行してみてください。

```blocks
input.onButtonPressed(Button.A, function () {
    is_prime = 1
    n = 7
    i = 2
    while (i <= Math.sqrt(n)) {
        if (n % i == 0) {
            is_prime = 0
            break;
        }
        i += 1
    }
    basic.showNumber(is_prime)
})
```

## 素数を求めるプログラムを関数にしよう @showdialog

![Let's Make a Function!](https://skytree-1.github.io/isprime/images/img02.png)




## 関数の作成 @showdialog

``||functions: 関数||`` を開き、``||functions: 関数を作成する...||`` を押し、関数名 **isPrime** を入力します。

![手順１](https://skytree-1.github.io/isprime/images/img03.png)

数値を受け取って、それが素数かどうかを判定するようにしたいので、パラメーターを追加するの次の「電卓」のマークをクリックして数値を受け取れるようにします。

![手順２](https://skytree-1.github.io/isprime/images/img04.png)

できたら「完了」ボタンを押すと、関数 ``||functions: isPrime||`` ができます。

```blocks
// @showtoolbox ["functions"]

function isPrime (数値: number) {
	
}
```

次のステップで、関数 **isPrime** を作成しましょう。

## 2-1 関数の作成
``||functions: 関数||`` を開き、``||functions: 関数を作成する...||`` を押し、関数名 **isPrime** を入力して、パラメーターを追加するの次の「電卓」のマークをクリックして「完了」ボタンを押します。

```blocks
function isPrime (数値: number) {
	
}
```


## 2-2 素数かどうか判定する関数
``||functions: isPrime||``の中に、``||input:ボタンAが押されたとき||`` に入っているブロックのうち``||variables:変数 n を（）にする||``と``||basic:数を表示||``以外の全部を移します。


```blocks
input.onButtonPressed(Button.A, function () {
    n = 7
    basic.showNumber(is_prime)
})
function isPrime (数値: number) {
    is_prime = 1
    i = 2
    while (i <= Math.sqrt(n)) {
        if (n % i == 0) {
            is_prime = 0
            break;
        }
        i += 1
    }
}
```

## 2-3 素数かどうか判定する関数（つづき）
``||functions: isPrime||`` の 関数名の横にある ``||variables: 数値||``を、すべての``||variables: n||`` の上にドラッグして``||variables: n||``を``||variables: 数値||``に変えます。
このとき、いらないブロックは、左側のゴミ箱に捨ててください。


```blocks
function isPrime (数値: number) {
    is_prime = 1
    i = 2
    while (i <= Math.sqrt(数値)) {
        if (数値 % i == 0) {
            is_prime = 0
            break;
        }
        i += 1
    }
}
```

## 2-4 素数かどうか判定する関数（つづき）
``||functions: isPrime||``の最終行に、``||functions: 関数||``の``||functions: 戻る||``ブロックを追加してして、空欄を ``||variables: is_prime||`` にして、結果を返すようにします。

```blocks
function isPrime (数値: number) {
    is_prime = 1
    i = 2
    while (i <= Math.sqrt(数値)) {
        if (数値 % i == 0) {
            is_prime = 0
            break;
        }
        i += 1
    }
    return is_prime
}
```
## 2-5 関数の呼び出し
``||input:ボタンAが押されたとき||`` にある``||basic:数を表示||``ブロックの``||variables: is_prime||``を、``||functions: 関数||``の``||functions: 呼び出し is_prime ||`` に変更して、パラメーターに ``||variables:n||`` を入れます。


```blocks
let n = 0

input.onButtonPressed(Button.A, function () {
    n = 7
    basic.showNumber(isPrime(n))
})
```

## Finish! @showdialog

完成！

素数を見つけるだけでも、
「どうすれば、もっと少ない計算でできる？」と考えることで、
プログラムはどんどん効率よくできます。

これが、アルゴリズムを工夫するということです。

## Challenge @showdialog

🔸 2～100の素数を見つけよう！

ここまで作った `isPrime()` 関数を使って、

**2～100の中から素数だけを取り出し、リストに入れて表示するプログラム**

を作ってみよう。

例えば、最初は

`[2, 3, 5, 7, ...]`

のようなリストを作り、素数を見つけるたびに追加していく。

【ヒント】

- `2` から `100` まで、順番に調べる
- `isPrime()` を使って、素数かどうかを判定する
- 素数だったら、リストに追加する
- 最後にリストの中身を表示する

**どんなプログラムになるかな？**


## サンプルプログラム @showdialog

```blocks
let n = 0

input.onButtonPressed(Button.B, function () {
    let prime_list: number[] = []
    for (let カウンター = 0; カウンター <= 98; カウンター++) {
        n = カウンター + 2
        if (isPrime(n) == 1) {
            prime_list.push(n)
        }
    }
    for (let カウンター = 0; カウンター <= prime_list.length - 1; カウンター++) {
        basic.showNumber(prime_list[カウンター])
    }
})
```
