---
title: 如何：在執行階段使用 C# 撰寫使用者設定
description: '瞭解如何在執行時間使用 c # 撰寫設定，方法是藉由呼叫 Save 方法，藉由保存應用程式會話之間的設定變更。'
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], run time
- application settings [Windows Forms], writing user settings
- application settings [Windows Forms], C#
ms.assetid: 9d061c7d-b33b-470f-a36d-edccb1d6f9a3
ms.openlocfilehash: 6154ff1b92d6c2d4c788299e59eb8f73e6b69c4b
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904321"
---
# <a name="how-to-write-user-settings-at-run-time-with-c"></a><span data-ttu-id="e3cc1-103">如何：在執行時間使用 C 撰寫使用者設定\#</span><span class="sxs-lookup"><span data-stu-id="e3cc1-103">How To: Write User Settings at Run Time with C\#</span></span>

<span data-ttu-id="e3cc1-104">應用程式範圍的設定是唯讀的，並只能在設計階段變更，或藉由更改應用程式工作階段之間的 .config 檔案變更。</span><span class="sxs-lookup"><span data-stu-id="e3cc1-104">Settings that are application-scoped are read-only, and can only be changed at design time or by altering the .config file in between application sessions.</span></span> <span data-ttu-id="e3cc1-105">不過，使用者範圍的設定可以在執行階段撰寫，就如同您變更任何屬性值一樣。</span><span class="sxs-lookup"><span data-stu-id="e3cc1-105">Settings that are user-scoped, however, can be written at run time just as you would change any property value.</span></span> <span data-ttu-id="e3cc1-106">新的值在應用程式工作階段期間保存。</span><span class="sxs-lookup"><span data-stu-id="e3cc1-106">The new value persists for the duration of the application session.</span></span> <span data-ttu-id="e3cc1-107">您可以藉由呼叫 Save 方法在應用程式工作階段之間保存設定的變更。</span><span class="sxs-lookup"><span data-stu-id="e3cc1-107">You can persist the changes to the settings between application sessions by calling the Save method.</span></span>  
  
## <a name="how-to-write-and-persist-user-settings-at-run-time-with-c"></a><span data-ttu-id="e3cc1-108">如何：在執行時間使用 C 撰寫和保存使用者設定\#</span><span class="sxs-lookup"><span data-stu-id="e3cc1-108">How To: Write and Persist User Settings at Run Time with C\#</span></span>
  
1. <span data-ttu-id="e3cc1-109">存取設定，並指派新值，如本範例所示：</span><span class="sxs-lookup"><span data-stu-id="e3cc1-109">Access the setting and assign it a new value as shown in this example:</span></span>  
  
   ```csharp
   Properties.Settings.Default.myColor = Color.AliceBlue;  
   ```  
  
2. <span data-ttu-id="e3cc1-110">如果您想要在應用程式工作階段之間保存變更的設定，請呼叫 Save 方法，如本範例所示：</span><span class="sxs-lookup"><span data-stu-id="e3cc1-110">If you want to persist the changes to the settings between application sessions, call the Save method as shown in this example:</span></span>  
  
    ```csharp
    Properties.Settings.Default.Save();  
    ```  
  
<span data-ttu-id="e3cc1-111">使用者設定會儲存在使用者的本機隱藏應用程式儲存資料夾的子資料夾內。</span><span class="sxs-lookup"><span data-stu-id="e3cc1-111">User settings are saved in a file within a subfolder of the user’s local hidden application data folder.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e3cc1-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3cc1-112">See also</span></span>

- [<span data-ttu-id="e3cc1-113">使用應用程式設定和使用者設定</span><span class="sxs-lookup"><span data-stu-id="e3cc1-113">Using Application Settings and User Settings</span></span>](using-application-settings-and-user-settings.md)
- [<span data-ttu-id="e3cc1-114">如何：在執行階段使用 C# 讀取設定</span><span class="sxs-lookup"><span data-stu-id="e3cc1-114">How To: Read Settings at Run Time With C#</span></span>](how-to-read-settings-at-run-time-with-csharp.md)
- [<span data-ttu-id="e3cc1-115">應用程式設定總覽</span><span class="sxs-lookup"><span data-stu-id="e3cc1-115">Application Settings Overview</span></span>](application-settings-overview.md)
