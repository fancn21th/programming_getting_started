# 第一天

什么是代码的执行顺序

## 第一个命令

```shell
  console.log // 打印到控制台
```

## 第一个流程顺序执行

```shell
  console.log("1");
  console.log("2");
  console.log("3");
```

## 什么是方法 (不得已的补充知识点)

```javascript
  // 顺序执行
  console.log("1");
  console.log("2");

  // 重复一次
  console.log("1");
  console.log("2");
  console.log("1");
  console.log("2");

  // 更简单的做法
  function oneTwo() {
    console.log("1");
    console.log("2");
  }

  oneTwo();
  oneTwo();
```

## 好复杂哦 下面代码执行顺序是什么?

你可以借助 `debugger` 工具来 一步步执行, 请关注 黄色背景的 区域变化 尤其是 代码行数的变化

也请你注意控制台里面 红色的信息和普通颜色的信息的区别

```javascript
  // 往 页面上输出内容
  function hello() {
    const div1 = document.createElement("div");
    document.body.appendChild(div1);
    div1.innerText = `hello world again`;
  }

  // 往 控制台输出内容
  function longtimeTask() {
    // 长时间任务
    const t0 = performance.now(); // 計時開始
    let count = 10000;
    for (let i = 0; i < count; i++) {
      console.log("hello world");
    }
    const t1 = performance.now(); // 計時結束
    console.log(
      ` ${count} console.log("Hello World"); 花费了 ${t1 - t0} 毫秒.`
    );
  }

  // 执行一个长时间的任务
  longtimeTask();
  // 往页面上写一段文字

  // 顺序执行
  hello();

  // 执行一个长时间的任务
  setTimeout(() => {
    longtimeTask();
  }, 0);

  // 插队成功!
  (async function () {
    hello();
  })();
```

## 超级补充知识

什么是微任务 和 宏任务

### 比喻的强大力量

- 第一, 什么是任务, 任务就是做一件事
- 第二, 什么是任务的优先级, 简单来说就是可以插队, 想一想迪士尼的 `fastpass`. 你有了 `fastpass` 就可以插队了

```javascript
  // 宏任务 排大队 长长的队 大概要2个小时才能进门
  setTimeout(() => {
    console.log("setTimeout");
  }, 0);

  // 微任务 排小队 短短的队 一会就进门了 好邪恶
  Promise.resolve().then(() => {
    console.log("Promise");
  });
```

## 总结

- 概念
  - 代码执行的顺序 不要去猜, 去看 控制台的输出和调试的步骤 , 也就是黄色背景和对应的代码行数
  - 写在靠后的代码, 并不一定靠后执行
  - 为什么 后写的代码要先执行? 请你思考?
  - 什么是  I/O

- 工具
  - chrome
    谷歌浏览器
  - vscode
    代码编辑器
  - debugger
    调试工具
  - function
    方法
  - console.log / console.error
    打印到控制台
  - performance.now
    计算时间
  - document
    输出到页面
