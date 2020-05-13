---
title: 如何：判斷檔案是否為元件
description: 本文說明如何以手動和程式設計方式判斷檔案是否為 .NET 元件。
ms.date: 08/19/2019
ms.assetid: ea5186bb-5bff-4dcb-bde9-d6ba4e2edd00
dev_langs:
- csharp
- vb
ms.openlocfilehash: fb1bcfa50ec380f10ab67cc47331f91dc3e4b32d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380138"
---
# <a name="how-to-determine-if-a-file-is-an-assembly"></a>如何：判斷檔案是否為元件

檔案只有受管理時才是組件，而且其中繼資料會包含組件項目。 如需元件和中繼資料的詳細資訊，請參閱[組件資訊清單](manifest.md)。  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>如何以手動方式判斷檔案是否為組件  
  
1. 啟動 [Ildasm.exe (IL 反組譯工具)](../../framework/tools/ildasm-exe-il-disassembler.md)。  
  
2. 載入您要測試的檔案。  
  
3. 如果 **ILDASM** 回報該檔案並非可攜式執行檔 (PE)，則檔案不是組件。 如需詳細資訊，請參閱 how [to： View assembly 內容](view-contents.md)主題。  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>如何以程式設計方式判斷檔案是否為組件  
  
1. 呼叫 <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> 方法，並傳遞您要測試之檔案的完整檔案路徑和名稱。  
  
2. 如果擲回 <xref:System.BadImageFormatException> 例外狀況，則檔案不是組件。  
  
## <a name="example"></a>範例  
此範例會測試一個 DLL 以查看其是否為組件。  

```csharp
class TestAssembly  
{  
    static void Main()  
    {  
  
        try  
        {  
            System.Reflection.AssemblyName testAssembly =  
                System.Reflection.AssemblyName.GetAssemblyName(@"C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll");  
  
            System.Console.WriteLine("Yes, the file is an assembly.");  
        }  
  
        catch (System.IO.FileNotFoundException)  
        {  
            System.Console.WriteLine("The file cannot be found.");  
        }  
  
        catch (System.BadImageFormatException)  
        {  
            System.Console.WriteLine("The file is not an assembly.");  
        }  
  
        catch (System.IO.FileLoadException)  
        {  
            System.Console.WriteLine("The assembly has already been loaded.");  
        }  
    }  
}  
/* Output (with .NET Framework 3.5 installed):  
    Yes, the file is an assembly.  
*/  
```  

```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```

<xref:System.Reflection.AssemblyName.GetAssemblyName%2A> 方法會載入測試檔案，然後在讀取資訊之後釋放它。  
  
## <a name="see-also"></a>請參閱

- <xref:System.Reflection.AssemblyName>
- [C# 程式設計手冊](../../csharp/programming-guide/index.md)
- [程式設計概念（Visual Basic）](../../visual-basic/programming-guide/concepts/index.md)
- [.NET 中的組件](index.md)
