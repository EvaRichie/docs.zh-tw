---
title: 作法：開發在 IIS 上執行的 WCF 資料服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- WCF Data Services, hosting
ms.assetid: f6f768c5-4989-49e3-a36f-896ab4ded86e
ms.openlocfilehash: 75dc18f3ee91ec077ed48c68ec62cb47910d9ddd
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543481"
---
# <a name="how-to-develop-a-wcf-data-service-running-on-iis"></a>如何：開發在 IIS 上執行的 WCF 資料服務

本文說明如何使用 WCF Data Services 建立以 Northwind 範例資料庫為基礎的資料服務，該資料庫是由在 Internet Information Services (IIS) 上執行的 ASP.NET Web 應用程式所裝載。 如需如何建立與 ASP.NET 程式開發伺服器上執行的 ASP.NET Web 應用程式相同的 Northwind 資料服務的範例，請參閱 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)。

> [!NOTE]
> 若要建立 Northwind 資料服務，請先在本機電腦上安裝 Northwind 範例資料庫。 若要安裝資料庫，請從 [Northwind 和 pubs 範例資料庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)執行 transact-sql 腳本，以進行 Microsoft SQL Server。

本文說明如何使用 Entity Framework 提供者來建立資料服務。 有其他資料服務提供者可以使用。 如需詳細資訊，請參閱 [資料服務提供者](data-services-providers-wcf-data-services.md)。

當您建立服務之後，您必須明確提供資料服務資源的存取權。 如需詳細資訊，請參閱 [如何：啟用資料服務的存取](how-to-enable-access-to-the-data-service-wcf-data-services.md)。

## <a name="create-the-aspnet-web-application-that-runs-on-iis"></a>建立在 IIS 上執行的 ASP.NET web 應用程式

1. 在 Visual Studio 中，於 [檔案]  功能表上選取 [新增]   > [專案]  。

2. 在 [ **新增專案** ] 對話方塊中，選取 **已安裝** 的 > [**Visual c #** 或 **Visual Basic**] > **Web** 類別目錄。

3. 選取 [ **ASP.NET Web 應用程式** ] 範本。

4. 輸入 `NorthwindService` 做為專案的名稱。

5. 按一下 [確定]。

6. 在 [ **專案** ] 功能表上，選取 [ **northwindservice.svc 屬性**]。

7. 選取 [ **Web** ] 索引標籤，然後選取 [ **使用本機 IIS Web 服務器**]。

8. 按一下 [ **建立虛擬目錄** ]，然後按一下 **[確定]**。

9. 在具有系統管理員權限的命令提示字元中，執行下列其中一個命令 (視作業系統而定)：

    - 32 位元系統：

        ```console
        "%windir%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

    - 64 位元系統：

        ```console
        "%windir%\Microsoft.NET\Framework64\v3.0\Windows Communication Foundation\ServiceModelReg.exe" -i
        ```

     這樣會確定 Windows Communication Foundation (WCF) 已在電腦上登錄。

10. 在具有系統管理員權限的命令提示字元中，執行下列其中一個命令 (視作業系統而定)：

    - 32 位元系統：

        ```console
        "%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

    - 64 位元系統：

        ```console
        "%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe" -i -enable
        ```

     這樣可確保 IIS 會在電腦上安裝 WCF 之後正確執行。 此外，您可能也必須重新啟動 IIS。

11. 當 ASP.NET 應用程式在 IIS7 上執行時，您也必須執行下列步驟：

    1. 開啟 [IIS 管理員]，並流覽至 [ **預設**的網站] 底下的 [PhotoService] 應用程式。

    2. 在 [功能檢視]**** 中，連按兩下 [驗證]****。

    3. 在 [驗證]**** 頁面上，選取 [匿名驗證]****。

    4. 在 [ **動作** ] 窗格中，按一下 [ **編輯** ]，設定匿名使用者將連接到網站的安全性主體。

    5. 在 [ **編輯匿名驗證認證** ] 對話方塊中，選取 [ **應用程式集**區身分識別]。

    > [!IMPORTANT]
    > 當您使用 Network Service 帳戶時，就會將與該帳戶相關聯的所有內部網路存取權授與匿名使用者。

12. 使用 SQL Server Management Studio、sqlcmd.exe 公用程式或 Visual Studio 中的 Transact-SQL 編輯器，針對已附加 Northwind 資料庫的 SQL Server 執行個體執行下列 Transact-SQL 命令：

    ```sql
    CREATE LOGIN [NT AUTHORITY\NETWORK SERVICE] FROM WINDOWS;
    GO
    ```

    這樣會在用來執行 IIS 之 Windows 帳戶的 SQL Server 執行個體中建立登入。 如此可讓 IIS 連接至 SQL Server 執行個體。

13. 當附加 Northwind 資料庫之後，執行下列 Transact-SQL 命令：

    ```sql
    USE Northwind
    GO
    CREATE USER [NT AUTHORITY\NETWORK SERVICE]
    FOR LOGIN [NT AUTHORITY\NETWORK SERVICE] WITH DEFAULT_SCHEMA=[dbo];
    GO
    ALTER LOGIN [NT AUTHORITY\NETWORK SERVICE]
    WITH DEFAULT_DATABASE=[Northwind];
    GO
    EXEC sp_addrolemember 'db_datareader', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    EXEC sp_addrolemember 'db_datawriter', 'NT AUTHORITY\NETWORK SERVICE'
    GO
    ```

    這樣會授與新登入的權限，此權限可讓 IIS 讀取 Northwind 資料庫中的資料並將資料寫入其中。

## <a name="define-the-data-model"></a>定義資料模型

1. 在**方案總管**中，以滑鼠右鍵按一下 ASP.NET 專案的名稱，然後按一下 [**加入**  >  **新專案**]。

2. 在 [ **加入新專案** ] 對話方塊中，選取 [ **ADO.NET 實體資料模型**]。

3. 若為資料模型的名稱，請輸入 `Northwind.edmx` 。

4. 在實體資料模型 Wizard 中，選取 [ **從資料庫產生**]，然後按 **[下一步]**。

5. 執行下列其中一個步驟，將資料模型連接至資料庫，然後按 **[下一步]**：

    - 如果您沒有已設定的資料庫連接，請按一下 [ **新增連接** ] 並建立新的連接。 如需詳細資訊，請參閱 [How to: Create Connections to SQL Server Databases](/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90))。 此 SQL Server 執行個體必須已附加 Northwind 範例資料庫。

         \- 或 -

    - 如果您擁有已經設定為連接至 Northwind 資料庫的資料庫連接，請從連接清單中選取該連接。

6. 在精靈的最後一頁上，選取資料庫中所有資料表的核取方塊，並且清除檢視表和預存程序 (Stored Procedure) 的核取方塊。

7. 按一下 **[完成** ] 以關閉嚮導。

## <a name="create-the-data-service"></a>建立資料服務

1. 在**方案總管**中，以滑鼠右鍵按一下 ASP.NET 專案的名稱，然後按一下 [**加入**  >  **新專案**]。

2. 在 [ **加入新專案** ] 對話方塊中，選取 [ **WCF 資料服務**]。

   ![Visual Studio 2015 中的 WCF 資料服務專案範本](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 資料服務**範本可在 Visual Studio 2015 中使用，但不能在 Visual Studio 2017 或更新版本中使用。

3. 在 [服務名稱] 中，輸入 `Northwind` 。

     Visual Studio 會針對新的服務建立 XML 標記和程式碼檔案。 根據預設，程式碼編輯器視窗隨即開啟。 在 **方案總管**中，服務的名稱、Northwind 和副檔名為 svc.cs 或 .svc。

4. 在資料服務的程式碼裡，於定義資料服務和型別的類別定義中，取代註解 `/* TODO: put your data source class name here */`，該型別是資料模型的實體容器，在這個案例中是 `NorthwindEntities`。 類別定義看起來應如下列：

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="see-also"></a>另請參閱

- [將資料公開為服務](exposing-your-data-as-a-service-wcf-data-services.md)
