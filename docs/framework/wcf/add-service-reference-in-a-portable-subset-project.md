---
title: 將服務參考加入至可攜式子集專案
ms.date: 03/30/2017
ms.assetid: 61ccfe0f-a34b-40ca-8f5e-725fa1b8095e
ms.openlocfilehash: e9a0d3fbc75a8c64af892f74acedfc41dc115da3
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687710"
---
# <a name="add-service-reference-in-a-portable-subset-project"></a><span data-ttu-id="c0156-102">將服務參考加入至可攜式子集專案</span><span class="sxs-lookup"><span data-stu-id="c0156-102">Add Service Reference in a Portable Subset Project</span></span>

<span data-ttu-id="c0156-103">可移植子集專案可讓 .NET 元件程式設計人員維護單一來源樹狀結構和組建系統，同時仍支援多個 .NET 執行 (桌面、Silverlight、Windows Phone 和 Xbox) 。</span><span class="sxs-lookup"><span data-stu-id="c0156-103">Portable subset projects enable .NET assembly programmers to maintain a single source tree and build system while still supporting multiple .NET implementations (desktop, Silverlight, Windows Phone, and Xbox).</span></span> <span data-ttu-id="c0156-104">便攜子集專案只參考可用於任何 .NET 執行的 .NET 元件的可移植程式庫。</span><span class="sxs-lookup"><span data-stu-id="c0156-104">Portable subset projects only reference portable libraries that are .NET assemblies that can be used on any .NET implementation.</span></span>
  
## <a name="add-service-reference-details"></a><span data-ttu-id="c0156-105">加入服務參考詳細資料</span><span class="sxs-lookup"><span data-stu-id="c0156-105">Add Service Reference Details</span></span>  
 <span data-ttu-id="c0156-106">將服務參考加入至可攜式子集專案時會強制執行下列限制：</span><span class="sxs-lookup"><span data-stu-id="c0156-106">When adding a service reference in a portable subset project the following restrictions are enforced:</span></span>  
  
1. <span data-ttu-id="c0156-107"><xref:System.Xml.Serialization.XmlSerializer> 只能使用常值編碼。</span><span class="sxs-lookup"><span data-stu-id="c0156-107">For <xref:System.Xml.Serialization.XmlSerializer>, only literal encodings are allowed.</span></span> <span data-ttu-id="c0156-108">SOAP 編碼會在匯出期間產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="c0156-108">SOAP encodings generate an error during import.</span></span>  
  
2. <span data-ttu-id="c0156-109">對於使用 <xref:System.Runtime.Serialization.DataContractSerializer> 案例的服務，會提供資料合約 Surrogate 以確保重複使用的型別只能來自可攜式子集。</span><span class="sxs-lookup"><span data-stu-id="c0156-109">For services that use <xref:System.Runtime.Serialization.DataContractSerializer> scenarios, a data contract surrogate is provided to ensure that reused types come only from the portable subset.</span></span>  
  
3. <span data-ttu-id="c0156-110">可攜式程式庫不支援需要依賴繫結程序的端點 (所有繫結程序，但是不包括 <xref:System.ServiceModel.BasicHttpBinding>、沒有異動流程的 <xref:System.ServiceModel.WSHttpBinding>、可靠工作階段或 MTOM 編碼和對等的自訂繫結程序)，將會被忽略。</span><span class="sxs-lookup"><span data-stu-id="c0156-110">Endpoints which rely on bindings not supported in portable libraries (all bindings except <xref:System.ServiceModel.BasicHttpBinding>, <xref:System.ServiceModel.WSHttpBinding> without transaction flow, reliable sessions, or MTOM encoding, and equivalent custom bindings) are ignored.</span></span>  
  
4. <span data-ttu-id="c0156-111">在匯出之前，會刪除所有作業中全部訊息描述之訊息標頭。</span><span class="sxs-lookup"><span data-stu-id="c0156-111">Message headers are deleted from all message descriptions in all operations before import.</span></span>  
  
5. <span data-ttu-id="c0156-112">會從產生的用戶端 Proxy 程式碼中移除非可攜式屬性 <xref:System.ComponentModel.DesignerCategoryAttribute>、<xref:System.SerializableAttribute> 和 <xref:System.ServiceModel.TransactionFlowAttribute>。</span><span class="sxs-lookup"><span data-stu-id="c0156-112">Non-portable attributes <xref:System.ComponentModel.DesignerCategoryAttribute>, <xref:System.SerializableAttribute>, and <xref:System.ServiceModel.TransactionFlowAttribute> are removed from generated client proxy code.</span></span>  
  
6. <span data-ttu-id="c0156-113">會從 <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.OperationContractAttribute> 和 <xref:System.ServiceModel.FaultContractAttribute> 中移除非可攜式屬性 ProtectionLevel、SessionMode、IsInitiating 和 IsTerminating。</span><span class="sxs-lookup"><span data-stu-id="c0156-113">Non-portable properties ProtectionLevel, SessionMode, IsInitiating, IsTerminating are removed from <xref:System.ServiceModel.ServiceContractAttribute>, <xref:System.ServiceModel.OperationContractAttribute>, and <xref:System.ServiceModel.FaultContractAttribute>.</span></span>  
  
7. <span data-ttu-id="c0156-114">所有服務作業都會產生為用戶端 Proxy 上的非同步作業。</span><span class="sxs-lookup"><span data-stu-id="c0156-114">All service operations are generated as asynchronous operations on the client proxy.</span></span>  
  
8. <span data-ttu-id="c0156-115">會將所產生且使用非可攜式型別的用戶端建構函式移除。</span><span class="sxs-lookup"><span data-stu-id="c0156-115">Generated client constructors which use non-portable types are removed.</span></span>  
  
9. <span data-ttu-id="c0156-116"><xref:System.Net.CookieContainer> 執行個體會在產生的用戶端上公開。</span><span class="sxs-lookup"><span data-stu-id="c0156-116">A <xref:System.Net.CookieContainer> instance is exposed on the generated client.</span></span>  
  
10. <span data-ttu-id="c0156-117">會在識別程式碼產生器組件及版本的檔案頂端插入註解：`// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="c0156-117">A comment is inserted at the top of the file identifying the assembly and version of the code generator:`// This code was auto-generated by Microsoft.VisualStudio.Portable.AddServiceReference, version 1.0.0.0`</span></span>  
  
11. <span data-ttu-id="c0156-118">不支援 <xref:System.Runtime.Serialization.ISerializable> 介面。</span><span class="sxs-lookup"><span data-stu-id="c0156-118">The <xref:System.Runtime.Serialization.ISerializable> interface is not supported.</span></span>  
  
12. <span data-ttu-id="c0156-119">不支援 Net.Tcp 和 PollingDuplex 繫結</span><span class="sxs-lookup"><span data-stu-id="c0156-119">Net.Tcp and PollingDuplex bindings are not supported</span></span>  
  
13. <span data-ttu-id="c0156-120">永遠使用 <xref:System.Runtime.Serialization.DataContractSerializer> 處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="c0156-120">The <xref:System.Runtime.Serialization.DataContractSerializer> will always be used for faults.</span></span>  
  
14. <span data-ttu-id="c0156-121">在可攜式子集專案中不支援 <xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A>。</span><span class="sxs-lookup"><span data-stu-id="c0156-121"><xref:System.ServiceModel.MessageContractAttribute.IsWrapped%2A> is not supported in portable subset projects.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c0156-122">請參閱</span><span class="sxs-lookup"><span data-stu-id="c0156-122">See also</span></span>

- [<span data-ttu-id="c0156-123">使用 WCF 用戶端存取服務</span><span class="sxs-lookup"><span data-stu-id="c0156-123">Accessing Services Using a WCF Client</span></span>](accessing-services-using-a-wcf-client.md)
- [<span data-ttu-id="c0156-124">可攜式類別庫</span><span class="sxs-lookup"><span data-stu-id="c0156-124">Portable Class Library</span></span>](../cross-platform/portable-class-library.md)
