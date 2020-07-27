---
title: 如何：使用程式碼加入事件處理常式
description: 使用此範例來瞭解如何使用程式碼，將事件處理常式新增至 Windows Presentation Foundation 中的專案，而不是使用 XAML 來宣告。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- event handlers [WPF], adding
- XAML [WPF], adding event handlers
ms.assetid: 269c61e0-6bd9-4291-9bed-1c5ee66da486
ms.openlocfilehash: b36969f7a65ccbf6c9d03b22767d9eacdc177ad1
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87166370"
---
# <a name="how-to-add-an-event-handler-using-code"></a><span data-ttu-id="a3a1c-103">如何：使用程式碼加入事件處理常式</span><span class="sxs-lookup"><span data-stu-id="a3a1c-103">How to: Add an Event Handler Using Code</span></span>
<span data-ttu-id="a3a1c-104">這個範例示範如何使用程式碼，將事件處理常式新增至專案。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-104">This example shows how to add an event handler to an element by using code.</span></span>  
  
 <span data-ttu-id="a3a1c-105">如果您想要將事件處理常式加入至專案 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，而且已經載入包含該專案的標記頁面，則必須使用程式碼加入處理常式。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-105">If you want to add an event handler to a [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] element, and the markup page that contains the element has already been loaded, you must add the handler using code.</span></span> <span data-ttu-id="a3a1c-106">或者，如果您要完全使用程式碼來建立應用程式的專案樹狀結構，而不使用宣告任何專案 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，您可以呼叫特定方法，將事件處理常式加入至結構化專案樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-106">Alternatively, if you are building up the element tree for an application entirely using code and not declaring any elements using [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], you can call specific methods to add event handlers to the constructed element tree.</span></span>  
  
## <a name="example"></a><span data-ttu-id="a3a1c-107">範例</span><span class="sxs-lookup"><span data-stu-id="a3a1c-107">Example</span></span>  
 <span data-ttu-id="a3a1c-108">下列範例會將新的加入 <xref:System.Windows.Controls.Button> 至一開始在中定義的現有頁面 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-108">The following example adds a new <xref:System.Windows.Controls.Button> to an existing page that is initially defined in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].</span></span> <span data-ttu-id="a3a1c-109">程式碼後置檔案會執行事件處理常式方法，然後在上加入該方法做為新的事件處理常式 <xref:System.Windows.Controls.Button> 。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-109">A code-behind file implements an event handler method and then adds that method as a new event handler on the <xref:System.Windows.Controls.Button>.</span></span>  
  
 <span data-ttu-id="a3a1c-110">C # 範例會使用 `+=` 運算子來指派事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-110">The C# example uses the `+=` operator to assign a handler to an event.</span></span> <span data-ttu-id="a3a1c-111">這是用來在 common language runtime （CLR）事件處理模型中指派處理常式的相同運算子。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-111">This is the same operator that is used to assign a handler in the common language runtime (CLR) event handling model.</span></span> <span data-ttu-id="a3a1c-112">Microsoft Visual Basic 不支援此運算子做為新增事件處理常式的方法。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-112">Microsoft Visual Basic does not support this operator as a means of adding event handlers.</span></span> <span data-ttu-id="a3a1c-113">而是需要下列其中一種技術：</span><span class="sxs-lookup"><span data-stu-id="a3a1c-113">It instead requires one of two techniques:</span></span>  
  
- <span data-ttu-id="a3a1c-114">搭配使用 <xref:System.Windows.UIElement.AddHandler%2A> 方法與 `AddressOf` 運算子，以參考事件處理常式的執行。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-114">Use the <xref:System.Windows.UIElement.AddHandler%2A> method, together with an `AddressOf` operator, to reference the event handler implementation.</span></span>  
  
- <span data-ttu-id="a3a1c-115">使用 `Handles` 關鍵字做為事件處理常式定義的一部分。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-115">Use the `Handles` keyword as part of the event handler definition.</span></span> <span data-ttu-id="a3a1c-116">這裡不會顯示這項技術;請參閱[Visual Basic 和 WPF 事件處理](visual-basic-and-wpf-event-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-116">This technique is not shown here; see [Visual Basic and WPF Event Handling](visual-basic-and-wpf-event-handling.md).</span></span>  
  
 [!code-xaml[RoutedEventAddRemoveHandler#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[RoutedEventAddRemoveHandler#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventAddRemoveHandler#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/VisualBasic/default.xaml.vb#handler)]  
  
> [!NOTE]
> <span data-ttu-id="a3a1c-117">在初始剖析的頁面中新增事件處理常式 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 會簡單許多。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-117">Adding an event handler in the initially parsed [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] page is much simpler.</span></span> <span data-ttu-id="a3a1c-118">在您要加入事件處理常式的物件專案中，加入與您要處理的事件名稱相符的屬性。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-118">Within the object element where you want to add the event handler, add an attribute that matches the name of the event that you want to handle.</span></span> <span data-ttu-id="a3a1c-119">然後指定該屬性的值，做為您在頁面的程式碼後置檔案中定義的事件處理常式方法的名稱 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-119">Then specify the value of that attribute as the name of the event handler method that you defined in the code-behind file of the [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] page.</span></span> <span data-ttu-id="a3a1c-120">如需詳細資訊，請參閱[XAML 總覽（WPF）](../../../desktop-wpf/fundamentals/xaml.md)或[路由事件總覽](routed-events-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a3a1c-120">For more information, see [XAML Overview (WPF)](../../../desktop-wpf/fundamentals/xaml.md) or [Routed Events Overview](routed-events-overview.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a3a1c-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a3a1c-121">See also</span></span>

- [<span data-ttu-id="a3a1c-122">路由事件概觀</span><span class="sxs-lookup"><span data-stu-id="a3a1c-122">Routed Events Overview</span></span>](routed-events-overview.md)
- [<span data-ttu-id="a3a1c-123">操作說明主題</span><span class="sxs-lookup"><span data-stu-id="a3a1c-123">How-to Topics</span></span>](events-how-to-topics.md)
