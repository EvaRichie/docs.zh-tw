---
title: SqlMetal.exe (程式碼產生工具)
description: 瞭解 SqlMetal.exe 程式碼產生工具。 使用工具來產生 .NET 的 LINQ to SQL 元件的程式碼和對應。
ms.date: 03/30/2017
helpviewer_keywords:
- SQLMetal [LINQ to SQL]
- code generation tool
- SQLMetal.exe
- LINQ to SQL, serialization
- LINQ to SQL, DBML files
- LINQ to SQL, SQLMetal
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
ms.openlocfilehash: 4edf11315892ed8267bee17d69a70033348eca5c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96272562"
---
# <a name="sqlmetalexe-code-generation-tool"></a>SqlMetal.exe (程式碼產生工具)

SqlMetal 命令列工具會為 .NET Framework 的 [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] 元件產生程式碼及對應。 藉由套用本主題稍後出現的選項，您就可以指示 SqlMetal 執行數個不同的動作，包括以下各項：  
  
- 從資料庫產生原始程式碼和對應屬性或對應檔。  
  
- 從資料庫產生中繼資料庫標記語言 (.dbml) 檔用於自訂。  
  
- 從 .dbml 檔產生程式碼和對應屬性或對應檔。  
  
 此工具會自動與 Visual Studio 一起安裝。 根據預設，這個檔案位於 `drive`:\Program Files\Microsoft SDKs\Windows\v`n.nn`\bin。 如果您沒有安裝 Visual Studio，您也可以下載 [Windows SDK](https://go.microsoft.com/fwlink/?LinkId=142225)以取得 SQLMetal 檔案。  
  
> [!NOTE]
> 使用 Visual Studio 的開發人員也可以使用物件關聯式設計工具來產生實體類別。 命令列方法會針對大型資料庫做適當調整。 由於 SqlMetal 是命令列工具，因此您可以在建置處理序中使用它。  
  
 若要執行這項工具，請使用 [Visual Studio 開發人員命令提示字元] (或 Windows 7 中的 [Visual Studio 命令提示字元])。 如需詳細資訊，請參閱[命令提示字元](developer-command-prompt-for-vs.md)。在命令提示字元中，鍵入下列命令：  
  
## <a name="syntax"></a>Syntax  
  
```console  
sqlmetal [options] [<input file>]  
```  
  
## <a name="options"></a>選項  

 若要檢視最新的選項清單，請進入安裝位置，並在命令提示字元輸入 `sqlmetal /?` 。  
  
 **連線選項**  
  
|選項|描述|  
|------------|-----------------|  
|**/server：***\<name>*|指定資料庫伺服器名稱。|  
|**/database：***\<name>*|指定伺服器上的資料庫目錄。|  
|**/user：***\<name>*|指定登入使用者識別碼。預設值：使用 Windows 驗證。|  
|**/password：***\<password>*|指定登入密碼。 預設值：使用 Windows 驗證。|  
|**/conn：***\<connection string>*|指定資料庫連接字串。 不可配合 **/server**、 **/database**、 **/user** 或 **/password** 選項使用。<br /><br /> 不要在連接字串中包含檔案名稱。 而是在命令列中加入檔名來做為輸入檔案。 例如，下行指定 "c:\northwnd.mdf" 作為輸入檔案： **sqlmetal /code:"c:\northwind.cs" /language:csharp "c:\northwnd.mdf"**。|  
|**/timeout：***\<seconds>*|指定 SqlMetal 存取資料庫時的逾時值。 預設值：0 (也就是沒有時間限制)。|  
  
 **擷取選項**  
  
|選項|描述|  
|------------|-----------------|  
|**/views**|擷取資料庫檢視。|  
|**/functions**|擷取資料庫函式。|  
|**/sprocs**|擷取預存程序。|  
  
 **輸出選項**  
  
|選項|描述|  
|------------|-----------------|  
|**/dbml** *[:file]*|以 .dbml 傳送輸出。 無法搭配 **/map** 選項使用。|  
|**/code** *[:file]*|以原始程式碼傳送輸出。 無法搭配 **/dbml** 選項使用。|  
|**/map** *[:file]*|產生 XML 對應檔而不是屬性。 無法搭配 **/dbml** 選項使用。|  
  
 **其他**  
  
|選項|描述|  
|------------|-----------------|  
|**/language：***\<language>*|指定原始程式碼語言。<br /><br /> 有效 *\<language>* ： vb、csharp。<br /><br /> 預設值：衍生自程式碼檔案名稱的副檔名。|  
|**/namespace：***\<name>*|指定所產生程式碼的命名空間。 預設值：沒有命名空間。|  
|**/coNtext：***\<type>*|指定資料庫內容類別的名稱。 預設值：衍生自資料庫名稱。|  
|**/entitybase：***\<type>*|指定所產生程式碼中實體類別的基底類別。 預設值：實體沒有基底類別。|  
|**/pluralize**|自動複數化或單數化類別和成員名稱。<br /><br /> 這個選項功能僅適用於美國英文版本。|  
|**/serialization：***\<option>*|產生可序列化的類別。<br /><br /> 有效 *\<option>* ：無、單向。 預設值：無。<br /><br /> 如需詳細資訊，請參閱[序列化](../data/adonet/sql/linq/serialization.md)。|  
  
 **輸入檔**  
  
|選項|描述|  
|------------|-----------------|  
|**\<input file>**|指定 SQL Server Express .mdf 檔、SQL Server Compact 3.5 .sdf 檔或 .dbml 中繼檔。|  
  
## <a name="remarks"></a>備註  

 SqlMetal 功能實際上包含兩個步驟：  
  
- 將資料庫的中繼資料擷取至 .dbml 檔。  
  
- 產生程式碼輸出檔。  
  
     使用適當的命令列選項，您就可以產生 Visual Basic 或 C# 原始程式碼，或是產生 XML 對應檔。  
  
 若要從 .mdf 檔擷取中繼資料，您必須在所有其他選項之後指定 .mdf 檔的名稱。  
  
 如果沒有指定 **/server** ，則會假設為 **localhost/sqlexpress** 。  
  
 如果下列其中一或多個條件為真，Microsoft SQL Server 2005 會擲回例外狀況：  
  
- SqlMetal 嘗試擷取呼叫本身的預存程序。  
  
- 預存程序、函式或檢視的巢狀層超過 32。  
  
     SqlMetal 會快取這個例外狀況並回報為警告。  
  
 若要指定輸入檔案名稱，請將名稱以輸入檔案加入命令列。 不支援將檔案名稱包含在連接字串中 (使用 **/conn** 選項)。  
  
## <a name="examples"></a>範例  

 產生 .dbml 檔，其中包含擷取的 SQL 中繼資料：  
  
 **sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml**  
  
 產生 .dbml 檔，其中包括使用 SQL Server Express 從 .mdf 檔擷取的 SQL 中繼資料：  
  
 **sqlmetal /dbml:mymeta.dbml mydbfile.mdf**  
  
 產生 .dbml 檔，其中包括從 SQL Server Express 擷取的 SQL 中繼資料：  
  
 **sqlmetal /server:.\sqlexpress /dbml:mymeta.dbml /database:northwind**  
  
 從 .dbml 中繼資料檔產生原始程式碼：  
  
 **sqlmetal /namespace:nwind /code:nwind.cs /language:csharp mymetal.dbml**  
  
 直接從 SQL 中繼資料產生原始程式碼：  
  
 **sqlmetal /server:myserver /database:northwind /namespace:nwind /code:nwind.cs /language:csharp**  
  
> [!NOTE]
> 當您使用 **/pluralize** 選項搭配 Northwind 範例資料庫時，請注意以下行為： 當 SqlMetal 提供資料表的資料列類型名稱時，資料表名稱會是單數。 當它為資料表提供 <xref:System.Data.Linq.DataContext> 屬性時，資料表名稱會是複數。 碰巧的是，Northwind 範例資料庫中的資料表已經是複數。 因此您不會看見該部分的運作情形。 雖然一般會將資料庫資料表的名稱設為單數，在 .NET 中仍然常會把集合名稱設為複數。  
  
## <a name="see-also"></a>另請參閱

- [作法：以 Visual Basic 或 C# 產生物件模型](../data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)
- [LINQ to SQL 中的程式碼產生](../data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [外部對應](../data/adonet/sql/linq/external-mapping.md)
