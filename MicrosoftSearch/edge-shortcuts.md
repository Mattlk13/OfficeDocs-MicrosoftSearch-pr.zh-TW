---
title: 自訂 Microsoft Edge 的網址列快捷方式
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
description: 為 Microsoft 搜尋新增自訂的 Microsoft Edge 快捷方式 Bing 或關閉組織的這些快捷方式
ms.openlocfilehash: 5a3352ebfd382fe482974f4f9d768a10973ce4bf
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62491135"
---
# <a name="customize-address-bar-shortcuts-for-microsoft-edge"></a>自訂 Microsoft Edge 的網址列快捷方式

協助您的使用者在從 Microsoft Edge 位址列進行搜尋時，保持焦點和尋找工作結果的速度。 預設會啟用兩個快捷方式：「工作」和您組織的慣用或簡短名稱。 在 [Microsoft Edge 位址] 列中，使用者可以輸入關鍵字，然後按 tab 鍵。 位址列會指出他們在您的組織內搜尋。 當他們輸入其搜尋並按 Enter 鍵時，他們會看到具有相關答案和結果的搜尋結果頁面。 您可以新增兩個自訂快捷方式關鍵字。

> [!NOTE]
> 本文適用于 Microsoft Edge 版本96或更新版本。

## <a name="manage-shortcuts-and-keywords"></a>管理快捷方式和關鍵字

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [設定[]。](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/configurations)
2. 在 [Microsoft 搜尋 Bing 設定] 下，選取 [**變更設定**]。
3. 在 Bing 面板的 Microsoft 搜尋中，預設會選取 [**啟用 Bing 快捷方式中的 Microsoft 搜尋**]。 若要停用這些快捷方式，請清除此核取方塊。
4. 在 [搜尋關鍵字] 欄位中，輸入一個或兩個以上的關鍵字。 您可以包含空格和特殊字元。
5. 選取 **[儲存]**。

## <a name="frequently-asked-questions"></a>常見問題集

**問：關鍵字無法使用。怎麼了？**

**A：** 在 [Microsoft Edge 位址] 列中，輸入 edge://settings/search，以移至您的搜尋設定。 確認已啟用 [ **使用我的輸入字元顯示搜尋和網站建議** ]。 您也可以使用 Microsoft Edge 的群組原則來啟用搜尋建議。 若要深入瞭解，請參閱 [SearchSuggestEnabled](/deployedge/microsoft-edge-policies#searchsuggestenabled)。

**問：這些快捷方式是否只支援英文關鍵字？**

**A：** 不。 針對當地語系化的關鍵字，您必須在 [搜尋關鍵字] 欄位中新增語言特有的關鍵字。

**問：將新關鍵字識別為快捷方式需要多久時間？**

**A：** Microsoft Edge 將自訂關鍵字識別為快捷方式，最多需要兩天。

**問：我可以新增 Google Chrome 使用者的快捷方式嗎？**

**A**：不是透過 Microsoft 365 系統管理中心。 使用者可以前往管理搜尋引擎的設定，以及在其他搜尋引擎下，新增網站名稱、關鍵字和查詢 URL，來建立其自己的快捷方式。

**問：使用 Windows 搜尋時，是否可以使用這些相同的關鍵字？**

**A**：否，只有 Microsoft Edge 支援這些關鍵字快捷方式。
