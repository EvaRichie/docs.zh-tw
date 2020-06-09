---
title: HOW TO：使用 Svcutil.exe 來匯出已編譯服務程式碼的中繼資料
ms.date: 03/30/2017
ms.assetid: 95d0aed3-16a2-4398-89bb-39418eeb7355
ms.openlocfilehash: 9acefdec63a6f518ead6cdbcb19ebc8c75609dd6
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595358"
---
# <a name="how-to-use-svcutilexe-to-export-metadata-from-compiled-service-code"></a><span data-ttu-id="c21ee-102">HOW TO：使用 Svcutil.exe 來匯出已編譯服務程式碼的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-102">How to: Use Svcutil.exe to Export Metadata from Compiled Service Code</span></span>
<span data-ttu-id="c21ee-103">Svcutil.exe 可匯出服務中繼資料、合約以及編譯組件資料類型，如下：</span><span class="sxs-lookup"><span data-stu-id="c21ee-103">Svcutil.exe can export metadata for services, contracts, and data types in compiled assemblies, as follows:</span></span>  
  
- <span data-ttu-id="c21ee-104">若要使用 Svcutil.exe 針對組件集合匯出所有編譯服務合約的中繼資料，請指定組件為輸入參數。</span><span class="sxs-lookup"><span data-stu-id="c21ee-104">To export metadata for all compiled service contracts for a set of assemblies using Svcutil.exe, specify the assemblies as input parameters.</span></span> <span data-ttu-id="c21ee-105">此為預設行為。</span><span class="sxs-lookup"><span data-stu-id="c21ee-105">This is the default behavior.</span></span>  
  
- <span data-ttu-id="c21ee-106">若要使用 Svcutil.exe 針對編譯服務匯出中繼資料，請指定服務組件或將組件指定為輸入參數。</span><span class="sxs-lookup"><span data-stu-id="c21ee-106">To export metadata for a compiled service using Svcutil.exe, specify the service assembly or assemblies as input parameters.</span></span> <span data-ttu-id="c21ee-107">您必須使用 `/serviceName` 選項指示您想要匯出之服務的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="c21ee-107">You must use the `/serviceName` option to indicate the configuration name of the service you want to export.</span></span> <span data-ttu-id="c21ee-108">Svcutil.exe 自動載入特定可執行組件的組態檔。</span><span class="sxs-lookup"><span data-stu-id="c21ee-108">Svcutil.exe automatically loads the configuration file for the specified executable assembly.</span></span>  
  
- <span data-ttu-id="c21ee-109">若要匯出組件集合內所有資料合約類型，請使用 `/dataContractOnly` 選項。</span><span class="sxs-lookup"><span data-stu-id="c21ee-109">To export all data contract types within a set of assemblies, use the `/dataContractOnly` option.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c21ee-110">使用 `/reference` 選項為任何相依組件指定檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c21ee-110">Use the `/reference` option to specify the file paths to any dependent assemblies.</span></span>  
  
### <a name="to-export-metadata-for-compiled-service-contracts"></a><span data-ttu-id="c21ee-111">若要匯出編譯服務合約的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-111">To export metadata for compiled service contracts</span></span>  
  
1. <span data-ttu-id="c21ee-112">將您的服務合約實作編譯成一個或多個類別程式庫。1</span><span class="sxs-lookup"><span data-stu-id="c21ee-112">Compile your service contract implementations into one or more class libraries.1</span></span>  
  
2. <span data-ttu-id="c21ee-113">執行 Svcutil.exe 處理編譯組件。</span><span class="sxs-lookup"><span data-stu-id="c21ee-113">Run Svcutil.exe on the compiled assemblies.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c21ee-114">您可能需要使用 `/reference` 參數來指定任何相依組件的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c21ee-114">You might need to use the `/reference` switch to specify the file path to any dependent assemblies.</span></span>  
  
    ```console
    svcutil.exe Contracts.dll  
    ```  
  
### <a name="to-export-metadata-for-a-compiled-service"></a><span data-ttu-id="c21ee-115">若要匯出編譯服務的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-115">To export metadata for a compiled service</span></span>  
  
1. <span data-ttu-id="c21ee-116">將您的服務實作編譯為可執行組件</span><span class="sxs-lookup"><span data-stu-id="c21ee-116">Compile your service implementation into an executable assembly.</span></span>  
  
2. <span data-ttu-id="c21ee-117">為您的服務可執行程式建立組態檔案並新增服務組態。</span><span class="sxs-lookup"><span data-stu-id="c21ee-117">Create a configuration file for your service executable and add a service configuration.</span></span>  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service name="MyService" >  
            <endpoint address="finder" contract="IPeopleFinder" binding="wsHttpBinding" />  
          </service>  
        </services>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
3. <span data-ttu-id="c21ee-118">使用 `/serviceName` 參數指定服務組態名稱，以 Svcutil.exe 處理編譯服務可執行檔。</span><span class="sxs-lookup"><span data-stu-id="c21ee-118">Run Svcutil.exe on the compiled service executable using the `/serviceName` switch to specify the configuration name of the service.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c21ee-119">您可能需要使用 `/reference` 參數來指定任何相依組件的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c21ee-119">You might need to use the `/reference` switch to specify the file path to any dependent assemblies.</span></span>  
  
    ```console  
    svcutil.exe /serviceName:MyService Service.exe /reference:path/Contracts.dll  
    ```  
  
### <a name="to-export-metadata-for-compiled-data-contracts"></a><span data-ttu-id="c21ee-120">若要匯出編譯資料合約的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-120">To export metadata for compiled data contracts</span></span>  
  
1. <span data-ttu-id="c21ee-121">將您的資料合約實作編譯成一個或多個類別程式庫。</span><span class="sxs-lookup"><span data-stu-id="c21ee-121">Compile your data contract implementations into one or more class libraries.</span></span>  
  
2. <span data-ttu-id="c21ee-122">執行 Svcutil.exe 處理編譯組件，將 `/dataContract` 參數指定只產生資料合約的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c21ee-122">Run Svcutil.exe on the compiled assemblies using the `/dataContract` switch to specify that only metadata for data contracts should be generated.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="c21ee-123">您可能需要使用 `/reference` 參數來指定任何相依組件的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="c21ee-123">You might need to use the `/reference` switch to specify the file path to any dependent assemblies.</span></span>  
  
    ```console  
    svcutil.exe /dataContractOnly Contracts.dll  
    ```  
  
## <a name="example"></a><span data-ttu-id="c21ee-124">範例</span><span class="sxs-lookup"><span data-stu-id="c21ee-124">Example</span></span>  
 <span data-ttu-id="c21ee-125">下列範例示範如何產生簡單服務實作與組態的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="c21ee-125">The following example demonstrates how to generate metadata for a simple service implementation and configuration.</span></span>  
  
 <span data-ttu-id="c21ee-126">若要匯出服務合約的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-126">To export metadata for the service contract.</span></span>  
  
```console  
svcutil.exe Contracts.dll  
```  
  
 <span data-ttu-id="c21ee-127">若要匯出資料合約的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-127">To export metadata for the data contracts.</span></span>  
  
```console  
svcutil.exe /dataContractOnly Contracts.dll  
```  
  
 <span data-ttu-id="c21ee-128">若要匯出服務實作的中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-128">To export metadata for the service implementation.</span></span>  
  
```console  
svcutil.exe /serviceName:MyService Service.exe /reference:<path>/Contracts.dll  
```  
  
 <span data-ttu-id="c21ee-129">`<path>` 為 Contracts.dll 的路徑。</span><span class="sxs-lookup"><span data-stu-id="c21ee-129">The `<path>` is the path to Contracts.dll.</span></span>  
  
```csharp
// The following service contract and data contracts are compiled into
// Contracts.dll.  
[ServiceContract(ConfigurationName="IPeopleFinder")]  
public interface IPersonFinder  
{  
    [OperationContract]  
    Address GetAddress(Person s);  
}  
  
[DataContract]  
public class Person  
{  
    [DataMember]  
    public string firstName;  
    [DataMember]  
    public string lastName;  
    [DataMember]  
    public int age;  
}  
  
[DataContract]  
public class Address  
{  
    [DataMember]  
    public string city;  
    [DataMember]  
    public string state;  
    [DataMember]  
    public string street;  
    [DataMember]  
    public int zipCode;  
    [DataMember]  
    public Person person;  
}  
```

```csharp
// The following service implementation is compiled into Service.exe.
// This service uses the contracts specified in Contracts.dll.  
[ServiceBehavior(ConfigurationName = "MyService")]  
public class MyService : IPersonFinder  
{  
    public Address GetAddress(Person person)  
    {  
        Address address = new Address();  
        address.person = person;  
        return address;  
    }  
}  
```

```xml  
<!-- The following is the configuration file for Service.exe. -->  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="MyService">  
         <endpoint  address="finder"  
                    binding="basicHttpBinding"  
                    contract="IPeopleFinder"/>  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a><span data-ttu-id="c21ee-130">請參閱</span><span class="sxs-lookup"><span data-stu-id="c21ee-130">See also</span></span>

- [<span data-ttu-id="c21ee-131">ServiceModel 中繼資料公用程式工具 (Svcutil.exe)</span><span class="sxs-lookup"><span data-stu-id="c21ee-131">ServiceModel Metadata Utility Tool (Svcutil.exe)</span></span>](../servicemodel-metadata-utility-tool-svcutil-exe.md)
- [<span data-ttu-id="c21ee-132">匯出和匯入中繼資料</span><span class="sxs-lookup"><span data-stu-id="c21ee-132">Exporting and Importing Metadata</span></span>](exporting-and-importing-metadata.md)
