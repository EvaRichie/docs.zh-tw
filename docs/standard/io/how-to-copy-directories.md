---
title: 如何：複製目錄
ms.date: 12/27/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directory copying
- I/O [.NET Framework], copying directories
- subdirectory copying
- copying directories
- directories [.NET Framework], copying
ms.assetid: 5a969765-e5f8-4b4e-977e-90e2b0a1fe3c
ms.openlocfilehash: f71f428037f33fdbc692ca2f02a4c767998d684e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288572"
---
# <a name="how-to-copy-directories"></a><span data-ttu-id="064f0-102">如何：複製目錄</span><span class="sxs-lookup"><span data-stu-id="064f0-102">How to: Copy directories</span></span>
<span data-ttu-id="064f0-103">本主題示範如何使用 I/O 類別將某一個目錄的內容同步複製到另一個位置。</span><span class="sxs-lookup"><span data-stu-id="064f0-103">This topic demonstrates how to use I/O classes to synchronously copy the contents of a directory to another location.</span></span>

<span data-ttu-id="064f0-104">如需非同步檔案複製的範例，請參閱[非同步檔案 I/O](asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="064f0-104">For an example of asynchronous file copy, see [Asynchronous file I/O](asynchronous-file-i-o.md).</span></span>

<span data-ttu-id="064f0-105">此範例會將 `DirectoryCopy` 方法的 `copySubDirs` 設定為 `true` 來複製子目錄。</span><span class="sxs-lookup"><span data-stu-id="064f0-105">This example copies subdirectories by setting the `copySubDirs` of the `DirectoryCopy` method to `true`.</span></span> <span data-ttu-id="064f0-106">`DirectoryCopy` 方法會以遞迴方式複製子目錄，方法是在每個子目錄上呼叫其本身，直到沒有其他要複製的子目錄為止。</span><span class="sxs-lookup"><span data-stu-id="064f0-106">The `DirectoryCopy` method recursively copies subdirectories by calling itself on each subdirectory until there are no more to copy.</span></span>  
  
## <a name="example"></a><span data-ttu-id="064f0-107">範例</span><span class="sxs-lookup"><span data-stu-id="064f0-107">Example</span></span>  
 [!code-csharp[System.IO.Directory_Copy#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Directory_Copy/cs/program.cs#1)]
 [!code-vb[System.IO.Directory_Copy#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Directory_Copy/vb/Program.vb#1)]  
  
[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="see-also"></a><span data-ttu-id="064f0-108">另請參閱</span><span class="sxs-lookup"><span data-stu-id="064f0-108">See also</span></span>

- <xref:System.IO.FileInfo>
- <xref:System.IO.DirectoryInfo>
- <xref:System.IO.FileStream>
- [<span data-ttu-id="064f0-109">檔案和資料流 I/O</span><span class="sxs-lookup"><span data-stu-id="064f0-109">File and stream I/O</span></span>](index.md)
- [<span data-ttu-id="064f0-110">一般 I/O 工作</span><span class="sxs-lookup"><span data-stu-id="064f0-110">Common I/O tasks</span></span>](common-i-o-tasks.md)
- [<span data-ttu-id="064f0-111">非同步檔案 I/O</span><span class="sxs-lookup"><span data-stu-id="064f0-111">Asynchronous file I/O</span></span>](asynchronous-file-i-o.md)
