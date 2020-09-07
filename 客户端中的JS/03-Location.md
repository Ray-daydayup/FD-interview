# location对象

location 对象存储了当前文档位置（URL）相关的信息，简单地说就是网页地址字符串。使用 window 对象的 location 属性可以访问。

location 对象定义了 8 个属性，其中 7 个属性可以获取当前 URL 的各部分信息，另一个属性（href）包含了完整的 URL 信息，详细说明如下表所示。为了便于更直观的理解，下表中各个属性将以下面 URL 示例信息为参考进行说明。

- **href**:声明了当前显示文档的完整 URL，与其他 location 属性只声明部分 URL 不同，把该属性设置为新的 URL 会使浏览器读取并显示新 URL 的内容
- **protocol**:声明了 URL 的协议部分，包括后缀的冒号。例如：“http:”
- **host**:声明了当前 URL 中的主机名和端口部分。例如：“www.123.cn:80”
- **hostname**:声明了当前 URL 中的主机名。例如：“www.123.cn”
- **port**:声明了当前 URL 的端口部分。例如：“80”
- **pathname**:声明了当前 URL的路径部分。例如：“news/index.asp”
- **search**:声明了当前 URL 的查询部分，包括前导问号。例如：“?id=123&name=location”
- **hash**:声明了当前 URL 中锚部分，包括前导符（#）。例如：“#top”,指定在文档中锚记的名称

location 对象还定义了两个方法：reload() 和 replace()。

- reload()：可以重新装载当前文档。
- replace()：可以装载一个新文档而无须为它创建一个新的历史记录。也就是说，在浏览器的历史列表中，新文档将替换当前文档。这样在浏览器中就不能通过单击“返回”按钮返回当前的文档。
- 对那些使用了框架并且显示多个临时页的网站来说，replace() 方法比较有用。这样临时页面都不被存储在历史列表中。

window.location 与 document.location 不同，前者引用 location 对象，后者只是一个只读字符串，与 document.URL 同义。但是，当存在服务器重定向时，document.location 包含的是已经装载的 URL，而 location.href 包含的则是原始请求文档的 URL。
