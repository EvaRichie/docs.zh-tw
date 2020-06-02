---
title: 通用設計模式
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- design patterns in class libraries
- class library design guidelines [.NET Framework], design patterns
ms.assetid: f7bd1361-4ab2-4132-972d-a044b8f197e1
ms.openlocfilehash: 9b9525a7597f7df6c9a554b51160a99f0e06232c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290963"
---
# <a name="common-design-patterns"></a><span data-ttu-id="7cb95-102">通用設計模式</span><span class="sxs-lookup"><span data-stu-id="7cb95-102">Common Design Patterns</span></span>
<span data-ttu-id="7cb95-103">有許多關於軟體模式、模式語言和反模式的書籍，可解決廣泛的模式主題。</span><span class="sxs-lookup"><span data-stu-id="7cb95-103">There are numerous books on software patterns, pattern languages, and antipatterns that address the very broad subject of patterns.</span></span> <span data-ttu-id="7cb95-104">因此，本章提供與一組非常有限的模式相關的指導方針和討論，在 .NET Framework Api 的設計中經常使用。</span><span class="sxs-lookup"><span data-stu-id="7cb95-104">Thus, this chapter provides guidelines and discussion related to a very limited set of patterns that are used frequently in the design of the .NET Framework APIs.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="7cb95-105">本節內容</span><span class="sxs-lookup"><span data-stu-id="7cb95-105">In This Section</span></span>  
 [<span data-ttu-id="7cb95-106">相依性屬性</span><span class="sxs-lookup"><span data-stu-id="7cb95-106">Dependency Properties</span></span>](dependency-properties.md)  
 [<span data-ttu-id="7cb95-107">Dispose 模式</span><span class="sxs-lookup"><span data-stu-id="7cb95-107">Dispose Pattern</span></span>](../garbage-collection/implementing-dispose.md)  
 <span data-ttu-id="7cb95-108">*部分©2005、2009 Microsoft Corporation。已保留擁有權限。*</span><span class="sxs-lookup"><span data-stu-id="7cb95-108">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>  
  
 <span data-ttu-id="7cb95-109">獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 節錄。\*\*</span><span class="sxs-lookup"><span data-stu-id="7cb95-109">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7cb95-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7cb95-110">See also</span></span>

- [<span data-ttu-id="7cb95-111">架構設計方針</span><span class="sxs-lookup"><span data-stu-id="7cb95-111">Framework Design Guidelines</span></span>](index.md)
