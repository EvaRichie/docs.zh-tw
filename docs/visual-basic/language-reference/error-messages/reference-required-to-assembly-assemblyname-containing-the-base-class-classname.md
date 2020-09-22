---
title: 需要組件 '<assemblyname>' (包含基底類別 '<classname>') 的參考
ms.date: 07/20/2015
f1_keywords:
- bc30007
- vbc30007
helpviewer_keywords:
- BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
ms.openlocfilehash: 07c09d0dfcb374b974fbda9099c4e85d6d054753
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90870909"
---
# <a name="reference-required-to-assembly-assemblyname-containing-the-base-class-classname"></a><span data-ttu-id="9391b-102">需要組件 '\<assemblyname>' (包含基底類別 '\<classname>') 的參考</span><span class="sxs-lookup"><span data-stu-id="9391b-102">Reference required to assembly '\<assemblyname>' containing the base class '\<classname>'</span></span>

<span data-ttu-id="9391b-103">需要元件 ' ' （ \<assemblyname> 包含基類 ' '）的參考 \<classname> 。</span><span class="sxs-lookup"><span data-stu-id="9391b-103">Reference required to assembly '\<assemblyname>' containing the base class '\<classname>'.</span></span> <span data-ttu-id="9391b-104">請在專案中加入一個參考。</span><span class="sxs-lookup"><span data-stu-id="9391b-104">Add one to your project.</span></span>  
  
 <span data-ttu-id="9391b-105">此類別是在專案中未直接參考的動態連結程式庫 (DLL) 或組件中所定義。</span><span class="sxs-lookup"><span data-stu-id="9391b-105">The class is defined in a dynamic-link library (DLL) or assembly that is not directly referenced in your project.</span></span> <span data-ttu-id="9391b-106">Visual Basic 編譯器需要參考，以避免在多個 DLL 或元件中定義類別的情況下不清楚。</span><span class="sxs-lookup"><span data-stu-id="9391b-106">The Visual Basic compiler requires a reference to avoid ambiguity in case the class is defined in more than one DLL or assembly.</span></span>  
  
 <span data-ttu-id="9391b-107">**錯誤 ID︰** BC30007</span><span class="sxs-lookup"><span data-stu-id="9391b-107">**Error ID:** BC30007</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="9391b-108">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="9391b-108">To correct this error</span></span>  
  
- <span data-ttu-id="9391b-109">在您的專案參考中包含未參考之 DLL 或組件的名稱。</span><span class="sxs-lookup"><span data-stu-id="9391b-109">Include the name of the unreferenced DLL or assembly in your project references.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9391b-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9391b-110">See also</span></span>

- [<span data-ttu-id="9391b-111">管理專案中的參考</span><span class="sxs-lookup"><span data-stu-id="9391b-111">Managing references in a project</span></span>](/visualstudio/ide/managing-references-in-a-project)
- [<span data-ttu-id="9391b-112">針對中斷參考進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="9391b-112">Troubleshooting Broken References</span></span>](/visualstudio/ide/troubleshooting-broken-references)
