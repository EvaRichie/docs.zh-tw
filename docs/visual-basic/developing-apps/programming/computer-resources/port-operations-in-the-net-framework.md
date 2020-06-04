---
title: .NET Framework 中的連接埠作業
ms.date: 07/20/2015
helpviewer_keywords:
- ports, Visual Basic
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
ms.openlocfilehash: 0ef0b8a7aec40603185d227d972cea655fd238c1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360133"
---
# <a name="port-operations-in-the-net-framework-with-visual-basic"></a><span data-ttu-id="07f10-102">.NET Framework 中使用 Visual Basic 的連接埠作業</span><span class="sxs-lookup"><span data-stu-id="07f10-102">Port Operations in the .NET Framework with Visual Basic</span></span>

<span data-ttu-id="07f10-103">您可以透過 <xref:System.IO.Ports?displayProperty=nameWithType> 命名空間中的 .NET Framework 類別，存取電腦的序列埠。</span><span class="sxs-lookup"><span data-stu-id="07f10-103">You can access your computer's serial ports through the .NET Framework classes in the <xref:System.IO.Ports?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="07f10-104">做為最重要的類別，<xref:System.IO.Ports.SerialPort> 會提供同步化與事件驅動之 I/O 的架構、PIN 和中斷狀態的存取權，以及序列驅動程式屬性的存取權。</span><span class="sxs-lookup"><span data-stu-id="07f10-104">The most important class, <xref:System.IO.Ports.SerialPort>, provides a framework for synchronous and event-driven I/O, access to pin and break states, and access to serial driver properties.</span></span> <span data-ttu-id="07f10-105">它可以包裝在 <xref:System.IO.Stream> 物件中，該物件可透過 <xref:System.IO.Ports.SerialPort.BaseStream> 屬性存取。</span><span class="sxs-lookup"><span data-stu-id="07f10-105">It can be wrapped in a <xref:System.IO.Stream> object, accessible through the <xref:System.IO.Ports.SerialPort.BaseStream> property.</span></span> <span data-ttu-id="07f10-106">將 <xref:System.IO.Ports.SerialPort> 包裝在 <xref:System.IO.Stream> 物件中，可讓使用資料流的類別存取序列埠。</span><span class="sxs-lookup"><span data-stu-id="07f10-106">Wrapping <xref:System.IO.Ports.SerialPort> in a <xref:System.IO.Stream> object allows the serial port to be accessed by classes that use streams.</span></span> <span data-ttu-id="07f10-107">命名空間包含可簡化序列埠控制的列舉。</span><span class="sxs-lookup"><span data-stu-id="07f10-107">The namespace includes enumerations that simplify the control of serial ports.</span></span>

<span data-ttu-id="07f10-108">建立 <xref:System.IO.Ports.SerialPort> 物件最簡單的方式，是透過 <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="07f10-108">The simplest way to create a <xref:System.IO.Ports.SerialPort> object is through the <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> method.</span></span>

> [!NOTE]
> <span data-ttu-id="07f10-109">您無法使用 .NET Framework 類別直接存取其他型別的連接埠，例如平行連接埠、USB 連接埠等。</span><span class="sxs-lookup"><span data-stu-id="07f10-109">You cannot use .NET Framework classes to directly access other types of ports, such as parallel ports, USB ports, and so on.</span></span>

## <a name="enumerations"></a><span data-ttu-id="07f10-110">列舉</span><span class="sxs-lookup"><span data-stu-id="07f10-110">Enumerations</span></span>

<span data-ttu-id="07f10-111">本表會列出並說明用於存取序列埠的主要列舉︰</span><span class="sxs-lookup"><span data-stu-id="07f10-111">This table lists and describes the main enumerations used for accessing a serial port:</span></span>

|<span data-ttu-id="07f10-112">列舉型別</span><span class="sxs-lookup"><span data-stu-id="07f10-112">Enumeration</span></span>|<span data-ttu-id="07f10-113">Description</span><span class="sxs-lookup"><span data-stu-id="07f10-113">Description</span></span>|
|---|---|
|<xref:System.IO.Ports.Handshake>|<span data-ttu-id="07f10-114">指定建立 <xref:System.IO.Ports.SerialPort> 物件之序列埠通訊使用的控制通訊協定。</span><span class="sxs-lookup"><span data-stu-id="07f10-114">Specifies the control protocol used in establishing a serial port communication for a <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.Parity>|<span data-ttu-id="07f10-115">指定 <xref:System.IO.Ports.SerialPort> 物件的同位位元。</span><span class="sxs-lookup"><span data-stu-id="07f10-115">Specifies the parity bit for a <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.SerialData>|<span data-ttu-id="07f10-116">指定 <xref:System.IO.Ports.SerialPort> 物件之序列埠接收到的字元類型。</span><span class="sxs-lookup"><span data-stu-id="07f10-116">Specifies the type of character that was received on the serial port of the <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.SerialError>|<span data-ttu-id="07f10-117">指定在 <xref:System.IO.Ports.SerialPort> 物件上發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="07f10-117">Specifies errors that occur on the <xref:System.IO.Ports.SerialPort> object</span></span>|
|<xref:System.IO.Ports.SerialPinChange>|<span data-ttu-id="07f10-118">指定在 <xref:System.IO.Ports.SerialPort> 物件上發生的變更類型。</span><span class="sxs-lookup"><span data-stu-id="07f10-118">Specifies the type of change that occurred on the <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.StopBits>|<span data-ttu-id="07f10-119">指定在 <xref:System.IO.Ports.SerialPort> 物件上使用的停止位元數目。</span><span class="sxs-lookup"><span data-stu-id="07f10-119">Specifies the number of stop bits used on the <xref:System.IO.Ports.SerialPort> object.</span></span>|

## <a name="see-also"></a><span data-ttu-id="07f10-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="07f10-120">See also</span></span>

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [<span data-ttu-id="07f10-121">存取電腦的連接埠</span><span class="sxs-lookup"><span data-stu-id="07f10-121">Accessing the Computer's Ports</span></span>](accessing-the-computer-s-ports.md)
