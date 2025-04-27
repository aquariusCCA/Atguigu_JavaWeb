# XML

![](E:\JavaWeb\筆記\images\1681452257379.png)

> Extendsible Markup Language（可扩展标记语言）由 W3C 組織發布，目前推薦遵守的是 W3C 組織於 2000 發布的 XML1.0 規範。
>
> - XML 和 HTML一样都是标记语言，也就是说它们的基本语法都是标签。
>
> - 可擴展的意思 : 也就是這些標籤並不是 HTML 裡面所定義的，而是我們自己所寫的。

+ **可扩展** 三个字表面上的意思是 XML 允许自定义格式。但这不代表你可以随便写。

+ 在 XML 基本语法规范的基础上，你使用的那些第三方应用程序、框架会通过 XML 约束的方式强制规定配置文件中可以写什么和怎么写

+ XML 基本语法这个知识点的定位是：我们不需要从零开始，从头到尾的一行一行编写 XML 文档，而是在第三方应用程序、框架已提供的配置文件的基础上修改。要改成什么样取决于你的需求，而怎么改取决 XML 基本语法和具体的 XML 约束。

- XML 的使命，就是**以一個統一的格式，組織有關係的數據，為不同平台下的應用程序服務**。

- 我们不同的平台有他自己的数据格式，但是不同平台之间如果相互想传递数据，那么就应该用同一种数据格式，这样大家都能读懂。就像加入 WTO 组织的各个国家一样。每个国家都有自己的语言和货币，但是如果大家都用自己的东西就很难沟通和衡量那么我们就使用统一的方式，使用英语作为交流语言，使用美元作为货币标准。

<img src="E:\JavaWeb\筆記\images\螢幕擷取畫面 2024-04-30 141458.png" style="zoom:50%;" />

- 主要用途 : XML 就是一種數據保存的格式而已，按照他的規則你就知道數據之間的歸系。XML 經常用在下面的情況之中。
  - 配置文件 
  - 數據交換 (**現在以 JSON 為主**)
  - 數據存儲
  - 保存關係型數據

**为什么我们要使用 XML 保存数据呢 ?** 

因为有些数据是不会经常变化的数据，我们需要固定的保存起来，然而这些数据又是有某些关系的。我们希望也把他们直接的关系用简明易懂的格式保存起来，方便后来查看这些数据的时候一下就能看懂他们直接的关系。

# 常见配置文件类型

1.  properties 文件 : 例如 druid 连接池就是使用 properties 文件作为配置文件
2.  XML 文件 : 例如 Tomcat 就是使用 XML 文件作为配置文件
3.  YAML 文件 : 例如 SpringBoot 就是使用 YAML 作为配置文件
4.  json 文件 : 通常用来做文件传输，也可以用来做前端或者移动端的配置文件
5.  等等...

## properties 配置文件

**示例 :**

```properties
atguigu.jdbc.url=jdbc:mysql://localhost:3306/atguigu
atguigu.jdbc.driver=com.mysql.cj.jdbc.Driver
atguigu.jdbc.username=root
atguigu.jdbc.password=root
```

- 语法规范
  - 由键值对组成
  - 键和值之间的符号是等号
  - 每一行都必须顶格写，前面不能有空格之类的其他符号

## xml 配置文件

**示例 :**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<students>
    <student>
        <name>张三</name>
        <age>18</age>
    </student>
    <student>
        <name>李四</name>
        <age>20</age>
    </student>
</students>
```

# XML的基本语法

+ XML 的基本语法和 HTML 的基本语法简直如出一辙。其实这不是偶然的，XML 基本语法 + HTML 约束 = HTML语法。在逻辑上 HTML 确实是 XML 的子集。

- XML 文档声明 : 这部分基本上就是固定格式，要注意的是文档声明一定要从第一行第一列开始写

  - ```xml
    <!-- 
    1. version 是版本号
    2. encoding 是 xml 的文件编码
    3. 注意 `<?xml` 要连在一起写，否则会有报错，錯誤寫法 : `< ?xml`
    -->
    <?xml version="1.0" encoding="UTF-8"?>
    ```

-   根标签
    
    -   &#x20;根标签有且只能有一个。
-   标签关闭
    -   双标签：开始标签和结束标签必须成对出现。
    -   单标签：单标签在标签内关闭。
-   标签嵌套
    
    -   可以嵌套，但是不能交叉嵌套。
-   注释不能嵌套
-   标签名、属性名建议使用小写字母
-   属性
    -   属性必须有值
    -   属性值必须加引号，单双都行

**範例**

```xml
<!-- xml声明 version是版本的意思   encoding是编码  -->
<?xml version="1.0" encoding="utf-8" ?>

<!-- books 表示多個圖書訊息 -->
<books> <!-- 这是xml注释 -->
    <book id="SN123123413241"> <!-- book标签描述一本图书   id属性描述 的是图书 的编号  -->
        <name>java编程思想</name> <!-- name标签描述 的是图书 的信息 -->
        <author>华仔</author>		<!-- author单词是作者的意思 ，描述图书作者 -->
        <price>9.9</price>		<!-- price单词是价格，描述的是图书 的价格 -->
    </book>
    
    <book id="SN12341235123">	<!-- book标签描述一本图书   id属性描述 的是图书 的编号  -->
        <name>葵花宝典</name>	<!-- name标签描述 的是图书 的信息 -->
        <author>班长</author>	<!-- author单词是作者的意思 ，描述图书作者 -->
        <price>5.5</price>	<!-- price单词是价格，描述的是图书 的价格 -->
    </book>
</books>
```

# XML 規則

- 標籤名不能包含空格
  - ![](E:\JavaWeb\筆記\images\標籤名不能包含空格.png)

- 雙標籤和單標籤
  - ![](E:\JavaWeb\筆記\images\雙標籤和單標籤.png)
- XML屬性必須用引號引起來
  - ![](E:\JavaWeb\筆記\images\XML屬性必須用引號引起來.png)
- XML標籤一定要閉合
  - ![](E:\JavaWeb\筆記\images\XML標籤一定要閉合.png)
- 標籤大小寫敏感
  - ![](E:\JavaWeb\筆記\images\標籤大小寫敏感.png)
- 標籤閉合位置不正確
  - ![](E:\JavaWeb\筆記\images\標籤閉合位置不正確.png)
- 根元素
  - 根元素就是頂級元素，沒有父標籤的元素叫頂級元素；根元素是沒有父標籤的頂級元素，而且是唯一一個才行。
  - ![](E:\JavaWeb\筆記\images\根元素.png)
- 特殊字符
  - ![](E:\JavaWeb\筆記\images\特殊字符.png)
- 不能以數字打頭
  - ![](E:\JavaWeb\筆記\images\不能以數字打頭.png)

# 文本区域（CDATA 区）

> CDATA 语法可以告诉 xml 解析器，我 CDATA 里的文本内容只是纯文本，不需要 xml 语法解析。

- 語法格式 : 

  - ```XML
    <![CDATA[這裡可以把你輸入的字符原樣顯示，不會被解析]]>
    ```

![](E:\JavaWeb\筆記\images\文本区域.png)

# XML的约束 (稍微了解)

- [xml约束的概念](https://www.cnblogs.com/cplinux/p/9734688.htmlhttps://www.cnblogs.com/cplinux/p/9734688.html)
- [XML 约束](https://cloud.tencent.com/developer/article/2343201)

> 一个 XML 文档一旦有了约束，那么这个 XML 文档就只能使用约束中创建的元素及属性。
>
> 如果约束没有创建 `<a>` 元素，那么 XML 文档就不能使用 `<a>` 元素。

XML 有两种约束：DTD 和 Schema，这二者都是用来描述 XML 文档结构，限定文档的数据类型的， 只是做法上不一样。

DTD 和 XML Schema 之间的关键区别在于 XML Schema 使用基于 XML 的语法，而 DTD 具有从 SGML DTD 保留的独特语法。虽然 DTD 经常因为需要学习新的语法而受到批评，但语法本身非常简洁。XML Schema 则相反，它很冗长，但也使用标签和 XML，因此 XML 的作者应该发现 XML Schema 的语法不那么令人生畏。

## DTD 约束

>DTD : 文档类型定义（Document Type Definition）是一套关于标记符的语法规则。

DTD 主要分为内部定义和外部定义：

内部 DTD 的定义，需要在顶部加入，语法如下:

```xml-dtd
<!DOCTYPE 根元素 [元素声明]>
```

### （一）把 dtd 约束直接写到 xml 文档中

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE users[
    <!ELEMENT users (user+) >    
    <!ELEMENT user (name,age,addr) >    
    <!ELEMENT name (#PCDATA) >    
    <!ELEMENT age (#PCDATA) >    
    <!ELEMENT addr (#PCDATA) >    
]>
<users>
    <user>
        <name>zhangsan</name>
        <age>23</age>
        <addr>shanghai</addr>
    </user>
    <user>
        <name>lisi</name>
        <age>24</age>
        <addr>beijing</addr>
    </user>
</users>
```

### （二）在 xml 文档中引用一个外部的 dtd 约束文档(dtd约束文档以.dtd作用扩展名)，

- 外部引用又包括两种
  - 一种是 SYSTEM 系统外部约束文档，也就是 xml 文档和 dtd 约束文档都在同一台机器上，
  - 一种是 PUBLIC 公共外部约束文档，也就是 xml 文档和 dtd 约束文档不在同一台机器上，需要通过网络把dtd 文档下载到本地

**引用形式如下 :**

```xml
<!DOCTYPE 根元素 SYSTEM "dtd文件路径">
<!DOCTYPE 根元素 PUBLIC "dtd文件的描述信息" "dtd的url">
```

**SYSTEM 系统外部约束文档示例**

**note.dtd**

```xml-dtd
<?xml version="1.0" encoding="UTF-8"?>
<!ELEMENT note (to,from,heading,body) >    
<!ELEMENT to (#PCDATA) >    
<!ELEMENT from (#PCDATA) >    
<!ELEMENT heading (#PCDATA) >    
<!ELEMENT body (#PCDATA) >    
```

**note.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE note SYSTEM "note.dtd">
<note>
	<to>Tove</to>
	<from>Jani</from>
	<heading>Reminder</heading>
	<body>Don't forget me this weekend!</body>
</note>
```

**PUBLIC 公共外部约束文档示例**

<img src="E:\JavaWeb\筆記\images\683560-20190502213356534-1266758955.jpg" style="zoom:50%;" />

```xml
<!DOCTYPE mapper  
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
```

> DOCTYPE 后面的 mapper 就是整个 xml 的根标签，PUBLIC 表示引用的 dtd 约束是一个公共约束

## shema 约束

> 同 DTD 一样，XML Schema（XML Schema Definition，XSD，XML Schema定义）也是一种用于定义和描述 XML 文档结构与内容的模式语言，它的出现克服了 DTD 的局限性。

### Schema 较 DTD 的优点

通过 XML Schema 与 DTD 的比较，将 XML Schema 所具有的一些显著优点进行列举，具体如下：

1. DTD 采用的是非 XML 语法格式，缺乏对文档结构、元素、数据类型等全面的描述。而 XML Schema 采用的是 XML 语法格式，而且它本身也是一种 XML 文档，因此，XML Schema 语法格式比 DTD 更好理解；
2. XML 有非常高的合法性要求，虽然 DTD 和 XML Schema 都用于对 XML 文档进行描述，都被用作验证 XML 合法性的基础。但是， DTD 本身合法性的验证必须采用另外一套机制，而 XML Schema 则采用与 XML 文档相同的合法性验证机制；
3. XML Schema 对名称空间支持得非常好，而 DTD 几乎不支持名称空间；
4. DTD 支持的数据类型非常有限。例如，DTD 可以指定元素中必须包含字符文本（PCDATA），但无法指定元素中必须包含非负整数，而 XML Schema 比 DTD 支持更多的数据类型，包括用户自定义的数据类型；
5. DTD 定义约束的能力非常有限，无法对 XML 实例文档作出更细致的语义限制，例如，无法很好地指定一个元素中的某个子元素必须出现 7-12 次；而 XML Schema 定义约束的能力非常强大，可以对 XML 实例文档作出细致的语义限制。

通过上面的比较可以发现，XML Schema 的功能比 DTD 强大很多，但相应的语法也比DTD复杂很多。Schema 是基于 XML 编写的，XML Schema 约束文件本身就是一个 XML 文档（文件后缀名为.xsd），文件内的代码要符合 XML 语法规范。

### Schema 名称空间

一个 XML 文档可以引入多个 Schema 约束文档，但是，由于约束文档中的元素或属性都是自定义的，因此，在 XML 文档中，极有可能出现代表不同含义的同名元素或属性，导致名称发生冲突。为此，在 XML 文档中，提供了名称空间，它可以唯一标识一个元素或者属性。

这就好比咱们系有两个同名的同学，如果老师要找那个同学，就得给他们的名字前面加个前缀，XXX 班的某某某。这个 “XXX班” 就相当于一个名称空间。

在使用名称空间时，首先必须声明名称空间。名称空间的声明就是在 XML 实例文档中为某个模式文档的名称空间指定一个临时的简写名称（起个别名），它通过一系列的保留属性来声明，这种属性的名字必须是以 `xmlns` 或者以 `xmlns:` 作为开始。它与其它任何 XML 属性一样，都可以通过直接或者使用默认的方式给出。

名称空间声明的语法格式如下所示：

```xml
<元素名称 xmlns:prefixname="URI">
```

在上述语法格式中，元素名称指的是在哪一个元素上声明名称空间，在这个元素上声明的名称空间适用于声明它的元素和属性，以及该元素中嵌套的所有元素及其属性。`xmlns:prefixname` 指的是该元素的属性名，它所对应的值是一个 URI 引用，用来标识该名称空间的名称。

我们来修改 bookShelf.xml 文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:書架 xmlns:xs="http://www.example.org/book/schema"
xmlns="http://www.w3.org/2001/XMLSchema-instance">
    <xs:書>
        <xs:書名>深入理解Java虚拟机</xs:書名>
        <xs:書名>129.00</xs:書名>
    </xs:書>
</xs:書架>
```

名称空间的使用就是将一个前缀（xs）绑定到代表某个名称空间的 `URI（http://www.example.org/book/schema）`上。

然后将前缀添加到元素名称前面来说明该元素属于哪个 Schema 文档。

如果一个 XML 文档有很多元素，而且这些元素都在同一个名称空间，这时，给每个元素名称都添加一个前缀将是一件非常烦琐的事情。

这时，可以使用默认的名称空间，默认名称空间声明时不需要加 “别名”，使用这些元素时，也不用加前缀。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<書架 xmlns="http://www.example.org/book/schema">
    <書>
        <書名>深入理解Java虚拟机</書名>
        <售價>129.00</售價>
    </書>
</書架>
```

### Schema 引入约束

> 如果想通过 XML Schema 文件对某个 XML 文档进行约束，必须将 XML 文档与 Schema 文件进行关联。在 XML 文档中引入 Schema 文件有两种方式：
>
> 1. 使用名称空间引入 Schema
> 2. 不使用名称空间引入 Schema

#### 使用名称空间引入Schema

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" 
    targetNamespace="http://www.itcast.org/book" 
    elementFormDefault="qualified">
    <element name="books">
        <complexType>
            <sequence>
                <element name="book">
                    <complexType>
                        <sequence>
                            <element name="name"></element>
                            <element name="author"></element>
                            <element name="price"></element>
                        </sequence>
                    </complexType>
                </element>
            </sequence>
        </complexType>
    </element>
</schema>
```

> 在定义 Schema 文件的时候，由于这个 Schema 文件本身就是 xml，它也要受到别的约束。而这个约束是W3C 组织提前定义好的，在 Schema 文件中需要提前引入进来在根标签中使用属性进行进入：
>
> - `xmlns="http://www.w3.org/2001/XMLSchema"`   引入 W3C 定义的 schema 书写的约束
> - `targetNamespace="http://www.itcast.org/book"` 给当前的 Schema 文件起名字（命名空间），
>   作用是当哪个 xml 要引入这个 schema 约束的时候，必须通过当前 targetNamespace 后面书写的 uri 地址来引入

在 xml 文件中引入当前的这个 Schema

schema instance（schema 实例），这个概念类似于类实例（对象），`http://www.w3.org/2001/XMLSchema-instance` 这个定义 schema 约束文件的元约束文件的命名空间，通过这个元约束的命名空间定义的 schema 约束文件就是 schema 实例。也就是说 schema 实例其实就是schema 约束文件，就像类实例就是类对象一样。

```xml
<books xmlns="http://www.itcast.org/book"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.itcast.org/book book.xsd">
	<book>
		<name>JavaWeb</name>
		<author>老王</author>
		<price>182</price>
	</book>
</books>
```

我们需要在 XML 文档中的根节点中使用 schemaLocation 属性来指定 Schema 文件。schemaLocation 属性有两个值：

第一个值是需要使用的名称空间。

第二个值是供命名空间使用的 XML Schema 文件的路径。

两者之间用空格分隔。

> 1. `http://www.itcast.org/book"`   它是 schema 文件中的 targetNamespace 属性的值
> 2. `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`   说明当前的 xml 是 schema 一个实例文档，其真正的含义是 xml schema instances 命名空间，也就是所有的 shema 实例都在这里面，是和下面的 sxi:shemaLocation进行绑定的
> 3. `xsi:schemaLocation="http://www.itcast.org/book book.xsd">`   这个是在引入当前的 schema 文件的真实路径

在每个 xml 文件中，我们都会看到  `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"` 这个命名空间是实例命名空间，我们在 xml 中引入的 schema 实例，都必须和 `"http://www.w3.org/2001/XMLSchema-instance"` 进行绑定，绑定是通过一个前缀进行绑定。在 books.xml 中，这个前缀是 xsi 。

![](E:\JavaWeb\筆記\images\683560-20190502230250653-297454263.jpg)

上图未没有进行绑定，报错信息如下：

The prefix "test" for attribute "test:schemaLocation" associated with an element type "books" is not bound.

books 元素的 "test:schemaLocation" 属性的前缀没有绑定

其实 schema 实例命名空间的前缀可以修改，例如把前缀修改成 test，那么上图就不会报错，示例如下图

![](E:\JavaWeb\筆記\images\683560-20190502230143947-2145444919.jpg)



**描述约束的文件以 .xsd为扩展名，在 xml 中引入多个 shema 的约束如下**

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd"> 
</beans>
```

在引入 shema 约束时，并没有再另外使用新的标签(DTD约束使用<!DOCTYPE>标签引入约束)，而是在根标签中使用 xmlns 属性来引入约束，xmlns 是 xml namespace 的简写。并通过 xsi:schemaLocation="" 把 schema 约束的位置进行指定，一般情况下会按照指定的位置到网络中下载约束文件，如果没有网络，需要自己指定本地约束文件。

#### 不使用名称空间引入 Schema

如果 book.xsd 与引用它的 XML 文件位于同一个目录中，我们可以不使用名称空间来引入 Schema，book.xsd 中不需要定义 targetNamespace（目标名称空间）了，book.xsd 代码：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" 
    elementFormDefault="qualified">
    <element name="books">
        <complexType>
            <sequence>
                <element name="book">
                    <complexType>
                        <sequence>
                            <element name="name"></element>
                            <element name="author"></element>
                            <element name="price"></element>
                        </sequence>
                    </complexType>
                </element>
            </sequence>
        </complexType>
    </element>
</schema>
```

修改 book.xml 文件，在 book.xml 中也不需要指定默认名称空间了。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<书架 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="book.xsd">
    <书>
        <书名>深入理解Java虚拟机</书名>
        <售价>129.00</售价>
    </书>
</书架>
```

> noNamespaceSchemaLocation 是一个在标准名称空间（`http://www.w3.org/2001/XMLSchema-instance`）里面定义好的属性，用于指定 book.xsd 文档位置。

# XML 解析

> 不管是 html 文件还是 xml 文件它们都标记型文档都可以使用 W3C 组织制定的 dom 技术来解析。dom 解析技术是 W3C 组织制定的，而所有的编程語言都对这个解析技术使用了自己语言的特点进行实现。Java 对 dom 技術解析标记也做了實現。

- 早期 JDK 为我们提供了两种 xml 解析技術 DOM 和 Sax (已经过时，但我们需要知道这两种技术)

  - **dom (Document Object Model, 即文档对象模型) :** 是 W3C 组织推荐的处理 XML 的一种方式。它下面有两个分支分別是 jDom 与 dom4j 它们可都可以对 XML 文件进行增删改查的操作。
  - **sax (Simple API for XML) :** 不是官方標準，但它是 XML 社區事實上的標準，幾乎所有的 XML 解析器都支持它。(只能進行解析)

- SUN 公司在 JDK5 版本对 dom 解析技术进行升级  → SAX (Simple API for XML)。

- SAX 解析 : 它跟 W3C 制定的解析不太一样。它是以类似事件机制通过回调告诉用户当前正在解析的内容。它是一行一行的读取 xml 文件进行解析的。不会创建大量 dom对象。所以它在解析 xml 的时候，在内存的使用上。和性能上。都优于 dom 解析。

- 第三方的解析 : 

  - **jDom :** 在 dom 基礎上進行了封裝。
  - **Dom4j :** 又對 jdom 進行了封裝，我們常用 dom4j 替換原生 dom 解析。
  - **pull :** 主要用在 Android 手机开发，和 sax 解析很相似都是事件机制解析 xml 文件，它是一個第三方開源的 Java 項目，但在 Android 的內核中已經嵌入了 Pull。(只能進行解析)

  > 这个 Dom4j 它第三方的解析技术。我们需要使用第三方给我们提供好的类库才可以解析 xmI 文件。

# DOM4J 进行 XML 解析

## DOM4J 的使用步骤

**dom4j 編程步驟 :** 

- 第一步 : 导入 jar 包 dom4j.jar
- 第二步 : 创建 SAXReader 解析器对象

- 第三步 : 先加载 xml 文件建 Document 對象
- 第四步 : 通过 Document 对象拿到根元素对象
- 第五步 : 通过 `根元素.elelemts(标签名)` 可以返回一个集合，这个集合里放着。所有你指定的标签名的元素对象
- 第六步 : 找到你想要修改、删除的子元素，进行相应在的操作
- 第七步 : 保存到硬盘上

## DOM4J 的 API 介绍

1.  创建 SAXReader对象

```java
SAXReader saxReader = new SAXReader();
```

2. 解析 XML 获取 Document 对象 : 需要传入要解析的 XML 文件的字节输入流

```java
Document document = reader.read(inputStream);
```

3. 获取文档的根标签

```java
Element rootElement = documen.getRootElement()
```

4. 获取标签的子标签

```java
//获取所有子标签
List<Element> sonElementList = rootElement.elements();

//获取指定标签名的子标签
List<Element> sonElementList = rootElement.elements("标签名");
```

5. 获取标签体内的文本

```java
String text = element.getText();
```

6. 获取标签的某个属性的值

```java
String value = element.attributeValue("属性名");
```

## 使用 dom4j 技術讀取 XML 文件得到 Document 對象

> document 对象表示的是整个文档（可以是 html 文档，也可以是 xml 文档）

```java
@Test
public void getDocument() throws DocumentException {
    // 要創建一個 Document 對象，需要我們先創建一個 SAXReader 对象。
    SAXReader reader = new SAXReader();
    // 這個對象用於讀取 xml 文件，然後返回一個 Document。
    Document document = reader.read("src/students.xml");
    // 打印控制台，看看是否創建成功
    System.out.println(document);
}
```

## 使用 dom4j 解析 xml

- **需要分四步操作 :**
  - 第一步，通过创建 SAXReader 对象。来读取 xml 文件，获取 Document 对象
  - 第二步，通过 Document 对象。拿到 XML 的根元素对象
  - 第三步，通过根元素对象。获取所有的 book 标签对象
  - 第四步，遍历每个 book 标签对象。然后获取到 book 标签对象内的每一个元素，再通过 getText() 方法拿到起始标签和结束标签之间的文本内容

```java
// 读取 xml 文件中的内容
@Test
public void readXML() throws DocumentException {
    // 第一步，通过创建 SAXReader 对象。来读取 xml 文件，获取 Document 对象
    SAXReader reader = new SAXReader();
    Document document = reader.read("src/students.xml");

    // 第二步，通过 Document 对象。拿到 XML 的根元素对象
    Element root = document.getRootElement();
    // 打印测试
    // Element.asXML(): 它将当前元素转换成为 String 对象
    System.out.println(root.asXML());

    // 第三步，通过根元素对象。获取所有的 student 标签对象
    // Element.elements(标签名)它可以拿到当前元素下的指定的子元素的集合
    List<Element> students = root.elements("student");

    // 第四步，遍历每个 student 标签对象。然后获取到 book 标签对象内的每一个元素，
    for (Element student : students) {
        // 测试
        System.out.println(student.asXML());

        // 拿到 student 下面的 name 元素对象
        Element nameElement = student.element("name");
        // 拿到 student 下面的 birthDay 元素对象
        Element birthDayElement = student.element("birthDay");
        // 拿到 student 下面的 age 元素对象
        Element ageElement = student.element("age");
        // 再通过 getText() 方法拿到起始标签和结束标签之间的文本内容
        System.out.println("學生:" + nameElement.getText() + " , 生日:" + birthDayElement.getText() + ", 年齡："
                           + ageElement.getText());
    }
}
```

## 使用 dom4j 解析 xml 並保存 xml 文件

```java
@Test
public void outputXML() throws Exception {
    // 1. 創建閱讀器
    SAXReader reader = new SAXReader();
    // 2. 讀取文檔
    Document document = reader.read("src/students.xml");
    // 3. 獲取根結點
    Element root = document.getRootElement();
    // 4. 通过根元素对象。获取第一個 student 标签对象
    Element student = root.element("student");
    Element studentName = student.element("name");
    studentName.setText("蕭士麟");
    studentName.setAttributeValue("type", "男生");
    // 5. 保存
    // OutputFormat 將我們輸出的數據格式化(看起來整齊)
    OutputFormat format = OutputFormat.createCompactFormat();
    XMLWriter xmlWriter = new XMLWriter(new FileOutputStream("src/out.xml"), format);
    xmlWriter.write(document);
    xmlWriter.close();
}
```
