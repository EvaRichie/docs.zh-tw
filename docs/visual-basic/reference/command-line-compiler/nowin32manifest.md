---
title: -nowin32manifest
ms.date: 03/13/2018
helpviewer_keywords:
- /nowin32manifest compiler option [Visual Basic]
- nowin32manifest compiler option [Visual Basic]
- -nowin32manifest compiler option [Visual Basic]
ms.assetid: c0528aae-83b3-4425-99f0-19448e9843e3
ms.openlocfilehash: 8fd902e1317c7c767303bcaa30cdc56cff712558
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91097614"
---
# <a name="-nowin32manifest-visual-basic"></a>-nowin32manifest (Visual Basic) 

指示編譯器不要將任何應用程式資訊清單內嵌在可執行檔中。  
  
## <a name="syntax"></a>語法  
  
```console  
-nowin32manifest  
```  
  
## <a name="remarks"></a>備註  

 使用此選項時，應用程式在 Windows Vista 上會虛擬化，除非您在 Win32 資源檔案中或於更新版本組建步驟期間提供應用程式資訊清單。 如需虛擬化的詳細資訊，請參閱 [Windows Vista 上的 ClickOnce 部署](/visualstudio/deployment/clickonce-deployment-on-windows-vista)。  
  
 如需建立資訊清單的詳細資訊，請參閱 [-win32manifest (Visual Basic) ](win32manifest.md)。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 命令列編譯器](index.md)
- [Application Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
