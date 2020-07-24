---
title: '如何剖析字串（c #）'
description: '瞭解如何剖析字串，以在 c # 中建立 XML 樹狀結構。 瞭解如何存取已剖析 XML 中的特定資料。'
ms.date: 07/20/2015
ms.assetid: 81e5686c-9658-42d8-a7e3-b11be0a2c98b
ms.openlocfilehash: a4664e090b6a44c52c519e61b66ccdc5d59a71f1
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104813"
---
# <a name="how-to-parse-a-string-c"></a>如何剖析字串（c #）

本主題示範如何剖析字串以便在 C# 中建立 XML 樹狀結構。

## <a name="example"></a>範例

下列 c # 程式碼說明如何剖析 XML 字串：

```csharp
XElement contacts = XElement.Parse(
    @"<Contacts>
        <Contact>
            <Name>Patrick Hines</Name>
            <Phone Type=""home"">206-555-0144</Phone>
            <Phone Type=""work"">425-555-0145</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>10</NetWorth>
        </Contact>
        <Contact>
            <Name>Gretchen Rivas</Name>
            <Phone Type=""mobile"">206-555-0163</Phone>
            <Address>
            <Street1>123 Main St</Street1>
            <City>Mercer Island</City>
            <State>WA</State>
            <Postal>68042</Postal>
            </Address>
            <NetWorth>11</NetWorth>
        </Contact>
    </Contacts>");
Console.WriteLine(contacts);
```

根 `Contacts` 節點有兩個 `Contact` 節點。 若要存取已剖析 XML 中的某些特定資料，請使用[system.xml.linq.xelement> （）](xref:System.Xml.Linq.XContainer.Elements)方法，在此情況下會傳回根節點的子項目 `Contacts` 。 下列範例會將第一個 `Contact` 節點列印到主控台：

```csharp
List<XElement> contactNodes = contacts.Elements("Contact").ToList();
Console.WriteLine(contactNodes[0]);
```

## <a name="see-also"></a>請參閱

- [如何尋找具有特定屬性的元素（c #）](how-to-find-an-element-with-a-specific-attribute.md)
