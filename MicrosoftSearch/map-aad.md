---
title: 對應 AAD 識別碼
ms.author: monaray
author: monaray97
manager: jameslau
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 如何對應 AAD 身分識別的步驟
ms.openlocfilehash: 3125f12ba1197cd65839fa9de2c4713104a3d35d
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62489917"
---
# <a name="map-your-azure-ad-identities"></a>對應您的 Azure AD 身分識別  

本文將引導您完成將 Azure AD 身分識別對應至資料來源的唯一識別碼 (非 Azure AD 身分識別的步驟，讓您的存取控制清單中的人員 (具有非) 身分) 識別的 ACL Azure AD 可以查看其範圍內的連接器搜尋結果。

這些步驟只會與使用「存取此資料來源的人」和「AAD」的「搜尋」許可權設定[Microsoft 的「](salesforce-connector.md)搜尋」許可權的搜尋系統管理員相關。 下列步驟會引導您如何將 Azure AD 使用者屬性對應至使用者的 **同盟 IDs**。

>[!NOTE]
>如果您是在 [搜尋許可權] 畫面上設定 [Salesforce 連接器](salesforce-connector.md)並只選取 [**存取此資料來源的人員** 和身分識別類型 **非 AAD** ]，請參閱 [對應您的非 Azure AD](map-non-aad.md)身分識別文章，以取得如何對應非 Azure AD 身分識別的步驟。  

## <a name="steps-for-mapping-your-azure-ad-properties"></a>對應 Azure AD 屬性的步驟

### <a name="1-select-azure-ad-user-properties-to-map"></a>1. 選取要對應的 Azure AD 使用者屬性

您可以選取需要對應至同盟識別碼的 Azure AD 屬性。

您可以從下拉式清單中選取 Azure AD 使用者屬性。 您也可以新增任意數目的 Azure AD 使用者屬性。若要建立組織的同盟識別碼對應，您也可以像您所需的屬性。

### <a name="2-create-formula-to-complete-mapping"></a>2. 建立完成對應的公式

您可以組合 Azure AD 使用者屬性的值，以建立唯一的同盟識別碼。

在 [公式] 方塊中，" {0} " 會對應至您所選取的 *第一個* Azure AD 屬性。 " {1} " 會對應至您所選取的 *第二個* Azure AD 屬性。 " {2} " 會對應至 *第三個* Azure AD 屬性等等。  

以下是一些具有範例正則運算式輸出和公式輸出的公式範例：

| 範例公式                  | 範例使用者的屬性 {0} 值                 | 範例使用者的屬性 {1} 值           | 公式的輸出                  |
| :------------------- | :------------------- |:---------------|:---------------|
| {0}.{1}@contoso .com  | firstname | 姓氏 |firstname.lastname@contoso.com
| {0}@domain .com                 | userid                 |             |userid@domain.com

在您提供公式後，您可以選擇性地按一下 [ **預覽** ]，以查看資料來源中5個隨機使用者的預覽，並套用各自的使用者對應。 預覽的輸出包含為這些使用者選取的步驟1中所選取的 Azure AD 使用者屬性值，以及該使用者的步驟2中所提供之最後一個公式的輸出。 此外，它也會指出是否可以透過 "Success" 或 "Failed" 圖示，將公式的輸出解析為您租使用者中的 Azure AD 使用者。  

>[!NOTE]
>按一下 [ **預覽**] 之後，如果有一或多個使用者對應的「失敗」狀態，您仍然可以繼續建立連接。 預覽會顯示5個隨機使用者，以及其從您的資料來源對應的映射。 如果您提供的對應未對應所有使用者，您可能會遇到此案例。

## <a name="sample-azure-ad-mapping"></a>範例 Azure AD 對應

請參閱下列快照，以取得樣本 Azure AD 對應。

![如何填滿 Azure AD 對應] 頁面的範例快照。](media/aad-mapping.png)

## <a name="limitations"></a>限制  

- 所有使用者只支援一個對應。 不支援條件式對應。  

- 發佈連線後，就無法變更對應。  

- Azure AD to 同盟識別碼轉換不支援 Azure AD 使用者屬性為 Regex 的運算式。