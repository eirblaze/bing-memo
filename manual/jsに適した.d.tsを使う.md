# 型定義ファイル `*.d.ts`

## 基本的な書式

```md
型定義ファイル `*.d.ts` の基本的な書式を、Javascript 初心者にもわかる言葉で、コード例とともに解説してください。
```

型定義ファイル \*.d.ts とは、TypeScript で JavaScript のライブラリやモジュールを使うときに必要なファイルです。型定義ファイルには、JavaScript のコードに対応する型情報が書かれています。これによって、TypeScript のコンパイラやエディタが、JavaScript のコードを正しく理解して、型チェックや補完などの機能を提供できます。

型定義ファイルの基本的な書式は、次のようになります。

```ts
// モジュール名やライブラリ名を宣言する
declare module "module-name" {
// エクスポートされる変数や関数やクラスなどの型を定義する
export let variable: type;
export function function(parameter: type): type;
export class class {
constructor(parameter: type);
method(parameter: type): type;
}
// エクスポートされない変数や関数やクラスなどの型を定義する
let variable: type;
function function(parameter: type): type;
class class {
constructor(parameter: type);
method(parameter: type): type;
}
}
```

例えば、次のような JavaScript のコードがあるとします。

```js
// math.js
export const PI = 3.14;
export function add(x, y) {
  return x + y;
}
export class Vector {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  length() {
    return Math.sqrt(this.x * this.x + this.y * this.y);
  }
}
```

このコードに対応する型定義ファイルは、次のように書けます。

```ts
// math.d.ts
declare module "math" {
  export const PI: number;
  export function add(x: number, y: number): number;
  export class Vector {
    constructor(x: number, y: number);
    length(): number;
  }
}
```

この型定義ファイルを使うと、TypeScript で math.js をインポートして使うことができます。

```ts
// app.ts
import { PI, add, Vector } from "math";
console.log(PI); // 3.14
console.log(add(1, 2)); // 3
let v = new Vector(3, 4);
console.log(v.length()); // 5
```

以上が、型定義ファイル `*.d.ts` の基本的な書式と使い方です。型定義ファイルは、JavaScript のライブラリやモジュールの作者が提供することもあれば、別の人が作って公開することもあります。型定義ファイルを探すときは、[DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)というリポジトリや[npm](https://www.npmjs.com/)というパッケージマネージャーを利用すると便利です。

## ブラウザ用

```md
型定義ファイル `*.d.ts` の基本的な書式 (node.js ではなく、 ブラウザで動作する js に向けた書式) を、Javascript初心者にもわかる言葉で、コード例とともに解説してください。
```

型定義ファイル *.d.ts とは、JavaScriptのコードに対して、型情報を付与するためのファイルです。JavaScriptは動的型付け言語なので、変数や関数の引数や戻り値の型を宣言する必要はありませんが、型定義ファイルを使うと、コードの品質や可読性を向上させることができます。また、型定義ファイルを利用すると、エディタやIDEでのコード補完やエラーチェックなどの機能も強化されます。

型定義ファイルは *.d.ts という拡張子を持ち、JavaScriptのコードと同じディレクトリに置くか、あるいは特定のディレクトリにまとめて置くことができます。型定義ファイルの中では、declare というキーワードを使って、変数や関数やクラスなどの型を宣言します。例えば、以下のようなコードがあるとします。

```js
// sample.js
function add(x, y) {
return x + y;
}

var result = add(1, 2);
console.log(result);
```

このコードに対して、型定義ファイルを作ると以下のようになります。

```ts
// sample.d.ts
declare function add(x: number, y: number): number;
declare var result: number;
```

型定義ファイルでは、コロン (:) の後に型名を書きます。ここでは、数値型を表す number という型名を使っています。他にも、文字列型を表す string や真偽値型を表す boolean などの基本的な型名があります。また、配列やオブジェクトや関数などの複合的な型も作ることができます。

型定義ファイルを作成したら、JavaScriptのコードから参照する必要があります。ブラウザで動作するJavaScriptでは、script タグの中で *.d.ts ファイルを指定します。例えば、以下のように書きます。

```html
<script src="sample.d.ts" type="text/typescript"></script>
<script src="sample.js"></script>
```

これで、ブラウザでJavaScriptを実行する際に、型定義ファイルが読み込まれて、型情報が反映されます。もし、型に合わない値を代入したり、引数に渡したりした場合は、エラーが発生します。

以上が、型定義ファイル *.d.ts の基本的な書式についての解説です。JavaScript初心者の方にもわかりやすいように説明しましたが、もっと詳しく知りたい方は、以下の参考文献をご覧ください。

- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html
- TypeScript Deep Dive: https://basarat.gitbook.io/typescript/type-system/intro

## プロジェクトフォルダに合わせる

```js
// js のプロジェクトフォルダに対して、*.d.ts の形で型定義ファイルを作成し、適切な場所に配置するにはどうすればよいかを、サンプルコードとともに、デザイナーにもわかりやすい言葉で解説してください。

// 型定義ファイルとは、JavaScript のコードに TypeScript の型情報を付与するためのファイルです。型定義ファイルは *.d.ts という拡張子を持ちます。型定義ファイルを作成することで、JavaScript のコードの品質や可読性を向上させることができます。

// 型定義ファイルを作成する方法はいくつかありますが、ここでは最も簡単な方法として、tsc コマンドを使って自動的に生成する方法を紹介します。tsc コマンドは TypeScript のコンパイラであり、JavaScript のコードから型定義ファイルを生成する機能を持ちます。

// まず、tsc コマンドを使えるようにするために、TypeScript をインストールします。npm を使ってグローバルにインストールする場合は、以下のコマンドを実行します。

npm install -g typescript

// 次に、js プロジェクトフォルダのルートに tsconfig.json という名前のファイルを作成します。このファイルは TypeScript の設定ファイルであり、型定義ファイルの生成方法や出力先などを指定します。以下は tsconfig.json の例です。

{
  "compilerOptions": {
    "allowJs": true, // JavaScript ファイルのコンパイルを許可する
    "declaration": true, // 型定義ファイルを生成する
    "outDir": "./types", // 型定義ファイルの出力先
    "rootDir": "./src" // JavaScript ファイルの入力元
  },
  "include": ["./src/**/*.js"] // 型定義ファイルを生成する対象の JavaScript ファイル
}

// この設定では、src フォルダ内のすべての JavaScript ファイルから型定義ファイルを生成し、types フォルダに出力することを指示しています。また、allowJs オプションを true にすることで、JavaScript ファイルのコンパイルを許可しています。

// 最後に、js プロジェクトフォルダのルートで以下のコマンドを実行します。

tsc

// これで、types フォルダ内に型定義ファイルが生成されます。型定義ファイルは JavaScript ファイルと同じ名前と階層構造を持ちます。例えば、src/foo/bar.js からは types/foo/bar.d.ts が生成されます。

// 型定義ファイルを使用するには、JavaScript ファイルの先頭に以下のようにコメントを追加します。

// @ts-check // TypeScript の型チェックを有効化する
// @ts-ignore // TypeScript のエラーを無視する（必要な場合）
/// <reference path="../types/foo/bar.d.ts" /> // 型定義ファイルへの参照

// これで、JavaScript のコードに対して TypeScript の型チェックが行われるようになります。型チェックはエディタや IDE でサポートされている場合が多く、コード中の型エラーや補完機能などが利用できるようになります。

// 以上が、js のプロジェクトフォルダに対して、*.d.ts の形で型定義ファイルを作成し、適切な場所に配置する方法です。デザイナーの方にもわかりやすく説明できたでしょうか。もし不明な点や質問がありましたら、お気軽にお尋ねください。
```

tsconfig.json で、型定義ファイルを集めたフォルダを指定するには、次のようにします。

1. 型定義ファイルを含むフォルダを作成します。例えば、`types` という名前のフォルダをプロジェクトのルートに作成します。
2. tsconfig.json ファイルを開きます。`compilerOptions` オブジェクトの中に、`typeRoots` という配列を追加します。
3. `typeRoots` 配列の中に、型定義ファイルを含むフォルダへの相対パスを記述します。例えば、`types` フォルダへのパスは `"./types"` となります。
4. tsconfig.json ファイルを保存します。

これで、型定義ファイルを集めたフォルダを指定することができました。TypeScript コンパイラは、このフォルダ内のすべての型定義ファイルを読み込みます。
