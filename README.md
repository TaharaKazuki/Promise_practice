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
 
 ### sample code
 ```js
 new Promise((resolve,reject) => {
  setTimeout(() => {
    resolve('こんにちは');①
  },1000);
 })
 .then((result) => {②
  console.log(result);　// こんにちは
 })
 .catch((error) => {
  console.log(error);
 })
 ```
 or 以下の様に変数に入れてもOK
 ```js
 
 const promise = new Promise((resolve, reject)=> {
  setTimeout(()=> {
    resolve('こんにちは');
  })
 });
 
 promise
  .then((result)=> {
    console.log(result); // こんにちは
  })
  .catch((error)=> {
    console.log(error);
  });
 
 ```
 【sample code説明】
 1. 最初の関数の中で、resolve①を実行すると、②thenの関数に処理が進む。
 1. resolveに渡した引数（ここでいうと'こんにちは'）がthenの引数として渡る。
 1. 処理のどこかでerror（rejectが呼ばれる）が起きた場合はthenではなくcatchの関数に処理が進む。

## Promiseでの直列処理

```js 
const function_1 = (num) => {
  return new Promise((resolve)=> {
    setTimeout(()=> {
      resolve(num);
    },3000)
  });
}

const function_2 = (num) => { //　②
  return new Promise((resolve)=> {
    setTimeout(()=> {
      resolve(num + num);// ③
    },1000)
  });
}

function_1(3)
  .then(function_2) //　①
  .then((result)=> {　// ③
    console.log(result);　//　6
  })
  .catch((error)=> {
    console.log(error);
  });
```
1. thenの中でPromiseを返せば、続けてthenを記載することが可能
1. `function_1`の非同期処理の完了後、１つ目のthenに移る。
1. １つ目のthenの中で`function_2`がコールバックで呼ばれる。
1.　`function_2`の非同期が行われ、resolveから２つ目のthenが呼ばれ、結果としてresultの結果に反映される。
1. `function_1`が終われば`function_2`が動くというような直列（同期）的な処理となる。

## Promiseでの並列処理

```js
const promise1 = new Promise(( resolve, reject ) => {
  setTimeout(() => {resolve( "1秒経過" )},1000);
});

const promise2 = new Promise(( resolve, reject ) => {
	setTimeout(() => {resolve( "2秒経過" )},2000);
});

const promise3 = new Promise(( resolve, reject ) => {
  setTimeout(() => {resolve( "3秒経過" )},3000);
});

Promise.all([
  promise1,
  promise2,
  promise3
]).then((result)=>{
  console.log(result[1]);
});

```


#### 参考資料
- [Promise再入門① Promise基本編](https://qiita.com/gcfuji/items/1dfe4265c36bea903ab3)
- [Promiseとasync/awaitを始めからていねいに](https://qiita.com/nabepon/items/1be1e83b0d17ee4f42a9)
