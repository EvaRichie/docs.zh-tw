---
title: 設定方法存取的安全性
description: 瞭解如何對不是供公用使用但仍需要公開的方法，讓方法存取安全。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, method access
- secure coding, method access
- security [.NET Framework], method access
- method access security
ms.assetid: f7c2d6ec-3b18-4e0e-9991-acd97189d818
ms.openlocfilehash: a7ef419cf3959cf7a3ffde874353dacd3815c81a
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309387"
---
# <a name="securing-method-access"></a>設定方法存取的安全性
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 有些方法可能不適合讓未受信任的任意程式碼呼叫。 這類方法會造成一些風險：方法可能會提供一些受限制的資訊；它可能會認定傳遞給它的任何資訊；它可能不會對參數執行錯誤檢查；它可能會因錯誤的參數發生問題或執行有害的動作。 您應該留意這些情況，並採取動作來協助保護方法。  
  
 在某些情況下，您可能需要限制不提供公用用途但仍必須是公用的方法。 例如，您可能會需要有跨您自己的 Dll 呼叫的介面，因此它必須是公用的，但為了防止客戶使用它，或惡意程式碼利用進入點進入您的元件，所以您不想將它公開。 另一個常見的原因是限制不適合公開使用的方法（但必須是公用的），以避免必須記載並支援可能是內部介面的方式。  
  
 Managed 程式碼提供數種方式以限制方法存取：  
  
- 限制類別、 組件、 或衍生類別的存取範圍，如果其可以信任。 這是最簡單限制方法存取權的方式。 一般來說，衍生類別可能會比它們衍生自的類別更值得信任，不過在某些情況下，它們會共用父類別的身分識別。 特別的是，請勿從關鍵字推斷信任 `protected` ，這不一定會用於安全性內容中。  
  
- 限制方法存取指定身分識別的呼叫者，基本上是您選擇的任何[特定辨識](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd%28v=vs.100%29)項（強式名稱、發行者、區域等等）。  
  
- 限制具有您選取權限之呼叫端的方法存取權。  
  
 同樣地，宣告式安全性可讓您控制類別的繼承。 您可以使用**InheritanceDemand**來執行下列動作：  
  
- 需要衍生類別以具有指定身分識別或權限。  
  
- 需要覆寫指定方法的衍生類別以具有指定身分識別或權限。  
  
 下列範例示範如何以要求呼叫端使用特定強勢名稱，來協助保護限制存取的公用類別。 這個範例會使用 <xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute> 具有強式名稱**要求**的。 如需如何使用強式名稱簽署元件的工作型資訊，請參閱[建立和使用強式名稱的元件](../../standard/assembly/create-use-strong-named.md)。  
  
```vb  
<StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey := "…hex…", Name := "App1", Version := "0.0.0.0")>  _  
Public Class Class1  
End Class  
```  
  
```csharp  
[StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey="…hex…", Name="App1", Version="0.0.0.0")]  
public class Class1  
{  
  
}
```  
  
## <a name="excluding-classes-and-members-from-use-by-untrusted-code"></a>將類別和成員排除在未受信任程式碼的使用之外  
 使用這一節中所示的宣告，來防止部分信任程式碼使用特定類別和方法，以及屬性和事件。 藉由將這些宣告套用至類別，您可以將保護套用至其所有方法、屬性和事件。 不過，欄位存取不會受到宣告式安全性的影響。 也請注意，連結要求協助防範立即呼叫端，且可能還是會受到引誘攻擊。  
  
> [!NOTE]
> .NET Framework 4 中引進了新的透明度模型。 [安全性透明的程式碼層級 2](security-transparent-code-level-2.md)模型會以屬性識別安全程式碼 <xref:System.Security.SecurityCriticalAttribute> 。 安全性關鍵的程式碼需要呼叫端和繼承者兩者都完全受信任。 從舊版 .NET Framework 程式碼存取安全性規則的組件可以呼叫層級 2 組件。 在此情況下，安全性關鍵屬性會被視為完全信任的連結要求。  
  
 在強式名稱的元件中，會將[LinkDemand](link-demands.md)套用至所有可公開存取的方法、屬性和事件，以限制其使用完全信任的呼叫端。 若要停用此功能，您必須套用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 屬性。 因此，只有不帶正負號的組件或具有此屬性的組件需要明確地標示類別，以排除不受信任的呼叫端您可以使用這些宣告以標記非為不受信任的呼叫端之類型的子集。  
  
 下列範例示範如何防止不受信任的程式碼使用類別和成員。  
  
 針對公用未密封的類別：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
Public Class CanDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public class CanDeriveFromMe  
{  
}  
```  
  
 針對公用密封的類別：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
NotInheritable Public Class CannotDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public sealed class CannotDeriveFromMe  
{  
}  
```  
  
 針對公用抽象類別：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _  
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
MustInherit Public Class CannotCreateInstanceOfMe_CanCastToMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public abstract class CannotCreateInstanceOfMe_CanCastToMe {}  
```  
  
 針對公用虛擬函式：  
  
```vb  
Class Base1
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overridable Sub CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Base1  
```  
  
```csharp  
class Base1
{  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
    public virtual void CanOverrideOrCallMe() {}  
}  
```  
  
 針對公用抽象函式：  
  
```vb  
MustInherit Class Base2  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Sub MustOverrideMe()  
    End Sub  
End Class 'Base2  
```  
  
```csharp  
abstract class Base2 {  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
public abstract void MustOverrideMe();  
}  
```  
  
 針對基底類別並不要求完全信任的公用覆寫函式：  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")]
    public override void CanOverrideOrCallMe()
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 針對基底類別要求完全信任的公用覆寫函式：  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]
    public override void CanOverrideOrCallMe()
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 針對公用介面：  
  
```vb  
Public Interface ICanCastToMe  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
    Sub CanImplementMe()  
End Interface 'ICanCastToMe  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
Class Implemented  
    Implements ICanCastToMe  
    Public Sub CanImplementMe()  
    End Sub 'CanImplementMe  
```  
  
```csharp  
public interface ICanCastToMe
{  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
void CanImplementMe();  
}  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
class Implemented : ICanCastToMe  
{  
    public void CanImplementMe()  
    {  
    }  
}  
```  
  
## <a name="virtual-internal-overrides-or-overloads-overridable-friend"></a>Virtual Internal 覆寫或 Overloads Overridable Friend  
  
> [!NOTE]
> 這一節會在將方法同時宣告為和時發出安全性問題 `virtual` `internal` （ `Overloads` `Overridable` `Friend` Visual Basic）。 此警告僅適用于 .NET Framework 版本1.0 和1.1，不適用於較新的版本。  
  
 在 .NET Framework 版本1.0 和1.1 中，當您確認程式碼無法供其他元件使用時，您必須留意類型系統協助工具的細微之處。 宣告為**虛擬**和**內部**的方法（Visual Basic 中的多載可覆**寫 Friend** ）可以覆寫父類別的 vtable 專案，而且只能從相同的元件內使用，因為它是內部的。 不過，覆寫的存取範圍是由**virtual**關鍵字決定，而且只要該程式碼可存取類別本身，就可以從另一個元件覆寫。 如果覆寫的可能性出現問題，請使用宣告式安全性來加以修正，或移除不是絕對必要的**虛擬**關鍵字。  
  
 即使語言編譯器會防止這些覆寫發生編譯錯誤，但使用其他編譯器撰寫的程式碼也可能會覆寫。  
  
## <a name="see-also"></a>另請參閱

- [安全程式碼撰寫方針](../../standard/security/secure-coding-guidelines.md)
