---
title: WriteOnly
ms.date: 07/20/2015
f1_keywords:
- WriteOnly
- vb.WriteOnly
helpviewer_keywords:
- write-only properties
- WriteOnly keyword [Visual Basic]
- sensitive data, protecting
- properties [Visual Basic], write-only
- sensitive data
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
ms.openlocfilehash: a9fa0a3a23561215d6ff122bc8e609b68ca6fc30
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84386630"
---
# <a name="writeonly-visual-basic"></a><span data-ttu-id="f5781-102">WriteOnly (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f5781-102">WriteOnly (Visual Basic)</span></span>
<span data-ttu-id="f5781-103">指定可寫入但無法讀取的屬性。</span><span class="sxs-lookup"><span data-stu-id="f5781-103">Specifies that a property can be written but not read.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f5781-104">備註</span><span class="sxs-lookup"><span data-stu-id="f5781-104">Remarks</span></span>  
  
## <a name="rules"></a><span data-ttu-id="f5781-105">規則</span><span class="sxs-lookup"><span data-stu-id="f5781-105">Rules</span></span>  
 <span data-ttu-id="f5781-106">**宣告內容。**</span><span class="sxs-lookup"><span data-stu-id="f5781-106">**Declaration Context.**</span></span> <span data-ttu-id="f5781-107">您只能在模組層級使用 `WriteOnly`。</span><span class="sxs-lookup"><span data-stu-id="f5781-107">You can use `WriteOnly` only at module level.</span></span> <span data-ttu-id="f5781-108">這表示屬性的宣告內容 `WriteOnly` 必須是類別、結構或模組，而且不能是原始程式檔、命名空間或程式。</span><span class="sxs-lookup"><span data-stu-id="f5781-108">This means the declaration context for a `WriteOnly` property must be a class, structure, or module, and cannot be a source file, namespace, or procedure.</span></span>  
  
 <span data-ttu-id="f5781-109">您可以將屬性宣告為 `WriteOnly` ，但不能宣告為變數。</span><span class="sxs-lookup"><span data-stu-id="f5781-109">You can declare a property as `WriteOnly`, but not a variable.</span></span>  
  
## <a name="when-to-use-writeonly"></a><span data-ttu-id="f5781-110">使用 WriteOnly 的時機</span><span class="sxs-lookup"><span data-stu-id="f5781-110">When to Use WriteOnly</span></span>  
 <span data-ttu-id="f5781-111">有時候您會想要讓使用中的程式碼能夠設定值，但不會探索其意義。</span><span class="sxs-lookup"><span data-stu-id="f5781-111">Sometimes you want the consuming code to be able to set a value but not discover what it is.</span></span> <span data-ttu-id="f5781-112">例如，需要保護機密資料（例如社交註冊號碼或密碼），使其無法存取未設定它的任何元件。</span><span class="sxs-lookup"><span data-stu-id="f5781-112">For example, sensitive data, such as a social registration number or a password, needs to be protected from access by any component that did not set it.</span></span> <span data-ttu-id="f5781-113">在這些情況下，您可以使用 `WriteOnly` 屬性來設定值。</span><span class="sxs-lookup"><span data-stu-id="f5781-113">In these cases, you can use a `WriteOnly` property to set the value.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="f5781-114">當您定義並使用 `WriteOnly` 屬性時，請考慮下列其他保護措施：</span><span class="sxs-lookup"><span data-stu-id="f5781-114">When you define and use a `WriteOnly` property, consider the following additional protective measures:</span></span>  
  
- <span data-ttu-id="f5781-115">**覆寫.**</span><span class="sxs-lookup"><span data-stu-id="f5781-115">**Overriding.**</span></span> <span data-ttu-id="f5781-116">如果屬性是類別的成員，則允許它預設為[NotOverridable](notoverridable.md)，而且不會將它宣告為 `Overridable` 或 `MustOverride` 。</span><span class="sxs-lookup"><span data-stu-id="f5781-116">If the property is a member of a class, allow it to default to [NotOverridable](notoverridable.md), and do not declare it `Overridable` or `MustOverride`.</span></span> <span data-ttu-id="f5781-117">這可防止衍生類別透過覆寫進行不想要的存取。</span><span class="sxs-lookup"><span data-stu-id="f5781-117">This prevents a derived class from making undesired access through an override.</span></span>  
  
- <span data-ttu-id="f5781-118">**存取層級。**</span><span class="sxs-lookup"><span data-stu-id="f5781-118">**Access Level.**</span></span> <span data-ttu-id="f5781-119">如果您將屬性的機密資料保存在一或多個變數中，請將其宣告為[私](private.md)用，讓其他程式碼都不能存取它們。</span><span class="sxs-lookup"><span data-stu-id="f5781-119">If you hold the property's sensitive data in one or more variables, declare them [Private](private.md) so that no other code can access them.</span></span>  
  
- <span data-ttu-id="f5781-120">**加密.**</span><span class="sxs-lookup"><span data-stu-id="f5781-120">**Encryption.**</span></span> <span data-ttu-id="f5781-121">以加密格式儲存所有機密資料，而不是純文字。</span><span class="sxs-lookup"><span data-stu-id="f5781-121">Store all sensitive data in encrypted form rather than in plain text.</span></span> <span data-ttu-id="f5781-122">如果惡意程式碼以某種方式取得該記憶體區域的存取權，就比較難以利用資料。</span><span class="sxs-lookup"><span data-stu-id="f5781-122">If malicious code somehow gains access to that area of memory, it is more difficult to make use of the data.</span></span> <span data-ttu-id="f5781-123">如果需要將敏感性資料序列化，加密也很有用。</span><span class="sxs-lookup"><span data-stu-id="f5781-123">Encryption is also useful if it is necessary to serialize the sensitive data.</span></span>  
  
- <span data-ttu-id="f5781-124">**重設.**</span><span class="sxs-lookup"><span data-stu-id="f5781-124">**Resetting.**</span></span> <span data-ttu-id="f5781-125">當定義屬性的類別、結構或模組被終止時，會將敏感性資料重設為預設值或其他無意義的值。</span><span class="sxs-lookup"><span data-stu-id="f5781-125">When the class, structure, or module defining the property is being terminated, reset the sensitive data to default values or to other meaningless values.</span></span> <span data-ttu-id="f5781-126">當釋放該記憶體區域以供一般存取時，這會提供額外的保護。</span><span class="sxs-lookup"><span data-stu-id="f5781-126">This gives extra protection when that area of memory is freed for general access.</span></span>  
  
- <span data-ttu-id="f5781-127">**暫.**</span><span class="sxs-lookup"><span data-stu-id="f5781-127">**Persistence.**</span></span> <span data-ttu-id="f5781-128">請勿保存任何機密資料（例如，在磁片上），如果您可以避免它。</span><span class="sxs-lookup"><span data-stu-id="f5781-128">Do not persist any sensitive data, for example on disk, if you can avoid it.</span></span> <span data-ttu-id="f5781-129">此外，請勿將任何敏感性資料寫入剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="f5781-129">Also, do not write any sensitive data to the Clipboard.</span></span>  
  
 <span data-ttu-id="f5781-130">`WriteOnly`修飾詞可以在此內容中使用：</span><span class="sxs-lookup"><span data-stu-id="f5781-130">The `WriteOnly` modifier can be used in this context:</span></span>  
  
 [<span data-ttu-id="f5781-131">Property Statement</span><span class="sxs-lookup"><span data-stu-id="f5781-131">Property Statement</span></span>](../statements/property-statement.md)  
  
## <a name="see-also"></a><span data-ttu-id="f5781-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f5781-132">See also</span></span>

- [<span data-ttu-id="f5781-133">唯讀</span><span class="sxs-lookup"><span data-stu-id="f5781-133">ReadOnly</span></span>](readonly.md)
- [<span data-ttu-id="f5781-134">私用</span><span class="sxs-lookup"><span data-stu-id="f5781-134">Private</span></span>](private.md)
- [<span data-ttu-id="f5781-135">關鍵字</span><span class="sxs-lookup"><span data-stu-id="f5781-135">Keywords</span></span>](../keywords/index.md)
