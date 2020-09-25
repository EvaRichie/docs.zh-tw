---
title: <behaviorExtensions>
ms.date: 03/30/2017
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
ms.openlocfilehash: 27bf9e380df1586b42cbe96a628a794364fae743
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204966"
---
# \<behaviorExtensions>

<span data-ttu-id="f6fdf-101">行為延伸可讓使用者建立使用者定義的行為項目。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-101">Behavior extensions enable the user to create user-defined behavior elements.</span></span> <span data-ttu-id="f6fdf-102">這些項目可以和標準的 Windows Communication Foundation (WCF) 行為項目並列使用。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-102">These elements can be used alongside the standard Windows Communication Foundation (WCF) behavior elements.</span></span> <span data-ttu-id="f6fdf-103">`behaviorExtensions` 區段會定義項目，讓項目可用於組態中。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-103">The `behaviorExtensions` section defines the element such that it can be used in configuration.</span></span> <span data-ttu-id="f6fdf-104">以下是典型行為擴充的範例。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-104">Here is an example of a typical behavior extension.</span></span>  
  
```xml  
<system.serviceModel>
  <extensions>
    <behaviorExtensions>
      <add name="myBehavior"
           type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
                 Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    </behaviorExtensions>
  </extensions>
</system.serviceModel>
```  
  
 <span data-ttu-id="f6fdf-105">若要將組態功能加入至項目，您必須寫入並註冊組態項目。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-105">To add configuration abilities to the element, you need to write and register a configuration element.</span></span> <span data-ttu-id="f6fdf-106">如需這方面的詳細資訊，請參閱 <xref:System.Configuration>。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-106">For more information on this, see the <xref:System.Configuration> documentation.</span></span>  
  
 <span data-ttu-id="f6fdf-107">在定義項目及其組態型別後，即可使用擴充，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-107">After the element and its configuration type are defined, the extension can be used, as shown in the following example.</span></span>  
  
```xml  
<behaviors>
  <behavior configurationName="testChannelBehavior">
    <myBehavior />
    <channelSecurity cacheCookies="false"
                     detectReplays="false"
                     maxCachedNonces="9"
                     maxClockSkew="00:00:03"
                     maxCookieCachingTime="00:07:24"
                     replayWindow="00:07:22.2190000" />
  </behavior>
</behaviors>
```  
  
## <a name="security"></a><span data-ttu-id="f6fdf-108">安全性</span><span class="sxs-lookup"><span data-stu-id="f6fdf-108">Security</span></span>  

 <span data-ttu-id="f6fdf-109">強烈建議您在 `machine.config` 和 `app.config` 檔案中註冊型別時，使用完整組件名稱。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-109">It is strongly recommended that you use fully qualified assembly names when registering types in the `machine.config` and `app.config` files.</span></span> <span data-ttu-id="f6fdf-110">如果型別不是唯一定義的型別，則 CLR 型別載入器會以指定的順序在以下位置中搜尋該型別：</span><span class="sxs-lookup"><span data-stu-id="f6fdf-110">If the type is not uniquely defined, the CLR type loader searches for it in the following locations in the specified order:</span></span>  
  
 <span data-ttu-id="f6fdf-111">如果型別的組件為已知，則載入器會搜尋組態檔案的重新導向位置、GAC、使用組態資訊的目前組件，和應用程式基底目錄。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-111">If the assembly of the type is known, the loader searches the configuration file's redirect locations, GAC, the current assembly using configuration information, and the application base directory.</span></span> <span data-ttu-id="f6fdf-112">如果組件為未知，則載入器會搜尋目前組件、mscorlib 和 `TypeResolve` 事件處理常式傳回的位置。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-112">If the assembly is unknown, the loader searches the current assembly, mscorlib, and the location returned by the `TypeResolve` event handler.</span></span> <span data-ttu-id="f6fdf-113">這個 CLR 搜尋順序可以用型別轉送機制和 AppDomain.TypeResolve 事件等攔截程序 (Hook) 來修改。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-113">This CLR search order can be modified with hooks such as the Type Forwarding mechanism and the AppDomain.TypeResolve event.</span></span>  
  
 <span data-ttu-id="f6fdf-114">攻擊者可能會利用 CLR 搜尋順序並執行未經授權的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-114">An attacker can exploit the CLR search order and execute unauthorized code.</span></span> <span data-ttu-id="f6fdf-115">使用完整 (強式) 名稱來唯一識別類型，可進一步提高您系統的安全性。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-115">Using fully qualified (strong) names uniquely identifies a type and further increases security of your system.</span></span>  
  
 <span data-ttu-id="f6fdf-116">如需詳細資訊，請參閱 [執行時間如何找出元件](../../../deployment/how-the-runtime-locates-assemblies.md) 和 <xref:System.AppDomain.TypeResolve> 。</span><span class="sxs-lookup"><span data-stu-id="f6fdf-116">For more information, see [How the Runtime Locates Assemblies](../../../deployment/how-the-runtime-locates-assemblies.md) and <xref:System.AppDomain.TypeResolve>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f6fdf-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f6fdf-117">See also</span></span>

- <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>
- [<span data-ttu-id="f6fdf-118">使用行為來設定與擴充執行階段</span><span class="sxs-lookup"><span data-stu-id="f6fdf-118">Configuring and Extending the Runtime with Behaviors</span></span>](../../../wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)
