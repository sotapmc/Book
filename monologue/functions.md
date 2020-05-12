# 函数库

Monologue 中用到了很多具有广泛用途的函数，这些函数有些来自网上搜集，有些是自己编写的。所有的函数以 `export function` 的形式放在 `@/functions.ts` 下，直接 `import` 即可使用。此页面用来解释每个函数的用途以及其参数含义。

每个函数的参数和返回值都会使用 TypeScript 中所用格式表示出来，但有例外

- 对于可选参数，省略 `undefined` 部分，取而代之会将 `:` 前加上 `?`
- 对于 `any` 任意值，不会使用 `:` 特地指定该类型
- 生成器函数（Generator）在前面会加上一个特有的符号 `*`

### `isPC(): boolean`

- **返回值**：布尔

根据 UA 数据判断用户当前所在的设备，并返回一个指示是否为桌面设备的布尔值。以此类推，如果需要判断是否为移动设备，仅需 `!isPC()`。

### `copy(text: string, callback?: Function): boolean`

- **参数**：
  - `text: string` 复制的目标文字
  - `callback?: Function` 处理完毕的回调函数
- **返回值**：布尔

复制一段文字到用户的剪贴板。默认情况下将会采用较新的 `navigator.clipboard` 方法，该方法是异步的因此可以提供一个回调函数执行。如果不支持 `navigator.clipboard`，那么将会使用 fallback 方法即传统的隐形 textfield 法。

### `isDate(target): boolean`

- **参数**
  - `target` 判断对象
- **返回值**：布尔

判断一个值是否为合法的日期。通常情况下，`target` 的值应符合 `string | number`，但实际上由于该函数的应用场景可能并没有什么前提，所以支持任何类型的值输入。但实际上对于除了 `string | number` 以外的类型，无需调用就能推断为 `false`。

### `isNumericString(str: string): boolean`

- **参数**
  - `str: string` 判断对象
- **返回值**：布尔

判断一个字符串是否为数字，实际上是使用正则表达式测试该字符串，并返回结果。

### `*createIterator(object: object): Generator<any[], void, unknown>`

- **参数**
  - `object: object` 创建对象
- **返回值**：生成器

快速获得一个对象的键值对遍历器。使用例：

```js
for (let [a, b] of createIterator(object)) {
    console.log(object[a] === b);
    // => true
}
```

### `isPCView(): boolean`

- **返回值**：布尔

判断当前视图是否为桌面视图。与 `isPC()` 需要区分开。`isPC()` 仅仅是判断设备类型，而没有判断实际上的横向可视范围。利用此函数可有效防止在桌面平台上以较低的窗口宽度打开页面造成的布局问题。

### `translateNumber(number: number): string`

- **参数**
  - `number: number` 操作对象
- **返回值**：字符串

利用 [Nzh](https://github.com/cnwhy/nzh) 将一个数字转换为中文。为了程序内部的一致性，该函数仅仅会返回简体中文小写的结果（`Nzh.cn.encodeS`）。如果没有特殊需要，请使用此函数处理相应场景。

### `isNumericStringBetween(str: string, from: number, to: number): boolean`

- **参数**
  - `str: string` 判断对象
  - `from: number` 起始值
  - `to: number` 结束值
- **返回值**：布尔

判断一个数字字符串（**须为整数**）是否在范围内，包含两端。例如 `isNumericString("1", 0, 10)` 会返回 `true`。

### `stringToBoolean(str: string): boolean`

- **不严格**
- **参数**
  - `str: string` 操作对象
- **返回值**：布尔

根据一个字符串的字面量，将其转换为合理的布尔值。目前仅支持将 `"1"` 或 `"true"`（不区分大小写）转换为布尔值。

### `fillArray<T>(array: Array<T>, value: T, length: number, overwrite?: boolean): Array<T>`

- **参数**
  - `array: Array<T>` 操作对象
  - `value: T` 填入值
  - `length: number` 填入数量
  - `overwrite?: boolean` 是否覆盖
- **返回值**：泛型数组

利用 `Array.prototype.fill` 方法向指定数组中填入相同的值。`length` 的大小应为正整数，如果填入了非正数会返回一个空数组。`overwrite` 的默认值为 `false`，如果指定为 `true` 将覆盖该数组先前的所有内容（将数组重初始化 `array = new Array<T>()`）。

### `getDuplicatedCount(array: Array<any>): Dictionary<any>`

- **不严格**
- **参数**
  - `array: Array<any>` 操作对象
- **返回值**：任意值词典

将一个任意值数组中重复的项目的数量整理为一个独立的对象（Object）返回。

需要注意的是，在统计过程中会**忽略数组元素的实际类型**，仅统计字面量。例如会将 `true` 和 `"true"` 同时归纳到结果对象中的 `true` key 中。

使用例：

```js
getDuplicatedCount([0, 0, 0, 1, 1, "2", "2", 2, true, "true"]);

// 返回值

{
    0: 3,
    1: 2,
    2: 3,
    true: 2
}
```

