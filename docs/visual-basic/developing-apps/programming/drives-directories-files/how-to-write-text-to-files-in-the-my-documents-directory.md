---
title: 作法：將文字寫入我的文件目錄中的檔案
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], writing to
- text, writing to files
- examples [Visual Basic], text files
- writing to files [Visual Basic], in My Documents
ms.assetid: 1c726124-781d-4976-9baa-ed46814ff3fe
ms.openlocfilehash: bb3a9bdc44f86fbcdb3c56ee088740efdfebe95d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546454"
---
# <a name="how-to-write-text-to-files-in-the-my-documents-directory-in-visual-basic"></a><span data-ttu-id="95e21-102">如何：在 Visual Basic 中將文字寫入我的文件目錄中的檔案</span><span class="sxs-lookup"><span data-stu-id="95e21-102">How to: Write Text to Files in the My Documents Directory in Visual Basic</span></span>

<span data-ttu-id="95e21-103">`My.Computer.FileSystem.SpecialDirectories` 物件可讓您存取特殊目錄，例如 [我的文件]\*\*\*\* 目錄。</span><span class="sxs-lookup"><span data-stu-id="95e21-103">The `My.Computer.FileSystem.SpecialDirectories` object allows you to access special directories, such as the **MyDocuments** directory.</span></span>  
  
## <a name="procedure"></a><span data-ttu-id="95e21-104">程序</span><span class="sxs-lookup"><span data-stu-id="95e21-104">Procedure</span></span>  
  
#### <a name="to-write-new-text-files-in-the-my-documents-directory"></a><span data-ttu-id="95e21-105">將新文字檔寫入 [我的文件] 目錄中</span><span class="sxs-lookup"><span data-stu-id="95e21-105">To write new text files in the My Documents directory</span></span>  
  
1. <span data-ttu-id="95e21-106">使用 `My.Computer.FileSystem.SpecialDirectories.MyDocuments` 屬性，來提供路徑。</span><span class="sxs-lookup"><span data-stu-id="95e21-106">Use the `My.Computer.FileSystem.SpecialDirectories.MyDocuments` property to supply the path.</span></span>  
  
     [!code-vb[VbFileIOWrite#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#1)]  
  
2. <span data-ttu-id="95e21-107">使用 `WriteAllText` 方法，將文字寫入指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="95e21-107">Use the `WriteAllText` method to write text to the specified file.</span></span>  
  
     [!code-vb[VbVbcnMyFileSystem#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#14)]  
  
## <a name="example"></a><span data-ttu-id="95e21-108">範例</span><span class="sxs-lookup"><span data-stu-id="95e21-108">Example</span></span>  

 [!code-vb[VbFileIOWrite#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#2)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="95e21-109">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="95e21-109">Compiling the Code</span></span>  

 <span data-ttu-id="95e21-110">請將 `test.txt` 取代為您想要寫入之檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="95e21-110">Replace `test.txt` with the name of the file you want to write to.</span></span>  
  
## <a name="robust-programming"></a><span data-ttu-id="95e21-111">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="95e21-111">Robust Programming</span></span>  

 <span data-ttu-id="95e21-112">這個程式碼會重新擲回將文字寫入檔案時可能發生的所有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="95e21-112">This code rethrows all the exceptions that may occur when writing text to the file.</span></span> <span data-ttu-id="95e21-113">使用 [OpenFileDialog](/dotnet/desktop/winforms/controls/openfiledialog-component-windows-forms) 和 [SaveFileDialog](/dotnet/desktop/winforms/controls/savefiledialog-component-windows-forms) 元件這類 Windows Forms 控制項以將使用者選項限制為有效檔案名稱，即可減少例外狀況的可能性。</span><span class="sxs-lookup"><span data-stu-id="95e21-113">You can reduce the likelihood of exceptions by using Windows Forms controls such as the [OpenFileDialog](/dotnet/desktop/winforms/controls/openfiledialog-component-windows-forms) and the [SaveFileDialog](/dotnet/desktop/winforms/controls/savefiledialog-component-windows-forms) components that limit the user choices to valid file names.</span></span> <span data-ttu-id="95e21-114">不過，使用這些控制項並不容易。</span><span class="sxs-lookup"><span data-stu-id="95e21-114">Using these controls is not foolproof, however.</span></span> <span data-ttu-id="95e21-115">在使用者選取檔案的時間與程式碼執行的時間之間，可以變更檔案系統。</span><span class="sxs-lookup"><span data-stu-id="95e21-115">The file system can change between the time the user selects a file and the time that the code executes.</span></span> <span data-ttu-id="95e21-116">因此，使用檔案時，幾乎一律都需要進行例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="95e21-116">Exception handling is therefore nearly always necessary when with working with files.</span></span>  
  
## <a name="net-framework-security"></a><span data-ttu-id="95e21-117">.NET Framework 安全性</span><span class="sxs-lookup"><span data-stu-id="95e21-117">.NET Framework Security</span></span>  

 <span data-ttu-id="95e21-118">如果要在部分信任內容中執行，則程式碼可能會因權限不足而擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="95e21-118">If you are running in a partial-trust context, the code might throw an exception due to insufficient privileges.</span></span> <span data-ttu-id="95e21-119">如需詳細資訊，請參閱 [Code Access Security Basics](../../../../framework/misc/code-access-security-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="95e21-119">For more information, see [Code Access Security Basics](../../../../framework/misc/code-access-security-basics.md).</span></span>  
  
 <span data-ttu-id="95e21-120">這個範例會建立新的檔案。</span><span class="sxs-lookup"><span data-stu-id="95e21-120">This example creates a new file.</span></span> <span data-ttu-id="95e21-121">如果應用程式需要建立檔案，該應用程式就需要資料夾的 [建立] 權限。</span><span class="sxs-lookup"><span data-stu-id="95e21-121">If an application needs to create a file, that application needs Create permission for the folder.</span></span> <span data-ttu-id="95e21-122">您可以使用存取控制清單來設定權限。</span><span class="sxs-lookup"><span data-stu-id="95e21-122">Permissions are set using access control lists.</span></span> <span data-ttu-id="95e21-123">如果檔案已經存在，則應用程式只需要 [寫入] 權限，這是較小的權限。</span><span class="sxs-lookup"><span data-stu-id="95e21-123">If the file already exists, the application needs only Write permission, a lesser privilege.</span></span> <span data-ttu-id="95e21-124">若有可能，更為安全的做法是在部署期間建立檔案，並且只授與單一檔案的 [讀取] 權限，而不授與資料夾的 [建立] 權限。</span><span class="sxs-lookup"><span data-stu-id="95e21-124">Where possible, it is more secure to create the file during deployment, and only grant Read privileges to a single file, rather than to grant Create privileges for a folder.</span></span> <span data-ttu-id="95e21-125">此外，將資料寫入使用者資料夾，比根資料夾或 **Program Files** 資料夾更安全。</span><span class="sxs-lookup"><span data-stu-id="95e21-125">Also, it is more secure to write data to user folders than to the root folder or the **Program Files** folder.</span></span> <span data-ttu-id="95e21-126">如需詳細資訊，請參閱 [ACL 技術概觀](/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="95e21-126">For more information, see [ACL Technology Overview](/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="95e21-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="95e21-127">See also</span></span>

- <xref:System.IO.Path.Combine%2A?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>
