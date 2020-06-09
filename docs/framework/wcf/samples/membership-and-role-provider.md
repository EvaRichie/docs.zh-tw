---
title: 成員資格和角色提供者
ms.date: 03/30/2017
ms.assetid: 0d11a31c-e75f-4fcf-9cf4-b7f26e056bcd
ms.openlocfilehash: e77e353fba194cb25b466387cf9def6773635e00
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591757"
---
# <a name="membership-and-role-provider"></a><span data-ttu-id="51e98-102">成員資格和角色提供者</span><span class="sxs-lookup"><span data-stu-id="51e98-102">Membership and Role Provider</span></span>
<span data-ttu-id="51e98-103">成員資格和角色提供者範例會示範服務如何使用 ASP.NET 成員資格和角色提供者來驗證及授權用戶端。</span><span class="sxs-lookup"><span data-stu-id="51e98-103">The Membership and Role Provider sample demonstrates how a service can use the ASP.NET membership and role providers to authenticate and authorize clients.</span></span>  
  
 <span data-ttu-id="51e98-104">在這個範例中，用戶端是主控台應用程式 (.exe)，而服務則是由網際網路資訊服務 (IIS) 所裝載。</span><span class="sxs-lookup"><span data-stu-id="51e98-104">In this sample, the client is a console application (.exe) and the service is hosted by Internet Information Services (IIS).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="51e98-105">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="51e98-105">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="51e98-106">此範例會示範：</span><span class="sxs-lookup"><span data-stu-id="51e98-106">The sample demonstrates how:</span></span>  
  
- <span data-ttu-id="51e98-107">用戶端可以使用使用者名稱-密碼組合進行驗證。</span><span class="sxs-lookup"><span data-stu-id="51e98-107">A client can authenticate by using the username-password combination.</span></span>  
  
- <span data-ttu-id="51e98-108">伺服器可以針對 ASP.NET 成員資格提供者驗證用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="51e98-108">The server can validate the client credentials against the ASP.NET membership provider.</span></span>  
  
- <span data-ttu-id="51e98-109">您可以使用伺服器的 X.509 憑證來驗證伺服器。</span><span class="sxs-lookup"><span data-stu-id="51e98-109">The server can be authenticated by using the server's X.509 certificate.</span></span>  
  
- <span data-ttu-id="51e98-110">伺服器可以使用 ASP.NET 角色提供者，將已驗證的用戶端對應至角色。</span><span class="sxs-lookup"><span data-stu-id="51e98-110">The server can map the authenticated client to a role by using the ASP.NET role provider.</span></span>  
  
- <span data-ttu-id="51e98-111">伺服器可以使用 `PrincipalPermissionAttribute` 來控制對服務所公開特定方法的存取。</span><span class="sxs-lookup"><span data-stu-id="51e98-111">The server can use the `PrincipalPermissionAttribute` to control access to certain methods that are exposed by the service.</span></span>  
  
 <span data-ttu-id="51e98-112">成員資格和角色提供者會設定為使用 SQL Server 所支援的存放區。</span><span class="sxs-lookup"><span data-stu-id="51e98-112">The membership and role providers are configured to use a store backed by SQL Server.</span></span> <span data-ttu-id="51e98-113">服務組態檔中會指定連接字串和各種選項。</span><span class="sxs-lookup"><span data-stu-id="51e98-113">A connection string and various options are specified in the service configuration file.</span></span> <span data-ttu-id="51e98-114">成員資料提供者的名稱會指定為 `SqlMembershipProvider`，而角色提供者的名稱會指定為 `SqlRoleProvider`。</span><span class="sxs-lookup"><span data-stu-id="51e98-114">The membership provider is given the name `SqlMembershipProvider` while the role provider is given the name `SqlRoleProvider`.</span></span>  
  
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
  
 <span data-ttu-id="51e98-115">服務會公開單一端點，以便與使用 Web.config 組態檔定義的服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="51e98-115">The service exposes a single endpoint for communicating with the service, which is defined by using the Web.config configuration file.</span></span> <span data-ttu-id="51e98-116">端點是由位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="51e98-116">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="51e98-117">繫結是以預設為使用 Windows 驗證的標準 `wsHttpBinding` 來設定。</span><span class="sxs-lookup"><span data-stu-id="51e98-117">The binding is configured with a standard `wsHttpBinding`, which defaults to using Windows authentication.</span></span> <span data-ttu-id="51e98-118">這個範例會將標準 `wsHttpBinding` 設定為使用使用者名稱驗證。</span><span class="sxs-lookup"><span data-stu-id="51e98-118">This sample sets the standard `wsHttpBinding` to use username authentication.</span></span> <span data-ttu-id="51e98-119">此行為會指定伺服器憑證要用於服務驗證。</span><span class="sxs-lookup"><span data-stu-id="51e98-119">The behavior specifies that the server certificate is to be used for service authentication.</span></span> <span data-ttu-id="51e98-120">伺服器憑證必須包含與 `SubjectName` `findValue` configuration 元素中的屬性相同的值 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 。</span><span class="sxs-lookup"><span data-stu-id="51e98-120">The server certificate must contain the same value for the `SubjectName` as the `findValue` attribute in the [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) configuration element.</span></span> <span data-ttu-id="51e98-121">此外，此行為會指定使用者名稱-密碼配對的驗證是由 ASP.NET 成員資格提供者執行，而角色對應是由 ASP.NET 角色提供者藉由指定針對兩個提供者所定義的名稱來執行。</span><span class="sxs-lookup"><span data-stu-id="51e98-121">In addition the behavior specifies that authentication of username-password pairs is performed by the ASP.NET membership provider and role mapping is performed by the ASP.NET role provider by specifying the names defined for the two providers.</span></span>  
  
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
  
 <span data-ttu-id="51e98-122">當您執行範例時，用戶端會在三個不同的使用者帳戶之下呼叫各種服務作業：Alice、Bob 和 Charlie。</span><span class="sxs-lookup"><span data-stu-id="51e98-122">When you run the sample, the client calls the various service operations under three different user accounts: Alice, Bob, and Charlie.</span></span> <span data-ttu-id="51e98-123">作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="51e98-123">The operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="51e98-124">所有四個以使用者 "Alice" 所進行的呼叫應該都會成功。</span><span class="sxs-lookup"><span data-stu-id="51e98-124">All four calls made as user "Alice" should succeed.</span></span> <span data-ttu-id="51e98-125">使用者 "Bob" 在嘗試呼叫 Divide 方法時，應該會收到拒絕存取錯誤。</span><span class="sxs-lookup"><span data-stu-id="51e98-125">User "Bob" should get an access denied error when trying to call the Divide method.</span></span> <span data-ttu-id="51e98-126">使用者 "Charlie" 在嘗試呼叫 Multiply 方法時，應該會收到拒絕存取錯誤。</span><span class="sxs-lookup"><span data-stu-id="51e98-126">User "Charlie" should get an access denied error when trying to call the Multiply method.</span></span> <span data-ttu-id="51e98-127">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="51e98-127">Press ENTER in the client window to shut down the client.</span></span>  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="51e98-128">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="51e98-128">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="51e98-129">若要建立方案的 c # 或 Visual Basic .NET 版本，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="51e98-129">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Running the Windows Communication Foundation Samples](running-the-samples.md).</span></span>  
  
2. <span data-ttu-id="51e98-130">請確定您已設定[ASP.NET 應用程式服務資料庫](https://go.microsoft.com/fwlink/?LinkId=94997)。</span><span class="sxs-lookup"><span data-stu-id="51e98-130">Ensure that you have configured the [ASP.NET Application Services Database](https://go.microsoft.com/fwlink/?LinkId=94997).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="51e98-131">如果您要執行 SQL Server Express Edition，則伺服器名稱為 .\SQLEXPRESS。</span><span class="sxs-lookup"><span data-stu-id="51e98-131">If you are running SQL Server Express Edition, your server name is .\SQLEXPRESS.</span></span> <span data-ttu-id="51e98-132">設定 ASP.NET 應用程式服務資料庫以及 Web.config 連接字串時，應該使用此伺服器。</span><span class="sxs-lookup"><span data-stu-id="51e98-132">This server should be used when configuring the ASP.NET Application Services Database as well as in the Web.config connection string.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="51e98-133">ASP.NET 背景工作進程帳戶必須擁有在此步驟中建立之資料庫的許可權。</span><span class="sxs-lookup"><span data-stu-id="51e98-133">The ASP.NET worker process account must have permissions on the database that is created in this step.</span></span> <span data-ttu-id="51e98-134">請使用 sqlcmd 公用程式或 SQL Server Management Studio 來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="51e98-134">Use the sqlcmd utility or SQL Server Management Studio to do this.</span></span>  
  
3. <span data-ttu-id="51e98-135">若要在單一或跨電腦的組態中執行本範例，請使用下列指示。</span><span class="sxs-lookup"><span data-stu-id="51e98-135">To run the sample in a single- or cross-computer configuration, use the following instructions.</span></span>  
  
### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="51e98-136">若要在同一部電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="51e98-136">To run the sample on the same computer</span></span>  
  
1. <span data-ttu-id="51e98-137">確認路徑中包含 Makecert.exe 所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="51e98-137">Make sure that the path includes the folder where Makecert.exe is located.</span></span>  
  
2. <span data-ttu-id="51e98-138">從開發人員命令提示字元中的範例安裝資料夾執行安裝程式 .bat，Visual Studio 以系統管理員許可權執行。</span><span class="sxs-lookup"><span data-stu-id="51e98-138">Run Setup.bat from the sample install folder in a Developer Command Prompt for Visual Studio run with administrator privileges.</span></span> <span data-ttu-id="51e98-139">這會安裝執行範例所需的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-139">This installs the service certificates required for running the sample.</span></span>  
  
3. <span data-ttu-id="51e98-140">從 \client\bin 啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="51e98-140">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="51e98-141">用戶端活動會顯示在用戶端主控台應用程式上。</span><span class="sxs-lookup"><span data-stu-id="51e98-141">Client activity is displayed on the client console application.</span></span>  
  
4. <span data-ttu-id="51e98-142">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="51e98-142">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="51e98-143">若要跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="51e98-143">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="51e98-144">在服務電腦上建立目錄。</span><span class="sxs-lookup"><span data-stu-id="51e98-144">Create a directory on the service computer.</span></span> <span data-ttu-id="51e98-145">使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。</span><span class="sxs-lookup"><span data-stu-id="51e98-145">Create a virtual application named servicemodelsamples for this directory by using the Internet Information Services (IIS) management tool.</span></span>  
  
2. <span data-ttu-id="51e98-146">將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。</span><span class="sxs-lookup"><span data-stu-id="51e98-146">Copy the service program files from \inetpub\wwwroot\servicemodelsamples to the virtual directory on the service computer.</span></span> <span data-ttu-id="51e98-147">確定複製 \bin 子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="51e98-147">Ensure that you copy the files in the \bin subdirectory.</span></span> <span data-ttu-id="51e98-148">同時將 Setup.bat、GetComputerName.vbs 和 Cleanup.bat 檔複製到服務電腦上。</span><span class="sxs-lookup"><span data-stu-id="51e98-148">Also copy the Setup.bat, GetComputerName.vbs, and Cleanup.bat files to the service computer.</span></span>  
  
3. <span data-ttu-id="51e98-149">在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。</span><span class="sxs-lookup"><span data-stu-id="51e98-149">Create a directory on the client computer for the client binaries.</span></span>  
  
4. <span data-ttu-id="51e98-150">將用戶端程式檔複製到用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="51e98-150">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="51e98-151">同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。</span><span class="sxs-lookup"><span data-stu-id="51e98-151">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>  
  
5. <span data-ttu-id="51e98-152">在伺服器上，以系統管理許可權開啟 Visual Studio 的開發人員命令提示字元，然後執行 `setup.bat service` 。</span><span class="sxs-lookup"><span data-stu-id="51e98-152">On the server, open a Developer Command Prompt for Visual Studio with administrative privileges and run `setup.bat service`.</span></span> <span data-ttu-id="51e98-153">`setup.bat`使用引數執行時，會 `service` 建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="51e98-153">Running `setup.bat` with the `service` argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
6. <span data-ttu-id="51e98-154">編輯 Web.config 以反映新的憑證名稱（在 `findValue` 的屬性中 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) ），這與電腦的完整功能變數名稱相同。</span><span class="sxs-lookup"><span data-stu-id="51e98-154">Edit Web.config to reflect the new certificate name (in the `findValue` attribute in the [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), which is the same as the fully-qualified domain name of the computer.</span></span>  
  
7. <span data-ttu-id="51e98-155">從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="51e98-155">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
8. <span data-ttu-id="51e98-156">在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。</span><span class="sxs-lookup"><span data-stu-id="51e98-156">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span>  
  
9. <span data-ttu-id="51e98-157">在用戶端上，以系統管理許可權開啟 Visual Studio 的開發人員命令提示字元，並執行 Importservicecert.bat。</span><span class="sxs-lookup"><span data-stu-id="51e98-157">On the client, open a Developer Command Prompt for Visual Studio with administrative privileges and run ImportServiceCert.bat.</span></span> <span data-ttu-id="51e98-158">這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="51e98-158">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
10. <span data-ttu-id="51e98-159">在用戶端電腦上，從命令提示字元啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="51e98-159">On the client computer, launch Client.exe from a command prompt.</span></span> <span data-ttu-id="51e98-160">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="51e98-160">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="51e98-161">若要在使用範例之後進行清除</span><span class="sxs-lookup"><span data-stu-id="51e98-161">To clean up after the sample</span></span>  
  
- <span data-ttu-id="51e98-162">當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。</span><span class="sxs-lookup"><span data-stu-id="51e98-162">Run Cleanup.bat in the samples folder after you have finished running the sample.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="51e98-163">跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-163">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="51e98-164">如果您已在電腦上執行使用憑證的 Windows Communication Foundation （WCF）範例，請務必清除已安裝在 CurrentUser-TrustedPeople 存放區中的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-164">If you have run Windows Communication Foundation (WCF) samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="51e98-165">若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="51e98-165">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>  
  
## <a name="the-setup-batch-file"></a><span data-ttu-id="51e98-166">設定批次檔</span><span class="sxs-lookup"><span data-stu-id="51e98-166">The Setup Batch File</span></span>  
 <span data-ttu-id="51e98-167">本範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要伺服器憑證安全性的自我裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="51e98-167">The Setup.bat batch file included with this sample allows you to configure the server with relevant certificates to run a self-hosted application that requires server certificate-based security.</span></span> <span data-ttu-id="51e98-168">這個批次檔必須經過修改才能跨電腦運作，或在非裝載的情況下運作。</span><span class="sxs-lookup"><span data-stu-id="51e98-168">This batch file must be modified to work across computers or to work in a non-hosted case.</span></span>  
  
 <span data-ttu-id="51e98-169">下面提供批次檔的各區段簡要概觀，讓將批次檔得以修改為在適當的組態下執行。</span><span class="sxs-lookup"><span data-stu-id="51e98-169">The following provides a brief overview of the different sections of the batch files so that they can be modified to run in the appropriate configuration.</span></span>  
  
- <span data-ttu-id="51e98-170">建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-170">Creating the server certificate.</span></span>  
  
     <span data-ttu-id="51e98-171">下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-171">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span> <span data-ttu-id="51e98-172">%SERVER_NAME% 變數會指定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="51e98-172">The %SERVER_NAME% variable specifies the server name.</span></span> <span data-ttu-id="51e98-173">您可以變更這個變數來指定自己的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="51e98-173">Change this variable to specify your own server name.</span></span> <span data-ttu-id="51e98-174">這個批次檔的預設為 localhost。</span><span class="sxs-lookup"><span data-stu-id="51e98-174">This batch file defaults it to localhost.</span></span>  
  
     <span data-ttu-id="51e98-175">憑證會儲存在 LocalMachine 存放區位置下的 My (Personal) 存放區中。</span><span class="sxs-lookup"><span data-stu-id="51e98-175">The certificate is stored in My (Personal) store under the LocalMachine store location.</span></span>  
  
    ```console
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
- <span data-ttu-id="51e98-176">將伺服器憑證安裝至用戶端的受信任憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="51e98-176">Installing the server certificate into the client's trusted certificate store.</span></span>  
  
     <span data-ttu-id="51e98-177">Setup.bat 批次檔中的下列程式行會將伺服器憑證複製到用戶端受信任人的存放區。</span><span class="sxs-lookup"><span data-stu-id="51e98-177">The following lines in the Setup.bat batch file copy the server certificate into the client trusted people store.</span></span> <span data-ttu-id="51e98-178">這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="51e98-178">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="51e98-179">如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。</span><span class="sxs-lookup"><span data-stu-id="51e98-179">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft-issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>  
  
    ```bat  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
