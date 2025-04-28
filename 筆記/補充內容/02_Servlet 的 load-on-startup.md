# 1. 什麼是 `load-on-startup`？
在 Servlet（Java Web 的後端元件）中，**預設**來說，Servlet 是「**第一次有用到時才初始化（懶加載，lazy loading）**」。

但有時候我們希望 Servlet 在 **Tomcat啟動時**就直接初始化、執行 `init()` 方法（例如需要先做一些資源準備、連資料庫等），這時就可以用 `load-on-startup`。

### 簡單來說：
- **不設定 `load-on-startup`** ➔ 第一次請求來的時候，Servlet 才會被創建。
- **設定 `load-on-startup`** ➔ Tomcat 啟動時就會創建這個 Servlet。

---

# 2. `load-on-startup` 的數字有什麼意義？
`<load-on-startup>數字</load-on-startup>`

- 數字是**正整數或0或負數**。
- **數字越小，啟動順序越前面**。
- 如果數字相同，Tomcat自己決定順序。

| 數字 | 代表意思 |
|:----|:----|
| 正數 (0, 1, 2...) | Tomcat啟動時**馬上加載**，數字越小，越先加載 |
| 負數或沒寫 | **延遲加載（Lazy Loading）**，第一次用到才創建 |

---

# 3. 為什麼自定義 Servlet 不建議用 1-5？
Tomcat 本身內建的一些重要系統 Servlet（比如管理 console、預設頁面等等）**可能已經用 1-5 這些數字**。
為了避免**啟動順序干擾**或**出問題**，自訂的 Servlet 建議從 **6以上** 開始用，這樣比較保險。

---

# 4. 簡單範例：沒有設定 vs 有設定 `load-on-startup`

假設有一個 Servlet 叫 `HelloServlet`。

### (1) 沒有設定 load-on-startup （預設 Lazy 加載）
```xml
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.example.HelloServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```
- 伺服器啟動時：**沒有初始化**這個 HelloServlet。
- 第一次訪問 `/hello` 時：**Tomcat 才創建 HelloServlet 實例並調用 `init()` 方法**。

---

### (2) 有設定 load-on-startup = 10
```xml
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.example.HelloServlet</servlet-class>
    <load-on-startup>10</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>hello</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```
- 伺服器啟動時：**Tomcat馬上創建 HelloServlet 實例並調用 `init()` 方法**。
- 即使沒人訪問 `/hello`，Servlet 也已經在記憶體中了。

---

# 5. 小總結

| 項目 | 沒有設定 `load-on-startup` | 設定了 `load-on-startup` |
|:----|:----|:----|
| 何時初始化？ | 第一次訪問時 | 伺服器啟動時 |
| 需要注意的順序？ | 不需要 | 數字越小越先初始化 |
| 自定義 Servlet 建議用多少？ | 不適用 | 建議 6以上 |

---

# 6. 小實際情境例子
如果你寫了一個「資料庫連線池初始化」的 Servlet，應該希望 Tomcat啟動時就準備好，不要等用戶第一次訪問才去建連線。
這時你就會這樣寫：

```xml
<servlet>
    <servlet-name>dbInit</servlet-name>
    <servlet-class>com.example.DbInitServlet</servlet-class>
    <load-on-startup>10</load-on-startup> <!-- 啟動時馬上執行 -->
</servlet>
```

這樣一開機就會幫你把連線準備好，系統比較穩定。

---

要不要我順便也給你一個**完整小Demo**，讓你可以自己在本地跑起來看？要的話我可以馬上生一份給你。  
要嗎？😃