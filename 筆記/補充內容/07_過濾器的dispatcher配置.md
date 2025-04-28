## 什麼是 dispatcher 配置？

在 JavaWeb 中，`Filter` 是攔截 **請求** 或 **響應** 的一種技術。  
而「dispatcher 配置」是指定**在什麼情況下**要啟動過濾器。

dispatcher 有四種情況：
| dispatcher 類型 | 說明 | 什麼情況會被攔截 |
|:---|:---|:---|
| REQUEST (預設) | 瀏覽器直接請求 | 直接請求資源，比如點超連結、直接訪問網頁 |
| FORWARD | 轉發的請求 | 伺服器內部用 `request.getRequestDispatcher().forward()` |
| INCLUDE | 包含的請求 | 使用 `request.getRequestDispatcher().include()` 包含其他資源 |
| ERROR | 錯誤處理的請求 | 使用 `<error-page>` 設定錯誤時跳轉的頁面 |

---

## 每個 dispatcher 的簡單說明 + 範例

### 1. `REQUEST`
- **說明**：瀏覽器直接請求時，才會觸發過濾器（預設值）。
- **範例**：
    - 使用者在瀏覽器輸入網址：`http://localhost:8080/myweb/hello.jsp`
    - 這個請求是「直接」發起的 → 會被 Filter 攔截。

    ```xml
    <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/hello.jsp</url-pattern>
        <dispatcher>REQUEST</dispatcher>
    </filter-mapping>
    ```

---

### 2. `FORWARD`
- **說明**：當伺服器**內部轉發**時，才會觸發過濾器。
- **範例**：
    - 例如登入成功後，程式寫：

    ```java
    request.getRequestDispatcher("/welcome.jsp").forward(request, response);
    ```
    - 這裡 `welcome.jsp` 的請求是由伺服器自己內部轉發的，不是使用者直接發送的，因此需要設定 `dispatcher=FORWARD` 才能攔截到。

    ```xml
    <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/welcome.jsp</url-pattern>
        <dispatcher>FORWARD</dispatcher>
    </filter-mapping>
    ```

---

### 3. `INCLUDE`
- **說明**：當伺服器**包含**一個頁面或資源時，才會觸發過濾器。
- **範例**：
    - 假設 `main.jsp` 包含 `menu.jsp`：

    ```jsp
    <jsp:include page="menu.jsp"/>
    ```
    - 這時候 `menu.jsp` 是被包含進來的，這個包含行為要被攔截，就需要用 `dispatcher=INCLUDE`。

    ```xml
    <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/menu.jsp</url-pattern>
        <dispatcher>INCLUDE</dispatcher>
    </filter-mapping>
    ```

---

### 4. `ERROR`
- **說明**：當發生錯誤時（例如 404、500），如果有設定 `<error-page>`，跳轉到錯誤頁面時才會觸發過濾器。
- **範例**：
    - 先在 `web.xml` 設定錯誤頁面：

    ```xml
    <error-page>
        <error-code>404</error-code>
        <location>/error404.jsp</location>
    </error-page>
    ```

    - 再設定攔截 `error404.jsp` 的過濾器：

    ```xml
    <filter-mapping>
        <filter-name>MyFilter</filter-name>
        <url-pattern>/error404.jsp</url-pattern>
        <dispatcher>ERROR</dispatcher>
    </filter-mapping>
    ```

    - 如果使用者請求了一個不存在的網頁，會跳到 `error404.jsp`，這時候 `MyFilter` 就會攔截。

---

## 小總結：

| dispatcher | 什麼時候觸發？ |
|:---|:---|
| REQUEST | 瀏覽器直接發出的請求 |
| FORWARD | 伺服器轉發的請求 |
| INCLUDE | 伺服器包含的請求 |
| ERROR | 錯誤頁面請求 |

---

## 一個完整示範 (簡單版 Filter + 配置)

```java
// MyFilter.java
import javax.servlet.*;
import java.io.IOException;

public class MyFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        System.out.println("過濾器攔截到了請求！");
        chain.doFilter(request, response); // 繼續放行
    }
}
```

```xml
<!-- web.xml 配置 -->
<filter>
    <filter-name>MyFilter</filter-name>
    <filter-class>com.example.MyFilter</filter-class>
</filter>

<filter-mapping>
    <filter-name>MyFilter</filter-name>
    <url-pattern>/*</url-pattern>
    <dispatcher>REQUEST</dispatcher>
    <dispatcher>FORWARD</dispatcher>
    <dispatcher>INCLUDE</dispatcher>
    <dispatcher>ERROR</dispatcher>
</filter-mapping>
```

這樣就會攔截各種情況的請求了！

---

要不要我再幫你畫一個簡單的「流程圖」讓你更直覺了解「直接請求、轉發、包含、錯誤」的差異？要的話告訴我！🌟  
要不要一起順便搭配一個「小專案實作例子」練習一下？我可以設計一個很簡單的！