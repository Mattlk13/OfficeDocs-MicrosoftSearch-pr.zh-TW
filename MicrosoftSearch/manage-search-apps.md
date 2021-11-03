---
title: 管理搜尋應用程式
ms.author: ankmis
author: jeffkizn
manager: parulm
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
ms.date: 10/27/2021
search.appverid:
- BFB160
- MET150
- MOE150
description: 管理組織的 bot 開發人員所發佈的搜尋應用程式
ms.openlocfilehash: 9bcd80ae20e8cdcffbcf64f4dfad4e2fc3b199f7
ms.sourcegitcommit: d2bb36b6d3102b08ced93faa5e102bdb7e7e1e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2021
ms.locfileid: "60723250"
---
# <a name="manage-search-apps-preview"></a>管理搜尋應用程式 (預覽) 

Microsoft 同盟搜尋平臺可讓您在 Microsoft 搜尋體驗中呈現資料，而不會將該資訊與您的 Microsoft 365 索引合併。 如需詳細資訊，請參閱 [宣佈 Microsoft 同盟搜尋平臺的開發人員預覽](https://techcommunity.microsoft.com/t5/microsoft-search-blog/announcing-developer-preview-of-the-microsoft-federated-search/ba-p/2480763)。 使用 Microsoft Bot 架構，您可以在搜尋結果頁面中顯示自訂應用程式中的資料作為搜尋應用程式。

> [!NOTE]
> 搜尋應用程式位於預覽中。 若要要求存取權，請使用[Microsoft 搜尋開發人員預覽] 表單](https://aka.ms/SearchDevPrivatePreview)。 在 [問題 7] 中，選取 [同盟搜尋]。

## <a name="create-search-apps"></a>建立搜尋應用程式

您組織中的開發人員可以建立搜尋應用程式，並提交以供搜尋系統管理員核准。 若要瞭解如何建立搜尋應用程式，請參閱：[連線要搜尋的 Bot 架構 bot](/azure/bot-service/bot-service-channel-connect-search)。 當開發人員建立搜尋應用程式和資料來源的連結之後，就可以準備好進行核准。 開發人員提交應用程式之後，它會顯示在搜尋 & 智慧系統管理中心。

## <a name="publish-search-apps"></a>發佈搜尋應用程式

搜尋管理員和編輯者可以發佈或停用搜尋應用程式。 立即發佈搜尋應用程式會在搜尋結果頁面中顯示結果。 停用搜尋應用程式表示組織中的使用者在搜尋結果頁面上不會看到此搜尋應用程式的結果。

- **發行狀態**：透過 Microsoft 搜尋，可對組織的使用者提供搜尋應用程式。
- **停用狀態**：您的使用者無法使用已儲存為停用狀態的搜尋應用程式。 如果您或其他專案關係人想要在發佈之前複查搜尋應用程式，請使用此狀態。
- **需要檢查狀態**：開發人員提交的搜尋應用程式會顯示在此狀態，直到發佈或停用。

開發人員可以隨時刪除搜尋應用程式。 若要深入瞭解，請參閱[連線的 Bot Framework bot 進行搜尋](/azure/bot-service/bot-service-channel-connect-search)。

> [!NOTE]
> 開發人員檔也稱為搜尋應用程式。

若要管理搜尋應用程式，請遵循下列步驟：

1. 在[Microsoft 365 系統管理中心](https://admin.microsoft.com/)中，移至 [[搜尋應用程式](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/searchapps)]。
1. 按一下清單視圖中的搜尋應用程式名稱。
1. 按一下 [ **啟用搜尋結果的答案] 頁面** 核取方塊，可允許此搜尋應用程式以所有垂直顯示結果。
1. 按一下 [ **發佈** ] 以發行此搜尋應用程式。
1. 如果您不想要看到此應用程式的結果，請按一下 [ **停用搜尋應用程式** ]。
1. 若要對搜尋應用程式的開發人員提供意見反應，您可以使用 [詳細資料] 面板中的 [ **傳送意見反應郵件** ] 連結。
