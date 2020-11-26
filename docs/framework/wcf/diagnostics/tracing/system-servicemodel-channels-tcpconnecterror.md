---
title: System.ServiceModel.Channels.TcpConnectError
ms.date: 03/30/2017
ms.assetid: 22d93797-072e-405d-a3e0-5c519ddf290b
ms.openlocfilehash: 5efc14109fb2ad2d4444baae0d9423694e0f5b25
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96246806"
---
# <a name="systemservicemodelchannelstcpconnecterror"></a>System.ServiceModel.Channels.TcpConnectError

TCP 連線作業失敗。  
  
## <a name="description"></a>描述  

 這個警告層級追蹤表示無法連接到 TCP 端點。 如果位於指定之 IP 位址和連接埠的遠端端點沒有回應，就會發生這個問題。 如果後續對其他有效 IP 位址 (例如 IPv4 或 IPv6 位址，或其他代表指定主機名稱的 IP 位址) 的連線嘗試成功的話，則會忽略這個追蹤。 這個追內的例外狀況會顯示有關錯誤的其他資訊。  
  
## <a name="see-also"></a>另請參閱

- [追蹤](index.md)
- [使用追蹤來疑難排解應用程式](using-tracing-to-troubleshoot-your-application.md)
- [系統管理與診斷](../index.md)
