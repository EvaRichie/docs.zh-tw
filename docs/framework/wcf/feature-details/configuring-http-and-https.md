---
title: 設定 HTTP 和 HTTPS
description: 瞭解如何設定 HTTP/HTTPS 以允許 WCF 服務和用戶端進行通訊。 使用 Netsh.exe 設定 URL 註冊和防火牆例外。
ms.date: 04/08/2019
helpviewer_keywords:
- configuring HTTP [WCF]
ms.assetid: b0c29a86-bc0c-41b3-bc1e-4eb5bb5714d4
ms.openlocfilehash: fbff78ff8e2c5c4fa73a56a3fdc15163596aa985
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245137"
---
# <a name="configuring-http-and-https"></a><span data-ttu-id="ea430-104">設定 HTTP 和 HTTPS</span><span class="sxs-lookup"><span data-stu-id="ea430-104">Configuring HTTP and HTTPS</span></span>

<span data-ttu-id="ea430-105">WCF 服務與用戶端可以透過 HTTP 和 HTTPS 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="ea430-105">WCF services and clients can communicate over HTTP and HTTPS.</span></span> <span data-ttu-id="ea430-106">HTTP/HTTPS 設定是使用 Internet Information Services (IIS)，或使用命令列工具設定。</span><span class="sxs-lookup"><span data-stu-id="ea430-106">The HTTP/HTTPS settings are configured by using Internet Information Services (IIS) or through the use of a command-line tool.</span></span> <span data-ttu-id="ea430-107">在 IIS HTTP 或 HTTPS 之下裝載 WCF 服務時，設定可以在 IIS (使用 inetmgr.exe 工具) 內進行。</span><span class="sxs-lookup"><span data-stu-id="ea430-107">When a WCF service is hosted under IIS HTTP or HTTPS settings can be configured within IIS (using the inetmgr.exe tool).</span></span> <span data-ttu-id="ea430-108">如果是自我裝載的 WCF 服務，可以使用命令列工具設定 HTTP 或 HTTPS 設定。</span><span class="sxs-lookup"><span data-stu-id="ea430-108">If a WCF service is self-hosted, HTTP or HTTPS settings are configured by using a command-line tool.</span></span>

<span data-ttu-id="ea430-109">您至少要設定 URL 註冊，並為您的服務將使用的 URL 新增防火牆例外。</span><span class="sxs-lookup"><span data-stu-id="ea430-109">At a minimum, you want to configure a URL registration and add a Firewall exception for the URL your service will be using.</span></span> <span data-ttu-id="ea430-110">您可以使用 Netsh.exe 工具來設定這些設定。</span><span class="sxs-lookup"><span data-stu-id="ea430-110">You can configure these settings with the Netsh.exe tool.</span></span>

## <a name="configuring-namespace-reservations"></a><span data-ttu-id="ea430-111">設定命名空間保留</span><span class="sxs-lookup"><span data-stu-id="ea430-111">Configuring namespace reservations</span></span>

<span data-ttu-id="ea430-112">命名空間保留區會將一部分 HTTP URL 命名空間的權限指派給特定的使用者群組。</span><span class="sxs-lookup"><span data-stu-id="ea430-112">Namespace reservation assigns the rights for a portion of the HTTP URL namespace to a particular group of users.</span></span> <span data-ttu-id="ea430-113">保留區會授予這些使用者建立服務的權限，以接聽那一部分的命名空間。</span><span class="sxs-lookup"><span data-stu-id="ea430-113">A reservation gives those users the right to create services that listen on that portion of the namespace.</span></span> <span data-ttu-id="ea430-114">保留是 URL 前置詞，這表示保留區會涵蓋保留路徑的所有子路徑。</span><span class="sxs-lookup"><span data-stu-id="ea430-114">Reservations are URL prefixes, meaning that the reservation covers all subpaths of the reservation path.</span></span> <span data-ttu-id="ea430-115">命名空間保留區允許兩種使用萬用字元的方式。</span><span class="sxs-lookup"><span data-stu-id="ea430-115">Namespace reservations permit two ways to use wildcards.</span></span> <span data-ttu-id="ea430-116">HTTP 伺服器 API 檔描述[包含萬用字元的命名空間宣告之間的解析順序](/windows/desktop/Http/routing-incoming-requests)。</span><span class="sxs-lookup"><span data-stu-id="ea430-116">The HTTP Server API documentation describes the [order of resolution between namespace claims that involve wildcards](/windows/desktop/Http/routing-incoming-requests).</span></span>

<span data-ttu-id="ea430-117">執行中的應用程式可以建立類似的要求來新增命名空間註冊區。</span><span class="sxs-lookup"><span data-stu-id="ea430-117">A running application can create a similar request to add namespace registrations.</span></span> <span data-ttu-id="ea430-118">註冊區與保留區會競爭使用命名空間的各個部分。</span><span class="sxs-lookup"><span data-stu-id="ea430-118">Registrations and reservations compete for portions of the namespace.</span></span> <span data-ttu-id="ea430-119">根據與[萬用字元的命名空間宣告之間的解析](/windows/desktop/Http/routing-incoming-requests)順序所提供的解析順序，保留的優先順序可能高於註冊。</span><span class="sxs-lookup"><span data-stu-id="ea430-119">A reservation may have precedence over a registration according to the order of resolution given in the [order of resolution between namespace claims that involve wildcards](/windows/desktop/Http/routing-incoming-requests).</span></span> <span data-ttu-id="ea430-120">在此情況中，保留區會封鎖執行中的應用程式，使其無法接收要求。</span><span class="sxs-lookup"><span data-stu-id="ea430-120">In this case, the reservation blocks the running application from receiving requests.</span></span>

<span data-ttu-id="ea430-121">下列範例會使用 Netsh.exe 工具：</span><span class="sxs-lookup"><span data-stu-id="ea430-121">The following example uses the Netsh.exe tool:</span></span>

```console
netsh http add urlacl url=http://+:80/MyUri user=DOMAIN\user
```

<span data-ttu-id="ea430-122">此命令會為 DOMAIN\user 帳戶的指定 URL 命名空間新增 URL 保留專案。</span><span class="sxs-lookup"><span data-stu-id="ea430-122">This command adds a URL reservation for the specified URL namespace for the DOMAIN\user account.</span></span> <span data-ttu-id="ea430-123">如需使用 netsh 命令的詳細資訊，請 `netsh http add urlacl /?` 在命令提示字元中輸入，然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="ea430-123">For more information on using the netsh command, type `netsh http add urlacl /?` in a command-prompt and press Enter.</span></span>

## <a name="configuring-a-firewall-exception"></a><span data-ttu-id="ea430-124">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="ea430-124">Configuring a firewall exception</span></span>

<span data-ttu-id="ea430-125">對透過 HTTP 通訊的 WCF 服務進行自我裝載時，您必須將例外狀況加入至防火牆組態中，以允許使用特殊 URL 的傳入連線。</span><span class="sxs-lookup"><span data-stu-id="ea430-125">When self-hosting a WCF service that communicates over HTTP, an exception must be added to the firewall configuration to allow inbound connections using a particular URL.</span></span>

## <a name="configuring-ssl-certificates"></a><span data-ttu-id="ea430-126">設定 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="ea430-126">Configuring SSL certificates</span></span>

<span data-ttu-id="ea430-127">Secure Sockets Layer (SSL) 通訊協定會在用戶端與伺服器上使用憑證來儲存加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea430-127">The Secure Sockets Layer (SSL) protocol uses certificates on the client and server to store encryption keys.</span></span> <span data-ttu-id="ea430-128">伺服器會在連線期間提供自己的 SSL 憑證，方便用戶端驗證伺服器的身分識別。</span><span class="sxs-lookup"><span data-stu-id="ea430-128">The server provides its SSL certificate when a connection is made so that the client can verify the server identity.</span></span> <span data-ttu-id="ea430-129">伺服器也可以向用戶端要求憑證，以便連線的雙方進行互相驗證。</span><span class="sxs-lookup"><span data-stu-id="ea430-129">The server can also request a certificate from the client to provide mutual authentication of both sides of the connection.</span></span>

<span data-ttu-id="ea430-130">憑證會依據 IP 位址與連線的連接埠號碼，儲存在集中保管的存放區。</span><span class="sxs-lookup"><span data-stu-id="ea430-130">Certificates are stored in a centralized store according to the IP address and port number of the connection.</span></span> <span data-ttu-id="ea430-131">特殊 IP 位址 0.0.0.0 會符合本機電腦的任何 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ea430-131">The special IP address 0.0.0.0 matches any IP address for the local machine.</span></span> <span data-ttu-id="ea430-132">請注意，憑證存放區不會根據路徑來區分 Url。</span><span class="sxs-lookup"><span data-stu-id="ea430-132">Note that the certificate store doesn't distinguish URLs based on the path.</span></span> <span data-ttu-id="ea430-133">包含相同 IP 位址與連接埠號碼組合的服務必須共用憑證，就算每項服務之 URL 中的路徑都不一樣也需這麼做。</span><span class="sxs-lookup"><span data-stu-id="ea430-133">Services with the same IP address and port combination must share certificates even if the path in the URL for the services is different.</span></span>

<span data-ttu-id="ea430-134">如需逐步指示，請參閱[如何：使用 SSL 憑證設定埠](how-to-configure-a-port-with-an-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="ea430-134">For step-by-step instructions, see [How to: Configure a Port with an SSL Certificate](how-to-configure-a-port-with-an-ssl-certificate.md).</span></span>

## <a name="configuring-the-ip-listen-list"></a><span data-ttu-id="ea430-135">設定 IP 接聽清單</span><span class="sxs-lookup"><span data-stu-id="ea430-135">Configuring the IP Listen List</span></span>

<span data-ttu-id="ea430-136">一旦使用者註冊了 URL，HTTP 伺服器 API 只會繫結至 IP 位址與連接埠。</span><span class="sxs-lookup"><span data-stu-id="ea430-136">The HTTP Server API only binds to an IP address and port once a user registers a URL.</span></span> <span data-ttu-id="ea430-137">根據預設，HTTP 伺服器 API 會針對電腦中的所有 IP 位址繫結至其 URL 中的連接埠。</span><span class="sxs-lookup"><span data-stu-id="ea430-137">By default, the HTTP Server API binds to the port in the URL for all of the IP addresses of the machine.</span></span> <span data-ttu-id="ea430-138">如果未使用 HTTP 伺服器 API 的應用程式先前已系結至該 IP 位址和埠的組合，就會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="ea430-138">A conflict arises if an application that doesn't use the HTTP Server API has previously bound to that combination of IP address and port.</span></span> <span data-ttu-id="ea430-139">IP 接聽清單可讓 WCF 服務與針對機器的部分 IP 位址使用埠的應用程式並存。</span><span class="sxs-lookup"><span data-stu-id="ea430-139">The IP Listen List allows WCF services to coexist with applications that use a port for some of the IP addresses of the machine.</span></span> <span data-ttu-id="ea430-140">如果 IP 接聽清單包含任何項目，則 HTTP 伺服器 API 只會繫結至清單所指定的特定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ea430-140">If the IP Listen List contains any entries, the HTTP Server API only binds to those IP addresses that the list specifies.</span></span> <span data-ttu-id="ea430-141">您需要系統管理員權限才能修改 IP 接聽清單。</span><span class="sxs-lookup"><span data-stu-id="ea430-141">Modifying the IP Listen List requires administrative privileges.</span></span>

<span data-ttu-id="ea430-142">使用 netsh 工具來修改 IP 接聽清單，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ea430-142">Use the netsh tool to modify the IP Listen List, as shown in the following example:</span></span>

```console
netsh http add iplisten ipaddress=0.0.0.0:8000
```

## <a name="other-configuration-settings"></a><span data-ttu-id="ea430-143">其他設定</span><span class="sxs-lookup"><span data-stu-id="ea430-143">Other configuration settings</span></span>

<span data-ttu-id="ea430-144">使用 <xref:System.ServiceModel.WSDualHttpBinding> 時，用戶端連線會使用與命名空間保留區及 Windows 防火牆相容的預設值。</span><span class="sxs-lookup"><span data-stu-id="ea430-144">When using <xref:System.ServiceModel.WSDualHttpBinding>, the client connection uses defaults that are compatible with namespace reservations and the Windows firewall.</span></span> <span data-ttu-id="ea430-145">如果您選擇自訂雙向連線的用戶端基底位址，則您必須同時在用戶端上設定這些 HTTP 設定值以符合新的位址。</span><span class="sxs-lookup"><span data-stu-id="ea430-145">If you choose to customize the client base address of a dual connection, then you also must configure these HTTP settings on the client to match the new address.</span></span>

<span data-ttu-id="ea430-146">HTTP 伺服器 API 有一些無法透過 Httpcfg.exe 取得的 advanced configuration 設定。</span><span class="sxs-lookup"><span data-stu-id="ea430-146">The HTTP Server API has some advanced configuration settings that aren't available through HttpCfg.</span></span> <span data-ttu-id="ea430-147">這些設定會維護在登錄中，並套用至所有在系統中使用 HTTP 伺服器 API 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea430-147">These settings are maintained in the registry and apply to all applications running on the systems that use the HTTP Server APIs.</span></span> <span data-ttu-id="ea430-148">如需這些設定的相關資訊，請參閱[Http.sys IIS 的登錄設定](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows)。</span><span class="sxs-lookup"><span data-stu-id="ea430-148">For information about these settings, see [Http.sys registry settings for IIS](https://support.microsoft.com/help/820129/http-sys-registry-settings-for-windows).</span></span> <span data-ttu-id="ea430-149">大部分的使用者都不需要變更這些設定。</span><span class="sxs-lookup"><span data-stu-id="ea430-149">Most users don't need to change these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea430-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ea430-150">See also</span></span>

- <xref:System.ServiceModel.WSDualHttpBinding>
- [<span data-ttu-id="ea430-151">如何：使用 SSL 憑證設定連接埠</span><span class="sxs-lookup"><span data-stu-id="ea430-151">How to: Configure a Port with an SSL Certificate</span></span>](how-to-configure-a-port-with-an-ssl-certificate.md)
