---
title: 作法：讀取和寫入隔離儲存區中的檔案
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- files, isolated storage
- reading data
- storing data using isolated storage, reading and writing to files
- writing to files within store
- data storage using isolated storage, reading and writing to files
- reading files within store
- isolated storage, reading and writing to files
- data stores, reading and writing to files
- stores, reading and writing to files
ms.assetid: f977ebdc-1b55-475a-bc3d-3376470b08ae
ms.openlocfilehash: eff020ebb1de40f83582bbf872339c7652d1d4b1
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830697"
---
# <a name="how-to-read-and-write-to-files-in-isolated-storage"></a><span data-ttu-id="67d27-102">作法：讀取和寫入隔離儲存區中的檔案</span><span class="sxs-lookup"><span data-stu-id="67d27-102">How to: Read and Write to Files in Isolated Storage</span></span>
<span data-ttu-id="67d27-103">若要在隔離存放區中的檔案內進行讀取或寫入，請使用具有資料流讀取器 (<xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 物件) 或資料流寫入器 (<xref:System.IO.StreamReader> 物件) 的 <xref:System.IO.StreamWriter> 物件。</span><span class="sxs-lookup"><span data-stu-id="67d27-103">To read from, or write to, a file in an isolated store, use an <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> object with a stream reader (<xref:System.IO.StreamReader> object) or stream writer (<xref:System.IO.StreamWriter> object).</span></span>  
  
## <a name="example"></a><span data-ttu-id="67d27-104">範例</span><span class="sxs-lookup"><span data-stu-id="67d27-104">Example</span></span>  
 <span data-ttu-id="67d27-105">下列程式碼範例會取得隔離存放區，並檢查存放區中是否存在名為 TestStore.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="67d27-105">The following code example obtains an isolated store and checks whether a file named TestStore.txt exists in the store.</span></span> <span data-ttu-id="67d27-106">如果不存在，它會建立檔案，並將 "Hello Isolated Storage" 寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="67d27-106">If it doesn't exist, it creates the file and writes "Hello Isolated Storage" to the file.</span></span> <span data-ttu-id="67d27-107">如果 TestStore.txt 已經存在，程式碼範例會從檔案讀取。</span><span class="sxs-lookup"><span data-stu-id="67d27-107">If TestStore.txt already exists, the example code reads from the file.</span></span>  
  
 [!code-csharp[Conceptual.IsolatedStorage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source5.cs#5)]
 [!code-vb[Conceptual.IsolatedStorage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source5.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="67d27-108">請參閱</span><span class="sxs-lookup"><span data-stu-id="67d27-108">See also</span></span>

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- <xref:System.IO.FileMode?displayProperty=nameWithType>
- <xref:System.IO.FileAccess?displayProperty=nameWithType>
- <xref:System.IO.StreamReader?displayProperty=nameWithType>
- <xref:System.IO.StreamWriter?displayProperty=nameWithType>
- [<span data-ttu-id="67d27-109">檔案和資料流 I/O</span><span class="sxs-lookup"><span data-stu-id="67d27-109">File and Stream I/O</span></span>](index.md)
- [<span data-ttu-id="67d27-110">隔離儲存區</span><span class="sxs-lookup"><span data-stu-id="67d27-110">Isolated Storage</span></span>](isolated-storage.md)
