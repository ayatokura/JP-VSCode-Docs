---
Order: 16
TOCTitle: September 2016
PageTitle: Visual Studio Code September 2016 1.6
MetaDescription: See what is new in the Visual Studio Code September 2016 Release (1.6)
MetaSocialImage: 1_6_release-highlights.png
---

# September 2016 (version 1.6)

## 1.6.1 Recovery Build

残されていた 1.6 の翻訳を追加し、いくつかの重要な[問題](https://github.com/Microsoft/vscode/milestone/31?closed=1)を修正した 1.6.1 リカバリビルドをリリースしました:

Downloads: [Windows](https://vscode-update.azurewebsites.net/1.6.1/win32/stable) | [Mac](https://vscode-update.azurewebsites.net/1.6.1/darwin/stable) | Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.6.1/linux-x64/stable) [.deb](https://vscode-update.azurewebsites.net/1.6.1/linux-deb-x64/stable) [.rpm](https://vscode-update.azurewebsites.net/1.6.1/linux-rpm-x64/stable) | Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.6.1/linux-ia32/stable) [.deb](https://vscode-update.azurewebsites.net/1.6.1/linux-deb-ia32/stable) [.rpm](https://vscode-update.azurewebsites.net/1.6.1/linux-rpm-ia32/stable)

## September Release Summary

Visual Studio Code 9 月リリース版へようこそ。このリリースではいくつかの重要な更新があり、ハイライトは次のとおりです:

* **[TypeScript 2.0](#typescript-20)** - [JavaScript](#javascript) と [TypeScript](#typescript) だけでなく、[拡張機能のオーサリング](#extension-authoring) に関連する改善
* **[Format on Save](#format-on-save)**  - 保存時にフォーマッタを実行する機能を追加
* **[Switch Windows](#switch-between-running-windows)** - コマンドパレット経由で VS Code ウィンドウ（インスタンス）間をすばやく移動可能に
* **[Search term history](#search-term-history)** - 検索ボックスにヒストリ機能を追加
* **[Launch script support](#launch-configuration-supports-npm-and-other-tools)**  - デバッグ実行前に npm スクリプトを起動可能に
* **[Workspacerecommendations](#workspace-extension-recommendations)** - チーム内の他のメンバーのためにワークスペースで推奨する拡張機能を提供可能に
* **[API for Settings](#new-apis)** - API を介して設定を変更できるようになり、永続的な [Auto Save](#auto-save-menu-item) と、[File Associations](#file-associations-configuration)　などの新しいオプションをサポート
* **[VIM style relative line numbers](#improvements-to-linenumber-and-whitespace-settings)** - 現在のカーソル位置から行番号の相対位置を表示
* **[Node 6.3+ Debugger](#experimental-nodejs-v63-debugger)** - V8 Inspector Protocol をサポートするために実験的な拡張機能が利用可能に
V8 Inspector Protocol のための実験的な拡張機能をサポート
* **[*PREVIEW*  Extensions Packs](#preview-extension-packs)** - Marketplace から 1回のダウンロードで複数の拡張機能をインストール可能な拡張機能バンドルセットを定義可能に
* **[*PREVIEW*  TS/JS Grammar](#preview-typescriptjavascript-grammar)** - 次の VS Code リリースに搭載予定の TypeScript/JavaScript に関する 200 以上の修正を行った新しいカラー表示機能をプレビューとして提供

VS Code の注目ポイントに関連するアップデート情報は、リリースノートの次のセクションに配置されています。その他のアップデートは、次のとおりです:

* **[Workbench](#workbench)** - 画像ファイルの寸法とファイルサイズの詳細をステータスバーに表示
* **[Editor](#editor)** - Unicode の UTF-16 サロゲートペアの改善をサポート、空白の設定を改善
* **[Languages](#languages)** - TML/Razor/Handlebar サポートの改善
* **[Extensions](#extensions)** - 拡張機能の識別子バッジ、拡張機能アップデートに関わるバージョンチェック
* **[Debugging](#debugging)** - 設定可能な外部端末サポート、source map の glob パターン
* **[Extension Authoring](#extension-authoring)** プログラムによる launch.json へのアクセスを含むデバッグプロトコルのアップデート

## Workbench

### Release notes inside VS Code

最新のリリースノートを確認するために、ブラウザからウェブサイトにアクセスする必要がなくなりました - VS Code から直接リリースノートを見ることができます。 **Show Release Notes** コマンドまたは **Help** > **Release Notes** メニューからアクセスする事ができます。
おそらく、あなたは、今、このリリースノートを VS Code から読んでいるかと思います :)

### Icons Everywhere

ファイルアイコンをサポートするために、8月リリース版で行った作業に引き続き、UI のより多くの場所にファイルアイコンの表示を追加しました。これは、ファイルの表示やその他ほとんどのツリー表示（例えば、問題パネル、検索結果、OPEN EDITOR セクション）と同様に **クイックオープン** の結果やエディタの見出しにも含まれています。

タブの見出しなど、アイコンをどこにも表示したくない場合は、新しい `workbench.editor.showIcons` 設定に false を追加してください。

![Icons](https://code.visualstudio.com/images/1_6_icons.png)

### Switch between running Windows

既にオープンされている VS Code ウインドウ間を素早く移動できるようにする新しいコマンドを追加しました。利用方法はとても簡単で、**Command Palette** (`(kb(workbench.action.showCommand)`) を開き、**Switch Window** とタイプしてください。
ドロップダウンには、現在開いているすべての VS Code ウインドウ (インスタンス) が表示されます。**Command Palette** (`(kb(workbench.action.showCommand)`) を開き、**Switch Window** を入力することで、キーボードを離れることなく一方から他方へすぐに VS Code 内から移動することができます。

![switch window](https://code.visualstudio.com/images/1_6_switch-window-animation.gif)

### Image dimensions & Binary file size

VS Code でバイナリファイルを開くと、ファイルのメタ情報をステータスバーに表示するようになりました。ファイルサイズの表示は全てのバイナリが対象になりますが、画像ファイルについてファイルサイズに加え画像のサイズを表示します。

![Status](https://code.visualstudio.com/images/1_6_status.png

また、VS Code はディスク上の画像ファイルの変更を検出するようになったので、常に最新の画像ファイルを表示することが可能になりました。

## Editor

### Format On Save

ソースコードを整形する度に保存していますか？
VS Code は、関連するインストール済みのフォーマッター拡張機能を自動的にピックアップし、ファイル保存時にフォーマットを適用する "Format On Save" をサポートしました。"Format On Save" を有効にするには、`"editor.formatOnSave": true` を設定してください。

> **Note:** カーソルと選択の安定性を維持するために、`"files.autoSave": "afterDelay"` 設定時はフォーマットは実行されません

### Search term history

グローバル検索ビューおよびエディタの検索ウィジェットにおいて、検索履歴を呼び出すことが可能になりました。

* `kbstyle(Alt+Up)` 検索履歴を後方に移動します。対応するコマンドは、`search.history.showPrevious` と `find.history.showPrevious`です
* `kbstyle(Alt+Down)` 検索履歴を前方に移動します。対応するコマンドは、`search.history.showNext` と `find.history.showNext` です

### Hover & IntelliSense UI consistency

ホバーウィジェットの UI は、IntelliSense が提供する多くの機能と揃うよう更新されました。

![hover](https://code.visualstudio.com/images/1_6_hover.png)

### Auto Save Menu Item

自動保存は、特に注目される機能です。この機能をより見つけやすくするために、VS Code の **File** メニューに **Auto Save** トグルを追加しました。これは、グローバルのユーザー設定である `settings.json` 構成ファイル内の `files.autoSave` [setting](https://code.visualstudio.com/docs/customization/userandworkspace) 設定を切り替えています。

### File Associations configuration

ファイルの拡張子と言語モードの関連付けを簡単に行うことが可能になりました。
ファイルの言語モードを変更する場合、言語モードの選択から **'xx' に対するファイルの関連付けの構成 (Configure File Association for...)** を選ぶことで拡張子と選択した言語の関連付けがユーザー設定ファイル (settings.json) の `"files.associations"` に保存され、有効になります。

### Unicode improvements

VS Code に、UTF-16 サロゲートペアのより良いハンドリングを実装し、すべての編集においてサロゲートペアを分割していないことを検証するよう Unicode サポートを改善しました。特に、ソースコードに絵文字のようなものを追加したい場合、この改善は重要になります。

### Improvements to LineNumber and Whitespace settings

いくつかのエディタ設定は、新しいオプションをサポートするように更新されました:

* `editor.renderWhitespace` に使用可能な値は `"all"`, `"boundary"` と `"none"` です。`"boundary"` オプションは、単語の間に単一のスペースをレンダリングしません。

* `editor.lineNumbers` に使用可能な値は `"on"`, `"off"` と `"relative"` です。`"relative"` は、現在のカーソル位置からの行数を示します。

## Languages

### TypeScript 2

VS Code 1.6 に TypeScript 2.0.3 がバンドルされましたが、ワークスペースにおいて、下記の操作を行うことにより TypeScript 1.8.10 に戻すことが可能です:

- ワークスペースのフォルダに移動します。(VS Code は終了しておきます)
- `npm install typescript@1.8.10` を実行し、ワークスペースに TypeScript 1.8.10 をインストールします
- ワークスペースを指定して VS Code を起動します。ワークスペースにインストールされたバージョン(1.8.10)または、バンドルされる TypeScript バージョン（2.0.3）を使用するか尋ねられるので、ワークスペースにインストールされたバージョン(1.8.10)を選択し、変更されたことを確認します。

### TypeScript

TypeScript 2.0.3 には、厳格な null チェックやモジュラーライブラリの依存関係などの多くの新機能が含まれています。新機能の完全なリストは[ここ](https://github.com/Microsoft/TypeScript/wiki/What%27s-new-in-TypeScript#typescript-20)で確認することができます。

また、新機能のほかに、TypeScript 2.0.3 には多くのバグ修正が含まれています。TypeScript 2.0.3 を使用して、既存のプロジェクトをコンパイルした場合、コンパイル時にエラーが発生する可能性があります。

### JavaScript

VS Code の JavaScript サポートは、TypeScript によりサポートされていますが、バンドルされる TypeScript は、バージョン 2.0.3 にアップデートされました。

これは、JavaScript サポートにいくつかの改善をもたらします:

- JS Doc サポートが改善され、多くの問題が修正されました
- アウトラインのサポート `Go to Symbol in File...` が改善されました
- パーサは現在、TypeScript パーサが認識可能な JavaScript の標準化提案の一部である任意の構文を使用できます。たとえば、静的クラスのプロパティには、無効のフラグが設定されません。

また、JavaScript にも適用可能である TypeScript への改善があります: 

- `jsconfig.json` ファイルでのグロビングをサポート
- [--lib を使用した、新しい ECMAScript バージョンの組み込み型宣言](https://github.com/Microsoft/TypeScript/wiki/What%27s-new-in-TypeScript#including-built-in-type-declarations-with---lib)のより良いサポート 
- [ファイル拡張子を持つモジュール・インポート](https://github.com/Microsoft/TypeScript/wiki/What%27s-new-in-TypeScript#module-identifiers-allow-for-js-extension)のための処理を改善

1 つの非常に大きな改善としては、型定義ファイル (typings) の取得が簡略化されたことです。`@types` パラメータにより NPM から直接、型定義ファイルを取得することができます。

例えば、`lodash` のための型定義ファイルを取得するには下記の様に実行します: 

```bash
npm install --save-dev @types/lodash
```

### PREVIEW TypeScript JavaScript Grammar

TypeScript および JavaScript の TextMate 文法が改訂されました。この改訂は、[マーケットプレイスの拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode.typescript-javascript-grammar)から利用可能です。また、10月中にこの改訂されたバージョンに切り替えることを計画していますので、この拡張機能をインストールして、ぜひフィードバックをください。

### Updated HTML/Razor/Handlebar Support

VS Code が利用可能になってから、いくつかの言語サポートは VS Code 内に直接実装され、拡張機能としては実装されていませんでした。
過去のマイルストーンにおいて、JSON, CSS, LESS, SASS 言語を拡張機能として切り出し、直接実装のコードを取り除きました。
9月リリース版では、HTML との組み合わせで多く使われる言語である、Razor や Handlebar のために同様のことを行っています。
これら全ての言語は、[language server protocol](https://github.com/Microsoft/language-server-protocol) を使用して実装され、主要なリファクタリングとなりますが、いくつかの言語機能はまだ実装されていません。

* Commenting actions inside `<script>` section of an HTML - [Issue 12969](https://github.com/Microsoft/vscode/issues/12969)
* Word highlighting - [Issue 12973](https://github.com/Microsoft/vscode/issues/12973)

次のイテレーションの間にこれらの機能を戻すことに取り組みます。

しかし、我々はまだ完了していません..今、私たちは拡張機能に言語を抽出したことを、次の課題は、つまり、これらの言語のネストをサポートするために、HTML の中に JavaScript や CSS を埋め込みます。10 月リリース版に向けて取り組む予定です。

## Extensions

### Workspace Extension Recommendations

多くの場合、個別のワークスペースで作業の生産性を高めるために拡張機能のセットを持っています。現在のワークスペースにおける拡張機能の推奨リストの作成をサポートしました。推奨セットは `.vscode` フォルダにあるファイル `extensions.json` で定義され、この機能は、チーム内で簡単に共有することができます。

**Extensions: Configure Workspace Recommended Extensions** コマンドを使用してこのファイルを作成することができます。

例えば、これは我々が [vscode ワークスペース](https://github.com/Microsoft/vscode/blob/master/.vscode/extensions.json) で使用している  `extensions.json` ファイルとなり、内容は次のとおりです:

```json
{
	"recommendations": [
		"eg2.tslint",
		"dbaeumer.vscode-eslint",
		"msjsdiag.debugger-for-chrome"
	]
}
```

上記の `recommendations` 設定から見ることができるように、VS Code のコードベースに取り組んでいる誰もが TSLint とESLint 拡張機能を使用することを勧ています。加えて、Chrome デバッガ拡張機能を使用することも勧めていることがわかります。

VS Code は、ワークスペースが初めて開かれたときに、推奨拡張機能をインストールするようユーザーに促します。また、ユーザーは、**Extensions: Show Workspace Recommended Extensions** コマンドで推奨される拡張機能のリストをレビューすることが可能です。

![Show Recommendations](https://code.visualstudio.com/images/1_6_recommendations.png)

### PREVIEW Extension Packs

マーケットプレイスで「拡張機能パック」を公開するためのサポートが追加されました。拡張機能パックは、一緒にインストールすることができる拡張機能のセットです。これは、簡単に他のユーザーとお気に入りの拡張機能を共有できます。
その他のユースケースとして、PHP 開発者が迅速に VS Code で開発を始めるために役立つ PHP 開発環境のような、特定のシナリオ向けの拡張機能セットを作成することです。
この機能は、まだ、より多くの改良が必要であることを理解した上でプレビュー(試用)として利用可能です。

拡張パックは、他の複数の拡張機能に依存する拡張機能として表現されます。この依存性は、 `package.json` ファイル内の `extensionDependencies` アトリビュートにて表現されています。

例えば、PHP のための拡張機能パックは、デバッガ、PHP 言語サービス、フォーマッタを含めます:

```json
  "extensionDependencies": [
      "felixfbecker.php-debug",
      "felixfbecker.php-intellisense",
      "Kasik96.format-php"
  ]
```

VS Code に拡張機能パックをインストールすることで、依存関係に従い拡張機能をインストールします。

### Extension identifier badge

ワークスペースの推奨拡張機能と拡張パックのために必要な拡張機能識別子の発見を容易にするために、拡張機能の概要ビューにバッジの表示を追加しました。
拡張機能は、`publisher name` と `extension name` をピリオド `.` で区切ったユニークな名前を使用して識別されます。

![Extension identifier](https://code.visualstudio.com/images/1_6_extension-identifier.png).

### Extension update version check

VS Code にインストールされた拡張機能と互換性のある、新しいバージョンの拡張機能が [マーケットプレース](https://marketplace.visualstudio.com/vscode) で利用可能な場合、あなたにだけ古い拡張機能も見えます。

>**Note:** これは、最新の [vsce](https://github.com/Microsoft/vscode-vsce) パブリッシングツールを利用して公開された拡張機能にのみ適用されます

## Debugging

### Configurable External Terminal

外部ターミナルでデバッグターゲットを実行すると、デバッガー拡張機能への VS Code サービスとして実行されるようになり、この利用手法が広く採用につながることを願っています。
この有用な副作用は、既存の `terminal.external.windowsExec`、` terminal.external.osxExec`、と `terminal.external.linuxExec` に設定された外部ターミナルで利用可能です。

>**Note:** このリリースでは、組み込みのデバッグ拡張機能のみがこの新機能を採用しています

### Launch configuration supports 'npm' and other tools

頻繁によせられる機能リクエストの一つは、launch configuration から 'npm' スクリプトの直接実行をサポートすることでした。これは、既存の launch configuration の概念を次のように変更することによって可能になりました:

- PATH 上で利用可能な任意のプログラム (例えば、'npm', 'mocha', 'gulp', etc.) を、`runtimeExecutable` アトリビュートに指定することができ、引数は `runtimeArgs` を経由して渡すことが可能になりました
- `program` アトリビュートは、起動するプログラムとして npm スクリプトが既に指定している場合などにはそのまま利用できますが、もはや必須ではありません
- `port ` アトリビュートを使用して任意のデバッグポートを指定している場合、デバッグポートも同様に NPM スクリプトで一般的に指定されているため、`--debug-brk=nnnn` アトリビュートは自動的で追加されなくなりました

それでは、"NPM"の例を見てみましょう。`package.json` が、例えば 'debug' スクリプトを持っている場合：

```json
  "scripts": {
    "debug": "node --nolazy --debug-brk=5858 myProgram.js"
  },
```

対応する起動設定は次のようになります:

```json
{
	"name": "Launch via NPM",
	"type": "node",
	"request": "launch",
	"cwd": "${workspaceRoot}",
	"runtimeExecutable": "npm",
	"windows": {
		"runtimeExecutable": "npm.cmd"
	},
	"runtimeArgs": [
		"run-script", "debug"
	],
	"port": 5858
}
```

>**Note:** Windows では、正しい拡張子を持つ `npm.cmd` を実行可能ファイルとして指定してください。例えば、`npm.cmd` の替わりに `npm` も存在しますが、これは、Linux や macOS のシェルスクリプトになります

### Glob pattern support for Source Map setup (Source Map 設定のための glob パターンサポート)

トランスパイルされたコード(例えば、TypeScript)をデバッグするとき、ビルドプロセスは特定のディレクトリに JavaScript コードを生成しますが、生成されたコードを見つけるために Node.js デバッガを支援する必要があります。
以前の VS Code バージョンでは、生成されたソースコードのルートディレクトリを `outDir` 属性に指定することにより実現していました。

9 月のリリース版では、生成された JavaScript ファイルのセットを対象に、含めるまたは除外するファイルを指定可能な複数の glob パターンを使用することが可能になりました。このために、新しい array 型の `outFiles` アトリビュートが導入されましたが、古い `outDir` もサポートされていますが、将来的には廃止する予定です。

次の例では、生成されたコードは "out" と "node_modules" ディレクトリに配置されますが、生成されたテストコードを Source Map から除外する方法を示しています:

```json
{
  "sourceMaps": true,
  "outFiles": [
    "${workspaceRoot}/{out,node_modules}/**/*.js",
    "!${workspaceRoot}/out/tests/**/*.js"
  ]
}
```

### Experimental Node Debugger

Node.js バージョン 6.3+ 以降で利用可能な `--inspect` フラグを介し、[V8 Inspector Protocol](https://chromedevtools.github.io/debugger-protocol-viewer/v8/) を使用する実験的なデバッグの拡張を実装しました。これは [Chrome や他のターゲット](https://developer.chrome.com/devtools/docs/debugger-protocol)により公開されているものと同じプロトコルになります。
この拡張は[vscode-chrome-debug-core](https://github.com/Microsoft/vscode-chrome-debug-core) ライブラリ上で実行され、Chromeデバッガ拡張機能やその他いくつかの拡張機能で利用されます。

>**Note** Windows では、Node.js 6.x は 32-bit バージョンのみのサポートとなります。最新のビルドとなる Node.js v7 は 32-bit または 64-bit で動作します。詳しくは、[この issue](https://github.com/nodejs/node/issues/8155) を参照してください

この拡張は、最終的に vscode-node-debug と同等の機能を持つようになる予定ですが、それはまだ存在していません。
概要は[ここ](https://github.com/Microsoft/vscode-node-cdp-debug/issues/7)に記録されており[vscode-node-debug2](https://github.com/Microsoft/vscode-node-cdp-debug/issues) リポジトリと [vscode-chrome-debug-core](https://github.com/microsoft/vscode-chrome-debug-core/issues) リポジトリで問題などを見ることができます。

既存の Node.js の launch configuration に `"type": "node2"` 設定を持っているのであれば、Node.js v6.3 以降で実行する限り同じ動作となります。

>**Note**: 拡張機能の [README](https://marketplace.visualstudio.com/items?itemName=ms-vscode.node-debug2) に記載されるトラブルシューティングのヒントを参照してください

## Extension Authoring

### Authoring in TypeScript

VS Code 拡張機能開発のための Yeoman ジェネレータは、TypeScript バージョン 2.0.x を使用するように更新されました。新規に VS Code 拡張機能の開発を開始する場合、Yeoman と拡張機能ジェネレータをインストールするために `npm install -g yo generator-code` を実行後に、`yo code` を実行してください。TypeScript 1.8.x を使用して開発された既存の拡張機能を持っている場合は、次の手順を使用し TypeScript 2.0.3 に移行することができます。

`package.json` ファイルを開き、次の変更を行います:

- `devDependencies` にある TypeScript の定義を `"typescript": "x.x.x"` から `"typescript": "^2.0.3"` に変更します
- Node.js 型定義ファイルを利用するため devDependencies に `"@types/node": "^6.0.40"` を追加
- 開発している拡張機能の devDependencies が Mocha テストを持っている場合は、少なくとも Mocha 2.3.3 へ変更
- Mocha 型定義ファイルを利用するため devDependencies に `"@types/mocha": "^2.2.32"` を追加
- script セクションにある `compile` script を `"compile": "tsc -watch -p ./"` に変更し、`vscode:prepublish` を `"vscode:prepublish": "tsc -p ./"` に変更します。

`devDependencies` セクションは次のようになります。

```json
"devDependencies": {
    "typescript": "^2.0.3",
    "vscode": "^1.0.0", // Or a higher version if necessary
    "mocha": "^2.3.3",
    "@types/node": "^6.0.40",
    "@types/mocha": "^2.2.32"
}
```

そして、`scripts` セクションは次のようになります:

```json
"scripts": {
    "vscode:prepublish": "tsc -p ./",
    "compile": "tsc -watch -p ./",
    "postinstall": "node ./node_modules/vscode/bin/install"
}
```

- `tsconfig.json`ファイルを開き、`"noLib": true` を `"lib": [ "es6" ]` に書き換え、`"target": "es5"` を `"target": "es6"` に書き換えます。

ファイルは次のようになります。

```json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es6",
        "outDir": "out",
        "lib": [
            "es6"
        ],
        "sourceMap": true,
        "rootDir": "."
    },
    "exclude": [
        "node_modules",
        ".vscode-test"
    ]
}
```

その後、ワークスペースの typings フォルダを削除し、端末から `npm install` を実行します。

### Authoring in JavaScript 

Yeoman ジェネレーターは、JavaScript を書く際に役立つ TypeScript 2.0.x の機能を利用するために更新されました。
既存の拡張機能を移行する、または、JavaScript オーサリングのために TypeScript 2.0.3 を使用するのであれば、次の操作を行う必要があります。

`package.json` ファイルを開き、次の変更を行います:

- devDependencies に `"typescript": "^2.0.3"`　を追加
- Node.js 型定義ファイルを利用するため devDependencies に `"@types/node": "^6.0.40"` を追加
- 開発している拡張機能の devDependencies が Mocha テストを持っている場合は、少なくとも Mocha 2.3.3 へ変更
- Mocha 型定義ファイルを利用するため devDependencies に `"@types/mocha": "^2.2.32"` を追加
- また、JavaScript ソースコードにリンティングを適用する ESLint を使用することをお勧めします。これを行うには、更に開発者の依存関係として次のエントリを追加します: `"eslint": "^3.6.0"` また、[ESLint 拡張機能](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) をインストールすることをお勧めします

`devDependencies` のセクションでは、次のようになります:

```json
"devDependencies": {
    "typescript": "^2.0.3",
    "vscode": "^1.0.0", // Or a higher version if necessary
    "mocha": "^2.3.3",
    "eslint": "^3.6.0",
    "@types/node": "^6.0.40",
    "@types/mocha": "^2.2.32"
}
```

- `jsconfig.json`ファイルを開き、`"noLib": true` を `"lib": [ "es6" ]` に書き換え、`"target": "es5"` を `"target": "es6"` に書き換えます。

ファイルの内容は次のようになります:

```json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es6",
        "lib": [
            "es6"
        ]
    },
    "exclude": [
        "node_modules"
    ]
}
```

ターゲットが `es6` に設定されていても require ステートメントを使用して、他のモジュールをインポートする必要があることに注意してください。現在、Node.js は、ES2015 モジュールをサポートしていません。

### New APIs

* ドキュメントがディスクに保存される前に実行される `onWillSaveTextDocument` イベントを追加しました。
これは、保存前に、ドキュメントの変更を行うための拡張機能を可能にし、*保存時に未使用の import を削除*, *ファイルの最後に改行を挿入* のような機能を可能にします

* 拡張機能から構成オプションの追加/更新/削除を行うことが可能な `WorkspaceConfiguration#update` をサポートしました。例えば、拡張機能がコードアクションの警告からリンターを構成することができる様になります

* `Terminal#processId` は、端末のシェルプロセス (例えば bash や cmd) のプロセス ID を含む `Thenable<number>` を返します

* `window.createTerminal` は、パスとシェルの引数を設定するためのパラメータが含まれます。拡張機能から、Python や PowerShell REPL など、好みのシェルを起動することができます。

*  `window.onDidCloseTerminal` は、端末がユーザによって閉じられたときに簡単に追跡することを拡張機能で可能にする新しいイベントです。現在、追跡が可能な端末は、API によって作成された端末のみに制限されています。

### Breaking Change: Button order in messages

メソッド `showInformationMessage`、`showWarningMessage`、`showErrorMessage` のいずれかを使用するとき、常にメッセージの隣にアクションとして表示する文字列をセットして渡すことができるようになりました。
以前のリリースでは、メッセージの順序は逆転しており、最初に渡されたアクションが最後に示されていました。このリリースでは、この予期しない動作を修正し、アクションは定められた順序で表示されます。
この変更の影響を受けているかを確認するために、この API を使用している拡張機能で確認してください。新しい動作がより自然だと考えた結果、以前の動作を維持するコードの追加は行いませんでした。

### Breaking Change: Terminals are created in the background

API ドキュメントでも述べたように、`window.createTerminal` と `Terminal.sendText` は、バックグラウンドで作成されるようになりました。
そのため、拡張機能から端末パネル上に作成した端末を表示したいときは `Terminal.show` を利用した明示的な呼び出しが必要になります。

## Debug Extension Authoring

### VS Code Debug Protocol

VS Code デバッグプロトコル仕様は、TypeScript 定義ファイルの代わりに、[language neutral JSON schema](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/debugProtocol.json)として保持されています。このスキーマは、自動的に特定の言語のために、クライアントまたはサーバのライブラリを生成するために使用することができます。[vscode-debugadapter-node](https://github.com/Microsoft/vscode-debugadapter-node) プロジェクトは、スキーマから TypeScript で利用される `d.ts` を生成するための[簡単なプログラム](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/src/generator.ts)が含まれています。このプログラムは、他の言語で同様の仕組みをサポートするための出発点として使用することができます。

### External Terminal support for 'runInTerminal' request

デバッグアダプタは、`runInTerminal` リクエストと `kind` パラメータの値である `external` を介し **External Terminal** でデバッグターゲットを簡単に実行することができます。
**External Terminal** は、**Integrated Terminal** に代わるものであり、対話型端末からの読み取りや、実行されている端末で出力を制御する必要があるようなコマンドラインアプリケーションの開発をサポートしています。
`runInTerminal` を呼び出す前に、` initialize` リクエストに渡された引数が `supportsRunInTerminalRequest` アトリビュートを持っていることとその値が true であることを確認することによってフロントエンドクライアントがサポートします。

### Initial Configurations contributed by a command

デバッグアダプタは `package.json` ファイル内にある `debuggers` コントリビューションの `initialConfigurations` アトリビュートの値としてコマンド名を指定することが可能になりました。デバッグアダプタ拡張機能は、`launch.json` ファイルが最初に生成される際に呼び出され、その後、指定されたコマンドを登録することが可能になります。コマンドは、`launch.json` ファイルの初期内容を返す必要があります - このように、デバッグアダプタは `launch.json` のカスタマイズの柔軟性を持っています。
[VS Code Mock Debug](https://github.com/Microsoft/vscode-mock-debug) が良い参考例になります: ['initialConfigurations' contribution](https://github.com/Microsoft/vscode-mock-debug/blob/master/package.json#L83) と [command registration](https://github.com/Microsoft/vscode-mock-debug/blob/master/src/extension.ts#L29)

### Debug Protocol Additions

デバッグアダプタは、ブレークポイントのための 'hit count' のサポートを実装しました。これにより、ユーザーは、それが実行を '中断' する前に、ブレークポイントの多くのヒットを無視する方法を指定することができます。
`SourceBreakpoint` と `FunctionBreakpoint` タイプは、デバッグアダプタに hit count expression を渡すためのオプションのアトリビュートである `hitCondition` をサポートしています。

VS Code でこの機能のための UI を有効にするには、デバッグアダプタの `supportsHitConditionalBreakpoints` に true を設定する必要があります。

>**Note:** 9月リリース版の VS Code は、hit count condition を編集するための UI を実装していません

## Miscellaneous

### New location for dirty indicator when Tabs are disabled (タブが無効になっている場合のダーティーファイルインジケーターについて)

タブ（タブ付きヘッダ）が無効になっている場合、**閉じる (Clodse)** ボタンの上にダーティーファイル(まだ保存されていないファイル)を示すインジケータを表示することにしました。
これは、ダーティーファイルの指標として **閉じる (Clodse)** ボタンと交換することで他の場所と同一の経験を提供します。（例えば、**開いているエディタ(OPEN EDITORS)** 内、またはタブが有効になっている場合）

![Status](https://code.visualstudio.com/images/1_6_dirty.png)

### Electron update

このリリースでは、[Electron](https://github.com/electron/electron) フレームワークのメジャーアップデートを採用しました。Chrome レンダリングエンジン (**49** から **52** へ) と Node.js (**5.10.0** から **6.5.0** へ) の大きなバージョン変更を含んだ Electron バージョン 1.3.7 を実行することで、この VS Code のリリースで動作する全ての拡張機能は、Node.js **6.5.0** ランタイムのフル機能を期待することが可能になることを意味します。
Node.js の変更点の完全なリストについては、[Node.js Changelog](https://github.com/nodejs/node/blob/master/CHANGELOG.md) を参照してください。

> **Note:** 拡張機能でネイティブ `npm` モジュールを使用することはお勧めしません。しかしながら、ネイティブモジュールを使用した拡張機能を作成している場合は、それらのすべてを再コンパイルすることを忘れないでください

### Detecting a corrupt installation

私たちは、 VS Code の問題を調査し、それに多くの時間を費やすことで、それは、最終的に壊れた VS Code のインストールによって引き起こされていることを発見しました。
いくつかの拡張機能は、半永久的(次の更新まで)であるように、VSのコード製品を直接変更(パッチ)するなどの手法をとっていますが、これは問題の再現性を困難にする可能性があります。

そこで、ディスク上に配置される VS Code の一部分などが変更されたかどうかを検出するバックグラウンドチェック機能を追加しました。この機能は VS Code へのパッチをブロックするものではありませんが、パッチが適用された VS Code を実行することは、サポートされていないバージョンを実行していることを意味していることについての意識を高めて欲しいと思っています。

![corrupt install](https://code.visualstudio.com/images/1_6_corrupt-install.png)

### Built-in Extensions

マーケットプレイスで公開される選ばれた拡張機能を VS Code にバンドルすることが可能になりました。このような拡張機能は、_Built-in_ 拡張機能として表示されます。
これにより、私たちは、VS Code コア開発から _Built-in_ 拡張機能の開発を分離して行うことが可能になります。

![builtin](https://code.visualstudio.com/images/1_6_builtin.png)

### Improvements in Issue Reporting

問題の報告に関連して、しばしばインストールされた拡張機能によって引き起こされる問題を調査することがあります。このような調査の助けとなるために、私たちは、問題の説明にインストールされている拡張機能のリストを送信する **Help** > **Report Issues** アクションを追加しました。
我々は問題を追跡すると共に、最終的には迅速に問題を解決するためのより多くの情報を持っているので、問題を報告するときには、ぜひ、このアクションを使用してください。

### macOS Sierra support

Apple からの macOS Sierra 最終版リリース、および、Electron アップデートにより、いくつかの問題を修正することができました。(Retina ディスプレイ利用時、フォントやアイコンなどがシャープに見えていませんでした)
しかし、[一部のユーザーからの報告](https://github.com/Microsoft/vscode/issues/12473)には、背景にブロックノイズが表示されるなどがあり、この根本的な問題には Chrome が関連しており、カスタムカラープロファイルを使用している場合に発生ように見えます。この問題を軽減するための回避策として、強制的に GPU ラスタライズを有効にして VS Code を実行する解決策を提供します:

```bash
code --force-gpu-rasterization
```

## New Commands

新しく実装されたコマンドを簡単なリストにまとめました:

Key|Command|Command id
---|-------|----------
Search||
`kb(find.history.showNext)`|次の検索用語 (Next Search Term)|`find.history.showNext`
`kb(find.history.showPrevious)`|前の検索用語 (Previous Search Term)|`find.history.showPrevious`
`kb(toggleSearchCaseSensitive)`|大文字と小文字を区別のトグル(Toggle Case Senstive)|`toggleSearchCaseSensitive`
`kb(toggleSearchRegex)`|正規表現のトグル (Toggle Regex)|`toggleSearchRegex`
`kb(toggleSearchWholeWord)`|単語単位のトグル (Toggle Whole Word)|`toggleSearchWholeWord`
Integrated Terminal||
`kb(workbench.action.terminal.scrollUpPage)`|スクロールアップ(Scroll Up)|`workbench.action.terminal.scrollUpPage`
`kb(workbench.action.terminal.scrollDownPage)`|スクロールダウン(Scroll Down)|`workbench.action.terminal.scrollDownPage`
`kb(workbench.action.terminal.clear)`|端末のクリア(Clear Terminal)|`workbench.action.terminal.clear`
Extensions||
`kb(workbench.extensions.action.updateAllExtensions)`|全ての拡張機能をアップデート(Update All Extensions)|`workbench.extensions.action.updateAllExtensions`
`kb(workbench.extensions.action.openExtensionsFolder)`|拡張機能フォルダの表示(Open Extensions Folder)|`workbench.extensions.action.openExtensionsFolder`
Navigation||
`kb(workbench.action.focusActiveEditorGroup)`|アクティブなエディタグループへフォーカスを移動(Focus Active Editor Group)|`workbench.action.focusActiveEditorGroup`
`kb(workbench.action.switchWindow)`|スイッチウィンドウ(Switch Window (Instance))|`workbench.action.switchWindow`
ヘルプ(Help)||
`kb(update.showCurrentReleaseNotes)`|リリースノートの表示(Show Release Notes)|`update.showCurrentReleaseNotes`
`kb(workbench.action.reportIssues)`|問題の報告(Report Issues)|`workbench.action.reportIssues`

## Notable Changes

このリリースではいくつかの注目すべき問題が解決されます: 

* [241](https://github.com/Microsoft/vscode/issues/241): Windows: Jump list misses files and folders in the recent category when opened
* [7470](https://github.com/Microsoft/vscode/issues/7470): Save file even w/o file changes - so that Nodemon, Gulp, Chokidar and other file watchers restart
* [7817](https://github.com/Microsoft/vscode/issues/7817): Integrated terminal scrolling not working in oh-my-zsh
* [7951](https://github.com/Microsoft/vscode/issues/7951): Images do not show updated when changed on disk
* [8819](https://github.com/Microsoft/vscode/issues/8819): Allow to Ctrl+click in File > Open Recent to open in new window
* [9354](https://github.com/Microsoft/vscode/issues/9354): Ability to remove file permanently (bypass trash)
* [9448](https://github.com/Microsoft/vscode/issues/9448): Lower case drive letter in Open New Command Prompt command on Windows
* [11049](https://github.com/Microsoft/vscode/issues/11049): Text cursor stops blinking in integrated terminal if you run external command
* [11129](https://github.com/Microsoft/vscode/issues/11129): Hovering cursor over integrated terminal on Mac shows a low-contrast cursor
* [11244](https://github.com/Microsoft/vscode/issues/11244): Scroll is gone after exiting vi in integrated terminal
* [11275](https://github.com/Microsoft/vscode/issues/11275): Terminal.dispose should not show the panel if it is hidden
* [11318](https://github.com/Microsoft/vscode/issues/11318) & [8365](https://github.com/Microsoft/vscode/issues/8365): Search and Problems views are now consistent with others in highlighting lines.
* [11727](https://github.com/Microsoft/vscode/issues/11727): Goto declaration should store current cursor in navigation history
* [11976](https://github.com/Microsoft/vscode/issues/11976): MarkerService and ProblemsView do not scale well and block UI thread
* [12574](https://github.com/Microsoft/vscode/issues/12574): Terminal scroll bar appears on top after hiding and displaying it

These are the [closed bugs](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22September+2016%22+is%3Aclosed) and these are the [closed feature requests](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22September+2016%22+is%3Aclosed+label%3Afeature-request) for the 1.6 update.
[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22September+2016%22+is%3Aclosed)と、1.6 アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22September+2016%22+is%3Aclosed+label%3Afeature-request)です。

## Contributions to Extensions

私たちのチームは、いくつかの VS Code 拡張機能の提供とメンテナンスに貢献しています。最も顕著な拡張機能としては：

* [Go](https://marketplace.visualstudio.com/items?itemName=lukehoban.Go)
* [Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* [VSCodeVim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)

## Thank You

最後になりましたが、VS Code をより良いものにするために協力してくれた次の方々に多大なる感謝を込めて：

* [Fred Bricon (@fbricon)](https://github.com/fbricon): Fix typos in log messages [PR vscode-languageserver-node#92](https://github.com/Microsoft/vscode-languageserver-node/pull/92)
* [Henning Dieterichs (@hediet)](https://github.com/hediet): Non-normative inconsistencies [PR language-server-protocol#68](https://github.com/Microsoft/language-server-protocol/pull/68)
* [Luke Persola (@Persola)](https://github.com/Persola): Correct grammar/rephrase README [PR language-server-protocol#56](https://github.com/Microsoft/language-server-protocol/pull/56)
* [Amadeusz Leonardo Juskowiak (@alfanick)](https://github.com/alfanick): Relative Line Number support  [PR #12055](https://github.com/Microsoft/vscode/pull/12055)
* [Artem Govorov (@ArtemGovorov)](https://github.com/ArtemGovorov): Clear buffered output on output clear event [PR #12057](https://github.com/Microsoft/vscode/pull/12057)
* [Logan Fleur (@effleurager)](https://github.com/effleurager): Fixed typo in git action error [PR #12419](https://github.com/Microsoft/vscode/pull/12419)
* [Jun Han (@formulahendry)](https://github.com/formulahendry): Fixes #9482: AutoClosePair between tags [PR #9535](https://github.com/Microsoft/vscode/pull/9535)
* [Kei Son (@heycalmdown)](https://github.com/heycalmdown)
  * fix minor typo [PR #11492](https://github.com/Microsoft/vscode/pull/11492)
  * Added new command to switch between workspaces [PR #11630](https://github.com/Microsoft/vscode/pull/11630)
* [Yuki Ueda (@Ikuyadeu)](https://github.com/Ikuyadeu): Remove workerMainCompatibility.html #11306 [PR #11369](https://github.com/Microsoft/vscode/pull/11369)
* [@marktrz](https://github.com/marktrz)
  * Implements whitespace rendering for "boundary" and "all" modes. [PR #11122](https://github.com/Microsoft/vscode/pull/11122)
  * Implements system variable "workspaceRootFolderName". [PR #11128](https://github.com/Microsoft/vscode/pull/11128)
* [Sam El-Husseini (@microsoftsam)](https://github.com/microsoftsam): Using Cmd+Scroll to zoom on a mac [PR #12477](https://github.com/Microsoft/vscode/pull/12477)
* [Denis Malinochkin (@mrmlnc)](https://github.com/mrmlnc): Display language identifier in Language Mode drop down [PR #12031](https://github.com/Microsoft/vscode/pull/12031)
* [Dmitry Nikitenko (@nDmitry)](https://github.com/nDmitry) and [@FichteFoll](https://github.com/FichteFoll): Redone YAML grammar [PR #11666](https://github.com/Microsoft/vscode/pull/11666)
* [Nic Holthaus (@nholthaus)](https://github.com/nholthaus): Add `konsole` as default terminal for KDE-plasma [PR #11452](https://github.com/Microsoft/vscode/pull/11452)
* [Paul Oppenheim (@pauloppenheim)](https://github.com/pauloppenheim): vscode-linux-*-build-deb - expected permission bits [PR #11558](https://github.com/Microsoft/vscode/pull/11558)
* [@Romanito](https://github.com/Romanito): Enable "Open with Code" on drive roots in Windows Explorer [PR #11870](https://github.com/Microsoft/vscode/pull/11870)
* [@sprinkle131313](https://github.com/sprinkle131313): Fixes debugger config launch for Linux and OSX. [PR #11092](https://github.com/Microsoft/vscode/pull/11092)
* [@ted-piotrowski](https://github.com/ted-piotrowski): Fix gulp methods for targeting arm systems [PR #12486](https://github.com/Microsoft/vscode/pull/12486)
* [Vincenzo Chianese (@XVincentX)](https://github.com/XVincentX)
  * Provide a changelog tab when this file is bundled in the package [PR #12035](https://github.com/Microsoft/vscode/pull/12035)
  * Take changelog from remote if provided [PR #12455](https://github.com/Microsoft/vscode/pull/12455)
* [Eklavya @eklavyamirani](https://github.com/eklavyamirani) Markdown syntax highlighting to support alternative header styles [PR #11066](https://github.com/Microsoft/vscode/pull/11066)

<!-- In-product release notes styles.  Do not modify without also modifying regex in gulpfile.common.js -->
<a id="scroll-to-top" role="button" aria-label="scroll to top" onclick="scroll(0,0)"><span class="icon"></span></a>
<link rel="stylesheet" type="text/css" href="css/inproduct_releasenotes.css"/>
