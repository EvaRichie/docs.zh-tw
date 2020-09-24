---
title: 作法：以 Visual Basic 或 C# 產生物件模型
ms.date: 03/30/2017
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
ms.openlocfilehash: 03525b6f39dcccfb9c68da6bab8b524efa3613ef
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91158405"
---
# <a name="how-to-generate-the-object-model-in-visual-basic-or-c"></a><span data-ttu-id="3da02-102">如何：在 Visual Basic 或 C 中產生物件模型\#</span><span class="sxs-lookup"><span data-stu-id="3da02-102">How to: Generate the Object Model in Visual Basic or C\#</span></span>

<span data-ttu-id="3da02-103">在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，採用您自己之程式語言的物件模型 (Object Model) 會對應至關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="3da02-103">In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], an object model in your own programming language is mapped to a relational database.</span></span> <span data-ttu-id="3da02-104">有兩種工具可讓您從現有資料庫的中繼資料自動產生 Visual Basic 或 c # 模型。</span><span class="sxs-lookup"><span data-stu-id="3da02-104">Two tools are available for automatically generating a Visual Basic or C# model from the metadata of an existing database.</span></span>  
  
- <span data-ttu-id="3da02-105">如果您使用 Visual Studio，可以使用物件關聯式設計工具來產生物件模型。</span><span class="sxs-lookup"><span data-stu-id="3da02-105">If you are using Visual Studio, you can use the Object Relational Designer to generate an object model.</span></span> <span data-ttu-id="3da02-106">O/R 設計工具提供豐富的使用者介面，可協助您產生 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 物件模型。</span><span class="sxs-lookup"><span data-stu-id="3da02-106">The O/R Designer provides a rich user interface to help you generate a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] object model.</span></span> <span data-ttu-id="3da02-107">如需詳細資訊，請參閱 [Visual Studio 中的 Linq TO SQL 工具](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)。</span><span class="sxs-lookup"><span data-stu-id="3da02-107">For more information see, [Linq to SQL Tools in Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).</span></span>
  
- <span data-ttu-id="3da02-108">SQLMetal 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="3da02-108">The SQLMetal command-line tool.</span></span> <span data-ttu-id="3da02-109">如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../tools/sqlmetal-exe-code-generation-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="3da02-109">For more information, see [SqlMetal.exe (Code Generation Tool)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="3da02-110">如果您沒有現有的資料庫而想要從物件模型建立一個資料庫，可以使用程式碼編輯器和 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 建立物件模型。</span><span class="sxs-lookup"><span data-stu-id="3da02-110">If you do not have an existing database and want to create one from an object model, you can create your object model by using your code editor and <xref:System.Data.Linq.DataContext.CreateDatabase%2A>.</span></span> <span data-ttu-id="3da02-111">如需詳細資訊，請參閱 [如何：動態建立資料庫](how-to-dynamically-create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3da02-111">For more information, see [How to: Dynamically Create a Database](how-to-dynamically-create-a-database.md).</span></span>  
  
 <span data-ttu-id="3da02-112">O/R 設計工具的檔提供如何使用 O/R 設計工具產生 Visual Basic 或 c # 物件模型的範例。</span><span class="sxs-lookup"><span data-stu-id="3da02-112">Documentation for the O/R Designer provides examples of how to generate a Visual Basic or C# object model by using the O/R Designer.</span></span> <span data-ttu-id="3da02-113">下列資訊提供了如何使用 SQLMetal 命令列工具的範例。</span><span class="sxs-lookup"><span data-stu-id="3da02-113">The following information provide examples of how to use the SQLMetal command-line tool.</span></span> <span data-ttu-id="3da02-114">如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../tools/sqlmetal-exe-code-generation-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="3da02-114">For more information, see [SqlMetal.exe (Code Generation Tool)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="3da02-115">範例</span><span class="sxs-lookup"><span data-stu-id="3da02-115">Example</span></span>  

 <span data-ttu-id="3da02-116">下列範例所示的 SQLMetal 命令列會產生 Visual Basic 程式碼，作為 Northwind 範例資料庫的屬性型物件模型。</span><span class="sxs-lookup"><span data-stu-id="3da02-116">The SQLMetal command line shown in the following example produces Visual Basic code as the attribute-based object model of the Northwind sample database.</span></span> <span data-ttu-id="3da02-117">預存程序和函式也會呈現。</span><span class="sxs-lookup"><span data-stu-id="3da02-117">Stored procedures and functions are also rendered.</span></span>  
  
```console  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## <a name="example"></a><span data-ttu-id="3da02-118">範例</span><span class="sxs-lookup"><span data-stu-id="3da02-118">Example</span></span>  

 <span data-ttu-id="3da02-119">下列範例中所示的 SQLMetal 命令列產生的 C# 程式碼與 Northwind 範例資料庫之以屬性為基礎的物件模型相同。</span><span class="sxs-lookup"><span data-stu-id="3da02-119">The SQLMetal command line shown in the following example produces C# code as the attribute-based object model of the Northwind sample database.</span></span> <span data-ttu-id="3da02-120">預存程序和函式也會呈現，而且會自動將資料表名稱複數化。</span><span class="sxs-lookup"><span data-stu-id="3da02-120">Stored procedures and functions are also rendered, and table names are automatically pluralized.</span></span>  
  
```console  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## <a name="see-also"></a><span data-ttu-id="3da02-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3da02-121">See also</span></span>

- [<span data-ttu-id="3da02-122">程式設計指南</span><span class="sxs-lookup"><span data-stu-id="3da02-122">Programming Guide</span></span>](programming-guide.md)
- [<span data-ttu-id="3da02-123">LINQ to SQL 物件模型</span><span class="sxs-lookup"><span data-stu-id="3da02-123">The LINQ to SQL Object Model</span></span>](the-linq-to-sql-object-model.md)
- [<span data-ttu-id="3da02-124">依逐步解說學習</span><span class="sxs-lookup"><span data-stu-id="3da02-124">Learning by Walkthroughs</span></span>](learning-by-walkthroughs.md)
- [<span data-ttu-id="3da02-125">作法：使用程式碼編輯器自訂實體類別</span><span class="sxs-lookup"><span data-stu-id="3da02-125">How to: Customize Entity Classes by Using the Code Editor</span></span>](how-to-customize-entity-classes-by-using-the-code-editor.md)
- [<span data-ttu-id="3da02-126">屬性架構對應</span><span class="sxs-lookup"><span data-stu-id="3da02-126">Attribute-Based Mapping</span></span>](attribute-based-mapping.md)
- [<span data-ttu-id="3da02-127">SqlMetal.exe (程式碼產生工具) </span><span class="sxs-lookup"><span data-stu-id="3da02-127">SqlMetal.exe (Code Generation Tool)</span></span>](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [<span data-ttu-id="3da02-128">外部對應</span><span class="sxs-lookup"><span data-stu-id="3da02-128">External Mapping</span></span>](external-mapping.md)
- [<span data-ttu-id="3da02-129">下載範例資料庫</span><span class="sxs-lookup"><span data-stu-id="3da02-129">Downloading Sample Databases</span></span>](downloading-sample-databases.md)
- [<span data-ttu-id="3da02-130">建立物件模型</span><span class="sxs-lookup"><span data-stu-id="3da02-130">Creating the Object Model</span></span>](creating-the-object-model.md)
