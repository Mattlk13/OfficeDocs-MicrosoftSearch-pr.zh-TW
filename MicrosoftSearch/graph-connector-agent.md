---
title: Microsoft Graph 連接器代理程式
ms.author: kam1
author: kam1
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
description: 使用 Microsoft 建置的檔案共用、SQL、Confluence 等連接器來編制內部部署內容索引的 Microsoft Graph 連接器代理程式概觀。
ms.openlocfilehash: cd5de802486269b3a0ea84f168b99c90bfb5db91
ms.sourcegitcommit: 1f8f69a9f7b48880ba23a38ed4bbd84d3e072f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2022
ms.locfileid: "67597071"
---
# <a name="microsoft-graph-connector-agent"></a>Microsoft Graph 連接器代理程式

使用內部部署連接器需要安裝 *Microsoft Graph 連接器代理程式* 軟體。 它允許在內部部署資料與連接器 API 之間進行安全的資料傳輸。 本文會引導您安裝和設定代理程式。

## <a name="installation"></a>安裝

從 [https://aka.ms/GCAdownload](https://aka.ms/gcadownload) 下載最新版的 Microsoft Graph 連接器代理程式，並使用安裝組態助理安裝軟體。 這裡[提供連接](./graph-connector-agent-releases.md)器代理程式軟體的版本資訊

使用下列所述機器的建議設定，連接器代理程式實例最多可以處理三個連線。 超過此範圍的任何連線都可能會降低代理程式上所有連線的效能。

建議的設定：

* Windows 10、Windows Server 2016 R2 和更新版本
* [.Net Framework 4.7.2](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net472)
* [.NET Core 桌面執行時間 3.1 (x64) ](https://dotnet.microsoft.com/download/dotnet-core/3.1)
* 8 核心，3 GHz
* 16 GB RAM、2 GB 磁碟空間
* 透過 443 對資料來源和網際網路的網路存取

如果您組織的 Proxy 伺服器或防火牆封鎖對未知網域的通訊，請將下列規則新增至 [允許] 清單：

| **M365 企業版** | **M365 Government** |
| ------------- | -------------|
| 1. `*.servicebus.windows.net` | 1. `*.servicebus.usgovcloudapi.net`
| 2. `*.events.data.microsoft.com` | 2. `*.events.data.microsoft.com`
| 3. `https://login.microsoftonline.com` | 3. `https://login.microsoftonline.com`
| 4. `https://gcs.office.com/` | 4. `https://gcsgcc.office.com/`
| 5. `https://graph.microsoft.com/` | 5. `https://graph.microsoft.com/`

>[!NOTE]
>不支援 Proxy 驗證。 如果您的環境有需要驗證的 Proxy，建議您允許連接器代理程式略過 Proxy。

## <a name="create-and-configure-an-app-for-the-agent"></a>建立和設定代理程式的應用程式  

首先，登入並注意帳戶的最低必要許可權是搜尋系統管理員。 然後，代理程式會要求您提供驗證詳細資料。 使用下列步驟來建立應用程式，並產生必要的驗證詳細資料。

### <a name="create-an-app"></a>建立應用程式

1. 移至[Azure 入口網站](https://portal.azure.com)，並使用租使用者的系統管理員認證登入。

2. 從流覽窗格流覽至 **[Azure Active Directory**  ->  **應用程式註冊**]，然後選取 [**新增註冊]**。

3. 提供應用程式的名稱，然後選取 [ **註冊]**。

4. 記下應用程式 (用戶端) 識別碼。

5. 從流覽窗格開啟 **API** 許可權，然後選取 [ **新增許可權]**。

6. 依序選取 **[Microsoft Graph** ] 和 [ **應用程式許可權]**。

7. 搜尋下列許可權，然後選取 **[新增許可權]**。

   | **Permission** | **當 是所需的許可權時** |
   | ------------- | -------------|
   | [ExternalItem.ReadWrite.OwnedBy](/graph/permissions-reference#application-permissions-52) | 需要一直連線 |
   | [Directory.Read.All](/graph/permissions-reference#application-permissions-23) | 檔案共用、MS SQL 和 Oracle SQL 連接器的必要專案 |

8. 選 **取 [TenantName] 的 [授與系統管理員同意]** ，然後選取 [ **是]** 來確認。

9. 檢查許可權是否處於「已授與」狀態。

    :::image type="content" alt-text="右側資料行以綠色表示授與的許可權。" source="media/onprem-agent/granted-state.png" lightbox="media/onprem-agent/granted-state.png":::

### <a name="configure-authentication"></a>設定驗證

您可以使用用戶端密碼或憑證來提供驗證詳細資料。 請遵循您選擇的步驟。

#### <a name="configuring-the-client-secret-for-authentication"></a>設定用戶端密碼以進行驗證

1. 移至[Azure 入口網站](https://portal.azure.com)，並使用租使用者的系統管理員認證登入。

2. 從流覽窗格開啟 **[應用程式註冊** ]，然後移至適當的應用程式。 在 [ **管理] 底** 下，選 **取 [憑證和秘密]**。

3. 選 **取 [新增用戶端密碼** ]，然後選取秘密的到期期間。 複製產生的秘密並儲存它，因為它不會再顯示。

4. 使用此用戶端密碼和應用程式識別碼來設定代理程式。 接受英數位元。 您無法在代理程式的 [ **名稱** ] 欄位中使用空白。

#### <a name="using-a-certificate-for-authentication"></a>使用憑證進行驗證

使用憑證式驗證有三個簡單的步驟：

1. 建立或取得憑證
2. 將憑證上傳至Azure 入口網站
3. 將憑證指派給代理程式

##### <a name="step-1-get-a-certificate"></a>步驟 1：取得憑證

您可以使用下列腳本來產生自我簽署憑證。 您的組織可能不允許自我簽署憑證。 在此情況下，請使用此資訊來瞭解需求，並根據組織的原則取得憑證。

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

##### <a name="step-2-upload-the-certificate-to-the-azure-portal"></a>步驟 2：將憑證上傳至Azure 入口網站

1. 開啟應用程式，然後從左窗格流覽至 [憑證和秘密] 區段。

2. 選 **取 [上傳憑證** ] 並上傳 .cer 檔案。

3. 開 **啟 [應用程式註冊** ]，然後從流覽窗格中選取 [ **憑證和秘密** ]。 複製憑證指紋。

:::image type="content" alt-text="在左窗格中選取憑證和秘密時的指紋憑證清單。" source="media/onprem-agent/certificates.png" lightbox="media/onprem-agent/certificates.png":::

##### <a name="step-3-assign-the-certificate-to-the-agent"></a>步驟 3：將憑證指派給代理程式

使用範例腳本來產生憑證，會將 PFX 檔案儲存在腳本中識別的位置。

1. 將憑證 pfx 檔案下載到代理程式電腦。

2. 按兩下 pfx 檔案以啟動憑證安裝對話方塊。

3. 安裝憑證時，選取 [ **本機電腦** ] 作為存放區位置。

4. 安裝憑證之後，請透過 [**開始**] 功能表開啟 **[管理電腦憑證**]。

5. 選取 [**個人**  >  憑證] 底下新安裝 **的憑證**。

6. 選取並按住 (，或以滑鼠右鍵按一下憑證上的 [) ]，然後選取 [**所有工作**  >  **管理私密金鑰** 選項]。

7. 在 [許可權] 對話方塊中，選取 [新增選項]。 它會彈出新的視窗。 選取其中的 [位置] 選項。 選取代理程式安裝在所顯示位置中的電腦，然後選取 [ **確定]**。

8. 在使用者選取對話方塊中，寫入： **NT Service\GcaHostService** ，然後選取 **[確定]**。 請勿選取 [ **檢查名稱]** 按鈕。

9. 在 [許可權] 對話方塊中選取 [確定]。 代理程式電腦現在已設定為代理程式使用憑證產生權杖。

## <a name="troubleshooting"></a>疑難排解

### <a name="installation-failure"></a>安裝失敗

如果安裝失敗，請執行下列命令來檢查安裝記錄：msiexec /i「< msi >\GcaInstaller.msi 的路徑」 /L*V「<目的地路徑 >\install.log」。 如果無法解決錯誤，請透過記錄檔的 MicrosoftGraphConnectorsFeedback@service.microsoft.com 傳送電子郵件給支援人員。

### <a name="registration-failure"></a>註冊失敗

如果登入以設定應用程式失敗，並顯示錯誤：「登入失敗，請選取登入按鈕再試一次」，即使在瀏覽器驗證成功之後，仍開啟 services.msc 並檢查 GcaHostService 是否正在執行。 如果未啟動，請手動啟動。

當服務無法啟動，並出現「服務因為登入失敗而無法啟動」錯誤時，請檢查虛擬帳戶 「NT Service\GcaHostService」 是否有許可權以服務身分登入電腦。 請檢查 [此連結](/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) 以取得指示。 如果 [本機原則\使用者權限指派] 中新增使用者或群組的選項呈現灰色，表示嘗試新增此帳戶的使用者在此電腦上沒有系統管理員許可權，或是有群組原則覆寫它。 必須更新群組原則，才能讓主機服務以服務身分登入。

### <a name="connection-failure"></a>連線失敗

如果 「測試連線」動作在建立連線時失敗，並顯示錯誤：「請檢查使用者名稱/密碼和資料來源路徑」，即使提供的使用者名稱和密碼正確，也請確定使用者帳戶具有連接器代理程式安裝所在電腦的互動式登入許可權。 您可以檢閱登 [入原則管理](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally#policy-management) 的相關檔，以檢查登入許可權。 此外，請確定資料來源和代理程式電腦位於相同的網路上。

如果在建立連線時出現下列失敗訊息：「1011：Graph 連接器代理程式無法連線或離線」，請登入安裝代理程式的電腦，並檢查其是否正在執行。 如果代理程式未執行，請啟動代理程式應用程式。 如果連線持續失敗，請確認在註冊期間提供給代理程式的憑證或用戶端密碼尚未過期，且具有必要的許可權。
