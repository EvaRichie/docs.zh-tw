---
title: MTOM 編碼方式
ms.date: 03/30/2017
ms.assetid: 820e316f-4ee1-4eb5-ae38-b6a536e8a14f
ms.openlocfilehash: cf048e1e6b2e2785accc1bde0336f07e3d84ae5e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84602528"
---
# <a name="mtom-encoding"></a>MTOM 編碼方式
這個範例透過 WSHttpBinding 使用「訊息傳輸最佳化機制」(Message Transmission Optimization Mechanism，MTOM) 訊息編碼。 MTOM 是以未經處理位元組的形式，將大型二進位附件與 SOAP 訊息一起傳輸的機制，可以提供較小的訊息。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MTOM`  
  
 根據預設，WSHttpBinding 會將訊息當做一般文字 XML 來傳送和接收。 若要啟用傳送和接收 MTOM 訊息的功能，請在繫結的組態 (例如，在下列範例程式碼) 中設定 `messageEncoding` 屬性 (Attribute)，或是使用 `MessageEncoding` 屬性 (Property) 直接在繫結上設定。 現在，服務或用戶端可以傳送和接收 MTOM 訊息。  
  
```xml  
<wsHttpBinding>  
  <binding name="WSHttpBinding_IUpload" messageEncoding="Mtom" />  
</wsHttpBinding>  
```  
  
 MTOM 編碼器可以將位元組陣列和資料流最佳化。 在這個範例中，作業會使用 `Stream` 參數，因此可加以最佳化。  

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
  public interface IUpload  
  {  
      [OperationContract]  
      int Upload(Stream data);  
  }  
```
  
 這個範例選用的合約會將二進位資料傳輸至服務，然後接收已上傳的位元組數目做為傳回值。 當安裝了服務並執行用戶端後，範例會列出數字 1000，表示總共收到 1000 個位元組。 輸出的其餘部分則列出各種承載的最佳化與非最佳化訊息大小。  
  
```console
Output:  
1000  
  
Text encoding with a 100 byte payload: 433  
MTOM encoding with a 100 byte payload: 912  
  
Text encoding with a 1000 byte payload: 1633  
MTOM encoding with a 1000 byte payload: 2080  
  
Text encoding with a 10000 byte payload: 13633  
MTOM encoding with a 10000 byte payload: 11080  
  
Text encoding with a 100000 byte payload: 133633  
MTOM encoding with a 100000 byte payload: 101080  
  
Text encoding with a 1000000 byte payload: 1333633  
MTOM encoding with a 1000000 byte payload: 1001080  
  
Press <ENTER> to terminate client.  
```  
  
 使用 MTOM 的目的在最佳化大型二進位承載的傳輸。 對小型二進位承載來說，使用 MTOM 傳送 SOAP 訊息會造成可觀的資源耗用，但是當它擴增到數千位元組以上時，反而會節省大量資源。 這是因為一般文字 XML 會使用 Base64 (每三個位元組需要四個字元) 來編碼二進位資料，使得資料大小增加三分之一。 MTOM 能夠將二進位資料當做未經處理的位元組傳輸，不但節省編碼/解碼時間，而且也產生較小的訊息。 相較於現今的商務文件和數位相片，數千位元組的臨界值實在是微不足道。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 使用下列命令安裝 ASP.NET 4.0。  
  
    ```console
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. 請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
3. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
4. 若要在單一或跨電腦設定中執行範例，請遵循執行[Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
