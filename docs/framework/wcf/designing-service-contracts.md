---
title: 設計服務合約
description: 瞭解服務合約，包括如何建立它們、可用的作業和資料類型，以及 WCF 程式設計中服務合約的其他層面。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF]
ms.assetid: 8e89cbb9-ac84-4f0d-85ef-0eb6be0022fd
ms.openlocfilehash: 366157b86ed7c420aed9a3a70838b4d6cd1e451f
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245384"
---
# <a name="designing-service-contracts"></a>設計服務合約
本主題說明何謂服務合約、如何定義服務合約、能夠進行哪些作業 (以及對基礎訊息交換的影響)、使用哪些資料型別以及其他問題，協助您設計能夠適當滿足情況需求的作業。  
  
## <a name="creating-a-service-contract"></a>建立服務合約  
 服務會公開作業的數量。 在 Windows Communication Foundation （WCF）應用程式中，藉由建立方法並使用屬性來標記來定義作業 <xref:System.ServiceModel.OperationContractAttribute> 。 接著，若要建立服務合約，請在以 <xref:System.ServiceModel.ServiceContractAttribute> 屬性標記的介面內宣告作業，或是在以相同屬性標記的類別中定義作業，藉此將作業分組。 （如需基本範例，請參閱[如何：定義服務合約](how-to-define-a-wcf-service-contract.md)）。  
  
 任何沒有屬性的方法 <xref:System.ServiceModel.OperationContractAttribute> 都不是服務作業，而且不會由 WCF 服務公開。  
  
 本主題將說明設計服務合約時的決策點：  
  
- 使用類別或介面。  
  
- 如何指定要交換的資料型別。  
  
- 您可以使用的交換模式類型。  
  
- 是否可以在合約中加入明確的安全性需求。  
  
- 作業輸入和輸出的限制。  
  
## <a name="classes-or-interfaces"></a>類別或介面  
 類別和介面都代表一組功能，因此兩者都可以用來定義 WCF 服務合約。 不過，建議您使用介面，因為介面會直接建立服務合約的模型。 在沒有實作的情況下，介面的功能不過就是定義包含特定簽章的方法群組。 執行服務合約介面，並已實作為 WCF 服務。  
  
 Managed 介面的所有優勢都會套用至服務合約介面：  
  
- 服務合約介面可擴充任意數目的其他服務合約介面。  
  
- 單一類別可藉由實作服務合約介面的方式，實作任意數目的服務合約。  
  
- 您可以藉由變更介面實作的方式修改服務合約的實作，同時讓服務合約維持不變。  
  
- 您只要實作舊介面和新介面，就能設定服務的版本。 舊的用戶端可連接到原始版本，而新的用戶端則可連接到新版本。  
  
> [!NOTE]
> 繼承自其他服務合約介面時，無法覆寫如名稱或命名空間這類作業屬性。 如果您嘗試這樣做，則會在目前的服務合約中建立新作業。  
  
 如需使用介面建立服務合約的範例，請參閱[如何：使用合約介面建立服務](./feature-details/how-to-create-a-service-with-a-contract-interface.md)。  
  
 不過，您可以使用類別定義服務合約，同時實作該合約。 直接將 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 分別套用至類別及該類別上的方法，藉此建立服務的好處在於速度和單純性。 而缺點則在於，Managed 類別不支援多重繼承，因此一次只能實作一個服務合約。 此外，對類別或方法簽章所做的任何修改，都會修改該服務的公開合約，如此可能會讓未修改的用戶端無法使用您的服務。 如需詳細資訊，請參閱[執行服務合約](implementing-service-contracts.md)。  
  
 如需使用類別來建立服務合約並同時加以執行的範例，請參閱[如何：使用合約類別建立服務](./feature-details/how-to-create-a-wcf-contract-with-a-class.md)。  
  
 至此您應了解使用介面和類別定義服務合約的差異。 下一步將要決定可在服務及其用戶端之間來回傳遞的資料。  
  
## <a name="parameters-and-return-values"></a>參數和傳回值  
 每一項作業都有傳回值和參數，即使它們是 `void`。 不過與區域方法不同的是，區域方法可以用來在物件之間傳遞物件的參考，服務作業則不會傳遞物件的參考， 而是傳遞物件的複本。  
  
 這點相當重要，因為參數或傳回值使用的每一個型別都必須可序列化，也就是說，必須能夠將該型別的物件轉換成位元組資料流，以及從位元組資料流轉換成物件。  
  
 基本型別預設為可序列化，.NET Framework 中的許多型別也是如此。  
  
> [!NOTE]
> 作業簽章中參數名稱的值是合約的一部分，而且必須區分大小寫。 如果您要在本機上使用相同的參數名稱，但是要修改已發行中繼資料的名稱，請參閱 <xref:System.ServiceModel.MessageParameterAttribute?displayProperty=nameWithType>。  
  
#### <a name="data-contracts"></a>資料合約  
 服務導向的應用程式（例如 Windows Communication Foundation （WCF）應用程式）是設計用來與 Microsoft 和非 Microsoft 平臺上最廣泛的用戶端應用程式交互操作。 為了盡可能提供最廣泛的互通性，建議您以 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性標記型別來建立資料合約，這是服務合約中描述服務作業所交換資料的部分。  
  
 資料合約為 Opt-in 式的合約：除非您明確套用資料合約屬性，否則不會序列化任何型別或資料成員。 資料合約與 Managed 程式碼的存取範圍無關：私用資料成員可以序列化，並且傳送至其他地方提供公開存取。 （如需資料合約的基本範例，請參閱[如何：建立類別或結構的基本資料合約](./feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)）。WCF 會處理基礎 SOAP 訊息的定義，以便啟用作業的功能，以及將您的資料類型序列化為訊息主體的傳入和傳出。 只要資料型別可以序列化，在設計您的作業時，就不需要考慮基礎訊息交換的基礎結構。  
  
 雖然一般 WCF 應用程式會使用 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性來建立作業的資料合約，但是您可以使用其他序列化機制。 標準 <xref:System.Runtime.Serialization.ISerializable>, <xref:System.SerializableAttribute> 和 <xref:System.Xml.Serialization.IXmlSerializable> 機制的功能都在於處理資料型別序列化為基礎 SOAP 訊息，以便在應用程式之間傳輸的過程。 如果您的資料型別需要特殊支援，可採用更多序列化策略。 如需 WCF 應用程式中資料類型序列化選項的詳細資訊，請參閱[指定服務合約中的資料傳輸](./feature-details/specifying-data-transfer-in-service-contracts.md)。  
  
#### <a name="mapping-parameters-and-return-values-to-message-exchanges"></a>將參數和傳回值對應到訊息交換  
 服務作業是由來回傳輸應用程式資料的基礎 SOAP 訊息交換所支援，此外還包括應用程式支援特定標準的安全性、交易和工作階段相關功能時所需的資料。 因為這是這種情況，服務作業的簽章會指示特定的基礎*訊息交換模式*（MEP），可支援資料傳輸和作業所需的功能。 您可以在 WCF 程式設計模型中指定三種模式：要求/回復、單向和雙工訊息模式。  
  
##### <a name="requestreply"></a>要求/回覆  
 要求/回覆模式是要求傳送者 (用戶端應用程式) 接收與要求相關聯之回覆的模式。 這是預設的 MEP，因為它支援將一個或多個參數傳遞至作業並將傳回值回傳給呼叫端的作業。 例如，下列 C# 程式碼範例示範基本的服務作業，此作業會取得一個字串並傳回一個字串。  
  
```csharp  
[OperationContractAttribute]  
string Hello(string greeting);  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<OperationContractAttribute()>  
Function Hello (ByVal greeting As String) As String  
```  
  
 這個作業簽章表示基礎訊息交換的形式。 如果沒有相互關聯，WCF 就無法判斷傳回值所預期的運算。  
  
 請注意，除非您指定不同的基礎訊息模式，否則即使是傳回 `void` （ `Nothing` 在 Visual Basic 中）的服務作業都是要求/回復訊息交換。 作業的結果會是：除非用戶端未同步叫用作業，否則用戶端會停止處理，直到收到傳回訊息為止 (即使一般情況下該訊息會是空的)。 下列 C# 程式碼範例示範一個作業，此作業會在用戶端收到空的訊息回應之後才傳回。  
  
```csharp  
[OperationContractAttribute]  
void Hello(string greeting);  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<OperationContractAttribute()>  
Sub Hello (ByVal greeting As String)  
```  
  
 如果作業的執行時間較長，前一個範例可能會降低用戶端效能與回應，但是即使要求/回覆作業傳回 `void`，這項作業仍有許多優點。 最明顯的優點就是可在回應訊息中傳回 SOAP 錯誤，表示通訊或處理過程中發生了某種服務相關的錯誤情況。 服務合約中指出的 SOAP 錯誤會做為 <xref:System.ServiceModel.FaultException%601> 物件傳遞至用戶端應用程式，其中型別參數為服務合約中指定的型別。 這會讓用戶端在 WCF 服務中輕鬆地通知有關錯誤狀況的資訊。 如需例外狀況、SOAP 錯誤和錯誤處理的詳細資訊，請參閱[指定和處理合約和服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md)。 若要查看要求/回復服務和用戶端的範例，請參閱[如何：建立要求-回復合約](./feature-details/how-to-create-a-request-reply-contract.md)。 如需有關要求-回復模式問題的詳細資訊，請參閱[要求-回復服務](./feature-details/request-reply-services.md)。  
  
##### <a name="one-way"></a>單向  
 如果 WCF 服務應用程式的用戶端不應該等候作業完成，也不會處理 SOAP 錯誤，則作業可以指定單向訊息模式。 單向作業是用戶端叫用作業，並在 WCF 將訊息寫入網路之後繼續處理的一種作業。 通常這表示，除非傳出訊息中傳送的資料相當大，否則用戶端幾乎會立即繼續執行 (除非傳送資料時發生錯誤)。 這種類型的訊息交換模式支援用戶端與伺服器應用程式之間，類似事件的行為。  
  
 若訊息交換僅包含送出訊息但未收到任何訊息，則不支援指定 `void` 以外傳回值的服務作業；在此情況下，會擲回 <xref:System.InvalidOperationException> 例外狀況。  
  
 沒有傳回訊息也就表示，可能未傳回任何 SOAP 錯誤，指出處理或通訊中發生任何錯誤。 (單向作業的通訊錯誤資訊需要雙工訊息交換模式)。  
  
 若要為傳回 `void` 的作業指定單向訊息交換，請將 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性設定為 `true`，如下列 C# 程式碼範例所示。  
  
```csharp  
[OperationContractAttribute(IsOneWay=true)]  
void Hello(string greeting);  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<OperationContractAttribute(IsOneWay := True)>  
Sub Hello (ByVal greeting As String)  
```  
  
 這個方法與之前的要求/回覆範例相同，但是將 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性設為 `true` 表示即使方法相同，服務作業仍不會送出傳回訊息，而且用戶端會在傳出訊息送至通道層之後立即傳回。 如需範例，請參閱[如何：建立單向合約](./feature-details/how-to-create-a-one-way-contract.md)。 如需單向模式的詳細資訊，請參閱[單向服務](./feature-details/one-way-services.md)。  
  
##### <a name="duplex"></a>雙工  
 雙工模式的特性在於同時擁有服務和用戶端的能力，可使用單向或要求/回覆傳訊方式分別傳送訊息給彼此。 這種雙向通訊的方式對於需要直接與用戶端通訊，或是提供非同步經驗給訊息交換之任一端 (包括類似事件的行為) 的服務而言相當實用。  
  
 由於與用戶單通訊時的額外機制，雙工模式會比要求/回覆或單向模式稍微複雜一些。  
  
 若要設計雙工合約，您必須同時設計回呼合約，並指派回呼合約的類型給標記服務合約之 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> 屬性 (Attribute) 的 <xref:System.ServiceModel.ServiceContractAttribute> 屬性 (Property)。  
  
 若要實作雙工模式，您必須建立另一個介面，其中包含在用戶端上呼叫的方法宣告。  
  
 如需建立服務的範例，以及存取該服務的用戶端，請參閱[如何：建立雙工合約](./feature-details/how-to-create-a-duplex-contract.md)和[如何：使用雙工合約來存取服務](./feature-details/how-to-access-services-with-a-duplex-contract.md)。 如需實用範例，請參閱[雙工](./samples/duplex.md)。 如需有關使用雙工合約之問題的詳細資訊，請參閱[雙工服務](./feature-details/duplex-services.md)。  
  
> [!CAUTION]
> 當服務收到雙工訊息時，會查看該傳入訊息中的 `ReplyTo` 項目，以判斷傳送回覆的位置。 如果用來接收訊息的通道不安全，那麼未受信任的用戶端可能會傳送惡意訊息，其中包含目標電腦的 `ReplyTo`，而導致該目標電腦拒絕服務 (DOS)。  
  
##### <a name="out-and-ref-parameters"></a>Out 和 Ref 參數  
 在大部分的情況下，您可以使用 `in` 參數（ `ByVal` Visual Basic 中）和 `out` 和 `ref` 參數（ `ByRef` 在 Visual Basic 中）。 由於 `out` 和 `ref` 這兩個參數都表示資料是從作業傳回，因此即使作業簽章 (如下所示) 傳回 `void`，仍會指定必須要求/回覆作業。  
  
```csharp  
[ServiceContractAttribute]  
public interface IMyContract  
{  
  [OperationContractAttribute]  
  public void PopulateData(ref CustomDataType data);  
}  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface IMyContract  
  <OperationContractAttribute()> _  
  Public Sub PopulateData(ByRef data As CustomDataType)  
End Interface  
```  
  
 唯一的例外狀況是簽章擁有特殊結構的情況。 例如，只有在用來宣告作業的方法傳回 <xref:System.ServiceModel.NetMsmqBinding> 時，才能使用 `void` 繫結與用戶端通訊；可能不會有輸出值，無論是傳回值或是 `ref` 或 `out` 參數。  
  
 此外，使用 `out` 或 `ref` 參數會要求作業擁有基礎回應訊息，以便攜回修改的物件。 如果您的作業是單向作業，則會在執行階段擲回 <xref:System.InvalidOperationException> 例外狀況。  
  
### <a name="specify-message-protection-level-on-the-contract"></a>指定合約上的訊息保護層級  
 設計合約時，您還必須決定實作合約之服務的訊息保護層級。 只有在訊息安全性套用至合約端點的繫結中時，才需要這樣做。 如果繫結的安全性已關閉 (也就是說，如果提供繫結的系統將 <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType> 設為 <xref:System.ServiceModel.SecurityMode.None?displayProperty=nameWithType> 這個值)，那麼您就不必決定合約的訊息保護層級。 在大部分情況下，系統所提供已套用訊息層級安全性的繫結會提供足夠的保護層級，因此您不需要考慮每項作業或每個訊息的保護層級。  
  
 保護層級是一個值，會指定支援服務的訊息 (或訊息部分) 為經過簽署、經過簽署且加密，或是已傳送但未包含簽章或加密。 保護層級可設定的範圍有許多種：於服務層級、適用特殊作業、適用該作業內的訊息，或訊息部分。 設定於某一範圍的值會變成更小範圍的預設值，除非有明確覆寫的值。 如果繫結組態無法提供合約所需的最小保護層級，則會擲回例外狀況。 而如果合約上未明確設定保護層級值，繫結組態就會控制所有訊息的保護層級 (如果繫結具備訊息安全性的話)。 此為預設行為。  
  
> [!IMPORTANT]
> 決定是否將合約的各種範圍明確設定為低於 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign?displayProperty=nameWithType> 的完整保護層級，通常是犧牲某種程度的安全性換取較高效能的決策。 在這種情況下，您的決定必須包含作業及其交換的資料值。 如需詳細資訊，請參閱[保護服務](securing-services.md)。  
  
 例如，下列程式碼範例不會設定合約上的 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 或 <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> 屬性。  
  
```csharp  
[ServiceContract]  
public interface ISampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute]  
  public int GetInt();
}  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<ServiceContractAttribute()> _  
Public Interface ISampleService  
  
  <OperationContractAttribute()> _  
  Public Function GetString()As String  
  
  <OperationContractAttribute()> _  
  Public Function GetData() As Integer  
  
End Interface  
```  
  
 與包含預設 `ISampleService` (預設的 <xref:System.ServiceModel.WSHttpBinding>，也就是 <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>) 的端點中的 <xref:System.ServiceModel.SecurityMode.Message> 實作互動時，所有訊息都會經過加密及簽署，因為這是預設的保護層級。 不過，使用包含預設 `ISampleService` (預設的 <xref:System.ServiceModel.BasicHttpBinding>，也就是 <xref:System.ServiceModel.SecurityMode>) 的 <xref:System.ServiceModel.SecurityMode.None> 服務時，所有訊息都會以文字傳送，因為此繫結沒有安全性，因此會忽略保護層級 (也就是說，訊息不會經過加密也不會簽署)。 如果將 <xref:System.ServiceModel.SecurityMode> 變更為 <xref:System.ServiceModel.SecurityMode.Message>，則這些訊息會經過加密並簽署 (因為該設定會成為繫結的預設保護層級)。  
  
 如果您要明確指定或調整合約的保護需求，請將 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 屬性 (或範圍較小的任何 `ProtectionLevel` 屬性) 設為服務合約需要的層級。 在這種情況下，若要使用明確的設定，繫結必須至少在使用的範圍內支援該設定。 例如，下列程式碼範例會明確指定一個 <xref:System.ServiceModel.OperationContractAttribute.ProtectionLevel%2A> 值，用於 `GetGuid` 作業。  
  
```csharp  
[ServiceContract]  
public interface IExplicitProtectionLevelSampleService  
{  
  [OperationContractAttribute]  
  public string GetString();  
  
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.None)]  
  public int GetInt();
  [OperationContractAttribute(ProtectionLevel=ProtectionLevel.EncryptAndSign)]  
  public int GetGuid();
}  
```  
  
 以下為 Visual Basic 程式碼的對等用法。  
  
```vb  
<ServiceContract()> _
Public Interface IExplicitProtectionLevelSampleService
    <OperationContract()> _
    Public Function GetString() As String
    End Function
  
    <OperationContract(ProtectionLevel := ProtectionLevel.None)> _
    Public Function GetInt() As Integer
    End Function
  
    <OperationContractAttribute(ProtectionLevel := ProtectionLevel.EncryptAndSign)> _
    Public Function GetGuid() As Integer
    End Function
  
End Interface  
```  
  
 實作此 `IExplicitProtectionLevelSampleService` 合約且擁有使用預設 <xref:System.ServiceModel.WSHttpBinding> (預設的 <xref:System.ServiceModel.SecurityMode?displayProperty=nameWithType>，也就是 <xref:System.ServiceModel.SecurityMode.Message>) 之端點的服務會有下列行為：  
  
- `GetString` 作業訊息會經過加密及簽署。  
  
- `GetInt` 作業訊息會以未加密且未簽署的文字 (也就是純文字) 傳送。  
  
- `GetGuid` 作業 <xref:System.Guid?displayProperty=nameWithType> 會在加密且簽署的訊息中傳回。  
  
 如需保護層級和使用方式的詳細資訊，請參閱[瞭解保護層級](understanding-protection-level.md)。 如需安全性的詳細資訊，請參閱[保護服務](securing-services.md)。  
  
##### <a name="other-operation-signature-requirements"></a>其他作業簽署需求  
 某些應用程式功能需要特殊類型的作業簽章。 例如，<xref:System.ServiceModel.NetMsmqBinding> 繫結支援長期服務和用戶端，其中應用程式可以在通訊期間重新啟動，並且從中斷的位置繼續進行，而不會遺漏任何訊息  （如需詳細資訊，請參閱[WCF 中的佇列](./feature-details/queues-in-wcf.md)）。不過，長期作業必須只接受一個 `in` 參數，而且沒有傳回值。  
  
 另一個範例是在作業中使用 <xref:System.IO.Stream> 類型。 遊於 <xref:System.IO.Stream> 參數包含整個訊息本文，因此如果輸入或輸出 (也就是 `ref` 參數、`out` 參數或傳回值) 為 <xref:System.IO.Stream> 類型，則必須是作業中指定的唯一輸入或輸出。 此外，參數或傳回型別都必須是 <xref:System.IO.Stream>、<xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> 或 <xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType>。 如需資料流程的詳細資訊，請參閱[大型資料和串流](./feature-details/large-data-and-streaming.md)。  
  
##### <a name="names-namespaces-and-obfuscation"></a>名稱、命名空間和混淆  
 當合約轉換為 WSDL 時，以及當建立及傳送合約訊息時，合約定義和作業中的 .NET 型別名稱和命名空間是有意義的。 因此，強烈建議使用所有支援合約之屬性 (Attribute) (例如 `Name`、`Namespace`、<xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.OperationContractAttribute> 和其他合約屬性 (Attribute) 的 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性 (Property)) 來明確設定服務合約名稱和命名空間。  
  
 這麼做的結果就是，如果未明確設定名稱和命名空間，對組件使用 IL 混淆會變更合約型別名稱和命名空間，並且導致 WSDL 遭到修改和連線交換 (通常會失敗)。 如果您未明確設定合約名稱和命名空間，但是想要使用混淆，請使用 <xref:System.Reflection.ObfuscationAttribute> 和 <xref:System.Reflection.ObfuscateAssemblyAttribute> 屬性，以防止合約型別名稱和命名空間遭到修改。  
  
## <a name="see-also"></a>另請參閱

- [如何：建立要求-回覆合約](./feature-details/how-to-create-a-request-reply-contract.md)
- [如何：建立單向合約](./feature-details/how-to-create-a-one-way-contract.md)
- [HOW TO：建立雙工合約](./feature-details/how-to-create-a-duplex-contract.md)
- [Specifying Data Transfer in Service Contracts](./feature-details/specifying-data-transfer-in-service-contracts.md)
- [指定及處理合約與服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md)
- [使用工作階段](using-sessions.md)
- [同步和非同步作業](synchronous-and-asynchronous-operations.md)
- [Reliable Services](reliable-services.md)
- [服務與異動](services-and-transactions.md)
