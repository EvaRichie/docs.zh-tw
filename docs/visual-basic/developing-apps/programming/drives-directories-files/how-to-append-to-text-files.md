---
title: 作法：附加至文字檔
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], appending to files
- I/O [Visual Basic], My.Computer.FileSystem.WriteAllText method
- I/O [Visual Basic], WriteAllText method
ms.assetid: bbbd7fb5-f169-41a9-b53f-520ea9613913
ms.openlocfilehash: 53b2e4c9030e9d1dd81a4121ad3f92aad796e3e1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359951"
---
# <a name="how-to-append-to-text-files-in-visual-basic"></a><span data-ttu-id="1663a-102">如何：在 Visual Basic 中附加至文字檔</span><span class="sxs-lookup"><span data-stu-id="1663a-102">How to: Append to Text Files in Visual Basic</span></span>

<span data-ttu-id="1663a-103">您可以使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> 方法來附加至文字檔，方法是指定將 `append` 參數設定為 `True`。</span><span class="sxs-lookup"><span data-stu-id="1663a-103">The <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> method can be used to append to a text file by specifying that the `append` parameter is set to `True`.</span></span>  
  
### <a name="to-append-to-a-text-file"></a><span data-ttu-id="1663a-104">附加至文字檔</span><span class="sxs-lookup"><span data-stu-id="1663a-104">To append to a text file</span></span>  
  
- <span data-ttu-id="1663a-105">使用 `WriteAllText` 方法，並指定要附加的目標檔案和字串以及將 `append` 參數設定為 `True`。</span><span class="sxs-lookup"><span data-stu-id="1663a-105">Use the `WriteAllText` method, specifying the target file and string to be appended and setting the `append` parameter to `True`.</span></span>  
  
     <span data-ttu-id="1663a-106">這個範例會將 `"This is a test string."` 字串寫入名為 `Testfile.txt` 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="1663a-106">This example writes the string `"This is a test string."` to the file named `Testfile.txt`.</span></span>  
  
     [!code-vb[VbFileIOWrite#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#6)]  
  
## <a name="robust-programming"></a><span data-ttu-id="1663a-107">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="1663a-107">Robust Programming</span></span>  

 <span data-ttu-id="1663a-108">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="1663a-108">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="1663a-109">因下列其中一項原因而導致路徑無效：它是長度為零的字串、它只包含空白字元、它包含無效的字元，或者它是裝置路徑 (開頭為 \\\\.\\) (<xref:System.ArgumentException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-109">The path is not valid for one of the following reasons: it is a zero-length string, it contains only white space, it contains invalid characters, or it is a device path (starts with \\\\.\\) (<xref:System.ArgumentException>).</span></span>  
  
- <span data-ttu-id="1663a-110">路徑無效，因為它是 `Nothing` (<xref:System.ArgumentNullException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-110">The path is not valid because it is `Nothing` (<xref:System.ArgumentNullException>).</span></span>  
  
- <span data-ttu-id="1663a-111">`File` 指向不存在的路徑 (<xref:System.IO.FileNotFoundException> 或 <xref:System.IO.DirectoryNotFoundException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-111">`File` points to a path that does not exist (<xref:System.IO.FileNotFoundException> or <xref:System.IO.DirectoryNotFoundException>).</span></span>  
  
- <span data-ttu-id="1663a-112">檔案正由另一個處理序使用中，或發生 I/O 錯誤 (<xref:System.IO.IOException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-112">The file is in use by another process, or an I/O error occurs (<xref:System.IO.IOException>).</span></span>  
  
- <span data-ttu-id="1663a-113">路徑超過系統定義的最大長度 (<xref:System.IO.PathTooLongException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-113">The path exceeds the system-defined maximum length (<xref:System.IO.PathTooLongException>).</span></span>  
  
- <span data-ttu-id="1663a-114">路徑中的檔案或目錄名稱含有冒號 (:)，或者是無效的格式 (<xref:System.NotSupportedException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-114">A file or directory name in the path contains a colon (:) or is in an invalid format (<xref:System.NotSupportedException>).</span></span>  
  
- <span data-ttu-id="1663a-115">使用者缺乏必要的使用權限來檢視路徑 (<xref:System.Security.SecurityException>)。</span><span class="sxs-lookup"><span data-stu-id="1663a-115">The user lacks necessary permissions to view the path (<xref:System.Security.SecurityException>).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1663a-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1663a-116">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- [<span data-ttu-id="1663a-117">寫入檔案</span><span class="sxs-lookup"><span data-stu-id="1663a-117">Writing to Files</span></span>](writing-to-files.md)
