npm パッケージを TypeScript で作成することで、型情報の配布を省略する方法を、コード例とともに解説しています。TypeScript は JavaScript のスーパーセットであり、型アノテーションやクラスなどの機能を提供します。TypeScript で書かれたコードは、tsc コマンドで JavaScript にコンパイルされますが、その際に型情報は失われます。型情報を保持するには、d.ts ファイルと呼ばれる宣言ファイルを生成する必要があります。しかし、このファイルを作成するのは手間がかかりますし、パッケージの利用者にも配布する必要があります。

そこで、npm パッケージを TypeScript で作成する場合には、型情報の配布を省略する方法があります。それは、package.json ファイルに "types" というフィールドを追加し、その値に TypeScript のソースファイルのパスを指定することです。例えば、以下のようにします。

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "main": "dist/index.js",
  "types": "src/index.ts"
}
```

このようにすると、パッケージの利用者は npm install my-package としてインストールした後、TypeScript のコードから import myPackage from 'my-package' としてインポートできます。そして、TypeScript のコンパイラは package.json の types フィールドを見て、型情報を src/index.ts ファイルから読み込みます。この方法ならば、d.ts ファイルを生成したり配布したりする必要がなくなります。

ただし、この方法にはいくつかの注意点があります。まず、パッケージの利用者も TypeScript を使っている必要があります。JavaScript のコードからインポートした場合には型情報は利用できません。また、パッケージの TypeScript のソースファイルは公開されることになりますので、プライベートな情報やコメントなどを含めないように注意してください。さらに、パッケージの TypeScript のソースファイルとコンパイルされた JavaScript のファイルの構造や名前が一致している必要があります。例えば、src/index.ts ファイルが dist/index.js ファイルにコンパイルされるようにしてください。

以上が、npm パッケージを TypeScript で作成することで、型情報の配布を省略する方法の解説です。この方法を使えば、型情報の管理や配布の手間を省くことができます。

## npm パッケージ を mjs の書式で作成するには、次の手順を実行します。

1. package.json ファイルに `"type": "module"` を追加します。これにより、パッケージ内のすべての JavaScript ファイルが ES モジュールとして扱われます。
2. パッケージのエントリポイントとなるファイルの拡張子を .mjs に変更します。例えば、index.js を index.mjs にリネームします。
3. エントリポイントファイルから他のモジュールをインポートする際には、完全なファイルパスを指定します。例えば、`import foo from './foo.js'` のようにします。
4. パッケージを公開する前に、`npm run test` や `npm run build` などのスクリプトを実行して、パッケージが正常に動作することを確認します。

## npm パッケージ を、ローカルフォルダの git ベアリポジトリからインストールするには、次の手順を実行します。

1. ローカルフォルダの git ベアリポジトリのパスをコピーします。例えば、`/home/user/my-repo.git` などです。
2. インストールしたいプロジェクトのフォルダに移動します。
3. `npm install` コマンドに、コピーしたパスを `git+file://` というプレフィックスとともに指定します。例えば、`npm install git+file:///home/user/my-repo.git` などです。
4. インストールが完了すると、`package.json` ファイルに、指定したパスが `dependencies` または `devDependencies` の項目として追加されます。
5. 以降は、通常の npm パッケージと同様に使用できます。

## 型定義ファイル

```jsonc
// npm パッケージ を、 mjs でリリースする際、型定義ファイルをどう設定するか、コード例とともに解説してください。

// mjs は ES モジュール の拡張子です。ES モジュール は JavaScript の標準的なモジュール システム で、import と export を使ってモジュール を読み込んだり提供したりできます。
// npm パッケージ を mjs でリリースする場合、package.json に以下のように設定します。
{
  "name": "my-package",
  "version": "1.0.0",
  "type": "module", // ES モジュール であることを宣言する
  "main": "index.mjs", // メインのモジュール ファイル を指定する
  "exports": {
    ".": "./index.mjs", // パッケージ の名前で import されたときに読み込まれるファイル を指定する
    "./foo": "./foo.mjs" // パッケージ のサブパスで import されたときに読み込まれるファイル を指定する
  }
}
```

```jsonc
// 型定義ファイル は TypeScript のコードを JavaScript に変換するときに生成されるファイルで、JavaScript のコードに型情報を付与するために使われます。
// 型定義ファイル を mjs と一緒にリリースする場合、package.json に以下のように設定します。
{
  "name": "my-package",
  "version": "1.0.0",
  "type": "module",
  "main": "index.mjs",
  "exports": {
    ".": "./index.mjs",
    "./foo": "./foo.mjs"
  },
  "types": "index.d.ts", // パッケージ の名前で import type されたときに読み込まれる型定義ファイル を指定する
  "typesVersions": {
    "*": {
      "*": ["*.d.ts"] // パッケージ のサブパスで import type されたときに読み込まれる型定義ファイル を指定する
    }
  }
}
```

```js
// 型定義ファイル を作成するには、TypeScript のコンパイラ オプション の declaration を true に設定します。
// 型定義ファイル の名前は、対応する mjs ファイル の名前に .d.ts を付けたものになります。
// 型定義ファイル の中身は、mjs ファイル の export 文に対応する型宣言文になります。
// 例えば、以下のような mjs ファイル があるとします。

// index.mjs
export function add(x, y) {
  return x + y;
}

export class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```

```js
// foo.mjs
import { Person } from "./index.mjs";

export function greet(person) {
  return `Hello, ${person.name}!`;
}

export const me = new Person("Alice", 20);
```

```ts
// この場合、以下のような型定義ファイル が生成されます。

// index.d.ts
export function add(x: number, y: number): number;
// export add: (x: number, y: number) => number;

export class Person {
  constructor(name: string, age: number);
  name: string;
  age: number;
}
```

```ts
// foo.d.ts
import { Person } from "./index";

export function greet(person: Person): string;

export const me: Person;
```
