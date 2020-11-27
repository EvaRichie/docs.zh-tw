---
title: 作法：建立類別或結構的基本資料合約
description: 遵循此範例以瞭解如何使用 DataContractAttribute 屬性，在 WCF 中使用類別或結構來建立資料合約。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataMemberAttribute
- DataContractAttribute class
- data contracts [WCF], creating for a class or structure
ms.assetid: bc464889-3070-4a2f-91d2-e788a0f686a7
ms.openlocfilehash: 5634eb3d3ec18d95fd7d6b3c89b572ab4f5b8eca
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254034"
---
# <a name="how-to-create-a-basic-data-contract-for-a-class-or-structure"></a><span data-ttu-id="b1317-103">作法：建立類別或結構的基本資料合約</span><span class="sxs-lookup"><span data-stu-id="b1317-103">How to: Create a Basic Data Contract for a Class or Structure</span></span>

<span data-ttu-id="b1317-104">本主題將示範使用類別或結構來建立資料合約的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="b1317-104">This topic shows the basic steps to create a data contract using a class or structure.</span></span> <span data-ttu-id="b1317-105">如需資料合約和其使用方式的詳細資訊，請參閱 [使用資料合約](using-data-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="b1317-105">For more information about data contracts and how they are used, see [Using Data Contracts](using-data-contracts.md).</span></span>  
  
 <span data-ttu-id="b1317-106">如需逐步解說建立基本 Windows Communication Foundation (WCF) 服務和用戶端之步驟的教學課程，請參閱 [消費者入門教學](../getting-started-tutorial.md)課程。</span><span class="sxs-lookup"><span data-stu-id="b1317-106">For a tutorial that walks through the steps of creating a basic Windows Communication Foundation (WCF) service and client, see the [Getting Started Tutorial](../getting-started-tutorial.md).</span></span> <span data-ttu-id="b1317-107">如需包含基本服務和用戶端的實用範例應用程式，請參閱 [基本資料合約](../samples/basic-data-contract.md)。</span><span class="sxs-lookup"><span data-stu-id="b1317-107">For a working sample application that consists of a basic service and client, see [Basic Data Contract](../samples/basic-data-contract.md).</span></span>  
  
### <a name="to-create-a-basic-data-contract-for-a-class-or-structure"></a><span data-ttu-id="b1317-108">建立類別或結構的基本資料合約</span><span class="sxs-lookup"><span data-stu-id="b1317-108">To create a basic data contract for a class or structure</span></span>  
  
1. <span data-ttu-id="b1317-109">請將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至類別，以宣告型別具有資料合約。</span><span class="sxs-lookup"><span data-stu-id="b1317-109">Declare that the type has a data contract by applying the <xref:System.Runtime.Serialization.DataContractAttribute> attribute to the class.</span></span> <span data-ttu-id="b1317-110">請注意，所有公用型別 (包括不含屬性的公用型別) 都是可序列化的。</span><span class="sxs-lookup"><span data-stu-id="b1317-110">Note that all public types, including those without attributes, are serializable.</span></span> <span data-ttu-id="b1317-111">如果沒有 <xref:System.Runtime.Serialization.DataContractSerializer> 屬性，<xref:System.Runtime.Serialization.DataContractAttribute> 會推斷資料合約。</span><span class="sxs-lookup"><span data-stu-id="b1317-111">The <xref:System.Runtime.Serialization.DataContractSerializer> infers a data contract if the <xref:System.Runtime.Serialization.DataContractAttribute> attribute is absent.</span></span> <span data-ttu-id="b1317-112">如需詳細資訊，請參閱可序列化的 [類型](serializable-types.md)。</span><span class="sxs-lookup"><span data-stu-id="b1317-112">For more information, see [Serializable Types](serializable-types.md).</span></span>  
  
2. <span data-ttu-id="b1317-113">藉由將 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Attribute) 套用至各個成員，定義序列化的成員 (屬性 (Property)、欄位或事件)。</span><span class="sxs-lookup"><span data-stu-id="b1317-113">Define the members (properties, fields, or events) that are serialized by applying the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute to each member.</span></span> <span data-ttu-id="b1317-114">這些成員稱為資料成員。</span><span class="sxs-lookup"><span data-stu-id="b1317-114">These members are called data members.</span></span> <span data-ttu-id="b1317-115">根據預設，所有公用型別都是可序列化的。</span><span class="sxs-lookup"><span data-stu-id="b1317-115">By default, all public types are serializable.</span></span> <span data-ttu-id="b1317-116">如需詳細資訊，請參閱可序列化的 [類型](serializable-types.md)。</span><span class="sxs-lookup"><span data-stu-id="b1317-116">For more information, see [Serializable Types](serializable-types.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="b1317-117">您可以將 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性套用至私用欄位，造成資料對他人公開。</span><span class="sxs-lookup"><span data-stu-id="b1317-117">You can apply the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute to private fields, causing the data to be exposed to others.</span></span> <span data-ttu-id="b1317-118">請確定成員沒有包含敏感性資料。</span><span class="sxs-lookup"><span data-stu-id="b1317-118">Be sure that the member does not contain sensitive data.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b1317-119">範例</span><span class="sxs-lookup"><span data-stu-id="b1317-119">Example</span></span>  

 <span data-ttu-id="b1317-120">下列範例說明如何將 `Person` 和 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至類別和其成員，以建立 <xref:System.Runtime.Serialization.DataMemberAttribute> 型別的資料合約。</span><span class="sxs-lookup"><span data-stu-id="b1317-120">The following example shows how to create a data contract for the `Person` type by applying the <xref:System.Runtime.Serialization.DataContractAttribute> and <xref:System.Runtime.Serialization.DataMemberAttribute> attributes to the class and its members.</span></span>  
  
 [!code-csharp[DataContractAttribute#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#2)]
 [!code-vb[DataContractAttribute#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#2)]  
  
## <a name="see-also"></a><span data-ttu-id="b1317-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b1317-121">See also</span></span>

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [<span data-ttu-id="b1317-122">使用資料合約</span><span class="sxs-lookup"><span data-stu-id="b1317-122">Using Data Contracts</span></span>](using-data-contracts.md)
- [<span data-ttu-id="b1317-123">快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="b1317-123">Getting Started Tutorial</span></span>](../getting-started-tutorial.md)
- [<span data-ttu-id="b1317-124">快速入門</span><span class="sxs-lookup"><span data-stu-id="b1317-124">Getting Started</span></span>](../samples/getting-started-sample.md)
