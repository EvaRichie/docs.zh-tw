---
title: 作法：使用 DataGrid 控制項實作驗證
description: 瞭解 Windows Presentation Foundation DataGrid 控制項如何在儲存格和資料列層級執行驗證，並提供驗證錯誤的意見反應。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], validation
- validation [WPF], DataGrid
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
ms.openlocfilehash: a6fe3693f94c3f554e96bc167b572cf854a1a34a
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87167602"
---
# <a name="how-to-implement-validation-with-the-datagrid-control"></a>作法：使用 DataGrid 控制項實作驗證
<xref:System.Windows.Controls.DataGrid>控制項可讓您在資料格和資料列層級執行驗證。 使用資料格層級驗證時，您會在使用者更新值時驗證系結資料物件的個別屬性。 使用資料列層級驗證時，您會在使用者認可資料列的變更時，驗證整個資料物件。 您也可以針對驗證錯誤提供自訂的視覺效果意見反應，或使用控制項提供的預設視覺效果意見反應 <xref:System.Windows.Controls.DataGrid> 。  
  
 下列程式說明如何將驗證規則套用至系結 <xref:System.Windows.Controls.DataGrid> ，並自訂視覺效果的意見反應。  
  
### <a name="to-validate-individual-cell-values"></a>驗證個別的資料格值  
  
- 在與資料行搭配使用的系結上，指定一或多個驗證規則。 這類似于在簡單控制項中驗證資料，如資料系結[總覽](../../../desktop-wpf/data/data-binding-overview.md)中所述。  
  
     下列範例顯示的 <xref:System.Windows.Controls.DataGrid> 控制項有四個數據行系結至商務物件的不同屬性。 有三個數據行會藉 <xref:System.Windows.Controls.ExceptionValidationRule> 由將 <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 屬性設定為來指定 `true` 。  
  
     [!code-xaml[DataGrid_Validation#BasicXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     當使用者輸入不正確值（例如 [課程識別碼] 資料行中的非整數）時，資料格周圍會出現紅色框線。 您可以變更此預設驗證意見反應，如下列程式所述。  
  
### <a name="to-customize-cell-validation-feedback"></a>自訂資料格驗證意見反應  
  
- 將資料行的 <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> 屬性設定為適用于資料行編輯控制項的樣式。 因為編輯控制項是在執行時間建立的，所以您無法使用 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> 附加屬性，就像使用簡單的控制項一樣。  
  
     下列範例會藉由加入具有驗證規則的三個數據行所共用的錯誤樣式，來更新上一個範例。 當使用者輸入不正確值時，樣式會變更儲存格背景色彩，並加入工具提示。 請注意，使用觸發程式來判斷是否有驗證錯誤。 這是必要的，因為目前沒有適用于資料格的專用錯誤範本。  
  
     [!code-xaml[DataGrid_Validation#CellValidationXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     您可以藉由取代資料行所使用的來執行更廣泛的自訂 <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> 。  
  
### <a name="to-validate-multiple-values-in-a-single-row"></a>若要驗證單一資料列中的多個值  
  
1. 執行檢查系結 <xref:System.Windows.Controls.ValidationRule> 資料物件之多個屬性的子類別。 在您的 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法執行中，將 `value` 參數值轉換成 <xref:System.Windows.Data.BindingGroup> 實例。 接著，您可以透過屬性存取資料物件 <xref:System.Windows.Data.BindingGroup.Items%2A> 。  
  
     下列範例會示範此程式，以驗證 `StartDate` 物件的屬性值是否 `Course` 早于其 `EndDate` 屬性值。  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2. 將驗證規則新增至 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=nameWithType> 集合。 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A>屬性可讓您直接存取實例的屬性，以將控制項所使用的所有系結 <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> <xref:System.Windows.Data.BindingGroup> 組成群組。  
  
     下列範例會 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> 在 XAML 中設定屬性。 <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A>屬性會設定為， <xref:System.Windows.Controls.ValidationStep.UpdatedValue> 因此只有在更新系結的資料物件之後，才會進行驗證。  
  
     [!code-xaml[DataGrid_Validation#RowValidationRulesXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     當使用者指定早于開始日期的結束日期時，資料列標題中會出現紅色驚嘆號（！）。 您可以變更此預設驗證意見反應，如下列程式所述。  
  
### <a name="to-customize-row-validation-feedback"></a>自訂資料列驗證意見反應  
  
- 設定 <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=nameWithType> 屬性。 這個屬性可讓您自訂個別控制項的資料列驗證意見反應 <xref:System.Windows.Controls.DataGrid> 。 您也可以使用隱含的資料列樣式來設定屬性，來影響多個控制項 <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=nameWithType> 。  
  
     下列範例會以更可見的指標取代預設資料列驗證意見反應。 當使用者輸入不正確值時，資料列標頭中會出現含有白色驚嘆號的紅色圓圈。 這會發生于資料列和資料格驗證錯誤。 相關聯的錯誤訊息會顯示在工具提示中。  
  
     [!code-xaml[DataGrid_Validation#RowValidationFeedbackXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## <a name="example"></a>範例  
 下列範例提供儲存格和資料列驗證的完整示範。 `Course`類別會提供範例資料物件， <xref:System.ComponentModel.IEditableObject> 以支援交易。 <xref:System.Windows.Controls.DataGrid>控制項會與互動， <xref:System.ComponentModel.IEditableObject> 讓使用者可以藉由按下 ESC 來還原變更。  
  
> [!NOTE]
> 如果您使用 Visual Basic，請在 Mainwindow.xaml 的第一行中，將取代 `x:Class="DataGridValidation.MainWindow"` 為 `x:Class="MainWindow"` 。  
  
 若要測試驗證，請嘗試下列動作：  
  
- 在 [課程識別碼] 資料行中，輸入非整數值。  
  
- 在 [結束日期] 資料行中，輸入早于開始日期的日期。  
  
- 刪除 [課程識別碼]、[開始日期] 或 [結束日期] 中的值。  
  
- 若要復原不正確資料格值，請將游標放回儲存格中，然後按下 ESC 鍵。  
  
- 若要在當前儲存格處於編輯模式時復原整個資料列的變更，請按 ESC 鍵兩次。  
  
- 發生驗證錯誤時，請將滑鼠指標移到資料列行首中的指示器上方，以查看相關聯的錯誤訊息。  
  
 [!code-csharp[DataGrid_Validation#FullCode](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xaml[DataGrid_Validation#FullXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Controls.DataGrid>
- [DataGrid](datagrid.md)
- [資料系結](../../../desktop-wpf/data/data-binding-overview.md)
- [執行系結驗證](../data/how-to-implement-binding-validation.md)
- [在自訂物件上執行驗證邏輯](../data/how-to-implement-validation-logic-on-custom-objects.md)
