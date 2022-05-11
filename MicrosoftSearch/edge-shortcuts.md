---
title: 自訂 Microsoft Edge 的網址列捷徑
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
ms.date: 03/15/2022
search.appverid:
- BFB160
- MET150
- MOE150
description: 在Bing中新增Microsoft 搜尋的自訂Microsoft Edge快捷方式，或為您的組織關閉這些快捷方式
ms.openlocfilehash: 5f21cfdcfad8479af41c556c7d7b85d1f5c37b7a
ms.sourcegitcommit: 06b3131514063e5816bd9bede3748c001162d3f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2022
ms.locfileid: "65349618"
---
# <a name="customize-address-bar-shortcuts-for-microsoft-edge"></a>自訂 Microsoft Edge 的網址列捷徑

從Microsoft Edge網址列搜尋時，協助使用者保持專注並更快速地尋找工作結果。 預設會啟用兩個快捷方式：'work' 和您組織的慣用或縮短名稱。 在Microsoft Edge網址列中，使用者可以輸入關鍵字，然後按 Tab 鍵。 網址列會指出他們在組織內搜尋。 當他們輸入搜尋並按 Enter 鍵時，會看到具有相關答案和結果的搜尋結果頁面。 您可以新增兩個自訂快捷方式關鍵字。

:::image type="content" alt-text="輸入工作關鍵字並使用Microsoft Edge快捷方式來搜尋工作的動畫 GIF。" source="media/edge-shortcuts/microsoft-edge-address-bar-shortcut.gif" lightbox="media/edge-shortcuts/microsoft-edge-address-bar-shortcut.gif":::

> [!NOTE]
> 本文適用于Microsoft Edge 96 版或更新版本。

## <a name="manage-shortcuts-and-keywords"></a>管理快捷方式和關鍵字

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [[組態]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/configurations)。
2. 在Bing快捷方式的 [Microsoft 搜尋] 底下，選取 [**變更]**。
3. 在面板中，預設會選取 [在 **Bing快捷方式中** 啟用Microsoft 搜尋。 若要停用這些快捷方式，請清除核取方塊。
4. 在 [搜尋關鍵字] 欄位中，輸入一或兩個以上的關鍵字。 您可以包含空格和特殊字元。
5. 選取 ****[儲存]。

## <a name="frequently-asked-questions"></a>常見問題集

**問：關鍵字無法運作。怎麼了？**

**答：** 在Microsoft Edge網址列中，輸入 edge://settings/search 以移至您的搜尋設定。 確認已啟 **用 [使用我的輸入字元顯示搜尋和網站建議** ]。 您也可以使用Microsoft Edge群組原則來啟用搜尋建議。 若要深入瞭解，請 [參閱 SearchSuggestEnabled](/deployedge/microsoft-edge-policies#searchsuggestenabled)。

**問：這些快捷方式是否只支援英文關鍵字？**

**答：** 否。 針對當地語系化的關鍵字，您必須在 [搜尋關鍵字] 欄位中新增特定語言的關鍵字。

**問：將新關鍵字辨識為快捷方式需要多久時間？**

**答：** Microsoft Edge最多需要兩天的時間，才能將自訂關鍵字辨識為快捷方式。

**問：我可以為 Google Chrome 使用者新增快捷方式嗎？**

**答**：不是透過Microsoft 365 系統管理中心。 使用者可以在 Chrome 中建立自己的快捷方式，方法是移至 [管理搜尋引擎] 的設定，以及在 [其他搜尋引擎] 底下，新增網站名稱、關鍵字和查詢 URL。

**問：使用 Windows 搜尋時，是否可以使用這些相同的關鍵字？**

**答**：否，只有Microsoft Edge支援這些關鍵字快捷方式。
