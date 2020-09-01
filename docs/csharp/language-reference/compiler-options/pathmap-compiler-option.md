---
description: -pathmap (C# 編譯器選項)
title: -pathmap (C# 編譯器選項)
ms.date: 05/16/2018
f1_keywords:
- /pathmap
helpviewer_keywords:
- -pathmap compiler option [C#]
- pathmap compiler option [C#]
- /pathmap compiler option [C#]
ms.openlocfilehash: 707a37c6946cfcaf429552f0aeece6b87f3ad71d
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89125003"
---
# <a name="-pathmap-c-compiler-options"></a>-pathmap (C# 編譯器選項)

**-pathmap** 編譯器選項會指定如何將實體路徑對應到編譯器所輸出的來源路徑名稱。

## <a name="syntax"></a>語法

```console
-pathmap:path1=sourcePath1,path2=sourcePath2
```

## <a name="arguments"></a>引數

 `path1` 目前環境中原始程式檔的完整路徑。

 `sourcePath1` 任何輸出檔案中替代 `path1` 的來源路徑。

若要指定多個對應的來源路徑，請以逗號隔開每個來源路徑。

## <a name="remarks"></a>備註

編譯器會基於下列因素，將來源路徑寫入其輸出中：

1. 將 <xref:System.Runtime.CompilerServices.CallerFilePathAttribute> 套用到選擇性參數時，會針對引數替代來源路徑。
1. 來源路徑內嵌於 PDB 檔案。
1. PDB 檔案的路徑內嵌於 PE (可攜式執行檔) 檔案。

此選項會將編譯器執行所在電腦上的每個實體路徑對應到應寫入輸出檔案的對應路徑。

## <a name="example"></a>範例

在目錄 **C:\\work\\tests** 中編譯 `t.cs`，並將該目錄對應到輸出中的 **\publish**：

```console
csc -pathmap:C:\work\tests=\publish t.cs
```

## <a name="see-also"></a>另請參閱

- [C # 編譯器選項](./index.md)
- [管理專案和方案屬性](/visualstudio/ide/managing-project-and-solution-properties)
