---
title: 使用資料合約解析程式
ms.date: 03/30/2017
ms.assetid: 2e68a16c-36f0-4df4-b763-32021bff2b89
ms.openlocfilehash: 20abd4d928fc51eb359949ecbb216615e9659b7f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595020"
---
# <a name="using-a-data-contract-resolver"></a><span data-ttu-id="a6572-102">使用資料合約解析程式</span><span class="sxs-lookup"><span data-stu-id="a6572-102">Using a Data Contract Resolver</span></span>
<span data-ttu-id="a6572-103">資料合約解析程式可讓您動態設定已知型別。</span><span class="sxs-lookup"><span data-stu-id="a6572-103">A data contract resolver allows you to configure known types dynamically.</span></span> <span data-ttu-id="a6572-104">在序列化或還原序列化資料合約未預期的型別時，就會需要已知型別。</span><span class="sxs-lookup"><span data-stu-id="a6572-104">Known types are required when serializing or deserializing a type not expected by a data contract.</span></span> <span data-ttu-id="a6572-105">如需已知類型的詳細資訊，請參閱[資料合約已知類型](data-contract-known-types.md)。</span><span class="sxs-lookup"><span data-stu-id="a6572-105">For more information about known types, see [Data Contract Known Types](data-contract-known-types.md).</span></span> <span data-ttu-id="a6572-106">已知型別通常會以靜態方式指定。</span><span class="sxs-lookup"><span data-stu-id="a6572-106">Known types are normally specified statically.</span></span> <span data-ttu-id="a6572-107">這表示，實作作業時，您必須知道此作業可能會接收的所有可能型別。</span><span class="sxs-lookup"><span data-stu-id="a6572-107">This means you would have to know all the possible types an operation may receive while implementing the operation.</span></span> <span data-ttu-id="a6572-108">不過，這項條件在某些情況中並不成立，此時，能夠以動態方式指定已知型別就很重要。</span><span class="sxs-lookup"><span data-stu-id="a6572-108">There are scenarios in which this is not true and being able to specify known types dynamically is important.</span></span>  
  
## <a name="creating-a-data-contract-resolver"></a><span data-ttu-id="a6572-109">建立資料合約解析程式</span><span class="sxs-lookup"><span data-stu-id="a6572-109">Creating a Data Contract Resolver</span></span>  
 <span data-ttu-id="a6572-110">建立資料合約解析程式需要實作兩個方法：<xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 與 <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A>。</span><span class="sxs-lookup"><span data-stu-id="a6572-110">Creating a data contract resolver involves implementing two methods, <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> and <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A>.</span></span> <span data-ttu-id="a6572-111">這兩個方法會分別實作序列化與還原序列化期間使用的回呼。</span><span class="sxs-lookup"><span data-stu-id="a6572-111">These two methods implement callbacks that are used during serialization and deserialization, respectively.</span></span> <span data-ttu-id="a6572-112"><xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> 方法會在序列化期間叫用，此方法會取得資料合約型別，並且對應到 `xsi:type` 名稱與命名空間。</span><span class="sxs-lookup"><span data-stu-id="a6572-112">The <xref:System.Runtime.Serialization.DataContractResolver.TryResolveType%2A> method is invoked during serialization and takes a data contract type and maps it to an `xsi:type` name and namespace.</span></span> <span data-ttu-id="a6572-113"><xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> 方法會在還原序列化期間叫用，此方法會取得 `xsi:type` 名稱與命名空間，並且解析為資料合約型別。</span><span class="sxs-lookup"><span data-stu-id="a6572-113">The <xref:System.Runtime.Serialization.DataContractResolver.ResolveName%2A> method is invoked during deserialization and takes an `xsi:type` name and namespace and resolves it to a data contract type.</span></span> <span data-ttu-id="a6572-114">這兩個方法都有 `knownTypeResolver` 參數，可以使用您實作中預設的已知型別解析程式。</span><span class="sxs-lookup"><span data-stu-id="a6572-114">Both of these methods have a `knownTypeResolver` parameter that can be used to use the default known type resolver in your implementation.</span></span>  
  
 <span data-ttu-id="a6572-115">下列範例顯示如何實作 <xref:System.Runtime.Serialization.DataContractResolver> 的對應，處理衍生自 `Customer` 資料合約型別，命名為 `Person` 的資料合約型別。</span><span class="sxs-lookup"><span data-stu-id="a6572-115">The following example shows how to implement a <xref:System.Runtime.Serialization.DataContractResolver> to map to and from a data contract type named `Customer` derived from a data contract type `Person`.</span></span>  
  
```csharp  
public class MyCustomerResolver : DataContractResolver  
{  
    public override bool TryResolveType(Type dataContractType, Type declaredType, DataContractResolver knownTypeResolver, out XmlDictionaryString typeName, out XmlDictionaryString typeNamespace)  
    {  
        if (dataContractType == typeof(Customer))  
        {  
            XmlDictionary dictionary = new XmlDictionary();  
            typeName = dictionary.Add("SomeCustomer");  
            typeNamespace = dictionary.Add("http://tempuri.com");  
            return true;  
        }  
        else  
        {  
            return knownTypeResolver.TryResolveType(dataContractType, declaredType, null, out typeName, out typeNamespace);  
        }  
    }  
  
    public override Type ResolveName(string typeName, string typeNamespace, DataContractResolver knownTypeResolver)  
    {  
        if (typeName == "SomeCustomer" && typeNamespace == "http://tempuri.com")  
        {  
            return typeof(Customer);  
        }  
        else  
        {  
            return knownTypeResolver.ResolveName(typeName, typeNamespace, null);  
        }  
    }  
}  
```  
  
 <span data-ttu-id="a6572-116">一旦定義了 <xref:System.Runtime.Serialization.DataContractResolver>，只要傳遞至 <xref:System.Runtime.Serialization.DataContractSerializer> 建構函式即可使用，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a6572-116">Once you have defined a <xref:System.Runtime.Serialization.DataContractResolver> you can use it by passing it to the <xref:System.Runtime.Serialization.DataContractSerializer> constructor as shown in the following example.</span></span>  
  
```csharp
XmlObjectSerializer serializer = new DataContractSerializer(typeof(Customer), null, Int32.MaxValue, false, false, null, new MyCustomerResolver());  
```  
  
 <span data-ttu-id="a6572-117">您可以在 <xref:System.Runtime.Serialization.DataContractResolver> 或 <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A?displayProperty=nameWithType> 方法的呼叫中指定 <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A?displayProperty=nameWithType>，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a6572-117">You can specify a <xref:System.Runtime.Serialization.DataContractResolver> in a call to the <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A?displayProperty=nameWithType> or <xref:System.Runtime.Serialization.DataContractSerializer.WriteObject%2A?displayProperty=nameWithType> methods, as shown in the following example.</span></span>  
  
```csharp
MemoryStream ms = new MemoryStream();  
DataContractSerializer serializer = new DataContractSerializer(typeof(Customer));  
XmlDictionaryWriter writer = XmlDictionaryWriter.CreateDictionaryWriter(XmlWriter.Create(ms));  
serializer.WriteObject(writer, new Customer(), new MyCustomerResolver());  
writer.Flush();  
ms.Position = 0;  
Console.WriteLine(((Customer)serializer.ReadObject(XmlDictionaryReader.CreateDictionaryReader(XmlReader.Create(ms)), false, new MyCustomerResolver()));  
```  
  
 <span data-ttu-id="a6572-118">您也可以在 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 上進行設定，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a6572-118">Or you can set it on the <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> as shown in the following example.</span></span>  
  
```csharp
ServiceHost host = new ServiceHost(typeof(MyService));  
  
ContractDescription cd = host.Description.Endpoints[0].Contract;  
OperationDescription myOperationDescription = cd.Operations.Find("Echo");  
  
DataContractSerializerOperationBehavior serializerBehavior = myOperationDescription.Behaviors.Find<DataContractSerializerOperationBehavior>();  
if (serializerBehavior == null)  
{  
    serializerBehavior = new DataContractSerializerOperationBehavior(myOperationDescription);  
    myOperationDescription.Behaviors.Add(serializerBehavior);  
}  
  
SerializerBehavior.DataContractResolver = new MyCustomerResolver();  
```  
  
 <span data-ttu-id="a6572-119">您可以透過實作可套用至服務的屬性，以宣告方式指定資料合約解析程式。</span><span class="sxs-lookup"><span data-stu-id="a6572-119">You can declaratively specify a data contract resolver by implementing an attribute that can be applied to a service.</span></span>  <span data-ttu-id="a6572-120">如需詳細資訊，請參閱[KnownAssemblyAttribute](../samples/knownassemblyattribute.md)範例。</span><span class="sxs-lookup"><span data-stu-id="a6572-120">For more information, see the [KnownAssemblyAttribute](../samples/knownassemblyattribute.md) sample.</span></span> <span data-ttu-id="a6572-121">這個範例會執行名為 "KnownAssembly" 的屬性，將自訂資料合約解析程式新增至服務的行為。</span><span class="sxs-lookup"><span data-stu-id="a6572-121">This sample implements an attribute called "KnownAssembly" that adds a custom data contract resolver to the service’s behavior.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a6572-122">請參閱</span><span class="sxs-lookup"><span data-stu-id="a6572-122">See also</span></span>

- [<span data-ttu-id="a6572-123">資料合約已知型別</span><span class="sxs-lookup"><span data-stu-id="a6572-123">Data Contract Known Types</span></span>](data-contract-known-types.md)
- [<span data-ttu-id="a6572-124">DataContractSerializer 範例</span><span class="sxs-lookup"><span data-stu-id="a6572-124">DataContractSerializer Sample</span></span>](../samples/datacontractserializer-sample.md)
- [<span data-ttu-id="a6572-125">KnownAssemblyAttribute</span><span class="sxs-lookup"><span data-stu-id="a6572-125">KnownAssemblyAttribute</span></span>](../samples/knownassemblyattribute.md)
