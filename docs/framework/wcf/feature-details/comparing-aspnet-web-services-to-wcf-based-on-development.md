---
title: 根據開發情況比較 ASP.NET Web 服務與 WCF
ms.date: 03/30/2017
ms.assetid: f362d00e-ce82-484f-9d4f-27e579d5c320
ms.openlocfilehash: c6e83bb234751dc477776f0fa540ffa8688dc667
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597588"
---
# <a name="comparing-aspnet-web-services-to-wcf-based-on-development"></a>根據開發情況比較 ASP.NET Web 服務與 WCF

Windows Communication Foundation （WCF）具有 ASP.NET 相容性模式選項，可讓 WCF 應用程式進行程式設計和設定，例如 ASP.NET Web 服務，以及模擬其行為。 下列各節將根據使用這兩種技術開發應用程式所需的功能，來比較 ASP.NET Web 服務和 WCF。

## <a name="data-representation"></a>資料表示

使用 ASP.NET 開發 Web 服務時，通常一開始會先定義服務所要使用的任何複雜資料型別。 ASP.NET 會依賴 <xref:System.Xml.Serialization.XmlSerializer> 將 .NET Framework 型別表示的資料轉譯為 XML 以便與服務進行來回傳輸，以及將接收到的 XML 資料轉譯為 .NET Framework 物件。 定義 ASP.NET 服務所要使用的複雜資料型別時需要定義 .NET Framework 類別，這個類別可由 <xref:System.Xml.Serialization.XmlSerializer> 序列化成 XML 以及從 XML 還原序列化。 這種類別可手動撰寫，或是使用命令列 XML 結構描述/資料型別支援公用程式 xsd.exe，從 XML 結構描述中的型別定義產生。

下列清單列出在定義可由 <xref:System.Xml.Serialization.XmlSerializer> 序列化成 XML 以及從 XML 還原序列化的 .NET Framework 類別時，必須瞭解的主要問題：

- 只有 .NET Framework 物件的公用欄位和屬性會轉譯為 XML。

- 集合類別 (Collection Class) 的執行個體只有在類別實作 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.ICollection> 介面時，才能序列化為 XML。

- 實作 <xref:System.Collections.IDictionary> 介面的類別 (例如 <xref:System.Collections.Hashtable>) 並不能序列化為 XML。

- 絕大多數在 <xref:System.Xml.Serialization> 命名空間 (Namespace) 中的屬性型別可以新增至 .NET Framework 類別及其成員，以控制如何使用 XML 來表示此類別執行個體。

WCF 應用程式開發通常也是以複雜類型的定義為開頭。 您可以使用 WCF 做為與 ASP.NET Web 服務相同的 .NET Framework 類型。

WCF <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 可以加入至 .NET Framework 類型，以指出類型的實例要序列化為 XML，以及要序列化之類型的特定欄位或屬性，如下列範例程式碼所示。

```csharp
//Example One:
[DataContract]
public class LineItem
{
    [DataMember]
    public string ItemNumber;
    [DataMember]
    public decimal Quantity;
    [DataMember]
    public decimal UnitPrice;
}

//Example Two:
public class LineItem
{
    [DataMember]
    private string itemNumber;
    [DataMember]
    private decimal quantity;
    [DataMember]
    private decimal unitPrice;

    public string ItemNumber
    {
      get
      {
          return this.itemNumber;
      }

      set
      {
          this.itemNumber = value;
      }
    }

    public decimal Quantity
    {
        get
        {
            return this.quantity;
        }

        set
        {
            this.quantity = value;
        }
    }

    public decimal UnitPrice
    {
      get
      {
          return this.unitPrice;
      }

      set
      {
          this.unitPrice = value;
      }
    }
}

//Example Three:
public class LineItem
{
     private string itemNumber;
     private decimal quantity;
     private decimal unitPrice;

     [DataMember]
     public string ItemNumber
     {
       get
       {
          return this.itemNumber;
       }

       set
       {
           this.itemNumber = value;
       }
     }

     [DataMember]
     public decimal Quantity
     {
          get
          {
              return this.quantity;
          }

          set
          {
             this.quantity = value;
          }
     }

     [DataMember]
     public decimal UnitPrice
     {
          get
          {
              return this.unitPrice;
          }

          set
          {
              this.unitPrice = value;
          }
     }
}
```

<xref:System.Runtime.Serialization.DataContractAttribute> 表示要序列化型別的零或多個欄位或屬性，而 <xref:System.Runtime.Serialization.DataMemberAttribute> 則表示會序列化特定的欄位或屬性。 <xref:System.Runtime.Serialization.DataContractAttribute> 可以套用於類別或結構。 <xref:System.Runtime.Serialization.DataMemberAttribute> 可以套用至欄位或屬性 (Property)，而套用此屬性 (Attribute) 的欄位和屬性 (Property) 可以是公用或私用。 套用至它們的類型實例在 <xref:System.Runtime.Serialization.DataContractAttribute> WCF 中稱為「資料合約」（data contract）。 這些資料合約會使用 <xref:System.Runtime.Serialization.DataContractSerializer> 來序列化為 XML。

下列為使用 <xref:System.Runtime.Serialization.DataContractSerializer> 和使用 <xref:System.Xml.Serialization.XmlSerializer> 之間的重要差異清單，以及 <xref:System.Xml.Serialization> 命名空間的各種屬性。

- <xref:System.Xml.Serialization.XmlSerializer> 和 <xref:System.Xml.Serialization> 命名空間屬性是設計用來讓您將 .NET Framework 型別對應至 XML 結構描述中任何有效型別，因此，它們會就控制如何使用 XML 來表示型別方面提供極為精密的控制。 <xref:System.Runtime.Serialization.DataContractSerializer>、<xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 對於控制如何使用 XML 來表示型別則提供較少的控制。 您只能指定在採用 XML 時用來表示型別及其欄位或屬性的命名空間和名稱，以及指定這些欄位和屬性在 XML 中的顯示順序：

  ```csharp
  [DataContract(
  Namespace="urn:Contoso:2006:January:29",
  Name="LineItem")]
  public class LineItem
  {
        [DataMember(Name="ItemNumber",IsRequired=true,Order=0)]
        public string itemNumber;
        [DataMember(Name="Quantity",IsRequired=false,Order = 1)]
        public decimal quantity;
        [DataMember(Name="Price",IsRequired=false,Order = 2)]
        public decimal unitPrice;
  }
  ```

  有關用來表示 .NET 型別之 XML 結構的其他任何項目，都由 <xref:System.Runtime.Serialization.DataContractSerializer> 決定。

- 透過這樣對如何使用 XML 來表示型別不允許太多控制的方式，使得 <xref:System.Runtime.Serialization.DataContractSerializer> 非常易於預測序列化 (Serialization) 處理序 (Process)，也因此更容易進行最佳化。 <xref:System.Runtime.Serialization.DataContractSerializer> 設計的實質優點是提供更高的效能 (約提升 10% 的效能)。

- 搭配 <xref:System.Xml.Serialization.XmlSerializer> 使用的屬性並不會指出要將型別的哪些欄位或屬性序列化為 XML，不過搭配 <xref:System.Runtime.Serialization.DataMemberAttribute> 使用的 <xref:System.Runtime.Serialization.DataContractSerializer> 會明確指示哪些欄位或屬性會進行序列化。 因此，資料合約為應用程式所要傳送及接收之資料結構的明確合約。

- <xref:System.Xml.Serialization.XmlSerializer> 只能將 .NET 物件的 Public 成員轉譯為 XML，而 <xref:System.Runtime.Serialization.DataContractSerializer> 則不論這些物件成員的存取修飾詞為何都會將這些成員轉譯為 XML。

- 這樣會導致其能夠將型別的非 Public 成員序列化為 XML，進而使得 <xref:System.Runtime.Serialization.DataContractSerializer> 在可以處理序列化為 XML 的各種 .NET 型別上具有較少限制。 特別值得一提的是，它可以將像是實作 <xref:System.Collections.Hashtable> 介面的 <xref:System.Collections.IDictionary> 的型別轉譯為 XML 型別。 <xref:System.Runtime.Serialization.DataContractSerializer> 很有可能可以在不用修改型別定義或為型別開發包裝函式的情況下，將任何預先存在的 .NET 型別執行個體轉譯為 XML。

- 對於 <xref:System.Runtime.Serialization.DataContractSerializer> 來說，能夠存取型別的非 Public 成員能力會造成它需要完全信任，而 <xref:System.Xml.Serialization.XmlSerializer> 則不需要。 完全信任程式碼存取權限可讓您完整存取電腦上的所有資源，並使用程式碼執行時所用的認證來存取。 此選項應謹慎使用，因為完全信任的程式碼會存取您電腦上的所有資源。

- <xref:System.Runtime.Serialization.DataContractSerializer> 併入了一些版本控制功能的支援：

  - <xref:System.Runtime.Serialization.DataMemberAttribute> 具有 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 屬性，這個屬性可以指派 false 的值以表示新增到資料合約新版本的成員 (沒有出現在舊版本中)，這樣便可以讓擁有新版合約的應用程式可以處理舊版合約。

  - 藉由讓資料合約實作 <xref:System.Runtime.Serialization.IExtensibleDataObject> 介面，便可讓 <xref:System.Runtime.Serialization.DataContractSerializer> 將定義於新版資料合約中的成員透過擁有舊版合約的應用程式傳遞。

儘管存在以上這些差異，但根據預設，只要 XML 的命名空間已明確定義，<xref:System.Xml.Serialization.XmlSerializer> 序列化型別的目標 XML 與 <xref:System.Runtime.Serialization.DataContractSerializer> 序列化型別的目標 XML 在語意上是完全相同的。 下列類別具有可與這兩個序列化程式一起使用的屬性，會依照和轉譯成以語義相同的 XML <xref:System.Xml.Serialization.XmlSerializer> <xref:System.Runtime.Serialization.DataContractAttribute> ：

```csharp
[Serializable]
[XmlRoot(Namespace="urn:Contoso:2006:January:29")]
[DataContract(Namespace="urn:Contoso:2006:January:29")]
public class LineItem
{
     [DataMember]
     public string ItemNumber;
     [DataMember]
     public decimal Quantity;
     [DataMember]
     public decimal UnitPrice;
}
```

Windows 軟體發展工具組（SDK）包含稱為「 [System.servicemodel 中繼資料公用程式工具」（Svcutil .exe）](../servicemodel-metadata-utility-tool-svcutil-exe.md)的命令列工具。 如同搭配 ASP.NET Web 服務使用的 xsd.exe 工具，Svcutil 可以從 XML 架構產生 .NET 資料類型的定義。 如果 <xref:System.Runtime.Serialization.DataContractSerializer> 可以發出採用 XML 結構描述定義格式的 XML，型別就是資料合約，否則這些型別會使用 <xref:System.Xml.Serialization.XmlSerializer> 來進行序列化。 Svcutil 也可以使用參數，從資料合約產生 XML 架構。 `dataContractOnly`

> [!NOTE]
> 雖然 ASP.NET Web 服務會使用 <xref:System.Xml.Serialization.XmlSerializer> ，而 wcf ASP.NET 相容性模式讓 wcf 服務模擬 ASP.NET Web 服務的行為，但 ASP.NET 相容性選項不會將一個限制為使用 <xref:System.Xml.Serialization.XmlSerializer> 。 使用者還是可以搭配 ASP.NET 相容性模式中的執行服務使用 <xref:System.Runtime.Serialization.DataContractSerializer>。

## <a name="service-development"></a>服務開發

若要使用 ASP.NET 開發服務，習慣上會將 <xref:System.Web.Services.WebService> 屬性新增至類別，以及將 <xref:System.Web.Services.WebMethodAttribute> 新增至該類別要成為服務作業的任何方法：

```csharp
[WebService]
public class Service : T:System.Web.Services.WebService
{
    [WebMethod]
    public string Echo(string input)
    {
       return input;
    }
}
```

ASP.NET 2.0 引入了將屬性 <xref:System.Web.Services.WebService> 和 <xref:System.Web.Services.WebMethodAttribute> 新增至介面 (而非類別)，以及撰寫類別來實作介面的選項：

```csharp
[WebService]
public interface IEcho
{
    [WebMethod]
    string Echo(string input);
}

public class Service : IEcho
{

   public string Echo(string input)
   {
        return input;
    }
}
```

我們建議您使用這個選項，因為具有 <xref:System.Web.Services.WebService> 屬性的介面會構成可以讓不同類別重複使用之服務所執行的作業合約，而這些類別可能會用不同方式來實作該份相同合約。

WCF 服務是藉由定義一或多個 WCF 端點來提供。 端點會由位址、繫結和服務合約所定義。 位址會定義服務的所在位置。 繫結會指定與服務的通訊方式。 服務合約會定義服務可以執行的作業。

通常會先定義服務合約，定義方式是將 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 新增至介面：

```csharp
[ServiceContract]
public interface IEcho
{
     [OperationContract]
     string Echo(string input);
}
```

<xref:System.ServiceModel.ServiceContractAttribute>會指定介面定義 WCF 服務合約，而則 <xref:System.ServiceModel.OperationContractAttribute> 表示介面的方法（如果有的話）會定義服務合約的作業。

完成定義服務合約之後，這個服務合約就會在類別實作用來定義此服務合約之介面的程序下，實作於類別中：

```csharp
public class Service : IEcho
{
    public string Echo(string input)
    {
       return input;
    }
}
```

在 WCF 中，實作為服務合約的類別稱為「服務類型」。

下一步是讓位址和繫結與服務類型產生關聯。 這通常是在設定檔中完成，方法是直接編輯檔案，或使用 WCF 所提供的設定編輯器。 下列是組態檔的範例。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
     <system.serviceModel>
      <services>
      <service name="Service ">
       <endpoint
        address="EchoService"
        binding="basicHttpBinding"
        contract="IEchoService "/>
      </service>
      </services>
     </system.serviceModel>
</configuration>
```

繫結會指定用來與應用程式通訊的一組通訊協定。 下表會列出表示常用選項的系統提供繫結。

|名稱|目的|
|----------|-------------|
|BasicHttpBinding|與支援 WS-BasicProfile 1.1 和 Basic Security Profile 1.0 之 Web 服務和用戶端的互通性。|
|WSHttpBinding|與支援 WS-* 通訊協定 (透過 HTTP) 之 Web 服務和用戶端的互通性。|
|WSDualHttpBinding|雙工 HTTP 通訊，使用這種通訊時，初始訊息的接收者不會直接回覆給初始傳送者，而是可能在一段期間使用符合 WS-* 通訊協定的 HTTP 傳輸任意數目的回應。|
|WSFederationBinding|HTTP 通訊，其中可以根據明確識別之認證提供者所發行的認證來控制對服務資源的存取。|
|NetTcpBinding|跨網路的 WCF 軟體實體之間的安全、可靠、高效能通訊。|
|NetNamedPipeBinding|在同一部電腦上的 WCF 軟體實體之間進行安全、可靠、高效能的通訊。|
|NetMsmqBinding|使用 MSMQ 在 WCF 軟體實體之間進行通訊。|
|MsmqIntegrationBinding|WCF 軟體實體與另一個使用 MSMQ 的軟體實體之間的通訊。|
|NetPeerTcpBinding|使用 Windows 對等網路在 WCF 軟體實體之間進行通訊。|

系統提供的繫結 <xref:System.ServiceModel.BasicHttpBinding> 併入了 ASP.NET Web 服務所支援的通訊協定集合。

WCF 應用程式的自訂系結可輕鬆定義為 WCF 用來執行個別通訊協定的繫結項目類別的集合。 還可以撰寫新的繫結項目來表示額外的通訊協定。

服務類型的內部行為可以透過使用一系列類別的屬性 (稱為行為) 來進行調整。 在下面範例中，<xref:System.ServiceModel.ServiceBehaviorAttribute> 類別是用來指定此服務類型要成為多執行緒。

```csharp
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple)]
public class DerivativesCalculatorServiceType: IDerivativesCalculator
```

有些像是 <xref:System.ServiceModel.ServiceBehaviorAttribute> 的行為是屬性。 而具有系統管理員可能要設定之屬性的其他行為，則可以在應用程式的組態中進行修改。

在程式設計服務類型時，常見的使用方式會包括 <xref:System.ServiceModel.OperationContext> 類別。 它的靜態 <xref:System.ServiceModel.OperationContext.Current%2A> 屬性會提供有關其中執行作業之內容資訊的存取。 <xref:System.ServiceModel.OperationContext> 類似於 <xref:System.Web.HttpContext> 和 <xref:System.EnterpriseServices.ContextUtil> 類別兩者。

## <a name="hosting"></a>Hosting

ASP.NET Web 服務會編譯為類別庫 (Class Library) 組件。 此時會提供稱為服務檔的檔案，該檔案擁有 .asmx 的副檔名，而且它所包含的 `@ WebService` 指示詞可識別其中包含服務程式碼的類別，以及可在其中找到該類別的組件。

`<%@ WebService Language="C#" Class="Service,ServiceAssembly" %>`

此服務檔會複製到網際網路資訊服務 (IIS) 中的 ASP.NET 應用程式根目錄，而組件則會複製到應用程式根目錄的 \bin 子目錄。 接著，該應用程式可以透過應用程式根目錄中服務檔的統一資源定位器 (URL) 來存取。

WCF 服務可以輕鬆地裝載在 IIS 5.1 或6.0 中，這是 IIS 7.0 和任何 .NET 應用程式中所提供的 Windows 進程啟用服務（WAS）。 若要將服務裝載於 IIS 5.1 或 6.0 之中，此服務必須使用 HTTP 做為通訊傳輸通訊協定。

若要將服務裝載於 IIS 5.1、6.0 或 WAS 之中，請使用下列步驟：

1. 將服務類型編譯為類別庫組件。

2. 使用可識別服務類型的 `@ ServiceHost` 指示詞，建立含有 .svc 副檔名的服務檔：

    `<%@ServiceHost language="c#" Service="MyService" %>`

3. 將服務檔複製到虛擬目錄，然後將組件複製到虛擬目錄的 \bin 子目錄。

4. 將組態檔複製到虛擬目錄，然後將檔案重新命名為 Web.config。

接著，該應用程式可以透過應用程式根目錄中服務檔的 URL 來存取。

若要在 .NET 應用程式中裝載 WCF 服務，請將服務類型編譯為應用程式所參考的類別庫元件，並將應用程式設計成使用類別來裝載服務 <xref:System.ServiceModel.ServiceHost> 。 下列是所需要的基礎程式設計範例：

```csharp
string httpBaseAddress = "http://www.contoso.com:8000/";
string tcpBaseAddress = "net.tcp://www.contoso.com:8080/";

Uri httpBaseAddressUri = new Uri(httpBaseAddress);
Uri tcpBaseAddressUri = new Uri(tcpBaseAddress);

Uri[] baseAddresses = new Uri[] {
 httpBaseAddressUri,
 tcpBaseAddressUri};

using(ServiceHost host = new ServiceHost(
typeof(Service), //"Service" is the name of the service type baseAddresses))
{
     host.Open();

     […] //Wait to receive messages
     host.Close();
}
```

下列範例會示範如何在 <xref:System.ServiceModel.ServiceHost> 的建構中指定一個或多個傳輸通訊協定的位址。 這些位址指的是基底位址 (Base Address)。

為 WCF 服務的任何端點提供的位址是相對於端點主機基底位址的位址。 主機的每個通訊傳輸通訊協定都可以擁有一個基底位址。 在上述組態檔的範例組態中，針對端點選取的 <xref:System.ServiceModel.BasicHttpBinding> 會以 HTTP 做為傳輸通訊協定，因此端點 `EchoService` 的位址會相對於主機的 HTTP 基底位址。 在上述範例中的主機案例中，HTTP 基底位址是 `http://www.contoso.com:8000/` 。 對於裝載於 IIS 或 WAS 的服務，其基底位址是服務之服務檔的 URL。

只有裝載于 IIS 或 WAS 中的服務，以及以 HTTP 做為傳輸通訊協定的設定，才可以使用 WCF ASP.NET 相容性模式選項。 若要開啟該選項，請遵循下列步驟。

1. 程式設計人員必須將 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 屬性新增至服務類型，並指定允許或需要 ASP.NET 相容性模式。

    ```csharp
    [System.ServiceModel.Activation.AspNetCompatibilityRequirements(
          RequirementsMode=AspNetCompatibilityRequirementsMode.Require)]
    public class DerivativesCalculatorServiceType: IDerivativesCalculator
    ```

2. 系統管理員必須將此應用程式設定成使用 ASP.NET 相容性模式。

    ```xml
    <configuration>
         <system.serviceModel>
          <services>
          […]
          </services>
          <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>
        </system.serviceModel>
    </configuration>
    ```

    WCF 應用程式也可以設定為使用 .asmx 作為其服務檔案（而不是 .svc）的延伸模組。

    ```xml
    <system.web>
         <compilation>
          <compilation debug="true">
          <buildProviders>
           <remove extension=".asmx"/>
           <add extension=".asmx"
            type="System.ServiceModel.ServiceBuildProvider,
            System.ServiceModel,
            Version=3.0.0.0,
            Culture=neutral,
            PublicKeyToken=b77a5c561934e089" />
          </buildProviders>
          </compilation>
         </compilation>
    </system.web>
    ```

    該選項可讓您在修改服務以使用 WCF 時，不必修改設定為使用 .asmx 服務檔之 Url 的用戶端。

## <a name="client-development"></a>用戶端開發

ASP.NET Web 服務的用戶端是使用命令列工具 WSDL.exe 所產生的，這項工具會提供 .asmx 檔案的 URL 做為輸入。 WCF 提供的對應工具是「 [System.servicemodel 中繼資料公用程式工具」（Svcutil .exe）](../servicemodel-metadata-utility-tool-svcutil-exe.md)。 它會產生程式碼模組，其中包含服務合約的定義和 WCF 用戶端類別的定義。 它還會產生含有服務位址和繫結的組態檔。

在程式設計遠端服務的用戶端時，通常建議根據非同步模式來進行程式設計。 根據預設，WSDL.exe 工具所產生的程式碼永遠可供同步和非同步模式使用。 「 [System.servicemodel 中繼資料公用程式」工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)所產生的程式碼可以提供任一種模式。 根據預設，此程式碼會提供給同步模式使用。 如果是使用 `/async` 參數來執行工具，所產生的程式碼會提供給非同步模式使用。

不保證在 ASP 產生的 WCF 用戶端類別中的名稱。根據預設，NET 的 WSDL.EXE 工具會比對 Svcutil 所產生之 WCF 用戶端類別中的名稱。 尤其是，在 Svcutil.exe 工具產生的程式碼中，必須使用 <xref:System.Xml.Serialization.XmlSerializer> 進行序列化的類別屬性名稱預設會被加上後置字元 Property，但是 WSDL.exe 工具就不是這種情形。

## <a name="message-representation"></a>訊息表示

您可以自訂 ASP.NET Web 服務所傳送及接收之 SOAP 訊息的標頭。 此時會從 <xref:System.Web.Services.Protocols.SoapHeader> 衍生類別來定義標頭的結構，接著，使用 <xref:System.Web.Services.Protocols.SoapHeaderAttribute> 來表示標頭是否存在。

```csharp
public class SomeProtocol : SoapHeader
{
     public long CurrentValue;
     public long Total;
}

[WebService]
public interface IEcho
{
     SomeProtocol ProtocolHeader
     {
      get;
     set;
     }

     [WebMethod]
     [SoapHeader("ProtocolHeader")]
     string PlaceOrders(PurchaseOrderType order);
}

public class Service: WebService, IEcho
{
     private SomeProtocol protocolHeader;

     public SomeProtocol ProtocolHeader
     {
         get
         {
              return this.protocolHeader;
         }

         set
         {
              this.protocolHeader = value;
         }
     }

     string PlaceOrders(PurchaseOrderType order)
     {
         long currentValue = this.protocolHeader.CurrentValue;
     }
}
```

WCF 會提供屬性、、 <xref:System.ServiceModel.MessageContractAttribute> <xref:System.ServiceModel.MessageHeaderAttribute> 和， <xref:System.ServiceModel.MessageBodyMemberAttribute> 以描述服務所傳送和接收的 SOAP 訊息結構。

```csharp
[DataContract]
public class SomeProtocol
{
     [DataMember]
     public long CurrentValue;
     [DataMember]
     public long Total;
}

[DataContract]
public class Item
{
     [DataMember]
     public string ItemNumber;
     [DataMember]
     public decimal Quantity;
     [DataMember]
     public decimal UnitPrice;
}

[MessageContract]
public class ItemMessage
{
     [MessageHeader]
     public SomeProtocol ProtocolHeader;
     [MessageBody]
     public Item Content;
}

[ServiceContract]
public interface IItemService
{
     [OperationContract]
     public void DeliverItem(ItemMessage itemMessage);
}
```

這個語法會產生訊息結構的明確表示，而訊息的結構會隱含在 ASP.NET Web 服務的程式碼中。 此外，在 ASP.NET 語法中，訊息標頭會表示為服務的屬性（例如 `ProtocolHeader` 上一個範例中的屬性），而在 WCF 語法中，則會更精確地表示為訊息的屬性。 此外，WCF 允許將訊息標頭新增至端點的設定。

```xml
<service name="Service ">
     <endpoint
      address="EchoService"
      binding="basicHttpBinding"
      contract="IEchoService ">
      <headers>
      <dsig:X509Certificate
       xmlns:dsig="http://www.w3.org/2000/09/xmldsig#">
       ...
      </dsig:X509Certificate>
      </headers>
     </endpoint>
</service>
```

該選項可讓您避免在用戶端或服務之程式碼中使用基礎結構通訊協定標頭的參考，實際上，這些標頭會依據端點的設定方式新增至訊息中。

## <a name="service-description"></a>服務描述

使用查詢 WSDL 向 ASP.NET Web 服務 .asmx 檔案發出 HTTP GET 要求，會讓 ASP.NET 產生 WSDL 來描述服務。 它會傳回 WSDL 做為要求的回應。

ASP.NET 2.0 可以驗證服務是否相容於 Web Services-Interoperability Organization (WS-I) 的 Basic Profile 1.1，而且可以插入有關服務相容於其 WSDL 的宣告。 透過 `ConformsTo` 屬性的 `EmitConformanceClaims` 和 <xref:System.Web.Services.WebServiceBindingAttribute> 參數，便可完成這個動作。

```csharp
[WebService(Namespace = "http://tempuri.org/")]
[WebServiceBinding(
     ConformsTo = WsiProfiles.BasicProfile1_1,
     EmitConformanceClaims=true)]
public interface IEcho
```

您可以自訂 ASP.NET 為服務產生的 WSDL。 建立 <xref:System.Web.Services.Description.ServiceDescriptionFormatExtension> 的衍生類別來將項目新增至 WSDL，便可進行自訂。

使用查詢 WSDL 針對 WCF 服務的 .svc 檔案發出 HTTP GET 要求，並在 IIS 51、6.0 或 WAS 中裝載 HTTP 端點，會導致 WCF 以 WSDL 回應來描述服務。 使用查詢 WSDL 向 .NET 應用程式所裝載之服務的 HTTP 基底位址發出 HTTP GET 要求，如果 httpGetEnabled 設定為 true，也會產生相同作用。

不過，WCF 也會使用它所產生的 WSDL 來回應透過 ws-metadataexchange 要求，以描述服務。 ASP.NET Web 服務並沒有 WS-MetadataExchange 要求的內建支援。

WCF 產生的 WSDL 可以廣泛地自訂。 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 類別提供了一些可以自訂 WSDL 的功能。 WCF 也可以設定為不產生 WSDL，而是在指定的 URL 使用靜態 WSDL 檔案。

```xml
<behaviors>
     <behavior name="DescriptionBehavior">
     <metadataPublishing
      enableMetadataExchange="true"
      enableGetWsdl="true"
      enableHelpPage="true"
      metadataLocation=
      "http://localhost/DerivativesCalculatorService/Service.WSDL"/>
     </behavior>
</behaviors>
```

## <a name="exception-handling"></a>例外狀況處理

在 ASP.NET Web 服務中，未處理的例外狀況會以 SOAP 錯誤傳回給用戶端。 您也可以明確擲回 <xref:System.Web.Services.Protocols.SoapException> 類別的執行個體，並對傳輸給用戶端的 SOAP 錯誤內容擁有更高的控制。

在 WCF 服務中，未處理的例外狀況不會以 SOAP 錯誤的形式傳回給用戶端，以防止不小心透過例外狀況公開敏感性資訊。 此時會提供組態設定，指定將未處理的例外狀況傳回給用戶端以進行偵錯。

若要將 SOAP 錯誤傳回給用戶端，您可以使用資料合約類型做為泛型型別，並擲回此泛型型別的執行個體，<xref:System.ServiceModel.FaultException%601>。 您還可以新增 <xref:System.ServiceModel.FaultContractAttribute> 屬性至作業，以指定作業可能產生的錯誤。

```csharp
[DataContract]
public class MathFault
{
     [DataMember]
     public string operation;
     [DataMember]
     public string problemType;
}

[ServiceContract]
public interface ICalculator
{
     [OperationContract]
     [FaultContract(typeof(MathFault))]
     int Divide(int n1, int n2);
}
```

這樣做會使得可能的錯誤將以 WSDL 向服務通告，讓用戶端程式設計人員預測作業可能產生的錯誤，並撰寫適當的 catch 陳述式。

```csharp
try
{
     result = client.Divide(value1, value2);
}
catch (FaultException<MathFault> e)
{
 Console.WriteLine("FaultException<MathFault>: Math fault while doing "
  + e.Detail.operation
  + ". Problem: "
  + e.Detail.problemType);
}
```

## <a name="state-management"></a>狀態管理

用來實作 ASP.NET Web 服務的類別可以從 <xref:System.Web.Services.WebService> 衍生。

```csharp
public class Service : WebService, IEcho
{

 public string Echo(string input)
 {
  return input;
 }
}
```

在這種情況下，該類別可以程式設計成使用 <xref:System.Web.Services.WebService> 基底類別 (Base Class) 的 Context 屬性來存取 <xref:System.Web.HttpContext> 物件。 <xref:System.Web.HttpContext> 物件可以使用其 Application 屬性來更新及擷取應用程式狀態資訊，並使用其 Session 屬性來更新及擷取工作階段狀態資訊。

對於透過使用 <xref:System.Web.HttpContext> 的 Session 屬性所存取之工作階段狀態資訊得實際存取位置，ASP.NET 提供了相當程度的控制。 此項資訊可能是儲存在 Cookie、資料庫、目前伺服器的記憶體，或是指定伺服器的記憶體中。 您可在服務的組態檔中選擇儲存位置。

WCF 提供可延伸的物件來進行狀態管理。 可擴充物件是指實作 <xref:System.ServiceModel.IExtensibleObject%601> 的物件。 最重要的擴充物件為 <xref:System.ServiceModel.ServiceHostBase> 和 <xref:System.ServiceModel.InstanceContext>。 `ServiceHostBase` 可讓您維護相同主機上所有服務類型之所有執行個體可以存取的狀態，而 `InstanceContext` 則可讓您維護相同服務類型執行個體中執行之任何程式碼可以存取的狀態。

在這裡，服務型別 `TradingSystem` 具有，其 <xref:System.ServiceModel.ServiceBehaviorAttribute> 指定來自相同 WCF 用戶端實例的所有呼叫都會路由傳送至相同的服務型別實例。

```csharp
[ServiceBehavior(InstanceContextMode = InstanceContextMode.PerSession)]
public class TradingSystem: ITradingService
```

類別 `DealData` 會定義相同服務類型執行個體中執行之任何程式碼可以存取的狀態。

```csharp
internal class DealData: IExtension<InstanceContext>
{
 public string DealIdentifier = null;
 public Trade[] Trades = null;
}
```

在實作服務合約其中一個作業的服務類型程式碼中，`DealData` 狀態物件會新增至目前服務類型執行個體的狀態中。

```csharp
string ITradingService.BeginDeal()
{
 string dealIdentifier = Guid.NewGuid().ToString();
 DealData state = new DealData(dealIdentifier);
 OperationContext.Current.InstanceContext.Extensions.Add(state);
 return dealIdentifier;
}
```

接著，該狀態物件可由實作服務合約之其他作業的程式碼進行擷取和修改。

```csharp
void ITradingService.AddTrade(Trade trade)
{
 DealData dealData =  OperationContext.Current.InstanceContext.Extensions.Find<DealData>();
 dealData.AddTrade(trade);
}
```

雖然 ASP.NET 可控制類別中的狀態資訊的 <xref:System.Web.HttpContext> 實際儲存位置，但是 WCF （至少在其初始版本中）不會控制可延伸物件的儲存位置。 這構成了為 WCF 服務選取 ASP.NET 相容性模式的最佳原因。 如果可設定狀態管理是必要的工作，這時選擇 ASP.NET 相容性模式可讓您以與 ASP.NET 完全相同的方式來使用 <xref:System.Web.HttpContext> 類別的功能，而且也可以設定使用 <xref:System.Web.HttpContext> 類別管理之狀態資訊的儲存位置。

## <a name="security"></a>安全性

用來保護 ASP.NET Web 服務的選項，就是用來保護任何 IIS 應用程式的選項。 由於 WCF 應用程式不僅可以裝載在 IIS 中，還能裝載于任何 .NET 可執行檔中，因此保護 WCF 應用程式的選項必須與 IIS 的功能分開。 不過，針對 ASP.NET Web 服務提供的功能也適用于在 ASP.NET 相容性模式下執行的 WCF 服務。

### <a name="security-authentication"></a>安全性：驗證

IIS 會提供可以用來控制存取應用程式的機能，而您可以從其中選取匿名存取或各種的驗證模式：Windows 驗證、摘要式驗證、基本驗證和 .NET Passport 驗證。 Windows 驗證選項可用來控制 ASP.NET Web 服務的存取。 不過，當 WCF 應用程式裝載于 IIS 時，IIS 必須設定為允許匿名存取應用程式，如此一來，就可以由 WCF 本身來管理驗證，這在其他各種選項中都支援 Windows 驗證。 其他選項還包括使用者名稱權杖、X.509 憑證、SAML 權杖和 CardSpace 卡，但是您也可以定義自訂的驗證機制。

### <a name="security-impersonation"></a>安全性：模擬

ASP.NET 提供了身分識別項目，透過此項目，ASP.NET Web 服務便可設定成模擬特定的使用者，或是目前要求所提供的任何使用者認證。 該元素可用來在以 ASP.NET 相容性模式執行的 WCF 應用程式中設定模擬。

WCF 設定系統會提供自己的身分識別元素，以指定要模擬的特定使用者。 此外，WCF 用戶端和服務也可以獨立設定以進行模擬。 用戶端可以設定為在傳輸要求時模擬目前使用者。

```xml
<behaviors>
     <behavior name="DerivativesCalculatorClientBehavior">
      <clientCredentials>
      <windows allowedImpersonationLevel="Impersonation"/>
      </clientCredentials>
     </behavior>
</behaviors>
```

服務作業可以設定為模擬目前要求所提供的任何使用者認證。

```csharp
[OperationBehavior(Impersonation = ImpersonationOption.Required)]
public void Receive(Message input)
```

### <a name="security-authorization-using-access-control-lists"></a>安全性：使用存取控制清單進行驗證

存取控制清單 (ACL) 可用來限制對 .asmx 檔案的存取。 不過，除了 ASP.NET 相容性模式以外，會忽略 WCF .svc 檔案上的 Acl。

### <a name="security-role-based-authorization"></a>安全性：以角色為基礎的授權

IIS Windows 驗證選項可以搭配 ASP.NET 設定語言所提供的 authorization 項目一起使用，以便根據獲指派使用者的 Windows 群組，為 ASP.NET Web 服務進行以角色為基礎的驗證。 ASP.NET 2.0 引進了更一般性的以角色為基礎的驗證機制：角色提供者。

角色提供者為類別，這些類別全部都會實作可查詢使用者所獲派角色的基本介面，而且每個角色提供者都知道如何從不同來源擷取該資訊。 ASP.NET 2.0 會提供可自 Microsoft SQL Server 資料庫中擷取角色指派的角色提供者，並提供另一個可自 Windows Server 2003 授權管理員擷取角色指派的角色提供者。

角色提供者機制實際上可以單獨用於任何 .NET 應用程式中的 ASP.NET，包括 WCF 應用程式。 下列 WCF 應用程式的範例設定會示範如何使用 ASP.NET 角色提供者，方法是透過來選取此選項 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 。

```xml
<system.serviceModel>
     <services>
         <service name="Service.ResourceAccessServiceType"
             behaviorConfiguration="ServiceBehavior">
             <endpoint
              address="ResourceAccessService"
              binding="wsHttpBinding"
              contract="Service.IResourceAccessContract"/>
         </service>
     </services>
     <behaviors>
       <behavior name="ServiceBehavior">
       <serviceAuthorization principalPermissionMode="UseAspNetRoles"/>
      </behavior>
     </behaviors>
</system.serviceModel>
```

### <a name="security-claims-based-authorization"></a>安全性：宣告架構的授權

WCF 其中一項最重要的創新，就是以宣告為基礎來授權存取受保護資源的完整支援。 宣告是由類型、權限和值組成。以駕照為例， 駕照會建立一組關於持有人的宣告，而其中一個宣告是持有人的生日。 該宣告的類型為生日，而宣告的值為駕駛人的出生日期。 宣告賦予持有人的權限會指定持有人可以如何使用宣告值。 例如，在宣告為駕駛人生日、權限為持有的案例中：駕駛人持有該生日，但無法更改這個日期。 宣告架構的授權也包含以角色為基礎的驗證，因為角色就是一種宣告類型。

宣告架構的授權方式會藉由將一組宣告與作業的存取需求進行比較，並根據該比較的結果授與或拒絕作業存取，來完成其作業。 在 WCF 中，您可以指定要用來執行宣告式授權的類別，方法是將值指派給的 `ServiceAuthorizationManager` 屬性 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 。

```xml
<behaviors>
     <behavior name='ServiceBehavior'>
     <serviceAuthorization
     serviceAuthorizationManagerType=
                   'Service.AccessChecker, Service' />
     </behavior>
</behaviors>
```

用來執行宣告架構授權的類別必須是衍生自 <xref:System.ServiceModel.ServiceAuthorizationManager>，而它只需要覆寫 `AccessCheck()` 方法。 每當叫用服務的作業時，WCF 會呼叫該方法，並提供 <xref:System.ServiceModel.OperationContext> 物件，在其屬性中具有使用者的宣告 `ServiceSecurityContext.AuthorizationContext` 。 WCF 會從使用者提供給驗證的任何安全性權杖，將使用者的宣告組合在一起，這會導致評估這些宣告是否足以執行有問題的作業。

該 WCF 會自動將來自任何一種安全性權杖的宣告組合成非常重要的創新，因為它會讓以宣告為基礎的授權程式碼完全獨立于驗證機制。 相對地，使用 ACL 或 ASP.NET 中角色的授權方式，與 Windows 驗證有密切的關係。

### <a name="security-confidentiality"></a>安全性：機密性

透過將 IIS 中的應用程式設定成使用 Secure Hypertext Transfer Protocol (HTTPS)，可以確保使用 ASP.NET Web 服務交換之訊息在傳輸層的機密性。 這也可以針對 IIS 中裝載的 WCF 應用程式來完成。 不過，裝載于 IIS 外部的 WCF 應用程式也可以設定為使用安全傳輸通訊協定。 更重要的是，WCF 應用程式也可以設定為使用 WS-安全性通訊協定來保護訊息，然後再進行傳輸。 使用 WS-Security 來保護只有訊息本文的方式，可以讓訊息機密地在媒介中傳輸，直到訊息到達最終目的地為止。

## <a name="globalization"></a>全球化

ASP.NET 設定語言可讓您指定個別服務的文化特性。 除了 ASP.NET 相容性模式以外，WCF 不支援該設定。 若要將不使用 ASP.NET 相容性模式的 WCF 服務當地語系化，請將服務類型編譯成文化特性特定的元件，並針對每個特定文化特性的元件擁有個別的文化特性（culture）特定端點。

## <a name="see-also"></a>請參閱

- [依據用途與使用的標準來比較 ASP.NET Web 服務與 WCF](comparing-aspnet-web-services-to-wcf-based-on-purpose-and-standards-used.md)
