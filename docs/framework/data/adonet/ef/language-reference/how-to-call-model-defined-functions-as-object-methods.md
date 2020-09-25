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
# <a name="how-to-call-model-defined-functions-as-object-methods"></a>如何：將模型定義函式當做物件方法來呼叫

本主題描述如何呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法，或做為自訂類別上的靜態方法。 *模型定義函數*是概念模型中定義的函數。 本主題的程序說明如何直接呼叫這些函式，而不是從 LINQ to Entities 查詢呼叫函式。 如需在 LINQ to Entities 查詢中呼叫模型定義函數的詳細資訊，請參閱 [如何：在查詢中呼叫模型定義函數](how-to-call-model-defined-functions-in-queries.md)。  
  
 無論您是呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 方法，或是做為自訂類別上的靜態方法，您必須先使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 將方法對應至模型定義函式。 不過，當您定義 <xref:System.Data.Objects.ObjectContext> 類別上的方法時，您必須使用 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 屬性公開 LINQ 提供者，而當您定義自訂類別上的靜態方法時，您必須使用 <xref:System.Linq.IQueryable.Provider%2A> 屬性公開 LINQ 提供者。 如需詳細資訊，請參閱下列程序後的範例。  
  
 以下程序提供的重要概述，是關於呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法，以及呼叫做為自訂類別上的靜態方法。 下面的範例提供更多關於程序中之步驟的詳細資訊。 程序假設您已在概念模型中定義函式。 如需詳細資訊，請參閱 [如何：在概念模型中定義自訂函數](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))。  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a>呼叫模型定義函式做為 ObjectContext 物件上的方法  
  
1. 加入來源檔案以擴充衍生自 <xref:System.Data.Objects.ObjectContext> 類別的部分類別，該類別由 Entity Framework 工具自動產生。 在另外的來源檔案中定義 CLR stub，可在檔案重新產生時，防止遺失變更的問題。  
  
2. 將 Common Language Runtime (CLR) 方法加入至執行下列工作的 <xref:System.Data.Objects.ObjectContext> 類別：  
  
    - 對應至概念模型中定義的函式。 若要對應方法，您必須將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。 請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。 LINQ 的函式名稱解析是區分大小寫的。  
  
    - 由 <xref:System.Linq.IQueryProvider.Execute%2A> 屬性傳回的方法會傳回 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 的結果。  
  
3. 呼叫方法做為 <xref:System.Data.Objects.ObjectContext> 類別之執行個體上的成員。  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a>呼叫模型定義函式做為自訂類別上的靜態方法  
  
1. 使用執行下列工作的靜態方法，將類別加入至您的應用程式：  
  
    - 對應至概念模型中定義的函式。 若要對應方法，您必須將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。 請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。  
  
    - 接受 <xref:System.Linq.IQueryable> 引數。  
  
    - 由 <xref:System.Linq.IQueryProvider.Execute%2A> 屬性傳回的方法會傳回 <xref:System.Linq.IQueryable.Provider%2A> 的結果。  
  
2. 呼叫方法做為自訂類別上之靜態方法的成員  
  
## <a name="example"></a>範例  

 **呼叫模型定義函式做為 ObjectContext 物件上的方法**  
  
 下列範例示範如何呼叫模型定義函式做為 <xref:System.Data.Objects.ObjectContext> 物件上的方法。 此範例使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。  
  
 考慮以下傳回特定產品之產品營收的概念模型函式。  (如需將函式新增至概念模型的相關資訊，請參閱 [如何：在概念模型中定義自訂](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))函式。 )   
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a>範例  

 下列程式碼會將方法加入至 `AdventureWorksEntities` 類別，該類別會對應至前述概念模型函式。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a>範例  

 下列程式碼會呼叫上述方法，顯示特定產品的產品營收：  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a>範例  

 下列範例示範如何呼叫傳回集合的模型定義函式 (做為 <xref:System.Linq.IQueryable%601> 物件)。 考慮以下傳回指定產品 ID 之所有 `SalesOrderDetails` 的概念模型函式。  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a>範例  

 下列程式碼會將方法加入至 `AdventureWorksEntities` 類別，該類別會對應至前述概念模型函式。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a>範例  

 下列程式碼會呼叫方法。 請注意，傳回的 <xref:System.Linq.IQueryable%601> 查詢會進一步定義，以傳回每一個 `SalesOrderDetail` 的小計總和。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a>範例  

 **呼叫模型定義函式做為自訂類別上的靜態方法**  
  
 下一個範例示範如何呼叫模型定義函式做為自訂類別上的靜態方法。 此範例使用 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。  
  
> [!NOTE]
> 當您呼叫模型定義函式做為自訂類別上的靜態方法時，模型定義函式必須接受集合，並傳回集合中之值的彙總。  
  
 考慮以下傳回 SalesOrderDetail 集合之產品營收的概念模型函式。  (如需將函數新增至概念模型的相關資訊，請參閱 [如何：在概念模型中定義自訂](/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))函式。 ) 。  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a>範例  

 下列程式碼會將類別加入至包含靜態方法的應用程式，該靜態方法會對應至前述的概念模型函式。  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a>範例  

 下列程式碼會呼叫上述方法，顯示 SalesOrderDetail 集合的產品營收：  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a>另請參閱

- [.edmx 檔概觀](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [LINQ to Entities 中的查詢](queries-in-linq-to-entities.md)
- [在 LINQ to Entities 查詢中呼叫函式](calling-functions-in-linq-to-entities-queries.md)
