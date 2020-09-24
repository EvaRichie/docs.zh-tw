---
title: <bindingElementExtensions>
ms.date: 03/30/2017
ms.assetid: bb597fc0-c947-451c-afda-bf23d42f4f4d
ms.openlocfilehash: 6ba97adfa696e00b4d6b75faf104c31436e25447
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91151126"
---
# \<bindingElementExtensions>

<span data-ttu-id="25dcd-101">這個區段會啟用電腦或應用程式組態檔中自訂繫結項目的使用。</span><span class="sxs-lookup"><span data-stu-id="25dcd-101">This section enables the use of a custom binding element from a machine or application configuration file.</span></span> <span data-ttu-id="25dcd-102">您可以透過使用 `add` 關鍵字，將項目的 `type` 屬性設定為繫結項目延伸，以及將 `name` 屬性設定為自訂繫結項目，來將自訂繫結項目加入至這個集合。</span><span class="sxs-lookup"><span data-stu-id="25dcd-102">You can add a custom binding element to this collection by using the `add` keyword, and setting the `type` attribute of the element to a binding element extension, as well as the `name` attribute to the custom binding element.</span></span>  
  
 <span data-ttu-id="25dcd-103">繫結延伸可讓使用者建立使用者定義的繫結項目，做為自訂繫結的一部分。</span><span class="sxs-lookup"><span data-stu-id="25dcd-103">Binding extensions enable the user to create user-defined binding elements for use as part of custom bindings.</span></span> <span data-ttu-id="25dcd-104">就程式設計角度而言，繫結延伸是實作抽象類別 (Abstract Class) <xref:System.ServiceModel.Channels.BindingElement> 的型別。</span><span class="sxs-lookup"><span data-stu-id="25dcd-104">Programmatically, a binding extension is a type that implements the abstract class <xref:System.ServiceModel.Channels.BindingElement>.</span></span> <span data-ttu-id="25dcd-105">在組態檔中，`bindingElementExtensions` 區段是用於定義延伸項目。</span><span class="sxs-lookup"><span data-stu-id="25dcd-105">In the configuration file, the `bindingElementExtensions` section is used to define an extension element.</span></span>  
  
 <span data-ttu-id="25dcd-106">下列範例使用 `add` 項目，以及 `name` 屬性，將繫結延伸加入至組態檔的 `bindingElementExtensions` 區段中。</span><span class="sxs-lookup"><span data-stu-id="25dcd-106">The following example uses the `add` element, as well as the `name` attribute to add a binding extension to the `bindingElementExtensions` section of the configuration file.</span></span>  
  
```xml  
<system.serviceModel>
  <extensions>
    <bindingElementExtensions>
      <add name="udpTransport"
           type="Microsoft.ServiceModel.Samples.UdpTransportSection, UdpTransport,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </bindingElementExtensions>
  </extensions>
</system.serviceModel>
```  
  
 <span data-ttu-id="25dcd-107">若要將組態功能加入至項目，使用者必須寫入並註冊 `bindingElementExtensionSection` 項目。</span><span class="sxs-lookup"><span data-stu-id="25dcd-107">To add configuration abilities to the element, the user needs to write and register a `bindingElementExtensionSection` element.</span></span> <span data-ttu-id="25dcd-108">如需這方面的詳細資訊，請參閱 <xref:System.Configuration>。</span><span class="sxs-lookup"><span data-stu-id="25dcd-108">For more information on this, see the <xref:System.Configuration> documentation.</span></span>  
  
 <span data-ttu-id="25dcd-109">在定義項目及其組態型別後，延伸即可做為自訂繫結的一部分，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="25dcd-109">After the element and its configuration type are defined, the extension can be used as part of a custom binding as shown in the following example.</span></span>  
  
```xml  
<customBinding>
  <binding name="test2">
    <udpTransport />
    <binaryMessageEncoding maxReadPoolSize="211"
                           maxWritePoolSize="2132"
                           maxSessionSize="3141" />
  </binding>
</customBinding>
```  
  
## <a name="see-also"></a><span data-ttu-id="25dcd-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="25dcd-110">See also</span></span>

- <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>
- [<span data-ttu-id="25dcd-111">擴充繫結</span><span class="sxs-lookup"><span data-stu-id="25dcd-111">Extending Bindings</span></span>](../../../wcf/extending/extending-bindings.md)
