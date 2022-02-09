---
title: Bing 中 Microsoft 搜尋的安全性和隱私權
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
description: 使用 Bing 中的 Microsoft 搜尋提供授權使用者的資訊，以保護公司的資料和使用者。
ms.openlocfilehash: 5d9ce2fb7cd40c8437ba8929170477bac0aac65e
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62493559"
---
# <a name="security-and-privacy-for-microsoft-search-in-bing"></a>Bing 中 Microsoft 搜尋的安全性和隱私權

使用增強型隱私權和安全性措施，Bing 中 Microsoft 搜尋可協助保護您的使用者和工作場所資料。

## <a name="secure-by-default"></a>預設安全性

Bing 要求中的 Microsoft 搜尋是透過 HTTPS 進行。 針對增強的安全性，此連接會以端對端為加密。
  
## <a name="authentication-and-authorization-with-azure-active-directory"></a>搭配 Azure Active Directory 的驗證與授權

Bing 中 Microsoft 搜尋的驗證是系結到 Azure Active Directory。 當 Microsoft Search 使用者前往 Bing，Bing 標頭會顯示 Microsoft 帳戶以及公司或學校帳戶的登入選項。 如果 Bing 無法判斷使用者是否為合格的參與者，使用者可以移至[探索 Microsoft Search](https://www.bing.com/business/explore) 頁面，該頁面會自動將使用者重新導向至組織的登入頁面。

使用者僅能透過公司或學校帳戶存取 Microsoft Search。 若要登入，他們必須使用與存取 Office 365 服務 (例如 SharePoint 或 Outlook) 相同的認證。 個人 Microsoft 帳戶無法用來登入 Microsoft Search。

## <a name="single-sign-on"></a>單一登入

如果使用者已在另一個服務中使用公司或學校帳戶驗證，例如 Outlook 或 SharePoint，當他們移至相同瀏覽器中的 Bing 時，系統會自動登入相同的工作或學校帳戶。 此外，當使用者登出他們的公司或學校帳戶時，系統會自動從相同瀏覽器中的其他 Microsoft Office 服務登出。
  
## <a name="communicates-with-the-microsoft-cloud-from-the-browser"></a>從瀏覽器與 Microsoft 雲端通訊

當使用者以公司或學校帳戶登入時，Bing 會在瀏覽器中下載所需的用戶端資料庫，以取得 Microsoft Search 結果。 隨後，當他們搜尋時，瀏覽器內的程式碼會呼叫 Office 365 雲端，以取得工作結果。 若要這麼做，Microsoft 搜尋會使用依照 SSAE 18 SOC2 Type 1 之控制目標所運作的專用 API。 這表示，「工作結果」和「工作資料」不會流過 Bing 系統，其受限於很低的資料處理控制目標，而不是工作結果在 Office 365 核心線上服務中處理時所服從。
  
## <a name="permissions"></a>權限

從 Office 365 工作負載 (例如 SharePoint 和商務用 OneDrive) 擷取的工作結果，都會在來源經過適當的安全性調整。 使用者無法看到像是 Word 文件或 PowerPoint 簡報這類透過 Office 365 檢視或存取的來源。 使用者只能查看自己的檔案，以及由作者在 SharePoint 中明確或隱含地 (例如透過群組資格) 與他們共用的檔案。

## <a name="microsoft-search-in-bing-protects-workplace-searches"></a>Bing 中的 Microsoft 搜尋保護工作地點搜尋

當使用者在 Bing 中的 Microsoft 搜尋進入搜尋查詢時，會發生兩個同時進行的搜尋要求：

- 組織內部資源的搜尋。
- 從 Bing .com 進行個別的公開結果搜尋。

由於工作地點搜尋可能是敏感的，因此 Microsoft 搜尋已執行一組信任量值，說明如何處理來自 Bing .com 的個別公開搜尋結果。

### <a name="logging"></a>記錄

- 所有與 Bing 流量中 Microsoft 搜尋相關的 Bing .com 搜尋記錄都與您的工作區身分識別解除關聯。
- 如果符合一組限制或頻率闕值，讓我們相信查詢不是特定組織所特有的查詢，則會依照 [隱私權](https://privacy.microsoft.com/privacystatement)說明的「搜尋和人工智慧」區段中所述的方式來處理查詢。 例如，這類查詢將用來建立公用功能的模型及定型，例如 autosuggest 或相關的搜尋。
- 不符合這組限制或頻率閾值的查詢，將會與公開的非 Microsoft Search 流量分開儲存。

### <a name="advertising"></a>廣告

Bing .com 上顯示的廣告與工作場所搜尋有關，與搜尋查詢的內容完全相關。 廣告永遠不會根據使用者的工作場所身分識別來鎖定使用者。

## <a name="gdpr"></a>GDPR

Microsoft 在[ 2018 年 5 月 21 日的部落格文章](https://blogs.microsoft.com/on-the-issues/2018/05/21/microsofts-commitment-to-gdpr-privacy-and-putting-customers-in-control-of-their-own-data/)反映了我們對 GDPR 規範，以及 Microsoft 會如何協助企業與組織履行 GDPR 合規性義務的承諾。 您可以在 Microsoft [信任中心常見問題集](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-faqs)中找到其他詳細資料。

針對客戶的內部資源所執行的查詢和傳回的結果會被視為客戶資料，如此一來，也會符合「[信任中心」常見問題解答](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-faqs)中所述的「文章28」所述的處理器承諾。 Microsoft 搜尋 從 Microsoft 搜尋移至 public Bing 的查詢中，Microsoft 會以資料控制者的 GDPR 義務達成。
