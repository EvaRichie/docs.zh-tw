---
title: 如何：手動產生用戶端資料服務類別 (WCF 資料服務)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, client library
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
ms.openlocfilehash: 368f2546652d21be44c0ffb4cc5f279c56beda51
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91165988"
---
# <a name="how-to-manually-generate-client-data-service-classes-wcf-data-services"></a>如何：手動產生用戶端資料服務類別 (WCF 資料服務)

WCF Data Services 與 Visual Studio 整合，可讓您在使用 [ **加入服務參考** ] 對話方塊，將參考加入至 Visual Studio 專案中的資料服務時，自動產生用戶端資料服務類別。 如需詳細資訊，請參閱 [如何：加入資料服務參考](how-to-add-a-data-service-reference-wcf-data-services.md)。 您也可以使用程式碼產生工具 `DataSvcUtil.exe`，手動產生同樣的用戶端資料服務類別。 這項工具（隨附于 WCF Data Services）會從資料服務定義產生 .NET Framework 類別。 同時，這項工具也可根據概念模型 (.csdl) 檔案，以及在 Visual Studio 專案中代表 Entity Framework 模型的 .edmx 檔案產生資料服務類別。

 本主題的範例會根據 Northwind 範例資料服務建立用戶端資料服務類別。 這項服務會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。 本主題中的某些範例需要 Northwind 模型的概念模型檔案。 如需詳細資訊，請參閱 [如何：使用 EdmGen.exe 產生模型和對應](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)檔。 本主題中的某些範例需要 Northwind 模型的 .edmx 檔。 如需詳細資訊，請參閱 [.edmx 檔案總覽](/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))。

### <a name="to-generate-c-classes-that-support-data-binding"></a>產生支援資料繫結的 C# 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > 您必須將提供給 `/uri:` 參數的值改為您的 Northwind 範例資料服務執行個體的 URI。

### <a name="to-generate-visual-basic-classes-that-support-data-binding"></a>產生支援資料繫結的 Visual Basic 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > 您必須將提供給 `/uri:` 參數的值改為您的 Northwind 資料服務範本之執行個體的 URI。

### <a name="to-generate-c-classes-based-on-the-service-uri"></a>根據服務 URI 產生 C# 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > 您必須將提供給 `/uri:` 參數的值改為您的 Northwind 範例資料服務執行個體的 URI。

### <a name="to-generate-visual-basic-classes-based-on-the-service-uri"></a>根據服務 URI 產生 Visual Basic 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc
    ```

    > [!NOTE]
    > 您必須將提供給 `/uri:` 參數的值改為您的 Northwind 資料服務範本之執行個體的 URI。

### <a name="to-generate-c-classes-based-on-the-conceptual-model-file-csdl"></a>根據概念模型檔 (CSDL) 產生 C# 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-conceptual-model-file-csdl"></a>根據概念模型檔 (CSDL) 產生 Visual Basic 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb
    ```

### <a name="to-generate-c-classes-based-on-the-edmx-file"></a>根據 .edmx 檔產生 C# 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs
    ```

### <a name="to-generate-visual-basic-classes-based-on-the-edmx-file"></a>根據服務 .edmx 檔產生 Visual Basic 類別

- 在命令提示字元中，執行下列命令但不含分行符號：

    ```console
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb
    ```

## <a name="see-also"></a>另請參閱

- [產生資料服務用戶端程式庫](generating-the-data-service-client-library-wcf-data-services.md)
- [作法：新增資料服務參考](how-to-add-a-data-service-reference-wcf-data-services.md)
- [WCF 資料服務用戶端公用程式 (DataSvcUtil.exe)](wcf-data-service-client-utility-datasvcutil-exe.md)
