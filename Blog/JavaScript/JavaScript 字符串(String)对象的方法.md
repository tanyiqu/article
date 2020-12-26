# JavaScript 字符串(String)对象的方法

### anchor()

描述：用于创建 HTML 锚

原型：```stringObject.anchor(anchorname)```

用法：

```html
<script>
    var txt="Hello world!"
    document.write(txt.anchor("myanchor"))
</script>
```

输出：

```
<a name="myanchor">Hello world!</a>
```

<br>

<br>

### big() 

描述：用于把字符串显示为大号字体

原型：```stringObject.big()```

用法：

```html
<script type="text/javascript">
    var str="Hello world!"
    document.write(str.big())
</script>
```

输出：

```
<big>Hello world!</big>
```

<br>

<br>

### blink()

描述：用于显示闪动的字符串。

原型：```stringObject.blink()```

用法：

```html
<script type="text/javascript">
    var str="Hello world!"
    document.write(str.blink())
</script>
```

输出：

```
<blink>Hello world!</blink>
```

<br>

<br>

### bold()

描述：用于把字符串显示为粗体。

原型：```stringObject.bold()```

用法：

```html
<script type="text/javascript">
    var str="Hello world!"
    document.write(str.bold())
</script>
```

输出：

```
<b>Hello world!</b>
```

<br>

<br>

### charAt()

描述：用于返回指定位置的字符

原型：```stringObject.charAt(index)```

| 参数  | 描述                                                       |
| :---- | :--------------------------------------------------------- |
| index | 必需。表示字符串中某个位置的数字，即字符在字符串中的下标。 |

用法：

```html
<script type="text/javascript">
    var str="Hello world!"
    document.write(str.charAt(1))
</script>
```

输出：

```
e
```

<br>

<br>

### charCodeAt()

描述：返回指定位置的字符的 Unicode 编码。这个返回值是 0 - 65535 之间的整数。

方法 charCodeAt() 与 charAt() 方法执行的操作相似，只不过前者返回的是位于指定位置的字符的编码，而后者返回的是字符子串。

原型：```stringObject.charCodeAt(index)```

| 参数  | 描述                                                       |
| :---- | :--------------------------------------------------------- |
| index | 必需。表示字符串中某个位置的数字，即字符在字符串中的下标。 |

用法：

```html
<script type="text/javascript">
    var str="Hello world!"
    console.log(str.charCodeAt(1))
</script>
```

输出：

```
101
```

<br>

<br>

### concat()

描述：用于连接两个或多个字符串。

原型：```stringObject.concat(stringX,stringX,...,stringX)```

| 参数    | 描述                                               |
| :------ | :------------------------------------------------- |
| stringX | 必需。将被连接为一个字符串的一个或多个字符串对象。 |

用法：

```html
<script type="text/javascript">
    var str1 = "Hello "
    var str2 = "world!"
    console.log(str1.concat(str2))
</script>
```

输出：

```
Hello world!
```

<br>

<br>

### fixed()

描述：用于把字符串显示为打字机字体

原型：```stringObject.fixed()```

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.fixed())
</script>
```

输出：

```
<tt>Hello world!</tt>
```

<br>

<br>

### fontcolor()

描述：用于按照指定的颜色来显示字符串。

原型：```stringObject.fontcolor(color)```

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| color | 必需。为字符串规定 font-color。该值必须是颜色名(red)、RGB 值(rgb(255,0,0))或者十六进制数 |

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.fontcolor("Red"))
</script>
```

输出：

```
<font color="Red">Hello world!</font>
```

<br>

<br>

### fontsize()

描述：用于按照指定的尺寸来显示字符串。

原型：```stringObject.fontsize(size)```

| 参数 | 描述          |
| :--- | :------------ |
| size | 1 至 7 的数字 |

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.fontsize(7))
</script>
```

输出：

```
<font size="7">Hello world!</font>
```

<br>

<br>

### fromCharCode()

描述：接受一个指定的 Unicode 值，然后返回一个字符串。

原型：```String.fromCharCode(numX,numX,...,numX)```

用法：

```html
<script type="text/javascript">
    console.log(String.fromCharCode(72, 69, 76, 76, 79))
    console.log(String.fromCharCode(65, 66, 67))
</script>
```

注释：该方法是 String 的静态方法，字符串中的每个字符都由单独的数字 Unicode 编码指定。

它不能作为您已创建的 String 对象的方法来使用。因此它的语法应该是 String.fromCharCode()，而不是 myStringObject.fromCharCode()。

| 参数 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| numX | 必需。一个或多个 Unicode 值，即要创建的字符串中的字符的 Unicode 编码。 |

输出：

```
HELLO
ABC
```

<br>

<br>

### indexOf()

描述：返回某个指定的字符串值在字符串中首次出现的位置。

原型：```stringObject.indexOf(searchvalue,fromindex)```

| 参数        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| searchvalue | 必需。规定需检索的字符串值。                                 |
| fromindex   | 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 stringObject.length - 1。如省略该参数，则将从字符串的首字符开始检索。 |

说明：该方法将从头到尾地检索字符串 stringObject，看它是否含有子串 searchvalue。开始检索的位置在字符串的 fromindex 处或字符串的开头（没有指定 fromindex 时）。如果找到一个 searchvalue，则返回 searchvalue 的第一次出现的位置。stringObject 中的字符位置是从 0 开始的。

注释：indexOf() 方法对大小写敏感！如果要检索的字符串值没有出现，则该方法返回 -1。

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    console.log(str.indexOf("Hello"))
    console.log(str.indexOf("World"))
    console.log(str.indexOf("world"))
</script>
```

输出：

```
0
-1
6
```

<br>

<br>

### italics()

描述：用于把字符串显示为斜体。

原型：```stringObject.italics()```

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.italics())
</script>
```

输出：

```
<i>Hello world!</i>
```

<br>

<br>

### lastIndexOf()

描述：返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。

原型：```stringObject.lastIndexOf(searchvalue,fromindex)```

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| *searchvalue* | 必需。规定需检索的字符串值。                                 |
| *fromindex*   | 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 *stringObject*.length - 1。如省略该参数，则将从字符串的最后一个字符处开始检索。 |

返回值：如果在 *stringObject* 中的 *fromindex* 位置之前存在 *searchvalue*，则返回的是出现的最后一个 *searchvalue* 的位置。

说明：该方法将从尾到头地检索字符串 *stringObject*，看它是否含有子串 *searchvalue*。开始检索的位置在字符串的 *fromindex* 处或字符串的结尾（没有指定 *fromindex* 时）。如果找到一个 *searchvalue*，则返回 *searchvalue* 的第一个字符在 *stringObject* 中的位置。*stringObject* 中的字符位置是从 0 开始的。

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    console.log(str.lastIndexOf("Hello"))
    console.log(str.lastIndexOf("World"))
    console.log(str.lastIndexOf("world"))
</script>
```

输出：

```
0
-1
6
```

<br>

<br>

### link()

描述：用于把字符串显示为超链接。

原型：```stringObject.link(url)```

| 参数 | 描述                     |
| :--- | :----------------------- |
| url  | 必需。规定要链接的 URL。 |

用法：

```html
<script type="text/javascript">
    var str = "Free Web Tutorials!"
    document.write(str.link("http://www.w3school.com.cn"))
</script>
```

输出：

```
<a href="http://www.w3school.com.cn">Free Web Tutorials!</a>
```

<br>

<br>

### localeCompare()

描述：用本地特定的顺序来比较两个字符串。

原型：```stringObject.localeCompare(target)```

| 参数   | 描述                                                 |
| :----- | :--------------------------------------------------- |
| target | 要以本地特定的顺序与 stringObject 进行比较的字符串。 |

用法：

```html
<script type="text/javascript">
    var str1 = '123456'
    var str2 = 'abcdef'
    console.log(str1.localeCompare(str2));
</script>
```

输出：

```
-1
```

<br>

<br>

### match()

描述：用于在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。

该方法类似 indexOf() 和 lastIndexOf()，但是它返回指定的值，而不是字符串的位置。

原型：

```stringObject.match(searchvalue)```

```stringObject.match(regexp)```

| 参数        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| searchvalue | 必需。规定要检索的字符串值。                                 |
| regexp      | 必需。规定要匹配的模式的 RegExp 对象。如果该参数不是 RegExp 对象，则需要首先把它传递给 RegExp 构造函数，将其转换为 RegExp 对象。 |

返回值：存放匹配结果的数组。该数组的内容依赖于 regexp 是否具有全局标志 g。

说明：match() 方法将检索字符串 stringObject，以找到一个或多个与 regexp 匹配的文本。这个方法的行为在很大程度上有赖于 regexp 是否具有标志 g。

如果 regexp 没有标志 g，那么 match() 方法就只能在 stringObject 中执行一次匹配。如果没有找到任何匹配的文本， match() 将返回 null。否则，它将返回一个数组，其中存放了与它找到的匹配文本有关的信息。该数组的第 0 个元素存放的是匹配文本，而其余的元素存放的是与正则表达式的子表达式匹配的文本。除了这些常规的数组元素之外，返回的数组还含有两个对象属性。index 属性声明的是匹配文本的起始字符在 stringObject 中的位置，input 属性声明的是对 stringObject 的引用。

如果 regexp 具有标志 g，则 match() 方法将执行全局检索，找到 stringObject 中的所有匹配子字符串。若没有找到任何匹配的子串，则返回 null。如果找到了一个或多个匹配子串，则返回一个数组。不过全局匹配返回的数组的内容与前者大不相同，它的数组元素中存放的是 stringObject 中所有的匹配子串，而且也没有 index 属性或 input 属性。

注意：在全局检索模式下，match() 即不提供与子表达式匹配的文本的信息，也不声明每个匹配子串的位置。如果您需要这些全局检索的信息，可以使用 RegExp.exec()。

用法1：

```html
<script type="text/javascript">
    var str = "Hello world!"
    console.log(str.match("world"))
    console.log(str.match("World"))
    console.log(str.match("worlld"))
    console.log(str.match("world!"))
</script>
```

输出1：

```
["world", index: 6, input: "Hello world!", groups: undefined]
null
null
["world!", index: 6, input: "Hello world!", groups: undefined]
```



用法2：

```html
<script type="text/javascript">
    var str = "1 plus 2 equal 3"
    console.log(str.match(/\d+/g))
</script>
```

输出2：

```
["1", "2", "3"]
```

<br>

<br>

### replace()

描述：用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。

原型：```stringObject.replace(regexp/substr,replacement)```

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| regexp/substr | 必需。规定子字符串或要替换的模式的 RegExp 对象。请注意，如果该值是一个字符串，则将它作为要检索的直接量文本模式，而不是首先被转换为 RegExp 对象。 |
| replacement   | 必需。一个字符串值。规定了替换文本或生成替换文本的函数。     |

用法1：

```html
<script type="text/javascript">
    var str = "Visit Microsoft!"
    document.write(str.replace(/Microsoft/, "W3School"))
</script>
```

输出1：

```
Visit W3School!
```



用法2：

```html
<script type="text/javascript">
    var str = "Welcome to Microsoft! "
    str = str + "We are proud to announce that Microsoft has "
    str = str + "one of the largest Web Developers sites in the world."
    document.write(str.replace(/Microsoft/g, "W3School"))
</script>
```

输出2：

```
Welcome to W3School! We are proud to announce that W3School has one of the largest Web Developers sites in the world.
```

<br>

<br>

### search()

描述：用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串。

原型：```stringObject.search(regexp)```

| 参数   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| regexp | 该参数可以是需要在 stringObject 中检索的子串，也可以是需要检索的 RegExp 对象。注释：要执行忽略大小写的检索，请追加标志 i。 |

用法1：

```html
<script type="text/javascript">
    var str = "Visit W3School!"
    document.write(str.search(/W3School/))
</script>
```

输出1：

```
6
```



用法2：

```html
<script type="text/javascript">
    var str = "Visit W3School!"
    document.write(str.search(/w3school/i))
</script>
```

输出2：

```
6
```

<br>

<br>

### slice()

描述：提取字符串的某个部分，并以新的字符串返回被提取的部分。

原型：```stringObject.slice(start,end)```

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| start | 要抽取的片断的起始下标。如果是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推。 |
| end   | 紧接着要抽取的片段的结尾的下标。若未指定此参数，则要提取的子串包括 start 到原字符串结尾的字符串。如果该参数是负数，那么它规定的是从字符串的尾部开始算起的位置。 |

返回值：一个新的字符串。包括字符串 stringObject 从 start 开始（包括 start）到 end 结束（不包括 end）为止的所有字符。

说明：String 对象的方法 slice()、substring() 和 substr() （不建议使用）都可返回字符串的指定部分。slice() 比 substring() 要灵活一些，因为它允许使用负数作为参数。slice() 与 substr() 有所不同，因为它用两个字符的位置来指定子串，而 substr() 则用字符位置和长度来指定子串。

还要注意的是，String.slice() 与 Array.slice() 相似。

用法：

```html
<script type="text/javascript">
    var str = "Hello happy world!"
    console.log(str.slice(6))
    console.log(str.slice(6, 11))
</script>
```

输出：

```
happy world!
happy
```

<br>

<br>

### small()

描述：用于把字符串显示为小号字。

原型：```stringObject.small()```

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.small())
</script>
```

输出：

```
<small>Hello world!</small>xxxxxxxxxx <small>Hello world!</small>e
```

<br>

<br>

### split()

描述：用于把一个字符串分割成字符串数组。

原型：```stringObject.split(separator,howmany)```

| 参数      | 描述                                                         |
| :-------- | :----------------------------------------------------------- |
| separator | 必需。字符串或正则表达式，从该参数指定的地方分割 stringObject。 |
| howmany   | 可选。该参数可指定返回的数组的最大长度。如果设置了该参数，返回的子串不会多于这个参数指定的数组。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。 |

返回值：一个字符串数组。该数组是通过在 *separator* 指定的边界处将字符串 stringObject 分割成子串创建的。返回的数组中的字串不包括 *separator* 自身。

但是，如果 *separator* 是包含子表达式的正则表达式，那么返回的数组中包括与这些子表达式匹配的字串（但不包括与整个正则表达式匹配的文本）。

注释：如果把空字符串 ("") 用作 *separator*，那么 stringObject 中的每个字符之间都会被分割。String.split() 执行的操作与 [Array.join](https://www.w3school.com.cn/jsref/jsref_join.asp) 执行的操作是相反的。

用法：

```html
<script type="text/javascript">
    var str = "How are you doing today?"
    console.log(str.split(" "))
    console.log(str.split(""))
    console.log(str.split(" ", 3))
</script>
```

输出：

```
["How", "are", "you", "doing", "today?"]
["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "d", "o", "i", "n", "g", " ", "t", "o", "d", "a", "y", "?"]
["How", "are", "you"]
```

<br>

<br>

### strike()

描述：用于显示加删除线的字符串。

原型：```stringObject.strike()```

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.strike())
</script>
```

输出：

```
<strike>Hello world!</strike>
```

<br>

<br>

### sub()

描述：用于把字符串显示为下标。

原型：```stringObject.sub()```

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    document.write(str.sub())
</script>
```

输出：

```
<sub>Hello world!</sub>
```

<br>

<br>

### substr()

描述：在字符串中抽取从 *start* 下标开始的指定数目的字符。

原型：```stringObject.substr(start,length)```

| 参数     | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| *start*  | 必需。要抽取的子串的起始下标。必须是数值。如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。 |
| *length* | 可选。子串中的字符数。必须是数值。如果省略了该参数，那么返回从 *stringObject* 的开始位置到结尾的字串。 |

返回值：一个新的字符串，包含从 *stringObject* 的 *start*（包括 start 所指的字符） 处开始的 *length* 个字符。如果没有指定 *length*，那么返回的字符串包含从 *start* 到 *stringObject* 的结尾的字符。

注释：substr() 的参数指定的是子串的开始位置和长度，因此它可以替代 substring() 和 slice() 来使用。

重要事项：ECMAscript 没有对该方法进行标准化，因此反对使用它。

重要事项：在 IE 4 中，参数 *start* 的值无效。在这个 BUG 中，*start* 规定的是第 0 个字符的位置。在之后的版本中，此 BUG 已被修正。

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    console.log(str.substr(3))
    console.log(str.substr(3, 7))
</script>
```

输出：

```
lo world!
lo worl
```

<br>

<br>

### substring()

描述：用于提取字符串中介于两个指定下标之间的字符。

原型：```1111111111```

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| *start* | 必需。一个非负的整数，规定要提取的子串的第一个字符在 stringObject 中的位置。 |
| *stop*  | 可选。一个非负的整数，比要提取的子串的最后一个字符在 stringObject 中的位置多 1。如果省略该参数，那么返回的子串会一直到字符串的结尾。 |

返回值：一个新的字符串，该字符串值包含 *stringObject* 的一个子字符串，其内容是从 *start* 处到 *stop*-1 处的所有字符，其长度为 *stop* 减 *start*。

说明：substring() 方法返回的子串包括 *start* 处的字符，但不包括 *stop* 处的字符。

如果参数 *start* 与 *stop* 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。如果 *start* 比 *stop* 大，那么该方法在提取子串之前会先交换这两个参数。

重要事项：与 slice() 和 substr()方法不同的是，substring() 不接受负的参数。

用法：

```html
<script type="text/javascript">
    var str = "Hello world!"
    console.log(str.substring(3))
    console.log(str.substring(3, 7))
</script>
```

输出：

```
lo world!
lo w
```

<br>

<br>

### toLocaleLowerCase()

描述：用于把字符串转换为小写。

原型：```stringObject.toLocaleLowerCase()```

返回值：一个新的字符串，在其中 stringObject 的所有大写字符全部被转换为了小写字符。

说明：与 toLowerCase() 不同的是，toLocaleLowerCase() 方法按照本地方式把字符串转换为小写。只有几种语言（如土耳其语）具有地方特有的大小写映射，所有该方法的返回值通常与 toLowerCase() 一样。

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.toLocaleLowerCase())
</script>
```

输出：

```
hello world!
```

<br>

<br>

### toLocaleUpperCase()

描述：用于把字符串转换为大写。

原型：```stringObject.toLocaleUpperCase()```

返回值：一个新的字符串，在其中 stringObject 的所有小写字符全部被转换为了大写字符。

说明：与 toUpperCase() 不同的是，toLocaleUpperCase() 方法按照本地方式把字符串转换为大写。只有几种语言（如土耳其语）具有地方特有的大小写映射，所有该方法的返回值通常与 toUpperCase() 一样。

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.toLocaleUpperCase())
</script>
```

输出：

```
HELLO WORLD!
```

<br>

<br>

### toLowerCase()

描述：用于把字符串转换为小写。

原型：```stringObject.toLowerCase()```

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.toLowerCase())
</script>
```

输出：

```
hello world!
```

<br>

<br>

### toUpperCase()

描述：用于把字符串转换为大写。

原型：```stringObject.toUpperCase()```

返回值：一个新的字符串，在其中 stringObject 的所有小写字符全部被转换为了大写字符。

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.toUpperCase())
</script>
```

输出：

```
HELLO WORLD!
```

<br>

<br>

### toString()

描述：toString() 方法返回字符串。

原型：```stringObject.toString()```

返回值：stringObject 的原始字符串值。一般不会调用该方法。

抛出：当调用该方法的对象不是 String 时抛出 TypeError 异常。

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.toString())
</script>
```

输出：

```
Hello World!
```

<br>

<br>

### valueOf()

描述：valueOf() 方法可返回 String 对象的原始值。

原始值是由从 String 对象下来的所有对象继承的。

valueOf() 方法通常由 JavaScript 在后台自动进行调用，而不是显式地处于代码中。

原型：```stringObject.valueOf()```

用法：

```html
<script type="text/javascript">
    var str = "Hello World!"
    console.log(str.valueOf())
</script>
```

输出：

```
Hello World!
```

<br>

<br>

整理自：https://www.w3school.com.cn/jsref/jsref_match.asp