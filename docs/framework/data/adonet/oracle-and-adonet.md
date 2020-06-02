---
title: Oracle 和 ADO.NET
description: 瞭解 Oracle .NET Framework Data Provider 的功能和行為，其可讓您使用 Oracle 呼叫介面來存取 Oracle 資料庫。
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
ms.openlocfilehash: 8757352a7444fad802ea88ba58e0fe643c86cbb8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286685"
---
# <a name="oracle-and-adonet"></a><span data-ttu-id="9a9a1-103">Oracle 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9a9a1-103">Oracle and ADO.NET</span></span>
> [!NOTE]
> <span data-ttu-id="9a9a1-104"><xref:System.Data.OracleClient> 中的型別已被取代。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-104">The types in <xref:System.Data.OracleClient> are deprecated.</span></span> <span data-ttu-id="9a9a1-105">目前版本的 .NET Framework 仍然支援這些型別，不過未來的版本就會將其移除。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-105">The types remain supported in the current version of.NET Framework but will be removed in a future release.</span></span> <span data-ttu-id="9a9a1-106">Microsoft 建議您使用協力廠商的 Oracle 提供者。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-106">Microsoft recommends that you use a third-party Oracle provider.</span></span>  
  
 <span data-ttu-id="9a9a1-107">本節說明 Oracle 的 .NET Framework Data Provider 特有的功能和行為。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-107">This section describes features and behaviors that are specific to the .NET Framework Data Provider for Oracle.</span></span>  
  
 <span data-ttu-id="9a9a1-108">Oracle 的 .NET Framework Data Provider 可讓您使用 oracle 用戶端軟體所提供的 Oracle 呼叫介面（OCI）來存取 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-108">The .NET Framework Data Provider for Oracle provides access to an Oracle database using the Oracle Call Interface (OCI) as provided by Oracle Client software.</span></span> <span data-ttu-id="9a9a1-109">資料提供者的功能設計類似于 SQL Server、OLE DB 和 ODBC 的 .NET Framework 資料提供者。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-109">The functionality of the data provider is designed to be similar to that of the .NET Framework data providers for SQL Server, OLE DB, and ODBC.</span></span>  
  
 <span data-ttu-id="9a9a1-110">若要使用 Oracle 的 .NET Framework Data Provider，應用程式必須參考 <xref:System.Data.OracleClient> 命名空間，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a9a1-110">To use the .NET Framework Data Provider for Oracle, an application must reference the <xref:System.Data.OracleClient> namespace as follows:</span></span>  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 <span data-ttu-id="9a9a1-111">當您編譯程式碼時，還必須將參考併入 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-111">You also must include a reference to the DLL when you compile your code.</span></span> <span data-ttu-id="9a9a1-112">例如，如果編譯 C# 程式，則命令列應包括：</span><span class="sxs-lookup"><span data-stu-id="9a9a1-112">For example, if you are compiling a C# program, your command line should include:</span></span>  
  
```console
csc /r:System.Data.OracleClient.dll  
```  
  
## <a name="in-this-section"></a><span data-ttu-id="9a9a1-113">本節內容</span><span class="sxs-lookup"><span data-stu-id="9a9a1-113">In This Section</span></span>  
 [<span data-ttu-id="9a9a1-114">系統需求</span><span class="sxs-lookup"><span data-stu-id="9a9a1-114">System Requirements</span></span>](system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 <span data-ttu-id="9a9a1-115">描述使用 Oracle 的 .NET Framework Data Provider 的需求，並說明使用時要注意的一些問題。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-115">Describes requirements for using the .NET Framework Data Provider for Oracle, and describes a number of issues to be aware when using it.</span></span>  
  
 [<span data-ttu-id="9a9a1-116">Oracle BFILE</span><span class="sxs-lookup"><span data-stu-id="9a9a1-116">Oracle BFILEs</span></span>](oracle-bfiles.md)  
 <span data-ttu-id="9a9a1-117">說明用來與 Oracle BFILE 資料型別搭配使用的 <xref:System.Data.OracleClient.OracleBFile> 類別。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-117">Describes the <xref:System.Data.OracleClient.OracleBFile> class, which is used to work with the Oracle BFILE data type.</span></span>  
  
 [<span data-ttu-id="9a9a1-118">Oracle LOB</span><span class="sxs-lookup"><span data-stu-id="9a9a1-118">Oracle LOBs</span></span>](oracle-lobs.md)  
 <span data-ttu-id="9a9a1-119">說明用來與 Oracle LOB 資料型別搭配使用的 <xref:System.Data.OracleClient.OracleLob> 類別。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-119">Describes the <xref:System.Data.OracleClient.OracleLob> class, which is used to work with Oracle LOB data types.</span></span>  
  
 [<span data-ttu-id="9a9a1-120">Oracle REF CURSOR</span><span class="sxs-lookup"><span data-stu-id="9a9a1-120">Oracle REF CURSORs</span></span>](oracle-ref-cursors.md)  
 <span data-ttu-id="9a9a1-121">說明 Oracle REF CURSOR 資料型別的支援。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-121">Describes support for the Oracle REF CURSOR data type.</span></span>  
  
 [<span data-ttu-id="9a9a1-122">OracleType</span><span class="sxs-lookup"><span data-stu-id="9a9a1-122">OracleTypes</span></span>](oracletypes.md)  
 <span data-ttu-id="9a9a1-123">說明可用來與 Oracle 資料型別搭配使用的結構，包括 <xref:System.Data.OracleClient.OracleNumber> 及 <xref:System.Data.OracleClient.OracleString>。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-123">Describes structures you can use to work with Oracle data types, including <xref:System.Data.OracleClient.OracleNumber> and <xref:System.Data.OracleClient.OracleString>.</span></span>  
  
 [<span data-ttu-id="9a9a1-124">Oracle 序列</span><span class="sxs-lookup"><span data-stu-id="9a9a1-124">Oracle Sequences</span></span>](oracle-sequences.md)  
 <span data-ttu-id="9a9a1-125">說明針對擷取伺服器產生的索引鍵 Oracle Sequence 值所提供的支援。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-125">Describes support for retrieving the server-generated key Oracle Sequence values.</span></span>  
  
 [<span data-ttu-id="9a9a1-126">Oracle 資料類型對應</span><span class="sxs-lookup"><span data-stu-id="9a9a1-126">Oracle Data Type Mappings</span></span>](oracle-data-type-mappings.md)  
 <span data-ttu-id="9a9a1-127">列出 Oracle 資料型別及其與 <xref:System.Data.OracleClient.OracleDataReader> 的對應。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-127">Lists Oracle data types and their mappings to the <xref:System.Data.OracleClient.OracleDataReader>.</span></span>  
  
 [<span data-ttu-id="9a9a1-128">Oracle 分散式異動</span><span class="sxs-lookup"><span data-stu-id="9a9a1-128">Oracle Distributed Transactions</span></span>](oracle-distributed-transactions.md)  
 <span data-ttu-id="9a9a1-129">說明如果 <xref:System.Data.OracleClient.OracleConnection> 物件判定異動處於作用中，它會如何自動登記在現有的分散式異動中。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-129">Describes how the <xref:System.Data.OracleClient.OracleConnection> object automatically enlists in an existing distributed transaction if it determines that a transaction is active.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="9a9a1-130">相關章節</span><span class="sxs-lookup"><span data-stu-id="9a9a1-130">Related Sections</span></span>  
 [<span data-ttu-id="9a9a1-131">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="9a9a1-131">Securing ADO.NET Applications</span></span>](securing-ado-net-applications.md)  
 <span data-ttu-id="9a9a1-132">說明使用 ADO.NET 的安全程式碼撰寫實施方針。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-132">Describes secure coding practices when using ADO.NET.</span></span>  
  
 [<span data-ttu-id="9a9a1-133">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="9a9a1-133">DataSets, DataTables, and DataViews</span></span>](./dataset-datatable-dataview/index.md)  
 <span data-ttu-id="9a9a1-134">說明如何建立及使用 `DataSets`、具型別 `DataSets`、`DataTables` 和 `DataViews`。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-134">Describes how to create and use `DataSets`, typed `DataSets`, `DataTables`, and `DataViews`.</span></span>  
  
 [<span data-ttu-id="9a9a1-135">在 ADO.NET 中擷取和修改資料</span><span class="sxs-lookup"><span data-stu-id="9a9a1-135">Retrieving and Modifying Data in ADO.NET</span></span>](retrieving-and-modifying-data.md)  
 <span data-ttu-id="9a9a1-136">說明如何使用 ADO.NET 中的資料。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-136">Describes how to work with data in ADO.NET.</span></span>  
  
 <span data-ttu-id="9a9a1-137">[SQL Server and ADO.NET](./sql/index.md) (SQL Server 和 ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="9a9a1-137">[SQL Server and ADO.NET](./sql/index.md)</span></span>  
 <span data-ttu-id="9a9a1-138">說明如何使用 SQL Server 特有的特性和功能。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-138">Describes how to work with features and functionality that are specific to SQL Server.</span></span>  
  
 [<span data-ttu-id="9a9a1-139">DbProviderFactory</span><span class="sxs-lookup"><span data-stu-id="9a9a1-139">DbProviderFactories</span></span>](dbproviderfactories.md)  
 <span data-ttu-id="9a9a1-140">說明可讓您在 ADO.NET 中撰寫提供者獨立程式碼的泛用類別。</span><span class="sxs-lookup"><span data-stu-id="9a9a1-140">Describes generic classes that allow you to write provider-independent code in ADO.NET.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9a9a1-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9a9a1-141">See also</span></span>

- [<span data-ttu-id="9a9a1-142">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9a9a1-142">ADO.NET</span></span>](index.md)
- <span data-ttu-id="9a9a1-143">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="9a9a1-143">[ADO.NET Overview](ado-net-overview.md)</span></span>
