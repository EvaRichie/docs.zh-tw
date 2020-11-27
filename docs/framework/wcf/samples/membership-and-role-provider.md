---
title: 成員資格和角色提供者
ms.date: 03/30/2017
ms.assetid: 0d11a31c-e75f-4fcf-9cf4-b7f26e056bcd
ms.openlocfilehash: fa2a813c2dc1a891119e922c86f045e7f2df7125
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264708"
---
# <a name="membership-and-role-provider"></a>成員資格和角色提供者

成員資格和角色提供者範例會示範服務如何使用 ASP.NET 成員資格和角色提供者來驗證及授權用戶端。  
  
 在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 此範例會示範：  
  
- 用戶端可以使用使用者名稱-密碼組合進行驗證。  
  
- 伺服器可以針對 ASP.NET 成員資格提供者驗證用戶端認證。  
  
- 您可以使用伺服器的 X.509 憑證來驗證伺服器。  
  
- 伺服器可以使用 ASP.NET 角色提供者，將已驗證的用戶端對應至角色。  
  
- 伺服器可以使用 `PrincipalPermissionAttribute` 來控制對服務所公開特定方法的存取。  
  
 成員資格和角色提供者會設定為使用 SQL Server 所支援的存放區。 服務組態檔中會指定連接字串和各種選項。 成員資料提供者的名稱會指定為 `SqlMembershipProvider`，而角色提供者的名稱會指定為 `SqlRoleProvider`。  
  
```xml  
<!-- Set the connection string for SQL Server -->  
<connectionStrings>  
  <add name="SqlConn"
       connectionString="Data Source=localhost;Integrated Security=SSPI;Initial Catalog=aspnetdb;" />  
</connectionStrings>  
  
<system.web>  
  <!-- Configure the Sql Membership Provider -->  
  <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">  
    <providers>  
      <clear />  
      <add
        name="SqlMembershipProvider"
        type="System.Web.Security.SqlMembershipProvider"
        connectionStringName="SqlConn"  
        applicationName="MembershipAndRoleProviderSample"  
        enablePasswordRetrieval="false"  
        enablePasswordReset="false"  
        requiresQuestionAndAnswer="false"  
        requiresUniqueEmail="true"  
        passwordFormat="Hashed" />  
    </providers>  
  </membership>  
  
  <!-- Configure the Sql Role Provider -->  
  <roleManager enabled ="true"
               defaultProvider ="SqlRoleProvider" >  
    <providers>  
      <add name ="SqlRoleProvider"
           type="System.Web.Security.SqlRoleProvider"
           connectionStringName="SqlConn"
           applicationName="MembershipAndRoleProviderSample"/>  
    </providers>  
  </roleManager>  
</system.web>  
```  
  
 服務會公開單一端點，以便與使用 Web.config 組態檔定義的服務進行通訊。 端點是由位址、繫結及合約所組成。 繫結是以預設為使用 Windows 驗證的標準 `wsHttpBinding` 來設定。 這個範例會將標準 `wsHttpBinding` 設定為使用使用者名稱驗證。 此行為會指定伺服器憑證要用於服務驗證。 伺服器憑證必須包含與 `SubjectName` `findValue` configuration 元素中屬性相同的值 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 。 此外，此行為會指定 ASP.NET 成員資格提供者執行使用者名稱-密碼組的驗證，並藉由指定為兩個提供者定義的名稱，由 ASP.NET 角色提供者執行角色對應。  
  
```xml  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- Set up a binding that uses Username as the client credential type -->  
      <binding>  
        <security mode ="Message">  
          <message clientCredentialType ="UserName"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior>  
        <!-- Configure role based authorization to use the Role Provider -->  
        <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                              roleProviderName ="SqlRoleProvider" />  
        <serviceCredentials>  
          <!-- Configure user name authentication to use the Membership Provider -->  
          <userNameAuthentication userNamePasswordValidationMode ="MembershipProvider"
                                  membershipProviderName ="SqlMembershipProvider"/>  
          <!-- Configure the service certificate -->  
          <serviceCertificate storeLocation ="LocalMachine"
                              storeName ="My"
                              x509FindType ="FindBySubjectName"  
                              findValue ="localhost" />  
        </serviceCredentials>  
        <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
        <serviceDebug includeExceptionDetailInFaults="false" />  
        <serviceMetadata httpGetEnabled="true"/>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 當您執行範例時，用戶端會在三個不同的使用者帳戶之下呼叫各種服務作業：Alice、Bob 和 Charlie。 作業要求和回應會顯示在用戶端主控台視窗中。 所有四個以使用者 "Alice" 所進行的呼叫應該都會成功。 使用者 "Bob" 在嘗試呼叫 Divide 方法時，應該會收到拒絕存取錯誤。 使用者 "Charlie" 在嘗試呼叫 Multiply 方法時，應該會收到拒絕存取錯誤。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 若要建立解決方案的 c # 或 Visual Basic .NET 版本，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
2. 確定您已設定 [ASP.NET 應用程式服務資料庫](https://go.microsoft.com/fwlink/?LinkId=94997)。  
  
    > [!NOTE]
    > 如果您要執行 SQL Server Express Edition，則伺服器名稱為 .\SQLEXPRESS。 設定 ASP.NET 應用程式服務資料庫時，以及 Web.config 連接字串中，都應該使用此伺服器。  
  
    > [!NOTE]
    > ASP.NET worker 進程帳戶必須具有在此步驟中建立之資料庫的許可權。 請使用 sqlcmd 公用程式或 SQL Server Management Studio 來執行這項操作。  
  
3. 若要在單一或跨電腦的組態中執行本範例，請使用下列指示。  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>若要在同一部電腦上執行範例  
  
1. 確認路徑中包含 Makecert.exe 所在的資料夾。  
  
2. 從開發人員命令提示字元中的範例安裝資料夾執行 Setup.bat，以 Visual Studio 以系統管理員許可權執行。 這會安裝執行範例所需的服務憑證。  
  
3. 從 \client\bin 啟動 Client.exe。 用戶端活動會顯示在用戶端主控台應用程式上。  
  
4. 如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-run-the-sample-across-computers"></a>若要跨電腦執行範例  
  
1. 在服務電腦上建立目錄。 使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。  
  
2. 將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。 確定複製 \bin 子目錄中的檔案。 同時將 Setup.bat、GetComputerName.vbs 和 Cleanup.bat 檔複製到服務電腦上。  
  
3. 在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。  
  
4. 將用戶端程式檔複製到用戶端電腦上的用戶端目錄。 同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。  
  
5. 在伺服器上，以系統管理許可權開啟 Visual Studio 的開發人員命令提示字元，然後執行 `setup.bat service` 。 `setup.bat`使用 `service` 引數執行時，會建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 service .cer 的檔案。  
  
6. 編輯 Web.config 以反映) 中的屬性 (新的憑證名稱，此名稱與 `findValue` [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 電腦的完整功能變數名稱相同。  
  
7. 從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。  
  
8. 在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。  
  
9. 在用戶端上，以系統管理許可權開啟 Visual Studio 的開發人員命令提示字元，然後執行 ImportServiceCert.bat。 這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。  
  
10. 在用戶端電腦上，從命令提示字元啟動 Client.exe。 如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>若要在使用範例之後進行清除  
  
- 當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。  
  
> [!NOTE]
> 跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。 如果您已執行 Windows Communication Foundation (使用跨電腦憑證的 WCF) 範例，請務必清除 TrustedPeople 存放區中已安裝的服務憑證。 若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## <a name="the-setup-batch-file"></a>設定批次檔  

 本範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要伺服器憑證安全性的自我裝載應用程式。 這個批次檔必須經過修改才能跨電腦運作，或在非裝載的情況下運作。  
  
 下面提供批次檔的各區段簡要概觀，讓將批次檔得以修改為在適當的組態下執行。  
  
- 建立伺服器憑證。  
  
     下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。 %SERVER_NAME% 變數會指定伺服器名稱。 您可以變更這個變數來指定自己的伺服器名稱。 這個批次檔的預設為 localhost。  
  
     憑證會儲存在 LocalMachine 存放區位置下的 My (Personal) 存放區中。  
  
    ```console
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
- 將伺服器憑證安裝至用戶端的受信任憑證存放區中。  
  
     Setup.bat 批次檔中的下列程式行會將伺服器憑證複製到用戶端受信任人的存放區。 這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。 如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。  
  
    ```bat  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```
