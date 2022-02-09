---
title: 管理結果類型
ms.author: jypal
author: jypal6
manager: jeffkizn
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: 管理搜尋結果頁面上的結果類型
ms.openlocfilehash: 177719b7d0a7971c8c9be87f1cdb0b5baca07a45
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62492289"
---
# <a name="manage-result-types"></a>管理結果類型

您可以使用結果類型來 [設計版面](customize-results-layout.md) 配置，以定義搜尋結果在搜尋結果頁面上的顯示方式。 結果配置可讓您直接在搜尋結果中顯示有用資訊，讓使用者可以快速找到所需的資訊。

內建的內容類型（如檔案和人員）具有無法修改的標準版面配置。 結果類型用於[Graph 連接器](connectors-overview.md)內容。 當您設定具有屬性對應的連接器時，Microsoft 搜尋會使用連接器搜尋結果的預設搜尋結果版面配置。 標籤 *標題* 最為重要;您應該永遠會有指派此標籤的屬性，以使用預設的結果版面配置。 不過，針對您的連接器內容建立自訂結果類型，可讓您的使用者更 impactful 這些結果。

使用 [縱向] 和 [連接器] 內容時，您必須建立結果類型或執行對應的預設版面配置。 否則，垂直不會顯示任何搜尋結果。

## <a name="understanding-result-types"></a>瞭解結果類型

建立您自己的 [搜尋結果版面](customize-results-layout.md) 配置，並在建立結果類型時覆寫預設搜尋結果版面配置。 搜尋結果類型是導致不同類型的搜尋結果顯示方式不同的規則。 其包含下列參數：

- **一或多個條件**  若要比較每個搜尋結果。 例如內容來源及標題等條件。
- 用於符合條件之搜尋結果的 **結果版面**   配置。 產生的版面配置會控制符合條件的結果在搜尋結果頁面上的顯示方式。

您可以針對垂直顯示的內容使用多種結果類型。 當您將多個內容來源組合成單一垂直時，這可能很重要。 即使只有一種內容類型時，也可以用於更 impactful 的版面配置。 例如，在顯示事件詳細資料的垂直中，您可以自訂「高嚴重性」事件，使其具有比「低嚴重性」事件更明顯的色彩。 若要這麼做，可以在 **Rules** 區段中的 ' 嚴重性 ' 屬性上定義條件。

## <a name="create-or-update-result-types"></a>建立或更新結果類型

結果類型管理經驗是由嚮導驅動，您可以逐步指導您定義名稱、內容來源、規則和版面配置。 結果類型可在組織層級和 SharePoint 網站層級進行自訂。

### <a name="manage-organization-level-result-types"></a>管理組織層級的結果類型

1. 在  [Microsoft 365 系統管理中心](https://admin.microsoft.com/)中，移至 [**自訂**] 區段中的 [[**結果類型**](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/resulttypes)] 頁面。
2. 若要建立新的結果類型，請按一下 [ **新增** ] 或選取一個現有的結果類型進行編輯。
3. 設定結果類型之後，您可以複習並加以儲存。

### <a name="manage-site-level-result-types"></a>管理網站層級的結果類型

1. 在您想要管理結果類型的 Sharepoint 網站中，按一下齒輪以開啟 [設定] 面板。
2. 選取 [ **網站資訊**]，然後選取 [ **查看所有網站設定**]。  
3. 尋找 [Microsoft 搜尋] 區段，然後選取 [ **設定搜尋設定**]。
4. 在功能窗格中，移至 [自訂經驗]，然後選取 [ **結果類型**]。
5. 若要新增結果類型，請按一下 [ **新增**]。 或者，若要編輯結果類型，請選取清單中的結果類型。
6. 修改結果類型之後，您可以檢查並儲存結果類型。

## <a name="troubleshooting"></a>正在疑難排解

以下是您可能會看到的常見問題清單，以及修正這些問題的動作。

|問題  |動作  |
|---------|---------|
| 我在搜尋頁面上看不到我的結果版面配置，雖然已建立一個。 | 可能會有幾分鐘的延遲，因為這些設定會進行快取。 請等候幾分鐘後再試一次。        |
| 在 [結果類型] 頁面上沒有看到任何內容來源。 | 請確定您已設定連接器和索引的資料。   |
