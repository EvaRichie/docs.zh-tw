---
title: 結構變數
ms.date: 07/20/2015
helpviewer_keywords:
- structures [Visual Basic], variables
- structures [Visual Basic], structure variables
- variables [Visual Basic], structure variables
- structure variables [Visual Basic]
ms.assetid: 156872f8-aabc-4454-8e2d-f2253c3c13c9
ms.openlocfilehash: 270e8ca26185e4a68def3b95f4ce6ab4c57a629c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393581"
---
# <a name="structure-variables-visual-basic"></a><span data-ttu-id="d6622-102">結構變數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d6622-102">Structure Variables (Visual Basic)</span></span>

<span data-ttu-id="d6622-103">建立結構之後，您可以將程式層級和模組層級變數宣告為該類型。</span><span class="sxs-lookup"><span data-stu-id="d6622-103">Once you have created a structure, you can declare procedure-level and module-level variables as that type.</span></span> <span data-ttu-id="d6622-104">例如，您可以建立一個結構來記錄電腦系統的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d6622-104">For example, you can create a structure that records information about a computer system.</span></span> <span data-ttu-id="d6622-105">下列範例示範此作業。</span><span class="sxs-lookup"><span data-stu-id="d6622-105">The following example demonstrates this.</span></span>

```vb
Public Structure systemInfo
    Public cPU As String
    Public memory As Long
    Public purchaseDate As Date
End Structure
```

<span data-ttu-id="d6622-106">您現在可以宣告該類型的變數。</span><span class="sxs-lookup"><span data-stu-id="d6622-106">You can now declare variables of that type.</span></span> <span data-ttu-id="d6622-107">下列宣告說明這種情況。</span><span class="sxs-lookup"><span data-stu-id="d6622-107">The following declaration illustrates this.</span></span>

```vb
Dim mySystem, yourSystem As systemInfo
```

> [!NOTE]
> <span data-ttu-id="d6622-108">在類別和模組中，使用[Dim 語句](../../../language-reference/statements/dim-statement.md)宣告的結構會預設為公用存取。</span><span class="sxs-lookup"><span data-stu-id="d6622-108">In classes and modules, structures declared using the [Dim Statement](../../../language-reference/statements/dim-statement.md) default to public access.</span></span> <span data-ttu-id="d6622-109">如果您想要將結構設為私用，請務必使用[private](../../../language-reference/modifiers/private.md)關鍵字來宣告。</span><span class="sxs-lookup"><span data-stu-id="d6622-109">If you intend a structure to be private, make sure you declare it using the [Private](../../../language-reference/modifiers/private.md) keyword.</span></span>

## <a name="access-to-structure-values"></a><span data-ttu-id="d6622-110">結構值的存取權</span><span class="sxs-lookup"><span data-stu-id="d6622-110">Access to Structure Values</span></span>

<span data-ttu-id="d6622-111">若要從結構變數的元素指派和抓取值，您可以使用與用來設定和取得物件屬性的相同語法。</span><span class="sxs-lookup"><span data-stu-id="d6622-111">To assign and retrieve values from the elements of a structure variable, you use the same syntax as you use to set and get properties on an object.</span></span> <span data-ttu-id="d6622-112">您可以將成員存取運算子（ `.` ）放在結構變數名稱和元素名稱之間。</span><span class="sxs-lookup"><span data-stu-id="d6622-112">You place the member access operator (`.`) between the structure variable name and the element name.</span></span> <span data-ttu-id="d6622-113">下列範例會存取先前宣告為類型之變數的元素 `systemInfo` 。</span><span class="sxs-lookup"><span data-stu-id="d6622-113">The following example accesses elements of the variables previously declared as type `systemInfo`.</span></span>

```vb
mySystem.cPU = "486"
Dim tooOld As Boolean
If yourSystem.purchaseDate < #1/1/1992# Then tooOld = True
```

## <a name="assigning-structure-variables"></a><span data-ttu-id="d6622-114">指派結構變數</span><span class="sxs-lookup"><span data-stu-id="d6622-114">Assigning Structure Variables</span></span>

<span data-ttu-id="d6622-115">如果兩者都是相同的結構類型，您也可以將一個變數指派給另一個。</span><span class="sxs-lookup"><span data-stu-id="d6622-115">You can also assign one variable to another if both are of the same structure type.</span></span> <span data-ttu-id="d6622-116">這會將一個結構的所有專案複製到另一個結構中的對應元素。</span><span class="sxs-lookup"><span data-stu-id="d6622-116">This copies all the elements of one structure to the corresponding elements in the other.</span></span> <span data-ttu-id="d6622-117">下列宣告說明這種情況。</span><span class="sxs-lookup"><span data-stu-id="d6622-117">The following declaration illustrates this.</span></span>

```vb
yourSystem = mySystem
```

<span data-ttu-id="d6622-118">如果結構專案是參考型別（例如 `String` 、 `Object` 或陣列），則會複製資料的指標。</span><span class="sxs-lookup"><span data-stu-id="d6622-118">If a structure element is a reference type, such as a `String`, `Object`, or array, the pointer to the data is copied.</span></span> <span data-ttu-id="d6622-119">在上述範例中，如果 `systemInfo` 已包含物件變數，則先前的範例會將的指標從複製 `mySystem` 到 `yourSystem` ，而透過某個結構的物件資料變更會在透過其他結構存取時生效。</span><span class="sxs-lookup"><span data-stu-id="d6622-119">In the previous example, if `systemInfo` had included an object variable, then the preceding example would have copied the pointer from `mySystem` to `yourSystem`, and a change to the object's data through one structure would be in effect when accessed through the other structure.</span></span>

## <a name="see-also"></a><span data-ttu-id="d6622-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d6622-120">See also</span></span>

- [<span data-ttu-id="d6622-121">資料類型</span><span class="sxs-lookup"><span data-stu-id="d6622-121">Data Types</span></span>](index.md)
- [<span data-ttu-id="d6622-122">基礎資料類型</span><span class="sxs-lookup"><span data-stu-id="d6622-122">Elementary Data Types</span></span>](elementary-data-types.md)
- [<span data-ttu-id="d6622-123">複合資料類型</span><span class="sxs-lookup"><span data-stu-id="d6622-123">Composite Data Types</span></span>](composite-data-types.md)
- [<span data-ttu-id="d6622-124">Value Types and Reference Types</span><span class="sxs-lookup"><span data-stu-id="d6622-124">Value Types and Reference Types</span></span>](value-types-and-reference-types.md)
- [<span data-ttu-id="d6622-125">結構</span><span class="sxs-lookup"><span data-stu-id="d6622-125">Structures</span></span>](structures.md)
- [<span data-ttu-id="d6622-126">疑難排解資料類型的問題</span><span class="sxs-lookup"><span data-stu-id="d6622-126">Troubleshooting Data Types</span></span>](troubleshooting-data-types.md)
- [<span data-ttu-id="d6622-127">作法：宣告結構</span><span class="sxs-lookup"><span data-stu-id="d6622-127">How to: Declare a Structure</span></span>](how-to-declare-a-structure.md)
- [<span data-ttu-id="d6622-128">結構與其他程式設計項目</span><span class="sxs-lookup"><span data-stu-id="d6622-128">Structures and Other Programming Elements</span></span>](structures-and-other-programming-elements.md)
- [<span data-ttu-id="d6622-129">結構與類別</span><span class="sxs-lookup"><span data-stu-id="d6622-129">Structures and Classes</span></span>](structures-and-classes.md)
- [<span data-ttu-id="d6622-130">Structure 陳述式</span><span class="sxs-lookup"><span data-stu-id="d6622-130">Structure Statement</span></span>](../../../language-reference/statements/structure-statement.md)
