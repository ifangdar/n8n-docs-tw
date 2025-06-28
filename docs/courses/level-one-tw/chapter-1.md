---
#https://www.notion.so/n8n/Frontmatter-432c2b8dff1f43d4b1c8d20075510fe4
contentType: tutorial
---

<!-- vale from-microsoft.We = NO -->
<!-- vale from-microsoft.FirstPerson = NO -->
# 瀏覽編輯器 UI

在本課程中，您將學習如何瀏覽[編輯器 UI](/glossary.md#editor-n8n)。我們將逐步介紹[畫布](/glossary.md#canvas-n8n)，並向您展示每個圖示的含義以及在 n8n 中建構工作流程時需要的功能位置。

/// warning | n8n 版本
本課程基於 n8n 版本 1.82.1。在其他版本中，某些使用者介面可能看起來不同，但這不應該影響核心功能。
///

## 開始使用

從設定 n8n 開始。

我們建議從 [n8n Cloud](https://app.n8n.cloud/register) 開始，這是一個託管解決方案，不需要安裝且包含免費試用。

/// note | 替代設定
如果 n8n Cloud 不適合您，您可以[使用 Docker 自託管](/hosting/installation/docker.md)。這是一個進階選項，僅建議熟悉託管服務、Docker 和命令列的技術使用者使用。
///

有關設定 n8n 的不同方式的更多詳細資訊，請參閱我們的[平台文件](/choose-n8n.md#platforms)。

一旦您執行了 n8n，請在瀏覽器視窗中開啟編輯器 UI。登入您的 n8n 實例。選擇**概覽**，然後選擇**建立工作流程**以檢視主畫布。

它應該看起來像這樣：

<figure><img src="/_images/courses/level-one/chapter-one/l1-c1-editor-ui.png" alt="編輯器 UI" style="width:100%"><figcaption align = "center"><i>編輯器 UI</i></figcaption></figure>

## 編輯器 UI 設定

編輯器 UI 是您建構[工作流程](/workflows/index.md)的網頁介面。您可以從編輯器 UI 存取所有工作流程和[憑證](/glossary.md#credential-n8n)，以及支援頁面。

### 左側面板

在**編輯器 UI**的左側，有一個面板包含管理工作流程的核心功能和設定。透過選擇小箭頭圖示來展開和收合它。

面板包含以下部分：

- **概覽**：包含您有權存取的所有工作流程和憑證。在本課程期間，在此建立新的工作流程。
- **專案**：（社群版不可用）專案將工作流程和憑證分組。您可以在專案中為使用者分配[角色](/user-management/rbac/role-types.md)，以控制他們在專案中可以做什麼。預設情況下提供**個人**專案。
- **管理面板**：僅限 n8n Cloud。存取您的 n8n 實例使用情況、計費和版本設定。
- **範本**：預製工作流程的集合。開始使用常見用例的好地方。
- **變數**：用於在工作流程中儲存和存取固定資料。此功能在專業版和企業版計劃中提供。
- **所有執行**：包含有關您的工作流程執行的資訊。
- **幫助**：包含有關 n8n 產品和社群的資源。
- **更新**：（當有更新可用時）任何最近產品更新的指示器。
- **設定**：在您的使用者名稱旁的省略號（`...`）選單下。管理使用者並存取各種功能的設定。

<figure style="text-align: center;"><img src="/_images/courses/level-one/chapter-one/l1-c1-side-panel.png" alt="編輯器 UI 左側選單" style="height: 600px;"><figcaption align = "center"><i>編輯器 UI 左側選單</i></figcaption></figure>

### 頂部列

**編輯器 UI**的頂部列包含以下資訊：

- **工作流程名稱**：預設情況下，n8n 將新工作流程命名為「我的工作流程」，但您可以隨時編輯名稱。
- **+ 新增標籤**：標籤可幫助您按類別、用例或任何對您相關的內容組織工作流程。標籤是選擇性的。
- **非活動/活動切換**：此按鈕啟用或停用當前工作流程。預設情況下，工作流程是停用的。
- **分享**：您可以在入門版、專業版和企業版計劃中與他人分享和協作工作流程。
- **儲存**：此按鈕儲存當前工作流程。
- **歷史記錄**：儲存工作流程後，您可以在此處檢視以前的版本。

<figure><img src="/_images/courses/level-one/chapter-one/l1-c1-top-bar.png" alt="編輯器 UI 頂部列" style="width:100%"><figcaption align = "center"><i>編輯器 UI 頂部列</i></figcaption></figure>

### 畫布

**畫布**是編輯器 UI 中的灰色點狀網格背景。它顯示幾個圖示和一個具有不同功能的節點：

- 用於縮放畫布以適應螢幕、放大或縮小畫布以及整理螢幕上節點的按鈕。
- 新增第一個節點後，會出現**執行工作流程**按鈕。當您點擊它時，n8n 會按順序執行畫布上的所有節點。
- 內部有**+**符號的按鈕。此按鈕開啟節點面板。
- 內部有便條圖示的按鈕。此按鈕向畫布新增[便利貼](/workflows/components/sticky-notes.md)（懸停在右上角 + 圖示時可見）。
- 帶有文字「新增第一步」的虛線方塊。這是您新增第一個節點的地方。

<figure><img src="/_images/courses/level-one/chapter-one/l1-c1-canvas.png" alt="工作流程畫布" style="width:100%"><figcaption align = "center"><i>工作流程畫布</i></figcaption></figure>

/// note | 移動畫布
您可以透過三種方式移動工作流程畫布：

- 在畫布上選擇 ++ctrl+left-button++ 並移動它。
- 在畫布上選擇 ++middle-button++ 並移動它。
- 將兩根手指放在觸控板上並滑動。
///


暫時不用擔心工作流程執行和啟用；我們稍後會在課程中解釋這些概念。

## 節點

您可以將節點視為建構區塊，它們提供不同的功能，當組合在一起時，構成一個功能機器：自動化工作流程。

/// note | 節點
節點是工作流程中的單個步驟：(a) 載入、(b) 處理或 (c) 傳送資料的步驟。
///

根據其功能，n8n 將節點分為四種類型：

- **應用程式**或**動作節點**新增、刪除和編輯資料；請求和傳送外部資料；並在其他系統中觸發事件。請參閱[動作節點庫](/integrations/builtin/app-nodes/index.md)以獲取這些節點的完整列表。
- **觸發節點**啟動工作流程並提供初始資料。請參閱[觸發節點庫](/integrations/builtin/trigger-nodes/index.md)以獲取觸發節點列表。
- **核心節點**可以是觸發或應用程式節點。雖然大多數節點連接到特定的外部服務，但核心節點提供邏輯、排程或通用 API 呼叫等功能。請參閱[核心節點庫](/integrations/builtin/core-nodes/index.md)以獲取核心節點的完整列表。
- **叢集節點**是一起工作以在工作流程中提供功能的節點群組，主要用於 AI 工作流程。請參閱[叢集節點](/integrations/builtin/cluster-nodes/index.md)以獲取更多資訊。

/// note | 了解更多
請參閱[節點類型](/integrations/builtin/node-types.md)以獲取所有節點類型的更詳細說明。
///

### 尋找節點

您可以在編輯器 UI 右側的**節點面板**中找到所有可用的節點。有三種方式可以開啟節點面板：

- 點擊畫布右上角的**+**圖示。
- 點擊畫布上現有節點右側的**+**圖示（您要新增另一個節點的節點）。
- 在鍵盤上點擊 ++tab++ 鍵。

<figure style="text-align: center; width:50%; margin:auto;"><img src="/_images/courses/level-one/chapter-one/l1-c1-node-menu-drilldown.gif" alt="節點面板"><figcaption align = "center"><i>節點面板</i></figcaption></figure>

在節點面板中，請注意，當新增第一個節點時，您將看到不同的觸發節點類別。新增觸發節點後，您會看到節點面板變更為顯示進階 AI、應用程式中的動作、資料轉換、流程、核心和人機協作節點。

如果您想尋找特定節點，請使用節點面板頂部的搜尋輸入。


### 新增節點

有兩種方式將節點新增到畫布：

- 在節點面板中選擇您想要的節點。新節點將自動連接到畫布上選定的節點。
- 從節點面板拖放節點到畫布。

### 節點按鈕

如果您將滑鼠懸停在節點上，您會注意到頂部出現三個圖示：

- 執行節點（播放圖示）
- 停用/啟用節點（電源圖示）
- 刪除節點（垃圾桶圖示）

還會有一個省略號圖示，它會開啟包含其他[節點選項](/workflows/components/nodes.md#node-controls)的內容選單。

/// note | 移動工作流程
要在畫布上移動工作流程，請用滑鼠或 ++ctrl+a++ 選擇所有節點，選擇並按住節點，然後將其拖動到畫布上的任何位置。
///

## 總結

在本課程中，您學習了如何瀏覽編輯器 UI、圖示的含義、如何存取左側和節點面板，以及如何將節點新增到畫布。

在下一課中，您將建構一個迷你工作流程，以實踐到目前為止所學的內容。