---
title: -errorreport
ms.date: 08/14/2018
helpviewer_keywords:
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
ms.openlocfilehash: b6a1c8fce17e3e5a54366c2ff4dff4e6aa668f56
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408656"
---
# <a name="-errorreport"></a>-errorreport

指定 Visual Basic 編譯器應該如何報告內部編譯器錯誤。

## <a name="syntax"></a>語法

```console
-errorreport:{ prompt | queue | send | none }
```

## <a name="remarks"></a>備註

此選項提供一個便利的方式，向 Microsoft 的 Visual Basic 團隊報告 Visual Basic 的內部編譯器錯誤（ICE）。 根據預設，編譯器不會將任何資訊傳送至 Microsoft。 不過，如果您遇到內部編譯器錯誤，此選項可讓您向 Microsoft 報告錯誤。 這項資訊可協助 Microsoft 工程師找出原因，並可協助改善下一版的 Visual Basic。

使用者傳送報表的能力取決於電腦和使用者原則許可權。

下表摘要說明選項的效果 `-errorreport` 。

|選項|行為|
|---|---|
|`prompt`|如果發生內部編譯器錯誤，則會出現對話方塊，讓您可以查看編譯器所收集的確切資料。 您可以判斷錯誤報表中是否有任何機密資訊，並決定是否要將它傳送給 Microsoft。 如果您決定傳送它，且電腦和使用者原則設定允許，則編譯器會將資料傳送給 Microsoft。|
|`queue`|佇列錯誤報告。 當您使用系統管理員許可權登入時，可以報告自上次登入後的任何失敗時間（每隔三天不會提示您傳送失敗的報告一次以上）。 這是未指定選項時的預設行為 `-errorreport` 。|
|`send`|如果發生內部編譯器錯誤，而且電腦和使用者原則設定允許，則編譯器會將資料傳送給 Microsoft。<br /><br /> `-errorreport:send`如果[Windows 錯誤報告](/windows/desktop/wer/windows-error-reporting)系統設定啟用 [報表]，則選項會嘗試自動傳送錯誤資訊給 Microsoft。 |
|`none`|如果發生內部編譯器錯誤，則不會將它收集或傳送給 Microsoft。|

編譯器會在錯誤發生時傳送包含堆疊的資料，這通常會包含一些原始程式碼。 如果搭配 `-errorreport` [-bugreport](bugreport.md)選項使用，則會傳送整個來源檔案。

此選項最適合搭配[-bugreport](bugreport.md)選項使用，因為它可讓 Microsoft 工程師更輕鬆地重現錯誤。

> [!NOTE]
> 此 `-errorreport` 選項無法從 Visual Studio 開發環境中使用; 只有在從命令列進行編譯時，才能使用此選項。

## <a name="example"></a>範例

下列程式碼會嘗試進行編譯 `T2.vb` ，如果編譯器遇到編譯器內部錯誤，則會提示您將錯誤報表傳送給 Microsoft。

```console
vbc -errorreport:prompt t2.vb
```

## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
- [編譯命令列的範例](sample-compilation-command-lines.md)
- [-bugreport](bugreport.md)
