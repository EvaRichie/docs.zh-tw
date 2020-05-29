---
title: 連接字串
ms.date: 10/10/2018
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.openlocfilehash: 3f56a487121757706ef6b4dfd11fcd761657431a
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202271"
---
# <a name="connection-strings-in-adonet"></a>ADO.NET 中的連接字串

連接字串 (Connection String) 包含可當做參數從資料提供者 (Data Provider) 傳遞至資料來源的初始化資訊。 此資料提供者會收到連接字串，做為屬性的值 <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> 。 提供者會剖析連接字串，並確保語法正確且支援關鍵字。 然後，方法會將剖析 <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> 的連接參數傳遞至資料來源。 資料來源會執行進一步的驗證，並建立連接。

## <a name="connection-string-syntax"></a>連接字串語法

連接字串是以分號分隔的索引鍵/值參數組清單：

```csharp
keyword1=value; keyword2=value;
```

關鍵字不區分大小寫。 不過，值可能會區分大小寫，視資料來源而定。 關鍵字和值都可以包含[空白字元](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)。 關鍵字和不具引號的值會忽略開頭和尾端空白字元。

如果值包含分號、 [Unicode 控制字元](https://en.wikipedia.org/wiki/Unicode_control_characters)或開頭或尾端空白字元，則必須以單引號或雙引號括住。 例如：

```csharp
Keyword=" whitespace  ";
Keyword='special;character';
```

封入字元可能不會出現在它所括住的值內。 因此，包含單引號的值只可用雙引號括住，反之亦然：

```csharp
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

您也可以使用其中兩個來將封入字元一併加以轉義：

```csharp
Keyword="double""quotation";
Keyword='single''quotation';
```

引號本身和等號不需要進行轉義，因此下列連接字串是有效的：

```csharp
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

因為每個值都會在下一個分號或字串結尾之前讀取，所以後者範例中的值是 `a=b=c` ，而最後一個分號是選擇性的。

所有的連接字串共用相同的基本語法，如下所述。 一組可辨識的關鍵字取決於該提供者，而且已從舊版 Api （例如*ODBC*）演變多年。 *SQL Server* （）的 *.NET Framework*資料提供者 `SqlClient` 支援來自較舊 api 的許多關鍵字，但通常更有彈性，而且會接受許多常用連接字串關鍵字的同義字。

輸入錯誤可能會導致錯誤。 例如， `Integrated Security=true` 是有效的，但 `IntegratedSecurity=true` 會造成錯誤。

在執行時間從未驗證的使用者輸入手動建立的連接字串，很容易遭受字串插入式攻擊，並危及資料來源的安全性。 為了解決這些問題， *ADO.NET* 2.0 引進了每個 *.NET Framework*資料提供者的[連接字串](connection-string-builders.md)產生器。 這些連接字串產生器會將參數公開為強型別屬性，並可在連接字串傳送至資料來源之前進行驗證。

## <a name="in-this-section"></a>本節內容

[連接字串產生器](connection-string-builders.md)\
示範如何使用 `ConnectionStringBuilder` 類別在執行階段建構有效的連接字串。

[連接字串和設定檔](connection-strings-and-configuration-files.md)\
示範如何在組態檔中儲存及擷取連接字串。

[連接字串語法](connection-string-syntax.md)\
說明如何針對`SqlClient`、`OracleClient`、`OleDb` 和 `Odbc` 設定提供者專用的連接字串。

[保護連接資訊](protecting-connection-information.md)\
示範的技術可保護用於連接至資料來源的資訊。

## <a name="see-also"></a>另請參閱

- [連接到資料來源](/cpp/data/odbc/connecting-to-a-data-source)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
