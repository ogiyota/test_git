# typescriptについて

## Javascript

動的型付言語
Javascriptエンジンが型検査をし、コードを実行する

## typescriptとは

1. Javascriptにコンパイルされる言語
2. 静的型付言語(コンパイル時に型検査を行う)
3. Javascriptの上位集合

TypescriptはJavascriptを機能拡張した言語

### 環境構築

npm install -g typescript

-gは付けなくても可

## Typescriptを使用するメリット

1. 可読性・保守性が上がる
2. Linterが便利

変数・関数に関する値がどのような型を使用するのか分かる

```index.ts

const a: number = 1;
const b: number = 2;

function add(a: number, b: number): number {
    return a + b;
}

```

tscにてコンパイル時にエラーが出る
Javascriptでは実行時にエラーが出る
ただ、vscodeはtscが内蔵されているのでリアルタイムにエラーを出してくれる

有名なLinterですとESLintなども同じようにエラーを出してくれますが型に関するエラーは出してくれないので併用するのが良いです。

### コンパイル方法

ターミナルにて
tsc index.ts
実行するのは
node index.js

## 型定義について

### 型注釈と型推論

型注釈は型も含めコードに記述
型推論は型を含めずにコードに記述

冗長になるので型推論が良いとされている
letとconstの違いに注意
関数の戻り値に関しては可読性向上の為に型注釈をする
関数の仮引数には必ず型注釈をする

### 基礎的な型

boolean 論理型
number 数字型（小数点も含める）
string 文字列型

### オブジェクトにおける型

```index.ts

const person: {
    name: string;
    age: number;
} = {
    name: '鈴木'
    age: 20
}

```

objectという型もあるが、どんなkeyを持っているのかの情報は持っていない
object全般を意味している

### 配列における型とタプル型とユニオン型

```index.ts
// 通常の配列の型
const fruits: string[] = ['Apple', 'Banana', 'Orange'];
// 型の後ろに[]を付ける

// ユニオン型
const product: (string | number)[] = ['製品A', 2192822];
// ( | )[]の形にする
// 単純な変数の場合　()を消す

// タプル型の場合
const food: [string, number, boolean] = ['お寿司', 200, true];
// 型配列に決められた型のみ許容

```

Typescriptは初期値を決めるときは厳格ですが、その後は比較的緩くなる。
pushなどで値は入れられるが、参照は不可

### 列挙型

```index.ts

const coffee = {
    hot: true,
    size: SHORT
}
// sizeの値を厳格に決めたい

const CoffeeSize = {
    SHORT: 'SHORT',
    TALL: 'TALL',
    GRANDE: 'GRANDE',
    VENTI: 'VENTI'
}

const coffee = {
    hot: true,
    size: CoffeeSize.TALL
}

coffee.size = 'small'

// これでも良いが、後々入れ替えが可能となってしまう

enum CoffeeSize {
    SHORT: 'SHORT',
    TALL: 'TALL',
    GRANDE: 'GRANDE',
    VENTI: 'VENTI'
}

const coffee = {
    hot: true,
    size: CoffeeSize.TALL
}

coffee.size = CoffeeSize.TALL

// これでenumで定義した4つの値のみを受け取ることが可能

enum CoffeeSize {
    SHORT,
    TALL,
    GRANDE,
    VENTI
}

// これで取得すると　0,1.2.3の順で値が取れる
```

### any型について

```index.ts

let x: any = 3;
let word: string = 'こんにちは';

word = x;

```

通ってしまう。
anyはなるべく使わない

### リテラル型

```index.ts

const ok: true = true;

```

constの場合だと自動でリテラル型となる

```index.ts

const coffee: 'SHORT' | 'TALL' | 'GRANDE' | 'VENTI' = 'TALL';

```

リテラル型とユニオン型を組み合わせるのも便利

### エイリアス

```index.ts

type Size = 'SHORT' | 'TALL' | 'GRANDE' | 'VENTI';

let coffee: Size = 'SHORT';

```

###　関数の型

```index.ts

function add(a: number, b: number): number {
    return a + b
}
add(1,2);

function hello(): void{
    console.log('hello');
}

// 戻り値のない場合はvoidを使用

```

undefined型もあるが、これは使わない

## 問題５問

1. 型推論と型注釈の違い
TypeScriptにおける「型推論」(Type Inference) と「型注釈」(Type Annotation) の違いを説明してください。

2. 関数の戻り値の型
次の関数の戻り値の型は何ですか？

```index.ts

function getTotal(a: number, b: number) {
    return a + b;
}

```
3. 列挙型 (Enum) の利用
TypeScriptにおける列挙型 (Enum) の主な利用目的は何ですか？

4. any型の使用に関する注意点
TypeScriptで any 型を使用する際のリスクや注意点は何ですか？

5. オブジェクトの型注釈
次のオブジェクトの型注釈は正しいですか？間違っていれば、どこが間違っているか指摘してください。

```index.ts

const person: {
    name: string;
    age: number;
} = {
    name: '山田',
    age: '三十'
};

```
