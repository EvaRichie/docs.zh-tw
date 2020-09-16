---
title: 如何：在查詢中呼叫模型定義函式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6c804e4d-f348-4afd-9f63-d3f0f24bc6a9
ms.openlocfilehash: 38c43fa509b5259aa94ca416aadb51b405fc5dc7
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90542394"
---
# <a name="how-to-call-model-defined-functions-in-queries"></a><span data-ttu-id="e402e-102">如何：在查詢中呼叫模型定義函式</span><span class="sxs-lookup"><span data-stu-id="e402e-102">How to: Call Model-Defined Functions in Queries</span></span>
<span data-ttu-id="e402e-103">本主題描述如何從 LINQ to Entities 查詢內呼叫概念模型中定義的函數。</span><span class="sxs-lookup"><span data-stu-id="e402e-103">This topic describes how to call functions that are defined in the conceptual model from within LINQ to Entities queries.</span></span>  
  
 <span data-ttu-id="e402e-104">下列程式提供從 LINQ to Entities 查詢中呼叫模型定義函數的高階大綱。</span><span class="sxs-lookup"><span data-stu-id="e402e-104">The procedure below provides a high-level outline for calling a model-defined function from within a LINQ to Entities query.</span></span> <span data-ttu-id="e402e-105">程序後的範例提供程序中之步驟相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e402e-105">The example that follows provides more detail about the steps in the procedure.</span></span> <span data-ttu-id="e402e-106">程序假設您已在概念模型中定義函式。</span><span class="sxs-lookup"><span data-stu-id="e402e-106">The procedure assumes that you have defined a function in the conceptual model.</span></span> <span data-ttu-id="e402e-107">如需詳細資訊，請參閱 [如何：在概念模型中定義自訂函數](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="e402e-107">For more information, see [How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).</span></span>  
  
### <a name="to-call-a-function-defined-in-the-conceptual-model"></a><span data-ttu-id="e402e-108">呼叫概念模型中定義的函式</span><span class="sxs-lookup"><span data-stu-id="e402e-108">To call a function defined in the conceptual model</span></span>  
  
1. <span data-ttu-id="e402e-109">將 Common Language Runtime (CLR) 方法加入至您的應用程式，該方法會對應至概念模型中所定義之函式。</span><span class="sxs-lookup"><span data-stu-id="e402e-109">Add a common language runtime (CLR) method to your application that maps to the function defined in the conceptual model.</span></span> <span data-ttu-id="e402e-110">若要對應方法，您必須將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。</span><span class="sxs-lookup"><span data-stu-id="e402e-110">To map the method, you must apply an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> to the method.</span></span> <span data-ttu-id="e402e-111">請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="e402e-111">Note that the <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> and <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> parameters of the attribute are the namespace name of the conceptual model and the function name in the conceptual model respectively.</span></span> <span data-ttu-id="e402e-112">LINQ 的函式名稱解析是區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="e402e-112">Function name resolution for LINQ is case sensitive.</span></span>  
  
2. <span data-ttu-id="e402e-113">呼叫 LINQ to Entities 查詢中的函式。</span><span class="sxs-lookup"><span data-stu-id="e402e-113">Call the function in a LINQ to Entities query.</span></span>  
  
## <a name="example"></a><span data-ttu-id="e402e-114">範例</span><span class="sxs-lookup"><span data-stu-id="e402e-114">Example</span></span>  
 <span data-ttu-id="e402e-115">下列範例示範如何從 LINQ to Entities 查詢中呼叫概念模型中定義的函數。</span><span class="sxs-lookup"><span data-stu-id="e402e-115">The following example demonstrates how to call a function that is defined in the conceptual model from within a LINQ to Entities query.</span></span> <span data-ttu-id="e402e-116">範例使用 School 模型。</span><span class="sxs-lookup"><span data-stu-id="e402e-116">The example uses the School model.</span></span> <span data-ttu-id="e402e-117">如需 School 模型的相關資訊，請參閱 [建立 School 範例資料庫](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)) 和 [產生 school .edmx](/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100))檔案。</span><span class="sxs-lookup"><span data-stu-id="e402e-117">For information about the School model, see [Creating the School Sample Database](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)) and [Generating the School .edmx File](/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100)).</span></span>  
  
 <span data-ttu-id="e402e-118">下列概念模型函式會傳回講師受雇之後經過的年份。</span><span class="sxs-lookup"><span data-stu-id="e402e-118">The following conceptual model function returns the number of years since an instructor was hired.</span></span> <span data-ttu-id="e402e-119">如需將函數新增至概念模型的相關資訊，請參閱 [如何：在概念模型中定義自訂](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))函式 ) 。</span><span class="sxs-lookup"><span data-stu-id="e402e-119">For information about adding the function to a conceptual model, see [How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).)</span></span>  
  
 [!code-xml[DP ConceptualModelFunctions#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp conceptualmodelfunctions/xml/school.edmx#1)]
  
## <a name="example"></a><span data-ttu-id="e402e-120">範例</span><span class="sxs-lookup"><span data-stu-id="e402e-120">Example</span></span>  
 <span data-ttu-id="e402e-121">接下來，將下列方法加入至您的應用程式並使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 將它對應至概念模型函式：</span><span class="sxs-lookup"><span data-stu-id="e402e-121">Next, add the following method to your application and use an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> to map it to the conceptual model function:</span></span>  
  
 [!code-csharp[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#2)]
 [!code-vb[DP ConceptualModelFunctions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#2)]  
  
## <a name="example"></a><span data-ttu-id="e402e-122">範例</span><span class="sxs-lookup"><span data-stu-id="e402e-122">Example</span></span>  
 <span data-ttu-id="e402e-123">現在您可以從 LINQ to Entities 查詢內呼叫概念模型函數。</span><span class="sxs-lookup"><span data-stu-id="e402e-123">Now you can call the conceptual model function from within a LINQ to Entities query.</span></span> <span data-ttu-id="e402e-124">下列程式碼會呼叫該方法，顯示受雇超過十年的所有講師：</span><span class="sxs-lookup"><span data-stu-id="e402e-124">The following code calls the method to display all instructors that were hired more than ten years ago:</span></span>  
  
 [!code-csharp[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp conceptualmodelfunctions/cs/program.cs#3)]
 [!code-vb[DP ConceptualModelFunctions#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp conceptualmodelfunctions/vb/module1.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="e402e-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e402e-125">See also</span></span>

- <span data-ttu-id="e402e-126">[.edmx 檔概觀](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="e402e-126">[.edmx File Overview](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span></span>
- [<span data-ttu-id="e402e-127">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="e402e-127">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
- [<span data-ttu-id="e402e-128">在 LINQ to Entities 查詢中呼叫函式</span><span class="sxs-lookup"><span data-stu-id="e402e-128">Calling Functions in LINQ to Entities Queries</span></span>](calling-functions-in-linq-to-entities-queries.md)
- [<span data-ttu-id="e402e-129">如何：將模型定義函式當做物件方法來呼叫</span><span class="sxs-lookup"><span data-stu-id="e402e-129">How to: Call Model-Defined Functions as Object Methods</span></span>](how-to-call-model-defined-functions-as-object-methods.md)
