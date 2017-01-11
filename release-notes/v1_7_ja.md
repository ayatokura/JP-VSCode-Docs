# October 2016 (version 1.7)

## 1.7.1 Recovery Build

JavaScript タイピングファイルの自動取得機能 ("Automated Typings Acquisition") を無効にする 1.7.1 Recovery Build をリリースしました。
NPM レジストリへの不要な負荷を避けるために、私たち開発チームは調整を必要とし、TypeScript と npmjs.org チームと緊密に協力しています。私たちは、将来のリリースでこの機能を有効にしたいと考えています。

もし、詳細について興味を持ったなら、出来事の経緯および NPM と VS Code の対応策を説明する[ブログの記事](http://code.visualstudio.com/blogs/2016/11/3/rollback)を参照してください。

## October Release Summary

Visual Studio Code 10月リリース版へようこそ。このリリースではいくつかの重要な更新があり、ハイライトは次のとおりです:

* **[Horizontal layout](#horizontal-layout)** - エディタの垂直または水平分割をサポート
* **[Keyboard Shortcuts Reference](#keyboard-shortcuts-reference)** - 印刷可能なOS 毎のキーボードショートカットの PDF チートシートを新たに提供
* **[JavaScript IntelliSense](#better-javascript-intellisense)** - IntelliSense のために VS Code が自動的に JavaScript モジュールおよびライブラリ、typings 情報をインストール
* **[CSS autocompletion within HTML](#css-completions-in-html)** - HTML に埋め込まれた CSS の多彩な自動補完をサポート
* **[Debug hit count control](#hit-count-conditional-breakpoints)** - ブレークポイントの 'hit count conditions' 設定をサポート
* **[Simplified Node.js debugging](#simplified-launch-configuration)** - Node.js デバッグセッションの設定をより簡単に
* **[Keymaps for Sublime and Atom](#keymaps-category)** - 人気のキーボードショートカットを VS Code で利用可能に
* **[Disable extensions](#disable-extensions)** - グローバル、または、特定のワークスペースの拡張機能を素早く無効にすることが可能に
* **[Improved TypeScript and JavaScript Grammar](#improved-typescript-and-javascript-grammar)** - Dark+ テーマで変数と関数リファレンスの色付けをサポート
* **[Extension Packs](#extension-packs)** - 拡張機能パックの依存関係を拡張機能の詳細で参照可能に

VS Code の注目ポイントに関連するアップデート情報は、リリースノートの次のセクションに配置されています。その他のアップデートは、次のとおりです:

* **[Workbench](#workbench)** - いくつかのビューの状態をユーザー設定に保存することにより再起動後も持続、クイックオープンから複数のファイルを開くことが可能に
* **[Editor](#editor)** - キーボードショートカットのリファレンス、より細かな書式設定コントロール
* **[Languages](#languages)** - JavaScript と CSS の改善
* **[Extensions](#extensions)** - マーケットプレイスに `Keymaps` と `Formatters` のための新しいカテゴリを追加
* **[Node.js Debugging](#node-debugging)** - マルチターゲットデバッグのサポート、新しいデバッグ設定の追加
* **[Extension Authoring](#extension-authoring)** - 拡張機能の変更履歴を扱う CHANGELOG.md ファイルのサポート、エディタタブのコンテキストメニューへ項目の追加が可能に

## Workbench

### Horizontal layout

エディタグループのレイアウトを縦または横のいずれかに変更することが可能になりました。どちらのレイアウトもエディタの移動やリサイズ、エディタ・グループの変更など以前と同じように動作を適用できます。

![Horizontal](http://code.visualstudio.com/images/1_7_horizontal.png)

現在のワークスペースで水平方向のレイアウトを有効にするには:

* **View** メニューの **Toggle Editor Group Layout** による切り替え
* コマンドパレットから **Toggle Vertical/Horizontal Editor Group Layout** を実行
* **OPEN EDITORS** ビューのヘッダ内アクションから変更

![toggle horizontal layout](http://code.visualstudio.com/images/1_7_toggle-horizontal-layout.png)

すぐに 2 つのレイアウトを切り替えるためのキーボードショートカット `(macOS: ⌥⌘1) ` が提供されます。
レイアウトの選択後、現在のワークスペースのためにレイアウトの設定を保存されるため、再起動後にも復元されます。

### Toggle Maximized Panel

パネルの大きさを最大化する(全体の高さの80％)グローバルワークベンチコマンドを導入しました。パネルが既に最大化されている場合、このコマンドは、その前のサイズのパネルを縮小します。パネルに出力される多くの情報をすぐに確認する場合など、これは本当に便利です。このコマンドは、現在、どのキーボードショートカットにもバインドされていませんが、簡単に独自の[キーバインドを追加](http://code.visualstudio.com/docs/customization/keybindings)することができます。

### Toggle Sidebar and Hide Status Bar now persisted in user settings

手動でユーザー設定ファイルを更新することなく、その状態を永続化させるために、表示メニューのトグルの一部を変更しました。例えば、これで、設定ファイルをコピーして別のマシンで同じ状態を簡単に復元できるようになります。

以下の設定は、表示メニューからそれらを変更した場合、ユーザー設定ファイルに変更が反映されます: 

* `workbench.sideBar.location` は、サイドバーの位置を制御します (左または右)
* `workbench.statusBar.visible` は、ステータスバーの表示を制御します

また、[表示]メニューからズームレベルを変更すると、今のレベルを `window.zoomLevel` に書き込みます。

### Open multiple files from Quick Open

[Will Prater (@wprater)](https://github.com/wprater) のおかげで、クイックオープンに表示されるファイルにカーソルを合わせ、右矢印キーを押すことにより複数のファイルを開くことができるようになりました。これは、クイックオープンからファイルを選択し、選択されたファイルをバックグラウンドで開き続けることが可能になります。

## Editor

### Keyboard Shortcuts Reference

**Help** > **Keyboard Shortcuts Reference** により、VS Code コマンドのキーボードショートカットが記載された印刷可能な PDF リファレンスシートが Web ブラウザに表示されます。便利なこのリファレンスを手元に置いておくことで、時間がない人でも VS Code のパワーユーザーになれるでしょう。

macOS で提供されるシートの例です:

![keyboard shortcuts pdf](http://code.visualstudio.com/images/1_7_keyboard-shortcuts-pdf.png)

VS Code がサポートする 3 つのプラットフォーム固有バージョンへのリンクは次のとおりです:

* [Windows](https://go.microsoft.com/fwlink/?linkid=832145)
* [macOS](https://go.microsoft.com/fwlink/?linkid=832143)
* [Linux](https://go.microsoft.com/fwlink/?linkid=832144)

>**Note:** また、code.visualstudio.com に掲載される[入門ビデオ](http://code.visualstudio.com/docs/introvideos/overview)をブラウザから参照するためのメニューコマンドを追加しました。(**Help** > **Introductory Videos**)

### Format Document / Format Selection

エディタは現在、**Format Document** (`kb(editor.action.formatDocument)`) と **Format Selection** (`kb(editor.action.formatSelection)`) の 2 つの明示的なフォーマットアクションを提供します。

![format on context menu](http://code.visualstudio.com/images/1_7_format-context-menu.png)

また、JavaScript、TypeScript、JSON、および HTML のデフォルトのフォーマッターを有効/無効にする、新しい構成オプションを追加しました。同じ言語の別な書式設定拡張機能がインストールされ、それを利用したい場合に、このオプションを使用します。

ソースコードの[書式設定の拡張機能](https://marketplace.visualstudio.com/search?target=VSCode&category=Formatters&sortBy=Downloads)を簡単に検索し見つけることができるように、マーケットプレイスに新しい `Formatters` [カテゴリ](#formatters-category)を追加しました。

![marketplace formatter extensions](http://code.visualstudio.com/images/1_7_marketplace-formatters.png)

## Languages

### Better JavaScript IntelliSense

>**Note:** 訳者注: ATA 機能は、多くのネットワークトラフィックを発生させることが確認され、現在、機能が無効にされています。詳細は冒頭の 1.7.1 Recovery build の項目にてご確認ください

現在の VS Code では、JavaScript ファイルにおいて IntelliSense 機能を提供するために、TypeScript 言語サーバーを使用しています。
過去に、`jsconfig.json` ファイルを作成し、手動ですべてのモジュールと使用しているライブラリの型付け（型定義）ファイルをインストールする必要がありました。
特に、あなたが純粋な JavaScript 開発者である場合、それらの作業は簡単な雑用では済まなかったはずです。

私たちは、TypeScript チームの友人と話をし、その中で、彼らは「自動タイピングの取得 "Automated Typings Acquisition" 」を思い付きました。ATA は、ほとんど目にすることのない typings ファイルを構成します。
ATA が有効になっている TypeScript 言語サーバーは、`package.json` ファイルを監視し、自動的にすべての依存関係の型付けのファイルをインストールしファイルシステム上にキャッシュします。
それはよく知られているクライアント側ライブラリへの参照を見つけたときと同じことを行います。
インテリセンスを起動すると、TypeScript サーバはキャッシュされた typings ファイルを使用します。
キャッシュは、すべてのワークスペース間で共有されます。
`jsconfig.json` ファイルがない場合、TypeScript サーバは、ワークスペース内のすべてが同じプロジェクトに属していることを前提として振る舞います。

VS Code を利用するユーザーが、できるだけ早くこの機能を手に入れることができればと思えたことが、とてもクールだと私たちは考えました。ATA の統合はまだ荒削りですが、この機能をデフォルトで有効にすることを決めました。
万が一、問題が発生した場合は、ユーザー設定の `typescript.disableAutomaticTypeAcquisition` を `true` にした設定することで、この機能を無効にすることが可能です。

ここでは、ATA を使用する際に知っておくべきいくつかのポイントを上げておきます:

- ATA は下位互換性があります。すでに `typings` フォルダを持っているか、`npm` を使用して typings ファイルをインストールしている場合、それらのファイルが ATA よりも優先されます
- ATA は、タイピングファイルの最新バージョンを取得します。ライブラリやモジュールの古いバージョンに依存している場合、ライブラリやモジュールと typings ファイルに記述された API によって公開される実際の API との間に不一致が存在する可能性があります。もし、typings ファイルの特定のバージョンが必要な場合は、それを手動でインストールすることができます: `npm install @typings/<module name>@x.y.z`
- npm モジュールが増えればバンドルされる typings ファイルもその数だけ増加します。つまり、typings ファイルを取得する唯一の方法は、モジュールをインストールすることです。ATA は npm モジュールそのものをインストールしないので、その作業はユーザー自身で行う必要があります
- `package.json` ファイルの依存関係が変更された際、対応する typings ファイルを取得し、インテリセンスで利用可能にするために短い遅延が発生します

### CSS completions in HTML

CSS スタイル用のコード補完、検証および注釈のカラー表示など CSS 言語機能を HTML 内で利用可能になりました。

![css intellisense in html](http://code.visualstudio.com/images/1_7_css-intellisense-in-html.png)

### Improved TypeScript and JavaScript Grammar

TypeScript と JavaScript 構文の強調表示は、TypeScript チームによって [TypeScript TextMate 文法](https://github.com/Microsoft/TypeScript-TmLanguage)に基づいて作成されました。ここ数カ月で、文法は完全に書き直されています。
主な目標は、可能な限り報告された多くの問題に対処することでした。

さらに、JavaScript React 構文のような機能をサポートしながら、[Atom grammar](https://marketplace.visualstudio.com/items?itemName=ms-vscode.js-atom-grammar) のような人気のある JavaScript 文法のようにスコープを生成することで、既存のカラーテーマと組み合わせたより良い体験を提供したいと考えました。

そして、努力の結果、変数や関数の参照を報告するための要求を含む、100 以上の問題が修正されました。本リリースでは、新しいスコープを活用し、デフォルトの Dark Plus と Light Plus テーマにおいて変数と関数参照を色付けすることを決めました。
気に入ってくれることを私たちは願っています！

Note: すでに、Dark+ と Light + テーマ上で、拡張機能として提供している [Latest TypeScript and JavaScript grammar extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.typescript-javascript-grammar)を使用している場合は、今すぐこの拡張機能をアンインストールしてください

### Linter Extensions

`vscode-eslint` と `vscode-tslint` 拡張機能により、保存時に自動的に修正可能な警告を正すための設定を提供します。

```json
{
    "eslint.autoFixOnSave": true,
    "tslint.autoFixOnSave": true,
}
```

Note: `files.autoSave` に　`afterDelay` が設定されている場合、上記の設定は無視されます。

## Extensions

### Keymaps category

キーボードショートカットは、生産性に不可欠であり、キーボード入力の習慣を変えることは厳しいものになります。この問題に対処するために、2 つの新しい拡張機能を追加し、マーケットプレイスに新しい `Keymaps` カテゴリを導入しました。この目的は、新しいキーボードショートカットを学ぶ必要性を除去することにより、エディタを切り替えやすくすることです。

私たちは、[Atom](https://marketplace.visualstudio.com/items?itemName=ms-vscode.atom-keybindings) と [Sublime Text](https://marketplace.visualstudio.com/items?itemName=ms-vscode.sublime-keybindings) で利用されるキーバインドを実現する拡張機能を作成しました。今後も、最も人気のあるキーボードショートカットの一部を取り入れ、我々に欠けているものをフィードバックをしたいと思います。私たちが提供する、キーボードショートカットに問題がある場合は、Issue での報告や、リポジトリに PR を行ってください。

![Keymaps](http://code.visualstudio.com/images/1_7_keymaps.png)

さらに、`keybindings` コントリビュート・ポイントを使用することで独自のキーマップ拡張機能を作成することができ、マーケットプレイスの `Keymaps` カテゴリに追加することができます。

### Formatters category

書式を整形する機能(フォーマッタ)を持つ拡張機能がすでに多く存在しています。最も人気のあるフォーマッタのいくつかは、100K 以上のインストール実績を持っています！私たちは、簡単にフォーマッタを見つけることができるよう、マーケットプレイスに新しい `Formatters` カテゴリを作成しました。
マーケットプレイスで[検索](https://marketplace.visualstudio.com/search?target=VSCode&category=Formatters&sortBy=Downloads) し、すぐにフォーマッタをインストールすることが可能になります。

下記は、私たちのお気に入りのフォーマッタです: 

* [beautify](https://marketplace.visualstudio.com/items?itemName=HookyQR.beautify)
* [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)
* [Clang-Format](https://marketplace.visualstudio.com/items?itemName=xaver.clang-format)
* [PHP Formatter](https://marketplace.visualstudio.com/items?itemName=Sophisticode.php-formatter)
* [Stylesheet Formatter](https://marketplace.visualstudio.com/items?itemName=dbalage.vscode-stylesheet-formatter)

### Disable extensions

多くの場合、ユーザーは複数のワークスペースを持っており、様々な拡張機能が、これらのワークスペースをサポートするためにインストールされています。ほとんどの場合、これらの拡張機能はシングルワークスペースで排他的に利用され、他人には必要ではありません。
例えば、あなたが JavaScript と Go 言語ワークスペースを持っている場合、Go 言語ワークスペースに JavaScript リンティング拡張機能は必要なく逆もまた同様です。
このリリースでは、ワークスペースのために必要だと思う拡張機能だけを実行することができ、その他の拡張機能を無効にすることができるようになります。拡張機能を実行したくない場合にもアンインストールする必要はありませんし、完全な VS Code アプリケーションのために拡張機能を無効にすることができます。

![Disable Extension](http://code.visualstudio.com/images/1_7_disableExtension.png)

また、VS Code 上から数回のクリックで、すべての拡張機能を有効/無効にすることができます。

![Disable All Extensions](http://code.visualstudio.com/images/1_7_disableAll.png)

### Extension packs

前回のリリースで、依存する他の拡張機能のインストールを解決するために「拡張パック」を導入しました。このリリースでは、パックのインストール時にインストールされる依存関係を表示するように拡張機能エディタに新しいタブ (Dependencies) を追加しました。

![Extension Pack](http://code.visualstudio.com/images/1_7_extensionPack.png)

拡張パックをアンインストールすると、依存関係を持つすべての拡張機能がアンインストールされます。

## Node Debugging

### Simplified launch configuration

Node.js のデバッグをできるだけ簡単にセットアップできるように、初期の `launch.json` に関連する作業をできるだけ簡素化することにしました：

* 必要だが、めったに変更されない属性については、それらを変更する必要がないことを見た目でも確認できるように灰色で表示されます
* それほど頻繁に使用されない属性(適切なデフォルト値を持ちます)は、「ノイズ」を低減するために、初期設定から削除されました。このような属性は、IntelliSense を使用して簡単に見つけることができます。
* コメントとオンラインドキュメントへのリンクが追加されました。
* オンラインデバッグに関する[ドキュメント](http://code.visualstudio.com/docs/editor/debugging#_launch-configurations)が書き直され、改善されました。

![launchjson](http://code.visualstudio.com/images/1_7_launchjson.png)

>**Note:** 私たちは VS Code にビルトインされる Node.js デバッガのみを変更することができます。他のデバッグ拡張機能で、同様の変更を行うためには、デバッグ拡張昨日の作者に頼る必要があります（必要であれば）

### Hit count conditional breakpoints

VS Code は、ブレークポイントのための 'hit count condition' 設定をサポートしました。（'expression condition'に加え、しばらく前に導入されました）
'hit count condition' は、'break' 実行前にブレークポイントにヒットする必要がある回数を制御します。

![HitCount](http://code.visualstudio.com/images/1_7_hitCount.gif)

'hit count condition' では、respected と式の正確な構文がどのように見えているかは、使用するデバッガ拡張機能に依存します。このマイルストーンでは、VS Code に組み込まれた Node.js デバッガだけが、ヒットカウントをサポートしています（他のデバッガー拡張機能がすぐにこの機能をサポートすることを願っています）。

Node.js デバッガによってサポートされているヒットカウントの構文は、整数または演算子 `<`, `<=`, `=`, `>`, `>=`, `%` のいずれか、また、`%` の後には整数が続きます。

いくつかの例:

- `>10` 10 ヒット後、常にブレーク
- `<3` 最初の 2 ヒットでブレーク
- `10` `>=10` と同じ
- `%2` 他のすべてのヒットでブレーク

### Multiple target debugging

10月のリリースでは、'マルチターゲットデバッグ' の実験的な早期実装が含まれています。この機能により、複数のデバッグセッションを VS Code の単一インスタンス(単一のプロジェクトフォルダ)内で同時にアクティブにすることが可能になります。

この機能は、次のようなシナリオに役立ちます:

* 拡張機能とデバッグアダプタ、または、言語サーバを同時にデバッグ
* 単一のプロジェクトフォルダからクライアントとサーバーをデバッグ
* クラスタ化されたプログラムのデバッグ

>**Note:** このマイルストーンでは、マルチターゲットデバッグのための内部抽象化を得ることと、どのように UI でこれを見せるかに焦点を当てています。そのため、マルチターゲットデバッグの UI と、それがどのように設定されているかについては、非常に **実験的** であり、間違いなく次のマイルストーンに渡って変更されて行くでしょう。

'マルチターゲットのデバッグ' を有効にするには `composite` タイプで新しい launch configuration を作成し、アレイ型属性 `configurationNames` を追加します。その属性の下で並列に起動する必要があり、他の launch configuration の名前をリストします。

`composit` 構成を起動した後、個々のセッションは、コールスタックビューでトップレベルの要素として表示されます。アクション(例えば、フローティングデバッグウィジェットないのすべてのアクション) は、常にコールスタックビューで現在選択されているセッションで実行されます。

![multiDebug](http://code.visualstudio.com/images/1_7_multiDebug.gif)

### Debug settings

次の新しい設定を導入しました：

* `debug.allowBreakpointsEverywhere` - ブレークポイントは任意のファイル(それだけではなく、明示的に登録されているもので)に設定されることを許可します。既存のデバッガ (例えば、Node.js のデバッガ) を使用し、新しい (トランスパイルが必要な) 言語をデバッグする場合に便利です。
* `debug.openExplorerOnEnd` - デバッグセッション終了時にエクスプローラを自動的に開くよう制御します

## Extension Authoring

### Breaking Change: `MarkedString[]` semantics

`MarkedString | MarkedString[]` を返す API 関連実装のセマンティクスを変更しました。各 `MarkedString` は、視覚的に水平線により他から分離されます。`HoverProvider` と ` Decoration` API のどちらも、この影響を受けています。

### Changelogs

VS Code の拡張機能詳細ビューから、拡張機能の CHANGELOG.md を直接表示することが可能になりました。

拡張機能の作者は、拡張機能の README.md に記載されていた既存の変更履歴を、個別の CHANGELOG.md ファイルへ移動することを推奨します。
CHANGELOG.mdは、拡張機能のワークスペースのルートに配置された場合、README.md と同様に `vsce` パブリッシングツールにより自動的に含まれます。

### Provide menu entries for the editor tab context menu

拡張機能のメニューエントリをエディタ・タブのコンテキストメニューに追加することが可能になりました(タブ機能が無効になっていても、これは動作します)。追加に必要なコントリビュートの関連するメニューパスは、`editor/title/context` です。

例:

```json
"commands": [{
    "command": "doSomething",
    "title": "Do Something"
}],
"menus": {
    "editor/title/context": [
        {
            "command": "doSomething"
        }
    ]
}
```

### onDidChangeVisibleTextEditors event

見えているエディタリストが変更されるたびにトリガーを発生させる [`onDidChangeVisibleTextEditors`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L3383) イベントを追加しました。

### Update Now: Using latest vscode.d.ts

今までと同様に、拡張 API の最新かつ最良のバージョンが [`vscode.d.ts`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts) ファイルに定義されています。

>**Note:** API バージョン 1.7.0 以降を使用するように拡張機能を更新する場合は、[vscode](https://www.npmjs.com/package/vscode)-node-module (^1.0.3) の最新バージョンを使用していることを確認し、TypeScript 2.0を使用してください

最新の vscode モジュールを利用するよう、既存の拡張機能を移行する方法については、[こちら](http://code.visualstudio.com/updates/v1_6#_extension-authoring)をお読みください。

## New Commands

Key|Command|Command id
---|-------|----------
`kb(workbench.action.toggleEditorGroupLayout)`|エディターグループの縦/横レイアウトを切り替える (Toggle editor group layout)|`workbench.action.toggleEditorGroupLayout`
`unassigned`|最大化されるパネルの切り替え (Toggle Maximized Panel)|`workbench.action.toggleMaximizedPanel`
Formatting||
`kb(editor.action.formatDocument)`|ドキュメントのフォーマット (Format document)|`editor.action.formatDocument`
`kb(editor.action.formatSelection)`|選択範囲のフォーマット (Format selection)|`editor.action.formatSelection`
Integrated Terminal||
`kb(workbench.action.terminal.scrollToTop)`|一番上にスクロール (Scroll to top)|`workbench.action.terminal.scrollToTop`
`kb(workbench.action.terminal.scrollToBottom)`|一番下にスクロール (Scroll to bottom)|`workbench.action.terminal.scrollToBottom`

## Notable Changes

* [929](https://github.com/Microsoft/vscode/issues/929): Windows 10: focus is not put to window but taskbar blinks
* [2814](https://github.com/Microsoft/vscode/issues/2814): Windows: Reveal in Explorer feature no longer bring the explorer window in front of vscode
* [6466](https://github.com/Microsoft/vscode/issues/6466): Open in Command Prompt doesn't open cwd when using cmder
* [10210](https://github.com/Microsoft/vscode/issues/10210): Can't copy the values of debugging elements such as exception messages
* [11334](https://github.com/Microsoft/vscode/issues/11334) & [13229](https://github.com/Microsoft/vscode/issues/13229): Improvements to terminal IME support
* [11431](https://github.com/Microsoft/vscode/issues/11431): RPM package lacks shortcut in PATH
* [12036](https://github.com/Microsoft/vscode/issues/12036): VS Code is very laggy when used on a system with touchscreens
* [12260](https://github.com/Microsoft/vscode/issues/12260): Not enough storage is available to process this command in terminal
* [12969](https://github.com/Microsoft/vscode/issues/12969): HTML: comments inside a script tag no longer sensitive to script language
* [13554](https://github.com/Microsoft/vscode/issues/13554): Integrated terminal occasionally wraps some lines
* [14102](https://github.com/Microsoft/vscode/issues/14102): Fold the default settings by default and remember editor state

[13919](https://github.com/Microsoft/vscode/issues/13919) の対応で、Windows でのファイル拡張子の関連付けが壊れていました。VS Code で開くには、ファイル拡張子の関連付けを再設定する必要があります。

[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22October+2016%22+is%3Aclosed)と、1.7 アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22October+2016%22+is%3Aclosed)です。

## Contributions to Extensions

私たちのチームは、いくつかの VS Code 拡張機能の提供とメンテナンスに貢献しています。最も顕著な拡張機能としては：

* [Go](https://marketplace.visualstudio.com/items?itemName=lukehoban.Go)
* [Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* [VSCodeVim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)

## Thank You

最後になりましたが、VS Code をより良いものにするために協力してくれた次の方々に多大なる感謝を込めて:

* [@barakd](https://github.com/barakd):  Git quick open should correct invalid branch names [PR #12194](https://github.com/Microsoft/vscode/pull/12194)
* [Christian Alexander (@ChristianAlexander)](https://github.com/ChristianAlexander)
  *  Use default cursor in feedback menu text. #12926 [PR #13719](https://github.com/Microsoft/vscode/pull/13719)
  *  Add --disable-gpu option to cli help. (#13706). [PR #13760](https://github.com/Microsoft/vscode/pull/13760)
* [Cliff Koh (@cliffkoh)](https://github.com/cliffkoh):  Fix typos and consistency issues [PR #14078](https://github.com/Microsoft/vscode/pull/14078)
* [Sergey Shakhnazarov (@daserge)](https://github.com/daserge):  Avoiding "write EPIPE process.send" error on exit [PR #13774](https://github.com/Microsoft/vscode/pull/13774)
* [xzper (@f111fei)](https://github.com/f111fei):  Fixed #13670 [PR #13739](https://github.com/Microsoft/vscode/pull/13739)
* [@greams](https://github.com/greams):  Add option for --list-extensions arg [PR #13131](https://github.com/Microsoft/vscode/pull/13131)
* [Kei Son (@heycalmdown)](https://github.com/heycalmdown):  Add an indicator for the current window [PR #13113](https://github.com/Microsoft/vscode/pull/13113)
* [Huachao Mao (@Huachao)](https://github.com/Huachao):  Update handlebars block comments symbols [PR #12271](https://github.com/Microsoft/vscode/pull/12271)
* [Michael Hudson (@Huddo121)](https://github.com/Huddo121):  Increase coverage of tests for IAction.isAction() [PR #13992](https://github.com/Microsoft/vscode/pull/13992)
* [Yuki Ueda (@Ikuyadeu)](https://github.com/Ikuyadeu):  fix ini #13648 [PR #13923](https://github.com/Microsoft/vscode/pull/13923)
* [Jeong Woo Chang (@inspiredjw)](https://github.com/inspiredjw):  Cannot read property 'uri' of null fix [PR #13263](https://github.com/Microsoft/vscode/pull/13263)
* [Jess Chadwick (@jchadwick)](https://github.com/jchadwick)
  *  Increasing test coverage for collections [PR #13817](https://github.com/Microsoft/vscode/pull/13817)
  *  Adding tests for editor state [PR #13792](https://github.com/Microsoft/vscode/pull/13792)
* [Kai Wood (@kaiwood)](https://github.com/kaiwood):  Add setting to prevent copying empty selections [PR #13678](https://github.com/Microsoft/vscode/pull/13678)
* [Krzysztof Cieślak (@Krzysztof-Cieslak)](https://github.com/Krzysztof-Cieslak)
  *  Fix #1939 - Show tag name instead of commit in GitStatusbar [PR #12584](https://github.com/Microsoft/vscode/pull/12584)
  *  Fix #1798 -  Disable UndoLastCommit when no commits [PR #12583](https://github.com/Microsoft/vscode/pull/12583)
  *  Implement Push To Remote  [PR #12550](https://github.com/Microsoft/vscode/pull/12550)
  *  Fix #13242 - Escape command title for CodeLens [PR #13244](https://github.com/Microsoft/vscode/pull/13244)
* [Michael (@michaelchiche)](https://github.com/michaelchiche):  fix typo in type definition [PR #13159](https://github.com/Microsoft/vscode/pull/13159)
* [Michael Chou (@MikeChou)](https://github.com/MikeChou):  Follow symlinks recursively in Linux launch script [PR #14046](https://github.com/Microsoft/vscode/pull/14046)
* [Denis Malinochkin (@mrmlnc)](https://github.com/mrmlnc)
  *  [emmet] Support for more languages [PR #12382](https://github.com/Microsoft/vscode/pull/12382)
  *  Update vscode-extension schema [PR #12739](https://github.com/Microsoft/vscode/pull/12739)
* [Renfred Harper (@renfredxh)](https://github.com/renfredxh):  Enable line highlighting for read only editors [PR #14022](https://github.com/Microsoft/vscode/pull/14022)
* [Robin Munn (@rmunn)](https://github.com/rmunn):  Remove incorrect ANSI escape code for LF [PR #13345](https://github.com/Microsoft/vscode/pull/13345)
* [Sirisak Lueangsaksri (@spywhere)](https://github.com/spywhere):  Sort the installed extension list [PR #13399](https://github.com/Microsoft/vscode/pull/13399)
* [Tereza Tomcova (@the-ress)](https://github.com/the-ress)
  * Call AllowSetForegroundWindow before sending IPC [PR #13255](https://github.com/Microsoft/vscode/pull/13255)
  * Convert strings passed from node using UTF-8, not the system code page [Issue #7727](https://github.com/Microsoft/vscode/issues/7727)
  * Follow Windows conventions when composing cmdline [Issue #8429](https://github.com/Microsoft/vscode/issues/8429)
* [Ivan Samoylenko (@The-Smallest)](https://github.com/The-Smallest):  Typo in project.json [PR #13461](https://github.com/Microsoft/vscode/pull/13461)
* [Will Prater (@wprater)](https://github.com/wprater)
  *  fix UI/UX regression [PR #13922](https://github.com/Microsoft/vscode/pull/13922)
  *  quick open files in background [PR #13925](https://github.com/Microsoft/vscode/pull/13925)
* [Toru Nagashima (@mysticatea)](https://github.com/mysticatea): Fixes zero location support [PR-ESLint #153](https://github.com/Microsoft/vscode-eslint/pull/153)
* [Dario Fuzinato (@fussinatto)](https://github.com/fussinatto): Fixing typos in readme [PR-ESLint #157](https://github.com/Microsoft/vscode-eslint/pull/157)
* [Morton Fox (@mortonfox)](https://github.com/mortonfox): Fix license link [PR-LSP #74](https://github.com/Microsoft/language-server-protocol/pull/74)
* [Asad Saeeduddin (@masaeedu)](https://github.com/masaeedu): Fix typo in protocol documentation [PR-LSP #85](https://github.com/Microsoft/language-server-protocol/pull/85)
* [Anton Kosyakov (@akosyakov)](https://github.com/akosyakov)
  * Fixes Microsoft/language-server-protocol #87 [PR-LSP #90](https://github.com/Microsoft/language-server-protocol/pull/90)
  * Fixes issues #72 and #78 [PR-LSP #91](https://github.com/Microsoft/language-server-protocol/pull/91)
* [Richard Lasjunies (@rlasjunies)](https://github.com/rlasjunies): support of fixes provided by TSLint engine [PR #96](https://github.com/Microsoft/vscode-tslint/pull/96)
* [Robert Stoll (@robstoll)](https://github.com/robstoll):  fixed regexp pattern, violated rule was missing [PR #107](https://github.com/Microsoft/vscode-tslint/pull/107)

<!-- In-product release notes styles.  Do not modify without also modifying regex in gulpfile.common.js -->
<a id="scroll-to-top" role="button" aria-label="scroll to top" onclick="scroll(0,0)"><span class="icon"></span></a>
<link rel="stylesheet" type="text/css" href="css/inproduct_releasenotes.css"/>