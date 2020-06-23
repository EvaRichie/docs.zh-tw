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
# <a name="using-systemtransactions-in-aspnet"></a>在 ASP.NET 中使用 System.Transactions
本主題說明如何成功運用 ASP.NET 應用程式中的 <xref:System.Transactions>。

## <a name="enable-distributedtransactionpermission-in-aspnet"></a>啟用 ASP.NET 中的 DistributedTransactionPermission
 <xref:System.Transactions>支援部分信任的呼叫端，並且以 `AllowPartiallyTrustedCallers` 屬性（APTCA）標記。 的信任層級 <xref:System.Transactions> 是根據所公開的資源類型（例如系統記憶體、共用的整個進程資源、全系統資源和其他資源）來定義， <xref:System.Transactions> 而這些資源是用來存取這些資源所需的信任層級。 在部分信任的環境中，非完整信任組件只能使用應用程式定義域內的交易 (在此情況下，系統記憶體是唯一受保護的資源)，除非它被授予了 <xref:System.Transactions.DistributedTransactionPermission>。

 每當交易的管理擴大至需由「Microsoft 分散式交易協調器」(MSDTC) 管理的情況時，就會要求<xref:System.Transactions.DistributedTransactionPermission> 。 這種情況會使用整個處理序的資源，特別是全域資源 (亦即在 MSDTC 記錄中保留的空格)。 資料庫的 Web 前端或是將資料庫當成所提供的服務一部分來使用的應用程式，都是這類用法的例子。

 ASP.NET 擁有專屬的信任層級，並透過原則檔將這些信任層級關聯至特定的權限。 如需詳細資訊，請參閱[ASP.NET 信任層級和原則](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))檔案。 當您一開始安裝 Windows SDK 時，不會有任何預設的 ASP.NET 原則檔案與相關聯 <xref:System.Transactions.DistributedTransactionPermission> 。 因此，當 ASP.NET 應用程式中的交易規模擴大至需由 MSDTC 管理時，在要求 <xref:System.Security.SecurityException> 時，擴大規模會失敗，並傳回 <xref:System.Transactions.DistributedTransactionPermission>。 若要在 ASP.NET 部分信任環境中啟用交易擴大規模，您應該在同一個預設信任層級中授予 <xref:System.Transactions.DistributedTransactionPermission> 權限 (與在 <xref:System.Data.SqlClient.SqlClientPermission> 中所授予的權限一樣)。 您可以選擇設定自訂的信任層級與原則檔來支援這項作業，或者也可以修改預設的原則檔，亦即 **Web_hightrust.config** 和 **Web_mediumtrust.config**。

 若要修改原則檔，請將的專案加入專案底下的專案中， `SecurityClass` `DistributedTransactionPermission` `SecurityClasses` `PolicyLevel` 並在 ASP.NET 的下新增對應的 `IPermission` 元素 `NamedPermissionSet` 。 下列組態檔示範如何進行。

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

 如需 ASP.NET 安全性原則的詳細資訊，請參閱[SecurityPolicy 元素（ASP.NET 設定架構）](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))。

## <a name="dynamic-compilation"></a>動態編譯
 如果您希望匯入並使用 ASP.NET 應用程式中的 <xref:System.Transactions> (在存取時動態編譯)，您可以在組態檔中放置 <xref:System.Transactions> 組件的參考。 具體而言，您應該將參考加入 `compilation/assemblies` 預設根**Web.config**設定檔的區段下，或是特定 Web 應用程式的設定檔。 下列範例示範此作業。

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

 如需詳細資訊，請參閱[針對編譯的元件加入元素（ASP.NET 設定架構）](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100))。

## <a name="see-also"></a>另請參閱

- [ASP.NET Trust Levels and Policy Files](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))
- [securityPolicy 項目 (ASP.NET 設定結構描述)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))
- [交易管理擴大規模](transaction-management-escalation.md)
