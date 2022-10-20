---
title: 將搜尋方塊新增至您的內部網路網站
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
ms.assetid: f980b90f-95e2-4b66-8b21-69f601ff4b50
ROBOTS: NoIndex
description: 將 Microsoft 搜尋搜尋方塊新增至您的內部網路網站或頁面，以取得相關的搜尋建議並更快速地尋找工作結果。
ms.openlocfilehash: cca526dbfde08b9cfcf38dd848e68cf5d011b23a
ms.sourcegitcommit: 851bd5803996acf15a8926cf49942208f4707738
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2022
ms.locfileid: "67733099"
---
# <a name="add-a-search-box-to-your-intranet-site"></a>將搜尋方塊新增至您的內部網路網站

若要讓使用者輕鬆存取組織的結果，請在 Bing 搜尋方塊中新增 Microsoft Search 至任何內部網路網站或頁面。 以下是一些優點：

- 內部網路入口網站上的搜尋方塊提供熟悉且受信任的進入點來開始搜尋
- 可新增至 SharePoint (傳統和新式) 、WordPress、SalesForce、Confluence 和其他內部網路頁面和網站
- 支援所有主要網頁瀏覽器，包括 Google Chrome 和 Microsoft Edge
- 只會顯示組織的搜尋建議，永遠不會包含 Web 建議
- 將使用者帶至 Bing 中的 Microsoft Search 工作結果頁面，其中排除廣告和 Web 結果
- 您可以控制搜尋方塊的外觀和行為，包括將使用者放在預設垂直或您已建立的自訂垂直上的能力

> [!NOTE]
>若要查看搜尋建議，使用者必須登入其 Azure AD 帳戶。 未登入的使用者會在輸入查詢之後，提示他們這麼做。
  
## <a name="add-a-search-box-to-a-sharepoint-wordpress-or-intranet-page"></a>將搜尋方塊新增至 SharePoint、WordPress 或內部網路頁面

您需要將兩個元件新增至頁面：搜尋方塊的容器和啟動該搜尋方塊的指令碼。
  
```html
<div id="bfb_searchbox"></div>
<script>
    var bfbSearchBoxConfig = {
        containerSelector: "bfb_searchbox"
    };
</script>
<script async src="https://www.bing.com/business/s?k=sb"></script>
```

- 針對 SharePoint 傳統或新式頁面，請從 [Microsoft Search 公用重現](https://github.com/microsoft-search/bing-search-box/releases/tag/v1)下載 bing-search-box.sppkg，將其部署至 SharePoint 應用程式目錄，然後將應用程式新增至 SharePoint 網站。 如需詳細資訊，請 [參閱將用戶端網頁元件部署至 SharePoint 頁面](/sharepoint/dev/spfx/web-parts/get-started/serve-your-web-part-in-a-sharepoint-page#deploy-the-helloworld-package-to-app-catalog)。
- 針對 WordPress 頁面，開啟編輯模式、新增自訂 HTML 小工具，然後新增腳本。

## <a name="add-a-search-box-to-your-confluence-page"></a>將搜尋方塊新增至 Confluence 頁面

在 [Confluence] 頁面上，選取 [ **編輯**]、新增具有這些參數的 iframe 小工具，然後選取 [發佈]。 
- Url： `https://www.bing.com/business/searchbox`
- 標題： `Org-Name search` 或 `Workplace search`
- 寬度： `560`
- 高度： `200`

## <a name="add-a-search-box-to-your-salesforce-home-page"></a>將搜尋方塊新增至您的 SalesForce 首頁

在 Visualforce Pages 中，建立新的檢視，並在 [標記] 區段中新增程式碼。

1. 以系統管理員身分登入您的 SalesForce 帳戶，然後選取右上角的 [ **安裝** 程式] 以開啟 [安裝程式] 頁面。
1. 在左側面板上，選取 [**平臺工具**  >  **自訂程式碼**  >  **] [Visualforce 頁面]**。
1. 建立新的檢視，並輸入其名稱。 在 [限制可見度] 區段中，將 [ **可見] 設定為 [所有使用者]**。
1. 儲存您的檢視。
1. 在檢視的中間，選取 [ **新增** ] 以開啟 [頁面編輯]。 輸入標籤、名稱，然後選取 [ **可供閃電體驗使用]、[體驗產生器網站] 和 [行動應用程式]** 核取方塊。
1. 在 [Visualforce 標記] 區段中，新增此程式碼並 **儲存**。

```html
<apex:page >
    <iframe width="500" height="300" src="https://www.bing.com/business/searchbox"></iframe>
</apex:page>
```

您也可以使用此程式碼自訂搜尋方塊的高度和寬度

```html
<apex:page >
  <div style="height:400px;">
  <div id="bfb_searchbox"></div>
  <script>
      var bfbSearchBoxConfig = {
          containerSelector: "bfb_searchbox",
          width: 400,
          strokeOutline: true
      };
  </script>
  <script async="async" src="https://www.bing.com/business/s?k=sb"></script>
  </div>
</apex:page>
```

若要將 Visualforce 元件新增至 SalesForce 首頁：
1. 移至您的 SalesForce 首頁。 `https://Instance-Name.lightning.force.com/lightning/page/home`
1. 選取齒輪圖示，然後 **選取 [編輯頁面]**。
1. 選取 [首頁] 上任何位置的 + (加) 圖示，以在該處新增 Visualforce 元件。
1. 在左側，選取 [Visualforce]。 在右側，選取您稍早建立的 Visualforce 頁面名稱。
1. 新增標籤並 **儲存**。
在您的 SalesForce 首頁上，您建立的搜尋方塊應該會出現。
  
## <a name="enable-the-search-box-for-mobile"></a>針對行動裝置啟用搜尋方塊

若要將內部網路網站或頁面提供給行動裝置使用者，請將 isMobile: true 新增至設定物件：
  
```html
<div id="bfb_searchbox"></div>
<script>
    var bfbSearchBoxConfig = {
        containerSelector: "bfb_searchbox", 
        isMobile: true
    };
</script>
<script async src="https://www.bing.com/business/s?k=sb"></script>
```

## <a name="put-focus-on-the-search-box-by-default"></a>根據預設，焦點會放置在搜尋方塊中

若要協助使用者加快搜尋速度，載入頁面或網站時，請將 focus: true 新增至設定物件來將游標放置在搜尋方塊中：
  
```html
<div id="bfb_searchbox"></div>
<script>
    var bfbSearchBoxConfig = {
        containerSelector: "bfb_searchbox",
        focus: true
    };
</script>
<script async src="https://www.bing.com/business/s?k=sb"></script>
```

## <a name="customize-the-appearance-of-the-search-box"></a>自訂搜尋方塊的外觀 

為了協助搜尋方塊更符合內部網路的樣式，您可以使用各種組態選項。 您可以混搭選項來符合您的需求。

```html
<div id="bfb_searchbox"></div>
<script>
    var bfbSearchBoxConfig = {
        containerSelector: "bfb_searchbox",
        width: 560,                             // default: 560, min: 360, max: 650
        height: 40,                             // default: 40, min: 40, max: 72
        cornerRadius: 6,                        // default: 6, min: 0, max: 25                                   
        strokeOutline: true,                    // default: true
        dropShadow: true,                       // default: false
        iconColor: "#067FA6",                   // default: #067FA6
        title: "Search box",                    // default: "Search box"
        vertical: "Person-people",              // default: not specified, search box directs to the All vertical on the WORK results page
        companyNameInGhostText: "Contoso"       // default: not specified
                                                // when absent, ghost text will be "Search work"
                                                // when specified, text will be "Search <companyNameInGhostText>"
    };
</script>
<script async src="https://www.bing.com/business/s?k=sb"></script>
```

## <a name="direct-users-to-a-default-or-custom-vertical"></a>將使用者導向至預設或自訂垂直

若要在企業營運應用程式或內部網路網站與您的工作結果之間提供簡單的整合，您也可以指定預設或自訂的垂直使用者在選取搜尋建議時應該登入。

使用 bfbSearchBoxConfig 中的垂直選項來定義您想要的垂直。 例如，如果您希望使用者一律登陸網站垂直，則使用預設垂直的其中一個，請使用 「Site-sites」 值。

:::image type="content" alt-text="Bing 中 Microsoft Search 的工作結果頁面螢幕擷取畫面，其中顯示網站垂直結果和 URL。" source="media/sites-vertical-esb.png" lightbox="media/sites-vertical-esb.png":::

針對自訂垂直，請使用 URL 結尾處的雜湊。 您可以從 Bing 上的工作頁面搜尋、按一下垂直標籤，然後在數位記號 (#) 之後複製值，來尋找這些值。

:::image type="content" alt-text="Bing 中 Microsoft Search 的工作結果頁面螢幕擷取畫面，其中顯示自訂簡報垂直結果和 URL。" source="media/custom-vertical-esb.png" lightbox="media/custom-vertical-esb.png":::

## <a name="use-an-iframe-to-embed-a-search-box"></a>使用 iFrame 來內嵌搜尋方塊

如果該網站沒有內嵌指令碼的選項，請使用 iFrame 來新增搜尋方塊。 您將無法自訂搜尋方塊。
  
```html
<iframe width="564" height="400" src="https://www.bing.com/business/searchbox"></iframe>
```

## <a name="inprivate-mode-and-conditional-access"></a>InPrivate 模式和條件式存取

如果在 InPrivate 視窗中開啟頁面或網站，則會停用內嵌搜尋方塊。 此外，使用 Microsoft Edge 中的 Azure AD 條件式存取支援時，Bing.com 在使用 InPrivate 模式時不支援 Azure AD 登入。 如需 Edge 中條件式存取的詳細資訊，請參閱 [Microsoft Edge 和條件式存取](/deployedge/ms-edge-security-conditional-access#accessing-conditional-access-protected-resources-in-microsoft-edge)。
