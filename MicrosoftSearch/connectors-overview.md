---
title: Microsoft Graph 連接器概述
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
description: Microsoft 搜尋的 Microsoft Graph 連接器的概覽
ms.openlocfilehash: 8bf63ba36032cbc0934f6d8120eddcdee69344b3
ms.sourcegitcommit: 6b49dced8c0c157110ceb38e678e969c76f80107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2021
ms.locfileid: "61558677"
---
<!---Previous ms.author: monaray --->

# <a name="overview-of-microsoft-graph-connectors"></a>Microsoft Graph 連接器的概述

[Microsoft 搜尋](./overview-microsoft-search.md)會索引所有的[Microsoft 365](https://www.microsoft.com/microsoft-365)資料，讓使用者可供搜尋。 透過 Microsoft Graph connector，您的組織可以為協力廠商資料編制索引，使其出現在 Microsoft 搜尋結果中。 這項功能可展開 Microsoft 365 生產力應用程式中可搜尋的內容來源類型，以及更廣泛的 Microsoft 生態用。 協力廠商資料可以位於內部部署或公用或私人雲端。

<!---link Microsoft Graph reference in line 19 when we have access to relevant documentation--->

本文的目的是協助 Microsoft 365 管理員找到可回答下列問題的資源：

* [哪些資料來源可以與 Microsoft 搜尋連線？](#what-data-sources-can-be-connected-to-microsoft-search)
* [如何管理連線？](#how-do-i-manage-my-connections)
* [Microsoft Graph 連接器的授權需求和使用條款為何？](#what-are-the-license-requirements-and-terms-of-use-for-connectors)
* [預覽功能為何？](#what-are-the-preview-features)
* [如何自訂及設定搜尋結果？](#how-do-i-customize-and-configure-search-results)
* [如何從自訂應用程式搜尋我的連接器資料？](#how-do-i-search-my-connector-data-from-a-custom-application)
* [如何自訂搜尋結果？](#how-do-i-customize-search-results)
* [連接器限制是什麼](#what-are-the-connector-limitations)

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

## <a name="what-data-sources-can-be-connected-to-microsoft-search"></a>哪些資料來源可以與 Microsoft 搜尋連線？

Microsoft 提供9個連接器和我們的生態系統合作夥伴已透過100以上的連接器建立。 您也可以建立您自己的連接器。

### <a name="microsoft-graph-connectors-by-microsoft"></a>microsoft Graph 連接器

您可以使用 Microsoft 所建立的連接器連線到下列資料來源：

<!---Add links below when new docs are created--->
* [Azure Data Lake Storage Gen2](azure-data-lake-connector.md)
* [Azure DevOps](azure-devops-connector.md)
* [Azure SQL 和 Microsoft SQL Server](MSSQL-connector.md)
* [Confluence 雲端 (預覽) ](confluence-cloud-connector.md)
* [企業網站](enterprise-web-connector.md)
* [MediaWiki](mediawiki-connector.md)
* [檔案共用](fileshare-connector.md)
* [Oracle SQL](OracleSQL-connector.md)
* [Salesforce](salesforce-connector.md)
* [ServiceNow 知識](servicenow-knowledge-connector.md)
* [ServiceNow 目錄 (預覽) ](servicenow-catalog-connector.md)

[Microsoft Graph 連接器圖庫](https://www.microsoft.com/microsoft-search/connectors)包含每個連接器的簡短描述。 如果您已準備好將其中一個資料來源連線至您的租使用者，請務必閱讀套用至資料來源之 Microsoft 安裝連接器中的 [安裝程式概述](configure-connector.md) 及其他任何文章。

### <a name="microsoft-graph-connectors-by-our-partners"></a>由我們的合作夥伴提供的 Microsoft Graph 連接器

[Microsoft Graph connector 圖庫](https://www.microsoft.com/microsoft-search/connectors)包含合作夥伴所建立之每個連接器的簡短說明，以及每個夥伴網站的連結。 若要深入瞭解，請直接與每個合作夥伴聯繫。

### <a name="build-your-own-microsoft-graph-connector"></a>建立您自己的 Microsoft Graph 連接器

您可以根據意願建立您自己的連接器。 如需建立連接器的開發人員檔，請參閱[Microsoft Graph 連接器概述](/graph/connecting-external-content-connectors-overview)。 如需建立連接器的快速入門，請參閱[組建第一個自訂的 Microsoft Graph 連接器](/graph/connecting-external-content-build-quickstart)。

## <a name="how-do-i-manage-my-connections"></a>如何管理連線？

您可以從[Microsoft 365 系統管理中心](https://admin.microsoft.com/)中的 [[連接器]](https://admin.microsoft.com/Adminportal/Home#/MicrosoftSearch/Connectors)索引標籤管理連線。 如需管理連線的詳細資訊，請參閱： [Manage a connections](manage-connector.md)。

## <a name="what-are-the-license-requirements-and-terms-of-use-for-connectors"></a>連接器的授權需求和使用條款為何？

您的組織中的使用者必須有有效的 Microsoft 365 或 Office 365 授權和足夠的連接器配額，才可在其搜尋結果中查看連接器的資料。

若要深入瞭解，請參閱 [授權需求和價格](licensing.md) 與 [使用條款](terms-of-use.md)。

## <a name="what-are-the-preview-features"></a>預覽功能為何？

雖然 Microsoft Graph 連接器和 Microsoft 搜尋 APIs 現在一般可用，但預覽中有許多功能。

預覽中的連接器和功能組包括：

* [Azure DevOps 連接器](azure-devops-connector.md)
* [Confluence 雲端連接器](confluence-cloud-connector.md)
* [ServiceNow 目錄連接器](servicenow-catalog-connector.md)
* [管理自訂篩選](custom-filters.md)
* [垂直中的多個連接](customize-search-page.md#multiple-connections-in-a-vertical)

## <a name="how-do-i-customize-and-configure-search-results"></a>如何自訂及設定搜尋結果？

有許多方式可自訂及設定搜尋結果。 若要深入瞭解，請參閱下列文章：

* [管理縱向](manage-verticals.md) 和 [結果類型](manage-result-types.md)
* [管理搜尋結果版面配置](customize-results-layout.md)
* [管理結果叢集](result-cluster.md)
* [管理自訂篩選](custom-filters.md)

## <a name="how-do-i-search-my-connector-data-from-a-custom-application"></a>如何從自訂應用程式搜尋我的連接器資料？

在索引自訂資料之後，開發人員可以 [查詢此資料](/graph/search-concept-custom-types)。 您可以在任何應用程式中查看資料。 如需詳細資訊，請參閱[Microsoft Graph 中的 Microsoft 搜尋 API 綜述](/graph/search-concept-overview)。

## <a name="how-do-i-customize-search-results"></a>如何自訂搜尋結果？

下一步是自訂搜尋結果（如本文中所建議的） [如何自訂及設定搜尋結果？](#how-do-i-customize-and-configure-search-results)。 若要深入瞭解自訂搜尋結果，請參閱 [自訂搜尋結果頁面](customize-search-page.md)。

## <a name="what-are-the-connector-limitations"></a>連接器限制為何？

* 當您 **發佈** Microsoft 建立的連接器時，可能需要幾分鐘的時間才能建立連線。 在此期間內，連接會顯示其狀態為 [擱置中]。

* 每秒大約四個專案會限制攝取輸送量。

* 不支援架構更新。 建立連線設定後，就無法更新架構。 您只可刪除並重新建立連線。

* 連接限制。 每個租使用者最多可以建立10個連接。

* 建立的連線之後，就無法進行編輯或變更。 如果您需要變更任何詳細資料，您必須刪除並重新建立連線。
