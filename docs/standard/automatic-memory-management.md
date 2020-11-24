---
title: Automatic Memory Management
ms.date: 03/30/2017
helpviewer_keywords:
- garbage collection, automatic memory management
- memory, allocating
- memory, automatic memory management
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- managed heap
- runtime, automatic memory management
ms.assetid: d4850de5-fa63-4936-a250-5678d118acba
ms.openlocfilehash: a38a95073759fa95d19a2baf4add191103f9264a
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95682012"
---
# <a name="automatic-memory-management"></a>Automatic Memory Management

自動記憶體管理是 Common Language Runtime 在 [Managed 執行](managed-execution-process.md)期間所提供的其中一項服務。 Common Language Runtime 的記憶體回收行程會管理應用程式記憶體的配置和釋放。 這表示開發人員在開發 Managed 應用程式時，不需要撰寫程式碼來執行記憶體管理工作。 自動記憶體管理可排除一些常見的問題，例如，忘記釋放物件而造成記憶體流失 (Memory Leak)，或嘗試存取已經釋放物件的記憶體。 本章節將描述記憶體回收行程如何配置和釋放記憶體。  
  
## <a name="allocating-memory"></a>配置記憶體  

 當您初始化新的處理序 (Process) 時，Runtime 會保留一塊連續的位址空間區域，供處理序使用。 這塊保留的位址空間稱為 Managed 堆積 (Heap)。 Managed 堆積會保留即將配置給堆積中下一個物件的位址指標。 剛開始會將這個指標設定為 Managed 堆積的基底位址 (Base Address)。 所有[參考類型](base-types/common-type-system.md)都是在 Managed 堆積上進行配置。 當應用程式建立第一個參考型別時，會為該型別配置 Managed 堆積基底位址的記憶體。 當應用程式建立第二個物件時，記憶體回收行程會為它配置緊接在第一個物件後面位址空間的記憶體。 只要有可供使用的位址空間，記憶體回收行程就會繼續用這種方式為新的物件配置空間。  
  
 從 Managed 堆積中配置記憶體要比 Unmanaged 記憶體配置快。 由於 Runtime 是用增加指標值的方式為物件配置記憶體，因此速度幾乎和從堆疊中配置記憶體一樣快。 此外，由於連續配置的新物件是連續儲存在 Managed 堆積中，因此應用程式可以非常快速地存取這些物件。  
  
<a name="cpconautomaticmemorymanagementreleasingmemoryanchor1"></a>

## <a name="releasing-memory"></a>釋放記憶體  

 記憶體回收行程的最佳化引擎會根據所做的配置，決定執行回收的最佳時機。 當記憶體回收行程執行回收時，會將應用程式已經不再使用的物件記憶體釋放出來。 它會檢查應用程式的根目錄 (Root)，判斷哪些物件已不再使用。 每一個應用程式都有一組根目錄。 每一個根目錄都會參考 Managed 堆積上的物件，要不然就是設定為 Null。 應用程式的根目錄包括執行緒堆疊上的靜態欄位、區域變數和參數，以及 CPU 暫存器。 記憶體回收行程可以存取 [Just-in-Time (JIT) 編譯器](managed-execution-process.md)和執行階段所保留的使用中根目錄清單。 它會用這份清單來檢查應用程式的根目錄，然後在處理序中建立圖形，其中包含可從根目錄取得的所有物件。  
  
 不在圖形中的物件就無法從應用程式的根目錄取得。 記憶體回收行程會考慮無法取得的物件項目，然後將配置給它們的記憶體釋放出來。 在回收期間，記憶體回收行程會檢查 Managed 堆積，尋找無法取得的物件所佔用的位址空間區塊。 每找到一個無法取得的物件時，它便會使用記憶體複製功能，壓縮記憶體中可取得的物件，然後釋放出為無法取得的物件所配置的位址空間區塊。 一旦壓縮完可取得物件的記憶體之後，記憶體回收行程會進行必要的指標更正，使應用程式的根目錄指向新位置中的物件。 它也會將 Managed 堆積的指標放在最後取得物件的後面。 請注意，只有當回收找到相當數量無法取得的物件時，才會壓縮記憶體。 如果 Managed 堆積中的所有物件在回收之後都存留下來，就不需要壓縮記憶體。  
  
 為了改善效能，Runtime 會為大型物件配置不同堆積中的記憶體。 記憶體回收行程會自動釋放大型物件的記憶體。 但是，為了避免移動記憶體中的大型物件，因此不會壓縮記憶體。  
  
## <a name="generations-and-performance"></a>層代和效能  

 為了要最佳化記憶體回收行程的效能，Managed 堆積分成三個層代 (Generation)：0、1 和 2。 執行階段的記憶體回收演算法，是根據電腦軟體產業利用實驗記憶體回收配置所發現的數個通用原理。 首先，壓縮部分 Managed 堆積的記憶體比壓縮整個 Managed 堆積要快。 其次，較新物件的存留期 (Lifetime) 較短，較舊物件的存留期較長。 最後，較新的物件通常都會彼此相關，而且應用程式也會同時存取。  
  
 執行階段的記憶體回收行程會將新的物件儲存在第 0 個層代。 在應用程式存留期初期建立的物件則會升階並儲存在第 1 個和第 2 個層代。 物件提升的程序會在這個主題稍後加以說明。 由於壓縮部分 Managed 堆積比壓縮整個堆積要快，因此這種配置允許記憶體回收行程釋放指定層代的記憶體，而不是在每次執行回收時釋放整個 Managed 堆積的記憶體。  
  
 事實上，當第 0 個層代已滿時，記憶體回收行程便會執行回收。 當第 0 個層代已滿時，如果應用程式嘗試建立新的物件，記憶體回收行程會發現第 0 個層代中已經沒有剩餘的位址空間可配置給物件。 這時記憶體回收行程便會執行回收，嘗試為該物件釋放出第 0 個層代的位址空間。 記憶體回收行程是從檢查第 0 個層代中的物件開始，而不是檢查 Managed 堆積中的所有物件。 這是最有效率的方式，因為新物件的存留期通常較短，因此在執行回收時，通常會認為應用程式已不再使用第 0 個層代中的許多物件。 此外，單獨回收第 0 個層代通常就能收回足夠的記憶體，讓應用程式繼續建立新的物件。  
  
 在記憶體回收行程執行層代 0 的回收之後，會壓縮可執行物件的記憶體，如同本主題中前面的[釋放記憶體](#cpconautomaticmemorymanagementreleasingmemoryanchor1)中的說明。 然後，記憶體回收行程會提升這些物件，並考慮 Managed 堆積第 1 個層代的這個部分。 由於回收之後存留下來的物件通常具有較長的存留期，因此才會將它們提升至較高的層代。 如此一來，每當記憶體回收行程執行第 0 個層代的回收時，就不需要再重新檢查第 1 和第 2 個層代中的物件了。  
  
 在記憶體回收行程執行第 0 個層代的第一次回收，並將可取得的物件提升至第 1 個層代之後，它會考慮 Managed 堆積第 0 個層代的其他部分。 接著會繼續為新的物件配置第 0 個層代中的記憶體，直到第 0 個層代已滿而必須再執行另一次回收為止。 這時候，記憶體回收行程的最佳化引擎會判斷是否需要檢查較舊層代中的物件。 例如，如果第 0 個層代的回收沒有收回足夠的空間讓應用程式成功建立完新的物件，記憶體回收行程可以執行第 1 個層代的回收，然後再執行第 2 個層代的回收。 如果仍然沒有收回足夠的記憶體，記憶體回收行程可以再依序執行第 2、第 1 和第 0 個層代的回收。 在每一次回收之後，記憶體回收行程都會壓縮第 0 個層代中可取得的物件，並將其提升至第 1 個層代。 在回收之後存留下來的第 1 個層代物件則會提升至第 2 個層代。 由於記憶體回收行程只支援三個層代，因此回收之後存留下來的第 2 個層代物件仍然會留在第 2 個層代中，直到未來回收時判斷它們無法取得為止。  
  
## <a name="releasing-memory-for-unmanaged-resources"></a>釋放 Unmanaged 資源的記憶體  

 對於應用程式所建立的大部分物件而言，您都可以依賴記憶體回收行程自動執行必要的記憶體管理工作。 但是，Unmanaged 資源需要明確清除。 最常見的 Unmanaged 資源類型就是包裝作業系統資源 (例如檔案控制代碼、視窗控制代碼或網路連接) 的物件。 雖然記憶體回收行程能夠追蹤封裝 Unmanaged 資源的 Managed 物件存留期，但是它並沒有關於如何清除資源的相關資訊。 當建立封裝 Unmanaged 資源的物件時，建議您提供必要的程式碼，在公用 **Dispose** 方法中清除 Unmanaged 資源。 您可以提供 **Dispose** 方法，讓物件的使用者在用完物件後，明確釋放出它所佔用的記憶體。 當您使用封裝 Unmanaged 資源的物件時，應留意 **Dispose** 的用法，並在必要時加以呼叫。 如需清除 Unmanaged 資源的詳細資訊，以及實作 **Dispose** 的設計模式範例，請參閱 [記憶體回收](garbage-collection/index.md)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.GC>
- [記憶體回收](garbage-collection/index.md)
- [Managed 執行進程](managed-execution-process.md)
