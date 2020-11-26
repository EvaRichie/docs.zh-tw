---
title: 錯誤合約
ms.date: 03/30/2017
ms.assetid: b31b140e-dc3b-408b-b3c7-10b6fe769725
ms.openlocfilehash: 898692119e3e71b1c5aeedcd65674a49842ef110
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245207"
---
# <a name="fault-contract"></a>錯誤合約

錯誤合約範例會示範如何在服務與用戶端之間傳達錯誤資訊。 此範例是以 [消費者入門](getting-started-sample.md)為基礎，而將額外的程式碼新增至服務，以將內部例外狀況轉換為錯誤。 用戶端會嘗試執行除數為零，以便強制在服務上造成錯誤狀況。  
  
> [!NOTE]
> 此範例的安裝程序與建置指示位於本主題的結尾。  
  
 計算機合約已修改成包含 <xref:System.ServiceModel.FaultContractAttribute>，如下列範例程式碼所示。  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    int Add(int n1, int n2);  
    [OperationContract]  
    int Subtract(int n1, int n2);  
    [OperationContract]  
    int Multiply(int n1, int n2);  
    [OperationContract]  
    [FaultContract(typeof(MathFault))]  
    int Divide(int n1, int n2);  
}  
```  
  
 <xref:System.ServiceModel.FaultContractAttribute> 屬性表示 `Divide` 作業會傳回 `MathFault` 類型的錯誤。 錯誤可能是能夠序列化的任何類型。 在此範例中，`MathFault` 是資料合約，如下列所示：  
  
```csharp
[DataContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public class MathFault  
{
    private string operation;  
    private string problemType;  
  
    [DataMember]  
    public string Operation  
    {  
        get { return operation; }  
        set { operation = value; }  
    }  
  
    [DataMember]
    public string ProblemType  
    {  
        get { return problemType; }  
        set { problemType = value; }  
    }  
}  
```  
  
 當發生除數為零的例外狀況時，`Divide` 方法會擲回 <xref:System.ServiceModel.FaultException%601> 例外狀況，如下列範例程式碼所示。 這個例外狀況會造成傳送至用戶端的錯誤。  
  
```csharp
public int Divide(int n1, int n2)  
{  
    try  
    {  
        return n1 / n2;  
    }  
    catch (DivideByZeroException)  
    {  
        MathFault mf = new MathFault();  
        mf.operation = "division";  
        mf.problemType = "divide by zero";  
        throw new FaultException<MathFault>(mf);  
    }  
}  
```  
  
 此用戶端程式碼會藉由要求除數為零強制發生錯誤。 當您執行範例時，作業要求和回應會顯示在用戶端主控台視窗中。 這個除數為零狀況將被報告為錯誤。 在用戶端視窗中按下 ENTER 鍵，即可關閉用戶端。  
  
```console  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
FaultException<MathFault>: Math fault while doing division. Problem: divide by zero  
  
Press <ENTER> to terminate client.  
```  
  
 用戶端會藉由攔截適當的 `FaultException<MathFault>` 例外狀況來執行這項動作：  
  
```csharp
catch (FaultException<MathFault> e)  
{  
    Console.WriteLine("FaultException<MathFault>: Math fault while doing " + e.Detail.operation + ". Problem: " + e.Detail.problemType);  
    client.Abort();  
}  
```  
  
 根據預設，未預期之例外狀況的詳細資訊並不會傳送到用戶端，以避免服務實作的詳細資訊逸出服務的安全界限。 `FaultContract` 提供方法說明合約中的錯誤，並將某些例外狀況類型標記為適合傳輸至用戶端。 `FaultException<T>` 會提供將錯誤傳送至取用者的執行階段機制。  
  
 但是，在偵錯時檢視服務失敗的內部詳細資訊是很有用的。 若要關閉之前描述的安全行為，您可以指示在伺服器上的每個未處理例外狀況的詳細資訊是否應該要包含在傳送至用戶端的錯誤中。 這是透過將 <xref:System.ServiceModel.ServiceBehaviorAttribute.IncludeExceptionDetailInFaults%2A> 設定為 `true` 所完成的。 您可以透過程式碼或組態來設定它，如下列範例所示。  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="True" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 此外，此行為必須透過將 `behaviorConfiguration` 設定檔中的服務屬性設定為 "CalculatorServiceBehavior"，與服務相關聯。  
  
 為了攔截用戶端上的這類錯誤，此時必須攔截非泛型的 <xref:System.ServiceModel.FaultException>。  
  
 這個行為應該只用於偵錯用途，而絕對不可啟用於實際執行環境中。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 若要建置方案的 C# 或 Visual Basic .NET 版本，請遵循 [Building the Windows Communication Foundation Samples](building-the-samples.md)中的指示。  
  
3. 若要在單一或跨電腦的設定中執行範例，請遵循執行 [Windows Communication Foundation 範例](running-the-samples.md)中的指示。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Faults`  
