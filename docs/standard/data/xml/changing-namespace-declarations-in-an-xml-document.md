---
title: 變更 XML 文件中的命名空間宣告
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
ms.openlocfilehash: 95f9c6301f656ad4da5edcfb66521589b9195114
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725361"
---
# <a name="changing-namespace-declarations-in-an-xml-document"></a><span data-ttu-id="a1773-102">變更 XML 文件中的命名空間宣告</span><span class="sxs-lookup"><span data-stu-id="a1773-102">Changing Namespace Declarations in an XML Document</span></span>

<span data-ttu-id="a1773-103">**XmlDocument** 公開命名空間宣告，而且 **xmlns** 屬性是文件物件模型的一部份。</span><span class="sxs-lookup"><span data-stu-id="a1773-103">The **XmlDocument** exposes namespace declarations and **xmlns** attributes as part of the document object model.</span></span> <span data-ttu-id="a1773-104">這些是儲存在 **XmlDocument** 中，因此當您儲存文件時，它可以保留那些屬性的位置。</span><span class="sxs-lookup"><span data-stu-id="a1773-104">These are stored in the **XmlDocument**, so when you save the document, it can preserve the location of those attributes.</span></span> <span data-ttu-id="a1773-105">變更這些屬性對已經存在於樹狀結構中之節點的 **Name**、**NamespaceURI** 和 **Prefix** 屬性並沒有影響。</span><span class="sxs-lookup"><span data-stu-id="a1773-105">Changing these attributes has no affect on the **Name**, **NamespaceURI**, and **Prefix** properties of other nodes already in the tree.</span></span> <span data-ttu-id="a1773-106">例如，如果載入下列文件，則 `test` 項目會具有 **NamespaceURI** `123.`</span><span class="sxs-lookup"><span data-stu-id="a1773-106">For example, if you load the following document, then the `test` element has **NamespaceURI** `123.`</span></span>  
  
```xml  
<test xmlns="123"/>  
```  
  
 <span data-ttu-id="a1773-107">如果如下所示移除 `xmlns` 屬性，則 `test` 項目仍會具有 `123` 的 **NamespaceURI**。</span><span class="sxs-lookup"><span data-stu-id="a1773-107">If you remove the `xmlns` attribute as follows, then the `test` element still has the **NamespaceURI** of `123`.</span></span>  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 <span data-ttu-id="a1773-108">同樣地，如果如下所示將不同的 `xmlns` 屬性加入 `doc` 項目，則 `test` 項目仍會具有 **NamespaceURI** `123`。</span><span class="sxs-lookup"><span data-stu-id="a1773-108">Likewise, if you add a different `xmlns` attribute to the `doc` element as follows, then the `test` element still has **NamespaceURI** `123`.</span></span>  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456")
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 <span data-ttu-id="a1773-109">因此，除非儲存並重新載入 **XmlDocument** 物件，否則變更 `xmlns` 屬性並不會產生任何影響。</span><span class="sxs-lookup"><span data-stu-id="a1773-109">Therefore, changing `xmlns` attributes will have no affect until you save and reload the **XmlDocument** object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a1773-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a1773-110">See also</span></span>

- [<span data-ttu-id="a1773-111">XML 文件物件模型 (DOM)</span><span class="sxs-lookup"><span data-stu-id="a1773-111">XML Document Object Model (DOM)</span></span>](xml-document-object-model-dom.md)
