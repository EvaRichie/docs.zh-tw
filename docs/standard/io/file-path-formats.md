---
title: Windows 系統上的檔案路徑格式
description: 在本文中，您將瞭解 Windows 系統上的檔案路徑格式，例如傳統 DOS 路徑、DOS 裝置路徑，以及通用命名慣例 (UNC) 路徑。
ms.date: 06/06/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O, long paths
- long paths
- path formats, Windows
ms.openlocfilehash: e24772ee9c9d22786c9cfece43017f8526434601
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188051"
---
# <a name="file-path-formats-on-windows-systems"></a><span data-ttu-id="69147-103">Windows 系統上的檔案路徑格式</span><span class="sxs-lookup"><span data-stu-id="69147-103">File path formats on Windows systems</span></span>

<span data-ttu-id="69147-104"><xref:System.IO> 命名空間中許多類型的成員都包含 `path` 參數，這可讓您指定檔案系統資源的絕對或相對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-104">Members of many of the types in the <xref:System.IO> namespace include a `path` parameter that lets you specify an absolute or relative path to a file system resource.</span></span> <span data-ttu-id="69147-105">接著這個路徑會傳遞給 [Windows 檔案系統 API](/windows/desktop/fileio/file-systems)。</span><span class="sxs-lookup"><span data-stu-id="69147-105">This path is then passed to [Windows file system APIs](/windows/desktop/fileio/file-systems).</span></span> <span data-ttu-id="69147-106">本主題討論您可以在 Windows 系統上使用的檔案路徑格式。</span><span class="sxs-lookup"><span data-stu-id="69147-106">This topic discusses the formats for file paths that you can use on Windows systems.</span></span>

## <a name="traditional-dos-paths"></a><span data-ttu-id="69147-107">傳統 DOS 路徑</span><span class="sxs-lookup"><span data-stu-id="69147-107">Traditional DOS paths</span></span>

<span data-ttu-id="69147-108">標準 DOS 路徑可以包含三個元件：</span><span class="sxs-lookup"><span data-stu-id="69147-108">A standard DOS path can consist of three components:</span></span>

- <span data-ttu-id="69147-109">磁碟區或磁碟機代號，後面接著磁碟區分隔符號 (`:`)。</span><span class="sxs-lookup"><span data-stu-id="69147-109">A volume or drive letter followed by the volume separator (`:`).</span></span>
- <span data-ttu-id="69147-110">目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="69147-110">A directory name.</span></span> <span data-ttu-id="69147-111">[目錄分隔符號字元](<xref:System.IO.Path.DirectorySeparatorChar>)會分隔巢狀目錄階層內的子目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-111">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates subdirectories within the nested directory hierarchy.</span></span>
- <span data-ttu-id="69147-112">選擇性的檔名。</span><span class="sxs-lookup"><span data-stu-id="69147-112">An optional filename.</span></span> <span data-ttu-id="69147-113">[目錄分隔符號字元](<xref:System.IO.Path.DirectorySeparatorChar>)會分隔檔案路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="69147-113">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates the file path and the filename.</span></span>

<span data-ttu-id="69147-114">如果三個元件全都存在，則是絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-114">If all three components are present, the path is absolute.</span></span> <span data-ttu-id="69147-115">如果未指定任何磁碟區或磁碟機代號，且目錄名稱開頭為[目錄分隔符號字元](<xref:System.IO.Path.DirectorySeparatorChar>)，則路徑是相對於目前磁碟機的根目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-115">If no volume or drive letter is specified and the directory name begins with the [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>), the path is relative from the root of the current drive.</span></span> <span data-ttu-id="69147-116">否則，路徑是相對於目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-116">Otherwise, the path is relative to the current directory.</span></span> <span data-ttu-id="69147-117">下表顯示一些可能的目錄和檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-117">The following table shows some possible directory and file paths.</span></span>

|<span data-ttu-id="69147-118">Path</span><span class="sxs-lookup"><span data-stu-id="69147-118">Path</span></span>  |<span data-ttu-id="69147-119">描述</span><span class="sxs-lookup"><span data-stu-id="69147-119">Description</span></span>  |
| -- | -- |
| `C:\Documents\Newsletters\Summer2018.pdf` | <span data-ttu-id="69147-120">磁片磁碟機根目錄的絕對檔案路徑 `C:` 。</span><span class="sxs-lookup"><span data-stu-id="69147-120">An absolute file path from the root of drive `C:`.</span></span> |
| `\Program Files\Custom Utilities\StringFinder.exe` | <span data-ttu-id="69147-121">從目前磁碟機根目錄開始的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-121">An absolute path from the root of the current drive.</span></span> |
| `2018\January.xlsx` | <span data-ttu-id="69147-122">到目前目錄之子目錄中檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-122">A relative path to a file in a subdirectory of the current directory.</span></span> |
| `..\Publications\TravelBrochure.pdf` | <span data-ttu-id="69147-123">到目前目錄之同級目錄中檔案的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-123">A relative path to file in a directory that is a peer of the current directory.</span></span> |
| `C:\Projects\apilibrary\apilibrary.sln` | <span data-ttu-id="69147-124">磁片磁碟機根目錄中檔案的絕對路徑 `C:` 。</span><span class="sxs-lookup"><span data-stu-id="69147-124">An absolute path to a file from the root of drive `C:`.</span></span> |
| `C:Projects\apilibrary\apilibrary.sln` | <span data-ttu-id="69147-125">從磁片磁碟機的目前的目錄開始的相對路徑 `C:` 。</span><span class="sxs-lookup"><span data-stu-id="69147-125">A relative path from the current directory of the `C:` drive.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="69147-126">請注意最後兩個路徑之間的差異。</span><span class="sxs-lookup"><span data-stu-id="69147-126">Note the difference between the last two paths.</span></span> <span data-ttu-id="69147-127">兩者都會在兩個案例中都指定選用的磁片區規範 (`C:`) ，但是第一個是從指定磁片區的根目錄開始，而第二個則不是。</span><span class="sxs-lookup"><span data-stu-id="69147-127">Both specify the optional volume specifier (`C:` in both cases), but the first begins with the root of the specified volume, whereas the second does not.</span></span> <span data-ttu-id="69147-128">因此，第一個是磁片磁碟機根目錄的絕對路徑 `C:` ，而第二個則是磁片磁碟機目前目錄的相對路徑 `C:` 。</span><span class="sxs-lookup"><span data-stu-id="69147-128">As result, the first is an absolute path from the root directory of drive `C:`, whereas the second is a relative path from the current directory of drive `C:`.</span></span> <span data-ttu-id="69147-129">當想要第一種格式時使用第二種格式，是在牽涉到 Windows 檔案路徑時常見的錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="69147-129">Use of the second form when the first is intended is a common source of bugs that involve Windows file paths.</span></span>

<span data-ttu-id="69147-130">您可以呼叫 <xref:System.IO.Path.IsPathFullyQualified%2A?displayProperty=nameWithType> 方法來判斷檔案路徑是否完整 (也就是路徑獨立於目前的目錄，目前目錄變更時它不會變更)。</span><span class="sxs-lookup"><span data-stu-id="69147-130">You can determine whether a file path is fully qualified (that is, it the path is independent of the current directory and does not change when the current directory changes) by calling the <xref:System.IO.Path.IsPathFullyQualified%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="69147-131">請注意，這類路徑可以包含相對目錄區段 (`.` 和 `..`)，而且如果解析的路徑永遠指向相同位置便仍然完整。</span><span class="sxs-lookup"><span data-stu-id="69147-131">Note that such a path can include relative directory segments (`.` and `..`) and still be fully qualified if the resolved path always points to the same location.</span></span>

<span data-ttu-id="69147-132">下例會說明絕對和相對路徑之間的差異。</span><span class="sxs-lookup"><span data-stu-id="69147-132">The following example illustrates the difference between absolute and relative paths.</span></span> <span data-ttu-id="69147-133">它會假設目錄 `D:\FY2018\` 存在，而且您沒有在執行 `D:\` 此範例之前，從命令提示字元設定任何的目前的目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-133">It assumes that the directory `D:\FY2018\` exists, and that you haven't set any current directory for `D:\` from the command prompt before running the example.</span></span>

[!code-csharp[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/cs/paths.cs)]
[!code-vb[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/vb/paths.vb)]

[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="unc-paths"></a><span data-ttu-id="69147-134">UNC 路徑</span><span class="sxs-lookup"><span data-stu-id="69147-134">UNC paths</span></span>

<span data-ttu-id="69147-135">通用命名慣例 (UNC) 路徑，用來存取網路資源，具有下列格式：</span><span class="sxs-lookup"><span data-stu-id="69147-135">Universal naming convention (UNC) paths, which are used to access network resources, have the following format:</span></span>

- <span data-ttu-id="69147-136">伺服器或主機名稱，前面加上 `\\`。</span><span class="sxs-lookup"><span data-stu-id="69147-136">A server or host name, which is prefaced by `\\`.</span></span> <span data-ttu-id="69147-137">伺服器名稱可以是 NetBIOS 電腦名稱或 IP/FQDN 位址 (支援 IPv4 以及 v6)。</span><span class="sxs-lookup"><span data-stu-id="69147-137">The server name can be a NetBIOS machine name or an IP/FQDN address (IPv4 as well as v6 are supported).</span></span>
- <span data-ttu-id="69147-138">共用名稱，它藉由 `\` 與主機名稱分隔。</span><span class="sxs-lookup"><span data-stu-id="69147-138">A share name, which is separated from the host name by `\`.</span></span> <span data-ttu-id="69147-139">伺服器和共用名稱會共同組成磁碟區。</span><span class="sxs-lookup"><span data-stu-id="69147-139">Together, the server and share name make up the volume.</span></span>
- <span data-ttu-id="69147-140">目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="69147-140">A directory name.</span></span> <span data-ttu-id="69147-141">[目錄分隔符號字元](<xref:System.IO.Path.DirectorySeparatorChar>)會分隔巢狀目錄階層內的子目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-141">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates subdirectories within the nested directory hierarchy.</span></span>
- <span data-ttu-id="69147-142">選擇性的檔名。</span><span class="sxs-lookup"><span data-stu-id="69147-142">An optional filename.</span></span> <span data-ttu-id="69147-143">[目錄分隔符號字元](<xref:System.IO.Path.DirectorySeparatorChar>)會分隔檔案路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="69147-143">The [directory separator character](<xref:System.IO.Path.DirectorySeparatorChar>) separates the file path and the filename.</span></span>

<span data-ttu-id="69147-144">以下是 UNC 路徑的一些範例：</span><span class="sxs-lookup"><span data-stu-id="69147-144">The following are some examples of UNC paths:</span></span>

|<span data-ttu-id="69147-145">Path</span><span class="sxs-lookup"><span data-stu-id="69147-145">Path</span></span>  |<span data-ttu-id="69147-146">描述</span><span class="sxs-lookup"><span data-stu-id="69147-146">Description</span></span>  |
| -- | -- |
| `\\system07\C$\` | <span data-ttu-id="69147-147">`C:`磁片磁碟機的根目錄 `system07` 。</span><span class="sxs-lookup"><span data-stu-id="69147-147">The root directory of the `C:` drive on `system07`.</span></span> |
| `\\Server2\Share\Test\Foo.txt` | <span data-ttu-id="69147-148">`Foo.txt`磁片區之測試目錄中的檔案 `\\Server2\Share` 。</span><span class="sxs-lookup"><span data-stu-id="69147-148">The `Foo.txt` file in the Test directory of the `\\Server2\Share` volume.</span></span>|

<span data-ttu-id="69147-149">UNC 路徑必須一律完整。</span><span class="sxs-lookup"><span data-stu-id="69147-149">UNC paths must always be fully qualified.</span></span> <span data-ttu-id="69147-150">它們可以包含相對目錄區段 (`.` 和 `..`)，但這些必須是完整路徑的一部分。</span><span class="sxs-lookup"><span data-stu-id="69147-150">They can include relative directory segments (`.` and `..`), but these must be part of a fully qualified path.</span></span> <span data-ttu-id="69147-151">您只能藉由將 UNC 路徑對應至磁碟機代號來使用相對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-151">You can use relative paths only by mapping a UNC path to a drive letter.</span></span>

## <a name="dos-device-paths"></a><span data-ttu-id="69147-152">DOS 裝置路徑</span><span class="sxs-lookup"><span data-stu-id="69147-152">DOS device paths</span></span>

<span data-ttu-id="69147-153">Windows 作業系統有指向包括檔案在內所有資源的　統一物件模型。</span><span class="sxs-lookup"><span data-stu-id="69147-153">The Windows operating system has a unified object model that points to all resources, including files.</span></span> <span data-ttu-id="69147-154">這些物件路徑可從 [主控台] 視窗存取，並已透過舊版 DOS 和 UNC 路徑對應到的符號連結特殊資料夾，公開至 Win32 圖層。</span><span class="sxs-lookup"><span data-stu-id="69147-154">These object paths are accessible from the console window and are exposed to the Win32 layer through a special folder of symbolic links that legacy DOS and UNC paths are mapped to.</span></span> <span data-ttu-id="69147-155">這個特殊資料夾是透過 DOS 裝置路徑語法來存取，這是其中一個：</span><span class="sxs-lookup"><span data-stu-id="69147-155">This special folder is accessed via the DOS device path syntax, which is one of:</span></span>

`\\.\C:\Test\Foo.txt`
`\\?\C:\Test\Foo.txt`

<span data-ttu-id="69147-156">除了透過磁碟機代號識別磁碟機之外，也可以使用磁碟區 GUID 來識別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="69147-156">In addition to identifying a drive by its drive letter, you can identify a volume by using its volume GUID.</span></span> <span data-ttu-id="69147-157">它的格式如下：</span><span class="sxs-lookup"><span data-stu-id="69147-157">This takes the form:</span></span>

`\\.\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`
`\\?\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`

> [!NOTE]
> <span data-ttu-id="69147-158">從 .NET Core 1.1 和 .NET Framework 4.6.2 開始，在 Windows 上執行的 .NET 實作會支援 DOS 裝置路徑語法。</span><span class="sxs-lookup"><span data-stu-id="69147-158">DOS device path syntax is supported on .NET implementations running on Windows starting with .NET Core 1.1 and .NET Framework 4.6.2.</span></span>

<span data-ttu-id="69147-159">DOS 裝置路徑由以下元件組成：</span><span class="sxs-lookup"><span data-stu-id="69147-159">The DOS device path consists of the following components:</span></span>

- <span data-ttu-id="69147-160">裝置路徑規範 (`\\.\` 或 `\\?\`)，這會將路徑識別為 DOS 裝置路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-160">The device path specifier (`\\.\` or `\\?\`), which identifies the path as a DOS device path.</span></span>

   > [!NOTE]
   > <span data-ttu-id="69147-161">`\\?\`所有版本的 .Net Core 和 .net 5 + 以及 .NET Framework 從版本4.6.2 開始都支援。</span><span class="sxs-lookup"><span data-stu-id="69147-161">The `\\?\` is supported in all versions of .NET Core and .NET 5+ and in .NET Framework starting with version 4.6.2.</span></span>

- <span data-ttu-id="69147-162">「真實」裝置物件的符號連結 (如果是磁碟機名稱即為 C:，若是磁碟區 GUID 則為 Volume{b75e2c83-0000-0000-0000-602f00000000})。</span><span class="sxs-lookup"><span data-stu-id="69147-162">A symbolic link to the "real" device object (C: in the case of a drive name, or Volume{b75e2c83-0000-0000-0000-602f00000000} in the case of a volume GUID).</span></span>

   <span data-ttu-id="69147-163">裝置路徑規範識別磁碟區或磁碟機之後，DOS 裝置路徑的第一個區段。</span><span class="sxs-lookup"><span data-stu-id="69147-163">The first segment of the DOS device path after the device path specifier identifies the volume or drive.</span></span> <span data-ttu-id="69147-164">(例如，`\\?\C:\` 和 `\\.\BootPartition\`。)</span><span class="sxs-lookup"><span data-stu-id="69147-164">(For example, `\\?\C:\` and `\\.\BootPartition\`.)</span></span>

   <span data-ttu-id="69147-165">對於呼叫的 UNC 有一個特定連結，不用多說，就是 `UNC`。</span><span class="sxs-lookup"><span data-stu-id="69147-165">There is a specific link for UNCs that is called, not surprisingly, `UNC`.</span></span> <span data-ttu-id="69147-166">例如：</span><span class="sxs-lookup"><span data-stu-id="69147-166">For example:</span></span>

  `\\.\UNC\Server\Share\Test\Foo.txt`
  `\\?\UNC\Server\Share\Test\Foo.txt`

    <span data-ttu-id="69147-167">針對裝置 UNC，「伺服器/共用」部分會形成磁碟區。</span><span class="sxs-lookup"><span data-stu-id="69147-167">For device UNCs, the server/share portion forms the volume.</span></span> <span data-ttu-id="69147-168">例如，在中 `\\?\server1\e:\utilities\\filecomparer\` ，伺服器/共用部分是 `server1\utilities` 。</span><span class="sxs-lookup"><span data-stu-id="69147-168">For example, in `\\?\server1\e:\utilities\\filecomparer\`, the server/share portion is `server1\utilities`.</span></span> <span data-ttu-id="69147-169">這一點在呼叫具有相對目錄區段的方法 (例如 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType>) 時很重要；無法瀏覽過磁碟區。</span><span class="sxs-lookup"><span data-stu-id="69147-169">This is significant when calling a method such as <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> with relative directory segments; it is never possible to navigate past the volume.</span></span>

<span data-ttu-id="69147-170">根據定義，DOS 裝置路徑是完整的。</span><span class="sxs-lookup"><span data-stu-id="69147-170">DOS device paths are fully qualified by definition.</span></span> <span data-ttu-id="69147-171">不允許相對目錄區段 (`.` 和 `..`)。</span><span class="sxs-lookup"><span data-stu-id="69147-171">Relative directory segments (`.` and `..`) are not allowed.</span></span> <span data-ttu-id="69147-172">目前目錄絕對不會進入其使用方式。</span><span class="sxs-lookup"><span data-stu-id="69147-172">Current directories never enter into their usage.</span></span>

## <a name="example-ways-to-refer-to-the-same-file"></a><span data-ttu-id="69147-173">範例：如何參考相同的檔案</span><span class="sxs-lookup"><span data-stu-id="69147-173">Example: Ways to refer to the same file</span></span>

<span data-ttu-id="69147-174">下列範例說明一些您可以用來在 <xref:System.IO> 命名空間使用 API 時參考檔案的方法。</span><span class="sxs-lookup"><span data-stu-id="69147-174">The following example illustrates some of the ways in which you can refer to a file when using the APIs in the <xref:System.IO> namespace.</span></span> <span data-ttu-id="69147-175">範例會具現化 <xref:System.IO.FileInfo> 物件，並使用其 <xref:System.IO.FileInfo.Name> 和 <xref:System.IO.FileInfo.Length> 屬性，以顯示檔案名稱和檔案的長度。</span><span class="sxs-lookup"><span data-stu-id="69147-175">The example instantiates a <xref:System.IO.FileInfo> object and uses its <xref:System.IO.FileInfo.Name> and <xref:System.IO.FileInfo.Length> properties to display the filename and the length of the file.</span></span>

[!code-csharp[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/cs/file-refs.cs)]
[!code-vb[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/vb/file-refs.vb)]

## <a name="path-normalization"></a><span data-ttu-id="69147-176">路徑正規化</span><span class="sxs-lookup"><span data-stu-id="69147-176">Path normalization</span></span>

<span data-ttu-id="69147-177">幾乎傳遞給 Windows API 的所有路徑都會正規化。</span><span class="sxs-lookup"><span data-stu-id="69147-177">Almost all paths passed to Windows APIs are normalized.</span></span> <span data-ttu-id="69147-178">在正規化期間，Windows 會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="69147-178">During normalization, Windows performs the following steps:</span></span>

- <span data-ttu-id="69147-179">識別路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-179">Identifies the path.</span></span>
- <span data-ttu-id="69147-180">將目前目錄套用到部份限定 (相對) 路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-180">Applies the current directory to partially qualified (relative) paths.</span></span>
- <span data-ttu-id="69147-181">規範化元件和目錄分隔符號。</span><span class="sxs-lookup"><span data-stu-id="69147-181">Canonicalizes component and directory separators.</span></span>
- <span data-ttu-id="69147-182">評估相對目錄元件 (`.` 表示目前目錄，`..` 表示父目錄)。</span><span class="sxs-lookup"><span data-stu-id="69147-182">Evaluates relative directory components (`.` for the current directory and `..` for the parent directory).</span></span>
- <span data-ttu-id="69147-183">修剪特定字元。</span><span class="sxs-lookup"><span data-stu-id="69147-183">Trims certain characters.</span></span>

<span data-ttu-id="69147-184">這個正規化會隱含地發生，但您可以明確地呼叫 <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> 方法來執行，這個方法會包裝對 [GetFullPathName() 函式](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)的呼叫。</span><span class="sxs-lookup"><span data-stu-id="69147-184">This normalization happens implicitly, but you can do it explicitly by calling the <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> method, which wraps a call to the  [GetFullPathName() function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea).</span></span> <span data-ttu-id="69147-185">您也可以直接使用 P/Invoke 呼叫 Windows [GetFullPathName() 函式](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)。</span><span class="sxs-lookup"><span data-stu-id="69147-185">You can also call the Windows [GetFullPathName() function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) directly using P/Invoke.</span></span>

### <a name="identify-the-path"></a><span data-ttu-id="69147-186">識別路徑</span><span class="sxs-lookup"><span data-stu-id="69147-186">Identify the path</span></span>

<span data-ttu-id="69147-187">路徑正規化的第一步就是識別路徑的類型。</span><span class="sxs-lookup"><span data-stu-id="69147-187">The first step in path normalization is identifying the type of path.</span></span> <span data-ttu-id="69147-188">路徑會落在一些分類的其中之一：</span><span class="sxs-lookup"><span data-stu-id="69147-188">Paths fall into one of a few categories:</span></span>

- <span data-ttu-id="69147-189">它們是裝置路徑，亦即它們開頭為兩個分隔符號和一個問號或句點 (`\\?` 或 `\\.`)。</span><span class="sxs-lookup"><span data-stu-id="69147-189">They are device paths; that is, they begin with two separators and a question mark or period (`\\?` or `\\.`).</span></span>
- <span data-ttu-id="69147-190">它們是 UNC 路徑，亦即它們開頭為兩個分隔符號，且沒有問號或句點。</span><span class="sxs-lookup"><span data-stu-id="69147-190">They are UNC paths; that is, they begin with two separators without a question mark or period.</span></span>
- <span data-ttu-id="69147-191">它們是完整的 DOS 路徑，亦即它們開頭為磁碟機代號、磁碟區分隔符號和元件分隔符號 (`C:\`)。</span><span class="sxs-lookup"><span data-stu-id="69147-191">They are fully qualified DOS paths; that is, they begin with a drive letter, a volume separator, and a component separator (`C:\`).</span></span>
- <span data-ttu-id="69147-192">它們指定舊版裝置 (`CON`、`LPT1`)。</span><span class="sxs-lookup"><span data-stu-id="69147-192">They designate a legacy device (`CON`, `LPT1`).</span></span>
- <span data-ttu-id="69147-193">它們相對於目前磁碟機的根目錄，亦即它們開頭單一元件分隔符號 (`\`)。</span><span class="sxs-lookup"><span data-stu-id="69147-193">They are relative to the root of the current drive; that is, they begin with a single component separator (`\`).</span></span>
- <span data-ttu-id="69147-194">它們相對於指定磁碟機的目前目錄，亦即它們開頭為磁碟機代號、磁碟區分隔符號，且沒有元件分隔符號 (`C:`)。</span><span class="sxs-lookup"><span data-stu-id="69147-194">They are relative to the current directory of a specified drive; that is, they begin with a drive letter, a volume separator, and no component separator (`C:`).</span></span>
- <span data-ttu-id="69147-195">它們相對於目前目錄，亦即它們開頭為其他任何字元 (`temp\testfile.txt`)。</span><span class="sxs-lookup"><span data-stu-id="69147-195">They are relative to the current directory; that is, they begin with anything else (`temp\testfile.txt`).</span></span>

<span data-ttu-id="69147-196">路徑的類型會決定是否要以某種方式套用目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-196">The type of the path determines whether or not a current directory is applied in some way.</span></span> <span data-ttu-id="69147-197">它也會判斷路徑的「根」是什麼。</span><span class="sxs-lookup"><span data-stu-id="69147-197">It also determines what the "root" of the path is.</span></span>

### <a name="handle-legacy-devices"></a><span data-ttu-id="69147-198">處理舊版裝置</span><span class="sxs-lookup"><span data-stu-id="69147-198">Handle legacy devices</span></span>

<span data-ttu-id="69147-199">如果路徑是舊版 DOS 裝置，例如 `CON`、`COM1` 或 `LPT1`，會在它前面加上 `\\.\` 轉換為裝置路徑然後傳回。</span><span class="sxs-lookup"><span data-stu-id="69147-199">If the path is a legacy DOS device such as `CON`, `COM1`, or `LPT1`, it is converted into a device path by prepending `\\.\` and returned.</span></span>

<span data-ttu-id="69147-200">開頭為舊版裝置名稱的路徑，一律會被 <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=nameWithType> 方法解譯成舊版裝置。</span><span class="sxs-lookup"><span data-stu-id="69147-200">A path that begins with a legacy device name is always interpreted as a legacy device by the <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="69147-201">例如，`CON.TXT` 的 DOS 裝置路徑是 `\\.\CON`，而 `COM1.TXT\file1.txt` 的 DOS 裝置路徑是 `\\.\COM1`。</span><span class="sxs-lookup"><span data-stu-id="69147-201">For example, the DOS device path for `CON.TXT` is `\\.\CON`, and the DOS device path for `COM1.TXT\file1.txt` is `\\.\COM1`.</span></span>

### <a name="apply-the-current-directory"></a><span data-ttu-id="69147-202">套用目前的目錄</span><span class="sxs-lookup"><span data-stu-id="69147-202">Apply the current directory</span></span>

<span data-ttu-id="69147-203">如果路徑不是完整格式，Windows 會套用目前目錄給它。</span><span class="sxs-lookup"><span data-stu-id="69147-203">If a path isn't fully qualified, Windows applies the current directory to it.</span></span> <span data-ttu-id="69147-204">UNC 和裝置路徑沒有套用目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-204">UNCs and device paths do not have the current directory applied.</span></span> <span data-ttu-id="69147-205">兩者都不會執行具有分隔符號的完整磁片磁碟機 `C:\` 。</span><span class="sxs-lookup"><span data-stu-id="69147-205">Neither does a full drive with separator `C:\`.</span></span>

<span data-ttu-id="69147-206">如果路徑開頭為單一元件分隔符號，則會套用目前目錄的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="69147-206">If the path starts with a single component separator, the drive from the current directory is applied.</span></span> <span data-ttu-id="69147-207">例如，如果檔案路徑是 `\utilities`，而目前目錄是 `C:\temp\`，則正規化會產生 `C:\utilities`。</span><span class="sxs-lookup"><span data-stu-id="69147-207">For example, if the file path is `\utilities` and the current directory is `C:\temp\`, normalization produces `C:\utilities`.</span></span>

<span data-ttu-id="69147-208">如果路徑開頭為磁碟機代號、磁碟區分隔符號且沒有元件分隔符號，則會套用從命令殼層設定的指定磁碟機最後一個目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-208">If the path starts with a drive letter, volume separator, and no component separator, the last current directory set from the command shell for the specified drive is applied.</span></span> <span data-ttu-id="69147-209">如果未設定最後一個目前目錄，則會單獨套用磁碟機。</span><span class="sxs-lookup"><span data-stu-id="69147-209">If the last current directory was not set, the drive alone is applied.</span></span> <span data-ttu-id="69147-210">例如，如果檔案路徑是 `D:sources`目前目錄是 `C:\Documents\`，且磁碟機 D: 上的最後一個目前目錄是 `D:\sources\`，則結果是 `D:\sources\sources`。</span><span class="sxs-lookup"><span data-stu-id="69147-210">For example, if the file path is `D:sources`, the current directory is `C:\Documents\`, and the last current directory on drive D: was `D:\sources\`, the result is `D:\sources\sources`.</span></span> <span data-ttu-id="69147-211">這些「磁碟機相對」路徑是常見的程式和指令碼邏輯錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="69147-211">These "drive relative" paths are a common source of program and script logic errors.</span></span> <span data-ttu-id="69147-212">假設開頭為代號與冒號的路徑不是相對路徑，這顯然不正確。</span><span class="sxs-lookup"><span data-stu-id="69147-212">Assuming that a path beginning with a letter and a colon isn't relative is obviously not correct.</span></span>

<span data-ttu-id="69147-213">如果路徑開頭為分隔符號以外的項目，則會套用目前磁碟機和目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-213">If the path starts with something other than a separator, the current drive and current directory are applied.</span></span> <span data-ttu-id="69147-214">例如，如果路徑是 `filecompare`，而目前目錄是 `C:\utilities\`，則結果是 `C:\utilities\filecompare\`。</span><span class="sxs-lookup"><span data-stu-id="69147-214">For example, if the path is `filecompare` and the current directory is `C:\utilities\`, the result is `C:\utilities\filecompare\`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69147-215">相對路徑在多執行緒應用程式 (也就是大部分應用程式) 中是危險的，因為目前目錄是以每個處理序為基準的一項設定。</span><span class="sxs-lookup"><span data-stu-id="69147-215">Relative paths are dangerous in multithreaded applications (that is, most applications) because the current directory is a per-process setting.</span></span> <span data-ttu-id="69147-216">任何執行緒都可以隨時變更目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-216">Any thread can change the current directory at any time.</span></span> <span data-ttu-id="69147-217">從 .NET Core 2.1 開始，您可以呼叫 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> 方法，從相對路徑以及您想要解析針對的基底路徑 (目前的目錄)，取得絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-217">Starting with .NET Core 2.1, you can call the <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> method to get an absolute path from a relative path and the base path (the current directory) that you want to resolve it against.</span></span>

### <a name="canonicalize-separators"></a><span data-ttu-id="69147-218">正常化分隔符號</span><span class="sxs-lookup"><span data-stu-id="69147-218">Canonicalize separators</span></span>

<span data-ttu-id="69147-219">所有正斜線 (`/`) 會轉換成標準的 Windows 分隔符號，也就是反斜線 (`\`)。</span><span class="sxs-lookup"><span data-stu-id="69147-219">All forward slashes (`/`) are converted into the standard Windows separator, the back slash (`\`).</span></span> <span data-ttu-id="69147-220">如果它們存在，跟隨在前兩個斜線後面的一系列斜線，會摺疊成單一斜線。</span><span class="sxs-lookup"><span data-stu-id="69147-220">If they are present, a series of slashes that follow the first two slashes are collapsed into a single slash.</span></span>

### <a name="evaluate-relative-components"></a><span data-ttu-id="69147-221">評估相對元件</span><span class="sxs-lookup"><span data-stu-id="69147-221">Evaluate relative components</span></span>

<span data-ttu-id="69147-222">處理路徑時，會評估由單一或雙句點 (`.` 或 `..`) 所組成的任何元件或區段：</span><span class="sxs-lookup"><span data-stu-id="69147-222">As the path is processed, any components or segments that are composed of a single or a double period (`.` or `..`) are evaluated:</span></span>

- <span data-ttu-id="69147-223">若為單一句點，會移除目前的區段，因為它是指目前目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-223">For a single period, the current segment is removed, since it refers to the current directory.</span></span>

- <span data-ttu-id="69147-224">若為雙句點，會移除目前的區段和父區段，因為雙句點是指父目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-224">For a double period, the current segment and the parent segment are removed, since the double period refers to the parent directory.</span></span>

   <span data-ttu-id="69147-225">只有在父目錄不超過路徑的根目錄時，才會移除父目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-225">Parent directories are only removed if they aren't past the root of the path.</span></span> <span data-ttu-id="69147-226">路徑的根目錄取決於路徑的類型。</span><span class="sxs-lookup"><span data-stu-id="69147-226">The root of the path depends on the type of path.</span></span> <span data-ttu-id="69147-227">對於 DOS 路徑是磁碟機 (`C:\`)、對於 UNC 是伺服器/共用 (`\\Server\Share`)，以及對於裝置路徑則是裝置路徑前置詞 (`\\?\` 或 `\\.\`)。</span><span class="sxs-lookup"><span data-stu-id="69147-227">It is the drive (`C:\`) for DOS paths, the server/share for UNCs (`\\Server\Share`), and the device path prefix for device paths (`\\?\` or `\\.\`).</span></span>

### <a name="trim-characters"></a><span data-ttu-id="69147-228">修剪字元</span><span class="sxs-lookup"><span data-stu-id="69147-228">Trim characters</span></span>

<span data-ttu-id="69147-229">在稍早移除分隔符號和相對區段時，正規化期間也會額外移除一些字元：</span><span class="sxs-lookup"><span data-stu-id="69147-229">Along with the runs of separators and relative segments removed earlier, some additional characters are removed during normalization:</span></span>

- <span data-ttu-id="69147-230">如果區段結尾為單一句點，會移除該句點。</span><span class="sxs-lookup"><span data-stu-id="69147-230">If a segment ends in a single period, that period is removed.</span></span> <span data-ttu-id="69147-231">(單句點或雙句點的區段在上一個步驟中正規化。</span><span class="sxs-lookup"><span data-stu-id="69147-231">(A segment of a single or double period is normalized in the previous step.</span></span> <span data-ttu-id="69147-232">三個以上句點的區段不會正規化，且實際上是有效的檔案/目錄名稱。)</span><span class="sxs-lookup"><span data-stu-id="69147-232">A segment of three or more periods is not normalized and is actually a valid file/directory name.)</span></span>

- <span data-ttu-id="69147-233">如果路徑結尾不是分隔符號，所有尾端句號和空格 (U+0020) 都會移除。</span><span class="sxs-lookup"><span data-stu-id="69147-233">If the path doesn't end in a separator, all trailing periods and spaces (U+0020) are removed.</span></span> <span data-ttu-id="69147-234">如果最後一個區段只是單句點或雙句點，它會屬於上述相對元件規則。</span><span class="sxs-lookup"><span data-stu-id="69147-234">If the last segment is simply a single or double period, it falls under the relative components rule above.</span></span>

   <span data-ttu-id="69147-235">此規則表示您可以建立具有尾端空格的目錄名稱，方法是在空格之後新增尾端分隔符號。</span><span class="sxs-lookup"><span data-stu-id="69147-235">This rule means that you can create a directory name with a trailing space by adding a trailing separator after the space.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="69147-236">您應該 **絕不** 建立具有尾端空格的目錄或檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="69147-236">You should **never** create a directory or filename with a trailing space.</span></span> <span data-ttu-id="69147-237">尾端空格可能會導致難以存取目錄或是不可能存取目錄，而應用程式在嘗試處理名稱包含尾端空格的目錄或檔案時，通常會失敗。</span><span class="sxs-lookup"><span data-stu-id="69147-237">Trailing spaces can make it difficult or impossible to access a directory, and applications commonly fail when attempting to handle directories or files whose names include trailing spaces.</span></span>

## <a name="skip-normalization"></a><span data-ttu-id="69147-238">略過正規化</span><span class="sxs-lookup"><span data-stu-id="69147-238">Skip normalization</span></span>

<span data-ttu-id="69147-239">一般而言，任何傳遞給 Windows API 的路徑 (實際上) 會傳遞給 [GetFullPathName 函式](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)並正規化。</span><span class="sxs-lookup"><span data-stu-id="69147-239">Normally, any path passed to a Windows API is (effectively) passed to the [GetFullPathName function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) and normalized.</span></span> <span data-ttu-id="69147-240">有一個重要的例外狀況：開頭為問號而非句號的裝置路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-240">There is one important exception: a device path that begins with a question mark instead of a period.</span></span> <span data-ttu-id="69147-241">除非路徑開頭完全為 `\\?\`(請注意我們使用了標準的反斜線)，否則它會正規化。</span><span class="sxs-lookup"><span data-stu-id="69147-241">Unless the path starts exactly with `\\?\` (note the use of the canonical backslash), it is normalized.</span></span>

<span data-ttu-id="69147-242">為何會想要略過正規化？</span><span class="sxs-lookup"><span data-stu-id="69147-242">Why would you want to skip normalization?</span></span> <span data-ttu-id="69147-243">有三個主要的原因：</span><span class="sxs-lookup"><span data-stu-id="69147-243">There are three major reasons:</span></span>

1. <span data-ttu-id="69147-244">存取通常無法使用，但是合法的路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-244">To get access to paths that are normally unavailable but are legal.</span></span> <span data-ttu-id="69147-245">例如，稱為 `hidden.` 的檔案或目錄便無法以任何其他方式存取。</span><span class="sxs-lookup"><span data-stu-id="69147-245">A file or directory called `hidden.`, for example, is impossible to access in any other way.</span></span>

1. <span data-ttu-id="69147-246">如果已經正規化，藉由略過正規化以改善效能。</span><span class="sxs-lookup"><span data-stu-id="69147-246">To improve performance by skipping normalization if you've already normalized.</span></span>

1. <span data-ttu-id="69147-247">僅限 .NET Framework，以略過 `MAX_PATH` 路徑長度的檢查，以允許超過259個字元的路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-247">On .NET Framework only, to skip the `MAX_PATH` check for path length to allow for paths that are greater than 259 characters.</span></span> <span data-ttu-id="69147-248">大部分的 API 都允許這點，但有些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="69147-248">Most APIs allow this, with some exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="69147-249">.NET Core 和 .NET 5 + 會隱含地處理長路徑，而且不會執行 `MAX_PATH` 檢查。</span><span class="sxs-lookup"><span data-stu-id="69147-249">.NET Core and .NET 5+ handles long paths implicitly and does not perform a `MAX_PATH` check.</span></span> <span data-ttu-id="69147-250">此 `MAX_PATH` 檢查只適用于 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="69147-250">The `MAX_PATH` check applies only to .NET Framework.</span></span>

<span data-ttu-id="69147-251">略過正規化和最大路徑檢查是兩個裝置路徑語法之間唯一的差異，它們在其他方面都一樣。</span><span class="sxs-lookup"><span data-stu-id="69147-251">Skipping normalization and max path checks is the only difference between the two device path syntaxes; they are otherwise identical.</span></span> <span data-ttu-id="69147-252">略過正規化時請小心，因為您可能會很容易就建立令「正常」應用程式難以處理的路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-252">Be careful with skipping normalization, since you can easily create paths that are difficult for "normal" applications to deal with.</span></span>

<span data-ttu-id="69147-253">開頭為 `\\?\` 的路徑，在您明確地將其傳遞給 [GetFullPathName 函式](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)時，仍會正規化。</span><span class="sxs-lookup"><span data-stu-id="69147-253">Paths that start with `\\?\` are still normalized if you explicitly pass them to the [GetFullPathName function](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea).</span></span>

<span data-ttu-id="69147-254">您可以將多個字元的路徑傳遞 `MAX_PATH` 至 [>getfullpathname](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) ，而不需要 `\\?\` 。</span><span class="sxs-lookup"><span data-stu-id="69147-254">You can pass paths of more than `MAX_PATH` characters to [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) without `\\?\`.</span></span> <span data-ttu-id="69147-255">它支援最長可達 Windows 可處理字串大小上限的任意長度路徑。</span><span class="sxs-lookup"><span data-stu-id="69147-255">It supports arbitrary length paths up to the maximum string size that Windows can handle.</span></span>

## <a name="case-and-the-windows-file-system"></a><span data-ttu-id="69147-256">大小寫與 Windows 檔案系統</span><span class="sxs-lookup"><span data-stu-id="69147-256">Case and the Windows file system</span></span>

<span data-ttu-id="69147-257">對於 Windows 檔案系統的特色，非 Windows 使用者和開發人員感到困惑的一點就是路徑和目錄名稱不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="69147-257">A peculiarity of the Windows file system that non-Windows users and developers find confusing is that path and directory names are case-insensitive.</span></span> <span data-ttu-id="69147-258">也就是說，目錄和檔案名稱會反映它們建立時所使用的字串大小寫。</span><span class="sxs-lookup"><span data-stu-id="69147-258">That is, directory and file names reflect the casing of the strings used when they are created.</span></span> <span data-ttu-id="69147-259">例如，方法呼叫</span><span class="sxs-lookup"><span data-stu-id="69147-259">For example, the method call</span></span>

```csharp
Directory.Create("TeStDiReCtOrY");
```

```vb
Directory.Create("TeStDiReCtOrY")
```

<span data-ttu-id="69147-260">會建立名為 TeStDiReCtOrY 的目錄。</span><span class="sxs-lookup"><span data-stu-id="69147-260">creates a directory named TeStDiReCtOrY.</span></span> <span data-ttu-id="69147-261">如果您重新命名目錄或檔案，以變更其大小寫，目錄或檔案名稱會反映將它重新命名時所使用字串的大小寫。</span><span class="sxs-lookup"><span data-stu-id="69147-261">If you rename a directory or file to change its case, the directory or file name reflects the case of the string used when you rename it.</span></span> <span data-ttu-id="69147-262">例如，下列程式碼將一個名為 test.txt 的檔案重新命名為 Test.txt：</span><span class="sxs-lookup"><span data-stu-id="69147-262">For example, the following code renames a file named test.txt to Test.txt:</span></span>

[!code-csharp[case-and-renaming](~/samples/snippets/standard/io/file-names/cs/rename.cs)]
[!code-vb[case-and-renaming](~/samples/snippets/standard/io/file-names/vb/rename.vb)]

<span data-ttu-id="69147-263">不過，目錄和檔案名稱比較不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="69147-263">However, directory and file name comparisons are case-insensitive.</span></span> <span data-ttu-id="69147-264">如果您搜尋名為 "test.txt" 的檔案，.NET 檔案系統 API 在比較時會忽略大小寫。</span><span class="sxs-lookup"><span data-stu-id="69147-264">If you search for a file named "test.txt", .NET file system APIs ignore case in the comparison.</span></span> <span data-ttu-id="69147-265">"Test.txt"、"TEST.TXT"、"test.TXT" 和任何其他大寫和小寫字母的組合都會與 "test.txt" 相符。</span><span class="sxs-lookup"><span data-stu-id="69147-265">"Test.txt", "TEST.TXT", "test.TXT", and any other combination of uppercase and lowercase letters will match "test.txt".</span></span>
