---
title: 在 SharePoint 網站中管理搜尋方塊
ms.author: keremy
author: jeffkizn
manager: parulm
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 如何自訂 SharePoint 網站上的搜尋方塊體驗
ms.openlocfilehash: 0dcc2327e62087e0e595dbacd98b77218d4181df
ms.sourcegitcommit: 9b8c55ef3dcdb9072aa472b4c51131707194c5e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2022
ms.locfileid: "67623251"
---
# <a name="search-box-settings-on-sharepoint-sites"></a>SharePoint 網站上的搜尋方塊設定

在 SharePoint 網站上自訂 Microsoft Search 的數種方式之一，就是量身打造套件導覽列中的搜尋方塊在 SharePoint 網站中的運作方式，以最符合您的需求。

如需其他自訂選項，請參閱 [變更 Microsoft 搜尋結果頁面以新增自訂垂直、結果類型和版面配置](customize-search-page.md)，以及 [建立自訂搜尋結果頁面](create-search-results-pages.md)。

> [!NOTE]
> 目前並非所有客戶都能使用套件導覽列搜尋方塊，但這些選項現在仍可設定，且會在可供使用時生效。

針對下列工作，您將使用 PowerShell 搭配 SharePoint PnP PowerShell 擴充功能。 您可以在這裡安裝並深入瞭解如何開始 [使用](/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps)。 您將使用下列命令登入網站或網站集合：

```powershell
Connect-PnPOnline -Url <yoursiteurl> -UseWebLogin
# this will prompt you to sign into your site. Use the site owner credentials 
```

## <a name="changing-the-scope-of-search"></a>變更搜尋範圍

當您現今在 SharePoint Online 中建立新網站並輸入搜尋方塊時，系統會帶您前往 Microsoft Search 結果頁面。 此頁面預設會顯示您目前網站的結果，並可讓您將搜尋範圍展開至目前網站與 (有一個) 或整個組織相關聯的中樞。

搜尋方塊預設使用的範圍取決於網站類型。

* 一般網站會搜尋目前的網站。
* 中樞網站會搜尋中樞內的所有網站。
* 首頁網站會搜尋所有內容。

在某些情況下，您可能想要將這些預設值變更為一律搜尋整個組織，或跨與網站相關聯的中樞，而不需要再按一下。

身為網站擁有者，您可以使用下列命令來變更這些預設值：

```powershell
Set-PnPSearchSettings -SearchScope Tenant
# DefaultScope | Hub | Site | Tenant
```

執行此命令之後，先前預設顯示目前網站結果的網站將會開始顯示整個組織的結果。

若要回到預設設定，請再次執行值為 「DefaultScope」 的命令。 若要搜尋中樞，請使用 「Hub」 作為 SearchScope 值。

此設定適用于個別月臺層級。 網站集合沒有對等的設定。

## <a name="show-or-hide-the-search-box"></a>顯示或隱藏搜尋方塊

如果您想要防止使用者搜尋或使用自訂搜尋方塊實作，您可以選擇隱藏套件導覽列搜尋方塊。

若要變更指定網站的此設定，請使用下列命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

或者，如果您想要為網站集合中的所有網站設定它，您可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

執行這些命令之後，搜尋方塊將不再顯示在頁面頂端的導覽列中。 若要返回顯示搜尋方塊，請使用提供給 「SearchBoxInNavBar」 參數的值，再次執行命令至 「Inherit」。

有幾點需要考慮：

* 此設定僅適用于套件導覽列中的搜尋方塊。 它不適用於頁面中的搜尋方塊，也不適用於傳統頁面上的搜尋方塊。

* 停用導覽列中的搜尋方塊之後，如果您想要網站中的搜尋功能，您必須使用自訂網頁元件或SharePoint 架構延伸模組自行提供。

* 此解決方案也會從網站的清單和文件庫中移除搜尋方塊。 除了全網站搜尋之外，您的自訂搜尋解決方案還需要考慮 SharePoint 清單和文件庫的內容搜尋。

* 如果您將設定套用至網域的根網站，SharePoint 起始頁面也會停止顯示搜尋方塊。

## <a name="changing-the-hint-displayed-in-the-search-box"></a>變更搜尋方塊中顯示的提示

您可以變更指定網站或網站集合的搜尋方塊所顯示的提示。 這是開始在搜尋方塊中輸入之前，會出現在搜尋方塊中的文字。 如果您已設定自訂結果頁面，或以其他方式變更搜尋行為，這可能有助於引導使用者瞭解搜尋預期的結果。

> [!NOTE]
> 若要能夠進行這項變更，您必須允許以租使用者系統管理員身分在有問題的網站上執行自訂腳本，預設不允許。 如需詳細資訊，請參閱 [允許或防止自訂腳本](/sharepoint/allow-or-prevent-custom-script) 。 您可以允許執行自訂腳本、進行變更，然後視需要還原為不允許網站的腳本。

若要變更指定月臺的此設定，請執行下列命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxPlaceholderText "my placeholder" 
```

或者，如果您想要為網站集合中的所有網站設定它，您可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxPlaceholderText "my placeholder" 
```

若要回到預設預留位置文字，請將值設定為空白 (「」) 。
