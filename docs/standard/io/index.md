---
title: 檔案與資料流 I/O - .NET
description: 瞭解檔案和資料流程 i/o 的基本概念，也就是在 .NET 中從儲存媒體傳輸資料。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- IO namespace
- files, I/O
- System.IO namespace
- I/O [.NET Framework]
- streams, I/O
- data streams, I/O
ms.assetid: 4f4a33a9-66b7-4cd7-a285-4ad3e4276cd2
ms.openlocfilehash: 2761d17846009ba06a2ffb1fc58b430f3ec9a949
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662715"
---
# <a name="file-and-stream-io"></a><span data-ttu-id="4745b-103">檔案和資料流 I/O</span><span class="sxs-lookup"><span data-stu-id="4745b-103">File and Stream I/O</span></span>

<span data-ttu-id="4745b-104">檔案和資料流 I/O (輸入/輸出) 是指對儲存媒體來回傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="4745b-104">File and stream I/O (input/output) refers to the transfer of data either to or from a storage medium.</span></span> <span data-ttu-id="4745b-105">在 .NET Framework 中，`System.IO` 命名空間包含能夠以同步和非同步方式在資料流和檔案上進行讀取和寫入的類型。</span><span class="sxs-lookup"><span data-stu-id="4745b-105">In the .NET Framework, the `System.IO` namespaces contain types that enable reading and writing, both synchronously and asynchronously, on data streams and files.</span></span> <span data-ttu-id="4745b-106">這些命名空間還包含對檔案進行壓縮和解壓縮的類型，以及透過管道和序列埠進行通訊的類型。</span><span class="sxs-lookup"><span data-stu-id="4745b-106">These namespaces also contain types that perform compression and decompression on files, and types that enable communication through pipes and serial ports.</span></span>

<span data-ttu-id="4745b-107">檔案是具有永續性存放裝置的已排序具名位元組集合。</span><span class="sxs-lookup"><span data-stu-id="4745b-107">A file is an ordered and named collection of bytes that has persistent storage.</span></span> <span data-ttu-id="4745b-108">當您使用檔案時，也會處理目錄路徑、磁碟存放裝置，以及檔案和目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="4745b-108">When you work with files, you work with directory paths, disk storage, and file and directory names.</span></span> <span data-ttu-id="4745b-109">相反地，資料流是可以用來讀取和寫入備份存放區的位元組序列，這類備份存放區可以是數種儲存媒體的其中一種 (例如磁碟或記憶體)。</span><span class="sxs-lookup"><span data-stu-id="4745b-109">In contrast, a stream is a sequence of bytes that you can use to read from and write to a backing store, which can be one of several storage mediums (for example, disks or memory).</span></span> <span data-ttu-id="4745b-110">就像除了磁碟以外，還有多種備份存放區一樣，資料流的種類除了檔案資料流之外，還有其他數種，例如網路、記憶體和管道資料流。</span><span class="sxs-lookup"><span data-stu-id="4745b-110">Just as there are several backing stores other than disks, there are several kinds of streams other than file streams, such as network, memory, and pipe streams.</span></span>

## <a name="files-and-directories"></a><span data-ttu-id="4745b-111">檔案和目錄</span><span class="sxs-lookup"><span data-stu-id="4745b-111">Files and directories</span></span>

<span data-ttu-id="4745b-112">您可以使用 <xref:System.IO?displayProperty=nameWithType> 命名空間中的類型與檔案和目錄互動。</span><span class="sxs-lookup"><span data-stu-id="4745b-112">You can use the types in the <xref:System.IO?displayProperty=nameWithType> namespace to interact with files and directories.</span></span> <span data-ttu-id="4745b-113">例如，您可以取得及設定檔案和目錄的屬性，並且根據搜尋條件擷取檔案和目錄集合。</span><span class="sxs-lookup"><span data-stu-id="4745b-113">For example, you can get and set properties for files and directories, and retrieve collections of files and directories based on search criteria.</span></span>

<span data-ttu-id="4745b-114">如需 Windows 系統的路徑命名慣例及檔案路徑表達方式，包括 .NET Core 1.1 及更新版本和 .NET Framework 4.6.2 及更新版本中支援的 DOS 裝置語法，請參閱 [Windows 系統上的檔案路徑格式](file-path-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-114">For path naming conventions and the ways to express a file path for Windows systems, including with the DOS device syntax supported in .NET Core 1.1 and later and the .NET Framework 4.6.2 and later, see [File path formats on Windows systems](file-path-formats.md).</span></span>

<span data-ttu-id="4745b-115">以下是常用的檔案和目錄類別：</span><span class="sxs-lookup"><span data-stu-id="4745b-115">Here are some commonly used file and directory classes:</span></span>

- <span data-ttu-id="4745b-116"><xref:System.IO.File> - 提供建立、複製、刪除、移動和開啟檔案的靜態方法，並協助建立 <xref:System.IO.FileStream> 物件。</span><span class="sxs-lookup"><span data-stu-id="4745b-116"><xref:System.IO.File> - provides static methods for creating, copying, deleting, moving, and opening files, and helps create a <xref:System.IO.FileStream> object.</span></span>

- <span data-ttu-id="4745b-117"><xref:System.IO.FileInfo> - 提供建立、複製、刪除、移動和開啟檔案的執行個體方法，並協助建立 <xref:System.IO.FileStream> 物件。</span><span class="sxs-lookup"><span data-stu-id="4745b-117"><xref:System.IO.FileInfo> - provides instance methods for creating, copying, deleting, moving, and opening files, and helps create a <xref:System.IO.FileStream> object.</span></span>

- <span data-ttu-id="4745b-118"><xref:System.IO.Directory> - 提供建立、移動和列舉目錄和子目錄的靜態方法。</span><span class="sxs-lookup"><span data-stu-id="4745b-118"><xref:System.IO.Directory> - provides static methods for creating, moving, and enumerating through directories and subdirectories.</span></span>

- <span data-ttu-id="4745b-119"><xref:System.IO.DirectoryInfo> - 提供建立、移動和列舉目錄和子目錄的執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="4745b-119"><xref:System.IO.DirectoryInfo> - provides instance methods for creating, moving, and enumerating through directories and subdirectories.</span></span>

- <span data-ttu-id="4745b-120"><xref:System.IO.Path> - 提供以跨平台方式處理目錄字串的方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="4745b-120"><xref:System.IO.Path> - provides methods and properties for processing directory strings in a cross-platform manner.</span></span>

<span data-ttu-id="4745b-121">您應該在呼叫檔案系統方法時，一律提供強固的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="4745b-121">You should always provide robust exception handling when calling filesystem methods.</span></span> <span data-ttu-id="4745b-122">如需詳細資訊，請參閱[處理 I/O 錯誤](handling-io-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-122">For more information, see [Handling I/O errors](handling-io-errors.md).</span></span>

<span data-ttu-id="4745b-123">除了使用這些類別之外，Visual Basic 使用者還可以使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=nameWithType> 類別針對檔案 I/O 提供的方法。</span><span class="sxs-lookup"><span data-stu-id="4745b-123">In addition to using these classes, Visual Basic users can use the methods and properties provided by the <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=nameWithType> class for file I/O.</span></span>

<span data-ttu-id="4745b-124">請參閱[如何：複製目錄](how-to-copy-directories.md)、[如何：建立目錄清單](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100))，以及[如何：列舉目錄和檔案](how-to-enumerate-directories-and-files.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-124">See [How to: Copy Directories](how-to-copy-directories.md), [How to: Create a Directory Listing](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100)), and [How to: Enumerate Directories and Files](how-to-enumerate-directories-and-files.md).</span></span>

## <a name="streams"></a><span data-ttu-id="4745b-125">資料流</span><span class="sxs-lookup"><span data-stu-id="4745b-125">Streams</span></span>

<span data-ttu-id="4745b-126">抽象基底類別 <xref:System.IO.Stream> 支援讀取和寫入位元組。</span><span class="sxs-lookup"><span data-stu-id="4745b-126">The abstract base class <xref:System.IO.Stream> supports reading and writing bytes.</span></span> <span data-ttu-id="4745b-127">代表繼承自 <xref:System.IO.Stream> 類別之資料流的所有類別。</span><span class="sxs-lookup"><span data-stu-id="4745b-127">All classes that represent streams inherit from the <xref:System.IO.Stream> class.</span></span> <span data-ttu-id="4745b-128"><xref:System.IO.Stream> 類別和它的衍生類別提供了資料來源和儲存機制的一般觀點，並且將程式設計人員與作業系統和基礎裝置的特有詳細資料加以隔離。</span><span class="sxs-lookup"><span data-stu-id="4745b-128">The <xref:System.IO.Stream> class and its derived classes provide a common view of data sources and repositories, and isolate the programmer from the specific details of the operating system and underlying devices.</span></span>

<span data-ttu-id="4745b-129">資料流包含三項基本作業：</span><span class="sxs-lookup"><span data-stu-id="4745b-129">Streams involve three fundamental operations:</span></span>

- <span data-ttu-id="4745b-130">讀取 - 從資料流將資料傳送至資料結構，例如位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="4745b-130">Reading - transferring data from a stream into a data structure, such as an array of bytes.</span></span>

- <span data-ttu-id="4745b-131">寫入 - 從資料來源將資料傳送至資料流。</span><span class="sxs-lookup"><span data-stu-id="4745b-131">Writing - transferring data to a stream from a data source.</span></span>

- <span data-ttu-id="4745b-132">搜尋 - 查詢和修改資料流內的目前位置。</span><span class="sxs-lookup"><span data-stu-id="4745b-132">Seeking - querying and modifying the current position within a stream.</span></span>

<span data-ttu-id="4745b-133">依據基礎資料來源或儲存機制而定，資料流可能只支援其中部分功能。</span><span class="sxs-lookup"><span data-stu-id="4745b-133">Depending on the underlying data source or repository, a stream might support only some of these capabilities.</span></span> <span data-ttu-id="4745b-134">例如，<xref:System.IO.Pipes.PipeStream> 類別不支援搜尋。</span><span class="sxs-lookup"><span data-stu-id="4745b-134">For example, the <xref:System.IO.Pipes.PipeStream> class does not support seeking.</span></span> <span data-ttu-id="4745b-135">資料流的 <xref:System.IO.Stream.CanRead%2A>、<xref:System.IO.Stream.CanWrite%2A> 和 <xref:System.IO.Stream.CanSeek%2A> 屬性會指定資料流支援的作業。</span><span class="sxs-lookup"><span data-stu-id="4745b-135">The <xref:System.IO.Stream.CanRead%2A>, <xref:System.IO.Stream.CanWrite%2A>, and <xref:System.IO.Stream.CanSeek%2A> properties of a stream specify the operations that the stream supports.</span></span>

<span data-ttu-id="4745b-136">以下是部分常用的資料流類別：</span><span class="sxs-lookup"><span data-stu-id="4745b-136">Here are some commonly used stream classes:</span></span>

- <span data-ttu-id="4745b-137"><xref:System.IO.FileStream> – 用於讀取和寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-137"><xref:System.IO.FileStream> – for reading and writing to a file.</span></span>

- <span data-ttu-id="4745b-138"><xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> – 用於讀取和寫入位於隔離儲存區中的檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-138"><xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> – for reading and writing to a file in isolated storage.</span></span>

- <span data-ttu-id="4745b-139"><xref:System.IO.MemoryStream> – 用於讀取和寫入做為備份存放區的記憶體。</span><span class="sxs-lookup"><span data-stu-id="4745b-139"><xref:System.IO.MemoryStream> – for reading and writing to memory as the backing store.</span></span>

- <span data-ttu-id="4745b-140"><xref:System.IO.BufferedStream> – 用於改善讀取和寫入作業的效能。</span><span class="sxs-lookup"><span data-stu-id="4745b-140"><xref:System.IO.BufferedStream> – for improving performance of read and write operations.</span></span>

- <span data-ttu-id="4745b-141"><xref:System.Net.Sockets.NetworkStream> – 用於透過網路通訊端讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="4745b-141"><xref:System.Net.Sockets.NetworkStream> – for reading and writing over network sockets.</span></span>

- <span data-ttu-id="4745b-142"><xref:System.IO.Pipes.PipeStream> – 用於透過匿名和具名管道讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="4745b-142"><xref:System.IO.Pipes.PipeStream> – for reading and writing over anonymous and named pipes.</span></span>

- <span data-ttu-id="4745b-143"><xref:System.Security.Cryptography.CryptoStream> – 用於將資料流連結至密碼編譯的轉換作業。</span><span class="sxs-lookup"><span data-stu-id="4745b-143"><xref:System.Security.Cryptography.CryptoStream> – for linking data streams to cryptographic transformations.</span></span>

<span data-ttu-id="4745b-144">以非同步方式處理資料流的範例，請參閱[非同步檔案 I/O](asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-144">For an example of working with streams asynchronously, see [Asynchronous File I/O](asynchronous-file-i-o.md).</span></span>

## <a name="readers-and-writers"></a><span data-ttu-id="4745b-145">讀取器及寫入器</span><span class="sxs-lookup"><span data-stu-id="4745b-145">Readers and writers</span></span>

<span data-ttu-id="4745b-146"><xref:System.IO?displayProperty=nameWithType> 命名空間提供從資料流讀取編碼字元以及將編碼字元寫入資料流的類型。</span><span class="sxs-lookup"><span data-stu-id="4745b-146">The <xref:System.IO?displayProperty=nameWithType> namespace also provides types for reading encoded characters from streams and writing them to streams.</span></span> <span data-ttu-id="4745b-147">通常資料流是針對位元組輸入和輸出所設計。</span><span class="sxs-lookup"><span data-stu-id="4745b-147">Typically, streams are designed for byte input and output.</span></span> <span data-ttu-id="4745b-148">讀取器和寫入器類型會處理編碼字元與位元組之間的轉換，讓資料流能夠完成作業。</span><span class="sxs-lookup"><span data-stu-id="4745b-148">The reader and writer types handle the conversion of the encoded characters to and from bytes so the stream can complete the operation.</span></span> <span data-ttu-id="4745b-149">每個讀取器和寫入器類別都會與資料流相關聯，可透過類別的 `BaseStream` 屬性擷取。</span><span class="sxs-lookup"><span data-stu-id="4745b-149">Each reader and writer class is associated with a stream, which can be retrieved through the class's `BaseStream` property.</span></span>

<span data-ttu-id="4745b-150">以下是常用的讀取器和寫入器類別：</span><span class="sxs-lookup"><span data-stu-id="4745b-150">Here are some commonly used reader and writer classes:</span></span>

- <span data-ttu-id="4745b-151"><xref:System.IO.BinaryReader> 和 <xref:System.IO.BinaryWriter> – 用於將基本資料類型當做二進位值讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="4745b-151"><xref:System.IO.BinaryReader> and <xref:System.IO.BinaryWriter> – for reading and writing primitive data types as binary values.</span></span>

- <span data-ttu-id="4745b-152"><xref:System.IO.StreamReader> 和 <xref:System.IO.StreamWriter> – 使用編碼值在字元與位元組之間進行轉換的方式讀取和寫入字元。</span><span class="sxs-lookup"><span data-stu-id="4745b-152"><xref:System.IO.StreamReader> and <xref:System.IO.StreamWriter> – for reading and writing characters by using an encoding value to convert the characters to and from bytes.</span></span>

- <span data-ttu-id="4745b-153"><xref:System.IO.StringReader> 和 <xref:System.IO.StringWriter> – 從字串讀取字元以及將字元寫入字串。</span><span class="sxs-lookup"><span data-stu-id="4745b-153"><xref:System.IO.StringReader> and <xref:System.IO.StringWriter> – for reading and writing characters to and from strings.</span></span>

- <span data-ttu-id="4745b-154"><xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter> – 做為其他讀取和寫入二進位資料以外的字元與字串之讀取器和寫入器的抽象基底類別。</span><span class="sxs-lookup"><span data-stu-id="4745b-154"><xref:System.IO.TextReader> and <xref:System.IO.TextWriter> – serve as the abstract base classes for other readers and writers that read and write characters and strings, but not binary data.</span></span>

<span data-ttu-id="4745b-155">請參閱[如何：從檔案讀取文字](how-to-read-text-from-a-file.md)、[如何：將文字寫入檔案](how-to-write-text-to-a-file.md)、[如何：從字串讀取字元](how-to-read-characters-from-a-string.md)，以及[如何：將字元寫入字串](how-to-write-characters-to-a-string.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-155">See [How to: Read Text from a File](how-to-read-text-from-a-file.md), [How to: Write Text to a File](how-to-write-text-to-a-file.md), [How to: Read Characters from a String](how-to-read-characters-from-a-string.md), and [How to: Write Characters to a String](how-to-write-characters-to-a-string.md).</span></span>

## <a name="asynchronous-io-operations"></a><span data-ttu-id="4745b-156">非同步 I/O 作業</span><span class="sxs-lookup"><span data-stu-id="4745b-156">Asynchronous I/O operations</span></span>

<span data-ttu-id="4745b-157">讀取或寫入大量資料可能會耗用大量資源。</span><span class="sxs-lookup"><span data-stu-id="4745b-157">Reading or writing a large amount of data can be resource-intensive.</span></span> <span data-ttu-id="4745b-158">如果您的應用程式需要保持對使用者的回應能力，您應該以非同步方式執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="4745b-158">You should perform these tasks asynchronously if your application needs to remain responsive to the user.</span></span> <span data-ttu-id="4745b-159">進行同步 I/O 作業時，UI 執行緒會遭到封鎖，直至耗用資源的作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="4745b-159">With synchronous I/O operations, the UI thread is blocked until the resource-intensive operation has completed.</span></span>  <span data-ttu-id="4745b-160">開發 Windows 8.x 存放區應用程式時，請使用非同步 i/o 作業，以防止建立您的應用程式已停止運作的印象。</span><span class="sxs-lookup"><span data-stu-id="4745b-160">Use asynchronous I/O operations when developing Windows 8.x Store apps to prevent creating the impression that your app has stopped working.</span></span>

<span data-ttu-id="4745b-161">非同步成員的名稱中包含 `Async`，例如 <xref:System.IO.Stream.CopyToAsync%2A>、<xref:System.IO.Stream.FlushAsync%2A>、<xref:System.IO.Stream.ReadAsync%2A> 和 <xref:System.IO.Stream.WriteAsync%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="4745b-161">The asynchronous members contain `Async` in their names, such as the <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>,  <xref:System.IO.Stream.ReadAsync%2A>, and <xref:System.IO.Stream.WriteAsync%2A> methods.</span></span> <span data-ttu-id="4745b-162">這些方法可搭配 `async` 和 `await` 關鍵字使用。</span><span class="sxs-lookup"><span data-stu-id="4745b-162">You use these methods with the `async` and `await` keywords.</span></span>

<span data-ttu-id="4745b-163">如需詳細資訊，請參閱[非同步檔案 I/O](asynchronous-file-i-o.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-163">For more information, see [Asynchronous File I/O](asynchronous-file-i-o.md).</span></span>

## <a name="compression"></a><span data-ttu-id="4745b-164">壓縮</span><span class="sxs-lookup"><span data-stu-id="4745b-164">Compression</span></span>

<span data-ttu-id="4745b-165">壓縮是指縮減檔案大小以便儲存的程序。</span><span class="sxs-lookup"><span data-stu-id="4745b-165">Compression refers to the process of reducing the size of a file for storage.</span></span> <span data-ttu-id="4745b-166">解壓縮則是指擷取壓縮檔的內容使其成為可使用格式的程序。</span><span class="sxs-lookup"><span data-stu-id="4745b-166">Decompression is the process of extracting the contents of a compressed file so they are in a usable format.</span></span> <span data-ttu-id="4745b-167"><xref:System.IO.Compression?displayProperty=nameWithType> 命名空間包含壓縮及解壓縮檔案和資料流的類型。</span><span class="sxs-lookup"><span data-stu-id="4745b-167">The <xref:System.IO.Compression?displayProperty=nameWithType> namespace contains types for compressing and decompressing files and streams.</span></span>

<span data-ttu-id="4745b-168">以下是壓縮和解壓縮檔案和資料流時經常使用的類別：</span><span class="sxs-lookup"><span data-stu-id="4745b-168">The following classes are frequently used when compressing and decompressing files and streams:</span></span>

- <span data-ttu-id="4745b-169"><xref:System.IO.Compression.ZipArchive> – 用於建立和擷取 zip 封存中的項目。</span><span class="sxs-lookup"><span data-stu-id="4745b-169"><xref:System.IO.Compression.ZipArchive> – for creating and retrieving entries in the zip archive.</span></span>

- <span data-ttu-id="4745b-170"><xref:System.IO.Compression.ZipArchiveEntry> – 用於表示壓縮檔。</span><span class="sxs-lookup"><span data-stu-id="4745b-170"><xref:System.IO.Compression.ZipArchiveEntry> – for representing a compressed file.</span></span>

- <span data-ttu-id="4745b-171"><xref:System.IO.Compression.ZipFile> – 用於建立、擷取和開啟壓縮的封裝。</span><span class="sxs-lookup"><span data-stu-id="4745b-171"><xref:System.IO.Compression.ZipFile> – for creating,  extracting, and opening a compressed package.</span></span>

- <span data-ttu-id="4745b-172"><xref:System.IO.Compression.ZipFileExtensions> – 用於建立和擷取壓縮封裝中的項目。</span><span class="sxs-lookup"><span data-stu-id="4745b-172"><xref:System.IO.Compression.ZipFileExtensions> – for creating and extracting entries in a compressed package.</span></span>

- <span data-ttu-id="4745b-173"><xref:System.IO.Compression.DeflateStream> – 使用 Deflate 演算法壓縮及解壓縮資料流。</span><span class="sxs-lookup"><span data-stu-id="4745b-173"><xref:System.IO.Compression.DeflateStream> – for compressing and decompressing streams using the Deflate algorithm.</span></span>

- <span data-ttu-id="4745b-174"><xref:System.IO.Compression.GZipStream> – 以 gzip 資料格式壓縮和解壓縮資料流。</span><span class="sxs-lookup"><span data-stu-id="4745b-174"><xref:System.IO.Compression.GZipStream> – for compressing and decompressing streams in gzip data format.</span></span>

<span data-ttu-id="4745b-175">請參閱[如何：壓縮與解壓縮檔案](how-to-compress-and-extract-files.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-175">See [How to: Compress and Extract Files](how-to-compress-and-extract-files.md).</span></span>

## <a name="isolated-storage"></a><span data-ttu-id="4745b-176">隔離儲存區 (Isolated Storage)</span><span class="sxs-lookup"><span data-stu-id="4745b-176">Isolated storage</span></span>

<span data-ttu-id="4745b-177">隔離儲存區 (Isolated Storage) 為資料儲存機制，藉著定義標準化方式，將程式碼與儲存的資料產生關聯，以提供隔離和安全。</span><span class="sxs-lookup"><span data-stu-id="4745b-177">Isolated storage is a data storage mechanism that provides isolation and safety by defining standardized ways of associating code with saved data.</span></span> <span data-ttu-id="4745b-178">儲存區提供依使用者、組件和 (選擇性) 網域隔離的虛擬檔案系統。</span><span class="sxs-lookup"><span data-stu-id="4745b-178">The storage provides a virtual file system that is isolated by user, assembly, and (optionally) domain.</span></span> <span data-ttu-id="4745b-179">隔離儲存區在應用程式未具備存取使用者檔案的權限時特別實用。</span><span class="sxs-lookup"><span data-stu-id="4745b-179">Isolated storage is particularly useful when your application does not have permission to access user files.</span></span> <span data-ttu-id="4745b-180">您可以藉由電腦的安全性原則所控制的方式儲存應用程式的設定或檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-180">You can save settings or files for your application in a manner that is controlled by the computer's security policy.</span></span>

<span data-ttu-id="4745b-181">Windows 8.x 存放區應用程式無法使用隔離儲存區;相反地，請使用命名空間中的應用程式資料類別 <xref:Windows.Storage?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="4745b-181">Isolated storage is not available for Windows 8.x Store apps; instead, use application data classes in the <xref:Windows.Storage?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="4745b-182">如需詳細資訊，請參閱[應用程式資料](https://docs.microsoft.com/previous-versions/windows/apps/hh464917%28v=win.10%29)。</span><span class="sxs-lookup"><span data-stu-id="4745b-182">For more information, see [Application data](https://docs.microsoft.com/previous-versions/windows/apps/hh464917%28v=win.10%29).</span></span>

<span data-ttu-id="4745b-183">以下是實作隔離儲存區時經常使用的類別：</span><span class="sxs-lookup"><span data-stu-id="4745b-183">The following classes are frequently used when implementing isolated storage:</span></span>

- <span data-ttu-id="4745b-184"><xref:System.IO.IsolatedStorage.IsolatedStorage> – 提供隔離儲存區實作所使用的基底類別。</span><span class="sxs-lookup"><span data-stu-id="4745b-184"><xref:System.IO.IsolatedStorage.IsolatedStorage> – provides the base class for isolated storage implementations.</span></span>

- <span data-ttu-id="4745b-185"><xref:System.IO.IsolatedStorage.IsolatedStorageFile> – 提供包含檔案和目錄的隔離存放區域。</span><span class="sxs-lookup"><span data-stu-id="4745b-185"><xref:System.IO.IsolatedStorage.IsolatedStorageFile> – provides an isolated storage area that contains files and directories.</span></span>

- <span data-ttu-id="4745b-186"><xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> - 公開隔離儲存區內的檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-186"><xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> - exposes a file within isolated storage.</span></span>

<span data-ttu-id="4745b-187">請參閱[隔離儲存區](isolated-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-187">See [Isolated Storage](isolated-storage.md).</span></span>

## <a name="io-operations-in-windows-store-apps"></a><span data-ttu-id="4745b-188">在 Windows 市集應用程式中的 I/O 作業</span><span class="sxs-lookup"><span data-stu-id="4745b-188">I/O operations in Windows Store apps</span></span>

<span data-ttu-id="4745b-189">適用于 Windows 8.x 存放區應用程式的 .NET 包含許多用來讀取和寫入資料流程的類型;不過，此集合不包含所有的 .NET Framework i/o 類型。</span><span class="sxs-lookup"><span data-stu-id="4745b-189">The .NET for Windows 8.x Store apps contains many of the types for reading from and writing to streams; however, this set does not include all the .NET Framework I/O types.</span></span>

<span data-ttu-id="4745b-190">在 Windows 8.x Store 應用程式中使用 i/o 作業時，需要注意的一些重要差異：</span><span class="sxs-lookup"><span data-stu-id="4745b-190">Some important differences to note when using I/O operations in Windows 8.x Store apps:</span></span>

- <span data-ttu-id="4745b-191">與檔案作業特別相關的類型（例如 <xref:System.IO.File> 、 <xref:System.IO.FileInfo> <xref:System.IO.Directory> 和 <xref:System.IO.DirectoryInfo> ）不會包含在適用于 Windows 8.x 存放區應用程式的 .net 中。</span><span class="sxs-lookup"><span data-stu-id="4745b-191">Types specifically related to file operations, such as <xref:System.IO.File>, <xref:System.IO.FileInfo>, <xref:System.IO.Directory> and <xref:System.IO.DirectoryInfo>, are not included in the .NET for Windows 8.x Store apps.</span></span> <span data-ttu-id="4745b-192">您應該改為使用 Windows 執行階段之 <xref:Windows.Storage?displayProperty=nameWithType> 命名空間中的型別，例如 <xref:Windows.Storage.StorageFile> 與 <xref:Windows.Storage.StorageFolder>。</span><span class="sxs-lookup"><span data-stu-id="4745b-192">Instead, use the types in the <xref:Windows.Storage?displayProperty=nameWithType> namespace of the Windows Runtime, such as <xref:Windows.Storage.StorageFile> and <xref:Windows.Storage.StorageFolder>.</span></span>

- <span data-ttu-id="4745b-193">無法使用隔離儲存區，請改用[應用程式資料](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10))。</span><span class="sxs-lookup"><span data-stu-id="4745b-193">Isolated storage is not available; instead, use [application data](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10)).</span></span>

- <span data-ttu-id="4745b-194">使用非同步方法，例如 <xref:System.IO.Stream.ReadAsync%2A> 和 <xref:System.IO.Stream.WriteAsync%2A>，防止封鎖 UI 執行緒。</span><span class="sxs-lookup"><span data-stu-id="4745b-194">Use asynchronous methods, such as <xref:System.IO.Stream.ReadAsync%2A> and <xref:System.IO.Stream.WriteAsync%2A>, to prevent blocking the UI thread.</span></span>

- <span data-ttu-id="4745b-195">無法使用路徑壓縮類型 <xref:System.IO.Compression.ZipFile> 和 <xref:System.IO.Compression.ZipFileExtensions>。</span><span class="sxs-lookup"><span data-stu-id="4745b-195">The path-based compression types <xref:System.IO.Compression.ZipFile> and <xref:System.IO.Compression.ZipFileExtensions> are not available.</span></span> <span data-ttu-id="4745b-196">您應該改為使用 <xref:Windows.Storage.Compression?displayProperty=nameWithType> 命名空間中的型別。</span><span class="sxs-lookup"><span data-stu-id="4745b-196">Instead, use the types in the <xref:Windows.Storage.Compression?displayProperty=nameWithType> namespace.</span></span>

<span data-ttu-id="4745b-197">如有需要，您可以在 .NET Framework 資料流和 Windows 執行階段資料流之間進行轉換。</span><span class="sxs-lookup"><span data-stu-id="4745b-197">You can convert between .NET Framework streams and Windows Runtime streams, if necessary.</span></span> <span data-ttu-id="4745b-198">如需詳細資訊，請參閱[如何：在 .NET Framework 資料流程和 Windows 執行階段資料流程之間進行轉換](how-to-convert-between-dotnet-streams-and-winrt-streams.md) <xref:System.IO.WindowsRuntimeStreamExtensions> 。</span><span class="sxs-lookup"><span data-stu-id="4745b-198">For more information, see [How to: Convert Between .NET Framework Streams and Windows Runtime Streams](how-to-convert-between-dotnet-streams-and-winrt-streams.md) or <xref:System.IO.WindowsRuntimeStreamExtensions>.</span></span>

<span data-ttu-id="4745b-199">如需有關 Windows 8.x 存放區應用程式中 i/o 作業的詳細資訊，請參閱[快速入門：讀取和寫入](https://docs.microsoft.com/previous-versions/windows/apps/hh758325(v=win.10))檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-199">For more information about I/O operations in a Windows 8.x Store app, see [Quickstart: Reading and writing files](https://docs.microsoft.com/previous-versions/windows/apps/hh758325(v=win.10)).</span></span>

## <a name="io-and-security"></a><span data-ttu-id="4745b-200">I/O 及安全性</span><span class="sxs-lookup"><span data-stu-id="4745b-200">I/O and security</span></span>

<span data-ttu-id="4745b-201">當您使用 <xref:System.IO?displayProperty=nameWithType> 命名空間中的類別時，必須遵循作業系統安全性需求，例如存取控制清單 (ACL)，以控制對檔案和目錄的存取。</span><span class="sxs-lookup"><span data-stu-id="4745b-201">When you use the classes in the <xref:System.IO?displayProperty=nameWithType> namespace, you must follow operating system security requirements such as access control lists (ACLs) to control access to files and directories.</span></span> <span data-ttu-id="4745b-202">任何 <xref:System.Security.Permissions.FileIOPermission> 需求上都會附加這個需求。</span><span class="sxs-lookup"><span data-stu-id="4745b-202">This requirement is in addition to any <xref:System.Security.Permissions.FileIOPermission> requirements.</span></span> <span data-ttu-id="4745b-203">您可以用程式設計的方式管理 ACL。</span><span class="sxs-lookup"><span data-stu-id="4745b-203">You can manage ACLs programmatically.</span></span> <span data-ttu-id="4745b-204">如需詳細資訊，請參閱[如何：新增或移除存取控制清單項目](how-to-add-or-remove-access-control-list-entries.md)。</span><span class="sxs-lookup"><span data-stu-id="4745b-204">For more information, see [How to: Add or Remove Access Control List Entries](how-to-add-or-remove-access-control-list-entries.md).</span></span>

<span data-ttu-id="4745b-205">預設安全性原則可避免網際網路或內部網路應用程式存取使用者電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="4745b-205">Default security policies prevent Internet or intranet applications from accessing files on the user’s computer.</span></span> <span data-ttu-id="4745b-206">因此，撰寫將透過網際網路或內部網路下載的程式碼時，請不要使用需要實體檔案路徑的 I/O 類別。</span><span class="sxs-lookup"><span data-stu-id="4745b-206">Therefore, do not use the I/O classes that require a path to a physical file when writing code that will be downloaded over the Internet or intranet.</span></span> <span data-ttu-id="4745b-207">相反地，針對傳統 .NET Framework 應用程式使用[隔離儲存區](isolated-storage.md)，或使用 Windows 8.X 存放區應用[程式的應用程式資料](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10))。</span><span class="sxs-lookup"><span data-stu-id="4745b-207">Instead, use [isolated storage](isolated-storage.md) for traditional .NET Framework applications, or use [application data](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10)) for Windows 8.x Store apps.</span></span>

<span data-ttu-id="4745b-208">只會對已建構的資料流進行安全性檢查。</span><span class="sxs-lookup"><span data-stu-id="4745b-208">A security check is performed only when the stream is constructed.</span></span> <span data-ttu-id="4745b-209">因此，請不要開啟資料流，然後將它傳遞至較不受信任的程式碼或應用程式定義域。</span><span class="sxs-lookup"><span data-stu-id="4745b-209">Therefore, do not open a stream and then pass it to less-trusted code or application domains.</span></span>

## <a name="related-topics"></a><span data-ttu-id="4745b-210">相關主題</span><span class="sxs-lookup"><span data-stu-id="4745b-210">Related topics</span></span>

- <span data-ttu-id="4745b-211">[一般 i/o 工作](common-i-o-tasks.md)</span><span class="sxs-lookup"><span data-stu-id="4745b-211">[Common I/O Tasks](common-i-o-tasks.md)</span></span>\
<span data-ttu-id="4745b-212">提供與檔案、目錄和資料流相關聯的 I/O 工作清單，並且連結至每一項工作的相關內容和範例。</span><span class="sxs-lookup"><span data-stu-id="4745b-212">Provides a list of I/O tasks associated with files, directories, and streams, and links to relevant content and examples for each task.</span></span>

- <span data-ttu-id="4745b-213">[非同步檔案 i/o](asynchronous-file-i-o.md)</span><span class="sxs-lookup"><span data-stu-id="4745b-213">[Asynchronous File I/O](asynchronous-file-i-o.md)</span></span>\
<span data-ttu-id="4745b-214">描述非同步 I/O 的效能利益和基本作業。</span><span class="sxs-lookup"><span data-stu-id="4745b-214">Describes the performance advantages and basic operation of asynchronous I/O.</span></span>

- <span data-ttu-id="4745b-215">[隔離儲存區](isolated-storage.md)</span><span class="sxs-lookup"><span data-stu-id="4745b-215">[Isolated Storage](isolated-storage.md)</span></span>\
<span data-ttu-id="4745b-216">描述資料儲存機制，此機制藉著定義標準化方式將程式碼與儲存的資料產生關聯，以提供隔離和安全。</span><span class="sxs-lookup"><span data-stu-id="4745b-216">Describes a data storage mechanism that provides isolation and safety by defining standardized ways of associating code with saved data.</span></span>

- <span data-ttu-id="4745b-217">[Ray](pipe-operations.md)</span><span class="sxs-lookup"><span data-stu-id="4745b-217">[Pipes](pipe-operations.md)</span></span>\
<span data-ttu-id="4745b-218">描述 .NET Framework 中的非同步與具名管道作業。</span><span class="sxs-lookup"><span data-stu-id="4745b-218">Describes anonymous and named pipe operations in the .NET Framework.</span></span>

- <span data-ttu-id="4745b-219">[記憶體對應檔案](memory-mapped-files.md)</span><span class="sxs-lookup"><span data-stu-id="4745b-219">[Memory-Mapped Files](memory-mapped-files.md)</span></span>\
<span data-ttu-id="4745b-220">描述記憶體對應檔案，這些檔案包含磁碟檔案在虛擬記憶體中的內容。</span><span class="sxs-lookup"><span data-stu-id="4745b-220">Describes memory-mapped files, which contain the contents of files on disk in virtual memory.</span></span> <span data-ttu-id="4745b-221">您可以使用記憶體對應檔案來編輯超大的檔案，以及建立供處理序間通訊使用的共用記憶體。</span><span class="sxs-lookup"><span data-stu-id="4745b-221">You can use memory-mapped files to edit very large files and to create shared memory for interprocess communication.</span></span>
