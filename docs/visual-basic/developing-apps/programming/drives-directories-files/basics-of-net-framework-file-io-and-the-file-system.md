---
title: .NET Framework 檔案 I/O 和檔案系統基本概念
ms.date: 07/20/2015
helpviewer_keywords:
- file access, file I/O in Visual Basic
- file attributes, determining
- streams, fundamental operations
- file permissions
- streams
- streams, definition
ms.assetid: 49d837c0-cf28-416f-8606-4d83d7b479ef
ms.openlocfilehash: 187a20617ec901e722a30ebfa571e4a55ed0b5c3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401793"
---
# <a name="basics-of-net-framework-file-io-and-the-file-system-visual-basic"></a><span data-ttu-id="f94b8-102">.NET Framework 檔案 I/O 和檔案系統基本概念 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f94b8-102">Basics of .NET Framework File I/O and the File System (Visual Basic)</span></span>

<span data-ttu-id="f94b8-103"><xref:System.IO> 命名空間中的類別是用來處理磁碟機、檔案和目錄。</span><span class="sxs-lookup"><span data-stu-id="f94b8-103">Classes in the <xref:System.IO> namespace are used to work with drives, files, and directories.</span></span>

<span data-ttu-id="f94b8-104"><xref:System.IO> 命名空間包含 <xref:System.IO.File> 和 <xref:System.IO.Directory> 類別，提供操縱檔案和目錄的 .NET Framework 功能。</span><span class="sxs-lookup"><span data-stu-id="f94b8-104">The <xref:System.IO> namespace contains the <xref:System.IO.File> and <xref:System.IO.Directory> classes, which provide the .NET Framework functionality that manipulates files and directories.</span></span> <span data-ttu-id="f94b8-105">因為這些物件的方法是靜態或共用成員，所以您可以直接使用它們，而不需要先建立類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f94b8-105">Because the methods of these objects are static or shared members, you can use them directly without creating an instance of the class first.</span></span> <span data-ttu-id="f94b8-106">這些類別是與 <xref:System.IO.FileInfo> 和 <xref:System.IO.DirectoryInfo> 類別相關聯，對 `My` 功能的使用者而言這應該十分熟悉。</span><span class="sxs-lookup"><span data-stu-id="f94b8-106">Associated with these classes are the <xref:System.IO.FileInfo> and <xref:System.IO.DirectoryInfo> classes, which will be familiar to users of the `My` feature.</span></span> <span data-ttu-id="f94b8-107">若要使用這些類別，您必須完整限定名稱，或在受影響程式碼的開頭包含 `Imports` 陳述式來匯入適當的命名空間。</span><span class="sxs-lookup"><span data-stu-id="f94b8-107">To use these classes, you must fully qualify the names or import the appropriate namespaces by including the `Imports` statement(s) at the beginning of the affected code.</span></span> <span data-ttu-id="f94b8-108">如需詳細資訊，請參閱 [Imports 陳述式 (.NET 命名空間和類型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)。</span><span class="sxs-lookup"><span data-stu-id="f94b8-108">For more information, see [Imports Statement (.NET Namespace and Type)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f94b8-109">本節中的其他主題使用 `My.Computer.FileSystem` 物件，而非處理磁碟機、檔案和目錄的 `System.IO` 類別。</span><span class="sxs-lookup"><span data-stu-id="f94b8-109">Other topics in this section use the `My.Computer.FileSystem` object instead of `System.IO` classes to work with drives, files, and directories.</span></span> <span data-ttu-id="f94b8-110">`My.Computer.FileSystem` 物件主要用於 Visual Basic 程式。</span><span class="sxs-lookup"><span data-stu-id="f94b8-110">The `My.Computer.FileSystem` object is intended primarily for use in Visual Basic programs.</span></span> <span data-ttu-id="f94b8-111">`System.IO` 類別旨在由任何支援 .NET Framework 的語言使用，包括 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="f94b8-111">`System.IO` classes are intended for use by any language that supports the .NET Framework, including Visual Basic.</span></span>

## <a name="definition-of-a-stream"></a><span data-ttu-id="f94b8-112">資料流的定義</span><span class="sxs-lookup"><span data-stu-id="f94b8-112">Definition of a Stream</span></span>

<span data-ttu-id="f94b8-113">.NET Framework 使用資料流來支援讀取和寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="f94b8-113">The .NET Framework uses streams to support reading from and writing to files.</span></span> <span data-ttu-id="f94b8-114">您可以將資料流視為一組包含開始和結束的一維連續資料，而資料指標表示目前在資料流中的位置。</span><span class="sxs-lookup"><span data-stu-id="f94b8-114">You can think of a stream as a one-dimensional set of contiguous data, which has a beginning and an end, and where the cursor indicates the current position in the stream.</span></span>

![游標顯示目前在 FileStream 中的位置。](./media/basics-of-net-framework-file-io-and-the-file-system/filestream-cursor-position.gif)

## <a name="stream-operations"></a><span data-ttu-id="f94b8-116">資料流作業</span><span class="sxs-lookup"><span data-stu-id="f94b8-116">Stream Operations</span></span>

<span data-ttu-id="f94b8-117">資料流中所包含的資料可能來自記憶體、檔案或 TCP/IP 通訊端。</span><span class="sxs-lookup"><span data-stu-id="f94b8-117">The data contained in the stream may come from memory, a file, or a TCP/IP socket.</span></span> <span data-ttu-id="f94b8-118">資料流具有可套用至它們的基本作業︰</span><span class="sxs-lookup"><span data-stu-id="f94b8-118">Streams have fundamental operations that can be applied to them:</span></span>

- <span data-ttu-id="f94b8-119">**正在讀取**。</span><span class="sxs-lookup"><span data-stu-id="f94b8-119">**Reading**.</span></span> <span data-ttu-id="f94b8-120">您可以讀取資料流，方法是將資料從資料流傳送至資料結構 (例如字串或位元組陣列)。</span><span class="sxs-lookup"><span data-stu-id="f94b8-120">You can read from a stream, transferring data from the stream into a data structure, such as a string or an array of bytes.</span></span>

- <span data-ttu-id="f94b8-121">**撰寫**。</span><span class="sxs-lookup"><span data-stu-id="f94b8-121">**Writing**.</span></span> <span data-ttu-id="f94b8-122">將資料從資料來源傳送至資料流，即可寫入資料流。</span><span class="sxs-lookup"><span data-stu-id="f94b8-122">You can write to a stream, transferring data from a data source into the stream.</span></span>

- <span data-ttu-id="f94b8-123">**搜尋**。</span><span class="sxs-lookup"><span data-stu-id="f94b8-123">**Seeking**.</span></span> <span data-ttu-id="f94b8-124">您可以查詢和修改您在資料流中的位置。</span><span class="sxs-lookup"><span data-stu-id="f94b8-124">You can query and modify your position in the stream.</span></span>

<span data-ttu-id="f94b8-125">如需詳細資訊，請參閱 [Composing Streams](../../../../standard/io/composing-streams.md)。</span><span class="sxs-lookup"><span data-stu-id="f94b8-125">For more information, see [Composing Streams](../../../../standard/io/composing-streams.md).</span></span>

## <a name="types-of-streams"></a><span data-ttu-id="f94b8-126">資料流類型</span><span class="sxs-lookup"><span data-stu-id="f94b8-126">Types of Streams</span></span>

<span data-ttu-id="f94b8-127">在 .NET Framework 中，資料流是透過 <xref:System.IO.Stream> 類別呈現，構成所有其他資料流的抽象類別。</span><span class="sxs-lookup"><span data-stu-id="f94b8-127">In the .NET Framework, a stream is represented by the <xref:System.IO.Stream> class, which forms the abstract class for all other streams.</span></span> <span data-ttu-id="f94b8-128">您無法直接建立 <xref:System.IO.Stream> 類別執行個體，但必須使用它所實作的其中一個類別。</span><span class="sxs-lookup"><span data-stu-id="f94b8-128">You cannot directly create an instance of the <xref:System.IO.Stream> class, but must use one of the classes it implements.</span></span>

<span data-ttu-id="f94b8-129">有許多類型的資料流，但若要使用檔案輸入/輸出 (I/O)，最重要的類型是可讀取和寫入檔案的 <xref:System.IO.FileStream> 類別，以及可在隔離儲存體中建立檔案和目錄的 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 類別。</span><span class="sxs-lookup"><span data-stu-id="f94b8-129">There are many types of streams, but for the purposes of working with file input/output (I/O), the most important types are the <xref:System.IO.FileStream> class, which provides a way to read from and write to files, and the <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> class, which provides a way to create files and directories in isolated storage.</span></span> <span data-ttu-id="f94b8-130">可以在使用檔案 I/O 時使用的其他資料流包括︰</span><span class="sxs-lookup"><span data-stu-id="f94b8-130">Other streams that can be used when working with file I/O include:</span></span>

- <xref:System.IO.BufferedStream>

- <xref:System.Security.Cryptography.CryptoStream>

- <xref:System.IO.MemoryStream>

- <span data-ttu-id="f94b8-131"><xref:System.Net.Sockets.NetworkStream>.</span><span class="sxs-lookup"><span data-stu-id="f94b8-131"><xref:System.Net.Sockets.NetworkStream>.</span></span>

<span data-ttu-id="f94b8-132">下表列出一般會使用資料流來完成的工作︰</span><span class="sxs-lookup"><span data-stu-id="f94b8-132">The following table lists tasks commonly accomplished with a stream:</span></span>

|<span data-ttu-id="f94b8-133">至</span><span class="sxs-lookup"><span data-stu-id="f94b8-133">To</span></span>|<span data-ttu-id="f94b8-134">請參閱</span><span class="sxs-lookup"><span data-stu-id="f94b8-134">See</span></span>|
|---|---|
|<span data-ttu-id="f94b8-135">讀取和寫入資料檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-135">Read and write to a data file</span></span>|[<span data-ttu-id="f94b8-136">作法：讀取和寫入新建立的資料檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-136">How to: Read and Write to a Newly Created Data File</span></span>](../../../../standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|
|<span data-ttu-id="f94b8-137">從檔案讀取文字</span><span class="sxs-lookup"><span data-stu-id="f94b8-137">Read text from a file</span></span>|[<span data-ttu-id="f94b8-138">作法：讀取檔案中的文字</span><span class="sxs-lookup"><span data-stu-id="f94b8-138">How to: Read Text from a File</span></span>](../../../../standard/io/how-to-read-text-from-a-file.md)|
|<span data-ttu-id="f94b8-139">將文字寫入檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-139">Write text to a file</span></span>|[<span data-ttu-id="f94b8-140">作法：將文字寫入檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-140">How to: Write Text to a File</span></span>](../../../../standard/io/how-to-write-text-to-a-file.md)|
|<span data-ttu-id="f94b8-141">讀取字串中的字元</span><span class="sxs-lookup"><span data-stu-id="f94b8-141">Read characters from a string</span></span>|[<span data-ttu-id="f94b8-142">作法：讀取字串中的字元</span><span class="sxs-lookup"><span data-stu-id="f94b8-142">How to: Read Characters from a String</span></span>](../../../../standard/io/how-to-read-characters-from-a-string.md)|
|<span data-ttu-id="f94b8-143">將字元寫入字串中</span><span class="sxs-lookup"><span data-stu-id="f94b8-143">Write characters to a string</span></span>|[<span data-ttu-id="f94b8-144">作法：將字元寫入字串</span><span class="sxs-lookup"><span data-stu-id="f94b8-144">How to: Write Characters to a String</span></span>](../../../../standard/io/how-to-write-characters-to-a-string.md)|
|<span data-ttu-id="f94b8-145">加密資料</span><span class="sxs-lookup"><span data-stu-id="f94b8-145">Encrypt data</span></span>|[<span data-ttu-id="f94b8-146">加密資料</span><span class="sxs-lookup"><span data-stu-id="f94b8-146">Encrypting Data</span></span>](../../../../standard/security/encrypting-data.md)|
|<span data-ttu-id="f94b8-147">解密資料</span><span class="sxs-lookup"><span data-stu-id="f94b8-147">Decrypt data</span></span>|[<span data-ttu-id="f94b8-148">解密資料</span><span class="sxs-lookup"><span data-stu-id="f94b8-148">Decrypting Data</span></span>](../../../../standard/security/decrypting-data.md)|

## <a name="file-access-and-attributes"></a><span data-ttu-id="f94b8-149">檔案存取和屬性</span><span class="sxs-lookup"><span data-stu-id="f94b8-149">File Access and Attributes</span></span>

<span data-ttu-id="f94b8-150">您可以控制如何建立檔案、如何開啟檔案，以及如何與 <xref:System.IO.FileAccess>、<xref:System.IO.FileMode> 和 <xref:System.IO.FileShare> 列舉共用，而列舉包含 <xref:System.IO.FileStream> 類別的建構函式所使用的旗標。</span><span class="sxs-lookup"><span data-stu-id="f94b8-150">You can control how files are created, opened, and shared with the <xref:System.IO.FileAccess>, <xref:System.IO.FileMode>, and <xref:System.IO.FileShare> enumerations, which contain the flags used by the constructors of the <xref:System.IO.FileStream> class.</span></span> <span data-ttu-id="f94b8-151">例如，當您開啟或建立新 <xref:System.IO.FileStream> 時，<xref:System.IO.FileMode> 列舉可讓您指定是否開啟檔案以進行附加、是否在指定的檔案不存在時建立新檔案、是否覆寫檔案等等。</span><span class="sxs-lookup"><span data-stu-id="f94b8-151">For example, when you open or create a new <xref:System.IO.FileStream>, the <xref:System.IO.FileMode> enumeration allows you to specify whether the file is opened for appending, whether a new file is created if the specified file does not exist, whether the file is overwritten, and so forth.</span></span>

<span data-ttu-id="f94b8-152"><xref:System.IO.FileAttributes> 列舉類型可收集檔案特定資訊。</span><span class="sxs-lookup"><span data-stu-id="f94b8-152">The <xref:System.IO.FileAttributes> enumeration enables the gathering of file-specific information.</span></span> <span data-ttu-id="f94b8-153"><xref:System.IO.FileAttributes> 列舉會傳回檔案的預存屬性，例如是否壓縮、加密、隱藏、唯讀、封存、目錄、系統檔案或暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="f94b8-153">The <xref:System.IO.FileAttributes> enumeration returns the file's stored attributes, such as whether it is compressed, encrypted, hidden, read-only, an archive, a directory, a system file, or a temporary file.</span></span>

<span data-ttu-id="f94b8-154">下表列出與檔案存取和檔案屬性有關的工作︰</span><span class="sxs-lookup"><span data-stu-id="f94b8-154">The following table lists tasks involving file access and file attributes:</span></span>

|<span data-ttu-id="f94b8-155">至</span><span class="sxs-lookup"><span data-stu-id="f94b8-155">To</span></span>|<span data-ttu-id="f94b8-156">請參閱</span><span class="sxs-lookup"><span data-stu-id="f94b8-156">See</span></span>|
|---|---|
|<span data-ttu-id="f94b8-157">開啟文字並將其附加至記錄檔</span><span class="sxs-lookup"><span data-stu-id="f94b8-157">Open and append text to a log file</span></span>|[<span data-ttu-id="f94b8-158">作法：開啟並附加至記錄檔</span><span class="sxs-lookup"><span data-stu-id="f94b8-158">How to: Open and Append to a Log File</span></span>](../../../../standard/io/how-to-open-and-append-to-a-log-file.md)|
|<span data-ttu-id="f94b8-159">判斷檔案的屬性</span><span class="sxs-lookup"><span data-stu-id="f94b8-159">Determine the attributes of a file</span></span>|<xref:System.IO.FileAttributes>|

## <a name="file-permissions"></a><span data-ttu-id="f94b8-160">檔案權限</span><span class="sxs-lookup"><span data-stu-id="f94b8-160">File Permissions</span></span>

<span data-ttu-id="f94b8-161">使用 <xref:System.Security.Permissions.FileIOPermission> 類別可以控制檔案和目錄的存取。</span><span class="sxs-lookup"><span data-stu-id="f94b8-161">Controlling access to files and directories can be done with the <xref:System.Security.Permissions.FileIOPermission> class.</span></span> <span data-ttu-id="f94b8-162">這對於使用 Web Form 的開發人員來說可能特別重要，其根據預設在名為 ASPNET 的特殊本機使用者帳戶內容中執行，而該帳戶則是在 ASP.NET 和 .NET Framework 安裝期間一同建立的。</span><span class="sxs-lookup"><span data-stu-id="f94b8-162">This may be particularly important for developers working with Web Forms, which by default run within the context of a special local user account named ASPNET, which is created as part of the ASP.NET and .NET Framework installations.</span></span> <span data-ttu-id="f94b8-163">當這類應用程式要求存取資源時，ASPNET 使用者帳戶會具有有限的權限，這樣可能會讓使用者無法執行從 Web 應用程式寫入檔案這類動作。</span><span class="sxs-lookup"><span data-stu-id="f94b8-163">When such an application requests access to a resource, the ASPNET user account has limited permissions, which may prevent the user from performing actions such as writing to a file from a Web application.</span></span> <span data-ttu-id="f94b8-164">如需詳細資訊，請參閱 <xref:System.Security.Permissions.FileIOPermission> 。</span><span class="sxs-lookup"><span data-stu-id="f94b8-164">For more information, see <xref:System.Security.Permissions.FileIOPermission>.</span></span>

## <a name="isolated-file-storage"></a><span data-ttu-id="f94b8-165">隔離檔案儲存區</span><span class="sxs-lookup"><span data-stu-id="f94b8-165">Isolated File Storage</span></span>

<span data-ttu-id="f94b8-166">隔離儲存區是嘗試解決處理使用者或程式碼可能缺乏必要權限的檔案時所產生的問題。</span><span class="sxs-lookup"><span data-stu-id="f94b8-166">Isolated storage is an attempt to solve problems created when working with files where the user or code may lack necessary permissions.</span></span> <span data-ttu-id="f94b8-167">隔離儲存區會將資料區間指派給每位使用者，以保留一或多個存放區。</span><span class="sxs-lookup"><span data-stu-id="f94b8-167">Isolated storage assigns each user a data compartment, which can hold one or more stores.</span></span> <span data-ttu-id="f94b8-168">存放區可以依使用者和組件彼此隔離。</span><span class="sxs-lookup"><span data-stu-id="f94b8-168">Stores can be isolated from each other by user and by assembly.</span></span> <span data-ttu-id="f94b8-169">只有建立存放區的使用者和組件才能存取存放區。</span><span class="sxs-lookup"><span data-stu-id="f94b8-169">Only the user and assembly that created a store have access to it.</span></span> <span data-ttu-id="f94b8-170">存放區是完整虛擬檔案系統；您可以在一個存放區內建立和管理目錄與檔案。</span><span class="sxs-lookup"><span data-stu-id="f94b8-170">A store acts as a complete virtual file system—within one store you can create and manipulate directories and files.</span></span>

<span data-ttu-id="f94b8-171">下表列出一般與隔離檔案儲存區相關聯的工作。</span><span class="sxs-lookup"><span data-stu-id="f94b8-171">The following table lists tasks commonly associated with isolated file storage.</span></span>

|<span data-ttu-id="f94b8-172">至</span><span class="sxs-lookup"><span data-stu-id="f94b8-172">To</span></span>|<span data-ttu-id="f94b8-173">請參閱</span><span class="sxs-lookup"><span data-stu-id="f94b8-173">See</span></span>|
|---|---|
|<span data-ttu-id="f94b8-174">建立隔離存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-174">Create an isolated store</span></span>|[<span data-ttu-id="f94b8-175">作法：取得隔離儲存區的存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-175">How to: Obtain Stores for Isolated Storage</span></span>](../../../../standard/io/how-to-obtain-stores-for-isolated-storage.md)|
|<span data-ttu-id="f94b8-176">列舉隔離存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-176">Enumerate isolated stores</span></span>|[<span data-ttu-id="f94b8-177">作法：列舉隔離儲存區的存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-177">How to: Enumerate Stores for Isolated Storage</span></span>](../../../../standard/io/how-to-enumerate-stores-for-isolated-storage.md)|
|<span data-ttu-id="f94b8-178">刪除隔離存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-178">Delete an isolated store</span></span>|[<span data-ttu-id="f94b8-179">作法：刪除隔離儲存區中的存放區</span><span class="sxs-lookup"><span data-stu-id="f94b8-179">How to: Delete Stores in Isolated Storage</span></span>](../../../../standard/io/how-to-delete-stores-in-isolated-storage.md)|
|<span data-ttu-id="f94b8-180">在隔離儲存區中建立檔案或目錄</span><span class="sxs-lookup"><span data-stu-id="f94b8-180">Create a file or directory in isolated storage</span></span>|[<span data-ttu-id="f94b8-181">作法：在隔離儲存區中建立檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="f94b8-181">How to: Create Files and Directories in Isolated Storage</span></span>](../../../../standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|
|<span data-ttu-id="f94b8-182">在隔離儲存區中尋找檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-182">Find a file in isolated storage</span></span>|[<span data-ttu-id="f94b8-183">作法：尋找隔離儲存區中的現有檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="f94b8-183">How to: Find Existing Files and Directories in Isolated Storage</span></span>](../../../../standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|
|<span data-ttu-id="f94b8-184">讀取或寫入隔離儲存區中的檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-184">Read from or write to a file in isolated storage</span></span>|[<span data-ttu-id="f94b8-185">作法：讀取和寫入隔離儲存區中的檔案</span><span class="sxs-lookup"><span data-stu-id="f94b8-185">How to: Read and Write to Files in Isolated Storage</span></span>](../../../../standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|
|<span data-ttu-id="f94b8-186">刪除隔離儲存區中的檔案或目錄</span><span class="sxs-lookup"><span data-stu-id="f94b8-186">Delete a file or directory in isolated storage</span></span>|[<span data-ttu-id="f94b8-187">作法：刪除隔離儲存區中的檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="f94b8-187">How to: Delete Files and Directories in Isolated Storage</span></span>](../../../../standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|

## <a name="file-events"></a><span data-ttu-id="f94b8-188">檔案事件</span><span class="sxs-lookup"><span data-stu-id="f94b8-188">File Events</span></span>

<span data-ttu-id="f94b8-189"><xref:System.IO.FileSystemWatcher> 元件可讓您監看系統或任何具有網路存取之電腦上的檔案和目錄變更。</span><span class="sxs-lookup"><span data-stu-id="f94b8-189">The <xref:System.IO.FileSystemWatcher> component allows you to watch for changes in files and directories on your system or on any computer to which you have network access.</span></span> <span data-ttu-id="f94b8-190">例如，如果修改檔案，您可能要將已進行變更的警示傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="f94b8-190">For example, if a file is modified, you might want to send a user an alert that the change has taken place.</span></span> <span data-ttu-id="f94b8-191">發生變更時，會引發一或多個事件、將其儲存在緩衝區中，並且交給 <xref:System.IO.FileSystemWatcher> 元件進行處理。</span><span class="sxs-lookup"><span data-stu-id="f94b8-191">When changes occur, one or more events are raised, stored in a buffer, and handed to the <xref:System.IO.FileSystemWatcher> component for processing.</span></span>

## <a name="see-also"></a><span data-ttu-id="f94b8-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f94b8-192">See also</span></span>

- [<span data-ttu-id="f94b8-193">撰寫資料流</span><span class="sxs-lookup"><span data-stu-id="f94b8-193">Composing Streams</span></span>](../../../../standard/io/composing-streams.md)
- [<span data-ttu-id="f94b8-194">檔案和資料流程 i/o</span><span class="sxs-lookup"><span data-stu-id="f94b8-194">File and Stream I/O</span></span>](../../../../standard/io/index.md)
- [<span data-ttu-id="f94b8-195">非同步檔案 i/o</span><span class="sxs-lookup"><span data-stu-id="f94b8-195">Asynchronous File I/O</span></span>](../../../../standard/io/asynchronous-file-i-o.md)
- [<span data-ttu-id="f94b8-196">用於 .NET Framework 檔案 I/O 和檔案系統的類別 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f94b8-196">Classes Used in .NET Framework File I/O and the File System (Visual Basic)</span></span>](classes-used-in-net-framework-file-io-and-the-file-system.md)
