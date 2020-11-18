---
title: 設定狀態資料的安全性
description: 將狀態資料宣告為私用或內部變數，以限制其存取權。 這類資料仍然可以透過反映、序列化和在調試中進行存取。
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET], state data
- code security, state data
- secure coding, state data
- state data security
ms.assetid: 12671309-2877-43fe-a3df-6863507e712d
ms.openlocfilehash: 849ed993befaceda1b04becbb7fb2530c5c62a77
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94824157"
---
# <a name="securing-state-data"></a><span data-ttu-id="d086c-104">設定狀態資料的安全性</span><span class="sxs-lookup"><span data-stu-id="d086c-104">Securing State Data</span></span>

<span data-ttu-id="d086c-105">處理機密資料或執行任何種類安全性決策的應用程式需要保持該資料在自己的控制之下，而且不能允許其他潛在惡意程式碼直接存取資料。</span><span class="sxs-lookup"><span data-stu-id="d086c-105">Applications that handle sensitive data or make any kind of security decisions need to keep that data under their own control and cannot allow other potentially malicious code to access the data directly.</span></span> <span data-ttu-id="d086c-106">保護記憶體中資料的最佳方式是將資料宣告為私用或內部 (具有限制為相同組件的範圍) 變數。</span><span class="sxs-lookup"><span data-stu-id="d086c-106">The best way to protect data in memory is to declare the data as private or internal (with scope limited to the same assembly) variables.</span></span> <span data-ttu-id="d086c-107">不過，即使此資料受限於存取權，您應該要注意︰</span><span class="sxs-lookup"><span data-stu-id="d086c-107">However, even this data is subject to access you should be aware of:</span></span>  
  
- <span data-ttu-id="d086c-108">使用反映機制，可以參考您物件的高度信任程式碼可以取得和設定私用成員。</span><span class="sxs-lookup"><span data-stu-id="d086c-108">Using reflection mechanisms, highly trusted code that can reference your object can get and set private members.</span></span>  
  
- <span data-ttu-id="d086c-109">使用序列化，如果高度信任程式碼可以使用物件的序列化格式存取對應的資料，則高度信任程式碼可以有效地取得和設定私用成員。</span><span class="sxs-lookup"><span data-stu-id="d086c-109">Using serialization, highly trusted code can effectively get and set private members if it can access the corresponding data in the serialized form of the object.</span></span>  
  
- <span data-ttu-id="d086c-110">在偵錯時，可以讀取此資料。</span><span class="sxs-lookup"><span data-stu-id="d086c-110">Under debugging, this data can be read.</span></span>  
  
 <span data-ttu-id="d086c-111">請確定沒有任何您自己的方法或屬性會在無意中公開這些值。</span><span class="sxs-lookup"><span data-stu-id="d086c-111">Make sure none of your own methods or properties exposes these values unintentionally.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d086c-112">請參閱</span><span class="sxs-lookup"><span data-stu-id="d086c-112">See also</span></span>

- [<span data-ttu-id="d086c-113">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="d086c-113">Secure Coding Guidelines</span></span>](secure-coding-guidelines.md)
- [<span data-ttu-id="d086c-114">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="d086c-114">ASP.NET Core Security</span></span>](/aspnet/core/security/)
