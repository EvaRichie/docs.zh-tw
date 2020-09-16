---
title: 資料類型對應
ms.date: 03/30/2017
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
ms.openlocfilehash: 065a9dcb5e03c784c5dec9ffbe6a3153aead9e3c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554706"
---
# <a name="data-type-mappings-in-adonet"></a><span data-ttu-id="f38f9-102">ADO.NET 中的資料類型對應</span><span class="sxs-lookup"><span data-stu-id="f38f9-102">Data Type Mappings in ADO.NET</span></span>
<span data-ttu-id="f38f9-103">.NET Framework 是以一般型別系統為基礎，其中定義了型別在執行階段的宣告、使用和管理方式。</span><span class="sxs-lookup"><span data-stu-id="f38f9-103">The .NET Framework is based on the common type system, which defines how types are declared, used, and managed in the runtime.</span></span> <span data-ttu-id="f38f9-104">它同時包含了都衍生自 <xref:System.Object> 基底類型的實值型別 (Value Type) 和參考型別 (Reference Type)。</span><span class="sxs-lookup"><span data-stu-id="f38f9-104">It consists of both value types and reference types, which all derive from the <xref:System.Object> base type.</span></span> <span data-ttu-id="f38f9-105">使用資料來源時，如果沒有明確指定資料型別，就會從資料提供者 (Data Provider) 推斷資料型別。</span><span class="sxs-lookup"><span data-stu-id="f38f9-105">When working with a data source, the data type is inferred from the data provider if it is not explicitly specified.</span></span> <span data-ttu-id="f38f9-106">例如，<xref:System.Data.DataSet> 物件與任何特定資料來源無關。</span><span class="sxs-lookup"><span data-stu-id="f38f9-106">For example, a <xref:System.Data.DataSet> object is independent of any specific data source.</span></span> <span data-ttu-id="f38f9-107">`DataSet` 內的資料是由資料來源擷取而來，且變更會藉由 `DataAdapter` 存回資料來源；</span><span class="sxs-lookup"><span data-stu-id="f38f9-107">Data in a `DataSet` is retrieved from a data source, and changes are persisted back to the data source by using a `DataAdapter`.</span></span> <span data-ttu-id="f38f9-108">這表示當使用 `DataAdapter` 資料來源中的值填滿時 <xref:System.Data.DataTable> `DataSet` ，中的資料行產生的資料類型 `DataTable` 會是 .NET Framework 類型，而不是用來連接到資料來源之 .NET Framework 資料提供者的特定類型。</span><span class="sxs-lookup"><span data-stu-id="f38f9-108">This means that when a `DataAdapter` fills a <xref:System.Data.DataTable> in a `DataSet` with values from a data source, the resulting data types of the columns in the `DataTable` are .NET Framework types, instead of types specific to the .NET Framework data provider that is used to connect to the data source.</span></span>  
  
 <span data-ttu-id="f38f9-109">同樣地，當 `DataReader` 從資料來源傳回值時，產生的值會儲存在具有 .NET Framework 類型的本機變數中。</span><span class="sxs-lookup"><span data-stu-id="f38f9-109">Likewise, when a `DataReader` returns a value from a data source, the resulting value is stored in a local variable that has a .NET Framework type.</span></span> <span data-ttu-id="f38f9-110">對於的 `Fill` 作業 `DataAdapter` 和的 `Get` 方法 `DataReader` ，會從 .NET Framework 資料提供者傳回的值來推斷 .NET Framework 型別。</span><span class="sxs-lookup"><span data-stu-id="f38f9-110">For both the `Fill` operations of the `DataAdapter` and the `Get` methods of the `DataReader`, the .NET Framework type is inferred from the value returned from the .NET Framework data provider.</span></span>  
  
 <span data-ttu-id="f38f9-111">如果您知道傳回值的特定型別，就可以使用 `DataReader` 具型別的存取子方法，而不用仰賴推斷的資料型別。</span><span class="sxs-lookup"><span data-stu-id="f38f9-111">Instead of relying on the inferred data type, you can use the typed accessor methods of the `DataReader` when you know the specific type of the value being returned.</span></span> <span data-ttu-id="f38f9-112">具型別存取子方法會以特定的 .NET Framework 型別傳回值，以提供更好的效能，這樣就不需要額外的型別轉換。</span><span class="sxs-lookup"><span data-stu-id="f38f9-112">Typed accessor methods give you better performance by returning a value as a specific .NET Framework type, which eliminates the need for additional type conversion.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f38f9-113">.NET Framework 資料提供者資料類型的 Null 值是以表示 `DBNull.Value` 。</span><span class="sxs-lookup"><span data-stu-id="f38f9-113">Null values for .NET Framework data provider data types are represented by `DBNull.Value`.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="f38f9-114">本節內容</span><span class="sxs-lookup"><span data-stu-id="f38f9-114">In This Section</span></span>  
 [<span data-ttu-id="f38f9-115">SQL Server 資料類型對應</span><span class="sxs-lookup"><span data-stu-id="f38f9-115">SQL Server Data Type Mappings</span></span>](sql-server-data-type-mappings.md)  
 <span data-ttu-id="f38f9-116">列出 <xref:System.Data.SqlClient> 的推斷資料型別對應和資料存取子方法。</span><span class="sxs-lookup"><span data-stu-id="f38f9-116">Lists inferred data type mappings and data accessor methods for <xref:System.Data.SqlClient>.</span></span>  
  
 [<span data-ttu-id="f38f9-117">OLE DB 資料類型對應</span><span class="sxs-lookup"><span data-stu-id="f38f9-117">OLE DB Data Type Mappings</span></span>](ole-db-data-type-mappings.md)  
 <span data-ttu-id="f38f9-118">列出 <xref:System.Data.OleDb> 的推斷資料型別對應和資料存取子方法。</span><span class="sxs-lookup"><span data-stu-id="f38f9-118">Lists inferred data type mappings and data accessor methods for <xref:System.Data.OleDb>.</span></span>  
  
 [<span data-ttu-id="f38f9-119">ODBC 資料類型對應</span><span class="sxs-lookup"><span data-stu-id="f38f9-119">ODBC Data Type Mappings</span></span>](odbc-data-type-mappings.md)  
 <span data-ttu-id="f38f9-120">列出 <xref:System.Data.Odbc> 的推斷資料型別對應和資料存取子方法。</span><span class="sxs-lookup"><span data-stu-id="f38f9-120">Lists inferred data type mappings and data accessor methods for <xref:System.Data.Odbc>.</span></span>  
  
 [<span data-ttu-id="f38f9-121">Oracle 資料類型對應</span><span class="sxs-lookup"><span data-stu-id="f38f9-121">Oracle Data Type Mappings</span></span>](oracle-data-type-mappings.md)  
 <span data-ttu-id="f38f9-122">列出 <xref:System.Data.OracleClient> 的推斷資料型別對應和資料存取子方法。</span><span class="sxs-lookup"><span data-stu-id="f38f9-122">Lists inferred data type mappings and data accessor methods for <xref:System.Data.OracleClient>.</span></span>  
  
 [<span data-ttu-id="f38f9-123">浮點數</span><span class="sxs-lookup"><span data-stu-id="f38f9-123">Floating-Point Numbers</span></span>](floating-point-numbers.md)  
 <span data-ttu-id="f38f9-124">說明開發人員在使用浮點數值 (Floating-Point Number) 時經常遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="f38f9-124">Describes issues that developers frequently encounter when working with floating-point numbers.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f38f9-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f38f9-125">See also</span></span>

- [<span data-ttu-id="f38f9-126">SQL Server 資料類型和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="f38f9-126">SQL Server Data Types and ADO.NET</span></span>](./sql/sql-server-data-types.md)
- [<span data-ttu-id="f38f9-127">設定參數和參數資料類型</span><span class="sxs-lookup"><span data-stu-id="f38f9-127">Configuring Parameters and Parameter Data Types</span></span>](configuring-parameters-and-parameter-data-types.md)
- [<span data-ttu-id="f38f9-128">擷取資料庫結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="f38f9-128">Retrieving Database Schema Information</span></span>](retrieving-database-schema-information.md)
- [<span data-ttu-id="f38f9-129">一般類型系統</span><span class="sxs-lookup"><span data-stu-id="f38f9-129">Common Type System</span></span>](../../../standard/base-types/common-type-system.md)
- <span data-ttu-id="f38f9-130">[轉換類型](/previous-versions/visualstudio/visual-studio-2008/t8s7t9bf(v=vs.90))</span><span class="sxs-lookup"><span data-stu-id="f38f9-130">[Converting Types](/previous-versions/visualstudio/visual-studio-2008/t8s7t9bf(v=vs.90))</span></span>
- <span data-ttu-id="f38f9-131">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="f38f9-131">[ADO.NET Overview](ado-net-overview.md)</span></span>
