---
title: 監視適用于 Microsoft 搜尋 的 Microsoft Graph 連接器
ms.author: mecampos
author: monaray97
manager: mnirkhe
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 監視您的線上狀態和索引配額使用率。
ms.openlocfilehash: edc136d62a04393b6acccfc5980da86fe82e64e1
ms.sourcegitcommit: b64b0ba3f779359fad24000c253a542ea92d053b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2022
ms.locfileid: "65245797"
---
# <a name="monitor-your-connections"></a>監控您的連線

若要存取和管理您的 Microsoft Graph連接器，您必須被指定為租使用者的搜尋系統管理員。 請連絡您的租使用者系統管理員，以布建搜尋系統管理員角色。

## <a name="connection-operations"></a>連線作業

在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [[**連接器] 索引卷** 標](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/Connectors)。

針對每個連接器類型，Microsoft 365 系統管理中心支援下表所示的作業。

作業 |  Microsoft 連接器 | 合作夥伴的連接器
--- | --- | ---
新增連線 | ：heavy_check_mark： (請參閱 [安裝程式概觀](configure-connector.md))  | ：x： (請參閱您的合作夥伴或自訂建置的連接器系統管理員 UX) 
刪除連線 | ：heavy_check_mark： | ：heavy_check_mark：
編輯已發佈的連線 | ：heavy_check_mark：名稱和描述<br></br> ：heavy_check_mark：連線設定<br></br> ：heavy_check_mark：屬性標籤<br></br> ：heavy_check_mark：架構<br></br> ：heavy_check_mark：重新整理排程<br></br> | ：heavy_check_mark：名稱<br></br> ：heavy_check_mark：描述
編輯草稿連線 | ：heavy_check_mark： | ：x：

## <a name="monitor-your-connection-state"></a>監視線上狀態

建立連線之後，已處理的專案數目會顯示在 [Microsoft 搜尋] 頁面的 [**連接器**]**索引** 標籤上。 在初始完整編目成功完成之後，會顯示定期累加編目進度。 此頁面提供連接器日常作業的相關資訊，以及記錄和錯誤歷程記錄的概觀。

每個連線的 **[狀態** ] 資料行中會顯示五個狀態：

* **同步處理**。 連接器會從來源編目資料，以編制現有專案的索引，並進行任何更新。

* **就緒**。 連線已就緒，而且沒有針對它執行的作用中編目。 **上次同步處理時間** 指出上次成功編目發生的時間。 連線就像上次同步處理時間一樣全新。

* **已暫停**。 系統管理員會透過 pause 選項來暫停編目。 下一個編目只會在手動繼續時執行。 不過，來自此連線的資料仍可繼續搜尋。

* **已失敗**。 連線發生重大失敗。 此錯誤需要手動介入。 系統管理員必須根據顯示的錯誤訊息採取適當的動作。 在發生錯誤之前已編制索引的資料是可搜尋的。

* **刪除失敗**。 連線刪除失敗。 視失敗原因而定，資料可能仍會編制索引、可能仍會取用專案配額，而且可能仍會針對連線執行編目。 我們建議您嘗試在此狀態下再次刪除連線。

## <a name="monitor-your-index-quota-utilization"></a>監視索引配額使用率

可用的索引配額和耗用量會顯示在連接器登陸頁面上。

:::image type="content" alt-text="索引配額使用率列。" source="media/quota_utilization.png" lightbox="media/quota_utilization.png":::

配額使用率列會根據貴組織的配額使用量來指出各種狀態：

狀態 | 配額使用率層級
--- | --- 
一般 | 079 &ndash; %
高 | 8089 &ndash; %
重大 | 90% &ndash; 99%
完整 | 100%

每個連接也會顯示已編制索引的專案數。 每個連線編制索引的專案數目會影響貴組織可用的總配額。

當超過貴組織的索引配額時，所有作用中的連線都會受到影響，且這些連線的運作超出 **限制** 狀態。 在此狀態下，您的作用中連線：  

* 無法新增專案。

* 能夠更新或刪除現有的專案。

若要修正此問題，您可以執行下列任何動作：

* 若要深入瞭解，請參閱為您的組織購買索引配額： [授權需求和定價](licensing.md)。

* 識別內嵌太多內容的連線，並加以更新以編制較少專案的索引，以騰出空間供配額使用。 若要更新連線，您必須使用新的擷取篩選器來刪除並建立新的連線，以減少專案。

* 永久刪除一或多個連線。
