---
title: 在 SharePoint Online 中建立自訂搜尋結果頁面
ms.author: jeffkizn
author: jeffkizn
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
description: 為 SharePoint Online 網站建立您自己的搜尋結果頁面
ms.openlocfilehash: 9b0bae9b3220b7b1fdd9479e2159741ad55eacda
ms.sourcegitcommit: d8950df5ac1f15e5ead77ec89e002402368638d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2022
ms.locfileid: "65926806"
---
# <a name="create-a-custom-search-results-page-in-sharepoint-online"></a>在 SharePoint Online 中建立自訂搜尋結果頁面

在 SharePoint 中自訂搜尋體驗的其中一種方式是建立網站的自訂搜尋結果頁面。 這可讓您使用您建立的頁面，而不是 Microsoft Search 結果頁面中的預設值。 這可讓您更靈活地瞭解搜尋結果體驗如何尋找您的使用者。

>[!NOTE]
> 若要變更預設可用的預設 Microsoft 搜尋結果頁面，請參閱 [自訂搜尋結果頁面](customize-search-page.md)。

使用自訂結果頁面，您可以建立新的頁面，以用來控制搜尋結果的配置和設計，以支援組織的需求。 您可以使用任何內建網頁元件、來自 SharePoint 模式和實務社群的開放原始碼搜尋網頁元件，以及您可能使用 SharePoint 架構開發的任何自訂網頁元件。

## <a name="configure-a-results-page"></a>設定結果頁面

若要在 SharePoint Online 中設定自訂結果頁面，請遵循下列步驟：

1. 流覽至您要設定自訂結果頁面的網站，然後移至 [ **網站集合設定] > [網站集合設定] > [搜尋設定]**。

2. 在 [搜尋設定] 中，清除 [ **使用與父系相同的結果頁面設定**] 中的選取範圍，選擇 [ **將查詢傳送至自訂結果頁面**]，並提供 [ **結果] 頁面 URL：** 的值。 然後，儲存您的變更。 您在這裡使用的 URL 應該是您建立的頁面，以作為自訂結果頁面，例如 `https://contoso.sharepoint.com/sites/search/SitePages/results.aspx` 。 如需這項功能的示範，請參閱 [此 Microsoft Ignite 研討會](https://youtu.be/jKpIDBalLW0?t=1508) 。

>[!NOTE]
> 自訂結果頁面必須與您的網站位於相同的網域，但不一定位於相同的網站集合中。  

或者，您可以使用 [Set-PnPSearchSettings SharePoint PnP PowerShell 命令](https://pnp.github.io/powershell/cmdlets/Set-PnPSearchSettings.html) 來設定值，而不是使用 [網站設定] 頁面。

設定之後，當您使用出現在頁面頂端導覽列中的 [Microsoft 搜尋] 方塊進行搜尋時，會顯示自訂搜尋結果頁面，並在您從網站頁面或網站首頁輸入搜尋時使用。 當您在清單、文件庫或網站內容頁面內搜尋時，不會使用它。 您可以使用連結，從清單和文件庫中的搜尋結果展開搜尋，以進入自訂結果頁面。

## <a name="change-the-layout-of-your-custom-results-page"></a>變更自訂結果頁面的版面配置

名為 **HeaderlessSearchResults 的** 版面配置可用來讓搜尋結果頁面看起來更接近現成的搜尋結果體驗。 這個新的版面配置只能針對設定為自訂搜尋結果頁面的頁面使用中。

若要設定版面配置，您可以使用 [Set-PnPPage PnP PowerShell 命令](https://pnp.github.io/powershell/cmdlets/Set-PnPPage.html) 搭配 -LayoutType HeaderlessSearchResults。

## <a name="use-sharepoint-framework-query-extensions"></a>使用 SharePoint 架構查詢延伸模組

自訂搜尋結果頁面也可以使用 [SharePoint 架構查詢延伸](/sharepoint/dev/spfx/building-search-extensions) 模組，在查詢傳送至搜尋引擎之前修改查詢。

## <a name="additional-resources"></a>其他資源

如需開放原始碼專案、開始使用我們的 Microsoft 搜尋 API，以及更多自訂和擴充性範例，請造訪 [GitHub 上的 Microsoft Search](https://github.com/microsoft-search)。
