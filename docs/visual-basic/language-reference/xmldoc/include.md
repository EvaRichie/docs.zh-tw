---
title: <include>
ms.date: 07/20/2015
helpviewer_keywords:
- include XML tag
- <include> XML tag
ms.assetid: ba8e9173-82cd-460b-8938-a075a2dfb36d
ms.openlocfilehash: 78a10624107cea349b01f484c641190a945dbd7e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400107"
---
# <a name="include-visual-basic"></a>\<include> (Visual Basic)
指的是描述原始程式碼中類型和成員的另一個檔案。  
  
## <a name="syntax"></a>語法  
  
```xml  
<include file="filename" path="tagpath[@name='id']" />  
```  
  
## <a name="parameters"></a>參數  
 `filename`  
 必要。 包含文件的檔案名稱。 檔案名稱可以使用路徑進行限定。 `filename`以雙引號（""）括住。  
  
 `tagpath`  
 必要。 `filename` 中導致 `name` 標記的標記路徑。 以雙引號（""）括住路徑。  
  
 `name`  
 必要。 標記中批註前面的名稱規範。 `Name`會有 `id` 。  
  
 `id`  
 必要。 位在註解前面的標記識別碼。 以單引號（' '）括住識別碼。  
  
## <a name="remarks"></a>備註  
 使用 `<include>` 標記來參考另一個檔案中描述原始程式碼中類型和成員的批註。 這是將文件註解直接放在原始程式碼檔中的替代方案。  
  
 此 `<include>` 標記會使用 W3C XML Path Language （XPath）1.0 版建議。 如需自訂使用方式的詳細資訊 `<include>` ，請參閱 <https://www.w3.org/TR/xpath> 。  
  
## <a name="example"></a>範例  
 這個範例會使用 `<include>` 標記，從名為的檔案匯入成員檔批註 `commentFile.xml` 。  
  
 [!code-vb[VbVbcnXmlDocComments#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#4)]  
  
 的格式如下所 `commentFile.xml` 示。  
  
```xml  
<Docs>  
<Members name="Open">  
<summary>Opens a file.</summary>  
<param name="filename">File name to open.</param>  
</Members>  
<Members name="Close">  
<summary>Closes a file.</summary>  
<param name="filename">File name to close.</param>  
</Members>  
</Docs>  
```  
  
## <a name="see-also"></a>另請參閱

- [XML 註解標籤](index.md)
