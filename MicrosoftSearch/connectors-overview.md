---
title: 適用于 Microsoft 搜尋 的 Microsoft Graph 連接器概觀
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
description: 瞭解您的組織如何使用 Microsoft Graph 連接器為協力廠商資料編制索引，使其出現在Microsoft 搜尋結果中。
ms.openlocfilehash: 5d5401e80971e7299abcaa1a0686390940133577
ms.sourcegitcommit: b64b0ba3f779359fad24000c253a542ea92d053b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2022
ms.locfileid: "65245770"
---
<!---Previous ms.author: monaray --->

# <a name="microsoft-graph-connectors-overview-for-microsoft-search"></a>適用于 Microsoft 搜尋 的 Microsoft Graph 連接器概觀

[Microsoft 搜尋](./overview-microsoft-search.md)索引所有[Microsoft 365](https://www.microsoft.com/microsoft-365)資料，使其可供使用者搜尋。 透過 Microsoft Graph連接器，您的組織可以為協力廠商資料編制索引，使其出現在Microsoft 搜尋結果中。 這項功能會擴充可在您的Microsoft 365生產力應用程式和更廣泛的 Microsoft 生態系統中搜尋的內容來源類型。 協力廠商資料可以裝載于內部部署或公用或私人雲端中。

下列影片說明Microsoft 搜尋體驗的 Microsoft Graph 連接器設定程式。

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4SjFa]

下列影片說明Microsoft 搜尋體驗的Graph連接器設定程式。
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4SjFa]

<!---link Microsoft Graph reference in line 19 when we have access to relevant documentation--->

本文旨在協助Microsoft 365系統管理員找出可用來回答下列問題的資源：

* [哪些資料來源可以連線到Microsoft 搜尋？](#what-data-sources-can-be-connected-to-microsoft-search)
* [如何?管理我的連線嗎？](#how-do-i-manage-my-connections)
* [Microsoft Graph 連接器的授權需求和使用規定為何？](#what-are-the-license-requirements-and-terms-of-use-for-connectors)
* [什麼是預覽功能？](#what-are-the-preview-features)
* [如何?自訂和設定搜尋結果？](#how-do-i-customize-and-configure-search-results)
* [如何?從自訂應用程式搜尋我的連接器資料嗎？](#how-do-i-search-my-connector-data-from-a-custom-application)
* [如何?自訂搜尋結果？](#how-do-i-customize-and-configure-search-results)
* [連接器有哪些限制？](#what-are-the-limitations-of-microsoft-graph-connectors)

<!---Add Value, scenario, example, and/or graphic in December updates--->
<!---Probably remove architecture section below
## Architecture

The following architectural diagram of the Microsoft Graph platform shows how Graph connector content flows through content indexing to user results in [Microsoft Search](./overview-microsoft-search.md) clients. The rest of this section explains each of the key building blocks in the diagram.

![Diagram: on-premises and cloud-based data is pulled by connectors and indexed by the Microsoft Search API, and then the Microsoft Search service delivers the results to users.](media/connectors-overview/highlevel-connectors.png)
Graph connectors can pull data from cloud-based (SaaS) data sources and on-premises data stores. The above diagram shows connections to only two data sources, but you can add connections to up ten sources per tenant.

The Microsoft Graph Connectors API instantiates one connection per data source. Then, the API indexes and stores the data. Established connections interact with Microsoft Search, so users can get search results.

You can use the Microsoft 365 [admin center](https://admin.microsoft.com) to setup and manage any of the Graph connectors by Microsoft. The admin center has a simple user interface that makes it easy to establish the connection to your data source, and monitor connection status and utilization.

***Edit paragraph below***
To create a **connection** to a data source, admins need authenticated access to the data and the entire content repository. The data is fed to the graph connector service for indexing.--->

## <a name="what-data-sources-can-be-connected-to-microsoft-search"></a>哪些資料來源可以連線到Microsoft 搜尋？

Microsoft 提供九個 Microsoft Graph 連接器，而我們的生態系統合作夥伴已建立超過 100 個以上的連接器。 您也可以建置自己的連接器。

### <a name="microsoft-graph-connectors-by-microsoft"></a>Microsoft Graph連接器

您可以使用 Microsoft 建立的連接器來連線到下列資料來源：

<!---Add links below when new docs are created--->
* [Azure Data Lake Storage Gen2](azure-data-lake-connector.md)
* [Azure DevOps](azure-devops-connector.md)
* [Azure SQL 和 Microsoft SQL Server](MSSQL-connector.md)
* [Confluence Cloud](confluence-cloud-connector.md)
* [Confluence 內部部署](confluence-onpremises-connector.md)
* [企業網站](enterprise-web-connector.md)
* [Jira Cloud](jira-connector.md)
* [MediaWiki](mediawiki-connector.md)
* [檔案共用](fileshare-connector.md)
* [Oracle SQL](OracleSQL-connector.md)
* [Salesforce](salesforce-connector.md)
* [ServiceNow 知識](servicenow-knowledge-connector.md)
* [ServiceNow 目錄](servicenow-catalog-connector.md)

[Microsoft Graph連接器資源庫](https://www.microsoft.com/microsoft-search/connectors)包含每個連接器的簡短描述。 If you're ready to connect one of these data sources to your tenant, be sure to read the [Setup overview](configure-connector.md) and any other articles in the Setup connectors by Microsoft section that apply to your data source.

### <a name="microsoft-graph-connectors-by-our-partners"></a>我們的合作夥伴Graph Microsoft Graph連接器

[Microsoft Graph連接器資源庫](https://www.microsoft.com/microsoft-search/connectors)包含合作夥伴所建立之每個連接器的簡短描述，以及每個合作夥伴網站的連結。 若要深入瞭解，請直接連絡每個合作夥伴。

### <a name="build-your-own-microsoft-graph-connector"></a>建置您自己的 Microsoft Graph 連接器

您可以視需要建置自己的連接器。 如需建置連接器的開發人員檔，請[參閱 Microsoft Graph 連接器概觀](/graph/connecting-external-content-connectors-overview)。 如需建置連接器的快速入門，請參閱[建置您的第一個自訂 Microsoft Graph連接器](/graph/connecting-external-content-build-quickstart)。

## <a name="how-do-i-manage-my-connections"></a>如何?管理我的連線嗎？

您可以在Microsoft 365 系統管理中心的 [[連接器](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/Connectors)] 索引標籤上管理聯[機](https://admin.microsoft.com/)。 如需管理連線的詳細資訊，請 [參閱監視您的連線](manage-connector.md)。

## <a name="what-are-the-license-requirements-and-terms-of-use-for-connectors"></a>連接器的授權需求和使用規定為何？

若要讓組織中的使用者在其搜尋結果中檢視連接器的資料，您需要有效的Microsoft 365或Office 365授權和足夠的連接器配額。

若要深入瞭解，請參閱 [授權需求和定價](licensing.md) 和 [使用規定](terms-of-use.md)。

## <a name="what-are-the-preview-features"></a>什麼是預覽功能？

雖然 Microsoft Graph連接器和Microsoft 搜尋 API 現已正式推出，但有幾個功能處於預覽狀態。

預覽中的連接器和功能集包括：

* [Azure DevOps連接器](azure-devops-connector.md)
* [Confluence 內部部署連接器](confluence-onpremises-connector.md)
* [垂直的多個連接](customize-search-page.md#multiple-connections-in-a-vertical)

## <a name="how-do-i-customize-and-configure-search-results"></a>如何?自訂和設定搜尋結果？

有許多方式可自訂和設定搜尋結果。 若要深入了解，請參閱下列文章：

* [管理搜尋垂直](manage-verticals.md) 和 [結果類型](manage-result-types.md)
* [管理搜尋結果版面配置](customize-results-layout.md)
* [管理結果叢集](result-cluster.md)
* [管理自訂篩選](custom-filters.md)

## <a name="how-do-i-search-my-connector-data-from-a-custom-application"></a>如何?從自訂應用程式搜尋我的連接器資料嗎？

編制自訂資料的索引之後，開發人員就可以 [查詢此資料](/graph/search-concept-custom-types)。 您可以在任何應用程式中檢視您的資料。 如需詳細資訊，請參閱[Microsoft Graph 中Microsoft 搜尋 API 的概觀](/graph/search-concept-overview)。

## <a name="what-are-the-limitations-of-microsoft-graph-connectors"></a>Microsoft Graph連接器有哪些限制？

* 當您 **發佈** Microsoft Graph 連接器時，可能需要幾分鐘的時間才能建立連線。 在該時間內，連線會將其狀態顯示為擱置中。

* 擷取輸送量會限制在每秒大約四個項目。

* 不支援架構更新。 建立連線設定之後，就無法更新架構。 您只能刪除並重新建立連線。

* 有一個連線限制。 每個租用戶最多可以建立 10 個連線。

* 建立連線之後，您就無法編輯或變更連線。 如果您需要變更任何詳細資料，您必須刪除並重新建立連線。
