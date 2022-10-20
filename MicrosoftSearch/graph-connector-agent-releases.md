---
title: Microsoft Graph 連接器代理程式的發行歷程記錄
ms.author: harshkum
author: harshkum
manager: Siva
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid: ''
description: Microsoft Graph 連接器代理程式的發行歷程記錄，可用來使用 Microsoft 建置的連接器為內部部署資料來源編制索引
ms.openlocfilehash: 4fac8522a597307975305243f11ec840f011dcab
ms.sourcegitcommit: 8357d8d66ed5771f314787ddc875ed1e20d6e940
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2022
ms.locfileid: "67423643"
---
# <a name="release-history-for-microsoft-graph-connector-agent"></a>Microsoft Graph 連接器代理程式的發行歷程記錄

為內部部署資料來源編制索引需要您安裝 *Microsoft Graph 連接器代理* 程式軟體。 它允許在內部部署資料與連接器 API 之間進行安全的資料傳輸。

如需安裝的說明，請參閱此 [頁面](graph-connector-agent.md#installation)

[下載最新的 Graph 連接器代理程式](https://aka.ms/gcadownload)

### <a name="version-1800-25-jul-2022"></a>版本 1.8.0.0 (*25 Jul 2022*) 
* 支援增量編目和 OAuth for Microsoft Graph 連接器 SDK
* 錯誤修正和可靠性改善

### <a name="version-1700-16-jun-2022"></a>版本 1.7.0.0 (*2022 年 6 月 16* 日) 
* 停止編目和擷取資料的能力
* 安全性增強功能
* 錯誤修正和可靠性改善

### <a name="version-1600-09-may-2022"></a>版本 1.6.0.0 (*2022 年 5 月* 9 日) 
* 儀表板變更以啟用連接器多個實例的監視
* 錯誤修正和可靠性改善

### <a name="version-1510-21-mar-2022"></a>版本 1.5.1.0 (*2022 年 3 月 21* 日) 
* 錯誤修正和可靠性改善
* 變更「企業網站」連接器的預設屬性標籤指派

### <a name="version-1500-16-feb-2022"></a>版本 1.5.0.0 (*2022 年 2 月 16* 日) 
* 能夠更新用於驗證的用戶端秘密&憑證 
* 內部網路內部部署連接器的 OAuth 2.0 支援 
* 支援剖析 OneNote (.one) 檔案 
* 已修正剖析文字檔案 (.doc *) & PowerPoint 檔案上次修改日期的問題 (.ppt*)  

### <a name="version-1400-13-jan-2022"></a>版本 1.4.0.0 (*2022 年 1 月 13* 日) 
* 支援連接器的多個實例
* 錯誤修正和可靠性改善

### <a name="version-1310-28-oct-2021"></a>版本 1.3.1.0 (*2021 年 10 月 28* 日) 
* 每秒的檔案共用連接器檔改善
* 其他效能改善
* Bug 修正

### <a name="version-1300-8-oct-2021"></a>版本 1.3.0.0 (*2021 年 10 月 8* 日) 
* 一般可靠性改善
* Bug 修正

### <a name="version-1210-not-supported-3-sept-2021"></a>2021 年 9 月 3 日 *不支援* 1.2.1.0 版 ()  (*2021 年 9 月*) 
* Bug 修正

### <a name="version-1200-not-supported-16-aug-2021"></a>版本 1.2.0.0 (*不支援*)  (*2021 年 8 月 16* 日) 
* 支援 33 種語言的當地語系化字串：英文 - 美國、阿拉伯文、希臘文、卡達隆尼亞文、捷克文、丹麥文、德文、希臘文、西班牙文、愛沙尼亞文、芬蘭文、義大利文、日文、韓文、立陶宛文、拉脫維亞文、拉脫維亞文、葡萄牙文、俄文、斯洛伐克文、斯洛維尼亞文、塞爾維亞 (拉丁) 、瑞典文、泰文、土耳其文、葡萄牙文、中文 - 中國、中文 - 臺灣
* 如果代理程式當機，則繼續完整編目
* Bug 修正

### <a name="version-1100-not-supported-9-july-2021"></a>2021 年 7 月 9 日 *不支援* 1.1.0.0 (版)  (*2021 年 7* 月) 
* 支援檔案共用連接器的排除規則
* 效能改善
* Bug 修正
