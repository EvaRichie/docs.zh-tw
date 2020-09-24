---
title: 概觀
description: 如需詳細說明和範例，請參閱 .NET Framework 中的 ADO.NET，並閱讀相關資源。
ms.date: 03/30/2017
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
ms.openlocfilehash: 459e4a548a4d1358b196dc41ec495921833728d4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153491"
---
# <a name="adonet-overview"></a><span data-ttu-id="5c513-103">ADO.NET 概觀</span><span class="sxs-lookup"><span data-stu-id="5c513-103">ADO.NET Overview</span></span>

<span data-ttu-id="5c513-104">ADO.NET 可讓您以一致的方式存取資料來源 (例如 SQL Server 與 XML)，以及透過 OLE DB 和 ODBC 所公開的資料來源。</span><span class="sxs-lookup"><span data-stu-id="5c513-104">ADO.NET provides consistent access to data sources such as SQL Server and XML, and to data sources exposed through OLE DB and ODBC.</span></span> <span data-ttu-id="5c513-105">資料共用的消費者應用程式可使用 ADO.NET 來連接至這些資料來源，並且擷取、處理及更新其中所含的資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-105">Data-sharing consumer applications can use ADO.NET to connect to these data sources and retrieve, handle, and update the data that they contain.</span></span>  
  
 <span data-ttu-id="5c513-106">ADO.NET 可將資料管理的資料存取分成不連續的元件，這些元件可分開使用，也可串聯使用。</span><span class="sxs-lookup"><span data-stu-id="5c513-106">ADO.NET separates data access from data manipulation into discrete components that can be used separately or in tandem.</span></span> <span data-ttu-id="5c513-107">ADO.NET 也包含 .NET Framework 資料提供者，以用於連接資料庫、執行命令和擷取結果。</span><span class="sxs-lookup"><span data-stu-id="5c513-107">ADO.NET includes .NET Framework data providers for connecting to a database, executing commands, and retrieving results.</span></span> <span data-ttu-id="5c513-108">這些結果會直接處理、放入 ADO.NET <xref:System.Data.DataSet> 物件中以便利用臨機操作 (Ad Hoc) 的方式公開給使用者、與多個來源的資料結合，或在各層之間進行傳遞。</span><span class="sxs-lookup"><span data-stu-id="5c513-108">Those results are either processed directly, placed in an ADO.NET <xref:System.Data.DataSet> object in order to be exposed to the user in an ad hoc manner, combined with data from multiple sources, or passed between tiers.</span></span> <span data-ttu-id="5c513-109">`DataSet` 物件也可以與 .NET Framework 資料提供者分開使用，以便管理應用程式本機的資料或來自 XML 的資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-109">The `DataSet` object can also be used independently of a .NET Framework data provider to manage data local to the application or sourced from XML.</span></span>  
  
 <span data-ttu-id="5c513-110">ADO.NET 類別 (Class) 位於 System.Data.dll 中，而且會與 System.Xml.dll 中的 XML 類別整合。</span><span class="sxs-lookup"><span data-stu-id="5c513-110">The ADO.NET classes are found in System.Data.dll, and are integrated with the XML classes found in System.Xml.dll.</span></span> <span data-ttu-id="5c513-111">如需連接至資料庫的範例程式碼，可從中抓取資料，然後在主控台視窗中顯示該資料，請參閱 [ADO.NET 程式碼範例](ado-net-code-examples.md)。</span><span class="sxs-lookup"><span data-stu-id="5c513-111">For sample code that connects to a database, retrieves data from it, and then displays that data in a console window, see [ADO.NET Code Examples](ado-net-code-examples.md).</span></span>  
  
 <span data-ttu-id="5c513-112">ADO.NET 可為撰寫 Managed 程式碼的開發人員提供類似於 ActiveX Data Objects (ADO) 提供給原生元件物件模型 (Component Object Model，COM) 開發人員的功能。</span><span class="sxs-lookup"><span data-stu-id="5c513-112">ADO.NET provides functionality to developers who write managed code similar to the functionality provided to native component object model (COM) developers by ActiveX Data Objects (ADO).</span></span> <span data-ttu-id="5c513-113">我們建議您使用 ADO.NET (而非 ADO) 來存取 .NET 應用程式中的資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-113">We recommend that you use ADO.NET, not ADO, for accessing data in your .NET applications.</span></span>  
  
 <span data-ttu-id="5c513-114">ADO.NET 會提供最直接的方法，讓您在 .NET Framework 中進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="5c513-114">ADO.NET provides the most direct method of data access within the .NET Framework.</span></span> <span data-ttu-id="5c513-115">若為較高層級的抽象概念，可讓應用程式針對概念模型（而不是基礎儲存體模型）運作，請參閱 [ADO.NET Entity Framework](./ef/index.md)。</span><span class="sxs-lookup"><span data-stu-id="5c513-115">For a higher-level abstraction that allows applications to work against a conceptual model instead of the underlying storage model, see the [ADO.NET Entity Framework](./ef/index.md).</span></span>  
  
 <span data-ttu-id="5c513-116">**隱私權聲明**： System.Data.dll、System.Data.Design.dll、System.Data.OracleClient.dll、System.Data.SqlXml.dll、System.Data.Linq.dll、System.Data.SqlServerCe.dll 和 System.Data.DataSetExtensions.dll 元件無法區分使用者的私用資料和非私用資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-116">**Privacy Statement**: The System.Data.dll, System.Data.Design.dll, System.Data.OracleClient.dll, System.Data.SqlXml.dll, System.Data.Linq.dll, System.Data.SqlServerCe.dll, and System.Data.DataSetExtensions.dll assemblies do not distinguish between a user's private data and non-private data.</span></span>  <span data-ttu-id="5c513-117">這些組件不會收集、儲存或傳輸任何使用者的私用資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-117">These assemblies do not collect, store, or transport any user's private data.</span></span> <span data-ttu-id="5c513-118">不過，協力廠商應用程式可能會使用這些組件來收集、儲存或傳輸使用者的私用資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-118">However, third-party applications might collect, store, or transport a user's private data using these assemblies.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="5c513-119">本節內容</span><span class="sxs-lookup"><span data-stu-id="5c513-119">In This Section</span></span>  

 [<span data-ttu-id="5c513-120">ADO.NET 架構</span><span class="sxs-lookup"><span data-stu-id="5c513-120">ADO.NET Architecture</span></span>](ado-net-architecture.md)  
 <span data-ttu-id="5c513-121">提供 ADO.NET 架構和元件的概觀。</span><span class="sxs-lookup"><span data-stu-id="5c513-121">Provides an overview of the architecture and components of ADO.NET.</span></span>  
  
 [<span data-ttu-id="5c513-122">ADO.NET 技術選項和方針</span><span class="sxs-lookup"><span data-stu-id="5c513-122">ADO.NET Technology Options and Guidelines</span></span>](ado-net-technology-options-and-guidelines.md)  
 <span data-ttu-id="5c513-123">說明實體資料平台隨附的產品和技術。</span><span class="sxs-lookup"><span data-stu-id="5c513-123">Describes the products and technologies included with the Entity Data Platform.</span></span>  
  
 [<span data-ttu-id="5c513-124">LINQ 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="5c513-124">LINQ and ADO.NET</span></span>](linq-and-ado-net.md)  
 <span data-ttu-id="5c513-125">說明如何在 ADO.NET 中實作 Language-Integrated Query (LINQ)，並且提供相關主題的連結。</span><span class="sxs-lookup"><span data-stu-id="5c513-125">Describes how Language-Integrated Query (LINQ) is implemented in ADO.NET and provides links to relevant topics.</span></span>  
  
 [<span data-ttu-id="5c513-126">.NET Framework 資料提供者</span><span class="sxs-lookup"><span data-stu-id="5c513-126">.NET Framework Data Providers</span></span>](data-providers.md)  
 <span data-ttu-id="5c513-127">提供 .NET Framework 資料提供者的設計概觀，以及 ADO.NET 所包含的 .NET Framework 資料提供者概觀。</span><span class="sxs-lookup"><span data-stu-id="5c513-127">Provides an overview of the design of the .NET Framework data provider and of the .NET Framework data providers that are included with ADO.NET.</span></span>  
  
 [<span data-ttu-id="5c513-128">ADO.NET 資料集</span><span class="sxs-lookup"><span data-stu-id="5c513-128">ADO.NET DataSets</span></span>](ado-net-datasets.md)  
 <span data-ttu-id="5c513-129">提供 `DataSet` 設計與元件的概觀。</span><span class="sxs-lookup"><span data-stu-id="5c513-129">Provides an overview of the `DataSet` design and components.</span></span>  
  
 [<span data-ttu-id="5c513-130">ADO.NET 中的並存執行</span><span class="sxs-lookup"><span data-stu-id="5c513-130">Side-by-Side Execution in ADO.NET</span></span>](side-by-side-execution.md)  
 <span data-ttu-id="5c513-131">討論各個 ADO.NET 版本之間的差異，以及它們在並存執行與應用程式相容性上的影響。</span><span class="sxs-lookup"><span data-stu-id="5c513-131">Discusses differences in ADO.NET versions and their effect on side-by-side execution and application compatibility.</span></span>  
  
 <span data-ttu-id="5c513-132">[ADO.NET Code Examples](ado-net-code-examples.md) (ADO.NET 程式碼範例)</span><span class="sxs-lookup"><span data-stu-id="5c513-132">[ADO.NET Code Examples](ado-net-code-examples.md)</span></span>  
 <span data-ttu-id="5c513-133">提供使用 ADO.NET 資料提供者來擷取資料的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="5c513-133">Provides code samples that retrieve data using the ADO.NET data providers.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="5c513-134">相關章節</span><span class="sxs-lookup"><span data-stu-id="5c513-134">Related Sections</span></span>  

 [<span data-ttu-id="5c513-135">ADO.NET 的新功能</span><span class="sxs-lookup"><span data-stu-id="5c513-135">What's New in ADO.NET</span></span>](whats-new.md)  
 <span data-ttu-id="5c513-136">簡介 ADO.NET 的新功能。</span><span class="sxs-lookup"><span data-stu-id="5c513-136">Introduces features that are new in ADO.NET.</span></span>  
  
 [<span data-ttu-id="5c513-137">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="5c513-137">Securing ADO.NET Applications</span></span>](securing-ado-net-applications.md)  
 <span data-ttu-id="5c513-138">說明使用 ADO.NET 的安全程式碼撰寫實施方針。</span><span class="sxs-lookup"><span data-stu-id="5c513-138">Describes secure coding practices when using ADO.NET.</span></span>  
  
 [<span data-ttu-id="5c513-139">ADO.NET 中的資料類型對應</span><span class="sxs-lookup"><span data-stu-id="5c513-139">Data Type Mappings in ADO.NET</span></span>](data-type-mappings-in-ado-net.md)  
 <span data-ttu-id="5c513-140">說明 .NET Framework 資料型別與 .NET Framework 資料提供者之間的資料型別對應。</span><span class="sxs-lookup"><span data-stu-id="5c513-140">Describes data type mappings between .NET Framework data types and the .NET Framework data providers.</span></span>  
  
 [<span data-ttu-id="5c513-141">在 ADO.NET 中傳送和修改資料</span><span class="sxs-lookup"><span data-stu-id="5c513-141">Retrieving and Modifying Data in ADO.NET</span></span>](retrieving-and-modifying-data.md)  
 <span data-ttu-id="5c513-142">說明如何連接至資料來源、擷取資料和修改資料。</span><span class="sxs-lookup"><span data-stu-id="5c513-142">Describes how to connect to a data source, retrieve data, and modify data.</span></span> <span data-ttu-id="5c513-143">這包括 `DataReaders` 和 `DataAdapters`。</span><span class="sxs-lookup"><span data-stu-id="5c513-143">This includes `DataReaders` and `DataAdapters`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5c513-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c513-144">See also</span></span>

- [<span data-ttu-id="5c513-145">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="5c513-145">ADO.NET</span></span>](index.md)
- [<span data-ttu-id="5c513-146">存取 Visual Studio 中的資料</span><span class="sxs-lookup"><span data-stu-id="5c513-146">Accessing data in Visual Studio</span></span>](/visualstudio/data-tools/accessing-data-in-visual-studio)
