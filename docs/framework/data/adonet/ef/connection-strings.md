---
title: ADO.NET Entity Framework 中的連接字串
description: 瞭解 Entity Framework 中的連接字串，其中包含連接到 ADO.NET 資料提供者以及模型和對應檔案的資訊。
ms.date: 10/15/2018
ms.assetid: 78d516bc-c99f-4865-8ff1-d856bc1a01c0
ms.openlocfilehash: 36b7724bc8dbb8f427f4bbf748b7b7801adea8db
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90542753"
---
# <a name="connection-strings-in-the-adonet-entity-framework"></a>ADO.NET Entity Framework 中的連接字串

連接字串 (Connection String) 包含可當做參數從資料提供者 (Data Provider) 傳遞至資料來源的初始化資訊。 此語法會因資料提供者而不同，而且連接字串會在嘗試開啟連接期間進行剖析。 Entity Framework 所使用的連接字串包含用來連接至支援 Entity Framework 之基礎 ADO.NET 資料提供者的資訊。 它們也包含必要之模型和對應檔的相關資訊。

EntityClient 提供者會在存取模型和對應中繼資料，以及連接至資料來源時使用連接字串。 您可以透過 <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> 的 <xref:System.Data.EntityClient.EntityConnection> 屬性來存取或設定連接字串。 <xref:System.Data.EntityClient.EntityConnectionStringBuilder> 類別 (Class) 可用來以程式設計方式建構或存取連接字串中的參數。 如需詳細資訊，請參閱 [如何：建立 EntityConnection 連接字串](how-to-build-an-entityconnection-connection-string.md)。

[實體資料模型工具](/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))會產生儲存在應用程式佈建檔中的連接字串。 <xref:System.Data.Objects.ObjectContext> 會在建立物件查詢時自動擷取這個連接資訊。 您可以從 <xref:System.Data.EntityClient.EntityConnection> 屬性中存取 <xref:System.Data.Objects.ObjectContext> 執行個體 (Instance) 所使用的 <xref:System.Data.Objects.ObjectContext.Connection%2A>。 如需詳細資訊，請參閱 [管理連接和交易](/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))。

## <a name="connection-string-syntax"></a>連接字串語法

若要瞭解連接字串的一般語法，請參閱 [連接字串語法 |ADO.NET 中的連接字串](../connection-strings.md#connection-string-syntax)。

## <a name="connection-string-parameters"></a>連接字串參數

下表列出 <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> 中關鍵字值的有效名稱。

|關鍵字|描述|
|-------------|-----------------|
|`Provider`|如果沒有指定 `Name` 關鍵字，就是必要項。 用來擷取基礎提供者之 <xref:System.Data.Common.DbProviderFactory> 物件的提供者名稱。 這個值是常數。<br /><br /> 當 `Name` 關鍵字未包含在實體連接字串中時，需要 `Provider` 關鍵字的非空白值。 此關鍵字與 `Name` 關鍵字互斥。|
|`Provider Connection String`|選擇性。 指定傳給基礎資料來源的提供者特定連接字串。 此連接字串包含資料提供者的有效關鍵字/值組。 無效的 `Provider Connection String` 會在資料來源對其進行評估時導致執行階段錯誤。<br /><br /> 此關鍵字與 `Name` 關鍵字互斥。<br /><br /> 請務必根據 [ADO.NET 連接字串](../connection-strings.md)的一般語法來將值換用。 請考慮下列連接字串範例： `Server=serverName; User ID = userID` 。 它必須進行轉義，因為它包含分號。 因為它不包含雙引號，所以可用於進行轉義：<br /><br /> `Provider Connection String ="Server=serverName; User ID = userID";`|
|`Metadata`|如果沒有指定 `Name` 關鍵字，就是必要項。 目錄、檔案和資源位置的垂直線分隔清單，您可在其中尋找中繼資料和對應資訊。 以下是一個範例：<br /><br /> `Metadata=`<br /><br /> `c:\model &#124; c:\model\sql\mapping.msl;`<br /><br /> 忽略垂直線分隔符號兩端的空白。<br /><br /> 此關鍵字與 `Name` 關鍵字互斥。|
|`Name`|應用程式可選擇性的在應用程式組態檔中指定連接名稱，以提供必要的關鍵字/值連接字串值。 在此情況下，您不能在連接字串中直接提供這些值。 在組態檔中不允許 `Name` 關鍵字。<br /><br /> 當 `Name` 關鍵字未包含在連接字串中時，需要 Provider 關鍵字的非空白值。<br /><br /> 此關鍵字與所有其他連接字串關鍵字互斥。|

以下是儲存在應用程式佈建檔中 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 的連接字串範例：

## <a name="model-and-mapping-file-locations"></a>模型和對應檔案位置

`Metadata` 參數包含要讓 `EntityClient` 提供者搜尋模型和對應檔案的位置清單。 模型和對應檔案通常會與應用程式可執行檔部署在相同的目錄中。 這些檔案也可以部署在特定位置中，或當做內嵌資源包含在應用程式中。

內嵌資源的指定方式如下：

`Metadata=res://<assemblyFullName>/<resourceName>`

下列選項可用於定義內嵌資源的位置：

|選項|描述|
|-|-|
|`assemblyFullName`|含有內嵌資源之組件 (Assembly) 的完整名稱。 此名稱包括簡單名稱、版本名稱、支援的文化特性 (Culture) 和公開金鑰 (Public Key)，如下所示：<br /><br /> `ResourceLib, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`<br /><br /> 資源可以內嵌在應用程式可存取的任何組件中。<br /><br /> 如果您指定萬用字元 (的 \*) `assemblyFullName` ，則 Entity Framework 執行時間會在下列位置中搜尋資源，順序如下：<br /><br /> 1. 呼叫元件。<br />2. 參考的元件。<br />3. 應用程式 bin 目錄中的元件。<br /><br /> 如果這些檔案不在其中一個位置內，就會擲回例外狀況 (Exception)。 **注意：**  當您使用萬用字元 ( * ) 時，Entity Framework 必須在所有元件中查看正確名稱的資源。 若要改善效能，請指定組件名稱而非萬用字元。|
|`resourceName`|內含資源的名稱，例如 Adventureworksmodel.edmx。 中繼資料服務只會尋找具有下列其中一個副檔名的檔案或資源：.csdl、.ssdl 或 .msl。 如果沒有指定 `resourceName`，就會載入所有中繼資料資源。 這些資源應該在組件中具有唯一的名稱。 如果您在組件的不同目錄中定義了具有相同名稱的多個檔案，`resourceName` 就必須在資源名稱前面包含資料夾結構，例如 FolderName.FileName.csdl。<br /><br /> 當您針對 `resourceName` 指定萬用字元 (*) 時，不需要使用 `assemblyFullName`。|

> [!NOTE]
> 若要改善效能，請在呼叫組件中內嵌資源，但非 Web 案例 (呼叫組件中沒有基礎對應和中繼資料檔案的參考) 除外。

下列範例會載入呼叫組件、參考的組件和應用程式 bin 目錄中其他組件的所有模型和對應檔案。

```csharp
Metadata=res://*/
```

下列範例會從 AdventureWorks 組件中載入 model.csdl 檔案，並且從執行中應用程式的預設目錄中載入 model.ssdl 和 model.msl 檔案。

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|model.ssdl|model.msl
```

下列範例會從特定組件中載入三個指定的資源。

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.csdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.ssdl|
res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/model.msl
```

下列範例會從組件中載入具有副檔名 .csdl、.msl 和 .ssdl 的所有內嵌資源。

```csharp
Metadata=res://AdventureWorks, 1.0.0.0, neutral, a14f3033def15840/
```

下列範例會從載入的元件位置載入相對檔案路徑中的所有資源，再加上 "datadir\metadata \\ "。

```csharp
Metadata=datadir\metadata\
```

下列範例會從已載入的組件位置中載入相對檔案路徑的所有資源。

```csharp
Metadata=.\
```

## <a name="support-for-the-124datadirectory124-substitution-string-and-the-web-application-root-operator-"></a>支援 &#124;DataDirectory&#124; 替代字串和 Web 應用程式根運算子 (~) 

`DataDirectory` 和 ~ 運算子會用在中 <xref:System.Data.EntityClient.EntityConnection.ConnectionString%2A> 做為 `Metadata` 和關鍵字的一部分 `Provider Connection String` 。 <xref:System.Data.EntityClient.EntityConnection> 會分別將 `DataDirectory` 和 ~ 運算子轉送至 <xref:System.Data.Metadata.Edm.MetadataWorkspace> 和存放區提供者。

|詞彙|描述|
|----------|-----------------|
|`&#124;DataDirectory&#124;`|解析成對應和中繼資料檔案的相對路徑。 這是透過 `AppDomain.SetData("DataDirectory", objValue)` 方法所設定的值。 `DataDirectory`替代字串必須以分隔號字元括住，且其名稱與管道字元之間不能有任何空格。 `DataDirectory` 名稱不區分大小寫。<br /><br /> 如果名為 "DataDirectory" 的實體目錄必須以中繼資料路徑清單的成員形式傳遞，請在名稱的任一側或兩側加上空白字元。 例如： `Metadata="DataDirectory1 &#124; DataDirectory &#124; DataDirectory2"` 。 ASP.NET 應用程式會將 &#124;DataDirectory&#124; 解析成 " \<application root> /app_data" 資料夾。|
|~|解析成 Web 應用程式根目錄。 位於前置位置的 ~ 字元一律會解譯成 Web 應用程式根目錄運算子 (~)，不過它可能會代表有效的本機子目錄。 若要參考這類本機子目錄，使用者應該明確傳遞 `./~`。|

您應該只在路徑的開頭指定 `DataDirectory` 和 ~ 運算子，因為它們無法在任何其他位置進行解析。 Entity Framework 將嘗試解析 `~/data`，但是它會將 `/data/~` 視為實體路徑。

以 `DataDirectory` 或 ~ 運算子為開頭的路徑無法解析成 `DataDirectory` 和 ~ 運算子分支外部的實體路徑。 例如，下列路徑將會解析：`~`、`~/data` 和 `~/bin/Model/SqlServer`。 下列路徑將無法解析：`~/..` 和 `~/../other`。

`DataDirectory` 和 ~ 運算子可擴充成包含子目錄，如下所示：`|DataDirectory|\Model` 和 `~/bin/Model`。

`DataDirectory` 替代字串和 ~ 運算子的解析並非遞迴方式。 例如，當 `DataDirectory` 包含 `~` 字元時，就會發生例外狀況。 這可防止無限遞迴 (Infinite Recursion)。

## <a name="see-also"></a>另請參閱

- [處理資料提供者](working-with-data-providers.md)
- [部署考慮](deployment-considerations.md)
- [管理連接和異動](/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [連接字串](../connection-strings.md)
