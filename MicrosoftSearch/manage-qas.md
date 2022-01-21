---
title: 管理問與答
ms.author: jeffkizn
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
ms.assetid: 7e3432e6-5317-4d63-90b0-52da6fddd343
description: 個別尋找及更新答案，或使用 Microsoft 搜尋工具&一次即可編輯 Q。
ms.openlocfilehash: 2250db51849e28c49a4b6b194b4ceedcc0423f3b
ms.sourcegitcommit: bbeccfde0c02a79481ac78ecaddc44ca7ff11407
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/21/2022
ms.locfileid: "62160957"
---
# <a name="manage-qas"></a>管理問與答

建立問與答的方法與建立書籤類似。 Q&如可讓您回答使用者的問題，而不只是提供網頁連結。 您也可以在 rtf 文字中格式化答案。 如果書簽和 Q&共用相同的關鍵字，則會先顯示書簽結果。 如同書簽，Q&會在新增或變更 Q&A 之後立即重新整理索引。

## <a name="add-or-edit-a-single-qa"></a>新增或編輯單一問與答

1. 在 [Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [**Q&A**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/qnas)
1. 若要在中加入 Q&，請選取 [ **新增**]。
若要編輯問與答，請在相關的問與答清單中選取問與答。 當您新增或編輯資訊時，預覽會自動更新。
1. 儲存變更。

### <a name="supported-html-tags"></a>支援的 HTML 標記

您可以使用現有的 HTML 內容或新增 HTML 標記至您的解答 (描述)。 會忽略不支援的標籤。

支援下列的 HTML 標記：

- blockquote
- div
- em
- h1、h2、h3 和 h4
- ol、ul 和 li
- p
- pre
- span
- strong
- table、thead、tbody、tr、th 和 td
- u
- a
- code
- br
- hr
- img

## <a name="add-or-edit-qas-using-browser-extensions"></a>使用瀏覽器延伸名新增或編輯 Q&

搜尋管理員可以使用[Microsoft 搜尋內容建立者副檔名](https://chrome.google.com/webstore/detail/microsoft-search-content/nocnablpaoeecfmfnjoheefkogmleipm)輕鬆建立 Q&A 和書簽答案。 將分機新增至 Microsoft Edge 或 Google Chrome，使用您的系統管理員帳戶登入，然後移至頁面或網站。 副檔名會建議書簽和 Q&根據頁面內容的答案。 您可以將其發佈或儲存為草稿。

## <a name="bulk-add-or-edit-qas"></a>大量新增或編輯問與答

系統管理員可以使用匯入及匯出功能，以大容量方式建立或編輯 Q&。

使用匯入/匯出功能可：

- 在 Q&範本檔中，大量新增 Q&以新增詳細資料，然後將其匯入。
- Bulk edit Q&出口 Q&為 .csv 檔案，請編輯 Q&匯出檔案中的詳細資料，然後匯入檔案。
- 將 Q&為-Export Q&改為 .csv 檔。

若要匯入或匯出 Q&如下：

1. 在 [問與答] 索引標籤的右上角，選取 [匯入]。
選取 [ **匯出** ]，以下載 .csv 檔案中的所有現有 Q&。
1. 在右窗格中，選取要使用 .csv 檔案匯入的選項。 下載範本檔案，以取得必要欄位及詳細資料的清單。
1. 新增或編輯 Q&範本檔中的詳細資料，然後將它儲存在您的電腦上。
1. 在 [ **Import Q&** 窗格中，選取 **[流覽]**，然後選取您要匯入的 .csv 檔案。
1. 選取 [匯入]。

重要的範本檔秘訣：

- 永不編輯這些欄位中的資料：**識別碼**、**上次修改日期**，以及 **上次修改者**
- 如果您包括現有 Q&A 的 **識別碼** ，它會被匯入檔案中的資訊所取代。
- 如果現有的 Q&A 具有相同的標題或 URL，則 Q&A 會更新匯入檔案中的資訊。
- 並非範本檔案中的所有欄位都是必要的，必要的欄位也會因 Q&狀態而異。
- [ **狀態** ] 欄位會判斷 Q&儲存為 *草稿*、 *建議* 或 *排程*，或是自動發行。
- 針對管理多個組織的合作夥伴：您可以從一個組織匯出 Q&，並將其匯入另一個組織。 但您必須在匯入之前，先移除 [識別碼] 資料行中的資料。

> [!NOTE]
> 您無法匯入 Q&，如同範本檔案中有任何錯誤。 若要防止錯誤，請確定您的匯入檔案格式正確，並包含所有必要的資訊。

如需避免錯誤的詳細資訊，請參閱 [防止匯入錯誤](manage-bookmarks.md#prevent-import-errors)。

## <a name="about-keywords-and-reserved-keywords"></a>關於關鍵字和保留關鍵字

Q&可以有多個關鍵字，並與其他答案共用相同的關鍵字，但無法共用 reserved 關鍵字。 保留的關鍵字是唯一的字詞或片語，可觸發一個特定的答案。 保留的關鍵字只能與一個應答相關聯。 請慎用保留關鍵字。

## <a name="frequently-asked-questions"></a>常見問題集

**問：在發佈後 Microsoft 搜尋中，q&a 可以在顯示多久時間？**

**A：** Q&a 是在發佈後立即 Microsoft 搜尋中提供。

**問：從 Microsoft 搜尋結果中移除的 Q&要花多久時間？**

**A**：已刪除的 Q&會立即從結果中移除。

**問：搜尋時，Q&的關鍵字比對書簽的工作是否相同？**

**A：**  如果是 Q&，則只支援基本層級的關鍵字比對英文關鍵字。 書簽支援更強健的關鍵字匹配層級。 針對書簽，會使用深入學習模型來判斷不同搜尋關鍵字的相似性。
