---
title: 中繼資料格式
ms.date: 03/30/2017
ms.assetid: baad1e68-28fc-4a6a-8a43-75e47e7fa871
ms.openlocfilehash: a304b6026ae9b8bc9506bfa82ab6eaa3c80b2a42
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679373"
---
# <a name="metadata-formats"></a><span data-ttu-id="12136-102">元資料格式</span><span class="sxs-lookup"><span data-stu-id="12136-102">Metadata formats</span></span>

<span data-ttu-id="12136-103">Windows Communication Foundation (WCF) 支援下表中的元資料格式。</span><span class="sxs-lookup"><span data-stu-id="12136-103">Windows Communication Foundation (WCF) supports the metadata formats in the following table.</span></span>  
  
## <a name="metadata-specifications-and-usage"></a><span data-ttu-id="12136-104">中繼資料規格和用法</span><span class="sxs-lookup"><span data-stu-id="12136-104">Metadata Specifications and Usage</span></span>  
  
|<span data-ttu-id="12136-105">通訊協定</span><span class="sxs-lookup"><span data-stu-id="12136-105">Protocol</span></span>|<span data-ttu-id="12136-106">規格和用法</span><span class="sxs-lookup"><span data-stu-id="12136-106">Specification and usage</span></span>|  
|--------------|-----------------------------|  
|<span data-ttu-id="12136-107">WSDL 1.1</span><span class="sxs-lookup"><span data-stu-id="12136-107">WSDL 1.1</span></span>|[<span data-ttu-id="12136-108">Web 服務描述語言 (WSDL) 1.1</span><span class="sxs-lookup"><span data-stu-id="12136-108">Web Services Description Language (WSDL) 1.1</span></span>](https://www.w3.org/TR/wsdl/)<br /><br /> <span data-ttu-id="12136-109">WCF 會使用 Web 服務描述語言 (WSDL) 來描述服務。</span><span class="sxs-lookup"><span data-stu-id="12136-109">WCF uses Web Services Description Language (WSDL) to describe services.</span></span>|  
|<span data-ttu-id="12136-110">XML 結構描述</span><span class="sxs-lookup"><span data-stu-id="12136-110">XML Schema</span></span>|<span data-ttu-id="12136-111">[XML 架構第2部分：資料類型第二版](https://www.w3.org/TR/2004/REC-xmlschema-2-20041028/) 及 [XML 架構第1部分：結構第二版](https://www.w3.org/TR/2004/REC-xmlschema-1-20041028/)</span><span class="sxs-lookup"><span data-stu-id="12136-111">[XML Schema Part 2: Datatypes Second Edition](https://www.w3.org/TR/2004/REC-xmlschema-2-20041028/) and [XML Schema Part 1: Structures Second Edition](https://www.w3.org/TR/2004/REC-xmlschema-1-20041028/)</span></span><br /><br /> <span data-ttu-id="12136-112">WCF 會使用 XML 架構來描述訊息中使用的資料類型。</span><span class="sxs-lookup"><span data-stu-id="12136-112">WCF uses the XML Schema to describe data types used in messages.</span></span>|  
|<span data-ttu-id="12136-113">WS 原則</span><span class="sxs-lookup"><span data-stu-id="12136-113">WS Policy</span></span>|[<span data-ttu-id="12136-114">Web 服務原則 1.2 - 架構 (WS-Policy)</span><span class="sxs-lookup"><span data-stu-id="12136-114">Web Services Policy 1.2 - Framework (WS-Policy)</span></span>](https://www.w3.org/Submission/WS-Policy/)<br /><br /> [<span data-ttu-id="12136-115">Web 服務原則 1.5 - 架構</span><span class="sxs-lookup"><span data-stu-id="12136-115">Web Services Policy 1.5 - Framework</span></span>](https://www.w3.org/TR/ws-policy/)<br /><br /> <span data-ttu-id="12136-116">WCF 會使用 WS-原則1.2 或1.5 規格搭配網域特定的判斷提示，以描述服務需求和功能。</span><span class="sxs-lookup"><span data-stu-id="12136-116">WCF uses the WS-Policy 1.2 or 1.5 specifications with domain-specific assertions to describe service requirements and capabilities.</span></span>|  
|<span data-ttu-id="12136-117">WS 原則附件</span><span class="sxs-lookup"><span data-stu-id="12136-117">WS Policy Attachments</span></span>|[<span data-ttu-id="12136-118">Web 服務原則 1.2 - 附件 (WS-PolicyAttachment)</span><span class="sxs-lookup"><span data-stu-id="12136-118">Web Services Policy 1.2 - Attachment (WS-PolicyAttachment)</span></span>](https://www.w3.org/Submission/WS-PolicyAttachment/)<br /><br /> <span data-ttu-id="12136-119">WCF 會執行 WS 原則附件，以在 WSDL 中的不同範圍附加原則運算式。</span><span class="sxs-lookup"><span data-stu-id="12136-119">WCF implements WS-Policy Attachments to attach policy expressions at various scopes in WSDL.</span></span>|  
|<span data-ttu-id="12136-120">WS 中繼資料交換</span><span class="sxs-lookup"><span data-stu-id="12136-120">WS Metadata Exchange</span></span>|[<span data-ttu-id="12136-121"> (WS-透過 ws-metadataexchange) 的 Web 服務中繼資料交換 </span><span class="sxs-lookup"><span data-stu-id="12136-121">Web Services Metadata Exchange (WS-MetadataExchange)</span></span>](https://www.w3.org/TR/ws-metadata-exchange/)<br /><br /> <span data-ttu-id="12136-122">WCF 會實透過 ws-metadataexchange 來取得 XML 架構、WSDL 和 WS 原則。</span><span class="sxs-lookup"><span data-stu-id="12136-122">WCF implements WS-MetadataExchange to retrieve XML Schema, WSDL, and WS-Policy.</span></span>|  
|<span data-ttu-id="12136-123">WSDL 的 WS 定址繫結</span><span class="sxs-lookup"><span data-stu-id="12136-123">WS Addressing Binding for WSDL</span></span>|[<span data-ttu-id="12136-124">Web 服務定址 1.0 - WSDL 繫結</span><span class="sxs-lookup"><span data-stu-id="12136-124">Web Services Addressing 1.0 - WSDL Binding</span></span>](https://www.w3.org/TR/ws-addr-wsdl/)<br /><br /> <span data-ttu-id="12136-125">WCF 會在 wsdl 中實址的 WS-ADDRESSING 系結，以附加定址資訊。</span><span class="sxs-lookup"><span data-stu-id="12136-125">WCF implements WS-Addressing Binding for WSDL to attach addressing information in WSDL.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="12136-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="12136-126">See also</span></span>

- [<span data-ttu-id="12136-127">系統提供的互通性繫結所支援的 Web 服務通訊協定</span><span class="sxs-lookup"><span data-stu-id="12136-127">Web Services Protocols Supported by System-Provided Interoperability Bindings</span></span>](web-services-protocols-supported-by-system-provided-interoperability-bindings.md)
- [<span data-ttu-id="12136-128">WSDL 與原則</span><span class="sxs-lookup"><span data-stu-id="12136-128">WSDL and Policy</span></span>](wsdl-and-policy.md)
