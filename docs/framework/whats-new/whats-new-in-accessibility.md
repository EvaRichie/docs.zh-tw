---
title: .NET Framework 中協助工具的新功能
titleSuffix: ''
description: 從 .NET Framework 4.7.1 開始，請參閱 .NET 協助工具的新功能。 協助工具功能可讓應用程式為輔助技術使用者提供適當的體驗。
ms.date: 01/05/2021
dev_langs:
- csharp
- vb
helpviewer_keywords:
- what's new [.NET Framework]
ms.openlocfilehash: c2ebaed8bf347eb8d8764f4bdf76dcc33db86bad
ms.sourcegitcommit: 3a8f1979a98c6c19217a1930e0af5908988eb8ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2021
ms.locfileid: "98536160"
---
# <a name="whats-new-in-accessibility-in-net-framework"></a><span data-ttu-id="d737f-104">.NET Framework 中協助工具的新功能</span><span class="sxs-lookup"><span data-stu-id="d737f-104">What's new in accessibility in .NET Framework</span></span>

<span data-ttu-id="d737f-105">.NET Framework 的目標是讓您的使用者更容易存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="d737f-105">.NET Framework aims to make applications more accessible for your users.</span></span> <span data-ttu-id="d737f-106">協助工具功能可讓應用程式提供適當的輔助技術使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="d737f-106">Accessibility features allow an application to provide an appropriate experience for users of Assistive Technology.</span></span> <span data-ttu-id="d737f-107">從 .NET Framework 4.7.1 開始，.NET Framework 包含大量的協助工具改善，可讓開發人員建立可存取的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d737f-107">Starting with .NET Framework 4.7.1, .NET Framework includes a large number of accessibility improvements that allow developers to create accessible applications.</span></span>

## <a name="accessibility-switches"></a><span data-ttu-id="d737f-108">協助工具參數</span><span class="sxs-lookup"><span data-stu-id="d737f-108">Accessibility switches</span></span>

<span data-ttu-id="d737f-109">如果您的應用程式是以 .NET Framework 4.7 或較早版本為目標，但是在 .NET Framework 4.7.1 或更新版本上執行，您可以將其設定為選擇加入協助工具功能。</span><span class="sxs-lookup"><span data-stu-id="d737f-109">You can configure your app to opt into accessibility features if it targets .NET Framework 4.7 or an earlier version but is running on .NET Framework 4.7.1 or later.</span></span> <span data-ttu-id="d737f-110">如果您的應用程式是以 .NET Framework 4.7.1 或更新版本為目標，您也可以將其設定為使用舊版的功能 (且不利用協助工具功能)。</span><span class="sxs-lookup"><span data-stu-id="d737f-110">You can also configure your app to use legacy features (and not take advantage of accessibility features) if it targets .NET Framework 4.7.1 or later.</span></span> <span data-ttu-id="d737f-111">每個包含協助工具功能的 .NET Framework 版本都有一個版本特定的協助工具參數，您可以將其新增至 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 應用程式佈建檔區段中的元素。</span><span class="sxs-lookup"><span data-stu-id="d737f-111">Each .NET Framework version that includes accessibility features has a version-specific accessibility switch, which you add to the [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element in the [`<runtime>`](../configure-apps/file-schema/runtime/index.md) section of the application's configuration file.</span></span> <span data-ttu-id="d737f-112">以下是支援的參數：</span><span class="sxs-lookup"><span data-stu-id="d737f-112">The following are the supported switches:</span></span>

|<span data-ttu-id="d737f-113">版本</span><span class="sxs-lookup"><span data-stu-id="d737f-113">Version</span></span>|<span data-ttu-id="d737f-114">參數</span><span class="sxs-lookup"><span data-stu-id="d737f-114">Switch</span></span>|
|---|---|
|<span data-ttu-id="d737f-115">.NET Framework 4.7.1</span><span class="sxs-lookup"><span data-stu-id="d737f-115">.NET Framework 4.7.1</span></span>|<span data-ttu-id="d737f-116">"Switch.UseLegacyAccessibilityFeatures"</span><span class="sxs-lookup"><span data-stu-id="d737f-116">"Switch.UseLegacyAccessibilityFeatures"</span></span>|
|<span data-ttu-id="d737f-117">.NET Framework 4.7.2</span><span class="sxs-lookup"><span data-stu-id="d737f-117">.NET Framework 4.7.2</span></span>|<span data-ttu-id="d737f-118">"Switch.UseLegacyAccessibilityFeatures.2"</span><span class="sxs-lookup"><span data-stu-id="d737f-118">"Switch.UseLegacyAccessibilityFeatures.2"</span></span>|
|<span data-ttu-id="d737f-119">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="d737f-119">.NET Framework 4.8</span></span>|<span data-ttu-id="d737f-120">"Switch.UseLegacyAccessibilityFeatures.3"</span><span class="sxs-lookup"><span data-stu-id="d737f-120">"Switch.UseLegacyAccessibilityFeatures.3"</span></span>|
|<span data-ttu-id="d737f-121">2020年8月11日-KB4569746 .NET Framework 4.8 的累積更新</span><span class="sxs-lookup"><span data-stu-id="d737f-121">August 11, 2020-KB4569746 Cumulative Update for .NET Framework 4.8</span></span>|<span data-ttu-id="d737f-122">"UseLegacyAccessibilityFeatures. 4"</span><span class="sxs-lookup"><span data-stu-id="d737f-122">"Switch.UseLegacyAccessibilityFeatures.4"</span></span>|

### <a name="taking-advantage-of-accessibility-enhancements"></a><span data-ttu-id="d737f-123">利用協助工具增強功能</span><span class="sxs-lookup"><span data-stu-id="d737f-123">Taking advantage of accessibility enhancements</span></span>

<span data-ttu-id="d737f-124">針對以 .NET Framework 4.7.1 或更新版本為目標的應用程式，預設會啟用新的協助工具功能。</span><span class="sxs-lookup"><span data-stu-id="d737f-124">The new accessibility features are enabled by default for applications that target .NET Framework 4.7.1 or later.</span></span> <span data-ttu-id="d737f-125">此外，以舊版 .NET Framework 為目標但在 .NET Framework 4.7.1 或更新版本上執行的應用程式可以選擇不使用舊版的協助工具 (行為，藉由 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 在應用程式佈建檔區段的元素中加入參數，並將其值設定為，以利用) 的協助工具改進 `false` 。</span><span class="sxs-lookup"><span data-stu-id="d737f-125">In addition, applications that target an earlier version of the .NET Framework but are running on .NET Framework 4.7.1 or later can opt out of legacy accessibility behaviors (and thereby take advantage of accessibility improvements) by adding switches to the [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element in the [`<runtime>`](../configure-apps/file-schema/runtime/index.md) section of the application's configuration file and setting their value to `false`.</span></span> <span data-ttu-id="d737f-126">下列程式碼片段說明如何加入宣告 .NET Framework 4.7.1 中引進的協助工具增強功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-126">The following snippet shows how to opt in to the accessibility enhancements that were introduced in .NET Framework 4.7.1:</span></span>

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
</runtime>
```

<span data-ttu-id="d737f-127">如果您選擇在稍後的 .NET Framework 版本中加入宣告協助工具功能，您也必須明確地加入舊版的功能。</span><span class="sxs-lookup"><span data-stu-id="d737f-127">If you choose to opt in to accessibility features in a later .NET Framework version, you must also explicitly opt in to the features from earlier versions.</span></span> <span data-ttu-id="d737f-128">若要設定您的應用程式以利用 .NET Framework 4.7.1 和4.7.2 中的協助工具改善，請新增下列 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素：</span><span class="sxs-lookup"><span data-stu-id="d737f-128">To configure your app to take advantage of accessibility improvements in both .NET Framework 4.7.1 and 4.7.2, add the the following [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element:</span></span>

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false" />
</runtime>
```

<span data-ttu-id="d737f-129">若要將您的應用程式設定為利用 .NET Framework 4.7.1、4.7.2、4.8 和2020年8月累積 4.8 .NET Framework 更新的協助工具改善，請新增下列 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 元素：</span><span class="sxs-lookup"><span data-stu-id="d737f-129">To configure your app to take advantage of accessibility improvements in .NET Framework 4.7.1, 4.7.2, 4.8, and the August 2020 cumulative update for .NET Framework 4.8, add the following [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element:</span></span>

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value=Switch.UseLegacyAccessibilityFeatures=false|Switch.UseLegacyAccessibilityFeatures.2=false|Switch.UseLegacyAccessibilityFeatures.3=false|Switch.UseLegacyAccessibilityFeatures.4=false"/>
</runtime>
```

### <a name="restoring-legacy-behavior"></a><span data-ttu-id="d737f-130">還原舊版行為</span><span class="sxs-lookup"><span data-stu-id="d737f-130">Restoring legacy behavior</span></span>

<span data-ttu-id="d737f-131">以4.7.1 開頭之 .NET Framework 版本的應用程式可以停用協助工具功能，方法是將參數加入至 [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) [`<runtime>`](../configure-apps/file-schema/runtime/index.md) 應用程式佈建檔區段中的專案，並將其值設定為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="d737f-131">Applications that target versions of .NET Framework starting with 4.7.1 can disable accessibility features by adding switches to the [`<AppContextSwitchOverrides>`](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) element in the [`<runtime>`](../configure-apps/file-schema/runtime/index.md) section of the application's configuration file and setting their value to `true`.</span></span> <span data-ttu-id="d737f-132">例如，下列組態會選擇退出 .NET Framework 4.7.2 中引進的協助工具功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-132">For example, the following configuration opts out of accessibility features introduced in .NET Framework 4.7.2:</span></span>

```xml
<runtime>
    <!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true|false;key2=true|false  -->
    <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures.2=true" />
</runtime>
```

## <a name="whats-new-in-accessibility-in-the-august-11-2020-cumulative-update-for-net-framework-48"></a><span data-ttu-id="d737f-133">2020年8月11日的協助工具新功能，.NET Framework 4.8 的累積更新</span><span class="sxs-lookup"><span data-stu-id="d737f-133">What's new in accessibility in the August 11, 2020 Cumulative Update for .NET Framework 4.8</span></span>

<span data-ttu-id="d737f-134">2020年8月11日 KB4569746 .NET Framework 4.8 的累積更新包含 Windows Forms 中的新協助工具功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-134">The August 11, 2020-KB4569746 Cumulative Update for .NET Framework 4.8 includes new accessibility features in Windows Forms:</span></span>

- <span data-ttu-id="d737f-135">解決通知 `PropertyGrid` 控制項專案的問題，以及螢幕讀取器的類別展開/折迭狀態。</span><span class="sxs-lookup"><span data-stu-id="d737f-135">Addresses an issue with announcing `PropertyGrid` control items and a category's expanded/collapsed state by screen readers.</span></span>

- <span data-ttu-id="d737f-136">更新 `PropertyGrid` 控制項和其內部元素的可存取模式。</span><span class="sxs-lookup"><span data-stu-id="d737f-136">Updates the accessible patterns of the `PropertyGrid` control and its inner elements.</span></span>

- <span data-ttu-id="d737f-137">更新控制項內部專案的可存取名稱， `PropertyGrid` 讓螢幕讀取器正確地宣告這些專案。</span><span class="sxs-lookup"><span data-stu-id="d737f-137">Updates the accessible names of the `PropertyGrid` control inner elements so they're correctly announced by screen readers.</span></span>

- <span data-ttu-id="d737f-138">定址控制項的周框矩形可存取屬性 `PropertyGridView` 。</span><span class="sxs-lookup"><span data-stu-id="d737f-138">Addresses bounding rectangle accessible properties for the `PropertyGridView` controls.</span></span>

- <span data-ttu-id="d737f-139">讓螢幕讀取器正確宣佈下拉式列示方塊資料格的展開/折迭狀態 `DataGridView` 。</span><span class="sxs-lookup"><span data-stu-id="d737f-139">Enables screen readers to correctly announce the expanded/collapsed state of `DataGridView` combo box cells.</span></span>

## <a name="whats-new-in-accessibility-in-net-framework-48"></a><span data-ttu-id="d737f-140">.NET Framework 4.8 協助工具的新功能</span><span class="sxs-lookup"><span data-stu-id="d737f-140">What's new in accessibility in .NET Framework 4.8</span></span>

<span data-ttu-id="d737f-141">.NET Framework 4.8 包含下列領域的新協助工具功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-141">.NET Framework 4.8 includes new accessibility features in the following areas:</span></span>

- [<span data-ttu-id="d737f-142">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="d737f-142">Windows Forms</span></span>](#winforms48)

- [<span data-ttu-id="d737f-143">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-143">Windows Presentation Foundation (WPF)</span></span>](#wpf48)

- [<span data-ttu-id="d737f-144">Windows Workflow Foundation (WF) 工作流程設計工具</span><span class="sxs-lookup"><span data-stu-id="d737f-144">Windows Workflow Foundation (WF) workflow designer</span></span>](#wf48)

<a name="winforms48"></a>

### <a name="windows-forms"></a><span data-ttu-id="d737f-145">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="d737f-145">Windows Forms</span></span>

<span data-ttu-id="d737f-146">在 .NET Framework 4.8 中，Windows Forms 已新增對許多常用控制項的 LiveRegions 和通知事件支援。</span><span class="sxs-lookup"><span data-stu-id="d737f-146">In .NET Framework 4.8, Windows Forms adds support for LiveRegions and Notification Events to many commonly used controls.</span></span> <span data-ttu-id="d737f-147">它也新增當使用者利用鍵盤巡覽至控制項時的工具提示支援。</span><span class="sxs-lookup"><span data-stu-id="d737f-147">It also adds support for ToolTips when a user navigates to a control by using the keyboard.</span></span>

<span data-ttu-id="d737f-148">**標籤與 StatusStrips 中的 UIA LiveRegions 支援**</span><span class="sxs-lookup"><span data-stu-id="d737f-148">**UIA LiveRegions Support in Labels and StatusStrips**</span></span>

<span data-ttu-id="d737f-149">UIA LiveRegions 可讓應用程式開發人員將控制項中的文字變更 (位於使用者正在處理的位置以外) 通知螢幕助讀程式。</span><span class="sxs-lookup"><span data-stu-id="d737f-149">UIA LiveRegions allow application developers to notify screen readers of a text change in a control that is located apart from the location where the user is working.</span></span> <span data-ttu-id="d737f-150">例如，對於顯示連線狀態的 <xref:System.Windows.Forms.StatusStrip> 控制項，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="d737f-150">This is useful, for example, for a <xref:System.Windows.Forms.StatusStrip> control that shows a connection status.</span></span> <span data-ttu-id="d737f-151">當連線中斷且狀態變更時，開發人員可能需要通知螢幕助讀程式。</span><span class="sxs-lookup"><span data-stu-id="d737f-151">If the connection is dropped and the status changes, the developer might want to notify the screen reader.</span></span>

<span data-ttu-id="d737f-152">從 .NET Framework 4.8 開始，Windows Forms 即針對 <xref:System.Windows.Forms.Label> 和 <xref:System.Windows.Forms.StatusStrip> 這兩個控制項實作 UIA LiveRegions。</span><span class="sxs-lookup"><span data-stu-id="d737f-152">Starting with .NET Framework 4.8, Windows Forms implements UIA LiveRegions for both the <xref:System.Windows.Forms.Label> and <xref:System.Windows.Forms.StatusStrip> controls.</span></span> <span data-ttu-id="d737f-153">例如，下列程式碼會在名為 `label1` 的 <xref:System.Windows.Forms.Label> 控制項中使用 LiveRegion：</span><span class="sxs-lookup"><span data-stu-id="d737f-153">For example, the following code uses the LiveRegion in a <xref:System.Windows.Forms.Label> control named `label1`:</span></span>

```csharp
public Form1()
{
   InitializeComponent();
   label1.AutomationLiveSetting = AutomationLiveSetting.Polite;
}

…
Label1.Text = “Ready!”;
```

<span data-ttu-id="d737f-154">不論使用者與應用程式互動的位置為何，朗讀程式均會播報「就緒」。</span><span class="sxs-lookup"><span data-stu-id="d737f-154">Narrator announces “Ready” regardless of where the user is interacting with the application.</span></span>

<span data-ttu-id="d737f-155">您也可以將您的 <xref:System.Windows.Forms.UserControl> 實作為 LiveRegion：</span><span class="sxs-lookup"><span data-stu-id="d737f-155">You can also implement your <xref:System.Windows.Forms.UserControl> as a LiveRegion:</span></span>

```csharp
using System;
using System.Windows.Forms;
using System.Windows.Forms.Automation;

namespace WindowsFormsApplication
{
   public partial class UserControl1 : UserControl, IAutomationLiveRegion
   {
      public UserControl1()
      {
         InitializeComponent();
      }

      public AutomationLiveSetting AutomationLiveSetting { get; set; }
      private AutomationLiveSetting IAutomationLiveRegion.GetLiveSetting()
      {
         return this.AutomationLiveSetting;
      }

      protected override void OnTextChanged(EventArgs e)
      {
         base.OnTextChanged(e);
         AutomationNotifications.UiaRaiseLiveRegionChangedEvent(this.AccessibilityObject);
      }
   }
}
```

<span data-ttu-id="d737f-156">**UIA 通知事件**</span><span class="sxs-lookup"><span data-stu-id="d737f-156">**UIA notification events**</span></span>

<span data-ttu-id="d737f-157">Windows 10 Fall Creators Update 中引進了 UIA 通知事件，其可讓您的應用程式引發 UIA 事件，並讓朗讀程式只依據您提供的事件文字來播報，而不需要在 UI 中具備對應的控制項。</span><span class="sxs-lookup"><span data-stu-id="d737f-157">The UIA Notification event, introduced in Windows 10 Fall Creators Update, allows your app to raise a UIA event, which leads to Narrator simply making an announcement based on text you supply with the event, without the need to have a corresponding control in the UI.</span></span> <span data-ttu-id="d737f-158">在某些情況下，這是大幅改善應用程式協助工具的直接方法。</span><span class="sxs-lookup"><span data-stu-id="d737f-158">In some scenarios, this is a straightforward way to dramatically improve the accessibility of your app.</span></span> <span data-ttu-id="d737f-159">它也可以用來通知可能需要長時間處理的程序進度。</span><span class="sxs-lookup"><span data-stu-id="d737f-159">In can also be useful to notify of the progress of some process that may take a long time.</span></span> <span data-ttu-id="d737f-160">如需 UIA 通知事件的詳細資訊，請參閱 [Can your desktop app leverage the new UI Notification event?](/archive/blogs/winuiautomation/can-your-desktop-app-leverage-the-new-uia-notification-event-in-order-to-have-narrator-say-exactly-what-your-customers-need) (傳統型應用程式可以利用新的 UI 通知事件嗎？)</span><span class="sxs-lookup"><span data-stu-id="d737f-160">For more information about UIA Notification Events, see [Can your desktop app leverage the new UI Notification event?](/archive/blogs/winuiautomation/can-your-desktop-app-leverage-the-new-uia-notification-event-in-order-to-have-narrator-say-exactly-what-your-customers-need).</span></span>

<span data-ttu-id="d737f-161">下列範例會引發[通知事件](xref:System.Windows.Forms.AccessibleObject.RaiseAutomationNotification%2A)：</span><span class="sxs-lookup"><span data-stu-id="d737f-161">The following example raises the [Notification event](xref:System.Windows.Forms.AccessibleObject.RaiseAutomationNotification%2A):</span></span>

```csharp
MethodInfo raiseMethod = typeof(AccessibleObject).GetMethod("RaiseAutomationNotification");
if (raiseMethod != null) {
   raiseMethod.Invoke(progressBar1.AccessibilityObject, new object[3] {/*Other*/ 4, /*All*/ 2, "The progress is 50%." });
}
```

<span data-ttu-id="d737f-162">**鍵盤存取的工具提示**</span><span class="sxs-lookup"><span data-stu-id="d737f-162">**ToolTips on keyboard access**</span></span>

<span data-ttu-id="d737f-163">在目標為 .NET Framework 4.7.2 和更早版本的應用程式中，只有將滑鼠指標移到控制項中才會觸發跳出該控制項的[工具提示](xref:System.Windows.Forms.ToolTip)。</span><span class="sxs-lookup"><span data-stu-id="d737f-163">In applications that target .NET Framework 4.7.2 and earlier versions, a control [tooltip](xref:System.Windows.Forms.ToolTip) can only be triggered to pop up by moving a mouse pointer into the control.</span></span> <span data-ttu-id="d737f-164">從 .NET Framework 4.8 開始，鍵盤使用者可以使用 Tab 鍵或方向鍵（不論是否有輔助按鍵）來將控制項放在一起，以觸發控制項的工具提示。</span><span class="sxs-lookup"><span data-stu-id="d737f-164">Starting with .NET Framework 4.8, a keyboard user can trigger a control's tooltip by focusing the control using a Tab key or arrow keys with or without modifier keys.</span></span> <span data-ttu-id="d737f-165">這個特定協助工具增強功能需要額外的 [AppContext 參數](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)：</span><span class="sxs-lookup"><span data-stu-id="d737f-165">This particular accessibility enhancement requires an additional [AppContext switch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1"/>
   </startup>
   <runtime>
      <!-- AppContextSwitchOverrides values are in the form of 'key1=true|false;key2=true|false  -->
      <!-- Please note that disabling Switch.UseLegacyAccessibilityFeatures, Switch.UseLegacyAccessibilityFeatures.2 and Switch.UseLegacyAccessibilityFeatures.3 is required to disable Switch.System.Windows.Forms.UseLegacyToolTipDisplay -->
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.System.Windows.Forms.UseLegacyToolTipDisplay=false"/>
   </runtime>
</configuration>
```

<span data-ttu-id="d737f-166">下圖顯示當使用者以鍵盤選取按鈕時的工具提示。</span><span class="sxs-lookup"><span data-stu-id="d737f-166">The following figure shows the tooltip when the user has selected a button with the keyboard.</span></span>

![當使用者使用鍵盤流覽至按鈕時，工具提示的螢幕擷取畫面。](./media/whats-new-in-accessibility/select-tooltip-with-keyboard.png)

<a name="wpf48"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="d737f-168">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-168">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="d737f-169">從 .NET Framework 4.8 開始，WPF 包含許多協助工具改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-169">Starting with .NET Framework 4.8, WPF includes a number of accessibility improvements.</span></span>

<span data-ttu-id="d737f-170">**螢幕朗讀程式不再播報含摺疊或隱藏可見度的項目**</span><span class="sxs-lookup"><span data-stu-id="d737f-170">**Screen narrators no longer announce elements with Collapsed or Hidden visibility**</span></span>

<span data-ttu-id="d737f-171">螢幕朗讀程式不會再播報含摺疊或隱藏可見度的項目。</span><span class="sxs-lookup"><span data-stu-id="d737f-171">Elements with collapsed or hidden visibility are no longer announced by screen reader.</span></span> <span data-ttu-id="d737f-172">如果使用者介面包含的項目可見度為 <xref:System.Windows.Visibility.Collapsed?displayProperty=nameWithType> 或 <xref:System.Windows.Visibility.Hidden?displayProperty=nameWithType>，則螢幕助讀程式向使用者播報時可能會表達錯誤。</span><span class="sxs-lookup"><span data-stu-id="d737f-172">User interfaces that contain elements with a Visibility of <xref:System.Windows.Visibility.Collapsed?displayProperty=nameWithType> or <xref:System.Windows.Visibility.Hidden?displayProperty=nameWithType> can be misrepresented by screen readers if they are announced to the user.</span></span> <span data-ttu-id="d737f-173">從 .NET Framework 4.8 開始，WPF 的 UIAutomation 樹狀結構控制項檢視中不會再包含摺疊或隱藏項目，因此螢幕助讀程式即無法再播報這些項目。</span><span class="sxs-lookup"><span data-stu-id="d737f-173">Starting with .NET Framework 4.8, WPF no longer includes collapsed or hidden elements in the Control View of the UIAutomation tree, so the screen readers can no longer announce these elements.</span></span>

<span data-ttu-id="d737f-174">**搭配使用非 Adorner 文字選取範圍的 SelectionTextBrush 屬性**</span><span class="sxs-lookup"><span data-stu-id="d737f-174">**SelectionTextBrush property for use with non-Adorner based text selection**</span></span>

<span data-ttu-id="d737f-175">在 .NET Framework 4.7.2 中，WPF 新增了在 <xref:System.Windows.Controls.TextBox> <xref:System.Windows.Controls.PasswordBox> 不使用裝飾項層的情況下繪製和文字選取的功能。</span><span class="sxs-lookup"><span data-stu-id="d737f-175">In .NET Framework 4.7.2, WPF added the ability to draw <xref:System.Windows.Controls.TextBox> and <xref:System.Windows.Controls.PasswordBox> text selection without using the Adorner layer.</span></span> <span data-ttu-id="d737f-176">在此案例中，選取文字的前景色彩取決於 <xref:System.Windows.SystemColors.HighlightTextBrush?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="d737f-176">The foreground color of the selected text in this scenario was dictated by <xref:System.Windows.SystemColors.HighlightTextBrush?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="d737f-177">.NET Framework 4.8 新增 `SelectionTextBrush` 屬性，可讓開發人員在使用非 Adorner 文字選取範圍時，針對選取的文字選取特定筆刷。</span><span class="sxs-lookup"><span data-stu-id="d737f-177">.NET Framework 4.8 adds a new property, `SelectionTextBrush`, that allows developers to select the specific brush for the selected text when using non-Adorner based text selection.</span></span> <span data-ttu-id="d737f-178">此屬性僅適用於 WPF 應用程式 (已啟用非 Adorner 文字選取範圍) 中 <xref:System.Windows.Controls.Primitives.TextBoxBase> 衍生的控制項和 <xref:System.Windows.Controls.PasswordBox> 控制項。</span><span class="sxs-lookup"><span data-stu-id="d737f-178">This property works only on <xref:System.Windows.Controls.Primitives.TextBoxBase>-derived controls and the <xref:System.Windows.Controls.PasswordBox> control in WPF applications with non-Adorner-based text selection enabled.</span></span> <span data-ttu-id="d737f-179">此屬性不適用於 <xref:System.Windows.Controls.RichTextBox> 控制項。</span><span class="sxs-lookup"><span data-stu-id="d737f-179">It does not work on the <xref:System.Windows.Controls.RichTextBox> control.</span></span> <span data-ttu-id="d737f-180">如果未啟用非 Adorner 文字選取範圍，則會忽略這個屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-180">If non-Adorner-based text selection is not enabled, this property is ignored.</span></span>

<span data-ttu-id="d737f-181">若要使用這個屬性，只要將它新增至您的 XAML 程式碼，並使用適當的筆刷或繫結即可。</span><span class="sxs-lookup"><span data-stu-id="d737f-181">To use this property, simply add it to your XAML code and use the appropriate brush or binding.</span></span> <span data-ttu-id="d737f-182">產生的文字選取範圍看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d737f-182">The resulting text selection looks like this:</span></span>

![使用 Hello World 選取的文字來執行應用程式的螢幕擷取畫面。](./media/whats-new-in-accessibility/selectiontextbrush-property.png)

<span data-ttu-id="d737f-184">您可以結合 `SelectionBrush` 和 `SelectionTextBrush` 屬性的用法，視需要產生任何背景和前景色彩的組合。</span><span class="sxs-lookup"><span data-stu-id="d737f-184">You can combine the use of the `SelectionBrush` and `SelectionTextBrush` properties to generate any background and foreground color combination that you deem appropriate.</span></span>

<span data-ttu-id="d737f-185">**支援 UIAutomation ControllerFor 屬性**</span><span class="sxs-lookup"><span data-stu-id="d737f-185">**Support for the UIAutomation ControllerFor property**</span></span>

<span data-ttu-id="d737f-186">UIAutomation 的 `ControllerFor` 屬性會傳回自動化項目的陣列，而這些項目是由支援此屬性的自動化項目所操作。</span><span class="sxs-lookup"><span data-stu-id="d737f-186">UIAutomation’s `ControllerFor` property returns an array of automation elements that are manipulated by the automation element that supports this property.</span></span> <span data-ttu-id="d737f-187">此屬性通常用於自動建議的協助工具。</span><span class="sxs-lookup"><span data-stu-id="d737f-187">This property is commonly used for Auto-suggest accessibility.</span></span> <span data-ttu-id="d737f-188">當自動化項目會影響應用程式 UI 或桌面的一或多個區段時，請使用 `ControllerFor`。</span><span class="sxs-lookup"><span data-stu-id="d737f-188">`ControllerFor` is used when an automation element affects one or more segments of the application UI or the desktop.</span></span> <span data-ttu-id="d737f-189">否則，您很難將控制作業的影響與 UI 項目建立關聯。</span><span class="sxs-lookup"><span data-stu-id="d737f-189">Otherwise, it is hard to associate the impact of the control operation with UI elements.</span></span> <span data-ttu-id="d737f-190">這項功能讓控制項能夠提供 `ControllerFor` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="d737f-190">This feature adds the ability for controls to provide a value for the `ControllerFor` property.</span></span>

<span data-ttu-id="d737f-191">.NET Framework 4.8 新增新的虛擬方法 <xref:System.Windows.Automation.Peers.AutomationPeer.GetControlledPeersCore?displayProperty=nameWithType?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="d737f-191">.NET Framework 4.8 adds a new virtual method, <xref:System.Windows.Automation.Peers.AutomationPeer.GetControlledPeersCore?displayProperty=nameWithType?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-192">若要提供 `ControllerFor` 屬性值，只要覆寫這個方法，並傳回控制項 (由此 <xref:System.Windows.Automation.Peers.AutomationPeer> 操作) 的 `List<AutomationPeer>` 即可：</span><span class="sxs-lookup"><span data-stu-id="d737f-192">To provide a value for the `ControllerFor` property, simply override this method and return a `List<AutomationPeer>` for the controls being manipulated by this <xref:System.Windows.Automation.Peers.AutomationPeer>:</span></span>

```csharp
public class AutoSuggestTextBox: TextBox
{
   protected override AutomationPeer OnCreateAutomationPeer()
   {
      return new AutoSuggestTextBoxAutomationPeer(this);
   }

   public ListBox SuggestionListBox;
}

internal class AutoSuggestTextBoxAutomationPeer : TextBoxAutomationPeer
{
   public AutoSuggestTextBoxAutomationPeer(AutoSuggestTextBox owner) : base(owner)
   {
   }

   protected override List<AutomationPeer> GetControlledPeersCore()
   {
      List<AutomationPeer> controlledPeers = new List<AutomationPeer>();
      AutoSuggestTextBox owner = Owner as AutoSuggestTextBox;
      controlledPeers.Add(UIElementAutomationPeer.CreatePeerForElement(owner.SuggestionListBox));
      return controlledPeers;
   }
}
```

<span data-ttu-id="d737f-193">**鍵盤存取的工具提示**</span><span class="sxs-lookup"><span data-stu-id="d737f-193">**Tooltips on keyboard access**</span></span>

<span data-ttu-id="d737f-194">在 .NET Framework 4.7.2 和更早版本中，只有當使用者將滑鼠游標停留在控制項上方時會顯示工具提示。</span><span class="sxs-lookup"><span data-stu-id="d737f-194">In .NET Framework 4.7.2 and earlier versions, tooltips display only when the user hovers the mouse cursor over a control.</span></span> <span data-ttu-id="d737f-195">在 .NET Framework 4.8 中，工具提示也會在鍵盤焦點上顯示，以及透過鍵盤快速鍵顯示。</span><span class="sxs-lookup"><span data-stu-id="d737f-195">In .NET Framework 4.8, tooltips also display on keyboard focus, as well as via a keyboard shortcut.</span></span>

<span data-ttu-id="d737f-196">若要啟用這項功能，應用程式需要以 .NET Framework 4.8 為目標，或使用 `Switch.UseLegacyAccessibilityFeatures.3` 和 `Switch.UseLegacyToolTipDisplay` [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 參數選擇加入。</span><span class="sxs-lookup"><span data-stu-id="d737f-196">To enable this feature, an application needs to target .NET Framework 4.8 or opt-in by using the `Switch.UseLegacyAccessibilityFeatures.3` and `Switch.UseLegacyToolTipDisplay` [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) switches.</span></span> <span data-ttu-id="d737f-197">下列是範例應用程式組態檔：</span><span class="sxs-lookup"><span data-stu-id="d737f-197">The following is a sample application configuration file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false;Switch.UseLegacyToolTipDisplay=false" />
   </runtime>
</configuration>
```

<span data-ttu-id="d737f-198">啟用之後，一旦控制項取得鍵盤焦點時，所有包含工具提示的控制項會都顯示工具提示。</span><span class="sxs-lookup"><span data-stu-id="d737f-198">Once enabled, all controls that contain a tooltip display it once the control receives keyboard focus.</span></span> <span data-ttu-id="d737f-199">工具提示可能會隨著時間或鍵盤焦點變更而關閉。</span><span class="sxs-lookup"><span data-stu-id="d737f-199">The tooltip can be dismissed over time or when the keyboard focus changes.</span></span> <span data-ttu-id="d737f-200">使用者也可以使用新的鍵盤快速鍵 Ctrl + Shift + F10，手動關閉工具提示。</span><span class="sxs-lookup"><span data-stu-id="d737f-200">Users can also dismiss the tooltip manually by using a new keyboard shortcut, Ctrl + Shift + F10.</span></span> <span data-ttu-id="d737f-201">工具提示關閉之後，您可以使用相同的鍵盤快速鍵使其再次顯示。</span><span class="sxs-lookup"><span data-stu-id="d737f-201">Once the tooltip has been dismissed it can be displayed again by using the same keyboard shortcut.</span></span>

> [!NOTE]
> <span data-ttu-id="d737f-202"><xref:System.Windows.Controls.Ribbon.Ribbon> 控制項上的[功能區工具提示](xref:System.Windows.Controls.Ribbon.RibbonToolTip)不會顯示在鍵盤焦點上；而只能透過鍵盤快速鍵顯示。</span><span class="sxs-lookup"><span data-stu-id="d737f-202">[Ribbon tooltips](xref:System.Windows.Controls.Ribbon.RibbonToolTip) on <xref:System.Windows.Controls.Ribbon.Ribbon> controls won’t show on keyboard focus; they only show via the keyboard shortcut.</span></span>

<span data-ttu-id="d737f-203">**新增支援 SizeOfSet 和 PositionInSet UIAutomation 屬性**</span><span class="sxs-lookup"><span data-stu-id="d737f-203">**Added Support for SizeOfSet and PositionInSet UIAutomation properties**</span></span>

<span data-ttu-id="d737f-204">Windows 10 引進 `SizeOfSet` 和 `PositionInSet` 這兩個新的 UIAutomation 屬性；應用程式會使用該屬性來描述集合中的項目計數。</span><span class="sxs-lookup"><span data-stu-id="d737f-204">Windows 10 introduced two new UIAutomation properties, `SizeOfSet` and `PositionInSet`, which are used by applications to describe the count of items in a set.</span></span> <span data-ttu-id="d737f-205">UIAutomation 用戶端應用程式 (例如螢幕助讀程式) 可以查詢應用程式的這些屬性，並播報應用程式 UI 的精確呈現。</span><span class="sxs-lookup"><span data-stu-id="d737f-205">UIAutomation client applications such as screen readers can then query an application for these properties and announce an accurate representation of the application’s UI.</span></span>

<span data-ttu-id="d737f-206">從 .NET Framework 4.8 開始，WPF 會將這兩個屬性公開至 WPF 應用程式中的 UIAutomation。</span><span class="sxs-lookup"><span data-stu-id="d737f-206">Starting with .NET Framework 4.8, WPF  exposes these two properties to UIAutomation in WPF applications.</span></span> <span data-ttu-id="d737f-207">這可由下列兩種方法來完成：</span><span class="sxs-lookup"><span data-stu-id="d737f-207">This can be accomplished in two ways:</span></span>

- <span data-ttu-id="d737f-208">藉由使用相依性屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-208">By using dependency properties.</span></span>

  <span data-ttu-id="d737f-209">WPF 新增 <xref:System.Windows.Automation.AutomationProperties.SizeOfSet?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationProperties.PositionInSet?displayProperty=nameWithType> 這兩個新的相依性屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-209">WPF adds two new dependency properties, <xref:System.Windows.Automation.AutomationProperties.SizeOfSet?displayProperty=nameWithType> and <xref:System.Windows.Automation.AutomationProperties.PositionInSet?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-210">開發人員可以使用 XAML 來設定其值：</span><span class="sxs-lookup"><span data-stu-id="d737f-210">A developer can use XAML to set their values:</span></span>

  ```xaml
  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="1">Button 1</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="2">Button 2</Button>

  <Button AutomationProperties.SizeOfSet="3"
    AutomationProperties.PositionInSet="3">Button 3</Button>
  ```

- <span data-ttu-id="d737f-211">藉由覆寫 AutomationPeer 虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="d737f-211">By overriding AutomationPeer virtual methods.</span></span>

  <span data-ttu-id="d737f-212">AutomationPeer 類別已新增 <xref:System.Windows.Automation.Peers.AutomationPeer.GetSizeOfSetCore> 和 <xref:System.Windows.Automation.Peers.AutomationPeer.GetPositionInSetCore> 虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="d737f-212">The <xref:System.Windows.Automation.Peers.AutomationPeer.GetSizeOfSetCore> and <xref:System.Windows.Automation.Peers.AutomationPeer.GetPositionInSetCore> virtual methods been added to the AutomationPeer class.</span></span> <span data-ttu-id="d737f-213">開發人員可以覆寫這些方法來提供 `SizeOfSet` 和 `PositionInSet` 的值，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d737f-213">A developer can provide values for `SizeOfSet` and `PositionInSet` by overriding these methods, as shown in the following example:</span></span>

  ```csharp
  public class MyButtonAutomationPeer : ButtonAutomationPeer
  {
    protected override int GetSizeOfSetCore()
    {
        // Call into your own logic to provide a value for SizeOfSet
        return CalculateSizeOfSet();
    }

    protected override int GetPositionInSetCore()
    {
        // Call into your own logic to provide a value for PositionInSet
        return CalculatePositionInSet();
    }
  }
  ```

<span data-ttu-id="d737f-214">此外，<xref:System.Windows.Controls.ItemsControl> 執行個體中的項目可自動提供這些屬性值，而不需要開發人員的額外動作。</span><span class="sxs-lookup"><span data-stu-id="d737f-214">In addition, items in <xref:System.Windows.Controls.ItemsControl> instances provide a value for these properties automatically without additional action from the developer.</span></span> <span data-ttu-id="d737f-215">如果 <xref:System.Windows.Controls.ItemsControl> 是分組形式，即會以各組來表示群組的集合，並將每個群組計算為個別的一組，而該群組內每個項目均提供其在該群組內的位置及群組大小。</span><span class="sxs-lookup"><span data-stu-id="d737f-215">If an <xref:System.Windows.Controls.ItemsControl> is grouped, the collection of groups is represented as a set, and each group is counted as a separate set, with each item inside that group providing its position inside that group as well as the size of the group.</span></span> <span data-ttu-id="d737f-216">虛擬化不會影響自動值。</span><span class="sxs-lookup"><span data-stu-id="d737f-216">Automatic values are not affected by virtualization.</span></span> <span data-ttu-id="d737f-217">即使某個項目未具現化，系統仍會將其計入集合的總大小，並會影響其同層級項目集合的位置。</span><span class="sxs-lookup"><span data-stu-id="d737f-217">Even if an item is not realized, it is still counted toward the total size of the set and affects the position in the set of its sibling items.</span></span>

<span data-ttu-id="d737f-218">只有在應用程式的目標為 .NET Framework 4.8 時，系統才會提供自動值。</span><span class="sxs-lookup"><span data-stu-id="d737f-218">Automatic values are only provided if the application targets .NET Framework 4.8.</span></span> <span data-ttu-id="d737f-219">若是以舊版 .NET Framework 為目標的應用程式，您可以設定 `Switch.UseLegacyAccessibilityFeatures.3` [AppContext 參數](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)，如下列 App.config 檔案中所示：</span><span class="sxs-lookup"><span data-stu-id="d737f-219">For applications that target an earlier version of the .NET Framework, you can set the `Switch.UseLegacyAccessibilityFeatures.3` [AppContext switch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md), as shown in the following App.config file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
   </startup>
   <runtime>
      <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false;Switch.UseLegacyAccessibilityFeatures.2=false;Switch.UseLegacyAccessibilityFeatures.3=false" />
   </runtime>
</configuration>
```

<a name="wf48"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a><span data-ttu-id="d737f-220">Windows Workflow Foundation (WF) 工作流程設計工具</span><span class="sxs-lookup"><span data-stu-id="d737f-220">Windows Workflow Foundation (WF) workflow designer</span></span>

<span data-ttu-id="d737f-221">工作流程設計工具包括下列各項 .NET Framework 4.8 的變更：</span><span class="sxs-lookup"><span data-stu-id="d737f-221">The workflow designer includes the following changes in .NET Framework 4.8:</span></span>

- <span data-ttu-id="d737f-222">使用朗讀程式的使用者會看到 FlowSwitch 案例標籤方面的改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-222">Users using Narrator will see improvements in FlowSwitch case labels.</span></span>

- <span data-ttu-id="d737f-223">使用朗讀程式的使用者會看到按鈕描述方面的改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-223">Users using Narrator will see improvements in button descriptions.</span></span>

- <span data-ttu-id="d737f-224">選擇高對比佈景主題之使用者會看到工作流程設計工具和其控制項在可見度方面的改善，例如項目之間的更佳對比比例，以及用於焦點項目的更明顯選取方塊。</span><span class="sxs-lookup"><span data-stu-id="d737f-224">Users who choose High Contrast themes will see improvements in the visibility of the Workflow Designer and its controls, like better contrast ratios between elements and more noticeable selection boxes used for focus elements.</span></span>

<span data-ttu-id="d737f-225">如果應用程式是以 .NET Framework 4.7.2 或更早的版本為目標，您可以將應用程式組態檔中的 `Switch.UseLegacyAccessibilityFeatures.3` [AppContext 參數](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 設為 `false` 來選擇加入這些變更。</span><span class="sxs-lookup"><span data-stu-id="d737f-225">If your application targets .NET Framework 4.7.2 or an earlier version, you can opt into these changes by setting the `Switch.UseLegacyAccessibilityFeatures.3` [AppContext switch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) to `false` in your application configuration file.</span></span> <span data-ttu-id="d737f-226">如需詳細資訊，請參閱本文的[利用協助工具增強功能](#taking-advantage-of-accessibility-enhancements)一節。</span><span class="sxs-lookup"><span data-stu-id="d737f-226">For more information, see the [Taking advantage of accessibility enhancements](#taking-advantage-of-accessibility-enhancements) section in this article.</span></span>

## <a name="whats-new-in-accessibility-in-net-framework-472"></a><span data-ttu-id="d737f-227">.NET Framework 4.7.2 協助工具的新功能</span><span class="sxs-lookup"><span data-stu-id="d737f-227">What's new in accessibility in .NET Framework 4.7.2</span></span>

<span data-ttu-id="d737f-228">.NET Framework 4.7.2 包含下列領域的新協助工具功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-228">.NET Framework 4.7.2 includes new accessibility features in the following areas:</span></span>

- [<span data-ttu-id="d737f-229">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="d737f-229">Windows Forms</span></span>](#winforms472)

- [<span data-ttu-id="d737f-230">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-230">Windows Presentation Foundation (WPF)</span></span>](#wpf472)

<a name="winforms472"></a>

### <a name="windows-forms"></a><span data-ttu-id="d737f-231">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="d737f-231">Windows Forms</span></span>

<span data-ttu-id="d737f-232">**高對比佈景主題中的作業系統定義色彩**</span><span class="sxs-lookup"><span data-stu-id="d737f-232">**OS-defined colors in High Contrast themes**</span></span>

<span data-ttu-id="d737f-233">從 .NET Framework 4.7.2 開始，Windows Forms 在高對比佈景主題中使用作業系統所定義的色彩。</span><span class="sxs-lookup"><span data-stu-id="d737f-233">Starting with .NET Framework 4.7.2, Windows Forms uses colors defined by the operating system in High Contrast themes.</span></span> <span data-ttu-id="d737f-234">這會影響下列控制項：</span><span class="sxs-lookup"><span data-stu-id="d737f-234">This affects the following controls:</span></span>

- <span data-ttu-id="d737f-235"><xref:System.Windows.Forms.ToolStripDropDownButton> 控制項的下拉式箭號。</span><span class="sxs-lookup"><span data-stu-id="d737f-235">The drop-down arrow of the <xref:System.Windows.Forms.ToolStripDropDownButton> control.</span></span>

- <span data-ttu-id="d737f-236"><xref:System.Windows.Forms.ButtonBase.FlatStyle> 設成 <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> 或 <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType> 的 <xref:System.Windows.Forms.Button>、<xref:System.Windows.Forms.RadioButton> 和 <xref:System.Windows.Forms.CheckBox>。</span><span class="sxs-lookup"><span data-stu-id="d737f-236">The <xref:System.Windows.Forms.Button>, <xref:System.Windows.Forms.RadioButton> and <xref:System.Windows.Forms.CheckBox> controls with <xref:System.Windows.Forms.ButtonBase.FlatStyle> set to <xref:System.Windows.Forms.FlatStyle.Flat?displayProperty=nameWithType> or <xref:System.Windows.Forms.FlatStyle.Popup?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-237">以往，選取的文字和背景色彩不會呈現對比，因此難以閱讀。</span><span class="sxs-lookup"><span data-stu-id="d737f-237">Previously, selected text and background colors were not contrasting and were hard to read.</span></span>

- <span data-ttu-id="d737f-238">包含在 <xref:System.Windows.Forms.GroupBox> 內的控制項，且其 <xref:System.Windows.Forms.Control.Enabled> 屬性設定為 `false`。</span><span class="sxs-lookup"><span data-stu-id="d737f-238">Controls contained within a <xref:System.Windows.Forms.GroupBox> that has its <xref:System.Windows.Forms.Control.Enabled> property set to `false`.</span></span>

- <span data-ttu-id="d737f-239"><xref:System.Windows.Forms.ToolStripButton>、<xref:System.Windows.Forms.ToolStripComboBox> 和 <xref:System.Windows.Forms.ToolStripDropDownButton> 控制項，它們在高對比模式下有更高的亮度對比率。</span><span class="sxs-lookup"><span data-stu-id="d737f-239">The <xref:System.Windows.Forms.ToolStripButton>, <xref:System.Windows.Forms.ToolStripComboBox>, and <xref:System.Windows.Forms.ToolStripDropDownButton> controls, which have an increased luminosity contrast ratio in High Contrast Mode.</span></span>

- <span data-ttu-id="d737f-240"><xref:System.Windows.Forms.DataGridViewLinkCell> 的 <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor> 屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-240">The <xref:System.Windows.Forms.DataGridViewLinkCell.LinkColor> property of the <xref:System.Windows.Forms.DataGridViewLinkCell>.</span></span>

<span data-ttu-id="d737f-241">**朗讀程式增強功能**</span><span class="sxs-lookup"><span data-stu-id="d737f-241">**Narrator improvements**</span></span>

<span data-ttu-id="d737f-242">從 .NET Framework 4.7.2 開始，朗讀程式支援的增強功能如下：</span><span class="sxs-lookup"><span data-stu-id="d737f-242">Starting with .NET Framework 4.7.2, Narrator support is enhanced as follows:</span></span>

- <span data-ttu-id="d737f-243">在播報 <xref:System.Windows.Forms.ToolStripMenuItem> 的文字時，現已會播報 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="d737f-243">It announces the value of the <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys?displayProperty=nameWithType> property when announcing the text of a <xref:System.Windows.Forms.ToolStripMenuItem>.</span></span>

- <span data-ttu-id="d737f-244">當 <xref:System.Windows.Forms.ToolStripMenuItem> 的 <xref:System.Windows.Forms.Control.Enabled> 屬性設定為 `false` 時，會指明該情況。</span><span class="sxs-lookup"><span data-stu-id="d737f-244">It indicates when a <xref:System.Windows.Forms.ToolStripMenuItem> has its <xref:System.Windows.Forms.Control.Enabled> property set to `false`.</span></span>

- <span data-ttu-id="d737f-245">當 <xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> 屬性設定為 `true` 時，會提供核取方塊狀態的回應。</span><span class="sxs-lookup"><span data-stu-id="d737f-245">It gives feedback on the state of a check box when the <xref:System.Windows.Forms.ListView.CheckBoxes?displayProperty=nameWithType> property is set to `true`.</span></span>

- <span data-ttu-id="d737f-246">朗讀程式掃描模式的焦點順序，與 ClickOnce 下載對話視窗中所看見的控制項順序已一致。</span><span class="sxs-lookup"><span data-stu-id="d737f-246">Narrator's Scan Mode focus order is consistent with the visual order of the controls on the ClickOnce download dialog window.</span></span>

<span data-ttu-id="d737f-247">**DataGridView 改善**</span><span class="sxs-lookup"><span data-stu-id="d737f-247">**DataGridView improvements**</span></span>

<span data-ttu-id="d737f-248">從 .NET Framework 4.7.2 開始，<xref:System.Windows.Forms.DataGridView> 控制項已經引進下列協助工具改善：</span><span class="sxs-lookup"><span data-stu-id="d737f-248">Starting with .NET Framework 4.7.2, the <xref:System.Windows.Forms.DataGridView> control has introduced the following accessibility improvements:</span></span>

- <span data-ttu-id="d737f-249">資料列可使用鍵盤排序。</span><span class="sxs-lookup"><span data-stu-id="d737f-249">Rows can be sorted using the keyboard.</span></span> <span data-ttu-id="d737f-250">使用者可使用 F3 鍵，依目前的資料行排序。</span><span class="sxs-lookup"><span data-stu-id="d737f-250">A user can use the F3 key in order to sort by the current column.</span></span>

- <span data-ttu-id="d737f-251">當 <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType> 設定為 <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType> 時，資料行標頭會變更色彩，以在目前的資料列中指出使用者滑過儲存格時所在的資料行位置。</span><span class="sxs-lookup"><span data-stu-id="d737f-251">When the <xref:System.Windows.Forms.DataGridView.SelectionMode?displayProperty=nameWithType> is set to <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType>, the column header changes color to indicate the current column as the user tabs through the cells in the current row.</span></span>

- <span data-ttu-id="d737f-252"><xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject?displayProperty=nameWithType> 的 <xref:System.Windows.Forms.AccessibleObject.Parent?displayProperty=nameWithType> 屬性會傳回正確的父控制項。</span><span class="sxs-lookup"><span data-stu-id="d737f-252">The <xref:System.Windows.Forms.AccessibleObject.Parent?displayProperty=nameWithType> property of a  <xref:System.Windows.Forms.DataGridViewLinkCell.DataGridViewLinkCellAccessibleObject?displayProperty=nameWithType> returns the correct parent control.</span></span>

<span data-ttu-id="d737f-253">**改良的視覺提示**</span><span class="sxs-lookup"><span data-stu-id="d737f-253">**Improved visual cues**</span></span>

- <span data-ttu-id="d737f-254"><xref:System.Windows.Forms.ButtonBase.Text> 屬性為空白的控制項 <xref:System.Windows.Forms.RadioButton> 與 <xref:System.Windows.Forms.CheckBox>，會於接收到焦點時顯示焦點指標。</span><span class="sxs-lookup"><span data-stu-id="d737f-254">The <xref:System.Windows.Forms.RadioButton> and <xref:System.Windows.Forms.CheckBox> controls with an empty <xref:System.Windows.Forms.ButtonBase.Text> property  display a focus indicator when they receive the focus.</span></span>

<span data-ttu-id="d737f-255">**已改進屬性方格支援**</span><span class="sxs-lookup"><span data-stu-id="d737f-255">**Improved Property Grid Support**</span></span>

- <span data-ttu-id="d737f-256"><xref:System.Windows.Forms.PropertyGrid> 控制項子項目現在只有在已啟用 PropertyGrid 項目的情況下，才會傳回 <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> 屬性的 `true`。</span><span class="sxs-lookup"><span data-stu-id="d737f-256">The <xref:System.Windows.Forms.PropertyGrid> control child elements now return a `true` for the  <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> property only when a PropertyGrid element is enabled.</span></span>

- <span data-ttu-id="d737f-257"><xref:System.Windows.Forms.PropertyGrid> 控制項子項目只有在使用者可變更 PropertyGrid 項目的情況下，才會傳回 <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> 屬性的 `false`。</span><span class="sxs-lookup"><span data-stu-id="d737f-257">The <xref:System.Windows.Forms.PropertyGrid> control child elements return a `false` for the <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> property only when a PropertyGrid element can be changed by the user.</span></span>

<span data-ttu-id="d737f-258">**改善的鍵盤導覽**</span><span class="sxs-lookup"><span data-stu-id="d737f-258">**Improved keyboard navigation**</span></span>

- <span data-ttu-id="d737f-259"><xref:System.Windows.Forms.ToolStripPanel.TabStop> 屬性設定為 `true` 的 <xref:System.Windows.Forms.ToolStripPanel> 內含焦點時，<xref:System.Windows.Forms.ToolStripButton> 控制項允許焦點</span><span class="sxs-lookup"><span data-stu-id="d737f-259">The <xref:System.Windows.Forms.ToolStripButton> control allows focus when contained within a <xref:System.Windows.Forms.ToolStripPanel> that has the <xref:System.Windows.Forms.ToolStripPanel.TabStop> property set to `true`</span></span>

<a name="wpf472"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="d737f-260">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-260">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="d737f-261">**CheckBox 和 RadioButton 控制項的變更**</span><span class="sxs-lookup"><span data-stu-id="d737f-261">**Changes to the CheckBox and RadioButton controls**</span></span>

<span data-ttu-id="d737f-262">在 .NET Framework 4.7.1 和舊版的傳統和高對比佈景主題中，WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWithType> 和 <xref:System.Windows.Controls.RadioButton?displayProperty=nameWithType> 控制項的焦點視覺效果不一致且不正確。</span><span class="sxs-lookup"><span data-stu-id="d737f-262">In .NET Framework 4.7.1 and earlier versions, the WPF <xref:System.Windows.Controls.CheckBox?displayProperty=nameWithType> and <xref:System.Windows.Controls.RadioButton?displayProperty=nameWithType> controls have inconsistent and, in Classic and High Contrast themes, incorrect focus visuals.</span></span>  <span data-ttu-id="d737f-263">當控制項沒有任何內容集時，會發生上述問題。</span><span class="sxs-lookup"><span data-stu-id="d737f-263">These issues occur in cases where the controls do not have any content set.</span></span>  <span data-ttu-id="d737f-264">這可能會讓人混淆佈景主題之間的轉換，也看不清楚焦點視覺效果。</span><span class="sxs-lookup"><span data-stu-id="d737f-264">This can make the transition between themes confusing and the focus visual hard to see.</span></span>

<span data-ttu-id="d737f-265">現在，.NET Framework 4.7.2 的這些視覺效果在各佈景主題之間會更一致；在傳統和高對比佈景主題中也可以看得更清楚。</span><span class="sxs-lookup"><span data-stu-id="d737f-265">In .NET Framework 4.7.2, these visuals are now more consistent across themes and more easily visible in Classic and High Contrast themes.</span></span>

<span data-ttu-id="d737f-266">**裝載於 WPF 應用程式的 WinForms 控制項**</span><span class="sxs-lookup"><span data-stu-id="d737f-266">**WinForms controls hosted in a WPF application**</span></span>

<span data-ttu-id="d737f-267">針對 .NET Framework 4.7.1 和舊版中裝載於 WPF 應用程式的 WinForms 控制項，如果 WinForms 層的第一個或最後一個控制項是 WPF <xref:System.Windows.Forms.Integration.ElementHost> 控制項，則使用者無法按 Tab 鍵移出該 WinForms 層。</span><span class="sxs-lookup"><span data-stu-id="d737f-267">For WinForms control hosted in a WPF application in .NET Framework 4.7.1 and earlier versions, users couldn't tab out of the WinForms layer if the first or last control in that layer is the WPF <xref:System.Windows.Forms.Integration.ElementHost> control.</span></span> <span data-ttu-id="d737f-268">在 .NET Framework 4.7.2 中，使用者現在能按 Tab 鍵移出 WinForms 層。</span><span class="sxs-lookup"><span data-stu-id="d737f-268">In .NET Framework 4.7.2, users are now able to tab out of the WinForms layer.</span></span>

<span data-ttu-id="d737f-269">不過，依賴焦點絕不會逸出 WinForms 層的自動化應用程式可能不再如預期運作。</span><span class="sxs-lookup"><span data-stu-id="d737f-269">However, automated applications that rely on focus never escaping the WinForms layer may no longer work as expected.</span></span>

## <a name="whats-new-in-accessibility-in-net-framework-471"></a><span data-ttu-id="d737f-270">.NET Framework 4.7.1 協助工具的新功能</span><span class="sxs-lookup"><span data-stu-id="d737f-270">What's new in accessibility in .NET Framework 4.7.1</span></span>

<span data-ttu-id="d737f-271">.NET Framework 4.7.1 包含下列領域的新協助工具功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-271">.NET Framework 4.7.1 includes new accessibility features in the following areas:</span></span>

- [<span data-ttu-id="d737f-272">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-272">Windows Presentation Foundation (WPF)</span></span>](#wpf471)

- [<span data-ttu-id="d737f-273">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="d737f-273">Windows Forms</span></span>](#winforms471)

- [<span data-ttu-id="d737f-274">ASP.NET Web 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-274">ASP.NET web controls</span></span>](#aspnet471)

- [<span data-ttu-id="d737f-275">.NET SDK 工具</span><span class="sxs-lookup"><span data-stu-id="d737f-275">.NET SDK Tools</span></span>](#tools471)

- [<span data-ttu-id="d737f-276">Windows Workflow Foundation (WF) 工作流程設計工具</span><span class="sxs-lookup"><span data-stu-id="d737f-276">Windows Workflow Foundation (WF) Workflow Designer</span></span>](#wf471)

<a name="wpf471"></a>

### <a name="windows-presentation-foundation-wpf"></a><span data-ttu-id="d737f-277">Windows Presentation Foundation (WPF)</span><span class="sxs-lookup"><span data-stu-id="d737f-277">Windows Presentation Foundation (WPF)</span></span>

<span data-ttu-id="d737f-278">**螢幕助讀程式改善**</span><span class="sxs-lookup"><span data-stu-id="d737f-278">**Screen reader improvements**</span></span>

<span data-ttu-id="d737f-279">如果啟用協助工具改善，則 .NET Framework 4.7.1 會包含下列影響螢幕助讀程式的增強功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-279">If accessibility improvements are enabled, .NET Framework 4.7.1 includes the following enhancements that affect screen readers:</span></span>

- <span data-ttu-id="d737f-280">在 .NET Framework 4.7 和舊版本中，螢幕助讀程式會將 <xref:System.Windows.Controls.Expander> 控制項宣告為按鈕。</span><span class="sxs-lookup"><span data-stu-id="d737f-280">In .NET Framework 4.7 and earlier versions, <xref:System.Windows.Controls.Expander> controls were announced by screen readers as buttons.</span></span> <span data-ttu-id="d737f-281">從 .NET Framework 4.7.1 開始，螢幕助讀程式已將它們正確地宣告為可展開/可摺疊的群組。</span><span class="sxs-lookup"><span data-stu-id="d737f-281">Starting with .NET Framework 4.7.1, they are correctly announced as expandable/collapsible groups.</span></span>

- <span data-ttu-id="d737f-282">在 .NET Framework 4.7 和舊版本中，螢幕助讀程式會將 <xref:System.Windows.Controls.DataGridCell> 控制項宣告為「自訂」。</span><span class="sxs-lookup"><span data-stu-id="d737f-282">In .NET Framework 4.7 and earlier versions, <xref:System.Windows.Controls.DataGridCell> controls were announced by screen readers as “custom.”</span></span> <span data-ttu-id="d737f-283">從 .NET Framework 4.7.1 開始，螢幕助讀程式現在已將它們正確地宣告為資料格儲存格 (當地語系化)。</span><span class="sxs-lookup"><span data-stu-id="d737f-283">Starting with .NET Framework 4.7.1, they are now correctly announced as data grid cell (localized).</span></span>

- <span data-ttu-id="d737f-284">從 .NET Framework 4.7.1 開始，螢幕助讀程式會宣告可編輯 <xref:System.Windows.Controls.ComboBox> 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d737f-284">Starting with .NET Framework 4.7.1, screen readers announce the name of an editable <xref:System.Windows.Controls.ComboBox>.</span></span>

- <span data-ttu-id="d737f-285">在 .NET Framework 4.7 和舊版本中，螢幕助讀程式會將 <xref:System.Windows.Controls.PasswordBox> 控制項宣告為「檢視中沒有項目」或具有不正確的行為。</span><span class="sxs-lookup"><span data-stu-id="d737f-285">In .NET Framework 4.7 and earlier versions, <xref:System.Windows.Controls.PasswordBox> controls were announced as “no item in view” or had otherwise incorrect behavior.</span></span> <span data-ttu-id="d737f-286">從 .NET Framework 4.7.1 開始，已修正此問題。</span><span class="sxs-lookup"><span data-stu-id="d737f-286">This issue is fixed starting with .NET Framework 4.7.1.</span></span>

<span data-ttu-id="d737f-287">**UIAutomation LiveRegion 支援**</span><span class="sxs-lookup"><span data-stu-id="d737f-287">**UIAutomation LiveRegion support**</span></span>

<span data-ttu-id="d737f-288">朗讀程式這類螢幕助讀程式可協助人員讀取應用程式 UI 內容，通常是透過具有焦點之 UI 內容的文字轉換語音輸出。</span><span class="sxs-lookup"><span data-stu-id="d737f-288">Screen readers such as Narrator help people read the UI contents of an application, usually by text-to-speech output of the UI content that has the focus.</span></span> <span data-ttu-id="d737f-289">不過，如果 UI 項目變更，而且沒有焦點，則使用者可能不會收到通知，並可能遺失重要資訊。</span><span class="sxs-lookup"><span data-stu-id="d737f-289">However, if a UI element changes and does not have the focus, the user may not be notified and may miss important information.</span></span> <span data-ttu-id="d737f-290">即時區域的目標在解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="d737f-290">Live regions aim at solving this problem.</span></span> <span data-ttu-id="d737f-291">開發人員可以使用它們來通知螢幕助讀程式或任何其他 UIAutomation 用戶端，已對 UI 項目進行重要變更。</span><span class="sxs-lookup"><span data-stu-id="d737f-291">A developer can use them to inform the screen reader or any other UIAutomation client that an important change has been made to a UI element.</span></span> <span data-ttu-id="d737f-292">螢幕助讀程式接著可以決定如何和何時通知使用者已進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="d737f-292">The screen reader can then decide how and when to inform the user of this change.</span></span>

<span data-ttu-id="d737f-293">為了支援即時區域，已將下列 API 新增至 WPF：</span><span class="sxs-lookup"><span data-stu-id="d737f-293">To support live regions, the following APIs have been added to WPF:</span></span>

- <span data-ttu-id="d737f-294"><xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> 欄位，可識別 **LiveSetting** 屬性和 **LiveRegionChanged** 事件。</span><span class="sxs-lookup"><span data-stu-id="d737f-294">The <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveSettingProperty?displayProperty=nameWithType> and <xref:System.Windows.Automation.AutomationElementIdentifiers.LiveRegionChangedEvent?displayProperty=nameWithType> fields, which identify the **LiveSetting** property and the **LiveRegionChanged** event.</span></span> <span data-ttu-id="d737f-295">它們可以使用 XAML 進行設定。</span><span class="sxs-lookup"><span data-stu-id="d737f-295">They can be set by using XAML.</span></span>

- <span data-ttu-id="d737f-296">**AutomationProperties.LiveSetting** 附加屬性，可通知螢幕助讀程式有關 UI 變更對使用者的重要性。</span><span class="sxs-lookup"><span data-stu-id="d737f-296">The **AutomationProperties.LiveSetting** attached property, which informs the screen reader of the importance of the UI change to the user.</span></span>

- <span data-ttu-id="d737f-297"><xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType> 屬性，可識別 **AutomationProperties.LiveSetting** 附加屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-297">The <xref:System.Windows.Automation.AutomationProperties.LiveSettingProperty?displayProperty=nameWithType> property, which identifies the **AutomationProperties.LiveSetting** attached property.</span></span>

- <span data-ttu-id="d737f-298"><xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType> 方法，可以覆寫以提供 **LiveSetting** 值。</span><span class="sxs-lookup"><span data-stu-id="d737f-298">The <xref:System.Windows.Automation.Peers.AutomationPeer.GetLiveSettingCore%2A?displayProperty=nameWithType> method, which can be overridden to provide a **LiveSetting** value.</span></span>

- <span data-ttu-id="d737f-299"><xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType> 和 <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> 方法，可以取得和設定 **LiveSetting** 值。</span><span class="sxs-lookup"><span data-stu-id="d737f-299">The <xref:System.Windows.Automation.AutomationProperties.GetLiveSetting%2A?displayProperty=nameWithType> and <xref:System.Windows.Automation.AutomationProperties.SetLiveSetting%2A?displayProperty=nameWithType> methods, which get and set a **LiveSetting** value.</span></span>

- <span data-ttu-id="d737f-300"><xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType> 列舉，可以定義下列可能的 **LiveSetting** 值：</span><span class="sxs-lookup"><span data-stu-id="d737f-300">The <xref:System.Windows.Automation.AutomationLiveSetting?displayProperty=nameWithType> enumeration, which defines the following possible **LiveSetting** values:</span></span>

  - <span data-ttu-id="d737f-301"><xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="d737f-301"><xref:System.Windows.Automation.AutomationLiveSetting.Off?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-302">如果即時區域的內容變更，項目不會傳送通知。</span><span class="sxs-lookup"><span data-stu-id="d737f-302">The element does not send notifications if the content of the live region has changed.</span></span>
  - <span data-ttu-id="d737f-303"><xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="d737f-303"><xref:System.Windows.Automation.AutomationLiveSetting.Polite?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-304">如果即時區域的內容變更，項目會傳送不中斷通知。</span><span class="sxs-lookup"><span data-stu-id="d737f-304">The element sends non-interruptive notifications if the content of the live region has changed.</span></span>

  - <span data-ttu-id="d737f-305"><xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="d737f-305"><xref:System.Windows.Automation.AutomationLiveSetting.Assertive?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d737f-306">如果即時區域的內容變更，項目會傳送中斷通知。</span><span class="sxs-lookup"><span data-stu-id="d737f-306">The element sends interruptive notifications if the content of the live region has changed.</span></span>

<span data-ttu-id="d737f-307">您可以在感興趣的項目上設定 **AutomationProperties.LiveSetting** 屬性，以建立 LiveRegion，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d737f-307">You can create a LiveRegion by setting the **AutomationProperties.LiveSetting** property on the element of interest, as shown in the following example:</span></span>

```xaml
<TextBlock Name="myTextBlock" AutomationProperties.LiveSetting="Assertive">announcement</TextBlock>
```

<span data-ttu-id="d737f-308">如果即時區域中的資料變更，而且您需要通知螢幕助讀程式，請明確地引發事件，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d737f-308">When the data in the live region changes and you need to inform a screen reader, you explicitly raise an event, as shown in the following sample.</span></span>

```csharp
var peer = FrameworkElementAutomationPeer.FromElement(myTextBlock);

peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged);
```

```vb
Dim peer = FrameworkElementAutomationPeer.FromElement(myTextBlock)
peer.RaiseAutomationEvent(AutomationEvents.LiveRegionChanged)

```

<span data-ttu-id="d737f-309">**High contrast**</span><span class="sxs-lookup"><span data-stu-id="d737f-309">**High contrast**</span></span>

<span data-ttu-id="d737f-310">從 .NET Framework 4.7.1 開始，已對各種 WPF 控制項進行高對比改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-310">Starting with .NET Framework 4.7.1, improvements in high contrast have been made to various WPF controls.</span></span> <span data-ttu-id="d737f-311">現在，設定 <xref:System.Windows.SystemParameters.HighContrast%2A> 佈景主題時，可以看到它們。</span><span class="sxs-lookup"><span data-stu-id="d737f-311">They are now visible when the <xref:System.Windows.SystemParameters.HighContrast%2A> theme is set.</span></span> <span data-ttu-id="d737f-312">其中包含：</span><span class="sxs-lookup"><span data-stu-id="d737f-312">These include:</span></span>

- <span data-ttu-id="d737f-313"><xref:System.Windows.Controls.Expander> 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-313"><xref:System.Windows.Controls.Expander> control</span></span>

  <span data-ttu-id="d737f-314">現在會顯示 <xref:System.Windows.Controls.Expander> 控制項的焦點視覺效果。</span><span class="sxs-lookup"><span data-stu-id="d737f-314">The focus visual for the  <xref:System.Windows.Controls.Expander> control is now visible.</span></span> <span data-ttu-id="d737f-315">現在也會顯示 <xref:System.Windows.Controls.ComboBox>、<xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.RadioButton> 控制項的鍵盤視覺效果。</span><span class="sxs-lookup"><span data-stu-id="d737f-315">The keyboard visuals for <xref:System.Windows.Controls.ComboBox>,<xref:System.Windows.Controls.ListBox>, and <xref:System.Windows.Controls.RadioButton> controls are visible as well.</span></span> <span data-ttu-id="d737f-316">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-316">For example:</span></span>

  <span data-ttu-id="d737f-317">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-317">Before:</span></span>

  ![具有焦點且沒有焦點視覺效果的展開器控制項螢幕擷取畫面。](./media/whats-new-in-accessibility/expander-control-before.png)

  <span data-ttu-id="d737f-319">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-319">After:</span></span>

  ![擴充控制項的螢幕擷取畫面，其中的焦點顯示控制項文字周圍的虛線。](./media/whats-new-in-accessibility/expander-control-after.png)

- <span data-ttu-id="d737f-321"><xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.RadioButton> 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-321"><xref:System.Windows.Controls.CheckBox> and <xref:System.Windows.Controls.RadioButton> controls</span></span>

  <span data-ttu-id="d737f-322">在高對比佈景主題中選取時，<xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.RadioButton> 控制項中的文字現在更容易出現。</span><span class="sxs-lookup"><span data-stu-id="d737f-322">The text in the <xref:System.Windows.Controls.CheckBox> and <xref:System.Windows.Controls.RadioButton> controls is now easier to see when selected in high contrast themes.</span></span> <span data-ttu-id="d737f-323">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-323">For example:</span></span>

  <span data-ttu-id="d737f-324">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-324">Before:</span></span>

  ![螢幕擷取畫面：高對比主題的文字可見度不佳的選項按鈕和複選按鈕。](./media/whats-new-in-accessibility/high-contrast-radio-button-before.png)

  <span data-ttu-id="d737f-326">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-326">After:</span></span>

  ![螢幕擷取畫面：高對比主題上具有更佳文字可見度的選項按鈕和複選按鈕。](./media/whats-new-in-accessibility/high-contrast-radio-button-after.png)

- <span data-ttu-id="d737f-328"><xref:System.Windows.Controls.ComboBox> 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-328"><xref:System.Windows.Controls.ComboBox> control</span></span>

  <span data-ttu-id="d737f-329">從 .NET Framework 4.7.1 開始，已停用的 <xref:System.Windows.Controls.ComboBox> 控制項框線色彩與已停用的文字色彩相同。</span><span class="sxs-lookup"><span data-stu-id="d737f-329">Starting with .NET Framework 4.7.1, the border of a disabled <xref:System.Windows.Controls.ComboBox> control is the same color as disabled text.</span></span> <span data-ttu-id="d737f-330">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-330">For example:</span></span>

  <span data-ttu-id="d737f-331">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-331">Before:</span></span>

  ![具有不同色彩之框線和控制項文字的已停用下拉式方塊的螢幕擷取畫面。](./media/whats-new-in-accessibility/combo-disabled-before.png)

  <span data-ttu-id="d737f-333">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-333">After:</span></span>

  ![已停用下拉式方塊的螢幕擷取畫面，其框線具有與控制項文字相同的色彩。](./media/whats-new-in-accessibility/combo-disabled-after.png)

  <span data-ttu-id="d737f-335">此外，已停用和聚焦按鈕會使用正確的佈景主題色彩。</span><span class="sxs-lookup"><span data-stu-id="d737f-335">In addition, disabled and focused buttons use the correct theme color.</span></span>

  <span data-ttu-id="d737f-336">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-336">Before:</span></span>

  ![黑色按鈕的螢幕擷取畫面，其中包含將焦點放在一起的灰色文字。](./media/whats-new-in-accessibility/button-theme-colors-before.png)

  <span data-ttu-id="d737f-338">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-338">After:</span></span>

  ![以黑色文字表示焦點我的藍色按鈕螢幕擷取畫面。](./media/whats-new-in-accessibility/button-theme-colors-after.png)

  <span data-ttu-id="d737f-340">最後，在 .NET Framework 4.7 和舊版本中將 <xref:System.Windows.Controls.ComboBox> 控制項的樣式設定為 `Toolbar.ComboBoxStyleKey` 會導致無法看到下拉式箭號。</span><span class="sxs-lookup"><span data-stu-id="d737f-340">Finally, in .NET Framework 4.7 and earlier versions, setting a <xref:System.Windows.Controls.ComboBox> control’s style to `Toolbar.ComboBoxStyleKey` caused the drop-down arrow to be invisible.</span></span> <span data-ttu-id="d737f-341">從 .NET Framework 4.7.1 開始，已修正此問題。</span><span class="sxs-lookup"><span data-stu-id="d737f-341">This issue is fixed starting with .NET Framework 4.7.1.</span></span> <span data-ttu-id="d737f-342">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-342">For example:</span></span>

  <span data-ttu-id="d737f-343">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-343">Before:</span></span>

  ![具有不可見下拉箭號之 ComboBox 控制項的螢幕擷取畫面。](./media/whats-new-in-accessibility/combo-box-style-key-before.png)

  <span data-ttu-id="d737f-345">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-345">After:</span></span>

  ![顯示下拉箭號之 ComBoxBox 控制項的螢幕擷取畫面。](./media/whats-new-in-accessibility/combo-box-style-key-after.png)

- <span data-ttu-id="d737f-347"><xref:System.Windows.Controls.DataGrid> 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-347"><xref:System.Windows.Controls.DataGrid> control</span></span>

  <span data-ttu-id="d737f-348">從 .NET Framework 4.7.1 開始，<xref:System.Windows.Controls.DataGrid> 控制項中的排序指標箭號現在會使用正確佈景主題色彩。</span><span class="sxs-lookup"><span data-stu-id="d737f-348">Starting with .NET Framework 4.7.1, the sort indicator arrow in <xref:System.Windows.Controls.DataGrid> controls now uses correct theme colors.</span></span> <span data-ttu-id="d737f-349">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-349">For example:</span></span>

  <span data-ttu-id="d737f-350">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-350">Before:</span></span>

  ![改進之前排序指標箭號的螢幕擷取畫面。](./media/whats-new-in-accessibility/sort-indicator-before.png)

  <span data-ttu-id="d737f-352">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-352">After:</span></span>

  ![改進之後排序指標箭號的螢幕擷取畫面。](./media/whats-new-in-accessibility/sort-indicator-after.png)

  <span data-ttu-id="d737f-354">此外，在 .NET Framework 4.7 和舊版本的高對比模式中，預設連結樣式會在滑鼠移至上方時變更為不正確的色彩。</span><span class="sxs-lookup"><span data-stu-id="d737f-354">In addition, in .NET Framework 4.7 and earlier versions, the default link style changed to an incorrect color on mouse over in high contrast modes.</span></span> <span data-ttu-id="d737f-355">從 .NET Framework 4.7.1 開始已解決此問題。</span><span class="sxs-lookup"><span data-stu-id="d737f-355">This is resolved starting with .NET Framework 4.7.1.</span></span> <span data-ttu-id="d737f-356">同樣地，從 .NET Framework 4.7.1 開始，<xref:System.Windows.Controls.DataGrid> 核取方塊資料行會使用鍵盤焦點回饋的預期色彩。</span><span class="sxs-lookup"><span data-stu-id="d737f-356">Similarly, <xref:System.Windows.Controls.DataGrid> checkbox columns uses the expected colors for keyboard focus feedback starting with .NET Framework 4.7.1.</span></span>

  <span data-ttu-id="d737f-357">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-357">Before:</span></span>

  ![顯示 [按我！] 連結的螢幕擷取畫面](./media/whats-new-in-accessibility/default-link-style-before.png)

  <span data-ttu-id="d737f-360">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-360">After:</span></span>

  ![顯示 [按我！] 連結的螢幕擷取畫面](./media/whats-new-in-accessibility/default-link-style-after.png)

<span data-ttu-id="d737f-363">如需 .NET Framework 4.7.1 中的 WPF 協助工具改善詳細資訊；請參閱 [WPF 的協助工具改善](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf)。</span><span class="sxs-lookup"><span data-stu-id="d737f-363">For more information on WPF accessibility improvements in .NET Framework 4.7.1, see [Accessibility improvements in WPF](../migration-guide/retargeting/4.7-4.7.1.md#accessibility-improvements-in-wpf).</span></span>

<a name="winforms471"></a>

### <a name="windows-forms-accessibility-improvements"></a><span data-ttu-id="d737f-364">Windows Forms 協助工具改善</span><span class="sxs-lookup"><span data-stu-id="d737f-364">Windows Forms accessibility improvements</span></span>

<span data-ttu-id="d737f-365">在 .NET Framework 4.7.1 中，Windows Forms (WinForms) 包含下列領域的協助工具變更。</span><span class="sxs-lookup"><span data-stu-id="d737f-365">In .NET Framework 4.7.1, Windows Forms (WinForms) includes accessibility changes in the following areas.</span></span>

<span data-ttu-id="d737f-366">**高對比模式中改善的顯示**</span><span class="sxs-lookup"><span data-stu-id="d737f-366">**Improved display in High Contrast mode**</span></span>

<span data-ttu-id="d737f-367">從 .NET Framework 4.7.1 開始，各種 WinForms 控制項都提供作業系統適用的高對比模式呈現改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-367">Starting with .NET Framework 4.7.1, various WinForms controls offer improved rendering in the HighContrast modes available in the operating system.</span></span> <span data-ttu-id="d737f-368">Windows 10 已變更某些高對比系統色彩的值，而且 Windows Forms 是以 Windows 10 Win32 架構為基礎。</span><span class="sxs-lookup"><span data-stu-id="d737f-368">Windows 10 has changed the values for some high contrast system colors, and Windows Forms is based on the Windows 10 Win32 framework.</span></span> <span data-ttu-id="d737f-369">為獲得最佳體驗，在最新版的 Windows 上執行，並新增最新作業系統變更，方法是在測試應用程式中新增 app.manifest 檔案，並將 Windows 10 支援的作業系統列取消註解，使它看起來如下：</span><span class="sxs-lookup"><span data-stu-id="d737f-369">For the best experience, run on the latest version of Windows and opt in to the latest OS changes by adding an app.manifest file in a test application and un-comment the Windows 10 supported OS  line so that it looks the following:</span></span>

```xml
<!-- Windows 10 -->
<supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
```

<span data-ttu-id="d737f-370">一些高對比變更範例包含：</span><span class="sxs-lookup"><span data-stu-id="d737f-370">Some examples of high contrast changes include:</span></span>

- <span data-ttu-id="d737f-371"><xref:System.Windows.Forms.MenuStrip> 項目中的核取記號較容易檢視。</span><span class="sxs-lookup"><span data-stu-id="d737f-371">Checkmarks in <xref:System.Windows.Forms.MenuStrip> items are easier to view.</span></span>

- <span data-ttu-id="d737f-372">選取時，已停用 <xref:System.Windows.Forms.MenuStrip> 項目較容易檢視。</span><span class="sxs-lookup"><span data-stu-id="d737f-372">When selected, disabled <xref:System.Windows.Forms.MenuStrip> items are easier to view.</span></span>

- <span data-ttu-id="d737f-373">所選取 <xref:System.Windows.Forms.Button> 控制項中的文字會與選取色彩成對比。</span><span class="sxs-lookup"><span data-stu-id="d737f-373">Text in a selected <xref:System.Windows.Forms.Button> control contrasts with the selection color.</span></span>

- <span data-ttu-id="d737f-374">已停用的文字較容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="d737f-374">Disabled text is easier to read.</span></span> <span data-ttu-id="d737f-375">例如：</span><span class="sxs-lookup"><span data-stu-id="d737f-375">For example:</span></span>

  <span data-ttu-id="d737f-376">之前：</span><span class="sxs-lookup"><span data-stu-id="d737f-376">Before:</span></span>

  ![應用程式的螢幕擷取畫面，其中使用在高對比模式下執行的不同控制項，在協助工具改善之前。](./media/whats-new-in-accessibility/high-contrast-mode-menu-items-before.png)

  <span data-ttu-id="d737f-378">之後：</span><span class="sxs-lookup"><span data-stu-id="d737f-378">After:</span></span>

  ![應用程式的螢幕擷取畫面，其中使用在協助工具改善後以高對比模式執行的不同控制項。](./media/whats-new-in-accessibility/high-contrast-mode-menu-items-after.png)

- <span data-ttu-id="d737f-380">執行緒例外狀況對話方塊中的高對比改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-380">High contrast improvements in the Thread Exception Dialog.</span></span>

<span data-ttu-id="d737f-381">**已改進朗讀程式支援**</span><span class="sxs-lookup"><span data-stu-id="d737f-381">**Improved Narrator support**</span></span>

<span data-ttu-id="d737f-382">.NET Framework 4.7.1 中的 Windows Forms 包含朗讀程式的下列協助工具改善：</span><span class="sxs-lookup"><span data-stu-id="d737f-382">Windows Forms in .NET Framework 4.7.1 includes the following accessibility improvements for the Narrator:</span></span>

- <span data-ttu-id="d737f-383">朗讀程式和其他 UI 自動化工具可以存取 <xref:System.Windows.Forms.MonthCalendar> 控制項。</span><span class="sxs-lookup"><span data-stu-id="d737f-383">The <xref:System.Windows.Forms.MonthCalendar> control can be accessed by the Narrator, as well as by other UI automation tools.</span></span>

- <span data-ttu-id="d737f-384"><xref:System.Windows.Forms.CheckedListBox> 控制項會在項目的核取狀態已經變更，因而通知使用者它們已變更清單項目值時通知 [朗讀程式]。</span><span class="sxs-lookup"><span data-stu-id="d737f-384">The <xref:System.Windows.Forms.CheckedListBox> control notifies Narrator when an item's check state has changed so the user is notified that they’ve changed the value of a list item.</span></span>

- <span data-ttu-id="d737f-385"><xref:System.Windows.Forms.DataGridViewCell> 控制項會向朗讀程式報告正確的唯讀狀態。</span><span class="sxs-lookup"><span data-stu-id="d737f-385">The <xref:System.Windows.Forms.DataGridViewCell> control reports the correct read-only status to Narrator.</span></span>

- <span data-ttu-id="d737f-386">朗讀程式現在可以讀取已停用 <xref:System.Windows.Forms.ToolStripMenuItem> 文字，而之前它會略過已停用的功能表項目。</span><span class="sxs-lookup"><span data-stu-id="d737f-386">Narrator can now read disabled <xref:System.Windows.Forms.ToolStripMenuItem> text, whereas previously it would skip over disabled menu items.</span></span>

<span data-ttu-id="d737f-387">**UIAutomation 協助工具模式的增強支援**</span><span class="sxs-lookup"><span data-stu-id="d737f-387">**Enhanced support for UIAutomation accessibility patterns**</span></span>

<span data-ttu-id="d737f-388">從 .NET Framework 4.7.1 開始，協助工具技術工具開發人員可以利用許多 WinForms 控制項的一般 API 協助工具模式和屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-388">Starting with .NET Framework 4.7.1, developers of accessibility technology tools can leverage common API accessibility patterns and properties for several WinForms controls.</span></span> <span data-ttu-id="d737f-389">這些協助工具改善包含：</span><span class="sxs-lookup"><span data-stu-id="d737f-389">These accessibility improvements include:</span></span>

- <span data-ttu-id="d737f-390"><xref:System.Windows.Forms.ComboBox> 和 <xref:System.Windows.Forms.ToolStripSplitButton> 現在支援[展開/摺疊模式](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="d737f-390">The <xref:System.Windows.Forms.ComboBox> and <xref:System.Windows.Forms.ToolStripSplitButton> now support the [expand/collapse pattern](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md).</span></span>

- <span data-ttu-id="d737f-391"><xref:System.Windows.Forms.DataGridViewCheckBoxCell> 現在支援[切換模式](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="d737f-391">The <xref:System.Windows.Forms.DataGridViewCheckBoxCell> now supports the [toggle pattern](../ui-automation/implementing-the-ui-automation-toggle-control-pattern.md).</span></span>

- <span data-ttu-id="d737f-392"><xref:System.Windows.Forms.ToolStripItem> 控制項支援 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 屬性和[展開/摺疊模式](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="d737f-392">The <xref:System.Windows.Forms.ToolStripItem> control supports the <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> property and the [expand/collapse pattern](../ui-automation/implementing-the-ui-automation-expandcollapse-control-pattern.md).</span></span>

- <span data-ttu-id="d737f-393"><xref:System.Windows.Forms.NumericUpDown> 和 <xref:System.Windows.Forms.DomainUpDown> 控制項支援 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> 屬性。</span><span class="sxs-lookup"><span data-stu-id="d737f-393">The <xref:System.Windows.Forms.NumericUpDown> and <xref:System.Windows.Forms.DomainUpDown> controls support the <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name> property.</span></span>

<span data-ttu-id="d737f-394">**改善的屬性瀏覽器體驗**</span><span class="sxs-lookup"><span data-stu-id="d737f-394">**Improved property browser experience**</span></span>

<span data-ttu-id="d737f-395">從 .NET Framework 4.7.1 開始，Windows Forms 包含：</span><span class="sxs-lookup"><span data-stu-id="d737f-395">Starting with .NET Framework 4.7.1, Windows Forms includes:</span></span>

- <span data-ttu-id="d737f-396">透過各種下拉式選取視窗進行更佳的鍵盤導覽。</span><span class="sxs-lookup"><span data-stu-id="d737f-396">Better keyboard navigation through the various drop-down selection windows.</span></span>
- <span data-ttu-id="d737f-397">減少不必要的定位停駐點。</span><span class="sxs-lookup"><span data-stu-id="d737f-397">A reduction of unnecessary tab stops.</span></span>
- <span data-ttu-id="d737f-398">更適當地報告控制項類型。</span><span class="sxs-lookup"><span data-stu-id="d737f-398">Better reporting of control types.</span></span>
- <span data-ttu-id="d737f-399">改善的朗讀程式行為。</span><span class="sxs-lookup"><span data-stu-id="d737f-399">Improved narrator behavior.</span></span>

<a name="aspnet471"></a>

### <a name="aspnet-web-controls"></a><span data-ttu-id="d737f-400">ASP.NET Web 控制項</span><span class="sxs-lookup"><span data-stu-id="d737f-400">ASP.NET web controls</span></span>

<span data-ttu-id="d737f-401">從 .NET Framework 4.7.1 和 Visual Studio 2017 15.3 版開始，ASP.NET 改進了 ASP.NET web 控制項如何與 Visual Studio 中的協助工具技術搭配運作。</span><span class="sxs-lookup"><span data-stu-id="d737f-401">Starting with .NET Framework 4.7.1 and Visual Studio 2017 version 15.3, ASP.NET improves how ASP.NET web controls work with accessibility technology in Visual Studio.</span></span> <span data-ttu-id="d737f-402">變更包括下列項目：</span><span class="sxs-lookup"><span data-stu-id="d737f-402">Changes include the following:</span></span>

- <span data-ttu-id="d737f-403">在控制項中執行遺失 UI 協助工具模式的變更，例如 [**詳細資料] View** wizard 中的 [**加入欄位**] 對話方塊，或是 **ListView** wizard 的 [**設定 listview** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d737f-403">Changes to implement missing UI accessibility patterns in controls, like the **Add Field** dialog in the **Details View** wizard, or the **Configure ListView** dialog of the **ListView** wizard.</span></span>

- <span data-ttu-id="d737f-404">變更以改善高對比模式中的顯示，例如 **資料頁 [欄位編輯器**]。</span><span class="sxs-lookup"><span data-stu-id="d737f-404">Changes to improve the display in High Contrast mode, like the **Data Pager Fields Editor**.</span></span>

- <span data-ttu-id="d737f-405">改善控制項鍵盤導覽體驗的變更，例如 [DataPager] 控制項的 [**編輯頁欄位**] wizard 中的 [**欄位**] 對話方塊、[**設定 ObjectCoNtext** ] 對話方塊或 [**設定資料來源**] wizard 的 [**設定資料選取**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d737f-405">Changes to improve the keyboard navigation experiences for controls, like the **Fields** dialog in the **Edit Pager Fields** wizard of the DataPager control, the **Configure ObjectContext** dialog, or the **Configure Data Selection** dialog of the **Configure Data Source** wizard.</span></span>

<a name="tools471"></a>

### <a name="net-sdk-tools"></a><span data-ttu-id="d737f-406">.NET SDK 工具</span><span class="sxs-lookup"><span data-stu-id="d737f-406">.NET SDK Tools</span></span>

<span data-ttu-id="d737f-407">[組態編輯器工具 (SvcConfigEditor.exe)](../wcf/configuration-editor-tool-svcconfigeditor-exe.md) 和[服務追蹤檢視器工具 (SvcTraceViewer.exe)](../wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 藉由修正各種協助工具問題來改善。</span><span class="sxs-lookup"><span data-stu-id="d737f-407">The [Configuration Editor Tool (SvcConfigEditor.exe)](../wcf/configuration-editor-tool-svcconfigeditor-exe.md) and [Service Trace Viewer Tool (SvcTraceViewer.exe)](../wcf/service-trace-viewer-tool-svctraceviewer-exe.md) have been improved by fixing varied accessibility issues.</span></span> <span data-ttu-id="d737f-408">其中大部分是小問題，例如未定義名稱，或未正確實作某些 UI 自動化模式。</span><span class="sxs-lookup"><span data-stu-id="d737f-408">Most of these were small issues, like a name not being defined or certain UI automation patterns not being implemented correctly.</span></span> <span data-ttu-id="d737f-409">雖然許多使用者並未注意到這些不正確的值，但使用螢幕助讀程式等輔助技術的客戶會發現這些 SDK 工具更易於存取。</span><span class="sxs-lookup"><span data-stu-id="d737f-409">While many users won’t be aware of these incorrect values, customers who use assistive technologies like screen readers will find these SDK tools more accessible.</span></span>

<span data-ttu-id="d737f-410">這些增強功能變更一些先前的行為，例如鍵盤焦點的順序。</span><span class="sxs-lookup"><span data-stu-id="d737f-410">These enhancements change some previous behaviors, such as keyboard focus order.</span></span>

<a name="wf471"></a>

### <a name="windows-workflow-foundation-wf-workflow-designer"></a><span data-ttu-id="d737f-411">Windows Workflow Foundation (WF) 工作流程設計工具</span><span class="sxs-lookup"><span data-stu-id="d737f-411">Windows Workflow Foundation (WF) Workflow Designer</span></span>

<span data-ttu-id="d737f-412">在工作流程設計工具中的協助工具變更包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="d737f-412">Accessibility changes in the Workflow Designer include the following:</span></span>

- <span data-ttu-id="d737f-413">在某些控制項中，定位順序變更為由左至右及由上至下：</span><span class="sxs-lookup"><span data-stu-id="d737f-413">The tab order changes to left to right and top to bottom in some controls:</span></span>

  - <span data-ttu-id="d737f-414">設定 <xref:System.ServiceModel.Activities.InitializeCorrelation> 活動之關聯性資料的初始化關聯性視窗。</span><span class="sxs-lookup"><span data-stu-id="d737f-414">The initialize correlation window for setting correlation data for the <xref:System.ServiceModel.Activities.InitializeCorrelation> activity.</span></span>

  - <span data-ttu-id="d737f-415"><xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 活動的內容定義視窗。</span><span class="sxs-lookup"><span data-stu-id="d737f-415">The content definition window for the <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.SendReply>, and <xref:System.ServiceModel.Activities.ReceiveReply> activities.</span></span>

- <span data-ttu-id="d737f-416">可透過鍵盤使用多個功能：</span><span class="sxs-lookup"><span data-stu-id="d737f-416">More functions are available via the keyboard:</span></span>

  - <span data-ttu-id="d737f-417">編輯活動的屬性時，如果第一次將焦點放在屬性群組，可以透過鍵盤將其摺疊。</span><span class="sxs-lookup"><span data-stu-id="d737f-417">When editing the properties of an activity, property groups can be collapsed by keyboard the first time they are focused.</span></span>

  - <span data-ttu-id="d737f-418">可透過鍵盤存取警告圖示。</span><span class="sxs-lookup"><span data-stu-id="d737f-418">Warning icons are accessible by keyboard.</span></span>

  - <span data-ttu-id="d737f-419">可透過鍵盤存取 [屬性] 視窗中的 [其他屬性] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d737f-419">The **More Properties** button in the **Properties** window is accessible by keyboard.</span></span>

  - <span data-ttu-id="d737f-420">鍵盤使用者可以存取工作流程設計工具之 [引數] 和 [變數] 窗格中的標頭項目。</span><span class="sxs-lookup"><span data-stu-id="d737f-420">Keyboard users can access the header items in the **Arguments** and **Variables** panes of the Workflow Designer.</span></span>

- <span data-ttu-id="d737f-421">在以下這類情況發生時，已改善具有焦點之項目的可見性：</span><span class="sxs-lookup"><span data-stu-id="d737f-421">Improved visibility of items with focus, such as when:</span></span>

  - <span data-ttu-id="d737f-422">在工作流程設計工具與活動設計工具所使用的資料格中新增資料列。</span><span class="sxs-lookup"><span data-stu-id="d737f-422">Adding rows to data grids used by the Workflow Designer and activity designers.</span></span>

  - <span data-ttu-id="d737f-423">使用 Tab 鍵循環顯示 <xref:System.ServiceModel.Activities.ReceiveReply> 和 <xref:System.ServiceModel.Activities.SendReply> 活動的欄位。</span><span class="sxs-lookup"><span data-stu-id="d737f-423">Tabbing through fields in the <xref:System.ServiceModel.Activities.ReceiveReply> and <xref:System.ServiceModel.Activities.SendReply> activities.</span></span>

  - <span data-ttu-id="d737f-424">設定變數或引數的預設值</span><span class="sxs-lookup"><span data-stu-id="d737f-424">Setting default values for variables or arguments</span></span>

- <span data-ttu-id="d737f-425">螢幕助讀程式現在可以正確辨識：</span><span class="sxs-lookup"><span data-stu-id="d737f-425">Screen readers can now correctly recognize:</span></span>

  - <span data-ttu-id="d737f-426">工作流程設計工具中設定的中斷點。</span><span class="sxs-lookup"><span data-stu-id="d737f-426">Breakpoints set in the workflow designer.</span></span>

  - <span data-ttu-id="d737f-427"><xref:System.Activities.Statements.FlowSwitch%601>、<xref:System.Activities.Statements.FlowDecision> 和 <xref:System.ServiceModel.Activities.CorrelationScope> 活動。</span><span class="sxs-lookup"><span data-stu-id="d737f-427">The <xref:System.Activities.Statements.FlowSwitch%601>, <xref:System.Activities.Statements.FlowDecision>, and <xref:System.ServiceModel.Activities.CorrelationScope> activities.</span></span>
  - <span data-ttu-id="d737f-428"><xref:System.ServiceModel.Activities.Receive> 活動的內容。</span><span class="sxs-lookup"><span data-stu-id="d737f-428">The contents of the <xref:System.ServiceModel.Activities.Receive> activity.</span></span>

  - <span data-ttu-id="d737f-429"><xref:System.Activities.Statements.InvokeMethod> 活動的目標類型。</span><span class="sxs-lookup"><span data-stu-id="d737f-429">The Target Type for the <xref:System.Activities.Statements.InvokeMethod> activity.</span></span>

  - <span data-ttu-id="d737f-430"><xref:System.Activities.Statements.TryCatch> 活動中的例外狀況下拉式方塊和 Finally 區段。</span><span class="sxs-lookup"><span data-stu-id="d737f-430">The Exception combo box and the Finally section in the <xref:System.Activities.Statements.TryCatch> activity.</span></span>

  - <span data-ttu-id="d737f-431">傳訊活動 (<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply>) 中的 [訊息類型] 下拉式方塊、[新增關聯性初始設定式] 視窗、[內容定義] 視窗和 [CorrelatesOn 定義] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d737f-431">The Message Type combo box, the splitter in the Add Correlation Initializers window, the Content Definition window, and the CorrelatesOn Definition window in the messaging activities (<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.SendReply>, and <xref:System.ServiceModel.Activities.ReceiveReply>).</span></span>

  - <span data-ttu-id="d737f-432">狀態機器轉換和轉換目的地。</span><span class="sxs-lookup"><span data-stu-id="d737f-432">State machine transitions and transitions destinations.</span></span>

  - <span data-ttu-id="d737f-433"><xref:System.Activities.Statements.FlowDecision> 活動的註釋和連接器。</span><span class="sxs-lookup"><span data-stu-id="d737f-433">Annotations and connectors on <xref:System.Activities.Statements.FlowDecision> activities.</span></span>

  - <span data-ttu-id="d737f-434">活動的操作 (右鍵) 功能表。</span><span class="sxs-lookup"><span data-stu-id="d737f-434">The context (right-click) menus for activities.</span></span>

  - <span data-ttu-id="d737f-435">屬性方格中的屬性值編輯器、[清除搜尋] 按鈕、[依分類] 及 [字母順序] 排序按鈕和 [運算式編輯器] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d737f-435">The property value editors, the Clear Search button, the By Category and Alphabetical sort buttons, and the Expression Editor dialog in the properties grid.</span></span>

  - <span data-ttu-id="d737f-436">工作流程設計工具中的顯示比例百分比。</span><span class="sxs-lookup"><span data-stu-id="d737f-436">The zoom percentage in the Workflow Designer.</span></span>

  - <span data-ttu-id="d737f-437"><xref:System.Activities.Statements.Parallel> 和 <xref:System.Activities.Statements.Pick> 活動中的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="d737f-437">The separator in <xref:System.Activities.Statements.Parallel> and <xref:System.Activities.Statements.Pick> activities.</span></span>

  - <span data-ttu-id="d737f-438"><xref:System.Activities.Statements.InvokeDelegate> 活動。</span><span class="sxs-lookup"><span data-stu-id="d737f-438">The <xref:System.Activities.Statements.InvokeDelegate> activity.</span></span>

  - <span data-ttu-id="d737f-439">字典活動 (`Microsoft.Activities.AddToDictionary<TKey,TValue>`、`Microsoft.Activities.RemoveFromDictionary<TKey,TValue>` 等) 的 [選取類型] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d737f-439">The Select Types window for dictionary activities (`Microsoft.Activities.AddToDictionary<TKey,TValue>`, `Microsoft.Activities.RemoveFromDictionary<TKey,TValue>`, etc.).</span></span>

  - <span data-ttu-id="d737f-440">[瀏覽並選取 .NET 類型] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d737f-440">The Browse and Select .NET Type window.</span></span>

  - <span data-ttu-id="d737f-441">工作流程設計工具中的階層連結。</span><span class="sxs-lookup"><span data-stu-id="d737f-441">Breadcrumbs in the Workflow Designer.</span></span>

- <span data-ttu-id="d737f-442">選擇高對比佈景主題的使用者會看到工作流程設計工具和其控制項在可見性方面的許多改善，例如項目之間的更佳對比比例以及用於焦點項目的更明顯選取方塊。</span><span class="sxs-lookup"><span data-stu-id="d737f-442">Users who choose High Contrast themes will see many improvements in the visibility of the Workflow Designer and its controls, like better contrast ratios between elements and more noticeable selection boxes used for focus elements.</span></span>

## <a name="see-also"></a><span data-ttu-id="d737f-443">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d737f-443">See also</span></span>

- [<span data-ttu-id="d737f-444">.NET Framework 中的新功能</span><span class="sxs-lookup"><span data-stu-id="d737f-444">What's new in the .NET Framework</span></span>](index.md)
