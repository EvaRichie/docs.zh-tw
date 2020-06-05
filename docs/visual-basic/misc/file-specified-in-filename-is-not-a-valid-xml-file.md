---
title: 檔案名稱中指定的檔案不是有效的 XML 檔案
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: a84042490935e3e7e5a6de2a802d9effd5b4d3d4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84358344"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a><span data-ttu-id="52a26-102">檔案名稱中指定的檔案不是有效的 XML 檔案</span><span class="sxs-lookup"><span data-stu-id="52a26-102">File specified in FileName is not a valid XML file</span></span>

<span data-ttu-id="52a26-103">您提供的檔案名稱不是有效的 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="52a26-103">The file name that you supplied is not a valid XML file.</span></span> <span data-ttu-id="52a26-104">若要指定 XML 文件所允許的結構和內容，您可以使用文件類型定義 (DTD)、Microsoft XDR (XML-Data Reduced) 結構描述或 XML 結構描述定義語言 (XSD) 結構描述。</span><span class="sxs-lookup"><span data-stu-id="52a26-104">To specify the allowed structure and content of an XML document, you can use a Document Type Definition (DTD), a Microsoft XML-Data Reduced (XDR) schema, or an XML Schema definition language (XSD) schema.</span></span> <span data-ttu-id="52a26-105">XSD 架構是在 .NET Framework 中指定 XML 文法的慣用方式。</span><span class="sxs-lookup"><span data-stu-id="52a26-105">XSD schemas are the preferred way to specify XML grammars in the .NET Framework.</span></span>

> [!NOTE]
> <span data-ttu-id="52a26-106">在某些舊版 Visual Studio 中， **XML 設計工具** 是具類型資料集和 XML 結構描述的設計工具。</span><span class="sxs-lookup"><span data-stu-id="52a26-106">In some earlier versions of Visual Studio, the **XML Designer** is the designer for typed datasets and XML schema.</span></span> <span data-ttu-id="52a26-107">**XML 設計工具** 仍可用來建立及編輯 XML 結構描述檔案。</span><span class="sxs-lookup"><span data-stu-id="52a26-107">The **XML Designer** can still be used to create and edit XML schema files.</span></span> <span data-ttu-id="52a26-108">不過，在 Visual Studio 2012 中，建立和編輯具類型資料集的設計工具是**DataSet 設計工具**。</span><span class="sxs-lookup"><span data-stu-id="52a26-108">However, in Visual Studio 2012, the designer for creating and editing typed datasets is the **Dataset Designer**.</span></span> <span data-ttu-id="52a26-109">如需詳細資訊，請參閱[建立和編輯具類型的資料集](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120))。</span><span class="sxs-lookup"><span data-stu-id="52a26-109">For more information, see [Creating and Editing Typed Datasets](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120)).</span></span>

## <a name="to-correct-this-error"></a><span data-ttu-id="52a26-110">更正這個錯誤</span><span class="sxs-lookup"><span data-stu-id="52a26-110">To correct this error</span></span>

- <span data-ttu-id="52a26-111">確認您提供的檔案名稱正確。</span><span class="sxs-lookup"><span data-stu-id="52a26-111">Check that you are supplying the correct file name.</span></span>

- <span data-ttu-id="52a26-112">將您要檢查的 XML 檔案載入 **XML 設計工具**，以檢查指定的檔案是否包含有效的 XML。</span><span class="sxs-lookup"><span data-stu-id="52a26-112">Check that the specified file contains valid XML by loading the XML file that you want to check into the **XML Designer**.</span></span> <span data-ttu-id="52a26-113">從 [XML] \*\*\*\* 功能表按一下 [驗證 XML] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="52a26-113">From the **XML** menu, click **Validate XML**.</span></span> <span data-ttu-id="52a26-114">[工作清單] \*\*\*\* 中會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="52a26-114">Errors are displayed in the **Task List**.</span></span>

- <span data-ttu-id="52a26-115">如果 XML 檔案有關聯的 XML 結構描述，請確認項目出現在定義的結構中，而且個別項目的內容符合結構描述中所指定的宣告資料類型。</span><span class="sxs-lookup"><span data-stu-id="52a26-115">If the XML file has an associated XML Schema, check that the elements appear in the defined structure and that the content of the individual elements conforms to the declared data types specified in the schema.</span></span>

## <a name="see-also"></a><span data-ttu-id="52a26-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="52a26-116">See also</span></span>

- <xref:System.Xml>
- [<span data-ttu-id="52a26-117">作法：剖析檔案路徑</span><span class="sxs-lookup"><span data-stu-id="52a26-117">How to: Parse File Paths</span></span>](../developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
