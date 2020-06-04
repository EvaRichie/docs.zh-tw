---
title: 屬性或方法呼叫不能包含 private 物件的參考，也不可以當做引數或傳回值
ms.date: 07/20/2015
f1_keywords:
- vbrID98
ms.assetid: 059b43e1-202d-4fa2-806b-7bad63c1e7ca
ms.openlocfilehash: 36c71cdb345d0fdc0da2b58865a1f11956bcb944
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409968"
---
# <a name="a-property-or-method-call-cannot-include-a-reference-to-a-private-object-either-as-an-argument-or-as-a-return-value"></a><span data-ttu-id="df727-102">屬性或方法呼叫不能包含 private 物件的參考，也不可以當做引數或傳回值</span><span class="sxs-lookup"><span data-stu-id="df727-102">A property or method call cannot include a reference to a private object, either as an argument or as a return value</span></span>

<span data-ttu-id="df727-103">可能導致本錯誤的原因包括：</span><span class="sxs-lookup"><span data-stu-id="df727-103">Among the possible causes of this error are:</span></span>  
  
- <span data-ttu-id="df727-104">用戶端已叫用跨處理序元件的屬性或方法，並嘗試將 private 物件的參考傳遞為其中一個引數。</span><span class="sxs-lookup"><span data-stu-id="df727-104">A client invoked a property or method of an out-of-process component and attempted to pass a reference to a private object as one of the arguments.</span></span>  
  
- <span data-ttu-id="df727-105">跨處理序元件已在其用戶端上叫用回撥方法，並嘗試傳遞 private 物件的參考。</span><span class="sxs-lookup"><span data-stu-id="df727-105">An out-of-process component invoked a call-back method on its client and attempted to pass a reference to a private object.</span></span>  
  
- <span data-ttu-id="df727-106">跨處理序元件已嘗試將 private 物件的參考傳遞為所引發事件的引數。</span><span class="sxs-lookup"><span data-stu-id="df727-106">An out-of-process component attempted to pass a reference to a private object as an argument of an event it was raising.</span></span>  
  
- <span data-ttu-id="df727-107">用戶端已嘗試將 private 物件參考指派給所處理事件的 `ByRef` 引數。</span><span class="sxs-lookup"><span data-stu-id="df727-107">A client attempted to assign a private object reference to a `ByRef` argument of an event it was handling.</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="df727-108">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="df727-108">To correct this error</span></span>  
  
1. <span data-ttu-id="df727-109">移除參考。</span><span class="sxs-lookup"><span data-stu-id="df727-109">Remove the reference.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="df727-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="df727-110">See also</span></span>

- [<span data-ttu-id="df727-111">私用</span><span class="sxs-lookup"><span data-stu-id="df727-111">Private</span></span>](../modifiers/private.md)
