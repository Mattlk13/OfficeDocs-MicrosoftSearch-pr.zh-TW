---
title: 常見問題集
ms.author: jeffkizn
author: jeffkizn
manager: parulm
ms.audience: Admin
ms.topic: reference
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 03/11/2022
search.appverid:
- BFB160
- MET150
- MOE150
description: 取得有關企業搜尋和 Microsoft Search 常見問題的解答
ms.openlocfilehash: a16e7acfbc3110e70da0a725325781311c8dca51
ms.sourcegitcommit: 7cf1aac92e3d46008be647c16a14460fa43642ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2022
ms.locfileid: "63438858"
---
<!-- markdownlint-disable no-trailing-punctuation -->
# <a name="frequently-asked-questions"></a>常見問題集

以下是最常見問題的清單。

> [!TIP]
> 在這裡看不到您的問題獲得解答嗎？ 請在這篇文章的意見反應中提出您的問題。

## <a name="is-advanced-query-understanding-supported"></a>是否支援進階查詢理解？

是的，Microsoft Search 會從較大的片語剖析查詢意圖。 這項功能會使用 AI 來瞭解常見的多餘片語，使用者會將其新增至不會影響其搜尋意圖的查詢。 例如，當使用者搜尋有關 *如何變更密碼的詳細資訊* 時，我們會從查詢中解壓縮較不重要的字詞，並根據相關的 *變更密碼（如變更密碼*）進行觸發。
  
這項功能不會覆寫[Microsoft 365 系統管理中心](https://admin.microsoft.com)中所設定的關鍵字。
  
## <a name="can-you-search-for-files-on-premises"></a>可以搜尋內部部署檔案嗎？

是。 如果您有 SharePoint 的混合式部署，您可以搜尋內部部署[SharePoint](http://sharepoint.com/)檔案。
  
## <a name="how-do-i-make-bing-the-default-search-engine-for-people-in-my-org"></a>如何讓 Bing 成為我的組織中人員的預設搜尋引擎？

以下是設定預設搜尋引擎、預設首頁及預設瀏覽器的指示，可為使用者提供[Bing](https://Bing.com)中 Microsoft 搜尋的最佳體驗：

- [將 Microsoft Edge 設定為您的預設瀏覽器](/deployedge/edge-default-browser)
- [讓 Bing 成為預設搜尋引擎](set-default-search-engine.md)
- [將 Bing.com 設為企業首頁](set-default-homepage.md)

## <a name="how-are-my-search-results-protected"></a>如何保護我的搜尋結果？

我們需要[Azure Active Directory](/azure/active-directory/)驗證，才能存取受信任的雲端的結果。 已驗證的使用者只會看到他們有權存取的內容。 在 Bing 中使用 Microsoft 搜尋時，會解除發現搜尋查詢，並以公用[Bing](https://Bing.com)搜尋流量分開記錄。

## <a name="can-i-search-across-federated-organizations"></a>可以跨同盟組織搜尋嗎？

否。

## <a name="where-can-i-get-info-about-office-365-security-compliance-and-privacy"></a>我可以在哪裡取得有關 Office 365 安全性、規範和隱私權的資訊？

詳細資料可在 Office 365 的[信任中心頁面](https://www.microsoft.com/TrustCenter/CloudServices/office365/default.aspx)上找到。

## <a name="can-guests-access-microsoft-search-in-my-organization"></a>來賓是否可以在我的組織中存取 Microsoft 搜尋？

Microsoft 365 透過[來賓存取](/microsoft-365/solutions/collaborate-with-people-outside-your-organization)，與組織外部的人員進行豐富的共同作業。 這些使用者可搜尋檔、網站、群組、清單及文件庫。 不過，來賓不會取得完整、個人化的 Microsoft 搜尋體驗，而且可能需要使用頁面中的搜尋方塊，而不是頁首中的「整合 Microsoft 搜尋」方塊。

## <a name="how-do-i-turn-microsoft-search-in-bing-on-or-off"></a>如何開啟或關閉 Bing 中的 Microsoft 搜尋？

大多陣列織（包括企業和教育版） Bing 中 Microsoft 搜尋預設為開啟。 若要在 Bing 中開啟 Microsoft 搜尋，請移至 Microsoft 365 系統管理中心中[的 [設定](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/configurations)] 頁面。 在 [Bing 設定] 下的 [Microsoft 搜尋] 下，選擇 [**變更設定**]，然後開啟 [**允許您的組織在 Bing 使用 Microsoft 搜尋**]。 這種變更需要長達24小時才會生效。

若此設定為 [關閉]，當使用者搜尋 Bing、Windows 搜尋或 Microsoft Edge 時，不會收到內部結果。 在 Bing 中關閉 Microsoft 搜尋不會停止或防止內部內容新增至您的搜尋索引。 它只會停用 Bing 進入 Microsoft 搜尋的進入點。 若要尋找答案和內部結果，使用者將需要使用其他進入點，例如 SharePoint 線上或 Office 365 應用程式。

## <a name="what-does-microsoft-search-cost"></a>Microsoft 搜尋成本是多少？

Microsoft 搜尋會搜尋您的 Microsoft 365 經驗; 搜尋資料時，不需要額外的成本。 有些功能（例如[Graph 連接器](connectors-overview.md)）附帶某些授權所包含的配額，[且有額外的配額可供購買](licensing.md)。
