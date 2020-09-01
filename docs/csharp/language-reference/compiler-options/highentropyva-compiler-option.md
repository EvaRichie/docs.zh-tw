---
description: -highentropyva (C# 編譯器選項)
title: -highentropyva (C# 編譯器選項)
ms.date: 07/20/2015
f1_keywords:
- /highentropyva
helpviewer_keywords:
- /highentropyva compiler option [C#]
- -highentropyva compiler option [C#]
- highentropyva compiler option [C#]
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
ms.openlocfilehash: 2c2e2780693a89072c4bb55b318be94089bf3ced
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125653"
---
# <a name="-highentropyva-c-compiler-options"></a>-highentropyva (C# 編譯器選項)
**-highentropyva** 編譯器選項會通知 Windows 核心某一特定可執行檔是否支援高熵位址空間配置隨機載入 (ASLR)。  
  
## <a name="syntax"></a>語法  
  
```console  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>引數  
 `+` &#124; `-`  
 此選項會指定，64 位元可執行檔或 [-platform:anycpu](./platform-compiler-option.md) 編譯器選項所標記的可執行檔支援高熵虛擬位址空間。 此選項預設為停用。 使用 **-highentropyva+** 或 **-highentropyva** 予以啟用。  
  
## <a name="remarks"></a>備註  
 當隨機化處理序的位址空間配置作為 ASLR 一部分時，**-highentropyva** 選項可讓相容的 Windows 核心版本使用較高程度的高熵。 使用較高程度的高熵表示可將大量位址配置到記憶體區域，例如堆疊和堆積， 因此更難猜測特定記憶體區域的位置。  
  
 指定 **-highentropyva** 編譯器選項時，目標可執行檔以及作為其依據的任何模組在作為 64 位元處理序執行時，都必須能夠處理大於 4 GB 的指標值。
