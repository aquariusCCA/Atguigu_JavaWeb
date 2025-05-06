# 1. ✅ Vue + JavaWeb 整合部署筆記

## 一、整體流程概覽

1. **Vue 專案打包** 為靜態資源（HTML、JS、CSS）。
2. **將打包後的靜態資源複製至 JavaWeb 專案的 webapp 目錄**（如 `src/main/webapp/`）。
3. **使用 IntelliJ IDEA 或 Maven 打成 `.war` 檔**，包含 Vue 靜態檔。
4. **部署至 Tomcat 或 Servlet 容器**，實現前後端整合。

---

## 二、詳細步驟

### 1. 打包 Vue 專案

```bash
npm run build
```

產出資料夾（例如 `dist/` 或 `build/`）會包含：

* `index.html`
* `/assets`、`/js`、`/css` 等靜態資源

---

### 2. 將 Vue 靜態資源複製到 Java 專案
> 將 `dist` 裡的內容（不是整個 `dist` 資料夾）放到 JavaWeb 專案的靜態資源資料夾，例如：

* **對於傳統 Java Web 專案：**

  ```
  src/main/webapp/
  ├── index.html
  ├── assets/
  ├── js/
  └── css/
  ```

* **Spring Boot（若為 `.jar`，則建議放 `resources/static` 或 `public`）**

---

### 3. 打包 JavaWeb 專案成 WAR

* 使用 IntelliJ IDEA 或 Maven 打包
* 輸出 `yourproject.war`，其中包含 Vue 的靜態頁面

---

## 三、Vue Router 路由模式處理（`history` 模式）

### 問題：

使用者直接訪問 `/scheduleSystem/dashboard` 等深層路由時，伺服器無法對應該靜態資源，會出現 404。

### 解法：Filter 轉發所有非靜態資源請求至 `index.html`

```java
@Override
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
        throws IOException, ServletException {

    HttpServletRequest req = (HttpServletRequest) request;
    String uri = req.getRequestURI();              // e.g., /scheduleSystem/dashboard
    String contextPath = req.getContextPath();     // e.g., /scheduleSystem
    String path = uri.substring(contextPath.length()); // e.g., /dashboard

    System.out.println("攔截 URI: " + uri);
    System.out.println("contextPath: " + contextPath);
    System.out.println("攔截路徑: " + path);

    // 白名單：放行 API、靜態資源（含副檔名）
    if (path.startsWith("/api") ||
            path.startsWith("/js") ||
            path.startsWith("/css") ||
            path.startsWith("/assets") ||
            path.contains(".")) {
        chain.doFilter(request, response);
        return;
    }

    // 其他轉發給 Vue 的 index.html
    request.getRequestDispatcher("/index.html").forward(request, response);
}
```

---

## 四、Vite 或 Vue CLI 設定 Base 路徑

### Vite 專案（vite.config.ts）：

```ts
export default defineConfig({
  base: '/scheduleSystem/', // 配合部署路徑
  build: {
    outDir: 'dist'
  }
});
```

---

## 五、注意事項總結

| 項目           | 說明                                          |
| ------------ | ------------------------------------------- |
| 🔀 Vue 路由模式  | 使用 `history` 模式時需轉發請求至 `index.html`         |
| 📁 靜態資源路徑    | Vue 打包時設定 `base` 為 `/scheduleSystem/`       |
| 🧩 Filter 設定 | 攔截所有請求 (`/*`)，排除靜態資源後，將其餘請求轉發至 `index.html` |
| 🌐 同源問題      | WAR 部署後屬於同源，通常不需要額外配置 CORS                  |
| 🗂️ 靜態頁面入口   | `index.html` 建議直接放在 `src/main/webapp/` 根目錄  |

---

# 2. 📘 Vite `base` 配置筆記整理

## 🔧 一、`base` 是什麼？

* `base` 是 Vite 中的設定項目，用來指定**靜態資源的公共路徑（Base Public Path）**。
* 預設為 `'/'`，但若你將專案部署到**子目錄（如 `/scheduleSystem/`）**，就必須設為該子目錄路徑。

### ✅ 語法範例：

```ts
// vite.config.js
export default defineConfig({
  base: '/scheduleSystem/',
})
```

---

## 🚦 二、`base` 的影響範圍

| 項目                                        | 是否受 `base` 影響                        | 說明                                   |
| ----------------------------------------- | ------------------------------------ | ------------------------------------ |
| HTML 中的 `<script>`、`<link>`、`img` 等靜態資源路徑 | ✅ 會套用 `base` 作為前綴                    |                                      |
| JS 中的 import 路徑（打包後）                      | ✅ 編譯後會加上 `base` 前綴                   |                                      |
| 打包後的 HTML 中 `src` 和 `href`                | ✅ 會從 `/scheduleSystem/assets/...` 開始 |                                      |
| **瀏覽器網址列的 URL**                           | ❌ 不會影響                               | 瀏覽器的 URL 是由前端 router（如 Vue Router）控制 |
| Vue Router 的路由解析                          | ❌ 不會自動受影響                            | 必須**手動設定 router 的 base path**        |

---

## 🧭 三、開發 vs 生產的不同

### 🔍 開發階段（`npm run dev`）：

* 若設定 `base: '/scheduleSystem/'`，開發伺服器 URL 將變為：

  ```bash
  ➜  Local: http://localhost:5173/scheduleSystem/
  ```

  這其實**是因為你設定了 `base: '/scheduleSystem/'`，導致 dev server 模擬生產環境資源路徑**，所以連開發伺服器的 URL 也套用了這個前綴。

### 🔍 重點來了：

| 項目                                 | 是否受 `base` 影響             | 說明                                   |
| ---------------------------------- | ------------------------- | ------------------------------------ |
| 開發伺服器 (`npm run dev`) 的啟動地址        | ✅ 會受影響（僅 URL 表面）          | 用來模擬部署在子目錄的情境                        |
| **瀏覽器網址列變成 `/scheduleSystem/` 開頭** | ✅ 開發時會變                   | **但這只是 Vite dev server 模擬，實際部署才有意義** |
| 真正的 router URL 行為                  | ❌ 除非你自己設定 router 的 `base` | Vite 不會自動幫你設定 Vue Router 的行為         |

---

### ⚠️ 注意：

你可能會以為 `base` 控制的是瀏覽器的路由行為，但實際上：

* `base` 是 **靜態資源的 public path 前綴**（HTML、JS、CSS 的 `src`、`href`）
* `localhost:5173/scheduleSystem/` 是為了開發階段模擬「部署到子目錄」的效果
* 即使網址列變成 `/scheduleSystem/`，這是資源前綴模擬，不是路由實際運作。
* 你**必須手動設定 Vue Router 的 `createWebHistory('/scheduleSystem/')`**，才能讓路由正確解析：

  ```ts
  createRouter({
    history: createWebHistory('/scheduleSystem/'),
    routes,
  })
  ```

---

## 🧪 四、開發與部署環境切換建議

### ✅ 正確搭配做法

```js
// vite.config.js
export default defineConfig({
  base: '/scheduleSystem/',
})
```

```ts
// router/index.ts
createRouter({
  history: createWebHistory('/scheduleSystem/'),
  routes,
})
```

### ✅ 建議做法（根據環境動態切換 `base`）：

> 若你想**在本機開發階段簡化 URL（不想每次都打 `/scheduleSystem/`）**：

```ts
// vite.config.js
export default defineConfig(({ mode }) => ({
  base: mode === 'production' ? '/scheduleSystem/' : '/',
}))
```

開發時不設 `base`，但打包前再改回 /scheduleSystem/

---

## ✅ 結論

* `vite.config.js` 中的 `base` 只控制靜態資源前綴，不會控制 Vue Router 的 URL 行為。
* 若你要部署到子目錄，需 **同時設定**：

  1. `vite.config.js > base: '/子目錄/'`
  2. `Vue Router > createWebHistory('/子目錄/')`
* 開發階段看到 `/scheduleSystem/` 是為了模擬真實部署，無需擔心。

---