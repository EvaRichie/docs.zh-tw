---
title: 如何：將模型定義函式當做物件方法來呼叫
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
ms.openlocfilehash: 5e5ae2fd838a34d7f665b23a14db2a599367e801
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197790"
---
# <a name="how-to-call-model-defined-functions-as-object-methods"></a><span data-ttu-id="bd45c-102">如何：將模型定義函式當做物件方法來呼叫</span><span class="sxs-lookup"><span data-stu-id="bd45c-102">How to: Call Model-Defined Functions as Object Methods</span></span>

<span data-ttu-id="bd45c-103">本主題描述如何呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法，或做為自訂類別上的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-103">This topic describes how to call a model-defined function as a method on an <xref:System.Data.Objects.ObjectContext> object or as a static method on a custom class.</span></span> <span data-ttu-id="bd45c-104">*模型定義函數*是概念模型中定義的函數。</span><span class="sxs-lookup"><span data-stu-id="bd45c-104">A *model-defined function* is a function that is defined in the conceptual model.</span></span> <span data-ttu-id="bd45c-105">本主題的程序說明如何直接呼叫這些函式，而不是從 LINQ to Entities 查詢呼叫函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-105">The procedures in the topic describe how to call these functions directly instead of calling them from LINQ to Entities queries.</span></span> <span data-ttu-id="bd45c-106">如需在 LINQ to Entities 查詢中呼叫模型定義函數的詳細資訊，請參閱 [如何：在查詢中呼叫模型定義函數](how-to-call-model-defined-functions-in-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="bd45c-106">For information about calling model-defined functions in LINQ to Entities queries, see [How to: Call Model-Defined Functions in Queries](how-to-call-model-defined-functions-in-queries.md).</span></span>  
  
 <span data-ttu-id="bd45c-107">無論您是呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 方法，或是做為自訂類別上的靜態方法，您必須先使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 將方法對應至模型定義函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-107">Whether you call a model-defined function as an <xref:System.Data.Objects.ObjectContext> method or as a static method on a custom class, you must first map the method to the model-defined function with an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>.</span></span> <span data-ttu-id="bd45c-108">不過，當您定義 <xref:System.Data.Objects.ObjectContext> 類別上的方法時，您必須使用 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 屬性公開 LINQ 提供者，而當您定義自訂類別上的靜態方法時，您必須使用 <xref:System.Linq.IQueryable.Provider%2A> 屬性公開 LINQ 提供者。</span><span class="sxs-lookup"><span data-stu-id="bd45c-108">However, when you define a method on the <xref:System.Data.Objects.ObjectContext> class, you must use the <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> property to expose the LINQ provider, whereas when you define a static method on a custom class, you must use the <xref:System.Linq.IQueryable.Provider%2A> property to expose the LINQ provider.</span></span> <span data-ttu-id="bd45c-109">如需詳細資訊，請參閱下列程序後的範例。</span><span class="sxs-lookup"><span data-stu-id="bd45c-109">For more information, see the examples that follow the procedures below.</span></span>  
  
 <span data-ttu-id="bd45c-110">以下程序提供的重要概述，是關於呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法，以及呼叫做為自訂類別上的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-110">The procedures below provide high-level outlines for calling a model-defined function as a method on an <xref:System.Data.Objects.ObjectContext> object and as a static method on a custom class.</span></span> <span data-ttu-id="bd45c-111">下面的範例提供更多關於程序中之步驟的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bd45c-111">The examples that follow provide more detail about the steps in the procedures.</span></span> <span data-ttu-id="bd45c-112">程序假設您已在概念模型中定義函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-112">The procedures assume that you have defined a function in the conceptual model.</span></span> <span data-ttu-id="bd45c-113">如需詳細資訊，請參閱 [如何：在概念模型中定義自訂函數](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="bd45c-113">For more information, see [How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).</span></span>  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a><span data-ttu-id="bd45c-114">呼叫模型定義函式做為 ObjectContext 物件上的方法</span><span class="sxs-lookup"><span data-stu-id="bd45c-114">To call a model-defined function as a method on an ObjectContext object</span></span>  
  
1. <span data-ttu-id="bd45c-115">加入來源檔案以擴充衍生自 <xref:System.Data.Objects.ObjectContext> 類別的部分類別，該類別由 Entity Framework 工具自動產生。</span><span class="sxs-lookup"><span data-stu-id="bd45c-115">Add a source file to extend the partial class derived from the <xref:System.Data.Objects.ObjectContext> class, auto-generated by the Entity Framework tools.</span></span> <span data-ttu-id="bd45c-116">在另外的來源檔案中定義 CLR stub，可在檔案重新產生時，防止遺失變更的問題。</span><span class="sxs-lookup"><span data-stu-id="bd45c-116">Defining the CLR stub in a separate source file will prevent the changes from being lost when the file is regenerated.</span></span>  
  
2. <span data-ttu-id="bd45c-117">將 Common Language Runtime (CLR) 方法加入至執行下列工作的 <xref:System.Data.Objects.ObjectContext> 類別：</span><span class="sxs-lookup"><span data-stu-id="bd45c-117">Add a common language runtime (CLR) method to your <xref:System.Data.Objects.ObjectContext> class that does the following:</span></span>  
  
    - <span data-ttu-id="bd45c-118">對應至概念模型中定義的函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-118">Maps to the function defined in the conceptual model.</span></span> <span data-ttu-id="bd45c-119">若要對應方法，您必須將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-119">To map the method, you must apply an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> to the method.</span></span> <span data-ttu-id="bd45c-120">請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="bd45c-120">Note that the <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> and <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> parameters of the attribute are the namespace name of the conceptual model and the function name in the conceptual model, respectively.</span></span> <span data-ttu-id="bd45c-121">LINQ 的函式名稱解析是區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="bd45c-121">Function name resolution for LINQ is case sensitive.</span></span>  
  
    - <span data-ttu-id="bd45c-122">由 <xref:System.Linq.IQueryProvider.Execute%2A> 屬性傳回的方法會傳回 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 的結果。</span><span class="sxs-lookup"><span data-stu-id="bd45c-122">Returns the results of the <xref:System.Linq.IQueryProvider.Execute%2A> method that is returned by the <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> property.</span></span>  
  
3. <span data-ttu-id="bd45c-123">呼叫方法做為 <xref:System.Data.Objects.ObjectContext> 類別之執行個體上的成員。</span><span class="sxs-lookup"><span data-stu-id="bd45c-123">Call the method as a member on an instance of the <xref:System.Data.Objects.ObjectContext> class.</span></span>  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a><span data-ttu-id="bd45c-124">呼叫模型定義函式做為自訂類別上的靜態方法</span><span class="sxs-lookup"><span data-stu-id="bd45c-124">To call a model-defined function as static method on a custom class</span></span>  
  
1. <span data-ttu-id="bd45c-125">使用執行下列工作的靜態方法，將類別加入至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="bd45c-125">Add a class to your application with a static method that does the following:</span></span>  
  
    - <span data-ttu-id="bd45c-126">對應至概念模型中定義的函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-126">Maps to the function defined in the conceptual model.</span></span> <span data-ttu-id="bd45c-127">若要對應方法，您必須將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-127">To map the method, you must apply an <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> to the method.</span></span> <span data-ttu-id="bd45c-128">請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。</span><span class="sxs-lookup"><span data-stu-id="bd45c-128">Note that the <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> and <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> parameters of the attribute are the namespace name of the conceptual model and the function name in the conceptual model, respectively.</span></span>  
  
    - <span data-ttu-id="bd45c-129">接受 <xref:System.Linq.IQueryable> 引數。</span><span class="sxs-lookup"><span data-stu-id="bd45c-129">Accepts an <xref:System.Linq.IQueryable> argument.</span></span>  
  
    - <span data-ttu-id="bd45c-130">由 <xref:System.Linq.IQueryProvider.Execute%2A> 屬性傳回的方法會傳回 <xref:System.Linq.IQueryable.Provider%2A> 的結果。</span><span class="sxs-lookup"><span data-stu-id="bd45c-130">Returns the results of the <xref:System.Linq.IQueryProvider.Execute%2A> method that is returned by the <xref:System.Linq.IQueryable.Provider%2A> property.</span></span>  
  
2. <span data-ttu-id="bd45c-131">呼叫方法做為自訂類別上之靜態方法的成員</span><span class="sxs-lookup"><span data-stu-id="bd45c-131">Call the method as a member a static method on the custom class</span></span>  
  
## <a name="example"></a><span data-ttu-id="bd45c-132">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-132">Example</span></span>  

 <span data-ttu-id="bd45c-133">**呼叫模型定義函式做為 ObjectContext 物件上的方法**</span><span class="sxs-lookup"><span data-stu-id="bd45c-133">**Calling a Model-Defined Function as a Method on an ObjectContext Object**</span></span>  
  
 <span data-ttu-id="bd45c-134">下列範例示範如何呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-134">The following example demonstrates how to call a model-defined function as a method on an <xref:System.Data.Objects.ObjectContext> object.</span></span> <span data-ttu-id="bd45c-135">此範例使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。</span><span class="sxs-lookup"><span data-stu-id="bd45c-135">The example uses the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).</span></span>  
  
 <span data-ttu-id="bd45c-136">考慮以下傳回特定產品之產品營收的概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-136">Consider the conceptual model function below that returns product revenue for a specified product.</span></span> <span data-ttu-id="bd45c-137"> (如需將函式新增至概念模型的相關資訊，請參閱 [如何：在概念模型中定義自訂](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))函式。 ) </span><span class="sxs-lookup"><span data-stu-id="bd45c-137">(For information about adding the function to your conceptual model, see [How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).)</span></span>  
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a><span data-ttu-id="bd45c-138">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-138">Example</span></span>  

 <span data-ttu-id="bd45c-139">下列程式碼會將方法加入至 `AdventureWorksEntities` 類別，該類別會對應至前述概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-139">The following code adds a method to the `AdventureWorksEntities` class that maps to the conceptual model function above.</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-140">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-140">Example</span></span>  

 <span data-ttu-id="bd45c-141">下列程式碼會呼叫上述方法，顯示特定產品的產品營收：</span><span class="sxs-lookup"><span data-stu-id="bd45c-141">The following code calls the method above to display the product revenue for a specified product:</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-142">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-142">Example</span></span>  

 <span data-ttu-id="bd45c-143">下列範例示範如何呼叫傳回集合的模型定義函式 (做為 <xref:System.Linq.IQueryable%601> 物件)。</span><span class="sxs-lookup"><span data-stu-id="bd45c-143">The following example demonstrates how to call a model-defined function that returns a collection (as an <xref:System.Linq.IQueryable%601> object).</span></span> <span data-ttu-id="bd45c-144">考慮以下傳回指定產品 ID 之所有 `SalesOrderDetails` 的概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-144">Consider the conceptual model function below that returns all the `SalesOrderDetails` for a given product ID.</span></span>  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-145">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-145">Example</span></span>  

 <span data-ttu-id="bd45c-146">下列程式碼會將方法加入至 `AdventureWorksEntities` 類別，該類別會對應至前述概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-146">The following code adds a method to the `AdventureWorksEntities` class that maps to the conceptual model function above.</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-147">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-147">Example</span></span>  

 <span data-ttu-id="bd45c-148">下列程式碼會呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-148">The following code calls the method.</span></span> <span data-ttu-id="bd45c-149">請注意，傳回的 <xref:System.Linq.IQueryable%601> 查詢會進一步定義，以傳回每一個 `SalesOrderDetail` 的小計總和。</span><span class="sxs-lookup"><span data-stu-id="bd45c-149">Note that the returned <xref:System.Linq.IQueryable%601> query is further refined to return line totals for each `SalesOrderDetail`.</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-150">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-150">Example</span></span>  

 <span data-ttu-id="bd45c-151">**呼叫模型定義函式做為自訂類別上的靜態方法**</span><span class="sxs-lookup"><span data-stu-id="bd45c-151">**Calling a Model-Defined Function as a Static Method on a Custom Class**</span></span>  
  
 <span data-ttu-id="bd45c-152">下一個範例示範如何呼叫模型定義函式做為自訂類別上的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="bd45c-152">The next example demonstrates how to call a model-defined function as a static method on a custom class.</span></span> <span data-ttu-id="bd45c-153">此範例使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。</span><span class="sxs-lookup"><span data-stu-id="bd45c-153">The example uses the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="bd45c-154">當您呼叫模型定義函式做為自訂類別上的靜態方法時，模型定義函式必須接受集合，並傳回集合中之值的彙總。</span><span class="sxs-lookup"><span data-stu-id="bd45c-154">When you call a model-defined function as a static method on a custom class, the model-defined function must accept a collection and return an aggregation of values in the collection.</span></span>  
  
 <span data-ttu-id="bd45c-155">考慮以下傳回 SalesOrderDetail 集合之產品營收的概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-155">Consider the conceptual model function below that returns product revenue for a SalesOrderDetail collection.</span></span> <span data-ttu-id="bd45c-156"> (如需將函數新增至概念模型的相關資訊，請參閱 [如何：在概念模型中定義自訂](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))函式。 ) 。</span><span class="sxs-lookup"><span data-stu-id="bd45c-156">(For information about adding the function to your conceptual model, see [How to: Define Custom Functions in the Conceptual Model](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100)).).</span></span>  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a><span data-ttu-id="bd45c-157">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-157">Example</span></span>  

 <span data-ttu-id="bd45c-158">下列程式碼會將類別加入至包含靜態方法的應用程式，該靜態方法會對應至前述的概念模型函式。</span><span class="sxs-lookup"><span data-stu-id="bd45c-158">The following code adds a class to your application that contains a static method that maps to the conceptual model function above.</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a><span data-ttu-id="bd45c-159">範例</span><span class="sxs-lookup"><span data-stu-id="bd45c-159">Example</span></span>  

 <span data-ttu-id="bd45c-160">下列程式碼會呼叫上述方法，顯示 SalesOrderDetail 集合的產品營收：</span><span class="sxs-lookup"><span data-stu-id="bd45c-160">The following code calls the method above to display the product revenue for a SalesOrderDetail collection:</span></span>  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a><span data-ttu-id="bd45c-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bd45c-161">See also</span></span>

- <span data-ttu-id="bd45c-162">[.edmx 檔概觀](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="bd45c-162">[.edmx File Overview](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))</span></span>
- [<span data-ttu-id="bd45c-163">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="bd45c-163">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
- [<span data-ttu-id="bd45c-164">在 LINQ to Entities 查詢中呼叫函式</span><span class="sxs-lookup"><span data-stu-id="bd45c-164">Calling Functions in LINQ to Entities Queries</span></span>](calling-functions-in-linq-to-entities-queries.md)
