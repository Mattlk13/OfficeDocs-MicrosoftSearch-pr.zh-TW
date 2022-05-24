---
title: MediaWiki Microsoft Graph連接器
ms.author: mecampos
author: mecampos
manager: umas
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 設定適用于 Microsoft 搜尋 的 MediaWiki Microsoft Graph 連接器
ms.openlocfilehash: ff8fd428095f531f7183730951c7bffc16cbe692
ms.sourcegitcommit: d267711f8e1c68849c99a4aad2bd387214825416
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2022
ms.locfileid: "65645935"
---
<!---Previous ms.author: monaray --->

# <a name="mediawiki-microsoft-graph-connector"></a>MediaWiki Microsoft Graph連接器

MediaWiki Microsoft Graph連接器可讓您的組織從使用 MediaWiki 軟體所建立的 Wiki 探索和編制資料索引。 此連接器會將指定的內容索引到Microsoft 搜尋，並支援定期編目，讓索引保持在最新狀態。

> [!NOTE]
> 請閱讀 [**Microsoft 365 系統管理中心文章中的設定 Microsoft Graph 連接器**](configure-connector.md)一文，以瞭解一般 Microsoft Graph 連接器設定指示。

本文適用于設定、執行及監視 MediaWiki 連接器的任何人。 它會補充一般設定程式，並顯示僅適用于 MediaWiki 連接器的指示。 本文也包含限制 [的相關](#limitations)資訊。

<!---## Before you get started-->

<!---Insert "Before you get started" recommendations for this data source-->

## <a name="step-1-add-a-connector-in-the-microsoft-365-admin-center"></a>步驟 1：在Microsoft 365 系統管理中心中新增連接器

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-2-name-the-connection"></a>步驟 2：命名連線

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-3-configure-the-connection-settings"></a>步驟 3：設定連線設定

輸入您的 **Wiki URL** ，然後從選項的下拉式功能表中選擇 **[驗證類型** ]。 選項為 **None**、 **Basic** 和 **OAuth 2.0 AAD**。

如果您選擇 **[基本** ] 作為 [驗證類型]，則必須提供 Wiki 的 **[使用者名稱** ] 和 [ **密碼** ]。

如果您選擇 **OAuth 2.0 AAD** 作為驗證類型，您必須提供 Wiki 安裝的 **資源標識** 符。 您也必須提供在 AAD 應用程式註冊頁面上產生的 **用戶端標識** 符和 **用戶端密碼** 。

## <a name="step-4-manage-search-permissions"></a>步驟 4：管理搜尋許可權

MediaWiki 連接器只支援每個人都能看見的搜尋權 **限**。 索引資料會出現在搜尋結果中，且組織中的所有使用者都可以看到。

## <a name="step-5-assign-property-labels"></a>步驟 5：指派屬性標籤

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-6-manage-schema"></a>步驟 6：管理架構

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-7-choose-refresh-settings"></a>步驟 7：選擇重新整理設定

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

## <a name="step-8-review-connection"></a>步驟 8：檢閱連線

請遵循一般 [設定指示](./configure-connector.md)。
<!---If the above phrase does not apply, delete it and insert specific details for your data source that are different from general setup instructions.-->

<!---## Troubleshooting-->
<!---To be added-->

## <a name="limitations"></a>限制

MediaWiki 連接器在預覽版本中有下列限制：

* 僅支援雲端式 Wiki。
* 僅支援具有Azure Active Directory或 Azure 驗證的基本或 OAuth 2.0。
* 不支援索引編制的命名空間選取。 僅索引 Main、Category 和 File 命名空間。
* 不支援存取控制清單 (ACL) 。 因此，組織中的所有使用者都可以看到已編制索引的頁面。