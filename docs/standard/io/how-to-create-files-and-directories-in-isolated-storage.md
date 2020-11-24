---
title: 作法：在隔離儲存區中建立檔案和目錄
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directories [.NET], isolated storage
- files [.NET], isolated storage
- isolated storage, creating files and directories
- data stores, creating files and directories
- data storage using isolated storage, creating files and directories
- stores, creating files and directories
- storing data using isolated storage, creating files and directories
ms.assetid: 2ca4d2a4-809b-4f00-bc08-bf4a64d3a5c3
ms.openlocfilehash: 1f6e8e1a048fcf7f8fd278eaac4988fa0e35791d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95684989"
---
# <a name="how-to-create-files-and-directories-in-isolated-storage"></a><span data-ttu-id="76b20-102">作法：在隔離儲存區中建立檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="76b20-102">How to: Create Files and Directories in Isolated Storage</span></span>

<span data-ttu-id="76b20-103">取得隔離儲存區之後，您可以建立目錄和檔案來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="76b20-103">After you've obtained an isolated store, you can create directories and files for storing data.</span></span> <span data-ttu-id="76b20-104">在存放區內，系統會以相對於虛擬檔案系統的根目錄指定檔案和目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="76b20-104">Within a store, file and directory names are specified with respect to the root of the virtual file system.</span></span>  
  
 <span data-ttu-id="76b20-105">若要建立目錄，請使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=nameWithType> 執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="76b20-105">To create a directory, use the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=nameWithType> instance method.</span></span> <span data-ttu-id="76b20-106">如果您指定不存在之目錄的子目錄，則會建立這兩個目錄。</span><span class="sxs-lookup"><span data-stu-id="76b20-106">If you specify a subdirectory of a directory that doesn't exist, both directories are created.</span></span> <span data-ttu-id="76b20-107">如果您指定已經存在的目錄，則會傳回方法而不會建立目錄，而且不會擲回任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76b20-107">If you specify a directory that already exists, the method returns without creating a directory, and no exception is thrown.</span></span> <span data-ttu-id="76b20-108">不過，如果您指定包含無效字元的目錄名稱，則會擲回 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76b20-108">However, if you specify a directory name that contains invalid characters, an <xref:System.IO.IsolatedStorage.IsolatedStorageException> exception is thrown.</span></span>  
  
 <span data-ttu-id="76b20-109">若要建立檔案，請使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="76b20-109">To create a file, use  the <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="76b20-110">在 Windows 作業系統中，隔離儲存區檔案和目錄名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="76b20-110">In the Windows operating system, isolated storage file and directory names are case-insensitive.</span></span> <span data-ttu-id="76b20-111">也就是說，如果您建立名為 `ThisFile.txt` 的檔案，然後再建立名為 `THISFILE.TXT` 的另一個檔案，則只會建立一個檔案。</span><span class="sxs-lookup"><span data-stu-id="76b20-111">That is, if you create a file named `ThisFile.txt`, and then create another file named `THISFILE.TXT`, only one file is created.</span></span> <span data-ttu-id="76b20-112">基於顯示用途，檔案名稱會保留其原始大小寫。</span><span class="sxs-lookup"><span data-stu-id="76b20-112">The file name keeps its original casing for display purposes.</span></span>  

 <span data-ttu-id="76b20-113"><xref:System.IO.IsolatedStorage.IsolatedStorageException>如果路徑包含的目錄不存在，則建立隔離儲存區檔案將會擲回。</span><span class="sxs-lookup"><span data-stu-id="76b20-113">Isolated storage file creation will throw an <xref:System.IO.IsolatedStorage.IsolatedStorageException> if the path contains a directory that does not exist.</span></span>
  
## <a name="example"></a><span data-ttu-id="76b20-114">範例</span><span class="sxs-lookup"><span data-stu-id="76b20-114">Example</span></span>  

 <span data-ttu-id="76b20-115">下列程式碼範例說明如何在隔離存放區中建立檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="76b20-115">The following code example illustrates how to create files and directories in an isolated store.</span></span>  
  
 [!code-csharp[Conceptual.IsolatedStorage#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source.cs#1)]
 [!code-vb[Conceptual.IsolatedStorage#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="76b20-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="76b20-116">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- [<span data-ttu-id="76b20-117">隔離儲存區</span><span class="sxs-lookup"><span data-stu-id="76b20-117">Isolated Storage</span></span>](isolated-storage.md)
