---
title: 疑難排解：對 Windows 服務進行偵錯
description: 開始進行 Windows 服務的調試。 當您對 Windows 服務應用程式進行偵錯時，您的服務會與 Windows Service Manager 互動。
ms.date: 03/30/2017
helpviewer_keywords:
- debugging Windows Service applications
- debugging [Visual Studio], Windows services
- troubleshooting service applications
- services, troubleshooting
- troubleshooting debugging, Windows Services
- Windows Service applications, debugging
- services, debugging
- Windows Service applications, troubleshooting
ms.assetid: cf859d4c-f04c-4cb7-81e3-bc7de8bea190
ms.openlocfilehash: 2c1180ef8e3e44c50f10a263d86dcae830d9cd0e
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96270389"
---
# <a name="troubleshooting-debugging-windows-services"></a>疑難排解：對 Windows 服務進行偵錯

當您對 Windows 服務應用程式進行偵錯時，您的服務會與 **Windows Service Manager** 互動。 **Service Manager** 會藉由呼叫 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法來啟動您的服務，然後等候 30 秒以待 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法傳回。 如果該方法此時並未傳回，管理員就會顯示錯誤，指出無法啟動服務。  
  
 當您以[如何：偵錯 Windows 服務應用程式](how-to-debug-windows-service-applications.md)中所述方式來對 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法進行偵錯時，一定會注意到這段 30 秒的期間。 如果您在 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法中放置中斷點，並且未在 30 秒內逐步執行它，則管理員將不會啟動服務。  
  
## <a name="see-also"></a>另請參閱

- [作法：偵錯 Windows 服務應用程式](how-to-debug-windows-service-applications.md)
- [Windows 服務應用程式簡介](introduction-to-windows-service-applications.md)
