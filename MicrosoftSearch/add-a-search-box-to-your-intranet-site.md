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
description: 將 Microsoft 搜尋搜尋方塊新增至您的內部網路網站或頁面，以取得相關的搜尋建議並快速尋找工作結果。
ms.openlocfilehash: 61bd7901b82cd81fb6da97e4376f2d9468f3ec3f
ms.sourcegitcommit: 2fc1bc29249d6342a10d85bca291a1bec8bc125c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2022
ms.locfileid: "62492053"
---
# <a name="add-a-search-box-to-your-intranet-site"></a>將搜尋方塊新增至您的內部網路網站

若要讓您的使用者能夠輕鬆存取組織的結果，請在 Bing 搜尋方塊中，將 Microsoft 搜尋新增至任何內部網路網站或頁面。 以下是一些優點：

- SharePoint 或內部網路入口網站上的搜尋方塊，提供開始搜尋的熟悉、信任的進入點。
- 支援所有主要網頁瀏覽器，包括 Google Chrome 和 Microsoft Edge
- 只會顯示您組織的搜尋建議，永遠不會包含 web 建議
- 讓使用者在 Bing 工作結果頁面中的 Microsoft 搜尋，但不包括廣告和 web 結果
- 您可以控制搜尋方塊的外觀和行為，包括讓使用者在預設垂直或自訂垂直上進行土地的功能。
  
## <a name="add-a-search-box-to-an-intranet-page"></a>將搜尋方塊新增至內部網路頁面

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

在 SharePoint 傳統網站上，新增指令碼編輯器網頁組件並將指令碼放置在其中。
  
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

為了協助讓搜尋方塊更符合您的內部網路的樣式，您可以使用各種不同的組態選項。 您可以混搭選項來符合您的需求。

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

## <a name="direct-users-to-a-default-or-custom-vertical"></a>將使用者定向至預設或自訂的垂直

若要在企業營運人員或內部網路網站與您的工作結果之間提供簡便的整合，您也可以自訂搜尋方塊，方法是指定使用者在按下搜尋建議時所應居住在該位置的預設或自訂垂直。

使用 bfbSearchBoxConfig 中的 [垂直] 選項來定義您想要的垂直方向。 例如，如果您想要讓使用者永遠在網站上水準土地，其中一個預設的縱向，請使用「網站網站」值。

:::image type="content" alt-text="Microsoft 搜尋中的工作結果頁面的螢幕擷取畫面 Bing 顯示網站的縱向結果和 URL。" source="media/sites-vertical-esb.png" lightbox="media/sites-vertical-esb.png":::

若為自訂的縱向，請在 URL 的結尾使用雜湊。 您可以從 Bing 中的 [工作] 頁面進行搜尋，按一下垂直標籤，然後在數位 sign ( # ) 之後複製值，以找到這些值。

:::image type="content" alt-text="Bing 顯示自訂簡報垂直結果和 URL 的 Microsoft 搜尋中的工作結果頁面的螢幕擷取畫面。" source="media/custom-vertical-esb.png" lightbox="media/custom-vertical-esb.png":::

## <a name="use-an-iframe-to-embed-a-search-box"></a>使用 iFrame 來內嵌搜尋方塊

如果該網站沒有內嵌指令碼的選項，請使用 iFrame 來新增搜尋方塊。 您將無法自訂搜尋方塊。
  
```html
<iframe width="564" height="400" src="https://www.bing.com/business/searchbox"></iframe>
```

## <a name="inprivate-mode-and-conditional-access"></a>InPrivate 模式和條件式存取

如果在 InPrivate 視窗中開啟頁面或網站，就會停用內嵌搜尋方塊。 此外，在 Microsoft Edge 中使用 Azure AD 條件式存取支援時，Bing .com 在使用 InPrivate 模式時不支援 AAD 登入。 如需 Edge 中的條件式存取的詳細資訊，請參閱[Microsoft Edge 和條件式存取](/deployedge/ms-edge-security-conditional-access#accessing-conditional-access-protected-resources-in-microsoft-edge)。 
