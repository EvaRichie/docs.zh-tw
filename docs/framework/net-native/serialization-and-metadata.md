---
title: 序列化和中繼資料
ms.date: 03/30/2017
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
ms.openlocfilehash: cc9adf0e6627ef3190e74fea5d4f0f3afd581811
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "81389225"
---
# <a name="serialization-and-metadata"></a><span data-ttu-id="c4344-102">序列化和中繼資料</span><span class="sxs-lookup"><span data-stu-id="c4344-102">Serialization and Metadata</span></span>

<span data-ttu-id="c4344-103">如果您的應用程式將物件序列化和還原序列化，您可能需要將項目加入至執行階段指示詞 (.rd.xml) 檔案，以確保執行階段有必要的中繼資料存在。</span><span class="sxs-lookup"><span data-stu-id="c4344-103">If your app serializes and deserializes objects, you may need to add entries to your runtime directives (.rd.xml) file to ensure that the necessary metadata is present at run time.</span></span> <span data-ttu-id="c4344-104">有兩種類別的序列化程式，在執行階段指示詞檔案中，各需要不同的處理：</span><span class="sxs-lookup"><span data-stu-id="c4344-104">There are two categories of serializers, and each requires different handling in your runtime directives file:</span></span>  
  
- <span data-ttu-id="c4344-105">反映型協力廠商序列化程式。</span><span class="sxs-lookup"><span data-stu-id="c4344-105">Reflection-based third-party serializers.</span></span> <span data-ttu-id="c4344-106">這些序列化程式需要修改您的執行階段指示詞檔案，將在下一節中討論。</span><span class="sxs-lookup"><span data-stu-id="c4344-106">These require modifications to your runtime directives file, and are discussed in the next section.</span></span>  
  
- <span data-ttu-id="c4344-107">在 .NET Framework Class Library 中找不到以反映為基礎的序列化程式。</span><span class="sxs-lookup"><span data-stu-id="c4344-107">Non-reflection-based serializers found in the .NET Framework class library.</span></span> <span data-ttu-id="c4344-108">這些序列化程式可能需要修改您的執行階段指示詞檔案，將在 [Microsoft 序列化程式](#Microsoft)一節中討論。</span><span class="sxs-lookup"><span data-stu-id="c4344-108">These may require modifications to your runtime directives file, and are discussed in the [Microsoft serializers](#Microsoft) section.</span></span>  
  
<a name="ThirdParty"></a>
## <a name="third-party-serializers"></a><span data-ttu-id="c4344-109">協力廠商序列化程式</span><span class="sxs-lookup"><span data-stu-id="c4344-109">Third-party serializers</span></span>

 <span data-ttu-id="c4344-110">協力廠商序列化程式 (包括 Newtonsoft.JSON) 通常是反映型。</span><span class="sxs-lookup"><span data-stu-id="c4344-110">Third-part serializers, including Newtonsoft.JSON, typically are reflection-based.</span></span> <span data-ttu-id="c4344-111">若指定序列化資料的二進位大型物件 (BLOB)，將會依名稱查閱目標類型的欄位，以將資料中的欄位指派給具象類型。</span><span class="sxs-lookup"><span data-stu-id="c4344-111">Given a binary large object (BLOB) of serialized data, the fields in the data are assigned to a concrete type by looking up the fields of the target type by name.</span></span> <span data-ttu-id="c4344-112">針對您嘗試在 `List<Type>` 集合中序列化或還原序列化的每個 <xref:System.Type> 物件，使用這些程式庫至少會導致 [MissingMetadataException](missingmetadataexception-class-net-native.md) 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c4344-112">At a minimum, using these libraries causes [MissingMetadataException](missingmetadataexception-class-net-native.md) exceptions for each <xref:System.Type> object that you try to serialize or deserialize in a `List<Type>` collection.</span></span>  
  
 <span data-ttu-id="c4344-113">若要為這些序列化程式解決因遺失中繼資料而導致的問題，最簡單的方法，就是收集要在單一命名空間 (例如 `App.Models`) 之下用於序列化的類型，並套用 `Serialize` 中繼資料指示詞：</span><span class="sxs-lookup"><span data-stu-id="c4344-113">The easiest way to address issues caused by missing metadata for these serializers is to collect types that will be used in serialization under a single namespace (such as `App.Models`) and apply a `Serialize` metadata directive to it:</span></span>  
  
```xml  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 <span data-ttu-id="c4344-114">如需範例中使用之語法的詳細資訊，請參閱[ \<Namespace> 元素](namespace-element-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="c4344-114">For information about the syntax used in the example, see [\<Namespace> Element](namespace-element-net-native.md).</span></span>  
  
<a name="Microsoft"></a>
## <a name="microsoft-serializers"></a><span data-ttu-id="c4344-115">Microsoft 序列化程式</span><span class="sxs-lookup"><span data-stu-id="c4344-115">Microsoft serializers</span></span>

 <span data-ttu-id="c4344-116">雖然 <xref:System.Runtime.Serialization.DataContractSerializer>、<xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 類別不會依賴反映，但確實需要根據所要序列化或還原序列化的物件來產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="c4344-116">Although the <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>, and <xref:System.Xml.Serialization.XmlSerializer> classes do not rely on reflection, they do require code to be generated based on the object to be serialized or deserialized.</span></span> <span data-ttu-id="c4344-117">適用於每個序列化程式的多載建構函式，包括用來指定要序列化或還原序列化之類型的 <xref:System.Type> 參數。</span><span class="sxs-lookup"><span data-stu-id="c4344-117">The overloaded constructors for each serializer include a <xref:System.Type> parameter that specifies the type to be serialized or deserialized.</span></span> <span data-ttu-id="c4344-118">您用來將該類型指定在程式碼中的方式，會定義您必須採取的動作，在下兩節中將進行討論。</span><span class="sxs-lookup"><span data-stu-id="c4344-118">How you specify that type in your code defines the action you must take, as discussed in the next two sections.</span></span>  
  
### <a name="typeof-used-in-the-constructor"></a><span data-ttu-id="c4344-119">用於建構函式的 typeof</span><span class="sxs-lookup"><span data-stu-id="c4344-119">typeof used in the constructor</span></span>

 <span data-ttu-id="c4344-120">如果您呼叫這些序列化類別的函式，並在方法呼叫中包含 c # [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator)運算子，**則不需要執行任何額外的工作**。</span><span class="sxs-lookup"><span data-stu-id="c4344-120">If you call a constructor of these serialization classes and include the C# [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) operator in the method call, **you do not have to do any additional work**.</span></span> <span data-ttu-id="c4344-121">例如，在對序列化類別建構函式進行的下列每個呼叫中，`typeof` 關鍵字會用來做為傳遞至建構函式之運算式的一部分。</span><span class="sxs-lookup"><span data-stu-id="c4344-121">For example, in each of the following calls to a serialization class constructor, the `typeof` keyword is used as part of the expression passed to the constructor.</span></span>  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 <span data-ttu-id="c4344-122">.NET Native 編譯器會自動處理此程式碼。</span><span class="sxs-lookup"><span data-stu-id="c4344-122">The .NET Native compiler will automatically handle this code.</span></span>  
  
### <a name="typeof-used-outside-the-constructor"></a><span data-ttu-id="c4344-123">在建構函式外部使用的 typeof</span><span class="sxs-lookup"><span data-stu-id="c4344-123">typeof used outside the constructor</span></span>

 <span data-ttu-id="c4344-124">如果您呼叫這些序列化類別的函式，並在提供給此函式參數的運算式外部使用 c # [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator)運算子 <xref:System.Type> （如下列程式碼所示），則 .NET Native 編譯器無法解析類型：</span><span class="sxs-lookup"><span data-stu-id="c4344-124">If you call a constructor of these serialization classes and use the C# [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) operator outside the expression supplied to the constructor’s <xref:System.Type> parameter, as in the following code, the .NET Native compiler cannot resolve the type:</span></span>  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 <span data-ttu-id="c4344-125">在此情況下，您必須加入像下列這樣的項目，以在執行階段指示詞檔案中指定類型：</span><span class="sxs-lookup"><span data-stu-id="c4344-125">In this case, you must specify the type in the runtime directives file by adding an entry like this:</span></span>  
  
```xml  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 <span data-ttu-id="c4344-126">同樣地，如果您呼叫和之類的函 <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29> 式，並提供要序列化的其他物件陣列（如下列程式碼所示）， <xref:System.Type> 則 .NET Native 編譯器無法解析這些類型。</span><span class="sxs-lookup"><span data-stu-id="c4344-126">Similarly, if you call a constructor such as <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29> and provide an array of additional <xref:System.Type> objects to serialize, as in the following code, the .NET Native compiler cannot resolve these types.</span></span>  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
<span data-ttu-id="c4344-127">將每個類型的下列專案加入至執行時間指示詞檔案：</span><span class="sxs-lookup"><span data-stu-id="c4344-127">Add entries such as the following for each type to the runtime directives file:</span></span>  
  
```xml  
<Type Name="t" Browse="Required Public" />  
```  
  
<span data-ttu-id="c4344-128">如需範例中使用之語法的詳細資訊，請參閱[ \<Type> 元素](type-element-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="c4344-128">For information about the syntax used in the example, see [\<Type> Element](type-element-net-native.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c4344-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c4344-129">See also</span></span>

- [<span data-ttu-id="c4344-130">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="c4344-130">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)
- [<span data-ttu-id="c4344-131">執行階段指示詞項目</span><span class="sxs-lookup"><span data-stu-id="c4344-131">Runtime Directive Elements</span></span>](runtime-directive-elements.md)
- [<span data-ttu-id="c4344-132">\<Type>元素</span><span class="sxs-lookup"><span data-stu-id="c4344-132">\<Type> Element</span></span>](type-element-net-native.md)
- [<span data-ttu-id="c4344-133">\<Namespace>元素</span><span class="sxs-lookup"><span data-stu-id="c4344-133">\<Namespace> Element</span></span>](namespace-element-net-native.md)
