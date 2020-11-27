---
title: Storeadm.exe (隔離儲存區工具)
description: 瞭解 Storeadm.exe 的隔離儲存區工具。 此工具會列出或移除目前使用者的所有現有存放區。
ms.date: 03/30/2017
helpviewer_keywords:
- Storeadm.exe
- listing stores for current user
- Isolated Storage tool
- stores, current user
- removing stores
ms.assetid: b81202b8-d91d-4b23-9c53-4a112f74a44a
ms.openlocfilehash: 974f3c464ff686a486657d08e77c97299cc94732
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283831"
---
# <a name="storeadmexe-isolated-storage-tool"></a>Storeadm.exe (隔離儲存區工具)

隔離儲存區 (Isolated Storage) 工具可以列出或移除目前使用者的所有現有存放區。  
  
 此工具會自動與 Visual Studio 一起安裝。 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。  
  
 在命令提示字元中，請輸入下列項目：  
  
## <a name="syntax"></a>語法  
  
```console  
storeadm [/list][/machine][/remove][/roaming][/quiet]  
```  
  
## <a name="parameters"></a>參數  
  
|選項|描述|  
|------------|-----------------|  
|**/h**[**elp**]|顯示工具的命令語法和選項。|  
|**/list**|顯示目前使用者的所有現有存放區。 包括這個使用者所執行的所有應用程式或組件的存放區。|  
|**/machine**|選取電腦存放區。 使用這個選項搭配 **/list** 或 **/remove** 選項，可指定動作應該套用至電腦存放區。<br /><br /> .NET Framework 2.0 的新功能|  
|**/quiet**|指定無訊息模式，隱藏資訊輸出，以便僅顯示錯誤訊息。|  
|**/remove**|永久移除目前使用者的所有現有存放區。|  
|**/roaming**|選取漫遊存放區。 使用這個選項搭配 **/list** 或 **/remove** 選項，可指定動作應該套用至漫遊存放區。|  
|**/?**|顯示工具的命令語法和選項。|  
  
## <a name="remarks"></a>備註  

 從命令列執行 Storeadm.exe 而沒有指定任何選項時，會顯示工具的語法和選項。  
  
 **/list** 和 **/remove** 選項通常不會同時使用；不過，如果指定了兩個以上的選項，則會依照出現在命令列上的順序執行這些選項。  
  
 應用程式可以選擇儲存至使用者的兩個存放區之一，或是儲存至電腦存放區：  
  
- 本機存放區位於保證不漫遊的位置 (在 Windows 2000 (含) 以後版本上)，即使已啟用該使用者的使用者資料漫遊也一樣。  
  
- 漫遊存放區位於能夠漫遊的位置，不過必須先透過 Windows NT 系統管理啟用使用者的漫遊功能才能進行漫遊。  
  
- 電腦存放區為電腦上所有使用者通用，並且存放在該電腦的通用目錄下。  
  
    > [!NOTE]
    > 電腦存放區是 .NET Framework 2.0 版中的新功能。  
  
 使用者的漫遊實際上是否啟用，並不會影響 Storeadm.exe 的系統管理。 執行該工具而沒有使用任何選項時，會將所有動作套用至本機存放區。 執行該工具搭配 **/roaming** 選項時，會將所有動作套用至能夠漫遊的存放區。 執行該工具搭配 **/machine** 選項時，會將所有動作套用至電腦存放區。  
  
## <a name="see-also"></a>另請參閱

- [工具](index.md)
- [隔離儲存區](../../standard/io/isolated-storage.md)
- [命令提示字元](developer-command-prompt-for-vs.md)
