---
title: 操作說明：建立和繫結至 ObservableCollection
description: 瞭解如何建立和系結至 Windows Presentation Foundation 中衍生自 ObservableCollection 類別的集合。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], ObservableCollection class
- notifications [WPF]
ms.assetid: 6cf7e275-df76-41c6-a611-53b889b8fd5a
ms.openlocfilehash: 36e3d2d84aff0ab96c9b2914da28d4c968c32bac
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617865"
---
# <a name="how-to-create-and-bind-to-an-observablecollection"></a>操作說明：建立和繫結至 ObservableCollection
這個範例示範如何建立和系結至衍生自類別的集合 <xref:System.Collections.ObjectModel.ObservableCollection%601> ，這是可在新增或移除專案時提供通知的集合類別。  
  
## <a name="example"></a>範例  
 下列範例顯示 `NameList` 集合的實作：  
  
```csharp  
public class NameList : ObservableCollection<PersonName>  
{  
    public NameList() : base()  
    {  
        Add(new PersonName("Willa", "Cather"));  
        Add(new PersonName("Isak", "Dinesen"));  
        Add(new PersonName("Victor", "Hugo"));  
        Add(new PersonName("Jules", "Verne"));  
    }  
  }  
  
  public class PersonName  
  {  
      private string firstName;  
      private string lastName;  
  
      public PersonName(string first, string last)  
      {  
          this.firstName = first;  
          this.lastName = last;  
      }  
  
      public string FirstName  
      {  
          get { return firstName; }  
          set { firstName = value; }  
      }  
  
      public string LastName  
      {  
          get { return lastName; }  
          set { lastName = value; }  
      }  
  }  
```  
  
```vb  
Public Class NameList  
    Inherits ObservableCollection(Of PersonName)  
  
    ' Methods  
    Public Sub New()  
        MyBase.Add(New PersonName("Willa", "Cather"))  
        MyBase.Add(New PersonName("Isak", "Dinesen"))  
        MyBase.Add(New PersonName("Victor", "Hugo"))  
        MyBase.Add(New PersonName("Jules", "Verne"))  
    End Sub  
  
End Class  
  
Public Class PersonName  
    ' Methods  
    Public Sub New(ByVal first As String, ByVal last As String)  
        Me._firstName = first  
        Me._lastName = last  
    End Sub  
  
    ' Properties  
    Public Property FirstName() As String  
        Get  
            Return Me._firstName  
        End Get  
        Set(ByVal value As String)  
            Me._firstName = value  
        End Set  
    End Property  
  
    Public Property LastName() As String  
        Get  
            Return Me._lastName  
        End Get  
        Set(ByVal value As String)  
            Me._lastName = value  
        End Set  
    End Property  
  
    ' Fields  
    Private _firstName As String  
    Private _lastName As String  
End Class  
```  
  
 您可以使用與其他 common language runtime （CLR）物件相同的方式來系結集合，如在[XAML 中讓資料可](how-to-make-data-available-for-binding-in-xaml.md)供系結中所述。 例如，您可以使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 具現化集合，並將集合指定為資源 (如這裡所示)：  
  
```xaml  
<Window  
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
  xmlns:c="clr-namespace:SDKSample"  
  x:Class="SDKSample.Window1"  
  Width="400"  
  Height="280"  
  Title="MultiBinding Sample">  
  
  <Window.Resources>  
    <c:NameList x:Key="NameListData"/>  
  
...  
  
</Window.Resources>  
```  
  
 然後，就可以繫結至集合：  
  
```xaml  
<ListBox Width="200"  
         ItemsSource="{Binding Source={StaticResource NameListData}}"  
         ItemTemplate="{StaticResource NameItemTemplate}"  
         IsSynchronizedWithCurrentItem="True"/>  
```  
  
 這裡並未顯示 `NameItemTemplate` 的定義。  
  
> [!NOTE]
> 集合中的物件必須滿足[繫結來源概觀](binding-sources-overview.md)中所述的需求。 特別是，如果您使用 <xref:System.Windows.Data.BindingMode.OneWay> 或 <xref:System.Windows.Data.BindingMode.TwoWay> （例如，想要在 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 來源屬性動態變更時進行更新），您必須執行適當的屬性變更通知機制，例如 <xref:System.ComponentModel.INotifyPropertyChanged> 介面。  
  
 如需詳細資訊，請參閱[資料繫結概觀](../../../desktop-wpf/data/data-binding-overview.md)中的＜繫結至集合＞一節。  
  
## <a name="see-also"></a>另請參閱

- [排序視圖中的資料](how-to-sort-data-in-a-view.md)
- [篩選視圖中的資料](how-to-filter-data-in-a-view.md)
- [使用 XAML 中的視圖排序和分組資料](how-to-sort-and-group-data-using-a-view-in-xaml.md)
- [資料系結總覽](../../../desktop-wpf/data/data-binding-overview.md)
- [操作說明主題](data-binding-how-to-topics.md)
