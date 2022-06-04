---
title: Azure DevOps Wiki Graph 連接器的結果配置
ms.author: vivg
author: vivg
manager: harshkum
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 適用于 Microsoft Search 之 Azure DevOps Wiki 連接器的結果配置 JSON
ms.openlocfilehash: 38969742087ccdeabc8bad55f2b2413659a1e401
ms.sourcegitcommit: 7cb5fb6aef414c6914818bb6fa94422345f3e173
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2022
ms.locfileid: "65897292"
---
# <a name="result-layout-for-azure-devops-wiki-graph-connector"></a>Azure DevOps Wiki Graph 連接器的結果配置

[Azure DevOps Wiki Graph 連接器](azure-devops-wiki-connector.md)可讓您的組織從 Azure DevOps 服務為 Wiki 編制索引。 設定連接器和索引內容之後，您必須設定搜尋結果頁面。

若要設定搜尋結果頁面，您需要：
1. 設定 [垂直搜尋](manage-verticals.md)。
2. 設定 [搜尋結果類型](manage-result-types.md)。

在本檔中，我們提供了設定 Azure DevOps Wiki 連接器結果配置所需的範例結果配置 JSON。

## <a name="before-you-get-started"></a>開始之前

您必須已設定 Azure DevOps Wiki Graph 連接器。 若要依原樣取用範例結果配置 JSON，您必須選取下列屬性以使用所述 [的搜尋架構編制索](configure-connector.md)引。

> [!NOTE]
> * **需要擷取** 搜尋屬性，才能在搜尋結果範本中顯示內容。 屬性也可以有其他搜尋屬性。  

| 屬性	 | 需要搜尋架構屬性 |
| -------- | -------- |
| 標題 | 檢索 |
| RemoteURL | 檢索 |
| LastPublishedAuthorName | 檢索 |
| LastPublishedDate | 檢索 |
| 內容 | Content 屬性 |
| 組織 | 檢索 |
| Project | 檢索 |
| WikiIdentifier | 檢索 |

## <a name="result-layout"></a>結果配置

在此範例中，您的搜尋結果看起來會像這樣：

![Azure DevOps Wiki 連接器的版面配置範例。](media/azure-devops-wiki-connector-example-layout.png)

以下是配置的相關聯 JSON 檔案：


```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "ColumnSet",
            "columns": [
                {
                    "type": "Column",
                    "width": "auto",
                    "items": [
                        {
                            "type": "Image",
                            "url": "https://searchuxcdn.blob.core.windows.net/designerapp/images/AzureDevOpsLogo.png",
                            "horizontalAlignment": "Center",
                            "altText": "Not available",
                            "width": "-1px",
                            "size": "Small"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": 8,
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "[${Title}](${RemoteURL})",
                            "color": "Accent",
                            "size": "Medium",
                            "weight": "Bolder"
                        },
                        {
                            "type": "TextBlock",
                            "text": "__${LastPublishedAuthorName}__ modified on {{DATE({LastPublishedDate})}}",
                            "spacing": "Small"
                        },
                        {
                            "type": "ColumnSet",
                            "columns": [
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Organization:__ ${Organization}"
                                        }
                                    ]
                                },
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Project:__ ${Project}"
                                        }
                                    ]
                                },
                                {
                                    "type": "Column",
                                    "width": "stretch",
                                    "items": [
                                        {
                                            "type": "TextBlock",
                                            "text": "__Wiki:__ ${WikiIdentifier}"
                                        }
                                    ]
                                }
                            ]
                        },
                        {
                            "type": "TextBlock",
                            "text": "${ResultSnippet}",
                            "wrap": true,
                            "maxLines": 3,
                            "spacing": "Medium"
                        }
                    ],
                    "horizontalAlignment": "Center",
                    "spacing": "Medium"
                }
            ]
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "$data": {
    }
}

```
## <a name="resources"></a>資源

[自訂搜尋結果頁面](customize-search-page.md)

[管理搜尋結果版面配置](customize-results-layout.md)
