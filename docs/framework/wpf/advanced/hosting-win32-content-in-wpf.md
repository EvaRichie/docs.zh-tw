---
title: 裝載 Win32 內容
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 3cc8644a-34f3-4082-9ddc-77623e4df2d8
ms.openlocfilehash: c0c62f1999feaf591c512314515f01e83fa12591
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052087"
---
# <a name="hosting-win32-content-in-wpf"></a>在 WPF 中裝載 Win32 內容

## <a name="prerequisites"></a>必要條件

請參閱[WPF 和 Win32 交互操作](wpf-and-win32-interoperation.md)。

## <a name="a-walkthrough-of-win32-inside-windows-presentation-framework-hwndhost"></a>Windows Presentation Framework （HwndHost）中的 Win32 逐步解說

若要在應用程式內重複使用 Win32 內容 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ，請使用 <xref:System.Windows.Interop.HwndHost> ，這是讓 hwnd 看起來像內容的控制項 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 。 就像一樣 <xref:System.Windows.Interop.HwndSource> ， <xref:System.Windows.Interop.HwndHost> 可以直接使用：衍生自 <xref:System.Windows.Interop.HwndHost> 並執行 `BuildWindowCore` 和 `DestroyWindowCore` 方法，然後具現化您的 <xref:System.Windows.Interop.HwndHost> 衍生類別，並將它放在您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式內。

如果您的 Win32 邏輯已經封裝為控制項，則您的 `BuildWindowCore` 實做比呼叫更少 `CreateWindow` 。 例如，若要在 c + + 中建立 Win32 LISTBOX 控制項：

```cpp
virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
    HWND handle = CreateWindowEx(0, L"LISTBOX",
    L"this is a Win32 listbox",
    WS_CHILD | WS_VISIBLE | LBS_NOTIFY
    | WS_VSCROLL | WS_BORDER,
    0, 0, // x, y
    30, 70, // height, width
    (HWND) hwndParent.Handle.ToPointer(), // parent hwnd
    0, // hmenu
    0, // hinstance
    0); // lparam

    return HandleRef(this, IntPtr(handle));
}

virtual void DestroyWindowCore(HandleRef hwnd) override {
    // HwndHost will dispose the hwnd for us
}
```

但是，假設 Win32 程式碼不是完全獨立的， 若是如此，您可以建立 Win32 對話方塊，並將其內容內嵌至較大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式。 此範例會在 Visual Studio 和 c + + 中顯示此項，不過也可以使用不同的語言或在命令列中執行此動作。

從簡單的對話方塊開始，它會編譯成 c + + DLL 專案。

接下來，將對話方塊引入較大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式：

- 將 DLL 編譯為 managed （ `/clr` ）

- 將對話變成控制項

- <xref:System.Windows.Interop.HwndHost>使用 `BuildWindowCore` 和 `DestroyWindowCore` 方法來定義的衍生類別

- 覆寫 `TranslateAccelerator` 方法以處理對話方塊索引鍵

- 覆寫 `TabInto` 方法以支援 tab 鍵

- 覆寫 `OnMnemonic` 方法以支援助憶鍵

- 將子類別具現化 <xref:System.Windows.Interop.HwndHost> ，並將其放在右 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素底下

### <a name="turn-the-dialog-into-a-control"></a>將對話變成控制項

您可以使用 WS_CHILD 和 DS_CONTROL 樣式，將對話方塊變成子 HWND。 移至定義對話方塊的資源檔（.rc），並尋找對話方塊定義的開頭：

```text
IDD_DIALOG1 DIALOGEX 0, 0, 303, 121
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU
```

將第二行變更為：

```text
STYLE DS_SETFONT | WS_CHILD | WS_BORDER | DS_CONTROL
```

此動作並不會將它完整封裝成獨立的控制項;您仍然需要呼叫， `IsDialogMessage()` 讓 Win32 可以處理特定訊息，但控制項變更的確提供了將這些控制項放在另一個 HWND 中的直接方式。

## <a name="subclass-hwndhost"></a>子類別 HwndHost

匯入下列命名空間：

```cpp
namespace ManagedCpp
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Input;
    using namespace System::Windows::Media;
    using namespace System::Runtime::InteropServices;
```

然後，建立的衍生類別 <xref:System.Windows.Interop.HwndHost> ，並覆寫 `BuildWindowCore` 和 `DestroyWindowCore` 方法：

```cpp
public ref class MyHwndHost : public HwndHost, IKeyboardInputSink {
    private:
        HWND dialog;

    protected:
        virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {
            InitializeGlobals();
            dialog = CreateDialog(hInstance,
                MAKEINTRESOURCE(IDD_DIALOG1),
                (HWND) hwndParent.Handle.ToPointer(),
                (DLGPROC) About);
            return HandleRef(this, IntPtr(dialog));
        }

        virtual void DestroyWindowCore(HandleRef hwnd) override {
            // hwnd will be disposed for us
        }
```

在這裡，您會使用 `CreateDialog` 來建立實際上是控制項的對話方塊。 因為這是在 DLL 內呼叫的第一個方法，所以您也應該呼叫稍後定義的函式來執行一些標準的 Win32 初始化，稱為 `InitializeGlobals()` ：

```cpp
bool initialized = false;
    void InitializeGlobals() {
        if (initialized) return;
        initialized = true;

        // TODO: Place code here.
        MSG msg;
        HACCEL hAccelTable;

        // Initialize global strings
        LoadString(hInstance, IDS_APP_TITLE, szTitle, MAX_LOADSTRING);
        LoadString(hInstance, IDC_TYPICALWIN32DIALOG, szWindowClass, MAX_LOADSTRING);
        MyRegisterClass(hInstance);
```

### <a name="override-translateaccelerator-method-to-handle-dialog-keys"></a>覆寫 TranslateAccelerator 方法以處理對話方塊索引鍵

如果您現在執行這個範例，您會看到顯示的對話方塊控制項，但它會忽略讓對話方塊成為功能對話方塊的所有鍵盤處理。 您現在應該覆寫 `TranslateAccelerator` 實作為（來自執行的 `IKeyboardInputSink` 介面 <xref:System.Windows.Interop.HwndHost> ）。 當應用程式收到 WM_KEYDOWN 並 WM_SYSKEYDOWN 時，就會呼叫這個方法。

```cpp
#undef TranslateAccelerator
        virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
            ModifierKeys modifiers) override
        {
            ::MSG m = ConvertMessage(msg);

            // Win32's IsDialogMessage() will handle most of our tabbing, but doesn't know
            // what to do when it reaches the last tab stop
            if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
                HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
                HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
                TraversalRequest^ request = nullptr;

                if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
                    // this code should work, but there’s a bug with interop shift-tab in current builds
                    request = gcnew TraversalRequest(FocusNavigationDirection::Last);
                }
                else if (!GetKeyState(VK_SHIFT) && GetFocus() == lastTabStop) {
                    request = gcnew TraversalRequest(FocusNavigationDirection::Next);
                }

                if (request != nullptr)
                    return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);

            }

            // Only call IsDialogMessage for keys it will do something with.
            if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
                switch (m.wParam) {
                    case VK_TAB:
                    case VK_LEFT:
                    case VK_UP:
                    case VK_RIGHT:
                    case VK_DOWN:
                    case VK_EXECUTE:
                    case VK_RETURN:
                    case VK_ESCAPE:
                    case VK_CANCEL:
                        IsDialogMessage(dialog, &m);
                        // IsDialogMessage should be called ProcessDialogMessage --
                        // it processes messages without ever really telling you
                        // if it handled a specific message or not
                        return true;
                }
            }

            return false; // not a key we handled
        }
```

這是一段很多的程式碼，因此可以使用一些更詳細的說明。 首先，使用 c + + 和 c + + 宏的程式碼;您必須注意，已有名為的宏 `TranslateAccelerator` （定義于 winuser 中）：

```cpp
#define TranslateAccelerator  TranslateAcceleratorW
```

因此，請務必定義 `TranslateAccelerator` 方法，而不是 `TranslateAcceleratorW` 方法。

同樣地，也會同時有非受控 winuser 和 managed `Microsoft::Win32::MSG` 結構。 您可以使用 c + + 運算子來區分兩者 `::` 。

```cpp
virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,
    ModifierKeys modifiers) override
{
    ::MSG m = ConvertMessage(msg);
}
```

這兩個 Msg 都有相同的資料，但有時使用非受控定義比較容易，因此在此範例中，您可以定義明顯的轉換常式：

```cpp
::MSG ConvertMessage(System::Windows::Interop::MSG% msg) {
    ::MSG m;
    m.hwnd = (HWND) msg.hwnd.ToPointer();
    m.lParam = (LPARAM) msg.lParam.ToPointer();
    m.message = msg.message;
    m.wParam = (WPARAM) msg.wParam.ToPointer();

    m.time = msg.time;

    POINT pt;
    pt.x = msg.pt_x;
    pt.y = msg.pt_y;
    m.pt = pt;

    return m;
}
```

回到 `TranslateAccelerator` 。 基本原則是呼叫 Win32 函式，盡可能地執行最多工作 `IsDialogMessage` ，但 `IsDialogMessage` 無法存取對話方塊以外的任何專案。 做為對話方塊周圍的使用者索引標籤，當 tab 鍵的執行超過對話方塊中的最後一個控制項時，您必須呼叫，將焦點設定到該 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 部分 `IKeyboardInputSite::OnNoMoreStops` 。

```cpp
// Win32's IsDialogMessage() will handle most of the tabbing, but doesn't know
// what to do when it reaches the last tab stop
if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {
    HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
    HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
    TraversalRequest^ request = nullptr;

    if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {
        request = gcnew TraversalRequest(FocusNavigationDirection::Last);
    }
    else if (!GetKeyState(VK_SHIFT) && GetFocus() ==  lastTabStop) { {
        request = gcnew TraversalRequest(FocusNavigationDirection::Next);
    }

    if (request != nullptr)
        return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);
}
```

最後，請呼叫 `IsDialogMessage`。 但是，方法的其中一項責任 `TranslateAccelerator` 就是告知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 您是否處理過此按鍵。 如果您沒有處理它，則輸入事件可以透過應用程式的其餘部分進行通道和反升。 在這裡，您將會公開鍵盤 messange 處理的怪癖，以及 Win32 中的輸入架構本質。 可惜的 `IsDialogMessage` 是，不會以任何方式傳回，不論是否處理特定的按鍵。 更糟的是，它會 `DispatchMessage()` 在不應處理的擊鍵上呼叫！  因此，您必須進行反向工程 `IsDialogMessage` ，而且只會針對您知道它將處理的金鑰呼叫它：

```cpp
// Only call IsDialogMessage for keys it will do something with.
if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {
    switch (m.wParam) {
        case VK_TAB:
        case VK_LEFT:
        case VK_UP:
        case VK_RIGHT:
        case VK_DOWN:
        case VK_EXECUTE:
        case VK_RETURN:
        case VK_ESCAPE:
        case VK_CANCEL:
            IsDialogMessage(dialog, &m);
            // IsDialogMessage should be called ProcessDialogMessage --
            // it processes messages without ever really telling you
            // if it handled a specific message or not
            return true;
    }
```

### <a name="override-tabinto-method-to-support-tabbing"></a>覆寫 TabInto 方法以支援 Tab 鍵

現在您已完成 `TranslateAccelerator` ，使用者可以在對話方塊內部定位，並將其移至更大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式。 但是使用者無法使用 tab 鍵回到對話方塊中。 若要解決這個問題，您可以覆寫 `TabInto` ：

```cpp
public:
    virtual bool TabInto(TraversalRequest^ request) override {
        if (request->FocusNavigationDirection == FocusNavigationDirection::Last) {
            HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);
            SetFocus(lastTabStop);
        }
        else {
            HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);
            SetFocus(firstTabStop);
        }
        return true;
    }
```

`TraversalRequest`參數會告訴您索引標籤動作是 tab 鍵或 shift tab。

### <a name="override-onmnemonic-method-to-support-mnemonics"></a>覆寫 OnMnemonic 方法以支援助憶鍵

鍵盤處理幾乎已完成，但有一件事遺漏–助憶鍵無法使用。 如果使用者按 alt-F，焦點 doe 不會跳至 [名字：] 編輯方塊。 因此，您會覆寫 `OnMnemonic` 方法：

```cpp
virtual bool OnMnemonic(System::Windows::Interop::MSG% msg, ModifierKeys modifiers) override {
    ::MSG m = ConvertMessage(msg);

    // If it's one of our mnemonics, set focus to the appropriate hwnd
    if (msg.message == WM_SYSCHAR && GetKeyState(VK_MENU /*alt*/)) {
        int dialogitem = 9999;
        switch (m.wParam) {
            case 's': dialogitem = IDOK; break;
            case 'c': dialogitem = IDCANCEL; break;
            case 'f': dialogitem = IDC_EDIT1; break;
            case 'l': dialogitem = IDC_EDIT2; break;
            case 'p': dialogitem = IDC_EDIT3; break;
            case 'a': dialogitem = IDC_EDIT4; break;
            case 'i': dialogitem = IDC_EDIT5; break;
            case 't': dialogitem = IDC_EDIT6; break;
            case 'z': dialogitem = IDC_EDIT7; break;
        }
        if (dialogitem != 9999) {
            HWND hwnd = GetDlgItem(dialog, dialogitem);
            SetFocus(hwnd);
            return true;
        }
    }
    return false; // key unhandled
};
```

為什麼不要 `IsDialogMessage` 在這裡呼叫？  您的問題與之前相同，您必須能夠在程式碼處理按鍵動作時通知程式 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 代碼，而且 `IsDialogMessage` 無法這麼做。 另外還有第二個問題，因為 `IsDialogMessage` 如果焦點的 HWND 不在對話方塊內，則會拒絕處理助憶鍵。

### <a name="instantiate-the-hwndhost-derived-class"></a>具現化 HwndHost 衍生類別

最後，現在所有的索引鍵和索引標籤支援都已就緒，您可以將放 <xref:System.Windows.Interop.HwndHost> 入較大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 應用程式。 如果主要應用程式是以撰寫的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ，最簡單的方式就是將它放在正確的位置，以保留 <xref:System.Windows.Controls.Border> 您要放置的空白元素 <xref:System.Windows.Interop.HwndHost> 。 在這裡，您會建立 <xref:System.Windows.Controls.Border> 名為的 `insertHwndHostHere` ：

```xaml
<Window x:Class="WPFApplication1.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Windows Presentation Framework Application"
    Loaded="Window1_Loaded"
    >
    <StackPanel>
        <Button Content="WPF button"/>
        <Border Name="insertHwndHostHere" Height="200" Width="500"/>
        <Button Content="WPF button"/>
    </StackPanel>
</Window>
```

然後，剩下的工作就是在程式碼序列中尋找一個不錯的位置來具現化， <xref:System.Windows.Interop.HwndHost> 並將它連接到 <xref:System.Windows.Controls.Border> 。 在此範例中，您會將它放在衍生類別的函式內 <xref:System.Windows.Window> ：

```csharp
public partial class Window1 : Window {
    public Window1() {
    }

    void Window1_Loaded(object sender, RoutedEventArgs e) {
        HwndHost host = new ManagedCpp.MyHwndHost();
        insertHwndHostHere.Child = host;
    }
}
```

這會提供您：

![執行之 WPF 應用程式的螢幕擷取畫面。](./media/hosting-win32-content-in-wpf/windows-presentation-foundation-application.png)

## <a name="see-also"></a>另請參閱

- [WPF 和 Win32 互通](wpf-and-win32-interoperation.md)
