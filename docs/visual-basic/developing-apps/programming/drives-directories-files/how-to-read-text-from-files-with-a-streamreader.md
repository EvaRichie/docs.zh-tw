---
title: 作法：以 StreamReader 從檔案讀取文字
ms.date: 07/20/2015
helpviewer_keywords:
- reading files [Visual Basic], text
- text, reading from files
- reading text from files [Visual Basic]
- files [Visual Basic], reading
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
ms.openlocfilehash: 6d05dac9b612659a74e25c0ce87c7524316d31a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411599"
---
# <a name="how-to-read-text-from-files-with-a-streamreader-visual-basic"></a><span data-ttu-id="44795-102">如何：以 StreamReader 從檔案讀取文字 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="44795-102">How to: Read Text from Files with a StreamReader (Visual Basic)</span></span>

<span data-ttu-id="44795-103">`My.Computer.FileSystem` 物件提供方法來開啟 <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter>。</span><span class="sxs-lookup"><span data-stu-id="44795-103">The `My.Computer.FileSystem` object provides methods to open a <xref:System.IO.TextReader> and a <xref:System.IO.TextWriter>.</span></span> <span data-ttu-id="44795-104">除非您選取 [全部]\*\*\*\* 索引標籤，否則 `OpenTextFileWriter` 和 `OpenTextFileReader` 這兩種方法是未出現在 IntelliSense 中的進階方法。</span><span class="sxs-lookup"><span data-stu-id="44795-104">These methods, `OpenTextFileWriter` and `OpenTextFileReader`, are advanced methods that do not appear in IntelliSense unless you select the **All** tab.</span></span>  
  
### <a name="to-read-a-line-from-a-file-with-a-text-reader"></a><span data-ttu-id="44795-105">使用文字讀取器從檔案讀取一行</span><span class="sxs-lookup"><span data-stu-id="44795-105">To read a line from a file with a text reader</span></span>  
  
- <span data-ttu-id="44795-106">使用 `OpenTextFileReader` 方法來開啟 <xref:System.IO.TextReader>，並指定檔案。</span><span class="sxs-lookup"><span data-stu-id="44795-106">Use the `OpenTextFileReader` method to open the <xref:System.IO.TextReader>, specifying the file.</span></span> <span data-ttu-id="44795-107">這個範例會開啟名為 `testfile.txt` 的檔案，並讀取其中一行，然後顯示訊息方塊中的行。</span><span class="sxs-lookup"><span data-stu-id="44795-107">This example opens the file named `testfile.txt`, reads a line from it, and displays the line in a message box.</span></span>  
  
     [!code-vb[VbFileIORead#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#1)]  
  
## <a name="robust-programming"></a><span data-ttu-id="44795-108">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="44795-108">Robust Programming</span></span>  

 <span data-ttu-id="44795-109">讀取的檔案必須是文字檔。</span><span class="sxs-lookup"><span data-stu-id="44795-109">The file that is read must be a text file.</span></span>  
  
 <span data-ttu-id="44795-110">請勿根據檔案名稱來判斷檔案內容。</span><span class="sxs-lookup"><span data-stu-id="44795-110">Do not make decisions about the contents of the file based on the name of the file.</span></span> <span data-ttu-id="44795-111">例如，檔案 Form1.vb 可能不是 Visual Basic 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="44795-111">For example, the file Form1.vb may not be a Visual Basic source file.</span></span>  
  
 <span data-ttu-id="44795-112">在應用程式中使用這些資料之前，請先驗證所有輸入值。</span><span class="sxs-lookup"><span data-stu-id="44795-112">Verify all inputs before using the data in your application.</span></span> <span data-ttu-id="44795-113">檔案內容可能與預期不同，並從檔案讀取資料的方法會失敗。</span><span class="sxs-lookup"><span data-stu-id="44795-113">The contents of the file may not be what is expected, and methods to read from the file may fail.</span></span>  
  
## <a name="net-framework-security"></a><span data-ttu-id="44795-114">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="44795-114">.NET Framework Security</span></span>  

 <span data-ttu-id="44795-115">若要讀取檔案，您的組件需要 <xref:System.Security.Permissions.FileIOPermission> 類別所授與的權限等級。</span><span class="sxs-lookup"><span data-stu-id="44795-115">To read from a file, your assembly requires a privilege level granted by the <xref:System.Security.Permissions.FileIOPermission> class.</span></span> <span data-ttu-id="44795-116">如果要在部分信任內容中執行，則程式碼可能會因權限不足而擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="44795-116">If you are running in a partial-trust context, the code might throw an exception due to insufficient privileges.</span></span> <span data-ttu-id="44795-117">如需詳細資訊，請參閱 [Code Access Security Basics](../../../../framework/misc/code-access-security-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="44795-117">For more information, see [Code Access Security Basics](../../../../framework/misc/code-access-security-basics.md).</span></span> <span data-ttu-id="44795-118">使用者也需要存取檔案。</span><span class="sxs-lookup"><span data-stu-id="44795-118">The user also needs access to the file.</span></span> <span data-ttu-id="44795-119">如需詳細資訊，請參閱 [ACL 技術概觀](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="44795-119">For more information, see [ACL Technology Overview](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="44795-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="44795-120">See also</span></span>

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:System.Windows.Forms.OpenFileDialog>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>
- [<span data-ttu-id="44795-121">SaveFileDialog 元件</span><span class="sxs-lookup"><span data-stu-id="44795-121">SaveFileDialog Component</span></span>](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md)
- [<span data-ttu-id="44795-122">從檔案讀取</span><span class="sxs-lookup"><span data-stu-id="44795-122">Reading from Files</span></span>](reading-from-files.md)
