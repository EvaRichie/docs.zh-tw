---
title: 結構與其他程式設計項目
ms.date: 07/20/2015
helpviewer_keywords:
- structures [Visual Basic], arrays
- procedures [Visual Basic], structures as arguments to
- objects [Visual Basic], structure elements
- arrays [Visual Basic], structure elements
- nested structures [Visual Basic]
ms.assetid: 0f849313-ccd2-4c9a-acb9-69de6751c088
ms.openlocfilehash: dbd24065a954e5611663963371d5a9f4bbbaea68
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393490"
---
# <a name="structures-and-other-programming-elements-visual-basic"></a><span data-ttu-id="1d14f-102">結構和其他程式設計項目 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1d14f-102">Structures and Other Programming Elements (Visual Basic)</span></span>
<span data-ttu-id="1d14f-103">您可以搭配使用結構與陣列、物件和程式，以及彼此結合。</span><span class="sxs-lookup"><span data-stu-id="1d14f-103">You can use structures in conjunction with arrays, objects, and procedures, as well as with each other.</span></span> <span data-ttu-id="1d14f-104">互動會使用與這些元素個別使用相同的語法。</span><span class="sxs-lookup"><span data-stu-id="1d14f-104">The interactions use the same syntax as these elements use individually.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="1d14f-105">您無法初始化結構宣告中的任何結構元素。</span><span class="sxs-lookup"><span data-stu-id="1d14f-105">You cannot initialize any of the structure elements in the structure declaration.</span></span> <span data-ttu-id="1d14f-106">您只能將值指派給已宣告為結構類型之變數的元素。</span><span class="sxs-lookup"><span data-stu-id="1d14f-106">You can assign values only to elements of a variable that has been declared to be of a structure type.</span></span>  
  
## <a name="structures-and-arrays"></a><span data-ttu-id="1d14f-107">結構和陣列</span><span class="sxs-lookup"><span data-stu-id="1d14f-107">Structures and Arrays</span></span>  
 <span data-ttu-id="1d14f-108">結構可以包含陣列做為它的一個或多個元素。</span><span class="sxs-lookup"><span data-stu-id="1d14f-108">A structure can contain an array as one or more of its elements.</span></span> <span data-ttu-id="1d14f-109">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-109">The following example illustrates this.</span></span>  
  
```vb  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As String  
    Public purchaseDate As Date  
End Structure
```  
  
 <span data-ttu-id="1d14f-110">在結構中存取陣列的值，與存取物件上屬性的方式相同。</span><span class="sxs-lookup"><span data-stu-id="1d14f-110">You access the values of an array within a structure the same way you access a property on an object.</span></span> <span data-ttu-id="1d14f-111">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-111">The following example illustrates this.</span></span>  
  
```vb  
Dim mySystem As systemInfo  
ReDim mySystem.diskDrives(3)  
mySystem.diskDrives(0) = "1.44 MB"  
```  
  
 <span data-ttu-id="1d14f-112">您也可以宣告結構的陣列。</span><span class="sxs-lookup"><span data-stu-id="1d14f-112">You can also declare an array of structures.</span></span> <span data-ttu-id="1d14f-113">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-113">The following example illustrates this.</span></span>  
  
```vb  
Dim allSystems(100) As systemInfo  
```  
  
 <span data-ttu-id="1d14f-114">您會遵循相同的規則來存取此資料結構的元件。</span><span class="sxs-lookup"><span data-stu-id="1d14f-114">You follow the same rules to access the components of this data architecture.</span></span> <span data-ttu-id="1d14f-115">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-115">The following example illustrates this.</span></span>  
  
```vb  
ReDim allSystems(5).diskDrives(3)  
allSystems(5).CPU = "386SX"  
allSystems(5).diskDrives(2) = "100M SCSI"  
```  
  
## <a name="structures-and-objects"></a><span data-ttu-id="1d14f-116">結構和物件</span><span class="sxs-lookup"><span data-stu-id="1d14f-116">Structures and Objects</span></span>  
 <span data-ttu-id="1d14f-117">結構可以包含物件做為其一個或多個元素。</span><span class="sxs-lookup"><span data-stu-id="1d14f-117">A structure can contain an object as one or more of its elements.</span></span> <span data-ttu-id="1d14f-118">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-118">The following example illustrates this.</span></span>  
  
```vb  
Protected Structure userInput  
    Public userName As String  
    Public inputForm As System.Windows.Forms.Form  
    Public userFileNumber As Integer  
End Structure  
```  
  
 <span data-ttu-id="1d14f-119">您應該在這類宣告中使用特定的物件類別，而不是 `Object` 。</span><span class="sxs-lookup"><span data-stu-id="1d14f-119">You should use a specific object class in such a declaration, rather than `Object`.</span></span>  
  
## <a name="structures-and-procedures"></a><span data-ttu-id="1d14f-120">結構和程式</span><span class="sxs-lookup"><span data-stu-id="1d14f-120">Structures and Procedures</span></span>  
 <span data-ttu-id="1d14f-121">您可以將結構當做程式引數來傳遞。</span><span class="sxs-lookup"><span data-stu-id="1d14f-121">You can pass a structure as a procedure argument.</span></span> <span data-ttu-id="1d14f-122">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-122">The following example illustrates this.</span></span>  
  
```vb  
Public currentCPUName As String = "700MHz Pentium compatible"  
Public currentMemorySize As Long = 256  
Public Sub fillSystem(ByRef someSystem As systemInfo)  
    someSystem.cPU = currentCPUName  
    someSystem.memory = currentMemorySize  
    someSystem.purchaseDate = Now  
End Sub  
```  
  
 <span data-ttu-id="1d14f-123">上述範例會以傳*址方式*傳遞結構，讓程式可以修改其專案，讓變更在呼叫程式碼中生效。</span><span class="sxs-lookup"><span data-stu-id="1d14f-123">The preceding example passes the structure *by reference*, which allows the procedure to modify its elements so that the changes take effect in the calling code.</span></span> <span data-ttu-id="1d14f-124">如果您想要針對這類修改來保護結構，請以傳值方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="1d14f-124">If you want to protect a structure against such modification, pass it by value.</span></span>  
  
 <span data-ttu-id="1d14f-125">您也可以從程式傳回結構 `Function` 。</span><span class="sxs-lookup"><span data-stu-id="1d14f-125">You can also return a structure from a `Function` procedure.</span></span> <span data-ttu-id="1d14f-126">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-126">The following example illustrates this.</span></span>  
  
```vb  
Dim allSystems(100) As systemInfo  
Function findByDate(ByVal searchDate As Date) As systemInfo  
    Dim i As Integer  
    For i = 1 To 100  
        If allSystems(i).purchaseDate = searchDate Then Return allSystems(i)  
    Next i  
   ' Process error: system with desired purchase date not found.  
End Function  
```  
  
## <a name="structures-within-structures"></a><span data-ttu-id="1d14f-127">結構內的結構</span><span class="sxs-lookup"><span data-stu-id="1d14f-127">Structures Within Structures</span></span>  
 <span data-ttu-id="1d14f-128">結構可以包含其他結構。</span><span class="sxs-lookup"><span data-stu-id="1d14f-128">Structures can contain other structures.</span></span> <span data-ttu-id="1d14f-129">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1d14f-129">The following example illustrates this.</span></span>  
  
```vb  
Public Structure driveInfo  
    Public type As String  
    Public size As Long  
End Structure  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As driveInfo  
    Public purchaseDate As Date  
End Structure  
```  
  
```vb  
Dim allSystems(100) As systemInfo  
ReDim allSystems(1).diskDrives(3)  
allSystems(1).diskDrives(0).type = "Floppy"  
```  
  
 <span data-ttu-id="1d14f-130">您也可以使用這項技術，將一個模組中定義的結構封裝在不同模組中定義的結構內。</span><span class="sxs-lookup"><span data-stu-id="1d14f-130">You can also use this technique to encapsulate a structure defined in one module within a structure defined in a different module.</span></span>  
  
 <span data-ttu-id="1d14f-131">結構可以包含任意深度的其他結構。</span><span class="sxs-lookup"><span data-stu-id="1d14f-131">Structures can contain other structures to an arbitrary depth.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1d14f-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d14f-132">See also</span></span>

- [<span data-ttu-id="1d14f-133">資料類型</span><span class="sxs-lookup"><span data-stu-id="1d14f-133">Data Types</span></span>](index.md)
- [<span data-ttu-id="1d14f-134">基礎資料類型</span><span class="sxs-lookup"><span data-stu-id="1d14f-134">Elementary Data Types</span></span>](elementary-data-types.md)
- [<span data-ttu-id="1d14f-135">複合資料類型</span><span class="sxs-lookup"><span data-stu-id="1d14f-135">Composite Data Types</span></span>](composite-data-types.md)
- [<span data-ttu-id="1d14f-136">Value Types and Reference Types</span><span class="sxs-lookup"><span data-stu-id="1d14f-136">Value Types and Reference Types</span></span>](value-types-and-reference-types.md)
- [<span data-ttu-id="1d14f-137">結構</span><span class="sxs-lookup"><span data-stu-id="1d14f-137">Structures</span></span>](structures.md)
- [<span data-ttu-id="1d14f-138">疑難排解資料類型的問題</span><span class="sxs-lookup"><span data-stu-id="1d14f-138">Troubleshooting Data Types</span></span>](troubleshooting-data-types.md)
- [<span data-ttu-id="1d14f-139">作法：宣告結構</span><span class="sxs-lookup"><span data-stu-id="1d14f-139">How to: Declare a Structure</span></span>](how-to-declare-a-structure.md)
- [<span data-ttu-id="1d14f-140">結構變數</span><span class="sxs-lookup"><span data-stu-id="1d14f-140">Structure Variables</span></span>](structure-variables.md)
- [<span data-ttu-id="1d14f-141">結構與類別</span><span class="sxs-lookup"><span data-stu-id="1d14f-141">Structures and Classes</span></span>](structures-and-classes.md)
- [<span data-ttu-id="1d14f-142">Structure 陳述式</span><span class="sxs-lookup"><span data-stu-id="1d14f-142">Structure Statement</span></span>](../../../language-reference/statements/structure-statement.md)
