---
title: 作法：使用非對稱金鑰加密 XML 元素
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [.NET], asymmetric keys
- AES algorithm
- System.Security.Cryptography.RSA class
- asymmetric keys [.NET]
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- key containers
- Advanced Encryption Standard algorithm
- encryption [.NET], asymmetric keys
ms.assetid: a164ba4f-e596-4bbe-a9ca-f214fe89ed48
ms.openlocfilehash: 1c824b00a1df920108cfcd8c4590b680020cdf3e
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555783"
---
# <a name="how-to-encrypt-xml-elements-with-asymmetric-keys"></a>作法：使用非對稱金鑰加密 XML 元素

您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別來加密 XML 文件內的項目。  XML 加密是交換或儲存加密 XML 資料的標準方法，不必擔心資料被輕易讀取。  如需 XML 加密標準的詳細資訊，請參閱全球資訊網協會 (W3C) XML 加密的規格，位於 <https://www.w3.org/TR/xmldsig-core/> 。  
  
 您可以使用 XML 加密將任何 XML 元素或文件取代為包含加密 XML 資料的 <`EncryptedData`> 元素。  <`EncryptedData`> 元素也可以包含子項目，其中包含加密期間所使用之金鑰和進程的相關資訊。  XML 加密可讓文件中包含多個加密的元素，並允許元素加密多次。  此程式中的程式碼範例會示範如何建立 <`EncryptedData`> 專案，以及您稍後可以在解密期間使用的其他幾個子項目。  
  
 此範例會使用兩個金鑰來加密 XML 元素。  它會產生 RSA 公開/私密金鑰組，並將金鑰組儲存到安全的金鑰容器。  然後，此範例會使用進階加密標準 (AES) 演算法來建立個別的工作階段金鑰。  範例會使用 AES 工作階段金鑰來加密 XML 文件，然後使用 RSA 公開金鑰來加密 AES 工作階段金鑰。  最後，此範例會將加密的 AES 工作階段金鑰和加密的 XML 資料，儲存至新 <> 元素內的 XML 檔 `EncryptedData` 。  
  
 若要解密 XML 項目，您可以從金鑰容器中擷取 RSA 私密金鑰、用它來解密工作階段金鑰，然後使用工作階段金鑰來解密文件。  如需如何解密使用此程式加密之 XML 元素的詳細資訊，請參閱[如何：使用非對稱金鑰解密 Xml 元素](how-to-decrypt-xml-elements-with-asymmetric-keys.md)。  
  
 這個範例適合多個應用程式需要共用加密資料或應用程式需要在它執行時間之間儲存加密資料的情況。
  
### <a name="to-encrypt-an-xml-element-with-an-asymmetric-key"></a>使用非對稱金鑰加密 XML 項目  
  
1. 建立 <xref:System.Security.Cryptography.CspParameters> 物件，並指定金鑰容器的名稱。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2. 使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別產生對稱金鑰。  當您將 <xref:System.Security.Cryptography.CspParameters> 物件傳遞到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別的建構函式時，金鑰會自動儲存到金鑰容器。  這個金鑰會用來加密 AES 工作階段金鑰，而且可以稍後擷取來進行解密。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3. 藉由從磁碟載入 XML 檔案，建立 <xref:System.Xml.XmlDocument> 物件。  <xref:System.Xml.XmlDocument> 物件會包含要加密的 XML 項目。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#4)]  
  
4. 在 <xref:System.Xml.XmlDocument> 物件中尋找指定的項目，並建立新的 <xref:System.Xml.XmlElement> 物件以代表您想要加密的項目。 在此範例中，`"creditcard"` 元素已加密。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
5. 使用 <xref:System.Security.Cryptography.Aes> 類別建立新的工作階段金鑰。  這個金鑰會加密 XML 項目，並再加密本身並放在 XML 文件中。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
6. 建立 <xref:System.Security.Cryptography.Xml.EncryptedXml> 類別的新執行個體，並使用它使用工作階段金鑰加密指定的項目。  <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> 方法會以加密位元組陣列傳回已加密的項目。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
7. 建構 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件並填入加密 XML 項目的 URL 識別項。  這個 URL 識別項可讓解密的一方知道 XML 包含加密的項目。  您可以使用 <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> 欄位來指定 URL 識別項。  純文字 XML 專案將由 `EncryptedData` 這個物件所封裝的 <> 元素所取代 <xref:System.Security.Cryptography.Xml.EncryptedData> 。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
8. 建立 <xref:System.Security.Cryptography.Xml.EncryptionMethod> 物件，它會初始化為用來產生工作階段金鑰之密碼編譯演算法的 URL 識別項。  將 <xref:System.Security.Cryptography.Xml.EncryptionMethod> 物件傳遞至 <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A> 屬性。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#9)]  
  
9. 建立 <xref:System.Security.Cryptography.Xml.EncryptedKey> 物件，以包含加密工作階段金鑰。  加密工作階段金鑰、將它加入 <xref:System.Security.Cryptography.Xml.EncryptedKey> 物件，然後輸入工作階段金鑰名稱和金鑰識別項 URL。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#10)]  
  
10. 建立新的 <xref:System.Security.Cryptography.Xml.DataReference> 物件，將加密的資料對應至特定工作階段金鑰。  此選用步驟可讓您輕鬆地指定 XML 文件的多個部分是由單一金鑰加密。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#11)]  
  
11. 將加密的金鑰加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#12)]  
  
12. 建立新的 <xref:System.Security.Cryptography.Xml.KeyInfo> 物件，指定 RSA 金鑰的名稱。  將它加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。 這有助於解密方識別要解密工作階段金鑰時所使用的正確非對稱金鑰。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#13)]  
  
13. 將加密項目資料加入 <xref:System.Security.Cryptography.Xml.EncryptedData> 物件。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#14)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#14)]  
  
14. 將來自原始 <xref:System.Xml.XmlDocument> 物件的項目取代為 <xref:System.Security.Cryptography.Xml.EncryptedData> 項目。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#15)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#15)]  
  
15. 儲存 <xref:System.Xml.XmlDocument> 物件。  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#16)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#16)]  
  
## <a name="example"></a>範例  
 這個範例假設名為 `"test.xml"` 的檔案已存在於和編譯程式相同的目錄中。  它同時也假設 `"test.xml"` 包含 `"creditcard"` 元素。  您可以將下列 XML 放入稱為 `test.xml` 的檔案，並使用它搭配此範例。  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
  
- 在以 .NET Framework 為目標的專案中，包含的參考 `System.Security.dll` 。

- 在以 .NET Core 或 .NET 5 為目標的專案中，安裝 NuGet 封裝[System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml)。
  
- 包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## <a name="net-security"></a>.NET 安全性

絕對不要以純文字儲存對稱密碼編譯金鑰，或以純文字格式在電腦之間傳輸對稱金鑰。  此外，絕對不要以純文字儲存或傳輸非對稱金鑰組的私密金鑰。  如需對稱和非對稱密碼編譯金鑰的詳細資訊，請參閱[產生加密和解密的金鑰](generating-keys-for-encryption-and-decryption.md)。  
  
絕對不要直接將金鑰內嵌在您的原始程式碼。  您可以使用[Ildasm.exe (IL](../../framework/tools/ildasm-exe-il-disassembler.md)解譯器) 或在文字編輯器（如 [記事本]）中開啟元件，輕鬆地從元件中讀取內嵌索引鍵。  
  
當您使用完密碼編譯金鑰，請從記憶體清除它，方法是將每個位元組設定為零，或呼叫 Managed 密碼編譯類別的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法。  偵錯工具有時可以從記憶體讀取密碼編譯金鑰，或是在記憶體位置被分頁至磁碟的情況下從硬碟機讀取。  
  
## <a name="see-also"></a>另請參閱

- [密碼編譯模型](cryptography-model.md)
- [密碼編譯服務](cryptographic-services.md)
- [跨平臺密碼編譯](cross-platform-cryptography.md)- <xref:System.Security.Cryptography.Xml>
- [作法：使用非對稱金鑰解密 XML 元素](how-to-decrypt-xml-elements-with-asymmetric-keys.md)
- [ASP.NET Core 資料保護](/aspnet/core/security/data-protection/introduction)
