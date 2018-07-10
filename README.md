# Promise_practice
自分自身用のPromiseオブジェクトの備忘録として、様々な資料を参考に作成。

## Promiseとは
- 非同期の処理を分かりやすく制御するオブジェクト

## Promiseの使い方
- Promiseはnewして使用する。
- Promiseオブジェクトの第1引数は必ず関数(resolve,reject:省略形でも可(res,rej))
  - 第1引数の関数は成功の処理と失敗の処理を実行する引数（関数：引数として与えられた関数）を取得することができる。
  - 成功時　-> resolve(引数(関数))
  - 失敗時　-> reject(引数(関数))
  
- newされたPromiseは関数を持つオブジェクトを返す
 - `then(onFulfilled,onRejected),catch(onRejected)`
 - thenでresolveされた処理、catchでrejectされた処理を受け取る
 - catchを使用し失敗の処理を記述する。
 
 ### sample code
 ```js
 new Promise((res,rej) => {
  setTimeout(() => {
    resolve('こんにちは');
  },1000);
 })
 .then((result) => {
  console.log(result);
 })
 .catch((error) => {
  console.log(error);
 })
 ```
 - 最初の関数の
 


#### 参考資料
- [Promise再入門① Promise基本編](https://qiita.com/gcfuji/items/1dfe4265c36bea903ab3)
- [Promiseとasync/awaitを始めからていねいに](https://qiita.com/nabepon/items/1be1e83b0d17ee4f42a9)
