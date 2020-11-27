---
title: 設定活動驗證
ms.date: 03/30/2017
ms.assetid: 25a4eccb-b8fc-4857-a01d-2683b6341219
ms.openlocfilehash: c3e10fc096b16ef2cf7a6c7533ac9bad8c5ec205
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96288953"
---
# <a name="configuring-activity-validation"></a>設定活動驗證

活動驗證可讓活動作者和使用者在執行前，先在活動的組態中識別及報告錯誤。 Windows Workflow Foundation (WF) 提供下列三種活動驗證類型：  
  
- `RequiredArgument` 與 `OverloadGroup` 屬性。  
  
- 命令式的程式碼式驗證。  
  
- 宣告式條件約束。  
  
 指出活動需要特定引數的 `RequiredArgument` 和 `OverloadGroup` 屬性。 命令式的程式碼式驗證提供讓活動自我驗證的簡易方式，而宣告式條件約束則可用於驗證活動及活動與包含該活動之工作流程的關聯性。 如果未根據驗證需求正確設定活動，就會傳回驗證錯誤與警告。 如果包含該活動的工作流程是使用工作流程設計工具建立的，則任何驗證錯誤與警告都會顯示在設計工具中。 如果工作流程是在工作流程設計工具以外建立的，則會在叫用該工作流程時傳回所有驗證錯誤。 無論工作流程的建立方式為何，含驗證錯誤的工作流程永遠不能執行。 本節提供這些活動驗證類型與活動驗證叫用方式的概觀。  
  
## <a name="in-this-section"></a>本節內容  

 [必要引數與多載群組](required-arguments-and-overload-groups.md)  
 描述如何使用 `RequiredArgument`和 `OverloadGroup` 屬性提供驗證。  
  
 [命令式的程式碼式驗證](imperative-code-based-validation.md)  
 描述如何將程式碼式的驗證用於 <xref:System.Activities.CodeActivity> 和 <xref:System.Activities.NativeActivity> 式的活動。  
  
 [宣告式條件約束](declarative-constraints.md)  
 描述如何使用宣告式條件約束提供複雜活動驗證。  
  
 [叫用活動驗證](invoking-activity-validation.md)  
 討論自動叫用活動驗證的時機，以及明確叫用驗證的方式。  
  
## <a name="reference"></a>參考  
  
## <a name="related-sections"></a>相關章節
