---
title: 全域組件快取
description: 瞭解全域組件快取，這是安裝 .NET 通用語言執行時間的電腦程式代碼快取。
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache)
- ACLs [.NET Framework]
- global assembly cache
- cache [.NET Framework], global assembly cache
- global assembly cache, about
- access control lists [.NET Framework]
ms.assetid: cf5eacd0-d3ec-4879-b6da-5fd5e4372202
ms.openlocfilehash: 7f08bb4cf279924b12432f259dae8ce5a8474285
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104905"
---
# <a name="global-assembly-cache"></a>全域組件快取
每部安裝通用語言執行平台的電腦都有稱為「全域組件快取」的全電腦程式碼快取。 全域組件快取會儲存特別指定為由電腦上數個應用程式共用的組件。  
  
 您應該只有在需要時才將組件安裝到全域組件快取，來共用組件。 一般來說，除非明確需要共用組件，否則會將組件相依性保留為私用，並且在應用程式目錄中尋找組件。 此外，不需要將組件安裝到全域組件快取，它們即可供 COM Interop 或非受控碼使用。  
  
> [!NOTE]
> 有些情況下您明確不想將組件安裝到全域組件快取。 如果您將構成應用程式的其中一個組件放入全域組件快取中，則可以使用 **xcopy** 命令複製應用程式目錄，以不再複寫或安裝應用程式。 您也必須在全域組件快取中移動組件。  
  
 將組件部署到全域組件快取的方式有兩種：  
  
- 使用設計來使用全域組件快取的安裝程式。 這是將組件安裝到全域組件快取慣用的選項。  
  
- 使用稱為[全域組件快取工具 (Gacutil.exe)](../tools/gacutil-exe-gac-tool.md) 的開發人員工具，它是由 Windows SDK 所提供。  
  
    > [!NOTE]
    > 在部署案例中，請使用 Windows Installer 將組件安裝到全域組件快取中。 您應該只在開發案例中使用全域組件快取工具，因為它不提供組件參考計數和在使用 Windows 安裝程式時提供的其他功能。  
  
 從 .NET Framework 4 開始，全域組件快取的預設位置為 **%windir%\Microsoft.NET\assembly**。 在舊版 .NET Framework 中，預設位置為 **%windir%\assembly**。  
  
 系統管理員通常會使用存取控制清單 (ACL) 來控制寫入和執行存取權，以便保護 systemroot 目錄。 因為全域組件快取安裝在 Systemroot 目錄的子目錄中，所以它會繼承該目錄的 ACL。 建議只有具備系統管理員權限的使用者才能從全域組件快取刪除檔案。  
  
 全域組件快取中部署的組件都必須具有強式名稱。 將組件新增至全域組件快取時，會對構成組件的所有檔案執行完整性檢查。 快取執行這些完整性檢查，以確保組件並未遭到破壞，比方說，當檔案已經變更，但資訊清單不會反映變更。  
  
## <a name="see-also"></a>另請參閱

- [.NET 中的組件](../../standard/assembly/index.md)
- [使用組件和全域組件快取](working-with-assemblies-and-the-gac.md)
- [強式名稱的元件](../../standard/assembly/strong-named.md)
