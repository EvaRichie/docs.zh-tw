---
title: 作法：移轉 XslTransform 程式碼
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 910beb2f-cfb3-4e8e-9936-f7e0c5f4064a
ms.openlocfilehash: d1e13d2bcc7525f261df90c36aa4214f318cf3c0
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722709"
---
# <a name="how-to-migrate-your-xsltransform-code"></a><span data-ttu-id="9afda-102">作法：移轉 XslTransform 程式碼</span><span class="sxs-lookup"><span data-stu-id="9afda-102">How to: Migrate Your XslTransform Code</span></span>

<span data-ttu-id="9afda-103">設計的新版 XSLT 類別與現有類別非常類似。</span><span class="sxs-lookup"><span data-stu-id="9afda-103">The new XSLT classes have been designed to be very similar to the existing classes.</span></span> <span data-ttu-id="9afda-104"><xref:System.Xml.Xsl.XslCompiledTransform> 類別取代了 <xref:System.Xml.Xsl.XslTransform> 類別。</span><span class="sxs-lookup"><span data-stu-id="9afda-104">The <xref:System.Xml.Xsl.XslCompiledTransform> class replaces the <xref:System.Xml.Xsl.XslTransform> class.</span></span> <span data-ttu-id="9afda-105">使用 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法編譯樣式表。</span><span class="sxs-lookup"><span data-stu-id="9afda-105">Style sheets are compiled using the <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> method.</span></span> <span data-ttu-id="9afda-106">使用 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法執行轉換。</span><span class="sxs-lookup"><span data-stu-id="9afda-106">Transforms are executed using the <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> method.</span></span> <span data-ttu-id="9afda-107">下列程序顯示常見的 XSLT 工作，並比較使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼與使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-107">The following procedures show common XSLT tasks, and compare the code using the <xref:System.Xml.Xsl.XslTransform> class versus the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
### <a name="to-transform-a-file-and-output-to-a-uri"></a><span data-ttu-id="9afda-108">轉換檔案及輸出為 URI</span><span class="sxs-lookup"><span data-stu-id="9afda-108">To transform a file and output to a URI</span></span>  
  
- <span data-ttu-id="9afda-109">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-109">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#9](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#9)]
     [!code-vb[XML_Migration#9](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#9)]  
  
- <span data-ttu-id="9afda-110">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-110">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#10](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#10)]
     [!code-vb[XML_Migration#10](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#10)]  
  
### <a name="to-compile-a-style-sheet-and-use-a-resolver-with-default-credentials"></a><span data-ttu-id="9afda-111">編譯樣式表並使用具有預設認證的解析程式</span><span class="sxs-lookup"><span data-stu-id="9afda-111">To compile a style sheet and use a resolver with default credentials</span></span>  
  
- <span data-ttu-id="9afda-112">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-112">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#11)]
     [!code-vb[XML_Migration#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#11)]  
  
- <span data-ttu-id="9afda-113">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-113">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#12](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#12)]
     [!code-vb[XML_Migration#12](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#12)]  
  
### <a name="to-use-an-xslt-parameter"></a><span data-ttu-id="9afda-114">使用 XSLT 參數</span><span class="sxs-lookup"><span data-stu-id="9afda-114">To use an XSLT parameter</span></span>  
  
- <span data-ttu-id="9afda-115">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-115">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#13](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#13)]
     [!code-vb[XML_Migration#13](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#13)]  
  
- <span data-ttu-id="9afda-116">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-116">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#14](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#14)]
     [!code-vb[XML_Migration#14](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#14)]  
  
### <a name="to-enable-xslt-scripting"></a><span data-ttu-id="9afda-117">啟用 XSLT 指令碼</span><span class="sxs-lookup"><span data-stu-id="9afda-117">To enable XSLT scripting</span></span>  
  
- <span data-ttu-id="9afda-118">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-118">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#15](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#15)]
     [!code-vb[XML_Migration#15](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#15)]  
  
- <span data-ttu-id="9afda-119">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-119">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
     [!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]  
  
### <a name="to-load-the-results-into-a-dom-object"></a><span data-ttu-id="9afda-120">將結果載入至 DOM 物件</span><span class="sxs-lookup"><span data-stu-id="9afda-120">To load the results into a DOM object</span></span>  
  
- <span data-ttu-id="9afda-121">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-121">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#19](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#19)]
     [!code-vb[XML_Migration#19](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#19)]  
  
- <span data-ttu-id="9afda-122">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-122">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="9afda-123"><xref:System.Xml.Xsl.XslCompiledTransform> 類別不具有將 XSLT 轉換結果當做 <xref:System.Xml.XmlReader> 物件傳回的方法。</span><span class="sxs-lookup"><span data-stu-id="9afda-123">The <xref:System.Xml.Xsl.XslCompiledTransform> class does not have a method that returns the XSLT transformation results as an <xref:System.Xml.XmlReader> object.</span></span> <span data-ttu-id="9afda-124">但是，您可以輸出至 XML 檔案，並將 XML 檔案載入到其他物件中。</span><span class="sxs-lookup"><span data-stu-id="9afda-124">However, you can output to an XML file and load the XML file into another object.</span></span>  
  
     [!code-csharp[XML_Migration#20](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#20)]
     [!code-vb[XML_Migration#20](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#20)]  
  
### <a name="to-stream-the-results-into-another-data-store"></a><span data-ttu-id="9afda-125">以資料流方式傳送結果至其他資料存放區</span><span class="sxs-lookup"><span data-stu-id="9afda-125">To stream the results into another data store</span></span>  
  
- <span data-ttu-id="9afda-126">使用 <xref:System.Xml.Xsl.XslTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-126">Code using the <xref:System.Xml.Xsl.XslTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#17](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#17)]
     [!code-vb[XML_Migration#17](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#17)]  
  
- <span data-ttu-id="9afda-127">使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9afda-127">Code using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>  
  
     [!code-csharp[XML_Migration#18](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#18)]
     [!code-vb[XML_Migration#18](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#18)]  
  
## <a name="see-also"></a><span data-ttu-id="9afda-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9afda-128">See also</span></span>

- [<span data-ttu-id="9afda-129">從 XslTransform 類別移轉</span><span class="sxs-lookup"><span data-stu-id="9afda-129">Migrating From the XslTransform Class</span></span>](migrating-from-the-xsltransform-class.md)
- [<span data-ttu-id="9afda-130">使用 XslCompiledTransform 類別</span><span class="sxs-lookup"><span data-stu-id="9afda-130">Using the XslCompiledTransform Class</span></span>](using-the-xslcompiledtransform-class.md)
