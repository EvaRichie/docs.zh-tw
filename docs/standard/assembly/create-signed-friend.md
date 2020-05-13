---
title: 如何：建立已簽署的 friend 元件
description: 本文說明如何使用 friend 元件搭配具有強式名稱的元件。 其中包含 .NET 安全性的相關資訊。
ms.date: 08/19/2019
ms.assetid: bab62063-61e6-453f-905f-77673df9534e
dev_langs:
- csharp
- vb
ms.openlocfilehash: b6176afed44e32911a37a0d753cea2bae7d8554e
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378547"
---
# <a name="how-to-create-signed-friend-assemblies"></a>如何：建立已簽署的 friend 元件
此範例示範如何搭配具有強式名稱的組件使用 friend 組件。 這兩個組件都必須具有強式名稱。 雖然此範例中的兩個組件使用相同的金鑰，但您可以針對這兩個組件使用不同的金鑰。  
  
## <a name="create-a-signed-assembly-and-a-friend-assembly"></a>建立已簽署的元件和 friend 元件  
  
1. 開啟命令提示字元。  
  
2. 使用下列命令順序和強式名稱工具，產生金鑰檔並顯示其公開金鑰。 如需詳細資訊，請參閱[sn.exe （強式名稱工具）](../../framework/tools/sn-exe-strong-name-tool.md)。  
  
    1. 產生此範例的強式名稱金鑰，並將它儲存在*FriendAssemblies*檔案中：  
  
         `sn -k FriendAssemblies.snk`  
  
    2. 從*FriendAssemblies*解壓縮公開金鑰，並將它放入*FriendAssemblies. publickey*：  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3. 顯示儲存在檔案*FriendAssemblies. publickey*中的公開金鑰：  
  
         `sn -tp FriendAssemblies.publickey`  
  
3. 建立名為*friend_signed_A*的 c # 或 Visual Basic 檔案，其中包含下列程式碼。 程式碼會使用 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性，將*friend_signed_B*宣告為 friend 元件。  

   強式名稱工具會在每次執行時產生新的公開金鑰。 因此，您必須將下列程式碼中的公開金鑰取代為剛產生的公開金鑰，如下列範例所示。  

   ```csharp  
   // friend_signed_A.cs  
   // Compile with:
   // csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   using System.Runtime.CompilerServices;  

   [assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")]  
   class Class1  
   {  
       public void Test()  
       {  
           System.Console.WriteLine("Class1.Test");  
           System.Console.ReadLine();  
       }  
   }  
   ```  

   ```vb  
   ' friend_signed_A.vb  
   ' Compile with:
   ' Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   Imports System.Runtime.CompilerServices  

   <Assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")>
   Public Class Class1  
       Public Sub Test()  
           System.Console.WriteLine("Class1.Test")  
           System.Console.ReadLine()  
       End Sub  
   End Class  
   ```  

4. 使用下列命令來編譯和簽署*friend_signed_A* 。  

   ```csharp
   csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
   ```  

   ```vb
   Vbc -target:library -keyfile:FriendAssemblies.snk friend_signed_A.vb  
   ```  

5. 建立名為*friend_signed_B*的 c # 或 Visual Basic 檔案，其中包含下列程式碼。 由於*friend_signed_A*會將*friend_signed_B*指定為 friend 元件，因此*friend_signed_B*中的程式碼可以 `internal` 從 friend_signed_A 存取（c #）或 `Friend` （ * *Visual Basic）類型和成員。 該檔案包含下列程式碼。  

   ```csharp  
   // friend_signed_B.cs  
   // Compile with:
   // csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   public class Program  
   {  
       static void Main()  
       {  
           Class1 inst = new Class1();  
           inst.Test();  
       }  
   }  
   ```  

   ```vb  
   ' friend_signed_B.vb  
   ' Compile with:
   ' Vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   Module Sample  
       Public Sub Main()  
           Dim inst As New Class1  
           inst.Test()  
       End Sub  
   End Module  
   ```  

6. 使用下列命令來編譯和簽署*friend_signed_B* 。  

   ```csharp
   csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
   ```  

   ```vb
   vbc -keyfile:FriendAssemblies.snk -r:friend_signed_A.dll friend_signed_B.vb  
   ```  

   編譯器所產生之組件的名稱必須符合傳遞至 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性的 Friend 組件名稱。 您必須使用編譯器選項，明確指定輸出元件（*.exe*或 *.dll*）的名稱 `-out` 。 如需詳細資訊，請參閱[-out （c # 編譯器選項）](../../csharp/language-reference/compiler-options/out-compiler-option.md)或[-out （Visual Basic）](../../visual-basic/reference/command-line-compiler/out.md)。  

7. 執行*friend_signed_B .exe*檔案。  

   程式會輸出字串**Class1。 Test**。  
  
## <a name="net-security"></a>.NET 安全性  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 屬性和 <xref:System.Security.Permissions.StrongNameIdentityPermission> 類別之間有相似性。 主要差異在於， <xref:System.Security.Permissions.StrongNameIdentityPermission> 可以要求安全性許可權來執行特定的程式碼區段，而屬性則 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 控制 `internal` （c #）或 `Friend` （Visual Basic）類型和成員的可見度。  
  
## <a name="see-also"></a>請參閱

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [.NET 中的組件](index.md)
- [Friend 組件](friend.md)
- [如何：建立未簽署的 friend 元件](create-unsigned-friend.md)
- [-keyfile （c #）](../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)
- [-keyfile （Visual Basic）](../../visual-basic/reference/command-line-compiler/keyfile.md)
- [Sn.exe （強式名稱工具）](../../framework/tools/sn-exe-strong-name-tool.md)
- [建立和使用強式名稱的組件](create-use-strong-named.md)
- [C# 程式設計手冊](../../csharp/programming-guide/index.md)
- [程式設計概念（Visual Basic）](../../visual-basic/programming-guide/concepts/index.md)
