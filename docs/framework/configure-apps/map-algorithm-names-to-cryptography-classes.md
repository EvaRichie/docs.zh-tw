---
title: 將演算法名稱對應至密碼編譯類別
description: 將演算法名稱對應至 .NET 中的密碼編譯類別。 開發人員有四個選項可建立密碼編譯物件。
ms.date: 03/30/2017
helpviewer_keywords:
- mapping algorithm names
- cryptography, mapping algorithm names
- cryptographic algorithms
- names [.NET Framework], algorithm mapping
ms.assetid: 01327c69-c5e1-4ef6-b73f-0a58351f0492
ms.openlocfilehash: b67db612496e56a341dab2e5fc4b52c954ff02b4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183386"
---
# <a name="mapping-algorithm-names-to-cryptography-classes"></a><span data-ttu-id="96718-104">將演算法名稱對應至密碼編譯類別</span><span class="sxs-lookup"><span data-stu-id="96718-104">Mapping Algorithm Names to Cryptography Classes</span></span>

<span data-ttu-id="96718-105">有四種方式可供開發人員使用 Windows SDK 建立密碼編譯物件：</span><span class="sxs-lookup"><span data-stu-id="96718-105">There are four ways a developer can create a cryptography object using the Windows SDK:</span></span>  
  
- <span data-ttu-id="96718-106">使用 **new** 運算子建立物件。</span><span class="sxs-lookup"><span data-stu-id="96718-106">Create an object by using the **new** operator.</span></span>  
  
- <span data-ttu-id="96718-107">藉由在該演算法的抽象類別上呼叫 **Create** 方法，建立可執行特定密碼編譯演算法的物件。</span><span class="sxs-lookup"><span data-stu-id="96718-107">Create an object that implements a particular cryptography algorithm by calling the **Create** method on the abstract class for that algorithm.</span></span>  
  
- <span data-ttu-id="96718-108">藉由呼叫方法，建立可執行特定密碼編譯演算法的物件 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="96718-108">Create an object that implements a particular cryptography algorithm by calling the <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> method.</span></span>  
  
- <span data-ttu-id="96718-109">建立物件，該物件會執行密碼編譯演算法的類別 (例如對稱封鎖密碼) ，方法是在該類型 (演算法的抽象類別上呼叫 **Create** 方法，例如 <xref:System.Security.Cryptography.SymmetricAlgorithm>) 。</span><span class="sxs-lookup"><span data-stu-id="96718-109">Create an object that implements a class of cryptographic algorithms (such as a symmetric block cipher) by calling the **Create** method on the abstract class for that type of algorithm (such as <xref:System.Security.Cryptography.SymmetricAlgorithm>).</span></span>  
  
 <span data-ttu-id="96718-110">例如，假設開發人員想要計算一組位元組的 SHA1 雜湊。</span><span class="sxs-lookup"><span data-stu-id="96718-110">For example, suppose a developer wants to compute the SHA1 hash of a set of bytes.</span></span> <span data-ttu-id="96718-111"><xref:System.Security.Cryptography>命名空間包含兩個 SHA1 演算法的實作為，一個純粹受控的實作為一個包裝 CryptoAPI。</span><span class="sxs-lookup"><span data-stu-id="96718-111">The <xref:System.Security.Cryptography> namespace contains two implementations of the SHA1 algorithm, one purely managed implementation and one that wraps CryptoAPI.</span></span> <span data-ttu-id="96718-112">開發人員可以藉 <xref:System.Security.Cryptography.SHA1Managed> 由呼叫 **new** 運算子，選擇具現化特定的 SHA1 實 (，例如) 。</span><span class="sxs-lookup"><span data-stu-id="96718-112">The developer can choose to instantiate a particular SHA1 implementation (such as the <xref:System.Security.Cryptography.SHA1Managed>) by calling the **new** operator.</span></span> <span data-ttu-id="96718-113">但是，如果 common language runtime 所載入的類別不重要，只要該類別會執行 SHA1 雜湊演算法，開發人員就可以藉由呼叫方法來建立物件 <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="96718-113">However, if it does not matter which class the common language runtime loads as long as the class implements the SHA1 hash algorithm, the developer can create an object by calling the <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="96718-114">這個方法會呼叫 \*\*cryptoconfig.createfromname. CreateFromName ( "system.string" ) \*\*，它必須傳回 SHA1 雜湊演算法的實值。</span><span class="sxs-lookup"><span data-stu-id="96718-114">This method calls **System.Security.Cryptography.CryptoConfig.CreateFromName("System.Security.Cryptography.SHA1")**, which must return an implementation of the SHA1 hash algorithm.</span></span>  
  
 <span data-ttu-id="96718-115">開發人員也可以呼叫 \*\*cryptoconfig.createfromname. CreateFromName ( "SHA1" ) \*\* 因為在預設的情況下，密碼編譯設定包含 .NET Framework 所隨附演算法的簡短名稱。</span><span class="sxs-lookup"><span data-stu-id="96718-115">The developer can also call **System.Security.Cryptography.CryptoConfig.CreateFromName("SHA1")** because, by default, cryptography configuration includes short names for the algorithms shipped in the .NET Framework.</span></span>  
  
 <span data-ttu-id="96718-116">如果使用哪一個雜湊演算法並不重要，開發人員可以呼叫 <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> 方法，以傳回可執行雜湊轉換的物件。</span><span class="sxs-lookup"><span data-stu-id="96718-116">If it does not matter which hash algorithm is used, the developer can call the <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> method, which returns an object that implements a hashing transformation.</span></span>  
  
## <a name="mapping-algorithm-names-in-configuration-files"></a><span data-ttu-id="96718-117">在設定檔中對應演算法名稱</span><span class="sxs-lookup"><span data-stu-id="96718-117">Mapping Algorithm Names in Configuration Files</span></span>  

 <span data-ttu-id="96718-118">依預設，執行時間會傳回 <xref:System.Security.Cryptography.SHA1CryptoServiceProvider> 所有四個案例的物件。</span><span class="sxs-lookup"><span data-stu-id="96718-118">By default, the runtime returns a <xref:System.Security.Cryptography.SHA1CryptoServiceProvider> object for all four scenarios.</span></span> <span data-ttu-id="96718-119">但是，電腦系統管理員可以變更最後兩個案例中的方法所傳回的物件類型。</span><span class="sxs-lookup"><span data-stu-id="96718-119">However, a machine administrator can change the type of object that the methods in the last two scenarios return.</span></span> <span data-ttu-id="96718-120">若要這樣做，您必須將易記的演算法名稱對應至您要在電腦設定檔中使用的類別 ( # A0) 。</span><span class="sxs-lookup"><span data-stu-id="96718-120">To do this, you must map a friendly algorithm name to the class you want to use in the machine configuration file (Machine.config).</span></span>  
  
 <span data-ttu-id="96718-121">下列範例會示範如何設定執行時間，以便 **建立** \*\*cryptoconfig.createfromname. CREATEFROMNAME ( "SHA1" ) \*\*，以及 **HashAlgorithm..** 會傳回一個物件的方法，如下所示 `MySHA1HashClass` 。</span><span class="sxs-lookup"><span data-stu-id="96718-121">The following example shows how to configure the runtime so that **System.Security.Cryptography.SHA1.Create**, **System.Security.CryptoConfig.CreateFromName("SHA1")**, and **System.Security.Cryptography.HashAlgorithm.Create** return a `MySHA1HashClass` object.</span></span>  
  
```xml  
<configuration>  
   <!-- Other configuration settings. -->  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MySHA1Hash="MySHA1HashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="SHA1" class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.SHA1"  
                       class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MySHA1Hash"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 <span data-ttu-id="96718-122">您可以在 [<>cryptoclass \> 元素](./file-schema/cryptography/cryptoclass-element.md) 中指定屬性的名稱， (先前的範例將屬性命名為 `MySHA1Hash`) 。</span><span class="sxs-lookup"><span data-stu-id="96718-122">You can specify the name of the attribute in the [<cryptoClass\> element](./file-schema/cryptography/cryptoclass-element.md) (the previous example names the attribute `MySHA1Hash`).</span></span> <span data-ttu-id="96718-123">專案中的屬性值 **\<cryptoClass>** 是通用語言執行時間用來尋找類別的字串。</span><span class="sxs-lookup"><span data-stu-id="96718-123">The value of the attribute in the **\<cryptoClass>** element is a string that the common language runtime uses to find the class.</span></span> <span data-ttu-id="96718-124">您可以使用符合指定 [完整型別名稱](../reflection-and-codedom/specifying-fully-qualified-type-names.md)所指定之需求的任何字串。</span><span class="sxs-lookup"><span data-stu-id="96718-124">You can use any string that meets the requirements specified in [Specifying Fully Qualified Type Names](../reflection-and-codedom/specifying-fully-qualified-type-names.md).</span></span>  
  
 <span data-ttu-id="96718-125">許多演算法名稱都可以對應到相同的類別。</span><span class="sxs-lookup"><span data-stu-id="96718-125">Many algorithm names can map to the same class.</span></span> <span data-ttu-id="96718-126">[ \<nameEntry> 元素](./file-schema/cryptography/nameentry-element.md)會將類別對應至一個易記的演算法名稱。</span><span class="sxs-lookup"><span data-stu-id="96718-126">The [\<nameEntry> element](./file-schema/cryptography/nameentry-element.md) maps a class to one friendly algorithm name.</span></span> <span data-ttu-id="96718-127">**Name**屬性可以是在命名空間中呼叫**cryptoconfig.createfromname. CreateFromName**方法或抽象密碼編譯類別的名稱時，所使用的字串。 <xref:System.Security.Cryptography></span><span class="sxs-lookup"><span data-stu-id="96718-127">The **name** attribute can be either a string that is used when calling the **System.Security.Cryptography.CryptoConfig.CreateFromName** method or the name of an abstract cryptography class in the <xref:System.Security.Cryptography> namespace.</span></span> <span data-ttu-id="96718-128">**類別**屬性的值是元素中的屬性名稱 **\<cryptoClass>** 。</span><span class="sxs-lookup"><span data-stu-id="96718-128">The value of the **class** attribute is the name of the attribute in the **\<cryptoClass>** element.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="96718-129">您可以藉由呼叫 <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> 或 \*\*Cryptoconfig.createfromname. CreateFromName ( "sha1" ) \*\* 方法來取得 SHA1 演算法。</span><span class="sxs-lookup"><span data-stu-id="96718-129">You can get an SHA1 algorithm by calling the <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> or the **Security.CryptoConfig.CreateFromName("SHA1")** method.</span></span> <span data-ttu-id="96718-130">每個方法都可保證它會傳回可執行 SHA1 演算法的物件。</span><span class="sxs-lookup"><span data-stu-id="96718-130">Each method guarantees only that it returns an object that implements the SHA1 algorithm.</span></span> <span data-ttu-id="96718-131">您不需要將演算法的每個易記名稱對應至設定檔中的相同類別。</span><span class="sxs-lookup"><span data-stu-id="96718-131">You do not have to map each friendly name of an algorithm to the same class in the configuration file.</span></span>  
  
 <span data-ttu-id="96718-132">如需預設名稱及其對應類別的清單，請參閱 <xref:System.Security.Cryptography.CryptoConfig> 。</span><span class="sxs-lookup"><span data-stu-id="96718-132">For a list of default names and the classes they map to, see <xref:System.Security.Cryptography.CryptoConfig>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="96718-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="96718-133">See also</span></span>

- [<span data-ttu-id="96718-134">密碼編譯服務</span><span class="sxs-lookup"><span data-stu-id="96718-134">Cryptographic Services</span></span>](../../standard/security/cryptographic-services.md)
- [<span data-ttu-id="96718-135">設定密碼編譯類別</span><span class="sxs-lookup"><span data-stu-id="96718-135">Configuring Cryptography Classes</span></span>](configure-cryptography-classes.md)
