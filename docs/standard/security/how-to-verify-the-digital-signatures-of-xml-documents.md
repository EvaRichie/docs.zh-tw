---
title: 作法：驗證 XML 文件的數位簽章
ms.date: 07/14/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.SignedXml class
- signatures, cryptographic
- System.Security.Cryptography.RSA class
- verifying signatures
- checking signatures
- XML digital signatures
- digital signatures, verifying
ms.assetid: a4d5ceb1-b9f5-47e8-9e4a-a2b39110002f
ms.openlocfilehash: b9b2dc6a558d1fd6acd2922a7c8ad82ce8776c26
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557043"
---
# <a name="how-to-verify-the-digital-signatures-of-xml-documents"></a>作法：驗證 XML 文件的數位簽章

您可以使用 <xref:System.Security.Cryptography.Xml> 命名空間中的類別，驗證使用數位簽章簽署的 XML 資料。 XML 數位簽章 (XMLDSIG) 可讓您驗證在簽署資料後，資料未經過變更。 如需 XMLDSIG 標準的詳細資訊，請參閱全球資訊網協會 (W3C) 規格，網址為 <https://www.w3.org/TR/xmldsig-core/> 。
  
> [!NOTE]
> 本文中的程式碼適用于 Windows。

此程式中的程式碼範例示範如何驗證封裝含在 <> 元素中的 XML 數位簽章 `Signature` 。  範例會從金鑰容器擷取 RSA 公開金鑰，然後使用金鑰來驗證簽章。  
  
如需如何使用這項技術來建立可驗證之數位簽章的相關資訊，請參閱[如何：使用數位簽章簽署 XML 檔](how-to-sign-xml-documents-with-digital-signatures.md)。  
  
### <a name="to-verify-the-digital-signature-of-an-xml-document"></a>驗證 XML 文件的數位簽章  
  
1. 若要驗證文件，您必須使用用於簽章的相同非對稱金鑰。  建立 <xref:System.Security.Cryptography.CspParameters> 物件，並指定用於簽章的金鑰容器名稱。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#2)]  
  
2. 使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別擷取公用金鑰。  當您將 <xref:System.Security.Cryptography.CspParameters> 物件傳遞到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 類別的建構函式時，金鑰會自動依名稱從金鑰容器載入。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#3)]  
  
3. 藉由從磁碟載入 XML 檔案，建立 <xref:System.Xml.XmlDocument> 物件。  <xref:System.Xml.XmlDocument> 物件包含要驗證的已簽署 XML 文件。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#4)]  
  
4. 建立新的 <xref:System.Security.Cryptography.Xml.SignedXml> 物件，並傳遞 <xref:System.Xml.XmlDocument> 物件給它。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#5)]  
  
5. 尋找 <`signature`> 元素，並建立新的 <xref:System.Xml.XmlNodeList> 物件。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#6)]  
  
6. 將第一個 <> 元素的 XML 載入 `signature` 至 <xref:System.Security.Cryptography.Xml.SignedXml> 物件。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#7)]  
  
7. 使用 <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignature%2A> 方法和 RSA 公開金鑰檢查簽章。  這個方法會傳回表示成功或失敗的布林值。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#8)]  
  
## <a name="example"></a>範例

這個範例假設名為 `"test.xml"` 的檔案已存在於和編譯程式相同的目錄中。  檔案 `"test.xml"` 必須使用[如何：使用數位簽章簽署 XML](how-to-sign-xml-documents-with-digital-signatures.md)檔中所述的技術來簽署。  
  
[!code-csharp[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#1)]
[!code-vb[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>編譯程式碼  
  
- 在以 .NET Framework 為目標的專案中，包含的參考 `System.Security.dll` 。

- 在以 .NET Core 或 .NET 5 為目標的專案中，安裝 NuGet 封裝[System.Security.Cryptography.Xml](https://www.nuget.org/packages/System.Security.Cryptography.Xml)。
  
- 包含下列命名空間：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## <a name="net-security"></a>.NET 安全性

絕對不要以純文字儲存或傳輸非對稱金鑰組的私密金鑰。  如需對稱和非對稱密碼編譯金鑰的詳細資訊，請參閱[產生加密和解密的金鑰](generating-keys-for-encryption-and-decryption.md)。  
  
絕對不要直接將私密金鑰內嵌在您的原始程式碼。  您可以使用[Ildasm.exe (IL](../../framework/tools/ildasm-exe-il-disassembler.md)解譯器) 或在文字編輯器（如 [記事本]）中開啟元件，輕鬆地從元件中讀取內嵌索引鍵。  
  
## <a name="see-also"></a>另請參閱

- [密碼編譯模型](cryptography-model.md)
- [密碼編譯服務](cryptographic-services.md)
- [跨平臺密碼編譯](cross-platform-cryptography.md)
- <xref:System.Security.Cryptography.Xml>
- [作法：使用數位簽章簽署 XML 文件](how-to-sign-xml-documents-with-digital-signatures.md)
- [ASP.NET Core 資料保護](/aspnet/core/security/data-protection/introduction)
