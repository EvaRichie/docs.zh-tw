---
title: 判斷服務作業持續時間
ms.date: 03/30/2017
ms.assetid: e8a93a2c-2c20-48b3-8986-57e90e9aa908
ms.openlocfilehash: 2607efe0d469f1235ee3d43d62f5e9781681668d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254827"
---
# <a name="determining-service-operation-duration"></a>判斷服務作業持續時間

如果在 Windows Communication Foundation (WCF) 應用程式中啟用分析追蹤，您可以藉由檢查事件記錄檔，輕鬆地判斷服務作業的執行持續時間。  本主題示範如何判斷服務作業完成所需的時間。  
  
### <a name="determining-service-operation-execution-duration"></a>判斷服務作業執行持續時間  
  
1. 按一下 [ **開始**]、[ **執行**]，然後輸入來開啟事件檢視器 `eventvwr.exe` 。  
  
2. 如果您尚未啟用分析追蹤，請展開 [**應用程式及服務記錄** 檔 **]、[** **Microsoft**]、[**應用程式伺服器-應用** 程式]。 選取 [ **View**]、[ **顯示分析和調試記錄**]。 以滑鼠右鍵按一下 [ **分析** ]，然後選取 [ **啟用記錄**]。 讓 [事件檢視器] 保持開啟狀態，如此在服務作業執行之後就能檢視追蹤。  
  
3. 接下來，開啟包含服務專案的 WCF 應用程式，以及與該服務互動的用戶端專案。  您可以遵循 [消費者入門教學](../../getting-started-tutorial.md)課程來建立這類應用程式。  如果您已安裝 WCF 範例，則可以開啟 [消費者入門](../../samples/getting-started-sample.md)，其中包含在教學課程中建立的已完成專案。  
  
4. 按 **F5** 執行伺服器應用程式。 以滑鼠右鍵按一下 **用戶端** 專案，然後選取 [ **Debug**]、[ **開始新實例**]，執行用戶端應用程式。  
  
5. 在 [事件檢視器] 中，重新整理分析記錄檔並依照 [事件 ID] 排序事件。  尋找事件識別碼為 [214-OperationCompleted](214-operationcompleted.md)的事件。  這些事件將顯示已完成的作業，以及作業的持續時間。  下列事件會顯示 Add 作業的持續時間。  
  
    ```output  
    An OperationInvoker completed the call to the 'Add' method.  The method call duration was '3' ms.  
    ```
