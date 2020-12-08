---
title: 通用用戶端 Web 技術
description: 使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式 |常見的用戶端 web 技術
author: ardalis
ms.author: wiwagn
no-loc:
- Blazor
ms.date: 12/01/2020
ms.openlocfilehash: a4549e48152b21af05c67f601c1db65029e346fa
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851662"
---
# <a name="common-client-side-web-technologies"></a>通用用戶端 Web 技術

> 「網站應由內而外呈現最佳效果。」
> _- Paul Cookson_

ASP.NET Core 應用程式是 Web 應用程式，通常依賴於如 HTML、CSS 和 JavaScript 等用戶端 Web 技術。 藉由將頁面 (HTML) 的內容與其版面配置和樣式 (CSS) 分離開來，以及其行為 (透過 JavaScript)，複雜的 Web 應用程式可以利用關注點分離原則。 當這些問題並非密不可分時，未來對應用程式結構、設計或行為的變更，可以更容易進行。

雖然 HTML 和 CSS 相對穩定，但 JavaScript 透過開發人員使用應用程式架構和公用程式來建置 Web 型應用程式，正以驚人的速度發展。 本章探討 網頁程式開發人員使用 JavaScript 的幾種方式，並提供角度和回應用戶端程式庫的概要說明。

> [!NOTE]
> Blazor 提供 JavaScript 架構的替代方案，以建立豐富的互動式用戶端使用者介面。

## <a name="html"></a>HTML

HTML 是用來建立網頁和 web 應用程式的標準標記語言。 其項目形成頁面的建置組塊、表示格式化的文字、影像、表單輸入和其他結構。 當瀏覽器向 URL 提出要求時，無論是擷取頁面或應用程式，傳回的第一件事都是 HTML 文件。 此 HTML 文件可能會以 CSS 的形式參考或包含其外觀和版面配置的其他資訊，或以 JavaScript 的形式表現行為。

## <a name="css"></a>CSS

CSS (階層式樣式表) 用來控制 HTML 項目的外觀和版面配置。 CSS 樣式可直接套用至 HTML 項目，在同一頁面上個別定義或在不同的檔案中定義，並由頁面所參考。 樣式串聯基於如何用於選擇指定的 HTML 項目。 比方說，樣式可能適用於整個文件，但套用於特定項目的樣式可能會將其覆寫。 同樣地，專案特定的樣式會由套用至已套用至專案之 CSS 類別的樣式覆寫，而該樣式會以該專案的特定實例 (的樣式覆寫) 。 圖 6-1

![CSS 的明確規則](./media/image6-1.png)

**圖6-1。** CSS 精確性規則，按順序。

建議您保留樣式於各自的樣式表檔案中，並且使用基於選取範圍的串聯，來實作應用程式中一致且可重複使用的樣式。 應避免在 HTML 中放置樣式規則；並且將樣式套用於特定的單個項目 (而不是整個項目類別或套用特定 CSS 類別的項目) 應屬例外情況，而非規則。

### <a name="css-preprocessors"></a>CSS 前置處理器

CSS 樣式表缺少對條件邏輯、變數和其他程式設計語言功能的支援。 因此，大型樣式表單通常會包含相當多的重複專案，因為相同的色彩、字型或其他設定會套用至許多不同的 HTML 專案和 CSS 類別變化。 透過新增對變數和邏輯的支援，CSS 前置處理器可以幫助您的樣式表遵循 [DRY Principle](https://deviq.com/don-t-repeat-yourself/) (DRY 準則)。

最熱門的 CSS 前置處理器是 Sass 和 LESS。 兩者都擴充 CSS 並回溯相容，這表示一般的 CSS 檔案即為有效的 Sass 或 LESS 檔案。 Sass 基於 Ruby，LESS 基於 JavaScript，而兩者通常都是作為本機開發程序的一部分執行。 兩者都有可用的命令列工具，以及使用 Gulp 或 Grunt 工作執行它們的 Visual Studio 內建支援。

## <a name="javascript"></a>JavaScript

JavaScript 是一種動態、解譯的程式設計語言，已在 ECMAScript 語言規格中進行標準化。 其為 Web 程式設計語言。 與 CSS 一樣，JavaScript 可以在 HTML 項目中 (如同頁面內的指令碼區塊) 或在個別的檔案中定義為屬性。 就像 CSS 一樣，建議您將 JavaScript 組織成不同的檔案，讓它盡可能與個別網頁或應用程式視圖上找到的 HTML 分開。

在 Web 應用程式中使用 JavaScript 時，您通常需要執行幾項工作：

- 選取 HTML 項目並擷取及/或更新其值。

- 查詢 Web API 以取得資料。

- 將命令傳送至 Web API (並回應回呼及其結果)。

- 執行驗證。

您可以使用 JavaScript 來單獨執行所有這些工作，但有許多程式庫能使這些工作更容易。 這些程式庫的第一個和最成功之一是 jQuery，這些都是在網頁上簡化這些工作的常用選擇。 對於單頁應用程式 (SPA)，jQuery 並不提供許多 Angular 和 React 能提供的所需功能。

### <a name="legacy-web-apps-with-jquery"></a>使用 jQuery 的傳統 Web 應用程式

雖然古由 JavaScript 架構標準所組成，但是 jQuery 仍是常用於使用 HTML/CSS 的程式庫，並建立對 web Api 進行 AJAX 呼叫的應用程式。 然而，jQuery 在瀏覽器文件物件模型 (DOM) 層級上運作，且預設只提供命令式模型，而非宣告式模型。

例如，假設文字方塊的值超過 10，則頁面上的項目應該可見。 在 jQuery 中，這項功能通常是藉由撰寫程式碼的事件處理常式來執行，該程式碼會檢查 textbox 的值，並根據該值來設定目標專案的可見度。 此程式是以程式碼為基礎的必要方法。 另一個架構則可能會使用資料繫結，以宣告方式將項目可見性繫結於文字方塊的值。 這種方法不需要撰寫任何程式碼，而只需要裝飾與資料系結屬性相關的元素。 當用戶端的行為變得更複雜時，資料系結方法通常會產生較少的程式碼和條件複雜度較簡單的解決方案。

### <a name="jquery-vs-a-spa-framework"></a>jQuery vs SPA 架構

| **因素** | **jQuery** | **Angular**|
|--------------------------|------------|-------------|
| 提取 DOM | **是** | **是** |
| AJAX 支援 | **是** | **是** |
| 宣告式資料繫結 | **否** | **是** |
| MVC 樣式路由 | **否** | **是** |
| 範本化 | **否** | **是** |
| 深層連結路由 | **否** | **是** |

jQuery 本身缺少的大部分功能，都可以藉由新增其他程式庫來新增。 然而，像 Angular 這樣的 SPA 架構能以更加整合的方式提供這些功能，因為從一開始就是為這些功能而設計的。 此外，jQuery 是命令式程式庫，這表示您需要呼叫 jQuery 函式，才能使用 jQuery 進行任何動作。 SPA 框架提供的大部分工作和功能都可以透過宣告方式完成，而不需要撰寫實際的程式碼。

資料系結是這項功能的絕佳範例。 在 jQuery 中，通常只會使用一行程式碼來取得 DOM 專案的值，或設定元素的值。 不過，每當您需要變更元素的值時，您都必須撰寫此程式碼，有時這會發生在頁面上的多個函式中。 另一個常見範例是項目可見性。 在 jQuery 中，您可能會有許多不同的位置，讓您撰寫程式碼來控制是否可以看見某些元素。 在這些情況下，使用資料繫結時，不需要撰寫程式碼。 您只需將問題的值或可見度系結至頁面上的 *viewmodel* ，該 viewmodel 的變更就會自動反映在繫結項目中。

### <a name="angular-spas"></a>Angular SPA

角度仍是全球最受歡迎的 JavaScript 架構之一。 從角度2開始，小組會從頭開始重建架構 (使用 [TypeScript](https://www.typescriptlang.org/)) ，並從原始的 AngularJS 名稱更名至角度。 現在多年來，重新設計的角度持續成為建立單一頁面應用程式的強大架構。

Angular 應用程式是由元件所建置。 這些元件將 HTML 範本與特殊物件組合，並控制頁面的一部分。 Angular 文件的簡單元件如下所示：

```js
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<h1>Hello {{name}}</h1>`
})

export class AppComponent { name = 'Angular'; }
```

元件使用 @Component 裝飾項目函式進行定義，該函式採用關於元件的中繼資料。 選取器屬性會識別頁面上要顯示此元件的元素識別碼。 範本屬性是一個簡單的 HTML 範本，其中包含一個在最後一行定義、與元件名稱屬性對應的預留位置。

透過使用元件和範本，而不是 DOM 項目，Angular 應用程式可以在較高的抽象層次上運作，並且與僅使用 JavaScript (也稱為 "vanilla JS") 或使用 jQuery 撰寫的應用程式相比，整體程式碼更少。 Angular 也會對您如何組織用戶端指令檔施加一些順序。 按照慣例，Angular 應用程式使用通用資料夾結構，而模組和元件指令檔則位於應用程式資料夾中。 有關建置、部署和測試應用程式的 Angular 指令碼通常位於較高層級的資料夾中。

您可以使用 CLI 來開發角度應用程式。 在本機開始 Angular 開發 (假設您已經安裝了 git 和 npm)，只需從 GitHub 複製一個存放庫並執行 `npm install` 和 `npm start` 即可。 除此之外，角度也提供自己的 CLI，可建立專案、新增檔案，以及協助測試、包裝和部署工作。 此 CLI 易懂性使其與 ASP.NET Core 特別相容，也就是功能強大的 CLI 支援。

Microsoft 開發了一個參考應用程式 eShopOnContainers，其中包含一個 Angular SPA 實作。 這個應用程式包含 Angular 模組來管理線上商店的購物籃、從其目錄中載入和顯示項目，以及處理訂單建立。 您可以從 [GitHub](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Web/WebSPA) 檢視和下載範例應用程式。

### <a name="react"></a>React

與 Angular 提供完整的模型檢視控制器模式實作不同，React只關注檢視。 React 並不是一個架構，只是一個程式庫，所以若要建置 SPA 則需要利用額外的程式庫。 有許多程式庫都是設計用於回應，以產生豐富的單一頁面應用程式。

React 最重要的功能之一是使用虛擬 DOM。 虛擬 DOM 為 React 提供了幾項優勢，包括效能 (虛擬 DOM 可最佳化實際 DOM 的哪些部分需要更新) 和可測試性 (無需使用瀏覽器測試 React 及其與虛擬 DOM 的互動)。

React 在 HTML 的工作方式上也很獨特。 在程式碼和標記之間沒有嚴格的分隔 (或許是出現於 HTML 屬性中的 JavaScript 參考)，React 直接在 JavaScript 程式碼中新增 HTML 作為 JSX。 JSX 是 HTML 的類似語法，可以編譯成純 JavaScript。 例如︰

```js
<ul>
{ authors.map(author =>
    <li key={author.id}>{author.name}</li>
)}
</ul>
```

如果您已經了解 JavaScript，學習 React 應該很容易。 與 Angular 或其他熱門的程式庫相較之下，學習曲線或涉及的特殊語法非常少。

由於 React 不是完整的架構，所以通常需要其他程式庫來處理路由、Web API 呼叫和相依性管理等事項。 好處是您可以挑選最適合的程式庫，但缺點是您需要做出所有決策，並在完成後驗證所有選定的程式庫能夠順利協作。 如果您想要好的起步，可以使用 React Slingshot 之類可以將一組相容程式庫與 React 一起預先封裝的入門套件。

### <a name="vue"></a>Vue

《快速入門手冊》中的「Vue 是一種漸進式架構，用來建立使用者介面。 與其他整合型架構不同的是，Vue 是從頭開始設計，以累加 adoptable。 核心程式庫只著重于 view 層，而且很容易就能挑選和整合其他程式庫或現有專案。 另一方面，Vue 與新式工具和支援程式庫搭配使用時，能夠提供精密的 Single-Page 應用程式。」

開始使用 Vue 時，只需要將它的腳本包含在 HTML 檔案中即可：

```html
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

新增架構之後，您就可以使用 Vue 的直接樣板化語法，以宣告方式將資料轉譯成 DOM：

```html
<div id="app">
  {{ message }}
</div>
```

然後新增下列腳本：

```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```

這就足以呈現 "Hello Vue！" 在頁面上。 不過請注意，Vue 不只是將訊息轉譯為 div 一次。 它支援資料系結和動態更新，因此如果變更的值 `message` ，中的值 `<div>` 會立即更新以反映它。

當然，這只是 Vue 有哪些功能的表面。 在過去幾年來，我們獲得了極大的普及度，並有大型的社區。 [支援元件和程式庫有大量且持續成長的清單，這些元件和程式庫](https://github.com/vuejs/awesome-vue#redux)也可與 Vue 搭配使用來擴充。 如果您想要將用戶端行為新增至您的 web 應用程式，或考慮建立完整的 SPA，Vue 值得調查。

### <a name="no-locblazor-webassembly"></a>Blazor WebAssembly

不同于其他 JavaScript `Blazor WebAssembly` 架構，它是單一頁面應用程式， (SPA) 架構，可使用 .net 建立互動式用戶端 web 應用程式。 Blazor WebAssembly 使用開放式 web 標準，而不使用外掛程式或將程式碼重新編譯成其他語言。 Blazor WebAssembly 適用于所有新式網頁瀏覽器，包括行動瀏覽器。

WebAssembly (縮寫) 可讓您在網頁瀏覽器內執行 .NET 程式碼 `wasm` 。 WebAssembly 是一種精簡的位元組程式碼格式，針對快速下載和最快執行速度而最佳化。 WebAssembly 是開放式的 Web 標準，在不含外掛程式的網頁瀏覽器中支援。

WebAssembly 程式碼可以透過 JavaScript 存取瀏覽器的完整功能，稱為 JavaScript 互通性，通常會縮短為 JavaScript interop 或 JS interop。 在瀏覽器中透過 WebAssembly 執行的 .NET 程式碼會在瀏覽器的 JavaScript 沙箱執行，且受沙箱所提供對用戶端電腦之惡意動作的保護。

如需詳細資訊，請參閱[ASP.NET Core Blazor 簡介](https://docs.microsoft.com/aspnet/core/blazor/?view=aspnetcore-5.0)

### <a name="choosing-a-spa-framework"></a>選擇 SPA 架構

當考慮哪一個選項最適合支援您的 SPA 時，請記住下列考慮：

- 您的小組是否熟悉該架構和其相依性 (在某些情況下包括 TypeScript)？

- 該架構是否專斷，以及您是否同意其預設的運作方式？

- 該架構 (或附屬程式庫) 是否包含您應用程式所需的全部功能？

- 是否有妥善記錄？

- 在社群中有多活躍？ 是否正在建立新的專案？

- 其核心小組有多活躍？ 問題是否得到解決、新版本是否定期發出？

架構會持續以 breakneck 速度演進。 使用上面列出的考量，來協助減輕選擇架構時，可能造成日後後悔對其依賴的風險。 如果您特別注重風險，請考慮提供商業支援及/或 由大型企業開發的架構。

> ### <a name="references--client-web-technologies"></a>參考資料 – 用戶端 Web 技術
>
> - **HTML 和 CSS**  
> <https://www.w3.org/standards/webdesign/htmlcss>
> - **Sass 與 LESS 比較**  
> <https://www.keycdn.com/blog/sass-vs-less/>
> - **以 LESS、Sass 和 Font Awesome 設定樣式**  
> <https://docs.microsoft.com/aspnet/core/client-side/less-sass-fa>
> - **ASP.NET Core 中的用戶端開發**  
> <https://docs.microsoft.com/aspnet/core/client-side/>
> - **jQuery**  
> <https://jquery.com/>
> - **jQuery vs AngularJS**  
> <https://www.airpair.com/angularjs/posts/jquery-angularjs-comparison-migration-walkthrough>
> - **Angular**  
> <https://angular.io/>
> - **React**  
> <https://reactjs.org/>
> - **Vue**  
> <https://vuejs.org/>
> - **角度與反應 vs Vue：要在2020中選擇的架構**
> <https://www.codeinwp.com/blog/angular-vs-vue-vs-react/>
> - **2020中 Front-End 開發的最上層 JavaScript 架構**  
> <https://www.freecodecamp.org/news/complete-guide-for-front-end-developers-javascript-frameworks-2019/>

>[!div class="step-by-step"]
>[上一個](common-web-application-architectures.md) 
>[下一步](develop-asp-net-core-mvc-apps.md)
