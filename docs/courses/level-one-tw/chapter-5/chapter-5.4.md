---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
contentType: tutorial
---

<!-- vale from-microsoft.We = NO -->
<!-- vale from-microsoft.FirstPerson = NO -->
# 4. 為處理中訂單設定值

在工作流程的這個步驟中，您將學習如何在使用 Edit Fields (Set) 節點將資料傳輸到 Airtable 之前選擇和設定資料。完成此步驟後，您的工作流程應該如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.4.json") ]]

Nathan 工作流程的下一步是過濾資料，只將所有 `processing` 訂單的 `employeeName` 和 `orderID` 插入 Airtable。

為此，您需要使用 [Edit Fields (Set) 節點](/integrations/builtin/core-nodes/n8n-nodes-base.set.md)，它允許您選擇和設定要從一個節點傳輸到另一個節點的資料。

/// note | Edit Fields 節點
Edit Fields 節點可以設定全新的資料以及覆寫已經存在的資料。此節點在期望從先前節點傳入資料的工作流程中至關重要，例如將值插入試算表或資料庫時。
///

## 在 Airtable 節點之前新增另一個節點

在您的工作流程中，從 **If 節點**的 `true` 連接器在 **Airtable 節點**之前新增另一個節點，方法與我們在[過濾訂單](/courses/level-one/chapter-5/chapter-5.3.md#add-if-node-before-the-airtable-node)課程中所做的相同。如果您的畫布感覺擁擠，請隨意將 Airtable 節點拖得更遠。

## 設定 Edit Fields 節點

現在，在您選擇了來自 If 節點 `true` 連接器的 **+** 符號後，搜尋 **Edit Fields (Set) 節點**。

開啟 Edit Fields 節點視窗後，設定這些參數：

- 確保**模式**設定為**手動映射**。
- 雖然您可以使用我們在[過濾訂單](/courses/level-one/chapter-5/chapter-5.3.md)課程中使用的**表達式編輯器**，但這次，讓我們將欄位從**輸入**拖曳到**要設定的欄位**：
    - 拖曳 **If** > **orderID** 作為第一個欄位。
    - 拖曳 **If** > **employeeName** 作為第二個欄位。
- 確保**包含其他輸入欄位**設定為 false。

選擇**執行步驟**。您應該看到以下結果：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-4-set-node.png" alt="Edit Fields (Set) 節點" style="width:100%"><figcaption align = "center"><i>Edit Fields (Set) 節點</i></figcaption></figure>

## 將資料新增到 Airtable

接下來，讓我們將這些值插入 Airtable：

1. 前往您的 Airtable 基地。
2. 新增一個名為 `processingOrders` 的新表格。
3. 用兩個新欄位替換現有欄位：
    - `orderID`（主要欄位）：數字
    - `employeeName`：單行文字

    ///note | 提醒
    如果您遇到困難，請參考[將資料插入 Airtable](/courses/level-one/chapter-5/chapter-5.2.md)課程。
    ///

4. 刪除新表格中的三個空行。
5. 在 n8n 中，將 Edit Fields 節點**連接器連接到 **Airtable 節點**。
6. 更新 Airtable 節點設定以指向新的 `processingOrders` 表格而不是 `orders` 表格。
7. 測試您的 Airtable 節點，確保它將記錄插入新的 `processingOrders` 表格。

在這個階段，您的工作流程現在應該如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.4.json") ]]

## 接下來是什麼？

**Nathan 🙋**：您已經自動化了我一半的工作！現在我仍然需要為我的同事計算已預訂的訂單。我們也可以自動化嗎？

**您 👩‍🔧**：是的！在下一步中，我將在節點中使用一些 JavaScript 程式碼來計算已預訂的訂單。