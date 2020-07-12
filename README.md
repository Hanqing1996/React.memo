* React.PureComponent是给类组件使用的
* React.memo(...)是给函数组件使用的
> 二者都是对props和state做浅层比较，以判断是否render组件

#### 注意
* 在不使用 React.memo 的情况下，哪怕父组件没有给子组件传递任何props，父组件的render 也会引起子组件的 render。
```
export default function App() {
  return (
    <div>
        <Child/> 
    </div>
  );
}
```
* 父组件的 render 一定会引起子组件 props 的值变化，这种情况下子组件不必加 React.memo（不然徒增判断新旧props差异的损耗）。


#### 什么情况子组件要加 React.memo
> 要搞清楚父组件因为什么而重新 render（第一次 render 不必考虑，此次的子组件 render 是必要的）
1. 子组件形如 <Child/>，不接受任何 props
2. 父组件是由于 setA 而重新 render，但是子组件形如 <Child b={B}/>

