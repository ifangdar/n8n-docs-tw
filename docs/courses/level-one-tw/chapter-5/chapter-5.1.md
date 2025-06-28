---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
contentType: tutorial
---

<!-- vale from-microsoft.We = NO -->
<!-- vale from-microsoft.FirstPerson = NO -->
# 1. 從資料倉儲獲取資料

在工作流程的這個部分，您將學習如何使用 [**HTTP Request**](/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/index.md) 節點透過發出 HTTP 請求來獲取資料。

完成本節後，您的工作流程將如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.1.json") ]]

首先，讓我們為建構 Nathan 的工作流程設定場景。

## 建立新工作流程

開啟您的編輯器 UI 並使用以下兩個可能的命令之一建立新工作流程：

- 在鍵盤上選擇 ++ctrl+alt+n++ 或 ++cmd+option+n++。
- 開啟左側選單，導覽至**工作流程**，然後選擇**新增工作流程**。

將此新工作流程命名為「Nathan 的工作流程」。

您需要做的第一件事是從 ABCorp 的舊資料倉儲獲取資料。

在前一章中，您使用了為特定服務（Hacker News）設計的動作節點。但並非所有應用程式或服務都有專用節點，例如 Nathan 公司的舊版資料倉儲。

雖然我們無法直接匯出資料，但 Nathan 告訴我們資料倉儲有幾個 API 端點。這就是我們在 n8n 中使用 [HTTP Request](/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/index.md) 節點存取資料所需的全部。

/// note | 沒有該服務的節點？
HTTP Request 節點是最通用的節點之一，允許您發出 HTTP 請求以從應用程式和服務查詢資料。您可以使用它來存取在 n8n 中沒有專用節點的應用程式或服務的資料。
///

## 新增 HTTP Request 節點

現在，在您的編輯器 UI 中，按照您在[新增節點](/courses/level-one/chapter-1.md#adding-nodes)課程中學到的方式新增 HTTP Request 節點。節點視窗將開啟，您需要在其中設定一些參數。

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-1-http-request-node.png" alt="HTTP Request 節點" style="width:100%"><figcaption align = "center"><i>HTTP Request 節點</i></figcaption></figure>

此節點將使用憑證。

/// note | 憑證
[憑證](/glossary.md#credential-n8n)是識別使用者或服務的唯一資訊片段，允許它們存取應用程式或服務（在我們的案例中，表示為 n8n 節點）。憑證的常見形式是使用者名稱和密碼，但根據服務的不同，它們可以採用其他形式。
///

在這種情況下，您將需要在註冊本課程時從 n8n 收到的電子郵件中包含的 ABCorp 資料倉儲 API 憑證。如果您尚未註冊，請[在此註冊](https://n8n-community.typeform.com/to/PDEMrevI){:target="_blank" .external-link}。

在 HTTP Request 節點的**參數**中，進行以下調整：

- **方法**：這應該預設為 GET。確保設定為 GET。
- **URL**：新增您在註冊本課程時收到的電子郵件中的**資料集 URL**。
- **傳送標頭**：將此控制項切換為 true。在**指定標頭**中，確保選擇**使用下面的欄位**。
    - **標頭參數** > **名稱**：輸入 `unique_id`。
    - **標頭參數** > **值**：您在註冊本課程時收到的電子郵件中的唯一 ID。
- **認證**：選擇**通用憑證類型**。此選項在允許您存取資料之前需要憑證。
    - **通用認證類型**：選擇**標頭認證**。（在您選擇通用憑證類型進行認證後，此欄位將出現。）
    - **標頭認證的憑證**：要新增您的憑證，選擇**+ 建立新憑證**。這將開啟憑證視窗。
    - 在憑證視窗中，將**名稱**設定為您在註冊本課程時收到的電子郵件中的**標頭認證名稱**。
    - 在憑證視窗中，將**值**設定為您在註冊本課程時收到的電子郵件中的**標頭認證值**。
    - 在憑證視窗中選擇**儲存**按鈕以儲存您的憑證。您的**憑證連接**視窗應該如下所示：
    <figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-1-http-request-node-credentials.png" alt="HTTP Request 節點憑證" style="width:100%"><figcaption align = "center"><i>HTTP Request 節點憑證</i></figcaption></figure>

/// note | 憑證命名
新憑證名稱預設遵循「<節點名稱>帳戶」格式。您可以透過點擊名稱來重新命名憑證，類似於重新命名節點。良好的做法是給它們命名，以識別應用程式/服務、類型和憑證的用途。命名慣例使追蹤和識別您的憑證變得更容易。
///

儲存後，退出憑證視窗以返回 HTTP Request 節點。

## 獲取資料

在 HTTP Request 節點視窗中選擇**執行步驟**按鈕。HTTP 請求結果的表格檢視應該如下所示：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-1-http-request-node-window.png" alt="HTTP Request 節點輸出" style="width:100%"><figcaption align = "center"><i>HTTP Request 節點輸出</i></figcaption></figure>

這個檢視應該讓您從[建構迷你工作流程](/courses/level-one/chapter-2.md)頁面感到熟悉。

這是來自 ABCorp 資料倉儲的資料，Nathan 需要處理這些資料。此資料集包含來自 30 個客戶的銷售資訊，有五個欄位：

- `orderID`：每個訂單的唯一 ID。
- `customerID`：每個客戶的唯一 ID。
- `employeeName`：負責客戶的 Nathan 同事的姓名。
- `orderPrice`：客戶訂單的總價格。
- `orderStatus`：客戶的訂單狀態是 `booked` 還是仍在 `processing`。

## 接下來是什麼？

**Nathan 🙋**：太棒了！您已經只用一個節點就自動化了我工作的重要部分。現在，我不必每次需要時都手動存取資料，我可以使用 HTTP Request 節點自動獲取資訊。

**您 👩‍🔧**：沒錯！在下一步中，我將幫助您更進一步，將您檢索到的資料插入 Airtable。