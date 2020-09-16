---
title: 如何：呼叫自訂資料庫函式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4354e5eb-dd45-469d-97fb-1c495705ee59
ms.openlocfilehash: 9879803c970b7965bf152c216367b216e201af38
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540304"
---
# <a name="how-to-call-custom-database-functions"></a>如何：呼叫自訂資料庫函式

本主題描述如何呼叫資料庫中定義的自訂資料庫函式，而資料庫是來自 LINQ to Entities 查詢。

從 LINQ to Entities 查詢呼叫的資料庫函式會在資料庫中執行。 在資料庫中執行函式可提升應用程式效能。

以下程序提供關於呼叫自訂資料庫函式的重要概述。 程序後的範例提供程序中之步驟相關詳細資訊。

## <a name="to-call-custom-functions-that-are-defined-in-the-database"></a>呼叫在資料庫中定義的自訂函式

1. 在您的資料庫中建立自訂函式。

     如需在 SQL Server 中建立自訂函數的詳細資訊，請參閱 [CREATE FUNCTION (transact-sql) ](/sql/t-sql/statements/create-function-transact-sql)。

2. 在 .edmx 檔案的存放結構定義語言 (SSDL) 中宣告函式。 函式的名稱必須和資料庫中宣告的函式名稱一樣。

     如需詳細資訊，請參閱 [ (SSDL) 的 Function 元素 ](/ef/ef6/modeling/designer/advanced/edmx/ssdl-spec#function-element-ssdl)。

3. 將對應的方法加入至應用程式程式碼的類別中，然後將 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute> 套用至方法。請注意，屬性的 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 和 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 參數分別是概念模型的命名空間名稱和概念模型中的函式名稱。 LINQ 的函式名稱解析是區分大小寫的。

4. 呼叫 LINQ to Entities 查詢中的方法。  

## <a name="example"></a>範例

下列範例示範如何從 LINQ to Entities 查詢中呼叫自訂資料庫函式。 範例使用 School 模型。 如需 School 模型的相關資訊，請參閱 [建立 School 範例資料庫](/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100)) 和 [產生 school .edmx](/previous-versions/dotnet/netframework-4.0/bb399739(v=vs.100))檔案。

下列程式碼會將 `AvgStudentGrade` 函式加入至 School 範例資料庫。

> [!NOTE]
> 無論資料庫伺服器為何，呼叫自訂資料庫函式的步驟都一樣。 不過，下列程式碼是專門在 SQL Server 資料庫中建立函式。 在其他資料庫中建立自訂函式的程式碼應該會不同。

[!code-sql[DP L2E MapToDBFunction#1](~/samples/snippets/tsql/VS_Snippets_Data/dp l2e maptodbfunction/tsql/create_avgstudentgrade.sql#1)]

## <a name="example"></a>範例

接下來，在您 *.edmx* 檔案的存放結構定義語言 (SSDL) 中宣告函數。 下列程式碼會 `AvgStudentGrade` 在 SSDL 中宣告函數：

[!code-xml[DP L2E MapToDBFunction#2](~/samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/school.edmx#2)]

## <a name="example"></a>範例

現在，建立方法，並將它對應至 SSDL 中宣告的函式。 使用 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>，將下列類別中的方法對應至 SSDL 中宣告的函式 (如上所述)。 呼叫此方法時，會執行資料庫中對應的函式。

[!code-csharp[DP L2E MapToDBFunction#3](~/samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#3)]
[!code-vb[DP L2E MapToDBFunction#3](~/samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#3)]

## <a name="example"></a>範例

最後，呼叫 LINQ to Entities 查詢中的方法。 下列程式碼會將學生的姓氏和平均分數顯示在主控台上：

[!code-csharp[DP L2E MapToDBFunction#4](~/samples/snippets/csharp/VS_Snippets_Data/dp l2e maptodbfunction/cs/program.cs#4)]
[!code-vb[DP L2E MapToDBFunction#4](~/samples/snippets/visualbasic/VS_Snippets_Data/dp l2e maptodbfunction/vb/module1.vb#4)]

## <a name="see-also"></a>另請參閱

- [.edmx 檔概觀](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [LINQ to Entities 中的查詢](queries-in-linq-to-entities.md)
