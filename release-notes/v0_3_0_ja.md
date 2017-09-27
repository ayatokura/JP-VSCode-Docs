---
Order: 1
TOCTitle: June 2015
PageTitle: Visual Studio Code 0.3.0
MetaDescription: Visual Studio Code 0.3.0
---

# June 2015 (0.3.0)

Visual Studio Code を利用すると共に、フィードバックを続けてくれてありがとうございます。
本リリースでは、フィードバックに基づき、頻繁に要求されるいくつかの機能強化を追加しながら、300 を超えるマイナーな改良とバグ修正を行いました。
そして、今後は毎月のアップデートを提供して行きます。

新しい VS Code を取得するために[アップデートの方法](/docs/supporting/howtoupdate.md)を参照してください。そして、このリリースにおける多数の変更点を確認してください。

## Key Bindings
## キー割り当て

ユーザーからのフィードバックにより、いくつかのキーバインディングの変更を行うことにしました。（ありがとう！）
変更が気に入らない場合は [keybindings](/docs/customization/keybindings.md) ドキュメントに記載されている方法で変更できます。

* OS ネィティブなファイルを開くダイアログは `Ctrl + O` (Mac: `cmd + O`) にアサインされました。VS Code の中でファイルを開くダイアログに、このキーをアサインしたことが混乱を招く原因になると強いフィードバックを受けたためです
* コードファイルを開くダイアログには、`kb(workbench.action.quickOpen)` を介してアクセスできるようになりました。私たちは、コードファイルを開くダイアログのための新しいキーを見つける必要がありましたが、多くのユーザーは、ファイルを開くダイアログを呼び出すために `kb(workbench.action.quickOpen)` を使用していたため、このトレンドに合わせることにしました
* 定義に移動するには `kb(editor.action.goToDeclaration)` を使用します。(Windows では `kbstyle(Ctrl+F12)`)
以前のリリースの VS Code エディタはブラウザ内で実行されていたため、F12 で開発者ツールを開きましたが、Visual Studio ユーザーから、Visual Studio の `Go To Definition` と同様の操作になるよう提案があり、それを実装しました
* ファイルの最初と最後にジャンプする `kbstyle(Cmd+Up)` と `kbstyle(Cmd+Down)` が Mac 上で期待通りに動作するようになりました
* `kb(editor.action.format)` でコードの整形が可能になりました

## Command line args
## コマンドラインの引数

コマンドラインから新しいファイルを作成することが可能になりました。新しくファイルを作成する場合は、パスを追加したファイル名を指定します。パスが指定されずファイル名だけの場合は、カレントディレクトリにファイルが作成されます。
指定されたファイルは、ダーティファイル（変更されたが、まだ保存されていないファイル）としてエディタ上で開かれます。(保存することで、指定されたパスに書き出されファイルが作成されます)

`code mynewfile.js`

コマンドラインから複数のフォルダまたはファイルを開くことができます。(一つのインスタンスで、複数のフォルダやファイルを開くわけではないことに注意してください。指定されたフォルダやファイルの数だけインスタンスが生成されます)
VS Code で複数のセッションを開くには、複数のフォルダまたはファイルのパスを引数に追加します。

`code c:\myfolder1 c:\myfolder2 c:\myapp\program.cs`

新しいフォルダやファイルを開く場合は、既に起動しているインスタンスを再利用します。

また、代わりに前のセッションを利用して新しいセッションを開くことができます。前のセッションを利用せずに VS Code を新たなウインドウで開始したい場合は、新しいスイッチ、`-n` または `--new-window` を使用してください。

`code -n`

## Editing

### Multi-cursor
### マルチカーソル

マルチ・カーソル機能を下記のように改善しました:

* `kb(editor.action.addSelectionToNextFindMatch)` カーソル位置の`単語が選択`されるか、または`現在選択中の文字列と次に出現する同じ文字列`を選択します。
* `kb(editor.action.moveSelectionToNextFindMatch)` `現在選択中の文字列と次に出現する同じ文字列の最後にカーソルを追加`し移動します。
* この 2 つのアクションは、検索ウィジェットの **matchCase** と **matchWholeWord** 設定を拾います。
* `kb(cursorUndo)` 最後のカーソル操作を取り消します。1 カーソルにあまりにも多くを追加したり、ミスした場合は `kb(cursorUndo)` を押すことで、最後のカーソル操作を取り消し、直前のカーソルの状態に戻ります。
* 上にカーソルを挿入 (`kb(editor.action.insertCursorAbove)`) および下にカーソルを挿入 (`kb(editor.action.insertCursorBelow)`) する操作では、最後に追加されたカーソルを明確にし、マルチカーソルが複数の画面の高さにまたがって動作することが容易になります。（例: スクリーンとしては 80 ラインのみの表示ですが、それを超えるラインでのマルチカーソル操作が可能）

### Comment action
### コメント・アクション

コメント・アクションのために下記の変更を追加しました:

* `kb(editor.action.addCommentLine)` 強制的にラインコメントを追加します
* `kb(editor.action.removeCommentLine)` 強制的にアンコメントします(複数行を選択した際、ラインコメントを含んでいるものがあれば、そのラインコメントは解除されます)
* `kb(editor.action.commentLine)` 行コメントのトグルは以前と同じように、選択されたコードのインデントに揃えて行コメントトークンを挿入します。また、変更が加えられていない空白または空白行だけを残します。`kb(editor.action.commentLine)` is also more forgiving with regards to selection state when toggling comments in languages which only support block comments, such as CSS or HTML.
CSS や HTML のような、ブロックコメントのみをサポートする言語にて、選択状態にある部分をコメントに切り替えるときなどは `kb(editor.action.commentLine)` が役立ちます。
* トグルブロックコメント (`kb(editor.action.blockComment)`) は、選択された範囲を対象にブロックコメントとして切り替える際に役立ちます。

![Block comments](https://code.visualstudio.com/images/0_3_0_BlockComments.png)

### Indentation

空の行で `kbstyle(Tab)` を押すと、正しい開始位置にカーソルを置くために、必要に応じて 1 つまたは複数のインデントが挿入されます。(これは、インデントが 1 つだけ挿入されるという意味ではありません)

### Shrink/expand selection

Quickly shrink or expand the current selection (applies to all languages).
現在の選択範囲を素早く縮小または拡大することが可能です。(すべての言語で利用可能)  トリガーは、`kb(editor.action.smartSelect.shrink)` と `kb(editor.action.smartSelect.grow)` です。

ここでは `kb(editor.action.smartSelect.grow)` による選択範囲を拡大する例を示します:

![Expand selection](images/0_3_0/expandselection.gif)

### Wrapping control
コードの読みやすさを向上させるために、**settings.json** に追加された新しい設定 `editor.wrappingIndent` で、折り返し行のインデント制御が可能になりました。以下の値が `editor.wrappingIndent` で利用可能です。:

* `none`: 行が折り返されると、それ以降の行は、カラム 1 から始まります

    ![WrappingIndent set to none](images/0_3_0/WrappingIndentNone.png)

* `same`: (This is the default.) 行が折り返されると、それ以降の行は、元の行と同じ位置から開始されます（これがデフォルトです。）

    ![WrappingIndent set to none](images/0_3_0/WrappingIndentSame.png)

* `indent`: 行が折り返されると、それ以降の行は、元の行からインデントされた位置から開始されます

    ![WrappingIndent set to indent](images/0_3_0/WrappingIndentIndent.png)

## Debugging

`launch.conf` では、`runtimeArgs` 属性を使用できます。Node.js または Mono にコマンドライン引数を渡す必要がある場合に便利です。(プログラムのデバッグ開始されないように)
Linux上でデバッグセッションを開始すると、入力/出力をサポートするためにターミナルを開きます。

TypeScript のデバッグにおいて、JavaScript のソースマップをサポートしました。 `launch.conf` の中で、`sourceMaps` アトリビュートを `true` に設定することで有効化されます。
さらに、`program` アトリビュートにソースマップを生成する TypeScript ファイルを指定できます。
TypeScript ファイルのソースマップを生成するには、`--sourcemap` オプションを付加してコンパイルしてください。

デバッグは、フォルダを持たないワークスペースでもサポートされました。
例えば、,フォルダがアクティブでないときにデバッグできます。(**ファイル**、**フォルダを閉じる**、または、新規ウィンドウを選択)
フォルダレスデバッグモードになっている場合は、VS Code に紫色のステータスバーが表示されます。

例外が投げられると、左のステータスバーにブレークポイントが設定されコードラインが赤でマークされます。

![Debugging UI](images/0_3_0/DebugVisualization.png)

このリリースで行われたデバッグへの変更は下記のとおりです。

* すべての変数を折り畳むためのアイコンが、変数ツリーに追加されました
* 変数ツリーからクリップボードに変数の値をコピーすることが可能になりました
* プラットフォームにより、利用可能な環境変数が異なることに注意してください
* ラウンチセッションを開始するときに VS Code が、うっかり OS X 上の任意の端末を乗っ取ることは無くなりました。以前にデバッグに使用された端末だけが、新しいセッションのために再利用されます。
* ランタイムまたはプログラムに渡される引数には、スペースが含まれていてもデバッグ可能になりました
* `kbstyle(F9)` と `kbstyle(F11)` が再び効くようになりました
* UNC パスを使ってデバッグが可能になりました
* Mono または Node.js が動作していない場合、それを伝えるより良いエラーメッセージが提供されれるようになりました
* OSX と Linux 上で動作する Mono 上の F# のデバッグをサポートしました

## Tasks

3 つの新しい [**problem matcher**](https://code.visualstudio.com/docs/editor/tasks#_processing-task-output-with-problem-matchers) を定義しました:

* `$jshint-stylish`: jshint で検出された問題を、Stylish reporter で生成する
* `$eslint-compact`: eslint で検出された問題を、Compact reporter で生成する
* `$eslint-stylish`: eslint で検出された問題を、Stylish reporter で生成する

複数行に渡る **problem matcher** は、いくつかのリンティングツールからスタイリッシュな出力をキャプチャするためにタスクシステムに追加されました。[Tasks](/docs/editor/tasks.md) で例を見ることができます。

オペレーティング・システムごとあるいは明示的なタスクごとに一貫したグローバルプロパティを再定義できます。詳細については、 [operating specific values](/docs/editor/tasks.md#operating-system-specific-properties) と [task specific values](/docs/editor/tasks.md#task-specific-properties) を参照してください。

新しいプロパティ、`suppressTaskName` は、タスク・コマンドが実行されたときに、タスク名を引数に追加するかどうかを示すために、オペレーティング・システムごと、またはタスクごとにグローバルに指定できます。[Tasks](/docs/editor/tasks.md) の Appendix を参照してください。

## Languages

### Rust

[Rust](http://www.rust-lang.org/) をサポート言語として追加しました。構文のカラー化とブラケットマッチングをサポートします。

### TypeScript

TypeScript 言語サービスは、TypeScript バージョン 1.5 にアップデートされました。

### JavaScript

もし、VS Code の JavaScript バリデータではなく JSHint などを利用したい場合は、下記の新しいオプションを使用することで、すべてのセマンティックと構文チェックをオフにできます。

* `javascript.validate.semanticValidation=[true|false]` VS Code にセマンティック・エラーを報告させるには `true` を使用してください（割り当てられていない変数などやその他。また、*すべての*リントチェック）
* `javascript.validate.syntaxValidation=[true|false]` VS Code にシンタックス・エラーを報告させるには `true` を使用してください (ブラケットのミスマッチなど)

### HTML

HTML tag の自動クローズ機能は削除され、IntelliSense の `</` に置き換えられました。

## CJK wrapping: 

中日韓（CJK）文字幅のより良い近似を得るために、ハーフ幅 **m** とフル幅 **m** を測定しています。
この結果により、CJK 文字を含むテキスト行は等幅フォントで表示され、オーバーフローによる水平スクロールバーを表示しません。

![Chinese text](images/0_3_0/ChineseLoremIpsum.png)

## File Compare

**File Compare** は現在、**Working Files** 内のファイルに適用されます。
新しいグローバルアクション **Files: Compare Opened File With** がコマンドパレットに追加されました。

![File Compare](images/0_3_0/compare.png)

## Copy Path
## パスのコピー

エクスプローラで任意のファイルまたはフォルダのパスをコピーすることが可能になりました。
右クリックでコンテキストメニューを表示し、**Copy Path** を選択します。

![Copy Path](images/0_3_0/CopyPath.gif)

コマンドパレットから実行可能な新しいグローバル・アクション **Files: Copy Path of the Active File** コマンドを追加しました。

![Palette Copy Path](images/0_3_0/CopyPathPalette.png)

## Close Folder
## フォルダを閉じる

新しいメニュー項目である **`ファイル | フォルダを閉じる`** は、現在アクティブなフォルダを閉じ、未保存の空の状態のファイルが 1 つオープンされた状態にワークスペースを構成し直します。
（あなたが自動保存を有効にしていない場合は、それが閉じられる前に、アクティブなフォルダ内の保留中の変更を保存するよう求められます。）

## File Encoding
## ファイルエンコーディング

**User Settings** または **Workspace Settings** の **files.encoding** 設定で、グローバルまたはワークスペース毎にファイルのエンコーディングを設定可能です。

![files.encoding setting](images/0_3_0/FilesEncodingSetting.png)

ステータスバーでファイルのエンコーディング設定を確認することが可能です。

![Encoding in status bar](images/0_3_0/FileEncoding.png)

ステータスバーに表示されるエンコーディング名をクリックすることで、アクティブなファイルのエンコーディングを変更し再オープンまたは保存することが可能です。

![Reopen or save with a different encoding](images/0_3_0/EncodingClicked.png)

どちらかを選択し、エンコーディングを決定します。

![Select an encoding](images/0_3_0/EncodingSelection.png)

## Settings
## 設定

JSON パーサーは、構文エラーなどがあっても動作し続けます。
たとえば、**settings.json** の末尾にカンマがある場合、これはエラーとして判断され適用されませんが、問題があることの通知も行われません。
VS Code は、カスタマイズにおける JSON 構文エラーを、視覚的なインジケータで通知するようになりました。
この例では、最後のブラケットに赤い波線ライン、および右端 5 行目の部分に赤いボックスが表示されています。

![JSON settings errors](images/0_3_0/settingserrors.png)

## UNC paths supported
このリリースから、UNC (Universal Naming Convention)パス を介して、Windows 上のファイルとフォルダにアクセスすることが可能になりました。

## Working files watched

**開いているフォルダ** 内に存在しないファイルも、**Working Files** 内部で変更を監視しているためファイルが変更されたタイミングでに更新されます。

## Linux 32-bit

Linux で 32 ビット・バイナリが利用できるようになりました。 ([download](http://go.microsoft.com/fwlink/?LinkID=615206))

## Other significant bug changes
また、以下の項目を修正しました。

* [16481](https://code.visualstudio.com/issues/Detail/16481): Opening files from a UNC folder
* [16457](https://code.visualstudio.com/issues/Detail/16457): Chinese characters not properly rendered on Linux
* [16574](https://code.visualstudio.com/issues/Detail/16574): Encoding issues
* [16500](https://code.visualstudio.com/issues/Detail/16500): $scope auto completes to $$scope
* [16514](https://code.visualstudio.com/issues/Detail/16514): HTML tags are incorrectly auto completed
* [16573](https://code.visualstudio.com/issues/Detail/16573): "CFBundleIdentifier" of "Visual Studio Code.app" should be changed from "com.github.atom-shell" to another unique identifier.

現在知られている問題のリストについては、[FAQ](/docs/supporting/faq.md) を参照してください。問題について参照したり、[ここ](/issues) で新たに報告できます。
