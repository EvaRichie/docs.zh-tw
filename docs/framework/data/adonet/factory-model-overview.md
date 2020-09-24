---
title: 處理站模型概觀
ms.date: 03/30/2017
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
ms.openlocfilehash: 7cee3966ab3a37d2dbc6dd0ea9ab26b485ef63fd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156390"
---
# <a name="factory-model-overview"></a>處理站模型概觀

ADO.NET 2.0 在 <xref:System.Data.Common> 命名空間 (Namespace) 中導入了新的基底類別 (Base Class)。 這些基底類別是抽象類別，表示它們無法直接具現化 (Instantiated)。 它們包括 <xref:System.Data.Common.DbConnection>、<xref:System.Data.Common.DbCommand> 和 <xref:System.Data.Common.DbDataAdapter>，而且可由 .NET Framework 資料提供者 (例如 <xref:System.Data.SqlClient> 和 <xref:System.Data.OleDb>) 共用。 加入基底類別可簡化針對 .NET Framework 資料提供者加入功能的程序，而且不需要建立新的介面。  
  
 ADO.NET 2.0 也導入了抽象基底類別，可讓開發人員撰寫不需仰賴特定資料提供者的泛型資料存取程式碼。  
  
## <a name="the-factory-design-pattern"></a>Factory 設計模式  

 撰寫獨立於提供者以外之程式碼的程式設計模型是以 "Factory" 設計模式為基礎，而這種設計模式會使用單一 API 來存取多個提供者之間的資料庫。 要適當命名此模式，因為它會要求僅用特定的物件來建立其他物件，與實際的 Factory 非常相似。 如需 factory 設計模式的詳細說明，請參閱 [撰寫 ASP.NET 2.0 和 ADO.NET 2.0 中的一般資料存取程式碼](/previous-versions/dotnet/articles/ms971499(v=msdn.10))。
  
 從 ADO.NET 2.0 開始，<xref:System.Data.Common.DbProviderFactories> 類別會提供 `static` (或 Visual Basic 中的 `Shared`) 方法來建立 <xref:System.Data.Common.DbProviderFactory> 執行個體。 然後，此執行個體會根據提供者資訊以及在執行階段提供的連接字串，傳回正確的強型別物件。  
  
## <a name="see-also"></a>另請參閱

- [取得 DbProviderFactory](obtaining-a-dbproviderfactory.md)
- [DbConnection、DbCommand 和 DbException](dbconnection-dbcommand-and-dbexception.md)
- [使用 DbDataAdapter 修改資料](modifying-data-with-a-dbdataadapter.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
