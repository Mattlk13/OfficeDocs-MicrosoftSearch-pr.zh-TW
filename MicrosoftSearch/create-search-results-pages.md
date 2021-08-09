---
title: 在 SharePoint Online 中建立自訂搜尋結果頁面
ms.author: jeffkizn
author: jeffkizn
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
description: 建立您自己的 SharePoint Online 網站的搜尋結果頁面
ms.openlocfilehash: 40944ef1eef7df41cd610b9f4abd037afe91dd8972a1a875901cecbac8756eb4
ms.sourcegitcommit: 71ac2a38971ca4452d1bddfc773ff8f45e1ffd77
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2021
ms.locfileid: "54533153"
---
# <a name="create-a-custom-search-results-page-in-sharepoint-online"></a>在 SharePoint Online 中建立自訂搜尋結果頁面

在 SharePoint 中自訂搜尋體驗的一種方式是建立網站的自訂搜尋結果頁面。 這可讓您使用您建立的頁面，而不是預設的 Microsoft 搜尋結果] 頁面。 這可讓您更靈活地瞭解搜尋結果的體驗對您的使用者的外觀。

>[!NOTE]
> 若要變更預設可供使用的預設 Microsoft 搜尋結果頁面，請參閱[自訂搜尋結果頁面](customize-search-page.md)。

使用自訂結果頁面，您可以建立新的頁面，用來控制搜尋結果的版面配置及設計，以支援組織的需求。 您可以使用來自 SharePoint 模式和慣例群組的任何內建網頁元件、開啟來源搜尋網頁元件，以及您使用 SharePoint 架構所開發的任何自訂網頁元件。

## <a name="configure-a-results-page"></a>設定結果頁面

若要在 SharePoint Online 中設定自訂結果頁面，請依照下列步驟進行：

1. 流覽至您要設定自訂結果頁面的網站，然後移至 **網站設定 > 網站集合設定 > 搜尋設定**。

2. 在 [搜尋設定] 中，清除 **[選取使用與我的父代相同的結果頁面設定**]，選擇 [**將查詢傳送至自訂結果頁面**]，並提供 **結果頁面 URL:** 的值。 然後，儲存您的變更。 您在這裡使用的 URL 應針對您建立用來做為自訂結果頁面的頁面。

>[!NOTE]
> 自訂結果頁面必須與您的網站位於相同的網域，但不一定要在相同的網站集合中。  

或者，您也可以使用[PnPSearchSettings SharePoint PnP PowerShell 命令](/powershell/module/sharepoint-pnp/set-pnpsearchsettings?view=sharepoint-ps)來設定值，而不是使用 [網站設定] 頁面。

設定之後，當您使用頁面頂端的導覽列中所顯示的 [Microsoft 搜尋] 方塊進行搜尋時，會顯示 [自訂搜尋結果] 頁面，當您從網站頁面或網站首頁輸入搜尋時，會使用該對話方塊。 當您在清單、文件庫或 [網站內容] 頁面中進行搜尋時，不會使用此功能。 您可以使用連結從清單和文件庫中的搜尋結果展開搜尋，以取得自訂結果頁面。

## <a name="change-the-layout-of-your-custom-results-page"></a>變更自訂結果頁面的版面配置

名為 **HeaderlessSearchResults** 的頁面配置可用於讓搜尋結果頁面看起來更接近我們的現成搜尋結果體驗。 只有設定為自訂搜尋結果頁面的頁面才能使用這種新的版面配置。

若要設定頁面配置，您可以使用 [PnPClientSidePageSharePoint PnP PowerShell 命令](/powershell/module/sharepoint-pnp/set-pnpclientsidepage?view=sharepoint-ps) 搭配-LayoutType HeaderlessSearchResults。

## <a name="use-sharepoint-framework-query-extensions"></a>使用 SharePoint 架構查詢擴充

自訂搜尋結果頁面也可以使用[SharePoint 架構查詢延伸](/sharepoint/dev/spfx/building-search-extensions)，在將查詢傳送至搜尋引擎之前修改查詢。

## <a name="additional-resources"></a>其他資源

若要深入瞭解自訂結果頁面，請參閱我們的 [Ignite 2019 搜尋自訂和開發會話](https://myignite.techcommunity.microsoft.com/sessions/85238?source=sessions)。

針對「開放來源」專案、開始使用 Microsoft 搜尋 APIs，以及更多自訂及擴充性範例，請造訪[GitHub 上的 Microsoft 搜尋](https://github.com/microsoft-search)。