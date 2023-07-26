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
````

tsconfig.json で、型定義ファイルを集めたフォルダを指定するには、次のようにします。

1. 型定義ファイルを含むフォルダを作成します。例えば、`types` という名前のフォルダをプロジェクトのルートに作成します。
2. tsconfig.json ファイルを開きます。`compilerOptions` オブジェクトの中に、`typeRoots` という配列を追加します。
3. `typeRoots` 配列の中に、型定義ファイルを含むフォルダへの相対パスを記述します。例えば、`types` フォルダへのパスは `"./types"` となります。
4. tsconfig.json ファイルを保存します。

これで、型定義ファイルを集めたフォルダを指定することができました。TypeScript コンパイラは、このフォルダ内のすべての型定義ファイルを読み込みます。
