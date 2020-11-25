---
title: .NET 組件檔格式
description: 了解用來描述並包含 .NET 應用程式和程式庫的 .NET 組件檔格式。
author: richlander
ms.date: 08/20/2019
ms.assetid: 6520323e-ff28-4c8a-ba80-e64a413199e6
ms.openlocfilehash: b1de3f46f04f24dd4bbb2f695de8741feb29f226
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95731536"
---
# <a name="net-assembly-file-format"></a>.NET 組件檔格式

.NET 會定義用來完整描述並包含 .NET 程式的二進位檔案格式（ *assembly*）。 組件用於程式本身以及任何相依的程式庫。 除了適當的 .NET 實作之外，.NET 程式也可以執行為一或多個沒有其他必要成品的組件。 原生相依性（包括作業系統 Api）是個別的考慮，而且不包含在 .NET 元件格式中，不過這些相依性有時會以這種格式描述 (例如 WinRT) 。

> 每個 CLI 元件都會攜帶該元件特定宣告、實作和參考的中繼資料。 因此，元件特定中繼資料是指元件中繼資料，而且產生的元件即為來自 ECMA 335 I.9.1 的自我描述元件和組件。

格式會依 [ECMA 335](https://www.ecma-international.org/publications/standards/Ecma-335.htm) 來完整指定並標準化。 所有 .NET 編譯器和執行階段都會使用這種格式。 所記載且不常更新的二進位格式目前狀態，已是互通性的主要優點 (即需求)。 此格式在 2005 ( .NET Framework 2.0) ，以配合泛型和處理器架構，最後會以實體方式更新。

格式為 CPU 並且無作業系統無關。 它已用作將目標設為許多晶片和 CPU 之 .NET 實作的一部分。 雖然格式本身具有 Windows 傳承，但是可在任何作業系統上實作。 為達 OS 互通性，大部分的值皆以位元組由小到大的格式儲存，這可說是最重大的選擇。 它沒有電腦指標大小 (例如，32 位元、64 位元) 的特定同質性。

.NET 組件格式對於指定的程式或程式庫結構也具有相當的描述性。 它描述元件的內部元件，特別是元件參考和定義的類型，以及其內部結構。 工具或 API 可以讀取和處理這項資訊以供顯示，或進行程式設計決策。

## <a name="format"></a>格式

.NET 二進位格式是根據 Windows [PE 檔案](https://en.wikipedia.org/wiki/Portable_Executable)格式。 事實上，.NET 類別庫是一致的 Windows PE，並且顯示在第一次看到 Windows 動態連結程式庫 (DLL) 或應用程式執行檔 (EXE) 時。 這是 Windows 上極為實用的特性，在此，它們可以偽裝為原生可執行二進位檔，並進行一些相同的處理 (例如，OS 載入、PE 工具)。

![組件標頭](../media/assembly-format/assembly-headers.png)

來自 ECMA 335 II.25.1 的組件標頭 (執行階段檔案格式的結構)。

## <a name="process-the-assemblies"></a>處理元件

可能會撰寫工具或 API 來處理組件。 元件資訊可讓您在執行時間進行程式設計決策、重新撰寫元件、在編輯器中提供 API IntelliSense，以及產生檔。 <xref:System.Reflection?displayProperty=nameWithType>、<xref:System.Reflection.MetadataLoadContext?displayProperty=nameWithType> 和 [Mono.Cecil](https://www.mono-project.com/docs/tools+libraries/libraries/Mono.Cecil/) 是常用於此目的工具的不錯範例。
