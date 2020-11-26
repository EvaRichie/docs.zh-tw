---
title: 作法：設定 ProtectionLevel 屬性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
- ProtectionLevel property
ms.assetid: 3d4e8f80-0f9e-4a26-9899-beb6584e78df
ms.openlocfilehash: 359364228c4ab4d5b247f4f42f3ef3391f774197
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236594"
---
# <a name="how-to-set-the-protectionlevel-property"></a><span data-ttu-id="b0b78-102">作法：設定 ProtectionLevel 屬性</span><span class="sxs-lookup"><span data-stu-id="b0b78-102">How to: Set the ProtectionLevel Property</span></span>

<span data-ttu-id="b0b78-103">您可以套用適當的屬性 (Attribute) 並設定屬性 (Property)，藉此設定保護層級。</span><span class="sxs-lookup"><span data-stu-id="b0b78-103">You can set the protection level by applying an appropriate attribute and setting the property.</span></span> <span data-ttu-id="b0b78-104">您可以設定服務層級的保護，以影響每一個訊息的所有部分，或是從方法到訊息部分，設定越發細微的保護層級。</span><span class="sxs-lookup"><span data-stu-id="b0b78-104">You can set protection at the service level to affect all parts of every message, or you can set protection at increasingly granular levels, from methods to message parts.</span></span> <span data-ttu-id="b0b78-105">如需屬性的詳細資訊 `ProtectionLevel` ，請參閱 [瞭解保護層級](understanding-protection-level.md)。</span><span class="sxs-lookup"><span data-stu-id="b0b78-105">For more information about the `ProtectionLevel` property, see [Understanding Protection Level](understanding-protection-level.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b0b78-106">您只能在程式碼中設定保護層級，而不能在組態中設定。</span><span class="sxs-lookup"><span data-stu-id="b0b78-106">You can set protection levels only in code, not in configuration.</span></span>  
  
### <a name="to-sign-all-messages-for-a-service"></a><span data-ttu-id="b0b78-107">簽署服務的所有訊息</span><span class="sxs-lookup"><span data-stu-id="b0b78-107">To sign all messages for a service</span></span>  
  
1. <span data-ttu-id="b0b78-108">建立服務的介面。</span><span class="sxs-lookup"><span data-stu-id="b0b78-108">Create an interface for the service.</span></span>  
  
2. <span data-ttu-id="b0b78-109">將 <xref:System.ServiceModel.ServiceContractAttribute> 屬性 (Attribute) 套用至服務，並且將 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 屬性 (Property) 設為 <xref:System.Net.Security.ProtectionLevel.Sign>，如以下程式碼中所示 (預設層級為 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>)。</span><span class="sxs-lookup"><span data-stu-id="b0b78-109">Apply the <xref:System.ServiceModel.ServiceContractAttribute> attribute to the service and set the <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> property to <xref:System.Net.Security.ProtectionLevel.Sign>, as shown in the following code (the default level is <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>).</span></span>  
  
     [!code-csharp[C_ProtectionLevel#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#1)]
     [!code-vb[C_ProtectionLevel#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#1)]  
  
### <a name="to-sign-all-message-parts-for-an-operation"></a><span data-ttu-id="b0b78-110">簽署作業的所有訊息部分</span><span class="sxs-lookup"><span data-stu-id="b0b78-110">To sign all message parts for an operation</span></span>  
  
1. <span data-ttu-id="b0b78-111">建立服務的介面，並且將 <xref:System.ServiceModel.ServiceContractAttribute> 屬性套用至介面。</span><span class="sxs-lookup"><span data-stu-id="b0b78-111">Create an interface for the service and apply the <xref:System.ServiceModel.ServiceContractAttribute> attribute to the interface.</span></span>  
  
2. <span data-ttu-id="b0b78-112">將方法宣告加入至介面。</span><span class="sxs-lookup"><span data-stu-id="b0b78-112">Add a method declaration to the interface.</span></span>  
  
3. <span data-ttu-id="b0b78-113">將 <xref:System.ServiceModel.OperationContractAttribute> 屬性 (Attribute) 套用至方法，並且將 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 屬性 (Property) 設為 <xref:System.Net.Security.ProtectionLevel.Sign>，如以下程式碼中所示。</span><span class="sxs-lookup"><span data-stu-id="b0b78-113">Apply the <xref:System.ServiceModel.OperationContractAttribute> attribute to the method, and set the <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> property to <xref:System.Net.Security.ProtectionLevel.Sign>, as shown in the following code.</span></span>  
  
     [!code-csharp[C_ProtectionLevel#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#2)]
     [!code-vb[C_ProtectionLevel#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#2)]  
  
## <a name="protecting-fault-messages"></a><span data-ttu-id="b0b78-114">保護錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="b0b78-114">Protecting Fault Messages</span></span>  

 <span data-ttu-id="b0b78-115">在服務上擲回的例外狀況可以當成 SOAP 錯誤傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="b0b78-115">Exceptions that are thrown on a service can be sent to a client as SOAP faults.</span></span> <span data-ttu-id="b0b78-116">如需有關建立強型別錯誤的詳細資訊，請參閱 [指定和處理合約和服務中的錯誤](specifying-and-handling-faults-in-contracts-and-services.md) 以及 [如何：在服務合約中宣告錯誤](how-to-declare-faults-in-service-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="b0b78-116">For more information about creating strongly typed faults, see [Specifying and Handling Faults in Contracts and Services](specifying-and-handling-faults-in-contracts-and-services.md) and [How to: Declare Faults in Service Contracts](how-to-declare-faults-in-service-contracts.md).</span></span>  
  
#### <a name="to-protect-a-fault-message"></a><span data-ttu-id="b0b78-117">保護錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="b0b78-117">To protect a fault message</span></span>  
  
1. <span data-ttu-id="b0b78-118">建立表示錯誤訊息的類型。</span><span class="sxs-lookup"><span data-stu-id="b0b78-118">Create a type that represents the fault message.</span></span> <span data-ttu-id="b0b78-119">以下範例將建立名為 `MathFault` 的類別，其中包含兩個欄位。</span><span class="sxs-lookup"><span data-stu-id="b0b78-119">The following example creates a class named `MathFault` with two fields.</span></span>  
  
2. <span data-ttu-id="b0b78-120">將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至類型，並且將 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性套用至應序列化的每一個欄位，如以下程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="b0b78-120">Apply the <xref:System.Runtime.Serialization.DataContractAttribute> attribute to the type and a <xref:System.Runtime.Serialization.DataMemberAttribute> attribute to each field that should be serialized, as shown in the following code.</span></span>  
  
     [!code-csharp[C_ProtectionLevel#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#3)]
     [!code-vb[C_ProtectionLevel#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#3)]  
  
3. <span data-ttu-id="b0b78-121">在傳回錯誤的介面中，將 <xref:System.ServiceModel.FaultContractAttribute> 屬性套用至傳回錯誤的方法，並且將 `detailType` 參數設為錯誤類別的類型。</span><span class="sxs-lookup"><span data-stu-id="b0b78-121">In the interface that will return the fault, apply the <xref:System.ServiceModel.FaultContractAttribute> attribute to the method that will return the fault and set the `detailType` parameter to the type of the fault class.</span></span>  
  
4. <span data-ttu-id="b0b78-122">同時，在建構函式中，將 <xref:System.ServiceModel.FaultContractAttribute.ProtectionLevel%2A> 屬性設為 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>，如以下程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="b0b78-122">Also in the constructor, set the <xref:System.ServiceModel.FaultContractAttribute.ProtectionLevel%2A> property to <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>, as shown in the following code.</span></span>  
  
     [!code-csharp[C_ProtectionLevel#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#4)]
     [!code-vb[C_ProtectionLevel#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#4)]  
  
## <a name="protecting-message-parts"></a><span data-ttu-id="b0b78-123">保護訊息部分</span><span class="sxs-lookup"><span data-stu-id="b0b78-123">Protecting Message Parts</span></span>  

 <span data-ttu-id="b0b78-124">使用訊息合約保護訊息的部分。</span><span class="sxs-lookup"><span data-stu-id="b0b78-124">Use a message contract to protect parts of a message.</span></span> <span data-ttu-id="b0b78-125">如需訊息合約的詳細資訊，請參閱 [使用訊息合約](./feature-details/using-message-contracts.md)。</span><span class="sxs-lookup"><span data-stu-id="b0b78-125">For more information about message contracts, see [Using Message Contracts](./feature-details/using-message-contracts.md).</span></span>  
  
#### <a name="to-protect-a-message-body"></a><span data-ttu-id="b0b78-126">保護訊息本文</span><span class="sxs-lookup"><span data-stu-id="b0b78-126">To protect a message body</span></span>  
  
1. <span data-ttu-id="b0b78-127">建立表示訊息的類型。</span><span class="sxs-lookup"><span data-stu-id="b0b78-127">Create a type that represents the message.</span></span> <span data-ttu-id="b0b78-128">以下範例將建立 `Company` 類別，其中包含兩個欄位 `CompanyName` 和 `CompanyID`。</span><span class="sxs-lookup"><span data-stu-id="b0b78-128">The following example creates a `Company` class with two fields, `CompanyName` and `CompanyID`.</span></span>  
  
2. <span data-ttu-id="b0b78-129">將 <xref:System.ServiceModel.MessageContractAttribute> 屬性 (Attribute) 套用至類別，並且將 <xref:System.ServiceModel.MessageContractAttribute.ProtectionLevel%2A> 屬性 (Property) 設為 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>。</span><span class="sxs-lookup"><span data-stu-id="b0b78-129">Apply the <xref:System.ServiceModel.MessageContractAttribute> attribute to the class and set the <xref:System.ServiceModel.MessageContractAttribute.ProtectionLevel%2A> property to <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>.</span></span>  
  
3. <span data-ttu-id="b0b78-130">將 <xref:System.ServiceModel.MessageHeaderAttribute> 屬性 (Attribute) 套用以訊息標頭表示的欄位，並且將 `ProtectionLevel` 屬性 (Property) 設為 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>。</span><span class="sxs-lookup"><span data-stu-id="b0b78-130">Apply the <xref:System.ServiceModel.MessageHeaderAttribute> attribute to a field that will be expressed as a message header and set the `ProtectionLevel` property to <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>.</span></span>  
  
4. <span data-ttu-id="b0b78-131">將套用 <xref:System.ServiceModel.MessageBodyMemberAttribute> 至將表示為訊息主體一部分的任何欄位，並將 `ProtectionLevel` 屬性設定為 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> ，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="b0b78-131">Apply the <xref:System.ServiceModel.MessageBodyMemberAttribute> to any field that will be expressed as part of the message body, and set the `ProtectionLevel` property to <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>, as shown in the following example.</span></span>  
  
     [!code-csharp[C_ProtectionLevel#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#5)]
     [!code-vb[C_ProtectionLevel#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#5)]  
  
## <a name="example"></a><span data-ttu-id="b0b78-132">範例</span><span class="sxs-lookup"><span data-stu-id="b0b78-132">Example</span></span>  

 <span data-ttu-id="b0b78-133">以下範例會在服務中的不同位置，設定數個屬性 (Attribute) 類別的 `ProtectionLevel` 屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="b0b78-133">The following example sets the `ProtectionLevel` property of several attribute classes at various places in a service.</span></span>  
  
 [!code-csharp[C_ProtectionLevel#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#6)]
 [!code-vb[C_ProtectionLevel#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#6)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="b0b78-134">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="b0b78-134">Compiling the Code</span></span>  

 <span data-ttu-id="b0b78-135">以下範例示範編譯範例程式碼所需的命名空間。</span><span class="sxs-lookup"><span data-stu-id="b0b78-135">The following code shows the namespaces required to compile the example code.</span></span>  
  
 [!code-csharp[C_ProtectionLevel#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#0)]
 [!code-vb[C_ProtectionLevel#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#0)]  
  
## <a name="see-also"></a><span data-ttu-id="b0b78-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b0b78-136">See also</span></span>

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.MessageContractAttribute>
- <xref:System.ServiceModel.MessageBodyMemberAttribute>
- [<span data-ttu-id="b0b78-137">了解保護層級</span><span class="sxs-lookup"><span data-stu-id="b0b78-137">Understanding Protection Level</span></span>](understanding-protection-level.md)
