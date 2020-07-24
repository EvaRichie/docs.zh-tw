---
title: '功能與程式性程式設計（LINQ to XML）（c #）'
description: 針對處理 XML，LINQ to XML 同時支援程式性、記憶體中 XML 樹狀結構修改，以及使用宣告式方法的功能結構。
ms.date: 07/20/2015
ms.assetid: fc64e39c-a487-4882-9169-da4de97917d9
ms.openlocfilehash: e19f9311c56f4fe2c5e7e5f228aca6c03c6fe04d
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103655"
---
# <a name="functional-vs-procedural-programming-linq-to-xml-c"></a>功能與程式性程式設計（LINQ to XML）（c #）
XML 應用程式有很多種：  
  
- 有些應用程式會採用 XML 來源文件，然後以不同於來源文件的組織結構產生新的 XML 文件。  
  
- 有些應用程式會採用 XML 來源文件，然後以完全不同的形式 (例如，HTML 或 CSV 文字檔)，產生結果文件。  
  
- 有些應用程式會採用 XML 來源文件，然後將記錄插入到資料庫中。  
  
- 有些應用程式會從其他來源 (例如，資料庫) 取得資料，然後從其中建立 XML 文件。  
  
 這些並非 XML 應用程式的全部類型，但是這些是 XML 程式設計人員必須實作的一組代表性的功能類型。  
  
 利用所有這些應用程式類型，開發人員可以採用兩種明顯不同的方法：  
  
- 使用宣告式方法的功能結構。  
  
- 使用程序性程式碼進行記憶體中 XML 樹狀結構修改。  
  
 LINQ to XML 同時支援這兩種方法。  
  
 使用功能性方法時，您可以撰寫採用來源文件的轉換，然後利用所需的組織結構產生全新的結果文件。  
  
 就地修改 XML 樹狀結構時，您可以撰寫可在記憶體中 XML 樹狀結構內周遊與導覽程式碼的程式碼，藉以在必要時插入、刪除與修改程式碼。  
  
 您可以搭配任一種方法使用 LINQ to XML。 您可以使用相同的類別，在某些情況下，也可以使用相同的方法。 但是，兩種方法的結構與目標差異相當大。 例如，在不同的情況下，其中一種方法的效能通常會比較好，而且或多或少會使用到記憶體。 此外，其中一種方法會比較容易撰寫，並產生較容易維護的程式碼。  
  
 若要查看這兩種方法的對比，請參閱[記憶體中的 XML 樹狀結構修改與功能結構（LINQ to XML）（c #）](./in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)。  
  
 如需撰寫功能性轉換的教學課程，請參閱 [XML 的純功能性轉換 (C#)](./introduction-to-pure-functional-transformations.md)。  
  
## <a name="see-also"></a>請參閱

- [LINQ to XML 程式設計概觀 (C#)](./linq-to-xml-overview.md)
