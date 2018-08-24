# MobX & 响应式编程

by Kuitos

## 自我介绍
* team: @mobxjs
* github: @kuitos 
* zhihu: @kuitos

The style of this slide is inspired by
Takahashi Method
高橋流簡報法

MobX 是什么

一种状态管理方案

Redux?

FP VS OOP

FP
* lambda 演算
* 声明式(函数组合)
* 无副作用

```js
// Component
dispatch(updateCounter())
// ActionCreator
function updateCounter() {
  ...
  dispatch({ type: 'COUNTER_UPDATE', payload })
}
// reducer
function reducer(state = {}, action) {
	switch (action.type) {
	  case 'COUNTER_UPDATE':
	  	return {...state, counter: state.counter++};
	}
}
```

OOP
* 图灵机
* 命令式(一把梭)
* 不关心副作用

```js
class Store {
    @observable counter = 0;
    @action updateCounter() {
        this.counter++;
    }
}
```

真香!

两者其实是可以和平共存的

但在前端这个上下文里
真实情况是

![](mobx-and-reactive-programming/handshake.jpg)

MobX 几个基础概念

observable

维护了一组 observer/watcher 的
可被观察的数据

```js
class ViewModel {
	@observable isLoading = false;
	@observable pageId = '';
}
```

derivation

数据变化的衍生行为
recomputed 或 副作用

* computed
* reaction

```js
class ViewModel {
    onInit() {
        reaction(
            () => this.userStore.role,
            role => {
                if (role === 'visitor') redirectTo('/index');
            }
        );
    }
    @computed get fullName() {
        return this.userStore.lastName + this.userStore.firstName;
    }
}
```

action

```js
class ViewModel {
    @action mutate() {
        this.counter++;
    }
}
```

```js
// 完整示例
class UserStore {
    @observable age = 10;
    @computed get isAdult() {
        return this.age >= 18;
    }
    @action setAge(v) {
        this.age = v;
    }
}
```

响应式编程

Reactive Programming

![](mobx-and-reactive-programming/1.jpg)

一个简单的解释

a := b + c

Imperative Programming

a = b + c

用 JS 来描述

Imperative Programming
```js
const obj = {
	b: 1,
	c: 2,
};
function setB(v) {
    obj.b = v;
    obj.a = obj.b + obj.c;
}
obj.a = obj.b + obj.c;
console.log(obj.a); // 3
setB(obj.b + 1);
console.log(obj.a); // 4
```

Reactive Programming
```js
const obj = {
	b: 1,
	c: 2,
	get a() {
		return obj.b + obj.c;
	}
};
console.log(obj.a); // 3
obj.b++;
console.log(obj.a); // 4
```

本质是依赖的控制反转
**Inversion of Control**

Imperative Programming
![](mobx-and-reactive-programming/2.jpg)

```js
class Foo {
	updateFooCounter() {
		this.counter++;
		Bar.increaseCounter();
	}
}
```

Reactive Programming
![](mobx-and-reactive-programming/3.jpg)

```ts
class Bar {
	constructor() {
		Foo.onCounterIncreasment(() => this.counter++);
	}
}
```

关注点分离

只关心自己依赖哪些状态
不关心自己的修改会触发哪些外部变化

典型代表

Excel 表格
![](mobx-and-reactive-programming/excel.jpg)

响应式编程实践

SSOT
Single Source Of Truth

同一个业务模型数据
只存储一次

```ts
// Bad Practise
class ViewModel {
    async onInit() {
        this.userList = await http.get('/users');
        this.userMatrix = this.otherStore.matrix.users;
        this.userTree = this.userStore.users.reduce(() => {}, {});
    }
}
```

所有能被衍生出来的数据
都应该是衍生出来的

```ts
// Best Practise
class ViewModel {
    get groups() {
        if (!isEmpty(this.nodeGroupStore.groups)) {
            return this.nodeGroupStore.groups.map((node, index) => {
                const viewNode: IViewNodeGroup = { ...node, opened: false };
                // 第一组默认展开
                if (index === 0) {
                    viewNode.opened = true;
                }
                return viewNode;
            });
        }
        return this.defaultNodeGroups;
    }
}
```

如何修改数据

提交源头的变更行为

```ts
class ViewModel {
    @computed get userAccount() {
        return format(this.accountStore.amount, '$');
    }
    onCharge(amount) {
        this.accountStore.charge(amount);
    }
}
```

通过Store实例的属性衍生数据
通过Store实例的方法改数据

CQRS
Command and Query Responsibility Segregation

![](mobx-and-reactive-programming/cqrs.png)

Command
如果一个方法修改了状态
该方法就是一个命令
且这样的方法应该声明为 void

Query
如果一个方法返回了数据
该方法就是一个查询
且这个方法里不允许修改对象的状态

```ts
class OrgStore {
    @observable members = [];
    @action async loadMembers() {
        this.members = await http.get('/members');
        // return this.members; x
    }
    @action async addMember(member) {
        this.members.push(member);
        try {
            await http.post('/members', member);
        } catch (e) {
            this.members.remove(member)
        }
    }
}
```

读写分离

Predictable
可预测

Derivable
可推导

Traceable
可溯源

响应式编程的本质

通过声明式的代码
描述了运行时的
**数据依赖关系图**

Q&A
