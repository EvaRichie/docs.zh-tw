---
title: 執行個體建構函式 - C# 程式設計手冊
description: '當您使用新的運算式來建立類別的物件時，c # 中的實例函式會建立並初始化任何實例成員變數。'
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], instance constructors
- instance constructors [C#]
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
ms.openlocfilehash: d70e786446fb198afb4e0311757cacb65b706f47
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864198"
---
# <a name="instance-constructors-c-programming-guide"></a>執行個體建構函式 (C# 程式設計手冊)

當您使用 [new](../../language-reference/operators/new-operator.md) 運算式來建立 [class](../../language-reference/keywords/class.md) 物件時，可使用執行個體建構函式來建立和初始化任何執行個體成員變數。 若要初始化[靜態](../../language-reference/keywords/static.md)類別或非靜態類別中的靜態變數，您可定義靜態建構函式。 如需詳細資訊，請參閱[靜態建構函式](./static-constructors.md)。  
  
 下列範例顯示執行個體建構函式：  
  
 [!code-csharp[csProgGuideObjects#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#5)]  
  
> [!NOTE]
> 為了清楚起見，這個類別會包含公用欄位。 我們不建議您在程式設計中使用公用欄位，因為這麼做會允許程式中的任何方法，在不受限制及未經驗證的情況下，存取物件的內部運作。 資料成員一般應為私用，而且只應透過類別方法和屬性來存取。  
  
 每當建立以 `Coords` 類別為基礎的物件時，即會呼叫這個執行個體建構函式。 像這種不接受任何引數的建構函式，稱為「無參數建構函式」**。 不過，提供額外的建構函式通常很實用。 比方說，我們可以將建構函式新增至 `Coords` 類別，以指定資料成員的起始值：  
  
 [!code-csharp[csProgGuideObjects#76](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#76)]  
  
 如此即可建立含有預設值或特定初始值的 `Coords` 物件，如下所示：  
  
 [!code-csharp[csProgGuideObjects#77](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#77)]  
  
 如果類別不含建構函式，則會自動產生無參數建構函式，並使用預設值來初始化物件欄位。 例如，系統會將 [int](../../language-reference/builtin-types/integral-numeric-types.md) 初始化為 0。 如需類型預設值的詳細資訊，請參閱[c # 類型的預設值](../../language-reference/builtin-types/default-values.md)。 因此，由於 `Coords` 類別的無參數建構函式會將所有資料成員初始化為零，所以您可以將其完全移除，而不需變更類別的運作方式。 本主題稍後的範例 1 提供使用多個建構函式的完整範例；範例 2 則提供自動產生建構函式的範例。  
  
 執行個體建構函式也可用來呼叫基底類別的執行個體建構函式。 類別建構函式可以透過初始設定式，來叫用基底類別的建構函式，如下所示：  
  
 [!code-csharp[csProgGuideObjects#78](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#78)]  
  
 在此範例中，`Circle` 類別會將代表半徑和高度的值傳遞給 `Shape` 所提供的建構函式，進而衍生 `Circle`。 本主題的範例 3 會示範使用 `Shape` 和 `Circle` 的完整範例。  
  
## <a name="example-1"></a>範例 1  
 下列範例示範的類別具有兩個類別建構函式，一個不含引數，一個具有兩個引數。  
  
 [!code-csharp[csProgGuideObjects#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#4)]  
  
## <a name="example-2"></a>範例 2  
 在此範例中，`Person` 類別並沒有任何建構函式；在這種情況下，系統就會自動提供無參數建構函式，並將欄位初始化為其預設值。  
  
 [!code-csharp[csProgGuideObjects#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#8)]  
  
 請注意，`age` 的預設值是 `0`，而 `name` 的預設值是 `null`。
  
## <a name="example-3"></a>範例 3  
 下列範例示範如何使用基底類別初始設定式。 `Circle` 類別衍生自一般類別 `Shape`，而 `Cylinder` 類別衍生自`Circle` 類別。 每個衍生類別上的建構函式會使用其基底類別初始設定式。  
  
 [!code-csharp[csProgGuideObjects#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#9)]  
  
 如需更多基底類別建構函式的叫用範例，請參閱 [virtual](../../language-reference/keywords/virtual.md)、[override](../../language-reference/keywords/override.md) 和 [base](../../language-reference/keywords/base.md)。  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [類別和結構](./index.md)
- [建構函式](./constructors.md)
- [完成項](./destructors.md)
- [static](../../language-reference/keywords/static.md)
