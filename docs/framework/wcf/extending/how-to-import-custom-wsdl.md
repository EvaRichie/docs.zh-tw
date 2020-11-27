---
title: 作法：匯入自訂 WSDL
ms.date: 03/30/2017
ms.assetid: ddc3718d-ce60-44f6-92af-a5c67477dd99
ms.openlocfilehash: c5aa554394743314a91afd6a5cdf86f9974e81f8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96249081"
---
# <a name="how-to-import-custom-wsdl"></a><span data-ttu-id="2b877-102">作法：匯入自訂 WSDL</span><span class="sxs-lookup"><span data-stu-id="2b877-102">How to: Import Custom WSDL</span></span>

<span data-ttu-id="2b877-103">這個主題會描述如何匯入自訂 WSDL。</span><span class="sxs-lookup"><span data-stu-id="2b877-103">This topic describes how to import custom WSDL.</span></span> <span data-ttu-id="2b877-104">若要處理自訂 WSDL，您必須實作 <xref:System.ServiceModel.Description.IWsdlImportExtension> 介面。</span><span class="sxs-lookup"><span data-stu-id="2b877-104">To handle the custom WSDL, you must implement the <xref:System.ServiceModel.Description.IWsdlImportExtension> interface.</span></span>  
  
### <a name="to-import-custom-wsdl"></a><span data-ttu-id="2b877-105">匯入自訂 WSDL</span><span class="sxs-lookup"><span data-stu-id="2b877-105">To import custom WSDL</span></span>  
  
1. <span data-ttu-id="2b877-106">實作 <xref:System.ServiceModel.Description.IWsdlImportExtension>。</span><span class="sxs-lookup"><span data-stu-id="2b877-106">Implement <xref:System.ServiceModel.Description.IWsdlImportExtension>.</span></span> <span data-ttu-id="2b877-107">實作 <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%28System.Web.Services.Description.ServiceDescriptionCollection%2CSystem.Xml.Schema.XmlSchemaSet%2CSystem.Collections.Generic.ICollection%7BSystem.Xml.XmlElement%7D%29> 方法，以便於匯入中繼資料前進行修改。</span><span class="sxs-lookup"><span data-stu-id="2b877-107">Implement the <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%28System.Web.Services.Description.ServiceDescriptionCollection%2CSystem.Xml.Schema.XmlSchemaSet%2CSystem.Collections.Generic.ICollection%7BSystem.Xml.XmlElement%7D%29> method to modify the metadata before it is imported.</span></span> <span data-ttu-id="2b877-108">實作 <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> 和 <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> 方法，以便修改從中繼資料匯入的合約和端點。</span><span class="sxs-lookup"><span data-stu-id="2b877-108">Implement the <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlEndpointConversionContext%29> and <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%28System.ServiceModel.Description.WsdlImporter%2CSystem.ServiceModel.Description.WsdlContractConversionContext%29> methods to modify contracts and endpoints imported from the metadata.</span></span> <span data-ttu-id="2b877-109">若要存取匯入的合約或端點，請使用相對應的內容物件 (<xref:System.ServiceModel.Description.WsdlContractConversionContext> 或 <xref:System.ServiceModel.Description.WsdlEndpointConversionContext>)：</span><span class="sxs-lookup"><span data-stu-id="2b877-109">To access the imported contract or endpoint, use the corresponding context object (<xref:System.ServiceModel.Description.WsdlContractConversionContext> or <xref:System.ServiceModel.Description.WsdlEndpointConversionContext>):</span></span>  
  
    ```csharp
    public class WsdlDocumentationImporter : IWsdlImportExtension
    {
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
    }
    ```
  
2. <span data-ttu-id="2b877-110">設定用戶端應用程式以使用自訂 WSDL 匯入工具。</span><span class="sxs-lookup"><span data-stu-id="2b877-110">Configure the client application to use the custom WSDL importer.</span></span> <span data-ttu-id="2b877-111">請注意，如果正在使用 Svcutil.exe，您應該針對 Svcutil.exe (Svcutil.exe.config) 將此組態新增至組態檔：</span><span class="sxs-lookup"><span data-stu-id="2b877-111">Note that if you are using Svcutil.exe, you should add this configuration to the configuration file for Svcutil.exe (Svcutil.exe.config):</span></span>  
  
    ```xml  
    <system.serviceModel>  
          <client>  
            <endpoint
              address="http://localhost:8000/Fibonacci"
              binding="wsHttpBinding"  
              contract="IFibonacci"  
            />  
            <metadata>  
              <wsdlImporters>  
                <extension type="Microsoft.WCF.Documentation.WsdlDocumentationImporter, WsdlDocumentation" />  
              </wsdlImporters>  
            </metadata>  
          </client>  
        </system.serviceModel>  
    ```  
  
3. <span data-ttu-id="2b877-112">建立新的 <xref:System.ServiceModel.Description.WsdlImporter> 執行個體 (在包含您要匯入之 WSDL 文件的 <xref:System.ServiceModel.Description.MetadataSet> 執行個體中傳遞)，並且呼叫 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>：</span><span class="sxs-lookup"><span data-stu-id="2b877-112">Create a new <xref:System.ServiceModel.Description.WsdlImporter> instance (passing in the <xref:System.ServiceModel.Description.MetadataSet> instance that contains the WSDL documents that you want to import), and call <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>:</span></span>  
  
    ```csharp
    WsdlImporter importer = new WsdlImporter(metaDocs);
    System.Collections.ObjectModel.Collection<ContractDescription> contracts = importer.ImportAllContracts();  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="2b877-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2b877-113">See also</span></span>

- [<span data-ttu-id="2b877-114">中繼資料</span><span class="sxs-lookup"><span data-stu-id="2b877-114">Metadata</span></span>](../feature-details/metadata.md)
- [<span data-ttu-id="2b877-115">匯出和匯入中繼資料</span><span class="sxs-lookup"><span data-stu-id="2b877-115">Exporting and Importing Metadata</span></span>](../feature-details/exporting-and-importing-metadata.md)
- [<span data-ttu-id="2b877-116">自訂 WSDL 發行物</span><span class="sxs-lookup"><span data-stu-id="2b877-116">Custom WSDL Publication</span></span>](../samples/custom-wsdl-publication.md)
