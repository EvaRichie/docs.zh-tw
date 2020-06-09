---
title: 透過 TCP 與 SOAP 安全性的 HTTPS 與 SSL 之間的憑證驗證差異
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates [WCF], validation differences
ms.assetid: 953a219f-4745-4019-9894-c70704f352e6
ms.openlocfilehash: dcde7bb4cc193d18737d26facbbd69ccd597d66b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599330"
---
# <a name="certificate-validation-differences-between-https-ssl-over-tcp-and-soap-security"></a><span data-ttu-id="332f6-102">透過 TCP 與 SOAP 安全性的 HTTPS 與 SSL 之間的憑證驗證差異</span><span class="sxs-lookup"><span data-stu-id="332f6-102">Certificate Validation Differences Between HTTPS, SSL over TCP, and SOAP Security</span></span>
<span data-ttu-id="332f6-103">除了透過 HTTP （HTTPS）或 TCP 的傳輸層安全性（TLS）之外，您還可以使用 Windows Communication Foundation （WCF）中的憑證搭配訊息層（SOAP）安全性。</span><span class="sxs-lookup"><span data-stu-id="332f6-103">You can use certificates in Windows Communication Foundation (WCF) with message-layer (SOAP) security in addition to transport-layer security (TLS) over HTTP (HTTPS) or TCP.</span></span> <span data-ttu-id="332f6-104">此主題說明這類憑證的不同驗證方法。</span><span class="sxs-lookup"><span data-stu-id="332f6-104">This topic describes differences in the way such certificates are validated.</span></span>  
  
## <a name="validation-of-https-client-certificates"></a><span data-ttu-id="332f6-105">HTTPS 用戶端憑證的驗證</span><span class="sxs-lookup"><span data-stu-id="332f6-105">Validation of HTTPS Client Certificates</span></span>  
 <span data-ttu-id="332f6-106">使用 HTTPS 在用戶端與服務之間通訊時，用戶端用來驗證服務的憑證必須支援信賴鏈結的原則。</span><span class="sxs-lookup"><span data-stu-id="332f6-106">When using HTTPS to communicate between a client and a service, the certificate that the client uses to authenticate to the service must support chain trust.</span></span> <span data-ttu-id="332f6-107">也就是說，它必須鏈結至受信任的根憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="332f6-107">That is, it must chain to a trusted root certificate authority.</span></span> <span data-ttu-id="332f6-108">否則，HTTP 層將發出訊息為「遠端伺服器傳回錯誤：(403) 禁止」的 <xref:System.Net.WebException>。</span><span class="sxs-lookup"><span data-stu-id="332f6-108">If not, the HTTP layer raises a <xref:System.Net.WebException> with the message "The remote server returned an error: (403) Forbidden."</span></span> <span data-ttu-id="332f6-109">WCF 會將此例外狀況呈現為 <xref:System.ServiceModel.Security.MessageSecurityException> 。</span><span class="sxs-lookup"><span data-stu-id="332f6-109">WCF surfaces this exception as a <xref:System.ServiceModel.Security.MessageSecurityException>.</span></span>  
  
## <a name="validation-of-https-service-certificates"></a><span data-ttu-id="332f6-110">HTTPS 服務憑證的驗證</span><span class="sxs-lookup"><span data-stu-id="332f6-110">Validation of HTTPS Service Certificates</span></span>  
 <span data-ttu-id="332f6-111">使用 HTTPS 在用戶端與服務之間通訊時，伺服器驗證的憑證必須預設支援信賴鏈結的原則。</span><span class="sxs-lookup"><span data-stu-id="332f6-111">When using HTTPS to communicate between a client and a service, the certificate that the server authenticates with must support chain trust by default.</span></span> <span data-ttu-id="332f6-112">也就是說，它必須鏈結至受信任的根憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="332f6-112">That is, it must chain to a trusted root certificate authority.</span></span> <span data-ttu-id="332f6-113">不進行線上檢查憑證是否已經被撤銷。</span><span class="sxs-lookup"><span data-stu-id="332f6-113">No online check is performed to see whether the certificate has been revoked.</span></span> <span data-ttu-id="332f6-114">您可以登錄 <xref:System.Net.Security.RemoteCertificateValidationCallback> 回呼覆寫此行為，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="332f6-114">You can override this behavior by registering a <xref:System.Net.Security.RemoteCertificateValidationCallback> callback, as shown in the following code.</span></span>  
  
 [!code-csharp[c_CertificateValidationDifferences#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#1)]
 [!code-vb[c_CertificateValidationDifferences#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#1)]  
  
 <span data-ttu-id="332f6-115">`ValidateServerCertificate` 簽名如下：</span><span class="sxs-lookup"><span data-stu-id="332f6-115">where the signature for `ValidateServerCertificate` is as follows:</span></span>  
  
 [!code-csharp[c_CertificateValidationDifferences#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#2)]
 [!code-vb[c_CertificateValidationDifferences#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#2)]  
  
 <span data-ttu-id="332f6-116">實作 `ValidateServerCertificate` 可執行任何用戶端應用程式開發者認為驗證服務憑證需要的檢查。</span><span class="sxs-lookup"><span data-stu-id="332f6-116">Implementing `ValidateServerCertificate` can perform any checks that the client application developer deems necessary to validate the service certificate.</span></span>  
  
## <a name="validation-of-client-certificates-in-ssl-over-tcp-or-soap-security"></a><span data-ttu-id="332f6-117">架構於 TCP 或 SOAP 安全性的用戶端 SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="332f6-117">Validation of Client Certificates in SSL over TCP or SOAP Security</span></span>  
 <span data-ttu-id="332f6-118">使用架構於 TCP 或訊息 (SOAP) 安全性的 Secure Sockets Layer (SSL) 時，用戶端憑證是根據 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> 類別之 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 屬性值進行驗證。</span><span class="sxs-lookup"><span data-stu-id="332f6-118">When using Secure Sockets Layer (SSL) over TCP or message (SOAP) security, client certificates are validated according to the <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> property value of the <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> class.</span></span> <span data-ttu-id="332f6-119">屬性設為其中一個 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值。</span><span class="sxs-lookup"><span data-stu-id="332f6-119">The property is set to one of the <xref:System.ServiceModel.Security.X509CertificateValidationMode> values.</span></span> <span data-ttu-id="332f6-120">撤銷檢查是根據 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.RevocationMode%2A> 類別的 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 屬性值執行。</span><span class="sxs-lookup"><span data-stu-id="332f6-120">Revocation checking is performed according to the values of the <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.RevocationMode%2A> property value of the <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> class.</span></span> <span data-ttu-id="332f6-121">屬性設為其中一個 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值。</span><span class="sxs-lookup"><span data-stu-id="332f6-121">The property is set to one of the <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> values.</span></span>  
  
 [!code-csharp[c_CertificateValidationDifferences#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#3)]
 [!code-vb[c_CertificateValidationDifferences#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#3)]  
  
## <a name="validation-of-service-certificate-in-ssl-over-tcp-and-soap-security"></a><span data-ttu-id="332f6-122">架構於 TCP 或 SOAP 安全性之服務 SSL 憑證驗證</span><span class="sxs-lookup"><span data-stu-id="332f6-122">Validation of Service Certificate in SSL over TCP and SOAP Security</span></span>  
 <span data-ttu-id="332f6-123">使用架構於 TCP 或 (SOAP) 訊息安全性的 SSL 時，服務憑證是根據 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 類別之 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> 屬性值進行驗證。</span><span class="sxs-lookup"><span data-stu-id="332f6-123">When using SSL over TCP or (SOAP) message security, service certificates are validated according to the <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> property value of the <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> class.</span></span> <span data-ttu-id="332f6-124">屬性設為其中一個 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值。</span><span class="sxs-lookup"><span data-stu-id="332f6-124">The property is set to one of the <xref:System.ServiceModel.Security.X509CertificateValidationMode> values.</span></span>  
  
 <span data-ttu-id="332f6-125">撤銷檢查是根據 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.RevocationMode%2A> 類別的 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> 屬性值執行。</span><span class="sxs-lookup"><span data-stu-id="332f6-125">Revocation checking is performed according to the values of the <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.RevocationMode%2A> property value of the <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> class.</span></span> <span data-ttu-id="332f6-126">屬性設為其中一個 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值。</span><span class="sxs-lookup"><span data-stu-id="332f6-126">The property is set to one of the <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> values.</span></span>  
  
 [!code-csharp[c_CertificateValidationDifferences#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#4)]
 [!code-vb[c_CertificateValidationDifferences#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="332f6-127">請參閱</span><span class="sxs-lookup"><span data-stu-id="332f6-127">See also</span></span>

- <xref:System.Net.Security.RemoteCertificateValidationCallback>
- [<span data-ttu-id="332f6-128">Working with Certificates</span><span class="sxs-lookup"><span data-stu-id="332f6-128">Working with Certificates</span></span>](working-with-certificates.md)
