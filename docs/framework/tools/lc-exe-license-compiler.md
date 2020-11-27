---
title: Lc.exe (授權編譯器)
description: 使用 Lc.exe 授權編譯器。 此工具會讀取具有授權資訊的文字檔，並將二進位檔案內嵌在 CLR 可執行檔中做為資源。
ms.date: 03/30/2017
helpviewer_keywords:
- Lc.exe
- .licx file
- License Compiler
- control licenses [Windows Forms]
- compiling licenses file
- license file
- .licenses file
- Windows Forms, control licenses
- licensed controls [Windows Forms]
ms.assetid: 2de803b8-495e-4982-b209-19a72aba0460
ms.openlocfilehash: d1644ff4d69c857e36e87f7e83f668908b7ba021
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96275758"
---
# <a name="lcexe-license-compiler"></a>Lc.exe (授權編譯器)

授權編譯器可以讀取包含授權資訊的文字檔，並產生可內嵌於通用語言執行平台可執行檔的二進位檔案做為資源。  
  
 每當將授權控制項加入至表單時，Windows Form 設計工具便會自動產生或更新 .licx 文字檔。 專案系統會將 .licx 文字檔轉換為可支援 .NET 控制項授權的 .licenses 二進位資源，當做編譯的一部分。 接著此二進位資源將嵌入專案輸出。  
  
 使用授權編譯器建置您的專案時，不支援 32 位元與 64 位元之間的跨平台編譯。 這是因為授權編譯器必須載入組件，卻不允許從 32 位元應用程式載入 64 位元組件，反之亦然。 在這種情況下，請使用授權編譯器，以手動方式從命令列編譯授權，並指定對應的架構。  
  
 此工具會自動與 Visual Studio 一起安裝。 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。  
  
 在命令提示字元中，請輸入下列項目：  
  
## <a name="syntax"></a>Syntax  
  
```console
      lc /target:  
targetPE /complist:filename [-outdir:path]  
/i:modules [/nologo] [/v]  
```  
  
|選項|描述|  
|------------|-----------------|  
|**/complist: filename** |指定要包含在 .licenses 檔案中含有授權元件清單的檔案名稱。 使用元件的完整名稱與每行只有一個元件方式參考每個元件。<br /><br /> 命令列使用者可以為專案中的每個表單指定個別的檔案。 Lc.exe 接受多個輸入檔並產生單一 .licenses 檔案。|  
|**/h**[**elp**]|顯示工具的命令語法和選項。|  
|**/i: module** |指定包含列於 **/complist** 檔案中之元件的模組。 若要指定一個以上的模組，請使用多個 **/i** 旗標。|  
|**/nologo**|隱藏 Microsoft 程式啟始資訊顯示。|  
|**/outdir: path** |指定要放置輸出 .licenses 檔案的目錄。|  
|**/target: targetPE** |指定要產生 .licenses 檔案的可執行檔。|  
|**/v**|指定詳細資訊模式；顯示編譯程序資訊。|  
|**@***file* 檔案|指定回應檔 (.rsp)。|  
|**/?**|顯示工具的命令語法和選項。|  
  
## <a name="example"></a>範例  
  
1. 如果您要使用名為 `HostApp.exe` 之應用程式中 `Samples.DLL` 所包含的授權控制項 `MyCompany.Samples.LicControl1`，可以建立包含下列程式碼的 `HostAppLic.txt`。  
  
    ```text
    MyCompany.Samples.LicControl1, Samples.DLL  
    ```  
  
2. 使用下列命令建立這個稱為 `HostApp.exe.licenses` 的 .licenses 檔案。  
  
    ```console  
    lc /target:HostApp.exe /complist:hostapplic.txt /i:Samples.DLL /outdir:c:\bindir  
    ```  
  
3. 建置包含 .licenses 檔案當做資源的 `HostApp.exe`。 如果您正在建置 C# 應用程式，可以使用下列命令來建置應用程式。  
  
    ```console
    csc /res:HostApp.exe.licenses /out:HostApp.exe *.cs  
    ```  
  
 下列命令會從由 `myApp.licenses`、`hostapplic.txt` 和 `hostapplic2.txt` 所指定的授權元件清單編譯 `hostapplic3.txt`。 `modulesList` 引數是指定包含授權元件的模組。  
  
```console  
lc /target:myApp /complist:hostapplic.txt /complist:hostapplic2.txt /complist: hostapplic3.txt /i:modulesList  
```  
  
## <a name="response-file-example"></a>回應檔範例  

 下列清單顯示回應檔 `response.rsp` 的範例。 如需回應檔的詳細資訊，請參閱[回應檔](/visualstudio/msbuild/msbuild-response-files)。  
  
```text  
/target:hostapp.exe  
/complist:hostapplic.txt
/i:WFCPrj.dll
/outdir:"C:\My Folder"  
```  
  
 下列命令列使用 `response.rsp` 檔。  
  
```console  
lc @response.rsp  
```  
  
## <a name="see-also"></a>另請參閱

- [工具](index.md)
- [Al.exe (元件連結器) ](al-exe-assembly-linker.md)
- [命令提示字元](developer-command-prompt-for-vs.md)
