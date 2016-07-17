# AbemaTVを少しだけ見やすくするChrome拡張

## 概要
これはChromeでAbemaTVを視聴する際にCSSやjavascriptを追加して少しだけ視聴しやすくするものです。以下の機能があります。
- 上下の黒帯パネルを透明化
- コメント欄を透明化(見やすいようにコメントの文字は白抜き黒縁に)し一行表示
- コメント欄の新着ボタンを自動クリック(設定で中断可)、非表示
- 緑の吹き出し非表示
- コメント入力欄の外枠クリックでコメント一覧の表示/非表示の切替
- 画面右の番組移動ボタンの並びに(一時的な)設定ボタンが追加されます
- 番組表の番組ページから番組開始前通知を設定できます。何分前に通知するかも設定できます。(デフォルト1分前)
- (設定で有効)Chromeのウィンドウが横長のときに映像が上下切れることなくウィンドウサイズにフィットするように映像のサイズを変更(デフォルトの状態では映像サイズがウィンドウ幅に合わさって横長のウィンドウでは上下が見えなくなってしまいます。)
- (設定で有効)コメントを横に流す
- (設定で有効)現在正常に動作しません。→ダブルクリックでフルスクリーン&フルスクリーンボタンをF11と同等のフルスクリーンに割り当て(コメント欄を表示したままフルスクリーンにできます。)
- (設定で有効)音量、全画面表示ボタンを非表示
- (設定で有効)コメント入力欄を一行にし投稿ボタン等を非表示
- (設定で有効)コメント欄を非表示し入力欄を下へ
- (設定で有効)矢印キーとマウスホイールでチャンネル変更を無効にする、設定でマウスホイールを音量変更に割り当てられる
- (設定で有効)流れるコメントに規定のNG処理を適用する(詳細は後述)
- (設定で有効)流れるコメントにあなたが決めたNG単語(書式は後述)が含まれる場合は流さない
- (設定で有効)コメント入力欄の端に番組の残り時間とゲージ(設定ボタン)を表示する。ゲージは設定ボタンになっています。表示位置も変更できます。ゲージを非表示にする場合はonairpage.js内の"&amp;nbsp;"を""に変更してください。
- (設定で有効)コメント欄を常に表示したままにする。この機能利用中は、画面右下のボタンはコメント一覧の表示/非表示切替ボタンになっています。
- (設定で有効)上下黒帯パネルを常に表示したままにする。
- (設定で有効)映像を枠に合わせて縮小する。
- (設定で有効)番組時間、タイトルを表示
- (設定で有効)新着コメントを強調
- (設定で有効)番組表の改善(番組タイトルの表示調節、週末青赤着色、放送画面へのリンク設置)
- コメント欄の文字色や背景色や透過度など見た目を設定できます。
- 特定のときに画面を真っ黒にしたりミュートにする機能は設定画面から非表示にしました。

<!--
コメント数無効関連は非表示、オプション画面でuuddlrlrba  
仕様変更により挙動がやや不安定です。
- (設定で有効)コメント数無効時に画面真っ黒(下半分だけ透かすことも可)
- (設定で有効)コメント数無効時にミュート
-->

他の方の改造版を順次反映させています。  
manifest.json記載のバージョン番号は基本的にウェブストア版を更新するときに増え、そうでないときはそのままです。見やすさのため0.0.22の次から0.1.0になります。
AbemaTVの仕様変更や(もしかしたら各々の環境で)うまく動作しなくなる可能性があります。  
ちょっとしたスクリプト・CSSですので自由に改造してみてください。また大したことないものですのでパブリックドメインみたいに自由に使用・改変・転載してください。(煮るなり焼くなり公式に取り入れるなり自由に)  
Linux上のChromiumで確認しながら実装しています。

### 規定のNG処理について
過度な期待は禁物
- (´･ω･｀)などの顔文字は可能な限り除去（不完全です）←このようなカッコを除去せず残すため
- twitterの#ハッシュタグや@宛先のようなものは除去
- ttp://URLは除去.net
- 同同同じ文字の繰り返しは3文字に短縮
- 同じ単語の繰り返しは2回に短縮短縮
- その他、改行や伸ば～～～し棒などに規定の処理があります。onairpage.js内の関数comeNGを参照。

### 自由入力欄の書式について
- 全ての行を1行ずつ処理していきます。改行は単語の区切りとなります。
- 通常の単語はそのまま記述してください。💦などの絵文字も扱えるはず。
- /(a|b|c)/iのように半角スラッシュで挟むと、正規表現として処理しようとします。
- /(a|b|c/igiのように正規表現に失敗すると、通常の単語として扱います。
- 行頭または文中の半角スラッシュ2回//以降の文字列はコメントとして扱います。/&#042;この形式&#042;/は現在非対応

## インストール方法
Chromeウェブストアに公開しました。[_bem_tv ext](https://chrome.google.com/webstore/detail/bemtv-ext/jgbkfdjdcbohgenpccfgldadaofnfknl?hl=ja&gl=JP) からインストールできます。インストール後、拡張機能のオプション画面で必要な機能を有効にしてください。

デベロッパーモードから導入する場合  
- ファイル一式をダウンロードする
- Chromeのその他のツール→拡張機能を開く
- 右上のデベロッパーモードをチェックする
- 「パッケージ化されていない拡張機能を読み込む」をクリックしこのファイルのあるディレクトリを選ぶ
- 拡張機能のオプション画面で必要な機能を有効にする

注：拡張機能が機能していないようであればAbemaTVを再読み込みしてください。また、危害を与える恐れがある云々とデベロッパーモードに関する警告が出ることがあります。(この拡張機能を信頼して使用する場合はキャンセルを押せばOKです)  
Firefox対応のため、拡張機能を読み込んだときにオレンジのエラーが出ます。気にしないでください。

放送画面右の設定ボタン、または番組残り時間をクリックすると設定ウィンドウが表示されますが、
このウィンドウでの設定は一時的なものであり、他のタブには反映されないし、このタブを閉じると全て破棄されます。
自由入力欄のNG単語なども失われますのでご注意ください。
永続的な設定はChromeの拡張機能のオプション画面でのみ行います。

## Firefox対応
Firefoxへの対応を目指して実験的にfirefoxでも読み込めるようにしています。そのためWebExtensionに対応したfirefoxでも一応使用できます。  
Firefoxではオプション画面へのアクセス手段がないのでAbemaTVのページの黒帯右上のその他のメニューか一時設定画面にあるリンクからオプション画面を開いてください。  
この拡張機能はChrome前提で作られているのでFirefoxではうまく動かない可能性が大きいです。コメント流しなど主要な機能を簡単に確認しただけなのでバグが多いと思われます。  
Firefox版は署名済みのものが[このページ](https://www.nakayuki.net/abema-ext/)からダウンロードできます。WebExtension非対応のFirefoxでは壊れたアドオンとみなされるので注意してください。Mozillaの公式アドオンサイトには審査に時間がかかるので掲載しない予定です。  
firefoxで読み込む際は元からあるChrome用のmanigest.jsonは使用せず、manifest-fx.jsonをmanifest.jsonにリネームして使用してください。  
firefoxでabout:debuggingを開けば一時的に拡張機能を読み込むことができます。(このフォルダの(↑でリネームした)manifest.jsonを選択)firefoxを起動している間だけ使用できます。(一旦閉じると拡張が消えてしまいます。)  
Firefox Developer Edition と Firefox Nightlyでは野良拡張の読み込みも可能です。about:configを開きxpinstall.signatures.requiredをfalseに設定の上で、manifest.jsonをfirefox用のに置き換えた上でこの拡張機能のファイル一式をzipで固め、拡張子を.xpiに変更しアドオンページからインストールできます。

## アップデート方法
ウェブストアから入れた場合はある程度更新がまとまったらウェブストア版も更新されますが、ウェブストアに最新版が公開されてから手元の拡張機能が最新になるまで時間がかかります。その場合は、Chromeの拡張機能の画面でデベロッパーモードにして「拡張機能を今すぐ更新」をクリックすればすぐ最新版になります。
デベロッパーモードからインストールした場合、既存の拡張機能を削除して入れ直すか、既存のフォルダ内を全部新版に置き換えて拡張機能の再読み込みをしてください。

## 更新履歴
Githubに公開以降はコミット履歴が残るので、原則としてこの更新履歴は更新しません。  
04/23 - 初版公開  
04/25 - abematv側の仕様変更で使えなくなったので修正、映像サイズ変更をデフォルト無効、jQueryを使用  
04/27 - 他の方の改造版の機能も含め機能追加、オプション設定画面追加  
04/27 - 整理してgithubへ  
05/03 - NG処理など追加  
05/08 - 一部機能を設定画面から非表示に  
05/09 - Chromeウェブストア公開

## 開発
この拡張機能の開発は2ch.netのAbemaTVスレで複数人で行っています。開発に参加したい方は気軽にプルリクエストか当該スレに上げるかしてください。順次ここにマージしていきます。

Chromeウェブストアへ公開しました。(デベロッパーモードからの読み込みだと自動アップデートができず警告がでることがあるため)
正規な視聴をより快適にする目的でDOM操作とCSSの追加をしているだけですので大目に見てください。
データや映像の取得やその手助けするような機能はいっさいありません。
もし何か問題がありましたら2ch.netのAbemaTVスレッドまでお願いします。
