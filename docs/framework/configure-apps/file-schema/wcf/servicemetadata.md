---
title: <serviceMetadata>
ms.date: 03/30/2017
ms.assetid: 2b4c3b4c-31d4-4908-a9b7-5bb411c221f2
ms.openlocfilehash: c421273d1d08db047a51f1f1e4f9d6c908f12986
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "84201789"
---
# \<serviceMetadata>
<span data-ttu-id="78cca-101">指定服務中繼資料和相關資訊的發行。</span><span class="sxs-lookup"><span data-stu-id="78cca-101">Specifies the publication of service metadata and associated information.</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceMetadata>**  
  
## <a name="syntax"></a><span data-ttu-id="78cca-102">語法</span><span class="sxs-lookup"><span data-stu-id="78cca-102">Syntax</span></span>  
  
```xml  
<serviceMetadata externalMetadataLocation="String"
                 httpGetBinding="String"
                 httpGetBindingConfiguration="String"
                 httpGetEnabled="Boolean"
                 httpGetUrl="String"
                 httpsGetBinding="String"
                 httpsGetBindingConfiguration="String"
                 httpsGetEnabled="Boolean"
                 httpsGetUrl="String"
                 policyVersion="Policy12/Policy15" />
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="78cca-103">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="78cca-103">Attributes and Elements</span></span>  
 <span data-ttu-id="78cca-104">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="78cca-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="78cca-105">屬性</span><span class="sxs-lookup"><span data-stu-id="78cca-105">Attributes</span></span>  
  
|<span data-ttu-id="78cca-106">屬性</span><span class="sxs-lookup"><span data-stu-id="78cca-106">Attribute</span></span>|<span data-ttu-id="78cca-107">描述</span><span class="sxs-lookup"><span data-stu-id="78cca-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="78cca-108">externalMetadataLocation</span><span class="sxs-lookup"><span data-stu-id="78cca-108">externalMetadataLocation</span></span>|<span data-ttu-id="78cca-109">包含 WSDL 檔案位置的 URI，此位置會傳回給使用者，以回應 WSDL 和 MEX 要求，而非自動產生的 WSDL。</span><span class="sxs-lookup"><span data-stu-id="78cca-109">A Uri that contains the location of a WSDL file, which is returned to the user in response to WSDL and MEX requests instead of the auto-generated WSDL.</span></span> <span data-ttu-id="78cca-110">如果未設定這個屬性，則會傳回預設 WSDL。</span><span class="sxs-lookup"><span data-stu-id="78cca-110">When this attribute is not set, the default WSDL is returned.</span></span> <span data-ttu-id="78cca-111">預設值是空字串。</span><span class="sxs-lookup"><span data-stu-id="78cca-111">The default is an empty string.</span></span>|  
|<span data-ttu-id="78cca-112">httpGetBinding</span><span class="sxs-lookup"><span data-stu-id="78cca-112">httpGetBinding</span></span>|<span data-ttu-id="78cca-113">字串，這個字串會指定透過 HTTP GET 擷取中繼資料所要使用之繫結的型別。</span><span class="sxs-lookup"><span data-stu-id="78cca-113">A string that specifies the type of the binding that will be used for metadata retrieval via HTTP GET.</span></span> <span data-ttu-id="78cca-114">這個設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="78cca-114">This setting is optional.</span></span> <span data-ttu-id="78cca-115">如果未指定這個設定，則會使用預設的繫結。</span><span class="sxs-lookup"><span data-stu-id="78cca-115">If it is not specified, the default bindings will be used.</span></span><br /><br /> <span data-ttu-id="78cca-116">只有當繫結的內部繫結項目支援 <xref:System.ServiceModel.Channels.IReplyChannel> 時，這些繫結才會受到支援。</span><span class="sxs-lookup"><span data-stu-id="78cca-116">Only bindings with inner binding elements that support <xref:System.ServiceModel.Channels.IReplyChannel> will be supported.</span></span> <span data-ttu-id="78cca-117">此外，該繫結的 <xref:System.ServiceModel.Channels.MessageVersion> 屬性 (Property) 必須是 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。</span><span class="sxs-lookup"><span data-stu-id="78cca-117">Additionally, the <xref:System.ServiceModel.Channels.MessageVersion> property of the binding must be <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.</span></span>|  
|<span data-ttu-id="78cca-118">httpGetBindingConfiguration</span><span class="sxs-lookup"><span data-stu-id="78cca-118">httpGetBindingConfiguration</span></span>|<span data-ttu-id="78cca-119">字串，這個字串會設定在 `httpGetBinding` 屬性中指定之繫結的名稱，該屬性會參考這個繫結中的其他組態資訊。</span><span class="sxs-lookup"><span data-stu-id="78cca-119">A string that sets the name of the binding that is specified in the `httpGetBinding` attribute, which references to the additional configuration information of this binding.</span></span> <span data-ttu-id="78cca-120">必須在 `<bindings>` 區段中定義相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="78cca-120">The same name must be defined in the `<bindings>` section.</span></span>|  
|<span data-ttu-id="78cca-121">httpGetEnabled</span><span class="sxs-lookup"><span data-stu-id="78cca-121">httpGetEnabled</span></span>|<span data-ttu-id="78cca-122">布林值，指定是否發行服務中繼資料以使用 HTTP/Get 要求進行擷取。</span><span class="sxs-lookup"><span data-stu-id="78cca-122">A Boolean value that specifies whether to publish service metadata for retrieval using an HTTP/Get request.</span></span> <span data-ttu-id="78cca-123">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="78cca-123">The default is `false`.</span></span><br /><br /> <span data-ttu-id="78cca-124">如果未指定 httpGetUrl 屬性，則中繼資料的發行位址會是服務位址加上 "?wsdl"。</span><span class="sxs-lookup"><span data-stu-id="78cca-124">If the httpGetUrl attribute is not specified, the address at which the metadata is published is the service address plus a "?wsdl".</span></span> <span data-ttu-id="78cca-125">例如，如果服務位址為 `http://localhost:8080/CalculatorService` ，則 HTTP/Get 中繼資料位址為 `http://localhost:8080/CalculatorService?wsdl` 。</span><span class="sxs-lookup"><span data-stu-id="78cca-125">For example, if the service address is `http://localhost:8080/CalculatorService`, the HTTP/Get metadata address is `http://localhost:8080/CalculatorService?wsdl`.</span></span><br /><br /> <span data-ttu-id="78cca-126">如果此屬性為 `false` ，或服務的位址不是以 HTTP 或 HTTPS 為基礎，則會忽略 "？ wsdl"。</span><span class="sxs-lookup"><span data-stu-id="78cca-126">If this property is `false`, or the address of the service is not based on HTTP or HTTPS, "?wsdl" is ignored.</span></span>|  
|<span data-ttu-id="78cca-127">httpGetUrl</span><span class="sxs-lookup"><span data-stu-id="78cca-127">httpGetUrl</span></span>|<span data-ttu-id="78cca-128">布林值，指定中繼資料的發行位址以使用 HTTP/Get 要求進行擷取。</span><span class="sxs-lookup"><span data-stu-id="78cca-128">A Uri that specifies the address at which the metadata is published for retrieval using an HTTP/Get request.</span></span> <span data-ttu-id="78cca-129">如果已指定相對 URI，則視為相對於服務的基底位址。</span><span class="sxs-lookup"><span data-stu-id="78cca-129">If a relative Uri is specified it will be treated as relative to the service’s base address.</span></span>|  
|<span data-ttu-id="78cca-130">httpsGetBinding</span><span class="sxs-lookup"><span data-stu-id="78cca-130">httpsGetBinding</span></span>|<span data-ttu-id="78cca-131">字串，這個字串會指定透過 HTTPS GET 擷取中繼資料所要使用之繫結的型別。</span><span class="sxs-lookup"><span data-stu-id="78cca-131">A string that specifies the type of the binding that will be used for metadata retrieval via HTTPS GET.</span></span> <span data-ttu-id="78cca-132">這個設定是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="78cca-132">This setting is optional.</span></span> <span data-ttu-id="78cca-133">如果未指定這個設定，則會使用預設的繫結。</span><span class="sxs-lookup"><span data-stu-id="78cca-133">If it is not specified, the default bindings will be used.</span></span><br /><br /> <span data-ttu-id="78cca-134">只有當繫結的內部繫結項目支援 <xref:System.ServiceModel.Channels.IReplyChannel> 時，這些繫結才會受到支援。</span><span class="sxs-lookup"><span data-stu-id="78cca-134">Only bindings with inner binding elements that support <xref:System.ServiceModel.Channels.IReplyChannel> will be supported.</span></span> <span data-ttu-id="78cca-135">此外，該繫結的 <xref:System.ServiceModel.Channels.MessageVersion> 屬性 (Property) 必須是 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。</span><span class="sxs-lookup"><span data-stu-id="78cca-135">Additionally, the <xref:System.ServiceModel.Channels.MessageVersion> property of the binding must be <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.</span></span>|  
|<span data-ttu-id="78cca-136">httpsGetBindingConfiguration</span><span class="sxs-lookup"><span data-stu-id="78cca-136">httpsGetBindingConfiguration</span></span>|<span data-ttu-id="78cca-137">字串，這個字串會設定在 `httpsGetBinding` 屬性中指定之繫結的名稱，該屬性會參考這個繫結中的其他組態資訊。</span><span class="sxs-lookup"><span data-stu-id="78cca-137">A string that sets the name of the binding that is specified in the `httpsGetBinding` attribute, which references to the additional configuration information of this binding.</span></span> <span data-ttu-id="78cca-138">必須在 `<bindings>` 區段中定義相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="78cca-138">The same name must be defined in the `<bindings>` section.</span></span>|  
|<span data-ttu-id="78cca-139">httpsGetEnabled</span><span class="sxs-lookup"><span data-stu-id="78cca-139">httpsGetEnabled</span></span>|<span data-ttu-id="78cca-140">布林值，指定是否發行服務中繼資料以使用 HTTPS/Get 要求進行擷取。</span><span class="sxs-lookup"><span data-stu-id="78cca-140">A Boolean value that specifies whether to publish service metadata for retrieval using an HTTPS/Get request.</span></span> <span data-ttu-id="78cca-141">預設值為 `false`。</span><span class="sxs-lookup"><span data-stu-id="78cca-141">The default is `false`.</span></span><br /><br /> <span data-ttu-id="78cca-142">如果未指定 httpsGetUrl 屬性，則中繼資料的發行位址會是服務位址加上 "?wsdl"。</span><span class="sxs-lookup"><span data-stu-id="78cca-142">If the httpsGetUrl attribute is not specified, the address at which the metadata is published is the service address plus a "?wsdl".</span></span> <span data-ttu-id="78cca-143">例如，如果服務位址是 " https://localhost:8080/CalculatorService "，則 HTTP/Get 中繼資料位址會是 " https://localhost:8080/CalculatorService?wsdl "。</span><span class="sxs-lookup"><span data-stu-id="78cca-143">For example, if the service address is "https://localhost:8080/CalculatorService", the HTTP/Get metadata address is "https://localhost:8080/CalculatorService?wsdl".</span></span><br /><br /> <span data-ttu-id="78cca-144">如果此屬性為 `false` ，或服務的位址不是以 HTTP 或 HTTPS 為基礎，則會忽略 "？ wsdl"。</span><span class="sxs-lookup"><span data-stu-id="78cca-144">If this property is `false`, or the address of the service is not based on HTTP or HTTPS, "?wsdl" is ignored.</span></span>|  
|<span data-ttu-id="78cca-145">httpsGetUrl</span><span class="sxs-lookup"><span data-stu-id="78cca-145">httpsGetUrl</span></span>|<span data-ttu-id="78cca-146">URI，指定中繼資料的發行位址以使用 HTTPS/Get 要求進行擷取。</span><span class="sxs-lookup"><span data-stu-id="78cca-146">A Uri that specifies the address at which the metadata is published for retrieval using an HTTPS/Get request.</span></span>|  
|<span data-ttu-id="78cca-147">policyVersion</span><span class="sxs-lookup"><span data-stu-id="78cca-147">policyVersion</span></span>|<span data-ttu-id="78cca-148">字串，指定所要使用的 WS-Policy 規格版本。</span><span class="sxs-lookup"><span data-stu-id="78cca-148">A string that specifies the version of the WS-Policy specification being used.</span></span> <span data-ttu-id="78cca-149">此屬性的型別為 <xref:System.ServiceModel.Description.PolicyVersion>。</span><span class="sxs-lookup"><span data-stu-id="78cca-149">This attribute is of type <xref:System.ServiceModel.Description.PolicyVersion>.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="78cca-150">子元素</span><span class="sxs-lookup"><span data-stu-id="78cca-150">Child Elements</span></span>  
 <span data-ttu-id="78cca-151">無</span><span class="sxs-lookup"><span data-stu-id="78cca-151">None</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="78cca-152">父項目</span><span class="sxs-lookup"><span data-stu-id="78cca-152">Parent Elements</span></span>  
  
|<span data-ttu-id="78cca-153">元素</span><span class="sxs-lookup"><span data-stu-id="78cca-153">Element</span></span>|<span data-ttu-id="78cca-154">描述</span><span class="sxs-lookup"><span data-stu-id="78cca-154">Description</span></span>|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|<span data-ttu-id="78cca-155">指定行為項目。</span><span class="sxs-lookup"><span data-stu-id="78cca-155">Specifies a behavior element.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="78cca-156">備註</span><span class="sxs-lookup"><span data-stu-id="78cca-156">Remarks</span></span>  
 <span data-ttu-id="78cca-157">這個組態項目可讓您控制服務的中繼資料發行功能。</span><span class="sxs-lookup"><span data-stu-id="78cca-157">This configuration element allows you to control the metadata publishing features of a service.</span></span> <span data-ttu-id="78cca-158">為避免不慎洩漏可能的敏感性服務中繼資料，Windows Communication Foundation （WCF）服務的預設設定會停用中繼資料發行。</span><span class="sxs-lookup"><span data-stu-id="78cca-158">To prevent unintentional disclosure of potentially sensitive service metadata, the default configuration for Windows Communication Foundation (WCF) services disables metadata publishing.</span></span> <span data-ttu-id="78cca-159">這個行為依預設為安全行為，但也表示您無法使用中繼資料匯入工具 (例如 Svcutil.exe) 來產生呼叫服務所需的用戶端程式碼，除非組態中已明確啟用服務的中繼發行行為。</span><span class="sxs-lookup"><span data-stu-id="78cca-159">This behavior is secure by default, but also means that you cannot use a metadata import tool (such as Svcutil.exe) to generate the client code required to call the service unless the service’s metadata publishing behavior is explicitly enabled in configuration.</span></span> <span data-ttu-id="78cca-160">使用這個組態項目，您就可以為服務啟用此發行行為。</span><span class="sxs-lookup"><span data-stu-id="78cca-160">Using this configuration element, you can enable this publishing behavior for your service.</span></span>  
  
 <span data-ttu-id="78cca-161">如需設定此行為的詳細範例，請參閱[中繼資料發行行為](../../../wcf/samples/metadata-publishing-behavior.md)。</span><span class="sxs-lookup"><span data-stu-id="78cca-161">For a detailed example of configuring this behavior, see [Metadata Publishing Behavior](../../../wcf/samples/metadata-publishing-behavior.md).</span></span>  
  
 <span data-ttu-id="78cca-162">選用的 `httpGetBinding` 和 `httpsGetBinding` 屬性可讓您設定透過 HTTP GET (或 HTTPS GET) 擷取中繼資料時所使用的繫結。</span><span class="sxs-lookup"><span data-stu-id="78cca-162">The optional `httpGetBinding` and `httpsGetBinding` attributes allow you to configure the bindings used for metadata retrieval via HTTP GET (or HTTPS GET).</span></span> <span data-ttu-id="78cca-163">如果未指定這些繫結，則會依適當情形，使用預設的繫結 (使用 HTTP 時為 `HttpTransportBindingElement`，使用 HTTPS 時則為 `HttpsTransportBindingElement`) 擷取中繼資料。</span><span class="sxs-lookup"><span data-stu-id="78cca-163">If they are not specified, the default bindings (`HttpTransportBindingElement`, in the case of HTTP and `HttpsTransportBindingElement`, in the case of HTTPS) are used for metadata retrieval as appropriate.</span></span> <span data-ttu-id="78cca-164">請注意，這些屬性 (Attribute) 無法搭配內建的 WCF 繫結使用。</span><span class="sxs-lookup"><span data-stu-id="78cca-164">Notice that you cannot use these attributes with the built-in WCF bindings.</span></span> <span data-ttu-id="78cca-165">只有當繫結的內部繫結項目支援 <xref:System.ServiceModel.Channels.IReplyChannel> 時，這些繫結才會受到支援。</span><span class="sxs-lookup"><span data-stu-id="78cca-165">Only bindings with inner binding elements that support <xref:System.ServiceModel.Channels.IReplyChannel> will be supported.</span></span> <span data-ttu-id="78cca-166">此外，該繫結的 <xref:System.ServiceModel.Channels.MessageVersion> 屬性 (Property) 必須是 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。</span><span class="sxs-lookup"><span data-stu-id="78cca-166">Additionally, the <xref:System.ServiceModel.Channels.MessageVersion> property of the binding must be <xref:System.ServiceModel.Channels.MessageVersion.None%2A>.</span></span>  
  
 <span data-ttu-id="78cca-167">若要降低將服務暴露給惡意使用者的機會，可以使用 SSL over HTTP (HTTPS) 機制來進行安全的傳輸。</span><span class="sxs-lookup"><span data-stu-id="78cca-167">To reduce the exposure of a service to malicious users, it is possible to secure the transfer using the SSL over HTTP (HTTPS) mechanism.</span></span> <span data-ttu-id="78cca-168">若要這麼做，您必須先將適當的 X.509 憑證，繫結至裝載服務之電腦上的特定連接埠 </span><span class="sxs-lookup"><span data-stu-id="78cca-168">To do so, you must first bind a suitable X.509 certificate to a specific port on the computer that is hosting the service.</span></span> <span data-ttu-id="78cca-169">（如需詳細資訊，請參閱[使用憑證](../../../wcf/feature-details/working-with-certificates.md)）。其次，將這個專案加入至服務設定，並將 `httpsGetEnabled` 屬性設為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="78cca-169">(For more information, see [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md).) Second, add this element to the service configuration and set the `httpsGetEnabled` attribute to `true`.</span></span> <span data-ttu-id="78cca-170">最後，將 `httpsGetUrl` 屬性設定為服務中繼資料端點的 URL，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="78cca-170">Finally, set the `httpsGetUrl` attribute to the URL of the service metadata endpoint, as shown in the following example.</span></span>  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="NewBehavior">
      <serviceMetadata httpsGetEnabled="true"
                       httpsGetUrl="https://myComputerName/myEndpoint" />
    </behavior>
  </serviceBehaviors>
</behaviors>
```  
  
## <a name="example"></a><span data-ttu-id="78cca-171">範例</span><span class="sxs-lookup"><span data-stu-id="78cca-171">Example</span></span>  
 <span data-ttu-id="78cca-172">下列範例會使用專案來設定服務，以公開中繼資料 \<serviceMetadata> 。</span><span class="sxs-lookup"><span data-stu-id="78cca-172">The following example configure a service to expose metadata by using the \<serviceMetadata> element.</span></span> <span data-ttu-id="78cca-173">它也設定了一個端點，將 `IMetadataExchange` 合約公開做為 WS-MetadataExchange (MEX) 通訊協定的實作。</span><span class="sxs-lookup"><span data-stu-id="78cca-173">It also configures an endpoint to expose the `IMetadataExchange` contract as an implementation of a WS-MetadataExchange (MEX) protocol.</span></span> <span data-ttu-id="78cca-174">此範例使用 `mexHttpBinding`，這個方便的標準繫結，相當於將安全性模式設定為 `wsHttpBinding` 的 `None`。</span><span class="sxs-lookup"><span data-stu-id="78cca-174">The example uses the `mexHttpBinding`, which is a convenience standard binding that is equivalent to the `wsHttpBinding` with the security mode set to `None`.</span></span> <span data-ttu-id="78cca-175">端點中會使用「mex」的相對位址，當針對服務基底位址進行解析時，會產生的端點位址 `http://localhost/servicemodelsamples/service.svc/mex` 。</span><span class="sxs-lookup"><span data-stu-id="78cca-175">A relative address of "mex" is used in the endpoint, which when resolved against the services base address results in an endpoint address of `http://localhost/servicemodelsamples/service.svc/mex`.</span></span>  
  
```xml  
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc -->
        <endpoint address=""
                  binding="wsHttpBinding"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex
             To expose the IMetadataExchange contract, you must enable the serviceMetadata behavior as demonstrated below. -->
        <endpoint address="mex"
                  binding="mexHttpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <!-- The serviceMetadata behavior publishes metadata through the IMetadataExchange contract. When this behavior is
               present, you can expose this contract through an endpoint as shown above. Setting httpGetEnabled to true publishes
               the service's WSDL at the <baseaddress>?wsdl eg. http://localhost/servicemodelsamples/service.svc?wsdl -->
          <serviceMetadata httpGetEnabled="True" />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a><span data-ttu-id="78cca-176">另請參閱</span><span class="sxs-lookup"><span data-stu-id="78cca-176">See also</span></span>

- <xref:System.ServiceModel.Configuration.ServiceMetadataPublishingElement>
- <xref:System.ServiceModel.Description.ServiceMetadataBehavior>
- [<span data-ttu-id="78cca-177">安全性行為</span><span class="sxs-lookup"><span data-stu-id="78cca-177">Security Behaviors</span></span>](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [<span data-ttu-id="78cca-178">中繼資料發行行為</span><span class="sxs-lookup"><span data-stu-id="78cca-178">Metadata Publishing Behavior</span></span>](../../../wcf/samples/metadata-publishing-behavior.md)
