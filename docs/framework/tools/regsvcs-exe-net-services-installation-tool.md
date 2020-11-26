---
title: Regsvcs.exe (.NET 服務安裝工具)
description: 使用 Regsvcs.exe （.NET 服務安裝工具）。 載入並註冊元件、設定您以程式設計方式新增至類別的服務等等。
ms.date: 03/30/2017
helpviewer_keywords:
- Regsvcs.exe
- .NET Services Installation tool
- loading assemblies
- assemblies [.NET Framework], registering
- type libraries
- registering assemblies
ms.assetid: 5220fe58-5aaf-4e8e-8bc3-b78c63025804
ms.openlocfilehash: 58a20084457cb217f3af73f4b4ff9ea251647782
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96238544"
---
# <a name="regsvcsexe-net-services-installation-tool"></a>Regsvcs.exe (.NET 服務安裝工具)

.NET 服務安裝工具會執行下列動作：  
  
- 載入和註冊組件。  
  
- 產生、註冊和安裝類型程式庫到指定的 COM+ 應用程式。  
  
- 設定您以程式設計方式加入至類別的服務。  
  
 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。  
  
 在命令提示字元中，請輸入下列項目：  
  
## <a name="syntax"></a>語法  
  
```console  
      regsvcs [/c | /fc | /u] [/tlb:typeLibraryFile] [/extlb]  
[/reconfig] [/componly] [/appname:applicationName]  
[/nologo] [/quiet]assemblyFile.dll
```  
  
## <a name="parameters"></a>參數  
  
|引數|描述|  
|--------------|-----------------|  
|*assemblyFile.dll*|來源組件檔。 這個組件必須以強式名稱簽署。 如需詳細資訊，請參閱[以強式名稱簽署組件](../../standard/assembly/sign-strong-name.md)。|  
  
|選項|描述|  
|------------|-----------------|  
|**/appdir:<路徑>** |指定應用程式的根目錄。|  
|**/appname:<應用程式名稱>** |指定要尋找或建立之 COM+ 應用程式的名稱。|  
|**/c**|建立目標應用程式。|  
|**/componly**|只設定元件，忽略方法和介面。|  
|**/exapp**|指定需要現有應用程式的工具。|  
|**/extlb**|使用現有的類型程式庫。|  
|**/fc**|尋找或建立目標應用程式。|  
|**/help**|顯示工具的命令語法和選項。|  
|**/noreconfig**|不要重新設定現有的目標應用程式。|  
|**/nologo**|隱藏 Microsoft 程式啟始資訊顯示。|  
|**/parname:** *name*|指定要尋找或建立之 COM+ 應用程式的名稱或 ID。|  
|**/reconfig**|重新設定現有的目標應用程式。 此為預設值。|  
|**/tlb:<型別程式庫檔案>** |指定要安裝的類型程式庫檔案。|  
|**u**|解除安裝目標應用程式。|  
|**/quiet**|指定安靜模式，隱藏標誌或成功訊息顯示。|  
|**/?**|顯示工具的命令語法和選項。|  
  
## <a name="remarks"></a>備註  

 Regsvcs.exe 需要由 *assemblyFile.dll* 所指定的來源組件檔。 這個組件必須使用強式名稱簽署。 如需強式名稱簽署的詳細資訊，請參閱[以強式名稱簽署組件](../../standard/assembly/sign-strong-name.md)。 目標應用程式和類型程式庫檔案的名稱是選擇項。 如果 *applicationName* 引數已經不存在，則可以從來源組件檔中產生，並且將會由 Regsvcs.exe 建立。 *typelibraryfile* 引數可以指定型別程式庫名稱。 如果您沒有指定類型程式庫名稱，Regsvcs.exe 會使用組件名稱做為預設值。  
  
 當 Regsvcs.exe 註冊元件的方法時，它會受制於這些方法上的[要求](/previous-versions/dotnet/netframework-4.0/9kc0c6st(v=vs.100))和[連結要求](../misc/link-demands.md)。 因為這個工具是在完全信任的環境中執行，所以大部分的使用權限需求都會成功。 不過，Regsvcs.exe 無法註冊方法受到 <xref:System.Security.Permissions.StrongNameIdentityPermission> 或 <xref:System.Security.Permissions.PublisherIdentityPermission> 的需求或連結要求保護的元件。  
  
 您必須擁有本機電腦上的系統管理員權限，才能使用 Regsvcs.exe。  
  
 在執行任何這些動作時，如果 Regsvcs.exe 失敗，會顯示對應的錯誤訊息。  
  
## <a name="examples"></a>範例  

 下列命令會將 `myTest.dll` 中包含的所有公用類別加入 `myTargetApp` (現有的 COM+ 應用程式)，並產生 `myTest.tlb` 類型程式庫。  
  
```console  
regsvcs /appname:myTargetApp myTest.dll  
```  
  
 下列命令會將 `myTest.dll` 中包含的所有公用類別加入 `myTargetApp` (現有的 COM+ 應用程式)，並產生 `newTest.tlb` 類型程式庫。  
  
```console  
regsvcs /appname:myTargetApp /tlb:newTest.tlb myTest.dll  
```  
  
## <a name="see-also"></a>另請參閱

- [工具](index.md)
- [如何：使用強式名稱簽署組件](../../standard/assembly/sign-strong-name.md)
- [命令提示字元](developer-command-prompt-for-vs.md)
