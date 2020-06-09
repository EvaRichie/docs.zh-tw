---
title: 端點：位址、繫結和合約
ms.date: 03/30/2017
helpviewer_keywords:
- endpoints [WCF]
- Windows Communication Foundation [WCF], endpoints
- WCF [WCF], endpoints
ms.assetid: 9ddc46ee-1883-4291-9926-28848c57e858
ms.openlocfilehash: 3ac7f0b165b99a1ed3702628958f7d4c7702f5b1
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593512"
---
# <a name="endpoints-addresses-bindings-and-contracts"></a>端點：位址、繫結和合約

所有與 Windows Communication Foundation （WCF）服務的通訊都是透過服務的*端點*進行。 端點可讓用戶端存取 WCF 服務所提供的功能。

端點包含四項屬性：

- 指出可在何處找到端點的位址。

- 指定用戶端可以如何與端點通訊的繫結。

- 識別可用作業的合約。

- 指定本機端點實作細節的行為集。

本主題討論此端點結構，並說明如何在 WCF 物件模型中表示它。

## <a name="the-structure-of-an-endpoint"></a>端點結構

每個端點都包含下列項目：

- 位址：位址會唯一識別端點並告訴潛在取用者服務的位置。 它在 WCF 物件模型中是由類別表示 <xref:System.ServiceModel.EndpointAddress> 。 <xref:System.ServiceModel.EndpointAddress> 類別包含：

  - <xref:System.ServiceModel.EndpointAddress.Uri%2A> 屬性，用來代表服務位址。

  - <xref:System.ServiceModel.EndpointAddress.Identity%2A> 屬性，用來代表服務的安全性身分識別以及一群選用的訊息標頭集合。 選用訊息標頭會用來提供其他更詳細的定址資訊來識別端點或與端點互動。

  如需詳細資訊，請參閱[指定端點位址](../specifying-an-endpoint-address.md)。

- 繫結：繫結會指定與端點的通訊方式。 包括：

  - 要使用的傳輸通訊協定 (例如，TCP 或 HTTP)。

  - 訊息使用的編碼 (例如，文字或二進位)。

  - 必要的安全性需求 (例如，SSL 或 SOAP 訊息安全性)。

  如需詳細資訊，請參閱 WCF 系結[總覽](../bindings-overview.md)。 系結在 WCF 物件模型中是以抽象基類來表示 <xref:System.ServiceModel.Channels.Binding> 。 在大部分情況中，使用者可以使用下列其中一種系統提供的繫結。 如需詳細資訊，請參閱[系統提供的](../system-provided-bindings.md)系結。

- 合約：合約會概略說明端點公開哪些功能給用戶端。 合約會指定：

  - 用戶端可以呼叫的作業。

  - 訊息格式。

  - 呼叫作業所需的輸入參數或資料型別。

  - 用戶端可以期待收到的處理或回應訊息型別。

  如需定義合約的詳細資訊，請參閱[設計服務合約](../designing-service-contracts.md)。

- 行為：您可以使用端點行為來自訂服務端點的本機行為。 端點行為是藉由參與建立 WCF 執行時間的程式來達到此目的。 <xref:System.ServiceModel.Description.ServiceEndpoint.ListenUri%2A> 屬性是一個端點行為範例，它可讓您指定不同於 SOAP 或 Web 服務描述語言 (WSDL) 位址的接聽位址。 如需詳細資訊，請參閱[ClientViaBehavior](../diagnostics/wmi/clientviabehavior.md)。

## <a name="defining-endpoints"></a>定義端點

您可以透過命令式程式碼或是宣告式組態來指定服務端點。 如需詳細資訊，請參閱[如何：在設定中建立服務端點](how-to-create-a-service-endpoint-in-configuration.md)和[如何：在程式碼中建立服務端點](how-to-create-a-service-endpoint-in-code.md)。

## <a name="in-this-section"></a>本節內容

本章節說明繫結、端點與位址的用途；說明如何設定繫結與端點；並示範如何使用 `ClientVia` 行為和 `ListenUri` 屬性。

[址](endpoint-addresses.md)\
描述如何在 WCF 中定址端點。

[關係](bindings.md)\
說明如何使用繫結程序來指定必要的傳輸、編碼與通訊協定詳細資料，以供用戶端與服務彼此通訊。

[協定](contracts.md)\
說明合約如何定義服務方法。

[如何：在設定中建立服務端點](how-to-create-a-service-endpoint-in-configuration.md)\
說明如何透過組態建立服務端點。

[如何：在程式碼中建立服務端點](how-to-create-a-service-endpoint-in-code.md)\
說明如何透過程式碼建立服務端點。

[如何：使用 Svcutil 來驗證已編譯的服務程式代碼](how-to-use-svcutil-exe-to-validate-compiled-service-code.md)\
描述如何使用[System.servicemodel 中繼資料公用程式工具（Svcutil）](../servicemodel-metadata-utility-tool-svcutil-exe.md)，在不裝載服務的情況下，偵測服務執行和設定中的錯誤。

## <a name="see-also"></a>請參閱

- [設定服務](../configuring-services.md)
- [擴充繫結](../extending/extending-bindings.md)
