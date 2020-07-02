---
ms.openlocfilehash: 6da589057cebfbf3f67a46b8d49d3a61f037c4c7
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622232"
---
### <a name="crash-in-selector-when-removing-an-item-from-a-custom-incc-collection"></a><span data-ttu-id="20779-101">從自訂 INCC 集合中移除項目時，選取器發生損毀</span><span class="sxs-lookup"><span data-stu-id="20779-101">Crash in Selector when removing an item from a custom INCC collection</span></span>

#### <a name="details"></a><span data-ttu-id="20779-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="20779-102">Details</span></span>

<span data-ttu-id="20779-103">在下列狀況中可能發生 <code>T:System.InvalidOperationException</code>：</span><span class="sxs-lookup"><span data-stu-id="20779-103">An <code>T:System.InvalidOperationException</code> can occur in the following scenario:</span></span><ul><li><span data-ttu-id="20779-104"><code>T:System.Windows.Controls.Primitives.Selector</code> 的 ItemsSource 是具有 <code>T:System.Collections.Specialized.INotifyCollectionChanged</code> 自訂實作的集合。</span><span class="sxs-lookup"><span data-stu-id="20779-104">The ItemsSource for a <code>T:System.Windows.Controls.Primitives.Selector</code> is a collection with a custom implementation of <code>T:System.Collections.Specialized.INotifyCollectionChanged</code>.</span></span></li><li><span data-ttu-id="20779-105">已從集合中移除選取的項目。</span><span class="sxs-lookup"><span data-stu-id="20779-105">The selected item is removed from the collection.</span></span></li><li><span data-ttu-id="20779-106"><code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code> 具有 <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> = -1 (表示未知的位置)。</span><span class="sxs-lookup"><span data-stu-id="20779-106">The <code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code> has <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> = -1 (indicating an unknown position).</span></span></li></ul><span data-ttu-id="20779-107">例外狀況的呼叫堆疊開頭為：at System.Windows.Threading.Dispatcher.VerifyAccess() at System.Windows.DependencyObject.GetValue(DependencyProperty dp) at System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject element)。在 .NET Framework 4.5 中，如果應用程式有超過一個以上的發送器執行緒，可能會發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="20779-107">The exception's callstack begins at System.Windows.Threading.Dispatcher.VerifyAccess() at System.Windows.DependencyObject.GetValue(DependencyProperty dp) at System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject element)This exception can occur in .NET Framework 4.5 if the application has more than one Dispatcher thread.</span></span> <span data-ttu-id="20779-108">在 .NET Framework 4.7 中，具有單一發送器執行緒的應用程式也可能會發生此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="20779-108">In .NET Framework 4.7 the exception can also occur in applications with a single Dispatcher thread.</span></span> <span data-ttu-id="20779-109">此問題已在 .NET Framework 4.7.1 中修正。</span><span class="sxs-lookup"><span data-stu-id="20779-109">The issue is fixed in .NET Framework 4.7.1.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="20779-110">建議</span><span class="sxs-lookup"><span data-stu-id="20779-110">Suggestion</span></span>

<span data-ttu-id="20779-111">升級至 .NET Framework 4.7.1。</span><span class="sxs-lookup"><span data-stu-id="20779-111">Upgrade to .NET Framework 4.7.1.</span></span>

| <span data-ttu-id="20779-112">名稱</span><span class="sxs-lookup"><span data-stu-id="20779-112">Name</span></span>    | <span data-ttu-id="20779-113">值</span><span class="sxs-lookup"><span data-stu-id="20779-113">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="20779-114">影響範圍</span><span class="sxs-lookup"><span data-stu-id="20779-114">Scope</span></span>   |<span data-ttu-id="20779-115">Minor</span><span class="sxs-lookup"><span data-stu-id="20779-115">Minor</span></span>|
|<span data-ttu-id="20779-116">版本</span><span class="sxs-lookup"><span data-stu-id="20779-116">Version</span></span>|<span data-ttu-id="20779-117">4.7</span><span class="sxs-lookup"><span data-stu-id="20779-117">4.7</span></span>|
|<span data-ttu-id="20779-118">類型</span><span class="sxs-lookup"><span data-stu-id="20779-118">Type</span></span>|<span data-ttu-id="20779-119">執行階段</span><span class="sxs-lookup"><span data-stu-id="20779-119">Runtime</span></span>|
