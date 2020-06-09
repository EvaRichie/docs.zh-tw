---
title: 建立已簽署及/或加密的自訂標頭
ms.date: 03/30/2017
ms.assetid: e8668b37-c79f-4714-9de5-afcb88b9ff02
ms.openlocfilehash: 0adb4100bca1add2c23ff2c802ddb5e2cb1c368c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579654"
---
# <a name="creating-a-custom-header-that-is-signed-and-or-encrypted"></a><span data-ttu-id="d76a4-102">建立已簽署及/或加密的自訂標頭</span><span class="sxs-lookup"><span data-stu-id="d76a4-102">Creating a custom header that is signed and-or encrypted</span></span>
<span data-ttu-id="d76a4-103">使用 WCF 用戶端來呼叫非 WCF 服務時，有時候必須使用自訂 SOAP 標頭。</span><span class="sxs-lookup"><span data-stu-id="d76a4-103">When calling a non-WCF service using a WCF client it is sometimes necessary to use custom SOAP headers.</span></span> <span data-ttu-id="d76a4-104">WCF 具有一個規範化 Bug，這個 Bug 會讓已簽署和加密的自訂標頭無法使用非 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="d76a4-104">There is a canonicalization bug in WCF that prevents custom headers that are signed and encrypted from working with a non-WCF service.</span></span> <span data-ttu-id="d76a4-105">這個問題是預設 XML 命名空間的規範化錯誤所造成。</span><span class="sxs-lookup"><span data-stu-id="d76a4-105">The problem is caused by the incorrect canonicalization of default XML namespaces.</span></span> <span data-ttu-id="d76a4-106">只有當您使用已簽署和 (或) 加密的自訂標頭來呼叫非 WCF 服務時，才會發生這個問題。</span><span class="sxs-lookup"><span data-stu-id="d76a4-106">This is only problematic when calling non-WCF services with custom headers that are signed and/or encrypted.</span></span>  <span data-ttu-id="d76a4-107">當此服務收到包含已簽署和 (或) 加密之自訂標頭的訊息時，它無法驗證簽章。</span><span class="sxs-lookup"><span data-stu-id="d76a4-107">When the service receives the message containing the signed and/or encrypted custom header it is unable to verify the signature.</span></span> <span data-ttu-id="d76a4-108">這種解決方法會避免規範化 Bug、允許與非 WCF 服務互通，但是無法防止與 WCF 服務互通。</span><span class="sxs-lookup"><span data-stu-id="d76a4-108">This workaround avoids the canonicalization bug, allows interoperability with non-WCF services, but does not prevent interoperability with WCF services.</span></span>  
  
## <a name="defining-the-custom-header"></a><span data-ttu-id="d76a4-109">定義自訂標頭</span><span class="sxs-lookup"><span data-stu-id="d76a4-109">Defining the custom header</span></span>  
 <span data-ttu-id="d76a4-110">自訂標頭的定義方式如下：定義訊息合約，然後使用 <xref:System.ServiceModel.MessageHeaderAttribute> 屬性來標記您想要當做標頭傳送的成員。</span><span class="sxs-lookup"><span data-stu-id="d76a4-110">Custom headers are defined by defining a message contract and marking the members you want to be sent as headers with a <xref:System.ServiceModel.MessageHeaderAttribute> attribute.</span></span> <span data-ttu-id="d76a4-111">若要解決規範化 Bug，您必須確定 XML 序列化程式會使用前置詞而非預設命名空間宣告來宣告自訂標頭的命名空間。</span><span class="sxs-lookup"><span data-stu-id="d76a4-111">To work around the canonicalization bug you must ensure that the XML serializer declares the namespace for the custom header with a prefix instead of a default namespace declaration.</span></span> <span data-ttu-id="d76a4-112">下列程式碼將示範如何使用正確的命名空間宣告來定義將當做訊息標頭使用的資料型別。</span><span class="sxs-lookup"><span data-stu-id="d76a4-112">The following code shows how to define the data type that will be used as a message header with the correct namespace declaration.</span></span>  
  
```csharp
[System.CodeDom.Compiler.GeneratedCodeAttribute("svcutil", "3.0.4506.648")]  
[System.SerializableAttribute()]  
[System.Diagnostics.DebuggerStepThroughAttribute()]  
[System.ComponentModel.DesignerCategoryAttribute("code")]  
[System.Xml.Serialization.XmlTypeAttribute(AnonymousType=true, Namespace="http://www.example.org/getMessage/")]  
public partial class msgHeaderElement  
{  
   // Define the XML namespace and force it to use an ‘h’ prefix  
    [System.Xml.Serialization.XmlNamespaceDeclarations]  
    public System.Xml.Serialization.XmlSerializerNamespaces _xsns = new System.Xml.Serialization.XmlSerializerNamespaces(new System.Xml.XmlQualifiedName[] { new System.Xml.XmlQualifiedName("h", "http://www.example.org/getMessage/") });  
  
    private string msgHeaderInputField;  
  [System.Xml.Serialization.XmlElementAttribute(Form=System.Xml.Schema.XmlSchemaForm.Unqualified, Order=0)]  
    public string msgHeaderInput  
    {  
        get  
        {  
            return this.msgHeaderInputField;  
        }  
        set  
        {  
            this.msgHeaderInputField = value;  
        }  
    }  
}  
```  
  
 <span data-ttu-id="d76a4-113">這段程式碼會宣告名為 `msgHeaderElement` 的新型別，而這個型別將使用 XML 序列化程式來序列化。</span><span class="sxs-lookup"><span data-stu-id="d76a4-113">This code declares a new type called `msgHeaderElement` that will be serialized with the XML Serializer.</span></span> <span data-ttu-id="d76a4-114">序列化這個型別的執行個體時，它將使用 ‘h’ 前置詞來定義命名空間，因而解決規範化 Bug。</span><span class="sxs-lookup"><span data-stu-id="d76a4-114">When an instance of this type is serialized, it will define a namespace with an ‘h’ prefix, thus working around the canonicalization bug.</span></span>  <span data-ttu-id="d76a4-115">然後，訊息合約會定義 `msgHeaderElement` 的執行個體，並且使用 <xref:System.ServiceModel.MessageHeaderAttribute> 屬性來標記它，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d76a4-115">The message contract would then define an instance of `msgHeaderElement` and mark it with the <xref:System.ServiceModel.MessageHeaderAttribute> attribute as shown in the following example.</span></span>  
  
```csharp
[MessageContract]  
public  class MyMessageContract  
{  
   // other message contents...  
   [MessageHeader(ProductionLevel=ProtectionLevel.EncryptAndSign)]  
   public msgHeaderElement;  
   // other message contents...  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="d76a4-116">請參閱</span><span class="sxs-lookup"><span data-stu-id="d76a4-116">See also</span></span>

- [<span data-ttu-id="d76a4-117">預設訊息合約</span><span class="sxs-lookup"><span data-stu-id="d76a4-117">Default Message Contract</span></span>](../samples/default-message-contract.md)
- [<span data-ttu-id="d76a4-118">訊息合約</span><span class="sxs-lookup"><span data-stu-id="d76a4-118">Message Contracts</span></span>](../samples/message-contracts.md)
- [<span data-ttu-id="d76a4-119">使用訊息合約</span><span class="sxs-lookup"><span data-stu-id="d76a4-119">Using Message Contracts</span></span>](using-message-contracts.md)
