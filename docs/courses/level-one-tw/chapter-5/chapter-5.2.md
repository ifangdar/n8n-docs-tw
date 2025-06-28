---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
contentType: tutorial
---

<!-- vale from-microsoft.We = NO -->
<!-- vale from-microsoft.FirstPerson = NO -->
# 2. 將資料插入 Airtable

在工作流程的這個步驟中，您將學習如何使用 [Airtable 節點](/integrations/builtin/app-nodes/n8n-nodes-base.airtable/index.md)將從 HTTP Request 節點接收到的資料插入 Airtable。

/// note | 試算表節點
您可以用另一個試算表應用程式/服務替換 Airtable 節點。例如，n8n 也有 [**Google Sheets**](/integrations/builtin/app-nodes/n8n-nodes-base.googlesheets/index.md) 的節點。
///

完成此步驟後，您的工作流程應該如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.2.json") ]]

## 設定您的表格

如果我們要將資料插入 Airtable，我們首先需要在那裡設定一個表格。要做到這一點：

1. [建立 Airtable 帳號](https://airtable.com/signup){:target="_blank" .external}。
2. 在您的 Airtable 工作區中，從頭開始新增一個新基地並命名它，例如，*初學者課程*。

	<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-2-create-airtable-base.png" alt="建立 Airtable 基地" style="width:100%"><figcaption align = "center"><i>建立 Airtable 基地</i></figcaption></figure>

3. 在初學者課程基地中，預設情況下，您有一個名為 **Table 1** 的表格，包含四個欄位：`Name`、`Notes`、`Assignee` 和 `Status`。這些欄位與我們無關，因為它們不在我們的「訂單」資料集中。這帶出了下一個要點：Airtable 中的欄位名稱必須與節點結果中的欄位名稱相符。透過執行以下操作準備表格：

	* 將表格從 **Table 1** 重新命名為 **orders**，以便更容易識別。
	* 刪除預設建立的 3 個空白記錄。
	* 刪除 `Notes`、`Assignee` 和 `Status` 欄位。
	* 編輯 `Name` 欄位（主要欄位）改為 `orderID`，欄位類型為**數字**。
	* 使用下表作為參考，新增其餘欄位及其欄位類型：

	 | 欄位名稱       | 欄位類型         |
	 |----------------|------------------|
	 | `orderID`      | 數字             |
	 | `customerID`   | 數字             |
	 | `employeeName` | 單行文字         |
	 | `orderPrice`   | 數字             |
	 | `orderStatus`  | 單行文字         |


現在您的表格應該如下所示：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-2-orders-table.png" alt="Airtable 中的訂單表格" style="width:100%"><figcaption align = "center"><i>Airtable 中的訂單表格</i></figcaption></figure>

現在表格已準備好，讓我們返回 n8n 編輯器 UI 中的工作流程。

## 將 Airtable 節點新增到 HTTP Request 節點

新增一個連接到 HTTP Request 節點的 Airtable 節點。

///note | 記住
您可以透過選擇現有節點旁邊的 **+** 圖示來新增連接到現有節點的節點。
///

在節點面板中：

1. 搜尋 Airtable。
2. 從**記錄動作**搜尋結果中選擇**建立記錄**。

這將新增 Airtable 節點到您的畫布並開啟節點詳細資訊視窗。

在 Airtable 節點視窗中，設定以下參數：

- **用於連接的憑證**：
	- 選擇**建立新憑證**。
	- 保持預設選項**使用連接：存取權杖**選中。
	- **存取權杖**：按照 [Airtable 憑證](/integrations/builtin/credentials/airtable.md)頁面的說明建立您的權杖。使用建議的範圍並新增對您的初學者課程基地的存取權限。完成後儲存憑證並關閉憑證視窗。
- **資源**：記錄。
- **操作**：建立。此操作將在表格中建立新記錄。
- **基地**：您可以從列表中選擇您的基地（例如，初學者課程）。
- **表格**：orders。
- **映射欄位模式**：自動映射。在此模式下，傳入的資料欄位必須與 Airtable 中的欄位相同。

## 測試 Airtable 節點

完成設定 Airtable 節點後，透過選擇**執行步驟**來執行它。這可能需要一些時間來處理，但您可以透過在 Airtable 中檢視基地來追蹤進度。

您的結果應該如下所示：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-2-airtable-node.png" alt="Airtable 節點結果" style="width:100%"><figcaption align = "center"><i>Airtable 節點結果</i></figcaption></figure>

所有 30 筆資料記錄現在將出現在 Airtable 的訂單表格中：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-2-airtable-records.png" alt="訂單表格中匯入的記錄" style="width:100%"><figcaption align = "center"><i>訂單表格中匯入的記錄</i></figcaption></figure>

## 接下來是什麼？

**Nathan 🙋**：哇，這個自動化已經非常有用了！但這會將 HTTP Request 節點收集的所有資料插入 Airtable。記得我實際上只需要在表格中插入處理中的訂單並計算已預訂訂單的價格嗎？

**您 👩‍🔧**：當然，沒問題。作為下一步，我將使用一個新節點根據訂單狀態過濾訂單。