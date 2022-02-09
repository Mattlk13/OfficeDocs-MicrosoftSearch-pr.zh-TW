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
description: 如何在 SharePoint 網站上自訂搜尋框體驗
ms.openlocfilehash: ae9ba9a83730963f02f9beb7e06d2372767d1e0a
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62492813"
---
# <a name="search-box-settings-on-sharepoint-sites"></a>SharePoint 網站上的搜尋方塊設定

您可以在 SharePoint 網站上自訂 Microsoft 搜尋其中一種方式，以定制套件導覽列中的 [搜尋] 方塊如何在 SharePoint 網站中運作，以最適合您的需求。

如需其他自訂選項，請參閱[變更「Microsoft 搜尋結果」頁面以新增自訂的縱向、結果類型及佈局](customize-search-page.md)，以及[建立自訂搜尋結果頁面](create-search-results-pages.md)。

> [!NOTE]
> 現在所有客戶都無法使用 [套件導覽列] 搜尋方塊，但這些選項仍可供設定，而且會在可用時生效。

對於下列所列的工作，您將使用 PowerShell 搭配 SharePoint PnP PowerShell 擴充。 您可以安裝並深入瞭解如何開始 [這裡](/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps)。 您將使用下列命令登入您的網站或網站集合：

```powershell
Connect-PnPOnline -Url <yoursiteurl> -UseWebLogin
# this will prompt you to sign into your site. Use the site owner credentials 
```

## <a name="changing-the-scope-of-search"></a>變更搜尋範圍

當您今天在 SharePoint Online 中建立新網站，然後在搜尋方塊中輸入時，將會進入 [Microsoft 搜尋結果] 頁面。 此頁面預設會顯示目前網站的結果，並可讓您將搜尋範圍擴充至目前網站 (關聯的中樞（如果有一個) 或整個組織）。

[搜尋] 方塊預設使用的範圍取決於網站類型。

* 一般網站會搜尋目前的網站。
* Hub sites 透過 hub 中的所有網站搜尋。
* 家庭網站搜尋所有內容。

在某些情況下，您可能會想要變更這些預設值，以無條件搜尋整個組織或與網站相關聯的 hub，而不需要另外按一下。

網站擁有者，您可以使用下列命令變更這些預設值：

```powershell
Set-PnPSearchSettings -SearchScope Tenant
# DefaultScope | Hub | Site | Tenant
```

執行這個命令之後，以前顯示目前網站的結果的網站預設會從整個組織開始顯示結果。

若要回到預設設定，請使用值 "DefaultScope" 重新執行命令。 若要在 Hub 中搜尋，請使用「Hub」做為 SearchScope 值。

此設定適用于個別網站層級。 網站集合沒有同等的設定。

## <a name="show-or-hide-the-search-box"></a>顯示或隱藏搜尋方塊

如果您想要防止使用者搜尋或使用自訂搜尋框的實施，您可以選擇隱藏 [套件導覽列搜尋] 方塊。

若要變更特定網站的此設定，請使用此命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

或者，如果您想要為網站集合中的所有網站設定它，您可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxInNavBar Hidden
# Hidden | Inherit
```

執行這些命令之後，搜尋方塊將不再顯示在頁面頂端的導覽列中。 若要回到顯示搜尋方塊，請使用提供給 "SearchBoxInNavBar" 參數的值，再次執行命令以「Inherit」。

請考慮下列幾點：

* 此設定僅適用于套件導覽列中的 [搜尋] 方塊。 它不會套用到頁面中的搜尋方塊，也不會套用到傳統頁面上的搜尋方塊。

* 當您停用導覽列中的搜尋方塊時，如果您想要在網站中使用搜尋功能，您必須自行使用自訂網頁元件或 SharePoint 架構延伸提供該功能。

* 此方案也會從網站的清單和文件庫中移除搜尋方塊。 除了整個網站搜尋之外，您的自訂搜尋解決方案也必須考慮 SharePoint 清單和文件庫的內容搜尋。

* 如果您將設定套用至網域的根網站，則 SharePoint 開始頁面也會停止顯示搜尋方塊。

## <a name="changing-the-hint-displayed-in-the-search-box"></a>變更搜尋方塊中顯示的提示

您可以針對指定的網站或網站集合變更搜尋方塊所顯示的提示。 這是在開始輸入文字之前，出現在搜尋方塊中的文字。 當您已設定自訂結果頁面或以其他方式變更搜尋行為時，這可協助您指導使用者如何進行搜尋。

> [!NOTE]
> 若要進行這項變更，您必須允許以租使用者管理員的身分在網站上執行自訂腳本，此為預設不允許的使用者。 如需詳細資訊，請參閱 https://docs.microsoft.com/sharepoint/allow-or-prevent-custom-script 。 您可以在必要時，允許執行自訂腳本，進行變更，然後再回復至禁止網站的腳本。

若要變更特定網站的此設定，請執行下列命令：

```powershell
Set-PnPSearchSettings -Scope Web -SearchBoxPlaceholderText "my placeholder" 
```

或者，如果您想要為網站集合中的所有網站設定它，您可以使用此命令：

```powershell
Set-PnPSearchSettings -Scope Site -SearchBoxPlaceholderText "my placeholder" 
```

若要回到預設的預留位置文字，請將值設為空白 ( "" ) 。