---
ms.openlocfilehash: 5c27e8acdf30533036546ba4cca9e06877bde362
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620116"
---
### <a name="xslt-style-sheet-exception-message-changed"></a><span data-ttu-id="cef48-101">XSLT 樣式表例外狀況訊息已變更</span><span class="sxs-lookup"><span data-stu-id="cef48-101">XSLT style sheet exception message changed</span></span>

#### <a name="details"></a><span data-ttu-id="cef48-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="cef48-102">Details</span></span>

<span data-ttu-id="cef48-103">在 .NET Framework 4.5 中，當 XSLT 檔太複雜時，錯誤訊息的文字為 &quot; 樣式表單太複雜。 &quot;在舊版中，錯誤訊息是「 &quot; XSLT 編譯錯誤」。 &quot;相依于錯誤訊息文字的應用程式代碼將不再有效。</span><span class="sxs-lookup"><span data-stu-id="cef48-103">In the .NET Framework 4.5, the text of the error message when an XSLT file is too complex is &quot;The style sheet is too complex.&quot; In previous versions, the error message was &quot;XSLT compile error.&quot; Application code that depends on the text of the error message will no longer work.</span></span> <span data-ttu-id="cef48-104">不過，例外狀況類型會保持不變，因此這項變更應該不會產生實際影響。</span><span class="sxs-lookup"><span data-stu-id="cef48-104">However, the exception types remain the same, so this change should have no real impact.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="cef48-105">建議</span><span class="sxs-lookup"><span data-stu-id="cef48-105">Suggestion</span></span>

<span data-ttu-id="cef48-106">請將依據此錯誤狀況之例外狀況訊息的任何應用程式程式碼更新為預期會有新訊息，或是 (甚至更佳的做法) 將程式碼更新為只依據尚未變更的例外狀況類型 (<xref:System.Xml.Xsl.XsltException?displayProperty=fullName>)。</span><span class="sxs-lookup"><span data-stu-id="cef48-106">Update any app code depending on the exception message from this error condition to expect the new message, or (even better) update the code to depend only on the exception type (<xref:System.Xml.Xsl.XsltException?displayProperty=fullName>), which has not changed.</span></span>

| <span data-ttu-id="cef48-107">名稱</span><span class="sxs-lookup"><span data-stu-id="cef48-107">Name</span></span>    | <span data-ttu-id="cef48-108">值</span><span class="sxs-lookup"><span data-stu-id="cef48-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="cef48-109">影響範圍</span><span class="sxs-lookup"><span data-stu-id="cef48-109">Scope</span></span>   |<span data-ttu-id="cef48-110">Edge</span><span class="sxs-lookup"><span data-stu-id="cef48-110">Edge</span></span>|
|<span data-ttu-id="cef48-111">版本</span><span class="sxs-lookup"><span data-stu-id="cef48-111">Version</span></span>|<span data-ttu-id="cef48-112">4.5</span><span class="sxs-lookup"><span data-stu-id="cef48-112">4.5</span></span>|
|<span data-ttu-id="cef48-113">類型</span><span class="sxs-lookup"><span data-stu-id="cef48-113">Type</span></span>|<span data-ttu-id="cef48-114">執行階段</span><span class="sxs-lookup"><span data-stu-id="cef48-114">Runtime</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="cef48-115">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="cef48-115">Affected APIs</span></span>

-<xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Type)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Reflection.MethodInfo,System.Byte[],System.Type[])?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li></ul>|
