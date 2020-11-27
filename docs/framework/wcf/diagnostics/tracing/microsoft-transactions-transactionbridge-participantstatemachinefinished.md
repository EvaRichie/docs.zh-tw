---
title: Microsoft.Transactions.TransactionBridge.ParticipantStateMachineFinished
ms.date: 03/30/2017
ms.assetid: 54b677f7-03ad-40f2-9c5d-297a8ad9bf90
ms.openlocfilehash: bd6c9124e6346437e2bb35df620e00bad13b60f3
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96258942"
---
# <a name="microsofttransactionstransactionbridgeparticipantstatemachinefinished"></a><span data-ttu-id="a9884-102">Microsoft.Transactions.TransactionBridge.ParticipantStateMachineFinished</span><span class="sxs-lookup"><span data-stu-id="a9884-102">Microsoft.Transactions.TransactionBridge.ParticipantStateMachineFinished</span></span>

<span data-ttu-id="a9884-103">參與者登記的狀態電腦已進入完成狀態。</span><span class="sxs-lookup"><span data-stu-id="a9884-103">The state machine for a participant enlistment entered the finished state.</span></span>  
  
## <a name="description"></a><span data-ttu-id="a9884-104">描述</span><span class="sxs-lookup"><span data-stu-id="a9884-104">Description</span></span>  

 <span data-ttu-id="a9884-105">當下層參與者登記的 2pc 程序已完成時，即進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="a9884-105">Traced when a subordinate participant enlistment has completed 2pc processing.</span></span> <span data-ttu-id="a9884-106">登記的結果可以是「已認可」或「已中止」。</span><span class="sxs-lookup"><span data-stu-id="a9884-106">The outcome for the enlistment can be Committed or Aborted.</span></span> <span data-ttu-id="a9884-107">如果任何參與者在「準備」期間表決為 ReadOnly 時，也會進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="a9884-107">It is also traced if any participant votes ReadOnly during Prepare.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a9884-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9884-108">See also</span></span>

- [<span data-ttu-id="a9884-109">追蹤</span><span class="sxs-lookup"><span data-stu-id="a9884-109">Tracing</span></span>](index.md)
- [<span data-ttu-id="a9884-110">使用追蹤來疑難排解應用程式</span><span class="sxs-lookup"><span data-stu-id="a9884-110">Using Tracing to Troubleshoot Your Application</span></span>](using-tracing-to-troubleshoot-your-application.md)
- [<span data-ttu-id="a9884-111">系統管理與診斷</span><span class="sxs-lookup"><span data-stu-id="a9884-111">Administration and Diagnostics</span></span>](../index.md)
