---
title: 作法：刪除隔離儲存區中的檔案和目錄
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- data storage using isolated storage, deleting files and directories
- directories [.NET], isolated storage
- files [.NET], isolated storage
- isolated storage, deleting files and directories
- data stores, deleting files and directories
- stores, creating files and directories
- deleting files within isolated stage file
- storing data using isolated storage, deleting files and directories
- deleting directories within isolated stage file
ms.assetid: 8fcc0dea-435b-4d40-ba4d-ba056265c202
ms.openlocfilehash: 9340796c835d91fe5401e467edd82cab80b2e653
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830788"
---
# <a name="how-to-delete-files-and-directories-in-isolated-storage"></a><span data-ttu-id="7c70c-102">作法：刪除隔離儲存區中的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="7c70c-102">How to: Delete Files and Directories in Isolated Storage</span></span>
<span data-ttu-id="7c70c-103">您可以刪除隔離儲存區檔案中的目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="7c70c-103">You can delete directories and files within an isolated storage file.</span></span> <span data-ttu-id="7c70c-104">在存放區內，檔案和目錄名稱都與作業系統相依，且會指定為相對於虛擬檔案系統的根目錄。</span><span class="sxs-lookup"><span data-stu-id="7c70c-104">Within a store, file and directory names are operating-system dependent and are specified as relative to the root of the virtual file system.</span></span> <span data-ttu-id="7c70c-105">它們在 Windows 作業系統上不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7c70c-105">They are not case-sensitive on Windows operating systems.</span></span>  
  
 <span data-ttu-id="7c70c-106"><xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType> 類別提供兩種方法來刪目錄和檔案：<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>。</span><span class="sxs-lookup"><span data-stu-id="7c70c-106">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType> class supplies two methods for deleting directories and files: <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>.</span></span> <span data-ttu-id="7c70c-107">如果您嘗試刪除不存在的檔案或目錄，會擲回 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7c70c-107">An <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception is thrown if you try to delete a file or directory that does not exist.</span></span> <span data-ttu-id="7c70c-108">如果您在名稱中包含萬用字元，<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 會擲回 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 例外狀況，且 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> 會擲回 <xref:System.ArgumentException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7c70c-108">If you include a wildcard character in the name, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> throws an <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception, and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> throws an <xref:System.ArgumentException> exception.</span></span>  
  
 <span data-ttu-id="7c70c-109">如果目錄中包含任何檔案或子目錄，則 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 方法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7c70c-109">The <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> method fails if the directory contains any files or subdirectories.</span></span> <span data-ttu-id="7c70c-110">您可以使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 方法擷取現有的檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="7c70c-110">You can use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> and <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> methods to retrieve the existing files and directories.</span></span> <span data-ttu-id="7c70c-111">如需有關搜尋存放區的虛擬檔案系統的詳細資訊，請參閱[操作說明：尋找隔離儲存區中的現有檔案和目錄](how-to-find-existing-files-and-directories-in-isolated-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="7c70c-111">For more information about searching the virtual file system of a store, see [How to: Find Existing Files and Directories in Isolated Storage](how-to-find-existing-files-and-directories-in-isolated-storage.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7c70c-112">範例</span><span class="sxs-lookup"><span data-stu-id="7c70c-112">Example</span></span>  
 <span data-ttu-id="7c70c-113">下列程式碼範例會建立數個目錄和檔案，然後再加以刪除。</span><span class="sxs-lookup"><span data-stu-id="7c70c-113">The following code example creates and then deletes several directories and files.</span></span>  
  
 [!code-cpp[Conceptual.IsolatedStorage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.IsolatedStorage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source4.cs#4)]
 [!code-vb[Conceptual.IsolatedStorage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source4.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="7c70c-114">請參閱</span><span class="sxs-lookup"><span data-stu-id="7c70c-114">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=nameWithType>
- [<span data-ttu-id="7c70c-115">隔離儲存區</span><span class="sxs-lookup"><span data-stu-id="7c70c-115">Isolated Storage</span></span>](isolated-storage.md)
