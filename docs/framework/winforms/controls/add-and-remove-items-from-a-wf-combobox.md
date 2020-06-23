---
title: 從 ComboBox、ListBox 或 CheckedListBox 控制項新增和移除專案
ms.date: 03/30/2017
description: 瞭解如何只在沒有資料系結的情況下，新增和移除 Windows Forms ComboBox、ListBox 和 CheckedListBox 控制項。
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- combo boxes [Windows Forms], adding items
- list boxes [Windows Forms], removing items
- ComboBox control [Windows Forms], adding and removing items
- ListBox control [Windows Forms], adding and removing items
- list boxes [Windows Forms], adding items
- combo boxes [Windows Forms], removing items
- CheckedListBox control [Windows Forms], adding and removing items
ms.assetid: 7224c8d2-4118-443e-ae1e-d7c17d1e69ee
ms.openlocfilehash: f3701257bbe410bf03c4c21700705e87b581bf2e
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904438"
---
# <a name="how-to-add-and-remove-items-from-a-windows-forms-combobox-listbox-or-checkedlistbox-control"></a><span data-ttu-id="0d5ea-103">如何：從 Windows Form 的 ComboBox、ListBox 或 CheckedListBox 控制項加入或移除項目</span><span class="sxs-lookup"><span data-stu-id="0d5ea-103">How to: Add and Remove Items from a Windows Forms ComboBox, ListBox, or CheckedListBox Control</span></span>
<span data-ttu-id="0d5ea-104">專案可以用各種方式加入至 Windows Forms 下拉式方塊、清單方塊或已核取清單方塊，因為這些控制項可以系結至各種不同的資料來源。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-104">Items can be added to a Windows Forms combo box, list box, or checked list box in a variety of ways, because these controls can be bound to a variety of data sources.</span></span> <span data-ttu-id="0d5ea-105">不過，本主題將示範最簡單的方法，而且不需要資料系結。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-105">However, this topic demonstrates the simplest method and requires no data binding.</span></span> <span data-ttu-id="0d5ea-106">顯示的專案通常是字串;不過，您可以使用任何物件。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-106">The items displayed are usually strings; however, any object can be used.</span></span> <span data-ttu-id="0d5ea-107">控制項中顯示的文字是物件的方法所傳回的值 `ToString` 。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-107">The text that is displayed in the control is the value returned by the object's `ToString` method.</span></span>  
  
### <a name="to-add-items"></a><span data-ttu-id="0d5ea-108">若要加入專案</span><span class="sxs-lookup"><span data-stu-id="0d5ea-108">To add items</span></span>  
  
1. <span data-ttu-id="0d5ea-109">使用類別的方法，將字串或物件新增至清單 `Add` `ObjectCollection` 。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-109">Add the string or object to the list by using the `Add` method of the `ObjectCollection` class.</span></span> <span data-ttu-id="0d5ea-110">使用屬性來參考集合 `Items` ：</span><span class="sxs-lookup"><span data-stu-id="0d5ea-110">The collection is referenced using the `Items` property:</span></span>  
  
    ```vb  
    ComboBox1.Items.Add("Tokyo")  
    ```  
  
    ```csharp  
    comboBox1.Items.Add("Tokyo");  
    ```  
  
    ```cpp  
    comboBox1->Items->Add("Tokyo");  
    ```  
  
     - <span data-ttu-id="0d5ea-111">或 -</span><span class="sxs-lookup"><span data-stu-id="0d5ea-111">or -</span></span>  
  
2. <span data-ttu-id="0d5ea-112">使用方法，在清單中的所需點插入字串或物件 `Insert` ：</span><span class="sxs-lookup"><span data-stu-id="0d5ea-112">Insert the string or object at the desired point in the list with the `Insert` method:</span></span>  
  
    ```vb  
    CheckedListBox1.Items.Insert(0, "Copenhagen")  
    ```  
  
    ```csharp  
    checkedListBox1.Items.Insert(0, "Copenhagen");  
    ```  
  
    ```cpp  
    checkedListBox1->Items->Insert(0, "Copenhagen");  
    ```  
  
     - <span data-ttu-id="0d5ea-113">或 -</span><span class="sxs-lookup"><span data-stu-id="0d5ea-113">or -</span></span>  
  
3. <span data-ttu-id="0d5ea-114">將整個陣列指派給 `Items` 集合：</span><span class="sxs-lookup"><span data-stu-id="0d5ea-114">Assign an entire array to the `Items` collection:</span></span>  
  
    ```vb  
    Dim ItemObject(9) As System.Object  
    Dim i As Integer  
       For i = 0 To 9  
       ItemObject(i) = "Item" & i  
    Next i  
    ListBox1.Items.AddRange(ItemObject)  
    ```  
  
    ```csharp  
    System.Object[] ItemObject = new System.Object[10];  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = "Item" + i;  
    }  
    listBox1.Items.AddRange(ItemObject);  
    ```  
  
    ```cpp  
    Array<System::Object^>^ ItemObject = gcnew Array<System::Object^>(10);  
    for (int i = 0; i <= 9; i++)  
    {  
       ItemObject[i] = String::Concat("Item", i.ToString());  
    }  
    listBox1->Items->AddRange(ItemObject);  
    ```  
  
### <a name="to-remove-an-item"></a><span data-ttu-id="0d5ea-115">若要移除專案</span><span class="sxs-lookup"><span data-stu-id="0d5ea-115">To remove an item</span></span>  
  
1. <span data-ttu-id="0d5ea-116">呼叫 `Remove` 或 `RemoveAt` 方法以刪除專案。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-116">Call the `Remove` or `RemoveAt` method to delete items.</span></span>  
  
     <span data-ttu-id="0d5ea-117">`Remove`具有一個指定要移除之專案的引數。`RemoveAt`</span><span class="sxs-lookup"><span data-stu-id="0d5ea-117">`Remove` has one argument that specifies the item to remove.`RemoveAt`</span></span> <span data-ttu-id="0d5ea-118">移除具有指定之索引編號的專案。</span><span class="sxs-lookup"><span data-stu-id="0d5ea-118">removes the item with the specified index number.</span></span>  
  
    ```vb  
    ' To remove item with index 0:  
    ComboBox1.Items.RemoveAt(0)  
    ' To remove currently selected item:  
    ComboBox1.Items.Remove(ComboBox1.SelectedItem)  
    ' To remove "Tokyo" item:  
    ComboBox1.Items.Remove("Tokyo")  
    ```  
  
    ```csharp  
    // To remove item with index 0:  
    comboBox1.Items.RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1.Items.Remove(comboBox1.SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1.Items.Remove("Tokyo");  
    ```  
  
    ```cpp  
    // To remove item with index 0:  
    comboBox1->Items->RemoveAt(0);  
    // To remove currently selected item:  
    comboBox1->Items->Remove(comboBox1->SelectedItem);  
    // To remove "Tokyo" item:  
    comboBox1->Items->Remove("Tokyo");  
    ```  
  
### <a name="to-remove-all-items"></a><span data-ttu-id="0d5ea-119">移除所有專案</span><span class="sxs-lookup"><span data-stu-id="0d5ea-119">To remove all items</span></span>  
  
1. <span data-ttu-id="0d5ea-120">呼叫 `Clear` 方法來移除集合中的所有專案：</span><span class="sxs-lookup"><span data-stu-id="0d5ea-120">Call the `Clear` method to remove all items from the collection:</span></span>  
  
    ```vb  
    ListBox1.Items.Clear()  
    ```  
  
    ```csharp  
    listBox1.Items.Clear();  
    ```  
  
    ```cpp  
    listBox1->Items->Clear();  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="0d5ea-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0d5ea-121">See also</span></span>

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- <xref:System.Windows.Forms.CheckedListBox>
- [<span data-ttu-id="0d5ea-122">如何：排序 Windows Form 中 ComboBox、ListBox 或 CheckedListBox 控制項的內容</span><span class="sxs-lookup"><span data-stu-id="0d5ea-122">How to: Sort the Contents of a Windows Forms ComboBox, ListBox, or CheckedListBox Control</span></span>](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [<span data-ttu-id="0d5ea-123">何時使用 Windows Forms ComboBox 取代 ListBox</span><span class="sxs-lookup"><span data-stu-id="0d5ea-123">When to Use a Windows Forms ComboBox Instead of a ListBox</span></span>](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)
- [<span data-ttu-id="0d5ea-124">用來列出選項的 Windows Form 控制項</span><span class="sxs-lookup"><span data-stu-id="0d5ea-124">Windows Forms Controls Used to List Options</span></span>](windows-forms-controls-used-to-list-options.md)
