---
title: LINQ to ADO.NET (入口網站頁面)
ms.date: 07/20/2015
ms.assetid: bbbd7c76-2981-4b91-b8d2-437547181f52
ms.openlocfilehash: 8c90783b56d6393ce3ac71945ed8ebffc8005ee1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84369176"
---
# <a name="linq-to-adonet-portal-page"></a><span data-ttu-id="d3b56-102">LINQ to ADO.NET (入口網站頁面)</span><span class="sxs-lookup"><span data-stu-id="d3b56-102">LINQ to ADO.NET (Portal Page)</span></span>
<span data-ttu-id="d3b56-103">LINQ to ADO.NET 可讓您使用語言整合式查詢（LINQ）程式設計模型，在 ADO.NET 中查詢任何可列舉物件。</span><span class="sxs-lookup"><span data-stu-id="d3b56-103">LINQ to ADO.NET enables you to query over any enumerable object in ADO.NET by using the Language-Integrated Query (LINQ) programming model.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="d3b56-104">LINQ to ADO.NET 檔位於 .NET Framework SDK 的 ADO.NET 區段： [LINQ 和 ADO.NET](../../../../framework/data/adonet/linq-and-ado-net.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b56-104">The LINQ to ADO.NET documentation is located in the ADO.NET section of the .NET Framework SDK: [LINQ and ADO.NET](../../../../framework/data/adonet/linq-and-ado-net.md).</span></span>
  
 <span data-ttu-id="d3b56-105">有三種不同的 ADO.NET 語言整合式查詢（LINQ）技術： LINQ to DataSet、 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 和 LINQ to Entities。</span><span class="sxs-lookup"><span data-stu-id="d3b56-105">There are three separate ADO.NET Language-Integrated Query (LINQ) technologies: LINQ to DataSet, [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)], and LINQ to Entities.</span></span> <span data-ttu-id="d3b56-106">LINQ to DataSet 可提供更豐富且最佳化的 <xref:System.Data.DataSet> 查詢，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 可讓您直接查詢 SQL Server 資料庫結構描述，而 LINQ to Entities 可讓您查詢實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="d3b56-106">LINQ to DataSet provides richer, optimized querying over the <xref:System.Data.DataSet>, [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] enables you to directly query SQL Server database schemas, and LINQ to Entities allows you to query an Entity Data Model.</span></span>  
  
## <a name="linq-to-dataset"></a><span data-ttu-id="d3b56-107">LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="d3b56-107">LINQ to DataSet</span></span>  
 <span data-ttu-id="d3b56-108"><xref:System.Data.DataSet> 是 ADO.NET 中最廣為使用的元件之一，也是中斷連線程式設計模型 (ADO.NET 建置於其上) 的重要元素。</span><span class="sxs-lookup"><span data-stu-id="d3b56-108">The <xref:System.Data.DataSet> is one of the most widely used components in ADO.NET, and is a key element of the disconnected programming model that ADO.NET is built on.</span></span> <span data-ttu-id="d3b56-109">雖然 <xref:System.Data.DataSet> 具有上述優點，但是它的查詢功能仍然有限。</span><span class="sxs-lookup"><span data-stu-id="d3b56-109">Despite this prominence, however, the <xref:System.Data.DataSet> has limited query capabilities.</span></span>  
  
 <span data-ttu-id="d3b56-110">LINQ to DataSet 可讓您使用許多其他資料來源適用的相同查詢功能，將更為豐富的查詢功能建置在 <xref:System.Data.DataSet> 中。</span><span class="sxs-lookup"><span data-stu-id="d3b56-110">LINQ to DataSet enables you to build richer query capabilities into <xref:System.Data.DataSet> by using the same query functionality that is available for many other data sources.</span></span>  
  
 <span data-ttu-id="d3b56-111">如需詳細資訊，請參閱 [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b56-111">For more information, see [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md).</span></span>  
  
## <a name="linq-to-sql"></a><span data-ttu-id="d3b56-112">LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="d3b56-112">LINQ to SQL</span></span>  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] <span data-ttu-id="d3b56-113">提供的執行階段基礎結構可以將關聯式資料當成物件來管理。</span><span class="sxs-lookup"><span data-stu-id="d3b56-113">provides a run-time infrastructure for managing relational data as objects.</span></span> <span data-ttu-id="d3b56-114">在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 中，關聯式資料庫的資料模型會對應至以開發人員的程式設計語言表示的物件模型。</span><span class="sxs-lookup"><span data-stu-id="d3b56-114">In [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)], the data model of a relational database is mapped to an object model expressed in the programming language of the developer.</span></span> <span data-ttu-id="d3b56-115">執行應用程式時，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 會將物件模型中的 Language-integrated Query (LINQ) 轉譯成 SQL，並將這些查詢傳送至資料庫以便執行。</span><span class="sxs-lookup"><span data-stu-id="d3b56-115">When you execute the application, [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] translates language-integrated queries in the object model into SQL and sends them to the database for execution.</span></span> <span data-ttu-id="d3b56-116">當資料庫傳回結果時，[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 會將結果轉譯回物件，方便您加以管理。</span><span class="sxs-lookup"><span data-stu-id="d3b56-116">When the database returns the results, [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] translates them back into objects that you can manipulate.</span></span>  
  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] <span data-ttu-id="d3b56-117">可支援資料庫的預存程序和使用者定義函式，以及物件模型中的繼承。</span><span class="sxs-lookup"><span data-stu-id="d3b56-117">includes support for stored procedures and user-defined functions in the database, and for inheritance in the object model.</span></span>  
  
 <span data-ttu-id="d3b56-118">如需詳細資訊，請參閱 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b56-118">For more information, see [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md).</span></span>  
  
## <a name="linq-to-entities"></a><span data-ttu-id="d3b56-119">LINQ to Entities</span><span class="sxs-lookup"><span data-stu-id="d3b56-119">LINQ to Entities</span></span>  
 <span data-ttu-id="d3b56-120">透過實體資料模型，關聯式資料會公開為 .NET 環境內的物件。</span><span class="sxs-lookup"><span data-stu-id="d3b56-120">Through the Entity Data Model, relational data is exposed as objects in the .NET environment.</span></span> <span data-ttu-id="d3b56-121">這讓物件層成為 LINQ 支援的理想目標，讓開發人員能夠根據用來建立商務邏輯的語言，為資料庫制訂查詢。</span><span class="sxs-lookup"><span data-stu-id="d3b56-121">This makes the object layer an ideal target for LINQ support, allowing developers to formulate queries against the database from the language used to build the business logic.</span></span> <span data-ttu-id="d3b56-122">這項功能稱為 LINQ to Entities。</span><span class="sxs-lookup"><span data-stu-id="d3b56-122">This capability is known as LINQ to Entities.</span></span> <span data-ttu-id="d3b56-123">如需詳細資訊，請參閱 [LINQ to Entities](../../../../framework/data/adonet/ef/language-reference/linq-to-entities.md)。</span><span class="sxs-lookup"><span data-stu-id="d3b56-123">See [LINQ to Entities](../../../../framework/data/adonet/ef/language-reference/linq-to-entities.md) for more information.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d3b56-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d3b56-124">See also</span></span>

- [<span data-ttu-id="d3b56-125">LINQ 和 ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d3b56-125">LINQ and ADO.NET</span></span>](../../../../framework/data/adonet/linq-and-ado-net.md)
- [<span data-ttu-id="d3b56-126">Language-Integrated Query (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d3b56-126">Language-Integrated Query (LINQ) (Visual Basic)</span></span>](index.md)
