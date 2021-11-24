

```ts
interface Info {
    firstName: string,
    lastName: string,
}

function getFullName(info: Info): string {
    return `${info.firstName}-${info.lastName}`
}
```

在定义接口的时候，你不要把它理解为是在定义一个对象，而要理解为{}括号包裹的是一个代码块，里面是一 条条声明语句，只不过声明的不是变量的值而是类型。声明也不用等号赋值，而是冒号指定类型。每条声明之前用 换行分隔即可，或者也可以使用分号或者逗号，都是可以的。

### 可选属性
```ts
interface Info {
    firstName: string,
    lastName: string,
    age?: number,
}
```

### 多余属性检查
```ts
interface Info {
    firstName: string,
    lastName: string,
    age?: number,
}

const info: Info = {
    firstName: 'da',
    lastName: 'yueba',
    name: 'xuan', // 报错 Object literal may only specify known properties, and 'name' does not exist in type 'Info'.
}
```

### 绕开多余参数检查

#### 1. 类型断言
```ts
interface Info {
    firstName: string,
    lastName: string,
    age?: number,
}

const info: Info = {
    firstName: 'da',
    lastName: 'yueba',
    name: 'xuan', // 不报错 
} as Info
```

#### 2. 索引签名
```ts
interface Info {
    firstName: string,
    lastName: string,
    age?: number,
    [prop: string]: any;
}

const info: Info = {
    firstName: 'da',
    lastName: 'yueba',
    name: 'xuan', // 不报错 
}
```

### 只读属性
```ts
interface Info {
    firstName: string,
    lastName: string,
    age?: number,
    readonly balance: number,
    [prop: string]: any;
}
```

### 函数类型
```ts
interface addFunc {
    (a: number, b: number): number,
}

const add:addFunc = (a:number, b:number) => a + b;
```
## 高级用法
### 索引类型
```ts
interface RoleDic { 
  readonly [id: number]: string; 
}
const role1: RoleDic = { 
  0: "super_admin", 1: "admin"
};
const role2: RoleDic = {
  s: "super_admin", // error 不能将类型"{ s: string; a: string; }"分配给类型"RoleDic"。 
  a: "admin" 
};
const role3: RoleDic =["super_admin", "admin"];
```
### 继承接口
```ts
interface Account {
  username: string,
}

interface VIP extends Account {
  discount: number
}

const vip:VIP = {
  username: 'u',
  discount: 90,
}
```
也可以继承多个接口
```ts
interface Account {
  username: string,
}

interface Role {
  role: number[],
}

interface VIP extends Account, Role {
  discount: number
}

const vip:VIP = {
  username: 'u',
  discount: 90,
  role: [1, 2, 3]
}
```

### 混合类型接口
