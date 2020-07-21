---
title: 風險降低：產品版本
description: 在本文中，您將瞭解如何 .NET Framework 4.6 和更新版本的產品版本已從舊版變更。
ms.date: 03/30/2017
ms.assetid: 1c4de9d7-9aba-427a-8f38-0ab9bfb8f85e
ms.openlocfilehash: 442c06446e763758d3a150ee9ff884a616541c07
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475394"
---
# <a name="mitigation-product-versioning"></a>風險降低：產品版本

在 .NET Framework 4.6 和更新版本中，舊版 .NET Framework (.NET Framework 4、4.5、4.5.1 和 4.5.2) 的產品版本均有所變更。

## <a name="product-versioning-changes"></a>產品版本變更

以下是詳細的變更：

- `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` 機碼中的 `Version` 項目值已變更為 `4.6.`*xxxxx* (.NET Framework 4.6 及其點發行版本)，以及 `4.7.`*xxxxx* (.NET Framework 4.7)。 在 .NET Framework 4.5、4.5.1 和 4.5.2 中，其格式為 `4.5.`*xxxxx*。

- .NET Framework 檔案的檔案和產品版本已從舊版配置 `4.0.30319.x` 變更為 `4.6.X.0` (.NET Framework 4.6 及其點發行版本)，以及 `4.7.X.0` (.NET Framework 4.7 及其點發行版本)。 在檔案上按一下滑鼠**右鍵之後，** 您就可以看到這些新值。

- Managed 組件的 <xref:System.Reflection.AssemblyFileVersionAttribute> 和 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 屬性，對於 .NET Framework 4.6 及其點版本，其 <xref:System.Version> 值的格式為 `4.6.X.0`，對於 .NET Framework 4.7，格式則為 `4.7.X.0`。

- 從 .NET Framework 4.6 開始，<xref:System.Environment.Version%2A?displayProperty=nameWithType> 屬性會傳回固定的版本字串 `4.0.30319.42000`。 在 .NET Framework 4、4.5、4.5.1 和 4.5.2 中，其會以 `4.0.30319.xxxxx` 格式傳回版本字串，其中 `xxxxx` 會小於 42000 (例如 "4.0.30319.18010")。 請注意，建議應用程式程式碼與 <xref:System.Environment.Version%2A?displayProperty=nameWithType> 屬性有任何新的相依性。

### <a name="handling-the-product-versioning-changes"></a>處理產品版本變更

一般而言，應用程式需要具備可偵測 .NET Framework 的執行階段版本和安裝目錄等項目的建議技術：

- 若要偵測 .NET Framework 的執行階段版本，請參閱[如何：判斷安裝的 .NET Framework 版本](how-to-determine-which-versions-are-installed.md)。

- 若要判斷 .NET Framework 的安裝路徑，請使用 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` 機碼中的 `InstallPath` 項目值。

  > [!IMPORTANT]
  > 子機碼名稱是 `NET Framework Setup`，不是 `.NET Framework Setup`。

- 若要判斷 .NET Framework Common Language Runtime 的目錄路徑，請呼叫 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory%2A?displayProperty=nameWithType> 方法。

- 若要取得 CLR 版本，請呼叫 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion%2A?displayProperty=nameWithType> 方法。   針對 .NET Framework 4 及其點發行版本 (.NET Framework 4.5、4.5.1、4.5.2 以及 .NET Framework 4.6、4.6.1、4.6.2 和 4.7)，該方法會傳回字串 `v4.0.30319`。

## <a name="see-also"></a>另請參閱

- [應用程式相容性](application-compatibility.md)
