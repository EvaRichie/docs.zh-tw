---
title: 預存程序
ms.date: 03/30/2017
ms.assetid: 4d23dd7a-a85f-44ff-a717-af7d0950c0fc
ms.openlocfilehash: 57420d95ec27af3b572940202fb6bc288c6888da
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203510"
---
# <a name="stored-procedures"></a>預存程序

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 使用物件模型中的方法來代表資料庫中的預存程式。 您可套用 <xref:System.Data.Linq.Mapping.FunctionAttribute> 屬性 (Attribute) 和 (視需要) 套用 <xref:System.Data.Linq.Mapping.ParameterAttribute> 屬性，將方法指定為預存程序。 如需詳細資訊，請參閱 [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)。  
  
 使用 Visual Studio 的開發人員通常會使用物件關聯式設計工具來對應預存程式。 本節中的主題顯示自行撰寫程式碼時，如何在應用程式中形成和呼叫這些方法。  
  
## <a name="in-this-section"></a>本節內容  

 [作法：傳回資料列集](how-to-return-rowsets.md)  
 描述如何傳回資料列，以及顯示如何使用輸入參數。  
  
 [作法：使用有參數的預存程序](how-to-use-stored-procedures-that-take-parameters.md)  
 描述如何使用輸入和輸出參數。  
  
 [作法：使用與多個結果型式對應的預存程序](how-to-use-stored-procedures-mapped-for-multiple-result-shapes.md)  
 描述如何為在相同預存程序中傳回多個圖案做準備。  
  
 [作法：使用與循序結果型式對應的預存程序](how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md)  
 描述如何為已知傳回序列情況下的多個圖案做準備。  
  
 [使用預存程序來自訂作業](customizing-operations-by-using-stored-procedures.md)  
 描述如何使用預存程序來實作插入、更新和刪除作業。  
  
 [以獨佔模式使用預存程序來自訂作業](customizing-operations-by-using-stored-procedures-exclusively.md)  
 描述如何只使用預存程序來實作插入、更新和刪除作業。  
  
## <a name="related-sections"></a>相關章節  

 [程式設計指南](programming-guide.md)  
 提供如何建立和使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 物件模型的相關資訊。  
  
 [逐步解說：僅使用預存程序 (Visual Basic)](walkthrough-using-only-stored-procedures-visual-basic.md)  
 包含可說明如何在 Visual Basic 中使用預存程序的相關程序。  
  
 [逐步解說：僅使用預存程序 (C#)](walkthrough-using-only-stored-procedures-csharp.md)  
 包含可說明如何在 C# 中使用預存程序的相關程序。
