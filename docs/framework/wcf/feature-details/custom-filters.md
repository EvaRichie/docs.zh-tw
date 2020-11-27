---
title: 自訂篩選器
ms.date: 03/30/2017
ms.assetid: 97cf247d-be0a-4057-bba9-3be5c45029d5
ms.openlocfilehash: b5ec07c2e2a77c7de8b240d21b1eb54bf858b43b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96258422"
---
# <a name="custom-filters"></a><span data-ttu-id="8f336-102">自訂篩選器</span><span class="sxs-lookup"><span data-stu-id="8f336-102">Custom Filters</span></span>

<span data-ttu-id="8f336-103">自訂篩選可讓您定義無法使用系統所提供訊息篩選完成的比對邏輯。</span><span class="sxs-lookup"><span data-stu-id="8f336-103">Custom filters allow you to define matching logic that cannot be accomplished using the system-provided message filters.</span></span> <span data-ttu-id="8f336-104">例如，您可能會建立自訂篩選，此篩選會雜湊特殊訊息項目，然後檢查值，判斷篩選應傳回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="8f336-104">For example, you might create a custom filter that hashes a particular message element and then examines the value to determine whether the filter should return true or false.</span></span>  
  
## <a name="implementation"></a><span data-ttu-id="8f336-105">實作</span><span class="sxs-lookup"><span data-stu-id="8f336-105">Implementation</span></span>  

 <span data-ttu-id="8f336-106">自訂篩選是 <xref:System.ServiceModel.Dispatcher.MessageFilter> 抽象基底類別的實作。</span><span class="sxs-lookup"><span data-stu-id="8f336-106">A custom filter is an implementation of the <xref:System.ServiceModel.Dispatcher.MessageFilter> abstract base class.</span></span> <span data-ttu-id="8f336-107">實作您的自訂篩選時，建構函式可以選擇性地接受單一字串參數。</span><span class="sxs-lookup"><span data-stu-id="8f336-107">When implementing your custom filter, the constructor can optionally accept a single string parameter.</span></span> <span data-ttu-id="8f336-108">此參數會包含傳遞至 MessageFilter 建構函式的組態資訊，以便提供篩選在執行階段執行比對時所需的任何值或組態。</span><span class="sxs-lookup"><span data-stu-id="8f336-108">This parameter contains the configuration information that is passed to the MessageFilter constructor in order to provide any values or configuration that the filter needs at runtime in order to perform matches.</span></span> <span data-ttu-id="8f336-109">例如，此參數可能用來提供篩選在要評估的訊息內尋找的值。</span><span class="sxs-lookup"><span data-stu-id="8f336-109">For example, this might be used to provide a value that the filter looks for within the message being evaluated.</span></span> <span data-ttu-id="8f336-110">下列範例示範接受字串參數之自訂訊息篩選的基本實作：</span><span class="sxs-lookup"><span data-stu-id="8f336-110">The following example demonstrates a basic implementation of a custom message filter that accepts a string parameter:</span></span>  
  
```csharp  
public class MyMessageFilter: MessageFilter  
{  
    string filterData;  
    public MyMessageFilter(string filterData)  
    {  
        if(string.IsNullOrEmpty(filterData)  
            throw new ArgumentNullException("filterData");  
        this.filterData=filterData;  
    }  
    public override bool Match(System.ServiceModel.Channels.Message message)  
    {  
        ...  
        return retValue;  
    }  
    public override bool Match(System.ServiceModel.Channels.MessageBuffer buffer)  
    {  
        ...  
        return retValue;  
    }  
}  
```  
  
> [!NOTE]
> <span data-ttu-id="8f336-111">在實際的執行中，Match 方法 (s) 包含可檢查訊息的邏輯，以判斷此訊息篩選準則是否應傳回 **true** 或 **false**。</span><span class="sxs-lookup"><span data-stu-id="8f336-111">In an actual implementation, the Match method(s) contains logic that will examine the message to determine if this message filter should return **true** or **false**.</span></span>  
  
### <a name="performance"></a><span data-ttu-id="8f336-112">效能</span><span class="sxs-lookup"><span data-stu-id="8f336-112">Performance</span></span>  

 <span data-ttu-id="8f336-113">實作自訂篩選時，最好將篩選完成訊息評估所需的時間長度上限納入考量。</span><span class="sxs-lookup"><span data-stu-id="8f336-113">When implementing a custom filter, it is important to take into consideration the maximum length of time required for the filter to complete the evaluation of a message.</span></span> <span data-ttu-id="8f336-114">在找到相符項目之前，可能會根據多個篩選評估訊息，因此，確保用戶端要求在可以評估所有篩選之前沒有逾時相當重要。</span><span class="sxs-lookup"><span data-stu-id="8f336-114">Since a message may be evaluated against multiple filters before a match is found, it is important to ensure that the client request does not time out before all filters can be evaluated.</span></span> <span data-ttu-id="8f336-115">為此，自訂篩選應該只包含評估訊息內容或屬性所需的程式碼，才能判斷該訊息是否符合篩選準則。</span><span class="sxs-lookup"><span data-stu-id="8f336-115">Therefore a custom filter should contain only the code necessary to evaluate the contents or attributes of a message in order to determine if it matches the filter criteria.</span></span>  
  
 <span data-ttu-id="8f336-116">一般而言，實作自訂篩選時，您應該避免下列狀況：</span><span class="sxs-lookup"><span data-stu-id="8f336-116">In general, you should avoid the following when implementing a custom filter:</span></span>  
  
- <span data-ttu-id="8f336-117">IO，例如，將資料儲存到磁碟或資料庫。</span><span class="sxs-lookup"><span data-stu-id="8f336-117">IO, such as saving data to disk or to a database.</span></span>  
  
- <span data-ttu-id="8f336-118">不必要的處理，例如，針對某個文件中的多筆記錄執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="8f336-118">Unnecessary processing, such as looping over multiple records in a document.</span></span>  
  
- <span data-ttu-id="8f336-119">封鎖作業，例如，與取得共用資源之鎖定或針對資料庫執行查詢有關的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8f336-119">Blocking operations, such as calls that involve obtaining a lock on shared resources or performing lookups against a database.</span></span>  
  
 <span data-ttu-id="8f336-120">在實際執行環境中使用自訂篩選之前，您應該執行效能測試，以判斷篩選評估訊息所需的平均時間長度。</span><span class="sxs-lookup"><span data-stu-id="8f336-120">Before using a custom filter in a production environment, you should run performance tests to determine the average length of time that the filter takes to evaluate a message.</span></span> <span data-ttu-id="8f336-121">結合其他篩選在篩選資料表中使用之平均處理時間時，這可讓您正確判斷用戶端應用程式應該指定的最大逾時值。</span><span class="sxs-lookup"><span data-stu-id="8f336-121">When combined with the average processing time of the other filters used in the filter table, this will allow you to accurately determine the maximum timeout value that should be specified by the client application.</span></span>  
  
## <a name="usage"></a><span data-ttu-id="8f336-122">使用方式</span><span class="sxs-lookup"><span data-stu-id="8f336-122">Usage</span></span>  

 <span data-ttu-id="8f336-123">若要使用您的自訂篩選準則搭配路由服務，您必須藉由指定「自訂」類型的新篩選項目、訊息篩選準則的完整類型名稱，以及元件的名稱，將它加入至篩選資料表。</span><span class="sxs-lookup"><span data-stu-id="8f336-123">In order to use your custom filter with the Routing Service, you must add it to the filter table by specifying a new filter entry of type "Custom," the fully qualified type name of the message filter, and the name of your assembly.</span></span>  <span data-ttu-id="8f336-124">就像使用其他 MessageFilters 一般，您可以指定 filterData 字串，這個字串將傳遞至自訂篩選的建構函式。</span><span class="sxs-lookup"><span data-stu-id="8f336-124">As with other MessageFilters, you can specify the string filterData that will be passed to your custom filter’s constructor.</span></span>  
  
 <span data-ttu-id="8f336-125">下列範例示範使用自訂篩選搭配路由服務：</span><span class="sxs-lookup"><span data-stu-id="8f336-125">The following examples demonstrate using a custom filter with the Routing Service:</span></span>  
  
```xml  
<!--ROUTING SECTION -->  
<routing>  
  <filters>  
    <filter name="CustomFilter1" filterType="Custom"
            customType="CustomAssembly.MyMessageFilter,
            CustomAssembly" filterData="custom data" />  
  </filters>  
  <filterTables>  
    <table name="routingTable1">  
      <filters>  
        <add filterName="CustomFilter1" endpointName="CalculatorService" />  
      </filters>  
    </table>  
  </filterTables>  
</routing>  
```  
  
```csharp  
RoutingConfiguration rc = new RoutingConfiguration();  
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();  
endpointList.Add(client);  
rc.FilterTable.Add(new MyMessageFilter("CustomData"), endpointList);  
```
