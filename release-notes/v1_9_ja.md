# January 2017 (version 1.9)

## 1.9.1 Recovery Build 

1.9 の翻訳を更新し、いくつかの[問題](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22January+Recovery+2017%22+is%3Aclosed)を修正した 1.9.1 リカバリービルドをリリースしました。

## January Release Summary

Visual Studio Code の 2017 年最初のリリースへようこそ。 このリリースではいくつかの重要な更新があり、ハイライトは次のとおりです:

* **[新しい Welcome ページ](#welcome-welcome-experience)** - 新規ユーザーか既存ユーザーかに関わらず、すぐに利用を開始できるウェルカムページを提供
* **[対話式のプレイグラウンド](#interactive-playground)** - ファイルやプロジェクトを作成することなく VS Code の高度な編集機能を体験可能
* **[エディタと Markdown プレビューの同期](#markdown-markdown-preview-and-editor-integration)** - Markdown プレビューとエディタを同期させるビューを提供
* **[ペーストへのフォーマット適用](#format-on-paste)** - ソースコードをプロジェクトに持ち込むと同時にソースコードの整形を可能に
* **[言語固有の設定](#language-specific-settings)** - 言語毎に固有のエディタ設定が可能に
* **[TypeScript リファレンス CodeLens](#typescript-codelens-typescript-references-codelens)** - VS Code に TypeScript 2.1.5 を同梱、TypeScript リファレンス CodeLens を追加
* **[起動構成を必要としないデバッグ](#debugging-without-a-launch-configuration)** - 単一ファイルのデバッグを可能にする構成ファイルなしのデバッグをサポート
* **[ソースコード内のインライン変数値](#inline-variable-values-in-source-code)** - デバッグ中にインライン変数の参照が可能に
* **[Node.js におけるシナリオ別の起動構成スニペットの拡張](#launch-configuration-snippets-for-node-scenarios)** - Mocha テスト、Gulp タスク、Yeoman ジェネレータのデバッグをより簡単に
* **[タスク実行のサポート改善](#task-support)** - 同一タスクから複数のコマンドを実行可能に
* **[統合ターミナル機能の改善](#integrated-terminal-improvements)** - 統合ターミナル機能のパフォーマンスおよび Windows サポートの改善

VS Code の重要な更新に関連するアップデート情報は、リリースノートの次のセクションに配置されています。その他のアップデートは、次のとおりです:

* **[ワークベンチ](#workbench)** - 新しいウィンドウでの表示を制御するための新しい設定、改良されたタブ見出し、Zen モードのカスタマイズ
* **[エディタ](#editor)** - スニペット用キーボードショートカットの追加、実装に移動コマンド、高速な検索ナビゲーション
* **[言語サポート](#languages)** - 外部ファイルからの Emmet 略語読み込む、HTML フォーマット設定、Markdown 編集機能の改善
* **[拡張機能](#extensions)** - Yeoman ジェネレータを使用した拡張機能パックを作成可能に
* **[デバッグ](#debugging)** - ユーザレベルの launch.json、コールスタックアクションのコピー
* **[Node.js のデバッグ](#node-debugging)** - 'マイコードのみ (Just My Code)'の改善、restart をサポートした起動構成
* **[拡張機能のオーサリング](#extension-authoring)** - 新しい insertSnippet API、言語を扱えるようになった openTextDocument API

## ワークベンチ (Workbench)

### Welcome ページの提供 (Welcome experience)

新しく VS Code を使いはじめるユーザーのために **Welcome** ページ (**Help** > **Welcome**) を追加しました。また、最近利用したフォルダ一覧 (**Recent**) とヘルプドキュメント (**Help**) のリンクも追加されています。

![Welcome document](https://code.visualstudio.com/images/1_9_welcome-page.png)

**Show welcome page on startup** オプションをチェックすることで、起動時に必ず Welcome ページを表示する状態に保たれます。それ以外の場合、起動時に開いているファイルがない場合にのみ Welcome ページが表示されます。

新しいユーザーであれば、**Welcome** ページからインターフェイスの概要 (**Interface overview**) を確認できます。キーボードショートカットを使用して、ユーザーインターフェイスの基本部分を呼び出す操作を学べます:

![Interface Overview](https://code.visualstudio.com/images/1_9_interface-overview.png)

### 対話式のプレイグラウンド (Interactive Playground)

**Welcome** ページに掲載される **Interactive Playground** では、インタラクティブなサンプルを使用しステップバイステップで VS Code の強力なコード編集機能の一部を紹介しています:

![Interface Overview](https://code.visualstudio.com/images/1_9_interactive-playground.png)

### 統合ターミナル機能の改善 (Integrated Terminal improvements)

#### パフォーマンス (Performance)

統合ターミナル機能のフロントエンドの多くは、パフォーマンスを念頭に置いて書き直されました。これにより、大量のデータを処理するときにアプリケーションをロックする必要がなくなり、結果として、約 5 倍の高速化が得られました。

変更前 (v1.8.1):

---------------

![Terminal performance before](https://code.visualstudio.com/images/1_9_terminal-before.gif)

変更後 (v1.9.0):

---------------

![Terminal performance before](https://code.visualstudio.com/images/1_9_terminal-after.gif)

#### Windows サポート (Windows support)

Windows 上のターミナルプロセスと通信するために使用されるライブラリがアップグレードされました。これにより、矢印キーが機能しなくなったり、プロンプトラインが同期しなくなるなど、 Windows 上のターミナル機能が抱えていた多くの問題が修正されました。[winpty](https://github.com/rprichard/winpty) ライブラリを作成しアップグレードを手助けしてくれた [Ryan Prichard](https://github.com/rprichard) に感謝します。

#### その他 (Other)

- **Windows 10 では新しく PowerShell がデフォルトに**: PowerShell が Windows 10 上で動作する VS Code のデフォルトのシェルになり、[今後の OS のデフォルト設定](https://blogs.windows.com/windowsexperience/2016/11/17/announcing-windows-10-insider-preview-build-14971-for-pc/#fwfzEgffOGmVfEXs.97)との整合性が向上しました。この変更に不都合があるユーザーは、`settings.json` ファイルで `terminal.integrated.shell.windows` を `cmd.exe` に設定することで、cmd.exe に戻すことができます
- **右クリックによるコピーまたはペースト**: Windows では、cmd.exe が提供していた機能と同様に、端末内で右クリックを行うことにより、選択がない場合はペーストされ、選択がある場合はコピーが実行されるようになりました。この機能は、Windows ではデフォルトで有効になっており、`terminal.integrated.rightClickCopyPaste` 設定を使用して（どのプラットフォームでも）設定できますが、これを有効にすると、コンテキストメニューは表示されなくなります
- **新しいカーソルスタイル**: 新たにラインと下線カーソルスタイルが端末に追加されました。これは `terminal.integrated.cursorStyle` 設定で構成できます
- **ワイドキャラクタのサポート**: ワイドキャラクタは、正しく 2 文字の幅を利用するようサイズが調整されるようになりました
- **表示スペースの使用率を向上**: 端末パネル内の個々の端末は、できるだけ多くの表示スペースを利用するよう調整されました

### フォルダで常に Hot Exit を有効化 (Always hot exit on folders)

`files.hotExit` 設定が単純な `true`/`false` 設定から、次のオプションを受け入れるように変更されました:

- `"off"`: Hot Exit を無効にします (以前の `false` 設定と同じです)
- `"onExit"`: アプリケーションが閉じると (Windows/Linux で最後のウィンドウが閉じるとき、または workbench.action.quit コマンドがトリガーされるとき (コマンド パレット、キー バインド、メニュー))、Hot Exit がトリガーされます。バックアップされているすべてのウィンドウは、次の起動時に復元されます。(古い `true`設定と同じです)
- `"onExitAndWindowClose"`: アプリケーションが閉じると (Windows/Linux で最後のウィンドウが閉じるとき、または workbench.action.quit コマンドがトリガーするとき (コマンド パレット、キー バインド、メニュー))、Hot Exit がトリガーされます。また、フォルダが開かれているウィンドウについても、それが最後のウィンドウかどうかに関係なく、Hot Exit がトリガーされます。フォルダーが開かれていないウィンドウはすべて、次回の起動時に復元されます。フォルダのウィンドウをシャットダウン前と同じ状態に復元するには、`window.reopenFolders` を `all` に設定します

### Zen モードの改善 (Zen mode improvements)

Zen モードにおける視覚的な混乱を減らすために、ワークベンチのタブも隠すようにしました。 また、Zen モードでの操作を快適にするために、次のオプションを導入しました。

* `"zenMode.hideStatusBar"` - Zen モードへ移行した際、ワークベンチの下部にあるステータスバーを非表示にするかどうかを制御します。`false` を設定すると表示されなくなります。
* `"zenMode.hideTabs"` - Zen モードへ移行した際、ワークベンチタブを非表示にするかどうかを制御します。タブが表示されるようにするには、false に設定します。
* `"zenMode.fullScreen"` - Zen モード のまま終了した場合に、ウィンドウを全画面表示モードに復元するかどうかを制御します。フルスクリーンにならないようにするには `false` に設定します。

### 検索結果のナビゲーション (Search result navigation)

検索ビューに、結果をより簡単にナビゲートするための 2 つの新しい操作方法を追加しました。

- 矢印キー - 矢印キーを使用して結果を選択すると、結果がエディタに表示されます。
- 2つの新しいコマンド： `search.action.focusNextSearchResult` と `search.action.focusPreviousSearchResult` - デフォルトで、これらは macOS: `F4` Win: `F4` と macOS: `⇧F4` Win: `Shift+F4` に割り当てられています。

![search result navigation](https://code.visualstudio.com/images/1_9_search-result-nav.gif)

### パネルのタイトルバーを更新 (Panels title bar update)

水平パネルのタイトルバーには、利用可能な他のすべてのパネルが表示されるようになり、パネル間の切り替えがより簡単になりました: 

![Panels](images/1_9/panel.png)

### タブのコンテキストメニューに新しい項目を追加 (New entries in the context menu of Tabs)

タブのコンテキストメニューにファイルを表示するための新しい項目が追加されました。 ファイルのパスをコピー、OS ネイティブのエクスプローラでファイルを表示、または、サイドバーのエクスプローラでファイルを表示できるようになりました。

![Tab Context Menu](https://code.visualstudio.com/images/1_9_tab-context.png)

### タブの閉じるボタンを制御する新しい設定 (New setting to control close button in Tabs)

閉じるボタンを右側 (デフォルト) に表示するか、左側に表示するか、まったく表示しないかを制御するための新しい `workbench.editor.tabCloseButton` 設定を追加しました。

![Tab Close Button on the Left](https://code.visualstudio.com/images/1_9_tabclose.png)

注意: 以前の `workbench.editor.showTabCloseButton` はこの新しいオプションの提供により削除されました

### 新しいウィンドウで開くか最後に使ったアクティブなウィンドウで開くかを制御 (Control whether to open a new window or use last active)

VS Code が既に実行されている場合に、新しいファイルまたはフォルダを開くと、最後にアクティブだったウィンドウで開くか、新しいウィンドウで開くかを決定することが可能になりました。 既存の `window.openFilesInNewWindow` 設定はこれをファイルに対して制御し、デフォルトでは新しいウィンドウが開きます。今回のリリースでは、これをより詳細に構成可能にし、ファイルを開くためのデフォルトの動作を変更したいと考えました。

* この動作をフォルダに設定するための `window.openFoldersInNewWindow` 設定が追加されました
* 設定可能な値として、`default` と ` on` と `off` に変更しました。(`window.openFilesInNewWindow` もこれらの値を使用します)
* どちらの設定も `default` がデフォルトの設定値になりました。ほとんどの場合、新しいウィンドウを開くのではなく、最後のアクティブなウィンドウを再利用するほうが望まれました。

値が `default` に設定されている場合、VS Code は開いているリクエストのコンテキストに基づき、ウィンドウの再利用について最良の推測を行います。常に同じ動作が必要な場合は、設定を `on` または `off` に変更してください。たとえば、**File** メニューからファイルまたはフォルダを選択するときに、常に新しいウィンドウが必要な場合は、これを `on` に設定します。

注：この設定が無視される場合もあります。(たとえば、`-new-window` または `-reuse-window` コマンドラインオプションを使用する場合など)

### 新しいウィンドウのサイズを制御する (Control the dimensions of new windows)

新しい設定 `window.newWindowDimensions` は、新しいウィンドウのサイズと位置を制御します。デフォルトでは、新しいウィンドウが画面の中央に小さな寸法で開きます。この設定を `inherit` に変更すると、新しいウィンドウは、最後のアクティブウィンドウと同じ大きさで開きます。`maximized` または `fullscreen` に設定すると、常に新しいウィンドウが最大化されるかフルスクリーンで表示されます。

### メニュー表示の制御 (Control menu visibility) (Windows, Linux)

新しい設定 `window.menuBarVisibility` は、Windows と Linux 上のトップメニューの表示に関するより細かい制御を可能にします。`default` は、メニューは表示されますが、フルスクリーン時に隠れます。メニューを隠すために、`toggle` を設定することができます。 `toggle` は、`kbstyle(Alt)` キーを押すことでメニューの表示/非表示を切り替えます。
`hidden` を設定すると `kbstyle(Alt)` を押してもメニューは隠れたままになります。

注意：メニューを明示的に `visible` に設定した場合、フルスクリーンモード時も表示されたままになります

### 未保存のダーティーファイルが存在していても簡単にすべてのエディタを閉じることが可能に (Easy to close all editors when they are dirty)

多くの未保存のエディタが開いてしまうことがあります(たとえば、検索と置換操作を実行した後に保存しなかったなど)。いままで、そのような状態のエディタをすべてを閉じたいときなどは、各エディタを1 つずつ保存または元に戻すように求められていました。本リリースでは、**Close All Editors** アクション (macOS: `⌘K ⌘W` Win: `Ctrl+K Ctrl+W`) により、すべてのダーティファイルが表示され、一度に閉じることが可能になりました:

![Close All Prompt](https://code.visualstudio.com/images/1_9_closeall.png)

### 出力のスクロールロック (Output scroll lock)

外部ユーザーからの [PR](https://github.com/Microsoft/vscode/pull/18768) により、出力パネルのタイトルバーにスクロールロックを切り替えるボタンを配置し、出力による自動スクロールを制御することが可能になりました。

![Output scroll lock](https://code.visualstudio.com/images/1_9_output_scroll_lock.png)

## 設定 (Settings)

本バージョンでも、VS Code 1.8 で行われた設定機能に関する改善を継続しています。

- 個々の単語に一致するように、設定のキー、値、許可された値、およびその説明と照合してより良い結果を得るために検索機能が改善されています
- エディットアクションのレイアウトを改善し、他のエディタアクションでよりアクセスしやすく、発見しやすくなりました(クイックフィックス)
- 検索機能をデフォルト(左)と設定エディタ(右)の両方に拡張することで、設定エディタの UI を改善しました。 これにより、デフォルトの設定および設定済みの項目を同時に検索することが可能になります

### ユーザーとワークスペース設定 (User and Workspace Settings)

- ユーザーとワークスペースの設定を 1 つの設定エディタからすばやく切り替えることができるようになりました。これは、ユーザー設定およびワークスペース設定のスコープを発見して理解することに役立ちます。

![Settings](https://code.visualstudio.com/images/1_9_settings.png)

### 言語固有の設定 (Language specific settings)

多くのユーザーは、1 つのワークスペースでさまざまな種類のファイルや言語を扱います。そのため、言語固有の設定を可能に関する([#1587](https://github.com/Microsoft/vscode/issues/1587))機能に多くのリクエストが寄せられ、今回のリリースでは、言語ごとにエディタをカスタマイズできるようになりました。

任意の言語をカスタマイズするには、**コマンドパレット** (macOS: `⇧⌘P` Win: `Ctrl+Shift+P`) から **基本設定：言語固有の設定を構成します... (Preferences: Configure language specific settings...)** (id: `workbench.action.configureLanguageBasedSettings`) を実行し、言語ピッカーを開きます。固有の設定を行いたい言語を選択することで、設定エディタが開き、固有の設定を行うための言語エントリが追加されます。

![Language mode for File](https://code.visualstudio.com/images/1_9_pref-config-lang-settings.png)

![Language mode for File](https://code.visualstudio.com/images/1_9_lang-selection.png)

![Language mode for File](https://code.visualstudio.com/images/1_9_lang-based-settings.png)

すでに開いているファイルがあり、このファイルタイプのエディタをカスタマイズしたい場合は、VS Code ウィンドウの右下のステータスバーに配置されている言語モードをクリックしてください。**'language_name' 言語ベース設定を構成します... (Configure 'language_name' language based settings...)** オプションが含まれる言語モードピッカーが開きます。これを選択することで、固有の設定を行うための適切な言語エントリが追加された設定エディタが開きます。

`settings.json` を直接開いて言語ベースの設定を行うこともできます。他の設定と同じようにワークスペース設定に配置することで、言語固有の設定を適用するワークスペースのスコープを指定できます。ユーザースコープとワークスペーススコープの両方で言語用の設定が定義されている場合は、ワークスペースに定義されているものよりユーザースコープが優先され結合されます。

次の例は、`typescript` と `markdown` 言語モード毎にエディタ設定をカスタマイズします: 

```json
{
  "[typescript]": {
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true
  },
  "[markdown]": {
    "editor.formatOnSave": true,
    "editor.wrappingColumn": 0,
    "editor.renderWhitespace": "all",
    "editor.acceptSuggestionOnEnter": false
  }
}
```

設定エディタで IntelliSense を使用すると、許可された言語ベースの設定を見つけることができます。すべてのエディタ設定と非エディタ設定がサポートされています。

**注**: 次の設定は、現在サポートされておらず、次のリリースでのサポートを予定しています。詳細については、[#19511](https://github.com/Microsoft/vscode/issues/19511) を参照してください。

```json
editor.tabSize
editor.insertSpaces
editor.detectIndentation
editor.trimAutoWhitespace
```

## タスク実行のサポート改善 (Task support)

### タスク毎のコマンド (Commands per task)

タスクごとに異なるコマンドを定義できるようになりました ([#981](https://github.com/Microsoft/vscode/issues/981))。これにより、独自のシェルスクリプトを記述することなく、異なるタスクに対して異なるコマンドを実行することができます。タスクごとのコマンドを使用する`tasks.json` ファイルは次のようになります:

```json
{
    "version": "0.1.0",
    "tasks": [
        {
            "taskName": "tsc",
            "command": "tsc",
            "args": ["-w"],
            "isShellCommand": true,
            "isBackground": true,
            "problemMatcher": "$tsc-watch"
        },
        {
            "taskName": "build",
            "command": "gulp",
            "args": ["build"],
            "isShellCommand": true
        }
    ]
}
```

最初のタスクは watch モードで TypeScript コンパイラを起動し、2 つ目は `gulp build` を開始します。 タスクがローカルコマンドを指定してタスク名を実行する場合、コマンドラインには含まれません(`suppressTaskName` はこれらのタスクに対して `true` です)。 ローカルコマンドはローカル引数を指定できるので、デフォルトでそれを追加する必要はありません。`tsc` タスクは `isBackground"：true` を指定しています。プロパティ `isWatching` は、廃止予定であり、今後のより多くのシナリオをサポートするために、`isBackground` の使用が推奨されます。

`tasks.json` ファイルでグローバルおよびタスクローカルコマンドの両方が指定されている場合、タスクローカルコマンドはグローバルコマンドより優先されます。 グローバルコマンドとタスクローカルコマンドがマージされることはありません。

タスクローカルコマンドも OS 固有のものにすることができます。構文はグローバルコマンドと同じです。OS 固有の引数をコマンドに追加する例を次に示します:

```json
{
    "taskName": "build",
    "command": "gulp",
    "windows": {
        "args": ["build", "win32"]
    },
    "linux": {
        "args": ["build", "linux"]
    },
    "osx": {
        "args": ["build", "osx"]
    },
    "isShellCommand": true
}
```

グローバルコマンドと同様に、OS 固有セクションの `args` と `options` プロパティは、task コマンドに統合されました。

### ターミナルでのタスク実行 (Task execution in Terminal)

出力ウィンドウの代わりに端末を使用する新しいタスク実行エンジンを実装しました。これは、いくつかの大きな利点をもたらします:

* ANSI 制御文字のサポート
* 端末への入力 (タスクは入力を読むことができます)
* プラットフォームの文字エンコーディングがデフォルトで使用されます
* 2 つ以上のタスクを並行して実行することができます

これらの機能は、デフォルトで無効になっていますが、アーリーアダプターは新しい実装についてのフィードバックを提供することができます。 これを有効にするには、`tasks.json`ファイルの先頭に `"_runner": "terminal"` プロパティを追加してください:

```json
{
    "version": "0.1.0",
    "_runner": "terminal",
    "tasks": [
        {
            "taskName": "tsc",
            "command": "tsc -w",
            "isShellCommand": true,
            "isBackground": true,
            "problemMatcher": "$tsc-watch",
            "isBuildCommand": true
        },
        {
            "taskName": "dir",
            "command": "dir",
            "isShellCommand": true
        }
    ]
}
```

下記のスクリーンキャストでは、最初に tsc コンパイラをバックグラウンドで起動 (macOS: `⇧⌘B` Win: `Ctrl+Shift+B`  を使用) し、次に別のターミナルで dir コマンドを実行しています。

![Tasks in Terminal](https://code.visualstudio.com/images/1_9_tasks.gif)

ターミナルでタスクを実行するために行った変更が 1 つあります: タスクがシェルコマンドの場合、シェルコマンドの引数はコマンド自体の一部として扱われるのが最善です。この理由は、適切な引用にあります。古いランナーでは、異なる種類の引用符が存在する Linux/Mac シェル (特に、文字のエスケープ、引用符に優先順位があるなど) がある場合、特にシェルコマンドを正確に引用するのは複雑でした。この変更により、引数が指定されている場合は、引用符のルールを影響を与えずにコマンドに追加することが可能になりました。

そして、これらの実装については、まだ進行途中にあり、フィードバックと提案は大歓迎です。

## エディタ (Editor)

### ペーストへのフォーマット適用 (Format on Paste)

ペースト時にフォーマットを適用する新しい設定を追加しました([#13945](https://github.com/Microsoft/vscode/issues/13945))。`editor.formatOnPaste: true` 設定を `settings.json` に追加するだけです。これは、選択範囲の書式設定をサポートする既存のフォーマッタで機能することに注意してください(TypeScript フォーマッタや Marketplace の他のフォーマッタなど)。

### テーママッチングルールが TextMate セマンティクスを尊重するようになりました (Theme matching rules now respect TextMate semantics)

VS Code の初期バージョンから、TextMate テーマをサポートしています。しかし、1 つの問題点があったため、トークン <-> テーマのルールマッチングを行うために CSS を残すことにしました。これは、その時点で進歩を遂げるという観点では素晴らしい方法でしたが、同時に、TextMate テーマが VS Code 上に正確に反映されないことも意味しました (たとえば、TextMate テーマのマッチングセマンティクスは CSS のクラス名のマッチングセマンティクスとは異なります)。問題が深刻化しており、実装を改善する時期と判断しました(この手法によって引き起こされるレンダリングの違いについては、[issue #3008](https://github.com/Microsoft/vscode/issues/3008) を参照してください)。

### TextMate スコープを検査するための新しいツール (New Tools for inspecting TextMate Scopes)

トークンのスコープと一致するテーマルールを調べる際に役立つ新しいウィジェットを導入しました。新しいウィジェットは、**コマンドパレット** (`kb（workbench.action.showCommands）`) から **開発者: TM スコープの検査 (Developer Tools：Inspect TM Scopes)** を起動することができます。

![Inspect TM Scopes](https://code.visualstudio.com/images/1_9_inspect-tm-scopes.png)

### スニペットの挿入 (Insert snippets)

お気に入りのスニペットをキーバインディングに割り当てることが可能になりました。選択されたテキストをシングルクォートで囲むサンプルは、次のようになります:

```json
{
	"key": "cmd+k '",
	"command": "editor.action.insertSnippet",
	"args": { "snippet": "'$TM_SELECTED_TEXT'" }
}
```

`snippet` でスニペットを定義するのではなく、`{ "name": "mySnippet" }` のような `name`プロパティを使ってスニペットを参照することもできます。

### 実装に移動 (Go To Implementation)

新しい **実装に移動 (Go to Implementation)** および **実装のプレビュー (Peek Implementation)** コマンドを使用すると、インターフェースから実装へ、または抽象メソッドからメソッド実装に素早くジャンプすることが可能になります。この機能を試すには、開発中の nightly build として提供されている TypeScript 2.2 のビルドをワークスペースにインストールする必要があります: `npm install typescript@next`

### 永続的な表示オプション (Persistent view options)

単語の折り返しの切り替え、空白のレンダリングの切り替え、および制御文字の切り替は、トグルされた値がユーザー設定に保持されるようになりました。


### マルチカーソルアクションにおける大文字と小文字の区別 (Match Case and Whole Words in multi-cursor actions)

マルチカーソルアクションは、"大文字と小文字の区別" と "単語全体" オプションのトグル値に基づいて常に動作するように変更されました。しかし、このトグルは Find ウィジェットが隠れている場合など、それらのトグル値が明確になっていませんでした。これをより明確にするために、次のアクションをトリガーすると、検索ウィジェットが表示されているときにトグルを強調表示します。また、2 つのオプションを簡単に認識することもできます。

マルチカーソルアクションは次のとおりです:

| ラベル | デフォルトのキーバインディング |
|---|---|
| 選択した項目を次の一致項目に追加 | macOS: `⌘D` Win: `Ctrl+D` |
| 最後に選択した項目を次の一致項目に移動 | macOS: `⌘K ⌘D` Win: `Ctrl+K Ctrl+D` |
| 選んだ項目を前の一致項目に追加する | `unassigned` |
| 最後に選んだ項目を前の一致項目に移動する | `unassigned` |
| 一致項目すべてを選択します | macOS: `⌥Enter` Win: `Alt+Enter` |
| すべての出現を変更する | macOS: `⌘F2` Win: `Ctrl+F2`  |

"大文字と小文字の区別" と "単語全体" の 2 つのオプションは、大文字小文字を区別して検索する (macOS: `⌥⌘C` Win: `Alt+C`) または、"単語全体" を検索する (macOS: `⌥⌘W` Win: `Alt+W`) のトグル操作で値を切り替えるときにもエディタの右上に表示される Find ウィジェットに含まれています。

### find ウィジェットにおける \n と \r\n 

find ウィジェットで利用する検索文字列の `\n` は、正規表現モードにおいて、行末シーケンスと常に一致するように変更されました。

これまでの `\n` は `\n` 文字と常に一致していましたが、本リリースから、`\n` は、ファイルの中の文字 `\n`、つまり行の終端文字 `\n` を(ステータスバーに **LF** インジケーターが表示されている場合)、ファイルの中の `\r\n` シーケンス、つまり行の終端文字 `\r\n` と一致するようになりました。(ステータスバーに **CRLF** インジケーターが表示されている場合)

### インデントルールの改善 (Indentation rules improvements)

言語拡張機能が特定の行の正しい字下げレベルを決定するために活用できるインデントルールの実装を改善させました。インデントの調整は、通常、ユーザーが行を書き終えてから `kbstyle(Enter)` を押すことによってトリガされます。

さらに、実験的に実装されたコマンド **Reindent Lines** を実装しました。インデントルールが適切に設定されている場合は、ファイル全体のインデントを調整するために使用することができます。

## 言語サポート (Languages)

### TypeScript リファレンス CodeLens (TypeScript references CodeLens)

TypeScrit リファレンス CodeLens は、クラス、インタフェース、メソッド、プロパティ、およびエクスポートされたオブジェクトの参照インラインカウントを表示します:

![TypeScript references codelens](https://code.visualstudio.com/images/1_9_ts-references-code-lens.png)

TypeScript リファレンス CodeLens を有効にするには、`"typescript.referencesCodeLens.enabled": true` を設定します。

参照数をクリックすると、参照元の一覧をすばやく確認することができます:

![TypeScript references codelens peek](https://code.visualstudio.com/images/1_9_ts-references-code-lens-peek.png)

### TypeScript

VS Code には TypeScript 2.1.5 が含まれています。このバージョンには、多くの重要な[バグ修正](https://github.com/Microsoft/TypeScript/issues?q=is%3Aissue+milestone%3A%22TypeScript+2.1.5%22+label%3A%22fixed%22+)が含まれています。

### TypeScript バージョンの構成 (TypeScript Version Configuration)

ワークスペースで使用される TypeScript のバージョンをより簡単に切り替えることができるようになりました。
ワークスペースで TypeScript または JavaScript ファイルを開き、ステータスバーに表示される TypeScript のバージョン番号をクリックすることで選択できます:

![TypeScript status bar version](https://code.visualstudio.com/images/1_9_ts-status-bar-version.png)

VS Code でどのバージョンの TypeScript を仕様するかを尋ねるメッセージボックスが表示されます: 

![TypeScript version selector](https://code.visualstudio.com/images/1_9_ts-select-ts-version-message.png)

TypeScript のバージョンを切り替えた場合、変更を適用するためにウィンドウの再読み込みが必要になります。

潜在的な[セキュリティ問題](＃settings-and-security) のため、VS Code は `typescript.tsdk` ワークスペース設定から TypeScript のバージョンを自動的にロードしなくなります。 `typescript.tsdk` ワークスペース設定を持つワークスペースが初めて読み込まれるときに、ワークスペース版の TypeScript または VS Code に組み込まれたバージョンを使用するかどうかを尋ねます。

>**注:** ウィンドウの再読み込みには、`Reload Window` コマンドを実行してください

### Markdown プレビューとエディタの統合 (Markdown Preview and editor integration)

VS Code は Markdown エディタのビューとそのプレビューを同期できるようになりました。([#6992](https://github.com/Microsoft/vscode/issues/6992)) デフォルトでは、Markdown プレビューは自動的にスクロールし、エディタ側で選択した行の要素を表示します。

![Markdown Preview editor selection scroll sync](https://code.visualstudio.com/images/1_9_markdown-selection-preview-scroll-sync.gif)

また、Markdown プレビューがスクロールされると、エディタも一緒にスクロールします：

![Markdown Preview to editor scroll sync](https://code.visualstudio.com/images/1_9_markdown-preview-to-editor-scroll-sync.gif)

さらに、Markdown プレビュー側で要素をダブルクリックすることで、エディタが自動的に開き、該当する要素にカーソルを移動させます:

![Markdown Preview double click switches to editor](https://code.visualstudio.com/images/1_9_markdown-double-click-preview-switch.gif)

### その他の Markdown 機能改善 (Other Markdown improvements)

* Markdown ファイル内で C++, Go, Rust, および Scala コードブロックのシンタックスハイライトをサポート
* 段落の直後の行にあるブロック要素の Markdown 構文ハイライト処理が修正されました
* Markdown プレビューが最初に開かれると、エディタで選択された行に自動的にスクロールします
* Markdown プレビュー時に左側に表示される灰色のバーは、現在選択されている行を示しています
* ローカルファイルへのリンクが Markdown プレビューで動作するようになりました
* Markdown エディタで、ローカルファイルへのリンクを `kbstyle(Ctrl)` を押しながらクリックすることで、エディタで開くことができるようになりました

### Emmet の環境設定、プロファイル、スニペット、および略語を外部ファイルから読み込む (Load Emmet preferences, profiles, snippets and abbreviations from external files)

新しい設定 `emmet.extensionsPath` は、`snippets.json`, `syntaxProfiles.json`,` preferences.json` のいずれか、またはすべてが存在する場所(絶対パスまたは相対パス)を提供するために使用できます。これらのファイルを使用した Emmet のカスタマイズ方法詳細については、[Emmet Customization](http://docs.emmet.io/customization/) を参照してください。

既存の設定 `emmet.preferences` と `emmet.syntaxProfiles` は、上記の json ファイルの値を上書きします。

**注**: ファイルの内容はキャッシュされるため、これらのファイルを新たに追加したときや、内容を変更するたびに VS Code ウィンドウを再読み込み (`Reload Window` コマンドの実行)をする必要があります

### SCSS map のサポート (SCSS map support)

SCSS 言語サポートは、SCSS map 構文（[＃1758](https://github.com/Microsoft/vscode/issues/1758) を理解できるようになりました。

### 新しい HTML 設定 (New HTML settings)

HTML フォーマッタ（[jsbeautifier](http://jsbeautifier.org/) ベース）が更新され、新しいオプションが利用可能になりました: 

- `html.format.contentUnformatted`: 再フォーマットしてはならないタグをカンマ区切りで示したリスト。`null` の場合、既定値として [Phrasing content](https://www.w3.org/TR/html5/dom.html#phrasing-content) にリストされているすべてのタグが対象になります
- `html.format.wrapAttributes`：属性の折り返し方を指定：
  - `auto`: 行の長さを超えたときに折り返す
  - `force`: 最初のものを除く、すべての属性を折り返す
  - `force-aligned`: 最初を除くすべての属性を折り返すと共にし整列させる
  - `force-expand-multiline`: 全ての属性を折り返す

次のオプションを使用すると、スクリプトとスタイルの検証を無効にすることができます:

- `html.validate.scripts`: 組み込みの HTML 言語サポートが、組み込みスクリプトを検証するかどうかを設定します
- `html.validate.styles`: 組み込みの HTML 言語サポートが、組み込みスタイルを検証するかどうかを設定します

### 新しい PHP 設定 (New PHP settings)

次のオプションを使用することで、組み込みの PHP 言語サポートの補完機能およびホバーサポートを無効にすることができます:

- `php.suggest.basic`: 組み込みの PHP 言語候補機能を有効にするかどうかを設定します。このサポートによって、PHP グローバルと変数の候補が示されます。

### `php.validate.executablePath` 設定の確認 (Confirmation of the `php.validate.executablePath` setting)

潜在的なセキュリティリスクを回避するため、`php.validate.executablePath` ワークスペース設定に指定されているプログラムを実行する前に確認を求めるようになりました

![Confirming PHP executable](https://code.visualstudio.com/images/1_9_confirming-php.png)

`php.validate.executablePath` がユーザー設定で設定されている場合は、確認は求められません。

## 拡張機能 (Extensions)

### 拡張パックを簡単に作成する (Easily create an Extension Pack)

[Extension Packs](https://code.visualstudio.com/Docs/extensionAPI/extension-manifest#_extension-packs) により、複数の拡張機能をまとめて一緒にインストールすることが可能になり、Extension Pack を作成するためのサポートが Code Yeoman ジェネレータに追加されました。

![extensionpackgenerator](https://code.visualstudio.com/images/1_9_extensionpack-generator.png)

ジェネレータは拡張機能パックを作成しますが、必要に応じて、現在インストールされている拡張機能一覧を拡張機能パックとして取り込むこともできます。 このようにして、お気に入りの拡張機能で拡張パックを簡単に作成し、マーケットプレイスに公開し、他のユーザーと共有することが可能になります。

## デバッグ (Debugging)

### 起動構成を必要としないデバッグ (Debugging without a launch configuration)

[ユーザーからのリクエスト](https://github.com/Microsoft/vscode/issues/285)により、単一ファイル(紫色のステータスバーで示される、いわゆる「フォルダが開かれていないワークスペース」の状態)において、デバッグを開始するための `launch.json` ファイルが必要なくなりました。`F5` を押すことで、すぐにデバッグセッションを開始できます。高度なデバッグ機能を必要とする場合は、引き続き `launch.json` が必要です。

>**注:** 現在、この機能は、Node.js および PowerShell デバッガでのみサポートされていますが、他のデバッグ拡張機能にもすぐに追加される予定です

![no folder debug](https://code.visualstudio.com/images/1_9_no_folder_debug.gif)

### ソースコード内のインライン変数値 (Inline variable values in source code)

ユーザーからの [PR](https://github.com/Microsoft/vscode/pull/16129) により、ソースコード内で変数値をインライン表示できるようになりました。
この機能はまだ実験中となるため、デフォルトでは無効になっています。これを有効にするには、`settings.json`で `debug.inlineValues "：true` を設定してください。

![debug inline values](https://code.visualstudio.com/images/1_9_inline_values.png)

### デバッグ環境の自動選択 (Automatically choosing debug environment)

アクティブなファイルにより、VS Code が自動的にデバッグ環境を選択するようになりました。
たとえば、ユーザーがエディタで JavaScript ファイルをアクティブにしており、`launch.json` ファイルをセットアップしたいのであれば、JavaScript 用の `launch.json` が自動的に生成されます。

### ユーザレベルの launch.json (User level launch.json)

[ユーからのリクエスト](https://github.com/Microsoft/vscode/issues/18401)により、
起動構成としてすべてのワークスペースで共有される 'launch' オブジェクトをユーザー設定に含めることが可能になりました。

### ドロップダウンから起動構成を追加する (Add launch configuration from dropdown)

デバッグビューのドロップダウンからオプションを選択するだけで、新しい起動構成を追加できるようになりました:

![add launch configuration](https://code.visualstudio.com/images/1_9_add_launch.png)

### コールスタックアクションのコピー (Copy callstack action)

コールスタックをクリップボードにコピーするためのコンテキストメニューアクションをコールスタックビューに追加しました。問題が発生したコールスタックをレポートする必要がある場合などに便利です。

![debug inline values](https://code.visualstudio.com/images/1_9_copy_stack.png)

## Node.js のデバッグ (Node Debugging)

### Node.js におけるシナリオ別の起動構成スニペット (Launch configuration snippets for Node scenarios)

よく使用されるいくつかの Node.js デバッグシナリオをサポートするために、いくつかの起動構成スニペットを追加しました。 これらのスニペットは、`launch.json` を編集するときに IntelliSense で利用されます:

![Launch configuration snippets for node.js](https://code.visualstudio.com/images/1_9_launch-snippets.png)

Here is the list of all snippets:
すべてのスニペットのリストは次のとおりです:

- **プログラムの起動 (Launch Program)**: Node.js プログラムをデバッグモードで起動します。 スニペットは、プログラムファイル名を入力するように求めます。s
- **NPM による起動 (Launch via NPM)**: npm の 'debug' スクリプトを通して node プログラムを起動します。 package.json に npm デバッグスクリプトを定義している場合は、これを起動構成から直接使用することができます。npm スクリプトで使用されるデバッグポートがスニペットで指定されたポートに対応することを確認してください
- **ポートへのアタッチ (Attach to Port)**: 実行中の Node.js プログラムのデバッグポートに接続します。 デバッグする Node.js プログラムがデバッグモードで起動され、使用されているデバッグポートがスニペットで指定されているものと同じであることを確認してください
- **プロセスへのアタッチ (Attach to Process)**: プロセスピッカーを開いて、デバッグ用の node または gulp プロセスを選択します。この起動構成では、デバッグモードで起動されていない node または gulp プロセスに接続することもできます
- **nodemon のセットアップ (Nodemon Setup)**: JavaScript ソースの変更を検知し自動的にデバッグセッションを再起動を可能とする nodemon をセットアップします。nodemon がワークスペースにではなく、グローバルにインストールされていることを確認してください。デバッグセッションを終了すると、プログラムはデバッグを終了するだけで、nodemon 自体は終了しません。 nodemon を終了するには、統合端末上で `Control-C` を押してください
- **Mocha テスト (Mocha Tests)**: プロジェクトの `test` フォルダ内に配置される mocha テストをデバッグします。プロジェクトの `node_modules` フォルダに`mocha` がインストールされていることを確認してください
- **Yemon ジェネレータ (Yeoman generator)** Yeoman ジェネレータをデバッグします。スニペットはジェネレータの名前を指定するように指示します。プロジェクトの `node_modules` フォルダに `yo` がインストールされていること、およびプロジェクトフォルダで `npm link` を実行しデバッグ用にインストールされていることを確認してください
- **gulp タスク (Gulp task)**: gulp タスクをデバッグします。スニペットは、グループタスクの名前を指定するように要求します。プロジェクトの `node_modules` フォルダに gulp がインストールされていることを確認してください。

### Just My Code の改善 (Just My Code improvements)

[VS Code 1.8](https://code.visualstudio.com/updates/v1_8#_just-my-code-node-and-node2) で実装された 'マイコードのみ (Just My Code)' 機能に、いくつかの仕上げを追加しました:

- `skipFiles` 属性により、コアモジュールをスキップすることをサポートします。'魔法の名前'となる `<node_internals>` により、Node.js に組み込まれているコアモジュールをグロブパターンで簡単に指定できるようになりました。

次の例では、`events.js` 以外のすべての内部モジュールをスキップします:

  ```json
  "skipFiles": [
     "<node_internals>/**/*.js",
     "!<node_internals>/events.js"
   ]
  ```

- スキップされたソースは、CALL STACKビュー内で淡色表示されます:

  ![Skipped source is dimmed in call stack view](https://code.visualstudio.com/images/1_9_dimmed-callstack.png)

  淡色表示されたエントリの上にカーソルを置くと、なぜスタックフレームが淡色に表示されているかの理由を表示します。

- 実行時にスキップするファイルを追加できるコンテキストメニューアクションを新たにサポート(`node2` のみ):

  ![toggle skip files](https://code.visualstudio.com/images/1_9_toggle-skip-file.png)

コールスタックの新しいコンテキストメニューアクション: **Toggle skipping this file** を使用すると、起動構成に  `"skipFiles"`を追加することなく実行時にファイルを簡単にスキップすることができます。このオプションは、現在のデバッグセッションでのみ存続します。起動構成の `skipFiles` オプションでスキップ対象となっているファイルのスキップを停止することもできます。

### Support 'restart' option for 'launch' requests

しばらくの間、VS Code の Node.js デバッガは起動構成の `attach` 構成において `restart` 属性をサポートしていました。詳細については、[Node.js Debugging: Attaching to Node.js](https://code.visualstudio.com/docs/editor/node-debugging#_attaching-to-nodejs)を参照してください。このリリースでは、`launch` 構成の `restart` 属性を新たにサポートします。

この機能を有効にすると、Node.js の終了を検出するたびに VS Code がデバッグセッションを再開します。この機能は、JavaScript ソースが変更されたことを検出することで Node.js を再起動させる [`nodemon` ユーティリティ](https://github.com/remy/nodemon)と組み合わせて使用します。

この起動設定 (IntelliSense によるスニペットとして利用可能) は、`nodemon` と` restart` オプションを利用します:

```json
{
	"type": "node",
	"request": "launch",
	"name": "nodemon",
	"cwd": "${workspaceRoot}",
	"runtimeExecutable": "nodemon",
	"runtimeArgs": [
		"--debug=5858"
	],
	"program": "${workspaceRoot}/app.js",
	"restart": true,
	"port": 5858
}
```

### ソースマップのサポートが常に有効に (Source map support now always enabled)

VS Code 1.9 以降、ソースマップのサポートがデフォルトで有効になりました。そのため、`sourceMaps` を `true` に設定する必要はなくなりましたが、Node.js デバッガには生成された JavaScript の場所を知らせる必要があるため、`outFiles` グロブパターンを指定する必要があります。また、`sourceMaps` に `false` を設定すると、ソースマップのサポートを無効にすることができます。

### コンソールでのオブジェクト表示の改善 (Better object display in the console) (node2)

`node2` デバッグアダプタでは、オブジェクトとともに `console.log` を呼び出すと、テキストプレビューではなく、コンソールに展開可能なオブジェクトが表示されるようになりました。

![log objects](https://code.visualstudio.com/images/1_9_log-objects.png)

## 拡張機能のオーサリング (Extension Authoring)

### スニペットを挿入するエディタ API (Editor API to insert a snippet)

エディタに `SnippetString` を挿入することができる、新しい` TextEditor＃insertSnippet` メソッドを追加しました。

### コードレンズのアップデート (Updating CodeLens)

`CodeLensProvider` は、レンズを変更などによりリフレッシュする必要があることをエディタに知らせるための `onDidChangeCodeLenses` イベントを持つことができるようになりました。

### 補完アイテムのコミット文字 (Completion item commit characters)

`CompletionItems` はコミット文字のリストを持つことができるようになりました。コミット文字が入力され、補完が選択されているときに、その文字が入力されると補完アイテムが挿入されます。

### 新しい ImplementationProvider API を追加 (Added new ImplementationProvider API)

新しい `ImplementationProvider` インターフェイスが追加され、新しい **Go to Implementation** 機能に対応しました。`ImplementationProvider` は、テキストドキュメント内の場所を実装場所のリストにマップします。たとえば、インタフェースからこのインタフェースを実装するクラス、または抽象メソッドから実装メソッドのリストへ移動するなどです。

拡張機能で **Go to Implementation** をサポートするには、`ImplementationProvider` を実装し、 `vscode.languages.registerImplementationProvider` を使ってプロバイダを登録することで可能になります。

### オプションの言語で無題のドキュメントを開くための新しい API を追加 (New API to open an untitled file with optional language)

`openTextDocument` メソッドに新しいオーバーロードが追加されました。これにより、無題のドキュメントをオプションの言語で開くことができます。たとえば、次のように呼び出すことができます:

`openTextDocument({ language: 'xml' })`

言語として XML を使用したテキストドキュメントを作成します。言語オプションを省略すると、プレーンテキストが言語として選択された無題のドキュメントが作成されます。

### TextEditorRevealType.AtTop

新しい `AtTop` 値が `TextEditorRevealType` enum 型に追加されました。 これにより、ビューポートの上部の範囲を明らかにすることができます。

### CompletionItemKind.Folder

新しい `Folder` 値が `CompletionItemKind` enum 型に追加されました。

### 提案中の Progress API (Proposed Progress API)

現在、ステータスバーやビューなど、エディタのさまざまな場所で進行状況を表示するための API が提案されています。しかし、それはまだ初期段階にあるため、フィードバックを求めています。この API を試すには、次のようにします:

* [`vscode.proposed.d.ts`](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.proposed.d.ts#L30) を TypeScript プロジェクトにコピーします
* 拡張機能の `package.json` に、 `"enableProposedApi": true` を追加することで提案された API を有効にできます

提案中の API は、拡張機能を開発するときにのみ利用可能です。作成した拡張機能がマーケットプレースに公開された場合に利用できないことに注意してください。

### Contributable SCM Providers

さまざまな [contributable providers] (https://github.com/Microsoft/vscode/issues/2824)から SCM 機能を提供するために、ソースコードを管理する機能に大きなリファクタリングを開始しました。また、すべての Git 機能が [SCM プロバイダ](https://github.com/Microsoft/vscode/blob/23c4c8d1b881cfbf48e76fbe67e350b4efecba68/src/vs/vscode.proposed.d.ts#L143)を利用するよう移行される予定です。

新しい動作は **SCM：Enable Preview SCM** コマンドで試してみることができます。このコマンドを実行することで、現在の Git 機能を実験的な機能に置き換えます (**SCM: Disable Preview SCM** コマンドで元に戻せます）。この機能は、未だ完全ではなく実装中であることに注意してください。実装の進捗状況は[#18615](https://github.com/Microsoft/vscode/issues/18615) で確認できます。

### デバッグ拡張機能の開発 (Debugger Extension Authoring)

`debuggers` コントリビュート・ポイントに、オプションとして利用できる次のサブコントリビュート・ポイントを追加しました：

- `languages` <br> このオプションは、デバッグ拡張機能が「デフォルトのデバッガ」として利用される言語をリストすることができます。VS Code が、特定のソース言語に対してデバッガを自動的に検出する必要がある場合にのみ、このオプションを使用してください

- `startSessionCommand` <br> VS Code がこの拡張を対象とする「デバッグ」または「実行」アクションを呼び出すコマンドの ID を取得します。起動構成が選択されている場合、それはコマンドの引数として渡されます (拡張機能は、必要に応じて起動構成を調整することができます）。既存の起動構成なしで「デバッグ」または「実行」が実行されると、空の起動設定が `startSessionCommand` に渡され、拡張機能が不足している属性を「埋め込む」ことを期待します。この動作は、現在エディタで開いているファイルに基づいています。

- `adapterExecutableCommand` <br> VS Code は、対応する拡張機能の package.json から `program`,` args`, `runtime` と `runtimeArgs` 属性を使用してデバッグアダプタを起動します。VS Code 1.9 から、拡張機能がコマンドを提供することも可能になり、これを利用することでデバッグアダプタの実行可能パスと引数は動的に設定されます。<br> package.json 内のデバッガのコントリビュート・ポイントに `program`, ` args`, `runtime` と `runtimeArgs` という属性を定義する代わりに、新しい属性 `adapterExecutableCommand` に、拡張機能に登録されているコマンドの ID を設定してください。 このコマンドは次の形式の構造体を返します:

  ```json
  command: "<executable>",
  args: [ "<argument1>", "<argument2>", ... ]
  ```

  `command` 属性は、実行可能ファイルへの絶対パスか、PATH 環境変数によって検索された実行ファイルの名前のいずれかでなければなりません。また、`node` は特別な値とみなされます。この値がセットされた場合は、PATH 上に存在する同名のコマンドを利用することはなく、VS Code にビルトインされている node ランタイムを利用することを意味します。

### VS Code デバッグ・プロトコル (VS Code Debug Protocol)

新しいオプションの属性 `presentationHint` が `Source` 型に追加されました。これにより、デバッグアダプタは、UI でソースをレンダリングするためのヒントを提供することができます。`deemphasize` の値は、ソースが利用できないこと、またはステッピングでスキップされたことを示すために使用できます。

## その他 (Miscellaneous)

### 設定とセキュリティ (Settings and security)

設定では、VS Code 上で作業を行うために必要となるいくつかの実行可能ファイルを指定することができます。たとえば、統合端末が使用するシェルを選択できます。これまでの設定と同じように、ユーザー設定やワークスペース設定として定義することもできますが、セキュリティを強化するためにも、ワークスペース毎に個別で定義することはできなくなりました。

ワークスペース・レベルでの設定が行えない項目の完全なリストを次に示します:

- git.path
- terminal.integrated.shell.linux
- terminal.integrated.shellArgs.linux
- terminal.integrated.shell.osx
- terminal.integrated.shellArgs.osx
- terminal.integrated.shell.windows
- terminal.integrated.shellArgs.windows
- terminal.external.windowsExec
- terminal.external.osxExec
- terminal.external.linuxExec

ワークスペースを開いたときに、ワークスペースで上記の項目が定義されているかを見つけ出し警告を出力します。また、ワークスペース・レベルで定義されているこれらの設定は無視されます。

`typescript.tsdk` と `php.validate.executablePath` 設定についても、それぞれに対処された同様のセキュリティt対策を適用しました。

### Ubuntu 上の Unity から新しいインスタンスを起動する (Launch new instance from Unity on Ubuntu)

Ubuntu 上の Unity ユーザインタフェースからアプリケーションの新しいインスタンスを起動する標準のショートカットにて、VS Code の新しいインスタンスを正しく開くようになりました。 (`Win+Shift+<number>`, `Shift+click`, middle click)

### パフォーマンスの問題を報告する新しいコマンド (New command to report performance issues)

**コマンドパレット** に新しいコマンド **Report Performance Issues** を追加しました。これにより、パフォーマンス問題についてレポートが必要になった場合に、環境情報とあらかじめ設定されたパフォーマンスのタイミングに関する詳細情報 (OS, CPU, メモリ, タスクのタイミングなど) が追記された、新しい GitHub issue を作成することができます。VS Code の動作が遅くなっていると感じた場合、ぜひ、この新しいコマンドを使って教えてください！

### エディタ性能の最適化 (Editor Performance Optimization)

特定の条件下において、エディタでフレームをペイントする時間(時間の 95％ 以上がそれに費やされる)を大幅に短縮するヒューリスティックな処理を追加しました。

使用しているフォントが等幅フォントのであったり (ほとんどのプログラミングフォントは等幅フォントです)、特定の行が ASCII 文字のみで構成されている場合 (ソースコードの行のほとんどが ASCII 範囲 32-126 またはタブにとどまっています)、特定のエディタデコレーション (CSS のカラーボックスのような) はライン上に存在しないため、テキストがペイントされた場所についてブラウザに問い合わせることをスキップでき、単純に JavaScript で計算を実行することが可能になります。

この最適化により、強制的なブラウザレイアウトが不要になり、フレームをペイントするのにかかる時間がさらに短縮されます。

>Note: カーソルがテキストからわずかに離れてレンダリングされていることに気がついた場合は知らせてください。この最適化は `editor.disableMonospaceOptimizations` で無効できます。

## 注目すべき変更 (Notable Changes)

* [16803](https://github.com/Microsoft/vscode/issues/16803): Preserve language picked for untitled text documents
* [16588](https://github.com/Microsoft/vscode/issues/16588): Preserve view state for untitled files between restarts
* [17408](https://github.com/Microsoft/vscode/issues/17408): Search does not work in UTF-16 LE encoded files
* [12831](https://github.com/Microsoft/vscode/issues/12831): Support standard tab navigation key shortcuts on macOS
* [10444](https://github.com/Microsoft/vscode/issues/10444): Persist character encoding of open files across restart
* [18037](https://github.com/Microsoft/vscode/issues/18037): Possible to save file multiple times leads to race condition
* [14464](https://github.com/Microsoft/vscode/issues/14464): Preserve editor relative sizes when switching layouts
* [18003](https://github.com/Microsoft/vscode/issues/18003): Search relevance in Quick Pick control
* [14625](https://github.com/Microsoft/vscode/issues/14625): Update menu when reassigning keybindings or installing keybinding extension
* [18290](https://github.com/Microsoft/vscode/issues/18290): Moving or renaming file does not preserve editor view state
* [12040](https://github.com/Microsoft/vscode/issues/12040): Identical file name path in tab is too long and difficult to diff
* [17495](https://github.com/Microsoft/vscode/issues/17495): Explorer: Does not sort files and folders with numerical values accordingly
* [7876](https://github.com/Microsoft/vscode/issues/7876): Allow to use Ctrl P/N for up and down navigation in quick open
* [6502](https://github.com/Microsoft/vscode/issues/6502): Apply excludes to editor history quick open too
* [18679](https://github.com/Microsoft/vscode/issues/18679): F4 added as a keybinding to navigate search results - may conflict with some extension keybindings
* [11908](https://github.com/Microsoft/vscode/issues/11908): ALT + Arrows does not work in integrated terminal
* [14479](https://github.com/Microsoft/vscode/issues/14479): Integrated Terminal eats half of the first line when you zoom
* [18952](https://github.com/Microsoft/vscode/issues/18952): Terminal tab stops broken after resize
* [18332](https://github.com/Microsoft/vscode/issues/18332): Background terminal scroll bars are not synced when the foreground terminal is resized
* [18758](https://github.com/Microsoft/vscode/issues/18758): Hard crash (of everything) when debugging nodejs
* [19377](https://github.com/Microsoft/vscode/issues/19377): Explorer refresh not working for folders with same prefix

[クローズされたバグ一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+label%3Abug+milestone%3A%22January+2017%22+is%3Aclosed)と、1.9 アップデートにて[クローズされた機能のリクエスト一覧](https://github.com/Microsoft/vscode/issues?q=is%3Aissue+milestone%3A%22January+2017%22+is%3Aclosed+label%3Afeature-request)です。

## 拡張機能への貢献 (Contributions to Extensions)

私たちのチームは、いくつかの VS Code 拡張機能の提供とメンテナンスに貢献しています。注目すべき拡張機能は：

* [Go](https://marketplace.visualstudio.com/items?itemName=lukehoban.Go)
* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)
* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
* [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome)
* [VSCodeVim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim)

さらに、IDE 利用シナリオのために設計された [early-stage PHP parser](https://github.com/Microsoft/tolerant-php-parser) をリリースしました。これは、拡張機能の作成者が PHP のためのより優れたツーリングサポートを提供するの際に役立ちます。パーサーは、PHPで書かれており、高速かつメモリ効率が高く、適切なエラー処理を提供し、典型的な構文ツリー(コメント/空白を含む)を生成します。

## Thank You

最後になりましたが、VS Code をより良いものにするために協力してくれた次の方々に多大なる感謝を込めて:

* [Adrian Perez (@aperezdc)](https://github.com/aperezdc)
  *  Add a few niceties for making Flatpak builds of VS Code [PR #17370](https://github.com/Microsoft/vscode/pull/17370)
  *  Add an AppData XML data file to Linux builds [PR #17369](https://github.com/Microsoft/vscode/pull/17369)
  *  Support building Flatpak application bundles [PR #16169](https://github.com/Microsoft/vscode/pull/16169)
* [Artem Govorov (@ArtemGovorov)](https://github.com/ArtemGovorov):  Add Toggle Output Scroll Lock action [PR #18768](https://github.com/Microsoft/vscode/pull/18768)
* [Charles Pierce (@charlespierce)](https://github.com/charlespierce):  #14464 Preserve editor size when switching layout [PR #17760](https://github.com/Microsoft/vscode/pull/17760)
* [Chirag Bhatia (@chirag64)](https://github.com/chirag64):  Fixes #19194 - Added option to clear Terminal in Terminal Context menu [PR #19393](https://github.com/Microsoft/vscode/pull/19393)
* [Geir Sagberg (@geirsagberg)](https://github.com/geirsagberg)
  *  Make high contrast detection configurable [PR #17394](https://github.com/Microsoft/vscode/pull/17394)
  *  Check window.autoDetectHighContrast on window load [PR #17832](https://github.com/Microsoft/vscode/pull/17832)
* [@hun1ahpu](https://github.com/hun1ahpu)
  *  Fix labels unit tests + root displayed as '.. [PR #18575](https://github.com/Microsoft/vscode/pull/18575)
  *  Right click to copy selection and paste on Windows [PR #17496](https://github.com/Microsoft/vscode/pull/17496)
* [Yuki Ueda (@Ikuyadeu)](https://github.com/Ikuyadeu)
  *  Re use readonly #12732 #13863 [PR #18251](https://github.com/Microsoft/vscode/pull/18251)
* [Jess Chadwick (@jchadwick)](https://github.com/jchadwick)
  *  Setting Powershell as default terminal for Windows 10+ (fixes #16838) [PR #18493](https://github.com/Microsoft/vscode/pull/18493)
  *  Fixing sorting of directory and filenames with numbers [PR #18539](https://github.com/Microsoft/vscode/pull/18539)
* [Jimi (Dimitris) Charalampidis (@JimiC)](https://github.com/JimiC):  Change order of Diff extensions. [PR #17680](https://github.com/Microsoft/vscode/pull/17680)
* [@jmdowns2](https://github.com/jmdowns2)
  *  Fix for #12833. [PR #17625](https://github.com/Microsoft/vscode/pull/17625)
  *  Fix for #16771.  [PR #17698](https://github.com/Microsoft/vscode/pull/17698)
* [Joel Day (@joelday)](https://github.com/joelday):  Adding an overload to TextEditor.edit for insertion of a SnippetString [PR #17628](https://github.com/Microsoft/vscode/pull/17628)
* [Morag S. (@morags)](https://github.com/morags):  Markdown fixes [PR #18704](https://github.com/Microsoft/vscode/pull/18704)
* [@mrdrogdrog](https://github.com/mrdrogdrog):  linux argument startup fix [PR #17853](https://github.com/Microsoft/vscode/pull/17853)
* [Manoj Patel (@nojvek)](https://github.com/nojvek)
  *  inline values as decorators when debugging [PR #16129](https://github.com/Microsoft/vscode/pull/16129)
  *  Fix bug in decorationRenderHelper [PR #18361](https://github.com/Microsoft/vscode/pull/18361)
* [Nick Olinger (@olingern)](https://github.com/olingern):  Cache release notes. Fixes #13257 [PR #15050](https://github.com/Microsoft/vscode/pull/15050)
* [Marcel Miranda Ackerman (@reaktivo)](https://github.com/reaktivo):  Adds support for moving the tab close button to the left [PR #17863](https://github.com/Microsoft/vscode/pull/17863)
* [John Rothfels (@rothfels)](https://github.com/rothfels):  Ensure workspace is read from WorkspaceContextService [PR #17494](https://github.com/Microsoft/vscode/pull/17494)
* [Ryan Patterson (@ryapapap)](https://github.com/ryapapap):  Option to exclude items from Git branch checkout list #13506 [PR #16792](https://github.com/Microsoft/vscode/pull/16792)
* [Matteo (@xadhoom)](https://github.com/xadhoom):  Add GConf2 dependency in rpm spec template [PR #16016](https://github.com/Microsoft/vscode/pull/16016)
* [David Terry (@xwvvvvwx)](https://github.com/xwvvvvwx):  Add config setting to control whether alt should show the menu bar [PR #17517](https://github.com/Microsoft/vscode/pull/17517)

`vscode-eslint` への貢献: 

* [Giovanni Calò (@giovannicalo)](https://github.com/giovannicalo): Fixed typo [PR #190](https://github.com/Microsoft/vscode-eslint/pull/190)

`vscode-tslint` への貢献: 

* [Yuichi Nukiyama (@YuichiNukiyama)](https://github.com/YuichiNukiyama):  Add jsEnable option [PR #154](https://github.com/Microsoft/vscode-tslint/pull/154)

`vscode-languageserver-node` への貢献::

* [Per Lundberg (@perlun)](https://github.com/perlun): README.md: Fixed typos [PR #138](https://github.com/Microsoft/vscode-languageserver-node/pull/138)
* [Federico Bond](https://github.com/federicobond): Fix typo [PR #144](https://github.com/Microsoft/vscode-languageserver-node/pull/144)

`language-server-protocol` への貢献:

* [Guillaume Martres (@smarter)](https://github.com/smarter): Fix incorrect numbering in CompletionItemKind [#151](https://github.com/Microsoft/language-server-protocol/pull/151)
* [Olivier Thomann (@othomann)](https://github.com/othomann): Fix some typos [#149](https://github.com/Microsoft/language-server-protocol/pull/149)

`vsce` への貢献:

* [Chris (@LaChRiZ)](https://github.com/LaChRiZ): fixed description in option baseImagesUrl of package command [#151](https://github.com/Microsoft/vscode-vsce/pull/151)

`vscode-generator-code` への貢献::

* [Spencer Elliott (@elliottsj)](https://github.com/elliottsj): Use `code` markup for `<user home>` in quickstarts [#61](https://github.com/Microsoft/vscode-generator-code/pull/61)

<!-- In-product release notes styles.  Do not modify without also modifying regex in gulpfile.common.js -->
<a id="scroll-to-top" role="button" aria-label="scroll to top" onclick="scroll(0,0); event.preventDefault(); event.stopPropagation()"><span class="icon"></span></a>
<link rel="stylesheet" type="text/css" href="css/inproduct_releasenotes.css"/>
