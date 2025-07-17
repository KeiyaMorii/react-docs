## イベントリスナーについて
このドキュメントでは、Reactにおけるイベントリスナー（イベントハンドラー）の基本的な使い方、注意点、実際のコード例をまとめます。

目次
- イベントリスナーとは
- 基本的な使い方
- onClick属性の使い方
- 書き方の違いと挙動
- イベントリスナー設定時の注意点
- 補足：addEventListenerとの違い

### イベントリスナーとは
イベントリスナー（イベントハンドラー）とは、ユーザーの操作（クリック、キー入力など）に応じて実行される関数です。
Reactでは、DOM要素の属性（例: onClick）として関数を渡すことでイベントリスナーを登録します。

基本的な使い方
Reactコンポーネント内で関数を定義し、その関数をイベント属性に渡します。

```
import React from 'react';

const Example = () => {
  const clickHandler = () => {
    alert('ボタンがクリックされました。');
  };

  return (
    <button onClick={clickHandler}>クリックしてね</button>
  );
};

export default Example;
```

### onClick属性の使い方
正しい例
onClick には「関数の参照」を渡します。
```
<button onClick={clickHandler}>クリックしてね</button>
```

この場合、「クリックされた時」にclickHandlerが実行されます。

書き方の違いと挙動
以下のような違いに注意してください。

書き方	挙動
onClick={clickHandler}	クリック時にclickHandlerが実行される
onClick={clickHandler()}	レンダリング時に即実行（ボタンクリック時は何も起きない）
onClick={() => { clickHandler() }}	クリック時にclickHandlerが実行される
onClick={() => { clickHandler }}	何も起こらない（参照してるだけ）

解説
- onClick={clickHandler} : 関数の参照を渡す。推奨。
- onClick={clickHandler()} : 関数を即実行し、その戻り値を渡す。ほとんどの場合非推奨。
- onClick={() => { clickHandler() }} : 無名関数経由で実行。パラメータを渡したいときなどに便利。
- onClick={() => { clickHandler }} : 無名関数内で参照するだけで実行しない。何も起きないので注意。

### イベントリスナー設定時の注意点
- 関数の参照を渡す (onClick={handler}) のが基本。
- 関数を「即時実行」（onClick={handler()}）すると、レンダリング時に1回だけ実行される（クリック時ではない）。
- パラメータ付きで関数を実行したい場合は、無名関数を使う。

```
<button onClick={() => handler(param)}>クリック</button>
```
- 無名関数が必要以上に作られる場合はパフォーマンスに注意。

### 補足：addEventListenerとの違い
ReactではaddEventListenerを直接使わず、イベント属性（onClickなど）を使うのが一般的です。
- addEventListenerなど生のイベントリスナー操作は通常不要です。
- Reactは独自の「合成イベント（SyntheticEvent）」システムを使い、どのブラウザでも同様の動作を保証します。
- どうしても生のDOMにアクセスしたい場合はrefやuseEffectを使って制御します。