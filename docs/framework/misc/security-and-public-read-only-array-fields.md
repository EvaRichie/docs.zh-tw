---
title: 安全及公開唯讀陣列欄位
description: 閱讀為什麼應該避免使用公用唯讀陣列欄位來定義應用程式的界限行為或安全性。
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
ms.openlocfilehash: 5e499f8052306cd1ad063c9f44a2a0f1d0b365ef
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855734"
---
# <a name="security-and-public-read-only-array-fields"></a>安全及公開唯讀陣列欄位

[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]

絕對不要使用受控程式庫中的唯讀公用陣列欄位來定義應用程式的界限行為或安全性，因為可以修改唯讀的公用陣列欄位。  
  
## <a name="remarks"></a>備註  

某些 .NET 類別包含唯讀的公用欄位，其中包含平臺特定的界限參數。 例如， <xref:System.IO.Path.InvalidPathChars> 欄位是描述檔案路徑字串中不允許之字元的陣列。 許多類似的欄位都會出現在整個 .NET 中。  
  
 公用唯讀欄位（例如）的值 <xref:System.IO.Path.InvalidPathChars> 可以由您的程式碼或共用您程式碼應用程式域的程式碼修改。  您不應該使用唯讀公用陣列欄位，如下所示來定義應用程式的界限行為。  如果您這樣做，惡意程式碼可以改變界限定義，並以非預期的方式使用您的程式碼。  
  
 在2.0 版和更新版本的 .NET Framework 中，您應該使用傳回新陣列的方法，而不是使用公用陣列欄位。  例如，您應該使用方法，而不是使用 <xref:System.IO.Path.InvalidPathChars> 欄位 <xref:System.IO.Path.GetInvalidPathChars%2A> 。  
  
 請注意，.NET Framework 類型不會使用公用欄位在內部定義界限類型。  相反地，.NET Framework 會使用個別的私用欄位。  變更這些公用欄位的值並不會改變 .NET Framework 類型的行為。  
  
## <a name="see-also"></a>另請參閱

- [安全程式碼撰寫方針](../../standard/security/secure-coding-guidelines.md)
