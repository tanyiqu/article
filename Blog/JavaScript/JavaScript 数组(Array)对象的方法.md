# JavaScript 数组(Array)对象的方法

### concat()

描述：用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

原型：```arrayObject.concat(arrayX,arrayX,......,arrayX)```

| 参数   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| arrayX | 必需。该参数可以是具体的值，也可以是数组对象。可以是任意多个。 |

返回值：返回一个新的数组。该数组是通过把所有 arrayX 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的元素，而不是数组。

用法：

```html
<script type="text/javascript">
    var a = [1, 2, 3];
    console.log(a.concat(4, 5));
</script>
```

输出：

```
[1, 2, 3, 4, 5]
```

<br>

### join()

描述：用于用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的。

原型：```arrayObject.join(separator)```

| 参数      | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| separator | 可选。指定要使用的分隔符。如果省略该参数，则使用逗号作为分隔符。 |

返回值：返回一个字符串。该字符串是通过把 arrayObject 的每个元素转换为字符串，然后把这些字符串连接起来，在两个元素之间插入 *separator* 字符串而生成的。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr.join());
</script>
```

输出：

```
George,John,Thomas
George.John.Thomas
```

<br>

### pop()

描述：用于删除并返回数组的最后一个元素。

原型：```arrayObject.pop()```

返回值：arrayObject 的最后一个元素。

说明：pop() 方法将删除 arrayObject 的最后一个元素，把数组长度减 1，并且返回它删除的元素的值。如果数组已经为空，则 pop() 不改变数组，并返回 undefined 值

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.pop())
    console.log(arr)
</script>
```

输出：

```
["George", "John", "Thomas"]
Thomas
["George", "John"]
```

<br>

### push()

描述：向数组的末尾添加一个或多个元素，并返回新的长度。

原型：```arrayObject.push(newelement1,newelement2,....,newelementX)```

| 参数        | 描述                             |
| :---------- | :------------------------------- |
| newelement1 | 必需。要添加到数组的第一个元素。 |
| newelement2 | 可选。要添加到数组的第二个元素。 |
| newelementX | 可选。可添加多个元素。           |

返回值：把指定的值添加到数组后的新长度。

说明：push() 方法可把它的参数顺序添加到 arrayObject 的尾部。它直接修改 arrayObject，而不是创建一个新的数组。push() 方法和 pop() 方法使用数组提供的先进后出栈的功能。

注释：该方法会改变数组的长度。

提示：要想数组的开头添加一个或多个元素，请使用 unshift() 方法。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.push("James"))
    console.log(arr)
</script>
```

输出：

```
["George", "John", "Thomas"]
4
["George", "John", "Thomas", "James"]
```

<br>

### reverse()

描述：用于颠倒数组中元素的顺序。

原型：```arrayObject.reverse()```

注释：该方法会改变原来的数组，而不会创建新的数组。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.reverse())
</script>
```

输出：

```
["George", "John", "Thomas"]
["Thomas", "John", "George"]
```

<br>

### shift()

描述：用于把数组的第一个元素从其中删除，并返回第一个元素的值。

原型：```arrayObject.shift()```

返回值：数组原来的第一个元素的值。

说明：如果数组是空的，那么 shift() 方法将不进行任何操作，返回 undefined 值。请注意，该方法不创建新数组，而是直接修改原有的 arrayObject。

注释：该方法会改变数组的长度。

提示：要删除并返回数组的最后一个元素，请使用 pop() 方法。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.shift())
    console.log(arr)
</script>
```

输出：

```
["George", "John", "Thomas"]
George
["John", "Thomas"]
```

<br>

### slice()

描述：从已有的数组中返回选定的元素。

原型：```arrayObject.slice(start,end)```

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| start | 必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。 |
| end   | 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。 |

返回值：返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。

说明：请注意，该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。

注释：您可使用负值从数组的尾部选取元素。如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.slice(1))
    console.log(arr.slice(2, 4))
</script>
```

输出：

```
["George", "John", "Thomas"]
["John", "Thomas"]
["Thomas"]
```

<br>

### sort()

描述：用于对数组的元素进行排序。

原型：```arrayObject.sort(sortby)```

| 参数     | 描述                             |
| :------- | :------------------------------- |
| *sortby* | 可选。规定排序顺序。必须是函数。 |

返回值：对数组的引用。请注意，数组在原数组上进行排序，不生成副本。

说明：

如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。要实现这一点，首先应把数组的元素都转换成字符串（如有必要），以便进行比较。

如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

- 若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
- 若 a 等于 b，则返回 0。
- 若 a 大于 b，则返回一个大于 0 的值。

用法1：

```html
<script type="text/javascript">
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    console.log(arr)
    console.log(arr.sort())
</script>
```

输出1：

```
["George", "John", "Thomas", "James", "Adrew", "Martin"]
["Adrew", "George", "James", "John", "Martin", "Thomas"]
```



用法2：

```html
<script type="text/javascript">
    var arr = new Array(6)
    arr[0] = "10"
    arr[1] = "5"
    arr[2] = "40"
    arr[3] = "25"
    arr[4] = "1000"
    arr[5] = "1"
    console.log(arr)
    console.log(arr.sort())
</script>
```

输出2：

```
["10", "5", "40", "25", "1000", "1"]
["1", "10", "1000", "25", "40", "5"]
```



用法3：

```html
<script type="text/javascript">
    function sortNumber(a, b) {
        return a - b
    }
    var arr = new Array(6)
    arr[0] = "10"
    arr[1] = "5"
    arr[2] = "40"
    arr[3] = "25"
    arr[4] = "1000"
    arr[5] = "1"
    console.log(arr)
    console.log(arr.sort(sortNumber))
</script>
```

输出3：

```
["10", "5", "40", "25", "1000", "1"]
["1", "5", "10", "25", "40", "1000"]
```

<br>

### splice()

描述：/从数组中添加/删除项目，然后返回被删除的项目。

原型：```arrayObject.splice(index,howmany,item1,.....,itemX)```

| 参数              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
| howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。       |
| item1, ..., itemX | 可选。向数组添加的新项目。                                   |

注释：该方法会改变原始数组。

返回值：

| 类型  | 描述                                 |
| :---- | :----------------------------------- |
| Array | 包含被删除项目的新数组，如果有的话。 |

说明：splice() 方法可删除从 index 处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。

如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。

用法1：

```html
<script type="text/javascript">
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    console.log(arr)
    arr.splice(2, 0, "William")
    console.log(arr)
    // 从第2个位置，删除0个元素，添加一个"William"
</script>
```

输出1：

```
["George", "John", "Thomas", "James", "Adrew", "Martin"]
["George", "John", "William", "Thomas", "James", "Adrew", "Martin"]
```



用法2：

```html
<script type="text/javascript">
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    console.log(arr)
    arr.splice(2, 1, "William")
    console.log(arr)
    // 从第2个位置，删除1个元素，添加一个"William"
</script>
```

输出2：

```
["George", "John", "Thomas", "James", "Adrew", "Martin"]
["George", "John", "William", "James", "Adrew", "Martin"]
```



用法3：

```html
<script type="text/javascript">
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    console.log(arr)
    arr.splice(2, 3, "William")
    console.log(arr)
    // 从第2个位置，删除3个元素，添加一个"William"
</script>
```

输出3：

```
["George", "John", "Thomas", "James", "Adrew", "Martin"]
["George", "John", "William", "Martin"]
```

<br>

### toString()

描述：把数组转换为字符串，并返回结果。

原型：```arrayObject.toString()```

返回值：arrayObject 的字符串表示。返回值与没有参数的 join() 方法返回的字符串相同。

说明：当数组用于字符串环境时，JavaScript 会调用这一方法将数组自动转换成字符串。但是在某些情况下，需要显式地调用该方法。

注释：数组中的元素之间用逗号分隔。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr.toString())
</script>
```

输出：

```
George,John,Thomas
```

<br>

### toLocaleString()

描述：把数组转换为本地字符串。

原型：```arrayObject.toLocaleString()```

返回值：arrayObject 的本地字符串表示。

说明：首先调用每个数组元素的 toLocaleString() 方法，然后使用地区特定的分隔符把生成的字符串连接起来，形成一个字符串。

用法：

```html
<script type="text/javascript">
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr.toLocaleString())
</script>
```

输出：

```
George, John, Thomas
```

<br>

### unshift()

描述：向数组的开头添加一个或更多元素，并返回新的长度。

原型：```arrayObject.unshift(newelement1,newelement2,....,newelementX)```

返回值：arrayObject 的新长度。

说明：unshift() 方法将把它的参数插入 arrayObject 的头部，并将已经存在的元素顺次地移到较高的下标处，以便留出空间。该方法的第一个参数将成为数组的新元素 0，如果还有第二个参数，它将成为新的元素 1，以此类推。

请注意，unshift() 方法不创建新的创建，而是直接修改原有的数组。

注释：该方法会改变数组的长度。

注意：unshift() 方法无法在 Internet Explorer 中正确地工作！

提示：要把一个或多个元素添加到数组的尾部，请使用 push() 方法。

用法：

```html
<script type="text/javascript">
    var arr = new Array()
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr)
    console.log(arr.unshift("William"))
    console.log(arr)
</script>
```

输出：

```
["George", "John", "Thomas"]
4
["William", "George", "John", "Thomas"]
```

<br>

### valueOf()

描述：valueOf() 方法返回 Array 对象的原始值。该原始值由 Array 对象派生的所有对象继承。valueOf() 方法通常由 JavaScript 在后台自动调用，并不显式地出现在代码中。

原型：```arrayObject.valueOf()```

用法：

```html
<script type="text/javascript">
    var arr = new Array()
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    console.log(arr.valueOf())
</script>
```

输出：

```
["George", "John", "Thomas"]
```

