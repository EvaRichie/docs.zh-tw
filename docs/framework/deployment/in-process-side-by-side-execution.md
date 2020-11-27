---
title: 同處理序並存執行
description: 使用同進程並存裝載，在單一 .NET 進程中執行多個版本的 common language runtime (CLR) 。
ms.date: 03/30/2017
helpviewer_keywords:
- in-process side-by-side execution
- side-by-side execution, in-process
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
ms.openlocfilehash: 85d0ec90a8877384517e9de3b56258d294e0c612
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283480"
---
# <a name="in-process-side-by-side-execution"></a>同處理序並存執行

從 .NET Framework 4 開始，您可以使用同處理序並存裝載，在單一處理序中執行多個 Common Language Runtime (CLR) 版本。 根據預設，Managed COM 元件會與建置它們的 .NET Framework 版本一起執行，不論針對程序所載入的 .NET Framework 版本為何。  
  
## <a name="background"></a>背景  

 .NET Framework 一律會提供受控碼應用程式的並存裝載，但在 .NET Framework 4 之前，並未針對受控 COM 元件提供該功能。 過去，載入至程序的 Managed COM 元件是與已載入的執行階段版本或 .NET Framework 的最新已安裝版本一起執行。 如果此版本與 COM 元件不相容，元件就會失敗。  
  
 .NET Framework 4 提供新的方式進行並存裝載，以確保下列各項：  
  
- 安裝新版的 .NET Framework 不會影響現有應用程式。  
  
- 應用程式會針對用來建置的 .NET Framework 版本執行。 除非明確指示，否則它們不會使用新版 .NET Framework。 不過，應用程式較容易轉換成使用新版 .NET Framework。  
  
## <a name="effects-on-users-and-developers"></a>使用者和開發人員的影響  
  
- **一般使用者和系統管理員**. 這些使用者現在可以更有信心，在單獨或與應用程式一起安裝新版執行階段時，不會對其電腦造成任何影響。 現有應用程式會繼續與之前一樣地執行。  
  
- **應用程式開發人員**。 並存裝載幾乎不會影響應用程式開發人員。 根據預設，應用程式一律會針對用來建置的 .NET Framework 版本執行；這並未變更。 不過，開發人員可以覆寫這個行為，並指示應用程式在較新版的 .NET Framework 下執行 (請參閱[情節 2](#scenarios))。  
  
- **程式庫開發人員和取用者**。 並存裝載無法解決程式庫開發人員所面對的相容性問題。 應用程式直接透過直接參考或 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 呼叫所載入的程式庫，會持續使用載入它之 <xref:System.AppDomain> 的執行階段。 您應該針對您想要支援的所有 .NET Framework 版本測試程式庫。 如果使用 .NET Framework 4 執行階段來編譯應用程式，但應用程式包括使用舊版執行階段所建置的程式庫，則該程式庫也會使用 .NET Framework 4 執行階段。 不過，如果您的應用程式是使用舊版執行階段所建置，且程式庫是使用 .NET Framework 4 所建置，則您必須強制應用程式使用 .NET Framework 4 (請參閱[情節 3](#scenarios))。  
  
- **Managed COM 元件開發人員**。 過去，會使用電腦上所安裝的最新執行階段版本來自動執行 Managed COM 元件。 您現在可以針對建置它們的執行階段版本執行 COM 元件。  
  
     如下表所示，使用 .NET Framework 1.1 版所建置的元件可以與第 4 版元件並存執行，但它們無法與 2.0、3.0 或 3.5 版元件一起執行，因為這些版本無法使用並存裝載。  
  
    |.NET Framework 版本|1.1|2.0 - 3.5|4|  
    |----------------------------|---------|----------------|-------|  
    |1.1|不適用|否|是|  
    |2.0 - 3.5|否|不適用|是|  
    |4|是|是|不適用|  
  
> [!NOTE]
> .NET Framework 3.0 和 3.5 版是根據 2.0 版透過累加方式所建置，不需要並存執行。 這些本質上是相同的版本。  
  
<a name="scenarios"></a>

## <a name="common-side-by-side-hosting-scenarios"></a>常見並存裝載案例  
  
- **情節 1：** 使用舊版 .NET Framework 所建置之 COM 元件的原生應用程式。  
  
     安裝的 .NET Framework 版本： .NET Framework 4 以及 COM 元件所使用的所有其他 .NET Framework 版本。  
  
     處理方式：在此情節中，不執行任何動作。 COM 元件會與註冊它們的 .NET Framework 版本一起執行。  
  
- **案例 2**：使用 .NET FRAMEWORK 2.0 SP1 建立的受控應用程式，您想要搭配 .NET Framework 2.0 執行，但願意在2.0 版不存在時，在 .NET Framework 4 上執行。  
  
     安裝的 .NET Framework 版本：舊版 .NET Framework 和 .NET Framework 4。  
  
     作法：在應用程式目錄的[應用程式佈建檔](../configure-apps/index.md)中，使用[ \<startup> 元素](../configure-apps/file-schema/startup/startup-element.md)和[ \<supportedRuntime> 元素](../configure-apps/file-schema/startup/supportedruntime-element.md)集，如下所示：  
  
    ```xml  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
- **案例3：** 原生應用程式，其使用以舊版 .NET Framework 所建立的 COM 元件，而您想要使用 .NET Framework 4 來執行這些元件。  
  
     安裝的 .NET Framework 版本： .NET Framework 4。  
  
     處理方式：在應用程式目錄的應用程式組態檔中，搭配使用 `<startup>` 項目與設為 `true` 的 `useLegacyV2RuntimeActivationPolicy` 屬性以及設定如下的 `<supportedRuntime>` 項目：  
  
    ```xml  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## <a name="example"></a>範例  

 下列範例示範執行 Managed COM 元件的 Unmanaged COM 主機，方法是使用編譯元件使用的 .NET Framework 版本。  
  
 若要執行下列範例，請編譯並註冊下列使用 .NET Framework 3.5 的受控 COM 元件。 若要註冊元件，請在 [專案] 功能表上按一下 [屬性]，再按一下 [組建] 索引標籤，然後選取 [註冊 COM Interop] 核取方塊。  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 編譯下列 Unmanaged C++ 應用程式，以啟用前一個範例所建立的 COM 物件。  
  
```cpp
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
```  
  
## <a name="see-also"></a>另請參閱

- [\<startup> 元素](../configure-apps/file-schema/startup/startup-element.md)
- [\<supportedRuntime> 元素](../configure-apps/file-schema/startup/supportedruntime-element.md)
