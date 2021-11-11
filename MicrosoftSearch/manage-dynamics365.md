---
title: 'Dynamics 365 同盟搜尋 (預覽) '
ms.author: dawholl
author: dawholl
manager: kellis
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
description: 管理在搜尋結果中顯示 Dynamics 365 內容的方式
ms.openlocfilehash: 79d2450d15c8597ced66c2903e273efa18a9629f
ms.sourcegitcommit: 245830f51e4edc99baf0922053c3d9a9733c7893
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/11/2021
ms.locfileid: "60907640"
---
# <a name="dynamics-365-federation-search-preview"></a>Dynamics 365 同盟搜尋 (預覽) 

## <a name="microsoft-search-federation-and-connectors"></a>Microsoft 搜尋同盟和連接器

為了讓 Microsoft 搜尋更有用，我們正在引進 Microsoft 搜尋同盟。 透過同盟搜尋，組織可以在 Microsoft 搜尋中存取這些案例中的資料：

* 系統中遵循嚴格合規性需求的資料
* 無法留下系統界限的資料
* 儲存在部署上的敏感性資料，您的組織不想要在雲端上建立索引

透過同盟搜尋連線存取的資料不會在 Microsoft 搜尋中編制索引。 此外，您也可以使用 Microsoft 的內建連接器，輕鬆設定同盟搜尋連線。 我們的 Dynamics 365 connector 目前正在預覽中。 如果您有興趣加入預覽，請在 [aka.ms/D365FederationSearchPreview](https://aka.ms/D365FederationSearchPreview)中告知我們。 如需發行時間範圍，請參閱[Microsoft 搜尋藍圖](https://www.microsoft.com/microsoft-365/roadmap?filters=Microsoft%20Search)。

## <a name="dynamics-365-federation-connector"></a>Dynamics 365 同盟連接器

Microsoft Dynamics 365 是一線智慧商務應用程式，專為企業資源規劃及客戶關係管理而設計。 透過 Dynamics 365 同盟，Microsoft 搜尋提供無縫的搜尋體驗，讓使用者可以輕鬆地找出 Dynamics 365 中所儲存的最相關客戶和商務資料。 Dynamics 365 同盟連接器提供一些重要優點：

* **易於管理：** 簡化處理以設定及維護 Dynamics 365 實例的搜尋連線。
* **便於使用：** 使用者可以輕鬆快捷地找到以 Dynamics 365 儲存的重要資訊，包括帳戶、連絡人、開啟的機會等等。
* **更豐富的內容：** 若要讓 Dynamics 365 搜尋結果更有用，包含潛在客戶、連絡人及帳戶詳細資料等重要資訊。
* **內建資料保護：** Dynamics 365 結果只會針對具有連線的實例存取權的使用者顯示。
* **整合的搜尋體驗：** 為了維持統一的體驗，Dynamics 365 的結果在所有搜尋專案點間都是一致的。 不論您在哪裡搜尋，都可以使用相同的外觀與風格取得相同的結果。

## <a name="what-users-experience"></a>使用者經驗

Dynamics 365 的答案會出現在所有 Microsoft 搜尋畫布上的搜尋結果中，包括 SharePoint 線上、Bing 和 Office。

:::image type="content" alt-text="SharePoint、Bing 及 Office 的 Dynamics 365 回應的螢幕擷取畫面。" source="media/dynamics365/dynamics365-answer.png" lightbox="media/dynamics365/dynamics365-answer.png":::

從問題的答案中，使用 [ **更多 dynamics 365 結果** ] 連結可輕鬆查看更多 dynamics 365 搜尋結果。 它會將使用者帶到專用的 Dynamics 365 結果頁面，並提供與查詢相關的更多結果。

:::image type="content" alt-text="Dynamics 365 的螢幕擷取畫面，以及 SharePoint、Bing 及 Office 的結果。" source="media/dynamics365/dynamics365-vertical.png" lightbox="media/dynamics365/dynamics365-vertical.png":::

按一下或攻絲任何結果會開啟 Dynamics 365 並顯示詳細資訊。

:::image type="content" alt-text="Dynamics 365 中詳細資料頁面的螢幕擷取畫面。" source="media/dynamics365/dynamics365-detail-page.png" lightbox="media/dynamics365/dynamics365-detail-page.png":::

不管您的使用者從何處開始搜尋，其經驗都會是一致的，讓他們能夠快速找到最相關的 Dynamics 365 結果。 請參閱 Microsoft 組建2021影片以取得示範。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4P83t]

## <a name="supported-query-patterns"></a>支援的查詢模式

使用 Microsoft 搜尋來尋找 Dynamics 365 結果時，會支援自然語言和產品名稱查詢。 此外，Dynamics 365 查詢不區分大小寫。 使用自然語言模式，透過客戶名稱或位置以及其他經常使用的查詢來尋找連絡人、帳戶及機遇。 以下是一些範例：

* 神秘是 Contoso 的連絡人
* Contoso 的開啟機會
* 西雅圖的開啟機遇
* 西雅圖的帳戶是什麼
* 西雅圖的連絡人
* 這個月的潛在客戶即將結束
* 高優先順序的通話
* 連絡人遺失的電子郵件

產品名稱模式支援 Dynamics 365 應用程式的範圍，並會觸發 Dynamics 365 的結果，不論其在查詢中的出現位置為何：

* D365
* Dynamics 365
* Dynamics 365
* Dynamics CRM
* Dynamics Sales
* Dynamics Service
* Dynamics Field Service
* Dynamics 客戶服務
* Dynamics Marketing
* Dynamics CE
* Dynamics 客戶參與
* 客戶接洽

## <a name="configure-the-dynamics-365-connector"></a>設定 Dynamics 365 連接器

使用此簡單設定，您可以為組織中的人員啟用 Dynamics 365 同盟搜尋體驗。 若要成功設定此連線，建議您先確認這些設定，再開始執行下列作業：

* Dataverse 搜尋是針對您想要連接的 Dynamics 365 環境啟用。 如需詳細資訊，請參閱 [Configure Dataverse search for 您的環境](/power-platform/admin/configure-relevance-search-organization)。
* 設定連接器的搜尋管理具有 Dynamics 365 的有效存取權。 如需詳細資訊，請參閱 [指派授權](/power-platform/admin/assign-licenses)。

驗證這些設定之後，請遵循下列步驟來設定連接器：

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com)中，移至 [[資料來源](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/connectors)]。

2. 在 [Microsoft 應用程式和服務] 區段的 [Microsoft Dynamics 365] 底下，選取 [ **管理** ] 以開啟 [microsoft dynamics 365] 面板。

3. 啟動組織的連接器。

4. 在 [ **端點** ] 清單中，選取您的 Dynamics 365 環境。

5. 在 [ **連接名稱**] 中，輸入此連線的描述性名稱。

6. 檢查並選取 [同意] 核取方塊。

7. 選取 [ **儲存** ] 以完成連接設定。

:::image type="content" alt-text="Microsoft 365 系統管理中心中 Dynamics 365 設定面板的螢幕擷取畫面。" source="media/dynamics365/dynamic365-connection-setup.png" lightbox="media/dynamics365/dynamic365-connection-setup.png":::

> [!TIP]
> 為了澄清使用者可以在搜尋類別中找到的內容類型，我們建議您更新垂直名稱。 若要自訂 Dynamics 365 垂直的名稱，請按一下 [ **編輯垂直**]。 如需詳細資訊，請參閱 [管理搜尋行業](/microsoftsearch/manage-verticals)。

當設定完成時，只有具有有效 Dynamics 365 授權的使用者和存取互連的 Dynamics 365 環境，才會顯示 Dynamics 365 的答案和垂直。 任何時候，您都可以變更連線端點環境或停用連接。
