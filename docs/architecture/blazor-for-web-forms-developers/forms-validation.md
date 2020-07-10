---
title: 表單和驗證
description: 瞭解如何在中使用用戶端驗證來建立表單 Blazor 。
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- Blazor WebAssembly
ms.date: 09/19/2019
ms.openlocfilehash: 1a99719f59415872510aef051d1f3c73daf53e15
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173272"
---
# <a name="forms-and-validation"></a><span data-ttu-id="13ba7-103">表單和驗證</span><span class="sxs-lookup"><span data-stu-id="13ba7-103">Forms and validation</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="13ba7-104">ASP.NET Web form 架構包含一組驗證服務器控制項，可處理輸入表單 (、、等等) 的驗證使用者輸入 `RequiredFieldValidator` `CompareValidator` `RangeValidator` 。</span><span class="sxs-lookup"><span data-stu-id="13ba7-104">The ASP.NET Web Forms framework includes a set of validation server controls that handle validating user input entered into a form (`RequiredFieldValidator`, `CompareValidator`, `RangeValidator`, and so on).</span></span> <span data-ttu-id="13ba7-105">ASP.NET Web form 架構也支援模型系結，並根據 (`[Required]` 、 `[StringLength]` 、等等) 的資料批註來驗證模型 `[Range]` 。</span><span class="sxs-lookup"><span data-stu-id="13ba7-105">The ASP.NET Web Forms framework also supports model binding and validating the model based on data annotations (`[Required]`, `[StringLength]`, `[Range]`, and so on).</span></span> <span data-ttu-id="13ba7-106">您可以使用不顯眼的 JavaScript 驗證，在伺服器和用戶端上強制執行驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="13ba7-106">The validation logic can be enforced both on the server and on the client using unobtrusive JavaScript-based validation.</span></span> <span data-ttu-id="13ba7-107">`ValidationSummary`伺服器控制項是用來向使用者顯示驗證錯誤的摘要。</span><span class="sxs-lookup"><span data-stu-id="13ba7-107">The `ValidationSummary` server control is used to display a summary of the validation errors to the user.</span></span>

Blazor<span data-ttu-id="13ba7-108">支援在用戶端和伺服器之間共用驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="13ba7-108"> supports the sharing of validation logic between both the client and the server.</span></span> <span data-ttu-id="13ba7-109">ASP.NET 提供許多一般伺服器驗證的預先建立 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="13ba7-109">ASP.NET provides pre-built JavaScript implementations of many common server validations.</span></span> <span data-ttu-id="13ba7-110">在許多情況下，開發人員仍然必須撰寫 JavaScript，才能完全執行其應用程式特定的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="13ba7-110">In many cases, the developer still has to write JavaScript to fully implement their app-specific validation logic.</span></span> <span data-ttu-id="13ba7-111">相同的模型類型、資料批註和驗證邏輯可以同時在伺服器和用戶端上使用。</span><span class="sxs-lookup"><span data-stu-id="13ba7-111">The same model types, data annotations, and validation logic can be used on both the server and client.</span></span>

Blazor<span data-ttu-id="13ba7-112">提供一組輸入元件。</span><span class="sxs-lookup"><span data-stu-id="13ba7-112"> provides a set of input components.</span></span> <span data-ttu-id="13ba7-113">輸入元件會處理將欄位資料系結至模型，並在提交表單時驗證使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="13ba7-113">The input components handle binding field data to a model and validating the user input when the form is submitted.</span></span>

|<span data-ttu-id="13ba7-114">輸入元件</span><span class="sxs-lookup"><span data-stu-id="13ba7-114">Input component</span></span>|<span data-ttu-id="13ba7-115">呈現的 HTML 元素</span><span class="sxs-lookup"><span data-stu-id="13ba7-115">Rendered HTML element</span></span>    |
|---------------|-------------------------|
|`InputCheckbox`|`<input type="checkbox">`|
|`InputDate`    |`<input type="date">`    |
|`InputNumber`  |`<input type="number">`  |
|`InputSelect`  |`<select>`               |
|`InputText`    |`<input>`                |
|`InputTextArea`|`<textarea>`             |

<span data-ttu-id="13ba7-116">`EditForm`元件會包裝這些輸入元件，並透過協調驗證程式 `EditContext` 。</span><span class="sxs-lookup"><span data-stu-id="13ba7-116">The `EditForm` component wraps these input components and orchestrates the validation process through an `EditContext`.</span></span> <span data-ttu-id="13ba7-117">建立時 `EditForm` ，您可以使用參數來指定要系結的模型實例 `Model` 。</span><span class="sxs-lookup"><span data-stu-id="13ba7-117">When creating an `EditForm`, you specify what model instance to bind to using the `Model` parameter.</span></span> <span data-ttu-id="13ba7-118">驗證通常是使用資料批註來完成，而且是可延伸的。</span><span class="sxs-lookup"><span data-stu-id="13ba7-118">Validation is typically done using data annotations, and it's extensible.</span></span> <span data-ttu-id="13ba7-119">若要啟用以資料注釋為基礎的驗證，請將 `DataAnnotationsValidator` 元件新增為的子系 `EditForm` 。</span><span class="sxs-lookup"><span data-stu-id="13ba7-119">To enable data annotation-based validation, add the `DataAnnotationsValidator` component as a child of the `EditForm`.</span></span> <span data-ttu-id="13ba7-120">`EditForm`元件提供便利的事件來處理有效的 (`OnValidSubmit`) 和不正確 (`OnInvalidSubmit`) 提交。</span><span class="sxs-lookup"><span data-stu-id="13ba7-120">The `EditForm` component provides a convenient event for handling valid (`OnValidSubmit`) and invalid (`OnInvalidSubmit`) submissions.</span></span> <span data-ttu-id="13ba7-121">另外還有一個更通用 `OnSubmit` 的事件，可讓您自行觸發和處理驗證。</span><span class="sxs-lookup"><span data-stu-id="13ba7-121">There's also a more generic `OnSubmit` event that lets you trigger and handle the validation yourself.</span></span>

<span data-ttu-id="13ba7-122">若要顯示驗證錯誤摘要，請使用 `ValidationSummary` 元件。</span><span class="sxs-lookup"><span data-stu-id="13ba7-122">To display a validation error summary, use the `ValidationSummary` component.</span></span> <span data-ttu-id="13ba7-123">若要顯示特定輸入欄位的驗證訊息，請使用 `ValidationMessage` 元件，並針對 `For` 指向適當模型成員的參數指定 lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="13ba7-123">To display validation messages for a specific input field, use the `ValidationMessage` component, specifying a lambda expression for the `For` parameter that points to the appropriate model member.</span></span>

<span data-ttu-id="13ba7-124">下列模型類型使用資料批註來定義數個驗證規則：</span><span class="sxs-lookup"><span data-stu-id="13ba7-124">The following model type defines several validation rules using data annotations:</span></span>

```csharp
using System;
using System.ComponentModel.DataAnnotations;

public class Starship
{
    [Required]
    [StringLength(16,
        ErrorMessage = "Identifier too long (16 character limit).")]
    public string Identifier { get; set; }

    public string Description { get; set; }

    [Required]
    public string Classification { get; set; }

    [Range(1, 100000,
        ErrorMessage = "Accommodation invalid (1-100000).")]
    public int MaximumAccommodation { get; set; }

    [Required]
    [Range(typeof(bool), "true", "true",
        ErrorMessage = "This form disallows unapproved ships.")]
    public bool IsValidatedDesign { get; set; }

    [Required]
    public DateTime ProductionDate { get; set; }
}
```

<span data-ttu-id="13ba7-125">下列元件示範如何 Blazor 根據模型類型，在中建立表單 `Starship` ：</span><span class="sxs-lookup"><span data-stu-id="13ba7-125">The following component demonstrates building a form in Blazor based on the `Starship` model type:</span></span>

```razor
<h1>New Ship Entry Form</h1>

<EditForm Model="@starship" OnValidSubmit="@HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />

    <p>
        <label for="identifier">Identifier: </label>
        <InputText id="identifier" @bind-Value="starship.Identifier" />
        <ValidationMessage For="() => starship.Identifier" />
    </p>
    <p>
        <label for="description">Description (optional): </label>
        <InputTextArea id="description" @bind-Value="starship.Description" />
    </p>
    <p>
        <label for="classification">Primary Classification: </label>
        <InputSelect id="classification" @bind-Value="starship.Classification">
            <option value="">Select classification ...</option>
            <option value="Exploration">Exploration</option>
            <option value="Diplomacy">Diplomacy</option>
            <option value="Defense">Defense</option>
        </InputSelect>
        <ValidationMessage For="() => starship.Classification" />
    </p>
    <p>
        <label for="accommodation">Maximum Accommodation: </label>
        <InputNumber id="accommodation" @bind-Value="starship.MaximumAccommodation" />
        <ValidationMessage For="() => starship.MaximumAccommodation" />
    </p>
    <p>
        <label for="valid">Engineering Approval: </label>
        <InputCheckbox id="valid" @bind-Value="starship.IsValidatedDesign" />
        <ValidationMessage For="() => starship.IsValidatedDesign" />
    </p>
    <p>
        <label for="productionDate">Production Date: </label>
        <InputDate id="productionDate" @bind-Value="starship.ProductionDate" />
        <ValidationMessage For="() => starship.ProductionDate" />
    </p>

    <button type="submit">Submit</button>
</EditForm>

@code {
    private Starship starship = new Starship();

    private void HandleValidSubmit()
    {
        // Save the data
    }
}
```

<span data-ttu-id="13ba7-126">提交表單之後，就不會將模型系結資料儲存到任何資料存放區，例如資料庫。</span><span class="sxs-lookup"><span data-stu-id="13ba7-126">After the form submission, the model-bound data hasn't been saved to any data store, like a database.</span></span> <span data-ttu-id="13ba7-127">在 Blazor WebAssembly 應用程式中，必須將資料傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="13ba7-127">In a Blazor WebAssembly app, the data must be sent to the server.</span></span> <span data-ttu-id="13ba7-128">例如，使用 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="13ba7-128">For example, using an HTTP POST request.</span></span> <span data-ttu-id="13ba7-129">在 Blazor 伺服器應用程式中，資料已經在伺服器上，但必須保存。</span><span class="sxs-lookup"><span data-stu-id="13ba7-129">In a Blazor Server app, the data is already on the server, but it must be persisted.</span></span> <span data-ttu-id="13ba7-130">處理應用程式中的資料存取 Blazor 是處理[資料](data.md)一節的主題。</span><span class="sxs-lookup"><span data-stu-id="13ba7-130">Handling data access in Blazor apps is the subject of the [Dealing with data](data.md) section.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13ba7-131">其他資源</span><span class="sxs-lookup"><span data-stu-id="13ba7-131">Additional resources</span></span>

<span data-ttu-id="13ba7-132">如需有關應用程式中[表單和驗證](/aspnet/core/blazor/forms-validation)的詳細資訊 Blazor ，請參閱 Blazor 檔集。</span><span class="sxs-lookup"><span data-stu-id="13ba7-132">For more information on [forms and validation](/aspnet/core/blazor/forms-validation) in Blazor apps, see the Blazor documentation.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="13ba7-133">[上一個](state-management.md) 
>[下一步](data.md)</span><span class="sxs-lookup"><span data-stu-id="13ba7-133">[Previous](state-management.md)
[Next](data.md)</span></span>
