---
title: 自訂訊息編碼器：自訂文字編碼器
ms.date: 03/30/2017
ms.assetid: 68ff5c74-3d33-4b44-bcae-e1d2f5dea0de
ms.openlocfilehash: b60fa2a84520ad208d435a0c9284c19b5de8e989
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600603"
---
# <a name="custom-message-encoder-custom-text-encoder"></a>自訂訊息編碼器：自訂文字編碼器

這個範例會示範如何使用 Windows Communication Foundation （WCF）來執行自訂文字訊息編碼器。

> [!WARNING]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Text`

<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>WCF 的僅支援 utf-8、utf-16 和位元組由大到小的 Unicode 編碼。 此範例中的自訂文字訊息編碼器可支援所有平臺支援的字元編碼，以因應互通性的需求。 此範例是由用戶端主控台程式（.exe）、Internet Information Services （IIS）所裝載的服務程式庫（.dll），以及文字訊息編碼器程式庫（.dll）所組成。 服務會實作定義要求-回覆通訊模式的合約。 合約是由 `ICalculator` 介面所定義，這個介面會公開數學運算作業 (加、減、乘、除)。 用戶端會對指定的數學運算作業提出同步要求，服務則會以結果回覆。 用戶端和服務都會使用 `CustomTextMessageEncoder`，而不使用預設的 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>。

自訂編碼器的實作是由訊息編碼器處理站、訊息編碼器、訊息編碼繫結項目和組態處理常式所組成，說明如下：

- 建置自訂編碼器和編碼器處理站。

- 建立自訂編碼器的繫結項目。

- 使用自訂繫結組態以整合自訂繫結項目。

- 開發自訂組態處理常式，以允許自訂繫結項目的檔案組態。

## <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例

1. 使用下列命令安裝 ASP.NET 4.0。

    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable
    ```

2. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。

3. 若要建立方案，請依照[建立 Windows Communication Foundation 範例](building-the-samples.md)中的指示進行。

4. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。

## <a name="message-encoder-factory-and-the-message-encoder"></a>訊息編碼器處理站和訊息編碼器

開啟 <xref:System.ServiceModel.ServiceHost> 或用戶端通道時，設計階段元件 `CustomTextMessageBindingElement` 會建立 `CustomTextMessageEncoderFactory`。 處理站則會建立 `CustomTextMessageEncoder`。 訊息編碼器會同時以資料流處理模式和緩衝模式來運作。 它會分別使用 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter> 來讀取和寫入訊息。 與僅支援 UTF-8、UTF-16 和位元組序 Unicode 的 WCF 優化 XML 讀取器和寫入器相反，這些讀取器和寫入器支援所有平臺支援的編碼。

下列程式碼範例示範 CustomTextMessageEncoder。

```csharp
public class CustomTextMessageEncoder : MessageEncoder
{
    private CustomTextMessageEncoderFactory factory;
    private XmlWriterSettings writerSettings;
    private string contentType;

    public CustomTextMessageEncoder(CustomTextMessageEncoderFactory factory)
    {
        this.factory = factory;

        this.writerSettings = new XmlWriterSettings();
        this.writerSettings.Encoding = Encoding.GetEncoding(factory.CharSet);
        this.contentType = $"{this.factory.MediaType}; charset={this.writerSettings.Encoding.HeaderName}";
    }

    public override string ContentType
    {
        get
        {
            return this.contentType;
        }
    }

    public override string MediaType
    {
        get
        {
            return factory.MediaType;
        }
    }

    public override MessageVersion MessageVersion
    {
        get
        {
            return this.factory.MessageVersion;
        }
    }

    public override Message ReadMessage(ArraySegment<byte> buffer, BufferManager bufferManager, string contentType)
    {
        byte[] msgContents = new byte[buffer.Count];
        Array.Copy(buffer.Array, buffer.Offset, msgContents, 0, msgContents.Length);
        bufferManager.ReturnBuffer(buffer.Array);

        MemoryStream stream = new MemoryStream(msgContents);
        return ReadMessage(stream, int.MaxValue);
    }

    public override Message ReadMessage(Stream stream, int maxSizeOfHeaders, string contentType)
    {
        XmlReader reader = XmlReader.Create(stream);
        return Message.CreateMessage(reader, maxSizeOfHeaders, this.MessageVersion);
    }

    public override ArraySegment<byte> WriteMessage(Message message, int maxMessageSize, BufferManager bufferManager, int messageOffset)
    {
        MemoryStream stream = new MemoryStream();
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);
        message.WriteMessage(writer);
        writer.Close();

        byte[] messageBytes = stream.GetBuffer();
        int messageLength = (int)stream.Position;
        stream.Close();

        int totalLength = messageLength + messageOffset;
        byte[] totalBytes = bufferManager.TakeBuffer(totalLength);
        Array.Copy(messageBytes, 0, totalBytes, messageOffset, messageLength);

        ArraySegment<byte> byteArray = new ArraySegment<byte>(totalBytes, messageOffset, messageLength);
        return byteArray;
    }

    public override void WriteMessage(Message message, Stream stream)
    {
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);
        message.WriteMessage(writer);
        writer.Close();
    }
}
```

下列程式碼範例示範如何建置訊息編碼器處理站。

```csharp
public class CustomTextMessageEncoderFactory : MessageEncoderFactory
{
    private MessageEncoder encoder;
    private MessageVersion version;
    private string mediaType;
    private string charSet;

    internal CustomTextMessageEncoderFactory(string mediaType, string charSet,
        MessageVersion version)
    {
        this.version = version;
        this.mediaType = mediaType;
        this.charSet = charSet;
        this.encoder = new CustomTextMessageEncoder(this);
    }

    public override MessageEncoder Encoder
    {
        get
        {
            return this.encoder;
        }
    }

    public override MessageVersion MessageVersion
    {
        get
        {
            return this.version;
        }
    }

    internal string MediaType
    {
        get
        {
            return this.mediaType;
        }
    }

    internal string CharSet
    {
        get
        {
            return this.charSet;
        }
    }
}
```

## <a name="message-encoding-binding-element"></a>訊息編碼繫結項目

繫結項目允許設定 WCF 執行時間堆疊。 若要在 WCF 應用程式中使用自訂訊息編碼器，必須有繫結項目，才能在執行時間堆疊中的適當層級上，使用適當的設定來建立訊息編碼器 factory。

`CustomTextMessageBindingElement` 是從 <xref:System.ServiceModel.Channels.BindingElement> 基底類別衍生，而且繼承自 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> 類別。 這可讓其他 WCF 元件將此繫結項目辨識為訊息編碼繫結項目。 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> 的實作會傳回相符之訊息編碼器處理站的執行個體，其中包含適當的設定。

`CustomTextMessageBindingElement` 會透過屬性公開 `MessageVersion`、`ContentType` 和 `Encoding` 的設定。 編碼器同時支援 Soap11Addressing 和 Soap12Addressing1 版本。 預設為 Soap11Addressing1。 `ContentType` 的預設值為 "text/xml"。 `Encoding` 屬性可讓您設定所需的字元編碼值。 範例用戶端和服務使用 ISO-8859-1 （採用 latin1-general）字元編碼，這不是 WCF 的支援 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 。

下列程式碼將示範如何使用自訂文字訊息編碼器，透過程式設計方式建立繫結。

```csharp
ICollection<BindingElement> bindingElements = new List<BindingElement>();
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();
CustomTextMessageBindingElement textBindingElement = new CustomTextMessageBindingElement();
bindingElements.Add(textBindingElement);
bindingElements.Add(httpBindingElement);
CustomBinding binding = new CustomBinding(bindingElements);
```

## <a name="adding-metadata-support-to-the-message-encoding-binding-element"></a>在訊息編碼繫結項目中新增中繼資料支援

任何衍生自 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> 的型別都會負責更新針對服務所產生之 WSDL 文件中的 SOAP 繫結版本。 藉由實作 `ExportEndpoint` 介面上的 <xref:System.ServiceModel.Description.IWsdlExportExtension> 方法，再修改產生的 WSDL，即可做到這點。 在這個範例中，`CustomTextMessageBindingElement` 將使用 `TextMessageEncodingBindingElement` 的 WSDL 匯出邏輯。

在這個範例中，用戶端組態會以手動方式設定。 由於 `CustomTextMessageBindingElement` 並不匯出原則判斷提示來描述其行為，您將無法使用 Svcutil.exe 產生用戶端組態。 您通常應該在自訂繫結項目上實作 <xref:System.ServiceModel.Description.IPolicyExportExtension> 介面，以便匯出可描述繫結項目所實作之行為或功能的自訂原則判斷提示。 如需如何匯出自訂繫結項目之原則判斷提示的範例，請參閱[Transport： UDP](transport-udp.md)範例。

## <a name="message-encoding-binding-configuration-handler"></a>訊息編碼繫結組態處理常式
上一個區段示範的是如何以程式設計方式使用自訂文字訊息編碼器。 `CustomTextMessageEncodingBindingSection` 將會實作可讓您在組態檔中指定自訂文字訊息編碼器使用方式的組態處理常式。 `CustomTextMessageEncodingBindingSection` 類別衍生自 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> 類別。 `BindingElementType` 屬性會通知組態系統要為此區段建立的繫結項目類型。

由 `CustomTextMessageBindingElement` 定義的所有設定都會公開為 `CustomTextMessageEncodingBindingSection` 中的屬性。 <xref:System.Configuration.ConfigurationPropertyAttribute> 有助於將組態項目屬性 (Attribute) 對應至屬性 (Property)，並可在屬性 (Attribute) 未設定時設定其預設值。 載入來自組態的值並將這些值套用至型別的屬性時，就會呼叫 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A> 方法，而這個方法會將屬性轉換為繫結項目的實體執行個體。

這個組態處理常式會在服務或用戶端的 App.config 或 Web.config 中對應至下列表示。

```xml
<customTextMessageEncoding encoding="utf-8" contentType="text/xml" messageVersion="Soap11Addressing1" />
```

這個範例會使用 ISO-8859-1 編碼方式。

若要使用這個組態處理常式，您必須先使用下列組態項目加以註冊。

```xml
<extensions>
    <bindingElementExtensions>
        <add name="customTextMessageEncoding" type="
Microsoft.ServiceModel.Samples.CustomTextMessageEncodingBindingSection,
                  CustomTextMessageEncoder" />
    </bindingElementExtensions>
</extensions>
```
