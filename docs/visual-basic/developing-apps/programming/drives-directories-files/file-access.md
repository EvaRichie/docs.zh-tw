---
title: 檔案存取
ms.date: 07/20/2015
helpviewer_keywords:
- file access
- files [Visual Basic], input and output
- file access, Visual Basic
- files [Visual Basic], I/O
- file I/O classes
- data [Visual Basic], accessing from files
- files [Visual Basic], accessing
- file access, using components
- My.Computer.FileSystem object, accessing files
- I/O [Visual Basic]
- sequential access
ms.assetid: 231533bf-d049-4345-befa-3fb78fe6517d
ms.openlocfilehash: 3b2042862ae81a52d62374e35a456766ed47edc9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401728"
---
# <a name="file-access-with-visual-basic"></a><span data-ttu-id="b5a68-102">使用 Visual Basic 存取檔案</span><span class="sxs-lookup"><span data-stu-id="b5a68-102">File Access with Visual Basic</span></span>

<span data-ttu-id="b5a68-103">`My.Computer.FileSystem` 物件提供用於處理檔案和資料夾的工具。</span><span class="sxs-lookup"><span data-stu-id="b5a68-103">The `My.Computer.FileSystem` object provides tools for working with files and folders.</span></span> <span data-ttu-id="b5a68-104">其屬性、方法和事件可讓您建立、複製、移動、調查及刪除檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="b5a68-104">Its properties, methods, and events allow you to create, copy, move, investigate, and delete files and folders.</span></span> <span data-ttu-id="b5a68-105">`My.Computer.FileSystem` 比 Visual Basic 所提供的舊版函式 (`FileOpen`、`FileClose`、`Input`、`InputString`、`LineInput` 等) 提供更佳效能，以利回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="b5a68-105">`My.Computer.FileSystem` provides better performance than the legacy functions (`FileOpen`, `FileClose`, `Input`, `InputString`, `LineInput`, etc.) that are provided by Visual Basic for backward compatibility.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="b5a68-106">本節內容</span><span class="sxs-lookup"><span data-stu-id="b5a68-106">In This Section</span></span>  

 [<span data-ttu-id="b5a68-107">從檔案讀取</span><span class="sxs-lookup"><span data-stu-id="b5a68-107">Reading from Files</span></span>](reading-from-files.md)  
 <span data-ttu-id="b5a68-108">列出主題，說明如何使用 `My.Computer.FileSystem` 物件從檔案讀取</span><span class="sxs-lookup"><span data-stu-id="b5a68-108">Lists topics dealing with using the `My.Computer.FileSystem` object to read from files</span></span>  
  
 [<span data-ttu-id="b5a68-109">寫入檔案</span><span class="sxs-lookup"><span data-stu-id="b5a68-109">Writing to Files</span></span>](writing-to-files.md)  
 <span data-ttu-id="b5a68-110">列出主題，說明如何使用 `My.Computer.FileSystem` 物件寫入檔案</span><span class="sxs-lookup"><span data-stu-id="b5a68-110">Lists topics dealing with using the `My.Computer.FileSystem` object to write to files</span></span>  
  
 [<span data-ttu-id="b5a68-111">建立、刪除和移動檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="b5a68-111">Creating, Deleting, and Moving Files and Directories</span></span>](creating-deleting-and-moving-files-and-directories.md)  
 <span data-ttu-id="b5a68-112">列出主題，說明如何使用 `My.Computer.FileSystem` 物件建立、複製、刪除及移動檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="b5a68-112">Lists topics dealing with using the `My.Computer.FileSystem` object to creating, copying, deleting and moving files and folders.</span></span>  
  
 [<span data-ttu-id="b5a68-113">使用 TextFieldParser 物件剖析文字檔</span><span class="sxs-lookup"><span data-stu-id="b5a68-113">Parsing Text Files with the TextFieldParser Object</span></span>](parsing-text-files-with-the-textfieldparser-object.md)  
 <span data-ttu-id="b5a68-114">討論如何使用 `TextFieldReader` 剖析文字檔 (例如記錄檔)。</span><span class="sxs-lookup"><span data-stu-id="b5a68-114">Discusses how to use the `TextFieldReader` to parse text files such as logs.</span></span>  
  
 [<span data-ttu-id="b5a68-115">檔案編碼方式</span><span class="sxs-lookup"><span data-stu-id="b5a68-115">File Encodings</span></span>](file-encodings.md)  
 <span data-ttu-id="b5a68-116">說明檔案編碼方式及其用法。</span><span class="sxs-lookup"><span data-stu-id="b5a68-116">Describes file encodings and their use.</span></span>  
  
 [<span data-ttu-id="b5a68-117">逐步解說：在 Visual Basic 中管理檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="b5a68-117">Walkthrough: Manipulating Files and Directories in Visual Basic</span></span>](walkthrough-manipulating-files-and-directories.md)  
 <span data-ttu-id="b5a68-118">示範如何建立公用程式來報告檔案和資料夾的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b5a68-118">Demonstrates how to create a utility that reports information about files and folders.</span></span>  
  
 [<span data-ttu-id="b5a68-119">疑難排解：讀取和寫入文字檔</span><span class="sxs-lookup"><span data-stu-id="b5a68-119">Troubleshooting: Reading from and Writing to Text Files</span></span>](troubleshooting-reading-from-and-writing-to-text-files.md)  
 <span data-ttu-id="b5a68-120">列出讀取和寫入文字檔時遇到的常見問題，並針對每個問題提供補救建議。</span><span class="sxs-lookup"><span data-stu-id="b5a68-120">Lists common problems encountered when reading and writing to text files, and suggests remedies for each.</span></span>
