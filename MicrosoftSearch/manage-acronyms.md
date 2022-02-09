---
title: 在 Microsoft 搜尋中管理縮寫詞答案
ms.author: rakkum
author: rakeshMSFT
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 在 Microsoft 搜尋中建立和更新縮寫的答案
ms.openlocfilehash: aab7dc3c93f868fdbd748d88706b383cb3ecc3db
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62490730"
---
# <a name="manage-acronyms-answers-in-microsoft-search"></a>在 Microsoft 搜尋中管理縮寫的答案

使用者通常會在組織或小組所用的不熟悉縮寫和縮寫中執行。 組織或小組特有的條款，對從一個小組移至另一個小組的人員來說可能是新的，可與內部協力廠商小組共同作業，或是組織的新功能。

組織不一定會有單一參考的標準術語。 缺乏單一參考會使尋找這些縮寫的定義變得很困難。 Microsoft 搜尋會解決縮寫的問題。

## <a name="what-users-experience"></a>使用者經驗

Microsoft 搜尋使用者可以在[Bing](https://Bing.com)、 [SharePoint](https://products.office.com/sharepoint/collaboration)、 [Office 365](https://Office.com)、Outlook 網頁版、Outlook mobile (Android) 以及 Teams 行動 (iOS 和 Android) 中取得定義。 在 [ **搜尋** ] 方塊中，使用者輸入如下範例的查詢：

- *什麼* DNN
- *定義* DNN
- DNN *定義*
- *擴大* DNN
- DNN *擴充*
- *的意義* DNN
- DNN *表示*
- DNN *代表*

結果會包含使用者組織中所顯示之 DNN 的所有意義。

> [!NOTE]
> 使用者必須輸入包含縮寫詞所指定 *關鍵字* 的查詢，以觸發其對應的答案。 縮寫詞查詢不區分大小寫。

## <a name="set-up-acronyms-answers"></a>設定縮寫詞答案

在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [[**縮寫**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/acronyms)]，然後選取 [**新增縮寫**]。

Microsoft 搜尋查詢兩個數據源，以提供使用者搜尋的縮寫答案：

1. **Admin-策劃**。 由系統管理員在系統管理員 [中央](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/acronyms)提供。
2. **System-策劃**。 從使用者的電子郵件和檔，以及組織內可公開使用的資料 Microsoft 搜尋探索。

### <a name="set-up-admin-curated-acronyms"></a>設定系統管理員-策劃縮寫

搜尋管理員可以在[Microsoft 搜尋系統管理中心](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch)的 [[首字]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/acronyms)索引標籤上新增縮寫。 您可以從任何內部網站或存放庫向系統管理中心新增縮寫。 您可以將這些縮寫詞新增至 **已發佈** 或 **草稿** 的狀態：

**發行狀態**。 組織中的使用者可以透過 Microsoft 搜尋使用縮寫。

> [!NOTE]
> 最多需要一天的縮寫，加入至發佈的狀態，可在 Microsoft 搜尋中使用。

**草稿狀態**。 如果您想要在 Microsoft 搜尋中查看縮寫，您可以新增草稿狀態的縮寫。 草稿狀態中的縮寫不會出現在搜尋結果中。 您必須將縮寫詞移至發佈的狀態，使其顯示在搜尋結果中。

**排除的狀態**。 若要防止首字縮寫出現在 Microsoft 搜尋中，請使用 **排除縮寫詞** 加以新增。 若要停止排除首字縮寫，您必須刪除排除的縮寫，並新增它或在您發佈的清單中驗證。

您可以在 CSV 檔案中個別加入縮寫或大容量匯入。 使用下表所示的欄位 Upload CSV 檔案：

| 縮寫 (強制)  | 代表 (強制)  | URL | 描述  | 狀態 (強制)  | 上次修改日期 | 上次修改者 | 識別碼 |
| --------- | --------- | --------- | ---------- | --------- |--------- |--------- |--------- |
| *XXX* | *拼寫縮寫* | *Source* |  | *已發佈、草稿或排除* |  |  |  |

### <a name="csv-fields"></a>CSV 欄位

**縮寫**。 包含實際的簡寫形式或縮寫。 例如， *DNN*。

**代表**。 包含縮寫的定義。 例如， *Deep 神經網路*。

**描述**。 縮寫的簡短描述，可提供使用者更多有關縮寫和其定義的資訊。 例如， *deep 神經網路是具有某一層級複雜性的神經網路，具有超過兩層的神經網路*。

**來源**。 您要讓使用者流覽的頁面或網站 URL，以取得有關縮寫的詳細資訊。

**狀態**。 此欄位可以採用兩個值：

- **草稿**。 將縮寫新增至草稿狀態。
- **發行**。 將縮寫新增至發行的狀態，使其可用於 Microsoft 搜尋。
- **排除**。 新增已排除狀態的縮寫，使其不會出現在 Microsoft 搜尋中。

### <a name="system-curated-acronyms"></a>系統策劃縮寫

將組織內使用的所有縮寫詞新增至答案可能是一項挑戰。 這項功能可找出搜尋系統管理員甚至不會察覺的縮寫。 若要執行這項作業，Microsoft 搜尋也會從這些來源探索並 curates 縮寫：

- 使用者的電子郵件
- [SharePoint](https://products.office.com/sharepoint/collaboration)、 [Microsoft OneDrive]( https://onedrive.live.com/about/)及[Microsoft OneNote](https://www.onenote.com/)中的檔
- 組織內使用者可以存取的公用檔 SharePoint、OneDrive 或 OneNote

Microsoft 搜尋會確保只有對檔具有存取權和許可權的使用者可以查看其所探索的首字縮寫。 在使用者的信箱中找到首字縮寫時，只有該使用者可以看到該縮寫。

> [!NOTE]
> 不需要安裝策劃的首字母縮寫。

## <a name="frequently-asked-questions"></a>常見問題集

**問：系統管理員-策劃和系統策劃資料排名的方式？**

**A：** 結果的排名可能會隨人員而異，因為每位使用者的結果都有個人化。 這兩種類別都不一定優先于另一種。

**問：使用者如何觸發縮寫詞答案？**

**A：** 若要取得縮寫的答案，使用者必須在 [Bing](https://bing.com)、 [SharePoint](https://products.office.com/sharepoint/collaboration)、 [Office 365](https://Office.com)、Outlook 網頁版、Outlook mobile (Android) 或 Teams 行動 (iOS 和 Android) **搜尋** 方塊中輸入特定查詢模式。

**問：在搜尋時，使用者是否可以只輸入縮寫？**

**A：** 在 Bing 中，使用者現在只要搜尋縮寫，就能找到縮寫的答案。您已不再需要關鍵字。 在階段中，其他 Microsoft 搜尋的進入點都會啟用相同的體驗。

**問：在發佈 Microsoft 搜尋後，系統管理員必須使用多久的縮寫才能顯示出來？**

**A：** 最多需要一天的縮寫，加入至發佈的狀態，可在 Microsoft 搜尋中使用。

**問：當您收到或傳送新的電子郵件或檔之後，系統策劃的首字母縮寫會出現多久時間？**

**A：** 在新的電子郵件或檔中找到的首字縮寫，在 Microsoft 搜尋結果中只會出現7天。

**問：若排除併發布縮寫，會發生什麼事？**

**A：** 排除的縮寫詞會具有優先順序，並可防止發佈的縮寫出現在搜尋結果中。 它不會刪除或移除已發佈的縮寫。

**問：從 Microsoft 搜尋結果中排除縮寫需要多久時間？**

**A：** 排除的首字的首字，會花費一天的時間，而不會出現在搜尋結果中。

**Q：針對系統策劃首字母縮寫，是否需要使用特定格式的檔？**

**A：** 不。 我們支援所有檔案類型，但不包括 image、folder 和 zip 檔案。

**問： Microsoft 是否會從所有語言的檔中探索縮寫？**

**A：** Microsoft 僅支援英文、西班牙文、法文、義大利文、德文和葡萄牙文的檔中的策劃首字母縮寫。 其他語言的支援會分階段新增。

**問：如果我的組織不想要顯示系統策劃首字母縮寫，該怎麼辦？我是否可以在搜尋結果中停止顯示此類型的縮寫？**

**A：** 若要在搜尋結果中關閉顯示系統策劃首字母縮寫，請遵循 [商務產品的連絡人支援服務](/microsoft-365/admin/contact-support-for-business-products)中的指示，建立客戶支援票證。
在您建立支援票證後，系統策劃縮寫的最多需要48小時，以避免出現在搜尋結果中。
