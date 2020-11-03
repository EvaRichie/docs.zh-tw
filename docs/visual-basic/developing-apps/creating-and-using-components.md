---
title: 建立及使用元件
ms.date: 07/20/2015
helpviewer_keywords:
- components [Visual Basic]
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
ms.openlocfilehash: 106b8791ee5cb3db95759ccca2fddd799661ef3c
ms.sourcegitcommit: 74d05613d6c57106f83f82ce8ee71176874ea3f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93282067"
---
# <a name="creating-and-using-components-in-visual-basic"></a><span data-ttu-id="8d540-102">在 Visual Basic 中建立和使用元件</span><span class="sxs-lookup"><span data-stu-id="8d540-102">Creating and Using Components in Visual Basic</span></span>

<span data-ttu-id="8d540-103">「元件」是實作 <xref:System.ComponentModel.IComponent?displayProperty=nameWithType> 介面的類別，或直接或間接衍生自可實作 <xref:System.ComponentModel.IComponent> 類別的類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-103">A *component* is a class that implements the <xref:System.ComponentModel.IComponent?displayProperty=nameWithType> interface or that derives directly or indirectly from a class that implements <xref:System.ComponentModel.IComponent>.</span></span> <span data-ttu-id="8d540-104">.NET 元件是可重複使用的物件，可以與其他物件互動，並提供外部資源和設計階段支援的控制權。</span><span class="sxs-lookup"><span data-stu-id="8d540-104">A .NET component is an object that is reusable, can interact with other objects, and provides control over external resources and design-time support.</span></span>  
  
 <span data-ttu-id="8d540-105">元件的一項重要功能是可以進行設計，這表示類別如果是元件，則可用於 Visual Studio 整合式開發環境。</span><span class="sxs-lookup"><span data-stu-id="8d540-105">An important feature of components is that they are designable, which means that a class that is a component can be used in the Visual Studio Integrated Development Environment.</span></span> <span data-ttu-id="8d540-106">元件可以新增至工具箱、拖曳並放至表單上，以及在設計介面上操作。</span><span class="sxs-lookup"><span data-stu-id="8d540-106">A component can be added to the Toolbox, dragged and dropped onto a form, and manipulated on a design surface.</span></span> <span data-ttu-id="8d540-107">元件的基礎設計階段支援是內建在 .NET 中。</span><span class="sxs-lookup"><span data-stu-id="8d540-107">Base design-time support for components is built into .NET.</span></span> <span data-ttu-id="8d540-108">元件開發人員不需要執行任何額外的工作，即可利用基本設計階段功能。</span><span class="sxs-lookup"><span data-stu-id="8d540-108">A component developer does not have to do any additional work to take advantage of the base design-time functionality.</span></span>  
  
 <span data-ttu-id="8d540-109">「控制項」類似於元件，都是可以設計的。</span><span class="sxs-lookup"><span data-stu-id="8d540-109">A *control* is similar to a component, as both are designable.</span></span> <span data-ttu-id="8d540-110">不過，控制項提供使用者介面，而元件則不提供。</span><span class="sxs-lookup"><span data-stu-id="8d540-110">However, a control provides a user interface, while a component does not.</span></span> <span data-ttu-id="8d540-111">控制項必須衍生自基底控制項類別其中之一︰<xref:System.Windows.Forms.Control> 或 <xref:System.Web.UI.Control>。</span><span class="sxs-lookup"><span data-stu-id="8d540-111">A control must derive from one of the base control classes: <xref:System.Windows.Forms.Control> or <xref:System.Web.UI.Control>.</span></span>  
  
## <a name="when-to-create-a-component"></a><span data-ttu-id="8d540-112">建立元件的時機</span><span class="sxs-lookup"><span data-stu-id="8d540-112">When to Create a Component</span></span>  

 <span data-ttu-id="8d540-113">如果您的類別將用在設計介面 (例如 Windows Forms 或 Web Forms 設計工具)，但沒有使用者介面，則它應該是元件，並且實作 <xref:System.ComponentModel.IComponent>，或衍生自直接或間接實作 <xref:System.ComponentModel.IComponent> 的類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-113">If your class will be used on a design surface (such as the Windows Forms or Web Forms Designer) but has no user interface, it should be a component and implement <xref:System.ComponentModel.IComponent>, or derive from a class that directly or indirectly implements <xref:System.ComponentModel.IComponent>.</span></span>  
  
 <span data-ttu-id="8d540-114"><xref:System.ComponentModel.Component> 和 <xref:System.ComponentModel.MarshalByValueComponent> 類別是 <xref:System.ComponentModel.IComponent> 介面的基底實作。</span><span class="sxs-lookup"><span data-stu-id="8d540-114">The <xref:System.ComponentModel.Component> and <xref:System.ComponentModel.MarshalByValueComponent> classes are base implementations of the <xref:System.ComponentModel.IComponent> interface.</span></span> <span data-ttu-id="8d540-115">這些類別的主要差異在於 <xref:System.ComponentModel.Component> 類別是以傳址方式封送處理，而 <xref:System.ComponentModel.IComponent> 是以傳值方式封送處理。</span><span class="sxs-lookup"><span data-stu-id="8d540-115">The main difference between these classes is that the <xref:System.ComponentModel.Component> class is marshaled by reference, while <xref:System.ComponentModel.IComponent> is marshaled by value.</span></span> <span data-ttu-id="8d540-116">下列清單為實作者提供廣泛的指導方針。</span><span class="sxs-lookup"><span data-stu-id="8d540-116">The following list provides broad guidelines for implementers.</span></span>  
  
- <span data-ttu-id="8d540-117">如果您的元件需要以傳址方式封送處理，則衍生自 <xref:System.ComponentModel.Component>。</span><span class="sxs-lookup"><span data-stu-id="8d540-117">If your component needs to be marshaled by reference, derive from <xref:System.ComponentModel.Component>.</span></span>  
  
- <span data-ttu-id="8d540-118">如果您的元件需要以傳值方式封送處理，則衍生自 <xref:System.ComponentModel.MarshalByValueComponent>。</span><span class="sxs-lookup"><span data-stu-id="8d540-118">If your component needs to be marshaled by value, derive from <xref:System.ComponentModel.MarshalByValueComponent>.</span></span>  
  
- <span data-ttu-id="8d540-119">如果您的元件因為單一繼承而不能衍生自其中一個基底實作，請實作 <xref:System.ComponentModel.IComponent>。</span><span class="sxs-lookup"><span data-stu-id="8d540-119">If your component cannot derive from one of the base implementations due to single inheritance, implement <xref:System.ComponentModel.IComponent>.</span></span>  
  
## <a name="component-classes"></a><span data-ttu-id="8d540-120">元件類別</span><span class="sxs-lookup"><span data-stu-id="8d540-120">Component Classes</span></span>  

 <span data-ttu-id="8d540-121"><xref:System.ComponentModel> 命名空間提供類別，用來實作元件和控制項的執行階段和設計階段行為。</span><span class="sxs-lookup"><span data-stu-id="8d540-121">The <xref:System.ComponentModel> namespace provides classes that are used to implement the run-time and design-time behavior of components and controls.</span></span> <span data-ttu-id="8d540-122">此命名空間包含基底類別和介面，以便實作屬性和類型轉換器、繫結至資料來源，以及授權元件。</span><span class="sxs-lookup"><span data-stu-id="8d540-122">This namespace includes the base classes and interfaces for implementing attributes and type converters, binding to data sources, and licensing components.</span></span>  
  
 <span data-ttu-id="8d540-123">核心元件類別包括︰</span><span class="sxs-lookup"><span data-stu-id="8d540-123">The core component classes are:</span></span>  
  
- <span data-ttu-id="8d540-124"><xref:System.ComponentModel.Component>.</span><span class="sxs-lookup"><span data-stu-id="8d540-124"><xref:System.ComponentModel.Component>.</span></span> <span data-ttu-id="8d540-125"><xref:System.ComponentModel.IComponent> 介面的基底實作。</span><span class="sxs-lookup"><span data-stu-id="8d540-125">A base implementation for the <xref:System.ComponentModel.IComponent> interface.</span></span> <span data-ttu-id="8d540-126">這個類別可在應用程式之間共用物件。</span><span class="sxs-lookup"><span data-stu-id="8d540-126">This class enables object sharing between applications.</span></span>  
  
- <span data-ttu-id="8d540-127"><xref:System.ComponentModel.MarshalByValueComponent>.</span><span class="sxs-lookup"><span data-stu-id="8d540-127"><xref:System.ComponentModel.MarshalByValueComponent>.</span></span> <span data-ttu-id="8d540-128"><xref:System.ComponentModel.IComponent> 介面的基底實作。</span><span class="sxs-lookup"><span data-stu-id="8d540-128">A base implementation for the <xref:System.ComponentModel.IComponent> interface.</span></span>  
  
- <span data-ttu-id="8d540-129"><xref:System.ComponentModel.Container>.</span><span class="sxs-lookup"><span data-stu-id="8d540-129"><xref:System.ComponentModel.Container>.</span></span> <span data-ttu-id="8d540-130"><xref:System.ComponentModel.IContainer> 介面的基底實作。</span><span class="sxs-lookup"><span data-stu-id="8d540-130">The base implementation for the <xref:System.ComponentModel.IContainer> interface.</span></span> <span data-ttu-id="8d540-131">這個類別會封裝零個或更多元件。</span><span class="sxs-lookup"><span data-stu-id="8d540-131">This class encapsulates zero or more components.</span></span>  
  
 <span data-ttu-id="8d540-132">用於元件授權的部分類別包括︰</span><span class="sxs-lookup"><span data-stu-id="8d540-132">Some of the classes used for component licensing are:</span></span>  
  
- <span data-ttu-id="8d540-133"><xref:System.ComponentModel.License>.</span><span class="sxs-lookup"><span data-stu-id="8d540-133"><xref:System.ComponentModel.License>.</span></span> <span data-ttu-id="8d540-134">所有授權的抽象基底類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-134">The abstract base class for all licenses.</span></span> <span data-ttu-id="8d540-135">授權是授與給元件的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="8d540-135">A license is granted to a specific instance of a component.</span></span>  
  
- <span data-ttu-id="8d540-136"><xref:System.ComponentModel.LicenseManager>.</span><span class="sxs-lookup"><span data-stu-id="8d540-136"><xref:System.ComponentModel.LicenseManager>.</span></span> <span data-ttu-id="8d540-137">提供屬性和方法以新增授權至元件，以及管理 <xref:System.ComponentModel.LicenseProvider>。</span><span class="sxs-lookup"><span data-stu-id="8d540-137">Provides properties and methods to add a license to a component and to manage a <xref:System.ComponentModel.LicenseProvider>.</span></span>  
  
- <span data-ttu-id="8d540-138"><xref:System.ComponentModel.LicenseProvider>.</span><span class="sxs-lookup"><span data-stu-id="8d540-138"><xref:System.ComponentModel.LicenseProvider>.</span></span> <span data-ttu-id="8d540-139">實作授權提供者的抽象基底類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-139">The abstract base class for implementing a license provider.</span></span>  
  
- <span data-ttu-id="8d540-140"><xref:System.ComponentModel.LicenseProviderAttribute>.</span><span class="sxs-lookup"><span data-stu-id="8d540-140"><xref:System.ComponentModel.LicenseProviderAttribute>.</span></span> <span data-ttu-id="8d540-141">指定要與類別一起使用的 <xref:System.ComponentModel.LicenseProvider> 類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-141">Specifies the <xref:System.ComponentModel.LicenseProvider> class to use with a class.</span></span>  
  
 <span data-ttu-id="8d540-142">常用於描述和保存元件的類別。</span><span class="sxs-lookup"><span data-stu-id="8d540-142">Classes commonly used for describing and persisting components.</span></span>  
  
- <span data-ttu-id="8d540-143"><xref:System.ComponentModel.TypeDescriptor>.</span><span class="sxs-lookup"><span data-stu-id="8d540-143"><xref:System.ComponentModel.TypeDescriptor>.</span></span> <span data-ttu-id="8d540-144">提供元件特性的相關資訊，例如其屬性 (attribute)、屬性 (property) 與事件。</span><span class="sxs-lookup"><span data-stu-id="8d540-144">Provides information about the characteristics for a component, such as its attributes, properties, and events.</span></span>  
  
- <span data-ttu-id="8d540-145"><xref:System.ComponentModel.EventDescriptor>.</span><span class="sxs-lookup"><span data-stu-id="8d540-145"><xref:System.ComponentModel.EventDescriptor>.</span></span> <span data-ttu-id="8d540-146">提供事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8d540-146">Provides information about an event.</span></span>  
  
- <span data-ttu-id="8d540-147"><xref:System.ComponentModel.PropertyDescriptor>.</span><span class="sxs-lookup"><span data-stu-id="8d540-147"><xref:System.ComponentModel.PropertyDescriptor>.</span></span> <span data-ttu-id="8d540-148">提供屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8d540-148">Provides information about a property.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="8d540-149">相關章節</span><span class="sxs-lookup"><span data-stu-id="8d540-149">Related Sections</span></span>  

 [<span data-ttu-id="8d540-150">針對控制項和元件撰寫進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="8d540-150">Troubleshooting Control and Component Authoring</span></span>](/dotnet/desktop/winforms/controls/troubleshooting-control-and-component-authoring)  
 <span data-ttu-id="8d540-151">說明如何修正常見問題。</span><span class="sxs-lookup"><span data-stu-id="8d540-151">Explains how to fix common problems.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8d540-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8d540-152">See also</span></span>

- [<span data-ttu-id="8d540-153">如何：在 Windows Forms 中存取設計階段支援</span><span class="sxs-lookup"><span data-stu-id="8d540-153">How to: Access Design-Time Support in Windows Forms</span></span>](/dotnet/desktop/winforms/controls/developing-windows-forms-controls-at-design-time)
