---
title: "檢查 Details 和 Delete 方法"
author: rick-anderson
description: "簡易 ASP.NET Core MVC 應用程式中的 Details 控制器方法和檢視。"
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.assetid: 870192b4-8d4f-45c7-8c14-83d02bc0ad79
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/details
ms.openlocfilehash: bab93a2faa122d9d6d2e71367519baa09bd76bd1
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2017
---
# <a name="examining-the-details-and-delete-methods"></a><span data-ttu-id="eac1b-104">檢查 Details 和 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="eac1b-104">Examining the Details and Delete methods</span></span>

<span data-ttu-id="eac1b-105">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="eac1b-105">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="eac1b-106">開啟 Movie 控制器，並檢查 `Details` 方法：</span><span class="sxs-lookup"><span data-stu-id="eac1b-106">Open the Movie controller and examine the `Details` method:</span></span>

<span data-ttu-id="eac1b-107">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_details)]</span><span class="sxs-lookup"><span data-stu-id="eac1b-107">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_details)]</span></span>

<span data-ttu-id="eac1b-108">建立這個動作方法的 MVC scaffolding 引擎，會新增一項註解以顯示叫用方法的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="eac1b-108">The MVC scaffolding engine that created this action method adds a comment showing an HTTP request that invokes the method.</span></span> <span data-ttu-id="eac1b-109">在此情況下，它是含有 `Movies` 控制器、`Details` 方法和 `id` 值這三個 URL 區段的 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="eac1b-109">In this case it's a GET request with three URL segments, the `Movies` controller, the `Details` method and an `id` value.</span></span> <span data-ttu-id="eac1b-110">回想一下，這些區段會在 *Startup.cs* 中定義。</span><span class="sxs-lookup"><span data-stu-id="eac1b-110">Recall these segments are defined in *Startup.cs*.</span></span>

<span data-ttu-id="eac1b-111">[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]</span><span class="sxs-lookup"><span data-stu-id="eac1b-111">[!code-csharp[Main](start-mvc/sample/MvcMovie/Startup.cs?highlight=5&name=snippet_1)]</span></span>

<span data-ttu-id="eac1b-112">EF 可讓您輕鬆使用 `SingleOrDefaultAsync` 方法來搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="eac1b-112">EF makes it easy to search for data using the `SingleOrDefaultAsync` method.</span></span> <span data-ttu-id="eac1b-113">此方法內建一項重要的安全性功能：程式碼會先驗證搜尋方法是否已找到電影，之後才嘗試對其執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="eac1b-113">An important security feature built into the method is that the code verifies that the search method has found a movie before it tries to do anything with it.</span></span> <span data-ttu-id="eac1b-114">比方說，駭客可能會將透過 `http://localhost:xxxx/Movies/Details/1` 連結建立的 URL 變更為類似 `http://localhost:xxxx/Movies/Details/12345` (或不代表實際電影的其他值)，導致站台發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="eac1b-114">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like  `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="eac1b-115">如果您未檢查是否有 null 的電影，應用程式會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="eac1b-115">If you did not check for a null movie, the app would throw an exception.</span></span>

<span data-ttu-id="eac1b-116">檢查 `Delete` 和 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="eac1b-116">Examine the `Delete` and `DeleteConfirmed` methods.</span></span>

<span data-ttu-id="eac1b-117">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete)]</span><span class="sxs-lookup"><span data-stu-id="eac1b-117">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete)]</span></span>

<span data-ttu-id="eac1b-118">請注意，`HTTP GET Delete` 方法並不會刪除指定的電影，而會傳回電影的檢視，您可在該檢視中提交 (HttpPost) 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="eac1b-118">Note that the `HTTP GET Delete` method doesn't delete the specified movie, it returns a view of the movie where you can submit (HttpPost) the deletion.</span></span> <span data-ttu-id="eac1b-119">如果您執行刪除作業以回應 GET 要求 (或是執行相關編輯作業、建立作業或任何會變更資料的其他作業)，則會造成安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="eac1b-119">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span>

<span data-ttu-id="eac1b-120">我們將可刪除資料的 `[HttpPost]` 方法命名為 `DeleteConfirmed`，以提供 HTTP POST 方法的唯一簽章或名稱。</span><span class="sxs-lookup"><span data-stu-id="eac1b-120">The `[HttpPost]` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="eac1b-121">這兩個方法簽章如下所示：</span><span class="sxs-lookup"><span data-stu-id="eac1b-121">The two method signatures are shown below:</span></span>

<span data-ttu-id="eac1b-122">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete2)]</span><span class="sxs-lookup"><span data-stu-id="eac1b-122">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete2)]</span></span>

<span data-ttu-id="eac1b-123">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete3)]</span><span class="sxs-lookup"><span data-stu-id="eac1b-123">[!code-csharp[Main](start-mvc/sample/MvcMovie/Controllers/MoviesController.cs?name=snippet_delete3)]</span></span>


<span data-ttu-id="eac1b-124">通用語言執行平台 (CLR) 需要多載方法，以提供唯一的參數簽章 (方法名稱相同但參數清單不同)。</span><span class="sxs-lookup"><span data-stu-id="eac1b-124">The common language runtime (CLR) requires overloaded methods to have a unique parameter signature (same method name but different list of parameters).</span></span> <span data-ttu-id="eac1b-125">不過，此處您需要兩個 `Delete` 方法，一個用於 GET，另一個用於 POST，且兩者都具有相同的參數簽章</span><span class="sxs-lookup"><span data-stu-id="eac1b-125">However, here you need two `Delete` methods -- one for GET and one for POST -- that both have the same parameter signature.</span></span> <span data-ttu-id="eac1b-126">(它們都需要接受單一整數作為參數)。</span><span class="sxs-lookup"><span data-stu-id="eac1b-126">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="eac1b-127">針對這個問題，有兩種解決方法：一個是為方法提供不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="eac1b-127">There are two approaches to this problem, one is to give the methods different names.</span></span> <span data-ttu-id="eac1b-128">這是 scaffolding 機制在上述範例採取的方法。</span><span class="sxs-lookup"><span data-stu-id="eac1b-128">That's what the scaffolding mechanism did in the preceding example.</span></span> <span data-ttu-id="eac1b-129">不過，這麼做會導致一個小問題：ASP.NET 會依名稱將 URL 區段與動作方法對應，一旦您重新命名方法，路由通常就會找不到這個方法。</span><span class="sxs-lookup"><span data-stu-id="eac1b-129">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="eac1b-130">解決辦法正如您看到的這個範例：將 `ActionName("Delete")` 屬性新增至 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="eac1b-130">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="eac1b-131">該屬性會執行路由系統的對應，以讓含有 POST 要求之 /Delete/ 的 URL 找到 `DeleteConfirmed` 方法。</span><span class="sxs-lookup"><span data-stu-id="eac1b-131">That attribute performs mapping for the routing system so that a URL that includes /Delete/ for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="eac1b-132">如果若干方法具有相同名稱和簽章，另一個常見解決辦法是以人為方式變更 POST 方法的簽章，以包含額外 (未使用) 的參數。</span><span class="sxs-lookup"><span data-stu-id="eac1b-132">Another common work around for methods that have identical names and signatures is to artificially change the signature of the POST method to include an extra (unused) parameter.</span></span> <span data-ttu-id="eac1b-133">這也是我們在上一篇文章中新增 `notUsed` 參數時所執行的操作。</span><span class="sxs-lookup"><span data-stu-id="eac1b-133">That's what we did in a previous post when we added the `notUsed` parameter.</span></span> <span data-ttu-id="eac1b-134">針對這裡的 `[HttpPost] Delete` 方法，您可以執行相同的動作：</span><span class="sxs-lookup"><span data-stu-id="eac1b-134">You could do the same thing here for the `[HttpPost] Delete` method:</span></span>

```csharp
// POST: Movies/Delete/6
[ValidateAntiForgeryToken]
public async Task<IActionResult> Delete(int id, bool notUsed)
```

<span data-ttu-id="eac1b-135">感謝您看完這份 ASP.NET Core MVC 簡介。</span><span class="sxs-lookup"><span data-stu-id="eac1b-135">Thanks for completing this introduction to ASP.NET Core MVC.</span></span> <span data-ttu-id="eac1b-136">歡迎您提供任何指教。</span><span class="sxs-lookup"><span data-stu-id="eac1b-136">We appreciate any comments you leave.</span></span> <span data-ttu-id="eac1b-137">完成本教學課程之後，非常建議您繼續參閱 [MVC 和 EF Core 使用者入門](xref:data/ef-mvc/intro)。</span><span class="sxs-lookup"><span data-stu-id="eac1b-137">[Getting started with MVC and EF Core](xref:data/ef-mvc/intro) is an excellent follow up to this tutorial.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="eac1b-138">上一步</span><span class="sxs-lookup"><span data-stu-id="eac1b-138">Previous</span></span>](validation.md)