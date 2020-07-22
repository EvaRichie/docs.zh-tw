---
title: 靜態類別和靜態類別成員 - C# 程式設計手冊
description: '靜態類別無法在 c # 中具現化。 您可以使用類別名稱本身來存取靜態類別的成員。'
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, static members
- static members [C#]
- static classes [C#]
- C# language, static classes
- static class members [C#]
ms.assetid: 235614b5-1371-4dbd-9abd-b406a8b0298b
ms.openlocfilehash: 4f187d772d2f2e4375fbe3cfdc8c48af691f1c7c
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86863873"
---
# <a name="static-classes-and-static-class-members-c-programming-guide"></a>靜態類別和靜態類別成員 (C# 程式設計手冊)

[static](../../language-reference/keywords/static.md) 類別基本上與非靜態類別相同，但有一項差異︰無法具現化靜態類別。 換句話說，您不能使用 [new](../../language-reference/operators/new-operator.md) 運算子來建立類別型別的變數。 因為沒有任何執行個體變數，所以您可以使用類別名稱本身來存取靜態類別的成員。 例如，如果您的 `UtilityClass` 靜態類別包含 `MethodA` 公用靜態方法，則會呼叫方法，如下列範例所示︰  
  
```csharp  
UtilityClass.MethodA();  
```  
  
 如果方法集只作業於輸入參數，並且不需要取得或設定任何內部執行個體欄位，則靜態類別可以用作其方便使用的容器。 例如，在 .NET 類別庫中，靜態 <xref:System.Math?displayProperty=nameWithType> 類別包含執行數學運算的方法，不需要儲存或抓取特定類別實例特有的資料 <xref:System.Math> 。 亦即，您可以指定類別名稱和方法名稱來套用類別的成員，如下列範例所示。  
  
```csharp  
double dub = -3.14;  
Console.WriteLine(Math.Abs(dub));  
Console.WriteLine(Math.Floor(dub));  
Console.WriteLine(Math.Round(Math.Abs(dub)));  
  
// Output:  
// 3.14  
// -4  
// 3  
```  
  
 如同所有類別類型的情況，當載入參考類別的程式時，.NET 執行時間會載入靜態類別的型別資訊。 程式無法指定確實載入類別的時間。 不過，一定會載入類別、初始化其欄位，並在第一次於程式中參考類別之前呼叫其靜態建構函式。 只會呼叫靜態建構函式一次，而且靜態類別在程式所在應用程式定義域的存留期間保留在記憶體中。  
  
> [!NOTE]
> 若要建立只允許建立它本身之一個執行個體的非靜態類別，請參閱 [Implementing Singleton in C#](https://docs.microsoft.com/previous-versions/msp-n-p/ff650316%28v=pandp.10%29) (在 C# 中實作單一)。  
  
 下列清單提供靜態類別的主要功能︰  
  
- 僅包含靜態成員。  
  
- 無法具現化。  
  
- 已密封。  
  
- 不能包含[執行個體建構函式](./instance-constructors.md)。  
  
 因此，建立靜態類別，基本上與建立只包含靜態成員和私用建構函式的類別相同。 私用建構函式可防止具現化類別。 使用靜態類別的優點在於編譯器可以確認不會意外新增任何執行個體成員。 編譯器將保證無法建立此類別的執行個體。  
  
 靜態類別已密封，因此無法進行繼承。 它們無法繼承自 <xref:System.Object> 以外的任何類別。 靜態類別不能包含實例的函數。 不過，它們可以包含靜態的「函數」（static）。 如果類別包含需要重要初始化的靜態成員，則非靜態類別也應該定義靜態建構函式。 如需詳細資訊，請參閱[靜態建構函式](./static-constructors.md)。  
  
## <a name="example"></a>範例  
 以下是包含兩種方法可將溫度從攝氏轉換為華氏以及從華氏轉換為攝氏的靜態類別範例︰  
  
 [!code-csharp[csProgGuideObjects#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#31)]  
  
## <a name="static-members"></a>靜態成員  
 非靜態類別可以包含靜態方法、欄位、屬性或事件。 即使尚未建立類別的執行個體，還是可以在類別上呼叫靜態成員。 靜態成員一律是透過類別名稱進行存取，而不是執行個體名稱。 不論建立多少個類別執行個體，都只會有一個靜態成員複本。 靜態方法和屬性無法存取其包含類型中的非靜態欄位和事件，而且它們無法存取任何物件的執行個體變數，除非它是明確地在方法參數中傳遞。  
  
 使用一些靜態成員宣告非靜態類別，會比將整個類別宣告為靜態更為常見。 靜態欄位的兩個常用用法是持續計算已具現化的物件數目，或是儲存必須在所有執行個體之間共用的值。  
  
 可以多載但無法覆寫靜態方法，因為它們屬於類別，而不是類別的任何執行個體。  
  
 雖然欄位不可以宣告為 `static const`，但是 [const](../../language-reference/keywords/const.md) 欄位在其行為中基本上是靜態的。 它屬於類型，而不是類型的執行個體。 因此，您 `const` 可以使用 `ClassName.MemberName` 用於靜態欄位的相同標記法來存取欄位。 不需要物件執行個體。  
  
 C # 不支援靜態區域變數（也就是在方法範圍中宣告的變數）。  
  
 在成員的傳回型別前面使用 `static` 關鍵字，即可宣告靜態類別成員，如下列範例所示︰  
  
 [!code-csharp[csProgGuideObjects#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#29)]  
  
 第一次存取靜態成員之前，以及呼叫靜態建構函式 (如果有的話) 之前，都會初始化靜態成員。 若要存取靜態類別成員，請使用類別的名稱來指定成員的位置，而不是變數名稱，如下列範例所示︰  
  
 [!code-csharp[csProgGuideObjects#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#30)]  
  
 如果您的類別包含靜態欄位，請提供在載入類別時初始化它們的靜態建構函式。  
  
 呼叫靜態方法會以 Microsoft 中繼語言（MSIL）產生呼叫指示，而實例方法的呼叫會產生 `callvirt` 指令，這也會檢查是否有 null 物件參考。 不過，大部分的時間，兩者之間的效能差異並不明顯。  
  
## <a name="c-language-specification"></a>C# 語言規格  

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)中的[靜態類別](~/_csharplang/spec/classes.md#static-classes)與[靜態和執行個體的成員](~/_csharplang/spec/classes.md#static-and-instance-members)。 語言規格是 C# 語法及用法的限定來源。
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [static](../../language-reference/keywords/static.md)
- [類別](./classes.md)
- [class](../../language-reference/keywords/class.md)
- [靜態建構函式](./static-constructors.md)
- [執行個體建構函式](./instance-constructors.md)
