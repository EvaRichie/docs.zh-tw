---
title: SQL XML 資料行值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
ms.openlocfilehash: cd55e2263d4b71fe62910ac918e331ebe37833eb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177276"
---
# <a name="sql-xml-column-values"></a><span data-ttu-id="82056-102">SQL XML 資料行值</span><span class="sxs-lookup"><span data-stu-id="82056-102">SQL XML Column Values</span></span>

<span data-ttu-id="82056-103">SQL Server 支援 `xml` 資料類型，開發人員可以使用 <xref:System.Data.SqlClient.SqlCommand> 類別的標準行為擷取包含此類型的結果集。</span><span class="sxs-lookup"><span data-stu-id="82056-103">SQL Server supports the `xml` data type, and developers can retrieve result sets including this type using standard behavior of the <xref:System.Data.SqlClient.SqlCommand> class.</span></span> <span data-ttu-id="82056-104">`xml` 資料行的擷取方式就如同擷取任何資料行 (例如，擷取到 <xref:System.Data.SqlClient.SqlDataReader>)，但如果您想要將資料行的內容當做 XML 使用，則必須使用 <xref:System.Xml.XmlReader>。</span><span class="sxs-lookup"><span data-stu-id="82056-104">An `xml` column can be retrieved just as any column is retrieved (into a <xref:System.Data.SqlClient.SqlDataReader>, for example) but if you want to work with the content of the column as XML, you must use an <xref:System.Xml.XmlReader>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="82056-105">範例</span><span class="sxs-lookup"><span data-stu-id="82056-105">Example</span></span>  

 <span data-ttu-id="82056-106">下列主控台應用程式會從 **AdventureWorks** 資料庫中的 **Sales.Store** 資料表，選取兩個資料列 (每個資料列包含一個 `xml` 資料行) 至 <xref:System.Data.SqlClient.SqlDataReader> 執行個體中。</span><span class="sxs-lookup"><span data-stu-id="82056-106">The following console application selects two rows, each containing an `xml` column, from the **Sales.Store** table in the **AdventureWorks** database to a <xref:System.Data.SqlClient.SqlDataReader> instance.</span></span> <span data-ttu-id="82056-107">針對每個資料列，會使用 <xref:System.Data.SqlClient.SqlDataReader> 的 <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 方法來讀取 `xml` 資料行的值。</span><span class="sxs-lookup"><span data-stu-id="82056-107">For each row, the value of the `xml` column is read using the <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> method of <xref:System.Data.SqlClient.SqlDataReader>.</span></span> <span data-ttu-id="82056-108">此值會儲存於 <xref:System.Xml.XmlReader>。</span><span class="sxs-lookup"><span data-stu-id="82056-108">The value is stored in an <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="82056-109">請注意，如果您想要將內容設定為 <xref:System.Data.SqlTypes.SqlXml> 變數，就必須使用 <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A>，而不是 <xref:System.Data.IDataRecord.GetValue%2A> 方法；<xref:System.Data.IDataRecord.GetValue%2A> 會以字串形式傳回 `xml` 資料行的值。</span><span class="sxs-lookup"><span data-stu-id="82056-109">Note that you must use <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> rather than the <xref:System.Data.IDataRecord.GetValue%2A> method if you want to set the contents to a <xref:System.Data.SqlTypes.SqlXml> variable; <xref:System.Data.IDataRecord.GetValue%2A> returns the value of the `xml` column as a string.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="82056-110">當您安裝 SQL Server 時，預設不會安裝 **AdventureWorks** 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="82056-110">The **AdventureWorks** sample database is not installed by default when you install SQL Server.</span></span> <span data-ttu-id="82056-111">您可以執行 SQL Server 安裝程式加以安裝。</span><span class="sxs-lookup"><span data-stu-id="82056-111">You can install it by running SQL Server Setup.</span></span>  
  
 [!code-csharp[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/VB/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="82056-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="82056-112">See also</span></span>

- <xref:System.Data.SqlTypes.SqlXml>
- [<span data-ttu-id="82056-113">SQL Server 中的 XML 資料</span><span class="sxs-lookup"><span data-stu-id="82056-113">XML Data in SQL Server</span></span>](xml-data-in-sql-server.md)
- <span data-ttu-id="82056-114">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="82056-114">[ADO.NET Overview](../ado-net-overview.md)</span></span>
