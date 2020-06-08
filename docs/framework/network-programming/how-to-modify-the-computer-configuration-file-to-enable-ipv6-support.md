---
title: 如何：修改電腦設定檔案以啟用 IPv6 支援
description: 瞭解如何修改電腦設定檔 machine.config，以在 .NET Framework 中啟用 IPv6 支援。
ms.date: 03/30/2017
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
ms.openlocfilehash: eb7b3665c0dbcf0edefa8c48a9e69297d7259067
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502518"
---
# <a name="how-to-modify-the-computer-configuration-file-to-enable-ipv6-support"></a><span data-ttu-id="f363a-103">如何：修改電腦設定檔案以啟用 IPv6 支援</span><span class="sxs-lookup"><span data-stu-id="f363a-103">How to: Modify the Computer Configuration File to Enable IPv6 Support</span></span>
<span data-ttu-id="f363a-104">下列程式碼範例示範如何修改電腦組態檔 *machine.config* 來啟用 IPv6 支援。</span><span class="sxs-lookup"><span data-stu-id="f363a-104">The following code example shows how to modify the computer configuration file, *machine.config*, to enable IPv6 support.</span></span> <span data-ttu-id="f363a-105">*machine.config* 檔案是儲存在 Windows 安裝目錄中的 *%Windir%\Microsoft.NET\Framework* 資料夾下。</span><span class="sxs-lookup"><span data-stu-id="f363a-105">The *machine.config* file is stored in the *%Windir%\Microsoft.NET\Framework* folder in the directory where Windows was installed.</span></span> <span data-ttu-id="f363a-106">針對電腦上安裝的每個 .NET Framework 版本， *%Windir%\Microsoft.NET\Framework*下的資料夾中有個別的*machine.config*檔案（例如*C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*）。</span><span class="sxs-lookup"><span data-stu-id="f363a-106">There is a separate *machine.config* file in the folders under *%Windir%\Microsoft.NET\Framework* for each version of the .NET Framework installed on the computer (for example, *C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config*).</span></span>  
  
 <span data-ttu-id="f363a-107">您也可以在應用程式的組態檔中進行這些設定，它的優先順序高於電腦組態檔。</span><span class="sxs-lookup"><span data-stu-id="f363a-107">These settings can also be made in the configuration file for the application, which has precedence over the computer configuration file.</span></span>  
  
 <span data-ttu-id="f363a-108">如果是 .NET Framework 1.1 版及更早版本，[已啟用 IPv6]\*\*\*\* 組態參數的值會指定 <xref:System.Net.Dns?displayProperty=nameWithType> 類別的成員是否傳回 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="f363a-108">For .NET Framework version 1.1 and earlier, the value of the **ipv6 enabled** configuration switch specifies whether members of the <xref:System.Net.Dns?displayProperty=nameWithType> class return IPv6 addresses.</span></span>  
  
 <span data-ttu-id="f363a-109">如果是 .NET Framework 2.0 版及更新版本，如果 Windows 支援 IPv6，則 <xref:System.Net.Dns?displayProperty=nameWithType> 類別的所有成員 (例如，<xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> 方法) 將會傳回含有一個限制的 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="f363a-109">For .NET Framework version 2.0 and later, if Windows supports IPv6, then all members of the <xref:System.Net.Dns?displayProperty=nameWithType> class (for example, the <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=nameWithType> method), will return IPv6 addresses with one limitation.</span></span> <span data-ttu-id="f363a-110"><xref:System.Net.Dns?displayProperty=nameWithType> 類別的過時成員 (例如，<xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> 方法) 會讀取並辨識組態檔中的值。</span><span class="sxs-lookup"><span data-stu-id="f363a-110">Obsolete members of the <xref:System.Net.Dns?displayProperty=nameWithType> class (for example, the <xref:System.Net.Dns.Resolve%2A?displayProperty=nameWithType> method) will read and recognize the value in the configuration file.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f363a-111">如果是 .NET Framework 2.0 版及更新版本，預設會啟用 IPv6。</span><span class="sxs-lookup"><span data-stu-id="f363a-111">For .NET Framework version 2.0 and later, IPv6 is enabled by default.</span></span> <span data-ttu-id="f363a-112">如果是 .NET Framework 1.1 版及更早版本，預設會停用 IPv6。</span><span class="sxs-lookup"><span data-stu-id="f363a-112">For .NET Framework version 1.1 and earlier, IPv6 is disabled by default.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f363a-113">範例</span><span class="sxs-lookup"><span data-stu-id="f363a-113">Example</span></span>  
  
```xml  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>
    ……………  
    </settings>  
    ………………  
</system.net>  
```  
  
## <a name="see-also"></a><span data-ttu-id="f363a-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f363a-114">See also</span></span>

- [<span data-ttu-id="f363a-115">IPv6 定址</span><span class="sxs-lookup"><span data-stu-id="f363a-115">IPv6 Addressing</span></span>](ipv6-addressing.md)
- [<span data-ttu-id="f363a-116">網路設定結構描述</span><span class="sxs-lookup"><span data-stu-id="f363a-116">Network Settings Schema</span></span>](../configure-apps/file-schema/network/index.md)
- [<span data-ttu-id="f363a-117">\<ipv6>元素（網路設定）</span><span class="sxs-lookup"><span data-stu-id="f363a-117">\<ipv6> Element (Network Settings)</span></span>](../configure-apps/file-schema/network/ipv6-element-network-settings.md)
