# 1. ✅ `<Context>` 應用部署層級設定筆記
### 📌 基本概念

- `<Context>` 元素表示 Tomcat 中**一個 Web 應用（WebApp）**的運行環境配置。
- 它是 **Tomcat 應用部署層級的核心設定單位**。
- 每個 `<Context>` 都對應一個應用的 Context Path，例如 `/myapp`。

---

### 📁 常見配置位置（3 種）

| 方式 | 路徑 | 特點 |
|------|------|------|
| 1️⃣ `server.xml` 裡的 `<Host>` 區塊中 | `conf/server.xml` | 全部集中管理，但修改後需重啟 Tomcat |
| 2️⃣ 獨立 XML 檔案 | `conf/Catalina/localhost/yourApp.xml` | 應用獨立管理，不必重啟 Tomcat（修改自動偵測） |
| 3️⃣ 自動部署方式（丟入 `webapps/`） | `webapps/*.war` 或資料夾 | 不需寫 `<Context>`，由 Tomcat 自動處理 |

> ⚠️ 實務上推薦使用第 2 種方式（獨立 XML 檔），比較穩定且模組化。

---

### 🧩 常用屬性

| 屬性 | 說明 | 範例 |
|------|------|------|
| `path` | 網址路徑，對應 Context Path（如 `/myapp`） | `path="/myapp"` |
| `docBase` | 實際應用的根目錄或 `.war` 檔路徑 | `docBase="D:/project/MyApp"` |
| `reloadable` | 是否開啟熱部署（修改 class/JSP 自動重載） | `reloadable="true"` |
| `crossContext` | 是否允許應用間共享 ServletContext | `crossContext="true"` |
| `debug` | 設定除錯等級（不常用） | `debug="1"` |

---

### 📍 範例 1：server.xml 中的配置

```xml
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
  <Context path="/car" docBase="D:/apps/carApp" reloadable="true" />
</Host>
```

- 網址：`http://localhost:8080/car`
- 實體位置：`D:/apps/carApp`

---

### 📍 範例 2：conf/Catalina/localhost/car.xml

```xml
<Context docBase="D:/apps/carApp" reloadable="true" />
```

- 檔名 `car.xml` 表示 Context Path 是 `/car`
- 不需寫 `path` 屬性，檔名就是路徑名
- 優點：修改後無需重啟 Tomcat

---

### 🚀 實務建議

| 情況 | 建議方式 |
|------|----------|
| 單純測試、快速上線 | 把 `.war` 丟進 `webapps/` |
| 想獨立配置應用 | 使用 `conf/Catalina/localhost/xxx.xml` |
| 想集中配置所有應用 | 修改 `server.xml` 的 `<Host>` 中加入 `<Context>`（但需重啟） |

---

### 🔒 安全注意事項

- 若 `docBase` 指向 Tomcat 目錄以外的地方，需確認權限設定允許存取。
- 開啟 `reloadable="true"` 雖方便開發，但會佔用較多資源，不建議用在生產環境。

---

### 📚 補充資源

- 官方文檔：`https://tomcat.apache.org/tomcat-9.0-doc/config/context.html`

---

# 2. ✅ 方式一: 使用 `server.xml` 的 `<Host>` 區塊來部署 Web 應用
> 以下是使用 **`server.xml` 裡的 `<Host>` 區塊中部署 Web 應用** 的完整教學流程：

---

### 📁 適用場景
- 想將 `.war` 或應用資料夾部署在 `webapps` 以外的位置
- 想手動設定網址路徑（Context Path）
- 想啟用 `reloadable` 或進行細節控制

---

### 🧾 步驟說明

#### 🔹 1. 打開 `conf/server.xml` 檔案

路徑類似：
```
apache-tomcat-x.x.xx/conf/server.xml
```

---

#### 🔹 2. 找到 `<Host>` 區塊，加入 `<Context>` 標籤

範例：

```xml
<Host name="localhost" appBase="webapps"
      unpackWARs="true" autoDeploy="true">

  <!-- 手動部署應用 -->
  <Context 
    path="/car" 
    docBase="C:/Users/Admin/Desktop/JavaWebTest.war" 
    reloadable="true" />
  
  <!-- 其他原本的內容 -->
</Host>
```

---

#### 🔍 說明：

| 屬性 | 作用 |
|------|------|
| `path="/car"` | 訪問網址為 `http://localhost:8080/car` |
| `docBase="..."` | 指定 `.war` 或應用資料夾的實體位置 |
| `reloadable="true"` | 修改 JSP/class 自動重新載入（適合開發用） |

📌 你可以用 `.war` 檔案路徑或已解壓好的資料夾路徑。

---

#### 🔹 3. 重啟 Tomcat

`server.xml` 被修改後，**必須重新啟動 Tomcat** 才會套用設定：

```bash
./bin/shutdown.sh
./bin/startup.sh
```

---

#### 🔹 4. 測試訪問

瀏覽器輸入：
```
http://localhost:8080/car
```

應該可以正常進入你部署的應用程式。

---

### ⚠️ 注意事項

- 修改 `server.xml` 後，一定要 **重啟 Tomcat** 才會生效。
- `path=""`（空字串）代表是 **預設網站**，即 `http://localhost:8080/`。
- `docBase` 可以是 `.war` 或資料夾，**建議使用絕對路徑**。
- 若部署路徑有中文或空格，建議使用英文路徑避免 Tomcat 錯誤。

---

### ✅ 範例總結

```xml
<Context 
  path="/car" 
  docBase="D:/Projects/CarSystem" 
  reloadable="true" />
```

這代表：
- 網址為：`http://localhost:8080/car`
- 實體檔案來自：`D:/Projects/CarSystem/`
- 支援修改 class/JSP 自動重新部署（適合開發階段）

---

如果你想部署成「預設網站」（也就是不輸入路徑就能打開），可以這樣：

```xml
<Context 
  path="" 
  docBase="D:/MyApp" />
```

對應網址是：
```
http://localhost:8080/
```

---

# 3. ✅ 方式二： 使用「獨立 XML 檔案」部署 Web 應用
> 以下是使用 **「獨立 XML 檔案」部署 Web 應用** 的完整教學方式，這是比修改 `server.xml` 更推薦的做法，因為它**模組化、靈活、無需重啟 Tomcat**，適合開發與管理多個 Web 應用。

---

### 📁 部署位置

Tomcat 中的這個路徑：

```
$TOMCAT_HOME/conf/Catalina/localhost/
```

每個放在這裡的 **XML 檔案**，都代表一個 Web 應用（Context）。

---

### 🧾 步驟說明

#### 🔹 1. 準備應用（.war 或資料夾）
你可以準備好：

- 一個 `.war` 檔案  
  例如：`D:/JavaWebApps/CarApp.war`

- 或一個解壓後的 Web 資料夾  
  例如：`D:/JavaWebApps/CarApp/`

---

#### 🔹 2. 建立對應的 XML 檔案

在這個路徑下建立 XML：

```
$TOMCAT_HOME/conf/Catalina/localhost/car.xml
```

檔名 `car.xml` 就是這個應用的網址 context path  
（如 `car.xml` → `http://localhost:8080/car`）

---

#### 🔹 3. 寫入 `<Context>` 配置

範例 1（使用 `.war` 檔）：

```xml
<Context docBase="D:/JavaWebApps/CarApp.war" reloadable="true" />
```

範例 2（使用資料夾）：

```xml
<Context docBase="D:/JavaWebApps/CarApp" reloadable="true" />
```

---

#### 🔹 4. 啟動 Tomcat（或等待自動載入）

Tomcat 會自動偵測 `conf/Catalina/localhost` 內的變更，**不需修改 `server.xml`、不需重啟 Tomcat**。

---

#### 🔹 5. 訪問你的應用

對應網址為：

```
http://localhost:8080/car
```

如果你使用 `ROOT.xml` 作為檔名，則會變成預設應用：

```
http://localhost:8080/
```

---

### ✅ 優點總結

| 特點 | 說明 |
|------|------|
| ✅ 模組化 | 每個應用一個 XML，容易維護 |
| ✅ 不需重啟 Tomcat | 新增 / 修改 XML 後，自動生效 |
| ✅ 避免污染 `server.xml` | 不會讓配置文件過於冗長或難管理 |
| ✅ 適合多應用管理 | 對開發與部署環境都很友好 |

---

### ⚠️ 注意事項

- `docBase` 一定要是**絕對路徑**。
- `reloadable="true"` 適合開發階段，正式環境建議設為 `false`。
- 如果 `.xml` 檔案中也寫了 `path` 屬性，**將會被忽略**，檔名就是路徑。

---

### 📝 範例總整理

```xml
<!-- 檔名 car.xml → 對應網址 /car -->
<Context 
  docBase="D:/JavaWebApps/CarApp" 
  reloadable="true" />
```

---

# 4. ✅ 方式三： 使用「自動部署方式（丟入 webapps/）」部署 Web 應用
> 這是最簡單、最常見的部署方式：**直接把 `.war` 或應用資料夾丟進 `webapps/` 目錄**，Tomcat 啟動後會自動解壓並部署。

---

### 🧾 適用情境

| 適合誰 | 說明 |
|--------|------|
| 🧪 初學者 | 最直觀、最無腦的部署法 |
| 👨‍💻 開發階段 | 想快速測試 `.war` 或資料夾內容 |
| 🚀 單一應用部署 | 小型或測試型專案，無需額外配置 |

---

### 📁 路徑說明

Tomcat 的預設部署目錄是：

```
$TOMCAT_HOME/webapps/
```

只要你把應用（資料夾或 `.war`）丟進這裡，Tomcat 啟動時會自動部署。

---

## 🧱 方法一：部署 `.war` 檔

### 🔹 步驟：

1. 準備好 `.war` 檔  
   例如：`MyApp.war`

2. 複製進去 Tomcat 的 `webapps/`  
   ```
   cp MyApp.war /path/to/tomcat/webapps/
   ```

3. 啟動 Tomcat  
   Tomcat 會自動將 `.war` 解壓為資料夾並部署

4. 訪問網址：  
   ```
   http://localhost:8080/MyApp
   ```

---

## 📦 方法二：部署解壓後的資料夾

### 🔹 步驟：

1. 準備好 Web 專案目錄結構，例如：

```
MyApp/
├── index.jsp
└── WEB-INF/
    └── web.xml
```

2. 複製整個資料夾進 `webapps/`：
   ```
   cp -r MyApp /path/to/tomcat/webapps/
   ```

3. 啟動 Tomcat

4. 訪問網址：
   ```
   http://localhost:8080/MyApp
   ```

---

## 🌐 想變成預設首頁（不加路徑）？

只需將檔案命名為 `ROOT`：

| 做法 | 結果網址 |
|------|-----------|
| 放入 `ROOT.war` | http://localhost:8080/ |
| 或建立 `ROOT/` 資料夾 | http://localhost:8080/ |

---

### ✅ 優點

- ✅ 最簡單、最快速
- ✅ 不需要改任何設定檔
- ✅ 適合快速測試和開發

---

### ⚠️ 注意事項

- 若 `.war` 和資料夾同名（如同時有 `MyApp.war` 和 `MyApp/`），可能出現衝突，建議：
  - 刪掉舊的資料夾再放入新的 `.war`
- Tomcat 每次啟動都會掃描並部署 `webapps` 裡的應用
- 要部署到其他路徑或目錄以外的地方，請改用 `<Context>` 或 conf/Catalina/localhost XML 配置法

---

### 📌 小結

| 你做的事 | Tomcat 幫你做的事 |
|----------|-------------------|
| 把 `.war` 或資料夾放進 `webapps/` | 自動解壓、自動部署、自動可訪問 |

---