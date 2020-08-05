---
title: .NET 的安全程式碼撰寫方針
description: 設計要使用的程式碼。NET 強制許可權和其他強制性，以協助防止惡意程式碼存取資料或執行其他動作。
ms.date: 07/15/2020
helpviewer_keywords:
- managed wrapper to native code implementation
- secure coding
- reusable components
- library code that exposes protected resources
- code, security
- code security
- secure coding, options
- components [.NET], security
- code security, options
- security-neutral code
- security [.NET], coding guidelines
ms.assetid: 4f882d94-262b-4494-b0a6-ba9ba1f5f177
ms.openlocfilehash: a05e0cec2814be88ac835d05601d5cf5f66383c3
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555952"
---
# <a name="secure-coding-guidelines"></a>安全程式碼撰寫方針

大部分的應用程式程式碼都可以直接使用 .NET 所實行的基礎結構。 某些情況還需要其他的應用程式特定安全性 (藉由擴充安全性系統或是使用新的臨機操作方法來建置)。

在您的程式碼中使用 .NET 強制執行的許可權和其他強制性時，您應該為防止惡意程式碼存取您不想要它擁有或執行其他不必要動作的資訊進行阻礙。 此外，在所有使用受信任程式碼的可預期案例中，您必須在安全性與可用性之間達成平衡。

本概觀說明設計程式碼以搭配使用安全性系統時，可以採用的不同方式。

## <a name="securing-resource-access"></a>保護資源存取

當設計和撰寫程式碼時，您需要保護並限制程式碼對資源的存取，特別是當使用或叫用未知來源的程式碼時。 因此，請牢記下列技術，以確保程式碼是安全的︰

- 請勿使用程式碼存取安全性 (CAS)。

- 請勿使用部分信任程式碼。

- 請勿使用[AllowPartiallyTrustedCaller](xref:System.Security.AllowPartiallyTrustedCallersAttribute)屬性 (APTCA) 。

- 請勿使用 .NET 遠端處理。

- 請勿使用分散式元件物件模型 (DCOM)。

- 請勿使用二進位格式器。

代碼啟用安全性和安全性透明的程式碼不支援做為部分信任程式碼的安全性界限。 建議不要載入及執行未知來源的程式碼，如此便不需要使用替代的安全措施。 替代的安全性措施包括︰

- 虛擬化

- AppContainers

- 作業系統 (OS) 使用者和權限

- Hyper-V 容器

## <a name="security-neutral-code"></a>安全性中性的程式碼

安全性中性的程式碼與安全性系統並無明顯關聯。 它會使用接收到的任何使用權限來執行。 雖然無法攔截與受保護作業相關聯之安全性例外狀況的應用程式 (例如使用檔案、網路功能等等) 可能會導致未處理的例外狀況，但安全性中性的程式碼仍然會利用 .NET 中的安全性技術。

安全性中性程式庫具有您須了解的特殊特性。 假設您的程式庫提供使用檔案或呼叫非受控碼的 API 元素。 如果您的程式碼沒有對應的許可權，則不會如所述執行。 然而，即使程式碼擁有使用權限，呼叫它的任何應用程式程式碼也必須要有相同的使用權限才能運作。 如果呼叫程式碼沒有正確的許可權，則 <xref:System.Security.SecurityException> 會顯示為代碼啟用安全性堆疊逐步解說的結果。

## <a name="application-code-that-isnt-a-reusable-component"></a>不是可重複使用元件的應用程式代碼

如果您的程式碼是不會被其他程式碼呼叫之應用程式的一部分，安全性就很簡單，而且可能不需要特殊的編碼。 不過請記住，惡意程式碼可以呼叫您的程式碼。 雖然程式碼存取安全性可以制止惡意程式碼存取資源，這類的程式碼還是可以讀取可能含有敏感資訊的欄位或屬性的值。

此外，如果您的程式碼接受網際網路或其他不可靠來源的使用者輸入，您也必須小心惡意輸入。

## <a name="managed-wrapper-to-native-code-implementation"></a>原生程式碼執行的 Managed 包裝函式

在這個案例中，通常某些有用的功能是在您想提供給 Managed 程式碼的機器碼中所實作。 使用平台叫用或 COM Interop 就可輕鬆撰寫 Managed 包裝函式。 但是，如果您這麼做，包裝函式的呼叫端就必須具有 Unmanaged 程式碼的權限才會成功。 在 [預設原則] 底下，這表示從內部網路或網際網路下載的程式碼不會與包裝函式一起使用。

除了將非受控程式碼許可權提供給使用這些包裝函式的所有應用程式，最好只將這些許可權授與包裝函式程式碼。 如果基礎功能未公開任何資源而且實作也一樣安全，包裝函式就只需要判斷它的權限，讓任何程式碼都可以透過它來呼叫。 當牽涉到資源時，安全性程式碼撰寫應該與下一章節說明的程式庫程式碼的狀況相同。 由於包裝函式對這些資源而言是可能公開的呼叫端，因此小心驗證機器碼安全性的程序是必要的，而且這個程序必須由包裝函式負責執行。

## <a name="library-code-that-exposes-protected-resources"></a>公開受保護資源的程式庫程式碼

下列方法最強大，因此可能會有危險 (如果不正確地進行安全性編碼) ：您的程式庫可作為介面，讓其他程式碼存取某些無法使用的特定資源，就像 .NET 類別會強制執行所用資源的許可權一樣。 不論您在何處公開資源，您的程式都必須先要求適用於資源的使用權限 (亦即它必須執行安全性檢查)，然後再判斷它的權限，以執行實際的作業。

## <a name="see-also"></a>另請參閱

- [設定狀態資料的安全性](securing-state-data.md)
- [安全性和使用者輸入](security-and-user-input.md)
- [安全性和競爭情形](security-and-race-conditions.md)
- [安全性和產生作業中的程式碼](security-and-on-the-fly-code-generation.md)
- [以角色為基礎的安全性](role-based-security.md)
- [ASP.NET Core 安全性](/aspnet/core/security/)
