# XML

![](images\1681452257379.png)

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
- XML 的基本语法和 HTML 的基本语法简直如出一辙。其实这不是偶然的，XML 基本语法 
-  HTML 约束 = HTML语法。在逻辑上 HTML 确实是 XML 的子集。
- XML 文档声明 : 这部分基本上就是固定格式，要注意的是文档声明一定要从第一行第一列开始写

## 🌟 XML 基本語法概念
### 1. 文件宣告（可選，但推薦加）
```xml
<?xml version="1.0" encoding="UTF-8"?>
```
- 必須放在檔案最上面第一行。
- version 是 XML 的版本（目前通常是 1.0）。
- encoding 指定字元編碼，常用 UTF-8。

### 2. 根元素
> 必須且只能有一個根元素！

**✅ 正確範例：**
```xml
<students>
    <student>...</student>
</students>
```

**❌ 錯誤範例（有兩個根）：**
```xml
<students>...</students>
<teachers>...</teachers>
```
（錯，外層只能有一個最頂層標籤）

#### ➔ 什麼是根元素？
> 沒有父元素、最外層、唯一一個 → 叫根元素（Root Element）。

### 3. 标签关闭
![](images\雙標籤和單標籤.png)

#### ➔ 雙標籤（成對出現）
![](images\XML標籤一定要閉合.png)

> 每個開始標籤 <tag> 都要有一個對應的結束標籤 </tag>。

**範例：**
```xml
<name>张三</name>
```

#### ➔ 單標籤（自閉合）
> 沒有內容的元素可以直接自閉合，用 `/`。

**範例：**
```xml
<br/>
```

**或者**
```xml
<photo src="image.png" />
```

### 4. 标签嵌套
> 可以嵌套，但不能交叉嵌套！

**✅ 正確嵌套：**
```xml
<student>
    <name>张三</name>
</student>
```

**❌ 錯誤交叉嵌套（絕對會報錯）：**
```xml
<student>
    <name>张三
</student></name>
```

### 5. 注释不能嵌套
XML 中的註解格式是這樣：

```xml
<!-- 這是註解 -->
```
> 不能在一個註解內再寫另一個註解！

**❌ 錯誤範例（註解嵌套）：**
```xml
<!-- 這是註解 <!-- 這也是註解 --> -->
```
>（這樣會直接報錯）

### 6. 标签名、属性名建議使用小寫字母
> 雖然 XML 語法不強制，但業界習慣是用小寫。

**範例（推薦）：**

```xml
<student id="1">
    <name>张三</name>
</student>
```

**而不是像這樣（不建議）：**
```xml
<Student Id="1">
    <Name>张三</Name>
</Student>
```

### 7. 屬性
#### ➔ 屬性必須有值
**❌ 錯誤範例：**
```xml
<student id>
```

**✅ 正確範例：**
```xml
<student id="1">
```
#### ➔ 屬性值必須加引號（單引號或雙引號皆可）
**範例：**
```xml
<student id="1" name='张三'>
```
>（雙引號、單引號都可以，但要一致且配對正確）

### 8. 標籤名不能包含空格
![](images\標籤名不能包含空格.png)
#### ❌ 錯誤範例：
```xml
<student name>张三</student name>
```
>（標籤名 student name 有空格，是錯的）

#### ✅ 正確範例：
```xml
<studentname>张三</studentname>
```
或
```xml
<student_name>张三</student_name>
```

### 9. XML 屬性必須用引號引起來
![](images\XML屬性必須用引號引起來.png)

#### ✅ 正確範例：
```xml
<student id="1" name="张三"/>
```

#### ❌ 錯誤範例：
```xml
<student id=1 name=张三/>
```
>（屬性值不能裸寫，一定要有引號）

### 10. 標籤大小寫敏感
![](images\標籤大小寫敏感.png)

> <name> 和 <Name> 是不同的元素！

#### 範例：
```xml
<name>张三</name> <!-- OK -->
<Name>张三</Name> <!-- OK，但注意這是不同名字 -->
```

>（不要混用大小寫）

### 11. 標籤閉合位置不正確
![](images\標籤閉合位置不正確.png)

#### ❌ 錯誤範例（閉錯位置）：
```xml
<student>
    <name>张三
</student>
</name>
```

#### ✅ 正確範例：
```xml
<student>
    <name>张三</name>
</student>
```

### 12. 特殊字符
- ![](images\特殊字符.png)

> 某些符號不能直接出現，必須用轉義字元表示：

| 字元 | 轉義寫法 |\
|---|---|
| <	| &lt; |
| >	| &gt; |
| &	| &amp; |
| '	| &apos; |
| "	| &quot; |

#### 範例：
```xml
<message>5 &lt; 10</message>
```

>（顯示結果是：5 < 10）

### 13. 不能以數字打頭
![](images\不能以數字打頭.png)

> 標籤名不能以數字開頭。

#### ❌ 錯誤範例：
```xml
<123student>张三</123student>
```

#### ✅ 正確範例：
```xml
<student123>张三</student123>
```

或

```xml
<_123student>张三</_123student>
```
>（可以用底線開頭）

## 範例

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

# 文本区域（CDATA 区）

> CDATA 语法可以告诉 xml 解析器，我 CDATA 里的文本内容只是纯文本，不需要 xml 语法解析。

**語法格式:**
```XML
<![CDATA[這裡可以把你輸入的字符原樣顯示，不會被解析]]>
```

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

### students.xml:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<students>
    <student>
        <name>张三</name>
        <age>18</age>
        <birthDay>2005-01-01</birthDay>
    </student>
    <student>
        <name>李四</name>
        <age>20</age>
        <birthDay>2003-02-02</birthDay>
    </student>
</students>
```

### 程式碼
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
