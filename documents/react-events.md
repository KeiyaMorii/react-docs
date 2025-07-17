## React主要イベントまとめ
このドキュメントでは、代表的なReactのイベントハンドラ（onChange, onBlur, onFocus, onMouseEnter, onMouseLeave）の使い方と挙動を解説します。

サンプルコード
```
import "./Example.css";

const Example = () => {
  return (
    <div>
      <h3>コンソールを確認してください。</h3>
      <label>
        入力値のイベント：
        <input
          type="text"
          onChange={() => console.log("onChange検知")}
          onBlur={() => console.log("onBlur検知")}
          onFocus={() => console.log("onFocus検知")}
        />
      </label>
      <div>
        <label>
          入力値を取得：
          <input type="text" onChange={(e) => console.log(e.target.value)} />
        </label>
      </div>
      <div
        className="hover-event"
        onMouseEnter={() => console.log("カーソルが入ってきました。")}
        onMouseLeave={() => console.log("カーソルが出ていきました。")}
      >
        ホバーしてね！
      </div>
    </div>
  );
};

export default Example;
```

### 各イベントの解説
onChange
- 用途
フォーム部品（input, textareaなど）の値が変更された際に都度発火します。
- Reactでは
DOMのoninputイベントと同じタイミングで発火します。
JavaScriptのonchange（フォーカスが外れた時発火）とは違うので注意してください。

例
```
<input
  type="text"
  onChange={() => console.log("onChange検知")}
/>
```
- 入力値の取得
```
<input
  type="text"
  onChange={(e) => console.log(e.target.value)}
/>
```
onBlur
- 用途
入力欄からフォーカスが外れた時に発火します（入力確定時の処理などに利用）。

例
```
<input
  type="text"
  onBlur={() => console.log("onBlur検知")}
/>
```
onFocus
- 用途
入力欄にフォーカス（カーソルやタブ移動で選択）した時に発火します。

例
```
<input
  type="text"
  onFocus={() => console.log("onFocus検知")}
/>
```
onMouseEnter / onMouseLeave
- 用途
マウスカーソルが要素に入った時（onMouseEnter）、離れた時（onMouseLeave）に発火します。

例
```
<div
  onMouseEnter={() => console.log("カーソルが入ってきました。")}
  onMouseLeave={() => console.log("カーソルが出ていきました。")}
>
  ホバーしてね！
</div>
```

### 補足
- イベントハンドラのコールバックは引数としてeventオブジェクト（例：e）を受け取り、e.target.valueで入力値などにアクセスできます。
- イベントごとに発火タイミングが異なりますので、用途・目的ごとに使い分けてください。

### 参考リンク
- React公式: Handling Events
- MDN: 入力フォームのイベント