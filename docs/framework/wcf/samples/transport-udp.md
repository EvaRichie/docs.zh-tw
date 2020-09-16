---
title: 傳輸：UDP
ms.date: 03/30/2017
ms.assetid: 738705de-ad3e-40e0-b363-90305bddb140
ms.openlocfilehash: dcf2d9896ab7c95101e224521174b54c88ca3fc2
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558994"
---
# <a name="transport-udp"></a>傳輸：UDP
UDP 傳輸範例示範如何將 UDP 單播和多播實作為自訂 Windows Communication Foundation (WCF) 傳輸。 此範例說明在 WCF 中建立自訂傳輸的建議程式，方法是使用通道架構並遵循 WCF 最佳作法。 建立自訂傳輸的步驟如下：  
  
1. 決定哪些通道 [訊息交換模式](#MessageExchangePatterns) (IOutputChannel、IInputChannel、IDuplexChannel、IRequestChannel 或 IReplyChannel) ChannelFactory 和 ChannelListener 將會支援。 然後決定是否要支援這些介面的工作階段變化。  
  
2. 建立支援「訊息交換模式」的通道處理站和接聽項。  
  
3. 確認已將所有網路特定例外狀況正規化為適當的 <xref:System.ServiceModel.CommunicationException> 衍生類別。  
  
4. 加入將 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 自訂傳輸新增至通道堆疊的元素。 如需詳細資訊，請參閱 [新增綁定](#AddingABindingElement)項。  
  
5. 新增繫結元素延伸區段，即可將新的繫結元素公開至組態系統。  
  
6. 新增中繼資料延伸，即可將功能傳達給其他端點。  
  
7. 新增繫結，此繫結會根據妥善定義的設定檔來預先設定繫結項目的堆疊。 如需詳細資訊，請參閱 [加入標準](#AddingAStandardBinding)系結。  
  
8. 新增繫結區段和繫結組態項目，即可將繫結公開至組態系統。 如需詳細資訊，請參閱 [新增設定支援](#AddingConfigurationSupport)。  
  
<a name="MessageExchangePatterns"></a>
## <a name="message-exchange-patterns"></a>訊息交換模式  
 撰寫自訂傳輸時的第一個步驟是決定傳輸所需要的「訊息交換模式」(Message Exchange Patterns，MEP)。 您可以從三個 MEP 中選擇：  
  
- 資料包 (IInputChannel/IOutputChannel)  
  
     當使用資料包 (Datagram) MEP 時，用戶端會使用「射後不理」(Fire and Forget) 交換來傳送訊息。 射後不理交換是一種需要以超出範圍之外的方式確認傳遞成功的交換。 訊息可能會在傳輸時遺失而永遠無法抵達服務。 即使傳送作業在用戶端已成功完成，也無法保證遠端端點已接收到該訊息。 資料包是訊息的基本建置組塊，您可以在資料包的最上層建立自己的通訊協定，其中包括可靠的通訊協定和安全的通訊協定。 用戶端資料包通道會實作 <xref:System.ServiceModel.Channels.IOutputChannel> 介面，服務資料包通道則會實作 <xref:System.ServiceModel.Channels.IInputChannel> 介面。  
  
- 要求-回應 (IRequestChannel/IReplyChannel)  
  
     在此 MEP 中，會傳送訊息，而且會接收回覆。 此模式是由要求-回應組合所構成。 遠端程序呼叫 (Remote Procedure Call，RPC) 與瀏覽器的 GET 就是要求-回應呼叫的例子。 這個模式又稱為「半雙工」。 在此 MEP 中，用戶端通道會實作 <xref:System.ServiceModel.Channels.IRequestChannel>，服務通道則會實作 <xref:System.ServiceModel.Channels.IReplyChannel>。  
  
- 雙工 (IDuplexChannel)  
  
     雙工 MEP 會允許用戶端傳送任意數目的訊息，並以任何順序接收這些訊息。 雙工 MEP 就像是電話交談，談話中說出的每個字都是一則訊息。 由於兩端都可以透過此種 MEP 來傳送和接收訊息，所以由用戶端和服務通道所實作的介面會是 <xref:System.ServiceModel.Channels.IDuplexChannel>。  
  
 上述的每個 MEP 都能支援「工作階段」(Session)。 工作階段感知通道提供的新增功能可以將通道中傳送及接收的所有訊息相互關聯。 因為要求與回覆相互關聯，「要求-回應」模式是一個獨立的兩訊息工作階段。 相較之下，支援工作階段的「要求-回應」模式，就意味著該通道上的所有要求/回應組合都是彼此相互關聯的。 如此一來，您總共有六種 MEP (資料包、要求-回應、雙工、搭配工作階段的資料包、搭配工作階段的要求-回應以及搭配工作階段的雙工) 可以選擇。  
  
> [!NOTE]
> 就 UDP 傳輸而言，唯一支援的 MEP 是「資料包」，因為 UDP 原本就是「射後不理」(Fire and Forget) 通訊協定。  
  
### <a name="the-icommunicationobject-and-the-wcf-object-lifecycle"></a>ICommunicationObject 和 WCF 物件生命週期  
 WCF 有一部通用的狀態機器，可用來管理物件的生命週期 <xref:System.ServiceModel.Channels.IChannel> ，例如 <xref:System.ServiceModel.Channels.IChannelFactory> 用於通訊的、和 <xref:System.ServiceModel.Channels.IChannelListener> 。 這些通訊物件可能呈現的狀態有五種。 這些狀態是由 <xref:System.ServiceModel.CommunicationState> 列舉表示，如下所述：  
  
- Created：這是 <xref:System.ServiceModel.ICommunicationObject> 在初次具現化 (Instantiated) 時的狀態。 在這個狀態下不會發生任何輸入/輸出 (I/O)。  
  
- Opening：呼叫 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 時物件會轉換至此狀態。 此時會將屬性設為不變，並且可以開始輸入/輸出。 只有從 Created 狀態轉變過來，這種轉換才算有效。  
  
- Opened：當開啟處理序完成時，物件會轉換至此狀態。 只有從 Opening 狀態轉變過來，這種轉換才算有效。 此時，物件完全無法進行傳輸。  
  
- Closing：當呼叫 <xref:System.ServiceModel.ICommunicationObject.Close%2A> 以執行非失誤性關機時，物件會轉換至此狀態。 只有從 Opened 狀態轉變過來，這種轉換才算有效。  
  
- Closed：在 Closed 狀態中，物件就不再可供使用。 一般來說，大部分組態仍然可供存取以便檢查，但是無法進行任何通訊。 這種狀態相當於正在處置。  
  
- Faulted：在 Faulted 狀態中，物件可供存取以便檢查，但是無法供使用。 當發生無法修復的錯誤時，物件會轉換至此狀態。 此狀態唯一有效的轉換為 `Closed` 狀態。  
  
 每個狀態轉換都會引發一些事件。 <xref:System.ServiceModel.ICommunicationObject.Abort%2A> 方法可在任何時間加以呼叫，讓物件立即從目前的狀態轉換為 Closed 狀態。 呼叫 <xref:System.ServiceModel.ICommunicationObject.Abort%2A> 會終止任何未完成的工作。  
  
<a name="ChannelAndChannelListener"></a>
## <a name="channel-factory-and-channel-listener"></a>通道處理站和通道接聽項  
 撰寫自訂傳輸的下一個步驟是，建立用戶端通道的 <xref:System.ServiceModel.Channels.IChannelFactory> 實作以及服務通道的 <xref:System.ServiceModel.Channels.IChannelListener> 實作。 通道層會使用建構通道所需的處理站模式。 WCF 提供此進程的基類協助程式。  
  
- <xref:System.ServiceModel.Channels.CommunicationObject> 類別會實作 <xref:System.ServiceModel.ICommunicationObject>，並強制執行先前在步驟 2 中所述的狀態機器。

- <xref:System.ServiceModel.Channels.ChannelManagerBase> 類別會實作 <xref:System.ServiceModel.Channels.CommunicationObject>，並為 <xref:System.ServiceModel.Channels.ChannelFactoryBase> 和 <xref:System.ServiceModel.Channels.ChannelListenerBase> 提供統一的基底類別。 <xref:System.ServiceModel.Channels.ChannelManagerBase> 類別可以和 <xref:System.ServiceModel.Channels.ChannelBase> 一起運作，而後者是實作 <xref:System.ServiceModel.Channels.IChannel> 的基底類別。  
  
- <xref:System.ServiceModel.Channels.ChannelFactoryBase>類別會 <xref:System.ServiceModel.Channels.ChannelManagerBase> 執行並 <xref:System.ServiceModel.Channels.IChannelFactory> 將多載合併 `CreateChannel` 成一個 `OnCreateChannel` 抽象方法。  
  
- <xref:System.ServiceModel.Channels.ChannelListenerBase> 類別會實作 <xref:System.ServiceModel.Channels.IChannelListener>。 它會負責基礎的狀態管理。  
  
 在這個範例中，處理站的實作包含在 UdpChannelFactory.cs 中，而接聽項的實作則包含在 UdpChannelListener.cs 中。 <xref:System.ServiceModel.Channels.IChannel> 的實作是在 UdpOutputChannel.cs 和 UdpInputChannel.cs 中。  
  
### <a name="the-udp-channel-factory"></a>UDP 通道處理站  
 `UdpChannelFactory` 是衍生自 <xref:System.ServiceModel.Channels.ChannelFactoryBase>。 範例會覆寫 <xref:System.ServiceModel.Channels.ChannelFactoryBase.GetProperty%2A>，以提供訊息編碼器之訊息版本的存取權。 範例也會覆寫 <xref:System.ServiceModel.Channels.ChannelFactoryBase.OnClose%2A>，以便在狀態機器進行轉換時卸除 <xref:System.ServiceModel.Channels.BufferManager> 的執行個體。  
  
#### <a name="the-udp-output-channel"></a>UDP 輸出通道  
 `UdpOutputChannel` 會實作 <xref:System.ServiceModel.Channels.IOutputChannel>。 建構函式會驗證引數，並根據傳進的 <xref:System.Net.EndPoint> 建構目的地 <xref:System.ServiceModel.EndpointAddress> 物件。  
  
```csharp
this.socket = new Socket(this.remoteEndPoint.AddressFamily, SocketType.Dgram, ProtocolType.Udp);  
```  
  
 可以依正常程序或非正常程序關閉通道。 如果依正常程序關閉通道，將會關閉通訊端，並且會呼叫基底類別 `OnClose` 方法。 如果因此發生例外狀況，則基礎結構會呼叫 `Abort`，確保已清除通道。  
  
```csharp
this.socket.Close(0);  
```  
  
 接著，我們會採用 `Send()` 和 `BeginSend()` / `EndSend()` 。 這分成兩個主要區段。 首先，將訊息序列化為位元組陣列。  
  
```csharp
ArraySegment<byte> messageBuffer = EncodeMessage(message);  
```  
  
 然後在網路上傳送產生的資料。  
  
```csharp
this.socket.SendTo(messageBuffer.Array, messageBuffer.Offset, messageBuffer.Count, SocketFlags.None, this.remoteEndPoint);  
```  
  
### <a name="the-udpchannellistener"></a>UdpChannelListener  
 `UdpChannelListener`範例所衍生的會衍生自 <xref:System.ServiceModel.Channels.ChannelListenerBase> 類別。 它會使用單一 UDP 通訊端來接收資料包。 `OnOpen` 方法會透過非同步迴圈的 UDP 通訊端來接收資料， 然後透過下列「訊息編碼架構」將資料轉換為訊息。  
  
```csharp
message = MessageEncoderFactory.Encoder.ReadMessage(new ArraySegment<byte>(buffer, 0, count), bufferManager);  
```  
  
 由於相同的資料包通道代表來自幾個來源的訊息，因此 `UdpChannelListener` 是單一接聽程式。 每次都有一個與此接聽程式相關聯的作用中 <xref:System.ServiceModel.Channels.IChannel> 。 只有當 `AcceptChannel` 方法所傳回的通道被接著處理後，範例才會產生另一個通道。 收到訊息時，就會將它加入此單一通道佇列中。  
  
#### <a name="udpinputchannel"></a>UdpInputChannel  
 `UdpInputChannel` 類別會實作 `IInputChannel`。 它包含由 `UdpChannelListener` 通訊端所填入的傳入訊息佇列。 這些訊息佇列會由 `IInputChannel.Receive` 方法加以清除。  
  
<a name="AddingABindingElement"></a>
## <a name="adding-a-binding-element"></a>新增繫結項目  
 既然建置了處理站和通道，就必須透過繫結公開至 ServiceModel 執行階段。 繫結是繫結項目的集合，表示與服務位址相關聯的通訊堆疊。 堆疊中的每個專案都以 [\<binding>](../../configure-apps/file-schema/wcf/bindings.md) 元素表示。  
  
 在此範例中，繫結項目為 `UdpTransportBindingElement`，其衍生自 <xref:System.ServiceModel.Channels.TransportBindingElement>。 它會覆寫下列方法來建置與繫結關聯的處理站。  
  
```csharp
public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
{  
    return (IChannelFactory<TChannel>)(object)new UdpChannelFactory(this, context);  
}  
  
public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
{  
    return (IChannelListener<TChannel>)(object)new UdpChannelListener(this, context);  
}  
```  
  
 它還包含可以用來複製 `BindingElement` 以及傳回我們的結構描述 (soap.udp) 的成員。  
  
## <a name="adding-metadata-support-for-a-transport-binding-element"></a>新增傳輸繫結項目的中繼資料支援  
 若要將傳輸整合到中繼資料系統中，必須同時支援匯入與匯出原則。 這可讓我們透過 [System.servicemodel 中繼資料公用程式工具 ( # A0) ](../servicemodel-metadata-utility-tool-svcutil-exe.md)來產生系結的用戶端。  
  
### <a name="adding-wsdl-support"></a>新增 WSDL 支援  
 繫結中的傳輸繫結項目是負責匯出與匯入中繼資料中的定址資訊。 當使用 SOAP 繫結時，傳輸繫結項目也應該匯出中繼資料中的正確傳輸 URI。  
  
#### <a name="wsdl-export"></a>WSDL 匯出  
 若要匯出定址資訊，`UdpTransportBindingElement` 會實作 `IWsdlExportExtension` 介面。 `ExportEndpoint` 方法會新增正確的定址資訊至 WSDL 連接埠。  
  
```csharp
if (context.WsdlPort != null)  
{  
    AddAddressToWsdlPort(context.WsdlPort, context.Endpoint.Address, encodingBindingElement.MessageVersion.Addressing);  
}  
```  
  
 當端點使用 SOAP 繫結時，`UdpTransportBindingElement` 方法的 `ExportEndpoint` 實作也會匯出傳輸 URI。  
  
```csharp
WsdlNS.SoapBinding soapBinding = GetSoapBinding(context, exporter);  
if (soapBinding != null)  
{  
    soapBinding.Transport = UdpPolicyStrings.UdpNamespace;  
}  
```  
  
#### <a name="wsdl-import"></a>WSDL 匯入  
 若要延伸 WSDL 匯入系統以處理位址匯入，就必須將下列組態新增至 Svcutil.exe 的組態檔中，如 Svcutil.exe.config 檔案所示。  
  
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
  
 當執行 Svcutil.exe 時，有兩個選項可以讓 Svcutil.exe 載入 WSDL 匯入延伸：  
  
1. 使用/SvcutilConfig 將 Svcutil.exe 指向設定檔： \<file> 。  
  
2. 將組態區段新增至與 Svcutil.exe 位於相同目錄的 Svcutil.exe.config 中。  
  
 `UdpBindingElementImporter` 型別會實作 `IWsdlImportExtension` 介面。 `ImportEndpoint` 方法會從 WSDL 連接埠匯入位址。  
  
```csharp
BindingElementCollection bindingElements = context.Endpoint.Binding.CreateBindingElements();  
TransportBindingElement transportBindingElement = bindingElements.Find<TransportBindingElement>();  
if (transportBindingElement is UdpTransportBindingElement)  
{  
    ImportAddress(context);  
}  
```  
  
### <a name="adding-policy-support"></a>新增原則支援  
 自訂繫結項目可以匯出服務端點之 WSDL 繫結的原則判斷提示，以表示該繫結項目的功能。  
  
#### <a name="policy-export"></a>原則匯出  
 `UdpTransportBindingElement`型別 `IPolicyExportExtension` 可用於新增匯出原則的支援。 因此，`System.ServiceModel.MetadataExporter` 會針對包含它的任何繫結，在產生原則時包含 `UdpTransportBindingElement`。  
  
 在 `IPolicyExportExtension.ExportPolicy` 中，我們會新增 UDP 的判斷提示以及其他判斷提示 (如果使用多點傳送模式)。 這是因為多點傳送模式會影響通訊堆疊的建構方式，所以必須同時對兩端進行協調。  
  
```csharp
ICollection<XmlElement> bindingAssertions = context.GetBindingAssertions();  
XmlDocument xmlDocument = new XmlDocument();  
bindingAssertions.Add(xmlDocument.CreateElement(  
UdpPolicyStrings.Prefix, UdpPolicyStrings.TransportAssertion, UdpPolicyStrings.UdpNamespace));  
if (Multicast)  
{  
    bindingAssertions.Add(xmlDocument.CreateElement(
        UdpPolicyStrings.Prefix,
        UdpPolicyStrings.MulticastAssertion,
        UdpPolicyStrings.UdpNamespace));  
}  
```  
  
 因為自訂傳輸繫結項目會負責處理定址，所以 `IPolicyExportExtension` 上的 `UdpTransportBindingElement` 實作也必須處理適當之 WS-Addressing 原則判斷提示的匯出，以表示所使用的 WS-Addressing 版本。  
  
```csharp
AddWSAddressingAssertion(context, encodingBindingElement.MessageVersion.Addressing);  
```  
  
#### <a name="policy-import"></a>原則匯入  
 若要延伸原則匯入系統，就必須將下列組態新增至 Svcutil.exe 的組態檔中，如 Svcutil.exe.config 檔案所示。  
  
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
  
 然後從已註冊類別 (`IPolicyImporterExtension`) 實作 `UdpBindingElementImporter`。 在 `ImportPolicy()` 中，查看命名空間中的判斷提示，然後處理用來產生傳輸的判斷提示，並且檢查其是否使用多點傳送。 此外，從繫結判斷提示清單中移除匯入所處理的判斷提示。 同樣地，當執行 Svcutil.exe 時有兩個整合的選項：  
  
1. 使用/SvcutilConfig 將 Svcutil.exe 指向設定檔： \<file> 。  
  
2. 將組態區段新增至與 Svcutil.exe 位於相同目錄的 Svcutil.exe.config 中。  
  
<a name="AddingAStandardBinding"></a>
## <a name="adding-a-standard-binding"></a>新增標準繫結  
 可以透過下列兩種方式使用繫結項目：  
  
- 透過自訂繫結：自訂繫結允許使用者根據任意一組繫結項目，建立自己的繫結。  
  
- 使用系統提供的繫結，其中包含我們的繫結元素。 WCF 提供一些系統定義的系結，例如 `BasicHttpBinding` 、 `NetTcpBinding` 和 `WsHttpBinding` 。 每個這個繫結都會與妥善定義的設定檔相關聯。  
  
 範例會在衍生自 `SampleProfileUdpBinding` 的 <xref:System.ServiceModel.Channels.Binding> 中實作設定檔繫結。 `SampleProfileUdpBinding` 中最多包含四個繫結項目：`UdpTransportBindingElement`、`TextMessageEncodingBindingElement CompositeDuplexBindingElement` 和 `ReliableSessionBindingElement`。  
  
```csharp
public override BindingElementCollection CreateBindingElements()  
{
    BindingElementCollection bindingElements = new BindingElementCollection();  
    if (ReliableSessionEnabled)  
    {  
        bindingElements.Add(session);  
        bindingElements.Add(compositeDuplex);  
    }  
    bindingElements.Add(encoding);  
    bindingElements.Add(transport);  
    return bindingElements.Clone();  
}  
```  
  
### <a name="adding-a-custom-standard-binding-importer"></a>新增自訂標準繫結匯入工具  
 根據預設，Svcutil.exe 和 `WsdlImporter` 型別會辨識並匯入系統定義的繫結。 否則，會將繫結程序當做 `CustomBinding` 執行個體匯入。 為了讓 Svcutil.exe 和 `WsdlImporter` 能夠匯入 `SampleProfileUdpBinding`，`UdpBindingElementImporter` 也會當做自訂標準繫結匯入工具。  
  
 自訂標準繫結匯入工具會實作 `ImportEndpoint` 介面上的 `IWsdlImportExtension` 方法，檢視從中繼資料匯入的 `CustomBinding` 執行個體，以檢查特定標準繫結是否已產生該執行個體。  
  
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
  
 一般來說，實作自訂標準繫結程序匯入工具包含檢查已匯入之繫結程序項目的屬性，以驗證只有變更由標準繫結程序設定的屬性，而所有其他屬性都還是預設值。 實作標準繫結匯入工具的基本策略，是建立標準繫結的執行個體、從繫結項目將屬性傳播至標準繫結支援的標準繫結執行個體，然後比較標準繫結與已匯入繫結項目上的繫結項目。  
  
<a name="AddingConfigurationSupport"></a>
## <a name="adding-configuration-support"></a>新增組態支援  
 若要透過組態公開傳輸，就必須實作兩個組態區段。 第一個是 `BindingElementExtensionElement` 的 `UdpTransportBindingElement`。 使用這個區段，`CustomBinding` 的實作就可以參考繫結項目。 第二個是 `Configuration` 的 `SampleProfileUdpBinding`。  
  
### <a name="binding-element-extension-element"></a>繫結項目延伸項目  
 區段 `UdpTransportElement` 是 `BindingElementExtensionElement`，它會將 `UdpTransportBindingElement` 公開至組態系統。 藉由一些基本的覆寫，範例定義了組態區段名稱、繫結項目型別和建立繫結項目的方式。 因此，可以接著在組態檔中登錄延伸區段，如下列程式碼所示。  
  
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
  
 您可以從自訂繫結參考該延伸，以使用 UDP 做為傳輸方式。  
  
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
  
### <a name="binding-section"></a>繫結區段  
 區段 `SampleProfileUdpBindingCollectionElement` 是 `StandardBindingCollectionElement`，它會將 `SampleProfileUdpBinding` 公開至組態系統。 大量實作會委派至衍生自 `SampleProfileUdpBindingConfigurationElement` 的 `StandardBindingElement`。 的 `SampleProfileUdpBindingConfigurationElement` 屬性會對應至的屬性 `SampleProfileUdpBinding` ，以及要從系結對應的函式 `ConfigurationElement` 。 最後，在 `OnApplyConfiguration` 中覆寫 `SampleProfileUdpBinding` 方法，如下列範例程式碼所示。  
  
```csharp
protected override void OnApplyConfiguration(string configurationName)  
{  
    if (binding == null)
        throw new ArgumentNullException("binding");

    if (binding.GetType() != typeof(SampleProfileUdpBinding))
    {
        throw new ArgumentException(string.Format(CultureInfo.CurrentCulture,
            "Invalid type for binding. Expected type: {0}. Type passed in: {1}.",
            typeof(SampleProfileUdpBinding).AssemblyQualifiedName,
            binding.GetType().AssemblyQualifiedName));
    }
    SampleProfileUdpBinding udpBinding = (SampleProfileUdpBinding)binding;

    udpBinding.OrderedSession = this.OrderedSession;
    udpBinding.ReliableSessionEnabled = this.ReliableSessionEnabled;
    udpBinding.SessionInactivityTimeout = this.SessionInactivityTimeout;
    if (this.ClientBaseAddress != null)
        udpBinding.ClientBaseAddress = ClientBaseAddress;
}
```  
  
 為了使用組態系統註冊這個處理常式，範例將下列區段新增至相關的組態檔。  
  
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
  
 因此，可以從 serviceModel 組態區段參考它。  
  
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
  
## <a name="the-udp-test-service-and-client"></a>UDP 測試服務和用戶端  
 您可以在 UdpTestService 和 UdpTestClient 目錄中，找到使用此範例傳輸的測試程式碼。 服務程式碼由兩項測試組成：其中一項測試會從程式碼設定繫結和端點，而另一項則是透過組態進行設定。 這兩項測試都會使用兩個端點。 一個端點會使用 `SampleUdpProfileBinding` [\<reliableSession>](/previous-versions/ms731375(v=vs.90)) 將設定為的 `true` 。 另一個端點會使用包含 `UdpTransportBindingElement` 的自訂繫結程序。 這相當於使用 `SampleUdpProfileBinding` [\<reliableSession>](/previous-versions/ms731375(v=vs.90)) 設定為的 `false` 。 這兩項測試都會建立服務、為每個繫結新增端點、開啟服務，然後等候使用者按下 ENTER，再關閉服務。  
  
 當啟動服務的測試應用程式時，您應該會看見下列輸出。  
  
```console
Testing Udp From Code.  
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
```  
  
 此時，您就可以對已發行的端點執行測試用戶端應用程式。 用戶端測試應用程式會為每個端點建立用戶端，並傳送五則訊息給每個端點。 下列是用戶端的輸出。  
  
```console
Testing Udp From Imported Files Generated By SvcUtil.  
0  
3  
6  
9  
12  
Press <ENTER> to complete test.  
```  
  
 下列是服務上的完整輸出。  
  
```console
Service is started from code...  
Press <ENTER> to terminate the service and start service from config...  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
Hello, world!  
   adding 0 + 0  
   adding 1 + 2  
   adding 2 + 4  
   adding 3 + 6  
   adding 4 + 8  
```  
  
 若要使用組態對已發行的端點執行用戶端應用程式，請在服務上按下 ENTER，然後再執行測試用戶端一次。 您應該會在服務上看見下列輸出。  
  
```console
Testing Udp From Config.  
Service is started from config...  
Press <ENTER> to terminate the service and exit...  
```  
  
 再次執行用戶端，會產生與前面相同的結果。  
  
 若要使用 Svcutil.exe 重新產生用戶端程式碼和組態，請啟動服務應用程式，然後從範例的根目錄執行下列 Svcutil.exe。  
  
```console
svcutil http://localhost:8000/udpsample/ /reference:UdpTransport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
```  
  
 請注意，Svcutil.exe 不會為 `SampleProfileUdpBinding` 產生繫結延伸組態，所以您必須以手動方式新增。  
  
```xml
<configuration>  
  <system.serviceModel>
    <extensions>  
      <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
      <bindingExtensions>  
        <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
      </bindingExtensions>  
    </extensions>  
  </system.serviceModel>  
</configuration>  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 若要建立方案，請依照 [建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。  
  
2. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
3. 請參閱前面的「UDP 測試服務和用戶端」一節。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transport\Udp`
