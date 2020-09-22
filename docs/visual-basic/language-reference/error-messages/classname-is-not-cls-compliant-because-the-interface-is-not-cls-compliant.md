---
title: "'<classname>' 不符合 CLS 標準，因為它所實作的介面 '<interfacename>' 不符合 CLS 標準"
ms.date: 07/20/2015
f1_keywords:
- bc40029
- vbc40029
helpviewer_keywords:
- BC40029
ms.assetid: 178452f3-5575-4da0-9d6c-53bcddb6a338
ms.openlocfilehash: a482d14094a3fa86b56ca84af46c45e6093416c5
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874629"
---
# <a name="classname-is-not-cls-compliant-because-the-interface-interfacename-it-implements-is-not-cls-compliant"></a><span data-ttu-id="f4eb5-102">'\<classname>' 不符合 CLS 標準，因為它所實作的介面 '\<interfacename>' 不符合 CLS 標準</span><span class="sxs-lookup"><span data-stu-id="f4eb5-102">'\<classname>' is not CLS-compliant because the interface '\<interfacename>' it implements is not CLS-compliant</span></span>

<span data-ttu-id="f4eb5-103">當類別或介面衍生自或實作標記為 `<CLSCompliant(True)>` 或未標記的類型時，則標記為 `<CLSCompliant(False)>` 。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-103">A class or interface is marked as `<CLSCompliant(True)>` when it derives from or implements a type that is marked as `<CLSCompliant(False)>` or is not marked.</span></span>  
  
 <span data-ttu-id="f4eb5-104">為了讓類別或介面符合 [語言獨立性以及與語言無關的元件](../../../standard/language-independence-and-language-independent-components.md) (cls) ，其整個繼承階層必須符合規範。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-104">For a class or interface to be compliant with the [Language Independence and Language-Independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS), its entire inheritance hierarchy must be compliant.</span></span> <span data-ttu-id="f4eb5-105">這表示它直接或間接繼承的每個類型都必須符合規範。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-105">That means every type from which it inherits, directly or indirectly, must be compliant.</span></span> <span data-ttu-id="f4eb5-106">同樣地，如果類別實作一或多個介面，則它們在整個繼承階層都必須符合標準。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-106">Similarly, if a class implements one or more interfaces, they must all be compliant throughout their inheritance hierarchies.</span></span>  
  
 <span data-ttu-id="f4eb5-107">將 <xref:System.CLSCompliantAttribute> 套用至程式設計項目時，請將屬性的 `isCompliant` 參數設定為 `True` 或 `False` ，表示符合標準或不符合標準。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-107">When you apply the <xref:System.CLSCompliantAttribute> to a programming element, you set the attribute's `isCompliant` parameter to either `True` or `False` to indicate compliance or noncompliance.</span></span> <span data-ttu-id="f4eb5-108">這個參數沒有預設值，您必須提供值。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-108">There is no default for this parameter, and you must supply a value.</span></span>  
  
 <span data-ttu-id="f4eb5-109">如果您未將 <xref:System.CLSCompliantAttribute> 套用至項目，則視為不符合標準。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-109">If you do not apply the <xref:System.CLSCompliantAttribute> to an element, it is considered to be noncompliant.</span></span>  
  
 <span data-ttu-id="f4eb5-110">根據預設，這個訊息是一個警告。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-110">By default, this message is a warning.</span></span> <span data-ttu-id="f4eb5-111">如需隱藏警告或將警告視為錯誤的相關資訊，請參閱 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-111">For information on hiding warnings or treating warnings as errors, see [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).</span></span>  
  
 <span data-ttu-id="f4eb5-112">**錯誤識別碼：** BC40029</span><span class="sxs-lookup"><span data-stu-id="f4eb5-112">**Error ID:** BC40029</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="f4eb5-113">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="f4eb5-113">To correct this error</span></span>  
  
- <span data-ttu-id="f4eb5-114">如果您必須符合 CLS 標準，請在不同的繼承階層或實作配置內定義這個類型。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-114">If you require CLS compliance, define this type within a different inheritance hierarchy or implementation scheme.</span></span>  
  
- <span data-ttu-id="f4eb5-115">如果您想要將這個類型保留在其目前繼承階層或實作配置內，請從其定義移除 <xref:System.CLSCompliantAttribute> 或將其標記為 `<CLSCompliant(False)>`。</span><span class="sxs-lookup"><span data-stu-id="f4eb5-115">If you require that this type remain within its current inheritance hierarchy or implementation scheme, remove the <xref:System.CLSCompliantAttribute> from its definition or mark it as `<CLSCompliant(False)>`.</span></span>  
