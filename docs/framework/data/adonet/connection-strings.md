---
title: 連接字串
description: 深入瞭解 ADO.NET 中的連接字串，其中包含從資料提供者傳遞至資料來源之參數的初始化資訊。
ms.date: 10/10/2018
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.openlocfilehash: baa6599a532746895cbb3920f2c623dd4c2be864
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287021"
---
# <a name="connection-strings-in-adonet"></a><span data-ttu-id="62224-103">ADO.NET 中的連接字串</span><span class="sxs-lookup"><span data-stu-id="62224-103">Connection Strings in ADO.NET</span></span>

<span data-ttu-id="62224-104">連接字串 (Connection String) 包含可當做參數從資料提供者 (Data Provider) 傳遞至資料來源的初始化資訊。</span><span class="sxs-lookup"><span data-stu-id="62224-104">A connection string contains initialization information that is passed as a parameter from a data provider to a data source.</span></span> <span data-ttu-id="62224-105">此資料提供者會收到連接字串，做為屬性的值 <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="62224-105">The data provider receives the connection string as the value of the <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="62224-106">提供者會剖析連接字串，並確保語法正確且支援關鍵字。</span><span class="sxs-lookup"><span data-stu-id="62224-106">The provider parses the connection string and ensures that the syntax is correct and that the keywords are supported.</span></span> <span data-ttu-id="62224-107">然後，方法會將剖析 <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> 的連接參數傳遞至資料來源。</span><span class="sxs-lookup"><span data-stu-id="62224-107">Then the <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> method passes the parsed connection parameters to the data source.</span></span> <span data-ttu-id="62224-108">資料來源會執行進一步的驗證，並建立連接。</span><span class="sxs-lookup"><span data-stu-id="62224-108">The data source performs further validation and establishes a connection.</span></span>

## <a name="connection-string-syntax"></a><span data-ttu-id="62224-109">連接字串語法</span><span class="sxs-lookup"><span data-stu-id="62224-109">Connection string syntax</span></span>

<span data-ttu-id="62224-110">連接字串是以分號分隔的索引鍵/值參數組清單：</span><span class="sxs-lookup"><span data-stu-id="62224-110">A connection string is a semicolon-delimited list of key/value parameter pairs:</span></span>

```csharp
keyword1=value; keyword2=value;
```

<span data-ttu-id="62224-111">關鍵字不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="62224-111">Keywords are not case-sensitive.</span></span> <span data-ttu-id="62224-112">不過，值可能會區分大小寫，視資料來源而定。</span><span class="sxs-lookup"><span data-stu-id="62224-112">Values, however, may be case-sensitive, depending on the data source.</span></span> <span data-ttu-id="62224-113">關鍵字和值都可以包含[空白字元](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)。</span><span class="sxs-lookup"><span data-stu-id="62224-113">Both keywords and values may contain [whitespace characters](https://en.wikipedia.org/wiki/Whitespace_character#Unicode).</span></span> <span data-ttu-id="62224-114">關鍵字和不具引號的值會忽略開頭和尾端空白字元。</span><span class="sxs-lookup"><span data-stu-id="62224-114">Leading and trailing white space is ignored in keywords and unquoted values.</span></span>

<span data-ttu-id="62224-115">如果值包含分號、 [Unicode 控制字元](https://en.wikipedia.org/wiki/Unicode_control_characters)或開頭或尾端空白字元，則必須以單引號或雙引號括住。</span><span class="sxs-lookup"><span data-stu-id="62224-115">If a value contains the semicolon, [Unicode control characters](https://en.wikipedia.org/wiki/Unicode_control_characters), or leading or trailing white space, it must be enclosed in single or double quotation marks.</span></span> <span data-ttu-id="62224-116">例如：</span><span class="sxs-lookup"><span data-stu-id="62224-116">For example:</span></span>

```csharp
Keyword=" whitespace  ";
Keyword='special;character';
```

<span data-ttu-id="62224-117">封入字元可能不會出現在它所括住的值內。</span><span class="sxs-lookup"><span data-stu-id="62224-117">The enclosing character may not occur within the value it encloses.</span></span> <span data-ttu-id="62224-118">因此，包含單引號的值只可用雙引號括住，反之亦然：</span><span class="sxs-lookup"><span data-stu-id="62224-118">Therefore, a value containing single quotation marks can be enclosed only in double quotation marks, and vice versa:</span></span>

```csharp
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

<span data-ttu-id="62224-119">您也可以使用其中兩個來將封入字元一併加以轉義：</span><span class="sxs-lookup"><span data-stu-id="62224-119">You can also escape the enclosing character by using two of them together:</span></span>

```csharp
Keyword="double""quotation";
Keyword='single''quotation';
```

<span data-ttu-id="62224-120">引號本身和等號不需要進行轉義，因此下列連接字串是有效的：</span><span class="sxs-lookup"><span data-stu-id="62224-120">The quotation marks themselves, as well as the equals sign, do not require escaping, so the following connection strings are valid:</span></span>

```csharp
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

<span data-ttu-id="62224-121">因為每個值都會在下一個分號或字串結尾之前讀取，所以後者範例中的值是 `a=b=c` ，而最後一個分號是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="62224-121">Since each value is read till the next semicolon or the end of string, the value in the latter example is `a=b=c`, and the final semicolon is optional.</span></span>

<span data-ttu-id="62224-122">所有的連接字串共用相同的基本語法，如下所述。</span><span class="sxs-lookup"><span data-stu-id="62224-122">All connection strings share the same basic syntax described above.</span></span> <span data-ttu-id="62224-123">一組可辨識的關鍵字取決於該提供者，而且已從舊版 Api （例如*ODBC*）演變多年。</span><span class="sxs-lookup"><span data-stu-id="62224-123">The set of recognized keywords depends on the provider, however, and has evolved over the years from earlier APIs such as *ODBC*.</span></span> <span data-ttu-id="62224-124">*SQL Server* （）的 *.NET Framework*資料提供者 `SqlClient` 支援來自較舊 api 的許多關鍵字，但通常更有彈性，而且會接受許多常用連接字串關鍵字的同義字。</span><span class="sxs-lookup"><span data-stu-id="62224-124">The *.NET Framework* data provider for *SQL Server* (`SqlClient`) supports many keywords from older APIs, but is generally more flexible and accepts synonyms for many of the common connection string keywords.</span></span>

<span data-ttu-id="62224-125">輸入錯誤可能會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="62224-125">Typing mistakes can cause errors.</span></span> <span data-ttu-id="62224-126">例如， `Integrated Security=true` 是有效的，但 `IntegratedSecurity=true` 會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="62224-126">For example, `Integrated Security=true` is valid, but `IntegratedSecurity=true` causes an error.</span></span>

<span data-ttu-id="62224-127">在執行時間從未驗證的使用者輸入手動建立的連接字串，很容易遭受字串插入式攻擊，並危及資料來源的安全性。</span><span class="sxs-lookup"><span data-stu-id="62224-127">Connection strings constructed manually at run time from unvalidated user input are vulnerable to string-injection attacks and jeopardize security at the data source.</span></span> <span data-ttu-id="62224-128">為了解決這些問題， *ADO.NET* 2.0 引進了每個 *.NET Framework*資料提供者的[連接字串](connection-string-builders.md)產生器。</span><span class="sxs-lookup"><span data-stu-id="62224-128">To address these problems, *ADO.NET* 2.0 introduced [connection string builders](connection-string-builders.md) for each *.NET Framework* data provider.</span></span> <span data-ttu-id="62224-129">這些連接字串產生器會將參數公開為強型別屬性，並可在連接字串傳送至資料來源之前進行驗證。</span><span class="sxs-lookup"><span data-stu-id="62224-129">These connection string builders expose parameters as strongly typed properties, and make it possible to validate the connection string before it's sent to the data source.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="62224-130">本節內容</span><span class="sxs-lookup"><span data-stu-id="62224-130">In This Section</span></span>

<span data-ttu-id="62224-131">[連接字串產生器](connection-string-builders.md)</span><span class="sxs-lookup"><span data-stu-id="62224-131">[Connection String Builders](connection-string-builders.md)</span></span>\
<span data-ttu-id="62224-132">示範如何使用 `ConnectionStringBuilder` 類別在執行階段建構有效的連接字串。</span><span class="sxs-lookup"><span data-stu-id="62224-132">Demonstrates how to use the `ConnectionStringBuilder` classes to construct valid connection strings at run time.</span></span>

<span data-ttu-id="62224-133">[連接字串和設定檔](connection-strings-and-configuration-files.md)</span><span class="sxs-lookup"><span data-stu-id="62224-133">[Connection Strings and Configuration Files](connection-strings-and-configuration-files.md)</span></span>\
<span data-ttu-id="62224-134">示範如何在組態檔中儲存及擷取連接字串。</span><span class="sxs-lookup"><span data-stu-id="62224-134">Demonstrates how to store and retrieve connection strings in configuration files.</span></span>

<span data-ttu-id="62224-135">[連接字串語法](connection-string-syntax.md)</span><span class="sxs-lookup"><span data-stu-id="62224-135">[Connection String Syntax](connection-string-syntax.md)</span></span>\
<span data-ttu-id="62224-136">說明如何針對`SqlClient`、`OracleClient`、`OleDb` 和 `Odbc` 設定提供者專用的連接字串。</span><span class="sxs-lookup"><span data-stu-id="62224-136">Describes how to configure provider-specific connection strings for `SqlClient`, `OracleClient`, `OleDb`, and `Odbc`.</span></span>

<span data-ttu-id="62224-137">[保護連接資訊](protecting-connection-information.md)</span><span class="sxs-lookup"><span data-stu-id="62224-137">[Protecting Connection Information](protecting-connection-information.md)</span></span>\
<span data-ttu-id="62224-138">示範的技術可保護用於連接至資料來源的資訊。</span><span class="sxs-lookup"><span data-stu-id="62224-138">Demonstrates techniques for protecting information used to connect to a data source.</span></span>

## <a name="see-also"></a><span data-ttu-id="62224-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="62224-139">See also</span></span>

- [<span data-ttu-id="62224-140">連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="62224-140">Connecting to a Data Source</span></span>](/cpp/data/odbc/connecting-to-a-data-source)
- <span data-ttu-id="62224-141">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="62224-141">[ADO.NET Overview](ado-net-overview.md)</span></span>
