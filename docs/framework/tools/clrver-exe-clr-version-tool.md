---
title: Clrver.exe (CLR 版本工具)
description: 請參閱 CLR 版本工具 Clrver.exe。 此工具會報告電腦上所有已安裝的 common language runtime （CLR）版本。
ms.date: 03/30/2017
helpviewer_keywords:
- Clrver.exe
- CLR Version tool
ms.assetid: cbc2ee86-bdc8-4a65-a8f1-ba23bce3a699
ms.openlocfilehash: e914034819418df00438c454e209e6c86779ba3c
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87167284"
---
# <a name="clrverexe-clr-version-tool"></a>Clrver.exe (CLR 版本工具)
CLR 版本工具 (Clrver.exe) 會報告電腦上已安裝的所有通用語言執行平台 (CLR) 版本。  
  
 此工具會自動與 Visual Studio 一起安裝。 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。  
  
 在命令提示字元中，請輸入下列項目：  
  
## <a name="syntax"></a>語法  
  
```console  
clrver [option]  
```  
  
## <a name="options"></a>選項。  
  
|選項|描述|  
|------------|-----------------|  
|`-all`|顯示電腦上所有正在使用 CLR 的處理序。|  
|*p&id*|顯示具有指定處理序 ID (PID) 的處理序所使用的 CLR 版本。|  
|`-?`|顯示工具的命令語法和選項。|  
  
## <a name="remarks"></a>備註  
 如果您呼叫 Clrver.exe 時未使用任何選項，則會顯示所有已安裝的 CLR 版本。 如果您指定另一個使用者的 PID，則必須具有系統管理權限才能取得版本資訊。  
  
> [!NOTE]
> 在 Windows Vista (含) 以後版本中，使用者帳戶控制 (UAC) 會判斷使用者的權限。 如果您是內建 Administrators 群組的成員，系統會將兩個執行階段存取語彙基元 (Token) 指派給您：標準使用者存取語彙基元及管理員存取語彙基元。 根據預設，您會屬於標準使用者角色。 若要執行需要系統管理權限的程式碼，您必須先將權限從標準使用者提高為系統管理員。 您可以在啟動命令提示字元時以滑鼠右鍵按一下命令提示字元圖示，並表示您要以系統管理員身分執行，藉此提高為系統管理員權限。  
  
 若您嘗試判斷 SYSTEM、LOCAL SERVICE 和 NETWORK SERVICE 處理序的 CLR 版本，系統會顯示一則訊息，表示 PID 不存在。  
  
## <a name="examples"></a>範例  
 下列命令會顯示電腦上安裝的所有 CLR 版本。  
  
 `clrver`  
  
 下列命令會顯示處理序 128 所使用的 CLR 版本。  
  
 `clrver 128`  
  
 下列命令會顯示所有 Managed 處理序及其使用的 CLR 版本。  
  
 `Clrver -all`  
  
## <a name="see-also"></a>另請參閱

- [工具](index.md)
- [命令提示字元](developer-command-prompt-for-vs.md)
