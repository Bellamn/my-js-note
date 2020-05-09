# asynchronous

## 微任务和宏任务
+ 首先需要搞清楚JS中是单线程的，并且执行的优先级是同步大于异步，并且是所有同步执行完后才回来执行异步操作异步操作中又分为微任务（promise等）和宏任务（setTimeOut、I/O操作等）。顾名思义，微任务是具体的点，而宏任务是大的一个块儿。
微任务和宏任务的执行顺序为前者优先

    ```javascript
    new Promise((resolve) => {
    console.log('1')
    resolve()
    console.log('2')
    }).then(() => {
    console.log('3')
    })
    setTimeout(() => {
    console.log('4')
    })
    console.log('5')

    // 输出结果 1 2 5 3 4
    ```
## Event loot 机制

+ 同步和异步任务分别进入不同的执行环境，同步的进入主线程，即主执行栈，异步的进入 Event Queue 。主线程内的任务执行完毕为空，会去 Event Queue 读取对应的任务，推入主线程执行。 上述过程的不断重复就是我们说的 Event Loop (事件循环)。
在事件循环中，每进行一次循环操作称为tick，通过阅读规范可知，每一次 tick 的任务处理模型是比较复杂的，其关键的步骤可以总结如下：
1. 在此次 tick 中选择最先进入队列的任务( oldest task )，如果有则执行(一次)
2. 检查是否存在 Microtasks ，如果存在则不停地执行，直至清空Microtask Queue
3. 更新 render
4. 主线程重复执行上述步骤

## 参考链接

- Sebastian Porto, [Asynchronous JS: Callbacks, Listeners, Control Flow Libs and Promises](http://sporto.github.com/blog/2012/12/09/callbacks-listeners-promises/)
