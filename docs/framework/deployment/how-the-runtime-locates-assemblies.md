---
title: 執行階段如何找出組件
description: 瞭解 common language runtime （CLR）如何找出並系結至在 .NET 中組成應用程式的元件。
ms.date: 03/30/2017
helpviewer_keywords:
- app.config files, assembly locations
- deploying applications [.NET Framework], assembly locations
- application configuration files, locating assemblies
- .NET Framework application deployment, locating assemblies
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 772ac6f4-64d2-4cfb-92fd-58096dcd6c34
ms.openlocfilehash: 4cf1e5787fe2e430d20208d8e79b610e9126c67c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622623"
---
# <a name="how-the-runtime-locates-assemblies"></a>執行階段如何找出組件

若要成功部署 .NET Framework 應用程式，您必須了解 Common Language Runtime 如何找出並繫結至構成應用程式的組件。 根據預設，執行階段會嘗試與用來建置應用程式的組件正確版本繫結。 組態檔設定可覆寫這個預設行為。

在嘗試找出組件，並解析組件參考時，Common Language Runtime 會執行數個步驟。 以下各節將會說明每個步驟。 在說明執行階段如何找出組件時，常會使用詞彙探查；它會依據其名稱和文化特性，參考用來尋找組件的啟發學習法集合。

> [!NOTE]
> 您可以使用 Windows SDK 中隨附的[組件繫結記錄檢視器 (Fuslogvw.exe)](../tools/fuslogvw-exe-assembly-binding-log-viewer.md) 來檢視記錄檔中的繫結資訊。

## <a name="initiating-the-bind"></a>初始化繫結

當執行階段嘗試將參考解析成另一個組件時，尋找並繫結至組件的程序即開始。 此參考可以是靜態或動態。 編譯器會在建置時，將靜態參考記錄在組件資訊清單的中繼資料中。 動態參考則是呼叫各種方法 (例如 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>) 時，即時建構的結果。

參考組件時，最好是使用完整參考，包括組件名稱、版本、文化特性和公開金鑰語彙基元 (如果有的話)。 執行階段會使用此資訊來尋找組件 (依照本節稍後說明的步驟)。 不論是靜態或動態組件的參考，執行階段都會使用相同的解析程序。

您也可以只提供組件的部分資訊給呼叫方法 (例如只指定組件名稱)，以對組件進行動態參考。 在此情況下，只會搜尋組件的應用程式目錄，而不會進行任何其他檢查。 您可以使用 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 或 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>等各種方法來載入組件，以進行部分參考。

最後，您可以使用之類的方法來建立動態參考 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> ，只提供部分資訊; 接著，您可以使用 [\<qualifyAssembly>](../configure-apps/file-schema/runtime/qualifyassembly-element.md) 應用程式佈建檔中的專案來限定參考。 這個項目可讓您在應用程式組態檔中，而不是在您的程式碼中，提供完整的參考資訊 (名稱、版本、文化特性和 (適用的話) 公開金鑰語彙基元)。 如果您想要完整限定參考外部應用程式目錄中的組件，或者如果您想要參考全域組件快取中的組件，但又想要在組態檔中 (而不是在您的程式碼中) 指定完整參考的方便性，您就會使用這項技術。

> [!NOTE]
> 這種類型的部分參考不應該用於數個應用程式之間共用的組件。 因為組態設定是依各應用程式來套用，而且依各組件，所以使用這種部分參考的共用組件，會要求使用共用組件的每個應用程式，在其組態檔中都要有合格的資訊。

執行階段會使用下列步驟來解析組件參考：

1. 檢查適用的組態檔，包括應用程式組態檔、發行者原則檔和電腦組態檔，以[判斷正確的組件版本](#step1) 。 如果組態檔位於遠端電腦上，執行階段必須先找出並下載應用程式組態檔。

2. [檢查組件名稱之前是否已經被繫結](#step2) ，如果是的話，會使用先前載入的組件。 如果先前載入組件的要求失敗，此要求會立即失敗，而不會嘗試載入組件。

    > [!NOTE]
    > 快取組件繫結失敗是 .NET Framework 2.0 版的新功能。

3. [檢查全域組件快取](#step3)。 如果那裡找到組件，執行階段會使用此組件。

4. 使用下列步驟來[探查組件](#step4) ：

    1. 如果組態和發行者原則不會影響原始參考，而且如果繫結要求是使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法來建立的，執行階段會檢查位置提示。

    2. 如果在組態檔中找到程式碼基底，執行階段只會檢查這個位置。 如果此探查失敗，執行階段會判定繫結要求失敗，且不會再發生其他探查。

    3. [探查一節](#step4)中會說明如何使用啟發學習法來探查組件。 如果在探查之後找不到組件，執行階段會要求 Windows Installer 提供組件。 這可以做為隨選安裝功能。

        > [!NOTE]
        > 針對沒有強式名稱的組件，不會進行版本檢查，執行階段也不會在全域組件快取中檢查沒有強式名稱的組件。

<a name="step1"></a>

## <a name="step-1-examining-the-configuration-files"></a>步驟 1：檢查組態檔

根據下列三個 XML 檔案，可以在不同層級設定組件繫結行為：

- 應用程式組態檔。

- 發行者原則檔。

- 電腦組態檔。

這些檔案遵循相同的語法，並提供繫結重新導向、程式碼位置，以及特定組件的繫結模式等資訊。 每個設定檔都可以包含重新導向系結進程的[ \<assemblyBinding> 元素](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)。 [ \<assemblyBinding> 元素](../configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)的子專案包含[ \<dependentAssembly> 專案。](../configure-apps/file-schema/runtime/dependentassembly-element.md) [ \<dependentAssembly> 元素](../configure-apps/file-schema/runtime/dependentassembly-element.md)的子系包括[ \<assemblyIdentity> 元素](/visualstudio/deployment/assemblyidentity-element-clickonce-deployment)、專案和[ \<bindingRedirect> ](../configure-apps/file-schema/runtime/bindingredirect-element.md)專案[ \<codeBase> 。](../configure-apps/file-schema/runtime/codebase-element.md)

> [!NOTE]
> 您可以在這三個組態檔中找到組態資訊；並非所有組態檔中的所有項目都有效。 例如，繫結模式和私用路徑資訊只能在應用程式組態檔中。 如需每個檔案內含資訊的完整清單，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。

### <a name="application-configuration-file"></a>應用程式組態檔

第一，Common Language Runtime 會檢查應用程式組態檔中，是否有資訊會覆寫儲存在呼叫組件資訊清單中的版本資訊。 應用程式組態檔可以隨著應用程式一起部署，但並不是執行應用程式的必要項目。 通常擷取這個檔案幾乎是瞬間完成，但是如果應用程式基底是在遠端電腦上 (例如在 Internet Explorer Web 架構案例中)，就必須下載組態檔。

針對用戶端可執行檔，應用程式組態檔會位在與應用程式可執行檔相同的目錄中，而且基底名稱與可執行檔相同，副檔名為 .config。 例如，C:\Program Files\Myapp\Myapp.exe 的設定檔是 C:\Program Files\Myapp\Myapp.exe.config。在以瀏覽器為基礎的案例中，HTML 檔案必須使用 **\<link>** 元素明確指向設定檔。

下列程式碼提供應用程式組態檔的簡單範例。 這個範例會將 <xref:System.Diagnostics.TextWriterTraceListener> 加入 <xref:System.Diagnostics.Debug.Listeners%2A> 集合，以啟用將偵錯資訊記錄至檔案的功能。

```xml
<configuration>
   <system.diagnostics>
      <trace useGlobalLock="false" autoflush="true" indentsize="0">
         <listeners>
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />
         </listeners>
      </trace>
   </system.diagnostics>
</configuration>
```

### <a name="publisher-policy-file"></a>發行者原則檔

第二，執行階段會檢查發行者原則檔 (如果有的話)。 元件發行者會將發行者原則檔以修正或更新形式發佈至共用元件。 這些檔案包含共用元件發行者所發行的相容性資訊，可將組件參考導向至新版本。 不同於應用程式和電腦組態檔，發行者原則檔是包含在自己的組件中，必須安裝在全域組件快取中。

發行者原則組態檔的範例如下：

```xml
<configuration>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">

            <dependentAssembly>
                <assemblyIdentity name="asm6" publicKeyToken="c0305c36380ba429" />
                <bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0"/>
            </dependentAssembly>

        </assemblyBinding>
    </runtime>
</configuration>
```

若要建立組件，您可以使用[組件連結器 (Al.exe)](../tools/al-exe-assembly-linker.md) 工具來搭配如下命令：

```console
Al.exe /link:asm6.exe.config /out:policy.3.0.asm6.dll /keyfile: compatkey.dat /v:3.0.0.0
```

`compatkey.dat` 是強式名稱金鑰檔案。 此命令會建立可以放在全域組件快取中的強式名稱組件。

> [!NOTE]
> 發行者原則會影響使用共用元件的所有應用程式。

發行者原則組態檔會覆寫來自應用程式的版本資訊 (也就是來自組件資訊清單，或來自應用程式組態檔)。 如果應用程式組態檔中沒有陳述式來將組件資訊清單中指定的版本重新導向，發行者原則檔就會覆寫組件資訊清單中指定的版本。 不過，如果應用程式組態檔中有重新導向陳述式，發行者原則會覆寫該版本，而不是資訊清單中指定的版本。

當共用元件更新時，就會使用發行者原則檔，而且使用該元件的所有應用程式，都應該收取共用元件的新版本。 除非應用程式組態檔強制執行安全模式，否則發行者原則檔中的設定會覆寫應用程式組態檔中的設定。

#### <a name="safe-mode"></a>安全模式
發行者原則檔通常會做為 Service Pack 或程式更新的一部分明確安裝。 如果升級後的共用元件有任何問題，您可以使用安全模式來忽略發行者原則檔中的覆寫。 安全模式是由專案所決定，該專案 **\<publisherPolicy apply="yes**&#124;**no"/>** 僅位於應用程式佈建檔中。 它會指定是否應該將發行者原則組態資訊從繫結程序中移除。

您可以針對整個應用程式或選取的組件來設定安全模式。 亦即，您可以針對構成應用程式的所有組件，關閉此原則，或是針對某些組件開啟此原則，但其他組件不開啟此原則。 若要選擇性地將發行者原則套用至構成應用程式的元件，請設定 **\<publisherPolicy apply\=no/>** 並指定您想要使用元素影響的元件 \<**dependentAssembly**> 。 若要將發行者原則套用至構成應用程式的所有元件，請設定 **\<publisherPolicy apply\=no/>** 無相依元件元素。 如需組態的詳細資訊，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。

### <a name="machine-configuration-file"></a>電腦組態檔
第三，執行階段會檢查電腦組態檔。 此檔案名為 Machine.config，位在本機電腦上，執行階段安裝所在之根目錄的 Config 子目錄中。 系統管理員可以使用這個檔案來指定電腦本機的組件繫結限制。 電腦組態檔中的設定優先順序高於所有其他組態設定；不過，這不表示所有組態設定都應該放在這個檔案中。 系統管理員原則檔決定的版本為最終版本，不能覆寫。 在 Machine.config 檔案中指定覆寫會影響所有應用程式。 如需組態檔的詳細資訊，請參閱 [使用組態檔設定應用程式](../configure-apps/index.md)。

<a name="step2"></a>

## <a name="step-2-checking-for-previously-referenced-assemblies"></a>步驟 2：檢查先前參考的組件

如果先前的呼叫中也有要求現在所要求的組件，Common Language Runtime 會使用已載入的組件。 在為構成應用程式的組件命名時，這可能會有分歧。 如需有關為組件命名的詳細資訊，請參閱 [組件名稱](../../standard/assembly/names.md)。

如果先前要求組件失敗，後續要求該組件會立即失敗，而不會嘗試載入組件。 從 .NET Framework 2.0 版開始，會快取組件繫結失敗，而所快取的資訊會用來判斷是否要嘗試載入組件。

> [!NOTE]
> 若要還原為不會快取系結失敗之 .NET Framework 版本1.0 和1.1 的行為，請在您的設定檔中包含[ \<disableCachingBindingFailures> 元素](../configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md)。

<a name="step3"></a>

## <a name="step-3-checking-the-global-assembly-cache"></a>步驟 3：檢查全域組件快取

針對強式名稱組件，繫結程序會繼續在全域組件快取中查看。 全域組件快取會儲存可供電腦上數個應用程式使用的組件。 全域組件快取中的所有組件都必須具有強式名稱。

<a name="step4"></a>

## <a name="step-4-locating-the-assembly-through-codebases-or-probing"></a>步驟 4：透過程式碼基底或探查找出組件

使用呼叫組件參考和組態檔中的資訊來判斷正確的組件版本之後，以及在其簽入全域組件快取 (僅適用於強式名稱組件) 之後，Common Language Runtime 會嘗試尋找組件。 尋找組件的程序包含下列步驟：

1. 如果在 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 應用程式佈建檔中找到元素，執行時間就會檢查指定的位置。 如果找到相符項目，則會使用該組件，而不會進行探查。 如果在那裡沒有找到該組件，則繫結要求會失敗。

2. 然後執行階段會使用本節稍後指定的規則來探查參考的組件。

> [!NOTE]
> 如果目錄中有多個版本的元件，而您想要參考該元件的特定版本，您必須使用專案， [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 而不是專案的 `privatePath` 屬性 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) 。 如果您使用專案 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) ，執行時間會在第一次找到符合所參考之簡單元件名稱的元件時停止探查，不論它是否為正確的相符專案。 如果是正確的相符項目，就會使用該組件。 如果不是正確的相符項目，就會停止探查，且繫結失敗。

### <a name="locating-the-assembly-through-codebases"></a>透過程式碼基底找出組件

程式碼基底資訊可以使用 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 設定檔中的元素來提供。 在執行階段嘗試探查參考的組件之前，一定會先檢查此程式碼基底。 如果包含最終版本重新導向的發行者原則檔也包含 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 元素，該專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 就是所使用的元素。 例如，如果您的應用程式佈建檔指定專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，而覆寫應用程式資訊的發行者原則檔也指定了專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，則 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 會使用發行者原則檔中的元素。

如果在元素指定的位置找不到相符專案 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，則系結要求會失敗，且不會採取任何進一步的步驟。 如果執行階段判斷有組件符合呼叫組件的準則，就會使用該組件。 當載入指定專案所指定的檔案時 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) ，執行時間會進行檢查，以確定名稱、版本、文化特性和公開金鑰與呼叫元件的參考相符。

> [!NOTE]
> 應用程式根目錄之外的參考元件必須具有強式名稱，而且必須安裝在全域組件快取中，或使用元素指定 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 。

### <a name="locating-the-assembly-through-probing"></a>透過探查找出組件

如果 [\<codeBase>](../configure-apps/file-schema/runtime/codebase-element.md) 應用程式佈建檔中沒有專案，則執行時間會使用四個準則來探查元件：

- 應用程式基底，這是執行應用程式所在的根位置。

- 文化特性，這是所參考之組件的文化特性屬性。

- 名稱，這是所參考之組件的名稱。

- `privatePath`元素的屬性 [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) ，這是根位置底下的使用者定義子目錄清單。 您可以使用應用程式定義域的 <xref:System.AppDomainSetup.PrivateBinPath?displayProperty=nameWithType> 屬性，將這個位置指定在應用程式組態檔和 Managed 程式碼中。 如果指定在 Managed 程式碼中，會先探查 Managed 程式碼 `privatePath` ，後面接著應用程式組態檔中指定的路徑。

#### <a name="probing-the-application-base-and-culture-directories"></a>探查應用程式基底和文化特性目錄

執行階段一定會從應用程式的基底開始探查，該基底可以是 URL，或是應用程式在電腦上的根目錄。 如果在應用程式基底中找不到參考的組件，而且沒有提供任何文化特性資訊，執行階段會搜尋具有該組件名稱的任何子目錄。 所探查的目錄包括：

- [應用程式基底] / [組件名稱].dll

- [應用程式基底] / [組件名稱] / [組件名稱].dll

如果有為參考的組件指定文化特性資訊，就只會探查下列目錄：

- [應用程式基底] / [文化特性] / [組件名稱].dll

- [應用程式基底] / [文化特性] / [組件名稱] / [組件名稱].dll

#### <a name="probing-with-the-privatepath-attribute"></a>使用 privatePath 屬性進行探查

除了文化特性子目錄以及為參考元件所命名的子目錄以外，執行時間也會探查使用專案的屬性指定的目錄 `privatePath` [\<probing>](../configure-apps/file-schema/runtime/probing-element.md) 。 使用 `privatePath` 屬性來指定的目錄，必須是應用程式根目錄的子目錄。 所探查的目錄會因為文化特性資訊是否包含在參考的組件要求中而有所不同。

執行階段只要一找到符合所參考之簡單組件名稱的組件 (無論是否確實相符)，就會停止探查。 如果是正確的相符項目，就會使用該組件。 如果不是正確的相符項目，就會停止探查，且繫結失敗。

如果包含文化特性，就會探查下列目錄：

- [應用程式基底] / [bin 路徑] / [文化特性] / [組件名稱].dll

- [應用程式基底] / [bin 路徑] / [文化特性] / [組件名稱] / [組件名稱].dll

如果沒有包含文化特性資訊，就會探查下列目錄：

- [應用程式基底] / [bin 路徑] / [組件名稱].dll

- [應用程式基底] / [bin 路徑] / [組件名稱] / [組件名稱].dll

#### <a name="probing-examples"></a>探查範例

假設有下列資訊：

- 參考的組件名稱：myAssembly

- 應用程式根目錄：`http://www.code.microsoft.com`

- [\<probing>](../configure-apps/file-schema/runtime/probing-element.md)設定檔中的元素指定： bin

- 文化特性：de

執行階段會探查下列 URL：

- `http://www.code.microsoft.com/de/myAssembly.dll`

- `http://www.code.microsoft.com/de/myAssembly/myAssembly.dll`

- `http://www.code.microsoft.com/bin/de/myAssembly.dll`

- `http://www.code.microsoft.com/bin/de/myAssembly/myAssembly.dll`

##### <a name="multiple-assemblies-with-the-same-name"></a>具有相同名稱的多個組件

下列範例示範如何設定具有相同名稱的多個組件。

```xml
<dependentAssembly>
   <assemblyIdentity name="Server" publicKeyToken="c0305c36380ba429" />
   <codeBase version="1.0.0.0" href="v1/Server.dll" />
   <codeBase version="2.0.0.0" href="v2/Server.dll" />
</dependentAssembly>
```

#### <a name="other-locations-probed"></a>探查的其他位置

組件位置也可以使用目前的繫結內容來決定。 當使用 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 方法時，以及在 COM Interop 案例中，最常發生這個情況。 如果組件使用 <xref:System.Reflection.Assembly.LoadFrom%2A> 方法來參考另一個組件，呼叫組件的位置會被視為有關在哪裡可以找到參考組件的提示。 如果找到相符項目，就會載入該組件。 如果沒有找到相符項目，執行階段會繼續進行其搜尋語意，然後查詢 Windows Installer，以提供組件。 如果沒有提供符合繫結要求的組件，則會擲回例外狀況。 如果有參考類型，此例外狀況是 Managed 程式碼中的 <xref:System.TypeLoadException> ，如果找不到要載入的組件，則為 <xref:System.IO.FileNotFoundException> 。

比方說，如果 Assembly1 參考 Assembly2，而且 Assembly1 是從 `http://www.code.microsoft.com/utils` 下載，則該位置會被視為有關在哪裡可以找到 Assembly2.dll 的提示。 執行階段接著會探查 `http://www.code.microsoft.com/utils/Assembly2.dll` 和 `http://www.code.microsoft.com/utils/Assembly2/Assembly2.dll` 中的組件。 如果在這兩個位置都找不到 Assembly2，執行階段就會查詢 Windows Installer。

## <a name="see-also"></a>另請參閱

- [組件載入的最佳做法](best-practices-for-assembly-loading.md)
- [部署](index.md)
