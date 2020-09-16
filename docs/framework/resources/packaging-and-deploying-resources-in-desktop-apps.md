---
title: 在 .NET 應用程式中封裝和部署資源
description: 在 .NET 應用程式中使用主要元件 (中樞) 和附屬元件 (輪輻) 來封裝和部署資源。 輪輻包含當地語系化的資源，但不含任何程式碼。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- deploying applications [.NET Framework], resources
- resource files, deploying
- hub-and-spoke resource deployment model
- resource files, packaging
- application resources, packaging
- single resource assembly
- satellite assemblies
- default culture for applications
- names [.NET Framework], resources
- fallback process for resources
- grouping cultures
- application resources, deploying
- application resources, naming conventions
- culture, packaging and deploying resources
- resource files, naming conventions
- packaging application resources
- application resources, fallback processes
- resource files, fallback processes
- localizing resources
- neutral cultures
ms.assetid: b224d7c0-35f8-4e82-a705-dd76795e8d16
ms.openlocfilehash: 056569f86afcbdf124f9e617e4ad07b09a194681
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90553996"
---
# <a name="packaging-and-deploying-resources-in-net-apps"></a>在 .NET 應用程式中封裝和部署資源

應用程式會依賴 <xref:System.Resources.ResourceManager> 類別所代表的 .NET Framework Resource Manager，來擷取當地語系化的資源。 Resource Manager 假設使用中樞和支點模型來封裝和部署資源。 中樞是主要組件，其中包含未當地語系化的可執行程式碼以及稱為中性或預設文化特性之單一文化特性的資源。 預設文化特性是應用程式的後援文化特性；如果找不到當地語系化的資源，則它是使用其資源的文化特性。 每個支點都會連線至附屬組件，其中包含單一文化特性但未包含任何程式碼的資源。

這個模型有數個優點：

- 在您部署應用程式之後，可以透過累加方式新增新文化特性的資源。 因為文化特性特定資源的後續開發可能需要很長一段時間，所以這可讓您先發行主要應用程式，並於日後提供文化特性特定資源。
- 您可以更新並變更應用程式的附屬組件，而不需要重新編譯應用程式。
- 應用程式只需要載入包含特定文化特性所需之資源的附屬組件。 這可以大幅降低系統資源的使用。

 不過，這個模型也有缺點：

- 您必須管理多組資源。
- 因為您必須測試數個組態，所以測試應用程式的初始成本會增加。 請注意，長期而言，測試一個具有數個附屬的核心應用程式，與測試並維護數個平行國際版本相較之下，較為簡單且費用較少。

## <a name="resource-naming-conventions"></a>資源命名慣例

當您封裝應用程式的資源時，必須使用 Common Language Runtime 所預期的資源命名慣例來命名它們。 執行階段會依文化特性名稱識別資源。 每個文化特性都會獲指定唯一名稱，此名稱通常是下列項目的組合：與語言建立關聯的兩個字母小寫文化特性名稱以及與國家或地區建立關聯的兩個字母大寫子文化特性名稱 (必要時)。 子文化特性名稱遵循文化特性名稱，以破折號 (-) 分隔。 範例包括 ja-JP (代表在日本日文)、en-US (美式英文)、de-DE (德國德文)，或 de-AT (奧地利德文)。 請參閱 [Windows 支援的語言/地區名稱清單](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)中的 [語言標記]**** 資料行。 文化名稱遵循 [BCP 47](https://tools.ietf.org/html/bcp47) 定義的標準。

> [!NOTE]
> 這兩個字母的文化特性名稱有一些例外，例如 `zh-Hans` 中文 (簡化) 。

> [!NOTE]
> 如需建立資源檔的資訊，請參閱[建立資源檔](creating-resource-files-for-desktop-apps.md)和[建立附屬組件](creating-satellite-assemblies-for-desktop-apps.md)。

<a name="cpconpackagingdeployingresourcesanchor1"></a>

## <a name="the-resource-fallback-process"></a>資源後援處理序

封裝和部署資源的中樞和支點模型會使用後援程序來找出適當的資源。 如果應用程式要求的當地語系化資源無法使用，通用語言執行平台 (CLR) 就會在文化特性的階層架構中搜尋最接近使用者應用程式所要求的適當後援資源，而擲回例外狀況只會做為最後手段。 在階層的每個層級，如果找到適當的資源，則執行階段會使用它。 如果找不到資源，則會繼續搜尋下一個層級。

若要改善查閱效能，請將 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性套用至主要組件，並將使用主要組件之中性語言的名稱傳遞給它。

### <a name="net-framework-resource-fallback-process"></a>.NET Framework 資源後援處理序

.NET Framework 資源後援處理序包含下列步驟：

> [!TIP]
> 您可以使用 [\<relativeBindForResources>](../configure-apps/file-schema/runtime/relativebindforresources-element.md) configuration 元素來優化資源的回復程式，以及執行時間探查資源元件的進程。 如需詳細資訊，請參閱[最佳化資源後援處理序](packaging-and-deploying-resources-in-desktop-apps.md#Optimizing)一節。

1. 執行階段會先檢查[全域組件快取](../app-domains/gac.md)是否有符合應用程式之所要求文化特性的組件。

     全域組件快取可以儲存多個應用程式所共用的資源組件。 這可讓您不需要在所建立之每個應用程式的目錄結構中包括特定資源集。 如果執行階段找到組件的參考，則會搜尋所要求資源的組件。 如果在組件中找到項目，則會使用所要求的資源。 如果找不到項目，會繼續搜尋。

2. 執行階段接下來會檢查目前執行中組件的目錄中是否有符合所要求文化特性的子目錄。 如果它找到子目錄，則會搜尋該子目錄中是否有所要求文化特性的有效附屬組件。 執行階段接著會搜尋所要求資源的附屬組件。 如果在組件中找到資源，則會使用它。 如果找不到資源，會繼續搜尋。

3. 執行階段接下來會查詢 Windows Installer，以判斷是否依需求安裝附屬組件。 如果是這樣，它會處理安裝、載入組件，並搜尋它或所要求的資源。 如果在組件中找到資源，則會使用它。 如果找不到資源，會繼續搜尋。

4. 執行階段會引發 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件，指出找不到附屬組件。 如果您選擇處理事件，則事件處理常式會傳回其資源用於查閱之附屬組件的參考。 否則，事件處理常式會傳回 `null` 並繼續搜尋。

5. 執行階段接下來會重新搜尋全域組件快取，這一次則會搜尋所要求文化特性的父組件。 如果父組件位於全域組件快取中，則執行階段會搜尋所要求資源的組件。

     父文化特性會定義為適當的後援文化特性。 請將父項視為後援候選項目，因為最好提供任何資源以擲回例外狀況。 此程序也可讓您重複使用資源。 只有在子文化特性不需要當地語系化所要求的資源時，才應該包括父層級的特定資源。 例如，如果您提供適用於 `en` (中性英文)、`en-GB` (英式英文) 和 `en-US` (美式英文) 的附屬組件，`en` 附屬組件就會包含一般術語，而 `en-GB` 和 `en-US` 附屬組件可以僅針對那些不同的詞彙提供覆寫。

6. 執行階段接著會檢查目前執行中組件的目錄，以查看它是否包含上層目錄。 如果已有上層目錄，則執行階段會搜尋目錄中是否有父文化特性的有效附屬組件。 如果找到組件，則執行階段會搜尋所要求資源的組件。 如果找到資源，則會使用它。 如果找不到資源，會繼續搜尋。

7. 執行階段接下來會查詢 Windows Installer，以判斷是否依需求安裝父附屬組件。 如果是這樣，它會處理安裝、載入組件，並搜尋它或所要求的資源。 如果在組件中找到資源，則會使用它。 如果找不到資源，會繼續搜尋。

8. 執行階段會引發 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件，指出找不到適當的後援資源。 如果您選擇處理事件，則事件處理常式會傳回其資源用於查閱之附屬組件的參考。 否則，事件處理常式會傳回 `null` 並繼續搜尋。

9. 執行階段接下來會如先前三個步驟所述搜尋父組件的多個可能層級。 每個文化特性都只有 <xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=nameWithType> 屬性所定義的一個父代，但是父代可能有其本身的父代。 文化特性的 <xref:System.Globalization.CultureInfo.Parent%2A> 屬性傳回 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 時，會停止搜尋父文化特性；針對資源後援，不會將不區分文化特性視為父文化特性或可有資源的文化特性。

10. 如果已搜尋原先指定的文化特性和所有父項，但仍然找不到資源，則會使用預設 (後援) 文化特性的資源。 通常，主要應用程式組件中會包含預設文化特性的資源。 不過，您可以指定 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性 (attribute) 之 <xref:System.Resources.NeutralResourcesLanguageAttribute.Location%2A> 屬性 (property) 的 <xref:System.Resources.UltimateResourceFallbackLocation.Satellite> 值，指出資源的最終後援位置是附屬組件，而不是主要組件。

    > [!NOTE]
    > 預設資源是可使用主要組件進行編譯的唯一資源。 除非您使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性指定附屬組件，否則它是最終後援 (最終父項)。 因此，建議您一律在主要組件中包括預設一組資源。 這樣有助於防止擲回例外狀況。 透過包括預設資源檔，您就能為所有資源提供後援，並確保使用者一律至少有一個資源，即使該資源不是文化特性特有的也一樣。

11. 最後，如果執行階段找不到預設 (後援) 文化特性的資源，則會擲回 <xref:System.Resources.MissingManifestResourceException> 或 <xref:System.Resources.MissingSatelliteAssemblyException> 例外狀況，指出找不到資源。

例如，假設應用程式要求已針對西班牙文 (墨西哥) (`es-MX` 文化特性) 進行當地語系化的資源。 執行階段會先在全域組件快取中搜尋符合 `es-MX` 的組件，但找不到。 執行階段接著會在目前執行中組件的目錄內搜尋 `es-MX` 目錄。 如果失敗，執行階段就會在全域組件快取中重新搜尋可反映適當後援文化特性的父組件，在此案例中為 `es` (西班牙文)。 如果找不到父組件，執行階段就會搜尋 `es-MX` 文化特性之父組件的所有可能層級，直到找到對應的資源為止。 如果找不到資源，執行階段會使用預設文化特性的資源。

<a name="Optimizing"></a>

#### <a name="optimizing-the-net-framework-resource-fallback-process"></a>將 .NET Framework 資源後援處理序最佳化

在下列情況中，您可以最佳化執行階段用來搜尋附屬組件中資源的程序。

- 附屬組件會部署在與程式碼組件相同的位置中。 如果程式碼組件安裝在[全域組件快取](../app-domains/gac.md)中，則也會將附屬組件安裝在全域組件快取中。 如果程式碼組件安裝在目錄中，則附屬組件會安裝在該目錄的文化特性特定資料夾中。

- 不會隨選安裝附屬組件。

- 應用程式碼不會處理 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件。

您可以在 [\<relativeBindForResources>](../configure-apps/file-schema/runtime/relativebindforresources-element.md) 應用程式佈建檔中包含專案並將其屬性設定為，以優化附屬元件的探查 `enabled` `true` ，如下列範例所示。

```xml
<configuration>
   <runtime>
      <relativeBindForResources enabled="true" />
   </runtime>
</configuration>
```

附屬組件的最佳化探查是選擇性功能。 也就是說，執行時間會遵循 [資源](packaging-and-deploying-resources-in-desktop-apps.md#cpconpackagingdeployingresourcesanchor1) 回溯程式中記載的步驟，除非該專案 [\<relativeBindForResources>](../configure-apps/file-schema/runtime/relativebindforresources-element.md) 存在於應用程式的設定檔中，而且其 `enabled` 屬性設定為 `true` 。 如果是這種情況，附屬組件的探查程序修改如下：

- 執行階段使用父程式碼組件的位置來探查附屬組件。 如果父組件安裝在全域組件快取中，則執行階段會在快取中探查，而不是在應用程式目錄中探查。 如果父組件安裝在應用程式目錄中，則執行階段會在應用程式目錄中探查，而不是在全域組件快取中探查。

- 執行階段不會查詢 Windows Installer 是否有附屬組件的隨選安裝。

- 如果探查特定資源組件失敗，則執行階段不會引發 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件。

### <a name="net-core-resource-fallback-process"></a>.NET Core 資源後援處理序

.NET Core 資源後援處理序包含下列步驟：

1. 執行階段會嘗試載入所要求文化特性的附屬組件。
     - 檢查目前執行中組件的目錄中是否有符合所要求文化特性的子目錄。 如果它找到子目錄，則會在該子目錄內搜尋所要求文化特性的有效附屬組件並載入它。

       > [!NOTE]
       > 在具備區分大小寫之檔案系統的作業系統 (也就是 Linux 和 macOS) 上，文化特性名稱子目錄搜尋會區分大小寫。 子目錄名稱必須完全符合 <xref:System.Globalization.CultureInfo.Name?displayProperty=nameWithType> 的大小寫 (例如 `es` 或 `es-MX`)。

       > [!NOTE]
       > 如果程式設計師已從 <xref:System.Runtime.Loader.AssemblyLoadContext> 衍生了自訂組件載入內容，則情況很複雜。 如果已將執行中組件載入到自訂內容，執行階段就會將附屬組件載入到自訂內容。 詳細資料不在本文的範圍內。 請參閱 <xref:System.Runtime.Loader.AssemblyLoadContext>。

     - 如果找不到附屬組件，<xref:System.Runtime.Loader.AssemblyLoadContext> 就會引發 <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> 事件，指出找不到附屬組件。 如果您選擇處理事件，則您的事件處理常式可以載入並傳回附屬組件的參考。
     - 如果仍然找不到附屬組件，AssemblyLoadContext 就會導致 AppDomain 觸發 <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> 事件，指出它找不到附屬組件。 如果您選擇處理事件，則您的事件處理常式可以載入並傳回附屬組件的參考。

2. 如果找到了附屬組件，執行階段就會在其中搜尋所要求的資源。 如果在組件中找到資源，則會使用它。 如果找不到資源，會繼續搜尋。

     > [!NOTE]
     > 為了在附屬組件內尋找資源，執行階段會搜尋目前 <xref:System.Globalization.CultureInfo.Name?displayProperty=nameWithType> 的 <xref:System.Resources.ResourceManager> 所要求的資源檔。 它會在資源檔內搜尋所要求的資源名稱。 如果找不到任一個，就會將資源視為找不到。

3. 執行階段接下來會透過許多可能的層級搜尋父文化特性組件，每次均會重複執行步驟 1 和 2。

     父文化特性會定義為適當的後援文化特性。 請將父項視為後援候選項目，因為最好提供任何資源以擲回例外狀況。 此程序也可讓您重複使用資源。 只有在子文化特性不需要當地語系化所要求的資源時，才應該包括父層級的特定資源。 例如，如果您提供適用於 `en` (中性英文)、`en-GB` (英式英文) 和 `en-US` (美式英文) 的附屬組件，`en` 附屬組件就會包含一般術語，而 `en-GB` 和 `en-US` 附屬組件僅會針對那些不同的詞彙提供覆寫。

     每個文化特性都只有 <xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=nameWithType> 屬性所定義的一個父代，但是父代可能有其本身的父代。 當文化特性的 <xref:System.Globalization.CultureInfo.Parent%2A> 屬性傳回 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> 時，即會停止搜尋父文化特性。 針對資源後援，不會將不因文化特性而異視為父文化特性或可擁有資源的文化特性。

4. 如果已搜尋原先指定的文化特性和所有父項，但仍然找不到資源，則會使用預設 (後援) 文化特性的資源。 通常，主要應用程式組件中會包含預設文化特性的資源。 不過，您可以指定 <xref:System.Resources.NeutralResourcesLanguageAttribute.Location%2A> 屬性的 <xref:System.Resources.UltimateResourceFallbackLocation.Satellite?displayProperty.nameWithType> 值，指出資源的最終後援位置是附屬組件，而不是主要組件。

    > [!NOTE]
    > 預設資源是可使用主要組件進行編譯的唯一資源。 除非您使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性指定附屬組件，否則它是最終後援 (最終父項)。 因此，建議您一律在主要組件中包括預設一組資源。 這樣有助於防止擲回例外狀況。 透過包括預設資源檔，您就能為所有資源提供後援，並確保使用者一律至少有一個資源，即使該資源不是文化特性特有的也一樣。

5. 最後，如果執行階段找不到預設 (後援) 文化特性的資源檔，即會擲回 <xref:System.Resources.MissingManifestResourceException> 或 <xref:System.Resources.MissingSatelliteAssemblyException> 例外狀況，指出找不到資源。 如果找到了資源檔，但所要求的資源不存在，要求就會傳回 `null`。

### <a name="ultimate-fallback-to-satellite-assembly"></a>附屬組件的最終後援

您可以選擇性地從主要組件中移除資源，並指定執行階段應該從對應至特定文化特性的附屬組件中載入最終後援資源。 若要控制後援程序，請使用 <xref:System.Resources.NeutralResourcesLanguageAttribute.%23ctor%28System.String%2CSystem.Resources.UltimateResourceFallbackLocation%29> 建構函式，並提供 <xref:System.Resources.UltimateResourceFallbackLocation> 參數的值，而此參數指定 Resource Manager 應該從主要組件還是附屬組件擷取後援資源。

下列 .NET Framework 範例會使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性，將應用程式的後援資源儲存在法文 (`fr`) 語言的附屬組件中。 此範例有兩個文字型資源檔案定義名為 `Greeting` 的單一字串資源。 首先，resources.fr.txt 包含法文語言資源。

```text
Greeting=Bon jour!
```

其次，resources,ru.txt 包含俄文語言資源。

```text
Greeting=Добрый день
```

從命令列執行[資源檔產生器 (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)，以將這兩個檔案編譯成 .resources 檔案。 法文語言資源的命令為：

**resgen.exe resources.fr.txt**

俄文語言資源的命令為：

**resgen.exe resources.ru.txt**

從法文語言資源的命令列執行[組件連結器 (Al.exe)](../tools/al-exe-assembly-linker.md) 以將 .resources 檔案內嵌到動態連結程式庫，如下所示：

**al /t:lib /embed:resources.fr.resources /culture:fr /out:fr\Example1.resources.dll**

而俄文語言資源如下所示：

**al /t:lib /embed:resources.ru.resources /culture:ru /out:ru\Example1.resources.dll**

應用程式原始程式碼位在名為 Example1.cs 或 Example1.vb 的檔案中。 它會包括 <xref:System.Resources.NeutralResourcesLanguageAttribute> 屬性，指出預設應用程式資源是在 fr 子目錄中。 它會執行個體化 Resource Manager、擷取 `Greeting` 資源的值，並將它顯示到主控台。

[!code-csharp[Conceptual.Resources.Packaging#1](~/samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.packaging/cs/example1.cs#1)]
[!code-vb[Conceptual.Resources.Packaging#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.packaging/vb/example1.vb#1)]

您接著可以從命令列編譯 C# 原始程式碼，如下所示：

```console
csc Example1.cs
```

Visual Basic 編譯器的命令十分類似：

```console
vbc Example1.vb
```

因為主要組件中未內嵌任何資源，所以您不需要使用 `/resource` 切換參數進行編譯。

當您從語言非俄文的系統執行此範例時，會顯示下列輸出：

```output
Bon jour!
```

## <a name="suggested-packaging-alternative"></a>建議的封裝替代方式

時間或預算限制可能會讓您無法針對應用程式所支援的每個子文化特性建立一組資源。 相反地，您可以建立所有相關子文化特性可使用之父文化特性的單一附屬組件。 例如，您可以提供要求地區特定英文資源之使用者所擷取的單一英文附屬組件 (en)，以及要求地區特定德文資源之使用者的單一德文附屬組件 (de)。 例如，德國德文 (de-DE)、奧地利德文 (de-AT) 和瑞士德文 (de-CH) 的要求會改為使用德文附屬組件 (de)。 預設資源是最終後援，因此應該是大部分應用程式使用者所要求的資源，請小心選擇這些資源。 這種方式所部署的資源具有較少的特定文化特性，但可以大幅減少您應用程式的當地語系化成本。

## <a name="see-also"></a>另請參閱

- [桌面應用程式中的資源](index.md)
- [全域組件快取](../app-domains/gac.md)
- [建立資源檔](creating-resource-files-for-desktop-apps.md)
- [建立附屬組件](creating-satellite-assemblies-for-desktop-apps.md)
