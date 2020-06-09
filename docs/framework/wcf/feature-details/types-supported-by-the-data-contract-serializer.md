---
title: 資料合約序列化程式支援的型別
ms.date: 03/30/2017
helpviewer_keywords:
- serialization [WCF], supported types
ms.assetid: 7381b200-437a-4506-9556-d77bf1bc3f34
ms.openlocfilehash: 15c3cda8329682fcbaa36609647ec49de7eb3c37
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595098"
---
# <a name="types-supported-by-the-data-contract-serializer"></a>資料合約序列化程式支援的型別

Windows Communication Foundation （WCF）會使用 <xref:System.Runtime.Serialization.DataContractSerializer> 做為其預設的序列化引擎，將資料轉換為 xml 並將 XML 轉換回資料。 <xref:System.Runtime.Serialization.DataContractSerializer> 主要是用來序列化「 *資料合約* 」(Data Contract) 型別。 但是，它支援其他許多型別，而您可將這些視為擁有隱含資料合約。 下列是可以序列化的完整型別清單：

- 所有具有不含任何參數之建構函式的公開可見型別。

- 資料合約型別： 這些是可以套用 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性的型別。 一般來說，代表商務物件的新自訂型別應該建立為資料合約型別。 如需詳細資訊，請參閱[使用資料合約](using-data-contracts.md)和[可序列化類型](serializable-types.md)。

- 集合型別： 這些是代表資料清單的型別。 這些可以是正常的型別陣列，或集合型別，例如 <xref:System.Collections.ArrayList> 和 <xref:System.Collections.Generic.Dictionary%602>。 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 屬性可以用來自訂這些型別的序列化 (但非必要)。 如需詳細資訊，請參閱[資料合約中的集合類型](collection-types-in-data-contracts.md)。

- 列舉型別： 列舉 (包括旗標列舉) 都是可序列化的型別。 或者，您也可以使用 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性來標示列舉型別，這樣一來，參與序列化的每個成員就必須加上 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性標示。 未標示的成員不會序列化。 如需詳細資訊，請參閱[資料合約中的列舉類型](enumeration-types-in-data-contracts.md)。

- .NET Framework 基本型別： 下列建置在 .NET Framework 中的型別都可以加以序列化並視為基本型別 (Primitive Type)： <xref:System.Byte>、 <xref:System.SByte>、 <xref:System.Int16>、 <xref:System.Int32>、 <xref:System.Int64>、 <xref:System.UInt16>、 <xref:System.UInt32>、 <xref:System.UInt64>、 <xref:System.Single>、 <xref:System.Double>、 <xref:System.Boolean>、 <xref:System.Char>、 <xref:System.Decimal>、 <xref:System.Object>和 <xref:System.String>。

- 其他基本型別： 這些型別並不是 .NET Framework 中的基本型別，但會被視為已序列化之 XML 形式的基本型別。 這些型別是 <xref:System.DateTime>、 <xref:System.DateTimeOffset>、 <xref:System.TimeSpan>、 <xref:System.Guid>、 <xref:System.Uri>、 <xref:System.Xml.XmlQualifiedName>和 <xref:System.Byte>的陣列。

  > [!NOTE]
  > 與其他基本型別不同的是，預設 <xref:System.DateTimeOffset> 不是已知型別 ( 如需詳細資訊，請參閱[資料合約已知類型](data-contract-known-types.md)）。

- 以 <xref:System.SerializableAttribute> 屬性標示的型別。 包含在 .NET Framework 基類程式庫中的許多類型都屬於此類別。 <xref:System.Runtime.Serialization.DataContractSerializer> 充分支援原本由 .NET Framework 遠端處理所使用的序列化程式設計模型，亦即 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>以及 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>(包含對 <xref:System.Runtime.Serialization.ISerializable> 介面的支援)。

- 代表原始 XML 的類型，或代表 ADO.NET 關聯式資料的類型。 支援 <xref:System.Xml.XmlElement> 型別和 <xref:System.Xml.XmlNode> 型別的陣列以直接代表 XML。 另外亦支援實作 <xref:System.Xml.Serialization.IXmlSerializable> 介面的型別，包括相關的 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 屬性，以及 <xref:System.Xml.Linq.XDocument> 和 <xref:System.Xml.Linq.XElement> 型別。 ADO.NET <xref:System.Data.DataTable> 類型和 <xref:System.Data.DataSet> 類型（以及其具類型的衍生類別）都會執行 <xref:System.Xml.Serialization.IXmlSerializable> 介面，因此符合此分類。 如需詳細資訊，請參閱[資料合約中的 XML 和 ADO.NET 類型](xml-and-ado-net-types-in-data-contracts.md)。

## <a name="limitations-of-using-certain-types-in-partial-trust-mode"></a>在部分信任模式中使用特定型別的限制

下列是在部分信任模式案例中使用特定型別的限制清單：

- 若要在部分信任程式碼中，透過 <xref:System.Runtime.Serialization.ISerializable> 序列化或還原序列化可實作 <xref:System.Runtime.Serialization.DataContractSerializer> 的型別需要 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter%2A> 和 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> 權限。

- 在[部分信任](partial-trust.md)模式下執行 WCF 程式碼時，不支援欄位的序列化和還原序列化 `readonly` （ `public` 和兩者 `private` ）。 這是因為產生的 IL 無法加以驗證，因此需要較高的權限。

- 部分信任環境同時支援 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer> 。 然而， <xref:System.Runtime.Serialization.DataContractSerializer> 的使用需視下列情況而定：

  - 所有可序列化的 `[DataContract]` 型別必須是公用的。

  - `[DataMember]` 型別中所有可序列化的 `[DataContract]` 欄位或屬性必須具有公用和讀/寫性質。 `readonly`在部分信任的應用程式中執行 WCF 時，不支援欄位的序列化和還原序列化。

  - 支援 `[Serializable]`/`ISerializable]` 程式設計模型。

  - 已知型別必須在程式碼或電腦層級組態 (`Machine.config`) 中指定。 為了安全起見，已知型別無法在應用程式層級的組態中指定。

- 在部分信任環境中，可實作 <xref:System.Runtime.Serialization.IObjectReference> 的型別會擲回例外狀況，因為 <xref:System.Runtime.Serialization.IObjectReference.GetRealObject%2A> 方法需要安全性權限 `[SecurityPermission(SecurityAction.LinkDemand, Flags=SecurityPermissionFlag.SerializationFormatter)]`。

## <a name="additional-notes-on-serialization"></a>其他序列化注意事項

下列規則也適用於「資料合約序列化程式」支援的型別：

- 資料合約序列化程式完全支援泛型型別。

- 資料合約序列化程式完全支援可為 null 的實數值型別。

- 介面型別會被視為 <xref:System.Object> 或是集合型別 (在集合介面的案例中)。

- 同時支援結構與類別。

- 不 <xref:System.Runtime.Serialization.DataContractSerializer> 支援 <xref:System.Xml.Serialization.XmlSerializer> 和 ASP.NET Web 服務所使用的程式設計模型。 特別是，它不支援 <xref:System.Xml.Serialization.XmlElementAttribute> 和 <xref:System.Xml.Serialization.XmlAttributeAttribute>之類的屬性。 若要啟用這個程式設計模型的支援，必須將 WCF 切換為使用， <xref:System.Xml.Serialization.XmlSerializer> 而不是 <xref:System.Runtime.Serialization.DataContractSerializer> 。

- <xref:System.DBNull> 型別會被特別處理。 它是一種單一型別，且在還原序列化時，還原序列化程式會尊重單一限制並將所有 `DBNull` 參考指向單一執行個體。 由於 `DBNull` 是一種可序列化型別，它需要 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter%2A> 權限。

## <a name="see-also"></a>另請參閱

- [資料合約中的 XML 和 ADO.NET 類型](xml-and-ado-net-types-in-data-contracts.md)
- [使用資料合約](using-data-contracts.md)
- [可序列化類型](serializable-types.md)
- [Collection Types in Data Contracts](collection-types-in-data-contracts.md)
- [Enumeration Types in Data Contracts](enumeration-types-in-data-contracts.md)
