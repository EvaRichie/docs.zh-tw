---
title: .NET Native 使用者入門
ms.date: 03/30/2017
ms.assetid: fc9e04e8-2d05-4870-8cd6-5bd276814afc
ms.openlocfilehash: b6cd4acaa377de7fc172fb12c9fb9ff1b832f88a
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90551206"
---
# <a name="getting-started-with-net-native"></a>.NET Native 使用者入門

不論是為了 Windows 10 撰寫新的 Windows 應用程式，或是移轉現有的 Windows 市集應用程式，都可遵循一組相同的程序進行。 若要建立 .NET Native 應用程式，請遵循下列步驟：

1. [開發以 Windows 10 為目標的通用 Windows 平台 (UWP) 應用程式](#Step1)，並測試應用程式的偵錯組建，以確保運作正常。

2. [處理其他反映和序列化使用方式](#Step2)。

3. [部署並測試應用程式的發行組建](#Step3)。

4. [手動解決遺漏中繼資料的問題](#Step4)，然後重複 [步驟 3](#Step3) 直到所有問題解決為止。

> [!NOTE]
> 如果您要將現有的 Windows Store 應用程式遷移至 .NET Native，請務必檢查將 [您的 Windows Store 應用程式遷移至 .NET Native](migrating-your-windows-store-app-to-net-native.md)。

<a name="Step1"></a>

## <a name="step-1-develop-and-test-debug-builds-of-your-uwp-app"></a>步驟 1：開發並測試 UWP 應用程式的偵錯組建

不論您要開發新的應用程式，或移轉現有的應用程式，都會遵循與所有 Windows 應用程式相同的程序。

1. 使用適用於 Visual C# 或 Visual Basic 的通用 Windows 應用程式範本，在 Visual Studio 中建立新的 UWP 專案。 根據預設，所有 UWP 應用程式都會以 CoreCLR 為目標，而其發行組建則使用 .NET Native 工具鏈進行編譯。

2. 請注意，使用 .NET Native 工具鏈編譯 UWP 應用程式專案與不使用此工具進行編譯之間有一些已知的相容性問題。 如需詳細資訊，請參閱 [移轉指南](migrating-your-windows-store-app-to-net-native.md) 。

您現在可以針對在本機系統 (或模擬器) 中執行的 .NET Native 介面區，撰寫 c # 或 Visual Basic 程式碼。

> [!IMPORTANT]
> 當您開發應用程式時，請記下在程式碼中使用的任何序列化或反映。

根據預設，debug 組建會以 JIT 編譯來啟用快速的 F5 部署，而發行組建則是使用 .NET Native 預先編譯技術來編譯。 這表示您應該建置並測試應用程式的偵錯組建以確保運作正常，再使用 .NET Native 工具鏈進行編譯。

<a name="Step2"></a>

## <a name="step-2-handle-additional-reflection-and-serialization-usage"></a>步驟 2：處理其他的反映和序列化使用

當您建立專案時會自動將執行階段指示詞檔 Default.rd.xml 加入您的專案。 如果您以 C# 進行開發，它位於您專案的 [屬性] **** 資料夾。 如果您以 Visual Basic 進行開發，它位於您專案的 [我的專案] **** 資料夾。

> [!NOTE]
> 如需 .NET 原生編譯程序的概觀 (其提供需要執行階段指示詞檔案的背景資訊)，請參閱 [.NET 原生和編譯](net-native-and-compilation.md)。

執行階段指示詞檔案會用來定義您的應用程式在執行階段所需的中繼資料。 在某些情況下，檔案的預設版本應已足夠。 不過，某些相依於序列化或反映的程式碼可能需要執行階段指示詞檔案中的其他項目。

**序列化**

序列化程式可分為兩種類別，這兩種類別都需要執行階段指示詞檔案中的其他項目：

- 非反映型序列化程式。 .NET Framework 類別庫中不依賴反映的序列化程式，例如 <xref:System.Runtime.Serialization.DataContractSerializer>、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>和 <xref:System.Xml.Serialization.XmlSerializer> 類別。 不過，這些序列化程式需要依據所要序列化或還原序列化的物件來產生程式碼。  如需詳細資訊，請參閱 [Serialization and Metadata](serialization-and-metadata.md)中的＜Microsoft 序列化程式＞一節。

- 協力廠商序列化程式。 協力廠商序列化程式庫是最常見的 Newtonsoft JSON 序列化程式，通常是以反映為基礎，而且需要.rd.xml 檔中的專案， \* 以支持對象序列化和還原序列化。 如需詳細資訊，請參閱 [Serialization and Metadata](serialization-and-metadata.md)中的＜協力廠商序列化程式＞一節。

**依賴反映的方法**

在某些情況下，很難察覺程式碼中是否有使用反映。 某些常見的 API 或程式設計模式不是反映 API 的一部分，但依賴反映才能順利執行。 其中包括下列類型具現化和方法建構方法：

- <xref:System.Type.MakeGenericType%2A?displayProperty=nameWithType> 方法

- <xref:System.Array.CreateInstance%2A?displayProperty=nameWithType> 和 <xref:System.Type.MakeArrayType%2A?displayProperty=nameWithType> 方法

- <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=nameWithType> 方法

如需詳細資訊，請參閱 [APIs That Rely on Reflection](apis-that-rely-on-reflection.md)。

> [!NOTE]
> 執行階段指示詞檔案中使用的類型名稱必須是完整名稱。 例如，檔案必須指定 "System.String"，而不是 "String"。

<a name="Step3"></a>

## <a name="step-3-deploy-and-test-the-release-builds-of-your-app"></a>步驟 3：部署並測試應用程式的發行組建

更新執行階段指示詞檔案之後，您可以重建並部署應用程式的發行組建。 .NET Native 二進位檔會放在專案的 [**屬性**] 對話方塊的 [**組建輸出路徑**] 文字方塊中指定之目錄的 [ilc.out] 子目錄中，[**編譯**] 索引標籤。未在此資料夾中的二進位檔未使用 .NET Native 編譯。 請在其目標平台上完整測試您的應用程式，並測試所有情況，包括失敗情況。

如果您的應用程式無法正常運作 (特別是如果在執行階段擲回 [MissingMetadataException](missingmetadataexception-class-net-native.md) 或 [MissingInteropDataException](missinginteropdataexception-class-net-native.md) 例外狀況)，請遵循下一節[步驟 4：手動解決遺漏中繼資料的問題](#Step4)中的指示進行。 啟用第一個可能發生的例外狀況可協助您尋找這些錯誤。

當您已測試並調試您的應用程式的偵錯工具組建，並確信您消除了 [MissingMetadataException](missingmetadataexception-class-net-native.md) 和 [MissingInteropDataException](missinginteropdataexception-class-net-native.md) 例外狀況之後，您應該將應用程式測試為優化的 .NET Native 應用程式。 若要執行這項操作，請將使用中的專案組態從 [偵錯] **** 變更為 [發行] ****。

<a name="Step4"></a>

## <a name="step-4-manually-resolve-missing-metadata"></a>步驟 4：手動解決遺漏中繼資料的問題

您在桌面上不會遇到的 .NET Native 最常見的失敗，就是執行時間 [MissingMetadataException](missingmetadataexception-class-net-native.md)、 [MissingInteropDataException](missinginteropdataexception-class-net-native.md)或 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外狀況。 在某些情況下，缺少中繼資料會發生未預期的行為，甚至導致應用程式失敗。 本節討論如何將指示詞加入至執行階段指示詞檔案，來偵錯及解決這些例外狀況。 如需執行階段指示詞格式的資訊，請參閱[執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)。 新增執行階段指示詞之後，您應該重新[部署和測試應用程式](#Step3)，並解決任何新的 [MissingMetadataException](missingmetadataexception-class-net-native.md)、[MissingInteropDataException](missinginteropdataexception-class-net-native.md) 和 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 例外狀況，直到未遇到其他任何例外狀況為止。

> [!TIP]
> 在較高層級指定執行階段指示詞，可讓應用程式彈性地回應程式碼變更。  建議在命名空間和類型層級加入執行階段指示詞，而不是在成員層級加入執行階段指示詞。 請注意，您可能需要在彈性與較大二進位檔案需要更長編譯時間之間進行取捨。

解決遺漏中繼資料的例外狀況時，請考慮下列問題：

- 發生例外狀況之前，應用程式正嘗試執行哪項作業？

  - 例如，應用程式正在執行資料繫結、序列化或還原序列化資料，還是直接使用反映 API？

- 這是獨立案例，還是您認為其他類型也會遇到相同問題？

  - 例如，當序列化應用程式物件模型中的類型時，擲回 [MissingMetadataException](missingmetadataexception-class-net-native.md) 例外狀況。  如果您知道即將序列化其他類型，您可以同時針對這些類型 (視程式碼組織程度而定也可能針對其包含命名空間) 加入執行階段指示詞。

- 是否可以重寫程式碼使其不使用反映？

  - 例如，當您知道預期類型時，程式碼是否使用 `dynamic` 關鍵字？

  - 程式碼是否在有一些更佳的替代方案時，呼叫相依於反映的方法？

> [!NOTE]
> 如需處理源自于桌面應用程式和 .NET Native 中的反映和中繼資料可用性差異之問題的詳細資訊，請參閱 [依賴反映的 api](apis-that-rely-on-reflection.md)。

如需處理測試應用程式時所發生之例外狀況和其他問題的一些特定範例，請參閱：

- [範例：處理繫結資料時所發生的例外狀況](example-handling-exceptions-when-binding-data.md)

- [範例：針對動態程式設計進行疑難排解](example-troubleshooting-dynamic-programming.md)

- [.NET 原生 App 中的執行階段例外狀況](runtime-exceptions-in-net-native-apps.md)

## <a name="see-also"></a>另請參閱

- [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)
- [.NET Native 設定和組態](/previous-versions/dn600164(v=vs.110))
- [.NET 原生和編譯](net-native-and-compilation.md)
- [反映和 .NET Native](reflection-and-net-native.md)
- [依賴反映的 API](apis-that-rely-on-reflection.md)
- [序列化和中繼資料](serialization-and-metadata.md)
- [將您的 Windows 市集應用程式移轉至 .NET Native](migrating-your-windows-store-app-to-net-native.md)
