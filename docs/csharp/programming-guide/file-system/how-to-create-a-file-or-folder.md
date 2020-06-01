---
title: '如何建立檔案或資料夾-c # 程式設計手冊'
ms.date: 07/20/2015
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
ms.openlocfilehash: 5efe3b7dc600645488816d6f931df57fc236efc9
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241639"
---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a><span data-ttu-id="54021-102">如何建立檔案或資料夾（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="54021-102">How to create a file or folder (C# Programming Guide)</span></span>
<span data-ttu-id="54021-103">您可以程式設計的方式在電腦上建立資料夾、建立子資料夾、在子資料夾中建立檔案，以及將資料寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="54021-103">You can programmatically create a folder on your computer, create a subfolder, create a file in the subfolder, and write data to the file.</span></span>  
  
## <a name="example"></a><span data-ttu-id="54021-104">範例</span><span class="sxs-lookup"><span data-stu-id="54021-104">Example</span></span>  
 [!code-csharp[csFilesandFolders#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#10)]  
  
 <span data-ttu-id="54021-105">若資料夾已經存在，<xref:System.IO.Directory.CreateDirectory%2A> 不會採取任何動作，也不會擲回任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="54021-105">If the folder already exists, <xref:System.IO.Directory.CreateDirectory%2A> does nothing, and no exception is thrown.</span></span> <span data-ttu-id="54021-106">但 <xref:System.IO.File.Create%2A?displayProperty=nameWithType> 會以新的檔案取代現有的檔案。</span><span class="sxs-lookup"><span data-stu-id="54021-106">However, <xref:System.IO.File.Create%2A?displayProperty=nameWithType> replaces an existing file with a new file.</span></span> <span data-ttu-id="54021-107">此例使用 `if`-`else` 陳述式防止現有的檔案被取代。</span><span class="sxs-lookup"><span data-stu-id="54021-107">The example uses an `if`-`else` statement to prevent an existing file from being replaced.</span></span>  
  
 <span data-ttu-id="54021-108">透過在範例中進行下列變更，您可以根據是否已有具特定名稱的檔案來指定不同的結果。</span><span class="sxs-lookup"><span data-stu-id="54021-108">By making the following changes in the example, you can specify different outcomes based on whether a file with a certain name already exists.</span></span> <span data-ttu-id="54021-109">如果沒有這類檔案，程式碼會建立一個。</span><span class="sxs-lookup"><span data-stu-id="54021-109">If such a file doesn't exist, the code creates one.</span></span> <span data-ttu-id="54021-110">如果有這類檔案，程式碼會將資料附加至該檔案。</span><span class="sxs-lookup"><span data-stu-id="54021-110">If such a file exists, the code appends data to that file.</span></span>  
  
- <span data-ttu-id="54021-111">指定非隨機的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="54021-111">Specify a non-random file name.</span></span>  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
    ```  
  
- <span data-ttu-id="54021-112">請在下列程式碼中以 `using` 陳述式取代 `if`-`else` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="54021-112">Replace the `if`-`else` statement with the `using` statement in the following code.</span></span>  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
    ```  
  
 <span data-ttu-id="54021-113">執行數次範例以確認資料是否每次都新增至檔案。</span><span class="sxs-lookup"><span data-stu-id="54021-113">Run the example several times to verify that data is added to the file each time.</span></span>  
  
 <span data-ttu-id="54021-114">若要取得更多可以嘗試的 `FileMode` 值，請參考 <xref:System.IO.FileMode>。</span><span class="sxs-lookup"><span data-stu-id="54021-114">For more `FileMode` values that you can try, see <xref:System.IO.FileMode>.</span></span>  
  
 <span data-ttu-id="54021-115">以下條件可能會造成例外狀況：</span><span class="sxs-lookup"><span data-stu-id="54021-115">The following conditions may cause an exception:</span></span>  
  
- <span data-ttu-id="54021-116">資料夾名稱的格式不正確。</span><span class="sxs-lookup"><span data-stu-id="54021-116">The folder name is malformed.</span></span> <span data-ttu-id="54021-117">舉例來說，其可能包含非法的字元，或是只有空白字元 (<xref:System.ArgumentException> 類別)。</span><span class="sxs-lookup"><span data-stu-id="54021-117">For example, it contains illegal characters or is only white space (<xref:System.ArgumentException> class).</span></span> <span data-ttu-id="54021-118">請使用 <xref:System.IO.Path> 類別建立有效的路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="54021-118">Use the <xref:System.IO.Path> class to create valid path names.</span></span>  
  
- <span data-ttu-id="54021-119">要建立之資料夾的父資料夾為唯讀 (<xref:System.IO.IOException> 類別)。</span><span class="sxs-lookup"><span data-stu-id="54021-119">The parent folder of the folder to be created is read-only (<xref:System.IO.IOException> class).</span></span>  
  
- <span data-ttu-id="54021-120">資料夾名稱為 `null` (<xref:System.ArgumentNullException> 類別)。</span><span class="sxs-lookup"><span data-stu-id="54021-120">The folder name is `null` (<xref:System.ArgumentNullException> class).</span></span>  
  
- <span data-ttu-id="54021-121">資料夾名稱過長 (<xref:System.IO.PathTooLongException> 類別)。</span><span class="sxs-lookup"><span data-stu-id="54021-121">The folder name is too long (<xref:System.IO.PathTooLongException> class).</span></span>  
  
- <span data-ttu-id="54021-122">資料夾名稱只是一個冒號 ":" (<xref:System.IO.PathTooLongException> 類別)。</span><span class="sxs-lookup"><span data-stu-id="54021-122">The folder name is only a colon, ":" (<xref:System.IO.PathTooLongException> class).</span></span>  
  
## <a name="net-security"></a><span data-ttu-id="54021-123">.NET 安全性</span><span class="sxs-lookup"><span data-stu-id="54021-123">.NET Security</span></span>  
 <span data-ttu-id="54021-124">在部分信任的狀況下，可能會擲回 <xref:System.Security.SecurityException> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="54021-124">An instance of the <xref:System.Security.SecurityException> class may be thrown in partial-trust situations.</span></span>  
  
 <span data-ttu-id="54021-125">如果您沒有建立資料夾的許可權，此範例會擲回類別的實例 <xref:System.UnauthorizedAccessException> 。</span><span class="sxs-lookup"><span data-stu-id="54021-125">If you don't have permission to create the folder, the example throws an instance of the <xref:System.UnauthorizedAccessException> class.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="54021-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="54021-126">See also</span></span>

- <xref:System.IO?displayProperty=nameWithType>
- [<span data-ttu-id="54021-127">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="54021-127">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="54021-128">檔案系統和登錄 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="54021-128">File System and the Registry (C# Programming Guide)</span></span>](./index.md)
