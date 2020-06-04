---
title: 撰寫查詢
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
ms.openlocfilehash: 25905d7ac3ca4bb66a22ad1df421b400eaa6b08f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413267"
---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>逐步解說：在 Visual Basic 中撰寫查詢

本逐步解說會示範如何使用 Visual Basic 語言功能來撰寫語言整合式查詢（LINQ）查詢運算式。 本逐步解說示範如何在學生物件清單上建立查詢、如何執行查詢，以及如何加以修改。 這些查詢會併入數個功能，包括物件初始化運算式、區欄位型別推斷和匿名型別。

完成本逐步解說之後，您就可以開始移至您感興趣之特定 LINQ 提供者的範例和檔。 LINQ 提供者包括 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 、LINQ to DataSet 和 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 。

## <a name="create-a-project"></a>建立專案

### <a name="to-create-a-console-application-project"></a>建立主控台應用程式專案

1. 啟動 Visual Studio。

2. 在 **[檔案]** 功能表上，指向 **[開新檔案]**，然後按一下 **[專案]**。

3. 在 [**已安裝的範本**] 清單中，按一下 [ **Visual Basic**]。

4. 在專案類型清單中，按一下 [**主控台應用程式**]。 在 [**名稱**] 方塊中，輸入專案的名稱，然後按一下 **[確定]**。

    隨即建立專案。 根據預設，它包含 System.web 的參考。 此外，[參考] 頁面上的 [匯**入的命名空間**] 清單 [[專案設計工具] （Visual Basic）](/visualstudio/ide/reference/references-page-project-designer-visual-basic)包含 <xref:System.Linq?displayProperty=nameWithType> 命名空間。

5. 在 [[編譯] 頁面上，[專案設計工具] （Visual Basic）](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，確定 [**選項推斷**] 已設定為 [**開啟**]。

## <a name="add-an-in-memory-data-source"></a>新增記憶體中的資料來源

本逐步解說中查詢的資料來源是物件的清單 `Student` 。 每個 `Student` 物件都包含名字、姓氏、類別年份，以及學生主體中的學術排名。

### <a name="to-add-the-data-source"></a>若要新增資料來源

- 定義 `Student` 類別，並建立類別的實例清單。

  > [!IMPORTANT]
  > `Student`[如何：建立專案清單](how-to-create-a-list-of-items.md)中提供定義類別及建立逐步解說範例所使用之清單所需的程式碼。 您可以從該處複製該檔案，並將它貼到您的專案中。 新的程式碼會取代您在建立專案時所出現的程式碼。

### <a name="to-add-a-new-student-to-the-students-list"></a>若要將新的學生新增至學生清單

- 請遵循方法中的模式 `getStudents` ，將類別的另一個實例新增 `Student` 至清單。 新增 student 會向您介紹物件初始化運算式。 如需詳細資訊，請參閱[物件初始化運算式：名稱和匿名型別](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。

## <a name="create-a-query"></a>建立查詢

執行時，本節中新增的查詢會產生一份清單，其中的學術排名會將其放在前十名。 因為查詢 `Student` 每次都會選取完整的物件，所以查詢結果的類型為 `IEnumerable(Of Student)` 。 不過，查詢定義中通常不會指定查詢的類型。 相反地，編譯器會使用區域型別推斷來判斷型別。 如需詳細資訊，請參閱[區欄位型別推斷](../../language-features/variables/local-type-inference.md)。 查詢的範圍變數 `currentStudent` 可作為來源中每個實例的參考，並 `Student` `students` 提供中每個物件屬性的存取權 `students` 。

### <a name="to-create-a-simple-query"></a>建立簡單查詢

1. 找出專案的方法中標示為的位置，如下所示 `Main` ：

    [!code-vb[VbLINQWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#1)]

    複製下列程式碼，並將它貼到中。

    [!code-vb[VbLINQWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#2)]

2. 將滑鼠指標停留 `studentQuery` 在您的程式碼中，以確認編譯器指派的類型為 `IEnumerable(Of Student)` 。

## <a name="run-the-query"></a>執行查詢

變數 `studentQuery` 包含查詢的定義，而不是執行查詢的結果。 執行查詢的一般機制是 `For Each` 迴圈。 傳回序列中的每個元素都是透過迴圈反覆運算變數來存取。 如需查詢執行的詳細資訊，請參閱[撰寫您的第一個 LINQ 查詢](writing-your-first-linq-query.md)。

### <a name="to-run-the-query"></a>若要執行查詢

1. 將下列迴圈新增至 `For Each` 專案中的查詢下方。

    [!code-vb[VbLINQWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#3)]

2. 將滑鼠指標停留在迴圈控制變數上 `studentRecord` ，以查看其資料類型。 的類型 `studentRecord` 會推斷為 `Student` ，因為會傳回 `studentQuery` 實例的集合 `Student` 。

3. 按 CTRL + F5，建立並執行應用程式。 請注意主控台視窗中的結果。

## <a name="modify-the-query"></a>修改查詢

如果查詢結果是依指定的順序，則會更容易掃描。 您可以根據任何可用的欄位來排序傳回的序列。

### <a name="to-order-the-results"></a>若要排序結果

1. 在 `Order By` `Where` 查詢的語句與語句之間加入下列子句 `Select` 。 `Order By`子句會根據每個學生的姓氏，從 A 到 Z 依字母順序排序結果。

    ```vb
    Order By currentStudent.Last Ascending
    ```

2. 若要依姓氏和名字進行排序，請將這兩個欄位加入至查詢：

    ```vb
    Order By currentStudent.Last Ascending, currentStudent.First Ascending
    ```

    您也可以指定 `Descending` 從 Z 到 A 的順序。

3. 按 CTRL + F5，建立並執行應用程式。 請注意主控台視窗中的結果。

### <a name="to-introduce-a-local-identifier"></a>引進區域識別碼

1. 加入本節中的程式碼，以在查詢運算式中引進區域識別碼。 本機識別碼會保存中繼結果。 在下列範例中， `name` 是一個識別碼，它會保存學生姓氏和名字的串連。 本機識別碼可以用來方便使用，也可以藉由儲存運算式的結果來提升效能，而這會計算多次。

    [!code-vb[VbLINQWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#4)]

2. 按 CTRL + F5，建立並執行應用程式。 請注意主控台視窗中的結果。

### <a name="to-project-one-field-in-the-select-clause"></a>若要在 Select 子句中投影一個欄位

1. `For Each`從這個區段加入查詢和迴圈，以建立查詢來產生一個序列，其專案與來源中的元素不同。 在下列範例中，來源是物件的集合 `Student` ，但只會傳回每個物件的其中一個成員：姓氏為 Garcia 的學生名字。 因為 `currentStudent.First` 是字串，所傳回之序列的資料類型 `studentQuery3` 是，這是 `IEnumerable(Of String)` 一系列的字串。 如先前的範例所示，的資料類型指派 `studentQuery3` 會留給編譯器使用區欄位型別推斷來判斷。

    [!code-vb[VbLINQWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#5)]

2. 將滑鼠指標停留 `studentQuery3` 在您的程式碼中，以確認指派的類型為 `IEnumerable(Of String)` 。

3. 按 CTRL + F5，建立並執行應用程式。 請注意主控台視窗中的結果。

### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>若要在 Select 子句中建立匿名型別

1. 加入本節中的程式碼，以查看如何在查詢中使用匿名型別。 當您想要從資料來源傳回數個欄位，而不是完成記錄（ `currentStudent` 先前範例中的記錄）或單一欄位（在上 `First` 一節中）時，您可以在查詢中使用它們。 您可以指定子句中的欄位，而 `Select` 編譯器會建立具有這些欄位做為其屬性的匿名型別，而不是定義新的命名型別，其中包含您想要包含在結果中的欄位。 如需詳細資訊，請參閱[匿名](../../language-features/objects-and-classes/anonymous-types.md)型別。

    下列範例會建立一個查詢，以根據學術排名的順序，傳回其學術排名介於1到10之間的老年人名稱和順位。 在此範例中，必須推斷的型別 `studentQuery4` ，因為 `Select` 子句會傳回匿名型別的實例，而且匿名型別沒有任何可用的名稱。

    [!code-vb[VbLINQWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#6)]

2. 按 CTRL + F5，建立並執行應用程式。 請注意主控台視窗中的結果。

## <a name="additional-examples"></a>其他範例

既然您已瞭解基本概念，以下是說明 LINQ 查詢彈性和能力的其他範例清單。 每個範例的前面都會加上其作用的簡短描述。 將滑鼠指標停留在每個查詢的查詢結果變數上，以查看推斷的類型。 使用 `For Each` 迴圈來產生結果。

[!code-vb[VbLINQWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQWalkthrough/VB/Class1.vb#7)]

## <a name="additional-information"></a>其他資訊

在您熟悉使用查詢的基本概念之後，您就可以開始閱讀您感興趣之特定 LINQ 提供者類型的檔和範例：

- [LINQ to Objects](linq-to-objects.md)

- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)

- [LINQ to XML](linq-to-xml.md)

- [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)

## <a name="see-also"></a>另請參閱

- [Language-Integrated Query (LINQ) (Visual Basic)](index.md)
- [使用 Visual Basic 撰寫 LINQ 入門](getting-started-with-linq.md)
- [區域型別推斷](../../language-features/variables/local-type-inference.md)
- [物件初始設定式：具名和匿名型別](../../language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [匿名類型](../../language-features/objects-and-classes/anonymous-types.md)
- [Visual Basic 中的 LINQ 簡介](../../language-features/linq/introduction-to-linq.md)
- [LINQ](../../language-features/linq/index.md)
- [查詢](../../../language-reference/queries/index.md)
