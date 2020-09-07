# History

- **History.length** 返回一个整数，该整数表示会话历史中元素的数目，包括当前加载的页。例如，在一个新的选项卡加载的一个页面中，这个属性返回1。
- **History.back()** 前往上一页, 用户可点击浏览器左上角的返回按钮模拟此方法. 等价于 history.go(-1).**Note: 当浏览器会话历史记录处于第一页时调用此方法没有效果，而且也不会报错。**
- **History.forward()** 在浏览器历史记录里前往下一页，用户可点击浏览器左上角的前进按钮模拟此方法. 等价于 history.go(1).**Note: 当浏览器历史栈处于最顶端时( 当前页面处于最后一页时 )调用此方法没有效果也不报错。**
- **History.go()** 通过当前页面的相对位置从浏览器历史记录( 会话记录 )加载页面。比如：参数为-1的时候为上一页，参数为1的时候为下一页. 当整数参数超出界限时( 译者注:原文为When integerDelta is out of bounds )，例如: 如果当前页为第一页，前面已经没有页面了，我传参的值为-1，那么这个方法没有任何效果也不会报错。调用没有参数的 go() 方法或者不是整数的参数时也没有效果。( 这点与支持字符串作为url参数的IE有点不同)。

## pushState() 方法

pushState() 方法包含 3 个参数，简单说明如下：

- 状态对象。状态对象是一个 JavaScript 对象直接量，与调用 pushState() 方法创建的新历史记录条目相关联。无论何时用户导航到新创建的状态，popstate 事件都会被触发，并且事件对象的 state 属性都包含历史记录条目的状态对象的拷贝。
- 标题。可以传入一个简短的标题，标明将要进入的状态。FireFox 浏览器目前忽略该参数，考虑到未来可能会对该方法进行修改，传一个空字符串会比较安全。
- 可选参数。新的历史记录条目的地址。

浏览器不会在调用 pushState() 方法后加载该地址，如果不指定则为文档当前 URL。

调用 pushState() 方法类似于设置 window.location='#foo'，它们都会在当前文档内创建和激活新的历史记录条目。但 pushState() 有自己的优势。

- 新的 URL 可以是任意的同源 URL。相反，使用 window.location 方法时，只有仅修改 hash 才能保证停留在相同的 document 中。
- 根据个人需要决定是否修改 URL。相反，设置 window.location='#foo'，只有在当前 hash 值不是 foo 时才创建一条新的历史记录。
- 可以在新的历史记录条目中添加抽象数据。如果使用基于 hash 的方法，只能把相关数据转码成一个很短的字符串。

**pushState() 方法永远不会触发 hashchange 事件。**

## replaceState() 方法

history.replaceState() 与 history.pushState() 用法相同，都包含 3 个相同的参数。不同之处是：pushState() 是在 history 栈中添加一个新的条目，replaceState() 是替换当前的记录值。例如，history 栈中有两个栈块，一个标记为 1，另一个标记为 2，现在有第 3 个栈块，标记为 3。当执行 pushState() 时，栈块 3 将被添加栈中，栈就有 3 个栈块了；而当执行 replaceState() 时，将使用栈块 3 替换当前激活的栈块 2，history 的记录条数不变。也就是说，pushState() 会让 history 的数量加 1。

为了响应用户的某些操作，需要更新当前历史记录条目的状态对象或 URL 时，使用 replaceState() 方法会特别合适。
popstate 事件
每当激活的历史记录发生变化时，都会触发 popstate 事件。如果被激活的历史记录条目是由 pushState() 创建，或者是被 replaceState() 方法替换的，popstate 事件的状态属性将包含历史记录的状态对象的一个拷贝。

当浏览会话历史记录时，不管是单击浏览器工具栏中的“前进”或者“后退”按钮，还是使用 JavaScript 的 history.go() 和 history.back() 方法，popstate 事件都会被触发。
