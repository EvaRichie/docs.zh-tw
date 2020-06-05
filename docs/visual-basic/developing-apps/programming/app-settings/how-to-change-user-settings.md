---
title: 作法：變更使用者設定
ms.date: 07/20/2015
helpviewer_keywords:
- user settings [Visual Basic], changing in Visual Basic
- user settings
- My.Settings object [Visual Basic], changing user settings
- examples [Visual Basic], changing user settings
ms.assetid: 41250181-c594-4854-9988-8183b9eb03cf
ms.openlocfilehash: c9b89459f9b443c3a447edce90fee3437bbf1b6a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410175"
---
# <a name="how-to-change-user-settings-in-visual-basic"></a><span data-ttu-id="33cde-102">如何：在 Visual Basic 中變更使用者設定</span><span class="sxs-lookup"><span data-stu-id="33cde-102">How to: Change User Settings in Visual Basic</span></span>

<span data-ttu-id="33cde-103">您可以將新值指派給 `My.Settings` 物件的設定屬性，來變更使用者設定。</span><span class="sxs-lookup"><span data-stu-id="33cde-103">You can change a user setting by assigning a new value to the setting's property on the `My.Settings` object.</span></span>  
  
 <span data-ttu-id="33cde-104">`My.Settings` 物件會將每項設定公開為屬性。</span><span class="sxs-lookup"><span data-stu-id="33cde-104">The `My.Settings` object exposes each setting as a property.</span></span> <span data-ttu-id="33cde-105">屬性名稱與設定名稱相同，而屬性類型與設定類型相同。</span><span class="sxs-lookup"><span data-stu-id="33cde-105">The property name is the same as the setting name, and the property type is the same as the setting type.</span></span> <span data-ttu-id="33cde-106">設定的 [範圍] 可判斷屬性是否為唯讀：[應用程式] 範圍設定的屬性為唯讀，而 [使用者] 範圍設定的屬性為讀寫。\*\*\*\*\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="33cde-106">The setting's **Scope** determines if the property is read-only: The property for an **Application**-scope setting is read-only, while the property for a **User**-scope setting is read-write.</span></span> <span data-ttu-id="33cde-107">如需詳細資訊，請參閱 [My.Settings 物件](../../../language-reference/objects/my-settings-object.md)。</span><span class="sxs-lookup"><span data-stu-id="33cde-107">For more information, see [My.Settings Object](../../../language-reference/objects/my-settings-object.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="33cde-108">雖然您可以在執行階段變更和儲存使用者範圍設定的值，但是應用程式範圍的設定為唯讀，且無法以程式設計方式變更。</span><span class="sxs-lookup"><span data-stu-id="33cde-108">Although you can change and save the values of user-scope settings at run time, application-scope settings are read-only and cannot be changed programmatically.</span></span> <span data-ttu-id="33cde-109">建立應用程式時，您可以使用 [專案設計工具] 或編輯應用程式組態檔，來變更應用程式範圍的設定。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="33cde-109">You can change application-scope settings when you create the application by using the **Project Designer** or by editing the application's configuration file.</span></span> <span data-ttu-id="33cde-110">如需詳細資訊，請參閱[管理應用程式設定 (.NET)](/visualstudio/ide/managing-application-settings-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="33cde-110">For more information, see [Managing Application Settings (.NET)](/visualstudio/ide/managing-application-settings-dotnet).</span></span>  
  
## <a name="example"></a><span data-ttu-id="33cde-111">範例</span><span class="sxs-lookup"><span data-stu-id="33cde-111">Example</span></span>  

 <span data-ttu-id="33cde-112">這個範例會變更 `Nickname` 使用者設定的值。</span><span class="sxs-lookup"><span data-stu-id="33cde-112">This example changes the value of the `Nickname` user setting.</span></span>  
  
 [!code-vb[VbVbalrMyResources#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#7)]  
  
 <span data-ttu-id="33cde-113">為了確保此範例正常運作，您的應用程式必須具有 `String` 類型的 `Nickname` 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="33cde-113">For this example to work, your application must have a `Nickname` user setting, of type `String`.</span></span>  
  
 <span data-ttu-id="33cde-114">應用程式關閉時，會儲存使用者設定。</span><span class="sxs-lookup"><span data-stu-id="33cde-114">The application saves the user settings when the application shuts down.</span></span> <span data-ttu-id="33cde-115">若要立即儲存設定，請呼叫 `My.Settings.Save` 方法。</span><span class="sxs-lookup"><span data-stu-id="33cde-115">To save the settings immediately, call the `My.Settings.Save` method.</span></span> <span data-ttu-id="33cde-116">如需詳細資訊，請參閱[如何：保存 Visual Basic 中的使用者設定](how-to-persist-user-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="33cde-116">For more information, see [How to: Persist User Settings in Visual Basic](how-to-persist-user-settings.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="33cde-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="33cde-117">See also</span></span>

- [<span data-ttu-id="33cde-118">My.Settings 物件</span><span class="sxs-lookup"><span data-stu-id="33cde-118">My.Settings Object</span></span>](../../../language-reference/objects/my-settings-object.md)
- [<span data-ttu-id="33cde-119">如何：在 Visual Basic 中讀取應用程式設定</span><span class="sxs-lookup"><span data-stu-id="33cde-119">How to: Read Application Settings in Visual Basic</span></span>](how-to-read-application-settings.md)
- [<span data-ttu-id="33cde-120">如何：保存 Visual Basic 中的使用者設定</span><span class="sxs-lookup"><span data-stu-id="33cde-120">How to: Persist User Settings in Visual Basic</span></span>](how-to-persist-user-settings.md)
- [<span data-ttu-id="33cde-121">如何：在 Visual Basic 中建立使用者設定的屬性方格</span><span class="sxs-lookup"><span data-stu-id="33cde-121">How to: Create Property Grids for User Settings in Visual Basic</span></span>](how-to-create-property-grids-for-user-settings.md)
- [<span data-ttu-id="33cde-122">管理應用程式設定 (.NET)</span><span class="sxs-lookup"><span data-stu-id="33cde-122">Managing Application Settings (.NET)</span></span>](/visualstudio/ide/managing-application-settings-dotnet)
