---
title: 概觀
description: 如需更詳細的說明和範例，請參閱 .NET Framework 中的 ADO.NET 總覽和閱讀資源。
ms.date: 03/30/2017
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
ms.openlocfilehash: 2ff3b7ad197bfe1e1c12e382f3a59bd470c57a75
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287151"
---
# <a name="adonet-overview"></a>ADO.NET 概觀
ADO.NET 可讓您以一致的方式存取資料來源 (例如 SQL Server 與 XML)，以及透過 OLE DB 和 ODBC 所公開的資料來源。 資料共用的消費者應用程式可使用 ADO.NET 來連接至這些資料來源，並且擷取、處理及更新其中所含的資料。  
  
 ADO.NET 可將資料管理的資料存取分成不連續的元件，這些元件可分開使用，也可串聯使用。 ADO.NET 也包含 .NET Framework 資料提供者，以用於連接資料庫、執行命令和擷取結果。 這些結果會直接處理、放入 ADO.NET <xref:System.Data.DataSet> 物件中以便利用臨機操作 (Ad Hoc) 的方式公開給使用者、與多個來源的資料結合，或在各層之間進行傳遞。 `DataSet` 物件也可以與 .NET Framework 資料提供者分開使用，以便管理應用程式本機的資料或來自 XML 的資料。  
  
 ADO.NET 類別 (Class) 位於 System.Data.dll 中，而且會與 System.Xml.dll 中的 XML 類別整合。 如需連接到資料庫的範例程式碼，從它抓取資料，然後在主控台視窗中顯示該資料，請參閱[ADO.NET 程式碼範例](ado-net-code-examples.md)。  
  
 ADO.NET 可為撰寫 Managed 程式碼的開發人員提供類似於 ActiveX Data Objects (ADO) 提供給原生元件物件模型 (Component Object Model，COM) 開發人員的功能。 我們建議您使用 ADO.NET (而非 ADO) 來存取 .NET 應用程式中的資料。  
  
 ADO.NET 會提供最直接的方法，讓您在 .NET Framework 中進行資料存取。 如需可讓應用程式針對概念模型（而不是基礎儲存體模型）進行處理的較高層級抽象，請參閱[ADO.NET Entity Framework](./ef/index.md)。  
  
 **隱私權聲明**： System.string、OracleClient、system.web、System.web、System.data.sqlserverce 和 system.data.datasetextensions.dll .dll 元件不會區分使用者的私用資料和非私用資料之間的區別，而是不會有任何差異的人來辨識，這就是不能分辨出來的，而是不會。  這些組件不會收集、儲存或傳輸任何使用者的私用資料。 不過，協力廠商應用程式可能會使用這些組件來收集、儲存或傳輸使用者的私用資料。  
  
## <a name="in-this-section"></a>本節內容  
 [ADO.NET 架構](ado-net-architecture.md)  
 提供 ADO.NET 架構和元件的概觀。  
  
 [ADO.NET 技術選項和方針](ado-net-technology-options-and-guidelines.md)  
 說明實體資料平台隨附的產品和技術。  
  
 [LINQ 和 ADO.NET](linq-and-ado-net.md)  
 說明如何在 ADO.NET 中實作 Language-Integrated Query (LINQ)，並且提供相關主題的連結。  
  
 [.NET Framework 資料提供者](data-providers.md)  
 提供 .NET Framework 資料提供者的設計概觀，以及 ADO.NET 所包含的 .NET Framework 資料提供者概觀。  
  
 [ADO.NET 資料集](ado-net-datasets.md)  
 提供 `DataSet` 設計與元件的概觀。  
  
 [ADO.NET 中的並存執行](side-by-side-execution.md)  
 討論各個 ADO.NET 版本之間的差異，以及它們在並存執行與應用程式相容性上的影響。  
  
 [ADO.NET Code Examples](ado-net-code-examples.md) (ADO.NET 程式碼範例)  
 提供使用 ADO.NET 資料提供者來擷取資料的程式碼範例。  
  
## <a name="related-sections"></a>相關章節  
 [ADO.NET 的新功能](whats-new.md)  
 簡介 ADO.NET 的新功能。  
  
 [設定 ADO.NET 應用程式的安全性](securing-ado-net-applications.md)  
 說明使用 ADO.NET 的安全程式碼撰寫實施方針。  
  
 [ADO.NET 中的資料類型對應](data-type-mappings-in-ado-net.md)  
 說明 .NET Framework 資料型別與 .NET Framework 資料提供者之間的資料型別對應。  
  
 [在 ADO.NET 中擷取和修改資料](retrieving-and-modifying-data.md)  
 說明如何連接至資料來源、擷取資料和修改資料。 這包括 `DataReaders` 和 `DataAdapters`。  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET](index.md)
- [存取 Visual Studio 中的資料](/visualstudio/data-tools/accessing-data-in-visual-studio)
