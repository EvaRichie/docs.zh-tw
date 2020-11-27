---
title: 消費者入門 >tutorial2
description: 本文將開始一系列的教學課程，介紹如何 Windows Workflow Foundation 應用程式進行程式設計。
ms.date: 03/30/2017
helpviewer_keywords:
- WF [WF], getting started
- Windows Workflow Foundation [WF], getting started
ms.assetid: c2d3585f-6b1a-4d4f-9865-bd7cd31c5d42
ms.openlocfilehash: e9856320faa82becf12dda04d02f6f1c08081feb
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293594"
---
# <a name="getting-started-tutorial"></a>快速入門教學課程

本節包含一組逐步解說主題，會介紹如何) 應用程式 (WF 進行程式設計 Windows Workflow Foundation。 您可以遵循這些主題的程序進行，建置一個數字猜測遊戲應用程式。 教學課程中的第一個主題會引導您透過步驟來建立工作流程所需的自訂活動。 在第二個主題中，這些活動會隨著內建工作流程活動組裝至流程圖工作流程。 在第三個主題中，會設定主應用程式執行工作流程，並在最後一個主題中介紹持續性。 這個程序中的每一個步驟都與之前的步驟息息相關，因此建議您最好依照順序完成。  
  
## <a name="in-this-section"></a>本節內容  

 [作法：建立活動](how-to-create-an-activity.md)  
 描述如何建立衍生自 <xref:System.Activities.NativeActivity%601> 的自訂活動，以及如何使用活動設計工具，將這個活動連同內建活動撰寫成複合活動。  
  
 [作法：建立工作流程](how-to-create-a-workflow.md)  
 說明如何利用內建活動和前述教學課程的自訂活動，來建立流程圖、循序和狀態機器工作流程。  
  
 [作法：執行工作流程](how-to-run-a-workflow.md)  
 描述如何從主機環境中叫用工作流程，在工作流程中來回傳遞資料，以及如何恢復書籤。  
  
 [作法：建立及執行長時間執行的工作流程](how-to-create-and-run-a-long-running-workflow.md)  
 說明如何將持續性加入工作流程應用程式。  
  
 [作法：建立自訂追蹤參與者](how-to-create-a-custom-tracking-participant.md)  
 說明如何建立自訂的追蹤參與者和追蹤設定檔。  
  
 [作法：並存裝載工作流程的多個版本](how-to-host-multiple-versions-of-a-workflow-side-by-side.md)  
 描述如何使用 `WorkflowIdentity` 裝載工作流程並存的多個版本。  
  
 [作法：更新執行中工作流程執行個體的定義](how-to-update-the-definition-of-a-running-workflow-instance.md)  
 說明如何使用動態更新來修改執行中的工作流程執行個體。  
  
## <a name="see-also"></a>另請參閱

- [Windows Workflow Foundation 程式設計](programming.md)
