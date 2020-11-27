---
title: 使用資料合約
description: 深入瞭解資料合約，該合約會定義每個參數或傳回類型的資料，這些資料會序列化為要在 WCF 用戶端與伺服器之間交換。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataContractAttribute class
- WCF, data
- data contracts [WCF]
ms.assetid: a3ae7b21-c15c-4c05-abd8-f483bcbf31af
ms.openlocfilehash: 97d234d094abf7666a341493f6b394c73513fa70
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289863"
---
# <a name="using-data-contracts"></a><span data-ttu-id="8bc25-103">使用資料合約</span><span class="sxs-lookup"><span data-stu-id="8bc25-103">Using Data Contracts</span></span>

<span data-ttu-id="8bc25-104">「 *資料合約* 」(Data Contract) 是服務與用戶端之間的正式合約，其中會抽象地描述要交換的資料。</span><span class="sxs-lookup"><span data-stu-id="8bc25-104">A *data contract* is a formal agreement between a service and a client that abstractly describes the data to be exchanged.</span></span> <span data-ttu-id="8bc25-105">也就是說，若要進行通訊，用戶端與服務並不需要共用相同的型別，而只需要共用相同的資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-105">That is, to communicate, the client and the service do not have to share the same types, only the same data contracts.</span></span> <span data-ttu-id="8bc25-106">資料合約會針對每個參數或傳回型別精確地定義哪些資料要序列化 (變成 XML) 才能進行交換。</span><span class="sxs-lookup"><span data-stu-id="8bc25-106">A data contract precisely defines, for each parameter or return type, what data is serialized (turned into XML) to be exchanged.</span></span>  
  
## <a name="data-contract-basics"></a><span data-ttu-id="8bc25-107">資料合約基本概念</span><span class="sxs-lookup"><span data-stu-id="8bc25-107">Data Contract Basics</span></span>  

 <span data-ttu-id="8bc25-108">Windows Communication Foundation (WCF) 預設會使用稱為「資料合約序列化程式」的序列化引擎來序列化和還原序列化資料， (將資料轉換成 XML) 。</span><span class="sxs-lookup"><span data-stu-id="8bc25-108">Windows Communication Foundation (WCF) uses a serialization engine called the Data Contract Serializer by default to serialize and deserialize data (convert it to and from XML).</span></span> <span data-ttu-id="8bc25-109">所有 .NET Framework 基本類型（例如整數和字串），以及視為基本類型（例如和）的特定類型，都 <xref:System.DateTime> <xref:System.Xml.XmlElement> 可以序列化而不需要其他準備，並視為具有預設資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-109">All .NET Framework primitive types, such as integers and strings, as well as certain types treated as primitives, such as <xref:System.DateTime> and <xref:System.Xml.XmlElement>, can be serialized with no other preparation and are considered as having default data contracts.</span></span> <span data-ttu-id="8bc25-110">許多 .NET Framework 類型也都有現有的資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-110">Many .NET Framework types also have existing data contracts.</span></span> <span data-ttu-id="8bc25-111">如需可序列化型別的完整清單，請參閱 [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-111">For a full list of serializable types, see [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md).</span></span>  
  
 <span data-ttu-id="8bc25-112">您建立的新複雜型別必須具有已針對其所定義的資料合約，才能夠進行序列化。</span><span class="sxs-lookup"><span data-stu-id="8bc25-112">New complex types that you create must have a data contract defined for them to be serializable.</span></span> <span data-ttu-id="8bc25-113">根據預設， <xref:System.Runtime.Serialization.DataContractSerializer> 會推斷資料合約，並且會序列化所有公開可見的型別。</span><span class="sxs-lookup"><span data-stu-id="8bc25-113">By default, the <xref:System.Runtime.Serialization.DataContractSerializer> infers the data contract and serializes all publicly visible types.</span></span> <span data-ttu-id="8bc25-114">型別的所有公用讀取/寫入屬性 (Property) 和欄位都會序列化。</span><span class="sxs-lookup"><span data-stu-id="8bc25-114">All public read/write properties and fields of the type are serialized.</span></span> <span data-ttu-id="8bc25-115">您可以藉由使用 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>，選擇不序列化成員。</span><span class="sxs-lookup"><span data-stu-id="8bc25-115">You can opt out members from serialization by using the <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>.</span></span> <span data-ttu-id="8bc25-116">您也可以使用 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Attribute) 明確建立資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-116">You can also explicitly create a data contract by using <xref:System.Runtime.Serialization.DataContractAttribute> and <xref:System.Runtime.Serialization.DataMemberAttribute> attributes.</span></span> <span data-ttu-id="8bc25-117">通常將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至該型別即可達成這點。</span><span class="sxs-lookup"><span data-stu-id="8bc25-117">This is normally done by applying the <xref:System.Runtime.Serialization.DataContractAttribute> attribute to the type.</span></span> <span data-ttu-id="8bc25-118">這個屬性可以套用至類別、結構和列舉型別 (Enumeration)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-118">This attribute can be applied to classes, structures, and enumerations.</span></span> <span data-ttu-id="8bc25-119">然後， <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性必須套用至資料合約型別的各個成員，以表示其為「 *資料成員*」(Data Member)，也就是這個成員應該要加以序列化。</span><span class="sxs-lookup"><span data-stu-id="8bc25-119">The <xref:System.Runtime.Serialization.DataMemberAttribute> attribute must then be applied to each member of the data contract type to indicate that it is a *data member*, that is, it should be serialized.</span></span> <span data-ttu-id="8bc25-120">如需詳細資訊，請參閱可序列化的 [類型](serializable-types.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-120">For more information, see [Serializable Types](serializable-types.md).</span></span>  
  
### <a name="example"></a><span data-ttu-id="8bc25-121">範例</span><span class="sxs-lookup"><span data-stu-id="8bc25-121">Example</span></span>  

 <span data-ttu-id="8bc25-122">下列範例會示範已經明確套用 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 屬性的服務合約 (介面)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-122">The following example shows a service contract (an interface) to which the <xref:System.ServiceModel.ServiceContractAttribute> and <xref:System.ServiceModel.OperationContractAttribute> attributes have been explicitly applied.</span></span> <span data-ttu-id="8bc25-123">此範例會示範基本型別不需要資料合約，而複雜型別則需要。</span><span class="sxs-lookup"><span data-stu-id="8bc25-123">The example shows that primitive types do not require a data contract, while a complex type does.</span></span>  
  
 [!code-csharp[C_DataContract#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#1)]
 [!code-vb[C_DataContract#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#1)]  
  
 <span data-ttu-id="8bc25-124">下列範例會示範如何透過將 `MyTypes.PurchaseOrder` 和 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至類別及其成員，以便建立 <xref:System.Runtime.Serialization.DataMemberAttribute> 型別的資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-124">The following example shows how a data contract for the `MyTypes.PurchaseOrder` type is created by applying the <xref:System.Runtime.Serialization.DataContractAttribute> and <xref:System.Runtime.Serialization.DataMemberAttribute> attributes to the class and its members.</span></span>  
  
 [!code-csharp[C_DataContract#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#2)]
 [!code-vb[C_DataContract#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#2)]  
  
### <a name="notes"></a><span data-ttu-id="8bc25-125">備註</span><span class="sxs-lookup"><span data-stu-id="8bc25-125">Notes</span></span>  

 <span data-ttu-id="8bc25-126">下列注意事項提供在建立資料合約時的考慮項目：</span><span class="sxs-lookup"><span data-stu-id="8bc25-126">The following notes provide items to consider when creating data contracts:</span></span>  
  
- <span data-ttu-id="8bc25-127"><xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 屬性只有在搭配未標記的型別使用時才會被接受。</span><span class="sxs-lookup"><span data-stu-id="8bc25-127">The <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> attribute is only honored when used with unmarked types.</span></span> <span data-ttu-id="8bc25-128">其中包含未使用 <xref:System.Runtime.Serialization.DataContractAttribute>、 <xref:System.SerializableAttribute>、 <xref:System.Runtime.Serialization.CollectionDataContractAttribute>或 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性其中一個所標記的型別，或未透過任何其他方式 (例如 <xref:System.Xml.Serialization.IXmlSerializable>) 標記為可序列化的型別。</span><span class="sxs-lookup"><span data-stu-id="8bc25-128">This includes types that are not marked with one of the <xref:System.Runtime.Serialization.DataContractAttribute>, <xref:System.SerializableAttribute>, <xref:System.Runtime.Serialization.CollectionDataContractAttribute>, or <xref:System.Runtime.Serialization.EnumMemberAttribute> attributes, or marked as serializable by any other means (such as <xref:System.Xml.Serialization.IXmlSerializable>).</span></span>  
  
- <span data-ttu-id="8bc25-129">您可以將 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Attribute) 套用至欄位和屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-129">You can apply the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute to fields, and properties.</span></span>  
  
- <span data-ttu-id="8bc25-130">成員存取層級 (內部、私密、保護或公用) 不會以任何形式影響資料合約。</span><span class="sxs-lookup"><span data-stu-id="8bc25-130">Member accessibility levels (internal, private, protected, or public) do not affect the data contract in any way.</span></span>  
  
- <span data-ttu-id="8bc25-131"><xref:System.Runtime.Serialization.DataMemberAttribute> 屬性在套用至靜態成員時會遭到忽略。</span><span class="sxs-lookup"><span data-stu-id="8bc25-131">The <xref:System.Runtime.Serialization.DataMemberAttribute> attribute is ignored if it is applied to static members.</span></span>  
  
- <span data-ttu-id="8bc25-132">取得屬性 (property-get) 的程式碼會在進行序列化時呼叫，以便讓屬性資料成員取得要進行序列化之屬性的值。</span><span class="sxs-lookup"><span data-stu-id="8bc25-132">During serialization, property-get code is called for property data members to get the value of the properties to be serialized.</span></span>  
  
- <span data-ttu-id="8bc25-133">在進行還原序列化時會先建立未初始化的物件，而不會呼叫該型別上的任何建構函式 (Constructor)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-133">During deserialization, an uninitialized object is first created, without calling any constructors on the type.</span></span> <span data-ttu-id="8bc25-134">接下來，所有的資料成員都會還原序列化。</span><span class="sxs-lookup"><span data-stu-id="8bc25-134">Then all data members are deserialized.</span></span>  
  
- <span data-ttu-id="8bc25-135">設定屬性 (property-set) 的程式碼會在進行還原序列化時呼叫，以便讓屬性資料成員設定要進行還原序列化之屬性的值。</span><span class="sxs-lookup"><span data-stu-id="8bc25-135">During deserialization, property-set code is called for property data members to set the properties to the value being deserialized.</span></span>  
  
- <span data-ttu-id="8bc25-136">若是有效的資料合約，該資料合約肯定是可能會序列化其所有資料成員。</span><span class="sxs-lookup"><span data-stu-id="8bc25-136">For a data contract to be valid, it must be possible to serialize all of its data members.</span></span> <span data-ttu-id="8bc25-137">如需可序列化型別的完整清單，請參閱 [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md)。</span><span class="sxs-lookup"><span data-stu-id="8bc25-137">For a full list of serializable types, see [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md).</span></span>  
  
     <span data-ttu-id="8bc25-138">對於泛型型別的處理方式與非泛型型別完全相同。</span><span class="sxs-lookup"><span data-stu-id="8bc25-138">Generic types are handled in exactly the same way as non-generic types.</span></span> <span data-ttu-id="8bc25-139">對於泛型參數沒有特殊的需求。</span><span class="sxs-lookup"><span data-stu-id="8bc25-139">There are no special requirements for generic parameters.</span></span> <span data-ttu-id="8bc25-140">以下列型別為例：</span><span class="sxs-lookup"><span data-stu-id="8bc25-140">For example, consider the following type.</span></span>  
  
 [!code-csharp[C_DataContract#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#3)]
 [!code-vb[C_DataContract#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#3)]  
  
 <span data-ttu-id="8bc25-141">無論用於泛型型別參數 (`T`) 的型別是否為可序列化的型別，這個型別都是可序列化的型別。</span><span class="sxs-lookup"><span data-stu-id="8bc25-141">This type is serializable whether the type used for the generic type parameter (`T`) is serializable or not.</span></span> <span data-ttu-id="8bc25-142">由於其一定可以序列化所有的資料成員，所以下列型別只有在泛型型別參數也屬於可序列化時才能進行序列化，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="8bc25-142">Because it must be possible to serialize all data members, the following type is serializable only if the generic type parameter is also serializable, as shown in the following code.</span></span>  
  
 [!code-csharp[C_DataContract#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#4)]
 [!code-vb[C_DataContract#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#4)]  
  
 <span data-ttu-id="8bc25-143">如需定義資料合約的 WCF 服務完整程式碼範例，請參閱 [Basic Data Contract](../samples/basic-data-contract.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="8bc25-143">For a complete code sample of a WCF service that defines a data contract see the [Basic Data Contract](../samples/basic-data-contract.md) sample.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8bc25-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8bc25-144">See also</span></span>

- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- [<span data-ttu-id="8bc25-145">可序列化的型別</span><span class="sxs-lookup"><span data-stu-id="8bc25-145">Serializable Types</span></span>](serializable-types.md)
- [<span data-ttu-id="8bc25-146">資料合約名稱</span><span class="sxs-lookup"><span data-stu-id="8bc25-146">Data Contract Names</span></span>](data-contract-names.md)
- [<span data-ttu-id="8bc25-147">資料合約等價</span><span class="sxs-lookup"><span data-stu-id="8bc25-147">Data Contract Equivalence</span></span>](data-contract-equivalence.md)
- [<span data-ttu-id="8bc25-148">資料成員順序</span><span class="sxs-lookup"><span data-stu-id="8bc25-148">Data Member Order</span></span>](data-member-order.md)
- [<span data-ttu-id="8bc25-149">資料合約已知型別</span><span class="sxs-lookup"><span data-stu-id="8bc25-149">Data Contract Known Types</span></span>](data-contract-known-types.md)
- [<span data-ttu-id="8bc25-150">向前相容資料合約</span><span class="sxs-lookup"><span data-stu-id="8bc25-150">Forward-Compatible Data Contracts</span></span>](forward-compatible-data-contracts.md)
- [<span data-ttu-id="8bc25-151">資料合約版本控制</span><span class="sxs-lookup"><span data-stu-id="8bc25-151">Data Contract Versioning</span></span>](data-contract-versioning.md)
- [<span data-ttu-id="8bc25-152">版本相容序列化回呼</span><span class="sxs-lookup"><span data-stu-id="8bc25-152">Version-Tolerant Serialization Callbacks</span></span>](version-tolerant-serialization-callbacks.md)
- [<span data-ttu-id="8bc25-153">資料成員預設值</span><span class="sxs-lookup"><span data-stu-id="8bc25-153">Data Member Default Values</span></span>](data-member-default-values.md)
- [<span data-ttu-id="8bc25-154">資料合約序列化程式支援的型別</span><span class="sxs-lookup"><span data-stu-id="8bc25-154">Types Supported by the Data Contract Serializer</span></span>](types-supported-by-the-data-contract-serializer.md)
- [<span data-ttu-id="8bc25-155">作法：建立類別或結構的基本資料合約</span><span class="sxs-lookup"><span data-stu-id="8bc25-155">How to: Create a Basic Data Contract for a Class or Structure</span></span>](how-to-create-a-basic-data-contract-for-a-class-or-structure.md)
