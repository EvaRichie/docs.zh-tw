---
title: 呼叫端資訊
ms.date: 07/20/2015
ms.assetid: 15d556eb-4d0c-4497-98a3-7f60abb7d6a1
ms.openlocfilehash: 33c7367626d66d1db2705fc2882ca0780d1b867f
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91090348"
---
# <a name="caller-information-visual-basic"></a>呼叫端資訊 (Visual Basic)

使用 Caller Info 屬性，您就可以取得有關方法之呼叫端的資訊。 您可以取得原始程式碼的檔案路徑、原始程式碼中的行號，以及呼叫端的成員名稱。 這項資訊有助於追蹤、偵錯及建立診斷工具。  
  
 若要取得這項資訊，可使用套用至選擇性參數的屬性，每個屬性都有預設值。 下表列出 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 命名空間中定義的 Caller Info 屬性：  
  
|屬性|描述|類型|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|包含呼叫端的原始程式檔完整路徑。 這是編譯時間的檔案路徑。|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|原始程式檔中呼叫方法所在的行號。|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|呼叫端的方法或屬性名稱。 請參閱本主題稍後的[成員名稱](#MEMBERNAMES)。|`String`|  
  
## <a name="example"></a>範例  

 下列範例將示範如何使用 Caller Info 屬性。 每次呼叫 `TraceMessage` 方法時，呼叫端資訊會替代做為選擇性參數的引數。  
  
```vb  
Private Sub DoProcessing()  
    TraceMessage("Something happened.")  
End Sub  
  
Public Sub TraceMessage(message As String,  
        <System.Runtime.CompilerServices.CallerMemberName> Optional memberName As String = Nothing,  
        <System.Runtime.CompilerServices.CallerFilePath> Optional sourcefilePath As String = Nothing,  
        <System.Runtime.CompilerServices.CallerLineNumber()> Optional sourceLineNumber As Integer = 0)  
  
    System.Diagnostics.Trace.WriteLine("message: " & message)  
    System.Diagnostics.Trace.WriteLine("member name: " & memberName)  
    System.Diagnostics.Trace.WriteLine("source file path: " & sourcefilePath)  
    System.Diagnostics.Trace.WriteLine("source line number: " & sourceLineNumber)  
End Sub  
  
' Sample output:  
'   message: Something happened.  
'   member name: DoProcessing  
'   source file path: C:\Users\username\Documents\Visual Studio 2012\Projects\CallerInfoVB\CallerInfoVB\Form1.vb  
'   source line number: 15  
```  
  
## <a name="remarks"></a>備註  

 您必須為每個選擇性參數指定明確的預設值。 您無法將 Caller Info 屬性套用至未指定為選擇性的參數。  
  
 Caller Info 屬性不會讓參數成為選擇性， 而是會影響省略引數時傳入的預設值。  
  
 在編譯時期，Caller Info 的值會做為常值發出至中繼語言 (IL)。 結果不受模糊化所影響，與 <xref:System.Exception.StackTrace%2A> 屬性中例外狀況的結果不同。  
  
 您可以明確提供選擇性引數來控制呼叫端資訊，或是隱藏呼叫端資訊。  
  
### <a name="member-names"></a><a name="MEMBERNAMES"></a> 成員名稱  

 您可以使用 `CallerMemberName` 屬性避免指定成員名稱做為所呼叫方法的 `String` 引數。 利用這個技巧就可以避免發生 [重新命名重構]**** 未變更 `String` 值這個問題。 這項優點對於下列工作特別有用：  
  
- 使用追蹤和診斷常式。  
  
- 當繫結資料時，實作 <xref:System.ComponentModel.INotifyPropertyChanged> 介面。 這個介面可讓物件的屬性告知繫結的控制項屬性已變更，所以控制項可以顯示更新的資訊。 沒有 `CallerMemberName` 屬性 (Attribute)，您就必須指定屬性 (Property) 名稱做為常值。  
  
 下圖顯示當您使用 `CallerMemberName` 屬性時，傳回的成員名稱。  
  
|呼叫發生於|成員名稱結果|  
|-------------------------|------------------------|  
|方法、屬性或事件|產生呼叫的方法、屬性或事件的名稱。|  
|建構函式|字串 ".ctor"|  
|靜態建構函式|字串 ".cctor"|  
|解構函式|字串 "Finalize"|  
|使用者定義的運算子或轉換|產生的成員名稱，例如 "op_Addition"。|  
|屬性建構函式|套用屬性的成員名稱。 如果屬性為成員內的任何項目 (例如參數、傳回值或泛型類型參數)，這個結果會是與該項目相關聯的成員名稱。|  
|無包含的成員 (例如，組件層級或套用至類型的屬性)。|選擇性參數的預設值。|  
  
## <a name="see-also"></a>另請參閱

- [屬性 (Visual Basic)](../../language-reference/attributes.md)
- [通用屬性 (Visual Basic)](attributes/common-attributes.md)
- [選擇性參數](../language-features/procedures/optional-parameters.md)
- [程式設計概念 (Visual Basic)](index.md)
