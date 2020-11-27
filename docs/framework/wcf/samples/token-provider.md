---
title: 權杖提供者
ms.date: 03/30/2017
ms.assetid: 947986cf-9946-4987-84e5-a14678d96edb
ms.openlocfilehash: e761f32ab26cf620b6ef1dddff2bcba53289af84
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96262329"
---
# <a name="token-provider"></a><span data-ttu-id="5f098-102">權杖提供者</span><span class="sxs-lookup"><span data-stu-id="5f098-102">Token Provider</span></span>

<span data-ttu-id="5f098-103">這個範例會示範如何實作自訂權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-103">This sample demonstrates how to implement a custom token provider.</span></span> <span data-ttu-id="5f098-104">Windows Communication Foundation (WCF) 中的權杖提供者是用來提供認證給安全性基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5f098-104">A token provider in Windows Communication Foundation (WCF) is used for supplying credentials to the security infrastructure.</span></span> <span data-ttu-id="5f098-105">一般而言，權杖提供者會檢查目標並發行適當的認證，讓安全性基礎結構能夠保護訊息的安全。</span><span class="sxs-lookup"><span data-stu-id="5f098-105">The token provider in general examines the target and issues appropriate credentials so that the security infrastructure can secure the message.</span></span> <span data-ttu-id="5f098-106">WCF 隨附預設的認證管理員權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-106">WCF ships with the default Credential Manager Token Provider.</span></span> <span data-ttu-id="5f098-107">WCF 也隨附于 CardSpace 權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-107">WCF also ships with a CardSpace token provider.</span></span> <span data-ttu-id="5f098-108">自訂權杖提供者適用於下列情況：</span><span class="sxs-lookup"><span data-stu-id="5f098-108">Custom token providers are useful in the following cases:</span></span>

- <span data-ttu-id="5f098-109">如果您有這些權杖提供者無法使用的認證存放區。</span><span class="sxs-lookup"><span data-stu-id="5f098-109">If you have a credential store that these token providers cannot operate with.</span></span>

- <span data-ttu-id="5f098-110">如果您想要提供自己的自訂機制，以便在使用者提供詳細資料給 WCF 用戶端架構使用認證時，將認證從點轉換。</span><span class="sxs-lookup"><span data-stu-id="5f098-110">If you want to provide your own custom mechanism for transforming the credentials from the point when the user provides the details to when the WCF client framework uses the credentials.</span></span>

- <span data-ttu-id="5f098-111">如果您要建置自訂權杖。</span><span class="sxs-lookup"><span data-stu-id="5f098-111">If you are building a custom token.</span></span>

 <span data-ttu-id="5f098-112">這個範例會示範如何建置自訂權杖提供者，以便將使用者的輸入轉換為不同的格式。</span><span class="sxs-lookup"><span data-stu-id="5f098-112">This sample shows how to build a custom token provider that transforms the input from the user into a different format.</span></span>

 <span data-ttu-id="5f098-113">簡而言之，這個範例示範下面的情形：</span><span class="sxs-lookup"><span data-stu-id="5f098-113">To summarize, this sample demonstrates the following:</span></span>

- <span data-ttu-id="5f098-114">用戶端如何透過使用者名稱/密碼組進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5f098-114">How a client can authenticate using a username/password pair.</span></span>

- <span data-ttu-id="5f098-115">如何使用自訂權杖提供者設定用戶端。</span><span class="sxs-lookup"><span data-stu-id="5f098-115">How a client can be configured with a custom token provider.</span></span>

- <span data-ttu-id="5f098-116">伺服器如何搭配自訂 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> (驗證使用者名稱與密碼是否相符) 來使用密碼驗證用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="5f098-116">How the server can validate the client credentials using a password with a custom <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> that validates that the username and password match.</span></span>

- <span data-ttu-id="5f098-117">用戶端如何使用伺服器的 X.509 憑證來驗證伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f098-117">How the server is authenticated by the client using the server's X.509 certificate.</span></span>

 <span data-ttu-id="5f098-118">這個範例也會示範如何在自訂權杖驗證程序之後存取呼叫者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5f098-118">This sample also shows how the caller's identity is accessible after the custom token authentication process.</span></span>

 <span data-ttu-id="5f098-119">服務會公開 (Expose) 單一的端點來與已使用組態檔 App.config 定義之服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="5f098-119">The service exposes a single endpoint for communicating with the service, defined using the App.config configuration file.</span></span> <span data-ttu-id="5f098-120">端點是由位址、繫結及合約所組成。</span><span class="sxs-lookup"><span data-stu-id="5f098-120">The endpoint consists of an address, a binding, and a contract.</span></span> <span data-ttu-id="5f098-121">繫結已設定成預設會使用訊息安全性的標準 `wsHttpBinding`。</span><span class="sxs-lookup"><span data-stu-id="5f098-121">The binding is configured with a standard `wsHttpBinding`, which uses message security by default.</span></span> <span data-ttu-id="5f098-122">這個範例會將標準 `wsHttpBinding` 設定為使用用戶端使用者名稱驗證。</span><span class="sxs-lookup"><span data-stu-id="5f098-122">This sample sets the standard `wsHttpBinding` to use client username authentication.</span></span> <span data-ttu-id="5f098-123">服務也會使用 serviceCredentials 行為來設定服務憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-123">The service also configures the service certificate using the serviceCredentials behavior.</span></span> <span data-ttu-id="5f098-124">serviceCredentials 行為可以讓您設定服務憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-124">The serviceCredentials behavior allows you to configure a service certificate.</span></span> <span data-ttu-id="5f098-125">服務憑證是由用戶端用來驗證服務並提供訊息保護。</span><span class="sxs-lookup"><span data-stu-id="5f098-125">A service certificate is used by a client to authenticate the service and provide message protection.</span></span> <span data-ttu-id="5f098-126">下列組態會參考在安裝範例期間所安裝的 localhost 憑證，如下列安裝指示中所述。</span><span class="sxs-lookup"><span data-stu-id="5f098-126">The following configuration references the localhost certificate installed during the sample setup as described in the following setup instructions.</span></span>

```xml
<system.serviceModel>
    <services>
      <service
          name="Microsoft.ServiceModel.Samples.CalculatorService"
          behaviorConfiguration="CalculatorServiceBehavior">
        <host>
          <baseAddresses>
            <!-- configure base address provided by host -->
            <add baseAddress ="http://localhost:8000/servicemodelsamples/service"/>
          </baseAddresses>
        </host>
        <!-- use base address provided by host -->
        <endpoint address=""
                  binding="wsHttpBinding"
                  bindingConfiguration="Binding1"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
      </service>
    </services>

    <bindings>
      <wsHttpBinding>
        <binding name="Binding1">
          <security mode="Message">
            <message clientCredentialType="UserName" />
          </security>
        </binding>
      </wsHttpBinding>
    </bindings>

    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceDebug includeExceptionDetailInFaults="False" />
          <!--
        The serviceCredentials behavior allows one to define a service certificate.
        A service certificate is used by a client to authenticate the service and provide message protection.
        This configuration references the "localhost" certificate installed during the setup instructions.
        -->
          <serviceCredentials>
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />
          </serviceCredentials>
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
```

 <span data-ttu-id="5f098-127">用戶端的端點組態是由組態名稱、服務端點的絕對位址、繫結和合約所組成。</span><span class="sxs-lookup"><span data-stu-id="5f098-127">The client endpoint configuration consists of a configuration name, an absolute address for the service endpoint, the binding, and the contract.</span></span> <span data-ttu-id="5f098-128">用戶端繫結已設定了適當的 `Mode` 與訊息 `clientCredentialType`。</span><span class="sxs-lookup"><span data-stu-id="5f098-128">The client binding is configured with the appropriate `Mode` and message `clientCredentialType`.</span></span>

```xml
<system.serviceModel>
  <client>
    <endpoint name=""
              address="http://localhost:8000/servicemodelsamples/service"
              binding="wsHttpBinding"
              bindingConfiguration="Binding1"
              contract="Microsoft.ServiceModel.Samples.ICalculator">
    </endpoint>
  </client>

  <bindings>
    <wsHttpBinding>
      <binding name="Binding1">
        <security mode="Message">
          <message clientCredentialType="UserName" />
        </security>
      </binding>
    </wsHttpBinding>
  </bindings>
</system.serviceModel>
```

 <span data-ttu-id="5f098-129">下列步驟說明如何開發自訂權杖提供者，並將它與 WCF 安全性架構整合：</span><span class="sxs-lookup"><span data-stu-id="5f098-129">The following steps show how to develop a custom token provider and integrate it with the WCF security framework:</span></span>

1. <span data-ttu-id="5f098-130">撰寫自訂權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-130">Write a custom token provider.</span></span>

     <span data-ttu-id="5f098-131">此範例會實作取得使用者名稱與密碼的自訂權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-131">The sample implements a custom token provider that obtains the username and password.</span></span> <span data-ttu-id="5f098-132">密碼必須符合這個使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-132">The password must match this username.</span></span> <span data-ttu-id="5f098-133">這個自訂權杖提供者僅供示範之用，因此不建議用於真實世界。</span><span class="sxs-lookup"><span data-stu-id="5f098-133">This custom token provider is for demonstration purposes only and is not recommended for real world deployment.</span></span>

     <span data-ttu-id="5f098-134">為了執行這個工作，自訂權杖提供者會衍生 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 類別並覆寫 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> 方法。</span><span class="sxs-lookup"><span data-stu-id="5f098-134">To perform this task, the custom token provider derives the <xref:System.IdentityModel.Selectors.SecurityTokenProvider> class and overrides the <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> method.</span></span> <span data-ttu-id="5f098-135">這個方法會建立並傳回新的 `UserNameSecurityToken`。</span><span class="sxs-lookup"><span data-stu-id="5f098-135">This method creates and returns a new `UserNameSecurityToken`.</span></span>

    ```csharp
    protected override SecurityToken GetTokenCore(TimeSpan timeout)
    {
        // obtain username and password from the user using console window
        string username = GetUserName();
        string password = GetPassword();
        Console.WriteLine("username: {0}", username);

        // return new UserNameSecurityToken containing information obtained from user
        return new UserNameSecurityToken(username, password);
    }
    ```

2. <span data-ttu-id="5f098-136">撰寫自訂安全性權杖管理員。</span><span class="sxs-lookup"><span data-stu-id="5f098-136">Write custom security token manager.</span></span>

     <span data-ttu-id="5f098-137">此 <xref:System.IdentityModel.Selectors.SecurityTokenManager> 會用來建立特定 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> (以 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 方法傳遞至該管理員) 的 `CreateSecurityTokenProvider`。</span><span class="sxs-lookup"><span data-stu-id="5f098-137">The <xref:System.IdentityModel.Selectors.SecurityTokenManager> is used to create <xref:System.IdentityModel.Selectors.SecurityTokenProvider> for specific <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> that is passed to it in `CreateSecurityTokenProvider` method.</span></span> <span data-ttu-id="5f098-138">安全性權杖管理員也會用來建立權杖驗證器與權杖序列化程式，但是這些不在本範例的討論範圍。</span><span class="sxs-lookup"><span data-stu-id="5f098-138">Security token manager is also used to create token authenticators and a token serializer, but those are not covered by this sample.</span></span> <span data-ttu-id="5f098-139">在這個範例中，自訂安全性權杖管理員繼承自 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 類別，並且會覆寫 `CreateSecurityTokenProvider` 方法，以便在傳遞的權杖需求表示要求使用者名稱提供者時傳回自訂使用者名稱權杖提供者。</span><span class="sxs-lookup"><span data-stu-id="5f098-139">In this sample, the custom security token manager inherits from <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> class and overrides the `CreateSecurityTokenProvider` method to return custom username token provider when the passed token requirements indicate that username provider is requested.</span></span>

    ```csharp
    public class MyUserNameSecurityTokenManager : ClientCredentialsSecurityTokenManager
    {
        MyUserNameClientCredentials myUserNameClientCredentials;

        public MyUserNameSecurityTokenManager(MyUserNameClientCredentials myUserNameClientCredentials)
            : base(myUserNameClientCredentials)
        {
            this.myUserNameClientCredentials = myUserNameClientCredentials;
        }

        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)
        {
            // if token requirement matches username token return custom username token provider
            // otherwise use base implementation
            if (tokenRequirement.TokenType == SecurityTokenTypes.UserName)
            {
                return new MyUserNameTokenProvider();
            }
            else
            {
                return base.CreateSecurityTokenProvider(tokenRequirement);
            }
        }
    }
    ```

3. <span data-ttu-id="5f098-140">撰寫自訂用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-140">Write a custom client credential.</span></span>

     <span data-ttu-id="5f098-141">用戶端認證類別會用來代表針對用戶端 Proxy 設定的認證，並且會建立用來取得權杖驗證器、權杖提供者以及權杖序列化程式的安全性權杖管理員。</span><span class="sxs-lookup"><span data-stu-id="5f098-141">Client credentials class is used to represent the credentials that are configured for the client proxy and creates security token manager that is used to obtain token authenticators, token providers and a token serializer.</span></span>

    ```csharp
    public class MyUserNameClientCredentials : ClientCredentials
    {
        public MyUserNameClientCredentials()
            : base()
        {
        }

        protected override ClientCredentials CloneCore()
        {
            return new MyUserNameClientCredentials();
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            // return custom security token manager
            return new MyUserNameSecurityTokenManager(this);
        }
    }
    ```

4. <span data-ttu-id="5f098-142">將用戶端設定成使用自訂用戶端認證。</span><span class="sxs-lookup"><span data-stu-id="5f098-142">Configure the client to use the custom client credential.</span></span>

     <span data-ttu-id="5f098-143">為了讓用戶端使用自訂用戶端認證，此範例會刪除預設用戶端認證類別，並提供新的用戶端認證類別。</span><span class="sxs-lookup"><span data-stu-id="5f098-143">In order for the client to use the custom client credential, the sample deletes the default client credential class and supplies the new client credential class.</span></span>

    ```csharp
    static void Main()
    {
        // ...
           // Create a client with given client endpoint configuration
          CalculatorClient client = new CalculatorClient();

          // set new credentials
           client.ChannelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));
         client.ChannelFactory.Endpoint.Behaviors.Add(new MyUserNameClientCredentials());
       // ...
    }
    ```

 <span data-ttu-id="5f098-144">為了在服務端上顯示呼叫者的資訊，此時會使用 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A>，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="5f098-144">On the service, to display the caller's information, use the <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> as shown in the following code example.</span></span> <span data-ttu-id="5f098-145"><xref:System.ServiceModel.ServiceSecurityContext.Current%2A> 包含有關目前呼叫者的宣告資訊。</span><span class="sxs-lookup"><span data-stu-id="5f098-145">The <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> contains claims information about the current caller.</span></span>

```csharp
static void DisplayIdentityInformation()
{
    Console.WriteLine("\t\tSecurity context identity  :  {0}",
        ServiceSecurityContext.Current.PrimaryIdentity.Name);
}
```

 <span data-ttu-id="5f098-146">當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="5f098-146">When you run the sample, the operation requests and responses are displayed in the client console window.</span></span> <span data-ttu-id="5f098-147">在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。</span><span class="sxs-lookup"><span data-stu-id="5f098-147">Press ENTER in the client window to shut down the client.</span></span>

## <a name="setup-batch-file"></a><span data-ttu-id="5f098-148">設定批次檔</span><span class="sxs-lookup"><span data-stu-id="5f098-148">Setup Batch File</span></span>

 <span data-ttu-id="5f098-149">這個範例中所包含的 Setup.bat 批次檔可讓您使用相關的憑證設定伺服器，以執行需要伺服器憑證安全性的自我裝載應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f098-149">The Setup.bat batch file included with this sample allows you to configure the server with the relevant certificate to run a self-hosted application that requires server certificate-based security.</span></span> <span data-ttu-id="5f098-150">這個批次檔必須經過修改才能跨電腦運作，或在非裝載的情況下運作。</span><span class="sxs-lookup"><span data-stu-id="5f098-150">This batch file must be modified to work across computers or to work in a non-hosted case.</span></span>

 <span data-ttu-id="5f098-151">下面提供批次檔的各區段簡要概觀，讓批次檔得以修改為在適當的組態下執行：</span><span class="sxs-lookup"><span data-stu-id="5f098-151">The following provides a brief overview of the different sections of the batch files so that they can be modified to run in the appropriate configuration:</span></span>

- <span data-ttu-id="5f098-152">建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-152">Creating the server certificate.</span></span>

     <span data-ttu-id="5f098-153">下列 Setup.bat 批次檔中的程式行會建立要使用的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-153">The following lines from the Setup.bat batch file create the server certificate to be used.</span></span> <span data-ttu-id="5f098-154">`%SERVER_NAME%` 變數會指定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-154">The `%SERVER_NAME%` variable specifies the server name.</span></span> <span data-ttu-id="5f098-155">您可以變更這個變數來指定自己的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-155">Change this variable to specify your own server name.</span></span> <span data-ttu-id="5f098-156">這個批次檔中的預設值為 localhost。</span><span class="sxs-lookup"><span data-stu-id="5f098-156">The default value in this batch file is localhost.</span></span>

    ```console
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- <span data-ttu-id="5f098-157">將伺服器憑證安裝至用戶端的受信任憑證存放區中。</span><span class="sxs-lookup"><span data-stu-id="5f098-157">Installing the server certificate into the client's trusted certificate store:</span></span>

     <span data-ttu-id="5f098-158">Setup.bat 批次檔中的下列程式行會將伺服器憑證複製到用戶端受信任人的存放區。</span><span class="sxs-lookup"><span data-stu-id="5f098-158">The following lines in the Setup.bat batch file copy the server certificate into the client trusted people store.</span></span> <span data-ttu-id="5f098-159">這是必要步驟，因為用戶端系統並未隱含信任 Makecert.exe 產生的憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-159">This step is required because certificates generated by Makecert.exe are not implicitly trusted by the client system.</span></span> <span data-ttu-id="5f098-160">如果您已經有一個以用戶端信任的根憑證 (例如 Microsoft 所發行的憑證) 為基礎的憑證，就不需要這個將伺服器憑證填入用戶端憑證存放區的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f098-160">If you already have a certificate that is rooted in a client trusted root certificate—for example, a Microsoft issued certificate—this step of populating the client certificate store with the server certificate is not required.</span></span>

    ```console
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

> [!NOTE]
> <span data-ttu-id="5f098-161">Setup.bat 批次檔是設計用來從 Windows SDK 命令提示字元執行。</span><span class="sxs-lookup"><span data-stu-id="5f098-161">The Setup.bat batch file is designed to be run from a Windows SDK Command Prompt.</span></span> <span data-ttu-id="5f098-162">它要求 MSSDK 環境變數指向安裝 SDK 的目錄。</span><span class="sxs-lookup"><span data-stu-id="5f098-162">It requires that the MSSDK environment variable point to the directory where the SDK is installed.</span></span> <span data-ttu-id="5f098-163">這個環境變數是自動在 Windows SDK 命令提示字元中設定。</span><span class="sxs-lookup"><span data-stu-id="5f098-163">This environment variable is automatically set within a Windows SDK Command Prompt.</span></span>

#### <a name="to-set-up-and-build-the-sample"></a><span data-ttu-id="5f098-164">若要設定和建置範例</span><span class="sxs-lookup"><span data-stu-id="5f098-164">To set up and build the sample</span></span>

1. <span data-ttu-id="5f098-165">確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="5f098-165">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="5f098-166">若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。</span><span class="sxs-lookup"><span data-stu-id="5f098-166">To build the solution, follow the instructions in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

#### <a name="to-run-the-sample-on-the-same-computer"></a><span data-ttu-id="5f098-167">若要在同一部電腦上執行範例</span><span class="sxs-lookup"><span data-stu-id="5f098-167">To run the sample on the same computer</span></span>

1. <span data-ttu-id="5f098-168">從使用系統管理員許可權開啟的 Visual Studio 2012 命令提示字元內，執行範例安裝資料夾中的 Setup.bat。</span><span class="sxs-lookup"><span data-stu-id="5f098-168">Run Setup.bat from the sample installation folder inside a Visual Studio 2012 command prompt opened with administrator privileges.</span></span> <span data-ttu-id="5f098-169">這會安裝執行範例所需的所有憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-169">This installs all the certificates required for running the sample.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f098-170">Setup.bat 批次檔是設計來從 Visual Studio 2012 命令提示字元執行。</span><span class="sxs-lookup"><span data-stu-id="5f098-170">The Setup.bat batch file is designed to be run from a Visual Studio 2012 Command Prompt.</span></span> <span data-ttu-id="5f098-171">在 Visual Studio 2012 命令提示字元中設定的 PATH 環境變數，會指向包含 Setup.bat 腳本所需之可執行檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="5f098-171">The PATH environment variable set within the Visual Studio 2012 Command Prompt points to the directory that contains executables required by the Setup.bat script.</span></span>  
  
2. <span data-ttu-id="5f098-172">從 service\bin 啟動 service.exe。</span><span class="sxs-lookup"><span data-stu-id="5f098-172">Launch service.exe from service\bin.</span></span>  
  
3. <span data-ttu-id="5f098-173">從 \client\bin 啟動 Client.exe。</span><span class="sxs-lookup"><span data-stu-id="5f098-173">Launch Client.exe from \client\bin.</span></span> <span data-ttu-id="5f098-174">用戶端活動會顯示在用戶端主控台應用程式上。</span><span class="sxs-lookup"><span data-stu-id="5f098-174">Client activity is displayed on the client console application.</span></span>  
  
4. <span data-ttu-id="5f098-175">在使用者名稱提示中，輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-175">At the username prompt, type a user name.</span></span>  
  
5. <span data-ttu-id="5f098-176">在密碼提示中，使用在使用者名稱提示中輸入的相同字串。</span><span class="sxs-lookup"><span data-stu-id="5f098-176">At the password prompt, use the same string that was typed for the username prompt.</span></span>  
  
6. <span data-ttu-id="5f098-177">如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="5f098-177">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
#### <a name="to-run-the-sample-across-computers"></a><span data-ttu-id="5f098-178">若要跨電腦執行範例</span><span class="sxs-lookup"><span data-stu-id="5f098-178">To run the sample across computers</span></span>  
  
1. <span data-ttu-id="5f098-179">在服務電腦上為服務二進位碼檔案建立一個目錄。</span><span class="sxs-lookup"><span data-stu-id="5f098-179">Create a directory on the service computer for the service binaries.</span></span>  
  
2. <span data-ttu-id="5f098-180">將服務程式檔複製到服務電腦上的服務目錄。</span><span class="sxs-lookup"><span data-stu-id="5f098-180">Copy the service program files to the service directory on the service computer.</span></span> <span data-ttu-id="5f098-181">同時，將 Setup.bat 和 Cleanup.bat 檔案複製到服務電腦中。</span><span class="sxs-lookup"><span data-stu-id="5f098-181">Also copy the Setup.bat and Cleanup.bat files to the service computer.</span></span>  
  
3. <span data-ttu-id="5f098-182">您伺服器憑證的主體名稱必須包含電腦的完整網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-182">You must have a server certificate with the subject name that contains the fully-qualified domain name of the computer.</span></span> <span data-ttu-id="5f098-183">此 Service.exe.config 檔必須更新以反映這個新憑證名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-183">The Service.exe.config file must be updated to reflect this new certificate name.</span></span> <span data-ttu-id="5f098-184">您可以修改 Setup.bat 批次檔來建立伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="5f098-184">You can create server certificate by modifying the Setup.bat batch file.</span></span> <span data-ttu-id="5f098-185">請注意，setup.bat 檔案必須從開發人員命令提示字元中執行，才能使用系統管理員許可權開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5f098-185">Note that the setup.bat file must be run from a Developer Command Prompt for Visual Studio opened with administrator privileges.</span></span> <span data-ttu-id="5f098-186">您必須將 `%SERVER_NAME%` 變數設定為用來裝載服務之電腦的完整主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5f098-186">You must set `%SERVER_NAME%` variable to fully-qualified host name of the computer that is used to host the service.</span></span>  
  
4. <span data-ttu-id="5f098-187">將伺服器憑證複製到用戶端的 CurrentUser-TrustedPeople 存放區中。</span><span class="sxs-lookup"><span data-stu-id="5f098-187">Copy the server certificate into the CurrentUser-TrustedPeople store of the client.</span></span> <span data-ttu-id="5f098-188">當伺服器憑證是由用戶端信任的簽發者發行時，您就不需要這麼做。</span><span class="sxs-lookup"><span data-stu-id="5f098-188">You do not need to do this when the server certificate is issued by a client trusted issuer.</span></span>  
  
5. <span data-ttu-id="5f098-189">在服務電腦的 Service.exe.config 檔中變更基底位址的值，以指定完整電腦名稱而不要指定 localhost。</span><span class="sxs-lookup"><span data-stu-id="5f098-189">In the Service.exe.config file on the service computer, change the value of the base address to specify a fully-qualified computer name instead of localhost.</span></span>  
  
6. <span data-ttu-id="5f098-190">在服務電腦上，從命令提示字元執行 service.exe。</span><span class="sxs-lookup"><span data-stu-id="5f098-190">On the service computer, run service.exe from a command prompt.</span></span>  
  
7. <span data-ttu-id="5f098-191">將語言特定資料夾下 \client\bin\ 資料夾中的用戶端程式檔案複製到用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="5f098-191">Copy the client program files from the \client\bin\ folder, under the language-specific folder, to the client computer.</span></span>  
  
8. <span data-ttu-id="5f098-192">在用戶端電腦上的 Client.exe.config 檔案中，變更端點的位址值以符合服務的新位址。</span><span class="sxs-lookup"><span data-stu-id="5f098-192">In the Client.exe.config file on the client computer, change the address value of the endpoint to match the new address of your service.</span></span>  
  
9. <span data-ttu-id="5f098-193">在用戶端電腦上，從命令提示字元視窗啟動 `Client.exe`。</span><span class="sxs-lookup"><span data-stu-id="5f098-193">On the client computer, launch `Client.exe` from a command prompt window.</span></span>  
  
10. <span data-ttu-id="5f098-194">如果用戶端和服務無法通訊，請參閱 [WCF 範例的疑難排解提示](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。</span><span class="sxs-lookup"><span data-stu-id="5f098-194">If the client and service are not able to communicate, see [Troubleshooting Tips for WCF Samples](/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).</span></span>  
  
#### <a name="to-clean-up-after-the-sample"></a><span data-ttu-id="5f098-195">若要在使用範例之後進行清除</span><span class="sxs-lookup"><span data-stu-id="5f098-195">To clean up after the sample</span></span>  
  
1. <span data-ttu-id="5f098-196">當您完成執行範例後，請執行範例資料夾中的 Cleanup.bat。</span><span class="sxs-lookup"><span data-stu-id="5f098-196">Run Cleanup.bat in the samples folder once you have finished running the sample.</span></span>
