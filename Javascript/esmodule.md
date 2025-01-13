
# エラー発生
 JS側でimportぶんを描いて実行したら
` main.js:1 Uncaught SyntaxError: Cannot use import statement outside a module`　というエラーが出た

```
import { hello } from "./module.js";
import { User } from "./module.js";
hello();
const user = new User("Tom");
user.hello;
```
html側での呼び出しにtype="module"を追加した場合、エラーが解消
`<script src="main.js" type="module"></script>`

- package.jsonで"type": "module"を指定した場合と、html側のjsの呼び出しで、type="module"を指定した場合の違い
JavaScriptでファイルを分割してインポート・エクスポートする仕組み（モジュールシステム）は２つある。

それらはES modulesとCommonJS。
主にES Modulesはブラウザで利用され、CommonJSはNode.jsで利用される。
JavaScriptには元々ファイルを分割して利用する仕組みがなく、これらの仕組みは後から追加されたもの
なので、ブラウザの<script>タグでJavaScriptファイルを読み込む場合、
そのファイルがES Modelesの機能を利用していることをブラウザに伝えるためにtype="module"と記載する必要がある。
この記述がないと、Cannot use import statement outside a module というエラーが発生。

一方、Node.js上ではES Moduleとは別のCommonJSがモジュールシステムを利用可能にしていますが、ES Modulesも利用可能にするように設定することができます。
その設定が、package.jsonに記載する、"type": "module"です。
