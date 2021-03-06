# 深浅拷贝

> 在js的应用中，对象和数组的拷贝是经常出现的情况，由于其是引用传递，直接赋值，可能导致原始对象或数组被无意的修改

## 浅拷贝

> 1.浅拷贝只能实现，一层引用的拷贝，如果一个对象中还有对象，那么这个值依然是引用值
>
> \`\`\` function clone\(Origin, Target\){ let target = Target \|\| {} for\(let props in Origin\){ target\[props\] = Origin\[props\] } return target }

```text
let obj = {
    a: '1',
    b: [1,2,3,4,5]
}
let obj2 = clone(obj)
//修改obj2 里b数组的值，obj里的值也会改变
obj2.b[1] = 'test' 
```

```text
> 2.Object.assign()也能实现浅拷贝
```

```text
let obj = {
    a: '1',
    b: [1,2,3,4,5]
}
let obj2 = Object.assign({}, obj, {a: 'a'})
```

```text
### 深拷贝

> 最简单的深拷贝方法，非JSON.parse()莫属，只需要短短几行代码就能实现深拷贝
```

function deepClone\(Origin\){ let obj = {} try{ obj = JSON.parse\(JSON.stringify\(Origin\)\) }catch\(e\){} return obj }

```text
> 用递归的方法实现深拷贝，这里我把数组的拷贝和对象拷贝写在了一起，当然也可以另外写一个专门用于数组的方法
```

function deepClone\(Origin, Target\){ let targ = Target \|\| {} for\(let \[prop, val\] of Object.entries\(Origin\)\){ if\(Object.prototype.toString.call\(val\) == '\[object Object\]'\){ targ\[prop\] = deepClone\(val\) }else if\(Object.prototype.toString.call\(val\) == '\[object Array\]'\){ targ\[prop\] = deepClone\(val, \[\]\) }else{ targ\[prop\] = val } } return targ } \`\`\`

