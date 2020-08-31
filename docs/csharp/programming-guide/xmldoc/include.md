---
title: '<include> -C # 程式設計指南'
description: 瞭解 XML <include> 的相片或視訊。 此標記可讓您參考另一個檔案中描述原始程式碼中類型和成員的批註。
ms.date: 07/20/2015
f1_keywords:
- include
- <include>
helpviewer_keywords:
- <include> C# XML tag
- include C# XML tag
ms.assetid: a8a70302-6196-4643-bd09-ef33f411f18f
ms.openlocfilehash: d2de8fea17850685668766bc4ec6e64b1be77cce
ms.sourcegitcommit: 2560a355c76b0a04cba0d34da870df9ad94ceca3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89053187"
---
# <a name="include-c-programming-guide"></a>\<include> (c # 程式設計手冊) 

## <a name="syntax"></a>語法

```xml
<include file='filename' path='tagpath[@name="id"]' />
```

## <a name="parameters"></a>參數

- `filename`

  包含文件的 XML 檔案名稱。 檔案名稱可以採用的原始程式碼檔的相對路徑。 請將 `filename` 括在單引號 (' ') 內。

- `tagpath`

  `filename` 中導致 `name` 標記的標記路徑。 請將路徑括在單引號 (' ') 內。

- `name`

  標記中位在註解前面的名稱規範；`name` 會有 `id`。

- `id`

  位在註解前面的標記識別碼。 請將識別碼括在雙引號 (" ") 內。

## <a name="remarks"></a>備註

`<include>`標記可讓您參考另一個檔案中描述原始程式碼中類型和成員的批註。 這是將文件註解直接放在原始程式碼檔中的替代方案。 將文件放入個別檔案，即可將原始檔控制套用至與原始程式碼不同的文件。 一個人可以簽出原始程式碼檔，而且其他人可以簽出文件檔。

`<include>`標記會使用 XML XPath 語法。 請參閱 XPath 檔以取得自訂您的 `<include>` 使用方式。

## <a name="example"></a>範例

這是多檔案範例。 以下是第一個使用的檔案 `<include>` 。

[!code-csharp[csProgGuideDocComments#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#5)]

第二個檔案（ *xml_include_tag.doc*）包含下列檔批註。

```xml
<MyDocs>

<MyMembers name="test">
<summary>
The summary for this type.
</summary>
</MyMembers>

<MyMembers name="test2">
<summary>
The summary for this other type.
</summary>
</MyMembers>

</MyDocs>
```

## <a name="program-output"></a>程式輸出

當您使用下列命令列編譯 Test 和 Test2 類別時，會產生下列輸出：`-doc:DocFileName.xml.`。在 Visual Studio 中，您可以在專案設計工具的 [建置] 窗格中指定 XML 文件註解選項。 當 c # 編譯器看到 `<include>` 標記時，會搜尋 *xml_include_tag.doc* 中的檔批註，而不是目前的原始程式檔。 編譯器接著會產生 *DocFileName.xml*，這是檔工具（例如 [>sandcastle](https://github.com/EWSoftware/SHFB) ）用來產生最終檔的檔案。  
  
```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>xml_include_tag</name>
    </assembly>
    <members>
        <member name="T:Test">
            <summary>
The summary for this type.
</summary>
        </member>
        <member name="T:Test2">
            <summary>
The summary for this other type.
</summary>
        </member>
    </members>
</doc>
```  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [建議使用的檔註解標記](./recommended-tags-for-documentation-comments.md)
