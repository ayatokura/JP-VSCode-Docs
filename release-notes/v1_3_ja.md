- [June 2016 (version 1.3)](#june-2016-version-13)
	- [Tabs](#tabs)
		- [Open Editors View](#open-editors-view)
		- [More on Editor Stacks](#more-on-editor-stacks)
	- [Extensions Management](#extensions-management)
	- [Workbench](#workbench)
		- [Problems panel](#problems-panel)
		- [More powerful Drag and Drop](#more-powerful-drag-and-drop)
			- [DROP TO SPLIT](#drop-to-split)
				- [DROP FEEDBACK](#drop-feedback)
				- [DRAG FROM EXPLORER AND OPENED EDITORS VIEW](#drag-from-explorer-and-opened-editors-view)
		- [Preview Editors](#preview-editors)
		- [Integrated Terminal](#integrated-terminal)
		- [Command Palette: File: Open Recent in new Window](#command-palette-file-open-recent-in-new-window)
		- [Restore Full screen](#restore-full-screen)
	- [Editor](#editor)
		- [Global Search and Replace](#global-search-and-replace)
		- [Indent Guides](#indent-guides)
		- [Suggestions for command identifiers](#suggestions-for-command-identifiers)
		- [Editor Font Zooming with mouse wheel](#editor-font-zooming-with-mouse-wheel)
		- [Multiline Find](#multiline-find)
		- [Emmet](#emmet)
	- [Languages](#languages)
		- [Extract CSS/LESS/SCSS and JSON into extensions](#extract-csslessscss-and-json-into-extensions)
		- [Extract Markdown into an extension](#extract-markdown-into-an-extension)
		- [Atom JavaScript grammar](#atom-javascript-grammar)
	- [Debugging](#debugging)
		- [Moveable Debug Toolbar](#moveable-debug-toolbar)
		- [Changing Variable Value](#changing-variable-value)
		- [Show Variable Type on Hover](#show-variable-type-on-hover)
		- [Step Back](#step-back)
		- [OS specific launch configurations](#os-specific-launch-configurations)
	- [Node.js Debugging](#nodejs-debugging)
		- [Attach to Process](#attach-to-process)
	- [Extension Authoring](#extension-authoring)
		- [Menu Items and Context Menu Entries](#menu-items-and-context-menu-entries)
		- [Add decorations before and after text](#add-decorations-before-and-after-text)
		- [API tweaks](#api-tweaks)
		- [Debug Extension Authoring: Command Variables](#debug-extension-authoring-command-variables)
		- [Debug Extension Authoring: Additions to the Debug Protocol](#debug-extension-authoring-additions-to-the-debug-protocol)
		- [Creating Errors/Warnings from an Extension (Diagnostics) ... (訳がだいぶあやしい)](#creating-errorswarnings-from-an-extension-diagnostics-訳)
	- [Monaco Editor](#monaco-editor)
		- [CSS/LESS/SCSS and JSON language services are now available](#csslessscss-and-json-language-services-are-now-available)
	- [Notable Bug Fixes](#notable-bug-fixes)
	- [Downloads](#downloads)
	- [Thank You](#thank-you)

<!-- /TOC -->

https://github.com/Microsoft/vscode-docs/blob/vnext/release-notes/June_2016.md

# June 2016 (version 1.3)

 VS Code の 6 月版をリリースできることに興奮しています
 エクステンション管理(エクステンション専用のビュー)にタブ機能 (タブ付きエディタペイン) など、いくつかの大きな変更を追加しました
 その他の新機能として、グローバルな検索と置換、改良されたドラッグ＆ドロップ、任意のインデントガイドなどが追加されています
 ターミナル機能など既存機能の強化や重要なバグ修正のセットも適用されています

 このリリースのハイライト:

* **タブ機能**：タブ付きエディタペインにより、すぐにファイルに移動したりワークベンチを整理することが可能になります
* **エクステンション**：エクステンションを検索、インストールおよび管理するための新しいエクステンション・ビューを追加
* **ワークベンチ**：強化されたls
ドラッグアンドドロップ、無駄なエディタを開くことなくファイルを参照可能なプレビューエディタやマルチプル・ターミナルをサポート
* **エディタ**：グローバル検索と置換、インデントガイド、エラーと警告を表示する `Problems Panel` を追加
* **言語サポート**: より良く完全な Emmet サポート、Atom JavaScript grammar エクステンションなど
* **デバッグ**：実行中の Node.js プロセスへのアタッチやデバッグセッション中の変数の値を変更可能など多くの改善やサポートが含まれます
* **エクステンション・オーサリング**：メニューバーとコンテキストメニューの為の新しい contribution point を追加。非テキストリソースのオープンやエディタのデコレータを追加することが可能な新しい API を提供します

6 月版の新機能の詳細は下記になります。

## Tabs

このリリースでは、VS Code のエディタ上にあるタイトル領域内に開いているファイルを**みんな大好き！タブ機能**として配置できます。
開いているファイルを整理するためにドラッグ＆ドロップでタブを移動したり、右クリックすることで**変更の表示** (diff) を切り替えるなどの便利なアクションを実行することができます。

![Tabs](https://code.visualstudio.com/images/June_2016_tabs.png)

タブを使用しない場合は、`workbench.editor.showTabs` の設定にて無効にすることができます。

タブスペースに全てのファイルを表示できるほど十分な余裕がない場合、タブは左右にあふれて表示されます。
そのような場合は、マウスを使って左右にスクロールさせることができます。
また、小さなオーバーフローアイコン(下の画像を参照)が有効になり、全てのタブグループ一覧を表示および選択することが可能です。(edt コマンドの追加)

![Tabs Overflow](https://code.visualstudio.com/images/June_2016_overflow.png)

新しいエディタが開くべき場所を制御できるよう `workbench.editor.openPositioning` の設定が追加されました。
デフォルトでは、アクティブなタブの右側に新しいエディタが開いてゆきますが、左側、またはすべてのエディターの先頭や末尾に開くように変更することも可能です。

### Open Editors View

エクスプローラーに追加された新しい **OPEN EDITORS** ビューは、以前のバージョンの **WORKING FILES** ビューを置き換えるものです。

![Open editors view](https://code.visualstudio.com/images/June_2016_open_editors.png)

**OPEN EDITORS** ビューは、Editor Stacks を視覚的に表現するもので:

 * 各エディタのグループとそれに属しているエディタが表示されています
 * エディタをクリックすることでアクティブにし、対応するグループでファイルを開きます
 * トップレベルのアクションとして、すべてを閉じたり、開いているすべてのエディタを保存することができます
 * エディタレベルのアクションでは、エディタを閉じたり保存することができます
 * コンテキストメニューのアクションは、より洗練されたアクションを提供します
 * エクスプローラからエディタ、または、エディタグループへドラッグアンドドロップすることが可能です

 また、`"explorer.openEditors.visible": 0` を設定することにより、**OPEN EDITORS** ビューを隠すこともできます。

> **Note:** **WORKING FILES** ビューは削除されました。
これに関する概要や影響を受けるコマンドについては、[issue #6605](https://github.com/Microsoft/vscode/issues/6605) を参照してください。

### More on Editor Stacks

ワークベンチでタブを有効にするための準備として、ユーザーが VS Code のエディタと触れあう方法をもう一度考え直してみました。
他のエディタやツールを使っていた多くのユーザーは、VS Code のエディタ（開いているファイル）における動作の一部で混乱していました。

例えば：

* dirty editor(エディタ上の未保存のファイルなど)を閉じる際、保存を要求されない
* エディタを閉じる事は、すでに開いているエディタなどを考慮することなくグループ全体を閉じていた
* エディタのヒストリ一覧は、これまで開かれたすべてのエディタのリストではなく、グループ内にオープンしたエディタのリストのみを表示していた
* エクスプローラでの **WORKING FILES** ビューが混乱を招くコンセプトだった

新しいコンセプトである **Editor Stacks** として、これらの問題に対処することにトライしました: 

* 3つの **エディタグループ** (LEFT, CENTER, RIGHT)を横に並べて開くことができ、各グループにはエディタのスタックが含まれています。
* あなたがエディタを開くたびに、開かれたエディタはスタックの一番上に追加されてゆきます
* グループからエディタを閉じると、最後のエディタが閉じられ、グループが非表示になるまで、そのグループ内で既に開かれているエディタがアクティブになるよう遷移してゆきます。
* 未保存のエディタであれば、保存するように求められます

ナビゲーションのためにグループで最近使用したエディタのリストを表示するには、`Ctrl+Shift+Tab (Windows, Linux)` または `⌃⇧Tab (Mac)` を使用してください。
`View: Show All Editors` コマンドでは、すべてのグループで開かれている全てのエディタのリストを表示することができます。

![Editor Stacks](https://code.visualstudio.com/images/June_2016_stacks.png)

**Editor Stacks** の動作は、タブ機能が有効か無効かの設定とは独立していることに注意してください。
タブ機能を使用しない場合でも、これらの機能の恩恵を利用することが可能です。

>**Note:** 
**Editor Stacks** による大きな概念の変更により、多くのコマンド ID の名前が変更されたり新しいコマンドが導入されています。
この機能による変更点などは、[Issue #6605](https://github.com/Microsoft/vscode/issues/6605) を参照してください。変更前の動作にキーバインドを変更する方法についてもガイダンスを提供しています。


## Extensions Management

エクステンションの管理経験を改善するための新しいビューである **Extensions View** を導入しました。
検索ボックスが空の場合(デフォルト)、インストールされたエクステンションの一覧を表示します。

エクステンションビューを表示するには、エクステンションビューアイコンをクリックするか `Ctrl+Shift+X (Windows, Linux)` または `⇧⌘X (Mac)` を押します:

![extension view icon](https://code.visualstudio.com/images/June_2016_extensions-view-icon.png)

検索ボックスに入力可能な予約後としては、下記があります: 

* `@outdated`
* `@recommended`
* `@popular`

`...` **More** ボタンをクリックすることにより、下記のメニューを表示することが可能です:

* 現在インストールされているエクステンションのリスト
* 更新可能な古いエクステンションのリスト (`@outdated`)
* ワークスペースに基づいた推奨エクステンションのリスト (`@recommended`)
* 世界的に人気のあるエクステンションのリスト (`@popular`)

エクステンションのリスト閲覧では、インストール、アンインストール、更新が可能です。
さらに、エクステンションをクリックすることで、エディタ領域に詳細な説明が表示されます。

![Extensions View](https://code.visualstudio.com/images/June_2016_extensions_viewlet.png)

## Workbench

### Problems panel

6 月のリリースにおいて、エラーや警告の他、言語サーバー、Linter などのような異なるソースから生成された情報を表示するためにツール内の下部にドッキングされた **Problems Panel** と呼ばれる新しいパネルを提供します。
以前のリリースでは、クイックボックスを利用してエラーと警告を示しましたが、この方法でエラーと警告を管理することは困難であるとユーザーからのフィードバックを受けました。
新しいパネルにより、問題をナビゲートし、エディタを開いている間にそれらを修正することが非常に簡単になります。

![Problems](https://code.visualstudio.com/images/June_2016_problems.png)

フィルタボックスは、ビューに集約された問題を検索したりフィルタリングするために利用されます。
フィルタリングは、タイプまたはテキストにより行うことができます。

**Problems view** を開くには:

* `Ctrl+Shift+M (windows, Linux)` または `⇧⌘M (Mac)` を入力
* メニューの **View** | **Problems** から
* コマンドパレットから **View: Show Problems** コマンドを実行

以前のリリースで、クイックオープン/クイックボックスでエラーと警告を表示するために使用されたキーバインディング `Ctrl+Shift+M (Windows, Linux)` または `⇧⌘M (Mac)` は Problems Panel を開きます。

 デフォルトでは、アクティブにされたファイルの問題を表示するよう **Problems view** が自動スクロールします。
 この自動でスクロールする動作をしたくない場合は、設定 `problems.autoReveal` によって無効にすることができます。
 アクティブなファイルを切り替える際、自動的に "Problem view" の該当エラーにスクロールさせたくない場合は、`problems.autoReveal` に `false` を設定してください。

> **Note** このビューは、言語サーバやリンター、ビルドタスク、ワークスペース外に構築された外部ビルド環境が生成したエラーをマーカーで表現しています。
また、問題点を参照するためには適切に設定またはカスタマイズされている必要があります。

### More powerful Drag and Drop

タブ上のすべての作業において、エディタでのドラッグ＆ドロップのサポートを向上させました。
ファイルを開くために、外部からファイルをドロップすることができる他、いろいろな操作が可能になります:

#### DROP TO SPLIT

エディタの左側または右側の領域にファイルをドラッグすることで、エディタをスプリットさせて新たにファイルを開くことが可能です。エクスプローラからドラッグする事も可能ですし、タブ機能が有効になっている場合はタブのドラッグも可能です。

![Problems](https://code.visualstudio.com/images/June_2016_dnd_editor.gif)

##### DROP FEEDBACK

エディタ領域上のファイルやタブをドラッグする際にドロップの目標位置を示す、ドロップフィードバック（ドロップ位置をハイライト）を得ることができます。

##### DRAG FROM EXPLORER AND OPENED EDITORS VIEW

エクスプローラ・ビューおよび **OPEN EDITORS** ビューからファイルまたはエディタを、特定の場所に配置されたエディタスペースにドラッグすることができます。

### Preview Editors

エディタスタックとタブ機能に、密接に関係するのが **Preview Editors** です。
例えば、多くのファイルをクリックして、クリックされたファイルの数だけタブが開かれることを想像してください。
これは、悪夢のはじまりです。

そのような場合、**Preview Editors** が開かれたエディタ（とタブ）の数を減らすために役立ちます。
エクスプローラでシングルクリックにて開かれたエディタは、プレビューモードとしてオープンします。
エディタはプレビューモードのままとなり、他のエディタが開くことはなくプレビューモードが解除されない限り、シングルクリックされたファイルは **Preview Editors** として、すでに開かれているエディタと同一の場所で開き続けます。

そして、特定のアクションにより、**Preview Editors** は通常のエディタとしてモードが変更されます。

* ファイルの内容を変更した場合、通常エディタモードとなります。
* 同じことは、タブ機能を有効にした場合でも、エクスプローラ上でファイルを「ダブルクリック」または特定のエディタのグループにファイルを移動するときにも当てはまります。

**Preview Editors** のタイトル(ファイル名)は、イタリックフォントスタイルを使用して表示されます。

![Preview Editor](https://code.visualstudio.com/images/June_2016_preview_editor.png)

**Preview Editors** の動作を制御するために、新しい設定を導入しました：

* `workbench.editor.enablePreview` は、**Preview Editors** をグローバルに有効または無効にします
* `workbench.editor.enablePreviewFromQuickOpen` クイックオープンからファイルを開いたときに、**Preview Editors** で開くことを有効または無効にします
 
### Integrated Terminal

VS Code 1.2.0 で導入された統合ターミナル機能は、このリリースでより多くの改善が行われており、主要な改善点は、VS Code の起動と同時にマルチプル・ターミナル機能が利用可能になることです。
追加のターミナルインスタンスは、**TERMINAL** パネルの右上にあるプラスアイコンを押すか、または "Ctrl+ Shift+\`" (Windows, Linux) または `⌃⇧ (Mac)` コマンドを投入することによって追加することができます。
ターミナルインスタンスが追加されると、複数のターミナルを切り替えるために使用することができるドロップダウンリストにターミナルのエントリを作成され追加されて行きます。

![Multiple terminal instances](https://code.visualstudio.com/images/June_2016_terminal_multiple_instances.png)

**TERMINAL** パネルおよびそのターミナルインスタンスの管理を支援するためにいくつかの新しいコマンドが追加されました。

追加されたコマンド:

* `workbench.action.terminal.focus`: ターミナルへフォーカスを移動。これはトグルのようなものですが、代わりにターミナルパネルが開かれている場合は、それを隠します。
* `workbench.action.terminal.focusNext`: フォーカスを次のターミナルインスタンスに移す
* `workbench.action.terminal.focusPrevious`: フォーカスを前のターミナルインスタンスに移す
* `workbench.action.terminal.kill`: フォーカスされているターミナルインスタンスを終了する

エディタ上で選択されたテキストをコマンドとしてターミナルで実行させる機能が、`workbench.action.terminal.runSelectedText` コマンドとして追加されました。

この機能を使用するには、エディタでテキストを選択し、**コマンドパレット**経由でコマンドを実行します。

![Run selected text](https://code.visualstudio.com/images/June_2016_terminal_run_selected.png)

![Run selected text result](https://code.visualstudio.com/images/June_2016_terminal_run_selected_result.png)

次の改善も追加されました:

* Linux と Windows の「コピー＆ペースト」は、それぞれ `Ctrl+Insert` と `Shift+Insert` として利用可能になりました
これは一時的に再設定不可能な実装となりますが、私たちは xterm.js ライブラリに [カスタマイズ可能な Copy/Paste キーバインデイング](https://github.com/sourcelair/xterm.js/issues/118) の実装を計画しています
* CJK キャラクタでは正しい文字幅が使用可能になり、この実装は、 [PR #144](https://github.com/sourcelair/xterm.js/pull/144) として [@jerch](https://github.com/jerch) が行いました
* 端末のパフォーマンスが大幅に向上し、大規模な出力を生成するコマンドを実行してもパフォーマンスが落ちることは無くなりました
* `Ctrl+Left` と `Ctrl+Right` により、シェルに入力中の単語単位でジャンプさせることが可能になりました
* ターミナルカーソルの点滅は、デフォルトで有効になり、エディタの `editor.cursorBlinking` 設定の値を共有します
* ターミナルがフォーカスされていない場合は、点滅しない中空カーソル(hollow cursor)が表示されます
* ターミナルのフォントサイズと行の高さは、[@kisstkondoros](https://github.com/kisstkondoros) の [PR](https://github.com/Microsoft/vscode/pull/6998) により設定でのカスタマイズが可能になりました
* 行全体をを選択しても、余白を含まず、また、テキストの色を反転させるように改善されました
  ![Terminal selection has been improved](https://code.visualstudio.com/images/June_2016_terminal_selection.png)
* `terminal.integrated.shellArgs.*` 設定を使用して Linux と OS X 上のターミナルシェルに引数を渡すことができます


### Command Palette: File: Open Recent in new Window

これは便利です。特に新しいウィンドウで開くやつ。
コマンドパレットから コマンド **File: Open Recent** で、以前のフォルダやファイルを開いてすぐに切り替えることが可能になりました。
デフォルトの動作は、選択したファイルまたはフォルダを実行中のインスタンスで開き直します。
このリリースでは、`Ctrl` (`Cmd` on Mac) が押された状態でエントリを選択した場合、新しいウィンドウに開くためのサポートが追加されました。

### Restore Full screen

新しい設定である `window.restoreFullscreen` は、フルスクリーンモードのまま閉じられたエディタを次回起動時にフルスクリーンでリストアします。

## Editor

### Global Search and Replace

[Global Search and Replace](https://github.com/Microsoft/vscode/issues/1690)は、多くのユーザーが基本機能として持っていると思っていました。
本リリースでは、置換機能を含む検索ビューを強化し、複数のファイル間のテキストを置き換えることができます。
結果によって、一度にすべてのファイルを置き換えるか、ファイルを選択するかを選ぶことができます。
また、結果やファイルを除外し、残りの置換を実行することができます。

さらに、リプレース前と後のファイルの差分をエディタビューで表示することができる素敵な Replace プレビューを提供します。

![Search and Replace](https://code.visualstudio.com/images/June_2016_searchAndReplace.png)

リプレース機能へアクセスするいくつかの方法:

* **検索ビュー** のサーチテキストボックスを展開する
* **編集** | **Replace in Files** メニュー、または、`Ctrl+Shift+H (Windows, Linux)` または `⇧⌘H (Mac)` を使う
* **コマンドパレット** から **Replace in Files** コマンドを実行する

>**注：** 表示可能な検索結果の最大値は 2048 までという制限があり、置換についても同様の制限が適用されます

### Indent Guides

VS Code でインデントガイドを表示することが可能になり、`editor.renderIndentGuides` を設定し有効にすることができます。

![Editor Indent Guides](https://code.visualstudio.com/images/June_2016_editor-indent-guides.jpg)

### Suggestions for command identifiers

`keybindings.json` ファイルを編集する際、現在利用可能なコマンドを補完対象とすることが可能になりました。

![Command Completions](https://code.visualstudio.com/images/June_2016_commad_ids.png)

### Editor Font Zooming with mouse wheel

[@kisstkondoros](https://github.com/kisstkondoros) からの [PR #6990](https://github.com/Microsoft/vscode/pull/6990) により、`editor.mouseWheelZoom: true` をセットすることで、`Ctrl` (`Cmd` on Mac) キーを押しながらマウスホイールでスクロールすることにより、エディタのフォントサイズを変更することが可能になりました。

![Mouse Wheel Zoom](https://code.visualstudio.com/images/June_2016_editor-mouse-wheel-zoom.gif)

### Multiline Find

複数行に渡る検索とリプレースをサポートしました: 

![Editor Indent Guides](https://code.visualstudio.com/images/June_2016_multiline-find.gif)

### Emmet

Denis Malinochkin ([@mrmlnc](https://github.com/mrmlnc)) からの Pull Request とテストの手助けなど素晴らしいサポートにより、Emmet の全ての機能をカバーすることが可能になりました。(Wrap with Abbreviation, Remove Tag, Update Tag, Balance, Toggle Comment, ...).

## Languages

### Extract CSS/LESS/SCSS and JSON into extensions

 CSS、LESS、SCSS 言語サポートは、VSCode エクステンションとしてリファクタリングされました。
 これらすべての言語は同じコードベースに基づいており、言語サーバを共有しています。

 言語サーバは、VSCode と通信するために、[language server protocol](https://github.com/Microsoft/language-server-protocol) を使用することで、別の node プロセスで実行されます。
 言語サーバプロトコルは、さらに、C＃、JSON、PowerShell、TSLint など多くの言語で使用されています。

### Extract Markdown into an extension

Markdown 言語サポートを通常の VS Code エクステンションとしてリファクタリングしました。
また、構文のハイライトのために Markdown TextMate grammar を使用し、[CommonMark Spec](http://spec.commonmark.org/0.25/) に準拠した [markdown-it ライブラリ](https://github.com/markdown-it/markdown-it)を利用して Markdown を HTML にレンダリングします。

### Atom JavaScript grammar

組み込みのJavaScriptの文法に代わるものとして、[Atom JavaScipt grammar](https://marketplace.visualstudio.com/items?itemName=ms-vscode.js-atom-grammar) をインストールすることができます。  
テーマなどで異なるビルトイン文法がサポートされている場合でも、変数や関数の参照のためのトークンを作成することにより異なる色付けをすることが可能です。


## Debugging

### Moveable Debug Toolbar
水平方向にデバッグツールバーをドラッグで移動できるようになりました。
ユーザからの要求により実装されました。[Issue #4580](https://github.com/Microsoft/vscode/issues/4580)

![Drag debug toolbar](https://code.visualstudio.com/images/June_2016_dnd_debug.gif)


### Changing Variable Value

デバッグ・エクステンションがサポートしていることが必要ですが、単純な変数の値の変更をサポートします。

Node.js のデバッガがこの機能をサポートした最初のエクステンションです:

![Drag debug toolbar](https://code.visualstudio.com/images/June_2016_set_variable_value.gif)

単純な変数は、変数ツリーのリーフです。例えば、変数、オブジェクトのプロパティ、または配列要素。

### Show Variable Type on Hover
タイプをサポートするデバッグ・アダプターのために、デバッグビューレット内の変数名の上にホバー機能による変数の型を示すことが可能になりました。

### Step Back
バックステップをサポートするデバッグアダプタでは、ステップバックアクションを利用することが可能になります。

![Step back](https://code.visualstudio.com/images/June_2016_step_back.png)


### OS specific launch configurations

`launch.json` 内にて、オペレーティング・システム固有の構成を指定することが可能になりました。
ユーザの要求によって実装されました。[Issue #1873](https://github.com/Microsoft/vscode/issues/1873)

例:

```json
{
   "type": "node",
   "request": "launch",
   "runtimeExecutable": "mynode",
   "windows": {
     "runtimeExecutable": "mynode.exe" 
   }
}
```

## Node.js Debugging

### Attach to Process

Node.js のデバッグでは、デバッグモードで起動していない Node.js プロセスにアタッチすることをサポートしています。
パフォーマンスなどの理由により、運用サーバー上などで、常にデバッグモードを有効にした状態で実行することができない場合に役に立ちます。

Node.js のプロセスにアタッチするために、attach launch configuration で `processId` 属性にアタッチしたい _process id_ を指定することができますが、デバッグセッションを開始する度に、launch configuration を編集することは非実用的であり、これを改善する方法として、例えば process picker のようなインタラクティブな UI に結合することができる新しいタイプの変数を導入しました:

![Process Picker](https://code.visualstudio.com/images/June_2016_attach_to_process.png)

ユーザがデバッグセッションを開始する前に、Node.js のプロセスを選択できるように $`${command.PickProcess}` 変数を使用するは launch configuration は次のとおりです。

```json
{
   "type": "Attach to Process",
   "type": "node",
   "request": "attach",
   "processId": "${command.PickProcess}"
}
```

## Extension Authoring

### Menu Items and Context Menu Entries

 エクステンションの作成者は、エクスプローラのコンテキストメニュー、エディタのコンテキストメニュー、およびエディタのタイトルメニューに貢献することを可能にします。
 
それは 2 つのステップで動作します:
 
 1. 強化された `commands` contribute point を使用して、コマンドにタイトルやアイコンを割り当てる
 2. 新しい `menus` contribute point を使用して、メニュー項目を作成する
 
 メニュー項目は、`editor/context` のようなメニューの位置のために定義されており、少なくとも `command`実行するように指定する必要があります。
  過度に散らかったメニューを回避するには、メニュー項目が示している条件を指定する必要があります。
最後に、代替コマンドおよびソートされた項目をグループ化して定義できます。
グループは、視覚的に分離され、最も顕著なものとしてナビゲーションと呼ばれる特別なグループがあります。

 ```
 "commands": [{
     "command": "markdown.showPreview",
     "title": "Open Preview",
     "icon": {
         "light": "./media/Preview.svg",
         "dark": "./media/Preview_inverse.svg"
     }
 }],
 "menus": {
     "explorer/context": [
         {
             "when": "resourceLangId == markdown",
             "command": "markdown.showPreview",
             "group": "navigation"
         }
     ]
 }
 ```
 
 ![Menu contribution](https://code.visualstudio.com/images/June_2016_menus-contributions.png)

Markdown 言語のリソースである場合のスニペットは、上記のエクスプローラのコンテキストメニューのナビゲーショングループにエントリを追加します。
メニューアイテムから実行される場合、現在のリソースの URI がコマンドに渡されることに *注意* してください。

### Add decorations before and after text

デコレーション API に新しい機能を追加しました。
デコレーション前後に 'attachments' を追加できます。
'attachments' は、アイコンだけでなく、装飾されたテキストの内容とすることができます。

下記の例は、テキストの color value に適用される CSS カラーデコレータです：

![Decorator attachment](https://code.visualstudio.com/images/June_2016_color_decorators.png)

デコレーションの 'attachment' は、'decoration type' (see ThemableDecorationInstanceRenderOptions, before & after) で定義され、個々の装飾に微調整することができます。(see ThemableDecorationRenderOptions, before & after).

### API tweaks

* Uri-class は、既存のものから URI を生成させることができます： `someUri.with({scheme: 'newScheme', path: 'newPath'})`
* `previewHTML` コマンドは、`title` を提供することが可能になりました
* HTML をプレビューする場合、現在適用されているテーマの body 要素のクラス名を利用しスタイルを適用します。テーマは、`vscode-light`, `vscode-dark`, and `vscode-high-contrast` など
* 画像などのような非テキストリソースを開くことができる新しいコマンド `vscode.open` を提供します

### Debug Extension Authoring: Command Variables

 VS Code は、しばらくの間 'launch configurations` で変数置換をサポートしています。
 このリリースでは、VS Code コマンドにバインドされた変数の新しいタイプを紹介します。 

 デバッグセッションが開始されると、基本となる launch configuration に存在するすべてのコマンド変数は、最初に収集された後に実行されます。
 複数の変数の存在は、複数の実行結果にはなりません。
 launch configuration に存在する全ての変数は、デバッグアダプタに渡される前に、コマンドの結果に置換されています。
 コマンドが実装され、エクステンションに登録し、その戻り値は、変数の値として使用されます。
 コマンドの実装は、UI なしの単純な式にもできますし、いくつか UI に基づいて洗練された機能がエクステンション API で提供されます。

この機能の例は、`node-debug` で見つけることができます。
ここでは、変数 `${command.PickProcess}` がプロセスピッカーコマンドにバインドされています。
新しい 'Attach to Process' launch configuration では、ユーザーは Node.js のプロセスを選択できるように変数を使用して launch configuration を実行してます。

新しいコマンド変数の導入は簡単です：

* あなたのエクステンションにコマンドを実装および登録します。(デバッグアダプタ内ではない)
* `debuggers` contribution point に `variables` セクションを追加します
* 変数ごと一つの名前または command-binding を追加します

例えば：

```
  "debuggers": {
    ...
    "variables": {
    "RemoteHost": "askUserForRemoteHostCommand"
    },
  ...
  }
```

* 変数は `${command.RemoteHost}` として launch configuration の任意の文字列型の値として使用することができます。

* `RemoteHost` 変数をユーザーが発見できるようにするには、`debuggers` contribution point の `configurationAttributes` または `initialConfigurations` セクションに追加することを検討してください。

### Debug Extension Authoring: Additions to the Debug Protocol

デバッグプロトコルは、次の 3 つの領域に拡張されました（VS Code は既に対応する UI を提供しています）: 

* **変数の編集**:デバッグアダプタが [supportsSetVariable`](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts#L594) を返すように実装されている場合、VS Code は、[setVariable request](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts#L476) 要求を呼び出すことにより、「変数ビュー」で構造化されていない（リーフ）変数の値を設定することをサポートします。
* **後方へのステッピング**:デバッグアダプタが [capability `supportsStepBack`](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts#L592) を返すように実装されている場合、VS Code は、バックステッピングのためのUIを有効にし、 [`stepBack` request](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts#L476) を呼び出します。
* **変数の型をホバー表示します**: デバッグアダプタは、[`variable` type](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts#L741)のためのオプションである `type` 属性を返す場合、変数名の上にマウスを重ねることで属性の値がホバー表示されます

### Creating Errors/Warnings from an Extension (Diagnostics) ... (訳がだいぶあやしい)

新しい **Problems Panel** の導入により、project wide builder やリンターのサポートに取り組むようになりました。
ドキュメントが閉じられたときの最初のステップとして、我々は問題の自動クリアを排除しました。そうでない場合は開き、誤っている project wide builder によって生成された問題セットを変更した文書を閉じます。この変更により、診断を生成するリンターのようなエクステンション機能は、ドキュメントが閉じているときにそれらをクリアする責任があります。
診断を生成するすべてのエクステンション・プロバイダは、この変更に採用する必要があります。

ドキュメントが閉じられたときの最初のステップとして、問題を自動的にクリアすることを止めました。
それ以外の場合は、開かれているあるいは閉じられているドキュメントは、project wide builder によって生成された問題セットを変更しますが、これは正しくありません。
この変更により、linter のような診断を生成する拡張機能は、ドキュメントが閉じているときにそれらをクリアする責任があります。
診断を生成するすべてのエクステンションプロバイダは、この変更を採用する必要があります。

linter で `vscode-language-server` node module を使用することで下記のように実現できます：

```typescript
 documents.onDidClose((event) => {
 	connection.sendDiagnostics({ uri: event.document.uri, diagnostics: [] });
 });
```

## Monaco Editor

Monaco Editor が [npm](https://www.npmjs.com/package/monaco-editor-core) として利用可能になりました！ - これは VS Code のソースコードエディタ部分を抜き出し、様々な Web アプリケーションへの統合や最新のブラウザで動作させることが可能になるライブラリパッケージです。いくつかの API を紹介する[デモサイト](https://microsoft.github.io/monaco-editor/index.html)を作成し公開しました。
`npm install monaco-editor` を実行することで Monaco Editor ライブラリを入手することが可能です。

Monaco Editor に関するリリースノートについては、[Microsoft/monaco-editor](https://github.com/Microsoft/monaco-editor/blob/master/CHANGELOG.md) を参照してください。

![Monaco Editor Playground](https://code.visualstudio.com/images/June_2016_monaco-editor-playground.png)

### CSS/LESS/SCSS and JSON language services are now available

また、CSS/LESS/SASS パーサーと language smarts code は、個別の node モジュールとなる [vscode-css-languageservice](https://github.com/Microsoft/vscode-css-languageservice) に分けられ、VS Code と [Monaco editor](https://github.com/Microsoft/monaco-editor) で利用されます。
Web ブラウザ上でも VS Code と同じ CSS の編集機能を提供します。

JSON も同様に、JSON Schema validator を含む言語サービス [vscode-json-languageservice](https://github.com/Microsoft/vscode-json-languageservice) として [Monaco editor](https://github.com/Microsoft/monaco-editor) で利用されます。

## Notable Bug Fixes

SASS モードの言語 ID が 'sass' から 'scss' へと変更されました。
Sass を利用するために任意のリンターの設定をカスタマイズしている場合、構成キーの名前を 'sass' から 'scss' に変更する必要があります。

* [6316](https://github.com/Microsoft/vscode/issues/6316): Update should reopen all last opened folders
* [1210](https://github.com/Microsoft/vscode/issues/1210): Open file dialog should start in the directory for the current active file
* [7391](https://github.com/Microsoft/vscode/issues/7391): editor becomes unresponsive all the time since last update
  * the fix improves considerably the memory footprint of all colorizers through the use of immutable linked lists for representing colorizer states in-between lines in [vscode-textmate](https://github.com/Microsoft/vscode-textmate).
* [8173](https://github.com/Microsoft/vscode/issues/8173): Noticeable delay opening a Markdown file (source)
  * the implementation of a 10x faster hand-written plist parser for TextMate grammars improves the start-up time of all colorizers. We are looking into extracting this implementation to its own node module.

また、Integrated Terminal では以下のバグが修正されました：

* [#8141](https://github.com/Microsoft/vscode/issues/8141): Cannot launch Electron apps from integrated terminal
* [#7911](https://github.com/Microsoft/vscode/issues/7911): Terminal lines appears to have margin
* [#7684](https://github.com/Microsoft/vscode/issues/7684): Clicking into editor does not properly take focus from Terminal view
* [#7458](https://github.com/Microsoft/vscode/issues/7458): Runaway terminalProcess processes 
* [#6738](https://github.com/Microsoft/vscode/issues/6738), [#7442](https://github.com/Microsoft/vscode/issues/7442), [#7444](https://github.com/Microsoft/vscode/issues/7444): Several issues related to resizing the terminal
* [#6743](https://github.com/Microsoft/vscode/issues/6743): Mouse wheel scrolling in integrated terminal only works on filled areas
* [#7357](https://github.com/Microsoft/vscode/issues/7357): Invoking the terminal sometimes yields an error "Cannot set property 'innerHTML' of undefined"
* [#6457](https://github.com/Microsoft/vscode/issues/6457): vim overrides the terminal color scheme

[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22June+2016%22+is%3Aclosed)と、1.3アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22June+2016%22+is%3Aclosed+label%3Afeature-request)です。

## Downloads

Downloads: [Windows](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/VSCodeSetup-stable.exe) |
[OS X](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/VSCode-darwin-stable.zip) | Linux 64-bit [.zip](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/VSCode-linux-x64-stable.zip) [.deb](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/vscode-amd64.deb) [.rpm](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/vscode-x86_64.rpm) | Linux 32-bit [.zip](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/VSCode-linux-ia32-stable.zip) [.deb](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/vscode-i386.deb) [.rpm](https://az764295.vo.msecnd.net/stable/e724f269ded347b49fcf1657fc576399354e6703/vscode-i386.rpm)

## Thank You


最後になりましたが、VS Code をより良いものにするために協力してくれた下記の方々に多大なる感謝を込めて：
* [Denis Malinochkin (@mrmlnc)](https://github.com/mrmlnc): Emmet - support all the features [PR #7926](https://github.com/Microsoft/vscode/pull/7926), [PR #8155](https://github.com/Microsoft/vscode/pull/8155), [PR #8489](https://github.com/Microsoft/vscode/pull/8489)
* [Rob Lourens (roblourens)](https://github.com/roblourens): UI support for TimeTravel Debugging [PR #7734](https://github.com/Microsoft/vscode/pull/7734)
* [xzper (f111fei)](https://github.com/f111fei): Debug: Fix setConfiguration error when name is null or undefined  [PR #7636](https://github.com/Microsoft/vscode/pull/7636)
* [Thomas Stringer (tstringer)](https://github.com/tstringer): Added remove and disable all breakpoints actions [PR #7627](https://github.com/Microsoft/vscode/pull/7627)
* [Ed Munoz (edumunoz)](https://github.com/edumunoz):
  * Remove leaked breakpoint after stopping with run-to-cursor [PR #7367](https://github.com/Microsoft/vscode/pull/7367)
  * report RunToCursorAction as not supported when session not stopped [PR #7371](https://github.com/Microsoft/vscode/pull/7371)
* [Giorgos Retsinas (@elemongw)](https://github.com/elemongw): Open window on activate when all windows are closed [PR #7547](https://github.com/Microsoft/vscode/pull/7547)
* [Andrew Arnott (@AArnott)](https://github.com/AArnott): LS Protocol-Clarifications regarding JSON-RPC header [PR #15](https://github.com/Microsoft/language-server-protocol/pull/15)
* [Vaclav Pavlin (@vpavlin)](https://github.com/vpavlin): LS Protocol-Fix typos in protocol.md  [PR #20](https://github.com/Microsoft/language-server-protocol/pull/20)
* [Tamas Kiss (@kisstkondoros)](https://github.com/kisstkondoros):
  * Gutter icon background size limited [PR #6553](https://github.com/Microsoft/vscode/pull/6553)
  * Horizontal selection movement implemented [PR #6887](https://github.com/Microsoft/vscode/pull/6887)
  * Option to hide the status bar implement [PR #6942](https://github.com/Microsoft/vscode/pull/6942)
  * Allow zooming with ctrl+mousewheel combination [PR #6990](https://github.com/Microsoft/vscode/pull/6990)
  * Add an option to display control characters [PR #7578](https://github.com/Microsoft/vscode/pull/7578)
  * fix for "screen cheese with long error messages" [PR #8432](https://github.com/Microsoft/vscode/pull/8432)
* [Basarat Ali Syed (@basarat)](https://github.com/basarat): fix : Standalone Monaco text edit validation [PR #7864](https://github.com/Microsoft/vscode/pull/7864)
* [Christian Svensson (@csvn)](https://github.com/csvn): Added order to snippet tab stops [PR #7925](https://github.com/Microsoft/vscode/pull/7925)
* [Phill (@ph1ll)](https://github.com/ph1ll): fix 'shaddow' typo [PR #7981](https://github.com/Microsoft/vscode/pull/7981)
* [Huachao Mao (@Huachao)](https://github.com/Huachao): Add Productivity into extension categories  [PR #7304](https://github.com/Microsoft/vscode/pull/7304)
* [Sajjad Hashemian (@sijad)](https://github.com/sijad):
  * Improve 'Open in Terminal' on OS X. [PR #6136](https://github.com/Microsoft/vscode/pull/6136)
  * Show warning for a long commit message [PR #7399](https://github.com/Microsoft/vscode/pull/7399)
* [Eshwar Andhavarapu (@gontadu)](https://github.com/gontadu): 
  * Addition of USE EXEC OPENQUERY syntax [PR #8046](https://github.com/Microsoft/vscode/pull/8046)
  * Added .dsql and .psql filetypes [PR #7491](https://github.com/Microsoft/vscode/pull/7491)
* [Cătălin Mariș (@alrra)](https://github.com/alrra): Treat `.webmanifest` files as JSON [PR #8019](https://github.com/Microsoft/vscode/pull/8019)
* [Øyvind Kallstad (@gravejester)](https://github.com/gravejester): Refactored PowerShell language definitions  [PR #7522](https://github.com/Microsoft/vscode/pull/7522)
* [Jan Niklas Hasse (@jhasse)](https://github.com/jhasse): Highlight .mk files as a Makefile  [PR #7328](https://github.com/Microsoft/vscode/pull/7328)
* [Christian Heilmann (@codepo8)](https://github.com/codepo8): Adding autocomplete values of to input/select/textarea  [PR #7152](https://github.com/Microsoft/vscode/pull/7152)