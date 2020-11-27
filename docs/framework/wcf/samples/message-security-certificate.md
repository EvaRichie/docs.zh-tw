---
title: 訊息安全性憑證
ms.date: 03/30/2017
helpviewer_keywords:
- WS Security
ms.assetid: 909333b3-35ec-48f0-baff-9a50161896f6
ms.openlocfilehash: 164a939fa7ee0112e1ceae24755854b09dc72603
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283987"
---
# <a name="message-security-certificate"></a><span data-ttu-id="c5c01-102">訊息安全性憑證</span><span class="sxs-lookup"><span data-stu-id="c5c01-102">Message Security Certificate</span></span>

<span data-ttu-id="c5c01-103">這個範例會示範如何實作應用程式，該應用程式會對用戶端使用搭配 X.509 v3 憑證驗證的 WS-Security，並要求使用伺服器之 X.509 v3 憑證進行驗證的伺服器。</span><span class="sxs-lookup"><span data-stu-id="c5c01-103">This sample demonstrates how to implement an application that uses WS-Security with X.509 v3 certificate authentication for the client and requires server authentication using the server's X.509 v3 certificate.</span></span> <span data-ttu-id="c5c01-104">這個範例會使用預設的設定值，使所有在用戶端與伺服器之間的應用程式訊息進行簽署與加密。</span><span class="sxs-lookup"><span data-stu-id="c5c01-104">This sample uses default settings such that all application messages between the client and server are signed and encrypted.</span></span> <span data-ttu-id="c5c01-105">此範例是以 [WSHttpBinding](wshttpbinding.md) 為基礎，而且是由用戶端主控台程式和 INTERNET INFORMATION SERVICES (IIS) 所裝載的服務程式庫所組成。</span><span class="sxs-lookup"><span data-stu-id="c5c01-105">This sample is based on the [WSHttpBinding](wshttpbinding.md) and consists of a client console program and a service library hosted by Internet Information Services (IIS).</span></span> <span data-ttu-id="c5c01-106">服務會實作定義要求-回覆通訊模式的合約。</span><span class="sxs-lookup"><span data-stu-id="c5c01-106">The service implements a contract that defines a request-reply communication pattern.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c5c01-107">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="c5c01-107">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="c5c01-108">這個範例示範如何使用組態控制驗證以及如何從安全性內容取得呼叫者身分識別，如下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="c5c01-108">The sample demonstrates controlling authentication by using configuration and how to obtain the caller’s identity from the security context, as shown in the following sample code.</span></span>  

```csharp
public class CalculatorService : ICalculator  
{  
    public string GetCallerIdentity()  
    {  
        // The client certificate is not mapped to a Windows identity by default.  
        // ServiceSecurityContext.PrimaryIdentity is populated based on the information  
        // in the certificate that the client used to authenticate itself to the service.  
        return ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    }  
    ...  
}  
```  
  
 <span data-ttu-id="c5c01-109">服務會公開一個與服務進行通訊的端點，以及一個使用組態檔 (Web.config) 定義並透過 WS-MetadataExchange 通訊協定公開服務之 WSDL 文件的端點。</span><span class="sxs-lookup"><span data-stu-id="c5c01-109">The service exposes one endpoint for communicating with the service and one endpoint for exposing the service's WSDL document using the WS-MetadataExchange protocol, defined by using the configuration file (Web.config).</span></span> <span data-ttu-id="c5c01-110">端點是由位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="c5c01-110">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="c5c01-111">系結是以標準元素設定 [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) ，預設為使用訊息安全性。</span><span class="sxs-lookup"><span data-stu-id="c5c01-111">The binding is configured with a standard [\<wsHttpBinding>](../../configure-apps/file-schema/wcf/wshttpbinding.md) element, which defaults to using message security.</span></span> <span data-ttu-id="c5c01-112">這個範例會將 `clientCredentialType` 屬性設定為 Certificate 以要求用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-112">This sample sets the `clientCredentialType` attribute to Certificate to require client authentication.</span></span>  
  
```xml  
<system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="wsHttpBinding"/>  
    </protocolMapping>  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding>  
          <security mode ="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
```  
  
 <span data-ttu-id="c5c01-113">此行為會指定當用戶端驗證服務時所使用的服務認證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-113">The behavior specifies the service's credentials that are used when the client authenticates the service.</span></span> <span data-ttu-id="c5c01-114">伺服器憑證主體名稱是在元素的屬性中指定 `findValue` [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5c01-114">The server certificate subject name is specified in the `findValue` attribute in the [\<serviceCredentials>](../../configure-apps/file-schema/wcf/servicecredentials.md) element.</span></span>  
  
```xml  
<!--For debugging purposes, set the includeExceptionDetailInFaults attribute to true.-->  
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <!--   
        The serviceCredentials behavior allows one to define a service certificate.  
        A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
        This configuration references the "localhost" certificate installed during the setup instructions.  
        -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 <span data-ttu-id="c5c01-115">用戶端端點組態是由服務端點的絕對位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="c5c01-115">The client endpoint configuration consists of an absolute address for the service endpoint, the binding, and the contract.</span></span> <span data-ttu-id="c5c01-116">用戶端繫結會設定成適當的安全性模式與驗證模式。</span><span class="sxs-lookup"><span data-stu-id="c5c01-116">The client binding is configured with the appropriate security mode and authentication mode.</span></span> <span data-ttu-id="c5c01-117">在跨電腦案例中執行時，請確定服務端點位址已隨同變更。</span><span class="sxs-lookup"><span data-stu-id="c5c01-117">When running in a cross-computer scenario, ensure that the service endpoint address is changed accordingly.</span></span>  
  
```xml  
<system.serviceModel>  
    <client>  
      <!-- Use a behavior to configure the client certificate to present to the service. -->  
      <endpoint address="http://localhost/servicemodelsamples/service.svc" binding="wsHttpBinding" bindingConfiguration="Binding1" behaviorConfiguration="ClientCertificateBehavior" contract="Microsoft.Samples.Certificate.ICalculator"/>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!--   
        This configuration defines the security mode as Message and   
        the clientCredentialType as Certificate.  
        -->  
        <binding name="Binding1">  
          <security mode="Message">  
            <message clientCredentialType="Certificate"/>  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
...  
</system.serviceModel>  
```  
  
 <span data-ttu-id="c5c01-118">用戶端實作可以透過組態檔或程式碼設定要使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-118">The client implementation can set the certificate to use, either through the configuration file or through code.</span></span> <span data-ttu-id="c5c01-119">下列範例會示範如何在組態檔中設定要使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-119">The following sample shows how to set the certificate to use in the configuration file.</span></span>  
  
```xml  
<system.serviceModel>  
  ...  
  
<behaviors>  
      <endpointBehaviors>  
        <behavior name="ClientCertificateBehavior">  
          <!--   
        The clientCredentials behavior allows one to define a certificate to present to a service.  
        A certificate is used by a client to authenticate itself to the service and provide message integrity.  
        This configuration references the "client.com" certificate installed during the setup instructions.  
        -->  
          <clientCredentials>  
            <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName"/>  
            <serviceCertificate>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certificate authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust"/>  
            </serviceCertificate>  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
</system.serviceModel>  
```  
  
 <span data-ttu-id="c5c01-120">下列範例會示範如何在程式中呼叫服務。</span><span class="sxs-lookup"><span data-stu-id="c5c01-120">The following sample shows how to call the service in your program.</span></span>  

```csharp
// Create a client.  
CalculatorClient client = new CalculatorClient();  
  
// Call the GetCallerIdentity service operation.  
Console.WriteLine(client.GetCallerIdentity());  
...  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
```
  
 <span data-ttu-id="c5c01-121">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-121">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="c5c01-122">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="c5c01-122">Press ENTER in the client window to shut down the client.</span></span>  
  
```console  
CN=client.com  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
 <span data-ttu-id="c5c01-123">「訊息安全性」範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定用戶端與伺服器，以執行需要憑證安全性的裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5c01-123">The Setup.bat batch file included with the Message Security samples enables you to configure the client and server with relevant certificates to run a hosted application that requires certificate-based security.</span></span> <span data-ttu-id="c5c01-124">此批次檔可以執行於三種模式。</span><span class="sxs-lookup"><span data-stu-id="c5c01-124">The batch file can be run in three modes.</span></span> <span data-ttu-id="c5c01-125">若要在單一電腦模式中執行，請在 Visual Studio 的開發人員命令提示字元中 **setup.bat** ;針對服務模式類型 **setup.bat 服務**;以及針對用戶端模式類型 **setup.bat 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="c5c01-125">To run in single-computer mode type **setup.bat** in a Developer Command Prompt for Visual Studio ; for service mode type **setup.bat service**; and for client mode type **setup.bat client**.</span></span> <span data-ttu-id="c5c01-126">當跨電腦執行範例時，會使用用戶端與伺服器模式。</span><span class="sxs-lookup"><span data-stu-id="c5c01-126">Use the client and server mode when running the sample across computers.</span></span> <span data-ttu-id="c5c01-127">如需詳細資訊，請參閱本主題結尾的安裝程序。</span><span class="sxs-lookup"><span data-stu-id="c5c01-127">See the setup procedure at the end of this topic for details.</span></span> <span data-ttu-id="c5c01-128">下面提供批次檔的各區段簡要概觀，讓批次檔得以修改為在適當的組態下執行：</span><span class="sxs-lookup"><span data-stu-id="c5c01-128">The following provides a brief overview of the different sections of the batch files so that they can be modified to run in appropriate configuration:</span></span>  
  
- <span data-ttu-id="c5c01-129">建立用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-129">Creating the client certificate.</span></span>  
  
     <span data-ttu-id="c5c01-130">批次檔中的下列程式行會建立用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-130">The following line in the batch file creates the client certificate.</span></span> <span data-ttu-id="c5c01-131">在所建立之憑證主體的名稱中，會使用指定的用戶端名稱。</span><span class="sxs-lookup"><span data-stu-id="c5c01-131">The client name specified is used in the subject name of the certificate created.</span></span> <span data-ttu-id="c5c01-132">憑證會儲存在位於 `My` 存放區的 `CurrentUser` 存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-132">The certificate is stored in `My` store at the `CurrentUser` store location.</span></span>  
  
    ```bat
    echo ************  
    echo making client cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
    ```  
  
- <span data-ttu-id="c5c01-133">將用戶端憑證安裝至伺服器的受信任憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-133">Installing the client certificate into the server’s trusted certificate store.</span></span>  
  
     <span data-ttu-id="c5c01-134">批次檔中的下列程式行會將用戶端憑證複製到伺服器的 TrustedPeople 存放區，讓伺服器可以做出相關的信任或不信任決定。</span><span class="sxs-lookup"><span data-stu-id="c5c01-134">The following line in the batch file copies the client certificate into the server's TrustedPeople store so that the server can make the relevant trust or no-trust decisions.</span></span> <span data-ttu-id="c5c01-135">為了讓安裝在 TrustedPeople 存放區中的憑證受 Windows Communication Foundation (WCF) 服務信任，用戶端憑證驗證模式必須設為 `PeerOrChainTrust` 或 `PeerTrust` 。</span><span class="sxs-lookup"><span data-stu-id="c5c01-135">In order for a certificate installed in the TrustedPeople store to be trusted by a Windows Communication Foundation (WCF) service, the client certificate validation mode must be set to `PeerOrChainTrust` or `PeerTrust`.</span></span> <span data-ttu-id="c5c01-136">請參閱先前的服務組態範例，以了解如何使用組態檔完成這個工作。</span><span class="sxs-lookup"><span data-stu-id="c5c01-136">See the previous service configuration sample to learn how this can be done by using a configuration file.</span></span>  
  
    ```bat
    echo ************  
    echo copying client cert to server's LocalMachine store  
    echo ************  
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople
    ```  
  
- <span data-ttu-id="c5c01-137">建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-137">Creating the server certificate.</span></span>  
  
     <span data-ttu-id="c5c01-138">下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-138">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span>  
  
    ```bat
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     <span data-ttu-id="c5c01-139">%SERVER_NAME% 變數會指定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c5c01-139">The %SERVER_NAME% variable specifies the server name.</span></span> <span data-ttu-id="c5c01-140">憑證是儲存在 LocalMachine 存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-140">The certificate is stored in the LocalMachine store.</span></span> <span data-ttu-id="c5c01-141">如果使用 (服務的引數來執行 Setup.bat 批次檔（例如）， **setup.bat 服務**) % SERVER_NAME% 就會包含電腦的完整功能變數名稱。</span><span class="sxs-lookup"><span data-stu-id="c5c01-141">If the Setup.bat batch file is run with an argument of service (such as, **setup.bat service**) the %SERVER_NAME% contains the fully-qualified domain name of the computer.</span></span> <span data-ttu-id="c5c01-142">否則，預設為 localhost。</span><span class="sxs-lookup"><span data-stu-id="c5c01-142">Otherwise it defaults to localhost.</span></span>  
  
- <span data-ttu-id="c5c01-143">將伺服器憑證安裝至用戶端的受信任憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-143">Installing the server certificate into the client’s trusted certificate store.</span></span>  
  
     <span data-ttu-id="c5c01-144">下列程式行會將伺服器憑證複製到用戶端受信任人的存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-144">The following line copies the server certificate into the client trusted people store.</span></span> <span data-ttu-id="c5c01-145">這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-145">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="c5c01-146">如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證的步驟。</span><span class="sxs-lookup"><span data-stu-id="c5c01-146">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft-issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>  
  
    ```console  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
- <span data-ttu-id="c5c01-147">授與憑證私密金鑰的權限。</span><span class="sxs-lookup"><span data-stu-id="c5c01-147">Granting permissions on the certificate's private key.</span></span>  
  
     <span data-ttu-id="c5c01-148">Setup.bat 檔案中的下列幾行，會讓儲存在 LocalMachine 存放區的伺服器憑證可供 ASP.NET 背景工作進程帳戶存取。</span><span class="sxs-lookup"><span data-stu-id="c5c01-148">The following lines in the Setup.bat file make the server certificate stored in the LocalMachine store accessible to the ASP.NET worker process account.</span></span>  
  
    ```bat
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="c5c01-149">如果您使用非美國的。英文版的 Windows，您必須編輯 Setup.bat 檔，並將 "NT AUTHORITY\NETWORK SERVICE" 帳戶名稱取代為您的相同區域。</span><span class="sxs-lookup"><span data-stu-id="c5c01-149">If you are using a non-U.S. English edition of Windows, you must edit the Setup.bat file and replace the "NT AUTHORITY\NETWORK SERVICE" account name with your regional equivalent.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c5c01-150">在這個批次檔中使用的工具位於 C:\Program Files\Microsoft Visual Studio 8\Common7\tools 或 C:\Program Files\Microsoft SDKs\Windows\v6.0\bin。</span><span class="sxs-lookup"><span data-stu-id="c5c01-150">The tools used in this batch file are located in either C:\Program Files\Microsoft Visual Studio 8\Common7\tools or C:\Program Files\Microsoft SDKs\Windows\v6.0\bin.</span></span> <span data-ttu-id="c5c01-151">上述其中一種目錄一定會出現在您的系統路徑中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-151">One of these directories must be in your system path.</span></span> <span data-ttu-id="c5c01-152">如果您已安裝 Visual Studio，在路徑中取得此目錄最簡單的方式就是開啟 Visual Studio 的開發人員命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c5c01-152">If you have Visual Studio installed, the easiest way to get this directory in your path is to open the Developer Command Prompt for Visual Studio.</span></span> <span data-ttu-id="c5c01-153">按一下 [ **開始**]，然後選取 [ **所有程式**]、[ **Visual Studio 2012**]、[ **工具**]。</span><span class="sxs-lookup"><span data-stu-id="c5c01-153">Click **Start**, and then select **All Programs**, **Visual Studio 2012**, **Tools**.</span></span> <span data-ttu-id="c5c01-154">這個命令提示字元包含已設定的適當路徑。</span><span class="sxs-lookup"><span data-stu-id="c5c01-154">This command prompt has the appropriate paths already configured.</span></span> <span data-ttu-id="c5c01-155">否則，您必須手動將適當目錄新增至您的路徑。</span><span class="sxs-lookup"><span data-stu-id="c5c01-155">Otherwise you must add the appropriate directory to your path manually.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c5c01-156">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c5c01-156">The samples may already be installed on your computer.</span></span> <span data-ttu-id="c5c01-157">請先檢查下列 (預設) 目錄，然後再繼續：</span><span class="sxs-lookup"><span data-stu-id="c5c01-157">Check for the following (default) directory before continuing:</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c5c01-158">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="c5c01-158">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c5c01-159">此範例位於下列目錄：</span><span class="sxs-lookup"><span data-stu-id="c5c01-159">This sample is located in the following directory:</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MessageSecurity`  
  
### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="c5c01-160">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="c5c01-160">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="c5c01-161">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c01-161">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2. <span data-ttu-id="c5c01-162">若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="c5c01-162">To build the C# or Visual Basic .NET edition of the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>  
  
### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="c5c01-163">若要在同一部電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="c5c01-163">To run the sample on the same computer</span></span>  
  
1. <span data-ttu-id="c5c01-164">以系統管理員許可權開啟 Visual Studio 的開發人員命令提示字元，然後從範例安裝資料夾執行 Setup.bat。</span><span class="sxs-lookup"><span data-stu-id="c5c01-164">Open a Developer Command Prompt for Visual Studio  with administrator privileges and run Setup.bat from the sample install folder.</span></span> <span data-ttu-id="c5c01-165">這會安裝執行範例所需的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-165">This installs all the certificates required for running the sample.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c5c01-166">Setup.bat 批次檔的設計是要從 Visual Studio 的開發人員命令提示字元執行。</span><span class="sxs-lookup"><span data-stu-id="c5c01-166">The Setup.bat batch file is designed to be run from a Developer Command Prompt for Visual Studio.</span></span> <span data-ttu-id="c5c01-167">它要求 path 環境變數指向安裝 SDK 的目錄。</span><span class="sxs-lookup"><span data-stu-id="c5c01-167">It requires that the path environment variable point to the directory where the SDK is installed.</span></span> <span data-ttu-id="c5c01-168">此環境變數會在 Visual Studio (2010) 的開發人員命令提示字元內自動設定。</span><span class="sxs-lookup"><span data-stu-id="c5c01-168">This environment variable is automatically set within a Developer Command Prompt for Visual Studio (2010).</span></span>  
  
2. <span data-ttu-id="c5c01-169">藉由輸入位址來確認對服務的存取權 `http://localhost/servicemodelsamples/service.svc` 。</span><span class="sxs-lookup"><span data-stu-id="c5c01-169">Verify access to the service using a browser by entering the address `http://localhost/servicemodelsamples/service.svc`.</span></span>  
  
3. <span data-ttu-id="c5c01-170">從 \client\bin 啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="c5c01-170">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="c5c01-171">用戶端活動會顯示在用戶端主控台應用程式上。</span><span class="sxs-lookup"><span data-stu-id="c5c01-171">Client activity is displayed on the client console application.</span></span>  
  
4. <span data-ttu-id="c5c01-172">如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="c5c01-172">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="c5c01-173">若要跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="c5c01-173">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="c5c01-174">在服務電腦上建立目錄。</span><span class="sxs-lookup"><span data-stu-id="c5c01-174">Create a directory on the service computer.</span></span> <span data-ttu-id="c5c01-175">使用 Internet Information Services (IIS) 管理工具，為這個目錄建立名為 servicemodelsamples 的虛擬應用程式。</span><span class="sxs-lookup"><span data-stu-id="c5c01-175">Create a virtual application named servicemodelsamples for this directory by using the Internet Information Services (IIS) management tool.</span></span>  
  
2. <span data-ttu-id="c5c01-176">將 \inetpub\wwwroot\servicemodelsamples 中的服務程式檔複製至服務電腦上的虛擬目錄中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-176">Copy the service program files from \inetpub\wwwroot\servicemodelsamples to the virtual directory on the service computer.</span></span> <span data-ttu-id="c5c01-177">確定複製 \bin 子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5c01-177">Ensure that you copy the files in the \bin subdirectory.</span></span> <span data-ttu-id="c5c01-178">同時將 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 檔案複製到服務電腦。</span><span class="sxs-lookup"><span data-stu-id="c5c01-178">Also copy the Setup.bat, Cleanup.bat, and ImportClientCert.bat files to the service computer.</span></span>  
  
3. <span data-ttu-id="c5c01-179">在用戶端電腦上為用戶端二進位碼檔案建立一個目錄。</span><span class="sxs-lookup"><span data-stu-id="c5c01-179">Create a directory on the client computer for the client binaries.</span></span>  
  
4. <span data-ttu-id="c5c01-180">將用戶端程式檔複製到用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="c5c01-180">Copy the client program files to the client directory on the client computer.</span></span> <span data-ttu-id="c5c01-181">同時，將 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 檔案複製到用戶端。</span><span class="sxs-lookup"><span data-stu-id="c5c01-181">Also copy the Setup.bat, Cleanup.bat, and ImportServiceCert.bat files to the client.</span></span>  
  
5. <span data-ttu-id="c5c01-182">在伺服器上，以具有系統管理員許可權 Visual Studio 的開發人員命令提示字元執行 **setup.bat 服務** 。</span><span class="sxs-lookup"><span data-stu-id="c5c01-182">On the server, run **setup.bat service** in a Developer Command Prompt for Visual Studio with administrator privileges.</span></span> <span data-ttu-id="c5c01-183">使用 **service** 引數執行 **setup.bat** 會建立具有電腦完整功能變數名稱的服務憑證，並將服務憑證匯出至名為 service .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5c01-183">Running **setup.bat** with the **service** argument creates a service certificate with the fully-qualified domain name of the computer and exports the service certificate to a file named Service.cer.</span></span>  
  
6. <span data-ttu-id="c5c01-184">編輯 Web.config，以反映) 中的屬性 (新的憑證名稱，此名稱與 `findValue` [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 電腦的完整功能變數名稱相同。</span><span class="sxs-lookup"><span data-stu-id="c5c01-184">Edit Web.config to reflect the new certificate name (in the `findValue` attribute in the [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)) which is the same as the fully-qualified domain name of the computer.</span></span>  
  
7. <span data-ttu-id="c5c01-185">從服務目錄中將 Service.cer 檔案複製至用戶端電腦上的用戶端目錄。</span><span class="sxs-lookup"><span data-stu-id="c5c01-185">Copy the Service.cer file from the service directory to the client directory on the client computer.</span></span>  
  
8. <span data-ttu-id="c5c01-186">在用戶端上，以具有系統管理員許可權之 Visual Studio 的開發人員命令提示字元執行 **setup.bat 用戶端** 。</span><span class="sxs-lookup"><span data-stu-id="c5c01-186">On the client, run **setup.bat client** in a Developer Command Prompt for Visual Studio with administrator privileges.</span></span> <span data-ttu-id="c5c01-187">使用 **用戶端** 引數執行 **setup.bat** 會建立名為 client.com 的用戶端憑證，並將用戶端憑證匯出至名為 client .cer 的檔案。</span><span class="sxs-lookup"><span data-stu-id="c5c01-187">Running **setup.bat** with the **client** argument creates a client certificate named client.com and exports the client certificate to a file named Client.cer.</span></span>  
  
9. <span data-ttu-id="c5c01-188">在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。</span><span class="sxs-lookup"><span data-stu-id="c5c01-188">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span> <span data-ttu-id="c5c01-189">若要這麼做，請使用伺服器的完整網域名稱取代 localhost。</span><span class="sxs-lookup"><span data-stu-id="c5c01-189">Do this by replacing localhost with the fully-qualified domain name of the server.</span></span>  
  
10. <span data-ttu-id="c5c01-190">從用戶端目錄將 Client.cer 檔案複製到伺服器上的服務目錄中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-190">Copy the Client.cer file from the client directory to the service directory on the server.</span></span>  
  
11. <span data-ttu-id="c5c01-191">在用戶端上，以具有系統管理許可權之 Visual Studio 的開發人員命令提示字元來執行 ImportServiceCert.bat。</span><span class="sxs-lookup"><span data-stu-id="c5c01-191">On the client, run ImportServiceCert.bat in a Developer Command Prompt for Visual Studio with administrative privileges.</span></span> <span data-ttu-id="c5c01-192">這樣會將服務憑證從 Service.cer 檔案匯入至 CurrentUser - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-192">This imports the service certificate from the Service.cer file into the CurrentUser - TrustedPeople store.</span></span>  
  
12. <span data-ttu-id="c5c01-193">在伺服器上，以具有系統管理許可權之 Visual Studio 的開發人員命令提示字元來執行 ImportClientCert.bat。</span><span class="sxs-lookup"><span data-stu-id="c5c01-193">On the server, run ImportClientCert.bat in a Developer Command Prompt for Visual Studio with administrative privileges.</span></span> <span data-ttu-id="c5c01-194">這樣便會從 Client.cer 檔將用戶端憑證匯入至 LocalMachine - TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="c5c01-194">This imports the client certificate from the Client.cer file into the LocalMachine - TrustedPeople store.</span></span>  
  
13. <span data-ttu-id="c5c01-195">在用戶端電腦上，從命令提示字元視窗啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="c5c01-195">On the client computer, launch Client.exe from a command prompt window.</span></span> <span data-ttu-id="c5c01-196">如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="c5c01-196">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="c5c01-197">若要在使用範例之後進行清除</span><span class="sxs-lookup"><span data-stu-id="c5c01-197">To clean up after the sample</span></span>  
  
- <span data-ttu-id="c5c01-198">當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。</span><span class="sxs-lookup"><span data-stu-id="c5c01-198">Run Cleanup.bat in the samples folder after you have finished running the sample.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c5c01-199">跨電腦執行此範例時，這個指令碼不會移除用戶端上的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-199">This script does not remove service certificates on a client when running this sample across computers.</span></span> <span data-ttu-id="c5c01-200">如果您已執行 Windows Communication Foundation (使用跨電腦憑證的 WCF) 範例，請務必清除 TrustedPeople 存放區中已安裝的服務憑證。</span><span class="sxs-lookup"><span data-stu-id="c5c01-200">If you have run Windows Communication Foundation (WCF) samples that use certificates across computers, be sure to clear the service certificates that have been installed in the CurrentUser - TrustedPeople store.</span></span> <span data-ttu-id="c5c01-201">若要這麼做，請使用下列命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="c5c01-201">To do this, use the following command: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` For example: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.</span></span>
