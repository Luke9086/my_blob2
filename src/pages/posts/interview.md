## 自我介绍

面试官您好，我是***，本科毕业于****，硕士毕业于****信息管理专业。我一开始是希望从事量化策略研究，但是我后来觉得不太适合自己，所以决定从事前端开发的工作。我自学了操作系统和计算机网络，然后也开发了一个yelp-camp的项目，用于分享露营地点。我也使用了react框架来实现了复杂的用户界面和流畅的用户体验。在项目中我用到了包括状态管理、组件化开发以及使用Redux进行全局状态的管理。我也非常希望能加入美团，来从事前端开发的工作。

## Deep copy

```javascript
var o = { name: "MiTaoEr", info: { address: "天津", color: "red" } };
var t = JSON.parse(JSON.stringify(o));
o.info.address = "北京";
console.log(t);
/* { name: 'MiTaoEr', info: { address: '天津', color: 'red' } } */

```

JSON 数据中没有函数和 undefined 类型，因此在进行序列化的过程中，对象中的这部分数据会被直接过滤掉，此外正则类型的数据也会被处理为空对象。

```javascript
        /* 深拷贝实现函数 */
        let deepClone = (val, wm = new WeakMap) => {
            if (val == null) return val;
            if (typeof val !== "object") return val;
            if (val instanceof Date) return new Date(val);
            if (val instanceof RegExp) return new RegExp(val);
            if (wm.has(val)) return wm.get(val);
            let _instance = new val.constructor;
            wm.set(val, _instance);

            for (let key in val) {
                if (val.hasOwnProperty(key)) _instance[key] = deepClone(val[key], wm);
            }
            return _instance;
        }

```

层序遍历

```javascript
var levelOrder = function(root) {
    //二叉树的层序遍历
    let res = [], queue = [];
    queue.push(root);
    if(root === null) {
        return res;
    }
    while(queue.length !== 0) {
        // 记录当前层级节点数
        let length = queue.length;
        //存放每一层的节点
        let curLevel = [];
        for(let i = 0;i < length; i++) {
            let node = queue.shift();
            curLevel.push(node.val);
            // 存放当前层下一层的节点
            node.left && queue.push(node.left);
            node.right && queue.push(node.right);
        }
        //把每一层的结果放到结果数组
        res.push(curLevel);
    }
    return res;
};

```

前序遍历

```javascript
var preorderTraversal = function(root) {
 let res=[];
 const dfs=function(root){
     if(root===null)return ;
     //先序遍历所以从父节点开始
     res.push(root.val);
     //递归左子树
     dfs(root.left);
     //递归右子树
     dfs(root.right);
 }
 //只使用一个参数 使用闭包进行存储结果
 dfs(root);
 return res;
};
```

中序遍历

```javascript
var inorderTraversal = function(root) {
    let res=[];
    const dfs=function(root){
        if(root===null){
            return ;
        }
        dfs(root.left);
        res.push(root.val);
        dfs(root.right);
    }
    dfs(root);
    return res;
};
```

后序遍历

```
var postorderTraversal = function(root) {
    let res=[];
    const dfs=function(root){
        if(root===null){
            return ;
        }
        dfs(root.left);
        dfs(root.right);
        res.push(root.val);
    }
    dfs(root);
    return res;
};
```



## 快速排序

快速排序使用[分治法open in new window](https://zh.wikipedia.org/wiki/分治法)（Divide and conquer）策略来把一个序列分为较小和较大的 2 个子序列，然后递归地排序两个子序列。具体算法描述如下：

1. 从序列中**随机**挑出一个元素，做为 “基准”(`pivot`)；
2. 重新排列序列，将所有比基准值小的元素摆放在基准前面，所有比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个操作结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；
3. 递归地把小于基准值元素的子序列和大于基准值元素的子序列进行快速排序。

------

插入排序

1从第一个元素开始，该元素可以认为已经被排序；

2取出下一个元素，在已经排序的元素序列中从后向前扫描；

3如果该元素（已排序）大于新元素，将该元素移到下一位置；

4重复步骤 3，直到找到已排序的元素小于或者等于新元素的位置；

5将新元素插入到该位置后；

重复步骤 2~5。

------

著作权归JavaGuide(javaguide.cn)所有 基于MIT协议 原文链接：https://javaguide.cn/cs-basics/algorithms/10-classical-sorting-algorithms.html

著作权归JavaGuide(javaguide.cn)所有 基于MIT协议 原文链接：https://javaguide.cn/cs-basics/algorithms/10-classical-sorting-algorithms.html

```
function quickSort(arr) {
    // 递归结束条件：数组长度小于或等于1
    if (arr.length <= 1) {
        return arr;
    }

    // 选择基准元素（pivot），这里选择数组中间的元素
    const pivotIndex = Math.floor(arr.length / 2);
    const pivot = arr.splice(pivotIndex, 1)[0]; // 从数组中取出基准元素，并从原数组中移除

    let left = [];
    let right = [];

    // 遍历数组，根据与基准元素的比较结果分配到左边或右边数组
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] < pivot) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }

    // 递归对左右两部分数组进行快速排序，然后将排序好的数组和基准元素合并
    return quickSort(left).concat([pivot], quickSort(right));
}

// 示例数组
const array = [6, 3, 8, 5, 2, 7, 4, 1];
console.log("Original array:", array);
const sortedArray = quickSort(array);
console.log("Sorted array:", sortedArray);

```

## 事件循环

可以看到，Eventloop 在处理宏任务和微任务的逻辑时的执行情况如下：

1. JavaScript 引擎首先从宏任务队列中取出第一个任务；
2. 执行完毕后，再将微任务中的所有任务取出，按照顺序分别全部执行（这里包括不仅指开始执行时队列里的微任务），如果在这一步过程中产生新的微任务，也需要执行，**也就是说在执行微任务过程中产生的新的微任务并不会推迟到下一个循环中执行，而是在当前的循环中继续执行。**
3. 然后再从宏任务队列中取下一个，执行完毕后，再次将 microtask queue 中的全部取出，循环往复，直到两个 queue 中的任务都取完。

作者：CUGGZ
链接：https://juejin.cn/post/6992167223523541023
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



filter(e=>e.id!==id)

删除id的函数

## 手写promise.all

```javascript
function promiseAll(promises) {
    return new Promise((resolve, reject) => {
        if (!Array.isArray(promises)) {
            return reject(new TypeError("Argument must be an array of promises."));
        }
        let results = [];
        let completed = 0;
        for (let i = 0; i < promises.length; i++) {
            Promise.resolve(promises[i]) // 处理非Promise值的情况，确保一致性
                .then(value => {
                    results[i] = value;  // 保持原数组的顺序
                    completed += 1;
                    if (completed === promises.length) {
                        resolve(results); // 当所有promises都解决时，resolve这个新Promise
                    }
                })
                .catch(reject); // 任何一个Promise失败了，新的Promise立即reject
        }
        if (promises.length === 0) {
            resolve(results); // 如果传入的数组为空，直接resolve一个空数组
        }
    });
}

// 使用示例
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'foo');
});

promiseAll([promise1, promise2, promise3]).then(values => {
    console.log(values);  // 输出: [3, 42, 'foo']
}).catch(error => {
    console.log('Failed:', error);
});

```

render

setstate and re-render and get new state value

side-effects

effects

AJAX changing parts of DOM unrelated to render

useEffect by default runs every time render

useEffect(fn,[])

only the first time

empty state and I wanna fetch data

## cookies

- *会话期* Cookie 会在当前的会话结束之后删除。浏览器定义了“当前会话”结束的时间，一些浏览器重启时会使用*会话恢复*。这可能导致会话 cookie 无限延长。
- *持久性* Cookie 在过期时间（`Expires`）指定的日期或有效期（`Max-Age`）指定的一段时间后被删除。

#### Domain 属性

`Domain` 指定了哪些主机可以接受 Cookie。如果不指定，该属性默认为同一 [host](https://developer.mozilla.org/zh-CN/docs/Glossary/Host) 设置 cookie，*不包含子域名*。如果指定了 `Domain`，则一般包含子域名。因此，指定 `Domain` 比省略它的限制要少。但是，当子域需要共享有关用户的信息时，这可能会有所帮助。

例如，如果设置 `Domain=mozilla.org`，则 Cookie 也包含在子域名中（如 `developer.mozilla.org`）。

#### Path 属性

`Path` 属性指定了一个 URL 路径，该 URL 路径必须存在于请求的 URL 中，以便发送 `Cookie` 标头。以字符 `%x2F` (“/”) 作为路径分隔符，并且子路径也会被匹配。

例如，设置 `Path=/docs`，则以下地址都会匹配：

- `/docs`
- `/docs/`
- `/docs/Web/`
- `/docs/Web/HTTP`

但是这些请求路径不会匹配以下地址：

- `/`
- `/docsets`
- `/fr/docs`

[`SameSite`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie#samesitesamesite-value) 属性允许服务器指定是否/何时通过跨站点请求发送（其中[站点](https://developer.mozilla.org/zh-CN/docs/Glossary/Site)由注册的域和*方案*定义：http 或 https）。这提供了一些针对跨站点请求伪造攻击（[CSRF](https://developer.mozilla.org/zh-CN/docs/Glossary/CSRF)）的保护。它采用三个可能的值：`Strict`、`Lax` 和 `None`。

使用 `Strict`，cookie 仅发送到它来源的站点。`Lax` 与 Strict 相似，只是在用户*导航*到 cookie 的源站点时发送 cookie。例如，通过跟踪来自外部站点的链接。`None` 指定浏览器会在同站请求和跨站请求下继续发送 cookie，但*仅在安全的上下文中*（即，如果 `SameSite=None`，且还必须设置 `Secure` 属性）。如果没有设置 `SameSite` 属性，则将 cookie 视为 `Lax`。

## useRef useState

### useRef

1. **保持引用不变**：`useRef`返回一个可变的`ref`对象，其`.current`属性被初始化为传递给`useRef`的参数。这个对象在组件的整个生命周期中保持不变。
2. **不触发重新渲染**：更新`ref`对象的`.current`属性不会触发组件的重新渲染。这使得`useRef`非常适合用于跟踪组件内的变量和状态，而不需要触发视图更新。
3. **DOM引用**：`useRef`常用于获取组件的DOM节点，例如，当你需要直接操作DOM时，可以将ref对象赋给元素的`ref`属性。
4. **保存任何可变值**：除了DOM引用外，`useRef`也常用于保存任何其他数据，比如一个计时器的ID或任何其他实例，其值可能在组件的多次渲染之间变化但不需要触发重新渲染。

### useState

1. **状态管理**：`useState`用于在函数组件中添加状态。它返回一个状态变量和一个用于更新这个状态的函数。这个状态在组件的重新渲染间是持久的。
2. **触发重新渲染**：当你通过`useState`的更新函数更新状态时，它会触发组件的重新渲染，从而反映状态的更新。
3. **用于数据绑定**：`useState`通常用于那些当数据变化时需要更新UI的场景。每次状态改变都会导致组件重新渲染，确保用户界面与状态数据保持同步。
4. **支持函数更新**：`useState`的更新函数支持函数式更新，这对于依赖于前一个状态来计算新状态的场景非常有用。

### 示例对比

这里有一个简单的示例来展示`useRef`和`useState`的区别

## ueEffect 模拟生命周期

在React中，`useEffect` 钩子提供了一种方式来模拟类组件的生命周期方法。通过适当的使用依赖项数组（第二个参数），可以在函数组件中实现与`componentDidMount`、`componentDidUpdate`、和`componentWillUnmount`相似的行为。下面将详细介绍如何使用 `useEffect` 来模拟这些生命周期方法：

### 1. 模拟 `componentDidMount`
要模拟 `componentDidMount` 的行为，可以传递一个空的依赖项数组给 `useEffect`。这意味着`useEffect` 中的代码只会在组件首次渲染后执行一次。

```jsx
useEffect(() => {
    // 这里的代码只会在组件首次渲染后执行一次，类似于 componentDidMount
    console.log('Component did mount');

    return () => {
        // 这里的代码会在组件卸载时执行，类似于 componentWillUnmount
        console.log('Component will unmount');
    };
}, []);
```

### 2. 模拟 `componentDidUpdate`
要模拟 `componentDidUpdate`，可以在 `useEffect` 的依赖项数组中指定需要观察的状态或属性。这样，只要这些依赖项发生变化，`useEffect` 就会被重新执行。

```jsx
useEffect(() => {
    // 这段代码会在依赖项中的状态或属性更新后执行，类似于 componentDidUpdate
    console.log('Component did update');

    return () => {
        // 这里不会执行任何清理操作，因为它每次更新都会调用
    };
}, [dependency1, dependency2]); // 只有当 dependency1 或 dependency2 改变时，useEffect 才会运行
```

### 3. 模拟 `componentWillUnmount`
要模拟组件卸载时的行为，可以在 `useEffect` 的清理函数中编写代码。这个清理函数会在组件卸载前执行，或者在依赖项改变导致旧的 `useEffect` 清理前执行。

```jsx
useEffect(() => {
    // 设置定时器、订阅事件、或执行某些只需要运行一次的效果

    return () => {
        // 清理定时器、取消订阅事件等，这里的代码会在组件卸载前执行，类似于 componentWillUnmount
        console.log('Component will unmount');
    };
}, []); // 依赖项为空，表示这个 effect 只在挂载和卸载时运行
```

### 总结
使用 `useEffect` 钩子来模拟类组件的生命周期方法是一种非常强大的技术，它使得在函数组件中处理副作用成为可能。通过合理使用依赖项数组，可以精确控制副作用的触发时机，以及何时进行必要的清理工作。这提高了代码的可维护性和性能，是React推荐的函数组件中处理副作用的方式。

## 跨域

180页

## useConext

在React中，`useContext` 是一个钩子（Hook），它允许你在组件树中访问跨层级的状态和函数，无需通过逐层传递 `props`。这个钩子是用来简化跨组件的数据传递，特别是对于一些需要在多个层级中使用的公共数据，如用户认证状态、主题设置、语言偏好等。

### 使用 `useContext`

`useContext` 钩子需要与 `React.createContext` 配合使用。首先，你需要使用 `React.createContext` 创建一个上下文（Context）对象。这个对象将包括一个 Provider 组件和一个 Consumer 组件。Provider 用于封装那些需要访问上下文数据的组件，并通过 `value` 属性提供上下文数据。`useContext` 钩子使得函数组件可以订阅这个上下文的变化，并读取上下文的值。

### 步骤示例

下面是如何使用 `useContext` 的一个基本步骤：

1. **创建上下文**
   ```javascript
   import React, { createContext } from 'react';
   
   const MyContext = createContext(null);
   ```

2. **提供上下文数据**
   在组件树的合适位置使用 Provider 来封装子组件，传递需要跨组件共享的数据。
   ```jsx
   import React from 'react';
   import { MyContext } from './MyContext';
   
   function App() {
     return (
       <MyContext.Provider value={{ sharedData: "Hello, Context!" }}>
         <ChildComponent />
       </MyContext.Provider>
     );
   }
   ```

3. **消费上下文数据**
   在需要使用上下文数据的组件内，使用 `useContext` 钩子访问这些数据。
   ```jsx
   import React, { useContext } from 'react';
   import { MyContext } from './MyContext';
   
   function ChildComponent() {
     const context = useContext(MyContext);
   
     return <p>{context.sharedData}</p>; // 输出：Hello, Context!
   }
   ```

### 优势

使用 `useContext` 可以大大简化组件之间的通信，特别是在需要将数据传递给深层嵌套组件时。与传统的通过 `props` 逐层传递相比，`useContext` 提供了一种更清洁、更直接的方式来共享数据。

### 注意事项

- 使用上下文时应该谨慎，因为它可能导致组件的重用性降低。如果过度使用，也可能使组件的依赖关系变得不清晰。
- `useContext` 会使得所有消费者组件在上下文值变化时重新渲染，因此，如果上下文数据经常变化，可能会引起性能问题。需要合理组织上下文数据，避免不必要的渲染。

总之，`useContext` 是React提供的一种强大工具，能够帮助开发者在组件间共享数据和状态，同时保持代码的整洁和组织。

## 原型继承和class继承

![image-20240424142420783](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20240424142420783.png)

组合式继承

## 如何优化性能

React性能优化是一个重要的主题，特别是当你的应用规模扩大、组件数量增多时，合理的优化措施可以显著提高应用的响应速度和用户体验。下面是一些常见的React性能优化策略：

### 1. 使用不可变数据
- 不可变数据有助于快速比较状态或属性是否变化，特别是在使用`PureComponent`或`React.memo`时。这样可以减少不必要的组件重新渲染。

### 2. 优化渲染列表
- 对于长列表或复杂的列表项，使用`React.memo`来避免无谓的重新渲染。
- 考虑使用窗口化或虚拟化技术（如`react-window`或`react-virtualized`），只渲染可视区域内的元素。

### 3. 组件懒加载
- 使用`React.lazy`和`Suspense`来实现路由级别的懒加载，从而减少应用的初始加载时间。

### 4. 避免匿名函数和对象字面量
- 在渲染方法或组件渲染函数中避免直接使用匿名函数和对象字面量，因为这会在每次渲染时创建新的引用，导致子组件无谓的重新渲染。

### 5. 使用`shouldComponentUpdate`和`React.memo`
- 对于类组件，可以通过实现`shouldComponentUpdate`生命周期方法来控制组件是否需要更新。
- 对于函数组件，使用`React.memo`可以避免组件在接收到相同的props时重新渲染。

### 6. 合理使用`useCallback`和`useMemo`
- `useCallback`可以缓存函数，避免因为函数的重新创建导致子组件的无谓渲染。
- `useMemo`可以缓存计算结果，避免在每次渲染时进行重复的计算。

### 7. 状态提升和拆分
- 对于跨多个组件共享的状态，考虑将状态提升到共同的父组件或使用上下文（Context）。
- 对于复杂组件，拆分为更小的子组件，使状态管理更局部化，减少不必要的渲染。

### 8. 减少DOM操作
- 减少不必要的DOM层级，简化渲染树。
- 避免使用内联样式，特别是在大型列表和表格中，因为这会增加JavaScript和DOM的处理时间。

### 9. 使用Key属性
- 在渲染列表时，合理使用`key`属性，确保React可以高效地对列表进行增删改查的DOM操作。

### 10. 监控和分析性能
- 使用React Developer Tools等工具进行性能分析。
- 利用Chrome DevTools的Performance标签页进行实时性能监测和问题诊断。

通过实施上述策略，可以有效地提升React应用的性能。始终记住，优化工作应该是基于性能瓶颈的具体分析结果来进行的，避免过早优化。

## useMemo useCallbaclk有什么区别

在React中，`useMemo` 和 `useCallback` 都是钩子（Hooks），用于优化性能，主要通过缓存来避免不必要的计算或重新渲染。尽管它们在功能上有所重叠，但它们各自有特定的用途和适用场景。

### useMemo

`useMemo` 用于缓存复杂函数的返回值。当你有一个计算成本较高的函数时，你可以使用 `useMemo` 来存储这个函数的结果，直到其依赖项发生变化。只有当依赖项改变时，函数才会重新执行，并缓存新的返回值。

**用途**：
- 缓存计算结果，避免在每次渲染时重复执行计算密集型的操作。
- 可以用来缓存组件，尤其是当组件的props没有变化时，避免不必要的虚拟DOM比较和重新渲染。

**示例**：
```jsx
const heavyComputation = expensiveValue => {
  // 模拟一个重计算过程
  console.log("Computing...");
  return expensiveValue * 2;
};

const Component = ({ expensiveValue }) => {
  const computedValue = useMemo(() => heavyComputation(expensiveValue), [expensiveValue]);

  return <div>{computedValue}</div>;
};
```

在上述示例中，只有当 `expensiveValue` 改变时，`heavyComputation` 函数才会重新执行，并更新 `computedValue`。

### useCallback

`useCallback` 用于缓存函数实例。当你将函数传递给子组件作为prop时，每次父组件渲染都会创建新的函数实例，即使函数体完全相同。这会导致接收该函数的子组件认为props发生了变化，从而触发不必要的重新渲染。通过 `useCallback`，你可以保证只有当函数的依赖项改变时，函数实例才会更新。

**用途**：
- 缓存事件处理器和传递给子组件的回调函数，减少子组件因接收新函数实例而导致的重新渲染。

**示例**：
```jsx
const Component = ({ id, onFetch }) => {
  const handleClick = useCallback(() => {
    onFetch(id);
  }, [id, onFetch]);

  return <button onClick={handleClick}>Fetch Data</button>;
};
```

在上述示例中，`handleClick` 会被缓存，并只有当 `id` 或 `onFetch` 发生变化时才会更新。

### 区别

- **目的**：`useMemo` 是为了缓存值（计算结果或组件），而 `useCallback` 是为了缓存函数实例。
- **返回内容**：`useMemo` 返回计算的结果，`useCallback` 返回函数本身。
- **适用场景**：`useMemo` 用于优化那些依赖特定数据进行昂贵计算的场景；`useCallback` 用于优化那些需要保证函数身份稳定以防止不必要渲染的场景。

理解和正确使用这两个钩子可以显著提高应用的性能，特别是在处理大量数据和复杂更新时。

## webpack和vite

`Webpack`和`Vite`都是现代前端开发中非常流行的工具，它们用于优化前端资源的加载和打包。虽然两者都服务于类似的目的，它们的工作方式和优势有所不同。

### Webpack

**概述**：
- Webpack是一个模块打包器（module bundler）。它的主要目的是打包JavaScript文件，但它也可以通过使用各种加载器（loaders）和插件（plugins）来处理其他资源，如样式表、图片和字体。
- 它工作的方式是将所有的资源视为模块，通过一个入口文件开始，解析依赖树，然后将所有这些资源打包成一个（或多个）包含所有应用依赖的静态文件。

**核心特点**：
- **加载器**：Webpack使用加载器来处理不同的文件类型，例如使用`babel-loader`来转换ES6+代码，使用`style-loader`和`css-loader`来处理CSS文件。
- **插件系统**：强大的插件系统允许开发者自定义Webpack的构建过程，例如优化打包文件、环境变量注入等。
- **代码拆分**：支持代码拆分，允许应用按需加载代码，从而提高加载速度。
- **开发服务器**：提供一个简单的web服务器和实现热模块替换（HMR）。

### Vite

**概述**：
- Vite是一个现代化的前端构建工具，它在开发模式下不需要打包操作，而是利用现代浏览器支持的原生ES模块加载（ESM）来提供服务。
- 它在生产模式下使用Rollup进行打包，Rollup通常比Webpack更快，输出更小的文件。

**核心特点**：
- **快速的冷启动**：不需要等待打包操作就可以启动开发服务器，因为Vite只在请求时才对模块进行处理。
- **即时模块热更新**（HMR）：由于没有预打包步骤，模块热更新几乎是瞬间完成的。
- **使用Rollup打包**：在生产环境中，Vite使用Rollup进行高效的打包。
- **丰富的插件生态**：虽然比Webpack少，但也支持通过插件扩展功能。

### 区别

- **启动速度**：Vite在开发模式下的启动速度远快于Webpack，因为Webpack需要在开发过程中构建整个应用。
- **模块处理**：Webpack将所有资源视为模块并进行预打包，而Vite利用ESM动态加载模块，减少了启动和更新时的负担。
- **生态系统**：Webpack的生态系统更成熟，插件和加载器更丰富，但Vite正在迅速发展，并逐渐扩展其功能和插件支持。

总结来说，Webpack是一个成熟的解决方案，适用于需要复杂配置和细粒度优化的大型应用。而Vite则更适合于现代开发，它利用ESM和更快的构建性能，为开发者提供了更快的开发体验。选择哪一个工具取决于项目需求、团队习惯以及对构建速度和灵活性的需求。

## 图片懒加载

### 2. 使用Intersection Observer API（推荐方法）

`Intersection Observer API`提供了一种方式，可以配置地监听元素是否进入了视口区域，适用于实现图片懒加载。这种方法比传统的监听scroll事件性能更好，因为它由浏览器直接支持，不需要进行复杂的计算或频繁的DOM访问。

```javascript
document.addEventListener("DOMContentLoaded", function() {
  const images = document.querySelectorAll('img[data-src]'); // 所有带data-src属性的图片

  const imageObserver = new IntersectionObserver((entries, observer) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const img = entry.target;
        img.src = img.getAttribute('data-src');
        img.removeAttribute('data-src');
        observer.unobserve(img); // 图片加载后取消观察
      }
    });
  }, {
    rootMargin: '0px 0px 50px 0px', // 触发提前量，可以根据需要调整
    threshold: 0.01
  });

  images.forEach(image => {
    imageObserver.observe(image);
  });
});

```

## 最大的难点

### 最有难度的点：细粒度的权限控制系统

在你的实习项目中，开发因子管理系统的一个关键难点可能是实现细粒度的权限控制系统。权限控制系统需要确保只有授权用户可以访问特定的数据和功能，例如防止普通员工查看其他人的成果展示。这要求前端不仅要正确显示数据和功能，还需要确保安全性和数据的访问控制。

### 解决方法：使用角色基权限管理（RBAC）和前端路由守卫

为了解决权限控制的问题，可以实施角色基权限管理（Role-Based Access Control, RBAC）系统，并结合前端路由守卫来控制用户访问。

#### 实施步骤：

1. **定义角色和权限**：
   - 首先，定义系统中的角色，如管理员、量化分析师、普通员工等。
   - 为每个角色分配不同的权限。例如，普通员工可以查看自己的成果展示，量化分析师可以查看所有人的成果，管理员可以管理用户权限。

2. **后端权限验证**：
   - 在后端实现权限控制逻辑。当请求数据时，后端需要验证请求用户的身份和权限，确保用户只能访问他们被授权的数据。
   - 使用JWT（JSON Web Tokens）或类似技术，在用户登录时生成包含用户角色信息的Token，并在随后的请求中使用这个Token来验证权限。

3. **前端路由守卫**：
   - 在React中，可以使用`react-router-dom`的`Route`组件结合上下文（Context API）或Redux来控制路由访问。
   - 创建高阶组件（HOC），用于包装受保护的路由。这个组件会检查用户的角色和权限，并决定是否允许访问目标页面或重定向到登录页面。

```javascript
import React from 'react';
import { Route, Redirect } from 'react-router-dom';

const ProtectedRoute = ({ component: Component, roles, ...rest }) => (
  <Route {...rest} render={props => {
    const currentUser = authenticationService.currentUserValue;
    if (!currentUser || !roles.includes(currentUser.role)) {
      // 不符合要求的用户尝试访问这个路由时被重定向到登录页面
      return <Redirect to={{ pathname: '/login', state: { from: props.location } }} />
    }

    // 授权所需角色的用户可以访问
    return <Component {...props} />
  }} />
);
```

4. **在应用中实施**：
   - 使用`ProtectedRoute`组件代替普通的`Route`组件，为需要权限控制的路由提供保护。
   - 根据用户的角色渲染不同的UI元素，例如，只有对应权限的用户才能看到导航到特定页面的链接。

### 总结

通过在后端实施强大的权限验证，并在前端利用路由守卫来防止未授权访问，可以有效地实现细粒度的权限控制。这不仅提高了系统的安全性，还确保了用户体验的一致性和合法性。

## Number结果

### 为什么 `Number('')` 是 0

当你使用`Number`函数转换一个空字符串`''`时，结果是`0`。根据ECMAScript规范，如果字符串仅包含空白字符（或者根本没有字符），则将其转换为`0`。空字符串被视为缺乏任何数值，因此按照规范被赋予了最自然的数值表示——即`0`。这类似于在逻辑上认为"没有值"可以等价于"零值"。

### 为什么 `Number(undefined)` 是 NaN

对于`undefined`，情况则完全不同。`undefined`在JavaScript中是一个表示缺少值的数据类型。当你试图将`undefined`转换为一个数字时，按照ECMAScript规范，这个转换操作无法找到一个合理的数值表示，因此结果是`NaN`（Not a Number），表示这不是一个有效的数字。

## 堆和栈的关系

在JavaScript中，堆（Heap）和栈（Stack）是两种数据结构，用于存储变量和管理执行上下文中的数据。尽管JavaScript开发者不需要手动管理这些内存结构，了解它们的工作原理有助于更好地理解性能问题、内存使用和垃圾回收等概念。

### 栈（Stack）
栈是一种线性的数据结构，遵循后进先出（LIFO，Last In First Out）的原则。在JavaScript的执行上下文中，栈用于存储原始数据类型（Undefined, Null, Boolean, Number, String, Symbol, BigInt）的值和函数调用的记录。

- **快速访问**：栈允许数据的快速访问和管理。每次函数调用都会在栈顶创建一个新的帧，存储函数的参数和局部变量。
- **大小限制**：栈空间相对较小，且有最大容量限制。当栈空间被耗尽（通常通过过深的递归或太多的函数调用），会引发“栈溢出”错误。
- **管理方式**：JavaScript引擎自动管理栈的推送和弹出操作。

### 堆（Heap）
堆是一种用于存储对象（及其他可能的复杂数据结构）的非结构化的内存区域。相对于栈，堆的结构更自由，容量更大，但访问速度较慢。

- **动态分配**：在堆上，内存是动态分配的。当创建一个对象时，对象被存储在堆内存中，并返回一个引用地址。这个地址被存储在执行栈中的变量里。
- **无大小限制**：堆的大小不是固定的，它可以动态扩展到系统的可用内存的限制。
- **垃圾回收**：JavaScript使用垃圾回收机制来自动清理不再被引用的对象，防止内存泄漏。由于堆是动态分配和回收的，所以垃圾回收在堆中尤其重要。

### 栈和堆的主要区别
1. **数据结构**：
   - 栈是结构化的，严格按照LIFO顺序操作。
   - 堆是非结构化的，可以随意存放和移除数据。

2. **存储内容**：
   - 栈主要存储原始值和指向堆内存中对象的引用。
   - 堆存储复杂数据结构，如对象、数组等。

3. **内存分配**：
   - 栈的内存分配在编译时进行。
   - 堆的内存分配在运行时进行。

4. **性能**：
   - 栈内存的分配和回收速度快。
   - 堆内存的分配和回收速度相对较慢，且管理成本更高。

5. **大小限制**：
   - 栈空间较小，易发生溢出。
   - 堆空间较大，受系统可用内存的限制。

了解堆和栈的这些基本差异有助于优化性能，特别是在处理大量数据和深层递归函数调用时。通过有效地管理存储原始类型和对象的方式，可以减少内存使用和避免性能瓶颈。