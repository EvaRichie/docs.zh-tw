---
title: 如何：使用 ADO.NET Entity Framework 資料來源建立資料服務 (WCF 資料服務)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, Entity Framework
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
ms.openlocfilehash: 1e559488a3260fafe6c211ff47226a258fc1289a
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557693"
---
# <a name="how-to-create-a-data-service-using-an-adonet-entity-framework-data-source-wcf-data-services"></a><span data-ttu-id="53596-102">如何：使用 ADO.NET Entity Framework 資料來源建立資料服務 (WCF 資料服務)</span><span class="sxs-lookup"><span data-stu-id="53596-102">How to: Create a Data Service Using an ADO.NET Entity Framework Data Source (WCF Data Services)</span></span>

<span data-ttu-id="53596-103">WCF Data Services 會將實體資料公開為數據服務。</span><span class="sxs-lookup"><span data-stu-id="53596-103">WCF Data Services exposes entity data as a data service.</span></span> <span data-ttu-id="53596-104">當資料來源為關係資料庫時，這個實體資料會由 NETEntity 架構提供。</span><span class="sxs-lookup"><span data-stu-id="53596-104">This entity data is provided by the ADO.NETEntity Framework when the data source is a relational database.</span></span> <span data-ttu-id="53596-105">本主題示範如何在以現有資料庫為基礎的 Visual Studio Web 應用程式中建立 Entity Framework 架構資料模型，並使用此資料模型建立新的資料服務。</span><span class="sxs-lookup"><span data-stu-id="53596-105">This topic shows you how to create an Entity Framework-based data model in a Visual Studio Web application that is based on an existing database and use this data model to create a new data service.</span></span>

<span data-ttu-id="53596-106">Entity Framework 也提供命令列工具，可在 Visual Studio 專案以外產生 Entity Framework 模型。</span><span class="sxs-lookup"><span data-stu-id="53596-106">The Entity Framework also provides a command line tool that can generate an Entity Framework model outside of a Visual Studio project.</span></span> <span data-ttu-id="53596-107">如需詳細資訊，請參閱 [如何：使用 EdmGen.exe 產生模型和對應](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)檔。</span><span class="sxs-lookup"><span data-stu-id="53596-107">For more information, see [How to: Use EdmGen.exe to Generate the Model and Mapping Files](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).</span></span>

## <a name="to-add-an-entity-framework-model-that-is-based-on-an-existing-database-to-an-existing-web-application"></a><span data-ttu-id="53596-108">若要將以現有資料庫為基礎的 Entity Framework 模型加入至現有的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="53596-108">To add an Entity Framework model that is based on an existing database to an existing Web application</span></span>

1. <span data-ttu-id="53596-109">在 [**專案**] 功能表上，按一下 [**加入**  >  **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="53596-109">On the **Project** menu, click **Add** > **New Item**.</span></span>

2. <span data-ttu-id="53596-110">在 [ **範本** ] 窗格中，按一下 [ **資料** ] 分類，然後選取 [ **ADO.NET 實體資料模型**]。</span><span class="sxs-lookup"><span data-stu-id="53596-110">In the **Templates** pane, click the **Data** category, and then select **ADO.NET Entity Data Model**.</span></span>

3. <span data-ttu-id="53596-111">輸入模型名稱，然後按一下 [ **新增**]。</span><span class="sxs-lookup"><span data-stu-id="53596-111">Enter the model name and then click **Add**.</span></span>

     <span data-ttu-id="53596-112">Entity Data Model 精靈的第一個頁面便會出現。</span><span class="sxs-lookup"><span data-stu-id="53596-112">The first page of the Entity Data Model Wizard is displayed.</span></span>

4. <span data-ttu-id="53596-113">在 [ **選擇模型內容** ] 對話方塊中，選取 [ **從資料庫產生**]。</span><span class="sxs-lookup"><span data-stu-id="53596-113">In the **Choose Model Contents** dialog box, select **Generate from database**.</span></span> <span data-ttu-id="53596-114">然後按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="53596-114">Then click **Next**.</span></span>

5. <span data-ttu-id="53596-115">按一下 [ **新增連接** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53596-115">Click the **New Connection** button.</span></span>

6. <span data-ttu-id="53596-116">在 [ **連接屬性** ] 對話方塊中，輸入您的伺服器名稱、選取驗證方法、輸入資料庫名稱，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="53596-116">In the **Connection Properties** dialog box, type your server name, select the authentication method, type the database name, and then click **OK**.</span></span>

     <span data-ttu-id="53596-117">[ **選擇您的資料連線** ] 對話方塊會以您的資料庫連接設定進行更新。</span><span class="sxs-lookup"><span data-stu-id="53596-117">The **Choose Your Data Connection** dialog box is updated with your database connection settings.</span></span>

7. <span data-ttu-id="53596-118">確定已核取 [ **在 App.Config 為：] 核取方塊中的 [儲存實體連接設定** ] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="53596-118">Ensure that the **Save entity connection settings in App.Config as:** checkbox is checked.</span></span> <span data-ttu-id="53596-119">然後按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="53596-119">Then click **Next**.</span></span>

8. <span data-ttu-id="53596-120">在 [ **選擇您的資料庫物件** ] 對話方塊中，選取您打算在資料服務中公開的所有資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="53596-120">In the **Choose Your Database Objects** dialog box, select all of database objects that you plan to expose in the data service.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53596-121">資料服務不會自動公開包含在資料模型中的物件，</span><span class="sxs-lookup"><span data-stu-id="53596-121">Objects included in the data model are not automatically exposed by the data service.</span></span> <span data-ttu-id="53596-122">必須由服務本身明確公開。</span><span class="sxs-lookup"><span data-stu-id="53596-122">They must be explicitly exposed by the service itself.</span></span> <span data-ttu-id="53596-123">如需詳細資訊，請參閱設定 [資料服務](configuring-the-data-service-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="53596-123">For more information, see [Configuring the Data Service](configuring-the-data-service-wcf-data-services.md).</span></span>

9. <span data-ttu-id="53596-124">按一下 [完成]\*\*\*\* 以完成程序。</span><span class="sxs-lookup"><span data-stu-id="53596-124">Click **Finish** to complete the wizard.</span></span>

     <span data-ttu-id="53596-125">這樣會根據特定資料庫建立預設資料模型。</span><span class="sxs-lookup"><span data-stu-id="53596-125">This creates a default data model based on the specific database.</span></span> <span data-ttu-id="53596-126">Entity Framework 可讓您自訂資料模型。</span><span class="sxs-lookup"><span data-stu-id="53596-126">The Entity Framework enables to customize the data model.</span></span> <span data-ttu-id="53596-127">如需詳細資訊，請參閱 [實體資料模型工具](/previous-versions/dotnet/netframework-4.0/bb738480(v=vs.100))工作（task）。</span><span class="sxs-lookup"><span data-stu-id="53596-127">For more information, see [Entity Data Model Tools Tasks](/previous-versions/dotnet/netframework-4.0/bb738480(v=vs.100)).</span></span>

## <a name="to-create-the-data-service-by-using-the-new-data-model"></a><span data-ttu-id="53596-128">若要使用新的資料模型建立資料服務</span><span class="sxs-lookup"><span data-stu-id="53596-128">To create the data service by using the new data model</span></span>

1. <span data-ttu-id="53596-129">在 Visual Studio 中開啟代表該資料模型的 .edmx 檔案。</span><span class="sxs-lookup"><span data-stu-id="53596-129">In Visual Studio, open the .edmx file that represents the data model.</span></span>

2. <span data-ttu-id="53596-130">在 **模型瀏覽器**中，以滑鼠右鍵按一下模型，再按一下 [ **屬性**]，然後記下實體容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="53596-130">In the **Model Browser**, right-click the model, click **Properties**, and then note the name of the entity container.</span></span>

3. <span data-ttu-id="53596-131">在**方案總管**中，以滑鼠右鍵按一下 ASP.NET 專案的名稱，然後按一下 [**加入**  >  **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="53596-131">In **Solution Explorer**, right-click the name of your ASP.NET project, and then click **Add** > **New Item**.</span></span>

4. <span data-ttu-id="53596-132">在 [**加入新專案**] 對話方塊中，選取 [ **Web** ] 類別中的 [ **WCF 資料服務**] 範本。</span><span class="sxs-lookup"><span data-stu-id="53596-132">In the **Add New Item** dialog box, select the **WCF Data Service** template in the **Web** category.</span></span>

   ![Visual Studio 2015 中的 WCF 資料服務專案範本](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > <span data-ttu-id="53596-134">**WCF 資料服務**範本可在 Visual Studio 2015 中使用，但不能在 Visual Studio 2017 或更新版本中使用。</span><span class="sxs-lookup"><span data-stu-id="53596-134">The **WCF Data Service** template is available in Visual Studio 2015, but not in Visual Studio 2017 or later.</span></span>

5. <span data-ttu-id="53596-135">提供服務的名稱，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="53596-135">Supply a name for the service, and then click **OK**.</span></span>

     <span data-ttu-id="53596-136">Visual Studio 會針對新的服務建立 XML 標記和程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="53596-136">Visual Studio creates the XML markup and code files for the new service.</span></span> <span data-ttu-id="53596-137">根據預設，程式碼編輯器視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="53596-137">By default, the code-editor window opens.</span></span>

6. <span data-ttu-id="53596-138">在資料服務的程式碼中，以繼承自 `/* TODO: put your data source class name here */` 類別且為資料模型實體容器 (您已在步驟 2 中記下該容器) 的型別，取代定義資料服務之類別定義中的 <xref:System.Data.Objects.ObjectContext> 註解。</span><span class="sxs-lookup"><span data-stu-id="53596-138">In the code for the data service, replace the comment `/* TODO: put your data source class name here */` in the definition of the class that defines the data service with the type that inherits from the <xref:System.Data.Objects.ObjectContext> class and that is the entity container of the data model, which was noted in step 2.</span></span>

7. <span data-ttu-id="53596-139">在資料服務的程式碼中，啟用已授權的用戶端以存取資料服務所公開的實體集。</span><span class="sxs-lookup"><span data-stu-id="53596-139">In the code for the data service, enable authorized clients to access the entity sets that the data service exposes.</span></span> <span data-ttu-id="53596-140">如需詳細資訊，請參閱 [建立資料服務](creating-the-data-service.md)。</span><span class="sxs-lookup"><span data-stu-id="53596-140">For more information, see [Creating the Data Service](creating-the-data-service.md).</span></span>

8. <span data-ttu-id="53596-141">若要使用 Web 瀏覽器測試 Northwind 資料服務，請遵循 [從網頁瀏覽器存取服務](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)主題中的指示。</span><span class="sxs-lookup"><span data-stu-id="53596-141">To test the Northwind.svc data service by using a Web browser, follow the instructions in the topic [Accessing the Service from a Web Browser](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="53596-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="53596-142">See also</span></span>

- [<span data-ttu-id="53596-143">定義 WCF 資料服務</span><span class="sxs-lookup"><span data-stu-id="53596-143">Defining WCF Data Services</span></span>](defining-wcf-data-services.md)
- [<span data-ttu-id="53596-144">資料服務提供者</span><span class="sxs-lookup"><span data-stu-id="53596-144">Data Services Providers</span></span>](data-services-providers-wcf-data-services.md)
- [<span data-ttu-id="53596-145">作法：使用反映提供者建立資料服務</span><span class="sxs-lookup"><span data-stu-id="53596-145">How to: Create a Data Service Using the Reflection Provider</span></span>](create-a-data-service-using-rp-wcf-data-services.md)
- [<span data-ttu-id="53596-146">作法：使用 LINQ to SQL 資料來源建立資料服務</span><span class="sxs-lookup"><span data-stu-id="53596-146">How to: Create a Data Service Using a LINQ to SQL Data Source</span></span>](create-a-data-service-using-linq-to-sql-wcf.md)
