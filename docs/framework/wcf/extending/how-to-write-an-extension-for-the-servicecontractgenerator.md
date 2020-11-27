---
title: 作法：撰寫 ServiceContractGenerator 的延伸模組
ms.date: 03/30/2017
ms.assetid: 876ca823-bd16-4bdf-9e0f-02092df90e51
ms.openlocfilehash: 3a81204ca470b9b94d9e8f048ecccbade74b2e10
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254632"
---
# <a name="how-to-write-an-extension-for-the-servicecontractgenerator"></a>作法：撰寫 ServiceContractGenerator 的延伸模組

本主題說明如何撰寫 <xref:System.ServiceModel.Description.ServiceContractGenerator> 的擴充。 您可以在作業行為上實作 <xref:System.ServiceModel.Description.IOperationContractGenerationExtension> 介面，或在合約行為上實作 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> 介面來達到這個目的。 本主題說明如何在合約行為上實作 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension> 介面。  
  
 <xref:System.ServiceModel.Description.ServiceContractGenerator> 會從 <xref:System.ServiceModel.Description.ServiceEndpoint>、<xref:System.ServiceModel.Description.ContractDescription> 和 <xref:System.ServiceModel.Channels.Binding> 執行個體中產生服務合約、用戶端類型，與用戶端組態。 一般來說，您可以從服務中繼資料匯入 <xref:System.ServiceModel.Description.ServiceEndpoint>、<xref:System.ServiceModel.Description.ContractDescription>，和 <xref:System.ServiceModel.Channels.Binding> 執行個體，然後使用這些執行個體來產生程式碼以呼叫服務。 此範例會使用 <xref:System.ServiceModel.Description.IWsdlImportExtension> 實作來處理 WSDL 附註，然後將程式碼產生擴充加入至匯入的合約中，以便在產生的程式碼中產生註解。  
  
### <a name="to-write-an-extension-for-the-servicecontractgenerator"></a>若要撰寫 ServiceContractGenerator 的擴充  
  
1. 實作 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension>。 若要修改產生的服務合約，請使用已傳入至 <xref:System.ServiceModel.Description.ServiceContractGenerationContext> 方法的 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> 執行個體。  
  
    ```csharp
    public void GenerateContract(ServiceContractGenerationContext context)  
    {  
        Console.WriteLine("In generate contract.");  
        context.ContractType.Comments.AddRange(Formatter.FormatComments(commentText));  
    }  
    ```  
  
2. 在相同類別上實作 <xref:System.ServiceModel.Description.IWsdlImportExtension>。 <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> 方法可以處理特定的 WSDL 擴充 (在此情況下為 WSDL 附註)，方法是將程式碼產生擴充加入至下列匯入的 <xref:System.ServiceModel.Description.ContractDescription> 執行個體。  
  
    ```csharp
    public void ImportContract(WsdlImporter importer, WsdlContractConversionContext context)
    {
        // Contract documentation
        if (context.WsdlPortType.Documentation != null)
        {
            context.Contract.Behaviors.Add(new WsdlDocumentationImporter(context.WsdlPortType.Documentation));
        }
        // Operation documentation
        foreach (Operation operation in context.WsdlPortType.Operations)
        {
            if (operation.Documentation != null)
            {
                OperationDescription operationDescription = context.Contract.Operations.Find(operation.Name);
                if (operationDescription != null)
                {
                    operationDescription.Behaviors.Add(new WsdlDocumentationImporter(operation.Documentation));
                }
            }
        }
    }
    public void BeforeImport(ServiceDescriptionCollection wsdlDocuments, XmlSchemaSet xmlSchemas, ICollection<XmlElement> policy)
    {
        Console.WriteLine("BeforeImport called.");
    }

    public void ImportEndpoint(WsdlImporter importer, WsdlEndpointConversionContext context)
    {
        Console.WriteLine("ImportEndpoint called.");
    }
    ```  
  
3. 將 WSDL 匯入工具加入至您的用戶端組態。  
  
    ```xml  
    <metadata>  
      <wsdlImporters>  
        <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
      </wsdlImporters>  
    </metadata>  
    ```  
  
4. 在用戶端程式碼中，建立 `MetadataExchangeClient` 並呼叫 `GetMetadata`。  
  
    ```csharp
    var mexClient = new MetadataExchangeClient(metadataAddress);  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet metaDocs = mexClient.GetMetadata();  
    ```  
  
5. 建立 `WsdlImporter` 並呼叫 `ImportAllContracts`。  
  
    ```csharp
    var importer = new WsdlImporter(metaDocs);
    System.Collections.ObjectModel.Collection<ContractDescription> contracts = importer.ImportAllContracts();  
    ```  
  
6. 為每個合約建立 `ServiceContractGenerator` 並呼叫 `GenerateServiceContractType`。  
  
    ```csharp
    var generator = new ServiceContractGenerator();  
    foreach (ContractDescription contract in contracts)  
    {  
       generator.GenerateServiceContractType(contract);  
    }  
    if (generator.Errors.Count != 0)  
       throw new Exception("There were errors during code compilation.");  
    ```  
  
7. 在實作 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension.GenerateContract%28System.ServiceModel.Description.ServiceContractGenerationContext%29> 的特定合約上，會針對每個合約行為自動呼叫 <xref:System.ServiceModel.Description.IServiceContractGenerationExtension>。 這個方法會接著修改傳入的 <xref:System.ServiceModel.Description.ServiceContractGenerationContext>。 在這個範例中會加入註解。  
  
## <a name="see-also"></a>另請參閱

- [中繼資料](../feature-details/metadata.md)
- [作法：匯入自訂 WSDL](how-to-import-custom-wsdl.md)
