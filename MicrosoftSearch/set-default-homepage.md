---
title: 設定預設首頁
ms.author: anfowler
author: adefowler
manager: shohara
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
ms.assetid: c020bd72-9906-4dfd-bc77-57287f5927ce
description: 了解如何將 Bing 設定為公司使用 Microsoft Search 的預設首頁。
ms.openlocfilehash: 98f38b3eb97955a764f3b3611256e2a1dabcce24
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62493402"
---
# <a name="make-bingcom-the-default-home-page"></a>讓 Bing.com 成為預設首頁

本文將說明如何將 Bing.com 設定為 Microsoft Edge、Google Chrome 和 Internet Explorer 瀏覽器的預設首頁。 
  
 
## <a name="microsoft-edge-on-windows-10-version-1511-or-later"></a>Windows 10 版本 1511 或更新版本上的 Microsoft Edge

設定此原則之後，使用者將無法變更此原則。 

1. 開啟 [群組原則管理主控台] (gpmc.msc)，然後切換以編輯任何現有原則或建立新原則。 
1. 瀏覽至 **[系統管理範本]\[Windows 元件]\[Microsoft Edge]**。    
1. 按兩下 **[設定起始頁面]**，將它設為 **[已啟用]**，然後輸入 `https://www.bing.com/business`
1.  將結果 GPO 連結到適當網域以強制執行結果 GPO。

  
## <a name="google-chrome-on-windows-xp-sp2-or-later"></a>Windows XP SP2 或更新版本上的 Google Chrome


您可以在 [Microsoft 支援](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra)網站上找到有關管理 ADMX 檔案的 Windows 支援文章和不同版本 Windows 適用的最新 ADMX 檔案。

您也將需要最新的 Google 原則檔案，可以在 [Google Chrome Enterprise 說明](https://support.google.com/chrome/a/answer/187202)上找到。
  
如果在 GPMC 中找不到本節中描述的設定，請下載適當的 ADMX 並將它們複製到[集中存放區](/previous-versions/windows/it-pro/windows-vista/cc748955%28v%3dws.10%29)。 控制器上的集中存放區是使用下列命名慣例的資料夾：
  
 **%systemroot%\sysvol\\<domain\>\policies\PolicyDefinitions**
  
控制站處理的每個網域都應該有個別的資料夾。 可以透過命令提示字元使用下列命令來複製 ADMX 檔案：
  
 `Copy <path_to_ADMX.ADMX> %systemroot%\sysvol\<domain>\policies\PolicyDefinitions`
  
1. 開啟 [群組原則管理主控台] (gpmc.msc)，然後切換以編輯任何現有原則或建立新原則。
1. 確定在 *[使用者設定]/[電腦設定]* 中的 **[系統管理範本]** 區段中都有下列資料夾：Google Chrome 和 Google Chrome - 預設設定 (使用者可以覆寫)。
   - 第一個區段的設定是固定的，而且本機系統管理員無法變更它們。
   - 使用者可以在瀏覽器設定中變更原則後面區段的設定。
   您應該決定使用者是否可以覆寫您的預設設定。 在以下步驟中，在與您的組織政策和需求對應資料夾中的設定進行變更。 以下步驟會使用 Google Chrome - 預設設定做為預設值。

1. 瀏覽至 **&lt;[電腦/使用者設定]&gt;\[系統管理範本]\[Google Chrome - 預設設定]\[首頁]**。 
1. 按兩下 **[將新分頁設為首頁]**，然後將它設為 **[已啟用]**。 
1. 瀏覽至 **[&lt;電腦/使用者設定&gt;]\[系統管理範本]\[Google Chrome - 預設設定]\[新分頁]**。 
1. 按兩下 **[設定新分頁 URL]**，將它設為 **[已啟用]**，然後輸入 `https://www.bing.com/business?form=BFBSPR` 
1. 將結果 GPO 連結到適當網域以強制執行結果 GPO。

## <a name="internet-explorer-50-or-later"></a>Internet Explorer 5.0 或更新版本
設定此原則之後，使用者仍可變更首頁。 

1. 開啟 [群組原則管理主控台] (gpmc.msc)，然後切換以編輯任何現有原則或建立新原則。
    
2. 瀏覽至 **[使用者設定]\[喜好設定]\[控制台設定]\[網際網路設定]**。
    
3. 以滑鼠右鍵按一下 **[網際網路設定]**，然後選取 **[Internet Explorer 10]**。
    
    > [!NOTE]
    > 您需要選取 Internet Explorer 10 的選項來為 Internet Explorer 11 套用設定，因為同一個設定也適用 Internet Explorer 11。 
  
4. 以紅色底線標示的設定表示沒有在目標電腦上設定，以綠色底線標示的設定則表示已經在目標電腦上設定。 若要變更底線，請使用以下列功能鍵：
    
    F5 - 啟用目前索引標籤上的所有設定
    
    F6 - 啟用目前選取的設定
    
    F7 - 停用目前選取的設定
    
    F8 - 停用目前索引標籤上的所有設定
    
5. 在進行任何設定之前，請先按 **F8** 以停用所有設定。 畫面看起來應該像這樣： 
    
    ![Internet Explorer 10 屬性] 對話方塊。](media/2fd55755-5007-4e33-a795-c42ce2fcef4a.jpg)
  
6. 在首頁設定上按下 **F6**，然後輸入 `https://www.bing.com/business?form=BFBSPR`
    
7. 將結果 GPO 連結到適當網域以強制執行結果 GPO。