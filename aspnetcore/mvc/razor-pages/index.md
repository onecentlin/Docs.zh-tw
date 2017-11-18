---
title: "ASP.NET Core 中的 Razor 頁面簡介"
author: Rick-Anderson
description: "此文件提供在 ASP.NET Core 中使用 Razor 頁面的概觀，以便於以頁面為焦點的案例之開發。"
keywords: "ASP.NET Core，Razor 頁面"
ms.author: riande
manager: wpickett
ms.date: 09/12/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/razor-pages/index
ms.openlocfilehash: 3112faa38bb9702f6856097e315c413f0974010d
ms.sourcegitcommit: 3ba32b2b6425ed94604cb0f681db0d5bb5f8ad58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2017
---
# <a name="introduction-to-razor-pages-in-aspnet-core"></a>ASP.NET Core 中的 Razor 頁面簡介

作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 與 [Ryan Nowak](https://github.com/rynowak)

Razor 頁面是 ASP.NET Core MVC 的新功能，更容易編寫以頁面為焦點的案例程式碼，也更具生產力。

如果您在尋找使用模型檢視控制器方法的教學課程，請參閱 [ASP.NET Core MVC 使用者入門](xref:tutorials/first-mvc-app/start-mvc)。

<a name="prerequisites"></a>

## <a name="aspnet-core-20-prerequisites"></a>ASP.NET Core 2.0 必要條件

安裝 [.NET Core](https://www.microsoft.com/net/core) 2.0.0 或更新版本。

如果您使用的是 Visual Studio，請安裝 [Visual Studio](https://www.visualstudio.com/vs/) 2017 15.3 版本或更新版本，加上下列工作負載：

* **ASP.NET 與網頁程式開發**
* **.NET Core 跨平台開發**

<a name="rpvs17"></a>

## <a name="creating-a-razor-pages-project"></a>建立 Razor 頁面專案

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

如需如何使用 Visual Studio 建立 Razor 頁面專案的詳細說明，請參閱[開始使用 Razor 頁面](xref:tutorials/razor-pages/razor-pages-start)。

#   <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

從命令列執行 `dotnet new razor`。

從 Visual Studio for Mac 開啟已產生的 *.csproj* 檔案。

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code) 

從命令列執行 `dotnet new razor`。

#   <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli) 

從命令列執行 `dotnet new razor`。

---

## <a name="razor-pages"></a>Razor 頁面

Razor 頁面是在 *Startup.cs* 中啟用：

[!code-cs[main](index/sample/RazorPagesIntro/Startup.cs?name=snippet_Startup)]

請考慮使用基本頁面：<a name="OnGet"></a>

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index.cshtml)]

上述程式碼看起來很像 Razor 檢視檔案。 讓它不同的是 `@page` 指示詞。 `@page` 會將檔案轉換成 MVC 動作，這表示它會直接處理要求，不用透過控制器。 `@page` 必須是頁面上的第一個 Razor 指示詞。 `@page` 會影響其他的 Razor 建構行為。

使用 `PageModel` 類別的類似頁面，顯示於下列兩個檔案中。 *Pages/Index2.cshtml* 檔案：

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml)]

*Pages/Index2.cshtml.cs*「程式碼後置」檔案：

[!code-cs[main](index/sample/RazorPagesIntro/Pages/Index2.cshtml.cs)]

依照慣例，`PageModel` 類別檔和附加 *.cs* 檔名的 Razor 頁面檔案名稱相同。 例如，前一個 Razor 頁面是 *Pages/Index2.cshtml*。 包含 `PageModel` 類別的檔案名為 *Pages/Index2.cshtml.cs*。

頁面的 URL 路徑關聯是由頁面在檔案系統中的位置決定。 下表顯示 Razor 頁面路徑和相符的 URL：

| 檔案名稱和路徑               | 比對 URL |
| ----------------- | ------------ |
| */Pages/Index.cshtml* | `/` 或 `/Index` |
| */Pages/Contact.cshtml* | `/Contact` |
| */Pages/Store/Contact.cshtml* | `/Store/Contact` |
| */Pages/Store/Index.cshtml* | `/Store` 或 `/Store/Index` |

附註：

* 執行階段預設會在 *Pages* 資料夾中尋找 Razor 頁面的檔案。
* `Index` 是 URL 未包含頁面時的預設頁面。

## <a name="writing-a-basic-form"></a>撰寫基本表單

Razor 頁面功能旨在讓常見模式容易搭配網頁瀏覽器使用。 [模型繫結](xref:mvc/models/model-binding)、[標記協助程式](xref:mvc/views/tag-helpers/intro)和 HTML 協助程式搭配 Razor 頁面類別中定義的屬性「就這麼簡單」。 `Contact` 模型請考慮實作基本的「與我們連絡」格式頁面：

本文件中的範例，會在 [Startup.cs](https://github.com/aspnet/Docs/blob/master/aspnetcore/mvc/razor-pages/index/sample/RazorPagesContacts/Startup.cs#L15-L16) 檔案中初始化 `DbContext`。

[!code-cs[main](index/sample/RazorPagesContacts/Startup.cs?highlight=15-16)]

資料模型：

[!code-cs[main](index/sample/RazorPagesContacts/Data/Customer.cs)]

*Pages/Create.cshtml* 檢視檔案：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml)]

*Pages/Create.cshtml.cs* 程式碼後置檔案供檢視之用：

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_ALL)]

依照慣例，`PageModel` 類別稱之為 `<PageName>Model`，與頁面位於相同的命名空間。

使用 `PageModel` 程式碼後置檔案可支援單元測試，但需要撰寫明確的建構函式和類別。 沒有 `PageModel` 程式碼後置檔案的頁面支援執行階段編譯，這會是開發中的優勢。  <!-- review: advantage because you can make changes and refresh the browser without explicitly compiling the app -->

在 `POST` 要求上執行的頁面具有 `OnPostAsync`「處理常式方法」 (當使用者張貼表單時)。 您可以新增任何 HTTP 指令動詞的處理常式方法。 最常見的處理常式包括：

* `OnGet`，初始化頁所需要的狀態。 [OnGet](#OnGet) 範例。
* `OnPost`，處理表單提交作業。

`Async` 命名尾碼是選擇性的，但依照慣例通常用於非同步函式。 上例中的 `OnPostAsync` 程式碼看起來類似您一般在控制器中撰寫的內容。 上述程式碼一般用於 Razor 頁面。 大部分的基本 MVC，像是[模型繫結](xref:mvc/models/model-binding)、[驗證](xref:mvc/models/validation)和動作結果都是共用的。  <!-- Review: Ryan, can we get a list of what is shared and what isn't? -->

前一個 `OnPostAsync` 方法：

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync)]

`OnPostAsync` 的基本流程：

檢查驗證錯誤。

*  如果沒有任何錯誤，會儲存資料並重新導向。
*  如果有錯誤，會再次顯示有驗證訊息的頁面。 用戶端驗證和傳統的 ASP.NET Core MVC 應用程式完全相同。 在許多情況下，用戶端會偵測到驗證錯誤，但從不提交給伺服器。

成功輸入資料後，`OnPostAsync` 處理常式方法會呼叫 `RedirectToPage` 協助程式方法，傳回 `RedirectToPageResult` 的執行個體。 `RedirectToPage` 是新的動作結果，類似於 `RedirectToAction` 或 `RedirectToRoute`，但會針對頁面自訂。 在上述範例中，它會重新導向至根索引頁面 (`/Index`)。 [產生頁面 URL](#url_gen)一節會詳細說明 `RedirectToPage`。

當提交的表單有驗證錯誤時 (傳遞至伺服器)，`OnPostAsync` 處理常式方法會呼叫 `Page` 協助程式方法。 `Page` 傳回 `PageResult` 的執行個體。 傳回 `Page` 類似於控制站中的動作傳回 `View`。 `PageResult` 是處理常式方法的預設 <!-- Review  --> 傳回型別。 傳回 `void` 的處理常式方法會呈現頁面。

`Customer` 屬性 (property) 使用 `[BindProperty]` 屬性 (attribute) 加入模型繫結。

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_PageModel&highlight=10-11)]

Razor 頁面預設只繫結屬性和非 GET 指令動詞。 繫結至屬性可以減少您必須撰寫的程式碼數量。 透過使用相同的屬性呈現表單欄位 (`<input asp-for="Customer.Name" />`) 並接受輸入，繫結可以減少程式碼。

首頁 (*Index.cshtml*)：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml)]

程式碼後置 *Index.cshtml.cs* 檔案：

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs)]

*Index.cshtml* 檔案包含下列標記可為每個連絡人建立編輯連結：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=21)]

[錨定標記協助程式](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)過去使用 [asp-route-{value}](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper#route) 屬性產生 [編輯] 頁面的連結。 該連結包含路由資料和連絡人識別碼。 例如，`http://localhost:5000/Edit/1`。

*Pages/Edit.cshtml* 檔案：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml?highlight=1)]

第一行包含 `@page "{id:int}"` 指示詞。 路由條件約束 `"{id:int}"` 通知頁面接受包含 `int` 路由資料的頁面要求。 如果頁面要求不包含可以轉換成 `int` 的路由資料，執行階段會傳回 HTTP 404 (找不到) 錯誤。

*Pages/Edit.cshtml.cs* 檔案：

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Edit.cshtml.cs)]

*Index.cshtml* 檔案也包含能夠為每個客戶連絡人建立刪除按鈕的標記：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Index.cshtml?range=22-23)]

使用 HTML 轉譯刪除按鈕時，其 `formaction` 會包含下列項目的參數：

* `asp-route-id` 屬性指定的客戶連絡人識別碼。
* `asp-page-handler` 屬性指定的 `handler`。

以下是轉譯的刪除按鈕範例，內含客戶連絡人識別碼 `1`：

```html
<button type="submit" formaction="/?id=1&amp;handler=delete">delete</button>
```

選取按鈕時，表單 `POST` 要求會傳送至伺服器。 依照慣例，會依據配置 `OnPost[handler]Async` 按 `handler` 參數的值來選取處理常式方法。

在此範例中，因為 `handler` 為 `delete`，所以會使用 `OnPostDeleteAsync` 處理常式方法來處理 `POST` 要求。 若 `asp-page-handler` 設為其他值 (例如 `remove`)，則會選取名為 `OnPostRemoveAsync` 的頁面處理常式。

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Index.cshtml.cs?range=26-37)]

`OnPostDeleteAsync` 方法：

* 接受查詢字串的 `id`。
* 使用 `FindAsync` 在資料庫中查詢客戶連絡人。
* 若找到客戶連絡人，會從客戶連絡人清單中予以移除。 資料庫隨即更新。
* 呼叫 `RedirectToPage` 以重新導向至根索引頁 (`/Index`)。

<a name="xsrf"></a>

## <a name="xsrfcsrf-and-razor-pages"></a>XSRF/CSRF 和 Razor 頁面

您不必撰寫任何[防偽驗證](xref:security/anti-request-forgery)程式碼。 防偽權杖的產生和驗證會自動包含在 Razor 頁面中。

<a name="layout"></a>
## <a name="using-layouts-partials-templates-and-tag-helpers-with-razor-pages"></a>搭配 Razor 頁面使用版面配置、部分、範本和標記協助程式。

頁面使用 Razor 檢視引擎的所有功能。 版面配置、部分、範本、標記協助程式、*_ViewStart.cshtml*、*_ViewImports.cshtml* 運作方式一如它們在傳統 Razor 檢視中的方式。

利用這些功能的一部分來清理此頁面。

將[版面配置頁面](xref:mvc/views/layout)新增至 *Pages/_Layout.cshtml*：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_LayoutSimple.cshtml)]

[配置](xref:mvc/views/layout)：

* 控制每個頁面的版面配置 (除非頁面退出版面配置)。
* 匯入 HTML 結構，例如 JavaScript 和樣式表。

如需詳細資訊，請參閱[版面配置頁面](xref:mvc/views/layout)。

[版面配置](xref:mvc/views/layout#specifying-a-layout)屬性是在 *Pages/_ViewStart.cshtml* 中設定：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewStart.cshtml)]

**注意：**版面配置是在 *Pages* 資料夾中。 頁面會以階層方式尋找其他檢視 (版面配置、範本、部分)，從目前頁面的相同資料夾開始。 您可以從任何 Razor 頁面下的 *Pages* 資料夾中，使用 *Pages* 資料夾中的版面配置。

我們**不**建議您將配置檔案放入 *Views/Shared* 資料夾。 *Views/Shared* 是 MVC 檢視模式。 Razor 頁面應該要依賴資料夾階層，不是路徑慣例。

Razor 頁面的檢視搜尋包括 *Pages* 資料夾。 搭配 MVC 控制器使用的版面配置、範本和部分以及傳統的 Razor 檢視「就這麼簡單」。

新增 *Pages/_ViewImports.cshtml* 檔案：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml)]

本教學課程稍後會說明 `@namespace`。 `@addTagHelper` 指示詞會將[內建標記協助程式](xref:mvc/views/tag-helpers/builtin-th/Index)帶入 *Pages* 資料夾中的所有頁面。

<a name="namespace"></a>

在頁面上明確使用 `@namespace` 指示詞時：

[!code-cshtml[main](index/sample/RazorPagesIntro/Pages/Customers/Namespace2.cshtml?highlight=2)]

指示詞會設定頁面的命名空間。 `@model` 指示詞不需要包含命名空間。

當 `@namespace` 指示詞包含在 *_ViewImports.cshtml* 中時，指定的命名空間會在匯入 `@namespace` 指示詞的頁面中提供所產生之命名空間的前置詞。 所產生命名空間的其餘部分 (後置字元部分) 是包含 *_ViewImports.cshtml* 的資料夾和包含頁面的資料夾之間，以句點分隔的相對路徑。

例如，程式碼後置檔案*Pages/Customers/Edit.cshtml.cs* 會以明確方式設定命名空間：

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/Edit.cshtml.cs?name=snippet_namespace)]

*Pages/_ViewImports.cshtml* 檔案會設定下列命名空間：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/_ViewImports.cshtml?highlight=1)]

針對 *Pages/Customers/Edit.cshtml* Razor 頁面產生的命名空間和程式碼後置檔案相同。 `@namespace` 指示詞的設計是為了將 C# 類別新增至專案，頁面產生的程式碼「就這麼簡單」，不必為程式碼後置檔案新增 `@using` 指示詞。

**注意：**`@namespace`也適用於傳統的 Razor 檢視。

原始的 *Pages/Create.cshtml* 檢視檔案：

[!code-cshtml[main](index/sample/RazorPagesContacts/Pages/Create.cshtml?highlight=2)]

更新的 *Pages/Create.cshtml* 檢視檔案：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/Create.cshtml?highlight=2)]

[Razor 頁面入門專案](#rpvs17)包含 *Pages/_ValidationScriptsPartial.cshtml*，連結用戶端驗證。

<a name="url_gen"></a>

## <a name="url-generation-for-pages"></a>產生頁面 URL

前面出現過的 `Create` 頁面使用 `RedirectToPage`：

[!code-cs[main](index/sample/RazorPagesContacts/Pages/Create.cshtml.cs?name=snippet_OnPostAsync&highlight=10)]

應用程式有下列檔案/資料夾結構：

* */Pages*

  * *Index.cshtml*
  * */Customer*

    * *Create.cshtml*
    * *Edit.cshtml*
    * *Index.cshtml*

*Pages/Customers/Create.cshtml* 和 *Pages/Customers/Edit.cshtml* 頁面在成功後會重新導向至 *Pages/Index.cshtml*。 字串 `/Index` 為 URI 的一部分，可存取前一個頁面。 字串 `/Index` 可以用來產生 *Pages/Index.cshtml* 頁面的 URI。 例如: 

* `Url.Page("/Index", ...)`
* `<a asp-page="/Index">My Index Page</a>`
* `RedirectToPage("/Index")`

頁面名稱是來自根 */Pages* 資料夾的頁面路徑 (包括前置的 `/`，例如 `/Index`)。 上述的 URL 產生範例比僅有硬式編碼的 URL 更有特色。 URL 產生使用[路由](xref:mvc/controllers/routing)，可以根據路由在目的地路徑中定義的方式，產生並且編碼參數。

產生頁面 URL 支援相關的名稱。 下表顯示從 *Pages/Customers/Create.cshtml* 以不同的 `RedirectToPage` 參數選取的索引頁：

| RedirectToPage(x)| 頁面 |
| ----------------- | ------------ |
| RedirectToPage("/Index") | *Pages/Index* |
| RedirectToPage("./Index"); | *Pages/Customers/Index* |
| RedirectToPage("../Index") | *Pages/Index* |
| RedirectToPage("Index")  | *Pages/Customers/Index* |

`RedirectToPage("Index")`、`RedirectToPage("./Index")` 和 `RedirectToPage("../Index")` 是「相對名稱」。 `RedirectToPage` 參數「結合」了目前頁面的路徑，以計算目的地頁面的名稱。  <!-- Review: Original had The provided string is combined with the page name of the current page to compute the name of the destination page. -- page name, not page path -->

相對名稱連結在以複雜結構建置網站時很有用。 如果您使用相對名稱連結資料夾中的頁面，您可以重新命名該資料夾。 所有連結仍可運作 (因為它們不包含資料夾名稱)。

## <a name="tempdata"></a>TempData

ASP.NET Core 公開[控制器](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller)上的 [TempData](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.controller#Microsoft_AspNetCore_Mvc_Controller_TempData) 屬性。 這個屬性會儲存資料，直到讀取為止。 `Keep` 和 `Peek` 方法可以用來檢查資料，不用刪除。 當有多個要求需要資料時，`TempData` 對重新導向很有幫助。

`[TempData]` 是 ASP.NET Core 2.0 的新屬性，在控制站和頁面都受支援。

下列程式碼會設定使用 `TempData` 的 `Message` 值：

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateDot.cshtml.cs?highlight=10-11,25&name=snippet_Temp)]

*Pages/Customers/Index.cshtml* 檔案中的下列標記會顯示使用 `TempData` 的 `Message` 值。

```cshtml
<h3>Msg: @Model.Message</h3>
```

*Pages/Customers/Index.cshtml.cs* 程式碼後置檔案會將 `[TempData]` 屬性 (attribute) 套用到 `Message` 屬性 (property)。

```cs
[TempData]
public string Message { get; set; }
```

如需詳細資訊，請參閱 [TempData](xref:fundamentals/app-state#temp)。

<a name="mhpp"></a>
## <a name="multiple-handlers-per-page"></a>每頁面有多個處理常式

下列頁面會使用 `asp-page-handler` 標記協助程式為兩個頁面處理常式產生標記：

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?highlight=12-13)]

<!-- Review: the FormActionTagHelper applies to all <form /> elements on a Razor page, even when there is no `asp-` attribute   -->

上例中的表單有兩個提交按鈕，每一個都使用 `FormActionTagHelper` 提交至不同的 URL。 `asp-page-handler` 屬性附隨於 `asp-page`。 `asp-page-handler` 產生的 URL 會提交至頁面所定義的每一個處理常式方法。 因為範例連結至目前的頁面，所以未指定 `asp-page`。

程式碼後置檔案：

[!code-cs[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml.cs?highlight=20,32)]

上述程式碼使用「具名的處理常式方法」。 具名的處理常式方法的建立方式是採用名稱中在 `On<HTTP Verb>` 後面、`Async` 之前 (如有) 的文字。 在上例中，頁面方法是 OnPost**JoinList**Async 和 OnPost**JoinListUC**Async。 移除 *OnPost* 和 *Async*，處理常式名稱就是 `JoinList` 和 `JoinListUC`。

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateFATH.cshtml?range=12-13)]

使用上述程式碼，提交至 `OnPostJoinListAsync` 的 URL 路徑是 `http://localhost:5000/Customers/CreateFATH?handler=JoinList`。 提交至 `OnPostJoinListUCAsync` 的 URL 路徑是 `http://localhost:5000/Customers/CreateFATH?handler=JoinListUC`。

## <a name="customizing-routing"></a>自訂路由

如果您不喜歡 URL 有查詢字串 `?handler=JoinList`，您可以變更路由，將處理常式名稱置於 URL 的路徑部分。 您可以新增路由範本，在 `@page` 指示詞後面用雙引號括住，以自訂路由。

[!code-cshtml[main](index/sample/RazorPagesContacts2/Pages/Customers/CreateRoute.cshtml?highlight=1)]

上述的路由會將處理常式名稱放入 URL 路徑，而不是放入查詢字串。 跟在 `handler` 後面的 `?` 表示路由參數為選擇性。

您可以使用 `@page` 將額外的區段和參數新增至頁面的路由。 無論什麼都**附加**至頁面的預設路由。 不支援使用絕對或虛擬路徑變更頁面的路由 (例如 `"~/Some/Other/Path"`)。

## <a name="configuration-and-settings"></a>組態與設定

若要設定進階選項，請在 MVC 產生器上使用擴充方法 `AddRazorPagesOptions`：

[!code-cs[main](index/sample/RazorPagesContacts/StartupAdvanced.cs?name=snippet_1)]

目前可以使用 `RazorPagesOptions` 設定頁面的根目錄，或新增頁面的應用程式模型慣例。 我們希望未來能以這種方式獲得更多的擴充性。

若要先行編譯檢視，請參閱 [Razor 檢視編譯](xref:mvc/views/view-compilation)。

[下載或檢視範例程式碼](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/razor-pages/index/sample)。

請參閱根據本簡介建置的[開始使用 ASP.NET Core 中的 Razor 頁面](xref:tutorials/razor-pages/razor-pages-start)。
