---
title: 訊息安全性匿名
ms.date: 03/30/2017
helpviewer_keywords:
- WS Security
ms.assetid: c321cbf9-8c05-4cce-b5a5-4bf7b230ee03
ms.openlocfilehash: 95101b8ec4f5a7fc60d0233ab6685b5c6851b44e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84584972"
---
# <a name="message-security-anonymous"></a><span data-ttu-id="99dd7-102">訊息安全性匿名</span><span class="sxs-lookup"><span data-stu-id="99dd7-102">Message Security Anonymous</span></span>
<span data-ttu-id="99dd7-103">訊息安全性匿名範例示範如何使用不具用戶端驗證的訊息層級安全性來執行 Windows Communication Foundation （WCF）應用程式，但這需要使用伺服器的 x.509 憑證來進行伺服器驗證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-103">The Message Security Anonymous sample demonstrates how to implement a Windows Communication Foundation (WCF) application that uses message-level security with no client authentication but that requires server authentication using the server's X.509 certificate.</span></span> <span data-ttu-id="99dd7-104">用戶端與伺服器之間的所有應用程式訊息都會經過簽署及加密。</span><span class="sxs-lookup"><span data-stu-id="99dd7-104">All application messages between the client and server are signed and encrypted.</span></span> <span data-ttu-id="99dd7-105">這個範例是以[WSHttpBinding](wshttpbinding.md)範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="99dd7-105">This sample is based on the [WSHttpBinding](wshttpbinding.md) sample.</span></span> <span data-ttu-id="99dd7-106">這個範例是由用戶端主控台程式 (.exe) 和網際網路資訊服務 (IIS) 所裝載的服務程式庫 (.dll) 所組成。</span><span class="sxs-lookup"><span data-stu-id="99dd7-106">This sample consists of a client console program (.exe) and a service library (.dll) hosted by Internet Information Services (IIS).</span></span> <span data-ttu-id="99dd7-107">服務會實作定義要求-回覆通訊模式的合約。</span><span class="sxs-lookup"><span data-stu-id="99dd7-107">The service implements a contract that defines a request-reply communication pattern.</span></span>

> [!NOTE]
> <span data-ttu-id="99dd7-108">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="99dd7-108">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

 <span data-ttu-id="99dd7-109">這個範例會將新作業新增至計算機介面，該介面會在用戶端未通過驗證時傳回 `True`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-109">This sample adds a new operation to the calculator interface that returns `True` if the client was not authenticated.</span></span>

```csharp
public class CalculatorService : ICalculator
{
    public bool IsCallerAnonymous()
    {
        // ServiceSecurityContext.IsAnonymous returns true if the caller is not authenticated.
        return ServiceSecurityContext.Current.IsAnonymous;
    }
    ...
}
```

 <span data-ttu-id="99dd7-110">此服務會公開 (Expose) 單一的端點來與已使用組態檔 Web.config 定義之服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="99dd7-110">The service exposes a single endpoint for communicating with the service, defined using a configuration file (Web.config).</span></span> <span data-ttu-id="99dd7-111">端點是由位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="99dd7-111">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="99dd7-112">此繫結是使用指定的 `wsHttpBinding` 繫結所設定的。</span><span class="sxs-lookup"><span data-stu-id="99dd7-112">The binding is configured with a `wsHttpBinding` binding.</span></span> <span data-ttu-id="99dd7-113">`wsHttpBinding` 繫結的預設安全性模式為 `Message`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-113">The default security mode for the `wsHttpBinding` binding is `Message`.</span></span> <span data-ttu-id="99dd7-114">`clientCredentialType` 屬性會設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-114">The `clientCredentialType` attribute is set to `None`.</span></span>

```xml
<system.serviceModel>

  <protocolMapping>
    <add scheme="http" binding="wsHttpBinding" />
  </protocolMapping>

  <bindings>
    <wsHttpBinding>
     <!-- This configuration defines the security mode as Message and -->
     <!-- the clientCredentialType as None. This mode provides -->
     <!-- server authentication only using the service certificate. -->

     <binding>
       <security mode="Message">
         <message clientCredentialType="None" />
       </security>
     </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 <span data-ttu-id="99dd7-115">要用於服務驗證的認證會在中指定 [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 。</span><span class="sxs-lookup"><span data-stu-id="99dd7-115">The credentials to be used for service authentication are specified in the [\<behavior>](../../configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md).</span></span> <span data-ttu-id="99dd7-116">伺服器憑證中包含的 `SubjectName` 值必須與 `findValue` 屬性的指定值相同，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="99dd7-116">The server certificate must contain the same value for the `SubjectName` as the value specified for the `findValue` attribute as shown in the following sample code.</span></span>

```xml
<behaviors>
  <serviceBehaviors>
    <behavior>
      <!--
    The serviceCredentials behavior allows you to define a service certificate.
    A service certificate is used by a client to authenticate the service and provide message protection.
    This configuration references the "localhost" certificate installed during the setup instructions.
    -->
      <serviceCredentials>
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
      </serviceCredentials>
      <serviceMetadata httpGetEnabled="True"/>
      <serviceDebug includeExceptionDetailInFaults="False" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```

 <span data-ttu-id="99dd7-117">用戶端端點組態是由服務端點的絕對位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="99dd7-117">The client endpoint configuration consists of an absolute address for the service endpoint, the binding, and the contract.</span></span> <span data-ttu-id="99dd7-118">`wsHttpBinding` 繫結的用戶端安全性模式為 `Message`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-118">The client security mode for the `wsHttpBinding` binding is `Message`.</span></span> <span data-ttu-id="99dd7-119">`clientCredentialType` 屬性會設定為 `None`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-119">The `clientCredentialType` attribute is set to `None`.</span></span>

```xml
<system.serviceModel>
  <client>
    <endpoint name=""
             address="http://localhost/servicemodelsamples/service.svc"
             binding="wsHttpBinding"
             behaviorConfiguration="ClientCredentialsBehavior"
             bindingConfiguration="Binding1"
             contract="Microsoft.ServiceModel.Samples.ICalculator" />
  </client>

  <bindings>
    <wsHttpBinding>
      <!--This configuration defines the security mode as -->
      <!--Message and the clientCredentialType as None. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="None"/>
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>
  ...
</system.serviceModel>
```

 <span data-ttu-id="99dd7-120">此範例會將 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 設定為 <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust> 以驗證服務的憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-120">The sample sets the <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> to <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust> for authenticating the service's certificate.</span></span> <span data-ttu-id="99dd7-121">此項作業會在用戶端 App.config 檔的 `behaviors` 區段中完成。</span><span class="sxs-lookup"><span data-stu-id="99dd7-121">This is done in the client's App.config file in the `behaviors` section.</span></span> <span data-ttu-id="99dd7-122">這表示如果憑證位在使用者之受信任人的存放區，則此憑證就受到信任，而不會執行驗證憑證的簽發者鏈結。</span><span class="sxs-lookup"><span data-stu-id="99dd7-122">This means that if the certificate is in the user's Trusted People store, then it is trusted without performing a validation of the certificate's issuer chain.</span></span> <span data-ttu-id="99dd7-123">範例中是基於方便而使用這項設定，這樣便能夠在不需要憑證授權單位 (CA) 發出之憑證的情況下執行此範例。</span><span class="sxs-lookup"><span data-stu-id="99dd7-123">This setting is used here for convenience so that the sample can be run without requiring certificates issued by a certification authority (CA).</span></span> <span data-ttu-id="99dd7-124">這個設定的安全性比預設值 (ChainTrust) 低。</span><span class="sxs-lookup"><span data-stu-id="99dd7-124">This setting is less secure than the default, ChainTrust.</span></span> <span data-ttu-id="99dd7-125">在實際執行程式碼 (Production Code) 中使用 `PeerOrChainTrust` 之前，應該要謹慎考量這項設定。</span><span class="sxs-lookup"><span data-stu-id="99dd7-125">The security implications of this setting should be carefully considered before using `PeerOrChainTrust` in production code.</span></span>

 <span data-ttu-id="99dd7-126">用戶端執行會將呼叫新增至 `IsCallerAnonymous` 方法，否則不會與[WSHttpBinding](wshttpbinding.md)範例不同。</span><span class="sxs-lookup"><span data-stu-id="99dd7-126">The client implementation adds a call to the `IsCallerAnonymous` method and otherwise does not differ from the [WSHttpBinding](wshttpbinding.md) sample.</span></span>

```csharp
// Create a client with a client endpoint configuration.
CalculatorClient client = new CalculatorClient();

// Call the GetCallerIdentity operation.
Console.WriteLine("IsCallerAnonymous returned: {0}", client.IsCallerAnonymous());

// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = client.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);

...

//Closing the client gracefully closes the connection and cleans up resources.
client.Close();

Console.WriteLine();
Console.WriteLine("Press <ENTER> to terminate client.");
Console.ReadLine();
```

 <span data-ttu-id="99dd7-127">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-127">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="99dd7-128">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="99dd7-128">Press ENTER in the client window to shut down the client.</span></span>

```console
IsCallerAnonymous returned: True
Add(100,15.99) = 115.99
Subtract(145,76.54) = 68.46
Multiply(9,81.25) = 731.25
Divide(22,7) = 3.14285714285714
Press <ENTER> to terminate client.
```

 <span data-ttu-id="99dd7-129">訊息安全性匿名範例所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要憑證安全性的裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="99dd7-129">The Setup.bat batch file included with the Message Security Anonymous sample enables you to configure the server with a relevant certificate to run a hosted application that requires certificate-based security.</span></span> <span data-ttu-id="99dd7-130">此批次檔可以在兩種模式中執行。</span><span class="sxs-lookup"><span data-stu-id="99dd7-130">The batch file can be run in two modes.</span></span> <span data-ttu-id="99dd7-131">若要在單一電腦模式中執行此批次檔，請在命令列中輸入 `setup.bat`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-131">To run the batch file in the single-computer mode, type `setup.bat` at the command line.</span></span> <span data-ttu-id="99dd7-132">若要在服務模式中執行此批次檔，請輸入 `setup.bat service`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-132">To run it in service mode, type `setup.bat service`.</span></span> <span data-ttu-id="99dd7-133">請在跨電腦執行範例時使用這個模式。</span><span class="sxs-lookup"><span data-stu-id="99dd7-133">Use this mode when running the sample across computers.</span></span> <span data-ttu-id="99dd7-134">如需詳細資訊，請參閱本主題結尾的安裝程序。</span><span class="sxs-lookup"><span data-stu-id="99dd7-134">See the setup procedure at the end of this topic for details.</span></span>

 <span data-ttu-id="99dd7-135">下面會提供批次檔之不同區段的簡短概觀。</span><span class="sxs-lookup"><span data-stu-id="99dd7-135">The following provides a brief overview of the different sections of the batch files:</span></span>

- <span data-ttu-id="99dd7-136">建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-136">Creating the server certificate.</span></span>

     <span data-ttu-id="99dd7-137">下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-137">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span>

    ```bat
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

     <span data-ttu-id="99dd7-138">%SERVER_NAME% 變數會指定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="99dd7-138">The %SERVER_NAME% variable specifies the server name.</span></span> <span data-ttu-id="99dd7-139">憑證是儲存在 LocalMachine 存放區中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-139">The certificate is stored in the LocalMachine store.</span></span> <span data-ttu-id="99dd7-140">如果使用 service 引數執行安裝批次檔 (例如 `setup.bat service`)，%SERVER_NAME% 就會包含電腦的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="99dd7-140">If the setup batch file is run with an argument of service (such as `setup.bat service`) the %SERVER_NAME% contains the fully-qualified domain name of the computer.</span></span> <span data-ttu-id="99dd7-141">否則，預設為 localhost。</span><span class="sxs-lookup"><span data-stu-id="99dd7-141">Otherwise it defaults to localhost.</span></span>

- <span data-ttu-id="99dd7-142">將伺服器憑證安裝至用戶端的受信任憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-142">Installing the server certificate into the client's trusted certificate store.</span></span>

     <span data-ttu-id="99dd7-143">下列程式行會將伺服器憑證複製到用戶端受信任人的存放區中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-143">The following line copies the server certificate into the client trusted people store.</span></span> <span data-ttu-id="99dd7-144">這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-144">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="99dd7-145">如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。</span><span class="sxs-lookup"><span data-stu-id="99dd7-145">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft-issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>

    ```console
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- <span data-ttu-id="99dd7-146">授與憑證私密金鑰的權限。</span><span class="sxs-lookup"><span data-stu-id="99dd7-146">Granting permissions on the certificate's private key.</span></span>

     <span data-ttu-id="99dd7-147">安裝程式 .bat 批次檔中的下列幾行，可讓 ASP.NET worker 進程帳戶存取儲存在 LocalMachine 存放區的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-147">The following lines in the Setup.bat batch file make the server certificate stored in the LocalMachine store accessible to the ASP.NET worker process account.</span></span>

    ```bat
    echo ************
    echo setting privileges on server certificates
    echo ************
    for /F "delims=" %%i in ('"%MSSDK%\bin\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE
    (ver | findstr "5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R
    iisreset
    ```

> [!NOTE]
> <span data-ttu-id="99dd7-148">如果您使用非英文版的 Windows，則必須編輯安裝 .bat 檔案，並將 `NT AUTHORITY\NETWORK SERVICE` 帳戶名稱取代為您的對等區域。</span><span class="sxs-lookup"><span data-stu-id="99dd7-148">If you are using a non-U.S. English edition of Windows you must edit the Setup.bat file and replace the `NT AUTHORITY\NETWORK SERVICE` account name with your regional equivalent.</span></span>

### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="99dd7-149">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="99dd7-149">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="99dd7-150">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="99dd7-150">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="99dd7-151">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="99dd7-151">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="99dd7-152">若要在同一部電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="99dd7-152">To run the sample on the same computer</span></span>

1. <span data-ttu-id="99dd7-153">確認路徑中包含 Makecert.exe 和 FindPrivateKey.exe 所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="99dd7-153">Ensure that the path includes the folder where Makecert.exe and FindPrivateKey.exe are located.</span></span>

2. <span data-ttu-id="99dd7-154">從開發人員命令提示字元中的範例安裝資料夾執行安裝程式 .bat，Visual Studio 以系統管理員許可權執行。</span><span class="sxs-lookup"><span data-stu-id="99dd7-154">Run Setup.bat from the sample install folder in a Developer Command Prompt for Visual Studio run with administrator privileges.</span></span> <span data-ttu-id="99dd7-155">這會安裝執行範例所需的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-155">This installs all the certificates required for running the sample.</span></span>

    > [!NOTE]
    > <span data-ttu-id="99dd7-156">安裝批次檔是設計用來從 Visual Studio 的開發人員命令提示字元執行。</span><span class="sxs-lookup"><span data-stu-id="99dd7-156">The setup batch file is designed to be run from a  Developer Command Prompt for Visual Studio.</span></span> <span data-ttu-id="99dd7-157">它要求 path 環境變數指向安裝 SDK 的目錄。</span><span class="sxs-lookup"><span data-stu-id="99dd7-157">It requires that the path environment variable point to the directory where the SDK is installed.</span></span> <span data-ttu-id="99dd7-158">此環境變數會在 Visual Studio 的開發人員命令提示字元中自動設定。</span><span class="sxs-lookup"><span data-stu-id="99dd7-158">This environment variable is automatically set within a Developer Command Prompt for Visual Studio.</span></span>  
  
3. <span data-ttu-id="99dd7-159">輸入位址以驗證使用瀏覽器存取服務 `http://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="99dd7-159">Verify access to the service using a browser by entering the address `http://localhost/servicemodelsamples/service.svc`.</span></span>  
  
4. <span data-ttu-id="99dd7-160">從 \client\bin 啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="99dd7-160">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="99dd7-161">用戶端活動會顯示在用戶端主控台應用程式上。</span><span class="sxs-lookup"><span data-stu-id="99dd7-161">Client activity is displayed on the client console application.</span></span>  
  
5. <span data-ttu-id="99dd7-162">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="99dd7-162">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="99dd7-163">若要跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="99dd7-163">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="99dd7-164">在服務電腦上建立目錄。</span><span class="sxs-lookup"><span data-stu-id="99dd7-164">Create a directory on the service computer.</span></span> <span data-ttu-id="99dd7-165">使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。</span><span class="sxs-lookup"><span data-stu-id="99dd7-165">Create a virtual application named servicemodelsamples for this directory by using the Internet Information Services (IIS) management tool.</span></span>  
  
2. <span data-ttu-id="99dd7-166">將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-166">Copy the service program files from \inetpub\wwwroot\servicemodelsamples to the virtual directory on the service computer.</span></span> <span data-ttu-id="99dd7-167">確定複製 \bin 子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="99dd7-167">Ensure that you copy the files in the \bin subdirectory.</span></span> <span data-ttu-id="99dd7-168">同時，將 Setup.bat 和 Cleanup.bat 檔案複製到服務電腦中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-168">Also copy the Setup.bat and Cleanup.bat files to the service computer.</span></span>  
  
3. <span data-ttu-id="99dd7-169">在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。</span><span class="sxs-lookup"><span data-stu-id="99dd7-169">Create a directory on the client computer for the client binaries.</span></span>  
  
4. <span data-ttu-id="99dd7-170">將用戶端程式檔複製到用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="99dd7-170">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="99dd7-171">同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。</span><span class="sxs-lookup"><span data-stu-id="99dd7-171">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>  
  
5. <span data-ttu-id="99dd7-172">在伺服器上，于 `setup.bat service` 使用系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元中執行。</span><span class="sxs-lookup"><span data-stu-id="99dd7-172">On the server, run `setup.bat service` in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="99dd7-173">`setup.bat`使用引數執行時，會 `service` 建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="99dd7-173">Running `setup.bat` with the `service` argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
6. <span data-ttu-id="99dd7-174">編輯 Web.config 以反映新的憑證名稱（在 `findValue` 的屬性中 [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) ），這與電腦的完整功能變數名稱相同。</span><span class="sxs-lookup"><span data-stu-id="99dd7-174">Edit Web.config to reflect the new certificate name (in the `findValue` attribute in the [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), which is the same as the fully-qualified domain name of the computer.</span></span>  
  
7. <span data-ttu-id="99dd7-175">從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="99dd7-175">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
8. <span data-ttu-id="99dd7-176">在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。</span><span class="sxs-lookup"><span data-stu-id="99dd7-176">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span>  
  
9. <span data-ttu-id="99dd7-177">在用戶端上，于 Visual Studio 以系統管理員許可權開啟的開發人員命令提示字元中執行 Importservicecert.bat。</span><span class="sxs-lookup"><span data-stu-id="99dd7-177">On the client, run ImportServiceCert.bat in a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="99dd7-178">這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="99dd7-178">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
10. <span data-ttu-id="99dd7-179">在用戶端電腦上，從命令提示字元啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="99dd7-179">On the client computer, launch Client.exe from a command prompt.</span></span> <span data-ttu-id="99dd7-180">如果用戶端和服務無法通訊，請參閱[WCF 範例的疑難排解秘訣](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="99dd7-180">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="99dd7-181">若要在使用範例之後進行清除</span><span class="sxs-lookup"><span data-stu-id="99dd7-181">To clean up after the sample</span></span>  
  
- <span data-ttu-id="99dd7-182">當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。</span><span class="sxs-lookup"><span data-stu-id="99dd7-182">Run Cleanup.bat in the samples folder after you have finished running the sample.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="99dd7-183">跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-183">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="99dd7-184">如果您已在電腦上執行使用憑證的 Windows Communication Foundation （WCF）範例，請務必清除已安裝在 CurrentUser-TrustedPeople 存放區中的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="99dd7-184">If you have run Windows Communication Foundation (WCF) samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="99dd7-185">若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`。</span><span class="sxs-lookup"><span data-stu-id="99dd7-185">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`</span></span>
