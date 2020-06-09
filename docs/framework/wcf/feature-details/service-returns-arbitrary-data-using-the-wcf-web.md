---
title: HOW TO：使用 WCF Web HTTP 程式設計模型建立傳回任意資料的服務
ms.date: 03/30/2017
ms.assetid: 0283955a-b4ae-458d-ad9e-6fbb6f529e3d
ms.openlocfilehash: 9753fbc9b333cb7e89ddc8dff030cb1f62ede23b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600357"
---
# <a name="how-to-create-a-service-that-returns-arbitrary-data-using-the-wcf-web-http-programming-model"></a><span data-ttu-id="197b4-102">HOW TO：使用 WCF Web HTTP 程式設計模型建立傳回任意資料的服務</span><span class="sxs-lookup"><span data-stu-id="197b4-102">How to: Create a Service That Returns Arbitrary Data Using The WCF Web HTTP Programming Model</span></span>
<span data-ttu-id="197b4-103">有時候，開發人員必須要能夠完全控制資料從服務作業傳回的方式。</span><span class="sxs-lookup"><span data-stu-id="197b4-103">Sometimes developers must have full control of how data is returned from a service operation.</span></span> <span data-ttu-id="197b4-104">當服務作業必須以 WCF 不支援的格式傳回資料時，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="197b4-104">This is the case when a service operation must return data in a format not supported by WCF.</span></span> <span data-ttu-id="197b4-105">本主題討論如何使用 WCF WEB HTTP 程式設計模型來建立這類服務。</span><span class="sxs-lookup"><span data-stu-id="197b4-105">This topic discusses using the WCF WEB HTTP Programming Model to create such a service.</span></span> <span data-ttu-id="197b4-106">該項服務提供一種會傳回資料流的作業。</span><span class="sxs-lookup"><span data-stu-id="197b4-106">This service has one operation that returns a stream.</span></span>  
  
### <a name="to-implement-the-service-contract"></a><span data-ttu-id="197b4-107">若要實作服務合約</span><span class="sxs-lookup"><span data-stu-id="197b4-107">To implement the service contract</span></span>  
  
1. <span data-ttu-id="197b4-108">定義服務合約。</span><span class="sxs-lookup"><span data-stu-id="197b4-108">Define the service contract.</span></span> <span data-ttu-id="197b4-109">該合約名稱為 `IImageServer`，並且擁有會傳回 `GetImage`的<xref:System.IO.Stream> 方法。</span><span class="sxs-lookup"><span data-stu-id="197b4-109">The contract is called `IImageServer` and has one method called `GetImage` that returns a <xref:System.IO.Stream>.</span></span>  
  
    ```csharp  
    [ServiceContract]  
        public interface IImageServer  
        {  
            [WebGet]  
            Stream GetImage(int width, int height);  
        }  
    ```  
  
     <span data-ttu-id="197b4-110">因為方法 <xref:System.IO.Stream> 會傳回，所以 WCF 會假設作業對於從服務作業傳回的位元組有完整的控制權，而且它不會對傳回的資料套用任何格式。</span><span class="sxs-lookup"><span data-stu-id="197b4-110">Because the method returns a <xref:System.IO.Stream>, WCF assumes that the operation has complete control over the bytes that are returned from the service operation and it applies no formatting to the data that is returned.</span></span>  
  
2. <span data-ttu-id="197b4-111">實作服務合約。</span><span class="sxs-lookup"><span data-stu-id="197b4-111">Implement the service contract.</span></span> <span data-ttu-id="197b4-112">該合約只能有一項作業 (`GetImage`)。</span><span class="sxs-lookup"><span data-stu-id="197b4-112">The contract has only one operation (`GetImage`).</span></span> <span data-ttu-id="197b4-113">這個方法會產生一張點陣圖，然後以 JPG 格式儲存為 <xref:System.IO.MemoryStream>。</span><span class="sxs-lookup"><span data-stu-id="197b4-113">This method generates a bitmap and then save it to a <xref:System.IO.MemoryStream> in .jpg format.</span></span> <span data-ttu-id="197b4-114">然後，這個作業會將該資料流傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="197b4-114">The operation then returns that stream to the caller.</span></span>  
  
    ```csharp
    public class Service : IImageServer
    {
        public Stream GetImage(int width, int height)
        {
            Bitmap bitmap = new Bitmap(width, height);
            for (int i = 0; i < bitmap.Width; i++)
            {
                for (int j = 0; j < bitmap.Height; j++)
                {
                    bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);
                }
            }
            MemoryStream ms = new MemoryStream();
            bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);
            ms.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
            return ms;
        }
    }
    ```  
  
     <span data-ttu-id="197b4-115">請注意程式碼的倒數第二行：`WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";`</span><span class="sxs-lookup"><span data-stu-id="197b4-115">Notice the second to last line of code: `WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";`</span></span>  
  
     <span data-ttu-id="197b4-116">這會將內容類型標頭設定為 `"image/jpeg"` 。</span><span class="sxs-lookup"><span data-stu-id="197b4-116">This sets the content type header to `"image/jpeg"`.</span></span> <span data-ttu-id="197b4-117">雖然本範例示範的是如何傳回 JPG 檔案，但是您可以修改範例內容，使其傳回您所需的任何資料類型。</span><span class="sxs-lookup"><span data-stu-id="197b4-117">Although this sample shows how to return a .jpg file, it can be modified to return any type of data that is required, in any format.</span></span> <span data-ttu-id="197b4-118">該作業必須要擷取或產生資料，然後將資料寫入資料流中。</span><span class="sxs-lookup"><span data-stu-id="197b4-118">The operation must retrieve or generate the data and then write it to a stream.</span></span>  
  
### <a name="to-host-the-service"></a><span data-ttu-id="197b4-119">若要裝載服務</span><span class="sxs-lookup"><span data-stu-id="197b4-119">To host the service</span></span>  
  
1. <span data-ttu-id="197b4-120">建立裝載服務的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="197b4-120">Create a console application to host the service.</span></span>  
  
    ```csharp
    class Program  
    {  
        static void Main(string[] args)  
        {  
        }
    }  
    ```  
  
2. <span data-ttu-id="197b4-121">建立一個變數，以保留該服務位於 `Main`方法內的基底位址。</span><span class="sxs-lookup"><span data-stu-id="197b4-121">Create a variable to hold the base address for the service within the `Main` method.</span></span>  
  
    ```csharp
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3. <span data-ttu-id="197b4-122">指定服務類別及基底位址，以建立該服務的 <xref:System.ServiceModel.ServiceHost> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="197b4-122">Create a <xref:System.ServiceModel.ServiceHost> instance for the service specifying the service class and the base address.</span></span>  
  
    ```csharp
    ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
    ```  
  
4. <span data-ttu-id="197b4-123">利用 <xref:System.ServiceModel.WebHttpBinding> 及 <xref:System.ServiceModel.Description.WebHttpBehavior>加入一個端點。</span><span class="sxs-lookup"><span data-stu-id="197b4-123">Add an endpoint using the <xref:System.ServiceModel.WebHttpBinding> and the <xref:System.ServiceModel.Description.WebHttpBehavior>.</span></span>  
  
    ```csharp  
    host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5. <span data-ttu-id="197b4-124">開啟服務主機。</span><span class="sxs-lookup"><span data-stu-id="197b4-124">Open the service host.</span></span>  
  
    ```csharp  
    host.Open();  
    ```  
  
6. <span data-ttu-id="197b4-125">等候使用者按下 ENTER 終止該服務。</span><span class="sxs-lookup"><span data-stu-id="197b4-125">Wait until the user presses ENTER to terminate the service.</span></span>  
  
    ```csharp
    Console.WriteLine("Service is running");  
    Console.Write("Press ENTER to close the host");  
    Console.ReadLine();  
    host.Close();  
    ```  
  
### <a name="to-call-the-raw-service-using-internet-explorer"></a><span data-ttu-id="197b4-126">若要使用 Internet Explorer 呼叫原始服務</span><span class="sxs-lookup"><span data-stu-id="197b4-126">To call the raw service using Internet Explorer</span></span>  
  
1. <span data-ttu-id="197b4-127">執行服務後，您應該會看見下列來自服務的輸出：</span><span class="sxs-lookup"><span data-stu-id="197b4-127">Run the service, you should see the following output from the service.</span></span> `Service is running Press ENTER to close the host`  
  
2. <span data-ttu-id="197b4-128">開啟 Internet Explorer，輸入 `http://localhost:8000/Service/GetImage?width=50&height=40`，您應該會看見對角線為藍色的黃色長方形。</span><span class="sxs-lookup"><span data-stu-id="197b4-128">Open Internet Explorer and type in `http://localhost:8000/Service/GetImage?width=50&height=40` you should see a yellow rectangle with a blue diagonal line through the center.</span></span>  
  
## <a name="example"></a><span data-ttu-id="197b4-129">範例</span><span class="sxs-lookup"><span data-stu-id="197b4-129">Example</span></span>  
 <span data-ttu-id="197b4-130">以下是這個主題的完整程式碼清單。</span><span class="sxs-lookup"><span data-stu-id="197b4-130">The following is a complete listing of the code for this topic.</span></span>  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Drawing;  
  
namespace RawImageService  
{  
    // Define the service contract  
    [ServiceContract]  
    public interface IImageServer  
    {  
        [WebGet]  
        Stream GetImage(int width, int height);  
    }  
  
    // implement the service contract  
    public class Service : IImageServer  
    {  
        public Stream GetImage(int width, int height)  
        {  
            // Although this method returns a jpeg, it can be  
            // modified to return any data you want within the stream  
            Bitmap bitmap = new Bitmap(width, height);  
            for (int i = 0; i < bitmap.Width; i++)  
            {  
                for (int j = 0; j < bitmap.Height; j++)  
                {  
                    bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);  
                }  
            }  
            MemoryStream ms = new MemoryStream();  
            bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);  
            ms.Position = 0;  
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";  
            return ms;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Service is running");  
            Console.Write("Press ENTER to close the host");  
            Console.ReadLine();  
            host.Close();  
  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a><span data-ttu-id="197b4-131">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="197b4-131">Compiling the Code</span></span>  
  
- <span data-ttu-id="197b4-132">編譯範例程式碼時，請參考 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。</span><span class="sxs-lookup"><span data-stu-id="197b4-132">When compiling the sample code reference System.ServiceModel.dll and System.ServiceModel.Web.dll.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="197b4-133">請參閱</span><span class="sxs-lookup"><span data-stu-id="197b4-133">See also</span></span>

- [<span data-ttu-id="197b4-134">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="197b4-134">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
