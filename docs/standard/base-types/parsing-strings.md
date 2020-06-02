---
title: 在 .NET 中剖析字串
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parsing strings, about parsing strings
- IFormatProvider interface, parsing strings
- base types, parsing strings
- Parse method
- parsing strings
ms.assetid: 5e758b41-db93-456b-8999-99b7304b090d
ms.openlocfilehash: ab446a8f868cabdeff73d1b72e1399b7c2beb1e1
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84277410"
---
# <a name="parsing-strings-in-net"></a><span data-ttu-id="053b4-102">在 .NET 中剖析字串</span><span class="sxs-lookup"><span data-stu-id="053b4-102">Parsing Strings in .NET</span></span>
<span data-ttu-id="053b4-103">剖析作業會將代表 .NET 基底類型的字串轉換成該基底類型。</span><span class="sxs-lookup"><span data-stu-id="053b4-103">A parsing operation converts a string that represents a .NET base type into that base type.</span></span> <span data-ttu-id="053b4-104">例如，剖析作業用來將字串轉換為浮點數或日期和時間值。</span><span class="sxs-lookup"><span data-stu-id="053b4-104">For example, a parsing operation is used to convert a string to a floating-point number or to a date and time value.</span></span> <span data-ttu-id="053b4-105">最常用來執行剖析作業的方法是 `Parse` 方法。</span><span class="sxs-lookup"><span data-stu-id="053b4-105">The method most commonly used to perform a parsing operation is the `Parse` method.</span></span> <span data-ttu-id="053b4-106">因為剖析是格式設定的反向作業 (這牽涉到將基底類型別轉換成其字串表示)，所以會套用許多相同的規則和慣例。</span><span class="sxs-lookup"><span data-stu-id="053b4-106">Because parsing is the reverse operation of formatting (which involves converting a base type into its string representation), many of the same rules and conventions apply.</span></span> <span data-ttu-id="053b4-107">就像格式化會使用實作 <xref:System.IFormatProvider> 介面的物件來提供區分文化特性的格式化資訊，剖析也會使用實作 <xref:System.IFormatProvider> 介面的物件來判斷如何解譯字串表示。</span><span class="sxs-lookup"><span data-stu-id="053b4-107">Just as formatting uses an object that implements the <xref:System.IFormatProvider> interface to provide culture-sensitive formatting information, parsing also uses an object that implements the <xref:System.IFormatProvider> interface to determine how to interpret a string representation.</span></span> <span data-ttu-id="053b4-108">如需詳細資訊，請參閱[格式類型](formatting-types.md)。</span><span class="sxs-lookup"><span data-stu-id="053b4-108">For more information, see [Formatting Types](formatting-types.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="053b4-109">本節內容</span><span class="sxs-lookup"><span data-stu-id="053b4-109">In This Section</span></span>  
 [<span data-ttu-id="053b4-110">剖析數值字串</span><span class="sxs-lookup"><span data-stu-id="053b4-110">Parsing Numeric Strings</span></span>](parsing-numeric.md)  
 <span data-ttu-id="053b4-111">描述如何將字串轉換成 .NET 數值類型。</span><span class="sxs-lookup"><span data-stu-id="053b4-111">Describes how to convert strings into .NET numeric types.</span></span>  
  
 [<span data-ttu-id="053b4-112">剖析日期和時間字串</span><span class="sxs-lookup"><span data-stu-id="053b4-112">Parsing Date and Time Strings</span></span>](parsing-datetime.md)  
 <span data-ttu-id="053b4-113">描述如何將字串轉換成 .NET **DateTime** 類型。</span><span class="sxs-lookup"><span data-stu-id="053b4-113">Describes how to convert strings into .NET **DateTime** types.</span></span>  
  
 [<span data-ttu-id="053b4-114">剖析其他字串</span><span class="sxs-lookup"><span data-stu-id="053b4-114">Parsing Other Strings</span></span>](parsing-other.md)  
 <span data-ttu-id="053b4-115">描述如何將字串轉換成 **Char**、**Boolean** 和 **Enum** 類型。</span><span class="sxs-lookup"><span data-stu-id="053b4-115">Describes how to convert strings into **Char**, **Boolean**, and **Enum** types.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="053b4-116">相關章節</span><span class="sxs-lookup"><span data-stu-id="053b4-116">Related Sections</span></span>  
 [<span data-ttu-id="053b4-117">格式化類型</span><span class="sxs-lookup"><span data-stu-id="053b4-117">Formatting Types</span></span>](formatting-types.md)  
 <span data-ttu-id="053b4-118">描述基本的格式化概念，例如格式規範和格式提供者。</span><span class="sxs-lookup"><span data-stu-id="053b4-118">Describes basic formatting concepts like format specifiers and format providers.</span></span>  
  
 [<span data-ttu-id="053b4-119">.NET 中的類型轉換</span><span class="sxs-lookup"><span data-stu-id="053b4-119">Type Conversion in .NET</span></span>](type-conversion.md)  
 <span data-ttu-id="053b4-120">描述如何轉換類型。</span><span class="sxs-lookup"><span data-stu-id="053b4-120">Describes how to convert types.</span></span>
