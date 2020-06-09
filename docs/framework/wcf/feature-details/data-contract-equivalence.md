---
title: 資料合約等價
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], equivalence
ms.assetid: f06f3c7e-c235-4ec1-b200-68142edf1ed1
ms.openlocfilehash: b96a32f5e11ed4808f8f35d02802afd1f48c3072
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601318"
---
# <a name="data-contract-equivalence"></a><span data-ttu-id="a8c9b-102">資料合約等價</span><span class="sxs-lookup"><span data-stu-id="a8c9b-102">Data Contract Equivalence</span></span>
<span data-ttu-id="a8c9b-103">若要讓用戶端成功地將特定型別的資料傳送至服務，或讓服務成功地將資料傳送至用戶端，傳送的型別不一定要存在於接收端。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-103">For a client to successfully send data of a certain type to a service, or a service to successfully send data to a client, the sent type does not necessarily have to exist on the receiving end.</span></span> <span data-ttu-id="a8c9b-104">唯一的需求是這兩個型別的資料合約必須相等 </span><span class="sxs-lookup"><span data-stu-id="a8c9b-104">The only requirement is that the data contracts of both types be equivalent.</span></span> <span data-ttu-id="a8c9b-105">（有時候不需要嚴格的等價，如[資料合約版本控制](data-contract-versioning.md)中所述）。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-105">(Sometimes, strict equivalence is not required, as discussed in [Data Contract Versioning](data-contract-versioning.md).)</span></span>  
  
 <span data-ttu-id="a8c9b-106">若要讓資料合約相等，則資料合約必須具有相同的命名空間和名稱。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-106">For data contracts to be equivalent, they must have the same namespace and name.</span></span> <span data-ttu-id="a8c9b-107">此外，某一端的每個資料成員都必須有另一端的對等資料成員。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-107">Additionally, each data member on one side must have an equivalent data member on the other side.</span></span>  
  
 <span data-ttu-id="a8c9b-108">若要讓資料成員相等，則資料成員必須具有相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-108">For data members to be equivalent, they must have the same name.</span></span> <span data-ttu-id="a8c9b-109">此外，還必須有相同的資料型別，也就是說，它們的資料合約必須相等。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-109">Additionally, they must represent the same type of data; that is, their data contracts must be equivalent.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="a8c9b-110">請注意，資料合約名稱、命名空間和資料成員名稱必須區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-110">Note that data contract names and namespaces, as well as data member names, are case-sensitive.</span></span>  
  
 <span data-ttu-id="a8c9b-111">如需有關資料合約名稱和命名空間以及資料成員名稱的詳細資訊，請參閱[資料合約名稱](data-contract-names.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-111">For more information about data contract names and namespaces, as well as data member names, see [Data Contract Names](data-contract-names.md).</span></span>  
  
 <span data-ttu-id="a8c9b-112">如果兩個型別存在於同一端 (傳送者或接收者)，但資料合約不相等 (例如，具有不同的資料成員)，則不應該為它們指定相同的名稱和命名空間。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-112">If two types exist on the same side (sender or receiver) and their data contracts are not equivalent (for example, they have different data members), you should not give them the same name and namespace.</span></span> <span data-ttu-id="a8c9b-113">這樣做可能會導致擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-113">Doing so may cause exceptions to be thrown.</span></span>  
  
 <span data-ttu-id="a8c9b-114">下列型別的資料合約是相等的：</span><span class="sxs-lookup"><span data-stu-id="a8c9b-114">The data contracts for the following types are equivalent:</span></span>  
  
 [!code-csharp[C_DataContractNames#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#5)]
 [!code-vb[C_DataContractNames#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#5)]  
  
## <a name="data-member-order-and-data-contract-equivalence"></a><span data-ttu-id="a8c9b-115">資料成員順序和資料合約等價</span><span class="sxs-lookup"><span data-stu-id="a8c9b-115">Data Member Order and Data Contract equivalence</span></span>  
 <span data-ttu-id="a8c9b-116">使用 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 類別的 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性，可能會影響資料合約等價。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-116">Using the <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> property of the <xref:System.Runtime.Serialization.DataMemberAttribute> class may affect data contract equivalence.</span></span> <span data-ttu-id="a8c9b-117">資料合約必須以相同順序顯示成員，才會相等。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-117">The data contracts must have members that appear in the same order to be equivalent.</span></span> <span data-ttu-id="a8c9b-118">預設順序是字母順序。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-118">The default order is alphabetical.</span></span> <span data-ttu-id="a8c9b-119">如需詳細資訊，請參閱[資料成員順序](data-member-order.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-119">For more information, see [Data Member Order](data-member-order.md).</span></span>  
  
 <span data-ttu-id="a8c9b-120">例如，下列程式碼會產生對等的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-120">For example, the following code results in equivalent data contracts.</span></span>  
  
 [!code-csharp[C_DataContractNames#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#6)]
 [!code-vb[C_DataContractNames#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#6)]  
  
 <span data-ttu-id="a8c9b-121">不過，下列程式碼不會產生對等的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-121">However, the following does not result in an equivalent data contract.</span></span>  
  
 [!code-csharp[C_DataContractNames#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#7)]
 [!code-vb[C_DataContractNames#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#7)]  
  
## <a name="inheritance-interfaces-and-data-contract-equivalence"></a><span data-ttu-id="a8c9b-122">繼承、介面和資料合約等價</span><span class="sxs-lookup"><span data-stu-id="a8c9b-122">Inheritance, Interfaces, and Data Contract Equivalence</span></span>  
 <span data-ttu-id="a8c9b-123">判斷等價時，繼承自另一個資料合約的資料合約會被視為只是一個包含所有來自基底型別之資料成員的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-123">When determining equivalence, a data contract that inherits from another data contract is treated as if it is just one data contract that includes all of the data members from the base type.</span></span> <span data-ttu-id="a8c9b-124">請記住，資料成員的順序必須相符，而且基底型別成員的順序必須在衍生型別成員之前。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-124">Keep in mind that the order of the data members must match and that base type members precede derived type members in the order.</span></span> <span data-ttu-id="a8c9b-125">此外，如果兩個資料成員有相同的順序值，則這些資料成員的順序為字母順序 (如下列程式碼範例)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-125">Furthermore, if, as in the following code example, two data members have the same order value, the ordering for those data members is alphabetical.</span></span> <span data-ttu-id="a8c9b-126">如需詳細資訊，請參閱[資料成員順序](data-member-order.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-126">For more information, see [Data Member Order](data-member-order.md).</span></span>  
  
 <span data-ttu-id="a8c9b-127">在下列範例中，`Employee` 型別的資料合約與 `Worker` 型別的資料合約相等。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-127">In the following example, the data contract for type `Employee` is equivalent to the data contract for the type `Worker`.</span></span>  
  
 [!code-csharp[C_DataContractNames#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#8)]
 [!code-vb[C_DataContractNames#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#8)]  
  
 <span data-ttu-id="a8c9b-128">在用戶端和服務之間傳遞參數和傳回值時，如果接收端點需要來自衍生類別的資料合約，則無法傳送來自基底類別的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-128">When passing parameters and return values between a client and a service, a data contract from a base class cannot be sent when the receiving endpoint expects a data contract from a derived class.</span></span> <span data-ttu-id="a8c9b-129">這符合物件導向程式設計原則。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-129">This is in accordance with object-oriented programming tenets.</span></span> <span data-ttu-id="a8c9b-130">在上述範例中，當需要時， `Person` 無法傳送類型的物件 `Employee` 。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-130">In the previous example, an object of type `Person` cannot be sent when an `Employee` is expected.</span></span>  
  
 <span data-ttu-id="a8c9b-131">如果需要來自基底類別的資料合約，只有在接收端點使用 <xref:System.Runtime.Serialization.KnownTypeAttribute> 知道衍生型別時，才能傳送來自衍生類別的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-131">A data contract from a derived class can be sent when a data contract from a base class is expected, but only if the receiving endpoint "knows" of the derived type using the <xref:System.Runtime.Serialization.KnownTypeAttribute>.</span></span> <span data-ttu-id="a8c9b-132">如需詳細資訊，請參閱[資料合約已知類型](data-contract-known-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-132">For more information, see [Data Contract Known Types](data-contract-known-types.md).</span></span> <span data-ttu-id="a8c9b-133">在上一個範例中，如果需要 `Employee`，只有在接收者程式碼使用 `Person` 將 <xref:System.Runtime.Serialization.KnownTypeAttribute> 型別的物件包含在已知型別的清單時，才能傳送它。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-133">In the previous example, an object of type `Employee` can be sent when a `Person` is expected, but only if the receiver code employs the <xref:System.Runtime.Serialization.KnownTypeAttribute> to include it in the list of known types.</span></span>  
  
 <span data-ttu-id="a8c9b-134">在應用程式之間傳遞參數和傳回值時，如果預期型別是介面，它相當於 <xref:System.Object> 型別的預期型別。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-134">When passing parameters and return values between applications, if the expected type is an interface, it is equivalent to the expected type being of type <xref:System.Object>.</span></span> <span data-ttu-id="a8c9b-135">因為每個型別最終都是衍生自 <xref:System.Object>，所以每個資料合約最終都會衍生自 <xref:System.Object> 的資料合約。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-135">Because every type ultimately derives from <xref:System.Object>, every data contract ultimately derives from the data contract for <xref:System.Object>.</span></span> <span data-ttu-id="a8c9b-136">因此，如果需要介面，則可以傳遞任何資料合約類型。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-136">Thus, any data contract type can be passed when an interface is expected.</span></span> <span data-ttu-id="a8c9b-137">若要成功使用介面，必須執行其他步驟。如需詳細資訊，請參閱[資料合約已知類型](data-contract-known-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a8c9b-137">Additional steps are required to successfully work with interfaces; for more information, see [Data Contract Known Types](data-contract-known-types.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a8c9b-138">請參閱</span><span class="sxs-lookup"><span data-stu-id="a8c9b-138">See also</span></span>

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [<span data-ttu-id="a8c9b-139">資料成員順序</span><span class="sxs-lookup"><span data-stu-id="a8c9b-139">Data Member Order</span></span>](data-member-order.md)
- [<span data-ttu-id="a8c9b-140">資料合約已知型別</span><span class="sxs-lookup"><span data-stu-id="a8c9b-140">Data Contract Known Types</span></span>](data-contract-known-types.md)
- [<span data-ttu-id="a8c9b-141">資料合約名稱</span><span class="sxs-lookup"><span data-stu-id="a8c9b-141">Data Contract Names</span></span>](data-contract-names.md)
