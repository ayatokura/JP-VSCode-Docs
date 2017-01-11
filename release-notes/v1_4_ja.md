# July 2016 (version 1.4)

7月の間、私たちは、機能追加への取り組みよりもバグのバックログ削減に多くの時間を割くことにしました。
しかしながら、いくつかの改善も追加することができてました。

本リリースのハイライトは下記のとおりです。

* **Workbench**: エディタアクションとして、**Open Preview** と **Switch to Changes View (変更の表示に切り替え)** をタイトルバーに戻しました。統合ターミナルで IME による入力およびコピー/ペーストをサポート
* **Editor**: より良いスニペットと提案制御。 新しい **Insert Snippet** コマンドをサポート
* **Debugging**: 特定のスタックフレームを再実行する、新しい **Restart Frame** アクション、特定のデバッガ拡張のみ実装されていた 'Variable paging' 機能を VS Code 本体に実装しすべてのデバッグ拡張機能で利用可能に
* **Extension Authoring**: より良い VIM ジェスチャーをサポートするための新しい 'move' コマンド、`DocumentLinkProvider` API によるカスタムリンクの制御、デバッグプロトコルの拡張

## Editor

### Snippets and Suggestions

デフォルトでは、1 ウィジェット内でスニペット及びコンプリーションの提案を示しています。
これは必ずしも望ましいものではないため、新たに `editor.snippetSuggestions` と呼ばれる構成設定を追加しました。

これは、スニペットを提案ウィジェットに表示するかどうかを制御します。
`"none"` を設定すると非表示となり、またはスニペットからの提案を `"top"`, `"inline"`, `"bottom"` の何れかでソートして表示するかを指定します。
デフォルトは、以前の動作となる `"inline"` です。

* [Support for TabCompletion #9579](https://github.com/Microsoft/vscode/issues/9579)

また、スニペットを挿入するために新しいコマンドを追加しました。これは、_Insert Snippet_ と呼ばれ、コマンドパレットで見つけることができます。

![snippet insert](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/insertSnippet.gif)

### タブ補完(Tab Completion)

タブ補完をサポートしました。`editor.tabCompletion` 設定を有効にしてください。そして、スニペットの接頭辞を入力し、それを挿入するには、Tabキーを押します。

![tab completions](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/tabCompletion.gif)

`quick suggestions` に注意してください。提示しているウィジェットも `Tab` に反応するためタブ補完を妨害する可能性があります。
その場合、quick suggestions (`editor.quickSuggestions = false`) か提示ウィジェット内のスニペットが表示されないようにする(`editor.snippetSuggestions = "none"`) のどちらかを無効にする必要があります。

いずれかの quick suggestions を無効にします。:

```json
    "editor.quickSuggestions": false
```

または、suggest widget からスニペットを削除します:
```json
    "editor.snippetSuggestions": "none"
```

## Workbench

### Editor Actions

前回のリリースでタブ機能を追加しましたが、タブを配置するスペースを確保するために、いくつかのメニューをタイトルヘッダーから取り除き、コンテキストメニューとしてエディタアクションを配置しました。
しかし、この変更からアクションを見つける事が困難である事を多くのユーザーのフィードバックから得る事ができました。
そのため、変更を再度見直し、このリリースではタイトルヘッダーにエディタアクションを表示するように戻しました。

![Menu Group Sorting](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/editor-actions-title.png)

### Drag and Drop

異なるウインドウ間でドラッグ・アンド・ドロップの操作によりタブを移動させることができるようになりました。
また、フォルダを VS Code にドロップすることで開く操作をサポートしていましたが、この操作は前回のリリースで欠落してしまっていたため、今回のリリースで再度サポートしました。

### Git commit message template

git で構成されているメッセージテンプレートを、VS Code の Git ビューで利用できるようにしました。デフォルトでコミット時のメッセージボックスに構成済みのメッセージテンプレートを表示します。

この機能に貢献してくれた [William Raiford](https://github.com/bill-mybiz) に感謝します。

### Faster Quick Open

Chromium などの大規模なワークスペースのためのクイックオープンのパフォーマンスを大幅に改善する上での最初のステップを作りました。

Mac OS (`kbstyle(⌘+P)`) および Linux (`kbstyle(Ctrl+P)`) では、Chromium ワークスペースの `Quick Open` は、以前のリリースに比べ約半分の時間で開くことができるようになりました。
Windows (`kbstyle(Ctrl+P)`) では、Mac OS に比べ倍ほど遅かった動作が、今では高速に動作するするようになりました。

そして、それはまだ終わっていません。次の Iteration では、より高速に動作するよう計画しています。

### Integrated Terminal

このリリースでは、統合ターミナル機能の完成を目指すための改善と互換性に関する改善を行っています：

- **IME サポート**: Input Method Editor (IME) のサポートを実装し、日中韓とインド語文字の入力が可能になりました

  ![IME support in Visual Studio Code](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/terminal_ime.png)

- **Windows と Linux でのコピー＆ペーストのサポート：**: より適切なコピー＆ペーストのサポートを Windows および Linux に実装しました
デフォルトのキーバインディングは、それぞれ、 `unassigned` と `unassigned` です。
- **コンテキストメニュー**: 右クリックで表示されるコンテキストメニューに、"New Terminal", "Copy", "Paste" オプションを追加しました。
- **アクセシビリティ**: タブのフォーカスモードを有効にする `Ctrl + M (Mac では ⌃⇧M)` を押すことで、エディタのようにターミナルからフォーカスをエスケープできるようになりました。
このモードを有効にすると、`Tab` と `Shift+Tab` が端末に渡されることはなく、代りにフォーカスされるエレメントを変更します。

## Languages

### JSON completions
JSON の補完のためにいくつかの小さな改善を実施：

- スキーマは、任意のデフォルト値を記載していない場合、スキーマベースの JSON ドキュメントでは、完全に空の配列、オブジェクトや文字列を提供します。
- `$schema` プロパティと値の補完をサポート。

## Debugging

### Restart Frame
VS Code は、スタックフレームの再開機能をサポートしました。
この機能は、コード上の問題を発見し、変更された入力値を使用してコードの一部を再実行させたい状況で役立ちます。 
デバッグ停止後に完全なデバッグセッションを再起動することは、非常に時間がかかることがあります。
`'Restart Frame'` アクションを使用すると、`'Set Value'` アクションでいくつかの変数を変更した後に、現在の関数を再実行することが可能になります:

![Restart Frame](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/restartFrame.gif)
`'Restart Frame'` アクションは、任意の状態の変化をアンロールしないため、予想通りに動作しない場合があります。

`'Restart Frame'` アクションは、基本となるデバッグ拡張機能がサポートしている場合にのみ使用可能です。

まずは、VS Code にビルトインされた Node デバッガのみでのサポートとなり、Node.js バージョン>=5.11 を使用してください。

### Variable Paging

以前の VS Code では、デバッグ拡張機能により配列のような大規模なデータ構造は「チャンク」に分割し、いくつかのデバッグ拡張機能だけがこの便利な機能をサポートしていました。
このリリースでは、将来的にすべてのデバッグ拡張が簡単に恩恵を受けることができるように、VS Code のデバッガフロントエンドにこの機能を移動させました。

![Variable Paging](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/variablePaging.png)

デバッグ拡張機能でこれを利用するための詳細な方法については、セクション "Debug Protocol Changes" を参照してください。

### Double Click Debug Toolbar Centers
デバッグツールバーのドラッグ・アイコンをダブルクリックすることで、デバッグツールバーを中心に配置し直します。これは、簡単にデフォルト状態を復元することができます。

## Extension Authoring

### New settings to replace deprecated __characterPairSupport and __electricCharacterSupport.

'__characterPairSupport' と '__electricCharacterSupport' 両方の設定が非推奨となり、拡張機能に含まれる language-configuration.json ファイルの `autoClosingPairs` 設定に置きかえられました。 
詳細な手順については、[#9281](https://github.com/Microsoft/vscode/issues/9281) を参照してください。

### Editor Commands

[VIM 拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) の [ロードマップ](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md)を実現するために、[上下移動コマンド](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md#up-down-motions) および[タブ関連のコマンド](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md#tabs)に関する、下記の Editor API を追加しました。

- **Move cursor:** エディタ内の異なる論理位置にカーソルを移動することを可能にする新しいコマンドが追加されました - [9143](https://github.com/Microsoft/vscode/issues/9143)
```javascript
commands.executeCommand('cursorMove', {to: 'up', by: 'wrappedLine', value: '2'})
```
- **Move active editor:** アクティブなエディタをグループ間またはそのグループ内でのタブ間で移動させるるための新しいコマンドを追加しました。 - [8234](https://github.com/Microsoft/vscode/issues/8234#issuecomment-234573410)
```javascript
commands.executeCommand('moveActiveEditor', {to: 'left', by: 'tab', value: '3'})
```

### Sorting of groups

前回のリリースでは、エディタ内の異なる場所にメニューアイテムを与えるためのサポートを追加しました。
このリリースでは、グループのソートをリファインしました。
メニューアイテムは、下記をデフォルト/ルールとし辞書順にソートされます。

エディタのコンテキストメニューのデフォルトルール:

* `navigation` - `navigation` グループは、すべてのケースで最初に表示されます
* `1_modification` - このグループは、コードに変更を加えるようなコマンドが含まれています
* `9_cutcopypaste`. - 基本的な編集コマンドと、最後となる既定のグループ

![Menu Group Sorting](https://raw.githubusercontent.com/Microsoft/vscode-docs/vnext/release-notes/images/July_2016/groupSorting.png)

これらのグループにメニュー項目を追加したり、メニュー項目の新しいグループを追加することができます。
このリリースでは、エディタのコンテキストメニューのみグループ化制御が可能ですが、まもなくエディタのタイトルメニューやエクスプローラのコンテキストメニューでも利用できるようになる予定です。

### DocumentLinkProvider API

VS Code には、エディタ上にある http, https, file リンクを検出しクリック可能にするリンク検出機能が組み込まれています。 
拡張機能の作成者が、カスタムリンク検出ロジックを追加することを可能にする新しい API を追加しました。

`DocumentLinkProvider` を実装し、エディタにそれを導入する [`registerDocumentLinkProvider`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L3814)-function を使用します。


### Debug Extension Authoring: Additions to the Debug Protocol (訳があやしい・・・)

[デバッグプロトコル](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts)は、次の領域に拡張されています(および VS Code が提供済みの対応する UI):

* **Restart Frame**: デバッグアダプタが `supportsRestartFrame` を返した場合、VS Code は、**CALL STACK** ビューのコンテキストメニューで **Restart Frame** アクションを選択できるようになるとともに、**Restart Frame** アクションの実行時に新しい `restartFrame` 要求を呼び出します。
`restartFrame` リクエストは、UI を新しい場所に更新することが可能なように `StoppedEvent` になる必要があります。
* **Variable Paging**: 
ページング変数とその子供たちのために 'variables paging' のサポートを追加しました。
VS Code 1.4 のデバッガ UI は、より良いスケーラブル（paged）UI で多くの子供を持つ変数を提示するために、これを使用して、断片的な方法で子供をフェッチします。
デバッグアダプタは、クライアントが 'variable paging' をサポートしているかどうかを
`initializeRequest`に引数として渡される `supportsVariablePaging` の値で調べることができます。<br>
デバッグアダプタは、オプションの `indexedVariables` 属性と `namedVariables` 属性を介して、インデックス付きプロパティの数（例えば、配列スロット）と変数の名前付きプロパティの両方を返すことができます。
この 2 つのプロパティは、`variablesReference` プロパティとして全ての場所に戻すことができ、`変数` と `スコープ` のデータ型が含まれた `evaluateRequest` レスポンスとなります。<br>
`variablesRequest`に追加されたオプション属性では、変数の子供達がフェッチする内容を VS Code デバッガ UI にてより良く制御できるようにました。<br>
`filter` 属性は、`indexed` または `named` のいずれかにフェッチされた子供たちを制限するために使用され、
`start` 属性と `count` 属性は、さらに一定の範囲に子を制限するために使用されています。
* **Continued Event**: デバッグアダプタは、必要に応じてデバッグ対象の実行が継続していることを伝えるために、`ContinueEvent` をクライアントに送信することが可能になりました
* **Source request supports mime type**: デバッグアダプタは、クライアントが適切なエディタを見つけるために使用する `SourceRequest` レスポンスに `mimeType` 属性を設定することが可能になりました
* **Variable Type client capability**:デバッグアダプタは、`initializeRequest` の引数として渡される `supportsVariableType` の値をチェックすることにより、 UI で変数の型の属性を示しているかどうかをクライアントが調べることができます。

## Notable Changes

* [4842](https://github.com/Microsoft/vscode/issues/4842): Allow to disable drag and drop in the files explorer
* [7839](https://github.com/Microsoft/vscode/issues/7839): Sometimes SVG icons do not show up on Windows 7
* [8788](https://github.com/Microsoft/vscode/issues/8788): Weird tabs auto scrolling behaviour
* [8704](https://github.com/Microsoft/vscode/issues/8704): Deleting folder containing dirty files closes dirty editors
* [8617](https://github.com/Microsoft/vscode/issues/8617): Run selected text in active terminal is not running the selected text on Windows
* [8219](https://github.com/Microsoft/vscode/issues/8219): Lines containing unicode characters in integrated terminal differ in height
* [9010](https://github.com/Microsoft/vscode/issues/9010): Global search and replace: Support regular expression variables in replace

These are the [closed bugs](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22July+2016%22+is%3Aclosed) and these are the [closed feature requests](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22July+2016%22+is%3Aclosed+label%3Afeature-request) for the 1.4 update.

## Downloads

Downloads: [Windows](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/VSCodeSetup-stable.exe) |
[OS X](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/VSCode-darwin-stable.zip) | Linux 64-bit [.zip](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/VSCode-linux-x64-stable.zip) [.deb](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/code_1.4.0-1470329130_amd64.deb) [.rpm](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/code-1.4.0-1470329130.el7.x86_64.rpm) | Linux 32-bit [.zip](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/VSCode-linux-ia32-stable.zip) [.deb](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/code_1.4.0-1470328389_i386.deb) [.rpm](https://az764295.vo.msecnd.net/stable/6276dcb0ae497766056b4c09ea75be1d76a8b679/code-1.4.0-1470328389.el7.i386.rpm)

## Thank You

最後になりましたが、VS Code をより良いものにするために協力してくれた下記の方々に多大なる感謝を込めて：

* [Lucian Wischik (@ljw1004)](https://github.com/ljw1004): Fix small typo [PR vscode-languageserver-node-example#17](https://github.com/Microsoft/vscode-languageserver-node-example/pull/17)
* [Markus Westerlind (@Marwes)](https://github.com/Marwes): DidOpenTextDocumentParams does not extend TextDocumentIdentifier [PR language-server-protocol#36](https://github.com/Microsoft/language-server-protocol/pull/36)
* [Eshwar Andhavarapu (@gontadu)](https://github.com/gontadu): Added more T-SQL keywords [PR #9469](https://github.com/Microsoft/vscode/pull/9469)
* [Pouya Kary (@pmkary)](https://github.com/pmkary): Added missing "rem" unit [PR #9497](https://github.com/Microsoft/vscode/pull/9497)
* [xzper (@f111fei)](https://github.com/f111fei):
  * Fix extracting zip file [PR #7599](https://github.com/Microsoft/vscode/pull/7599)
  * Fix installing extension by dropping [PR #8786](https://github.com/Microsoft/vscode/pull/8786)
  * Fix debounceEvent [PR #9186](https://github.com/Microsoft/vscode/pull/9186)
* [Sorin Iclanzan (@iclanzan)](https://github.com/iclanzan): Fix sensitivity not always being applied. [PR #9005](https://github.com/Microsoft/vscode/pull/9005)
* [Tamas Kiss (@kisstkondoros)](https://github.com/kisstkondoros):
  * Fixes invisible cursor in long editor lines [PR #8854](https://github.com/Microsoft/vscode/pull/8854)
  * Fixes mousewheel zoom in case of inline diff view [PR #8853](https://github.com/Microsoft/vscode/pull/8853)
  * New cursor animation styles implemented [PR #8153](https://github.com/Microsoft/vscode/pull/8153)
* [一丝 (@yisibl)](https://github.com/yisibl): Add Selection To Previous Find Match [PR #8677](https://github.com/Microsoft/vscode/pull/8677)
* [Giorgos Retsinas (@elemongw)](https://github.com/elemongw): [Mac] `Ctrl+P` and `Ctrl+N` for up and down navigation. [PR #7316](https://github.com/Microsoft/vscode/pull/7316)
* [William Raiford (@bill-mybiz)](https://github.com/bill-mybiz): Git commit message templates, restore previous message on undo. [PR #8933](https://github.com/Microsoft/vscode/pull/8933)
* [Georgios Kalpakas (@gkalpak)](https://github.com/gkalpak): docs(LanguageConfiguration): fix typo [PR #8703](https://github.com/Microsoft/vscode/pull/8703)
* [David Wilson (@daviwil)](https://github.com/daviwil):
  * Roll back PowerShell syntax definition [PR #9922](https://github.com/Microsoft/vscode/pull/9923)
  * Fixes for PowershellSyntax.tmLanguage [PR #9707](https://github.com/Microsoft/vscode/pull/9707)
* [David Hollinger III (@dhollinger)](https://github.com/dhollinger): Remove .pp from Ruby extension list [PR #8637](https://github.com/Microsoft/vscode/pull/8637)