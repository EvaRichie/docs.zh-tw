---
title: 當地語系化
ms.date: 03/30/2017
helpviewer_keywords:
- culture, localization
- application development [.NET], localization
- globalization [.NET], localization
- code blocks
- international applications [.NET], localization
- global applications, localization
- world-ready applications, localization
- user interface blocks
- localization [.NET], about localization
- localizing resources
ms.assetid: 49d520d7-92d7-44ee-bb24-8b615db1d41b
ms.openlocfilehash: 5d47d002c714ea80b6f94c810f2dca726c273134
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829826"
---
# <a name="localization"></a>當地語系化

當地語系化是一種程序，可將應用程式資源翻譯為應用程式所支援之每個文化特性的當地語系化版本。 只有在完成[可當地語系化檢閱](localizability-review.md)步驟，以確認全球化的應用程式已準備好進行當地語系化之後，才能繼續進行當地語系化步驟。

準備好進行當地語系化的應用程式分成兩個概念性區塊，其中一個區塊包含所有使用者介面元素，另一個區塊則包含可執行檔程式碼。 使用者介面區塊包含只可當地語系化的使用者介面元素，例如字串、錯誤訊息、對話方塊、功能表、內嵌物件資源，以及適用於中性文化特性的其他元素。 程式碼區塊僅包含可供所有支援的文化特性使用的應用程式程式碼。 Common Language Runtime 支援附屬組件資源模型，可將應用程式的可執行檔程式碼與其資源分開。 如需有關實作此模型的詳細資訊，請參閱 [.NET 中的資源](../../framework/resources/index.md)。

針對每個當地語系化版本的應用程式，加入新的附屬組件，其中包含轉譯成適用於目標文化特性之語言的當地語系化使用者介面區塊。 所有文化特性的程式碼區塊應該維持不變。 當地語系化版本的使用者介面區塊結合程式碼區塊之後，會產生您應用程式的當地語系化版本。

Windows Software Development Kit (SDK) 提供 Windows Forms 資源編輯器 (Winres.exe)，讓您可以快速地將 Windows Forms 當地語系化成目標文化特性。 如需有關使用此工具的相關資訊，請參閱 [Winres.exe (Windows Forms 資源編輯器)](../../framework/tools/winres-exe-windows-forms-resource-editor.md)。

## <a name="see-also"></a>請參閱

- [全球化和當地語系化](index.md)
- [當地語系化能力審查](localizability-review.md)
- [全球化](globalization.md)
- [桌面應用程式中的資源](../../framework/resources/index.md)
