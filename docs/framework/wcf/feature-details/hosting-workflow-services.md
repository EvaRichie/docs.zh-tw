---
title: 裝載工作流程服務
ms.date: 03/30/2017
ms.assetid: 2d55217e-8697-4113-94ce-10b60863342e
ms.openlocfilehash: 95d8d8b8ea15ef543471afb19462ccb424e8e39b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555805"
---
# <a name="hosting-workflow-services"></a>裝載工作流程服務

您必須裝載工作流程服務，才能讓它回應傳入的訊息。 工作流程服務使用了 WCF 訊息基礎結構，因此會以類似的方式裝載。 就像 WCF 服務一樣，工作流程服務可以裝載于任何受控應用程式、Internet Information Services (IIS) ，或在 Windows Process Activation Services () 。 此外，工作流程服務可以裝載于 Windows Server App Fabric 底下。 如需 Windows Server App Fabric 的詳細資訊，請參閱 [Windows Server 應用程式](/previous-versions/appfabric/ff384253(v=azure.10))網狀架構檔、 [appfabric 裝載功能](/previous-versions/appfabric/ee677189(v=azure.10))和 [appfabric 裝載概念](/previous-versions/appfabric/ee677371(v=azure.10))。 如需裝載 WCF 服務之各種方式的詳細資訊，請參閱 [裝載服務](../hosting-services.md)。

## <a name="hosting-in-a-managed-application"></a>在 Managed 應用程式中裝載
 若要在 Managed 應用程式中裝載工作流程服務，請使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 類別。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 建構函式可讓您指定單一工作流程服務執行個體、工作流程服務定義，或是一個活動使用工作流程訊息的多個活動。 呼叫 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 會造成服務開始接聽傳入的訊息。

## <a name="hosting-under-iis-or-was"></a>在 IIS 或 WAS 底下裝載
 在 IIS 或 WAS 底下裝載工作流程服務，需要建立虛擬目錄，並且在虛擬目錄中放入定義服務及其行為的檔案。 在 IIS 或 WAS 底下裝載工作流程服務時，有幾個可能的方法：

- 將定義工作流程服務的 .xamlx 檔案置入 IIS/WAS 虛擬目錄，與指定服務行為、端點及其他組態項目的 Web.config 檔案放在一起。

- 將定義工作流程服務的 .xamlx 檔案置入 IIS/WAS 虛擬目錄。 這個 .xamlx 檔案指定要公開的端點。 端點是在 `WorkflowService.Endpoints` 項目中指定的，如下列範例所示。

    ```xml
    <WorkflowService xmlns="http://schemas.microsoft.com/netfx/2009/xaml/servicemodel"  xmlns:p1="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:sad="clr-namespace:System.Activities.Debugger;assembly=System.Activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
      <WorkflowService.Endpoints>
        <Endpoint ServiceContractName="IWorkFlowEchoService" AddressUri="">
          <Endpoint.Binding>
            <BasicHttpBinding />
          </Endpoint.Binding>
        </Endpoint>
      </WorkflowService.Endpoints>
    <!-- ... -->
    </WorkflowService>
    ```

    > [!NOTE]
    > 行為不能在 .xamlx 檔案中指定，所以如果需要指定行為設定，就必須使用 Web.config。

- 將定義工作流程服務的 .xamlx 檔案置入 IIS/WAS 虛擬目錄。 此外，請將 .svc 檔案放進虛擬目錄。 這個 .svc 檔案可讓您指定一個自訂的 Web 服務裝載處理站、套用自訂行為，或是從自訂位置載入組態。

- 將包含活動的組件置入 IIS/WAS 虛擬目錄，該活動會使用多個 WCF 訊息活動。

 定義工作流程服務的 service1.xamlx 檔案必須包含 <`Service`> 根項目或根項目，其中包含任何衍生自的型別 <xref:System.Workflow.ComponentModel.Activity> 。 使用 Visual Studio 活動範本時，會建立 service1.xamlx 檔案。 使用 WCF Workflow Service 範本時，會建立 service1.xamlx 檔案。

## <a name="hosting-workflow-services-under-windows-server-app-fabric"></a>在 Windows Server App Fabric 底下裝載工作流程服務
 在 Windows Server App Fabric 底下裝載工作流程服務的方式與在 IIS/WAS 底下裝載的方式相同。 唯一的差異在於已安裝 Windows Server App Fabric 的事實。 Windows Server App Fabric 提供了一些加入至 Internet Information Services 管理員的工具，以及 Powershell 指令程式。 這些工具會簡化部署、管理和追蹤工作流程與 WCF 服務的作業。

## <a name="referencing-custom-activities"></a>參考自訂活動
 自訂活動的參考必須加入至 `Assemblies` <> 下的 <> 區段， `System.Web.Compilation` 以便將它們載入至應用程式域，而 XAML 還原序列化程式可以找到類型。 這些設定可以在應用程式層級進行，如果設定值應該套用到電腦上的所有應用程式，則可以在根 Web.config 進行這些設定。

## <a name="deployment"></a>部署
 Web 部署工具的建立，是要讓部署的工作更容易進行。 此工具可讓您在 IIS 6.0 與 IIS 7.0 之間移轉應用程式、同步處理伺服器陣列，以及封裝、封存及部署 Web 應用程式。 如需詳細資訊，請參閱 [MS Deployment Tool](https://go.microsoft.com/fwlink/?LinkId=178690)。

## <a name="see-also"></a>另請參閱

- [工作流程服務主機內部](workflow-service-host-internals.md)
- [設定 WorkflowServiceHost](configuring-workflowservicehost.md)
