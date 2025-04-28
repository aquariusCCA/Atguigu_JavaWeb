# 1. 回顧 JavaWeb 中的路徑

在 JavaWeb 開發中，**路徑**分為兩大類：

## 1.1 相對路徑（Relative Path）
- **`.`**：表示當前目錄  
  （例如：`./index.html`，表示當前目錄下的 `index.html`）
- **`..`**：表示上一級目錄  
  （例如：`../css/style.css`，表示回到上一層再找 `css/style.css`）
- **`資源名`**：直接寫資源名，表示當前目錄下的資源  
  （例如：`image/logo.png`）

✅ 特點：**隨著當前頁面位置不同，資源路徑也不同**，容易出錯。

---

## 1.2 絕對路徑（Absolute Path）
- **完整的網址格式**：
  ```
  http://IP:port/工程路徑/資源路徑
  ```
  例如：  
  ```
  http://localhost:8080/myapp/css/style.css
  ```

✅ 特點：**無論在哪個頁面，路徑都是固定的，不會出錯。**

> 🔥 在實際開發中，為了避免出錯，**通常推薦使用絕對路徑。**

---

# 2. `/` 在 Web 中的不同意義

在 Web 項目中，`/`（斜杠）有兩種不同的解析方式，取決於**誰在解析它**：

---

## 2.1 被瀏覽器解析 `/`
- 當 `href`、`src`、`form action` 等在 HTML 中遇到 `/`，**是瀏覽器在解析**。
- **解析結果**：瀏覽器會自動指向網站根目錄  
  ```
  http://IP:port/
  ```
- **例子**：
  ```html
  <a href="/">首頁</a>
  ```
  👉 這裡的 `/` 代表瀏覽器打開 `http://IP:port/`

---

## 2.2 被伺服器解析 `/`
- 當在 Java 程式碼中遇到 `/`（如 Servlet 配置、跳轉、獲取資源路徑），是**伺服器（Tomcat）在解析**。
- **解析結果**：伺服器會指向**工程應用的根目錄**  
  ```
  http://IP:port/工程名/
  ```

- **常見場景**：
  1. **Servlet 映射**
     ```xml
     <url-pattern>/servlet1</url-pattern>
     ```
     👉 `/servlet1` 表示在工程內部匹配 `/servlet1`
  2. **獲取真實磁碟路徑**
     ```java
     servletContext.getRealPath("/");
     ```
     👉 獲取到 Web 應用在磁碟中的根目錄實際路徑
  3. **內部轉發**
     ```java
     request.getRequestDispatcher("/index.jsp").forward(request, response);
     ```
     👉 轉發到 `/index.jsp`，其實是轉發到當前工程下的 `index.jsp`

---

## 2.3 特殊情況：`response.sendRedirect("/")`
- 調用 `response.sendRedirect("/")`，這個斜杠是**讓瀏覽器去解析**。
- 所以結果是跳轉到網站根目錄：
  ```
  http://IP:port/
  ```

✅ 注意：**`sendRedirect()` 是重新讓瀏覽器發請求，所以按瀏覽器解析路徑規則。**

---

# 小結總覽

| 誰解析 `/` | 解釋結果 | 常見場景 |
|:---|:---|:---|
| 瀏覽器 | `http://IP:port/`（網站根目錄） | `<a>、<form>、sendRedirect()` |
| 伺服器（Tomcat） | `http://IP:port/工程名/`（應用根目錄） | Servlet 映射、資源獲取、內部轉發 |

---

這樣補充完之後，你的講義就會邏輯非常清楚，從路徑基礎 → `/` 的解析規則 → 實際場景，全都銜接得上。  
要不要我也順便幫你畫一個簡單的「瀏覽器 vs 伺服器解析路徑」的流程圖？會更容易理解哦！要的話告訴我～🚀