---
title: System.Object 方法
ms.date: 03/30/2017
ms.assetid: 5397fca0-689e-443e-802f-e1cbdc866427
ms.openlocfilehash: d2b96ca9e7bedd0e0438b47698d4b963844c92f3
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91155636"
---
# <a name="systemobject-methods"></a><span data-ttu-id="3161b-102">System.Object 方法</span><span class="sxs-lookup"><span data-stu-id="3161b-102">System.Object Methods</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="3161b-103">支援下列 <xref:System.Object> 方法。</span><span class="sxs-lookup"><span data-stu-id="3161b-103">supports the following <xref:System.Object> methods.</span></span>  
  
|||  
|-|-|  
|<xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>|<xref:System.Object.Equals%28System.Object%2CSystem.Object%29?displayProperty=nameWithType>|  
|<xref:System.Object.ToString?displayProperty=nameWithType>||  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="3161b-104">不支援下列 <xref:System.Object> 方法。</span><span class="sxs-lookup"><span data-stu-id="3161b-104">does not support the following <xref:System.Object> methods.</span></span>  
  
|||  
|-|-|  
|<xref:System.Object.GetHashCode?displayProperty=nameWithType>|<xref:System.Object.ReferenceEquals%28System.Object%2CSystem.Object%29?displayProperty=nameWithType>|  
|<xref:System.Object.MemberwiseClone?displayProperty=nameWithType>|<xref:System.Object.GetType?displayProperty=nameWithType>|  
|<span data-ttu-id="3161b-105">二進位型別 (例如 <xref:System.Object.ToString?displayProperty=nameWithType>、`BINARY`、`VARBINARY` 和 `IMAGE`) 的 `TIMESTAMP`。</span><span class="sxs-lookup"><span data-stu-id="3161b-105"><xref:System.Object.ToString?displayProperty=nameWithType> for binary types such as `BINARY`, `VARBINARY`, `IMAGE`, and `TIMESTAMP`.</span></span>||  
  
## <a name="differences-from-net"></a><span data-ttu-id="3161b-106">與 .NET 的差異</span><span class="sxs-lookup"><span data-stu-id="3161b-106">Differences from .NET</span></span>  

 <span data-ttu-id="3161b-107">Double 的輸出會 <xref:System.Object.ToString?displayProperty=nameWithType> 使用 sql `CONVERT` (NVARCHAR (30) 、 @x ，2) on sql。</span><span class="sxs-lookup"><span data-stu-id="3161b-107">The output of <xref:System.Object.ToString?displayProperty=nameWithType> for double uses SQL `CONVERT`(NVARCHAR(30), @x, 2) on SQL.</span></span> <span data-ttu-id="3161b-108">在此情況下，SQL 一律會使用 16 位數和科學記號表示法 (例如，"0.000000000000000e+000" 代表 0)。</span><span class="sxs-lookup"><span data-stu-id="3161b-108">SQL always uses 16 digits and scientific notation in this case (for example, "0.000000000000000e+000" for 0).</span></span> <span data-ttu-id="3161b-109">因此，<xref:System.Object.ToString?displayProperty=nameWithType> 轉換不會產生與 .NET Framework 中 <xref:System.Convert.ToString%2A?displayProperty=nameWithType> 相同的字串。</span><span class="sxs-lookup"><span data-stu-id="3161b-109">As a result, <xref:System.Object.ToString?displayProperty=nameWithType> conversion does not produce the same string as <xref:System.Convert.ToString%2A?displayProperty=nameWithType> in the .NET Framework.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3161b-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3161b-110">See also</span></span>

- [<span data-ttu-id="3161b-111">資料類型與函式</span><span class="sxs-lookup"><span data-stu-id="3161b-111">Data Types and Functions</span></span>](data-types-and-functions.md)
