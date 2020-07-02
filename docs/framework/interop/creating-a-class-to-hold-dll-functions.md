---
title: 建立類別以包裝 DLL 函式
description: 在 .NET 中建立受控類別包裝函式以保存 DLL 函式，這有助於封裝平臺功能。
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- platform invoke, creating class for functions
- DLL functions
ms.assetid: e08e4c34-0223-45f7-aa55-a3d8dd979b0f
ms.openlocfilehash: b8aa0361ee5213cb947a102f903d1a7a35331f17
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622168"
---
# <a name="creating-a-class-to-hold-dll-functions"></a><span data-ttu-id="caf33-103">建立類別以包裝 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="caf33-103">Creating a Class to Hold DLL Functions</span></span>
<span data-ttu-id="caf33-104">將常用 DLL 函式包裝在 Managed 類別中，是封裝平台功能的有效方法。</span><span class="sxs-lookup"><span data-stu-id="caf33-104">Wrapping a frequently used DLL function in a managed class is an effective approach to encapsulate platform functionality.</span></span> <span data-ttu-id="caf33-105">雖然不會強制您在每個案例這麼做，但提供類別包裝函式十分方便，因為定義 DLL 函式十分麻煩又容易發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="caf33-105">Although it is not mandatory to do so in every case, providing a class wrapper is convenient because defining DLL functions can be cumbersome and error-prone.</span></span> <span data-ttu-id="caf33-106">如果您是使用 Visual Basic 或 C# 進行程式設計，則必須在類別或 Visual Basic 模組內宣告 DLL 函式。</span><span class="sxs-lookup"><span data-stu-id="caf33-106">If you are programming in Visual Basic or C#, you must declare DLL functions within a class or Visual Basic module.</span></span>  
  
 <span data-ttu-id="caf33-107">在類別內，您可以為每個您想要呼叫的 DLL 函式定義靜態方法。</span><span class="sxs-lookup"><span data-stu-id="caf33-107">Within a class, you define a static method for each DLL function you want to call.</span></span> <span data-ttu-id="caf33-108">定義可以包含其他資訊，例如傳遞方法引數時所使用的字元集或呼叫慣例；略過這項資訊，即可選取預設設定。</span><span class="sxs-lookup"><span data-stu-id="caf33-108">The definition can include additional information, such as the character set or the calling convention used in passing method arguments; by omitting this information, you select the default settings.</span></span> <span data-ttu-id="caf33-109">如需宣告選項和其預設設定的完整清單，請參閱[在 Managed 程式碼中建立原型](creating-prototypes-in-managed-code.md)。</span><span class="sxs-lookup"><span data-stu-id="caf33-109">For a complete list of declaration options and their default settings, see [Creating Prototypes in Managed Code](creating-prototypes-in-managed-code.md).</span></span>  
  
 <span data-ttu-id="caf33-110">包裝之後，即可在對任何其他類別呼叫靜態方法時，於類別上呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="caf33-110">Once wrapped, you can call the methods on the class as you call static methods on any other class.</span></span> <span data-ttu-id="caf33-111">平台叫用會自動處理基礎匯出的函式。</span><span class="sxs-lookup"><span data-stu-id="caf33-111">Platform invoke handles the underlying exported function automatically.</span></span>  
  
 <span data-ttu-id="caf33-112">設計平台叫用的 Managed 類別時，請考慮類別與 DLL 函式之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="caf33-112">When designing a managed class for platform invoke, consider the relationships between classes and DLL functions.</span></span> <span data-ttu-id="caf33-113">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="caf33-113">For example, you can:</span></span>  
  
- <span data-ttu-id="caf33-114">在現有類別內，宣告 DLL 函式。</span><span class="sxs-lookup"><span data-stu-id="caf33-114">Declare DLL functions within an existing class.</span></span>  
  
- <span data-ttu-id="caf33-115">建立每個 DLL 函式的個別類別，來隔離函式，以及輕鬆找到函式。</span><span class="sxs-lookup"><span data-stu-id="caf33-115">Create an individual class for each DLL function, keeping functions isolated and easy to find.</span></span>  
  
- <span data-ttu-id="caf33-116">為一組相關 DLL 函式建立一個類別，以形成邏輯群組，並減少額外負荷。</span><span class="sxs-lookup"><span data-stu-id="caf33-116">Create one class for a set of related DLL functions to form logical groupings and reduce overhead.</span></span>  
  
 <span data-ttu-id="caf33-117">您可以依需要命名類別和其方法。</span><span class="sxs-lookup"><span data-stu-id="caf33-117">You can name the class and its methods as you please.</span></span> <span data-ttu-id="caf33-118">如需示範如何建構要與平台叫用搭配使用之 .NET 型宣告的範例，請參閱[使用平台叫用封送處理資料](marshaling-data-with-platform-invoke.md)。</span><span class="sxs-lookup"><span data-stu-id="caf33-118">For examples that demonstrate how to construct .NET-based declarations to be used with platform invoke, see [Marshaling Data with Platform Invoke](marshaling-data-with-platform-invoke.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="caf33-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="caf33-119">See also</span></span>

- [<span data-ttu-id="caf33-120">使用 Unmanaged DLL 函式</span><span class="sxs-lookup"><span data-stu-id="caf33-120">Consuming Unmanaged DLL Functions</span></span>](consuming-unmanaged-dll-functions.md)
- [<span data-ttu-id="caf33-121">識別 DLL 中的函式</span><span class="sxs-lookup"><span data-stu-id="caf33-121">Identifying Functions in DLLs</span></span>](identifying-functions-in-dlls.md)
- [<span data-ttu-id="caf33-122">在 Managed 程式碼中建立原型</span><span class="sxs-lookup"><span data-stu-id="caf33-122">Creating Prototypes in Managed Code</span></span>](creating-prototypes-in-managed-code.md)
- [<span data-ttu-id="caf33-123">呼叫 DLL 函式</span><span class="sxs-lookup"><span data-stu-id="caf33-123">Calling a DLL Function</span></span>](calling-a-dll-function.md)
