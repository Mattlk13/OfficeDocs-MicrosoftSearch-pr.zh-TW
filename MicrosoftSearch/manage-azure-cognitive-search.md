---
title: Microsoft Search (Preview) 中的 Azure 認知搜尋結果
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 06/03/2022
description: 管理 Azure 認知搜尋內容在搜尋結果中顯示的方式
ms.openlocfilehash: 314a7d0efe95585a140a443da57f5beb5ab7b3f0
ms.sourcegitcommit: 7cb5fb6aef414c6914818bb6fa94422345f3e173
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2022
ms.locfileid: "65897312"
---
# <a name="azure-cognitive-search-results-in-microsoft-search-preview"></a>Microsoft Search (Preview) 中的 Azure 認知搜尋結果

[Azure 認知搜尋](/azure/search/search-what-is-azure-search) 是一項雲端搜尋服務，可為開發人員提供基礎結構、API 和工具，以透過 Web、行動和企業應用程式中的私人、異質內容建置豐富的搜尋體驗。 使用此連接器，使用者可以直接從 Microsoft Search 端點搜尋其 Azure 認知搜尋 (ACS) 資料。 連線有一些主要優點：

* **容易使用：** 使用者可以輕鬆快速地尋找儲存在 Azure 認知搜尋 (ACS) 中的重要資訊，而不需要流覽至新的應用程式或頁面。
* **易於尋找：** Bing.com、Office.com 和 SharePoint 中的使用者可以看到 ACS 內容。
* **可自訂的許可權：** ACS 結果可以設定為針對組織中的每個人或特定的 Azure AD 存取控制清單顯示。
* **可調整的結果配置：** 您可以根據資料的架構，使用預設版面配置來格式化 ACS 結果，也可以使用新式結果類型自訂。
* **快速設定：** 設定簡單且容易維護與 ACS 索引的搜尋連線。
* **整合搜尋體驗：** 為了維持一致的體驗，ACS 結果會在所有搜尋進入點之間保持一致。 無論您在何處搜尋，都會以相同的外觀和風格取得相同的結果。

我們的 Azure 認知搜尋連接器目前為預覽狀態。 如果您有興趣加入預覽版，請在 [aka.ms/D365-ACS-Preview-MicrosoftSearch](https://aka.ms/D365-ACS-Preview-MicrosoftSearch)中讓我們知道。

## <a name="what-users-experience"></a>使用者體驗的內容

ACS 結果會出現在搜尋體驗中的專用垂直或索引標籤中。 例如，出現在 Bing 工作結果頁面上的 ACS 結果與出現在 Office.com 或 SharePoint 結果頁面上的結果相同。

:::image type="content" alt-text="Bing 中 Azure 認知搜尋工作結果的結果" source="media/azure-cognitive-search/acs-results-bing.png" lightbox="media/azure-cognitive-search/acs-results-bing.png":::

:::image type="content" alt-text="Office.com 結果中來自 Azure 認知搜尋的結果。" source="media/azure-cognitive-search/acs-results-office.png" lightbox="media/azure-cognitive-search/acs-results-office.png":::

查看我們的 Microsoft Build 2022 影片以取得示範。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4Ybrw]

## <a name="setup"></a>設定

1. 在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)，移至 [[資料來源]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)。
2. 在 [Microsoft 應用程式和服務] 區段中，選取 **[新增應用程式或服務]**。 :::image type="content" alt-text="[資料來源] 頁面，其中已醒目提示 [新增應用程式或服務] 的連結。" source="media/azure-cognitive-search/acs-data-source.png" lightbox="media/azure-cognitive-search/acs-data-source.png":::
3. 選 **取 [Azure 認知搜尋]**，然後選取 [ **下一步]**。
4. 在 [ **連線詳細資料]** 窗格中：

    - 輸入連線名稱和描述。 此名稱將用來作為 Bing、Office.com 和 SharePoint 上 ACS 垂直的顯示名稱。
    - 在 [資料來源] 欄位中，使用 格式 `<your-service>.search.windows.net/indexes/<your-index>` 輸入 ACS 索引的 URL。 將 取代為搜尋服務資源的名稱，並將 `<your-index>` 取代 `<your-service>` 為索引的名稱。
    - 新增您的系統管理員和查詢 API 金鑰。 如需尋找或建立 API 金鑰的相關資訊，請 [參閱尋找現有的金鑰](/azure/search/search-security-api-keys#find-existing-keys)。
    - 選取 [授權] 核取方塊，然後選取 [ **下一步]**。

5. 在 [ **搜尋許可權** ] 頁面上，選擇為組織中的每個人啟用連線，或將結果限制為特定存取控制清單。
6. 在 [ **新增語意屬性標籤]** 窗格中：

    - 如果這些標籤足以顯示結果，請選取您想要針對每個列出的標籤顯示的來源屬性。 選取的屬性將用來建立結果的預設新式結果類型 (MRT) 。 您必須選取 Title 的屬性。 其他則是選擇性但建議的，因為它們讓結果更具資訊性。
    - 如果這些標籤不足以顯示您的結果，您可以將它們保留空白，並在稍後建立自訂 MRT。 如需建立自訂 MRT 的資訊，請 [參閱管理結果類型](/microsoftsearch/manage-result-types)。

7. 確認輸入的資訊正確無誤，然後選取 [ **完成]**。
1. 建立連線之後，系統會再次將您重新導向至 [資料來源] 頁面。 如果您想要變更出現在 ACS 垂直上的顯示名稱，請選取新建立的 ACS 連線下方的 **[垂直編輯** ]。 :::image type="content" alt-text="具有 [編輯垂直名稱] 連結的 Azure 認知搜尋連線。" source="media/azure-cognitive-search/acs-custom-vertical.png" lightbox="media/azure-cognitive-search/acs-custom-vertical.png":::

如需垂直的詳細資訊，請[參閱管理搜尋垂直。](/microsoftsearch/manage-verticals) 成功設定 ACS 連線之後，您應該會看到線上狀態 [就緒]。

> [!NOTE]
> 啟用連線之後，由於系統各層的快取，新的垂直和 ACS 結果最多可能需要 24 小時才會出現在您的 Microsoft Search 端點中。

## <a name="query-patterns"></a>查詢模式

在 Microsoft Search 中搜尋 ACS 結果支援簡單的查詢語法。 這包括關鍵字查詢語言、AND、OR 和 NOT 運算子。 如需詳細資訊，請參閱 [Azure 認知搜尋中的簡單查詢語法](/azure/search/query-simple-syntax)。 若要調整可搜尋的資料欄位，您可以 [修改 ACS 索引的欄位屬性](/azure/search/search-what-is-an-index#field-attributes)。

## <a name="customize-result-types"></a>自訂結果類型

若要改變 ACS 結果的格式化方式，例如版面配置或顯示的欄位，您可以建立自訂的新式結果類型。 若要開始使用，請移至 Microsoft 365 系統管理中心的 [ [結果類型] 設定](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/resulttypes) 。 如需詳細資訊，請 [參閱管理結果類型](/microsoftsearch/manage-result-types)。

## <a name="edit-the-connection"></a>編輯連線

啟用連線之後，您可以修改端點和連線名稱。 在 [[資料來源](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)] 的已設定連線下方，選取 [編輯] 進行變更。  :::image type="content" alt-text="具有連線詳細資料的 Azure 認知搜尋連線和窗格。" source="media/azure-cognitive-search/acs-edit-settings.png" lightbox="media/azure-cognitive-search/acs-edit-settings.png":::

若要停用連線，請清除 [ **為您的組織啟用此聯** 機] 核取方塊和 [ **儲存]**。

## <a name="troubleshooting"></a>疑難排解

如果新式結果類型中特定結果的任何欄位空白，功能變數名稱會以大括弧顯示。

:::image type="content" alt-text="以大括弧括住範例欄位 1 和 2 的 ACS 垂直。" source="media/azure-cognitive-search/acs-result-troubleshooting.png" lightbox="media/azure-cognitive-search/acs-result-troubleshooting.png":::

若要減輕此問題，請建立自訂 MRT 並新增這一行： `"$when": "${exampleFieldName != null && exampleFieldName != ''}"` ，並以適當的功能變數名稱取代 `exampleFieldName` 。 針對 MRT 中任何可以是空的欄位執行此動作。

如果您在使用預覽連接器時有意見反應或問題，請 [與我們連絡](https://aka.ms/ACSConnectorFeedback)。
