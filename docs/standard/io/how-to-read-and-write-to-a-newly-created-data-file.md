---
title: 如何：讀取和寫入新建立的資料檔案
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- streams, reading and writing data
- BinaryReader class, examples
- I/O [.NET Framework], reading data
- I/O [.NET Framework], writing data
- BinaryWriter class, examples
ms.assetid: e209d949-31e8-44ea-8e38-87f9093f3093
ms.openlocfilehash: 18f44af81a38a48da3115d2082ef45af39f06529
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291808"
---
# <a name="how-to-read-and-write-to-a-newly-created-data-file"></a><span data-ttu-id="dfcac-102">如何：讀取和寫入新建立的資料檔案</span><span class="sxs-lookup"><span data-stu-id="dfcac-102">How to: Read and write to a newly created data file</span></span>
<span data-ttu-id="dfcac-103"><xref:System.IO.BinaryWriter?displayProperty=nameWithType> 和 <xref:System.IO.BinaryReader?displayProperty=nameWithType> 類別用於寫入和讀取資料，而不是字元字串。</span><span class="sxs-lookup"><span data-stu-id="dfcac-103">The <xref:System.IO.BinaryWriter?displayProperty=nameWithType> and <xref:System.IO.BinaryReader?displayProperty=nameWithType> classes are used for writing and reading data other than character strings.</span></span> <span data-ttu-id="dfcac-104">下列範例顯示如何建立空的檔案資料流、將資料寫入其中，以及從中讀取資料。</span><span class="sxs-lookup"><span data-stu-id="dfcac-104">The following example shows how to create an empty file stream, write data to it, and read data from it.</span></span>

<span data-ttu-id="dfcac-105">此範例會在目前的目錄中建立一個稱為 *Test.data* 的資料檔案、建立相關聯的 <xref:System.IO.BinaryWriter> 和 <xref:System.IO.BinaryReader> 物件，而且會使用 <xref:System.IO.BinaryWriter> 物件，將 0 到 10 的整數寫入 *Test.data*，讓檔案指標留在檔案的結尾。</span><span class="sxs-lookup"><span data-stu-id="dfcac-105">The example creates a data file called *Test.data* in the current directory, creates the associated <xref:System.IO.BinaryWriter> and <xref:System.IO.BinaryReader> objects, and uses the <xref:System.IO.BinaryWriter> object to write the integers 0 through 10 to *Test.data*, which leaves the file pointer at the end of the file.</span></span> <span data-ttu-id="dfcac-106"><xref:System.IO.BinaryReader> 物件接著會將檔案指標設定為原點， 並讀出指定的內容。</span><span class="sxs-lookup"><span data-stu-id="dfcac-106">The <xref:System.IO.BinaryReader> object then sets the file pointer back to the origin and reads out the specified content.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="dfcac-107">如果 *Test.data* 已存在於目前的目錄中，則會擲回 <xref:System.IO.IOException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="dfcac-107">If *Test.data* already exists in the current directory, an <xref:System.IO.IOException> exception is thrown.</span></span> <span data-ttu-id="dfcac-108">使用檔案模式選項 <xref:System.IO.FileMode.Create?displayProperty=nameWithType>，而不是 <xref:System.IO.FileMode.CreateNew?displayProperty=nameWithType>，來一律建立新檔案，而不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="dfcac-108">Use the file mode option <xref:System.IO.FileMode.Create?displayProperty=nameWithType> rather than <xref:System.IO.FileMode.CreateNew?displayProperty=nameWithType> to always create a new file without throwing an exception.</span></span>  
  
## <a name="example"></a><span data-ttu-id="dfcac-109">範例</span><span class="sxs-lookup"><span data-stu-id="dfcac-109">Example</span></span>  
 [!code-csharp[System.IO.BinaryReaderWriter#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/CS/source6.cs#7)]
 [!code-vb[System.IO.BinaryReaderWriter#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/VB/source6.vb#7)]  
  
## <a name="see-also"></a><span data-ttu-id="dfcac-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dfcac-110">See also</span></span>

- <xref:System.IO.BinaryReader>  
- <xref:System.IO.BinaryWriter>  
- <xref:System.IO.FileStream>  
- <xref:System.IO.FileStream.Seek%2A?displayProperty=nameWithType>  
- <xref:System.IO.SeekOrigin>  
- [<span data-ttu-id="dfcac-111">如何：列舉目錄和檔案</span><span class="sxs-lookup"><span data-stu-id="dfcac-111">How to: Enumerate directories and files</span></span>](how-to-enumerate-directories-and-files.md)  
- [<span data-ttu-id="dfcac-112">如何：開啟並附加至記錄檔</span><span class="sxs-lookup"><span data-stu-id="dfcac-112">How to: Open and append to a log file</span></span>](how-to-open-and-append-to-a-log-file.md)  
- [<span data-ttu-id="dfcac-113">如何：從檔案讀取文字</span><span class="sxs-lookup"><span data-stu-id="dfcac-113">How to: Read text from a file</span></span>](how-to-read-text-from-a-file.md)  
- [<span data-ttu-id="dfcac-114">如何：將文字寫入檔案</span><span class="sxs-lookup"><span data-stu-id="dfcac-114">How to: Write text to a file</span></span>](how-to-write-text-to-a-file.md)  
- [<span data-ttu-id="dfcac-115">如何：從字串讀取字元</span><span class="sxs-lookup"><span data-stu-id="dfcac-115">How to: Read characters from a string</span></span>](how-to-read-characters-from-a-string.md)  
- [<span data-ttu-id="dfcac-116">如何：將字元寫入字串</span><span class="sxs-lookup"><span data-stu-id="dfcac-116">How to: Write characters to a string</span></span>](how-to-write-characters-to-a-string.md)  
- [<span data-ttu-id="dfcac-117">檔案和資料流 I/O</span><span class="sxs-lookup"><span data-stu-id="dfcac-117">File and stream I/O</span></span>](index.md)
