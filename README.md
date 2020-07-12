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
