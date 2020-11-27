---
title: 作法：建立自訂授權原則
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 05b0549b-882d-4660-b6f0-5678543e5475
ms.openlocfilehash: fef7aa531c946ecacef30bb79f2362bad4d375ed
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256023"
---
# <a name="how-to-create-a-custom-authorization-policy"></a><span data-ttu-id="70d1d-102">作法：建立自訂授權原則</span><span class="sxs-lookup"><span data-stu-id="70d1d-102">How to: Create a Custom Authorization Policy</span></span>

<span data-ttu-id="70d1d-103">Windows Communication Foundation 中 (WCF) 的身分識別模型基礎結構支援以宣告為基礎的授權模型。</span><span class="sxs-lookup"><span data-stu-id="70d1d-103">The Identity Model infrastructure in Windows Communication Foundation (WCF) supports a claim-based authorization model.</span></span> <span data-ttu-id="70d1d-104">宣告會從權杖擷取出來 (可以選擇性地由自訂授權原則進行處理)，接著會放置到可隨後進行檢查以做出授權決策的 <xref:System.IdentityModel.Policy.AuthorizationContext>。</span><span class="sxs-lookup"><span data-stu-id="70d1d-104">Claims are extracted from tokens, optionally processed by custom authorization policy, and then placed into an <xref:System.IdentityModel.Policy.AuthorizationContext> that can then be examined to make authorization decisions.</span></span> <span data-ttu-id="70d1d-105">自訂原則可用於將來自傳入權杖的宣告轉換為應用程式所需要的宣告。</span><span class="sxs-lookup"><span data-stu-id="70d1d-105">A custom policy can be used to transform claims from incoming tokens into claims expected by the application.</span></span> <span data-ttu-id="70d1d-106">如此一來，應用層就可以與 WCF 支援的不同權杖類型所服務之不同宣告的詳細資料分開。</span><span class="sxs-lookup"><span data-stu-id="70d1d-106">In this way, the application layer can be insulated from the details on the differing claims served up by the different token types that WCF supports.</span></span> <span data-ttu-id="70d1d-107">本主題會說明如何實作自訂授權原則，以及如何將該原則新增至服務所使用的原則集合。</span><span class="sxs-lookup"><span data-stu-id="70d1d-107">This topic shows how to implement a custom authorization policy and how to add that policy to the collection of policies used by a service.</span></span>  
  
### <a name="to-implement-a-custom-authorization-policy"></a><span data-ttu-id="70d1d-108">實作自訂授權原則</span><span class="sxs-lookup"><span data-stu-id="70d1d-108">To implement a custom authorization policy</span></span>  
  
1. <span data-ttu-id="70d1d-109">定義衍生自 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 的新類別。</span><span class="sxs-lookup"><span data-stu-id="70d1d-109">Define a new class that derives from <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.</span></span>  
  
2. <span data-ttu-id="70d1d-110">透過在類別的建構函式 (Constructor) 中產生唯一字串，並在每次存取該屬性時傳回該字串，便可實作唯讀的 <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="70d1d-110">Implement the read-only <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> property by generating a unique string in the constructor for the class and returning that string whenever the property is accessed.</span></span>  
  
3. <span data-ttu-id="70d1d-111">透過傳回表示原則簽發者的 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A>，便可實作唯讀的 <xref:System.IdentityModel.Claims.ClaimSet> 屬性。</span><span class="sxs-lookup"><span data-stu-id="70d1d-111">Implement the read-only <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> property by returning a <xref:System.IdentityModel.Claims.ClaimSet> that represents the policy issuer.</span></span> <span data-ttu-id="70d1d-112">這可能是表示應用程式的 `ClaimSet` 或內建的 `ClaimSet` (例如，由靜態 `ClaimSet` 屬性傳回的 <xref:System.IdentityModel.Claims.ClaimSet.System%2A>)。</span><span class="sxs-lookup"><span data-stu-id="70d1d-112">This could be a `ClaimSet` that represents the application or a built-in `ClaimSet` (for example, the `ClaimSet` returned by the static <xref:System.IdentityModel.Claims.ClaimSet.System%2A> property.</span></span>  
  
4. <span data-ttu-id="70d1d-113">實作 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法，如下列程序所述。</span><span class="sxs-lookup"><span data-stu-id="70d1d-113">Implement the <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> method as described in the following procedure.</span></span>  
  
### <a name="to-implement-the-evaluate-method"></a><span data-ttu-id="70d1d-114">實作 Evaluate 方法</span><span class="sxs-lookup"><span data-stu-id="70d1d-114">To implement the Evaluate method</span></span>  
  
1. <span data-ttu-id="70d1d-115">有兩個參數會傳遞至這個方法：即 <xref:System.IdentityModel.Policy.EvaluationContext> 類別的執行個體，以及某個物件參考。</span><span class="sxs-lookup"><span data-stu-id="70d1d-115">Two parameters are passed to this method: an instance of the <xref:System.IdentityModel.Policy.EvaluationContext> class and an object reference.</span></span>  
  
2. <span data-ttu-id="70d1d-116">如果自訂授權原則 <xref:System.IdentityModel.Claims.ClaimSet> 會新增實例，而不考慮目前的內容 <xref:System.IdentityModel.Policy.EvaluationContext> ，則請 `ClaimSet` 呼叫 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 方法並 `true` 從方法傳回來新增每個實例 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> 。</span><span class="sxs-lookup"><span data-stu-id="70d1d-116">If the custom authorization policy adds <xref:System.IdentityModel.Claims.ClaimSet> instances without regard to the current content of the <xref:System.IdentityModel.Policy.EvaluationContext>, then add each `ClaimSet` by calling the <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> method and return `true` from the <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> method.</span></span> <span data-ttu-id="70d1d-117">傳回 `true`，就是向授權基礎結構表示該授權原則已執行其工作，因此不需要重新呼叫。</span><span class="sxs-lookup"><span data-stu-id="70d1d-117">Returning `true` indicates to the authorization infrastructure that the authorization policy has performed its work and does not need to be called again.</span></span>  
  
3. <span data-ttu-id="70d1d-118">如果自訂授權原則只會在 `EvaluationContext` 中已出現某些宣告時新增宣告集，則請檢查 `ClaimSet` 屬性所傳回的 <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A> 執行個體來查看這些宣告。</span><span class="sxs-lookup"><span data-stu-id="70d1d-118">If the custom authorization policy adds claim sets only if certain claims are already present in the `EvaluationContext`, then look for those claims by examining the `ClaimSet` instances returned by the <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A> property.</span></span> <span data-ttu-id="70d1d-119">如果這些宣告有存在，則呼叫 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 方法來新增新的宣告集，如果沒有要新增其他宣告集，則傳回 `true`，向授權基礎結構表示授權原則已完成其工作。</span><span class="sxs-lookup"><span data-stu-id="70d1d-119">If the claims are present, then add the new claim sets by calling the <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> method and, if no more claim sets are to be added, return `true`, indicating to the authorization infrastructure that the authorization policy has completed its work.</span></span> <span data-ttu-id="70d1d-120">如果沒有存在這些宣告，則傳回 `false`，表示如果有其他授權原則要新增更多宣告集至 `EvaluationContext`，就應該重新呼叫授權原則。</span><span class="sxs-lookup"><span data-stu-id="70d1d-120">If the claims are not present, return `false`, indicating that the authorization policy should be called again if other authorization policies add more claim sets to the `EvaluationContext`.</span></span>  
  
4. <span data-ttu-id="70d1d-121">在更複雜的處理案例中，<xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法的第二個參數可用來儲存狀態變數，也就是授權基礎結構後來要進行特定評估而呼叫 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法時所傳回的變數。</span><span class="sxs-lookup"><span data-stu-id="70d1d-121">In more complex processing scenarios, the second parameter of the <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> method is used to store a state variable that the authorization infrastructure will pass back during each subsequent call to the <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> method for a particular evaluation.</span></span>  
  
### <a name="to-specify-a-custom-authorization-policy-through-configuration"></a><span data-ttu-id="70d1d-122">透過組態指定自訂授權原則</span><span class="sxs-lookup"><span data-stu-id="70d1d-122">To specify a custom authorization policy through configuration</span></span>  
  
1. <span data-ttu-id="70d1d-123">在 `policyType` 項目之 `add` 項目的 `authorizationPolicies` 項目的 `serviceAuthorization` 屬性中，指定自訂授權原則的類型。</span><span class="sxs-lookup"><span data-stu-id="70d1d-123">Specify the type of the custom authorization policy in the `policyType` attribute in the `add` element in the `authorizationPolicies` element in the `serviceAuthorization` element.</span></span>  
  
    ```xml  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
        <serviceAuthorization serviceAuthorizationManagerType=  
                  "Samples.MyServiceAuthorizationManager" >  
          <authorizationPolicies>  
            <add policyType="Samples.MyAuthorizationPolicy" />  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
### <a name="to-specify-a-custom-authorization-policy-through-code"></a><span data-ttu-id="70d1d-124">透過程式碼指定自訂授權原則</span><span class="sxs-lookup"><span data-stu-id="70d1d-124">To specify a custom authorization policy through code</span></span>  
  
1. <span data-ttu-id="70d1d-125">建立 <xref:System.Collections.Generic.List%601> 的 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>。</span><span class="sxs-lookup"><span data-stu-id="70d1d-125">Create a <xref:System.Collections.Generic.List%601> of <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.</span></span>  
  
2. <span data-ttu-id="70d1d-126">建立自訂授權原則的執行個體。</span><span class="sxs-lookup"><span data-stu-id="70d1d-126">Create an instance of the custom authorization policy.</span></span>  
  
3. <span data-ttu-id="70d1d-127">新增授權原則執行個體至清單中。</span><span class="sxs-lookup"><span data-stu-id="70d1d-127">Add the authorization policy instance to the list.</span></span>  
  
4. <span data-ttu-id="70d1d-128">針對每個自訂授權原則重複步驟 2 和 3。</span><span class="sxs-lookup"><span data-stu-id="70d1d-128">Repeat steps 2 and 3 for each custom authorization policy.</span></span>  
  
5. <span data-ttu-id="70d1d-129">指派唯讀的清單版本至 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="70d1d-129">Assign a read-only version of the list to the <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A> property.</span></span>  
  
     [!code-csharp[c_CustomAuthPol#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#8)]
     [!code-vb[c_CustomAuthPol#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#8)]  
  
## <a name="example"></a><span data-ttu-id="70d1d-130">範例</span><span class="sxs-lookup"><span data-stu-id="70d1d-130">Example</span></span>  

 <span data-ttu-id="70d1d-131">下列範例會示範完整的 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 實作。</span><span class="sxs-lookup"><span data-stu-id="70d1d-131">The following example shows a complete <xref:System.IdentityModel.Policy.IAuthorizationPolicy> implementation.</span></span>  
  
 [!code-csharp[c_CustomAuthPol#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#5)]
 [!code-vb[c_CustomAuthPol#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#5)]  
  
## <a name="see-also"></a><span data-ttu-id="70d1d-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70d1d-132">See also</span></span>

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [<span data-ttu-id="70d1d-133">作法：比較宣告</span><span class="sxs-lookup"><span data-stu-id="70d1d-133">How to: Compare Claims</span></span>](how-to-compare-claims.md)
- [<span data-ttu-id="70d1d-134">作法：為服務建立自訂授權管理員</span><span class="sxs-lookup"><span data-stu-id="70d1d-134">How to: Create a Custom Authorization Manager for a Service</span></span>](how-to-create-a-custom-authorization-manager-for-a-service.md)
- [<span data-ttu-id="70d1d-135">授權原則</span><span class="sxs-lookup"><span data-stu-id="70d1d-135">Authorization Policy</span></span>](../samples/authorization-policy.md)
