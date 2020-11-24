---
title: 自訂序列化
description: 自訂序列化是控制型別的序列化和還原序列化。 控制序列化可以確保序列化相容性。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- binary serialization, custom serialization
- custom serialization
- binary serialization, controlling
- OptionalFieldAttribute class, custom serialization
- ISerializable interface, custom serialization
- OnDeserializingAttribute class, custom serialization
- OnSerializedAttribute class, custom serialization
- serialization, custom serialization
- serialization, controlling
- OnDeserializedAttribute class, custom serialization
- OnSerializingAttribute class, custom serialization
ms.assetid: 12ed422d-5280-49b8-9b71-a2ed129c0384
ms.openlocfilehash: 4ca78c71f464a914c07583825d4a7027ebb11bf6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679035"
---
# <a name="custom-serialization"></a><span data-ttu-id="55725-104">自訂序列化</span><span class="sxs-lookup"><span data-stu-id="55725-104">Custom serialization</span></span>

<span data-ttu-id="55725-105">自訂序列化是控制型別序列化與還原序列化的程序。</span><span class="sxs-lookup"><span data-stu-id="55725-105">Custom serialization is the process of controlling the serialization and deserialization of a type.</span></span> <span data-ttu-id="55725-106">控制序列化就可確保序列化相容性，也就是在類型版本之間進行序列化與還原序列化的作業，而不違反類型的核心功能性。</span><span class="sxs-lookup"><span data-stu-id="55725-106">By controlling serialization, it's possible to ensure serialization compatibility, which is the ability to serialize and deserialize between versions of a type without breaking the core functionality of the type.</span></span> <span data-ttu-id="55725-107">例如，在第一版的型別中，可能只有兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="55725-107">For example, in the first version of a type, there may be only two fields.</span></span> <span data-ttu-id="55725-108">在型別的下一版中，加入了更多的欄位。</span><span class="sxs-lookup"><span data-stu-id="55725-108">In the next version of a type, several more fields are added.</span></span> <span data-ttu-id="55725-109">然而第二版的應用程式必須對這兩種型別進行序列化及還原序列化。</span><span class="sxs-lookup"><span data-stu-id="55725-109">Yet the second version of an application must be able to serialize and deserialize both types.</span></span> <span data-ttu-id="55725-110">下列章節會說明控制序列化的方法。</span><span class="sxs-lookup"><span data-stu-id="55725-110">The following sections describe how to control serialization.</span></span>

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]
  
> [!IMPORTANT]
> <span data-ttu-id="55725-111">在 .NET Framework 4.0 之前的版本中，會使用來完成部分信任元件中的自訂使用者資料序列化 `GetObjectData` 。</span><span class="sxs-lookup"><span data-stu-id="55725-111">In versions previous to .NET Framework 4.0, serialization of custom user data in a partially trusted assembly was accomplished using `GetObjectData`.</span></span> <span data-ttu-id="55725-112">從版本4.0 開始，該方法會以屬性標記 <xref:System.Security.SecurityCriticalAttribute> ，以防止在部分信任的元件中執行。</span><span class="sxs-lookup"><span data-stu-id="55725-112">Starting with version 4.0, that method is marked with the <xref:System.Security.SecurityCriticalAttribute> attribute, which prevents execution in partially trusted assemblies.</span></span> <span data-ttu-id="55725-113">若要解決此狀況，請實作 <xref:System.Runtime.Serialization.ISafeSerializationData> 介面。</span><span class="sxs-lookup"><span data-stu-id="55725-113">To work around this condition, implement the <xref:System.Runtime.Serialization.ISafeSerializationData> interface.</span></span>  
  
## <a name="running-custom-methods-during-and-after-serialization"></a><span data-ttu-id="55725-114">序列化期間及序列化之後執行自訂方法</span><span class="sxs-lookup"><span data-stu-id="55725-114">Running custom methods during and after serialization</span></span>

<span data-ttu-id="55725-115">在序列化期間和之後執行自訂方法的建議方式是將下列屬性套用至用來在序列化期間和之後更正資料的方法：</span><span class="sxs-lookup"><span data-stu-id="55725-115">The recommended way to run custom methods during and after serialization is to apply the following attributes to methods that are used to correct data during and after serialization:</span></span>  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute>  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute>  
  
 <span data-ttu-id="55725-116">這些屬性允許型別參與序列化及還原序列化程序的任何一個或所有四個階段。</span><span class="sxs-lookup"><span data-stu-id="55725-116">These attributes allow the type to participate in any one of, or all four of the phases, of the serialization and deserialization processes.</span></span> <span data-ttu-id="55725-117">屬性指定應在每個階段叫用的型別方法。</span><span class="sxs-lookup"><span data-stu-id="55725-117">The attributes specify the methods of the type that should be invoked during each phase.</span></span> <span data-ttu-id="55725-118">這些方法並不存取序列化資料流，而是允許您在序列化前後或還原序列化前後變更物件。</span><span class="sxs-lookup"><span data-stu-id="55725-118">The methods do not access the serialization stream but instead allow you to alter the object before and after serialization, or before and after deserialization.</span></span> <span data-ttu-id="55725-119">屬性可套用在所有層級的型別繼承階層，且會呼叫從基本到最具衍生性之階層中的每個方法。</span><span class="sxs-lookup"><span data-stu-id="55725-119">The attributes can be applied at all levels of the type inheritance hierarchy, and each method is called in the hierarchy from the base to the most derived.</span></span> <span data-ttu-id="55725-120">此機制避開實作 <xref:System.Runtime.Serialization.ISerializable> 介面的複雜性以及任何產生的問題，方法是將序列化與還原序列化的責任賦予最具衍生性的實作。</span><span class="sxs-lookup"><span data-stu-id="55725-120">This mechanism avoids the complexity and any resulting issues of implementing the <xref:System.Runtime.Serialization.ISerializable> interface by giving the responsibility for serialization and deserialization to the most derived implementation.</span></span> <span data-ttu-id="55725-121">除此之外，此機制允許格式子忽略欄位填入以及自序列化資料流的擷取。</span><span class="sxs-lookup"><span data-stu-id="55725-121">Additionally, this mechanism allows the formatters to ignore the population of fields and retrieval from the serialization stream.</span></span> <span data-ttu-id="55725-122">如需控制序列化與還原序列化的詳細資訊以及範例，請按一下任何一個先前的連結。</span><span class="sxs-lookup"><span data-stu-id="55725-122">For details and examples of controlling serialization and deserialization, click any of the previous links.</span></span>  
  
 <span data-ttu-id="55725-123">除此之外，當加入新欄位至現有可序列化型別時，即對欄位套用 <xref:System.Runtime.Serialization.OptionalFieldAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="55725-123">In addition, when adding a new field to an existing serializable type, apply the <xref:System.Runtime.Serialization.OptionalFieldAttribute> attribute to the field.</span></span> <span data-ttu-id="55725-124">在處理遺漏新欄位的資料流時，<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 及 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 會忽略缺少的欄位。</span><span class="sxs-lookup"><span data-stu-id="55725-124">The <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> and the <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> ignores the absence of the field when a stream that is missing the new field is processed.</span></span>  
  
## <a name="implementing-the-iserializable-interface"></a><span data-ttu-id="55725-125">實作 ISerializable 介面</span><span class="sxs-lookup"><span data-stu-id="55725-125">Implementing the ISerializable interface</span></span>  

 <span data-ttu-id="55725-126">控制序列化的另一個方法是實作物件上的 <xref:System.Runtime.Serialization.ISerializable> 介面。</span><span class="sxs-lookup"><span data-stu-id="55725-126">The other way to control serialization is achieved by implementing the <xref:System.Runtime.Serialization.ISerializable> interface on an object.</span></span> <span data-ttu-id="55725-127">不過請注意，前一節的方法會取代此方法來控制序列化。</span><span class="sxs-lookup"><span data-stu-id="55725-127">Note, however, that the method in the previous section supersedes this method to control serialization.</span></span>  
  
 <span data-ttu-id="55725-128">此外，對於標記為 [Serializable](xref:System.SerializableAttribute) 屬性且在類別層級或其建構函式上擁有宣告式或命令式安全性的類別，不應使用預設序列化。</span><span class="sxs-lookup"><span data-stu-id="55725-128">In addition, you should not use default serialization on a class that is marked with the [Serializable](xref:System.SerializableAttribute) attribute and has declarative or imperative security at the class level or on its constructors.</span></span> <span data-ttu-id="55725-129">取代的做法是讓這些類別實作 <xref:System.Runtime.Serialization.ISerializable> 介面。</span><span class="sxs-lookup"><span data-stu-id="55725-129">Instead, these classes should always implement the <xref:System.Runtime.Serialization.ISerializable> interface.</span></span>  
  
 <span data-ttu-id="55725-130">實作 <xref:System.Runtime.Serialization.ISerializable> 包括實作 `GetObjectData` 方法，以及還原序列化某物件時使用的特殊建構函式。</span><span class="sxs-lookup"><span data-stu-id="55725-130">Implementing <xref:System.Runtime.Serialization.ISerializable> involves implementing the `GetObjectData` method and a special constructor that is used when the object is deserialized.</span></span> <span data-ttu-id="55725-131">下列範例程式碼顯示如何在上一個章節的 <xref:System.Runtime.Serialization.ISerializable> 類別上實作 `MyObject`。</span><span class="sxs-lookup"><span data-stu-id="55725-131">The following sample code shows how to implement <xref:System.Runtime.Serialization.ISerializable> on the `MyObject` class from a previous section.</span></span>  
  
```csharp
[Serializable]
public class MyObject : ISerializable
{
    public int n1;
    public int n2;
    public String str;

    public MyObject()
    {
    }

    protected MyObject(SerializationInfo info, StreamingContext context)
    {
      n1 = info.GetInt32("i");
      n2 = info.GetInt32("j");
      str = info.GetString("k");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public virtual void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue("i", n1);
        info.AddValue("j", n2);
        info.AddValue("k", str);
    }
}
```

```vb
<Serializable()>  _
Public Class MyObject
    Implements ISerializable
    Public n1 As Integer
    Public n2 As Integer
    Public str As String

    Public Sub New()
    End Sub

    Protected Sub New(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        n1 = info.GetInt32("i")
        n2 = info.GetInt32("j")
        str = info.GetString("k")
    End Sub 'New

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overridable Sub GetObjectData(ByVal info As SerializationInfo, ByVal context As StreamingContext)
        info.AddValue("i", n1)
        info.AddValue("j", n2)
        info.AddValue("k", str)
    End Sub
End Class
```  
  
 <span data-ttu-id="55725-132">在序列化期間呼叫 **GetObjectData** 時，您必須填入方法呼叫所提供的 <xref:System.Runtime.Serialization.SerializationInfo>。</span><span class="sxs-lookup"><span data-stu-id="55725-132">When **GetObjectData** is called during serialization, you are responsible for populating the <xref:System.Runtime.Serialization.SerializationInfo> provided with the method call.</span></span> <span data-ttu-id="55725-133">以名稱與值的配對，加入想要序列化的變數。</span><span class="sxs-lookup"><span data-stu-id="55725-133">Add the variables to be serialized as name and value pairs.</span></span> <span data-ttu-id="55725-134">任何文字都能當成名稱使用。</span><span class="sxs-lookup"><span data-stu-id="55725-134">Any text can be used as the name.</span></span> <span data-ttu-id="55725-135">您可自由決定要加入哪些成員變數至 <xref:System.Runtime.Serialization.SerializationInfo>，前提是在還原序列化期間序列化足夠的資料以還原物件。</span><span class="sxs-lookup"><span data-stu-id="55725-135">You have the freedom to decide which member variables are added to the <xref:System.Runtime.Serialization.SerializationInfo>, provided that sufficient data is serialized to restore the object during deserialization.</span></span> <span data-ttu-id="55725-136">如果基底物件實作 <xref:System.Runtime.Serialization.ISerializable>，衍生類別應呼叫基底物件的 **GetObjectData** 方法。</span><span class="sxs-lookup"><span data-stu-id="55725-136">Derived classes should call the **GetObjectData** method on the base object if the latter implements <xref:System.Runtime.Serialization.ISerializable>.</span></span>  
  
 <span data-ttu-id="55725-137">請注意，序列化可允許其他程式碼看到或變更原本無法存取的物件執行個體資料。</span><span class="sxs-lookup"><span data-stu-id="55725-137">Note that serialization can allow other code to see or modify object instance data that is otherwise inaccessible.</span></span> <span data-ttu-id="55725-138">因此，執行序列化的程式碼需要已指定 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 旗標的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute)。</span><span class="sxs-lookup"><span data-stu-id="55725-138">Therefore, code that performs serialization requires the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified.</span></span> <span data-ttu-id="55725-139">依照預設原則，這個使用權限不會授與給網際網路下載或內部網路的程式碼；只有本機電腦上的程式碼才會被授與這個使用權限。</span><span class="sxs-lookup"><span data-stu-id="55725-139">Under default policy, this permission is not given to Internet-downloaded or intranet code; only code on the local computer is granted this permission.</span></span> <span data-ttu-id="55725-140">**GetObjectData** 方法必須明確加以保護，做法是要求已指定 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 旗標的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 或要求專門協助保護私人資料的其他權限。</span><span class="sxs-lookup"><span data-stu-id="55725-140">The **GetObjectData** method must be explicitly protected either by demanding the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified or by demanding other permissions that specifically help protect private data.</span></span>  
  
 <span data-ttu-id="55725-141">如果私用欄位儲存機密資訊，您應該要求 **GetObjectData** 的適當權限以保護資料。</span><span class="sxs-lookup"><span data-stu-id="55725-141">If a private field stores sensitive information, you should demand the appropriate permissions on **GetObjectData** to protect the data.</span></span> <span data-ttu-id="55725-142">請記住，擁有已指定 **SerializationFormatter** 旗標之 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 授權的程式碼，可以檢視與變更儲存在私用欄位的資料。</span><span class="sxs-lookup"><span data-stu-id="55725-142">Remember that code that has been granted [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the **SerializationFormatter** flag specified can view and modify the data stored in private fields.</span></span> <span data-ttu-id="55725-143">已授與此 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 的惡意呼叫者，可檢視資料 (例如隱藏的目錄位置或授與的權限) 並以資料利用電腦上的安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="55725-143">A malicious caller granted this [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) can view data such as hidden directory locations or granted permissions and use the data to exploit a security vulnerability on the computer.</span></span> <span data-ttu-id="55725-144">如需可指定的安全性權限旗標完整清單，請參閱 [SecurityPermissionFlag 列舉](xref:System.Security.Permissions.SecurityPermissionFlag)。</span><span class="sxs-lookup"><span data-stu-id="55725-144">For a complete list of the security permission flags you can specify, see the [SecurityPermissionFlag Enumeration](xref:System.Security.Permissions.SecurityPermissionFlag).</span></span>  
  
 <span data-ttu-id="55725-145">特別要強調的是，將 <xref:System.Runtime.Serialization.ISerializable> 新增至類別時，您必須同時實作 **GetObjectData** 以及特殊的建構函式。</span><span class="sxs-lookup"><span data-stu-id="55725-145">It's important to stress that when <xref:System.Runtime.Serialization.ISerializable> is added to a class you must implement both **GetObjectData** and the special constructor.</span></span> <span data-ttu-id="55725-146">如果遺漏 **GetObjectData**，編譯器會警告您。</span><span class="sxs-lookup"><span data-stu-id="55725-146">The compiler warns you if **GetObjectData** is missing.</span></span> <span data-ttu-id="55725-147">然而，因為不可能強制實作建構函式，因此若缺少建構函式時並不會發出警告，若試圖對無建構函式的類別還原序列化時會擲出例外狀況。</span><span class="sxs-lookup"><span data-stu-id="55725-147">However, because it is impossible to enforce the implementation of a constructor, no warning is provided if the constructor is absent, and an exception is thrown when an attempt is made to deserialize a class without the constructor.</span></span>  
  
 <span data-ttu-id="55725-148">目前設計在避開潛在安全性與版本設定問題上，較 <xref:System.Runtime.Serialization.ISerializationSurrogate.SetObjectData%2A> 方法更受歡迎。</span><span class="sxs-lookup"><span data-stu-id="55725-148">The current design was favored above a <xref:System.Runtime.Serialization.ISerializationSurrogate.SetObjectData%2A> method to get around potential security and versioning problems.</span></span> <span data-ttu-id="55725-149">例如，若 `SetObjectData` 方法定義為介面的一部分，就必須為公用，因此使用者必須撰寫程式碼避免多次呼叫 **SetObjectData** 方法。</span><span class="sxs-lookup"><span data-stu-id="55725-149">For example, a `SetObjectData` method must be public if it is defined as part of an interface; thus users must write code to defend against having the **SetObjectData** method called multiple times.</span></span> <span data-ttu-id="55725-150">否則，對執行作業程序中物件呼叫 **SetObjectData** 方法的惡意應用程式，就可能造成潛在的問題。</span><span class="sxs-lookup"><span data-stu-id="55725-150">Otherwise, a malicious application that calls the **SetObjectData** method on an object in the process of executing an operation can cause potential problems.</span></span>  
  
 <span data-ttu-id="55725-151">在還原序列化期間，<xref:System.Runtime.Serialization.SerializationInfo> 將使用專門的建構函式傳遞給類別。</span><span class="sxs-lookup"><span data-stu-id="55725-151">During deserialization, <xref:System.Runtime.Serialization.SerializationInfo> is passed to the class using the constructor provided for this purpose.</span></span> <span data-ttu-id="55725-152">物件還原序列化後，即忽略所有對建構函式所設定的可視性約束，因此您可將類別標示為公用的、保護的、內部的或私用的。</span><span class="sxs-lookup"><span data-stu-id="55725-152">Any visibility constraints placed on the constructor are ignored when the object is deserialized; so you can mark the class as public, protected, internal, or private.</span></span> <span data-ttu-id="55725-153">不過，最好的做法是除非類別已密封，此時應將建構函式標示為保護的，在此狀況下建構函式應標示為私人的。</span><span class="sxs-lookup"><span data-stu-id="55725-153">However, it is a best practice to make the constructor protected unless the class is sealed, in which case the constructor should be marked private.</span></span> <span data-ttu-id="55725-154">建構函式應進行徹底的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="55725-154">The constructor should also perform thorough input validation.</span></span> <span data-ttu-id="55725-155">為了避免惡意程式碼的濫用，建構函式應使用任何其他建構函式，強制執行取得類別的執行個體時所需的相同安全性檢查和使用權限。</span><span class="sxs-lookup"><span data-stu-id="55725-155">To avoid misuse by malicious code, the constructor should enforce the same security checks and permissions required to obtain an instance of the class using any other constructor.</span></span> <span data-ttu-id="55725-156">如果您未遵循此建議，惡意程式碼可以預先序列化物件，並以指定為 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> 旗標的 [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) 取得控制，然後在用戶端電腦還原序列化物件，略過所有使用公用建構函式在標準執行個體建構期間套用的安全性。</span><span class="sxs-lookup"><span data-stu-id="55725-156">If you do not follow this recommendation, malicious code can preserialize an object, obtain control with the [SecurityPermission](xref:System.Security.Permissions.SecurityPermissionAttribute) with the <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter> flag specified and deserialize the object on a client computer bypassing any security that would have been applied during standard instance construction using a public constructor.</span></span>  
  
 <span data-ttu-id="55725-157">若想要還原物件的狀態，只要從 <xref:System.Runtime.Serialization.SerializationInfo> 以序列化期間使用的名稱擷取變數值，</span><span class="sxs-lookup"><span data-stu-id="55725-157">To restore the state of the object, simply retrieve the values of the variables from <xref:System.Runtime.Serialization.SerializationInfo> using the names used during serialization.</span></span> <span data-ttu-id="55725-158">若基底類別實作 <xref:System.Runtime.Serialization.ISerializable>，應呼叫基底建構函式以允許基底物件還原變數。</span><span class="sxs-lookup"><span data-stu-id="55725-158">If the base class implements <xref:System.Runtime.Serialization.ISerializable>, the base constructor should be called to allow the base object to restore its variables.</span></span>  
  
 <span data-ttu-id="55725-159">從實作 <xref:System.Runtime.Serialization.ISerializable> 的類別衍生新類別時，若也有需要序列化的變數時，衍生類別必須也實作兩者的建構函式以及 **GetObjectData** 方法。</span><span class="sxs-lookup"><span data-stu-id="55725-159">When you derive a new class from one that implements <xref:System.Runtime.Serialization.ISerializable>, the derived class must implement both the constructor as well as the **GetObjectData** method if it has variables that need to be serialized.</span></span> <span data-ttu-id="55725-160">下列程式碼範例示範如何使用先前所示的 `MyObject` 類別做到這點。</span><span class="sxs-lookup"><span data-stu-id="55725-160">The following code example shows how this is done using the `MyObject` class shown previously.</span></span>  
  
```csharp
[Serializable]
public class ObjectTwo : MyObject
{
    public int num;

    public ObjectTwo()
      : base()
    {
    }

    protected ObjectTwo(SerializationInfo si, StreamingContext context)
      : base(si, context)
    {
        num = si.GetInt32("num");
    }

    [SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter = true)]
    public override void GetObjectData(SerializationInfo si, StreamingContext context)
    {
        base.GetObjectData(si,context);
        si.AddValue("num", num);
    }
}
```

```vb
<Serializable()>  _
Public Class ObjectTwo
    Inherits MyObject
    Public num As Integer

    Public Sub New()

    End Sub

    Protected Sub New(ByVal si As SerializationInfo, _
    ByVal context As StreamingContext)
        MyBase.New(si, context)
        num = si.GetInt32("num")
    End Sub

    <SecurityPermissionAttribute(SecurityAction.Demand, SerializationFormatter := True)> _
    Public Overrides Sub GetObjectData(ByVal si As SerializationInfo, ByVal context As StreamingContext)
        MyBase.GetObjectData(si, context)
        si.AddValue("num", num)
    End Sub
End Class
```  
  
 <span data-ttu-id="55725-161">請不要忘記在還原序列化建構函式中呼叫基底類別。</span><span class="sxs-lookup"><span data-stu-id="55725-161">Don't forget to call the base class in the deserialization constructor.</span></span> <span data-ttu-id="55725-162">若不這麼做，將永遠不會呼叫基底類別上的建構函式，物件在還原序列化之後就不會完整建構。</span><span class="sxs-lookup"><span data-stu-id="55725-162">If this isn't done, the constructor on the base class is never called, and the object is not fully constructed after deserialization.</span></span>  
  
 <span data-ttu-id="55725-163">物件由內向外重新建構；在還原序列化期間呼叫方法可能會造成無法想像的副作用，因為呼叫的方法可能參考該呼叫尚未還原序列化時的物件參考。</span><span class="sxs-lookup"><span data-stu-id="55725-163">Objects are reconstructed from the inside out; and calling methods during deserialization can have undesirable side effects, because the methods called might refer to object references that have not been deserialized by the time the call is made.</span></span> <span data-ttu-id="55725-164">如果還原序列化的類別實作 <xref:System.Runtime.Serialization.IDeserializationCallback>，在整個物件圖形還原序列化後，即自動呼叫 <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="55725-164">If the class being deserialized implements the <xref:System.Runtime.Serialization.IDeserializationCallback>, the <xref:System.Runtime.Serialization.IDeserializationCallback.OnDeserialization%2A> method is automatically called when the entire object graph has been deserialized.</span></span> <span data-ttu-id="55725-165">此時，所有參考的子物件已完整還原。</span><span class="sxs-lookup"><span data-stu-id="55725-165">At this point, all the child objects referenced have been fully restored.</span></span> <span data-ttu-id="55725-166">雜湊表是不使用事件接聽程式就很難還原序列化的常見類別範例。</span><span class="sxs-lookup"><span data-stu-id="55725-166">A hash table is a typical example of a class that is difficult to deserialize without using the event listener.</span></span> <span data-ttu-id="55725-167">在還原序列化期間擷取索引鍵與值組很容易，但將這些物件加回雜湊表卻會造成問題，因為無法保證從雜湊表衍生的類別已還原序列化。</span><span class="sxs-lookup"><span data-stu-id="55725-167">It is easy to retrieve the key and value pairs during deserialization, but adding these objects back to the hash table can cause problems, because there is no guarantee that classes that derived from the hash table have been deserialized.</span></span> <span data-ttu-id="55725-168">因此於此階段呼叫雜湊表上的方法實屬不當。</span><span class="sxs-lookup"><span data-stu-id="55725-168">Calling methods on a hash table at this stage is therefore not advisable.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="55725-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="55725-169">See also</span></span>

- [<span data-ttu-id="55725-170">二進位序列化</span><span class="sxs-lookup"><span data-stu-id="55725-170">Binary Serialization</span></span>](binary-serialization.md)
- [<span data-ttu-id="55725-171">XML 和 SOAP 序列化</span><span class="sxs-lookup"><span data-stu-id="55725-171">XML and SOAP Serialization</span></span>](xml-and-soap-serialization.md)
- [<span data-ttu-id="55725-172">安全性和序列化</span><span class="sxs-lookup"><span data-stu-id="55725-172">Security and Serialization</span></span>](../../framework/misc/security-and-serialization.md)
