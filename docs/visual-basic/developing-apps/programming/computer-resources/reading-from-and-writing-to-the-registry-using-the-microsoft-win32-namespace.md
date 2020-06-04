---
title: 使用 Microsoft.Win32 命名空間讀取和寫入登錄
ms.date: 07/20/2015
helpviewer_keywords:
- registry [Visual Basic]
ms.assetid: 4a0dcce0-c27b-4199-baa8-ee4528da6a56
ms.openlocfilehash: 10431b1ad40ed320541a22fb46cc8db6dbb775b0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360068"
---
# <a name="reading-from-and-writing-to-the-registry-using-the-microsoftwin32-namespace-visual-basic"></a>使用 Microsoft.Win32 命名空間讀取和寫入登錄 (Visual Basic)

雖然 `My.Computer.Registry` 應該會涵蓋對登錄進行程式設計時的基本需求，但是您也可以使用 .NET Framework <xref:Microsoft.Win32> 命名空間中的 <xref:Microsoft.Win32.Registry> 和 <xref:Microsoft.Win32.RegistryKey> 類別。  
  
## <a name="keys-in-the-registry-class"></a>登錄類別中的機碼  

 <xref:Microsoft.Win32.Registry> 類別提供可用來存取子機碼和其值的基底登錄機碼。 基底機碼本身是唯讀的。 下表列出並描述 <xref:Microsoft.Win32.Registry> 類別所公開的七個機碼。  
  
|**關鍵**|**說明**|  
|-------------|---------------------|  
|<xref:Microsoft.Win32.Registry.ClassesRoot>|定義文件類型以及與這些類型相關聯的屬性。|  
|<xref:Microsoft.Win32.Registry.CurrentConfig>|包含非使用者特定的硬體組態資訊。|  
|<xref:Microsoft.Win32.Registry.CurrentUser>|包含目前使用者偏好設定的相關資訊 (例如環境變數)。|  
|<xref:Microsoft.Win32.Registry.DynData>|包含動態登錄資料 (例如虛擬裝置驅動程式所使用的動態登錄資料)。|  
|<xref:Microsoft.Win32.Registry.LocalMachine>|包含五個子機碼 (Hardware、SAM、Security、Software 和 System) 來保存本機電腦的組態資料。|  
|<xref:Microsoft.Win32.Registry.PerformanceData>|包含軟體元件的效能資訊。|  
|<xref:Microsoft.Win32.Registry.Users>|包含預設使用者偏好設定的相關資訊。|  
  
> [!IMPORTANT]
> 將資料寫入目前使用者 (<xref:Microsoft.Win32.Registry.CurrentUser>)，比寫入本機電腦 (<xref:Microsoft.Win32.Registry.LocalMachine>) 更為安全。 其他處理序 (可能為惡意) 先前已建立過您正在建立的機碼時，會發生一般稱為「佔用」的情況。 若要避免發生此問題，請使用 <xref:Microsoft.Win32.RegistryKey.GetValue%2A> 這類方法，以在還沒有索引鍵時傳回 `Nothing`。  
  
## <a name="reading-a-value-from-the-registry"></a>讀取登錄中的值  

 下列程式碼示範如何讀取 HKEY_CURRENT_USER 中的字串。  
  
 [!code-vb[VbResourceTasks#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#20)]  
  
 下列程式碼會依序讀取字串、遞增字串，以及將字串寫入 HKEY_CURRENT_USER。  
  
 [!code-vb[VbResourceTasks#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.SystemException>
- <xref:System.ApplicationException>
- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [Try...Catch...Finally 陳述式](../../../language-reference/statements/try-catch-finally-statement.md)
- [讀取和寫入登錄](reading-from-and-writing-to-the-registry.md)
- [安全性和登錄](security-and-the-registry.md)
