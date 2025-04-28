# 1. 在 Tomcat `conf/context.xml` 中統一配置 MySQL 資料庫連線

打開 `conf/context.xml`，在 `<Context>` 標籤裡面加上這段：

```xml
<Context>

    <!-- 監控 web.xml 變更 -->
    <WatchedResource>WEB-INF/web.xml</WatchedResource>

    <!-- 配置一個全局的資料庫連線池 -->
    <Resource 
        name="jdbc/MyDB" 
        auth="Container"
        type="javax.sql.DataSource" 
        maxTotal="100" 
        maxIdle="30" 
        maxWaitMillis="10000"
        username="你的資料庫帳號" 
        password="你的資料庫密碼" 
        driverClassName="com.mysql.cj.jdbc.Driver"
        url="jdbc:mysql://localhost:3306/你的資料庫名稱?serverTimezone=UTC&useSSL=false" />
    
</Context>
```

🔹這段意思是：  
- 建立一個名字叫 `jdbc/MyDB` 的連線池資源。
- 包含連線用的帳號、密碼、URL、驅動類名等資訊。
- 這個連線池會由 Tomcat 管理（例如最大 100 個連線）。

> ⚡ 注意：要把 `你的資料庫帳號`、`你的資料庫密碼` 和 `你的資料庫名稱` 替換成你自己用的資料。

---

# 2. 在 `JDBCUtils.java` 中通過 JNDI 獲取連線

`JNDI`（Java Naming and Directory Interface）可以讓你的程式**向 Tomcat 要**這個連線池，不用自己硬編寫帳密。

範例 `JDBCUtils.java`：

```java
package com.example.utils;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.sql.DataSource;
import java.sql.Connection;

public class JDBCUtils {

    private static DataSource dataSource;

    static {
        try {
            // 1. 初始化 JNDI 內容
            Context initContext = new InitialContext();
            // 2. 從環境中查找資源（名字要跟 context.xml 裡的 name 一樣）
            dataSource = (DataSource) initContext.lookup("java:comp/env/jdbc/MyDB");
        } catch (Exception e) {
            e.printStackTrace();
            throw new ExceptionInInitializerError(e);
        }
    }

    /**
     * 從連線池取得一個 Connection 連線
     */
    public static Connection getConnection() throws Exception {
        return dataSource.getConnection();
    }

    /**
     * 這裡也可以順便加一個關閉連線的方法（可選）
     */
    public static void close(AutoCloseable resource) {
        if (resource != null) {
            try {
                resource.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

---

# 補充說明：

| 項目 | 說明 |
|:---|:---|
| `java:comp/env/jdbc/MyDB` | 必須寫這樣的格式，固定有 `java:comp/env/` 前綴，後面跟你在 `context.xml` 設的 `name`。 |
| `DataSource` | 是一個連線池物件，你每次調 `getConnection()`，Tomcat 會給你一條新連線。 |
| `AutoCloseable` | 因為 `Connection`、`Statement`、`ResultSet` 都是 AutoCloseable，可以用這種統一的關閉方法。 |

---

# 整體流程簡單整理一下：

```
1. 在 conf/context.xml 中定義資料庫連線池 (Resource)
2. 程式裡面使用 JNDI 查找連線池 (lookup)
3. 透過連線池拿 Connection
4. 用完記得關閉 Connection
```

---

要不要我再順便教你一個**簡單的測試方法**？  
比如寫個 `main()`，直接用 `JDBCUtils.getConnection()` 測試能不能成功連到資料庫？🚀  
要的話我可以直接附上喔～要不要？