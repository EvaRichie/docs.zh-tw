---
title: .NET Framework 的概觀
description: 閱讀有關 .NET 的總覽，這是支援建立和執行 Windows 應用程式和 web 服務的技術。
ms.date: 03/30/2017
helpviewer_keywords:
- application development [.NET Framework]
- common language runtime
- common language runtime, about
- common language runtime, overview
ms.assetid: 29848c96-fc36-462d-8072-ba223a40b697
ms.openlocfilehash: 3577a3ad13d9ef6935a1bed8a29e3d594857928e
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557758"
---
# <a name="overview-of-net-framework"></a>.NET Framework 概觀

.NET Framework 是一種技術，可支援建立和執行 Windows 應用程式和 web 服務。 .NET Framework 的設計目的是要滿足下列目標：

- 提供一致的物件導向程式設計環境，不論物件程式碼是在本機儲存和執行、在本機執行、在本機執行，或是在遠端執行。

- 提供可減少軟體部署和版本控制衝突的程式碼執行環境。

- 提供加強程式碼安全執行的程式碼執行環境，包括未知或非完全信任之協力廠商所建立的程式碼。

- 提供可消除編寫指令碼或解譯環境效能問題的程式碼執行環境。

- 使開發人員在開發各類應用程式 (例如 Windows 架構應用程式和 Web 架構應用程式) 時享有一致的體驗。

- 若要建立業界標準的所有通訊，以確保以 .NET Framework 為基礎的程式碼與任何其他程式碼整合。

> [!NOTE]
> 如需使用者和開發人員 .NET Framework 的一般簡介，請參閱 [開始](index.md)使用。

.NET Framework 是由 common language runtime (CLR) 和 .NET Framework 類別庫所組成。 Common language runtime 是 .NET Framework 的基礎。 請將執行階段視為在執行階段管理程式碼的代理程式，可提供記憶體管理、執行緒管理和遠端作業等核心服務，並同時強制執行嚴格的型別安全及其他形式的程式碼精確度，以提升安全性和穩定性。 事實上，程式碼管理的概念是此執行階段的基本原則。 針對執行階段所開發的程式碼稱為 Managed 程式碼，而不針對執行階段所開發的程式碼稱為 Unmanaged 程式碼。 類別庫是一組完整的物件導向集合，可用來開發應用程式，範圍從傳統的命令列或圖形化使用者介面， (GUI) 應用程式到以 ASP.NET 提供的最新創新（例如 Web Form 和 XML Web 服務）為基礎的應用程式。

.NET Framework 可以由未受管理的元件裝載，而這些元件會將 common language runtime 載入其進程中，並開始執行 managed 程式碼，藉此建立可同時利用 managed 和非受控功能的軟體環境。 .NET Framework 不只提供數個執行時間主機，也支援協力廠商執行階段主機的開發。

例如，ASP.NET 裝載執行階段以提供可擴充、伺服器端的 Managed 程式碼環境。 ASP.NET 可直接與執行時間搭配運作，以啟用 ASP.NET apps 和 XML web service，這兩者將在本文稍後討論。

Internet Explorer 是裝載執行階段的 Unmanaged 應用程式範例 (採用 MIME 類型擴充的形式)。 使用 Internet Explorer 裝載執行階段，讓您能夠將 Managed 元件或 Windows Form 控制項嵌入 HTML 文件。 以這種方式裝載執行階段，就會讓 Managed 行動程式碼變得可行，不過只有 Managed 程式碼才能提供明顯的改善，例如非完全信任執行和隔離檔案儲存。

下圖顯示 Common Language Runtime 和類別庫與您的應用程式及整體系統的關係。 下圖也顯示 Managed 程式碼是如何在較大架構中運作的。

![下圖也顯示受控碼是如何在較大的架構中運作。](./media/overview/language-runtime-class-library-relationship.gif)

下列各節會更詳細地說明 .NET Framework 的主要功能。

## <a name="features-of-the-common-language-runtime"></a>Common Language Runtime 的功能

Common Language Runtime 負責管理記憶體、執行緒執行、程式碼執行、程式碼安全驗證、編譯 (Compilation) 和其他系統服務。 這些功能都內建到在 Common Language Runtime 上執行的 Managed 程式碼中。

就安全性而言，Managed 元件會根據若干因素而被授予不同程度的信任，這些因素包括元件的原始出處 (例如網際網路、企業網路或本機電腦)。 這表示即使是在相同作用中的應用程式中使用，Managed 元件可能可以也可能無法執行檔案存取作業、註冊存取作業或其他易受影響的功能。

Runtime 也會藉由實作嚴格的型別和程式碼驗證基礎架構，也就是一般型別系統 (CTS)，強制執行程式碼的加強性。 CTS 確保所有 Managed 程式碼都能夠自我描述。 不同的 Microsoft 和協力廠商語言編譯器會產生符合 CTS 的 Managed 程式碼。 這表示 Managed 程式碼不但能夠使用其他 Managed 型別和執行個體，同時還能嚴格強制執行型別精確度和型別安全。

此外，Runtime 的 Managed 環境排除許多常見的軟體問題。 例如，Runtime 能夠自動處理物件配置，並管理對物件的參考，而且在不再用它們時加以釋放。 這種自動記憶體管理解決了兩個最常見的應用程式錯誤：記憶體流失和無效的記憶體參考。

Runtime 也提升開發人員的產能。 例如，程式設計人員可以用自己選擇的開發語言撰寫應用程式，但仍充分利用其他開發人員以其他語言所撰寫的執行階段、類別庫和元件。 選擇以執行階段為目標來開發編譯器的廠商都可作到這一點。 以 .NET Framework 為目標的語言編譯器可以將 .NET Framework 的功能提供給以該語言所撰寫的現有程式碼使用，大幅簡化現有應用程式的移轉程序。

Runtime 是為未來軟體所設計的，但它也支援目前和過去的軟體。 Managed 和 Unmanaged 程式碼的互通性 (Interoperability)，讓開發人員繼續使用必要的 COM 元件和 DLL。

Runtime 是為增強效能所設計的。 雖然 Common Language Runtime 提供許多標準的執行階段服務，但未曾解譯 Managed 程式碼。 透過一項稱為 Just-In-Time (JIT) 編譯的功能，所有的 Managed 程式碼都可使用執行所在系統的原生機器語言執行。 同時，記憶體管理員移除分散的記憶體的可能性，增加記憶體參考位置，以進一步提高效能。

最後，執行階段可由高效能的伺服器端應用程式裝載，例如 Microsoft SQL Server 和 Internet Information Services (IIS)。 這個基礎架構讓您使用 Managed 程式碼撰寫商務邏輯的同時，仍能夠享受到由業界最佳、可支援執行階段主應用程式的企業伺服器所提供的超高效能。

## <a name="net-framework-class-library"></a>.NET Framework 類別庫

.NET Framework 類別庫是與 Common Language Runtime 緊密整合的可重複使用型別的集合。 此類別庫為物件導向，能提供類型讓您撰寫自己的 Managed 程式碼從其衍生功能。 這不但使 .NET Framework 類型易於使用，也減少了學習 .NET Framework 新功能所需的時間。 此外，協力廠商元件也可以與 .NET Framework 中的類別完美整合。

例如，.NET Framework 集合類別會實作一組介面，以開發您自己的集合類別。 您的集合類別會與 .NET Framework 中的類別完美結合。

與面向物件類別庫的預期一樣，.NET Framework 型別可讓您完成許多常見的程式設計工作，包括字串管理、資料收集、資料庫連接和檔案存取。 除了通用工作，類別庫還包括能夠支援各種特定開發案例的型別。 您可以使用 .NET Framework 來開發下列類型的應用程式和服務：

- 主控台應用程式。 請參閱[建置主控台應用程式](../../standard/building-console-apps.md)。

- Windows GUI 應用程式 (Windows Forms)。 請參閱 [Windows Forms](/dotnet/desktop/winforms/)。

- Windows Presentation Foundation (WPF) 應用程式。 請參閱 [Windows Presentation Foundation](/dotnet/desktop/wpf/)。

- ASP.NET 應用程式。 請參閱[使用 ASP.NET 的 Web 應用程式](../develop-web-apps-with-aspnet.md)。

- Windows 服務 請參閱 [Windows 服務應用程式簡介](../windows-services/introduction-to-windows-service-applications.md)。

- 使用 Windows Communication Foundation (WCF) 的服務導向應用程式。 請參閱[使用 WCF 以服務為導向的應用程式](../wcf/index.md)。

- 使用 Windows Workflow Foundation (WF) 啟用工作流程的應用程式。 請參閱 [Windows Workflow Foundation](../windows-workflow-foundation/index.md)。

Windows Forms 類別是一組完整且可重複使用的類型，可大幅簡化 Windows GUI 的開發。 如果要撰寫 ASP.NET Web Form 應用程式，即可使用 Web Form 類別。

## <a name="see-also"></a>另請參閱

- [系統需求](system-requirements.md)
- [安裝指南](../install/index.md)
- [開發指南](../development-guide.md)
- [工具](../tools/index.md)
- [.NET 範例與教學課程](../../samples-and-tutorials/index.md)
- [.NET API 瀏覽器](../../../api/index.md)
