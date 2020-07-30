---
title: '如何取得檔案、資料夾和磁片磁碟機的相關資訊-c # 程式設計手冊'
description: 瞭解如何取得檔案、資料夾和磁片磁碟機的相關資訊。 請參閱程式碼範例和其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- files [C#], getting information about
ms.assetid: 22fc2da6-5494-405b-995e-c0b99142a93e
ms.openlocfilehash: f696cd90f197bede1a64949d211a563ce9a18376
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87299925"
---
# <a name="how-to-get-information-about-files-folders-and-drives--c-programming-guide"></a><span data-ttu-id="5abb4-104">如何取得有關檔案、資料夾和磁片磁碟機的資訊（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="5abb4-104">How to get information about files, folders, and drives  (C# Programming Guide)</span></span>
<span data-ttu-id="5abb4-105">在 .NET 中，您可以使用下列類別來存取檔案系統資訊：</span><span class="sxs-lookup"><span data-stu-id="5abb4-105">In .NET, you can access file system information by using the following classes:</span></span>  
  
- <xref:System.IO.FileInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.DirectoryInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.DriveInfo?displayProperty=nameWithType>  
  
- <xref:System.IO.Directory?displayProperty=nameWithType>  
  
- <xref:System.IO.File?displayProperty=nameWithType>  
  
 <span data-ttu-id="5abb4-106"><xref:System.IO.FileInfo> 和 <xref:System.IO.DirectoryInfo> 類別分別代表檔案和目錄，其所包含的屬性 (Property) 會公開 NTFS 檔案系統所支援的許多檔案屬性 (Attribute)。</span><span class="sxs-lookup"><span data-stu-id="5abb4-106">The <xref:System.IO.FileInfo> and <xref:System.IO.DirectoryInfo> classes represent a file or directory and contain properties that expose many of the file attributes that are supported by the NTFS file system.</span></span> <span data-ttu-id="5abb4-107">這些類別也包含用於開啟、關閉、移動及刪除檔案和資料夾的方法。</span><span class="sxs-lookup"><span data-stu-id="5abb4-107">They also contain methods for opening, closing, moving, and deleting files and folders.</span></span> <span data-ttu-id="5abb4-108">您可以將代表檔案、資料夾或磁碟機名稱的字串傳入建構函式，來建立這些類別的執行個體：</span><span class="sxs-lookup"><span data-stu-id="5abb4-108">You can create instances of these classes by passing a string that represents the name of the file, folder, or drive in to the constructor:</span></span>  
  
```csharp  
System.IO.DriveInfo di = new System.IO.DriveInfo(@"C:\");  
```  
  
 <span data-ttu-id="5abb4-109">您也可以呼叫 <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=nameWithType>、<xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=nameWithType> 和 <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=nameWithType>，取得檔案、資料夾或磁碟機名稱。</span><span class="sxs-lookup"><span data-stu-id="5abb4-109">You can also obtain the names of files, folders, or drives by using calls to <xref:System.IO.DirectoryInfo.GetDirectories%2A?displayProperty=nameWithType>, <xref:System.IO.DirectoryInfo.GetFiles%2A?displayProperty=nameWithType>, and <xref:System.IO.DriveInfo.RootDirectory%2A?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="5abb4-110"><xref:System.IO.Directory?displayProperty=nameWithType> 和 <xref:System.IO.File?displayProperty=nameWithType> 類別提供靜態方法，擷取目錄和檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5abb4-110">The <xref:System.IO.Directory?displayProperty=nameWithType> and <xref:System.IO.File?displayProperty=nameWithType> classes provide static methods for retrieving information about directories and files.</span></span>  
  
## <a name="example"></a><span data-ttu-id="5abb4-111">範例</span><span class="sxs-lookup"><span data-stu-id="5abb4-111">Example</span></span>  
 <span data-ttu-id="5abb4-112">下列範例示範用來存取檔案和資料夾相關資訊的各種方法。</span><span class="sxs-lookup"><span data-stu-id="5abb4-112">The following example shows various ways to access information about files and folders.</span></span>  
  
 [!code-csharp[csFilesandFolders#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#6)]  
  
## <a name="robust-programming"></a><span data-ttu-id="5abb4-113">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="5abb4-113">Robust Programming</span></span>  
 <span data-ttu-id="5abb4-114">當您處理使用者指定的路徑字串時，您也應該處理下列情況所發生的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="5abb4-114">When you process user-specified path strings, you should also handle exceptions for the following conditions:</span></span>  
  
- <span data-ttu-id="5abb4-115">檔案名稱的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="5abb4-115">The file name is malformed.</span></span> <span data-ttu-id="5abb4-116">例如，包含無效的字元，或只包含空白字元。</span><span class="sxs-lookup"><span data-stu-id="5abb4-116">For example, it contains invalid characters or only white space.</span></span>  
  
- <span data-ttu-id="5abb4-117">檔案名稱為 null。</span><span class="sxs-lookup"><span data-stu-id="5abb4-117">The file name is null.</span></span>  
  
- <span data-ttu-id="5abb4-118">檔案名稱超過系統定義的長度上限。</span><span class="sxs-lookup"><span data-stu-id="5abb4-118">The file name is longer than the system-defined maximum length.</span></span>  
  
- <span data-ttu-id="5abb4-119">檔案名稱包含冒號 (:)。</span><span class="sxs-lookup"><span data-stu-id="5abb4-119">The file name contains a colon (:).</span></span>  
  
 <span data-ttu-id="5abb4-120">如果應用程式沒有足夠的權限可讀取指定的檔案，則不論是否存在路徑，`Exists` 方法都會傳回 `false`；此方法不會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5abb4-120">If the application does not have sufficient permissions to read the specified file, the `Exists` method returns `false` regardless of whether a path exists; the method does not throw an exception.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5abb4-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5abb4-121">See also</span></span>

- <xref:System.IO?displayProperty=nameWithType>
- [<span data-ttu-id="5abb4-122">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="5abb4-122">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="5abb4-123">檔案系統和登錄 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="5abb4-123">File System and the Registry (C# Programming Guide)</span></span>](./index.md)
