# 瀏覽器和 Session 之間的關聯機制（技術內幕版）
![](./images/瀏覽器和%20Session%20之間關連的技術內幕.png "")

**核心是：Session 本身存放在伺服器，瀏覽器端透過 Cookie (或 URL重寫) 來識別 Session。**  

## 1. 什麼是 Session？

- **Session（會話）** 是伺服器端的一塊記憶體資料，專門用來存放某個「瀏覽器客戶端」在短時間內的交互狀態。  
- 比如：登入資訊、購物車內容、偏好設置等。

✅ **重要點**：**Session 資料存在伺服器，不存在瀏覽器。**

---

## 2. 問題：伺服器怎麼知道是同一個瀏覽器？

瀏覽器關掉再打開、不同頁面之間跳轉... 伺服器要能「認得出來」是同一個用戶。

👉 **這就需要一個「身份識別標籤」，稱為 `Session ID`。**

---

## 3. 瀏覽器和 Session 的關聯技術：兩種方法

### 3.1 Cookie 傳遞 Session ID （主流做法）
- 第一次連線時，伺服器創建一個 Session，並產生一個唯一的 **Session ID**。
- 伺服器透過**Set-Cookie**響應頭，告訴瀏覽器把這個 Session ID 存起來。
- 瀏覽器之後每次請求都會自動帶上這個 Cookie（包含 Session ID）給伺服器。

🔵 **流程示意：**
```plaintext
1. 瀏覽器發送請求（無 Session）
2. 伺服器產生 Session，並回應：
    Set-Cookie: JSESSIONID=ABC123; Path=/; HttpOnly
3. 瀏覽器收到後把 JSESSIONID 存入 Cookie
4. 以後每次請求，自動在請求頭帶上：
    Cookie: JSESSIONID=ABC123
5. 伺服器根據 JSESSIONID 找到對應的 Session 資料
```

✅ **特點**：隱式、安全（可以設置 HttpOnly、Secure），不改變 URL。

---

### 3.2 URL 重寫（URL Rewriting）（備用方案）
- 有些情況（比如瀏覽器禁用 Cookie），就沒辦法用 Cookie 傳 Session ID。
- 伺服器會**把 Session ID 附加到 URL** 上，像這樣：

```plaintext
http://localhost:8080/myapp/index.jsp;jsessionid=ABC123
```
- 伺服器解析 URL 的 `jsessionid`，認出用戶的 Session。

✅ **特點**：兼容無 Cookie 的環境，但 URL 變長、不太安全（容易被偷）。

---

# 總結

| 技術點 | 說明 |
|:---|:---|
| Session 存哪裡？ | 伺服器記憶體 |
| 瀏覽器怎麼認？ | 依靠 Session ID |
| Session ID 怎麼傳？ | 通常透過 Cookie，自動帶回 |
| 沒有 Cookie 怎麼辦？ | 用 URL 重寫，把 Session ID 帶到網址上 |
| Session 何時失效？ | 超時、自動刪除、手動刪除 |

---