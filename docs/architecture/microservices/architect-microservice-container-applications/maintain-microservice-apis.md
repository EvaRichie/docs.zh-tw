---
title: 建立、發展以及版本控制微服務 API 與協定
description: 因為需求會變更，所以要建立考慮演進和版本控制的 API 與合約。
ms.date: 01/13/2021
ms.openlocfilehash: 84eeaa9776947abda6171949c730f8473e97b241
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189456"
---
# <a name="creating-evolving-and-versioning-microservice-apis-and-contracts"></a>建立、發展以及版本控制微服務 API 與協定

微服務 API 是服務與其用戶端之間的協定。 您只能在不中斷微服務 API 合約的前提下獨立演進微服務，因此合約十分重要。 如果您變更協定，會影響用戶端應用程式或您的 API 閘道。

API 定義的性質取決於您所用的通訊協定。 例如，若您使用傳訊 (像是 [AMQP](http://www.amqp.org/))，API 會由訊息類型組成。 如果您使用 HTTP 和 RESTful 服務，API 則包含 URL 和要求與回應的 JSON 格式。

但是，即使您審慎考量您的初始合約，服務 API 仍必須隨著時間而變更。 發生這種情況時，尤其如果您的 API 是由多個用戶端應用程式取用的公用 API，您通常無法強制所有用戶端升級到新的 API 合約。 您通常需要以累加方式部署服務的新版本，並且要能夠同時執行服務協定的新舊兩種版本。 因此，為您的服務版本控制制定策略非常重要。

當 API 變化很小時，例如對 API 新增屬性或參數時，使用舊 API 的用戶端應該切換並使用新版本的服務。 您可以為所需的任何遺漏屬性提供預設值，而用戶端可以略過任何額外的回應屬性。

不過，有時候您會需要對服務 API 進行重大且不相容的變更。 因為您可能無法強制用戶端應用程式或服務立刻升級到新版本，所以服務必須繼續支援舊版的 API 一段時間。 如果您使用 HTTP 式的機制 (例如 REST)，其中一個方法是在 URL 或是 HTTP 標頭內嵌 API 版本號碼。 然後您可以決定要在相同的服務執行個體中同時實作服務的兩個版本，或是要部署不同的執行個體，分別處理各一個 API 版本。 這項功能的一個好方法是 [中繼程式模式](https://en.wikipedia.org/wiki/Mediator_pattern) (例如， [MediatR 程式庫](https://github.com/jbogard/MediatR)) 將不同的實版本分離成獨立的處理常式。

最後，如果您使用 REST 架構，[Hypermedia](https://www.infoq.com/articles/mark-baker-hypermedia) (超媒體) 即為進行服務版本控制及允許演進 API 的最佳解決方案。

## <a name="additional-resources"></a>其他資源

- **Scott Hanselman。ASP.NET Core RESTful Web API 版本設定變得更簡單** \
  <https://www.hanselman.com/blog/ASPNETCoreRESTfulWebAPIVersioningMadeEasy.aspx>

- **RESTful web API 的版本控制** \
  <https://docs.microsoft.com/azure/architecture/best-practices/api-design#versioning-a-restful-web-api>

- **Roy版本控制、超媒體和 REST** \
  <https://www.infoq.com/articles/roy-fielding-on-versioning>

>[!div class="step-by-step"]
>[上一個](asynchronous-message-based-communication.md) 
>[下一步](microservices-addressability-service-registry.md)
