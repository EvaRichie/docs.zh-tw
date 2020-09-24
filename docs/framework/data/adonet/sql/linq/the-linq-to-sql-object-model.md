---
title: LINQ to SQL 物件模型
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81dd0c37-e2a4-4694-83b0-f2e49e693810
ms.openlocfilehash: b17e1b6f4a6f849e3b42d69e9b9c2d5f906218e1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155506"
---
# <a name="the-linq-to-sql-object-model"></a>LINQ to SQL 物件模型

在中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，以開發人員的程式設計語言表示的物件模型會對應至關係資料庫的資料模型。 然後就會根據物件模型對資料執行作業。  
  
 在這種情況下，您不會發出資料庫命令 (例如，`INSERT`) 至資料庫。 而是在您的物件模型中變更值和執行方法。 當您要查詢資料庫或將變更傳送至資料庫時，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會將您的要求轉譯為正確的 SQL 命令，並將這些命令傳送至資料庫。  
  
 ![顯示 Linq 物件模型的螢幕擷取畫面。](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 下表摘要說明物件模型中最基本的元素 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，以及其與關聯式資料模型中專案的關聯性：  
  
|LINQ to SQL 物件模型|關聯式資料模型|  
|------------------------------|---------------------------|  
|實體類別|資料表|  
|類別成員|資料行|  
|關聯|外部索引鍵關聯性|  
|方法|預存程序或函式|  
  
> [!NOTE]
> 下列說明假設您對於關聯式資料模型和規則有基本知識。  
  
## <a name="linq-to-sql-entity-classes-and-database-tables"></a>LINQ to SQL 實體類別和資料庫資料表  

 在中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，資料庫資料表是由 *實體類別*表示。 實體類別就像您可能建立的任何其他類別，但您會使用能讓類別與資料庫資料表產生關聯的特殊資訊來標註此類別。 您可將自訂屬性 (<xref:System.Data.Linq.Mapping.TableAttribute>) 加入至您的類別宣告，藉以產生此附註，如下列範例所示：  
  
### <a name="example"></a>範例  

 [!code-csharp[DLinqObjectModel#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#1)]
 [!code-vb[DLinqObjectModel#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#1)]  
  
 只有宣告為資料表的類別執行個體 (也就是實體類別) 可以儲存至資料庫。  
  
 如需詳細資訊，請參閱以屬性為 [基礎之對應](attribute-based-mapping.md)的資料表屬性區段。  
  
## <a name="linq-to-sql-class-members-and-database-columns"></a>LINQ to SQL 類別成員和資料庫資料行  

 除了使類別和資料表產生關聯以外，您還會指定欄位或屬性，以表示資料庫資料行。 基於這個目的，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會定義 <xref:System.Data.Linq.Mapping.ColumnAttribute> 屬性，如下列範例所示：  
  
### <a name="example"></a>範例  

 [!code-csharp[DLinqObjectModel#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#2)]
 [!code-vb[DLinqObjectModel#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#2)]  
  
 只有對應到資料行的欄位和屬性會保存至資料庫或自資料庫擷取。 至於未宣告為資料行者，則會被視為應用程式邏輯的暫時性部分。  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute> 屬性 (Attribute) 具有各種屬性 (Property)，您可以用於自訂表示資料行的這些成員 (例如，指定成員以表示主索引鍵資料行)。 如需詳細資訊，請參閱以屬性為 [基礎之對應](attribute-based-mapping.md)的資料行屬性區段。  
  
## <a name="linq-to-sql-associations-and-database-foreign-key-relationships"></a>LINQ to SQL 關聯和資料庫外部索引鍵關聯性  

 在中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，您可以藉由套用屬性，將資料庫關聯 (（例如外鍵與主鍵關聯性) ） <xref:System.Data.Linq.Mapping.AssociationAttribute> 。 在下列程式碼區段中， `Order` 類別包含 `Customer` 具有屬性的屬性 <xref:System.Data.Linq.Mapping.AssociationAttribute> 。 這個屬性 (Property) 與其屬性 (Attribute) 提供了與 `Order` 類別有關的 `Customer` 類別。  
  
 下列程式碼範例顯示 `Customer` 類別中的 `Order` 屬性 (Property)。  
  
### <a name="example"></a>範例  

 [!code-csharp[DLinqObjectModel#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#3)]
 [!code-vb[DLinqObjectModel#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#3)]  
  
 如需詳細資訊，請參閱以屬性為 [基礎之對應](attribute-based-mapping.md)的 [關聯屬性] 區段。  
  
## <a name="linq-to-sql-methods-and-database-stored-procedures"></a>LINQ to SQL 方法和資料庫預存程序  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支援預存程序和使用者定義函式。 在中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，您可以將這些資料庫定義的抽象概念對應至用戶端物件，以便從用戶端程式代碼以強型別的方式存取它們。 方法簽章與資料庫中定義的程序和函式簽章十分相似。 您可以使用 IntelliSense 來探索這些方法。  
  
 呼叫對應程序所傳回的結果集是強型別集合。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 會使用 <xref:System.Data.Linq.Mapping.FunctionAttribute> 和 <xref:System.Data.Linq.Mapping.ParameterAttribute> 屬性，將預存程序和函式對應至方法。 <xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A> 屬性可以區分表示預存程序的方法和表示使用者定義函式的方法。 如果此屬性設為 `false` (預設值)，則此方法表示預存程序。 如果設為 `true`，則此方法表示資料庫函式。  
  
> [!NOTE]
> 如果您使用 Visual Studio，可以使用物件關聯式設計工具來建立對應至預存程式和使用者定義函數的方法。  
  
### <a name="example"></a>範例  

 [!code-csharp[DLinqObjectModel#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#4)]
 [!code-vb[DLinqObjectModel#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#4)]  
  
 如需詳細資訊，請參閱 [屬性型對應](attribute-based-mapping.md) 和 [預存程式](stored-procedures.md)的函數屬性、預存程式屬性和參數屬性區段。  
  
## <a name="see-also"></a>另請參閱

- [屬性架構對應](attribute-based-mapping.md)
- [背景資訊](background-information.md)
