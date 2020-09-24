---
title: LINQ to SQL 的典型使用步驟
ms.date: 03/30/2017
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
ms.openlocfilehash: dc8c4be1e895ee5c4c7947e6311e5bf71008490f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164256"
---
# <a name="typical-steps-for-using-linq-to-sql"></a>LINQ to SQL 的典型使用步驟

若要實作 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 應用程式，請遵循本主題稍後所說明的步驟。 請注意，許多步驟都是選擇性的步驟。 您可以放心使用預設狀態下的物件模型。  
  
 若要快速開始使用，請使用物件關聯式設計工具建立您的物件模型，並開始撰寫查詢的程式碼。  
  
## <a name="creating-the-object-model"></a>建立物件模型  

 第一步是從現有關聯式資料庫的中繼資料 (Metadata) 建立物件模型。 物件模型會根據開發人員的程式設計語言來表示資料庫。 如需詳細資訊，請參閱 [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)。  
  
### <a name="1-select-a-tool-to-create-the-model"></a>1. 選取用來建立模型的工具。  

 用於建立模型的工具有三種。  
  
- 物件關聯式設計工具  
  
     這個設計工具提供了豐富的使用者介面，可用於從現有資料庫建立物件模型。 此工具是 Visual Studio IDE 的一部分，最適合用於小型或中型資料庫。  
  
- SQLMetal 程式碼產生工具  
  
     此命令列公用程式提供與 O/R 設計工具稍微不同的選項組。 若要建立大型資料庫的模型，使用這項工具最適合。 如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../tools/sqlmetal-exe-code-generation-tool.md)。  
  
- 程式碼編輯器  
  
     您可以使用 [Visual Studio 程式碼編輯器] 或其他編輯器來撰寫自己的程式碼。 當您有現有的資料庫，而且可以使用 O/R 設計工具或 SQLMetal 工具時，不建議使用這種方法，這種方法可能會很容易發生錯誤。 但是，程式碼編輯器很適合用於調整您已經使用其他工具所產生的程式碼。 如需詳細資訊，請參閱 [如何：使用程式碼編輯器自訂實體類別](how-to-customize-entity-classes-by-using-the-code-editor.md)。  
  
### <a name="2-select-the-kind-of-code-you-want-to-generate"></a>2. 選取您要產生的程式碼類型。  
  
- C # 或 Visual Basic 原始程式碼檔，用於以屬性為基礎的對應。  
  
     然後，您會在 Visual Studio 專案中包含這個程式碼檔案。 如需詳細資訊，請參閱以 [屬性為基礎的對應](attribute-based-mapping.md)。  
  
- XML 檔：適用於外部對應。  
  
     使用這種方法，您可以將對應中繼資料留在應用程式程式碼外。 如需詳細資訊，請參閱 [外部對應](external-mapping.md)。  
  
    > [!NOTE]
    > O/R 設計工具不支援產生外部對應檔案。 您必須使用 SQLMetal 工具來實作這項功能。  
  
- DBML 檔：您可以在產生最終程式碼檔之前修改這個檔案。  
  
     這是一項進階功能。  
  
### <a name="3-refine-the-code-file-to-reflect-the-needs-of-your-application"></a>3. 精簡程式碼檔案，以反映應用程式的需求。  

 基於這個目的，您可以使用 O/R 設計工具或程式碼編輯器。  
  
## <a name="using-the-object-model"></a>使用物件模型  

 下圖顯示在兩層式案例中，開發人員和資料之間的關係。 針對其他案例，請參閱 [具有 LINQ to SQL 的多層式和遠端應用程式](n-tier-and-remote-applications-with-linq-to-sql.md)。  
  
 ![顯示 Linq 物件模型的螢幕擷取畫面。](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 您現在有了物件模型，接著就可以描述資訊要求以及操作該模型內的資料。 您會由物件模型中的物件和屬性觀點思考，而不是由資料庫的資料列和資料行觀點思考。 您不會直接處理資料庫。  
  
 當您指示 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 執行所述的查詢，或呼叫 `SubmitChanges()` 您已操作的資料時，會以 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 資料庫的語言與資料庫進行通訊。  
  
 下列表示使用所建立之物件模型的一般步驟。  
  
### <a name="1-create-queries-to-retrieve-information-from-the-database"></a>1. 建立查詢以從資料庫中取出資訊。  

 如需詳細資訊，請參閱 [查詢概念](query-concepts.md) 和 [查詢範例](query-examples.md)。  
  
### <a name="2-override-default-behaviors-for-insert-update-and-delete"></a>2. 覆寫 Insert、Update 和 Delete 的預設行為。  

 這是選擇性步驟。 如需詳細資訊，請參閱 [自訂插入、更新和刪除作業](customizing-insert-update-and-delete-operations.md)。  
  
### <a name="3-set-appropriate-options-to-detect-and-report-concurrency-conflicts"></a>3. 設定適當的選項來偵測和報告並行衝突。  

 您可以讓模型保有處理並行衝突時所用的預設值，也可加以變更以符合您的目的。 如需詳細資訊，請參閱 [如何：指定測試並行衝突的成員](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) 和 [如何：指定並行例外狀況的](how-to-specify-when-concurrency-exceptions-are-thrown.md)擲回時機。  
  
### <a name="4-establish-an-inheritance-hierarchy"></a>4. 建立繼承階層。  

 這是選擇性步驟。 如需詳細資訊，請參閱 [繼承支援](inheritance-support.md)。  
  
### <a name="5-provide-an-appropriate-user-interface"></a>5. 提供適當的使用者介面。  

 這個步驟是選擇性的步驟，要視應用程式的使用方式而定。  
  
### <a name="6-debug-and-test-your-application"></a>6. 針對您的應用程式進行 Debug 和 test。  

 如需詳細資訊，請參閱 [偵錯工具支援](debugging-support.md)。  
  
## <a name="see-also"></a>另請參閱

- [快速入門](getting-started.md)
- [建立物件模型](creating-the-object-model.md)
- [預存程序](stored-procedures.md)
