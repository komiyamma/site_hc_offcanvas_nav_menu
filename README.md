HC Off-canvas Nav
===============

[![Version](https://img.shields.io/npm/v/hc-offcanvas-nav.svg)](https://www.npmjs.com/package/hc-offcanvas-nav) [![Downloads](https://img.shields.io/npm/dt/hc-offcanvas-nav.svg)](https://www.npmjs.com/package/hc-offcanvas-nav)

ARIAを使用した、オフキャンバスの多階層ナビゲーションを作成するためのJavaScriptライブラリです。依存関係はありませんが、jQueryプラグインとしても機能します。[デモ](https://somewebmedia.github.io/hc-offcanvas-nav/)

<img src="https://somewebmedia.github.io/hc-offcanvas-nav/hc-offcanvas-nav.png" width="440">

### 特徴
- 多階層メニューのサポート
- ナビゲーション要素の無限ネスト
- メニュー項目内のカスタムコンテンツ
- 選択したDOM要素のプッシュ/スライド
- タッチスワイプジェスチャー
- さまざまなナビゲーション位置
- 依存関係なし
- 柔軟でシンプルなマークアップ
- 公開されている多数の[オプション](#options)、[メソッド](#methods)、[イベント](#events)
- 2つの[テーマ](#themes)
- クロスブラウザ互換性
- 完全なARIAキーボードサポート
  - <a href="https://www.w3.org/TR/wai-aria-practices/#dialog_modal">ダイアログの<abbr title="Accessible Rich Internet Application">ARIA</abbr>デザインパターン</a>に基づいています
  - Tabキーでオフキャンバスナビゲーション内のすべてのフォーカス可能な項目をループします
  - <kbd>Esc</kbd>キーで閉じることができます

## クイックスタート

### インストール

このパッケージは下記の方法でインストールできます:

- [npm](https://www.npmjs.com/package/hc-offcanvas-nav): `npm install --save hc-offcanvas-nav`

または、[最新リリース](https://github.com/somewebmedia/hc-offcanvas-nav/tags)をダウンロードしてください。

### HC Off-canvas Navの読み込み

#### scriptタグとcssタグ
```html
<link rel="stylesheet" href="/path/to/hc-offcanvas-nav.css">

<script src="/path/to/hc-offcanvas-nav.js"></script>
```

#### Webpack/Browserify

スクリプト内でHC Off-canvas Navを読み込むには、通常このようになります:

```js
const hcOffcanvasNav = require('hc-offcanvas-nav');
```

#### Babel

```js
import hcOffcanvasNav from 'hc-offcanvas-nav';
```

#### AMD (Asynchronous Module Definition)

AMDを使用している場合、モジュールは自動的に`hcOffcanvasNav`として定義されます。

#### SCSS

```scss
@import 'hc-offcanvas-nav/src/scss/core';
@import 'hc-offcanvas-nav/src/scss/toggle';
@import 'hc-offcanvas-nav/src/scss/theme-default';
```

## 使い方

メニュー要素がDOMで利用可能になったら、Navを呼び出すようにしてください。

#### Vanilla JS

```js
document.addEventListener('DOMContentLoaded', function() {

  var Nav = new hcOffcanvasNav('#main-nav', {
    disableAt: 1024,
    customToggle: '.toggle',
    navTitle: 'All Categories',
    levelTitles: true,
    levelTitleAsBack: true
  });

});
```

#### jQuery

```js
jQuery(document).ready(function($) {

  $('#main-nav').hcOffcanvasNav({
    disableAt: 1024,
    customToggle: $('.toggle'),
    navTitle: 'All Categories',
    levelTitles: true,
    levelTitleAsBack: true
  });

});
```

HC Off-canvas NavをjQueryプラグインとして動作させるには、jQueryがグローバルな`window`オブジェクトのプロパティである必要があります。Babel/Webpack/BrowserifyとjQueryを組み合わせて使用する場合は注意してください。

#### HTMLメニュー構造の例

```html
<nav id="main-nav">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li>
      <a href="#">Services</a>
      <ul>
        <li>
          <a href="#">Hosting</a>
          <ul>
            <li><a href="#">Private Server</a></li>
            <li><a href="#">Managed Hosting</a></li>
          </ul>
        </li>
        <li><a href="#">Domains</a></li>
        <li><a href="#">Websites</a></li>
      </ul>
    </li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

## テーマ

HC Off-canvas Navには現在、デフォルトとCarbonの2つのテーマがあります。Carbonテーマを使用するには、デフォルトのCSSの代わりにCarbonテーマのCSSを呼び出します:

```html
<link rel="stylesheet" href="/path/to/hc-offcanvas-nav.carbon.css">
```

`src`ディレクトリからSCSSをコンパイルする場合は、そこから`@include`します:

```scss
@import 'hc-offcanvas-nav/src/scss/core';
@import 'hc-offcanvas-nav/src/scss/toggle';
@import 'hc-offcanvas-nav/src/scss/theme-carbon';
```

## オプション

| プロパティ | デフォルト | 型 | 説明 |
|---|---|---|---|
| **width** | `280` | int / str | ナビゲーションの幅。`left`と`right`の位置で使用されます。 |
| **height** | `'auto'` | int / str | ナビゲーションの高さ。`top`と`bottom`の位置で使用されます。 |
| **disableAt** | `false` | int / bool | この解像度以上でオフキャンバスメニューを非表示にし、元のメニューを表示します。 |
| **pushContent** | `null` | str / Element obj | ナビゲーションが開いたときにプッシュされるコンテンツ要素（文字列セレクタまたはHTML要素オブジェクト）。 |
| **expanded** | `false`| bool | メニューを展開モードで初期化します。コンテンツはプッシュされません。 |
| **position** | `'left'` | str | メニューが開く位置。利用可能なオプション: `'left'`, `'right'`, `'top'`, `'bottom'`。 |
| **swipeGestures** | `true`| bool | ネイティブアプリのような開閉スワイプジェスチャーを有効にします。`left`と`right`の位置でのみ機能します。 |
| **levelOpen** | `'overlap'` | str | サブメニューレベルのオープンエフェクト。利用可能なオプション: `'overlap'`, `'expand'`, `'none'`または`false`。 |
| **levelSpacing** | `40` | int | レベルがオーバーラップする場合、これはそれらの間の間隔です。展開または常に開いている場合、これはサブメニューのテキストインデントです。 |
| **levelTitles** | `true` | bool | サブメニューに親アイテム名であるタイトルを表示します。オーバーラップしたレベルでのみ機能します。 |
| **navTitle** | `null` | str / Element obj | メインナビゲーション（第1レベル）のタイトル。画像（ロゴ）のようなHTMLオブジェクトも可能です。 |
| **navClass** | `''` | str | カスタムナビゲーションクラス。 |
| **disableBody** | `true` | bool | ナビゲーションが開いているときにボディのスクロールを無効にします。 |
| **closeOpenLevels** | `true` | bool | ナビゲーションが閉じるときに、開いているすべてのサブレベルを閉じる必要があります。 |
| **closeActiveLevel** | `false` | bool | ナビゲーションが閉じるときに、最初にアクティブだったサブレベル（[`data-nav-active`](#data-attributes)を参照）をクリアする必要があります。 |
| **closeOnClick** | `true` | bool | リンクがクリックされたときにナビゲーションを閉じます。 |
| **closeOnEsc** | `true` | bool | <kbd>Esc</kbd>ボタンでナビゲーションを閉じます。 |
| **customToggle** | `null` | str / Element obj | カスタムナビゲーショントグル要素。 |
| **activeToggleClass** | `null` | str | カスタムのアクティブなトグルクラス。 |
| **insertClose** | `true` | bool / int | ナビゲーションの閉じるボタンを挿入します。リスト内のボタンの位置となる0から始まるインデックスを表す整数も使用できます。負の数もサポートされています。 |
| **insertBack** | `true` | bool / int | サブメニューに戻るボタンを挿入します。リスト内のボタンの位置となる0から始まるインデックスを表す整数も使用できます。負の数もサポートされています。オーバーラップしたレベルでのみ機能します。 |
| **labelClose** | `''` | str | 閉じるボタンのラベル。 |
| **labelBack** | `'Back'` | str | 戻るボタンのラベル。 |
| **levelTitleAsBack** | `true` | bool | レベルタイトルを戻るラベルとして使用します。 |
| **rtl** | `false` | bool | コンテンツの方向を右から左に設定します。 |
| **bodyInsert** | `'prepend'` | str | ナビゲーションをbodyの先頭に追加するか、末尾に追加するかを選択します。 |
| **keepClasses** | `true` | bool | 元のメニューとそのアイテムのクラスを保持するか除外するか。 |
| **removeOriginalNav** | `false` | bool | 元のメニューをDOMから削除します。ナビゲーションを更新する予定がある場合は使用しないでください！ |
| **ariaLabels** | `{...}` | obj | ARIA属性のラベル。HC Off-canvas Navを英語以外の言語で使用する場合は、すべてのプロパティを翻訳する必要があります。次のセクションを参照してください。 |

画面に表示されるテキストがない要素の`aria-label`属性のARIAラベル。

```js
ariaLabels: {
  open:     'メニューを開く',
  close:    'メニューを閉じる',
  submenu:  'サブメニュー'
}
```

## メソッド

HC Off-canvas Nav APIは、オフキャンバスを制御するためのいくつかのメソッドを提供し、すべてのアクティブなインスタンスで公開されています。

#### Vanilla JS

```js
var Nav = new hcOffcanvasNav();
```

#### jQuery

```js
var $nav = $('#main-nav').hcOffcanvasNav();
var Nav = $nav.data('hcOffcanvasNav');
```

### .getSettings()

現在の設定を返します。

```js
var currentSettings = Nav.getSettings();
```

### .isOpen()

ナビゲーションが開いているかどうかを確認し、booleanを返します。

```js
if (Nav.isOpen()) {
  // 何かをする
}
```

### .update(options, updateDOM)

指定された設定のみを新しいものに更新します。

```js
Nav.update({
  disableAt: 1024,
  navTitle: 'All pages'
});
```

ナビゲーションのDOMを更新します。空の設定オブジェクトを渡す必要はありません、メソッドは賢いです。元のナビゲーションが変更された場合に使用します。

```js
Nav.update(true);
```

設定とナビゲーションDOMの両方を更新します。元のナビゲーションが変更され、特定の設定も更新したい場合に使用します。

```js
Nav.update({
  disableAt: 1024,
  navTitle: 'All pages'
}, true);
```

### .open(level, index)

ナビゲーションが閉じている場合に開きます。

```js
Nav.open();
```

ナビゲーションを開き、特定のサブメニューも開きます。各レベルのサブメニューには、親メニューではなくそのレベルに相対的な独自のインデックスがあります。

```js
Nav.open(2, 1);
```
上記のコードは、以下の例の構造でネストされたメニューを開きます:

```html
<nav>
  <ul><!-- Level: 0 -->
    <li></li>
    <li>
      <ul><!-- Level: 1, Index 0 -->
        <li>
          <ul><!-- Level: 2, Index: 0 -->
            <li></li>
            <li></li>
          </ul>
        </li>
        <li>
          <ul><!-- Level: 2, Index: 1 -->
            <li></li>
            <li></li>
          </ul>
        </li>
      </ul>
    </li>
    <li></li>
    <li>
      <ul><!-- Level: 1, Index 1 -->
        <li>
          <ul><!-- Level: 2, Index: 2 -->
            <li></li>
            <li></li>
          </ul>
        </li>
        <li></li>
      </ul>
    </li>
  </ul>
</nav>
```

### .close()

ナビゲーションが開いている場合に閉じます。

```js
Nav.close();
```

### .toggle()

ナビゲーションを開閉（トグル）します。

```js
Nav.toggle();
```

### .on(eventName, cb)

ナビゲーションに[イベント](#events)リスナーをアタッチします。

```js
Nav.on('close', function() {
  // close時になにかする
});
```

### .off(eventName, cb)

ナビゲーションから[イベント](#events)リスナーを削除します。

```js
// 特定の関数を削除
Nav.off('close', onCloseFunction);

// すべてのイベントリスナーを削除
Nav.off('close');
```

## イベント

| イベント | 説明 |
|---|---|
| **open** | ナビゲーションが開かれた後に毎回トリガーされます。 |
| **open.level** | いずれかのレベルが開かれた後に毎回トリガーされます。 |
| **close** | ナビゲーションが閉じられた後に毎回トリガーされます。 |
| **close.once** | ナビゲーションが閉じられた後に一度だけトリガーされ、その後自身をデタッチします。 |
| **close.level** | いずれかのレベルが閉じられた後に毎回トリガーされます。 |
| **toggle** | ナビゲーションが開閉されるたびにトリガーされます。 |

すべてのイベントは、最初の引数としてEventオブジェクトを、2番目の引数としてプラグインのSettingsオブジェクトを返します。

- `open.level`と`close.level`は、新しく開かれたレベルとインデックスを`Event.data`プロパティで返します。
- `toggle`イベントは、アクションを`Event.data`プロパティで返します。

開閉イベントはナビゲーションのアニメーションが終了した後にトリガーされますが、トグルイベントは即座にトリガーされます。

例:

```js
// 閉じるたびにナビゲーションの開始位置を変更する
Nav.on('close', function(e, settings) {
  Nav.update({
    position: settings.position === 'left' ? 'right' : 'left'
  });
});

// 一度だけナビゲーションの開始位置を変更する
Nav.on('close.once', function(e, settings) {
  Nav.update({
    position: settings.position === 'left' ? 'right' : 'left'
  });
});

Nav.on('open.level', (e, settings) => {
  localStorage.setItem('NavLevel', e.data.currentLevel);
  localStorage.setItem('NavIndex', e.data.currentIndex);
});

Nav.on('close.level', (e, settings) => {
  localStorage.setItem('NavLevel', e.data.currentLevel);
  localStorage.setItem('NavIndex', e.data.currentIndex);
});

Nav.on('toggle', (e, settings) => {
  if (e.data.action == 'open') {
    // `open`アクションがトリガーされたときに何かをする
  }
});
```

## Data属性

| 属性 | 受け入れる値 | HTML要素 | 説明 |
|---|---|---|---|
| **data-nav-active** | | `<ul>`, `<li>` | 次回ナビゲーションが開くときに、指定されたサブメニュー（または親の`<li>`要素がこの属性を持つサブメニュー）を開きます。[`expanded`](#options)オプションと共に機能します。 |
| **data-nav-highlight** | | `<li>` | リストアイテムをハイライトします。 |
| **data-nav-custom-content** | | `<li>` | リストアイテムに添付されます。アイテムのコンテンツをそのまま複製します。 |
| **data-nav-close** | bool | `<a>` | アイテムのリンクに添付されます。クリック時にナビゲーションを閉じる必要があるかどうかをナビゲーションに伝えます。 |

```html
<nav id="main-nav">
  <ul>
    <li data-nav-custom-content>
      <div>Some custom content</div>
    </li>
    <li data-nav-highlight><a href="#">Home</a></li>
    <li data-nav-active>
      <a href="#">About</a>
      <ul data-nav-active><!-- またはactive属性はここにあってもよい -->
        <li><a href="#">Team</a></li>
        <li><a href="#">Project</a></li>
        <li><a href="#">Services</a></li>
      </ul>
    </li>
    <li><a href="#">Contact</a></li>
    <li><a data-nav-close="false" href="#">Add Page</a></li>
  </ul>
</nav>
```

### WordPressのdata属性統合

WordPressテーマのナビゲーションをデータ対応にしたい場合は、このコードを`functions.php`ファイルに配置するだけで、すぐに機能するはずです。**このカスタムWalkerを`wp_nav_menu`の引数に割り当てないでください！** また、すでに独自のカスタムWalkerを使用していても心配ありません。このコードがすべてを処理します。

```php
/*
 * HC Off-canvas Navのメニューデータサポートを追加します
 */

$hc_nav_menu_walker;

class HC_Walker_Nav_Menu extends Walker_Nav_Menu {

  public function start_lvl(&$output, $depth = 0, $args = array()) {
    global $hc_nav_menu_walker;
    $hc_nav_menu_walker->start_lvl($output, $depth, $args);
  }

  public function end_lvl(&$output, $depth = 0, $args = array()) {
    global $hc_nav_menu_walker;
    $hc_nav_menu_walker->end_lvl($output, $depth, $args);
  }

  public function start_el(&$output, $item, $depth = 0, $args = array(), $id = 0) {
    global $hc_nav_menu_walker;

    $item_output = '';

    $hc_nav_menu_walker->start_el($item_output, $item, $depth, $args, $id);

    if ($item->current_item_parent) {
      $item_output = preg_replace('/<li/', '<li data-nav-active', $item_output, 1);
    }

    if ($item->current) {
      $item_output = preg_replace('/<li/', '<li data-nav-highlight', $item_output, 1);
    }

    $output .= $item_output;
  }

  public function end_el(&$output, $item, $depth = 0, $args = array(), $id = 0) {
    global $hc_nav_menu_walker;
    $hc_nav_menu_walker->end_el($output, $item, $depth, $args, $id);
  }
}

add_filter('wp_nav_menu_args', function($args) {
  global $hc_nav_menu_walker;

  if (!empty($args['walker'])) {
    $hc_nav_menu_walker = $args['walker'];
  }
  else {
    $hc_nav_menu_walker = new Walker_Nav_Menu();
  }

  $args['walker'] = new HC_Walker_Nav_Menu();

  return $args;
});
```

## 開発ビルド

このパッケージには[Gulp](https://gulpjs.com/)が付属しています。以下のタスクが利用可能です:

  * `default` JSとSCSSを`/dist`にコンパイルし、デモを`/docs`にビルドします。
  * `demo` `default`タスクを実行し、デモのhtmlページを開きます。
  * `watch` ソースのJSおよびSCSSファイルを監視し、保存するたびに自動的にビルドします。

コンパイルされたJSとCssを最小化したくない場合は、`--dev`コマンドを渡すことができます。

## ライセンス

コードとドキュメントはMITライセンスの下でリリースされています。
