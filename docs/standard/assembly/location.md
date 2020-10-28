---
title: 組件位置
description: .NET 元件的位置會決定 CLR 如何尋找它，以及是否可以與其他元件共用。
ms.date: 08/20/2019
helpviewer_keywords:
- locating assemblies
- assemblies [.NET], location
ms.assetid: 9f1f41a7-2954-49d3-a2c0-62b6ef4d40ab
ms.openlocfilehash: 1fa1c486c0cddce4ddcfae7f2df27e2e85c88e66
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687603"
---
# <a name="assembly-location"></a>組件位置

組件的位置可判斷 Common Language Runtime 是否可以在參考時找到它，也可以判斷是否可以與其他組件共用組件。 您可以在下列位置中部署組件：

- 應用程式的目錄或子目錄。

     這是部署組件的最常用位置。 應用程式根目錄的子目錄可以根據語言或文化特性。 如果組件具有文化特性屬性中的資訊，則必須在具有該文化特性名稱之應用程式目錄下的子目錄中。

- 全域組件快取。

     這是只要安裝 Common Language Runtime 的位置就會安裝的全機器程式碼快取。 在大部分情況下，如果您想要與多個應用程式共用組件，則應該將它部署到全域組件快取。

- 在 HTTP 伺服器上。

     HTTP 伺服器上部署的組件必須具有強式名稱；您指向應用程式組態檔的程式碼基底區段中的組件。

## <a name="see-also"></a>請參閱

- [建立組件](create.md)
- [全域組件快取](../../framework/app-domains/gac.md)
- [執行時間如何找出元件](../../framework/deployment/how-the-runtime-locates-assemblies.md)
