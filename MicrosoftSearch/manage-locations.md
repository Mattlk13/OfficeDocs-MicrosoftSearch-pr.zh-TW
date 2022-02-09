---
title: 管理位置
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
ms.assetid: 8ab9aa00-cd74-405f-8410-9a1c3cfacdb9
description: 隨著時間，您可能會需要更新位置的狀態和內容以讓它保持相關。
ms.openlocfilehash: 39366e467db09f3a680d1a5fef889b12233a88c9
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62492487"
---
# <a name="manage-locations"></a>管理位置

## <a name="location"></a>位置

位置利用提供辦公室、校區和大樓的準確位置以及方向和導覽，可協助使用者尋找地址並找到組織的大樓。 系統管理員應該新增組織的所有重要位置。 與書籤和問與答不同，索引不會立即更新，並且需要數小時的時間，新增或變更的位置才會顯示在搜尋結果中。

### <a name="add-or-edit-a-single-location"></a>新增或編輯單一位置

1. 在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [[**位置**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/locations)]
1. 若要新增位置， **請選取 [新增]**。
1. 若要編輯位置，請在相關的位置清單中選取該位置。
1. 當您新增或編輯資訊時，預覽會自動更新。
1. 儲存變更。

### <a name="bulk-add-or-edit-locations"></a>大量新增或編輯位置

系統管理員可以使用匯入或匯出功能來大量新增或編輯位置。

使用匯入/匯出功能，以便：

1. 大量新增位置 - 在位置範本檔案中新增詳細資料，然後將它匯入。
1. 大量編輯位置 - 將位置匯出至 .csv 檔案，然後編輯匯出的 .csv 檔案中位置的詳細資料，然後匯入更新的 .csv 檔案。
1. 備份位置–將現有位置匯出至 .csv 檔。

若要匯出或匯入位置：

1. 在 [位置] 索引標籤的右上角，選取 [匯入]。
選取 [匯出] 來下載 .csv 檔案中的現有位置。
1. 在右窗格中，選擇使用 .csv 檔案匯入的選項。
下載範本檔案以取得必要欄位的清單和詳細資料。
1. 在範本檔案中新增或編輯位置詳細資料，然後將它儲存在您的電腦上。
1. 在 [匯入位置] 窗格中，選取 [瀏覽]，然後選取您要匯入的 .csv 檔案。
1. 選取 [匯入]。

以下是有關範本檔案的一些重點：

- 永不編輯這些欄位中的資料：*識別碼*、*上次修改日期*，以及 *上次修改者*
- 如果您包括現有位置的 *識別碼* ，它會被匯入檔案中的資訊所取代。
- 如果存在同名的現有位置，該位置將會以匯入檔案中的資訊進行更新。
- 並非範本檔案中的所有欄位都是必要的，必要的欄位會視位置狀態而異。
- 根據 [ *省/州* ] 欄位，位置將會儲存為草稿、建議、排程，或會自動發行。
- 針對管理多個組織的合作夥伴，您可以從一個組織匯出您的位置，然後將其匯入另一個組織。 但您必須在匯入之前，先移除 [識別碼] 資料行中的資料。

> [!NOTE]
> 如果範本檔案中有任何錯誤，就無法匯入位置。 若要避免錯誤，請確定您匯入的檔案的格式正確，並包含所有必要的資訊。

如需如何避免錯誤的詳細資訊，請參閱[防止匯入錯誤](manage-bookmarks.md#prevent-import-errors)。
