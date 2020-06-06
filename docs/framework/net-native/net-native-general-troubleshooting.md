---
title: .NET Native 一般疑難排解
ms.date: 03/30/2017
ms.assetid: ee8c5e17-35ea-48a1-8767-83298caac1e8
ms.openlocfilehash: 2bea81e380fed6c456898e9883658ef874c8dd97
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128232"
---
# <a name="net-native-general-troubleshooting"></a><span data-ttu-id="101fe-102">.NET Native 一般疑難排解</span><span class="sxs-lookup"><span data-stu-id="101fe-102">.NET Native General Troubleshooting</span></span>

<span data-ttu-id="101fe-103">本主題說明如何針對使用 .NET Native 開發應用程式時可能遇到的潛在問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="101fe-103">This topic describes how to troubleshoot potential issues that you might encounter when developing apps with .NET Native.</span></span>

- <span data-ttu-id="101fe-104">**問題：** 您的建置輸出視窗未正確更新。</span><span class="sxs-lookup"><span data-stu-id="101fe-104">**Issue:** Your build output window isn't properly updated.</span></span>

  <span data-ttu-id="101fe-105">**解決方式：** 建置輸出視窗必須等到建置完成才會更新。</span><span class="sxs-lookup"><span data-stu-id="101fe-105">**Resolution:** The build output window isn't updated until the build completes.</span></span> <span data-ttu-id="101fe-106">建置時間可能長達數分鐘，因此您可能晚點才會看到更新。</span><span class="sxs-lookup"><span data-stu-id="101fe-106">Build times may be up to several minutes, so you might experience a delay in seeing the updates.</span></span>

- <span data-ttu-id="101fe-107">**問題：** ARM 的應用程式正式版本建置時間變長。</span><span class="sxs-lookup"><span data-stu-id="101fe-107">**Issue:** Your app’s retail build time for ARM has increased.</span></span>

  <span data-ttu-id="101fe-108">**解決方式：** 當您將應用程式部署至 ARM 裝置時，會叫用 .NET Native 的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="101fe-108">**Resolution:** When you deploy an app to your ARM device, the .NET Native infrastructure is invoked.</span></span> <span data-ttu-id="101fe-109">這個編譯會執行大量最佳化，同時確保該非靜態語意 (例如反映) 仍然能夠正常運作。</span><span class="sxs-lookup"><span data-stu-id="101fe-109">This compilation performs a large number of optimizations while ensuring that non-static semantics such as reflection continue to work.</span></span> <span data-ttu-id="101fe-110">此外，應用程式使用的 .NET Framework 部分已靜態連結，以取得最佳效能，因此也必須編譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="101fe-110">In addition, the portion of the .NET Framework that the app uses is statically linked in for optimal performance and has to be compiled into native code as well.</span></span> <span data-ttu-id="101fe-111">這就是編譯需要更多時間的原因。</span><span class="sxs-lookup"><span data-stu-id="101fe-111">This is why compilation takes longer.</span></span>

  <span data-ttu-id="101fe-112">不過，對於標準開發電腦上的大多數應用程式而言，編譯時間仍然在標準編譯的一分鐘內。</span><span class="sxs-lookup"><span data-stu-id="101fe-112">However, compilation times are still within a minute of standard compilation for most apps on a standard development machine.</span></span>  <span data-ttu-id="101fe-113">一般而言，光是在標準開發電腦上產生 .NET Framework 的原生映像就需要數分鐘。</span><span class="sxs-lookup"><span data-stu-id="101fe-113">Typically, just generating native images for the .NET Framework on a standard development machine takes several minutes.</span></span>  <span data-ttu-id="101fe-114">即使執行所有最佳化來改善產生的程式碼 (包括使用 .NET Framework)，應用程式建置時間通常還是需要一到兩分鐘。</span><span class="sxs-lookup"><span data-stu-id="101fe-114">Even with all the optimizations to improve the generated code and with including the .NET Framework, app build times are typically a minute or two.</span></span>

  <span data-ttu-id="101fe-115">我們將調查多執行緒編譯和其他最佳化，持續提升編譯效能。</span><span class="sxs-lookup"><span data-stu-id="101fe-115">We are continuing to work on improving compilation performance by investigating multi-threaded compilation and other optimizations.</span></span>

- <span data-ttu-id="101fe-116">**問題：** 您不知道您的應用程式是使用 .NET Native 編譯。</span><span class="sxs-lookup"><span data-stu-id="101fe-116">**Issue:** You don’t know if your app was compiled using .NET Native.</span></span>

  <span data-ttu-id="101fe-117">**解決方式：** 如果叫用 .NET Native 編譯器，您會發現組建時間較長，而且 [工作管理員] 會顯示各種 .NET Native 元件進程，例如 ILC.OUT .exe 和 nutc_driver .exe。</span><span class="sxs-lookup"><span data-stu-id="101fe-117">**Resolution:** If the .NET Native compiler is invoked, you'll notice longer build times, and Task Manager will show various .NET Native component processes such as ILC.exe and nutc_driver.exe.</span></span>

  <span data-ttu-id="101fe-118">使用 .NET Native 成功建立專案之後，您會在 obj 設定架構 \\ *config* \  *arch* \\ *專案名稱*ilc\out. 中找到輸出。 您可以在 [bin 架構設定 \appx] 下找到最終的原生套件內容 \\ *arch* \\ *config*</span><span class="sxs-lookup"><span data-stu-id="101fe-118">After you successfully build your project with .NET Native, you'll find the output under obj\\*config*\ *arch*\\*projectname*.ilc\out.  The final native package contents can be found under bin\\*arch*\\*config*\AppX.</span></span> <span data-ttu-id="101fe-119">\\ *arch* \\ *config*如果您已部署應用程式，最終的原生套件內容會位於 \bin 架構設定 \appx 下之下。</span><span class="sxs-lookup"><span data-stu-id="101fe-119">The final native package contents are under \bin\\*arch*\\*config*\AppX if you have deployed the app.</span></span>

- <span data-ttu-id="101fe-120">**問題：** 以 .NET Native 編譯的應用程式正在擲回執行階段例外狀況 (通常是 [MissingMetadataException](missingmetadataexception-class-net-native.md) 或 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外狀況)，未使用 .NET Native 編譯時不會擲回該例外狀況。</span><span class="sxs-lookup"><span data-stu-id="101fe-120">**Issue:** Your .NET Native-compiled app is throwing runtime exceptions (typically [MissingMetadataException](missingmetadataexception-class-net-native.md) or [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) exceptions) that it did not throw when compiled without .NET Native.</span></span>

  <span data-ttu-id="101fe-121">**解決方式：** 擲回例外狀況的原因是 .NET Native 未提供可透過反映提供的中繼資料或實作程式碼</span><span class="sxs-lookup"><span data-stu-id="101fe-121">**Resolution:** The exceptions are thrown because .NET Native did not provide either the metadata or the implementation code that is otherwise available through reflection.</span></span> <span data-ttu-id="101fe-122">（如需詳細資訊，請參閱[.NET Native 和編譯](net-native-and-compilation.md)）。若要排除例外狀況，您必須在執行時間指示詞[（rd .xml）](runtime-directives-rd-xml-configuration-file-reference.md)檔案中加入一個專案，讓 .NET Native 工具鏈可以讓中繼資料或程式碼在執行時間可供使用。</span><span class="sxs-lookup"><span data-stu-id="101fe-122">(For more information, see [.NET Native and Compilation](net-native-and-compilation.md).) To eliminate the exception, you have to add an entry to your [runtime directives (rd.xml) file](runtime-directives-rd-xml-configuration-file-reference.md) so that the .NET Native tool chain can make the metadata or implementation code available at runtime.</span></span> <span data-ttu-id="101fe-123">您可以使用兩個疑難排解工具，這些工具會產生要加入執行階段指示詞檔案的必要項目：</span><span class="sxs-lookup"><span data-stu-id="101fe-123">Two troubleshooters are available that will generate the necessary entry to add to your runtime directives file:</span></span>

  - <span data-ttu-id="101fe-124">針對類型的 [MissingMetadataException 疑難排解工具](https://dotnet.github.io/native/troubleshooter/type.html) 。</span><span class="sxs-lookup"><span data-stu-id="101fe-124">The [MissingMetadataException troubleshooter](https://dotnet.github.io/native/troubleshooter/type.html) for types.</span></span>

  - <span data-ttu-id="101fe-125">針對方法的 [MissingMetadataException 疑難排解工具](https://dotnet.github.io/native/troubleshooter/method.html) 。</span><span class="sxs-lookup"><span data-stu-id="101fe-125">The [MissingMetadataException troubleshooter](https://dotnet.github.io/native/troubleshooter/method.html) for methods.</span></span>

  <span data-ttu-id="101fe-126">如需詳細資訊，請參閱[反映和 .NET Native](reflection-and-net-native.md)。</span><span class="sxs-lookup"><span data-stu-id="101fe-126">For more information, see [Reflection and .NET Native](reflection-and-net-native.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="101fe-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="101fe-127">See also</span></span>

- [<span data-ttu-id="101fe-128">將您的 Windows 市集應用程式移轉至 .NET Native</span><span class="sxs-lookup"><span data-stu-id="101fe-128">Migrating Your Windows Store App to .NET Native</span></span>](migrating-your-windows-store-app-to-net-native.md)
