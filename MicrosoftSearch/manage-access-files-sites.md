---
title: 管理檔與網站的存取權
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
description: 系統管理員如何在組織內適當地限制存取網站和檔案的方式。
ms.openlocfilehash: b6599bc39b7fc302e435c30caf09d4d5d503aecb
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62489854"
---
# <a name="manage-access-to-files-and-sites"></a>管理檔與網站的存取權

並非每個檔案或網站都應該可供組織中的每個人使用。 管理員和使用者可以使用最能解決特定問題的解決方案，管理敏感或機密資訊的存取。 如果有足夠的存取控制不會持續套用，可能會產生所謂的「oversharing」。 讓您更容易尋找組織內共用的資訊，使用 Microsoft 搜尋不會不慎存取具有不正確限制的檔案和網站。

搜尋管理員無法解決這些 oversharing 問題。 不受限制存取的檔案和網站將會出現在內部搜尋結果中，而且會透過其他探索途徑來呈現。 不過，當控制以避免 oversharing 時，就會關閉所有的可包含搜尋的功能。

## <a name="solutions-to-prevent-oversharing"></a>避免 oversharing 的解決方案

使用下列工具、原則及技術來限制或模糊存取訊號，以協助防止 oversharing。 若要執行這些解決方案，可能需要全域、規範或安全性系統管理員存取權。 我們也建議使用內部活動，向您的使用者講解如何正確保護、標記和許可權其網站與檔案。

### <a name="public-sites-or-sites-with-public-groups-as-owners"></a>使用公用群組做為擁有者的公用網站或網站

可與所有人共用的單向檔案是透過公用網站或具有公用群組的網站擁有者。 敏感度標籤可以防止使用者建立公用群組或網站。 如需設定所有標籤以建立私人群組/網站，以及要求群組/網站標籤的詳細資訊，請參閱[使用敏感度標籤來保護 Microsoft Teams、Microsoft 365 群組和 SharePoint 網站中的內容](/microsoft-365/compliance/sensitivity-labels-teams-groups-sites)。

另一個選項是控制誰可以在您的組織中建立 Microsoft 365 群組。 如需詳細資訊，請參閱[為需要建立 Microsoft 365 群組的使用者建立群組](/microsoft-365/solutions/manage-creation-of-groups#step-1-create-a-group-for-users-who-need-to-create-microsoft-365-groups)。

在實施上述任一項解決方案時，我們也建議您為使用者設定可要求建立公用群組的處理常式，並通知使用者有關變更。

若限制建立群組的能力無法讓您的組織使用，您可以透過審核監控活動，包括群組的建立。 如需有關基本及高級審核的詳細資訊，請參閱[Microsoft 365 中的審計方案](/microsoft-365/compliance/auditing-solutions-overview)。

### <a name="shared-files"></a>共用檔

若要限制所有分類為商務機密的檔案的存取權，您可以定義及套用組織的資料分類。 需要收集資料範例，以協助訓練新的分類器。 如需必要條件和許可權的詳細資訊，請參閱 [瞭解資料分類](/microsoft-365/compliance/data-classification-overview)。

若要限制檔案存取特定群組的成員，如主管，您可以建立範圍設定為安全性群組的自訂標籤。 然後，當安全性群組成員套用標籤時，會自動限制對群組的存取。 若要深入瞭解自訂標籤，請參閱 [建立和設定敏感度標籤及其原則](/microsoft-365/compliance/create-sensitivity-labels) ，並 [使用敏感度標籤來限制對內容的存取，以套用加密](/microsoft-365/compliance/encryption-sensitivity-labels)。

為了確保檔和電子郵件已正確標示，系統管理員也可以設定預設的標籤原則，並要求使用者貼上標籤。 如需詳細資訊，請參閱[要求使用者在電子郵件和文件中套用標籤](/microsoft-365/compliance/sensitivity-labels-office-apps#require-users-to-apply-a-label-to-their-email-and-documents) (部分機器翻譯)。

您也可以在搜尋時，禁止顯示最近的檔案，也可以將檔案 oversharing 減至最少。 這可以在群組層級或組織中的每個人進行。 若要停止顯示群組的最近檔，請參閱[在 Microsoft Graph 中自訂專案 insights 隱私權](/graph/insights-customize-item-insights-privacy)。 群組成員將可以查看其自己最近的檔案，但其他人會收到未找到任何結果的訊息。 若要為組織中的所有人關閉最近使用的檔案，您必須關閉 Delve。 如需詳細資訊，請參閱[控制存取 Delve](/sharepoint/delve-for-office-365-admins#control-access-to-delve)。

> [!Note]
> 使用者仍然可以在 Microsoft 搜尋結果中找到與其共用的檔案。 自訂專案 insights 或關閉 Delve 只會停止在使用者的最近使用的檔案清單中顯示檔案。

### <a name="sites-and-files-between-groups"></a>群組間的網站與檔案

若要限制群組間的檔案和網站共用（例如，使用行銷小組管理機密專案的財務小組），您可以定義及實施資訊屏障原則。 這些壁壘也會防止在 Microsoft Teams、SharePoint 和 OneDrive 中進行通訊和共同作業的其他方面。 如需詳細資訊，請參閱[瞭解 Microsoft 365 中的資訊障礙](/microsoft-365/compliance/information-barriers)。

## <a name="get-access-insights"></a>取得 access insights

Access 控管提供組織中最具機密檔和 overshared 網站的網站洞察力。 如需概述，請參閱[SharePoint 和 OneDrive 中安全性和符合性的新功能](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/what-s-new-in-security-and-compliance-in-sharepoint-and-onedrive/ba-p/1696705)。 您必須為 [您的組織提名](https://forms.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR3-O9WDTKhhDtgWfphwS9YhUM0hJNklNRkZKMlhLNDRZNzlEQlVDSjdZVi4u) 這種預覽。
