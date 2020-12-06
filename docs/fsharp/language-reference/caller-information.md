---
title: 呼叫者資訊
description: 描述如何使用呼叫端資訊引數屬性，從方法取得呼叫端資訊。
ms.date: 11/04/2019
ms.openlocfilehash: 700cde26fbe4e6c48155f88bfc63af59af86cfe2
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739772"
---
# <a name="caller-information"></a><span data-ttu-id="0f987-103">呼叫者資訊</span><span class="sxs-lookup"><span data-stu-id="0f987-103">Caller information</span></span>

<span data-ttu-id="0f987-104">使用 Caller Info 屬性，您就可以取得有關方法之呼叫端的資訊。</span><span class="sxs-lookup"><span data-stu-id="0f987-104">By using Caller Info attributes, you can obtain information about the caller to a method.</span></span> <span data-ttu-id="0f987-105">您可以取得原始程式碼的檔案路徑、原始程式碼中的行號，以及呼叫端的成員名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-105">You can obtain file path of the source code, the line number in the source code, and the member name of the caller.</span></span> <span data-ttu-id="0f987-106">這項資訊有助於追蹤、偵錯及建立診斷工具。</span><span class="sxs-lookup"><span data-stu-id="0f987-106">This information is helpful for tracing, debugging, and creating diagnostic tools.</span></span>

<span data-ttu-id="0f987-107">若要取得這項資訊，可使用套用至選擇性參數的屬性，每個屬性都有預設值。</span><span class="sxs-lookup"><span data-stu-id="0f987-107">To obtain this information, you use attributes that are applied to optional parameters, each of which has a default value.</span></span> <span data-ttu-id="0f987-108">下表列出 [CompilerServices](/dotnet/api/system.runtime.compilerservices) 命名空間中定義的呼叫端資訊屬性：</span><span class="sxs-lookup"><span data-stu-id="0f987-108">The following table lists the Caller Info attributes that are defined in the [System.Runtime.CompilerServices](/dotnet/api/system.runtime.compilerservices) namespace:</span></span>

|<span data-ttu-id="0f987-109">屬性</span><span class="sxs-lookup"><span data-stu-id="0f987-109">Attribute</span></span>|<span data-ttu-id="0f987-110">描述</span><span class="sxs-lookup"><span data-stu-id="0f987-110">Description</span></span>|<span data-ttu-id="0f987-111">類型</span><span class="sxs-lookup"><span data-stu-id="0f987-111">Type</span></span>|
|---------|-----------|----|
|[<span data-ttu-id="0f987-112">CallerFilePath</span><span class="sxs-lookup"><span data-stu-id="0f987-112">CallerFilePath</span></span>](/dotnet/api/system.runtime.compilerservices.callerfilepathattribute)|<span data-ttu-id="0f987-113">包含呼叫端的原始程式檔完整路徑。</span><span class="sxs-lookup"><span data-stu-id="0f987-113">Full path of the source file that contains the caller.</span></span> <span data-ttu-id="0f987-114">這是編譯時間的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="0f987-114">This is the file path at compile time.</span></span>|`String`
|[<span data-ttu-id="0f987-115">CallerLineNumber</span><span class="sxs-lookup"><span data-stu-id="0f987-115">CallerLineNumber</span></span>](/dotnet/api/system.runtime.compilerservices.callerlinenumberattribute)|<span data-ttu-id="0f987-116">原始程式檔中呼叫方法所在的行號。</span><span class="sxs-lookup"><span data-stu-id="0f987-116">Line number in the source file at which the method is called.</span></span>|`Integer`|
|[<span data-ttu-id="0f987-117">CallerMemberName</span><span class="sxs-lookup"><span data-stu-id="0f987-117">CallerMemberName</span></span>](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)|<span data-ttu-id="0f987-118">呼叫端的方法或屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-118">Method or property name of the caller.</span></span> <span data-ttu-id="0f987-119">請參閱本主題稍後的「成員名稱」一節。</span><span class="sxs-lookup"><span data-stu-id="0f987-119">See the Member Names section later in this topic.</span></span>|`String`|

## <a name="example"></a><span data-ttu-id="0f987-120">範例</span><span class="sxs-lookup"><span data-stu-id="0f987-120">Example</span></span>

<span data-ttu-id="0f987-121">下列範例顯示如何使用這些屬性來追蹤呼叫者。</span><span class="sxs-lookup"><span data-stu-id="0f987-121">The following example shows how you might use these attributes to trace a caller.</span></span>

```fsharp
open System.Diagnostics
open System.Runtime.CompilerServices
open System.Runtime.InteropServices

type Tracer() =
    member _.DoTrace(message: string,
                      [<CallerMemberName; Optional; DefaultParameterValue("")>] memberName: string,
                      [<CallerFilePath; Optional; DefaultParameterValue("")>] path: string,
                      [<CallerLineNumber; Optional; DefaultParameterValue(0)>] line: int) =
        Trace.WriteLine(sprintf $"Message: {message}")
        Trace.WriteLine(sprintf $"Member name: {memberName}")
        Trace.WriteLine(sprintf $"Source file path: {path}")
        Trace.WriteLine(sprintf $"Source line number: {line}")
```

## <a name="remarks"></a><span data-ttu-id="0f987-122">備註</span><span class="sxs-lookup"><span data-stu-id="0f987-122">Remarks</span></span>

<span data-ttu-id="0f987-123">呼叫端資訊屬性只能套用至選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="0f987-123">Caller Info attributes can only be applied to optional parameters.</span></span> <span data-ttu-id="0f987-124">呼叫端資訊屬性會讓編譯器針對每個以呼叫端資訊屬性裝飾的選擇性參數，寫入適當的值。</span><span class="sxs-lookup"><span data-stu-id="0f987-124">The Caller Info attributes cause the compiler to write the proper value for each optional parameter decorated with a Caller Info attribute.</span></span>

<span data-ttu-id="0f987-125">在編譯時期，Caller Info 的值會做為常值發出至中繼語言 (IL)。</span><span class="sxs-lookup"><span data-stu-id="0f987-125">Caller Info values are emitted as literals into the Intermediate Language (IL) at compile time.</span></span> <span data-ttu-id="0f987-126">不同于例外狀況之 [StackTrace](/dotnet/api/system.diagnostics.stacktrace) 屬性的結果，結果不會受到模糊化的影響。</span><span class="sxs-lookup"><span data-stu-id="0f987-126">Unlike the results of the [StackTrace](/dotnet/api/system.diagnostics.stacktrace) property for exceptions, the results aren't affected by obfuscation.</span></span>

<span data-ttu-id="0f987-127">您可以明確提供選擇性引數來控制呼叫端資訊，或是隱藏呼叫端資訊。</span><span class="sxs-lookup"><span data-stu-id="0f987-127">You can explicitly supply the optional arguments to control the caller information or to hide caller information.</span></span>

## <a name="member-names"></a><span data-ttu-id="0f987-128">成員名稱</span><span class="sxs-lookup"><span data-stu-id="0f987-128">Member names</span></span>

<span data-ttu-id="0f987-129">您可以使用 [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) 屬性來避免將成員名稱指定為 `String` 所呼叫方法的引數。</span><span class="sxs-lookup"><span data-stu-id="0f987-129">You can use the [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) attribute to avoid specifying the member name as a `String` argument to the called method.</span></span> <span data-ttu-id="0f987-130">藉由使用這項技術，您可以避免重新命名重構不會變更值的問題 `String` 。</span><span class="sxs-lookup"><span data-stu-id="0f987-130">By using this technique, you avoid the problem that Rename Refactoring doesn't change the `String` values.</span></span> <span data-ttu-id="0f987-131">這項優點對於下列工作特別有用：</span><span class="sxs-lookup"><span data-stu-id="0f987-131">This benefit is especially useful for the following tasks:</span></span>

- <span data-ttu-id="0f987-132">使用追蹤和診斷常式。</span><span class="sxs-lookup"><span data-stu-id="0f987-132">Using tracing and diagnostic routines.</span></span>
- <span data-ttu-id="0f987-133">在系結資料時執行 [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) 介面。</span><span class="sxs-lookup"><span data-stu-id="0f987-133">Implementing the [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) interface when binding data.</span></span> <span data-ttu-id="0f987-134">這個介面可讓物件的屬性告知繫結的控制項屬性已變更，所以控制項可以顯示更新的資訊。</span><span class="sxs-lookup"><span data-stu-id="0f987-134">This interface allows the property of an object to notify a bound control that the property has changed, so that the control can display the updated information.</span></span> <span data-ttu-id="0f987-135">如果沒有 [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) 屬性，您必須將屬性名稱指定為常值。</span><span class="sxs-lookup"><span data-stu-id="0f987-135">Without the [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) attribute, you must specify the property name as a literal.</span></span>

<span data-ttu-id="0f987-136">下圖顯示當您使用 CallerMemberName 屬性時所傳回的成員名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-136">The following chart shows the member names that are returned when you use the CallerMemberName attribute.</span></span>

|<span data-ttu-id="0f987-137">呼叫發生於</span><span class="sxs-lookup"><span data-stu-id="0f987-137">Calls occurs within</span></span>|<span data-ttu-id="0f987-138">成員名稱結果</span><span class="sxs-lookup"><span data-stu-id="0f987-138">Member name result</span></span>|
|-------------------|------------------|
|<span data-ttu-id="0f987-139">方法、屬性或事件</span><span class="sxs-lookup"><span data-stu-id="0f987-139">Method, property, or event</span></span>|<span data-ttu-id="0f987-140">產生呼叫的方法、屬性或事件的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-140">The name of the method, property, or event from which the call originated.</span></span>|
|<span data-ttu-id="0f987-141">建構函式</span><span class="sxs-lookup"><span data-stu-id="0f987-141">Constructor</span></span>|<span data-ttu-id="0f987-142">字串 ".ctor"</span><span class="sxs-lookup"><span data-stu-id="0f987-142">The string ".ctor"</span></span>|
|<span data-ttu-id="0f987-143">靜態建構函式</span><span class="sxs-lookup"><span data-stu-id="0f987-143">Static constructor</span></span>|<span data-ttu-id="0f987-144">字串 ".cctor"</span><span class="sxs-lookup"><span data-stu-id="0f987-144">The string ".cctor"</span></span>|
|<span data-ttu-id="0f987-145">解構函式</span><span class="sxs-lookup"><span data-stu-id="0f987-145">Destructor</span></span>|<span data-ttu-id="0f987-146">字串 "Finalize"</span><span class="sxs-lookup"><span data-stu-id="0f987-146">The string "Finalize"</span></span>|
|<span data-ttu-id="0f987-147">使用者定義的運算子或轉換</span><span class="sxs-lookup"><span data-stu-id="0f987-147">User-defined operators or conversions</span></span>|<span data-ttu-id="0f987-148">產生的成員名稱，例如 "op_Addition"。</span><span class="sxs-lookup"><span data-stu-id="0f987-148">The generated name for the member, for example, "op_Addition".</span></span>|
|<span data-ttu-id="0f987-149">屬性建構函式</span><span class="sxs-lookup"><span data-stu-id="0f987-149">Attribute constructor</span></span>|<span data-ttu-id="0f987-150">套用屬性的成員名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-150">The name of the member to which the attribute is applied.</span></span> <span data-ttu-id="0f987-151">如果屬性為成員內的任何項目 (例如參數、傳回值或泛型類型參數)，這個結果會是與該項目相關聯的成員名稱。</span><span class="sxs-lookup"><span data-stu-id="0f987-151">If the attribute is any element within a member (such as a parameter, a return value, or a generic type parameter), this result is the name of the member that's associated with that element.</span></span>|
|<span data-ttu-id="0f987-152">無包含的成員 (例如，組件層級或套用至類型的屬性)。</span><span class="sxs-lookup"><span data-stu-id="0f987-152">No containing member (for example, assembly-level or attributes that are applied to types)</span></span>|<span data-ttu-id="0f987-153">選擇性參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="0f987-153">The default value of the optional parameter.</span></span>|

## <a name="see-also"></a><span data-ttu-id="0f987-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0f987-154">See also</span></span>

- [<span data-ttu-id="0f987-155">屬性</span><span class="sxs-lookup"><span data-stu-id="0f987-155">Attributes</span></span>](attributes.md)
- [<span data-ttu-id="0f987-156">具名引數</span><span class="sxs-lookup"><span data-stu-id="0f987-156">Named arguments</span></span>](parameters-and-arguments.md#named-arguments)
- [<span data-ttu-id="0f987-157">選擇性參數</span><span class="sxs-lookup"><span data-stu-id="0f987-157">Optional parameters</span></span>](parameters-and-arguments.md#optional-parameters)
