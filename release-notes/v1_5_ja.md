---
Order: 15
TOCTitle: August 2016
PageTitle: Visual Studio Code August 2016 1.5
MetaDescription: See what is new in the Visual Studio Code August 2016 Release (1.5)
MetaSocialImage: 1_5_social.jpg
---

# August 2016 (version 1.5)

## 1.5.3 Fully Translated Build

予定していたよりも 2 週間ほど長くかかっていましたが、1.5.3リリースは、サポートされている 9 つの言語に完全に翻訳された 8 月リリース版となります:

Downloads: [Windows](https://vscode-update.azurewebsites.net/1.5.3/win32/stable) | [Mac](https://vscode-update.azurewebsites.net/1.5.3/darwin/stable) | Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.3/linux-x64/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.3/linux-deb-x64/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.3/linux-rpm-x64/stable) | Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.3/linux-ia32/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.3/linux-deb-ia32/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.3/linux-rpm-ia32/stable)

## 1.5.2 Recovery Build

いくつかの重要な問題を解決するために 1.5.2 リカバリービルドをリリースしました:

* [11702](https://github.com/Microsoft/vscode/issues/11702): Unable to bypass ssl verification any more for corp firewall
* [11714](https://github.com/Microsoft/vscode/issues/11714): Terminal focus key binding is not working correctly after update to 1.5
* [11742](https://github.com/Microsoft/vscode/issues/11742): Bug in cursor location within user snippets
* [11754](https://github.com/Microsoft/vscode/issues/11754): ShowQuickPick does not fulfil the promises

Downloads: [Windows](https://vscode-update.azurewebsites.net/1.5.2/win32/stable) | [OS X](https://vscode-update.azurewebsites.net/1.5.2/darwin/stable) | Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.2/linux-x64/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.2/linux-deb-x64/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.2/linux-rpm-x64/stable) | Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.2/linux-ia32/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.2/linux-deb-ia32/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.2/linux-rpm-ia32/stable)

## 1.5.1 Recovery Build

`editor.fontSize` が 0 に設定されている場合に何も表示されなくなる[問題](https://github.com/Microsoft/vscode/issues/11715)を解決するために、1.5.1 リカバリービルドをリリースしました。

Downloads: [Windows](https://vscode-update.azurewebsites.net/1.5.1/win32/stable) | [OS X](https://vscode-update.azurewebsites.net/1.5.1/darwin/stable) | Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.1/linux-x64/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.1/linux-deb-x64/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.1/linux-rpm-x64/stable) | Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.1/linux-ia32/stable) [.deb](https://vscode-update.azurewebsites.net/1.5.1/linux-deb-ia32/stable) [.rpm](https://vscode-update.azurewebsites.net/1.5.1/linux-rpm-ia32/stable)

## August Release Summary
## 2016/8 月版のリリースまとめ

VS Code チームの 8 月は、とても大変なひと月でしたが、おかげで素晴らしいリリースを提供することができました。主要なアップデートは UI の更新、拡張機能サポート、デバッグ機能、拡張性を提供する API のサポートです。

本リリースのハイライトは次のとおりです:

* **Workbench**: ファイルアイコンテーマの実装により、ファイルエクスプローラがより便利になります。 VS Code には、2 つのアイコンテーマが含まれていますが、マーケットプレースからより多くのテーマが提供されます
* **Debugging**: デバッグコンソールにおける [REPL(Read-Eval-Print-Loop) 対話的に実行して結果を確認する手段] を効率良く実行するために、IntelliSense をサポートしました(現時点では
 Node.js のみ)。デバッガプロトコルを利用することにより、他のデバッグ拡張機能でも IntelliSense をサポートすることが可能になります。また、複数行の入力をサポート
* **Extensions**:
  * インストール済み、または、マーケットプレイス上にある拡張機能のコントリビューション(コマンド、設定、言語 ID)を VS Code 上から参照することが可能に
  * インストール回数や評価の並べ替えでマーケットプレイスの拡張機能を検索することが可能に
  * インストール済みの拡張機能の自動更新および、更新可能な全ての拡張機能を一度にアップデートすることが可能に
* **Editor**: ワードラップと自動保存を制御する新しい設定を追加
* **Quick Open**: 大規模なプロジェクトのためにクイックオープンのパフォーマンスを向上
* **Extension Authoring**: VIM 拡張機能のためにエディタ・コマンド API を拡張

>**Note:** 完全に翻訳された 1.5 を提供する予定でしたが、残念ながら、翻訳に関連するいくつかの遅延が発生し、このリリースでは計画を見送ることにしました。近く、これらの成果を含んだアップデートを提供する予定です

## Workbench

### File Icon Themes
### ファイルアイコンテーマ

ファイルエクスプローラは、ファイルとフォルダのアイコンを表示することが可能になりました。ファイルアイコンを有効にするには、File Icon Theme を選択してください:

- グローバルメニューから設定する方法: **File(ファイル)** > **Preferences(基本設定)** > **File Icon Theme** (Mac では、 **Code** の配下にある **Preferences (基本設定)** メニュー内にあります)
- **コマンドパレット** (Win, Linux: Ctrl+Shift+P, Mac: ⇧⌘P) から呼びす **Preferences: File Icon Theme** コマンド

デフォルトでは、ファイルアイコンセットが設定されていないため、ファイルエクスプローラにアイコンは表示されません。アイコンテーマが選択されると、テーマが適用され、再起動後も有効になります。

このリリースでは、ファイルとフォルダのアイコンのみがファイルエクスプローラに表示されますが、今後、エディタタブや他の場所でもファイルアイコンを使用できるようにする予定です。

VS Code 1.5 には 2 つのアイコンテーマが含まれていますが、コミュティから多くのテーマが提供されることに期待しています。

|None (デフォルト)|Minimal File Icons|Seti File Icons|
|-----|-----|-----|
|![None/Standard Icon Theme](https://code.visualstudio.com/images/1_5_None.png)|![Minimal Icon Theme](https://code.visualstudio.com/images/1_5_Minimal.png)|![Seti Icon Theme](https://code.visualstudio.com/images/1_5_Seti.png)|

Jesse Weed が作成した [Seti UI](https://github.com/jesseweed/seti-ui) テーマ、Roberto Huertas によるアイコン拡張機能の実装により、この機能を望んでいた多くのユーザーにとても素晴らしい Seti UI アイコンテーマを提供することが可能になりました。

### 統合ターミナル内のキーバインディングサポート (Key binding support within the Integrated Terminal)

新しい `terminal.integrated.commandsToSkipShell` 設定には、シェルに送信したくない VS Code のコマンド ID を指定します。この設定により、ターミナルがフォーカスされている場合でも、指定されたキーバインドはシェルに渡されず、VS Code のコマンドアクションを使用することができます。例: フォーカスがターミナルにあっても、`F1` などの機能を実行することを可能にします。

## Editor

### Editor settings
### エディタの設定

このリリースではいくつか便利な[エディタの設定](/docs/customization/userandworkspace.md)が追加されました:

* `editor.renderLineHighlight` - 現在の行のハイライトを無効にします
* `editor.fontWeight` - エディタのフォントの太さをカスタマイズします (**normal**, **bold**).
* `editor.wordWrap` - `editor.wrappingColumn` 設定をベースに、ワードラップを切り替えます。

### Auto Save when application loses focus
### アプリケーションがフォーカスを失った時に自動保存

ウィンドウの切り替えをトリガーに、ファイルを自動保存(`files.autoSave` [setting](/docs/customization/userandworkspace.md))する、新しい `onWindowChange` 設定を追加

### Quick Open got a lot quicker
### より高速になったクイックオープン

過去 2 回のイテレーションに渡り、大規模なワークスペース ('大規模' とは 'Chromium-repository-large'のようなワークスペース)のために行った改修においてクイックオープンの動作が高速化されました。新しくクローニングされた Chromium リポジトリには、220,000 以上のファイルが含まれています。
我々の開発マシンにおけるクイックオープンでは、バージョン 1.3 の約 30 秒から、バージョン 1.5 では約 3 から 4 秒程度(もちろん、プラットフォームに依存します) になりました。
これは、キャッシュを利用していない時のパフォーマンスですが、キャッシュの使用を前提に 0.5 秒台の結果を得るようにしました。

ユーザーがクイックオープンを呼び出すときに、すぐにキャッシュの更新を開始し、キャッシュから読み込まれたときに UI スレッドをブロックすることはなく、0.5秒と言う値は、キャッシュが期限切れであったとしても、エンド・ユーザーが気づくパフォーマンスです。
上で述べたように、これは Chromium リポジトリのためのものであり、あなたのプロジェクトが小さい場合は、遅延は全く見られないでしょう。

### Keep Quick Open visible even when focus is outside
### フォーカスに影響されないクイックオープン

フォーカスの移動に影響されるクイックオープンウィジェットの開閉を制御することが可能な、新しい `workbench.quickOpen.closeOnFocusLost` 設定を追加しました。
デフォルトでは、フォーカスが移動するとクイックオープンは閉じますが、`false` を設定することにより、それを開いたままにすることが可能になります。

### Include symbol results in file Quick Open results
### ファイルクイックオープンの結果に含まれるシンボル結果

ファイル検索のクイックオープンに表示されるシンボルを抑制するための新しい設定 `search.quickOpen.includeSymbols` を追加しました。
以前のリリースでは、一般的なファイルピッカー内にシンボルの結果を含んでいましたが、問題を抱えているためこれをオプションにしました。
シンボルを含む以前の動作に戻す必要がある場合は、このオプションを `true` に設定してください。
この設定を有効にするとグローバルシンボルの結果を返すための検索に時間を必要とします。そのため、全体的なファイル検索速度が遅くなることに注意してください。

>**Note:** **Show All Symbols** (Win, Linux: `Ctrl+T`,  Mac: `⌘T`) コマンドを使用して、グローバルシンボルを検索することができます。

### New actions to move Tabs left or right within a group
### エディタグループ内で左または右にタブを移動するための新しいアクション

エディタのグループ内にて、タブ(タブのヘッダ)を右または左に移動するための新しいアクションが追加されました。
追加された 2 つのアクションとそれらのデフォルトキーバインドは次のとおりです:

アクション | コマンドパレット | キーバインディング
--- | --- | ---
`workbench.action.moveEditorLeftInGroup` | エディタを左へ移動 (Move Editor Left) | `(Win, Linux: Ctrl+Shift+PageUp, Mac: ⌘K ⇧⌘←)`
`workbench.action.moveEditorRightInGroup` | エディタを右へ移動 (Move Editor Right) | `(Win, Linux: Ctrl+Shift+PageDown, Mac: ⌘K ⇧⌘→)`

### Closed editors reopen at their previous index
### 以前のインデックスで再開されるエディタアクション

直前に閉じられたエディタを再呼び出しするアクション `workbench.action.reopenClosedEditor` (Win, Linux: Ctrl+Shift+T, Mac: ⇧⌘T) を新たに提供します。
このリリースでは、エディタはクローズされる前と同じ順序を維持し、同じインデックスで再開されます。

### Mac OS: Cmd+E no longer opens Quick Open
### Mac OS: Cmd+E によるクイックオープンの廃止

ファイル検索のためのクイックオープンを起動する(ドキュメント化されていない)キーバインドを削除することを決めました。 `kbstyle(Cmd+E)` の動作を以前のバージョンに戻したい場合は、キーバインディングの構成を設定します:

```json
{ "key": "cmd+e", "command": "workbench.action.quickOpen" }
```

この変更の背後にある理由として、Mac OS における `kbstyle(Cmd+E)` には、現在アクティブなファイル内の検索を実行する機能が主として割り当てられているためです。

## Languages

### TypeScript

Visual Studio Code には TypeScript の正式にリリースされたバージョンがバンドルされており、8月のリリースでは、バージョン `1.8.10` となります。また、9月中に、バージョン `2.0` が利用可能になる予定ですが、`npm install -g typescript@rc` を実行することにより、リリース候補版をインストールすることもできます。

異なる TypeScript バージョンを VS Code 上またはコマンドラインツールから利用すると、バージョンに依存したエラーによりビルドツールが混乱してしまいます。当然ですが、`2.0` でサポートされた機能は `1.8.1` では利用できません。もし、VS Code 上で TypeScript の新しいバージョンを使用したい場合は、`typescript.tsdk` 設定を使用します。詳細は [マニュアル](https://code.visualstudio.com/docs/languages/typescript#_using-newer-typescript-versions) を参照してください。

VS Code は、ワークスペースフォルダに任意の TypeScript バージョンが含まれていることを検知します。(`npm install typescript@x.x.x` 経由でインストールされたもの)

VS Code は、ワークスペースにインストールされた TypeScript を検出かつ `typescript.tsdk` 設定が使用されていない場合、VS Code にバンドルされる TypeScript バージョンをユーザに通知し、バンドルバージョンを使用するかどうかを尋ねます。

![TypeScript Version Check](https://code.visualstudio.com/images/1_5_ts-version-check.png)

**More Information** アクションは、常にローカルにインストールされた TypeScript のバージョンを使用するよう VS Code を設定する方法のドキュメントを表示します。VS Code では、TypeScript 言語サーバがグローバルにインストールされている `tsc` コンパイラと差異があるかをチェックします。異なる場合は、対応する情報メッセージが示されます。

### HTML

組み込みのコード補完プロバイダをアクティブにするかを制御するために、新しい設定が追加されました。対応するサジェスチョンを参照したくない場合は、これらの設定を使用します。

```json
// Configures if the built-in HTML language suggests Angular V1 tags and properties.
"html.suggest.angular1": true,

// Configures if the built-in HTML language suggests Ionic tags, properties and values.
"html.suggest.ionic": true,

// Configures if the built-in HTML language suggests HTML5 tags, properties and values.
"html.suggest.html5": true
```

### LESS

LESS 構文の検証は、最近 LESS に追加された機能の一部をサポートするために、最新のものを取り込んでいます。次のものが含まれます:

- Named Parameters in Mixins
- Mixins as functions
- Passing Rulesets to Mixins
- CSS Guards
- Merge

これらの機能の詳細については、[LESS ドキュメント](http://lesscss.org/features/)を参照してください。

### Settings to enable/disable Emmet for languages
### 言語のための Emmet 設定

新しく追加された `emmet.syntaxProfiles` 設定を利用することで、他の言語と既存の Emmet 構文プロファイル (例えば `html`、`css` など) を関連付けることができます。設定は、言語 ID を受け取り、Emmet プロファイルに関連付けます。

例えば、JavaScript で Emmet HTML 略語を使用するには次のように設定します:

```json
{
    "emmet.syntaxProfiles": {
        "javascript": "html"
     }
}
```

`emmet.excludeLanguages` 設定を使用して特定の言語における Emmet 略語の使用を無効にすることができます。
次の設定は、PHP ファイル編集時に Emmet を無効にします:

```json
{
    "emmet.excludeLanguages": [
        "php"
    ]
}
```

### Linter Extensions
### リンター拡張機能 (Linter Extensions)

`vscode-eslint` と `vscode-tslint` 拡張機能を、ファイル保存時に実行する新しい設定を追加しました。

```json
{
    "tslint.run": "onSave"
}
```

## Extensions

### Easier Updates
### より簡単な更新

**すべての拡張機能を更新**するためのアクションが用意されました。

![Extension update all](https://code.visualstudio.com/images/1_5_extension-update-all.png)

さらに、`extensions.autoUpdate` 設定を `true` に設定すると、ユーザーの介入なしに拡張機能を自動更新できるようになります。

### Extension Contribution Details View
### 拡張機能のコントリビューション詳細ビュー

拡張機能をインストールする前に、各拡張機能のコントリビューション・ポイントを表示する **Contributions** セクションを VS Code の拡張機能閲覧で参照することが可能になりました。

![Extension Details](https://code.visualstudio.com/images/1_5_extension-details.png)

### Extension Sorting
### 拡張機能一覧のソート

拡張機能ビューは、インストールカウント以外の方法で拡張機能を並べ替えることができるようになりました。

![Extension sort](https://code.visualstudio.com/images/1_5_extension-sort.png)

### Marketplace Performance Improvements
### マーケットプレースのパフォーマンス改善

[マーケットプレース](https://marketplace.visualstudio.com/vscode)は、ダウンロードにおけるダウンロード時間と拡張クエリの可用性を改善するため、CDN に刷新されました。

## Debugging

### Suggestions in Debug Console
### デバッグコンソールでの Intelisense サポート

**デバッグコンソール** で、入力中の内容に関するサジェスチョンを示すことが可能になりました。現時点では、この機能は Node.js デバッグのためにのみ利用可能ですが、他のデバッガではデバッガ・プロトコルを通してサジェスチョン機能を実装することが可能です。

![Debug Console Suggest](https://code.visualstudio.com/images/1_5_debug_repl_suggest.png)

### Multi-Line Debug Console Input
### デバッグコンソールへの複数行入力

**デバッグコンソール**への複数行にまたがる入力が可能になりました。複数行の入力は、`Shift + Enter` で行うことが可能です。

![Debug Console Multiline](https://code.visualstudio.com/images/1_5_debug_repl_multiline.png)

### Multi-Level Variable Paging
### マルチレベルの変数ページング

子供の数が多いデータ構造は、マルチレベルのチャンクにより表示されます。これは、より良いパフォーマンスをもたらす他、簡単に多数の子を横断することができます。

![Variable Multi Level Paging](https://code.visualstudio.com/images/1_5_debug_variable_paging.png)

## Node Debugging

### Launch debug target in Integrated Terminal
### 統合ターミナル上でのデバッグターゲット実行

**Integrated Terminal** で Node.js デバッグターゲットを起動できるようになりました。対話型端末からの読み取りやそれらが実行されている端末上の出力を制御する必要があるような Node.jsベースのコマンドラインアプリケーションを開発する際に役立ちます。Node.js プログラムを実行するために 3 つのオプション (**Debug Console**, **Integrated Terminal**, 外部コンソール)を提供してきましたが、このリリースから `launch.json` の `externalConsole` アトリビュートを非推奨とし、新しいアトリビュート `console` を導入し、次の値を設定できるようにしました: `internalConsole`, `integratedTerminal`, `externalTerminal`

![New launch attribute Attribute console](https://code.visualstudio.com/images/1_5_debug-console-attribute.png)

>**Note:** VS Code は、`internalConsoleOptions` 属性に構成されたオプションに応じて、**統合ターミナル** を非表示にして **Debug Console** を開きます。
これを避けるには、 `internalConsoleOptions` へ `neverOpen` を設定してください。

>**Note:** このリリースでは、すべてのデバッグセッションは、新しい**統合ターミナル**を作成します。次のリリースでは、可能な場合は、既存の**統合ターミナル**を再利用する実装を予定しています。

## Extension Authoring
## 拡張機能のオーサリング

>**Note:** VS Code 8 月のリリース版では、TypeScript `1.8.10` の正式版がバンドルされ、拡張機能の開発は、このバージョンを使用して行われるべきです。将来のリリースにおいて、拡張機能の開発のために TypeScript `2.0.x` をサポートする予定です。

### Editor Commands
### エディタコマンド

[VIM 拡張機能](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)の[ロードマップ](https://github.com/VSCodeVim/Vim/blob/master/ROADMAP.md)を実現するために、特にウィンドウのスクロールや折り畳みに関連する新しい API をエディタに追加しました:

- **Scroll editor:** エディタ画面の上下スクロール - See [9609](https://github.com/Microsoft/vscode/issues/9609).

```javascript
  commands.executeCommand('editorScroll', {to: 'up', by: 'page', value: '1'})
```

- **Reveal line:** エディタ上で異なる論理位置とラインを明確にする - See [9609](https://github.com/Microsoft/vscode/issues/9609).

```javascript
  commands.executeCommand('revealLine', {lineNumber: '10', at: 'top'})
```

- **Fold:** 現在のカーソルの上または下または `n` レベルでエディタのコンテンツを折りたたみます。

```javascript
  commands.executeCommand('editor.fold', {levels: '2', up: false})
```

- **Unfold:** 現在のカーソルの上または下または `n` レベルでエディタの折りたたまれているコンテンツを展開します。

```javascript
  commands.executeCommand('editor.unfold', {levels: '2'})
```

### Powerful Completion Items
### 補完機能の強化

[`Completion Item`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L2246) は、追加のテキスト編集や追加のコマンドをサポートしました。

これらを使用すると、さらに高度な補完が可能になります：

* シンボルを補完したときに import 文を追加
* 補完後、プロジェクトにライブラリを追加

### Stable Input Box and Quick Open
### 安定した入力ボックスとクイックオープン

クイックオープンが開いているか何か入力を求められているときに、フォーカスが VS Code または他のウィンドウの別の部分に移動してもダイアログが閉じないよう制御する、新しい `ignoreFocusOut` オプションが追加されました。
また、キャンセルトークンを使用してそれらをプログラムから閉じることができます。

### New context menu keys
### 新しいコンテキストメニューキー

キーバインディングとメニュー項目をより細かく制御するための新しいコンテキストキーを追加しました：

* `explorerResourceIsFolder` - エクスプローラ上でファイルまたはフォルダが選択された場合に反映されます
* `resourceFilename`  - エディタ/エクスプローラで現在アクティブなファイルの名前

### New Theme Settings
### 新しいテーマ設定

このリリースでは、TextMate のテーマの設定として、以下の内部の色を公開すると共に、テーマの作成者は、これらをカスタマイズすることが可能になります。

- `rangeHighlight`: 範囲の背景色を強調します。これは、クイックオープンと検索機能で利用されます。
- `selectionHighlight`: 選択によりハイライトされたリージョンの背景色
- `inactiveSelection`: フォーカスされていない選択された領域の背景色
- `wordHighlight`: 変数を読み取るような読み取りアクセス中のシンボルの背景色
- `wordHighlightStrong`: 変数への書き込みのような書き込みアクセス時のシンボルの背景色
- `findMatchHighlight`: 検索条件に一致するリージョンの背景色
- `currentFindMatchHighlight`: 検索条件に一致する現在の領域の背景色
- `findRangeHighlight`: 検索のために選択された領域の背景色
- `activeLinkForeground`: アクティブリンクの色
- `hoverHighlight`: ホバーの背景色
- `referenceHighlight`: 参照時に全ての参照を見つけた時の背景色
- `guide`: 入れ子のレベルを示すインデントガイドの色

### Integrated Terminal API
### 統合ターミナル API

ターミナル（複数可）を作成し、それらにテキストを送信するような、統合端末を超えた基本的な制御が可能となるいくつかの拡張を API に追加しました。API の詳細な説明については、[`window` API reference page](https://code.visualstudio.com/docs/extensionAPI/vscode-api#_window) を参照してください。

### Additions to the Debug Protocol
### デバッグプロトコルへの機能追加

[debug protocol](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts) は、次のエリア（とVSコードが既に対応する提供済みの UI）に拡張されています:

* **IntelliSense Support for the Debug Console**: デバッグアダプタは、**Debug Console** で IntelliSense によるサジェスチョンを提供するために、`completions` リクエストを実装することができます。VS Code でこの機能を有効にするには、 デバッグアダプタが持つ `supportsCompletionsRequest` 機能に `true` を設定する必要があります。

* **Run in Terminal Request**: デバッグアダプタは `runInTerminal` リクエスト経由で、簡単に VS Code の統合ターミナル上にてデバッグターゲットを実行することができます。(これは、VS Code のデバッグアダプタから最初のリクエストとして呼び出されることで利用できます) **Integrated Terminal** は、**Debug Console** の代替となり、対話型端末からの読み取りおよび/またはそれらが実行されている端末上で、出力を制御する必要があるコマンドラインアプリケーションのより良い開発をサポートします。フロントエンドクライアントは、`runInTerminal` が呼び出される前に、 `initialize` リクエストに含まれる `supportsRunInTerminalRequest` アトリビュートとその値が `true` であることを検証することでサポートします。

## Engineering

もともとは [Manoj Patel (@nojvek)](https://github.com/nojvek) からの [PR #9791](https://github.com/Microsoft/vscode/pull/9791) が発端となり、ビルド毎に更新された TypeScript ファイルの[テストカバレッジ](https://coveralls.io/github/Microsoft/vscode?branch=master)を持つようにしました。

## Notable Changes

* [6602](https://github.com/Microsoft/vscode/issues/6602): Add scroll bar to integrated terminal
* [8499](https://github.com/Microsoft/vscode/issues/8499): Cannot distinguish different files with the same path.filename(x)
* [8983](https://github.com/Microsoft/vscode/issues/8983): Closing a dirty split editor (existing OR untitled) should not affect the initial editor
* [9405](https://github.com/Microsoft/vscode/issues/9405): Resizing terminal only resizes the active terminal instance
* [9589](https://github.com/Microsoft/vscode/issues/9589): Save: Flush to disk after writing to file
* [9675](https://github.com/Microsoft/vscode/issues/9675): Undo/Redo adds a stop in between CHN Characters
* [9822](https://github.com/Microsoft/vscode/issues/9822): Terminal IME composition view appears on top of text when at the bottom of the screen
* [9937](https://github.com/Microsoft/vscode/issues/9937): Increase rule stack protection limit - Syntax highlighting broken in JS with multiple nested functions
* [9962](https://github.com/Microsoft/vscode/issues/9962): Explorer can freeze for large folders and many glob patterns
* [10100](https://github.com/Microsoft/vscode/issues/10100): Terminal cursor does not invert text color
* [10148](https://github.com/Microsoft/vscode/issues/10148): After updating to 1.4.0 the react-native extension no longer accepted as a debugger
* [10302](https://github.com/Microsoft/vscode/issues/10302): Support standard keybindings for scrolling terminal by one line on each platform
* [10360](https://github.com/Microsoft/vscode/issues/10360): File rename can close editors
* [10586](https://github.com/Microsoft/vscode/issues/10586): TabCompletionController causes severe perf hit

[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22August+2016%22+is%3Aclosed)と、1.5アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22August+2016%22+is%3Aclosed+label%3Afeature-request)です。

## Monaco Editor 0.6.0

VS Code と同様の間隔で、"Monaco" エディタを毎月リリースします。変更履歴は [こちら](https://github.com/Microsoft/monaco-editor/blob/master/CHANGELOG.md)で参照することができます。

## Downloads

* [Windows](https://vscode-update.azurewebsites.net/1.5.0/win32/stable)
* [Mac](https://vscode-update.azurewebsites.net/1.5.0/darwin/stable)
* Linux 64-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.0/linux-x64/stable)
  [.deb](https://vscode-update.azurewebsites.net/1.5.0/linux-deb-x64/stable)
  [.rpm](https://vscode-update.azurewebsites.net/1.5.0/linux-rpm-x64/stable)
* Linux 32-bit: [.tar.gz](https://vscode-update.azurewebsites.net/1.5.0/linux-ia32/stable)
  [.deb](https://vscode-update.azurewebsites.net/1.5.0/linux-deb-ia32/stable)
  [.rpm](https://vscode-update.azurewebsites.net/1.5.0/linux-rpm-ia32/stable)

## Thank You

最後になりましたが、VS Code をより良いものにするために協力してくれた次の方々に多大なる感謝を込めて：

* [Karsten Thoms (@kthoms)](https://github.com/kthoms):
  * Typo: Header File Name -> Header Field Name [PR language-server-protocol#43](https://github.com/Microsoft/language-server-protocol/pull/43)
  * Consistent text style [PR language-server-protocol#44](https://github.com/Microsoft/language-server-protocol/pull/44)
  * Typo fixed [PR language-server-protocol#45](https://github.com/Microsoft/language-server-protocol/pull/45)
  * Consistent use of suffix 'Request' in headers [PR language-server-protocol#46](https://github.com/Microsoft/language-server-protocol/pull/46)
* [Nagaraj (@ramamurthynagaraj)](https://github.com/ramamurthynagaraj):
  * Fixing warning while executing expand select action on an empty page. [PR #10787](https://github.com/Microsoft/vscode/pull/10787)
  * Fixes #10556: Considering non open files dirty count using file dirty event [PR #10590](https://github.com/Microsoft/vscode/pull/10590)
  * Added editor.fontWeight configuration [PR #10515](https://github.com/Microsoft/vscode/pull/10515)
  * Fixes 10754 - Using mode transition constructor so that modeId is available [PR #10784](https://github.com/Microsoft/vscode/pull/10784)
* [Jared Hester (@cloudRoutine)](https://github.com/cloudRoutine):
  * removed ocaml extensions [PR #10240](https://github.com/Microsoft/vscode/pull/10240)
  * don't auto close on single quote [PR #10239](https://github.com/Microsoft/vscode/pull/10239)
* [Fabian Lauer (@FabianLauer)](https://github.com/FabianLauer):
  * Git commit using '--signoff' [PR #10410](https://github.com/Microsoft/vscode/pull/10410)
  * Git: Ignore untracked files in change count badge [PR #10448](https://github.com/Microsoft/vscode/pull/10448)
* [Sandy Armstrong (@sandyarmstrong)](https://github.com/sandyarmstrong):
  * Support CompletionItemKind.Method. [PR #10225](https://github.com/Microsoft/vscode/pull/10225)
  * Fix show in IE11 [PR #10309](https://github.com/Microsoft/vscode/pull/10309)
  * Correct docs for IEditorScrollbarOptions.useShadows [PR #11312](https://github.com/Microsoft/vscode/pull/11312)
* [Natacha Gabbamonte (@natgabb)](https://github.com/natgabb): Fix params link under Completion Request [PR language-server-protocol#42](https://github.com/Microsoft/language-server-protocol/pull/42)
* [Quinn Slack (@sqs)](https://github.com/sqs): Print child process stderr to output channel [PR vscode-languageserver-node#83](https://github.com/Microsoft/vscode-languageserver-node/pull/83)
* [Kaloyan Raev (@kaloyan-raev)](https://github.com/kaloyan-raev): Contribute JSON Schema for composer.json [PR #10698](https://github.com/Microsoft/vscode/pull/10698)
* [Eshwar Andhavarapu (@gontadu)](https://github.com/gontadu): Added .bash_aliases to recognised extensions [PR #10651](https://github.com/Microsoft/vscode/pull/10651)
* [Scott Addie (@scottaddie)](https://github.com/scottaddie): Update default project.json TFMs [PR #9965](https://github.com/Microsoft/vscode/pull/9965)
* [@hm1992](https://github.com/hm1992): Detect shebang for Groovy files [PR #9709](https://github.com/Microsoft/vscode/pull/9709)
* [Toru Nagashima (@mysticatea)](https://github.com/mysticatea): Update: supports the range of lint results. [PR vscode-eslint#102](https://github.com/Microsoft/vscode-eslint/pull/102)
* [@sprinkle131313](https://github.com/sprinkle131313):
  * Recently closed editors open at same position as they were closed [PR #11076](https://github.com/Microsoft/vscode/pull/11076)
  * Changes cursor animations to start in default state [PR #11093](https://github.com/Microsoft/vscode/pull/11093)
* [Meai1 (@Meai1)](https://github.com/Meai1): Check if adapter is null and let it print errors [PR #9966](https://github.com/Microsoft/vscode/pull/9966)
* [Rajkumar Janakiraman (@rajkumar42)](https://github.com/rajkumar42): Improve evaluate on hover feature [PR #9821](https://github.com/Microsoft/vscode/pull/9821)
* [Manoj Patel (@nojvek)](https://github.com/nojvek): Travis builds post coverage info to coveralls.io, README badge [PR #9791](https://github.com/Microsoft/vscode/pull/9791)
* [William Raiford (@bill-mybiz)](https://github.com/bill-mybiz): Restore Previous Commit Message on Undo Last Commit [PR #9796](https://github.com/Microsoft/vscode/pull/9796)
* [Aldo Fregoso (@AldoMX)](https://github.com/AldoMX): Fixed `code.sh` to start VS Code under Cygwin [PR #10508](https://github.com/Microsoft/vscode/pull/10508)
* [Nathan Novielli (@natenovielli)](https://github.com/natenovielli): Only 'git fetch' if there is a remote repository available [PR #10853](https://github.com/Microsoft/vscode/pull/10853)
* [Denis Malinochkin (@mrmlnc)](https://github.com/mrmlnc): Emmet implementation tweaks [PR #11009](https://github.com/Microsoft/vscode/pull/11009), [PR #11003](https://github.com/Microsoft/vscode/pull/11003), [PR #11001](https://github.com/Microsoft/vscode/pull/11001)
* [Ashhar Hasan (@hashhar)](https://github.com/hashhar): Fix for issue 1490 [PR #7029](https://github.com/Microsoft/vscode/pull/7029)
* [Belleve Invis (@be5invis)](https://github.com/be5invis): Add mouse-keyboard event crossover to prevent menu bar from showing up after multi-selecting [PR #9154](https://github.com/Microsoft/vscode/pull/9154)
* [Eric Amodio (@eamodio)](https://github.com/eamodio): Fixes #7749 - Focus on CodeLens click [PR #9249](https://github.com/Microsoft/vscode/pull/9249)
* [Christian Alexander (@ChristianAlexander)](https://github.com/ChristianAlexander): Allow workspaceContains to specify directories [PR #9394](https://github.com/Microsoft/vscode/pull/9394)
* [Grant Mathews (@johnfn)](https://github.com/johnfn): Fix flipping axes behavior [PR #10322](https://github.com/Microsoft/vscode/pull/10322)
* [Pavel Kolev (@paveldk)](https://github.com/paveldk): Fix sending message to terminated worker [PR #10833](https://github.com/Microsoft/vscode/pull/10833)
* [Jun Han (@formulahendry)](https://github.com/formulahendry): Run entire text in terminal if selection is empty [PR #9480](https://github.com/Microsoft/vscode/pull/9480)

<!-- In-product release notes styles.  Do not modify without also modifying regex in gulpfile.common.js -->
<a id="scroll-to-top" role="button" aria-label="scroll to top" href="#"><span class="icon"></span></a>
<link rel="stylesheet" type="text/css" href="css/inproduct_releasenotes.css"/>
