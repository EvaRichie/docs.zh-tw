---
title: 在 ASP.NET 中使用 System.Transactions
description: 在 ASP.NET 應用程式內使用 System.object。 啟用分散式交易許可權，並使用動態編譯。
ms.date: 03/30/2017
ms.assetid: 1982c300-7ea6-4242-95ed-dc28ccfacac9
ms.openlocfilehash: 48907faf99953e34d045a1e0d79eed8a788187b5
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141640"
---
# <a name="using-systemtransactions-in-aspnet"></a><span data-ttu-id="71ba5-104">在 ASP.NET 中使用 System.Transactions</span><span class="sxs-lookup"><span data-stu-id="71ba5-104">Using System.Transactions in ASP.NET</span></span>
<span data-ttu-id="71ba5-105">本主題說明如何成功運用 ASP.NET 應用程式中的 <xref:System.Transactions>。</span><span class="sxs-lookup"><span data-stu-id="71ba5-105">This topic describes how you can successfully use <xref:System.Transactions> inside an ASP.NET application.</span></span>

## <a name="enable-distributedtransactionpermission-in-aspnet"></a><span data-ttu-id="71ba5-106">啟用 ASP.NET 中的 DistributedTransactionPermission</span><span class="sxs-lookup"><span data-stu-id="71ba5-106">Enable DistributedTransactionPermission in ASP.NET</span></span>
 <span data-ttu-id="71ba5-107"><xref:System.Transactions>支援部分信任的呼叫端，並且以 `AllowPartiallyTrustedCallers` 屬性（APTCA）標記。</span><span class="sxs-lookup"><span data-stu-id="71ba5-107"><xref:System.Transactions> supports partially trusted callers and is marked with the `AllowPartiallyTrustedCallers` attribute (APTCA).</span></span> <span data-ttu-id="71ba5-108">的信任層級 <xref:System.Transactions> 是根據所公開的資源類型（例如系統記憶體、共用的整個進程資源、全系統資源和其他資源）來定義， <xref:System.Transactions> 而這些資源是用來存取這些資源所需的信任層級。</span><span class="sxs-lookup"><span data-stu-id="71ba5-108">The trust levels for <xref:System.Transactions> are defined based on the types of resources (for example, system memory, shared process-wide resources, system-wide resources, and other resources) that <xref:System.Transactions> exposes and the level of trust that should be required to access those resources.</span></span> <span data-ttu-id="71ba5-109">在部分信任的環境中，非完整信任組件只能使用應用程式定義域內的交易 (在此情況下，系統記憶體是唯一受保護的資源)，除非它被授予了 <xref:System.Transactions.DistributedTransactionPermission>。</span><span class="sxs-lookup"><span data-stu-id="71ba5-109">In a partial-trust environment, a non-full trust assembly can only use transactions within the Application Domain (in this case, the only resource being protected is system memory), unless it is granted the <xref:System.Transactions.DistributedTransactionPermission>.</span></span>

 <span data-ttu-id="71ba5-110">每當交易的管理擴大至需由「Microsoft 分散式交易協調器」(MSDTC) 管理的情況時，就會要求<xref:System.Transactions.DistributedTransactionPermission> 。</span><span class="sxs-lookup"><span data-stu-id="71ba5-110"><xref:System.Transactions.DistributedTransactionPermission> is demanded whenever transaction management is escalated to be managed by the Microsoft Distributed Transaction Coordinator (MSDTC).</span></span> <span data-ttu-id="71ba5-111">這種情況會使用整個處理序的資源，特別是全域資源 (亦即在 MSDTC 記錄中保留的空格)。</span><span class="sxs-lookup"><span data-stu-id="71ba5-111">This kind of scenario utilizes process-wide resources and particularly a global resource, which is the reserved space in the MSDTC log.</span></span> <span data-ttu-id="71ba5-112">資料庫的 Web 前端或是將資料庫當成所提供的服務一部分來使用的應用程式，都是這類用法的例子。</span><span class="sxs-lookup"><span data-stu-id="71ba5-112">An example of this usage is a Web front-end to a database or an application that uses a database as part of the services it provides.</span></span>

 <span data-ttu-id="71ba5-113">ASP.NET 擁有專屬的信任層級，並透過原則檔將這些信任層級關聯至特定的權限。</span><span class="sxs-lookup"><span data-stu-id="71ba5-113">ASP.NET has its own set of trust levels and associates a specific set of permissions with these trust levels through policy files.</span></span> <span data-ttu-id="71ba5-114">如需詳細資訊，請參閱[ASP.NET 信任層級和原則](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))檔案。</span><span class="sxs-lookup"><span data-stu-id="71ba5-114">For more information, see [ASP.NET Trust Levels and Policy Files](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100)).</span></span> <span data-ttu-id="71ba5-115">當您一開始安裝 Windows SDK 時，不會有任何預設的 ASP.NET 原則檔案與相關聯 <xref:System.Transactions.DistributedTransactionPermission> 。</span><span class="sxs-lookup"><span data-stu-id="71ba5-115">When you initially install the Windows SDK, none of the default ASP.NET policy files are associated with the <xref:System.Transactions.DistributedTransactionPermission>.</span></span> <span data-ttu-id="71ba5-116">因此，當 ASP.NET 應用程式中的交易規模擴大至需由 MSDTC 管理時，在要求 <xref:System.Security.SecurityException> 時，擴大規模會失敗，並傳回 <xref:System.Transactions.DistributedTransactionPermission>。</span><span class="sxs-lookup"><span data-stu-id="71ba5-116">As such, when your transaction in an ASP.NET application is escalated to be managed by the MSDTC, the escalation fails with a <xref:System.Security.SecurityException> upon demanding the <xref:System.Transactions.DistributedTransactionPermission>.</span></span> <span data-ttu-id="71ba5-117">若要在 ASP.NET 部分信任環境中啟用交易擴大規模，您應該在同一個預設信任層級中授予 <xref:System.Transactions.DistributedTransactionPermission> 權限 (與在 <xref:System.Data.SqlClient.SqlClientPermission> 中所授予的權限一樣)。</span><span class="sxs-lookup"><span data-stu-id="71ba5-117">To enable transaction escalation in an ASP.NET partial trust environment, you should grant the <xref:System.Transactions.DistributedTransactionPermission> in the same default trust levels as those of <xref:System.Data.SqlClient.SqlClientPermission>.</span></span> <span data-ttu-id="71ba5-118">您可以選擇設定自訂的信任層級與原則檔來支援這項作業，或者也可以修改預設的原則檔，亦即 **Web_hightrust.config** 和 **Web_mediumtrust.config**。</span><span class="sxs-lookup"><span data-stu-id="71ba5-118">You can either configure your own custom trust level and policy file to support this, or you can modify the default policy files, which are **Web_hightrust.config** and **Web_mediumtrust.config**.</span></span>

 <span data-ttu-id="71ba5-119">若要修改原則檔，請將的專案加入專案底下的專案中， `SecurityClass` `DistributedTransactionPermission` `SecurityClasses` `PolicyLevel` 並在 ASP.NET 的下新增對應的 `IPermission` 元素 `NamedPermissionSet` 。</span><span class="sxs-lookup"><span data-stu-id="71ba5-119">To modify the policy files, add a `SecurityClass` element for `DistributedTransactionPermission` to the `SecurityClasses` element under the `PolicyLevel` element and add a corresponding `IPermission` element under the ASP.NET `NamedPermissionSet` for System.Transactions.</span></span> <span data-ttu-id="71ba5-120">下列組態檔示範如何進行。</span><span class="sxs-lookup"><span data-stu-id="71ba5-120">The following configuration file demonstrates this.</span></span>

```xml
<SecurityClasses>
   <SecurityClass Name="DistributedTransactionPermission" Description="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
...
</SecurityClasses>

<PermissionSet
  class="NamedPermissionSet"
  version="1"
  Name="ASP.Net">
     <IPermission
        class="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"
        version="1"
        Unrestricted="true"
     />
...
</PermissionSet>
```

 <span data-ttu-id="71ba5-121">如需 ASP.NET 安全性原則的詳細資訊，請參閱[SecurityPolicy 元素（ASP.NET 設定架構）](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="71ba5-121">For more information about ASP.NET security policy, see [securityPolicy Element (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100)).</span></span>

## <a name="dynamic-compilation"></a><span data-ttu-id="71ba5-122">動態編譯</span><span class="sxs-lookup"><span data-stu-id="71ba5-122">Dynamic Compilation</span></span>
 <span data-ttu-id="71ba5-123">如果您希望匯入並使用 ASP.NET 應用程式中的 <xref:System.Transactions> (在存取時動態編譯)，您可以在組態檔中放置 <xref:System.Transactions> 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="71ba5-123">If you want to import and use <xref:System.Transactions> in an ASP.NET application that is dynamically compiled on access, you should place a reference to the <xref:System.Transactions> assembly in the configuration file.</span></span> <span data-ttu-id="71ba5-124">具體而言，您應該將參考加入 `compilation/assemblies` 預設根**Web.config**設定檔的區段下，或是特定 Web 應用程式的設定檔。</span><span class="sxs-lookup"><span data-stu-id="71ba5-124">Specifically, the reference should be added under the `compilation/assemblies` section of the default root **Web.config** configuration file, or a specific Web application's configuration file.</span></span> <span data-ttu-id="71ba5-125">下列範例示範此作業。</span><span class="sxs-lookup"><span data-stu-id="71ba5-125">The following example demonstrates this.</span></span>

```xml
<configuration>
   <system.web>
      <compilation>
         <assemblies>
      <add assembly="System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
         </assemblies>
      </compilation>
   </system.web>
</configuration>
```

 <span data-ttu-id="71ba5-126">如需詳細資訊，請參閱[針對編譯的元件加入元素（ASP.NET 設定架構）](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="71ba5-126">For more information, see [add Element for assemblies for compilation (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100)).</span></span>

## <a name="see-also"></a><span data-ttu-id="71ba5-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="71ba5-127">See also</span></span>

- <span data-ttu-id="71ba5-128">[ASP.NET Trust Levels and Policy Files](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="71ba5-128">[ASP.NET Trust Levels and Policy Files](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))</span></span>
- <span data-ttu-id="71ba5-129">[securityPolicy 項目 (ASP.NET 設定結構描述)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="71ba5-129">[securityPolicy Element (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))</span></span>
- [<span data-ttu-id="71ba5-130">交易管理擴大規模</span><span class="sxs-lookup"><span data-stu-id="71ba5-130">Transaction Management Escalation</span></span>](transaction-management-escalation.md)
