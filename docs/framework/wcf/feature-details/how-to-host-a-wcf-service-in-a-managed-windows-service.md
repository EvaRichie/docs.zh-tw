---
title: HOW TO：在 Managed Windows 服務中裝載 WCF 服務
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8e37363b-4dad-4fb6-907f-73c30fac1d9a
ms.openlocfilehash: dbd51abbc30b1010f7c4f206aad9a773eca0a714
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593174"
---
# <a name="how-to-host-a-wcf-service-in-a-managed-windows-service"></a>HOW TO：在 Managed Windows 服務中裝載 WCF 服務

本主題概述建立由 Windows 服務裝載的 Windows Communication Foundation （WCF）服務時所需的基本步驟。 此案例是由 managed Windows 服務裝載選項所啟用，這是一項長時間執行的 WCF 服務，在不是訊息啟動的安全環境中裝載于 Internet Information Services （IIS）外部。 服務的存留期會改由作業系統來控制。 所有 Windows 版本都提供這個裝載選項。

Windows 服務可以透過 Microsoft Management Console (MMC) 中的 Microsoft.ManagementConsole.SnapIn 嵌入式管理單元進行管理，並設定成系統啟動時自動啟動。 這個裝載選項包含將 WCF 服務裝載為 managed Windows 服務的應用程式域（AppDomain），因此服務的進程存留期是由 Windows 服務的服務控制管理員（SCM）所控制。

服務程式碼包含服務合約的服務實作、Windows 服務類別以及安裝程式類別。 服務實類別 `CalculatorService` 是 WCF 服務。 `CalculatorWindowsService` 是一項 Windows 服務。 為了限定為 Windows 服務，此類別會繼承自 `ServiceBase`，並且實作 `OnStart` 和 `OnStop` 方法。 在 `OnStart` 中，會為 <xref:System.ServiceModel.ServiceHost> 型別建立並開啟 `CalculatorService`。 使用 `OnStop` 時，則會停止與處置服務。 主機也會負責提供服務主機的基底位址，該位址必須設定在應用程式設定中。 繼承自 <xref:System.Configuration.Install.Installer> 的安裝程式類別，會允許 Installutil.exe 工具將程式當做 Windows 服務進行安裝。

## <a name="construct-the-service-and-provide-the-hosting-code"></a>建構服務並提供裝載程式碼

1. 建立名為**Service**的新 Visual Studio**主控台應用程式**專案。

2. 將 Program.cs 重新命名為 Service.cs。

3. 將命名空間變更為 `Microsoft.ServiceModel.Samples` 。

4. 加入下列組件的參考：

    - System.ServiceModel.dll

    - System.ServiceProcess.dll

    - System.Configuration.Install.dll

5. 使用陳述式將下列內容加入至 Service.cs。

     [!code-csharp[c_HowTo_HostInNTService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#0)]
     [!code-vb[c_HowTo_HostInNTService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#0)]

6. 定義 `ICalculator` 服務合約，如下列程式碼所示。

     [!code-csharp[c_HowTo_HostInNTService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#1)]
     [!code-vb[c_HowTo_HostInNTService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#1)]

7. 在 `CalculatorService` 類別中實作服務合約，如下列程式碼所示。

     [!code-csharp[c_HowTo_HostInNTService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#2)]
     [!code-vb[c_HowTo_HostInNTService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#2)]

8. 建立繼承自 `CalculatorWindowsService` 類別的新類別，名為 <xref:System.ServiceProcess.ServiceBase>。 加入名為 `serviceHost` 的區域變數，以參考 <xref:System.ServiceModel.ServiceHost> 執行個體。 定義 `Main` 方法來呼叫 `ServiceBase.Run(new CalculatorWindowsService)`。

     [!code-csharp[c_HowTo_HostInNTService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#3)]
     [!code-vb[c_HowTo_HostInNTService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#3)]

9. 建立並開啟新的 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 執行個體，以覆寫 <xref:System.ServiceModel.ServiceHost> 方法，如下列程式碼所示。

     [!code-csharp[c_HowTo_HostInNTService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#4)]
     [!code-vb[c_HowTo_HostInNTService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#4)]

10. 覆寫用來關閉 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 的 <xref:System.ServiceModel.ServiceHost> 方法，如下列程式碼所示。

     [!code-csharp[c_HowTo_HostInNTService#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#5)]
     [!code-vb[c_HowTo_HostInNTService#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#5)]

11. 建立繼承自 `ProjectInstaller` 且其 <xref:System.Configuration.Install.Installer> 標記設為 <xref:System.ComponentModel.RunInstallerAttribute> 的新類別，名為 `true`。 這樣 Installutil.exe 工具就能安裝此 Windows 服務。

     [!code-csharp[c_HowTo_HostInNTService#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#6)]
     [!code-vb[c_HowTo_HostInNTService#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#6)]

12. 移除您在建立專案時所產生的 `Service` 類別。

13. 將應用程式組態檔加入至專案。 以下列組態 XML 取代該檔案的內容。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <system.serviceModel>    <services>
          <!-- This section is optional with the new configuration model
               introduced in .NET Framework 4. -->
          <service name="Microsoft.ServiceModel.Samples.CalculatorService"
                   behaviorConfiguration="CalculatorServiceBehavior">
            <host>
              <baseAddresses>
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>
              </baseAddresses>
            </host>
            <!-- this endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service  -->
            <endpoint address=""
                      binding="wsHttpBinding"
                      contract="Microsoft.ServiceModel.Samples.ICalculator" />
            <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
            <endpoint address="mex"
                      binding="mexHttpBinding"
                      contract="IMetadataExchange" />
          </service>
        </services>
        <behaviors>
          <serviceBehaviors>
            <behavior name="CalculatorServiceBehavior">
              <serviceMetadata httpGetEnabled="true"/>
              <serviceDebug includeExceptionDetailInFaults="False"/>
            </behavior>
          </serviceBehaviors>
        </behaviors>
      </system.serviceModel>
    </configuration>
    ```

     以滑鼠右鍵按一下**方案總管**中的 app.config 檔案，然後選取 [**屬性**]。 在 [**複製到輸出目錄**] 底下，選取 [**更新時複製**]。

     此範例會在組態檔中明確地指定端點。 如果您沒有將任何端點加入至服務中，執行階段會為您加入預設端點。 在這個範例中，由於服務將 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 設定為 `true`，表示您的服務也已啟用中繼資料發行。 如需預設端點、繫結和行為的詳細資訊，請參閱[簡化的組態](../simplified-configuration.md)和 [WCF 服務的簡化組態](../samples/simplified-configuration-for-wcf-services.md)。

## <a name="install-and-run-the-service"></a>安裝並執行服務

1. 建置方案以建立 `Service.exe` 可執行檔。

2. 開啟 Visual Studio 的開發人員命令提示字元，然後流覽至專案目錄。 在命令提示字元中輸入 `installutil bin\service.exe` 以安裝 Windows 服務 

     在命令提示字元中輸入 `services.msc` 以存取服務控制管理員 (SCM)。 Windows 服務應該會在 [服務] 中顯示為 "WCFWindowsServiceSample"。 只有在 Windows 服務正在執行時，WCF 服務才會回應用戶端。 若要啟動服務，請在 SCM 中以滑鼠右鍵按一下它，然後選取 [開始]，或在命令提示字元中輸入**net Start WCFWindowsServiceSample** 。

3. 若要變更服務，必須先加以停止並解除安裝。 若要停止服務，請以滑鼠右鍵按一下 SCM 中的服務並選取 [停止]，或在命令提示字元中**輸入 net Stop WCFWindowsServiceSample** 。 請注意，如果您在停止 Windows 服務後執行用戶端，則當用戶端嘗試存取此服務時將會發生 <xref:System.ServiceModel.EndpointNotFoundException> 例外狀況。 若要在命令提示字元中卸載 Windows 服務類型**installutil.exe/u bin\service.exe** 。

## <a name="example"></a>範例

以下是本主題所使用之程式碼的完整清單：

[!code-csharp[c_HowTo_HostInNTService#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinntservice/cs/service.cs#8)]
[!code-vb[c_HowTo_HostInNTService#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostinntservice/vb/service.vb#8)]

就像「自我裝載」選項一樣，Windows 服務裝載環境要求將某些裝載程式碼撰寫成應用程式的一部分。 服務會實作成為主控台應用程式並包含專屬的裝載程式碼。 在其他裝載環境中，例如 Internet Information Services (IIS) 所裝載的 Windows 處理序啟用服務 (WAS)，開發人員就不需要撰寫裝載程式碼。

## <a name="see-also"></a>請參閱

- [簡化設定](../simplified-configuration.md)
- [在受控應用程式中裝載](hosting-in-a-managed-application.md)
- [裝載服務](../hosting-services.md)
- [Windows Server AppFabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
