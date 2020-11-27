---
title: 組態與中繼資料支援
ms.date: 03/30/2017
ms.assetid: 27c240cb-8cab-472c-87f8-c864f4978758
ms.openlocfilehash: fe7de6fddeccbc83bc81eea69c27c7da5df5c8c3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96257993"
---
# <a name="configuration-and-metadata-support"></a><span data-ttu-id="068d4-102">組態與中繼資料支援</span><span class="sxs-lookup"><span data-stu-id="068d4-102">Configuration and Metadata Support</span></span>

<span data-ttu-id="068d4-103">這個主題描述如何啟用繫結和繫結項目的組態與中繼資料支援。</span><span class="sxs-lookup"><span data-stu-id="068d4-103">This topic describes how to enable configuration and metadata support for bindings and binding elements.</span></span>  
  
## <a name="overview-of-configuration-and-metadata"></a><span data-ttu-id="068d4-104">組態與中繼資料概觀</span><span class="sxs-lookup"><span data-stu-id="068d4-104">Overview of Configuration and Metadata</span></span>  

 <span data-ttu-id="068d4-105">本主題將討論下列工作，這些工作是「 [開發通道](developing-channels.md) 」工作清單中的選擇性專案1、2和4。</span><span class="sxs-lookup"><span data-stu-id="068d4-105">This topic discusses the following tasks, which are optional items 1, 2, and 4 in the [Developing Channels](developing-channels.md) task list.</span></span>  
  
- <span data-ttu-id="068d4-106">啟用繫結項目的組態檔支援。</span><span class="sxs-lookup"><span data-stu-id="068d4-106">Enabling configuration file support for a binding element.</span></span>  
  
- <span data-ttu-id="068d4-107">啟用繫結的組態檔支援。</span><span class="sxs-lookup"><span data-stu-id="068d4-107">Enabling configuration file support for a binding.</span></span>  
  
- <span data-ttu-id="068d4-108">匯出繫結項目的 WSDL 和原則判斷提示。</span><span class="sxs-lookup"><span data-stu-id="068d4-108">Exporting WSDL and policy assertions for a binding element.</span></span>  
  
- <span data-ttu-id="068d4-109">識別要插入並設定繫結或繫結項目的 WSDL 和原則判斷提示。</span><span class="sxs-lookup"><span data-stu-id="068d4-109">Identifying WSDL and policy assertions to insert and configure your binding or binding element.</span></span>  
  
 <span data-ttu-id="068d4-110">如需建立使用者定義系結和繫結項目的詳細資訊，請參閱分別 [建立 User-Defined](creating-user-defined-bindings.md) 系結和 [建立 BindingElement](creating-a-bindingelement.md)。</span><span class="sxs-lookup"><span data-stu-id="068d4-110">For information about creating user-defined bindings and binding elements, see [Creating User-Defined Bindings](creating-user-defined-bindings.md) and [Creating a BindingElement](creating-a-bindingelement.md), respectively.</span></span>  
  
## <a name="adding-configuration-support"></a><span data-ttu-id="068d4-111">新增組態支援</span><span class="sxs-lookup"><span data-stu-id="068d4-111">Adding Configuration Support</span></span>  

 <span data-ttu-id="068d4-112">若要啟用通道的組態檔支援，您必須實作兩個組態區段，其中一個是 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType>，它會啟用繫結項目的組態支援；而另一個是 <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=nameWithType> 和 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=nameWithType>，它會啟用繫結的組態支援。</span><span class="sxs-lookup"><span data-stu-id="068d4-112">To enable configuration file support for a channel, you must implement two configuration sections, <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType>, which enables configuration support for binding elements, and the <xref:System.ServiceModel.Configuration.StandardBindingElement?displayProperty=nameWithType> and <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602?displayProperty=nameWithType>, which enable configuration support for bindings.</span></span>  
  
 <span data-ttu-id="068d4-113">更簡單的方法是使用 [ConfigurationCodeGenerator](../samples/configurationcodegenerator.md) 範例工具，為您的系結和繫結項目產生設定程式碼。</span><span class="sxs-lookup"><span data-stu-id="068d4-113">An easier way to do this is to use the [ConfigurationCodeGenerator](../samples/configurationcodegenerator.md) sample tool to generate configuration code for your bindings and binding elements.</span></span>  
  
### <a name="extending-bindingelementextensionelement"></a><span data-ttu-id="068d4-114">延伸 BindingElementExtensionElement</span><span class="sxs-lookup"><span data-stu-id="068d4-114">Extending BindingElementExtensionElement</span></span>  

 <span data-ttu-id="068d4-115">下列範例程式碼取自 [Transport： UDP](../samples/transport-udp.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="068d4-115">The following example code is taken from the [Transport: UDP](../samples/transport-udp.md) sample.</span></span> <span data-ttu-id="068d4-116">`UdpTransportElement` 是 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>，它會將 `UdpTransportBindingElement` 公開至組態系統。</span><span class="sxs-lookup"><span data-stu-id="068d4-116">The `UdpTransportElement` is a <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> that exposes `UdpTransportBindingElement` to the configuration system.</span></span> <span data-ttu-id="068d4-117">範例會使用一些基本的覆寫，定義組態區段名稱、繫結項目的型別，以及如何建立繫結項目。</span><span class="sxs-lookup"><span data-stu-id="068d4-117">With a few basic overrides, the sample defines the configuration section name, the type of the binding element and how to create the binding element.</span></span> <span data-ttu-id="068d4-118">然後使用者可以在組態檔中登錄延伸區段，如同下列所示。</span><span class="sxs-lookup"><span data-stu-id="068d4-118">Users can then register the extension section in a configuration file as follows.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
      <add name="udpTransport" type="Microsoft.ServiceModel.Samples.UdpTransportElement, UdpTransport" />  
      </bindingElementExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="068d4-119">您可以從自訂繫結參考該延伸，以使用 UDP 做為傳輸方式。</span><span class="sxs-lookup"><span data-stu-id="068d4-119">The extension can be referenced from custom bindings to use UDP as the transport.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <customBinding>  
       <binding configurationName="UdpCustomBinding">  
         <udpTransport/>  
       </binding>  
      </customBinding>  
    </bindings>  
  </system.serviceModel>  
</configuration>  
```  
  
### <a name="adding-configuration-for-a-binding"></a><span data-ttu-id="068d4-120">新增繫結組態</span><span class="sxs-lookup"><span data-stu-id="068d4-120">Adding Configuration for a Binding</span></span>  

 <span data-ttu-id="068d4-121">區段 `SampleProfileUdpBindingCollectionElement` 是 <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602>，它會將 `SampleProfileUdpBinding` 公開至組態系統。</span><span class="sxs-lookup"><span data-stu-id="068d4-121">The section `SampleProfileUdpBindingCollectionElement` is a <xref:System.ServiceModel.Configuration.StandardBindingCollectionElement%602> that exposes `SampleProfileUdpBinding` to the configuration system.</span></span> <span data-ttu-id="068d4-122">大量實作會委派至衍生自 `SampleProfileUdpBindingConfigurationElement` 的 <xref:System.ServiceModel.Configuration.StandardBindingElement>。</span><span class="sxs-lookup"><span data-stu-id="068d4-122">The bulk of the implementation is delegated to the `SampleProfileUdpBindingConfigurationElement`, which derives from <xref:System.ServiceModel.Configuration.StandardBindingElement>.</span></span> <span data-ttu-id="068d4-123">的 `SampleProfileUdpBindingConfigurationElement` 屬性會對應至的屬性 `SampleProfileUdpBinding` ，以及要從系結對應的函式 `ConfigurationElement` 。</span><span class="sxs-lookup"><span data-stu-id="068d4-123">The `SampleProfileUdpBindingConfigurationElement` has properties that correspond to the properties on `SampleProfileUdpBinding`, and functions to map from the `ConfigurationElement` binding.</span></span> <span data-ttu-id="068d4-124">最後，在 `OnApplyConfiguration` 中會覆寫 `SampleProfileUdpBinding` 方法，如同下列範例程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="068d4-124">Finally, the `OnApplyConfiguration` method is overridden in the `SampleProfileUdpBinding`, as shown in the following sample code.</span></span>  
  
```csharp
protected override void OnApplyConfiguration(string configurationName)  
{  
            if (binding == null)  
                throw new ArgumentNullException("binding");  
  
            if (binding.GetType() != typeof(SampleProfileUdpBinding))  
            {  
                var expectedType = typeof(SampleProfileUdpBinding).AssemblyQualifiedName;
                var typePassedIn = binding.GetType().AssemblyQualifiedName;
                throw new ArgumentException($"Invalid type for binding. Expected type: {expectedType}. Type passed in: {typePassedIn}.");  
            }  
            SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;  
  
            udpBinding.OrderedSession = this.OrderedSession;  
            udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;  
            udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;  
            if (this.ClientBaseAddress != null)  
                   udpBinding.ClientBaseAddress = ClientBaseAddress;  
}  
```  
  
 <span data-ttu-id="068d4-125">若要使用組態系統註冊這個處理常式，請將下列區段新增至相關的組態檔。</span><span class="sxs-lookup"><span data-stu-id="068d4-125">To register this handler with the configuration system, add the following section to the relevant configuration file.</span></span>  
  
```xml  
<configuration>  
  <configSections>  
     <sectionGroup name="system.serviceModel">  
         <sectionGroup name="bindings">  
                 <section name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
         </sectionGroup>  
     </sectionGroup>  
  </configSections>  
</configuration>  
```  
  
 <span data-ttu-id="068d4-126">然後，您可以從 [設定] 區段參考它 [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) 。</span><span class="sxs-lookup"><span data-stu-id="068d4-126">It can then be referenced from the [\<system.serviceModel>](../../configure-apps/file-schema/wcf/system-servicemodel.md) configuration section.</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <endpoint configurationName="calculator"  
                address="soap.udp://localhost:8001/"
                bindingConfiguration="CalculatorServer"  
                binding="sampleProfileUdpBinding"
                contract= "Microsoft.ServiceModel.Samples.ICalculatorContract">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="adding-metadata-support-for-a-binding-element"></a><span data-ttu-id="068d4-127">新增繫結項目的中繼資料支援</span><span class="sxs-lookup"><span data-stu-id="068d4-127">Adding Metadata Support for a Binding Element</span></span>  

 <span data-ttu-id="068d4-128">若要將通道整合至中繼資料系統，通道必須同時支援匯入與匯出原則。</span><span class="sxs-lookup"><span data-stu-id="068d4-128">To integrate a channel into the metadata system, it must support both the import and export of policy.</span></span> <span data-ttu-id="068d4-129">這可讓諸如 [System.servicemodel 中繼資料公用程式工具 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md) 產生繫結項目的用戶端。</span><span class="sxs-lookup"><span data-stu-id="068d4-129">This allows tools such as [ServiceModel Metadata Utility Tool (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) to generate clients of the binding element.</span></span>  
  
### <a name="adding-wsdl-support"></a><span data-ttu-id="068d4-130">新增 WSDL 支援</span><span class="sxs-lookup"><span data-stu-id="068d4-130">Adding WSDL Support</span></span>  

 <span data-ttu-id="068d4-131">繫結中的傳輸繫結項目是負責匯出與匯入中繼資料中的定址資訊。</span><span class="sxs-lookup"><span data-stu-id="068d4-131">The transport binding element in a binding is responsible for exporting and importing addressing information in metadata.</span></span> <span data-ttu-id="068d4-132">當使用 SOAP 繫結時，傳輸繫結項目也應該匯出中繼資料中的正確傳輸 URI。</span><span class="sxs-lookup"><span data-stu-id="068d4-132">When using a SOAP binding, the transport binding element should also export a correct transport URI in metadata.</span></span> <span data-ttu-id="068d4-133">下列範例程式碼取自 [Transport： UDP](../samples/transport-udp.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="068d4-133">The following example code is taken from the [Transport: UDP](../samples/transport-udp.md) sample.</span></span>  
  
#### <a name="wsdl-export"></a><span data-ttu-id="068d4-134">WSDL 匯出</span><span class="sxs-lookup"><span data-stu-id="068d4-134">WSDL Export</span></span>  

 <span data-ttu-id="068d4-135">若要匯出定址資訊，會實 `UdpTransportBindingElement` 作為 <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> 介面。</span><span class="sxs-lookup"><span data-stu-id="068d4-135">To export addressing information, the `UdpTransportBindingElement` implements the <xref:System.ServiceModel.Description.IWsdlExportExtension?displayProperty=nameWithType> interface.</span></span> <span data-ttu-id="068d4-136"><xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=nameWithType> 方法會新增正確的定址資訊至 WSDL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="068d4-136">The <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A?displayProperty=nameWithType> method adds the correct addressing information to the WSDL port.</span></span>  
  
```csharp  
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 <span data-ttu-id="068d4-137">當端點使用 SOAP 繫結時，`UdpTransportBindingElement` 方法的 <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> 實作也會匯出傳輸 URI：</span><span class="sxs-lookup"><span data-stu-id="068d4-137">The `UdpTransportBindingElement` implementation of the <xref:System.ServiceModel.Description.IWsdlExportExtension.ExportEndpoint%2A> method also exports a transport URI when the endpoint uses a SOAP binding:</span></span>  
  
```csharp  
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### <a name="wsdl-import"></a><span data-ttu-id="068d4-138">WSDL 匯入</span><span class="sxs-lookup"><span data-stu-id="068d4-138">WSDL Import</span></span>  

 <span data-ttu-id="068d4-139">若要延伸 WSDL 匯入系統以處理位址匯入，請將下列組態新增至 Svcutil.exe 的組態檔中，如同 Svcutil.exe.config 檔中所示：</span><span class="sxs-lookup"><span data-stu-id="068d4-139">To extend the WSDL import system to handle importing the addresses, add the following configuration to the configuration file for Svcutil.exe as shown in the Svcutil.exe.config file:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <wsdlImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </wsdlImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="068d4-140">當執行 Svcutil.exe 時，有兩個選項可以讓 Svcutil.exe 載入 WSDL 匯入延伸：</span><span class="sxs-lookup"><span data-stu-id="068d4-140">When running Svcutil.exe, there are two options for getting Svcutil.exe to load the WSDL import extensions:</span></span>  
  
1. <span data-ttu-id="068d4-141">使用/SvcutilConfig 將 Svcutil.exe 指向設定檔： \<file> 。</span><span class="sxs-lookup"><span data-stu-id="068d4-141">Point Svcutil.exe to the configuration file using the /SvcutilConfig:\<file>.</span></span>  
  
2. <span data-ttu-id="068d4-142">將組態區段新增至與 Svcutil.exe 位於相同目錄的 Svcutil.exe.config 中。</span><span class="sxs-lookup"><span data-stu-id="068d4-142">Add the configuration section to Svcutil.exe.config in the same directory as Svcutil.exe.</span></span>  
  
 <span data-ttu-id="068d4-143">`UdpBindingElementImporter` 型別會實作 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> 介面。</span><span class="sxs-lookup"><span data-stu-id="068d4-143">The `UdpBindingElementImporter` type implements the <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> interface.</span></span> <span data-ttu-id="068d4-144">`ImportEndpoint` 方法會從 WSDL 連接埠匯入位址：</span><span class="sxs-lookup"><span data-stu-id="068d4-144">The `ImportEndpoint` method imports the address from the WSDL port:</span></span>  
  
```csharp  
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### <a name="adding-policy-support"></a><span data-ttu-id="068d4-145">新增原則支援</span><span class="sxs-lookup"><span data-stu-id="068d4-145">Adding Policy Support</span></span>  

 <span data-ttu-id="068d4-146">自訂繫結項目可以匯出服務端點之 WSDL 繫結的原則判斷提示，以表示該繫結項目的功能。</span><span class="sxs-lookup"><span data-stu-id="068d4-146">The custom binding element can export policy assertions in the WSDL binding for a service endpoint to express the capabilities of that binding element.</span></span> <span data-ttu-id="068d4-147">下列範例程式碼取自 [Transport： UDP](../samples/transport-udp.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="068d4-147">The following example code is taken from the [Transport: UDP](../samples/transport-udp.md) sample.</span></span>  
  
#### <a name="policy-export"></a><span data-ttu-id="068d4-148">原則匯出</span><span class="sxs-lookup"><span data-stu-id="068d4-148">Policy Export</span></span>  

 <span data-ttu-id="068d4-149">`UdpTransportBindingElement`型別 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> 可用於新增匯出原則的支援。</span><span class="sxs-lookup"><span data-stu-id="068d4-149">The `UdpTransportBindingElement` type implements <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> to add support for exporting policy.</span></span> <span data-ttu-id="068d4-150">因此，<xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> 會針對包含它的任何繫結，在產生原則時包含 `UdpTransportBindingElement`。</span><span class="sxs-lookup"><span data-stu-id="068d4-150">As a result, <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> includes `UdpTransportBindingElement` in the generation of policy for any binding that includes it.</span></span>  
  
 <span data-ttu-id="068d4-151">在 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=nameWithType> 中，新增 UDP 的判斷提示和其他判斷提示 (如果通道使用多點傳送模式)。</span><span class="sxs-lookup"><span data-stu-id="068d4-151">In <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A?displayProperty=nameWithType>, add an assertion for UDP and another assertion if the channel is in multicast mode.</span></span> <span data-ttu-id="068d4-152">這是因為多點傳送模式會影響通訊堆疊的建構方式，所以必須同時對兩端進行協調。</span><span class="sxs-lookup"><span data-stu-id="068d4-152">This is because multicast mode affects how the communication stack is constructed, and thus must be coordinated between both sides.</span></span>  
  
```csharp  
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.MulticastAssertion,     UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 <span data-ttu-id="068d4-153">因為自訂傳輸繫結項目會負責處理定址，所以 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> 上的 `UdpTransportBindingElement` 實作也必須處理適當之 WS-Addressing 原則判斷提示的匯出，以表示所使用的 WS-Addressing 版本。</span><span class="sxs-lookup"><span data-stu-id="068d4-153">Because custom transport binding elements are responsible for handling addressing, the <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType> implementation on the `UdpTransportBindingElement` must also handle exporting the appropriate WS-Addressing policy assertions to indicate the version of WS-Addressing being used.</span></span>  
  
```csharp  
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### <a name="policy-import"></a><span data-ttu-id="068d4-154">原則匯入</span><span class="sxs-lookup"><span data-stu-id="068d4-154">Policy Import</span></span>  

 <span data-ttu-id="068d4-155">若要延伸原則匯入系統，請將下列組態新增至 Svcutil.exe 的組態檔中，如同 Svcutil.exe.config 檔中所示：</span><span class="sxs-lookup"><span data-stu-id="068d4-155">To extend the policy import system, add the following configuration to the configuration file for Svcutil.exe as shown in the Svcutil.exe.config file:</span></span>  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <client>  
      <metadata>  
        <policyImporters>  
          <extension type=" Microsoft.ServiceModel.Samples.UdpBindingElementImporter, UdpTransport" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="068d4-156">然後從已註冊類別 (<xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType>) 實作 `UdpBindingElementImporter`。</span><span class="sxs-lookup"><span data-stu-id="068d4-156">Then we implement <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> from our registered class (`UdpBindingElementImporter`).</span></span> <span data-ttu-id="068d4-157">在 <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType> 中，檢視適當命名空間的判斷提示，然後處理用來產生傳輸的判斷提示，並且檢查其是否使用多點傳送。</span><span class="sxs-lookup"><span data-stu-id="068d4-157">In <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType>, examine the assertions in the appropriate namespace and process the ones for generating the transport and checking if it is multicast.</span></span> <span data-ttu-id="068d4-158">此外，從繫結判斷提示清單中移除匯入工具處理的判斷提示。</span><span class="sxs-lookup"><span data-stu-id="068d4-158">In addition, remove the assertions that the importer handles from the list of binding assertions.</span></span> <span data-ttu-id="068d4-159">同樣地，當執行 Svcutil.exe 時有兩個整合的選項：</span><span class="sxs-lookup"><span data-stu-id="068d4-159">Again, when running Svcutil.exe, there are two options for integration:</span></span>  
  
1. <span data-ttu-id="068d4-160">使用/SvcutilConfig 將 Svcutil.exe 指向設定檔： \<file> 。</span><span class="sxs-lookup"><span data-stu-id="068d4-160">Point Svcutil.exe to our configuration file using the /SvcutilConfig:\<file>.</span></span>  
  
2. <span data-ttu-id="068d4-161">將組態區段新增至與 Svcutil.exe 位於相同目錄的 Svcutil.exe.config 中。</span><span class="sxs-lookup"><span data-stu-id="068d4-161">Add the configuration section to Svcutil.exe.config in the same directory as Svcutil.exe.</span></span>  
  
### <a name="adding-a-custom-standard-binding-importer"></a><span data-ttu-id="068d4-162">新增自訂標準繫結匯入工具</span><span class="sxs-lookup"><span data-stu-id="068d4-162">Adding a Custom Standard Binding Importer</span></span>  

 <span data-ttu-id="068d4-163">根據預設，Svcutil.exe 和 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> 型別會識別與匯入系統提供的繫結。</span><span class="sxs-lookup"><span data-stu-id="068d4-163">Svcutil.exe and the <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> type, by default, recognize and import system-provided bindings.</span></span> <span data-ttu-id="068d4-164">否則，會將繫結程序當做 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> 執行個體匯入。</span><span class="sxs-lookup"><span data-stu-id="068d4-164">Otherwise, the binding gets imported as a <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> instance.</span></span> <span data-ttu-id="068d4-165">為了讓 Svcutil.exe 和 <xref:System.ServiceModel.Description.WsdlImporter> 能夠匯入 `SampleProfileUdpBinding`，`UdpBindingElementImporter` 也會當做自訂標準繫結匯入工具。</span><span class="sxs-lookup"><span data-stu-id="068d4-165">To enable Svcutil.exe and the <xref:System.ServiceModel.Description.WsdlImporter> to import the `SampleProfileUdpBinding` the `UdpBindingElementImporter` also acts as a custom standard binding importer.</span></span>  
  
 <span data-ttu-id="068d4-166">自訂標準系結匯入工具 `ImportEndpoint` 會在介面上執行方法 <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> ，以檢查 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> 從中繼資料匯入的實例，看看它是否可能已由特定的標準系結產生。</span><span class="sxs-lookup"><span data-stu-id="068d4-166">A custom standard binding importer implements the `ImportEndpoint` method on the <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> interface to examine the <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType> instance imported from metadata to see if it could have been generated by specific standard binding.</span></span>  
  
```csharp  
if (context.Endpoint.Binding is CustomBinding)  
{  
    Binding binding;  
    if (transportBindingElement is UdpTransportBindingElement)  
    {  
        //if TryCreate is true, the CustomBinding will be replace by a SampleProfileUdpBinding in the  
        //generated config file for better typed generation.  
        if (SampleProfileUdpBinding.TryCreate(bindingElements, out binding))  
        {  
            binding.Name = context.Endpoint.Binding.Name;  
            binding.Namespace = context.Endpoint.Binding.Namespace;  
            context.Endpoint.Binding = binding;  
        }  
    }  
}  
```  
  
 <span data-ttu-id="068d4-167">一般來說，實作自訂標準繫結程序匯入工具包含檢查已匯入之繫結程序項目的屬性，以驗證只有變更由標準繫結程序設定的屬性，而所有其他屬性都還是預設值。</span><span class="sxs-lookup"><span data-stu-id="068d4-167">Generally, implementing a custom standard binding importer involves checking the properties of the imported binding elements to verify that only properties that could have been set by the standard binding have changed and all other properties are their defaults.</span></span> <span data-ttu-id="068d4-168">實作標準繫結匯入工具的基本策略，是建立標準繫結的執行個體、從繫結項目將屬性傳播至標準繫結支援的標準繫結執行個體，然後比較標準繫結與已匯入繫結項目上的繫結項目。</span><span class="sxs-lookup"><span data-stu-id="068d4-168">A basic strategy for implementing a standard binding importer is to create an instance of the standard binding, propagate the properties from the binding elements to the standard binding instance that the standard binding supports, and the compare the binding elements from the standard binding with the imported binding elements.</span></span>
