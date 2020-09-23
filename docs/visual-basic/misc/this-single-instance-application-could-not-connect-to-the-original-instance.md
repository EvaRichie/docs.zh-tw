---
title: 此單一執行個體應用程式無法連接到原始執行個體
ms.date: 07/20/2015
f1_keywords:
- vbrAppModel_SingleInstanceCantConnect
ms.assetid: 7c2c0cee-02a1-4157-be03-39d18e18408f
ms.openlocfilehash: 8e2caa158c3874d216671979430a03b11bf60066
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91095677"
---
# <a name="this-single-instance-application-could-not-connect-to-the-original-instance"></a><span data-ttu-id="35322-102">此單一執行個體應用程式無法連接到原始執行個體</span><span class="sxs-lookup"><span data-stu-id="35322-102">This single-instance application could not connect to the original instance</span></span>

<span data-ttu-id="35322-103">此單一執行個體應用程式無法連接到原始執行個體。</span><span class="sxs-lookup"><span data-stu-id="35322-103">This single-instance application could not connect to the original instance.</span></span> <span data-ttu-id="35322-104">此問題的部分可能原因如下：</span><span class="sxs-lookup"><span data-stu-id="35322-104">Some of the possible causes for this problem are as follows:</span></span>  
  
- <span data-ttu-id="35322-105">原始執行個體停止回應。</span><span class="sxs-lookup"><span data-stu-id="35322-105">The original instance stopped responding.</span></span>  
  
- <span data-ttu-id="35322-106">應用程式沒有建立核心物件的權限。</span><span class="sxs-lookup"><span data-stu-id="35322-106">The application does not have permissions to create kernel objects.</span></span> <span data-ttu-id="35322-107">如需核心物件的詳細資訊，請參閱 [mutex](../../standard/threading/mutexes.md)。</span><span class="sxs-lookup"><span data-stu-id="35322-107">For more information about kernel objects, see [Mutexes](../../standard/threading/mutexes.md).</span></span>  
  
     <span data-ttu-id="35322-108">核心物件的主檔名 (Base Name) 是由連接組件的 GUID、主要版本號碼，以及次要版本號碼所組成。</span><span class="sxs-lookup"><span data-stu-id="35322-108">The base name for the kernel objects comes from concatenating the assembly's GUID, major version number, and minor version number.</span></span> <span data-ttu-id="35322-109">例如，基底名稱可能是 `3639f15d-9547-43da-8145-60da347829915.1`。</span><span class="sxs-lookup"><span data-stu-id="35322-109">For example, the base name could be `3639f15d-9547-43da-8145-60da347829915.1`.</span></span>  
  
## <a name="to-correct-this-error-when-developing-the-application"></a><span data-ttu-id="35322-110">在開發應用程式時更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="35322-110">To correct this error when developing the application</span></span>  
  
1. <span data-ttu-id="35322-111">檢查應用程式並未進入沒有回應的狀態。</span><span class="sxs-lookup"><span data-stu-id="35322-111">Check that the application does not go into an unresponsive state.</span></span>  
  
2. <span data-ttu-id="35322-112">檢查應用程式有足夠的權限可建立核心物件。</span><span class="sxs-lookup"><span data-stu-id="35322-112">Check that the application has sufficient permissions to create kernel objects.</span></span>  
  
3. <span data-ttu-id="35322-113">重新啟動應用程式的原始執行個體。</span><span class="sxs-lookup"><span data-stu-id="35322-113">Restart the original instance of the application.</span></span>  
  
4. <span data-ttu-id="35322-114">重新啟動電腦，以針對連接到原始執行個體應用程式所需的資源，清除可能正在使用它的任何處理序。</span><span class="sxs-lookup"><span data-stu-id="35322-114">Restart the computer to clear any process that may be using the resource that is required to connect to the original instance application.</span></span>  
  
5. <span data-ttu-id="35322-115">記下錯誤發生時的情況，並致電 Microsoft 產品支援服務。</span><span class="sxs-lookup"><span data-stu-id="35322-115">Note the circumstances under which the error occurred, and telephone Microsoft Product Support Services.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="35322-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="35322-116">See also</span></span>

- [<span data-ttu-id="35322-117">偵錯工具基礎</span><span class="sxs-lookup"><span data-stu-id="35322-117">Debugger Basics</span></span>](/visualstudio/debugger/debugger-feature-tour)
