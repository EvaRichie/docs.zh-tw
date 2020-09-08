---
title: 修改 XML 樹狀中的項目、屬性和節點
description: 瞭解您可以用來修改元素、其子節點或其屬性的方法和屬性。
ms.date: 07/20/2015
ms.assetid: 0ed22e4e-4c6b-4eb1-b0eb-06685efd8c33
ms.openlocfilehash: 671ba38350e443d95c92a9bd790eac3d2deb5cdd
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552765"
---
# <a name="modify-elements-attributes-and-nodes-in-an-xml-tree-linq-to-xml"></a>修改 XML 樹狀結構中的元素、屬性和節點 (LINQ to XML) 

下表摘要說明您可以用於修改項目、其子項目或其屬性的方法和屬性。

下列方法會修改 <xref:System.Xml.Linq.XElement> ：

|方法|描述|
|------------|-----------------|
|<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>|以剖析的 XML 取代項目。|
|<xref:System.Xml.Linq.XElement.RemoveAll%2A?displayProperty=nameWithType>|移除項目的所有內容 (子節點和屬性)。|
|<xref:System.Xml.Linq.XElement.RemoveAttributes%2A?displayProperty=nameWithType>|移除項目的屬性。|
|<xref:System.Xml.Linq.XElement.ReplaceAll%2A?displayProperty=nameWithType>|取代項目的所有內容 (子節點和屬性)。|
|<xref:System.Xml.Linq.XElement.ReplaceAttributes%2A?displayProperty=nameWithType>|取代項目的屬性。|
|<xref:System.Xml.Linq.XElement.SetAttributeValue%2A?displayProperty=nameWithType>|設定屬性的值。 建立屬性 (如果不存在)。 如果值設定為 `null`，移除屬性。|
|<xref:System.Xml.Linq.XElement.SetElementValue%2A?displayProperty=nameWithType>|設定子項目的值。 建立項目 (如果不存在)。 如果值設定為 `null`，移除項目。|
|<xref:System.Xml.Linq.XElement.Value%2A?displayProperty=nameWithType>|以指定的文字取代項目的內容 (子節點)。|
|<xref:System.Xml.Linq.XElement.SetValue%2A?displayProperty=nameWithType>|設定項目的值。|

下列方法會修改 <xref:System.Xml.Linq.XAttribute> ：

|方法|描述|
|------------|-----------------|
|<xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=nameWithType>|設定屬性的值。|
|<xref:System.Xml.Linq.XAttribute.SetValue%2A?displayProperty=nameWithType>|設定屬性的值。|

 下列方法會修改 <xref:System.Xml.Linq.XNode> 包含 <xref:System.Xml.Linq.XElement> 或) 的 (<xref:System.Xml.Linq.XDocument> ：

|方法|描述|
|------------|-----------------|
|<xref:System.Xml.Linq.XNode.ReplaceWith%2A?displayProperty=nameWithType>|以新內容取代節點。|

 下列方法會修改 <xref:System.Xml.Linq.XContainer> <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument>)  (：

|方法|描述|
|------------|-----------------|
|<xref:System.Xml.Linq.XContainer.ReplaceNodes%2A?displayProperty=nameWithType>|以新內容取代子節點：|
