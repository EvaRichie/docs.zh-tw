---
title: 網際網路通訊協定第 6 版
description: 瞭解 IPv6 通訊協定，以及它與 IPv4 的不同之處。 .NET Framework 應用程式支援 IPv6，但可能需要設定。
ms.date: 03/30/2017
helpviewer_keywords:
- IPv6, improvements
- IPv4
- IPv6
- Internet Protocol version 6, improvements
- Internet Protocol version 6
ms.assetid: e6fa8ebd-010a-4c48-a5ec-a5102c53c06f
ms.openlocfilehash: dd8b0b26e449fba7479d2678aff25ed49e721a90
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502388"
---
# <a name="internet-protocol-version-6"></a>網際網路通訊協定第 6 版
網際網路通訊協定第 6 版 (IPv6) 是網際網路網路層級的新標準通訊協定套件。 IPv6 旨在解決網際網路通訊協定當前版本 (稱為 IPv4) 有關位址耗竭、安全性、自動組態和擴充性等等的許多問題。 IPv6 展開網際網路的功能，以啟用新種類的應用程式，包括點對點與行動應用程式。 以下是目前 IPv4 通訊協定的主要問題：  
  
- 快速消耗位址空間。  
  
     這導致使用網路位址轉譯器 (NAT) 將多個私人位址對應到單一公用 IP 位址。 這項機制引起的主要問題是處理額外負荷以及缺乏端對端連線。  
  
- 缺少階層式支援。  
  
     因為其固有的預先定義類別組織，IPv4 缺少真正的階層式支援。 不可能以真正對應網路拓撲的方式來建立 IP 位址的結構。 此一重大的設計缺陷創造了對大型路由表的需求，以將 IPv4 封包傳遞至網際網路上的任何位置。  
  
- 複雜的網路組態。  
  
     使用 IPv4，必須以靜態方式或使用 DHCP 等組態通訊協定指派位址。 理想的情況下，主機可能不必依賴 DHCP 基礎結構的管理。 相反地，它們可以根據所在的網路區段自行設定。  
  
- 缺少內建的驗證和機密性。  
  
     IPv4 不需要任何提供交換資料驗證或加密之機制的支援。 這會隨著 IPv6 變更。 網際網路通訊協定安全性 (IPSec) 是 IPv6 支援需求。  
  
 新的通訊協定套件必須滿足下列基本需求：  
  
- 低額外負荷的大規模路由和定址。  
  
- 各種連線情況的自動組態。  
  
- 內建的驗證和機密性。  
  
 如需詳細資訊，請參閱 [IPv6 定址](ipv6-addressing.md)、[IPv6 路由](ipv6-routing.md)、[IPv6 自動組態](ipv6-auto-configuration.md)、[啟用和停用 IPv6](enabling-and-disabling-ipv6.md) 以及[如何：修改電腦組態檔以啟用 IPv6 支援](how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)。  
  
## <a name="references"></a>參考資料  
 以下是您可在[網際網路工程任務推動小組 (IETF)](https://www.ietf.org/) 網站中找到的精選 RFC 文件：  
  
- RFC 1287，前進未來網際網路架構。  
  
- RFC 1454，下一版 IP 的建議比較。  
  
- RFC 2373，IP 第 6 版定址架構。  
  
- RFC 2374，IPv6 彙總全域單點傳播位址格式。  
  
 您也可以在 [IP 版本 6 (IPv6)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379498%28v=ws.10%29) 找到 IPv6 的相關資訊。  
  
## <a name="see-also"></a>另請參閱

- [IPv6 通訊端範例](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms180981%28v=vs.85%29)
- [網路程式設計範例](network-programming-samples.md)
- [通訊端](sockets.md)
