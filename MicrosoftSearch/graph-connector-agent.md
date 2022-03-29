---
title: Graph 連接器代理程式
ms.author: rusamai
author: rsamai
manager: jameslau
audience: Admin
ms.audience: Admin
ms.topic: article
ms.service: mssearch
ms.localizationpriority: medium
search.appverid:
- BFB160
- MET150
- MOE150
description: Graph 連接器代理程式使用 Microsoft 建立的連接器為檔案共用、SQL、Confluence 等建立內部部署內容的索引。
ms.openlocfilehash: 1282add056393179e0dda88b4b60f8be210e2dc1
ms.sourcegitcommit: b0fff1c58aad93615816b059457dcfd257b3a5bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2022
ms.locfileid: "64404899"
---
# <a name="microsoft-graph-connector-agent"></a>Microsoft Graph Connector 代理程式

使用部署連接器時，需要安裝 *Microsoft Graph 連接器代理程式* 軟體。 它可讓內部部署資料和連接器 APIs 之間進行安全的資料傳輸。 本文將引導您完成安裝和設定代理程式的步驟。

## <a name="installation"></a>安裝

 (GCA) [https://aka.ms/GCAdownload](https://aka.ms/gcadownload) 下載最新版本的 Graph 連接器代理程式，並使用安裝精靈安裝軟體。 GCA 軟體的版本資訊可于[這裡](./graph-connector-agent-releases.md)取得

使用下列所述機器的建議設定，Graph 連接器代理程式實例最多可以處理三個連接。 超過該數目的任何連線可能會降低代理程式上所有連接的效能。

建議的設定：

* Windows 10，Windows Server 2016 R2 以上
* [.Net Framework 4.7.2 版](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net472)
* [.NET Core Desktop Runtime 3.1 (x64) ](https://dotnet.microsoft.com/download/dotnet-core/3.1)
* 8核心，3 GHz
* 16 GB 的 RAM，2 GB 的磁碟空間
* 透過443對資料來源和網際網路的網路存取

如果您組織的 proxy 伺服器或防火牆封鎖與未知網域的通訊，請將下列規則新增至 ' allow」清單。

1. *.servicebus.windows.net
2. events.data.microsoft.com
3. https://<span>login.microsoftonline.</span>com
4. HTTPs://<span>gc。</span>com
5. HTTPs://<span>graph。</span>com

>[!NOTE]
>不支援 Proxy 驗證。 如果您的環境具有需要驗證的 proxy，我們建議的做法是讓連接器代理程式略過 proxy。

## <a name="create-and-configure-an-app-for-the-agent"></a>建立及設定代理程式的應用程式  

首先，登入並注意，帳戶的必要許可權最低為「搜尋管理員」。 然後，代理程式會要求您提供驗證詳細資料。 使用下列步驟來建立應用程式，並產生必要的驗證詳細資料。

### <a name="create-an-app"></a>建立應用程式

1. 移至 [Azure 入口網站](https://portal.azure.com) ，並使用租使用者的系統管理員認證登入。

2. 流覽至功能窗格中 **Azure Active Directory**  ->  的 **應用程式註冊**，然後選取 [新增] [**註冊**]。

3. 提供應用程式的名稱，然後選取 [ **註冊**]。

4. 記下應用程式 (用戶端) 識別碼。

5. 從功能窗格開啟 **API 許可權** ，然後選取 [ **新增許可權**]。

6. 選取 [ **Microsoft Graph** ]，然後選取 [**應用程式許可權**]。

7. 在 [許可權] 中搜尋 "ReadWrite ExternalItem"、"OwnedBy" 和 [ReadWrite ExternalItem]，然後選取 [ **新增許可權**]。

8. 選取 **[授與「TenantName] 的系統管理員同意** ，並選取 [ **是**]。

9. 檢查許可權是否處於「授與」狀態。

    :::image type="content" alt-text="顯示為以綠色的右側欄授與的許可權。" source="media/onprem-agent/granted-state.png" lightbox="media/onprem-agent/granted-state.png":::

### <a name="configure-authentication"></a>設定驗證

您可以使用用戶端密碼或憑證提供驗證詳細資料。 遵循您的選擇步驟。

#### <a name="configuring-the-client-secret-for-authentication"></a>設定用戶端密碼進行驗證

1. 移至 [Azure 入口網站](https://portal.azure.com) ，並使用租使用者的系統管理員認證登入。

2. 從功能窗格開啟 **應用程式註冊** ，然後移至適當的應用程式。 在 [ **管理**] 下，選取 [ **憑證和機密**]。

3. 選取 [ **新增用戶端密碼** ]，然後選取密碼到期期限。 複製產生的密碼並加以儲存，因為它不會再次顯示。

4. 使用此用戶端密碼和應用程式識別碼來設定代理程式。 您不能在代理程式的 [ **名稱** ] 欄位中使用空格。 會接受字母數位字元。

#### <a name="using-a-certificate-for-authentication"></a>使用憑證進行驗證

使用憑證型驗證有三個簡單的步驟：

1. 建立或取得憑證
2. 將憑證 Upload 至 Azure 入口網站
3. 將憑證指派給代理程式

##### <a name="step-1-get-a-certificate"></a>步驟1：取得憑證

下列腳本可用於產生自我簽署憑證。 您的組織可能不允許自我簽署的憑證。 在此情況下，請使用此資訊來瞭解需求，並根據組織的原則取得憑證。

```powershell
$dnsName = "<TenantDomain like agent.onmicrosoft.com>" # Your DNS name
$password = "<password>" # Certificate password
$folderPath = "D:\New folder\" # Where do you want the files to get saved to? The folder needs to exist.
$fileName = "agentcert" # What do you want to call the cert files? without the file extension
$yearsValid = 10 # Number of years until you need to renew the certificate
$certStoreLocation = "cert:\LocalMachine\My"
$expirationDate = (Get-Date).AddYears($yearsValid)
$certificate = New-SelfSignedCertificate -DnsName $dnsName -CertStoreLocation $certStoreLocation -NotAfter $expirationDate -KeyExportPolicy Exportable -KeySpec Signature
$certificatePath = $certStoreLocation + '\' + $certificate.Thumbprint
$filePath = $folderPath + '\' + $fileName
$securePassword = ConvertTo-SecureString -String $password -Force -AsPlainText
Export-Certificate -Cert $certificatePath -FilePath ($filePath + '.cer')
Export-PfxCertificate -Cert $certificatePath -FilePath ($filePath + '.pfx') -Password $securePassword
```

##### <a name="step-2-upload-the-certificate-in-the-azure-portal"></a>步驟2：在 Azure 入口網站中 Upload 憑證

1. 開啟應用程式，並流覽至左窗格中的 [憑證和機密] 區段。

2. 選取 [ **Upload 憑證**] 並上傳 .cer 檔案。

3. 開啟 **應用程式註冊** ，然後從功能窗格中選取 **憑證和密碼** 。 複製憑證指紋。

:::image type="content" alt-text="在左窗格中選取憑證和密碼時的指紋憑證清單。" source="media/onprem-agent/certificates.png" lightbox="media/onprem-agent/certificates.png":::

##### <a name="step-3-assign-the-certificate-to-the-agent"></a>步驟3：將憑證指派給代理程式

如果您使用範例腳本來產生憑證，則可以在腳本中所識別的位置找到 PFX 檔案。

1. 將憑證 pfx 檔案下載到代理程式電腦上。

2. 連按兩下 pfx 檔，以啟動 [憑證安裝] 對話方塊。

3. 安裝憑證時，選取存放區位置的 **本機電腦** 。

4. 安裝憑證之後，請透過 [開始] 功能表開啟 **管理電腦憑證**。

5. 選取 [**個人**  >  **憑證**] 底下的新安裝憑證。

6. 以滑鼠右鍵按一下 [cert]，然後選取 [**所有任務**  >  **管理私密金鑰**] 選項。

7. 在 [許可權] 對話方塊中，選取 [新增] 選項。 它會向裡彈出新的視窗。 選取其中的 [位置] 選項。 在顯示的位置清單中，選取代理安裝所在的機器，然後按一下 **[確定]**。

8. 在 [使用者選擇] 對話方塊中，寫入： **NT Service\GcaHostService** ，然後按一下 **[確定]**。 不要按一下 [ **檢查名稱** ] 按鈕。

9. 在 [許可權] 對話方塊中按一下 [確定]。 代理程式機器現在已設定為讓代理程式使用憑證來產生權杖。

## <a name="troubleshooting"></a>疑難排解

### <a name="installation-failure"></a>安裝失敗

在安裝失敗的情況下，請執行下列步驟來檢查安裝記錄檔： msiexec/i "< msi # A1\GcaInstaller.msi"/L * V "< 目的地路徑 > \install.log" 的路徑。 如果錯誤無法解析，請使用記錄檔來支援 MicrosoftGraphConnectorsFeedback@service.microsoft.com。

### <a name="registration-failure"></a>註冊失敗

如果登入至 config 應用程式失敗，並出現「登入失敗，請按一下登入」按鈕，再試一次。」。 在瀏覽器驗證成功之後，請開啟 services.msc，並檢查 GcaHostService 是否正在執行中。 如果不是，請手動啟動。

當服務無法啟動時，錯誤是「因為登入失敗而無法啟動服務」，請檢查 virtual account： NT Service\GcaHostService 是否有權登入機器上的服務。 如需相關指示，請查看 [此連結](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) 。 [！注意] 如果新增使用者或群組的選項在本機使用者管理員許可權指派中為灰色，表示嘗試新增此帳戶的使用者在此機器上沒有系統管理員許可權，或是有群組原則覆寫此項。 必須更新群組原則，以允許主機服務以服務的身分登入。

### <a name="connection-failure"></a>連接失敗

在建立與錯誤 ' 請檢查 username/password 和 datasource 路徑 ' 時的「測試連線」動作失敗時，即使提供的使用者名稱和密碼正確，也請確認使用者帳戶對安裝 Graph 連接器代理程式的機器具有互動登入許可權。 請參閱 [登錄原則管理](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally#policy-management) 的檔，以檢查登入許可權。 此外，請確定資料來源和代理程式機器位於相同的網路上。

在發生失敗時建立連線： "1011：無法存取或離線使用 Graph connector 代理程式]。請登入安裝代理程式的機器，如果尚未執行代理程式，請將其啟動。 如果連線持續失敗，請確認在註冊期間提供給代理程式的憑證或用戶端密碼未到期且具有必要許可權。
