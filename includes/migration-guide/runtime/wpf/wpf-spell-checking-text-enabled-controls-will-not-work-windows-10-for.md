---
ms.openlocfilehash: 1d2e4a058008676c6ea85becebd4bb9220569ef3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621161"
---
### <a name="wpf-spell-checking-in-text-enabled-controls-will-not-work-in-windows-10-for-languages-not-in-the-oss-input-language-list"></a><span data-ttu-id="91baa-101">若語言不在 OS 的輸入語言清單中，啟用文字之控制項中的　WPF 拼字檢查不適用於 Windows 10</span><span class="sxs-lookup"><span data-stu-id="91baa-101">WPF spell checking in text-enabled controls will not work in Windows 10 for languages not in the OS's input language list</span></span>

#### <a name="details"></a><span data-ttu-id="91baa-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="91baa-102">Details</span></span>

<span data-ttu-id="91baa-103">因為只有輸入語言清單上的語言可以使用平台拼字檢查功能，所以拼字檢查工具在 Windows 10 上執行時可能不適用於啟用 WPF 文字的控制項。在 Windows 10 中，將語言新增至可用鍵盤的清單時，Windows 會自動下載並安裝對應的 Feature on Demand (FOD) 套件，以提供拼字檢查功能。</span><span class="sxs-lookup"><span data-stu-id="91baa-103">When running on Windows 10, the spell checker may not work for WPF text-enabled controls because platform spell-checking capabilities are available only for languages present in the input languages list.In Windows 10, when a language is added to the list of available keyboards, Windows automatically downloads and installs a corresponding Feature on Demand (FOD) package that provides spell-checking capabilities.</span></span> <span data-ttu-id="91baa-104">只要將語言加入輸入語言清單中，就可支援拼字檢查工具。</span><span class="sxs-lookup"><span data-stu-id="91baa-104">By adding the language to the input languages list, the spell checker will be supported.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="91baa-105">建議</span><span class="sxs-lookup"><span data-stu-id="91baa-105">Suggestion</span></span>

<span data-ttu-id="91baa-106">請注意，要進行拼字檢查的語言或文字必須新增為輸入語言，拼字檢查才能在 Windows 10 中正常運作。</span><span class="sxs-lookup"><span data-stu-id="91baa-106">Be aware that the language or text to be spell-checked must be added as an input language for spell-checking to work in Windows 10.</span></span>

| <span data-ttu-id="91baa-107">名稱</span><span class="sxs-lookup"><span data-stu-id="91baa-107">Name</span></span>    | <span data-ttu-id="91baa-108">值</span><span class="sxs-lookup"><span data-stu-id="91baa-108">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="91baa-109">影響範圍</span><span class="sxs-lookup"><span data-stu-id="91baa-109">Scope</span></span>   |<span data-ttu-id="91baa-110">Edge</span><span class="sxs-lookup"><span data-stu-id="91baa-110">Edge</span></span>|
|<span data-ttu-id="91baa-111">版本</span><span class="sxs-lookup"><span data-stu-id="91baa-111">Version</span></span>|<span data-ttu-id="91baa-112">4.6</span><span class="sxs-lookup"><span data-stu-id="91baa-112">4.6</span></span>|
|<span data-ttu-id="91baa-113">類型</span><span class="sxs-lookup"><span data-stu-id="91baa-113">Type</span></span>|<span data-ttu-id="91baa-114">執行階段</span><span class="sxs-lookup"><span data-stu-id="91baa-114">Runtime</span></span>|
