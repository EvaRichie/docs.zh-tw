---
title: 一般 I/O 工作
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- I/O, common tasks
ms.assetid: bf00c380-706a-4e38-b829-454a480629fc
ms.openlocfilehash: 9474d6c0340583e285a6dc47933c602f799f121d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287415"
---
# <a name="common-io-tasks"></a>一般 I/O 工作
<xref:System.IO> 命名空間 (Namespace) 提供了幾個允許可在檔案、目錄和資料流上執行各種動作 (例如讀取和寫入) 的類別。 如需詳細資訊，請參閱檔案[和資料流程 i/o](index.md)。  
  
## <a name="common-file-tasks"></a>一般檔案工作  
  
|作法...|請參閱這個主題中的範例…|  
|-------------------|--------------------------------------|  
|建立文字檔|<xref:System.IO.File.CreateText%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.CreateText%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.File.Create%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.Create%2A?displayProperty=nameWithType> 方法|  
|寫入文字檔|[作法：將文字寫入檔案](how-to-write-text-to-a-file.md)<br /><br /> [如何：寫入文字檔（c + +/CLI）](/cpp/dotnet/how-to-write-a-text-file-cpp-cli)|  
|從文字檔讀取|[作法：讀取檔案中的文字](how-to-read-text-from-a-file.md)|  
|將文字附加至檔案|[作法：開啟並附加至記錄檔](how-to-open-and-append-to-a-log-file.md)<br /><br /> <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.AppendText%2A?displayProperty=nameWithType> 方法|  
|重新命名檔案或移動檔案|<xref:System.IO.File.Move%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.MoveTo%2A?displayProperty=nameWithType> 方法|  
|刪除檔案|<xref:System.IO.File.Delete%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.Delete%2A?displayProperty=nameWithType> 方法|  
|複製檔案|<xref:System.IO.File.Copy%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.CopyTo%2A?displayProperty=nameWithType> 方法|  
|取得檔案大小|<xref:System.IO.FileInfo.Length%2A?displayProperty=nameWithType> 屬性|  
|取得檔案的屬性|<xref:System.IO.File.GetAttributes%2A?displayProperty=nameWithType> 方法|  
|設定檔案的屬性|<xref:System.IO.File.SetAttributes%2A?displayProperty=nameWithType> 方法|  
|判斷檔案是否存在|<xref:System.IO.File.Exists%2A?displayProperty=nameWithType> 方法|  
|讀取二進位檔案|[作法：讀取和寫入新建立的資料檔案](how-to-read-and-write-to-a-newly-created-data-file.md)|  
|寫入至二進位檔案|[作法：讀取和寫入新建立的資料檔案](how-to-read-and-write-to-a-newly-created-data-file.md)|  
|擷取副檔名|<xref:System.IO.Path.GetExtension%2A?displayProperty=nameWithType> 方法|  
|擷取檔案的完整路徑|<xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> 方法|  
|從路徑擷取檔案名稱和副檔名|<xref:System.IO.Path.GetFileName%2A?displayProperty=nameWithType> 方法|  
|變更檔案的副檔名|<xref:System.IO.Path.ChangeExtension%2A?displayProperty=nameWithType> 方法|  
  
## <a name="common-directory-tasks"></a>一般目錄工作  
  
|作法...|請參閱這個主題中的範例…|  
|-------------------|--------------------------------------|  
|存取特殊資料夾中的檔案，例如 [我的文件]|[作法：將文字寫入檔案](how-to-write-text-to-a-file.md)|  
|建立目錄|<xref:System.IO.Directory.CreateDirectory%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.FileInfo.Directory%2A?displayProperty=nameWithType> 屬性|  
|建立子目錄|<xref:System.IO.DirectoryInfo.CreateSubdirectory%2A?displayProperty=nameWithType> 方法|  
|重新命名目錄或移動目錄|<xref:System.IO.Directory.Move%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.DirectoryInfo.MoveTo%2A?displayProperty=nameWithType> 方法|  
|複製目錄|[作法：複製目錄](how-to-copy-directories.md)|  
|刪除目錄|<xref:System.IO.Directory.Delete%2A?displayProperty=nameWithType> 方法<br /><br /> <xref:System.IO.DirectoryInfo.Delete%2A?displayProperty=nameWithType> 方法|  
|請參閱目錄中的檔案與子目錄|[作法：列舉目錄和檔案](how-to-enumerate-directories-and-files.md)|  
|尋找目錄的大小|<xref:System.IO.Directory?displayProperty=nameWithType> 類別|  
|判斷目錄是否存在|<xref:System.IO.Directory.Exists%2A?displayProperty=nameWithType> 方法|  
  
## <a name="see-also"></a>另請參閱

- [檔案和資料流程 i/o](index.md)
- [撰寫資料流](composing-streams.md)
- [非同步檔案 i/o](asynchronous-file-i-o.md)
