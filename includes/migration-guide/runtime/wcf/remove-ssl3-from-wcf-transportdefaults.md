---
ms.openlocfilehash: 9b734fe960165b6d4b97b861cb3e8f31979f25c5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621084"
---
### <a name="remove-ssl3-from-the-wcf-transportdefaults"></a><span data-ttu-id="53495-101">從 WCF TransportDefaults 中移除 SSL3</span><span class="sxs-lookup"><span data-stu-id="53495-101">Remove Ssl3 from the WCF TransportDefaults</span></span>

#### <a name="details"></a><span data-ttu-id="53495-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="53495-102">Details</span></span>

<span data-ttu-id="53495-103">當使用 NetTcp 搭配傳輸安全性和憑證類型的認證時，SSL 3 通訊協定已不再是用來交涉安全連接的預設通訊協定。</span><span class="sxs-lookup"><span data-stu-id="53495-103">When using NetTcp with transport security and a credential type of certificate, the SSL 3 protocol is no longer a default protocol used for negotiating a secure connection.</span></span> <span data-ttu-id="53495-104">在大部分情況下，應該不會影響現有的應用程式，因為 TLS 1.0 一律包含在 NetTcp 的通訊協定清單中。</span><span class="sxs-lookup"><span data-stu-id="53495-104">In most cases there should be no impact to existing apps as TLS 1.0 has always been included in the protocol list for NetTcp.</span></span> <span data-ttu-id="53495-105">所有現有的用戶端應該能夠使用至少 TLS 1.0 來交涉連接。</span><span class="sxs-lookup"><span data-stu-id="53495-105">All existing clients should be able to negotiate a connection using at least TLS1.0.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="53495-106">建議</span><span class="sxs-lookup"><span data-stu-id="53495-106">Suggestion</span></span>

<span data-ttu-id="53495-107">如果需要 SSL3，請使用下列組態機制其中之一，將 SSL3 新增至交涉通訊協定的清單。</span><span class="sxs-lookup"><span data-stu-id="53495-107">If Ssl3 is required, use one of the following configuration mechanisms to add Ssl3 to the list of negotiated protocols.</span></span><ul><li><xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols></li><li><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols></li><li>[<](~/docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md)</li><li><span data-ttu-id="53495-108">[&lt;customBinding&gt; 的 &lt;sslStreamSecurity&gt; 區段]~/docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)</span><span class="sxs-lookup"><span data-stu-id="53495-108">[&lt;sslStreamSecurity&gt; section of &lt;customBinding&gt;]~/docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md)</span></span></li></ul>

| <span data-ttu-id="53495-109">名稱</span><span class="sxs-lookup"><span data-stu-id="53495-109">Name</span></span>    | <span data-ttu-id="53495-110">值</span><span class="sxs-lookup"><span data-stu-id="53495-110">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="53495-111">影響範圍</span><span class="sxs-lookup"><span data-stu-id="53495-111">Scope</span></span>   |<span data-ttu-id="53495-112">Edge</span><span class="sxs-lookup"><span data-stu-id="53495-112">Edge</span></span>|
|<span data-ttu-id="53495-113">版本</span><span class="sxs-lookup"><span data-stu-id="53495-113">Version</span></span>|<span data-ttu-id="53495-114">4.6.2</span><span class="sxs-lookup"><span data-stu-id="53495-114">4.6.2</span></span>|
|<span data-ttu-id="53495-115">類型</span><span class="sxs-lookup"><span data-stu-id="53495-115">Type</span></span>|<span data-ttu-id="53495-116">執行階段</span><span class="sxs-lookup"><span data-stu-id="53495-116">Runtime</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="53495-117">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="53495-117">Affected APIs</span></span>

-<xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols?displayProperty=nameWithType></li><li><xref:System.ServiceModel.TcpTransportSecurity.SslProtocols?displayProperty=nameWithType></li></ul>|
