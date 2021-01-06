---
title: 適用于 WCF 開發人員的介面定義語言-gRPC
description: 介紹通訊協定緩衝區 IDL。
ms.date: 12/15/2020
ms.openlocfilehash: 60cedd9b7c29bf54165b15f512c0b2159cb5dda9
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938074"
---
# <a name="interface-definition-language"></a><span data-ttu-id="85cd3-103">介面定義語言</span><span class="sxs-lookup"><span data-stu-id="85cd3-103">Interface Definition Language</span></span>

<span data-ttu-id="85cd3-104">使用 WCF) 的 Windows Communication Foundation (，服務可以使用 Web 服務定義語言 (WSDL) 來公開描述中繼資料。</span><span class="sxs-lookup"><span data-stu-id="85cd3-104">With Windows Communication Foundation (WCF), services can expose description metadata by using the Web Service Definition Language (WSDL).</span></span> <span data-ttu-id="85cd3-105">WSDL 是在執行時間使用 .NET 反映動態產生的。</span><span class="sxs-lookup"><span data-stu-id="85cd3-105">WSDL is generated dynamically by using .NET reflection at runtime.</span></span> <span data-ttu-id="85cd3-106">開發人員可以使用此中繼資料來產生這些服務的用戶端，如果它們是使用平臺中立的系結（例如 SOAP over HTTP），可能會使用其他語言。</span><span class="sxs-lookup"><span data-stu-id="85cd3-106">Developers can use this metadata to generate clients for those services, potentially in other languages if they're using a platform-neutral binding such as SOAP over HTTP.</span></span>

<span data-ttu-id="85cd3-107">gRPC 使用介面定義語言 (從通訊協定緩衝區) 的 IDL。</span><span class="sxs-lookup"><span data-stu-id="85cd3-107">gRPC uses the Interface Definition Language (IDL) from Protocol Buffers.</span></span> <span data-ttu-id="85cd3-108">通訊協定緩衝區的 IDL 是具有開啟規格的自訂、平臺中立語言。</span><span class="sxs-lookup"><span data-stu-id="85cd3-108">The Protocol Buffers IDL is a custom, platform-neutral language with an open specification.</span></span> <span data-ttu-id="85cd3-109">開發人員會撰寫 `.proto` 用來描述服務的檔案，以及它們的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="85cd3-109">Developers author `.proto` files to describe services, along with their inputs and outputs.</span></span> <span data-ttu-id="85cd3-110">`.proto`然後，您可以使用這些檔案來產生用戶端和伺服器的語言或平臺特定的存根，讓多個不同的平臺進行通訊。</span><span class="sxs-lookup"><span data-stu-id="85cd3-110">These `.proto` files can then be used to generate language- or platform-specific stubs for clients and servers, allowing multiple different platforms to communicate.</span></span> <span data-ttu-id="85cd3-111">藉由共用檔案 `.proto` ，小組可以產生程式碼來使用彼此的服務，而不需要採取程式碼相依性。</span><span class="sxs-lookup"><span data-stu-id="85cd3-111">By sharing `.proto` files, teams can generate code to use each others' services, without needing to take a code dependency.</span></span>

<span data-ttu-id="85cd3-112">Protobuf IDL 的優點之一，就是作為自訂語言，它可讓 gRPC 完全與語言和平臺無關，而不會 favoring 任何技術。</span><span class="sxs-lookup"><span data-stu-id="85cd3-112">One of the advantages of the Protobuf IDL is that as a custom language, it enables gRPC to be completely language and platform agnostic, not favoring any technology over another.</span></span>

<span data-ttu-id="85cd3-113">Protobuf IDL 也設計為方便人們進行讀取和寫入，而 WSDL 則是以機器可讀取/可寫入的格式表示。</span><span class="sxs-lookup"><span data-stu-id="85cd3-113">The Protobuf IDL is also designed for humans to both read and write, whereas WSDL is intended as a machine-readable/writable format.</span></span> <span data-ttu-id="85cd3-114">變更 WCF 服務的 WSDL 通常需要變更服務、執行服務，以及重新產生伺服器的 WSDL 檔案。</span><span class="sxs-lookup"><span data-stu-id="85cd3-114">Changing the WSDL of a WCF service typically requires changing the service, running the service, and regenerating the WSDL file from the server.</span></span> <span data-ttu-id="85cd3-115">相較之下，使用檔案時 `.proto` ，變更很容易與文字編輯器一起套用，並且會自動流經產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="85cd3-115">By contrast, with a `.proto` file, changes are simple to apply with a text editor, and automatically flow through the generated code.</span></span> <span data-ttu-id="85cd3-116">Visual Studio 2019 在 `.proto` 儲存檔案時，會在背景中建立檔案。</span><span class="sxs-lookup"><span data-stu-id="85cd3-116">Visual Studio 2019 builds `.proto` files in the background when they are saved.</span></span> <span data-ttu-id="85cd3-117">使用其他編輯器（例如 VS Code）時，會在建立專案時套用變更。</span><span class="sxs-lookup"><span data-stu-id="85cd3-117">With other editors, such as VS Code, the changes are applied when the project is built.</span></span>

<span data-ttu-id="85cd3-118">相較于 XML （尤其是 SOAP），使用 Protobuf 編碼的訊息有許多優點。</span><span class="sxs-lookup"><span data-stu-id="85cd3-118">When compared with XML, and particularly SOAP, messages encoded by using Protobuf have many advantages.</span></span> <span data-ttu-id="85cd3-119">Protobuf 訊息通常會小於序列化為 SOAP XML 的相同資料，並透過網路進行編碼、解碼和傳輸，可能會更快。</span><span class="sxs-lookup"><span data-stu-id="85cd3-119">Protobuf messages tend to be smaller than the same data serialized as SOAP XML, and encoding, decoding, and transmitting them over a network can be faster.</span></span>

<span data-ttu-id="85cd3-120">相較于 SOAP，Protobuf 的潛在缺點是，因為人類無法讀取訊息，所以需要其他工具來將訊息內容進行調試。</span><span class="sxs-lookup"><span data-stu-id="85cd3-120">The potential disadvantage of Protobuf compared to SOAP is that, because the messages aren't readable by humans, additional tooling is required to debug message content.</span></span>

> [!TIP]
> <span data-ttu-id="85cd3-121">gRPC *支援* 的伺服器反映可動態存取不含預先編譯存根的服務，不過它比應用程式特定的用戶端更適合一般用途工具。</span><span class="sxs-lookup"><span data-stu-id="85cd3-121">gRPC *does* support server reflection for dynamically accessing services without pre-compiled stubs, although it's intended more for general-purpose tools than application-specific clients.</span></span> <span data-ttu-id="85cd3-122">如需詳細資訊，請參閱 GitHub 上的 [GRPC 伺服器反映通訊協定](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md) 。</span><span class="sxs-lookup"><span data-stu-id="85cd3-122">For more information, see [GRPC Server Reflection Protocol](https://github.com/grpc/grpc/blob/master/doc/server-reflection.md) on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="85cd3-123">與 NetTCP 系結搭配使用的 WCF 二進位格式，在壓縮度和效能方面更接近 Protobuf。</span><span class="sxs-lookup"><span data-stu-id="85cd3-123">WCF's binary format, used with the NetTCP binding, is much closer to Protobuf in terms of compactness and performance.</span></span> <span data-ttu-id="85cd3-124">但是，NetTCP 只能在 .NET 用戶端和伺服器之間使用，而 Protobuf 則是跨平臺的解決方案。</span><span class="sxs-lookup"><span data-stu-id="85cd3-124">But NetTCP is only usable between .NET clients and servers, whereas Protobuf is a cross-platform solution.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="85cd3-125">[上一個](approach.md) 
>[下一步](network-protocols.md)</span><span class="sxs-lookup"><span data-stu-id="85cd3-125">[Previous](approach.md)
[Next](network-protocols.md)</span></span>
