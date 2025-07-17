## useState フックについて
### 概要
useState は、React の関数コンポーネントで状態（state）を管理するためのフックです。
「状態」とは、ユーザーの入力、API の取得結果、UI の動的変化など、コンポーネントの再描画に影響を与える値のことです。

基本構文
```
const [state, setState] = useState(初期値);
```
- state：現在の状態の値
- setState：状態を更新する関数
- useState(初期値)：状態の初期値を指定

サンプル
入力フォームの値を状態として管理する例
```
import { useState } from "react";

const Example = () => {
  const [value, setValue] = useState(""); // 初期値は空文字

  return (
    <>
      <input
        type="text"
        value={value}
        onChange={e => setValue(e.target.value)}
      />
      <p>入力値：{value}</p>
    </>
  );
};

export default Example;
```

数値をカウントする例
```
import { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0); // 初期値は0

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <span>{count}</span>
    </div>
  );
};

export default Counter;
```

### 詳細解説
1. 状態の更新で再描画
setState を呼ぶと、そのコンポーネントが再描画され、最新の状態値が UI に反映されます。

2. useState の戻り値
useState は配列 [状態, 更新関数] を返すため、分割代入で使うのが一般的です。

3. 初期値について
初期値は number, string, null, undefined, object, array など何でもOKです。

初期値はコンポーネントの初回レンダリング時のみ1度だけ使われます。

4. 関数型更新
新しい状態が前の状態に依存する場合、下記のように関数を渡せます。
```
setCount(prevCount => prevCount + 1);
```

5. 注意点
- 状態の変更は非同期で行われることがあります。変更直後に state を参照すると、以前の値が返る場合があります。
- 状態に直接代入はしないでください。[NG例] count = 2;
- 必ずsetCount(2)のように更新関数で変更しましょう。