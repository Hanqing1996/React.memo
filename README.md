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

> 最简单的验证方法，如果加不加都一样（log一下，发现子组件都render了），就不必加
1. 子组件形如 <Child/>，不接受任何 props
2. 父组件是由于 setA 而重新 render，但是子组件形如 <Child b={B}/>

#### 下面的 Money 就不必加 React.memo
```
const Money = () => {

    const [tags, setTags] = useState<Tag[]>([
        {id: 1, name: 'fuck'},
        {id: 2, name: 'fuck2'},
        {id: 3, name: 'fuck3'},
        {id: 4, name: 'fuck4'},
    ])

    const [selectedTags, setSelectedTags] = useState<string[]>([])

    const onUpdateTags = (tags: Tag []) => {
        console.log('onUpdateTags');
        setTags(tags)
    }

    const onUpdateSelectedTags = (tags: string[]) => {
        console.log('onUpdateSelectedTags');
        setSelectedTags(tags)
    }

    return (
    ...
            <MoneyTags tags={tags} selectedTags={selectedTags} onUpdateTags={onUpdateTags}
                       onUpdateSelectedTags={onUpdateSelectedTags}/>
     ...
     )
}
```

