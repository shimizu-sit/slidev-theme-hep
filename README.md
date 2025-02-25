# slidev-theme-hep

[![NPM version](https://img.shields.io/npm/v/slidev-theme-hep?color=3AB9D4&label=)](https://github.com/AvencastF/slidev-theme-hep/pkgs/npm/slidev-theme-hep)

 [Slidev](https://github.com/slidevjs/slidev)用のHigh Energy Physics(HEP)の学術テーマである. 

## ❤️‍🔥 Demo

HEPテーマのデモページ

### [link](https://avencastf.github.io/slidev-theme-hep/)



## 🛠 Install

`slides.md`に以下のfromtmatterを追加する．Slidevを起動すると，テーマを自動的にインストールするよう促される．

```
theme: hep
```

テーマの使い方についてもっと知りたい場合： [how to use a theme](https://sli.dev/guide/theme-addon#use-theme).

## 💼 Layouts

このテーマに以下のレイアウトがある．

### Cover

![sc-cover](screenshot/001.png)

| **Parameter** |    **Type**     |            **Default**            |       **Notes**        |
| ------------- | --------------- | --------------------------------- | ---------------------- |
| `background`  | `string`        | `'ATLAS/ATLAS-Detector.png'`      |                        |
| `authors`     | `名前: [所属];` | `{}`                              | 以下の例を参照         |
| `meeting`     | `string`        | `''` (空白)                       | プレゼンテーマ         |
| `preTitle`    | `string`        | `'An Example Title'`              | プレゼンタイトル       |
| `preDate`     | `string`        | `new Date().toLocaleDateString()` | 自動で現在の日付になる |

`authors` : 著者と対応する所属は以下のように設定できる

```yaml
authors:  # 筆頭著者は発表者である前提，かつ，アンダーラインがつく
  - First Author: ["Institution 1", "Institution 2"] 
  - Second Author: ["Institution 3"]
  - Third Author: ["Institution 1", "Institution 3"] 
```
<span style="color: red;">**筆頭著者が発表者であることが前提であることに留意すること** </span>

---

### pageBar

![sc-cover](screenshot/002.png)

このレイアウトは，ページの下に**ボトムバー**とタイトルの左側に**装飾ボックス**を配置したレイアウトである．プレゼンテーション全体に一貫してスライド情報を表示するための構造的なアプローチを与えようとしています．このレイアウトの主要部分は次のとおりです．

- **Title Bar at Bottom**：スライドの下部には，以下の情報を含む水平のバー(`BarBottom`というコンポーネント)がある
  - タイトル(`title`)：コンフィギュレーションから取得したプレゼンテーションのタイトルを表示する
  - 著者名(`author`)：コンフィギュレーションで定義された著者のリストから最初の著者（筆頭著者）の名前を表示する
  - ミーティングまたはイベント名(`meeting`)：これもコンフィギュレーション設定から取得する
- **Page Number**：右下には自動スライド番号インジケータを表示する



---

## 🗿 Components

このテーマには以下のコンポーネントがある．

### `TextBox`

Text Boxコンポーネントは，スタイル付きコンテナ内にテキストコンテンツを表示するように設計された柔軟なVueコンポーネントである．
このコンポーネントは親コンポーネント内に絶対的に配置され，さまざまなスタイルや「info」や「warning」などのラベルでカスタマイズできる．
テキストコンテンツは，読みやすくするために改行文字をHTMLの改行に自動変換する機能をサポートしている．

#### Props

このコンポーネントは以下のプロップを受け付ける

|      Prop      |  Type  |                          Default                           |                     Description                     |
| -------------- | ------ | ---------------------------------------------------------- | --------------------------------------------------- |
| `text`         | String | None                                                       | テキストボックス内に表示するテキスト内容            |
| `position`     | Object | `{ top: '0px', left: '0px', right: '0px', bottom: '0px' }` | 親テキストボックス内のテキストボックスの絶対位置    |
| `customStyles` | Object | None                                                       | テキストボックスコンテナ用の追加カスタムCSSスタイル |
| `label`        | String | `'info'`                                                   | テキストコンテンツのスタイルを決定するラベル        |

#### Styling

このコンポーネントには，以下のの定義済みクラスを持つCSSがスコープされている


|      Class Name      |                      Description                       |                                    Style Properties                                    |
| -------------------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| `text-box-container` | テキストボックのコンテナで中央揃え，フレックスアライン | `display: flex; flex-direction: column; justify-content: center; align-items: center;` |
| `text-content`       | テキストボックスの内容                                 | `padding: 0.5rem;`                                                                     |
| `warning`            | 警告ラベルのスタイル                                   | `background-color: #ffcc00; color: red;`                                               |
| `info`               | 情報ラベルのスタイル                                   | `background-color: transparent; color: #0FA3B1; font-weight: 550; font-size: 1.5em;`   |

`customStyles`プロップは，これらのプリセットクラスを超えてさらにカスタマイズすることがｄけいる．ユーザは，`.text-box-container`に適用したい任意のCSSプロパティを持つオブジェクトを渡すことができる．

使用例:

```html
<Text-Box
  text="This is an info message with\nmultiple lines."
  :position="{ top: '20px', left: '20px' }"
  label="info"
/>
<Text-Box
  text="This is a warning message!"
  :customStyles="{ fontSize: '1em', fontWeight: 'bold' }"
  label="warning"
/>
```

### `PlotlyGraph`

The `PlotlyGraph` component is a Vue wrapper for Plotly.js, allowing for easy embedding and manipulation of Plotly graphs within your Vue application. The component accepts various props to customize the graph's dimensions and font sizes.

#### Props

The component accepts the following props for configuration:

| Prop                      | Type   | Description                                                     |
| ------------------------- | ------ | --------------------------------------------------------------- |
| `filePath`                | String | The URL or path to the configuration file for the Plotly graph. |
| `graphWidth`              | Number | The width of the graph in pixels.                               |
| `graphHeight`             | Number | The height of the graph in pixels.                              |
| `xTitleFontSize`          | Number | The font size for the x-axis title.                             |
| `yTitleFontSize`          | Number | The font size for the y-axis title.                             |
| `tickFontSize`            | Number | The font size for the tick labels on both axes.                 |
| `annotationFontSizeScale` | Number | A scale factor to adjust the font size of annotations.          |

#### Usage

To use the `PlotlyGraph` component, you must provide the `filePath` prop with a valid URL or path to a Plotly configuration file. 
Other props are optional and allow you to customize the appearance of the graph.

**It's highly recommended to produce the JSON file for plotting by [Plotly](https://plotly.com/python/) in Python.**

#### Example

```html
<PlotlyGraph
  filePath="path/to/plotly/config.json"
  graphWidth="600"
  graphHeight="400"
  xTitleFontSize="14"
  yTitleFontSize="14"
  tickFontSize="12"
  annotationFontSizeScale="1.5"
/>
```

---


## Contributing

- `npm install`
- `npm run dev` to start theme preview of `example.md`
- Edit the `example.md` and style to see the changes
- `npm run export` to generate the preview PDF
- `npm run screenshot` to generate the preview PNG



[![Visitors](https://api.visitorbadge.io/api/combined?path=https%3A%2F%2Fgithub.com%2FAvencastF%2Fslidev-theme-hep&countColor=%23263759)](https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2FAvencastF%2Fslidev-theme-hep)
