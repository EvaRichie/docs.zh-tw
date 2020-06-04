---
title: 自動實作的屬性
ms.date: 07/20/2015
f1_keywords:
- vb.AutoProperty
- vb.AutoImplementedProperty
helpviewer_keywords:
- properties [Visual Basic], auto-implemented
- auto-implemented properties [Visual Basic]
ms.assetid: 5c669f0b-cf95-4b4e-ae84-9cc55212ca87
ms.openlocfilehash: d991a385e537c43daeb708e96e712acd92110379
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403378"
---
# <a name="auto-implemented-properties-visual-basic"></a><span data-ttu-id="c68f6-102">自動實作的屬性 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c68f6-102">Auto-Implemented Properties (Visual Basic)</span></span>
<span data-ttu-id="c68f6-103">*自動執行的屬性*可讓您快速指定類別的屬性，而不需要將程式碼寫入 `Get` 和 `Set` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-103">*Auto-implemented properties* enable you to quickly specify a property of a class without having to write code to `Get` and `Set` the property.</span></span> <span data-ttu-id="c68f6-104">當您撰寫自動實作屬性之程式碼時，Visual Basic 編譯器會自動建立私用欄位，來存放建立關聯的 `Get` 和 `Set` 程序外，另外存放屬性變數。</span><span class="sxs-lookup"><span data-stu-id="c68f6-104">When you write code for an auto-implemented property, the Visual Basic compiler automatically creates a private field to store the property variable in addition to creating the associated `Get` and `Set` procedures.</span></span>  
  
 <span data-ttu-id="c68f6-105">使用自動實作屬性、屬性 (包括預設值)，可以在單行中宣告。</span><span class="sxs-lookup"><span data-stu-id="c68f6-105">With auto-implemented properties, a property, including a default value, can be declared in a single line.</span></span> <span data-ttu-id="c68f6-106">下列範例顯示三個屬性宣告。</span><span class="sxs-lookup"><span data-stu-id="c68f6-106">The following example shows three property declarations.</span></span>  
  
 [!code-vb[VbVbalrAutoImplementedProperties#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#1)]  
  
 <span data-ttu-id="c68f6-107">自動實作屬性相當於屬性值儲存在私用欄位的屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-107">An auto-implemented property is equivalent to a property for which the property value is stored in a private field.</span></span> <span data-ttu-id="c68f6-108">下列程式碼範例顯示自動實作屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-108">The following code example shows an auto-implemented property.</span></span>  
  
 [!code-vb[VbVbalrAutoImplementedProperties#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#5)]  
  
 <span data-ttu-id="c68f6-109">下列程式碼範例顯示先前的自動實作屬性範例的對等程式碼。</span><span class="sxs-lookup"><span data-stu-id="c68f6-109">The following code example shows the equivalent code for the previous auto-implemented property example.</span></span>  
  
 [!code-vb[VbVbalrAutoImplementedProperties#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#2)]  
  
 <span data-ttu-id="c68f6-110">下列程式碼會示範唯讀屬性實作：</span><span class="sxs-lookup"><span data-stu-id="c68f6-110">The following code show implementing readonly properties:</span></span>  
  
```vb  
Class Customer  
   Public ReadOnly Property Tags As New List(Of String)  
   Public ReadOnly Property Name As String = ""  
   Public ReadOnly Property File As String  
  
   Sub New(file As String)  
      Me.File = file  
   End Sub  
End Class  
```  
  
 <span data-ttu-id="c68f6-111">如範例所示，您可以使用初始化運算式指派給屬性，或在包含類型的建構函式中指派給屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-111">You can assign to the property with initialization expressions as shown in the example, or you can assign to the properties in the containing type’s constructor.</span></span>  <span data-ttu-id="c68f6-112">您可以在任何時間指派給唯讀屬性的支援欄位。</span><span class="sxs-lookup"><span data-stu-id="c68f6-112">You can assign to the backing fields of readonly properties at any time.</span></span>  
  
## <a name="backing-field"></a><span data-ttu-id="c68f6-113">支援欄位</span><span class="sxs-lookup"><span data-stu-id="c68f6-113">Backing Field</span></span>  
 <span data-ttu-id="c68f6-114">當您宣告自動執行的屬性時，Visual Basic 會自動建立一個隱藏的私用欄位，稱為*支援欄位*以包含屬性值。</span><span class="sxs-lookup"><span data-stu-id="c68f6-114">When you declare an auto-implemented property, Visual Basic automatically creates a hidden private field called the *backing field* to contain the property value.</span></span> <span data-ttu-id="c68f6-115">支援欄位名稱是自動實作屬性名稱前面加上底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="c68f6-115">The backing field name is the auto-implemented property name preceded by an underscore (_).</span></span> <span data-ttu-id="c68f6-116">例如，如果您宣告名為 `ID` 的自動實作屬性，會將支援欄位命名為 `_ID`。</span><span class="sxs-lookup"><span data-stu-id="c68f6-116">For example, if you declare an auto-implemented property named `ID`, the backing field is named `_ID`.</span></span> <span data-ttu-id="c68f6-117">如果包含也命名為 `_ID` 的成員類別，則會產生名稱衝突，且 Visual Basic 將報告編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="c68f6-117">If you include a member of your class that is also named `_ID`, you produce a naming conflict and Visual Basic reports a compiler error.</span></span>  
  
 <span data-ttu-id="c68f6-118">支援欄位也具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="c68f6-118">The backing field also has the following characteristics:</span></span>  
  
- <span data-ttu-id="c68f6-119">支援欄位的存取修飾詞一律為 `Private`，即使屬性本身有不同的存取層級，例如 `Public`。</span><span class="sxs-lookup"><span data-stu-id="c68f6-119">The access modifier for the backing field is always `Private`, even when the property itself has a different access level, such as `Public`.</span></span>  
  
- <span data-ttu-id="c68f6-120">如果屬性標記為 `Shared`，支援欄位也會共用。</span><span class="sxs-lookup"><span data-stu-id="c68f6-120">If the property is marked as `Shared`, the backing field also is shared.</span></span>  
  
- <span data-ttu-id="c68f6-121">為屬性所指定的屬性並不適用於支援欄位。</span><span class="sxs-lookup"><span data-stu-id="c68f6-121">Attributes specified for the property do not apply to the backing field.</span></span>  
  
- <span data-ttu-id="c68f6-122">可從類別內的程式碼，和從偵錯工具 (例如 [監看式] 視窗) 中存取的支援欄位。</span><span class="sxs-lookup"><span data-stu-id="c68f6-122">The backing field can be accessed from code within the class and from debugging tools such as the Watch window.</span></span> <span data-ttu-id="c68f6-123">不過，支援欄位不會顯示在 IntelliSense 文字自動完成清單中。</span><span class="sxs-lookup"><span data-stu-id="c68f6-123">However, the backing field does not show in an IntelliSense word completion list.</span></span>  
  
## <a name="initializing-an-auto-implemented-property"></a><span data-ttu-id="c68f6-124">初始化自動實作屬性</span><span class="sxs-lookup"><span data-stu-id="c68f6-124">Initializing an Auto-Implemented Property</span></span>  
 <span data-ttu-id="c68f6-125">任何可以用來初始化欄位的運算式，對初始化自動實作屬性都是有效的。</span><span class="sxs-lookup"><span data-stu-id="c68f6-125">Any expression that can be used to initialize a field is valid for initializing an auto-implemented property.</span></span> <span data-ttu-id="c68f6-126">當您初始化自動實作屬性時，會評估運算式，並傳遞給屬性的 `Set` 程序。</span><span class="sxs-lookup"><span data-stu-id="c68f6-126">When you initialize an auto-implemented property, the expression is evaluated and passed to the `Set` procedure for the property.</span></span> <span data-ttu-id="c68f6-127">下列程式碼範例會顯示一些包括起始值的自動實作屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-127">The following code examples show some auto-implemented properties that include initial values.</span></span>  
  
 [!code-vb[VbVbalrAutoImplementedProperties#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#3)]  
  
 <span data-ttu-id="c68f6-128">無法初始化 `Interface`，或標示為 `MustOverride` 的自動實作屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-128">You cannot initialize an auto-implemented property that is a member of an `Interface`, or one that is marked `MustOverride`.</span></span>  
  
 <span data-ttu-id="c68f6-129">當您將自動實作屬性宣告為 `Structure` 的成員時，如果它標示為 `Shared`，您只能初始化自動實作屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-129">When you declare an auto-implemented property as a member of a `Structure`, you can only initialize the auto-implemented property if it is marked as `Shared`.</span></span>  
  
 <span data-ttu-id="c68f6-130">當您將自動實作屬性宣告為陣列時，您無法指定明確的陣列界限。</span><span class="sxs-lookup"><span data-stu-id="c68f6-130">When you declare an auto-implemented property as an array, you cannot specify explicit array bounds.</span></span> <span data-ttu-id="c68f6-131">不過，您可以使用陣列初始設定式來提供值，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c68f6-131">However, you can supply a value by using an array initializer, as shown in the following examples.</span></span>  
  
 [!code-vb[VbVbalrAutoImplementedProperties#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrautoimplementedproperties/vb/module1.vb#4)]  
  
## <a name="property-definitions-that-require-standard-syntax"></a><span data-ttu-id="c68f6-132">需要標準語法的屬性定義</span><span class="sxs-lookup"><span data-stu-id="c68f6-132">Property Definitions That Require Standard Syntax</span></span>  
 <span data-ttu-id="c68f6-133">自動實作屬性很方便，並且支援許多程式設計案例。</span><span class="sxs-lookup"><span data-stu-id="c68f6-133">Auto-implemented properties are convenient and support many programming scenarios.</span></span> <span data-ttu-id="c68f6-134">不過，在某些情況下，您無法使用自動執行的屬性，而必須改為使用標準或*擴充*的屬性語法。</span><span class="sxs-lookup"><span data-stu-id="c68f6-134">However, there are situations in which you cannot use an auto-implemented property and must instead use standard, or *expanded*, property syntax.</span></span>  
  
 <span data-ttu-id="c68f6-135">如果您想要執行下列任何一項，您必須使用已展開屬性定義語法：</span><span class="sxs-lookup"><span data-stu-id="c68f6-135">You have to use expanded property-definition syntax if you want to do any one of the following:</span></span>  
  
- <span data-ttu-id="c68f6-136">將程式碼新增至屬性的 `Get` 或 `Set` 程序，例如在 `Set` 程序中用來驗證傳入值的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c68f6-136">Add code to the `Get` or `Set` procedure of a property, such as code to validate incoming values in the `Set` procedure.</span></span> <span data-ttu-id="c68f6-137">比方說，您可能想要先確認代表電話號碼的字串包含必要的數字，再設定屬性值。</span><span class="sxs-lookup"><span data-stu-id="c68f6-137">For example, you might want to verify that a string that represents a telephone number contains the required number of numerals before setting the property value.</span></span>  
  
- <span data-ttu-id="c68f6-138">指定 `Get` 和 `Set` 程序的不同協助工具。</span><span class="sxs-lookup"><span data-stu-id="c68f6-138">Specify different accessibility for the `Get` and `Set` procedure.</span></span> <span data-ttu-id="c68f6-139">比方說，您可能想要製作 `Set` 程序 `Private` 和 `Get` 程序 `Public`。</span><span class="sxs-lookup"><span data-stu-id="c68f6-139">For example, you might want to make the `Set` procedure `Private` and the `Get` procedure `Public`.</span></span>  
  
- <span data-ttu-id="c68f6-140">建立 `WriteOnly` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-140">Create properties that are `WriteOnly`.</span></span>  
  
- <span data-ttu-id="c68f6-141">使用參數化屬性 (包括 `Default` 屬性)。</span><span class="sxs-lookup"><span data-stu-id="c68f6-141">Use parameterized properties (including `Default` properties).</span></span> <span data-ttu-id="c68f6-142">若要指定屬性的參數，或指定 `Set` 程序的其他參數，您必須宣告已展開屬性。</span><span class="sxs-lookup"><span data-stu-id="c68f6-142">You must declare an expanded property in order to specify a parameter for the property, or to specify additional parameters for the `Set` procedure.</span></span>  
  
- <span data-ttu-id="c68f6-143">將屬性放在支援欄位，或變更支援欄位的存取層級。</span><span class="sxs-lookup"><span data-stu-id="c68f6-143">Place an attribute on the backing field, or change the access level of the backing field.</span></span>  
  
- <span data-ttu-id="c68f6-144">提供支援欄位的 XML 註解。</span><span class="sxs-lookup"><span data-stu-id="c68f6-144">Provide XML comments for the backing field.</span></span>  
  
## <a name="expanding-an-auto-implemented-property"></a><span data-ttu-id="c68f6-145">展開自動實作屬性</span><span class="sxs-lookup"><span data-stu-id="c68f6-145">Expanding an Auto-Implemented Property</span></span>  
 <span data-ttu-id="c68f6-146">如果您必須將自動實作屬性轉換為包含 `Get` 或 `Set` 程序的已展開屬性，Visual Basic 程式碼編輯器可以自動產生屬性的 `Get` 和 `Set` 程序和 `End Property` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c68f6-146">If you have to convert an auto-implemented property to an expanded property that contains a `Get` or `Set` procedure, the Visual Basic Code Editor can automatically generate the `Get` and `Set` procedures and `End Property` statement for the property.</span></span> <span data-ttu-id="c68f6-147">如果您將游標放在語句後面的空白行上，則會產生程式碼 `Property` ，輸入 `G` （適用于 `Get` ）或 `S` （適用于 `Set` ），然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="c68f6-147">The code is generated if you put the cursor on a blank line following the `Property` statement, type a `G` (for `Get`) or an `S` (for `Set`) and press ENTER.</span></span> <span data-ttu-id="c68f6-148">當您在 `Property` 陳述式結束時按下 ENTER，Visual Basic 程式碼編輯器會自動產生唯讀和唯寫屬性的 `Get` 或 `Set` 程序。</span><span class="sxs-lookup"><span data-stu-id="c68f6-148">The Visual Basic Code Editor automatically generates the `Get` or `Set` procedure for read-only and write-only properties when you press ENTER at the end of a `Property` statement.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c68f6-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c68f6-149">See also</span></span>

- [<span data-ttu-id="c68f6-150">如何：在 Visual Basic 中宣告及呼叫預設屬性</span><span class="sxs-lookup"><span data-stu-id="c68f6-150">How to: Declare and Call a Default Property in Visual Basic</span></span>](./how-to-declare-and-call-a-default-property.md)
- [<span data-ttu-id="c68f6-151">如何：宣告混合存取層級的屬性</span><span class="sxs-lookup"><span data-stu-id="c68f6-151">How to: Declare a Property with Mixed Access Levels</span></span>](./how-to-declare-a-property-with-mixed-access-levels.md)
- [<span data-ttu-id="c68f6-152">Property Statement</span><span class="sxs-lookup"><span data-stu-id="c68f6-152">Property Statement</span></span>](../../../language-reference/statements/property-statement.md)
- [<span data-ttu-id="c68f6-153">唯讀</span><span class="sxs-lookup"><span data-stu-id="c68f6-153">ReadOnly</span></span>](../../../language-reference/modifiers/readonly.md)
- [<span data-ttu-id="c68f6-154">WriteOnly</span><span class="sxs-lookup"><span data-stu-id="c68f6-154">WriteOnly</span></span>](../../../language-reference/modifiers/writeonly.md)
- [<span data-ttu-id="c68f6-155">物件和類別</span><span class="sxs-lookup"><span data-stu-id="c68f6-155">Objects and Classes</span></span>](../objects-and-classes/index.md)
