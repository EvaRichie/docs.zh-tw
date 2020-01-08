---
title: 擴充功能
ms.date: 12/13/2019
description: 瞭解如何載入 SQLite 延伸模組。
ms.openlocfilehash: ab00ccf31b8a22407fc177c18149fe4825a19091
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/25/2019
ms.locfileid: "75447255"
---
# <a name="extensions"></a><span data-ttu-id="bd950-103">擴充功能</span><span class="sxs-lookup"><span data-stu-id="bd950-103">Extensions</span></span>

<span data-ttu-id="bd950-104">SQLite 支援在執行時間載入擴充功能。</span><span class="sxs-lookup"><span data-stu-id="bd950-104">SQLite supports loading extensions at run time.</span></span> <span data-ttu-id="bd950-105">延伸模組包括其他 SQL 函數、定序、虛擬資料表等專案。</span><span class="sxs-lookup"><span data-stu-id="bd950-105">Extensions include things like additional SQL functions, collations, virtual tables, and more.</span></span>

<span data-ttu-id="bd950-106">.NET Core 包含額外的邏輯，可在其他地方尋找原生程式庫，例如參考的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bd950-106">.NET Core includes additional logic for locating native libraries in additional places like referenced NuGet packages.</span></span> <span data-ttu-id="bd950-107">可惜的是，SQLite 無法利用這個邏輯;它會直接呼叫平臺 API 來載入程式庫。</span><span class="sxs-lookup"><span data-stu-id="bd950-107">Unfortunately, SQLite can't leverage this logic; it calls the platform API directly to load libraries.</span></span> <span data-ttu-id="bd950-108">因此，在載入 SQLite 擴充功能之前，您的應用程式可能需要修改路徑、LD_LIBRARY_PATH 或 DYLD_LIBRARY_PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="bd950-108">Because of this, your app may need to modify the PATH, LD_LIBRARY_PATH, or DYLD_LIBRARY_PATH environment variables before loading SQLite extensions.</span></span> <span data-ttu-id="bd950-109">GitHub 上有[一個範例](https://github.com/dotnet/samples/blob/master/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs)，示範如何在參考的 NuGet 套件內尋找目前執行時間的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="bd950-109">There's [a sample](https://github.com/dotnet/samples/blob/master/samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs) on GitHub that demonstrates finding binaries for the current runtime inside a referenced NuGet package.</span></span>

<span data-ttu-id="bd950-110">若要載入擴充功能，請呼叫 <xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="bd950-110">To load an extension, call the <xref:Microsoft.Data.Sqlite.SqliteConnection.LoadExtension%2A> method.</span></span> <span data-ttu-id="bd950-111">如果連接已關閉並重新開啟，則 Sqlite 會確保延伸模組保持載入。</span><span class="sxs-lookup"><span data-stu-id="bd950-111">Microsoft.Data.Sqlite will ensure that the extension remains loaded even if the connection is closed and reopened.</span></span>

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ExtensionsSample/Program.cs?name=snippet_LoadExtension)]

## <a name="see-also"></a><span data-ttu-id="bd950-112">請參閱</span><span class="sxs-lookup"><span data-stu-id="bd950-112">See also</span></span>

* [<span data-ttu-id="bd950-113">執行時間可載入的擴充功能</span><span class="sxs-lookup"><span data-stu-id="bd950-113">Run-Time Loadable Extensions</span></span>](https://www.sqlite.org/loadext.html)