---
title: 管理搜尋結果版面配置
ms.author: jypal
author: jypal6
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 使用適應性卡，建立配置以查看自訂的搜尋結果
ms.openlocfilehash: 4120d9a1a979b57ce8e6c34d93a585d07c440605
ms.sourcegitcommit: 33d23aac77c3f6a66f1509c4d44d8d1ed462d92a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2021
ms.locfileid: "61356997"
---
<!-- markdownlint-disable no-hard-tabs -->
# <a name="create-a-layout-to-customize-search-results"></a>建立版式以自訂搜尋結果

您可以使用 [搜尋版面配置設計工具]，設計自訂垂直方向的結果版面配置。 您可以選擇版面設計工具中提供的範本，以開始設計版面配置，並在符合您的需求時加以使用。 或者，您可以選擇以各種方式編輯這些範本，以符合您的需求。 例如，新增/移除影像、新增/移除文字，以及修改文字。 若所有範本都不符合您的需求，您可以選擇使用空白範本來開始設計您的版面配置。  

準備好版面配置之後，請使用 [自我調整卡範本語言](/adaptive-cards/templating/language) 來建立結果版面 JSON，用來定義結果類型。 您可以使用版面配置設計工具中的對應步驟，將結果屬性對應至 layout。  

## <a name="create-a-layout-on-your-own"></a>自行建立版面配置

您必須瞭解 [自訂卡](/adaptive-cards/authoring-cards/getting-started) 及其 [架構](https://adaptivecards.io/explorer/)，才能自行建立版面配置。 搜尋結果版面配置使用自我調整卡所提供之元素的子集，您可以使用版面配置設計工具來瞭解支援的元素集合。  

建立您自己的版面配置時，請使用連接器中的資料建立自我調整卡的版面配置，然後完成 layout。
建立您自己的版面配置有兩個主要步驟：

- 設計版面配置。
- 將資料與範本分開。

### <a name="design-the-layout"></a>設計版面配置

在這個範例中，我們會顯示具有頁首、標誌、連結及描述文字的版面配置。

![具有標頭、連結及描述的版面配置範例。](media/Verts-ExampleLayout.png)

以下是版面配置的關聯 JSON 檔案：

```json
{ 
    "type": "AdaptiveCard", 
    "version": "1.3", 
    "body": [ 
        { 
            "type": "ColumnSet", 
            "columns": [ 
                { 
                    "type": "Column", 
                    "width": "auto", 
                    "items": [ 
                        { 
                            "type": "Image", 
                            "url": "https://searchuxcdn.blob.core.windows.net/designerapp/images/OOTBLayouts/search.png", 
                            "altText": "Thumbnail image", 
                            "horizontalAlignment": "center", 
                            "size": "small" 
                        } 
                    ], 
                    "horizontalAlignment": "center" 
                }, 
                { 
                    "type": "Column", 
                    "width": 10, 
                    "items": [ 
                        { 
                            "type": "TextBlock", 
                            "text": "[Contoso Solutions](https://contoso.com)", 
                            "weight": "bolder", 
                            "color": "accent", 
                            "size": "medium", 
                            "maxLines": 3 
                        }, 
                        { 
                            "type": "TextBlock", 
                            "text": "[https://contoso.com](https://contoso.com)", 
                            "weight": "bolder", 
                            "spacing": "small", 
                            "maxLines": 3 
                        }, 
                        { 
                            "type": "TextBlock", 
                            "text": "Marketing team at Contoso.., and looking at the Contoso Marketing documents on the team site. This contains the data from FY20 and will taken over to FY21...Marketing Planning is ongoing for FY20..", 
                            "maxLines": 3, 
                            "wrap": true 
                        } 
                    ], 
                    "spacing": "medium" 
                } 
            ] 
        } 
    ], 
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json" 
} 
```

### <a name="separate-the-data-from-the-layout"></a>分隔資料與版面配置

您可以從版面配置中分隔資料，並系結資料。

以下是系結資料後的版面配置 JSON：

```json
{ 
    "type": "AdaptiveCard", 
    "version": "1.3", 
    "body": [ 
        { 
            "type": "ColumnSet", 
            "columns": [ 
                { 
                    "type": "Column", 
                    "width": "auto", 
                    "items": [ 
                        { 
                            "type": "Image", 
                            "url": "https://searchuxcdn.blob.core.windows.net/designerapp/images/OOTBLayouts/search.png", 
                            "altText": "Thumbnail image", 
                            "horizontalAlignment": "center", 
                            "size": "small" 
                        } 
                    ], 
                    "horizontalAlignment": "center" 
                }, 
                { 
                    "type": "Column", 
                    "width": 10, 
                    "items": [ 
                        { 
                            "type": "TextBlock", 
                            "text": "[${title}](${titleLink})", 
                            "weight": "bolder", 
                            "color": "accent", 
                            "size": "medium", 
                            "maxLines": 3 
                        }, 
                        { 
                            "type": "TextBlock", 
                            "text": "[${titleLink}](${titleLink})", 
                            "weight": "bolder", 
                            "spacing": "small", 
                            "maxLines": 3 
                        }, 
                        { 
                            "type": "TextBlock", 
                            "text": "${description}", 
                            "maxLines": 3, 
                            "wrap": true 
                        } 
                    ], 
                    "spacing": "medium" 
                } 
            ] 
        } 
    ], 
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json" 
} 
```

資料範例：在 **預覽模式** 中，指定 **範例資料編輯器** 中的範例資料，以查看資料繫結卡。

```json
{ 
    "title": "Contoso Solutions", 
    "titleLink": "https://contoso.com", 
    "description": "Marketing team at Contoso.., and looking at the Contoso Marketing documents on the team site. This contains the data from FY20 and will taken over to FY21...Marketing Planning is ongoing for FY20.." 
} 
```

## <a name="map-the-layout-to-the-result-properties"></a>將版面配置對應至結果屬性

您必須將版面配置的每個欄位對應到 result 屬性或連接器屬性，以產生結果版面配置 JSON。

![在 [搜尋版面配置設計] 頁面上，具有選取欄位及開啟屬性窗格之範例版面配置的螢幕抓入。](media/Verts-SearchLayoutDesigner.png)

選取版面配置中的欄位，以反白顯示需要對應的變數。 您可以將多個變數用於單一欄位，而且所有欄位都必須對應至 result 屬性。

### <a name="show-snippet-on-search-result"></a>顯示搜尋結果的程式碼片段  

在連接器結果的 **content** 屬性上產生的動態程式碼片段會顯示在搜尋結果中。 **ResultSnippet** 是一種系統屬性，可充當針對每個連接器結果所產生之程式碼片段的預留位置屬性。 若要在結果版面配置中顯示程式碼片段， **ResultSnippet** 系統屬性必須對應至適當的欄位，例如「描述」，在搜尋結果版面配置中。 在每個結果上產生的程式碼片段也會反白顯示程式碼片段中使用者所輸入的查詢字詞的相符專案。

## <a name="things-to-consider"></a>考慮事項

開始之前，請先執行一些工作，您應該避免使用一些事項，以確保您的版面配置順利。

### <a name="do"></a>要

- 若要使用靜態連結的徽標和 result 屬性，請編輯範本，以在版面配置中提供標誌連結。
- 建議使用方形徽標，以確保正確對齊結果。 若要避免 pixelation，請使用具有最小大小32px 的標誌（由32px）。
- 針對結果 JSON 中所用 result 屬性沒有傳回資料的情況，驗證結果版面配置。 若 `$when` 屬性不包含資料，請使用條件來隱藏元素。  
- 請確定 `$when` condition 和 result 屬性的資料類型相符。 例如， `Number` `Text` 在條件中不會比較 `$when` 。  
- 設計結果版面配置時，請考慮主題需求。  
- 請確定 `Textblock`   元素可以處理動態內容。 您可以使用 `wrap` 和 `maxLines` 元素屬性來達到此目的。
- 使用在 Markdown 中時，正確地格式化日期 `{DATE()}` 。  

### <a name="dont"></a>不要

- 綁定值時，請勿定義不正確資料類型。 如需資料類型的相關資訊，請參閱 [管理搜尋架構](/sharepoint/search/manage-the-search-schema)。
- 請遵循結果版面 JSON 的最大高度，避免在結果頁面上裁剪結果。 如果您超出結果版面配置的最大高度，將會在結果頁面上裁剪結果。
- 不使用 `px` 元素屬性中的值。
- 在結果版面配置中，請勿使用 markdown 搭配 **ResultSnippet** 屬性，在搜尋結果中醒目提示查詢比對。

## <a name="resources"></a>資源

[自訂搜尋結果頁面](customize-search-page.md)

[自我調整卡片](/adaptive-cards/authoring-cards/getting-started)

[自我調整卡片範本語言](/adaptive-cards/templating/language)

[自我調整卡片架構](https://adaptivecards.io/explorer/)
