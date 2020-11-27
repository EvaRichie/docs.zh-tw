---
title: 設定 Net.TCP Port Sharing Service
ms.date: 03/30/2017
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
ms.openlocfilehash: 854cd7d26e26ee340d577b1bfd890f750e581a38
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96284143"
---
# <a name="configuring-the-nettcp-port-sharing-service"></a><span data-ttu-id="98ef6-102">設定 Net.TCP Port Sharing Service</span><span class="sxs-lookup"><span data-stu-id="98ef6-102">Configuring the Net.TCP Port Sharing Service</span></span>

<span data-ttu-id="98ef6-103">使用 Net.TCP 傳輸的自我裝載服務可以控制好幾項進階設定，例如 `ListenBacklog` 和 `MaxPendingAccepts`，這些設定掌管網路通訊時使用的基礎 TCP 通訊端行為。</span><span class="sxs-lookup"><span data-stu-id="98ef6-103">Self-hosted services that use the Net.TCP transport can control several advanced settings, such as `ListenBacklog` and `MaxPendingAccepts`, which govern the behavior of the underlying TCP socket used for network communication.</span></span> <span data-ttu-id="98ef6-104">但是，如果傳輸繫結已經停用連接埠共用 (預設為啟用)，則每個通訊端的這些設定只能套用在繫結層級中。</span><span class="sxs-lookup"><span data-stu-id="98ef6-104">However, these settings for each socket only apply at the binding level if the transport binding has disabled port sharing, which is enabled by default.</span></span>  
  
 <span data-ttu-id="98ef6-105">當 net.tcp 繫結啟用了連接埠共用 (在傳輸繫結項目上設定 `portSharingEnabled =true`)，就會隱含地允許外部處理序 (亦即 SMSvcHost.exe，可裝載 Net.TCP Port Sharing Service) 為自己管理 TCP 通訊端。</span><span class="sxs-lookup"><span data-stu-id="98ef6-105">When a net.tcp binding enables port sharing (by setting `portSharingEnabled =true` on the transport binding element), it implicitly allows an external process (namely the SMSvcHost.exe, which hosts the Net.TCP Port Sharing Service) to manage the TCP socket on its behalf.</span></span> <span data-ttu-id="98ef6-106">例如，使用 TCP 時請指定：</span><span class="sxs-lookup"><span data-stu-id="98ef6-106">For example, when using TCP, specify:</span></span>  
  
```xml  
<tcpTransport portSharingEnabled="true"  />  
```  
  
 <span data-ttu-id="98ef6-107">以這種方式進行設定時，任何在服務的傳輸繫結項目上指定的通訊端設定都會被忽略，且會優先使用 SMSvcHost.exe 所指定的通訊端設定。</span><span class="sxs-lookup"><span data-stu-id="98ef6-107">When configured in this way, any socket settings specified on the service's transport binding element are ignored in favor of the socket settings specified by SMSvcHost.exe.</span></span>  
  
 <span data-ttu-id="98ef6-108">若要設定 SMSvcHost.exe，請建立名為 SmSvcHost.exe.config 的 XML 組態檔並將其置放在與 SMSvcHost.exe 可執行檔相同的實體目錄中 (例如，C:\Windows\Microsoft.NET\Framework\v4.5)。</span><span class="sxs-lookup"><span data-stu-id="98ef6-108">To configure the SMSvcHost.exe, create an XML configuration file named SmSvcHost.exe.config and place it in the same physical directory as the SMSvcHost.exe executable (for example, C:\Windows\Microsoft.NET\Framework\v4.5).</span></span>  
  
 <span data-ttu-id="98ef6-109">下列範例示範針對所有明確陳述之可設定值使用預設值的 SMSvcHost.exe.config 範例。</span><span class="sxs-lookup"><span data-stu-id="98ef6-109">The following example illustrates a sample SMSvcHost.exe.config, with the default settings for all configurable values stated explicitly.</span></span>  
  
```xml  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!-- 16 * # of processors -->  
          maxPendingAccepts="4"<!-- 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!-- 30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
    </system.serviceModel.activation>
</configuration>  
```  
  
## <a name="when-to-modify-smsvchostexeconfig"></a><span data-ttu-id="98ef6-110">需要修改 SMSvcHost.exe.config 時</span><span class="sxs-lookup"><span data-stu-id="98ef6-110">When to Modify SMSvcHost.exe.config</span></span>  

 <span data-ttu-id="98ef6-111">一般來說，修改 SMSvcHost.exe.config 檔時需要特別小心，因為此檔中指定的任何組態設定都會影響電腦上使用 Net.TCP Port Sharing Service 的所有服務。</span><span class="sxs-lookup"><span data-stu-id="98ef6-111">In general, care should be taken when modifying the contents of the SMSvcHost.exe.config file, because any configuration settings specified in this file affect all of the services on a computer that uses the Net.TCP Port Sharing Service.</span></span> <span data-ttu-id="98ef6-112">這包括 Windows Vista 上的應用程式，這些應用程式會使用 Windows Process Activation Service 的 TCP 啟動功能， () 。</span><span class="sxs-lookup"><span data-stu-id="98ef6-112">This includes applications on Windows Vista that use the TCP Activation features of the Windows Process Activation Service (WAS).</span></span>  
  
 <span data-ttu-id="98ef6-113">但是，有時候您可能需要變更 Net.TCP Port Sharing Service 的預設組態。</span><span class="sxs-lookup"><span data-stu-id="98ef6-113">However, sometimes you may need to change the default configuration for the Net.TCP Port Sharing Service.</span></span> <span data-ttu-id="98ef6-114">例如，`maxPendingAccepts` 的預設值為 4 \* 處理器數量。</span><span class="sxs-lookup"><span data-stu-id="98ef6-114">For example, the default value for `maxPendingAccepts` is 4 \* number of processors.</span></span> <span data-ttu-id="98ef6-115">裝載大量使用連接埠共用服務的伺服器，可以增加此值來達到最大的輸送量。</span><span class="sxs-lookup"><span data-stu-id="98ef6-115">Servers that host a large number of services that use port sharing may increase this value to achieve maximum throughput.</span></span> <span data-ttu-id="98ef6-116">`maxPendingConnections` 的預設值為 100。</span><span class="sxs-lookup"><span data-stu-id="98ef6-116">The default value for `maxPendingConnections` is 100.</span></span> <span data-ttu-id="98ef6-117">如果有多個並行用戶端都在呼叫服務，而服務正在卸除用戶端連接時，您也應該考慮增加這個值。</span><span class="sxs-lookup"><span data-stu-id="98ef6-117">You should consider increasing this value also if there are multiple concurrent clients calling the service and the service is dropping client connections.</span></span>  
  
 <span data-ttu-id="98ef6-118">SMSvcHost.exe.config 同時包含一些可能會用到連接埠共用服務的處理序身分識別資訊。</span><span class="sxs-lookup"><span data-stu-id="98ef6-118">SMSvcHost.exe.config also contains information about the process identities that may make use of the port sharing service.</span></span> <span data-ttu-id="98ef6-119">當處理序連接至連接埠共用服務以運用共用的 TCP 連接埠時，會將正在連接的處理序之處理序身分識別與允許使用連接埠共用服務的身分識別清單進行比對。</span><span class="sxs-lookup"><span data-stu-id="98ef6-119">When a process connects to the port sharing service to make use of a shared TCP port, the process identity of the connecting process is checked against a list of identities that are permitted to make use of the port sharing service.</span></span> <span data-ttu-id="98ef6-120">這些身分識別會在 SMSvcHost.exe.config 檔的區段中指定為安全識別碼 (Sid) \<allowAccounts> 。</span><span class="sxs-lookup"><span data-stu-id="98ef6-120">These identities are specified as security identifiers (SIDs) in the \<allowAccounts> section of the SMSvcHost.exe.config file.</span></span> <span data-ttu-id="98ef6-121">根據預設，系統帳戶 (LocalService、LocalSystem 和 NetworkService) 以及 Administrators 群組的成員會被授予使用連接埠共用服務的權限。</span><span class="sxs-lookup"><span data-stu-id="98ef6-121">By default, permission to use the port sharing service is granted to system accounts (LocalService, LocalSystem, and NetworkService) as well as members of the Administrators group.</span></span> <span data-ttu-id="98ef6-122">允許處理序以其他身分識別 (例如，使用者身分識別) 來執行以連接至連接埠共用服務的應用程式，必須明確地將適當的 SID 新增至 SMSvcHost.exe.config (這些變更會等到重新啟動 SMSvc.exe 處理序之後才套用)。</span><span class="sxs-lookup"><span data-stu-id="98ef6-122">Applications that allow a process running as another identity (for example, a user identity) to connect to the port sharing service must explicitly add the appropriate SID to the SMSvcHost.exe.config (these changes are not applied until the SMSvc.exe process is restarted).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="98ef6-123">在具有「使用者帳戶控制」 (UAC) 啟用的 Windows Vista 系統上，本機使用者需要較高的許可權，即使其帳戶是 Administrators 群組的成員也一樣。</span><span class="sxs-lookup"><span data-stu-id="98ef6-123">On Windows Vista systems with User Account Control (UAC) enabled, local users require elevated permissions even if their account is a member of the Administrators group.</span></span> <span data-ttu-id="98ef6-124">若要允許這些使用者在不提高許可權的情況下使用埠共用服務，使用者的 SID (或使用者所屬群組的 SID) 必須明確地新增到 \<allowAccounts> SMSvcHost.exe.config 的區段。</span><span class="sxs-lookup"><span data-stu-id="98ef6-124">To allow these users to make use of the port sharing service without elevation, the user's SID (or the SID of a group in which the user is a member) must be explicitly added to the \<allowAccounts> section of SMSvcHost.exe.config.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="98ef6-125">預設的 SMSvcHost.exe.config 檔案會指定自訂 `etwProviderId` 來防止 SMSvcHost.exe 追蹤干擾服務追蹤。</span><span class="sxs-lookup"><span data-stu-id="98ef6-125">The default SMSvcHost.exe.config file specifies a custom `etwProviderId` to prevent SMSvcHost.exe tracing from interfering with service traces.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="98ef6-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98ef6-126">See also</span></span>

- [\<net.tcp>](../../configure-apps/file-schema/wcf/net-tcp.md)
