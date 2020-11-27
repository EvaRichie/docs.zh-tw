---
title: 資料成員預設值
description: 瞭解當資料成員有 .NET Framework 預設值時，如何從序列化資料中省略該資料成員。 WCF 可以藉由不序列化預設值來改善效能。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data members [WCF], default values
- data members [WCF]
ms.assetid: 53a3b505-4b27-444b-b079-0eb84a97cfd8
ms.openlocfilehash: 98b19fdabebeb8a1d43a66a192cb523b82ada618
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261991"
---
# <a name="data-member-default-values"></a><span data-ttu-id="b6d11-104">資料成員預設值</span><span class="sxs-lookup"><span data-stu-id="b6d11-104">Data Member Default Values</span></span>

<span data-ttu-id="b6d11-105">在 .NET Framework 中，類型具有 *預設值* 的概念。</span><span class="sxs-lookup"><span data-stu-id="b6d11-105">In the .NET Framework, types have a concept of *default values*.</span></span> <span data-ttu-id="b6d11-106">例如，任何參考型別的預設值為 `null`，整數型別則為零。</span><span class="sxs-lookup"><span data-stu-id="b6d11-106">For example, for any reference type the default value is `null`, and for an integer type it is zero.</span></span> <span data-ttu-id="b6d11-107">有時候資料成員設為預設值時，會需要從序列化資料中省略該成員。</span><span class="sxs-lookup"><span data-stu-id="b6d11-107">It is occasionally desirable to omit a data member from serialized data when it is set to its default value.</span></span> <span data-ttu-id="b6d11-108">因為此成員為預設值，而實際值不需要序列化，因此這樣做可促進效能。</span><span class="sxs-lookup"><span data-stu-id="b6d11-108">Because the member has a default value, an actual value need not be serialized; this has a performance advantage.</span></span>  
  
 <span data-ttu-id="b6d11-109">若要省略序列化資料中的成員，請將 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 屬性 (Attribute) 的 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Property) 設為 `false` (預設值為 `true`)。</span><span class="sxs-lookup"><span data-stu-id="b6d11-109">To omit a member from serialized data, set the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> property of the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute to `false` (the default is `true`).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b6d11-110">您應該在有特殊需要時，將 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 屬性設定為 `false`，例如為了互通性或縮減資料大小。</span><span class="sxs-lookup"><span data-stu-id="b6d11-110">You should set the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> property to `false` if there is a specific need to do so, such as for interoperability or data size reduction.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b6d11-111">範例</span><span class="sxs-lookup"><span data-stu-id="b6d11-111">Example</span></span>  

 <span data-ttu-id="b6d11-112">以下程式碼中有數個成員的 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 都設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="b6d11-112">The following code has several members with the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> set to `false`.</span></span>  
  
 [!code-csharp[DataMemberAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datamemberattribute/cs/overview.cs#4)]
 [!code-vb[DataMemberAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datamemberattribute/vb/overview.vb#4)]  
  
 <span data-ttu-id="b6d11-113">如果這個類別的執行個體已序列化，則結果可能如下：`employeeName` 和 `employeeID` 將會序列化。</span><span class="sxs-lookup"><span data-stu-id="b6d11-113">If an instance of this class is serialized, the result is as follows: `employeeName` and `employeeID` is serialized.</span></span> <span data-ttu-id="b6d11-114">`employeeName` 的 null 值和 `employeeID` 的零值將明確成為序列化資料的一部分。</span><span class="sxs-lookup"><span data-stu-id="b6d11-114">The null value for `employeeName` and the zero value for `employeeID` is explicitly part of the serialized data.</span></span> <span data-ttu-id="b6d11-115">不過，`position`、`salary` 和 `bonus` 成員都不會序列化。</span><span class="sxs-lookup"><span data-stu-id="b6d11-115">However, the `position`, `salary`, and `bonus` members are not serialized.</span></span> <span data-ttu-id="b6d11-116">最後，即使 `targetSalary` 屬性設為 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>，`false` 通常仍會序列化，因為 57800 不符合 .NET 預設的整數值，也就是零。</span><span class="sxs-lookup"><span data-stu-id="b6d11-116">Finally, `targetSalary` is serialized as usual, even though the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> property is set to `false`, because 57800 does not match the .NET default value for an integer, which is zero.</span></span>  
  
### <a name="xml-representation"></a><span data-ttu-id="b6d11-117">XML 表示</span><span class="sxs-lookup"><span data-stu-id="b6d11-117">XML Representation</span></span>  

 <span data-ttu-id="b6d11-118">如果之前的範例已序列化為 XML，則表示方式將類似以下內容：</span><span class="sxs-lookup"><span data-stu-id="b6d11-118">If the previous example is serialized to XML, the representation is similar to the following.</span></span>  
  
```xml  
<Employee>  
   <employeeName xsi:nil="true" />  
   <employeeID>0</employeeID>  
<targetSalary>57800</targetSalary>  
</Employee>  
```  
  
 <span data-ttu-id="b6d11-119">`xsi:nil` 屬性 (Attribute) 是全球資訊網協會 (W3C) XML 結構描述執行個體命名空間中的特殊屬性，會提供可互通的方式明確表示 null 值。</span><span class="sxs-lookup"><span data-stu-id="b6d11-119">The `xsi:nil` attribute is a special attribute in the World Wide Web Consortium (W3C) XML Schema instance namespace that provides an interoperable way to explicitly represent a null value.</span></span> <span data-ttu-id="b6d11-120">請注意，XML 中沒有任何關於職位、薪資及獎金資料成員的資訊。</span><span class="sxs-lookup"><span data-stu-id="b6d11-120">Note that there is no information at all in the XML about position, salary, and bonus data members.</span></span> <span data-ttu-id="b6d11-121">接收端可以分別將這些成員解譯為 `null`、零和 `null`。</span><span class="sxs-lookup"><span data-stu-id="b6d11-121">The receiving end can interpret these as `null`, zero, and `null`, respectively.</span></span> <span data-ttu-id="b6d11-122">不過不保證協力廠商的還原序列化程式能夠正確解譯，這也是不建議使用此模式的原因。</span><span class="sxs-lookup"><span data-stu-id="b6d11-122">There is no guarantee that a third-party deserializer can make the correct interpretation, which is why this pattern is not recommended.</span></span> <span data-ttu-id="b6d11-123"><xref:System.Runtime.Serialization.DataContractSerializer> 類別永遠會為遺漏的值選取正確解譯。</span><span class="sxs-lookup"><span data-stu-id="b6d11-123">The <xref:System.Runtime.Serialization.DataContractSerializer> class always selects the correct interpretation for missing values.</span></span>  
  
### <a name="interaction-with-isrequired"></a><span data-ttu-id="b6d11-124">與 IsRequired 互動</span><span class="sxs-lookup"><span data-stu-id="b6d11-124">Interaction with IsRequired</span></span>  

 <span data-ttu-id="b6d11-125">如同 [資料合約版本](data-contract-versioning.md)設定中所討論的屬性，屬性 <xref:System.Runtime.Serialization.DataMemberAttribute> <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> (預設值為 `false`) 。</span><span class="sxs-lookup"><span data-stu-id="b6d11-125">As discussed in [Data Contract Versioning](data-contract-versioning.md), the <xref:System.Runtime.Serialization.DataMemberAttribute> attribute has an <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> property (the default is `false`).</span></span> <span data-ttu-id="b6d11-126">這個屬性會表示還原序列化指定的資料成員時，是否必須以序列化的資料表示該成員。</span><span class="sxs-lookup"><span data-stu-id="b6d11-126">The property indicates whether a given data member must be present in the serialized data when it is being deserialized.</span></span> <span data-ttu-id="b6d11-127">如果 `IsRequired` 設為 `true` (表示一定要使用一個值)，且 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 設為 `false` (表示如果使用預設值，則不需要使用該值)，因為結果會互相矛盾，所以無法序列化此資料成員的預設值。</span><span class="sxs-lookup"><span data-stu-id="b6d11-127">If `IsRequired` is set to `true`, (which indicates that a value must be present) and <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> is set to `false` (indicating that the value must not be present if it is set to its default value), default values for this data member cannot be serialized because the results would be contradictory.</span></span> <span data-ttu-id="b6d11-128">如果這類資料成員設為其預設值 (通常為 `null` 或零)，並且嘗試進行序列化，則會擲回 <xref:System.Runtime.Serialization.SerializationException>。</span><span class="sxs-lookup"><span data-stu-id="b6d11-128">If such a data member is set to its default value (usually `null` or zero) and a serialization is attempted, a <xref:System.Runtime.Serialization.SerializationException> is thrown.</span></span>  
  
### <a name="schema-representation"></a><span data-ttu-id="b6d11-129">結構描述表示</span><span class="sxs-lookup"><span data-stu-id="b6d11-129">Schema Representation</span></span>  

 <span data-ttu-id="b6d11-130">當屬性設定為時，XML 架構定義語言 (XSD) 架構表示資料成員的詳細 `EmitDefaultValue` `false` 資料，將在 [資料合約架構參考](data-contract-schema-reference.md)中討論。</span><span class="sxs-lookup"><span data-stu-id="b6d11-130">The details of the XML Schema definition language (XSD) schema representation of data members when the `EmitDefaultValue` property is set to `false` are discussed in [Data Contract Schema Reference](data-contract-schema-reference.md).</span></span> <span data-ttu-id="b6d11-131">不過，以下提供簡要的概觀。</span><span class="sxs-lookup"><span data-stu-id="b6d11-131">However, the following is a brief overview:</span></span>  
  
- <span data-ttu-id="b6d11-132">當 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 設定為時 `false` ，它會在架構中表示為 WINDOWS COMMUNICATION FOUNDATION (WCF) 的特定注釋。</span><span class="sxs-lookup"><span data-stu-id="b6d11-132">When the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> is set to `false`, it is represented in the schema as an annotation specific to Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="b6d11-133">目前沒有可互通的方式能表示這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b6d11-133">There is no interoperable way to represent this information.</span></span> <span data-ttu-id="b6d11-134">特別是結構描述中的 "default" 屬性 (Attribute) 不是用於此目的時，`minOccurs` 屬性只會受到 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 設定的影響，而 `nillable` 屬性只會受到資料成員的型別影響。</span><span class="sxs-lookup"><span data-stu-id="b6d11-134">In particular, the "default" attribute in the schema is not used for this purpose, the `minOccurs` attribute is affected only by the <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> setting, and the `nillable` attribute is affected only by the type of the data member.</span></span>  
  
- <span data-ttu-id="b6d11-135">實際使用的預設值不會在結構描述中表示。</span><span class="sxs-lookup"><span data-stu-id="b6d11-135">The actual default value to use is not present in the schema.</span></span> <span data-ttu-id="b6d11-136">端看接收端點如何適當地解譯遺失的項目而定。</span><span class="sxs-lookup"><span data-stu-id="b6d11-136">It is up to the receiving endpoint to appropriately interpret a missing element.</span></span>  
  
 <span data-ttu-id="b6d11-137">在架構匯入時， <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> `false` 只要偵測到先前提及的 WCF 專屬注釋，屬性會自動設定為。</span><span class="sxs-lookup"><span data-stu-id="b6d11-137">On schema import, the <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> property is automatically set to `false` whenever the WCF-specific annotation mentioned previously is detected.</span></span> <span data-ttu-id="b6d11-138">針對將屬性設為的參考型別，它也會設定為，以 `false` `nillable` `false` 支援使用 ASP.NET Web 服務時經常發生的特定互通性案例。</span><span class="sxs-lookup"><span data-stu-id="b6d11-138">It is also set to `false` for reference types that have the `nillable` property set to `false` to support specific interoperability scenarios that commonly occur when consuming ASP.NET Web services.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b6d11-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b6d11-139">See also</span></span>

- <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
