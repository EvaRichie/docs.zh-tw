---
title: 使用可為 Null 的參考類型進行設計
description: 本進階教學課程提供可為 Null 的參考類型簡介。 您將了解如何在參考值可能為 Null 時表達您的設計意圖，以及在它們不能為 Null 時強制執行編譯器。
ms.date: 02/19/2019
ms.technology: csharp-null-safety
ms.custom: mvc
ms.openlocfilehash: 70e6a7a906bc9a35918cf3e26c3e23bd0cfdafde
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91755846"
---
# <a name="tutorial-express-your-design-intent-more-clearly-with-nullable-and-non-nullable-reference-types"></a>教學課程：使用可為 Null 與不可為 Null 的參考類型更清楚地表達您的設計意圖

C # 8.0 導入了 [可為](../nullable-references.md)null 的參考型別，以可為 null 的實值型別補充實數值型別。 您可以藉由將 `?` 附加至類型，來將變數宣告為**可為 Null 的參考類型**。 例如，`string?` 代表可為 Null 的 `string`。 您可以使用這些新類型更清楚地表達設計意圖：部分變數「永遠都必須有值」**，而其他變數「可能會遺漏值」**。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
>
> - 在設計中併入可為 Null 與不可為 Null 的參考類型
> - 在整個程式碼中啟用可為 Null 的參考類型檢查。
> - 撰寫程式碼，以使編譯器強制執行這些設計決策。
> - 在您自己的設計中使用可為 Null 的參考功能

## <a name="prerequisites"></a>必要條件

您必須設定電腦以執行 .NET Core，包括 c # 8.0 編譯器。 C # 8.0 編譯器適用于 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)或 [.net Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0)。

本教學課程假設您已熟悉 C# 和 .NET，包括 Visual Studio 或 .NET Core CLI。

## <a name="incorporate-nullable-reference-types-into-your-designs"></a>在設計中併入可為 Null 的參考類型

在本教學課程中，您會建置程式庫來將問卷執行模型化。 程式碼會使用可為 Null 的參考類型和不可為 Null 的參考類型來代表真實世界的概念。 問卷問題絕對不能是 Null。 受訪者可能不想回答問題。 `null`在此情況下，回應可能為。

您將為此範例撰寫的程式碼會表達該意圖，而編譯器會強制執行該意圖。

## <a name="create-the-application-and-enable-nullable-reference-types"></a>建立應用程式並啟用可為 Null 的參考類型

在 Visual Studio 中或從命令列中使用 `dotnet new console` 來建立新的主控台應用程式。 為應用程式 `NullableIntroduction` 命名。 建立應用程式之後，您必須指定整個專案在啟用的 **可為 null 注釋內容**中進行編譯。 開啟 *.csproj* 檔案，並將元素加入 `Nullable` 至 `PropertyGroup` 元素。 將值設為 `enable`。 您必須加入宣告 **可為 null 的參考型別** 功能，即使是在 c # 8.0 專案中也一樣。 這是因為一旦開啟此功能之後，現有的參考變數宣告就會變成**不可為 Null 的參考類型**。 雖然該決策將有助於找出現有程式碼可能沒有正確的 null 檢查的問題，但它可能無法正確反映您的原始設計意圖：

```xml
<Nullable>enable</Nullable>
```

### <a name="design-the-types-for-the-application"></a>設計適用於應用程式的類型

此問卷應用程式需要建立一些類別：

- 用來將問題清單模型化的類別。
- 用來將已針對問卷連絡之人員清單模型化的類別。
- 用來將填寫問卷的人員所提供的答案模型化的類別。

這些類型將使用可為 Null 和不可為 Null 的參考類型，來表達哪些成員是必要的，而哪些成員是選擇性的。 可為 Null 的參考類型會清楚地傳達該設計意圖：

- 屬於問卷一部分的問題絕對不能是 Null：詢問空白的問題並無任何意義。
- 受訪者絕對不能是 Null。 您會想要追蹤連絡過的人員，甚至是拒絕參與的受訪者。
- 對於問題的任何回應可能會是 Null。 受訪者可以拒絕回答部分或所有問題。

如果您已經使用 c # 進行程式設計，您可能會習慣參考型別，而這些型別可讓 `null` 您遺漏其他機會宣告不可為 null 的實例：

- 問題的集合不應為 Null。
- 受訪者的集合不應為 Null。

當您撰寫程式碼時，您會看到一個不可為 null 的參考型別做為參考的預設值，可避免可能導致的常見錯誤 <xref:System.NullReferenceException> 。 本教學課程中的一堂課程是，您已決定哪些變數可能或無法執行 `null` 。 此語言不提供語法來表達那些決策。 但現在已提供。

您將建立的應用程式會執行下列步驟：

1. 建立問卷並在其中加入問題。
1. 針對問卷建立一組虛擬隨機的受訪者。
1. 連絡人的意見回應，直到完成的問卷大小達到目標數目為止。
1. 寫出問卷回應的重要統計資料。

## <a name="build-the-survey-with-nullable-and-non-nullable-reference-types"></a>使用可為 null 且不可為 null 的參考型別來建立問卷

您將撰寫的第一個程式碼會建立問卷。 您會撰寫類別來將問卷問題和問卷執行模型化。 您的問卷具有三種類型的問題，其會依答案的格式來區別：是/否的答案、數字答案，以及文字答案。 建立 `public SurveyQuestion` 類別：

```csharp
namespace NullableIntroduction
{
    public class SurveyQuestion
    {
    }
}
```

編譯器會針對啟用的可為 null 注釋內容中的程式碼，將每個參考型別變數宣告解釋為 **不可為 null** 的參考型別。 您可以藉由新增問題文字的屬性和問題的類型來查看第一個警告，如下列程式碼所示：

```csharp
namespace NullableIntroduction
{
    public enum QuestionType
    {
        YesNo,
        Number,
        Text
    }

    public class SurveyQuestion
    {
        public string QuestionText { get; }
        public QuestionType TypeOfQuestion { get; }
    }
}
```

由於您尚未將 `QuestionText` 初始化，因此，編譯器會發出警告，表示尚未將不可為 Null 的屬性初始化。 您的設計要求問題文字不可為 Null，因此，您也會新增建構函式來將它和 `QuestionType` 值初始化。 完成的類別定義看起來類似下列程式碼：

[!code-csharp[DefineQuestion](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyQuestion.cs)]

新增建構函式會移除警告。 建構函式引數也是不可為 Null 的參考類型，因次，編譯器不會發出任何警告。

接著，建立名為 `SurveyRun` 的 `public` 類別。 這個類別包含 `SurveyQuestion` 物件和方法的清單，可在問卷中新增問題，如下列程式碼所示：

```csharp
using System.Collections.Generic;

namespace NullableIntroduction
{
    public class SurveyRun
    {
        private List<SurveyQuestion> surveyQuestions = new List<SurveyQuestion>();

        public void AddQuestion(QuestionType type, string question) =>
            AddQuestion(new SurveyQuestion(type, question));
        public void AddQuestion(SurveyQuestion surveyQuestion) => surveyQuestions.Add(surveyQuestion);
    }
}
```

和以前一樣，您必須將清單物件初始化為非 Null 的值，否則編譯器會發出警告。 不會在 `AddQuestion` 的第二個多載中進行任何 Null 檢查，因為不需要：您已將該變數宣告成不可為 Null。 其值不可以是 `null`。

切換至編輯器中的 *Program.cs* ，並以 `Main` 下列幾行程式碼取代的內容：

[!code-csharp[AddQuestions](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#AddQuestions)]

由於整個專案都是在啟用的可為 null 注釋內容中，因此當您傳遞 `null` 給任何需要不可為 null 參考型別的方法時，將會收到警告。 將下列這一行新增到 `Main` 來試用它：

```csharp
surveyRun.AddQuestion(QuestionType.Text, default);
```

## <a name="create-respondents-and-get-answers-to-the-survey"></a>建立受訪者並取得問卷的答案

接著，撰寫程式碼來產生問卷的答案。 這項過程涉及幾項小型工作：

1. 建置方法來產生受訪者物件。 這些物件代表系統要求您填寫問卷的人員。
1. 建置邏輯來模擬向受訪者詢問問題，然後收集答案，或記下受訪者沒有回答。
1. 重複執行，直到有足夠的受訪者回答問卷為止。

您需要一個類型來代表問卷回應，所以現在要新增該類別。 啟用可為 Null 的支援。 新增 `Id` 屬性和建構函式來將它初始化，如下列程式碼所示：

```csharp
namespace NullableIntroduction
{
    public class SurveyResponse
    {
        public int Id { get; }

        public SurveyResponse(int id) => Id = id;
    }
}
```

接著，新增 `static` 方法，藉由產生隨機識別碼來建立新的參與者：

[!code-csharp[GenerateRespondents](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#Random)]

這個類別的主要責任是產生參與者對問卷問題所做的回應。 這個責任有數個步驟：

1. 要求參與問卷。 如果該人員不同意，請傳回遺漏 (或 Null) 回應。
1. 詢問每個問題並記錄答案。 每個答案也可能遺漏 (或 Null)。

將下列程式碼新增至 `SurveyResponse` 類別：

[!code-csharp[AnswerSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#AnswerSurvey)]

問卷答案的儲存體是 `Dictionary<int, string>?`，指出它可能是 Null。 您正在使用新的語言功能，來向編譯器和稍後要讀取您程式碼的任何人宣告您的設計意圖。 如果您在 `surveyResponses` 未先檢查值的情況下進行 `null` 取值，您將會收到編譯器警告。 您不會在 `AnswerSurvey` 方法中收到警告，因為編譯器可判斷並未將 `surveyResponses` 變數設定為上述的非 Null 值。

針對遺漏的問題使用 `null`，醒目提示使用可為 Null 參考型別時的一項關鍵點：您的目標不是從程式中移除所有 `null` 值。 您的目標是確保您所撰寫程式碼能夠表達出設計意圖。 遺漏值是在您程式碼中進行表達的必要概念。 `null` 值是表達那些遺漏值的清楚方式。 嘗試移除所有 `null` 值只會導向定義其他方式，在不使用 `null` 的情況下表達那些遺漏值。

接著，您需要在 `SurveyRun` 類別中撰寫 `PerformSurvey` 方法。 在 `SurveyRun` 類別中新增下列程式碼：

[!code-csharp[PerformSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#PerformSurvey)]

同樣地，您對於可為 Null 之 `List<SurveyResponse>?` 的選擇，表示回應可能是 Null。 這表示尚未將問卷提供給任何受訪者。 請注意，受訪者會持續新增，直到有足夠的受訪者同意為止。

執行問卷的最後一個步驟是在 `Main` 方法的結尾處新增執行問卷的呼叫：

[!code-csharp[RunSurvey](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#RunSurvey)]

## <a name="examine-survey-responses"></a>檢查問卷回應

最後一個步驟是顯示問卷結果。 您將在所撰寫的多個類別中新增程式碼。 此程式碼示範用來區別可為 Null 與不可為 Null 之參考類型的值。 一開始，請將下列兩個運算式主體成員新增至 `SurveyResponse` 類別：

[!code-csharp[ReportResponses](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyResponse.cs#SurveyStatus)]

因為 `surveyResponses` 是可為 null 的參考型別，所以必須先有 null 檢查，再將它取消參考。 `Answer`方法會傳回不可為 null 的字串，因此我們必須使用 null 聯合運算子來涵蓋遺漏答案的案例。

接著，將這三個運算式主體成員新增到 `SurveyRun` 類別：

[!code-csharp[ReportResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/SurveyRun.cs#RunReport)]

`AllParticipants` 成員必須將下列因素納入考量：`respondents` 變數可能是 Null，但傳回的值不可為 Null。 如果您藉由移除 `??` 及其後的空序列來變更該運算式，則編譯器會警告您方法可能傳回 `null`，而它的傳回簽章會傳回不可為 Null 的類型。

最後，在 `Main` 方法的底部新增下列迴圈：

[!code-csharp[DisplaySurveyResults](~/samples/snippets/csharp/NullableIntroduction/NullableIntroduction/Program.cs#WriteAnswers)]

您不需要在這個程式碼中進行任何 `null` 檢查，由於您已設計了基礎介面，因此它們全部都會傳回不可為 Null 的參考類型。

## <a name="get-the-code"></a>取得程式碼

您可以從 [csharp/NullableIntroduction](https://github.com/dotnet/samples/tree/master/csharp/NullableIntroduction) 資料夾的[範例](https://github.com/dotnet/samples)存放庫中取得已完成教學課程的程式碼。

藉由在可為 Null 與不可為 Null 的參考類型之間變更類型宣告來進行實驗。 請參閱如何產生不同的警告以確保您不會意外地為 `null` 取值。

## <a name="next-steps"></a>後續步驟

請透過將現有的應用程式遷移至使用可為 Null 參考型別，來深入了解：
> [!div class="nextstepaction"]
> [升級應用程式以使用可為 Null 參考型別](upgrade-to-nullable-references.md)

瞭解如何在使用 Entity Framework 時使用可為 null 的參考型別：
> [Entity Framework Core 基本概念：使用可為 Null 的參考型別](https://docs.microsoft.com/en-us/ef/core/miscellaneous/nullable-reference-types)
