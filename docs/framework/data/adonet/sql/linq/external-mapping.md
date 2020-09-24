---
title: 外部對應
ms.date: 03/30/2017
ms.assetid: 076606b8-d889-4ba0-b5da-ae577b146f23
ms.openlocfilehash: 79427cde0784746480e851cf1be56c8bce854919
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91161382"
---
# <a name="external-mapping"></a><span data-ttu-id="c0516-102">外部對應</span><span class="sxs-lookup"><span data-stu-id="c0516-102">External Mapping</span></span>

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="c0516-103">支援 *外部對應*，也就是您使用個別 XML 檔案來指定資料庫的資料模型與物件模型之間的對應的進程。</span><span class="sxs-lookup"><span data-stu-id="c0516-103">supports *external mapping*, a process by which you use a separate XML file to specify mapping between the data model of the database and your object model.</span></span> <span data-ttu-id="c0516-104">使用外部對應檔案的好處如下：</span><span class="sxs-lookup"><span data-stu-id="c0516-104">Advantages of using an external mapping file include the following:</span></span>  
  
- <span data-ttu-id="c0516-105">您可以將對應程式碼與應用程式的程式碼分開來。</span><span class="sxs-lookup"><span data-stu-id="c0516-105">You can keep your mapping code out of your application code.</span></span> <span data-ttu-id="c0516-106">如此一來，就可以避免應用程式的程式碼變得雜亂。</span><span class="sxs-lookup"><span data-stu-id="c0516-106">This approach reduces clutter in your application code.</span></span>  
  
- <span data-ttu-id="c0516-107">您可以將外部對應檔案視為組態檔。</span><span class="sxs-lookup"><span data-stu-id="c0516-107">You can treat an external mapping file something like a configuration file.</span></span> <span data-ttu-id="c0516-108">例如，在交付二進位碼檔案之後，只要換掉外部對應檔案，就可以更新應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="c0516-108">For example, you can update how your application behaves after shipping the binaries by just swapping out the external mapping file.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c0516-109">規格需求</span><span class="sxs-lookup"><span data-stu-id="c0516-109">Requirements</span></span>  

 <span data-ttu-id="c0516-110">對應檔案必須是 XML 檔案，而且檔案必須根據 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 架構定義進行驗證 ( .xsd) 檔。</span><span class="sxs-lookup"><span data-stu-id="c0516-110">The mapping file must be an XML file, and the file must validate against a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] schema definition (.xsd) file.</span></span>  
  
 <span data-ttu-id="c0516-111">適用的規則如下：</span><span class="sxs-lookup"><span data-stu-id="c0516-111">The following rules apply:</span></span>  
  
- <span data-ttu-id="c0516-112">對應檔案必須是 XML 檔。</span><span class="sxs-lookup"><span data-stu-id="c0516-112">The mapping file must be an XML file.</span></span>  
  
- <span data-ttu-id="c0516-113">XML 對應檔案必須根據 XML 結構描述定義檔進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c0516-113">The XML mapping file must be valid against the XML schema definition file.</span></span> <span data-ttu-id="c0516-114">如需詳細資訊，請參閱 [如何：驗證 DBML 和外部對應](how-to-validate-dbml-and-external-mapping-files.md)檔。</span><span class="sxs-lookup"><span data-stu-id="c0516-114">For more information, see [How to: Validate DBML and External Mapping Files](how-to-validate-dbml-and-external-mapping-files.md).</span></span>  
  
- <span data-ttu-id="c0516-115">外部對應會覆寫以屬性 (Attribute) 為基礎的對應。</span><span class="sxs-lookup"><span data-stu-id="c0516-115">External mapping overrides attribute-based mapping.</span></span> <span data-ttu-id="c0516-116">也就是說，當您使用外部對應來源建立 <xref:System.Data.Linq.DataContext> 時，<xref:System.Data.Linq.DataContext> 會忽略已在類別上建立的所有對應屬性。</span><span class="sxs-lookup"><span data-stu-id="c0516-116">In other words, when you use an external mapping source to create a <xref:System.Data.Linq.DataContext>, the <xref:System.Data.Linq.DataContext> ignores all mapping attributes you have created on classes.</span></span> <span data-ttu-id="c0516-117">不論類別是否包含在外部對應檔案中，結果都是一樣。</span><span class="sxs-lookup"><span data-stu-id="c0516-117">This behavior is true whether the class is included in the external mapping file.</span></span>  
  
- [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="c0516-118">不支援混合使用兩種對應方式 (以屬性為基礎和外部)。</span><span class="sxs-lookup"><span data-stu-id="c0516-118">does not support the hybrid use of the two mapping approaches (attribute-based and external).</span></span>  
  
## <a name="xml-schema-definition-file"></a><span data-ttu-id="c0516-119">XML 結構描述定義檔</span><span class="sxs-lookup"><span data-stu-id="c0516-119">XML Schema Definition File</span></span>  

 <span data-ttu-id="c0516-120">[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的外部對應必須根據下列 XML 結構描述定義進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c0516-120">External mapping in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] must be valid against the following XML schema definition.</span></span>  
  
 <span data-ttu-id="c0516-121">這個結構描述定義檔與用來驗證 DBML 檔案的結構描述定義檔不同。</span><span class="sxs-lookup"><span data-stu-id="c0516-121">Distinguish this schema definition file from the schema definition file that is used to validate a DBML file.</span></span> <span data-ttu-id="c0516-122">如需詳細資訊，請參閱 LINQ to SQL) 中的程式 [代碼產生](code-generation-in-linq-to-sql.md) 。</span><span class="sxs-lookup"><span data-stu-id="c0516-122">For more information, see [Code Generation in LINQ to SQL](code-generation-in-linq-to-sql.md)).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c0516-123">Visual Studio 使用者也會在 [XML 架構] 對話方塊的 [Linqtosqlmapping.xsd .xsd] 中找到這個 XSD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c0516-123">Visual Studio users will also find this XSD file in the XML Schemas dialog box as "LinqToSqlMapping.xsd".</span></span> <span data-ttu-id="c0516-124">若要正確地使用此檔案來驗證外部對應檔案，請參閱 [如何：驗證 DBML 和外部對應](how-to-validate-dbml-and-external-mapping-files.md)檔。</span><span class="sxs-lookup"><span data-stu-id="c0516-124">To use this file correctly for validating an external mapping file, see [How to: Validate DBML and External Mapping Files](how-to-validate-dbml-and-external-mapping-files.md).</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-16"?>  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://schemas.microsoft.com/linqtosql/mapping/2007" xmlns="http://schemas.microsoft.com/linqtosql/mapping/2007"  
elementFormDefault="qualified" >  
  <xs:element name="Database" type="Database" />  
  <xs:complexType name="Database">  
    <xs:sequence>  
      <xs:element name="Table" type="Table" minOccurs="0" maxOccurs="unbounded" />  
      <xs:element name="Function" type="Function" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Provider" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Table">  
    <xs:sequence>  
      <xs:element name="Type" type="Type" minOccurs="1" maxOccurs="1" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Type">  
    <xs:sequence>  
      <xs:choice minOccurs="0" maxOccurs="unbounded">  
        <xs:element name="Column" type="Column" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Association" type="Association" minOccurs="0" maxOccurs="unbounded" />  
      </xs:choice>  
      <xs:element name="Type" type="Type" minOccurs="0" maxOccurs="unbounded" />  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="required" />  
    <xs:attribute name="InheritanceCode" type="xs:string" use="optional" />  
    <xs:attribute name="IsInheritanceDefault" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Column">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="IsPrimaryKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsDbGenerated" type="xs:boolean" use="optional" />  
    <xs:attribute name="CanBeNull" type="xs:boolean" use="optional" />  
    <xs:attribute name="UpdateCheck" type="UpdateCheck" use="optional" />  
    <xs:attribute name="IsDiscriminator" type="xs:boolean" use="optional" />  
    <xs:attribute name="Expression" type="xs:string" use="optional" />  
    <xs:attribute name="IsVersion" type="xs:boolean" use="optional" />  
    <xs:attribute name="AutoSync" type="AutoSync" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Association">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Member" type="xs:string" use="required" />  
    <xs:attribute name="Storage" type="xs:string" use="optional" />  
    <xs:attribute name="ThisKey" type="xs:string" use="optional" />  
    <xs:attribute name="OtherKey" type="xs:string" use="optional" />  
    <xs:attribute name="IsForeignKey" type="xs:boolean" use="optional" />  
    <xs:attribute name="IsUnique" type="xs:boolean" use="optional" />  
    <xs:attribute name="DeleteRule" type="xs:string" use="optional" />  
    <xs:attribute name="DeleteOnNull" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Function">  
    <xs:sequence>  
      <xs:element name="Parameter" type="Parameter" minOccurs="0" maxOccurs="unbounded" />  
      <xs:choice>  
        <xs:element name="ElementType" type="Type" minOccurs="0" maxOccurs="unbounded" />  
        <xs:element name="Return" type="Return" minOccurs="0" maxOccurs="1" />  
      </xs:choice>  
    </xs:sequence>  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Method" type="xs:string" use="required" />  
    <xs:attribute name="IsComposable" type="xs:boolean" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Parameter">  
    <xs:attribute name="Name" type="xs:string" use="optional" />  
    <xs:attribute name="Parameter" type="xs:string" use="required" />  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
    <xs:attribute name="Direction" type="ParameterDirection" use="optional" />  
  </xs:complexType>  
  <xs:complexType name="Return">  
    <xs:attribute name="DbType" type="xs:string" use="optional" />  
  </xs:complexType>  
  <xs:simpleType name="UpdateCheck">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="WhenChanged" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="ParameterDirection">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="In" />  
      <xs:enumeration value="Out" />  
      <xs:enumeration value="InOut" />  
    </xs:restriction>  
  </xs:simpleType>  
  <xs:simpleType name="AutoSync">  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Never" />  
      <xs:enumeration value="OnInsert" />  
      <xs:enumeration value="OnUpdate" />  
      <xs:enumeration value="Always" />  
      <xs:enumeration value="Default" />  
    </xs:restriction>  
  </xs:simpleType>  
</xs:schema>  
```  
  
## <a name="see-also"></a><span data-ttu-id="c0516-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c0516-125">See also</span></span>

- [<span data-ttu-id="c0516-126">LINQ to SQL 中的程式碼產生</span><span class="sxs-lookup"><span data-stu-id="c0516-126">Code Generation in LINQ to SQL</span></span>](code-generation-in-linq-to-sql.md)
- [<span data-ttu-id="c0516-127">參考</span><span class="sxs-lookup"><span data-stu-id="c0516-127">Reference</span></span>](reference.md)
- [<span data-ttu-id="c0516-128">作法：產生物件模型作為外部檔案</span><span class="sxs-lookup"><span data-stu-id="c0516-128">How to: Generate the Object Model as an External File</span></span>](how-to-generate-the-object-model-as-an-external-file.md)
