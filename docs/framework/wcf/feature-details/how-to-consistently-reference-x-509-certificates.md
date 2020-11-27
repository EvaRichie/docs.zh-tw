---
title: 作法：一律參考 X.509 憑證
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates [WCF], referencing X.509 certificates
ms.assetid: a6de1c63-e450-4640-ad08-ad7302dbfbfc
ms.openlocfilehash: b5be8990384178c1954834204c23c0b9cf4a5ad9
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96257271"
---
# <a name="how-to-consistently-reference-x509-certificates"></a><span data-ttu-id="eae67-102">作法：一律參考 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="eae67-102">How to: Consistently Reference X.509 Certificates</span></span>

<span data-ttu-id="eae67-103">您可以用幾種方式來識別憑證：依據憑證的雜湊、依據簽發者和序號，或是依據主體金鑰識別元 (SKI)。</span><span class="sxs-lookup"><span data-stu-id="eae67-103">You can identify a certificate in several ways: by the hash of the certificate, by the issuer and serial number, or by the subject key identifier (SKI).</span></span> <span data-ttu-id="eae67-104">SKI 會提供憑證之主體公開金鑰的唯一識別，而且通常會在使用 XML 數位簽章時使用。</span><span class="sxs-lookup"><span data-stu-id="eae67-104">The SKI provides a unique identification for the certificate's subject public key and is often used when working with XML digital signing.</span></span> <span data-ttu-id="eae67-105">SKI 值通常是 x.509 憑證的一部分，作為 *x.509 憑證延伸*。</span><span class="sxs-lookup"><span data-stu-id="eae67-105">The SKI value is usually part of the X.509 certificate as an *X.509 certificate extension*.</span></span> <span data-ttu-id="eae67-106">Windows Communication Foundation (WCF) 具有預設的 *參考樣式* ，如果憑證中遺漏 SKI 延伸模組，則會使用簽發者和序號。</span><span class="sxs-lookup"><span data-stu-id="eae67-106">Windows Communication Foundation (WCF) has a default *referencing style* that uses the issuer and serial number if the SKI extension is missing from the certificate.</span></span> <span data-ttu-id="eae67-107">如果憑證包含 SKI 延伸，預設的參考樣式便會使用 SKI 來指向憑證。</span><span class="sxs-lookup"><span data-stu-id="eae67-107">If the certificate contains the SKI extension, the default referencing style uses the SKI to point to the certificate.</span></span> <span data-ttu-id="eae67-108">如果透過開發應用程式的過程中，您將無法使用不使用 SKI 延伸的憑證切換到使用 SKI 延伸模組的憑證，則 WCF 產生之訊息中所使用的參考樣式也會變更。</span><span class="sxs-lookup"><span data-stu-id="eae67-108">If mid-way through development of an application, you switch from using certificates that do not use the SKI extension to certificates that use the SKI extension, the referencing style used in WCF-generated messages also changes.</span></span>  
  
 <span data-ttu-id="eae67-109">如果無論 SKI 延伸是否存在都必須使用一致的參考樣式，這時就可以設定需要的參考樣式，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="eae67-109">If a consistent referencing style is required regardless of SKI extension presence, it is possible to configure the desired referencing style as shown in the following code.</span></span>  
  
## <a name="example"></a><span data-ttu-id="eae67-110">範例</span><span class="sxs-lookup"><span data-stu-id="eae67-110">Example</span></span>  

 <span data-ttu-id="eae67-111">下列範例會建立自訂的安全性繫結項目，該項目會使用單一的一致參考樣式、簽發者名稱及序號。</span><span class="sxs-lookup"><span data-stu-id="eae67-111">The following example creates a custom security binding element that uses a single consistent referencing style, the issuer name and serial number.</span></span>  
  
 [!code-csharp[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_referencingcertificatesconsistently/cs/source.cs#1)]
 [!code-vb[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_referencingcertificatesconsistently/vb/source.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="eae67-112">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="eae67-112">Compiling the Code</span></span>  

 <span data-ttu-id="eae67-113">要編譯程式碼時，必須有下列命名空間：</span><span class="sxs-lookup"><span data-stu-id="eae67-113">The following namespaces are required to compile the code:</span></span>  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Security.Tokens>  
  
## <a name="see-also"></a><span data-ttu-id="eae67-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="eae67-114">See also</span></span>

- [<span data-ttu-id="eae67-115">使用憑證</span><span class="sxs-lookup"><span data-stu-id="eae67-115">Working with Certificates</span></span>](working-with-certificates.md)
