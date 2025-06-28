---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
contentType: tutorial
---

<!-- vale from-microsoft.We = NO -->
<!-- vale from-microsoft.FirstPerson = NO -->
# 3. 過濾訂單

在工作流程的這個步驟中，您將學習如何使用條件邏輯過濾資料，以及如何使用 [If 節點](/integrations/builtin/core-nodes/n8n-nodes-base.if.md)在節點中使用表達式。

完成此步驟後，您的工作流程應該如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.3.json") ]]

要只將處理中的訂單插入 Airtable，我們需要按 `orderStatus` 過濾我們的資料。基本上，我們想告訴程式，*如果* `orderStatus` 是 processing，*則*將所有具有此狀態的記錄插入 Airtable；*否則*，例如，如果 `orderStatus` 不是 *processing*，計算所有具有其他 `orderStatus`（`booked`）的訂單總和。

這個 if-then-else 命令是條件邏輯。在 n8n 工作流程中，您可以使用 [If 節點](/integrations/builtin/core-nodes/n8n-nodes-base.if.md)新增條件邏輯，它根據比較操作有條件地分割工作流程。

/// note | If 與 Switch
如果您需要根據多於布林值（true 和 false）來過濾資料，請使用 [Switch 節點](/integrations/builtin/core-nodes/n8n-nodes-base.switch.md)。Switch 節點類似於 If 節點，但支援多個輸出連接器。
///

## 在 Airtable 節點之前新增 If 節點

首先，讓我們在從 HTTP Request 節點到 Airtable 節點的連接之間新增一個 If 節點：

1. 將滑鼠懸停在 **HTTP Request** 節點和 **Airtable** 節點之間的箭頭連接上。
2. 選擇 HTTP Request 節點和 Airtable 節點之間的 **+** 符號。

## 設定 If 節點

選擇加號會移除 Airtable 節點到 HTTP 請求的連接。現在，讓我們新增連接到 HTTP Request 節點的 If 節點：

1. 搜尋 If 節點。
2. 當它出現在搜尋中時選擇它。

對於 If 節點，我們將使用表達式。

/// note | 表達式
[表達式](/glossary.md#expression-n8n)是程式語言中的字元和符號串，可以評估以獲得值，通常根據其輸入。在 n8n 工作流程中，您可以在節點中使用表達式來引用另一個節點的輸入資料。在我們的範例中，If 節點引用 HTTP Request 節點輸出的資料。
///

在 If 節點視窗中，設定參數：

- 設定 `value1` 佔位符為 `{{ $json.orderStatus }}`，步驟如下：
    1. 將滑鼠懸停在 value1 欄位上。
    2. 選擇 `value1` 欄位右側的**表達式**標籤。
    3. 接下來，透過選擇連結圖示開啟表達式編輯器：
    <figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-3-if-node-open-editor.png" alt="開啟表達式編輯器" style="width:100%"><figcaption align = "center"><i>開啟表達式編輯器</i></figcaption></figure>
    4. 使用左側面板選擇 **HTTP Request** > **orderStatus** 並將其拖曳到視窗中央的**表達式**欄位中。
    <figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-3-if-node-expression-editor.png" alt="IF 節點中的表達式編輯器" style="width:100%"><figcaption align = "center"><i>If 節點中的表達式編輯器</i></figcaption></figure>
    6. 新增表達式後，關閉**編輯表達式**對話框。

- **操作**：選擇 **String** > **is equal to**
- 設定 `value2` 佔位符為 `processing`。

/// warning | 資料類型
選擇**操作**時，請確保選擇正確的資料類型（boolean、date & time、number 或 string）。
///

選擇**執行步驟**來測試 If 節點。

您的結果應該如下所示：

<figure><img src="/_images/courses/level-one/chapter-five/l1-c5-5-3-if-node-output.png" alt="If 節點輸出" style="width:100%"><figcaption align = "center"><i>If 節點輸出</i></figcaption></figure>

請注意，具有 `processing` 訂單狀態的訂單應該顯示在 **True 分支**輸出中，而具有 `booked` 訂單狀態的訂單應該顯示在 **False 分支**輸出中。

完成後關閉 If 節點詳細檢視。

## 將資料插入 Airtable

接下來，我們想將這些資料插入 Airtable。還記得 Nathan 在[將資料插入 Airtable](/courses/level-one/chapter-5/chapter-5.2.md)課程結束時說的話嗎？

> 我實際上只需要在表格中插入處理中的訂單...

由於 Nathan 只需要表格中的 `processing` 訂單，我們將 Airtable 節點連接到 If 節點的 `true` 連接器。

在這種情況下，由於 Airtable 節點已經在我們的畫布上，選擇 **If 節點** `true` 連接器並將其拖曳到 Airtable 節點。

此時重新測試 Airtable 節點是個好主意。在執行之前，開啟您在 Airtable 中的表格並刪除所有現有行。然後在 n8n 中開啟 Airtable 節點視窗並選擇**執行步驟**。

檢視您在 Airtable 中的資料，確保您的工作流程只新增了正確的訂單（那些 `orderStatus` 為 `processing` 的訂單）。現在應該有 14 筆記錄而不是 30 筆。

在這個階段，您的工作流程應該如下所示：

[[ workflowDemo("file:////courses/level-one/chapter-5/chapter-5.3.json") ]]

## 接下來是什麼？

**Nathan 🙋**：這個 If 節點對於過濾資料非常有用！現在我有了所有關於處理中訂單的資訊。我實際上只需要 `employeeName` 和 `orderID`，但我想我可以保留所有其他欄位以防萬一。

**您 👩‍🔧**：實際上，我不建議這樣做。插入更多資料需要更多的計算能力，資料傳輸速度較慢且需要更長時間，並且在您的表格中佔用更多儲存資源。在這種特殊情況下，14 筆記錄和 5 個欄位可能看起來不會產生顯著差異，但如果您的業務增長到數千筆記錄和數十個欄位，事情會累積起來，即使是一個額外的欄位也會影響效能。

**Nathan 🙋**：哦，這很有用。您能從處理中的訂單中只選擇兩個欄位嗎？

**您 👩‍🔧**：當然，我會在下一步中做到這一點。