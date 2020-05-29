---
title: 受控偵錯工具-.NET Core
description: 概述 Visual Studio 和 Visual Studio Code 受控偵錯工具。
ms.date: 08/05/2019
ms.openlocfilehash: 28cc21980bc78234f7af3b4668e2fa77fbf8ce5b
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84200866"
---
# <a name="net-core-managed-debuggers"></a><span data-ttu-id="45eac-103">.NET Core 受控偵錯工具</span><span class="sxs-lookup"><span data-stu-id="45eac-103">.NET Core managed debuggers</span></span>

<span data-ttu-id="45eac-104">偵錯工具可以逐步暫停或執行程式。</span><span class="sxs-lookup"><span data-stu-id="45eac-104">Debuggers allow programs to be paused or executed step-by-step.</span></span> <span data-ttu-id="45eac-105">暫停時，可以查看進程的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="45eac-105">When paused, the current state of the process can be viewed.</span></span> <span data-ttu-id="45eac-106">藉由逐步執行主要章節，您可以瞭解您的程式碼及其產生結果的原因。</span><span class="sxs-lookup"><span data-stu-id="45eac-106">By stepping through key sections, you gain understanding of your code and why it produces the result that it does.</span></span>

<span data-ttu-id="45eac-107">Microsoft 會在**Visual Studio**和**Visual Studio Code**中提供受控碼的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="45eac-107">Microsoft provides debuggers for managed code in **Visual Studio** and **Visual Studio Code**.</span></span>

## <a name="visual-studio-managed-debugger"></a><span data-ttu-id="45eac-108">Visual Studio managed 偵錯工具</span><span class="sxs-lookup"><span data-stu-id="45eac-108">Visual Studio managed debugger</span></span>

<span data-ttu-id="45eac-109">**Visual Studio**是一個整合式開發環境，其中提供最完整的偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="45eac-109">**Visual Studio** is an integrated development environment with the most comprehensive debugger available.</span></span> <span data-ttu-id="45eac-110">對於在 Windows 上工作的開發人員而言，Visual Studio 是絕佳的選擇。</span><span class="sxs-lookup"><span data-stu-id="45eac-110">Visual Studio is an excellent choice for developers working on Windows.</span></span>

- [<span data-ttu-id="45eac-111">教學課程-使用 Visual Studio 在 Windows 上調試 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="45eac-111">Tutorial - Debugging a .NET Core application on Windows with Visual Studio</span></span>](../tutorials/debugging-with-visual-studio.md)

<span data-ttu-id="45eac-112">雖然 Visual Studio 是 Windows 應用程式，但仍可用於從遠端對 Linux 和 macOS 應用程式進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="45eac-112">While Visual Studio is a Windows application, it can still be used to debug Linux and macOS apps remotely.</span></span>

- [<span data-ttu-id="45eac-113">在 Linux/OSX 上使用 Visual Studio 來進行 .NET Core 應用程式的偵錯工具</span><span class="sxs-lookup"><span data-stu-id="45eac-113">Debugging a .NET Core application on Linux/OSX with Visual Studio</span></span>](https://github.com/Microsoft/MIEngine/wiki/Offroad-Debugging-of-.NET-Core-on-Linux---OSX-from-Visual-Studio)

 <span data-ttu-id="45eac-114">ASP.NET Core 應用程式的偵錯工具需要稍微不同的指示。</span><span class="sxs-lookup"><span data-stu-id="45eac-114">Debugging ASP.NET Core apps require slightly different instructions.</span></span>

- [<span data-ttu-id="45eac-115">Visual Studio 中的 Debug ASP.NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="45eac-115">Debug ASP.NET Core apps in Visual Studio</span></span>](/visualstudio/debugger/how-to-enable-debugging-for-aspnet-applications#debug-aspnet-core-apps)

## <a name="visual-studio-code-managed-debugger"></a><span data-ttu-id="45eac-116">Visual Studio Code managed 偵錯工具</span><span class="sxs-lookup"><span data-stu-id="45eac-116">Visual Studio Code managed debugger</span></span>

<span data-ttu-id="45eac-117">**Visual Studio Code**是輕量的跨平臺程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="45eac-117">**Visual Studio Code** is a lightweight cross-platform code editor.</span></span> <span data-ttu-id="45eac-118">它使用與 Visual Studio 相同的 .NET Core 偵錯工具實作為，但使用簡化的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="45eac-118">It uses the same .NET Core debugger implementation as Visual Studio, but with a simplified user interface.</span></span>

- [<span data-ttu-id="45eac-119">教學課程-使用 Visual Studio Code 來調試 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="45eac-119">Tutorial - Debugging a .NET Core application with Visual Studio Code</span></span>](../tutorials/debugging-with-visual-studio-code.md)
- [<span data-ttu-id="45eac-120">在 Visual Studio Code 中偵錯</span><span class="sxs-lookup"><span data-stu-id="45eac-120">Debugging in Visual Studio Code</span></span>](https://code.visualstudio.com/docs/editor/debugging)
