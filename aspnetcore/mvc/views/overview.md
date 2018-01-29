---
title: Widoki w podstawowej platformy ASP.NET MVC
author: ardalis
description: "Dowiedz się, jak widoki obsługi aplikacji prezentacji danych i interakcji z użytkownikiem w nazwie wzorca MVC ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 12/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/overview
ms.openlocfilehash: b88c3ea05e37a82c7bcbde953c10a04ce1943dc5
ms.sourcegitcommit: 09b342b45e7372ba9ebf17f35eee331e5a08fb26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2018
---
# <a name="views-in-aspnet-core-mvc"></a><span data-ttu-id="37860-103">Widoki w podstawowej platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="37860-103">Views in ASP.NET Core MVC</span></span>

<span data-ttu-id="37860-104">Przez [Steve Smith](https://ardalis.com/) i [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="37860-104">By [Steve Smith](https://ardalis.com/) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="37860-105">W tym dokumencie opisano widoki używane w aplikacjach ASP.NET Core MVC.</span><span class="sxs-lookup"><span data-stu-id="37860-105">This document explains views used in ASP.NET Core MVC applications.</span></span> <span data-ttu-id="37860-106">Aby uzyskać informacje na stronach Razor, zobacz [wprowadzenie do stron Razor](xref:mvc/razor-pages/index).</span><span class="sxs-lookup"><span data-stu-id="37860-106">For information on Razor Pages, see [Introduction to Razor Pages](xref:mvc/razor-pages/index).</span></span>

<span data-ttu-id="37860-107">W **M**odelu -**V**rzeglądaj -**C**wzorzec ontroller (MVC) *widoku* obsługuje interakcję danych aplikacji prezentacji i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37860-107">In the **M**odel-**V**iew-**C**ontroller (MVC) pattern, the *view* handles the app's data presentation and user interaction.</span></span> <span data-ttu-id="37860-108">Widok jest szablonu HTML z osadzonych [znaczników Razor](xref:mvc/views/razor).</span><span class="sxs-lookup"><span data-stu-id="37860-108">A view is an HTML template with embedded [Razor markup](xref:mvc/views/razor).</span></span> <span data-ttu-id="37860-109">Kod znaczników razor jest kod, który współdziała z kod znaczników HTML do tworzenia strony sieci Web, które są wysyłane do klienta.</span><span class="sxs-lookup"><span data-stu-id="37860-109">Razor markup is code that interacts with HTML markup to produce a webpage that's sent to the client.</span></span>

<span data-ttu-id="37860-110">W programie ASP.NET Core MVC, widoki są *.cshtml* pliki, które używają [język programowania C#](/dotnet/csharp/) w znaczniku Razor.</span><span class="sxs-lookup"><span data-stu-id="37860-110">In ASP.NET Core MVC, views are *.cshtml* files that use the [C# programming language](/dotnet/csharp/) in Razor markup.</span></span> <span data-ttu-id="37860-111">Zwykle, Wyświetl pliki są podzielone na foldery o nazwie dla każdej aplikacji [kontrolerów](xref:mvc/controllers/actions).</span><span class="sxs-lookup"><span data-stu-id="37860-111">Usually, view files are grouped into folders named for each of the app's [controllers](xref:mvc/controllers/actions).</span></span> <span data-ttu-id="37860-112">Foldery są przechowywane w *widoków* folder w katalogu głównym aplikacji:</span><span class="sxs-lookup"><span data-stu-id="37860-112">The folders are stored in a *Views* folder at the root of the app:</span></span>

![Widoki folder w rozwiązaniu Explorer programu Visual Studio jest otwarty z folderu głównej otwarte, aby wyświetlić pliki About.cshtml, Contact.cshtml i Index.cshtml](overview/_static/views_solution_explorer.png)

<span data-ttu-id="37860-114">*Home* kontrolera jest reprezentowana przez *Home* folder wewnątrz *widoków* folderu.</span><span class="sxs-lookup"><span data-stu-id="37860-114">The *Home* controller is represented by a *Home* folder inside the *Views* folder.</span></span> <span data-ttu-id="37860-115">*Home* folder zawiera widoki dla *o*, *skontaktuj się z*, i *indeksu* stron sieci Web (strona główna).</span><span class="sxs-lookup"><span data-stu-id="37860-115">The *Home* folder contains the views for the *About*, *Contact*, and *Index* (homepage) webpages.</span></span> <span data-ttu-id="37860-116">Gdy użytkownik zażąda jeden z tych trzech stron internetowych akcji kontrolera w *Home* kontrolera ustalić, który z trzech widoków jest używane do tworzenia i zwraca go użytkownikowi strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="37860-116">When a user requests one of these three webpages, controller actions in the *Home* controller determine which of the three views is used to build and return a webpage to the user.</span></span>

<span data-ttu-id="37860-117">Użyj [układów](xref:mvc/views/layout) sekcje spójne strony sieci Web i obniżyć powtarzania kodu.</span><span class="sxs-lookup"><span data-stu-id="37860-117">Use [layouts](xref:mvc/views/layout) to provide consistent webpage sections and reduce code repetition.</span></span> <span data-ttu-id="37860-118">Układy często zawierają nagłówka, elementy nawigacji i menu i stopki.</span><span class="sxs-lookup"><span data-stu-id="37860-118">Layouts often contain the header, navigation and menu elements, and the footer.</span></span> <span data-ttu-id="37860-119">Nagłówku i stopce zazwyczaj zawiera schematyczny znaczników dla wielu elementów metadanych i linki do zasobów skryptu i stylu.</span><span class="sxs-lookup"><span data-stu-id="37860-119">The header and footer usually contain boilerplate markup for many metadata elements and links to script and style assets.</span></span> <span data-ttu-id="37860-120">Układy pomóc w uniknięciu tego znacznika umożliwiającego w widoków.</span><span class="sxs-lookup"><span data-stu-id="37860-120">Layouts help you avoid this boilerplate markup in your views.</span></span>

<span data-ttu-id="37860-121">[Widoki częściowe](xref:mvc/views/partial) ograniczyć zduplikowania kodu za pomocą wielokrotnego użytku części widoków zarządzania.</span><span class="sxs-lookup"><span data-stu-id="37860-121">[Partial views](xref:mvc/views/partial) reduce code duplication by managing reusable parts of views.</span></span> <span data-ttu-id="37860-122">Na przykład widoku częściowego jest przydatne w przypadku autora biografię na blogu witryny sieci Web wyświetlaną w kilka widoków.</span><span class="sxs-lookup"><span data-stu-id="37860-122">For example, a partial view is useful for an author biography on a blog website that appears in several views.</span></span> <span data-ttu-id="37860-123">Biografię autora jest zwykłej Wyświetl zawartość i nie wymaga kod do wykonania w celu uzyskania zawartości strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="37860-123">An author biography is ordinary view content and doesn't require code to execute in order to produce the content for the webpage.</span></span> <span data-ttu-id="37860-124">Autor biografię zawartość jest dostępna do widoku przez powiązanie modelu samodzielnie, więc używanie widoku częściowego dla tego typu zawartości jest idealnym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="37860-124">Author biography content is available to the view by model binding alone, so using a partial view for this type of content is ideal.</span></span>

<span data-ttu-id="37860-125">[Wyświetlanie składników](xref:mvc/views/view-components) są podobne do częściowego widoki, ponieważ umożliwiają zmniejszenie powtarzających się kod, ale są one odpowiednie dla widoku zawartości, która wymaga kod wymagany do uruchomienia na serwerze w celu renderowania strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="37860-125">[View components](xref:mvc/views/view-components) are similar to partial views in that they allow you to reduce repetitive code, but they're appropriate for view content that requires code to run on the server in order to render the webpage.</span></span> <span data-ttu-id="37860-126">Widok składniki są przydatne, gdy renderowanej zawartości wymaga interakcji z bazy danych, takich jak koszyka zakupów witryna sieci Web.</span><span class="sxs-lookup"><span data-stu-id="37860-126">View components are useful when the rendered content requires database interaction, such as for a website shopping cart.</span></span> <span data-ttu-id="37860-127">Widok składniki nie są ograniczone do modelu powiązania w celu generowania danych wyjściowych strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="37860-127">View components aren't limited to model binding in order to produce webpage output.</span></span>

## <a name="benefits-of-using-views"></a><span data-ttu-id="37860-128">Korzyści wynikające z korzystania z widoków</span><span class="sxs-lookup"><span data-stu-id="37860-128">Benefits of using views</span></span>

<span data-ttu-id="37860-129">Widoki pomóc w ustaleniu [ **S**eparation **o**f **C**oncerns (SoC) projektu](http://deviq.com/separation-of-concerns/) w aplikacji MVC, oddzielając znaczników interfejsu użytkownika z inne części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-129">Views help to establish a [**S**eparation **o**f **C**oncerns (SoC) design](http://deviq.com/separation-of-concerns/) within an MVC app by separating the user interface markup from other parts of the app.</span></span> <span data-ttu-id="37860-130">Następującego projektu SoC sprawia, że aplikacja moduły, który zapewnia kilka korzyści:</span><span class="sxs-lookup"><span data-stu-id="37860-130">Following SoC design makes your app modular, which provides several benefits:</span></span>

* <span data-ttu-id="37860-131">Aplikacja jest łatwiejsze w obsłudze, ponieważ jest lepiej zorganizowany.</span><span class="sxs-lookup"><span data-stu-id="37860-131">The app is easier to maintain because it's better organized.</span></span> <span data-ttu-id="37860-132">Widoki zazwyczaj są pogrupowane według funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-132">Views are generally grouped by app feature.</span></span> <span data-ttu-id="37860-133">Dzięki temu można łatwiej znaleźć widoki pokrewne podczas pracy z funkcją.</span><span class="sxs-lookup"><span data-stu-id="37860-133">This makes it easier to find related views when working on a feature.</span></span>
* <span data-ttu-id="37860-134">Są luźno powiązane z części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-134">The parts of the app are loosely coupled.</span></span> <span data-ttu-id="37860-135">Możesz skompilować i aktualizacji aplikacji widoków niezależnie od składniki dostępu logikę i dane biznesowe.</span><span class="sxs-lookup"><span data-stu-id="37860-135">You can build and update the app's views separately from the business logic and data access components.</span></span> <span data-ttu-id="37860-136">Widoki aplikacji można modyfikować, bez konieczności aktualizacji innych części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-136">You can modify the views of the app without necessarily having to update other parts of the app.</span></span>
* <span data-ttu-id="37860-137">Możliwe jest łatwiejsze testowanie części interfejsu użytkownika aplikacji, ponieważ widoki są osobne jednostki.</span><span class="sxs-lookup"><span data-stu-id="37860-137">It's easier to test the user interface parts of the app because the views are separate units.</span></span>
* <span data-ttu-id="37860-138">Z powodu zapewnienia lepszej organizacji jest mniej prawdopodobne, że zostanie przypadkowo sekcje powtarzania interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37860-138">Due to better organization, it's less likely that you'll accidently repeat sections of the user interface.</span></span>

## <a name="creating-a-view"></a><span data-ttu-id="37860-139">Tworzenie widoku</span><span class="sxs-lookup"><span data-stu-id="37860-139">Creating a view</span></span>

<span data-ttu-id="37860-140">Widoki, które są specyficzne dla kontrolera są tworzone w *widoków / [ControllerName]* folderu.</span><span class="sxs-lookup"><span data-stu-id="37860-140">Views that are specific to a controller are created in the *Views/[ControllerName]* folder.</span></span> <span data-ttu-id="37860-141">Widoki, które są współużytkowane przez kontrolery są umieszczane w *widoków/Shared* folderu.</span><span class="sxs-lookup"><span data-stu-id="37860-141">Views that are shared among controllers are placed in the *Views/Shared* folder.</span></span> <span data-ttu-id="37860-142">Aby utworzyć widok, Dodaj nowy plik i nadaj mu taką samą nazwę jak jego akcji kontrolera skojarzone z *.cshtml* rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="37860-142">To create a view, add a new file and give it the same name as its associated controller action with the *.cshtml* file extension.</span></span> <span data-ttu-id="37860-143">Aby utworzyć widok, który odpowiada *o* akcji w *Home* kontroler, tworzyć *About.cshtml* w pliku *widoków domowych*folderu:</span><span class="sxs-lookup"><span data-stu-id="37860-143">To create a view that corresponds with the *About* action in the *Home* controller, create an *About.cshtml* file in the *Views/Home* folder:</span></span>

[!code-cshtml[Main](../../common/samples/WebApplication1/Views/Home/About.cshtml)]

<span data-ttu-id="37860-144">*Razor* znaczników rozpoczyna się od `@` symbolu.</span><span class="sxs-lookup"><span data-stu-id="37860-144">*Razor* markup starts with the `@` symbol.</span></span> <span data-ttu-id="37860-145">Kod C# instrukcje uruchamiania przez umieszczenie C# w [bloki kodu Razor](xref:mvc/views/razor#razor-code-blocks) przez nawiasy klamrowe (`{ ... }`).</span><span class="sxs-lookup"><span data-stu-id="37860-145">Run C# statements by placing C# code within [Razor code blocks](xref:mvc/views/razor#razor-code-blocks) set off by curly braces (`{ ... }`).</span></span> <span data-ttu-id="37860-146">Na przykład znajdują się w sekcji przypisania "Informacje o" `ViewData["Title"]` przedstawionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="37860-146">For example, see the assignment of "About" to `ViewData["Title"]` shown above.</span></span> <span data-ttu-id="37860-147">Możesz wyświetlić wartości w pliku HTML po prostu odwołuje się do wartości o `@` symbolu.</span><span class="sxs-lookup"><span data-stu-id="37860-147">You can display values within HTML by simply referencing the value with the `@` symbol.</span></span> <span data-ttu-id="37860-148">Wyświetlanie zawartości `<h2>` i `<h3>` elementów wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="37860-148">See the contents of the `<h2>` and `<h3>` elements above.</span></span>

<span data-ttu-id="37860-149">Wyświetl zawartość pokazanym powyżej jest tylko część całą stronę sieci Web, który jest renderowany do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37860-149">The view content shown above is only part of the entire webpage that's rendered to the user.</span></span> <span data-ttu-id="37860-150">Resztę układu strony i innych typowych aspektów widoku są określone w innych plików widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-150">The rest of the page's layout and other common aspects of the view are specified in other view files.</span></span> <span data-ttu-id="37860-151">Aby dowiedzieć się więcej, zobacz [tematu układu](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="37860-151">To learn more, see the [Layout topic](xref:mvc/views/layout).</span></span>

## <a name="how-controllers-specify-views"></a><span data-ttu-id="37860-152">Jak określić widoki, kontrolery</span><span class="sxs-lookup"><span data-stu-id="37860-152">How controllers specify views</span></span>

<span data-ttu-id="37860-153">Widoki są zazwyczaj zwracane z akcji jako [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult), który jest typem [ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult).</span><span class="sxs-lookup"><span data-stu-id="37860-153">Views are typically returned from actions as a [ViewResult](/aspnet/core/api/microsoft.aspnetcore.mvc.viewresult), which is a type of [ActionResult](/aspnet/core/api/microsoft.aspnetcore.mvc.actionresult).</span></span> <span data-ttu-id="37860-154">Metodę akcji można tworzyć i zwracać `ViewResult` bezpośrednio, ale często nie jest stosowana.</span><span class="sxs-lookup"><span data-stu-id="37860-154">Your action method can create and return a `ViewResult` directly, but that isn't commonly done.</span></span> <span data-ttu-id="37860-155">Ponieważ większość kontrolerów dziedziczyć [kontrolera](/aspnet/core/api/microsoft.aspnetcore.mvc.controller), po prostu `View` metody pomocnika do zwrócenia `ViewResult`:</span><span class="sxs-lookup"><span data-stu-id="37860-155">Since most controllers inherit from [Controller](/aspnet/core/api/microsoft.aspnetcore.mvc.controller), you simply use the `View` helper method to return the `ViewResult`:</span></span>

<span data-ttu-id="37860-156">*HomeController.cs*</span><span class="sxs-lookup"><span data-stu-id="37860-156">*HomeController.cs*</span></span>

[!code-csharp[Main](../../common/samples/WebApplication1/Controllers/HomeController.cs?highlight=5&range=16-21)]

<span data-ttu-id="37860-157">Po powrocie z tej akcji *About.cshtml* renderowania widoku w ostatniej sekcji jako następujące strony sieci Web:</span><span class="sxs-lookup"><span data-stu-id="37860-157">When this action returns, the *About.cshtml* view shown in the last section is rendered as the following webpage:</span></span>

![Strona renderowane w przeglądarce Edge — informacje](overview/_static/about-page.png)

<span data-ttu-id="37860-159">`View` Metoda pomocnika ma kilka przeciążeń.</span><span class="sxs-lookup"><span data-stu-id="37860-159">The `View` helper method has several overloads.</span></span> <span data-ttu-id="37860-160">Opcjonalnie można określić:</span><span class="sxs-lookup"><span data-stu-id="37860-160">You can optionally specify:</span></span>

* <span data-ttu-id="37860-161">Jawne widoku do zwrócenia:</span><span class="sxs-lookup"><span data-stu-id="37860-161">An explicit view to return:</span></span>

  ```csharp
  return View("Orders");
  ```
* <span data-ttu-id="37860-162">A [modelu](xref:mvc/models/model-binding) do przekazania do widoku:</span><span class="sxs-lookup"><span data-stu-id="37860-162">A [model](xref:mvc/models/model-binding) to pass to the view:</span></span>

  ```csharp
  return View(Orders);
  ```
* <span data-ttu-id="37860-163">Widoku i modelu:</span><span class="sxs-lookup"><span data-stu-id="37860-163">Both a view and a model:</span></span>

  ```csharp
  return View("Orders", Orders);
  ```

### <a name="view-discovery"></a><span data-ttu-id="37860-164">Widok odnajdywania</span><span class="sxs-lookup"><span data-stu-id="37860-164">View discovery</span></span>

<span data-ttu-id="37860-165">Po powrocie z operacji widoku proces jest nazywany *widok odnajdywania* ma miejsce.</span><span class="sxs-lookup"><span data-stu-id="37860-165">When an action returns a view, a process called *view discovery* takes place.</span></span> <span data-ttu-id="37860-166">Ten proces Określa plik widoku, który jest używany na podstawie nazwy widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-166">This process determines which view file is used based on the view name.</span></span> 

<span data-ttu-id="37860-167">Domyślne zachowanie `View` — metoda (`return View();`) jest do zwrócenia widoku z taką samą nazwę jak metody akcji, z którego jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="37860-167">The default behavior of the `View` method (`return View();`) is to return a view with the same name as the action method from which it's called.</span></span> <span data-ttu-id="37860-168">Na przykład *o* `ActionResult` nazwę metody kontrolera jest używana do wyszukiwania pliku widok o nazwie *About.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="37860-168">For example, the *About* `ActionResult` method name of the controller is used to search for a view file named *About.cshtml*.</span></span> <span data-ttu-id="37860-169">Najpierw środowiska uruchomieniowego jest wyszukiwany w *widoków / [ControllerName]* folderu dla widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-169">First, the runtime looks in the *Views/[ControllerName]* folder for the view.</span></span> <span data-ttu-id="37860-170">Jeśli nie znajdzie pasującego widoku wyszukuje *Shared* folderu dla widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-170">If it doesn't find a matching view there, it searches the *Shared* folder for the view.</span></span>

<span data-ttu-id="37860-171">Nie ma znaczenia, gdy zwracają niejawnie `ViewResult` z `return View();` lub jawnego przesłania nazwy widoku, aby `View` metody z `return View("<ViewName>");`.</span><span class="sxs-lookup"><span data-stu-id="37860-171">It doesn't matter if you implicitly return the `ViewResult` with `return View();` or explicitly pass the view name to the `View` method with `return View("<ViewName>");`.</span></span> <span data-ttu-id="37860-172">W obu przypadkach widok odnajdywania wyszukuje odpowiedniego pliku widoku w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="37860-172">In both cases, view discovery searches for a matching view file in this order:</span></span>

   1. <span data-ttu-id="37860-173">*Views/\[ControllerName]\[ViewName].cshtml*</span><span class="sxs-lookup"><span data-stu-id="37860-173">*Views/\[ControllerName]\[ViewName].cshtml*</span></span>
   1. <span data-ttu-id="37860-174">*Widoki/udostępnione/\[ViewName] .cshtml*</span><span class="sxs-lookup"><span data-stu-id="37860-174">*Views/Shared/\[ViewName].cshtml*</span></span>

<span data-ttu-id="37860-175">Ścieżka pliku widoku można podać zamiast nazwy widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-175">A view file path can be provided instead of a view name.</span></span> <span data-ttu-id="37860-176">Jeśli przy użyciu ścieżką bezwzględną, zaczynając od katalogu głównego aplikacji (opcjonalnie rozpoczynających się od "/" lub "~ /"), *.cshtml* rozszerzenia musi być określona:</span><span class="sxs-lookup"><span data-stu-id="37860-176">If using an absolute path starting at the app root (optionally starting with "/" or "~/"), the *.cshtml* extension must be specified:</span></span>

```csharp
return View("Views/Home/About.cshtml");
```

<span data-ttu-id="37860-177">Umożliwia także ścieżkę względną do określenia widoków w różnych katalogach bez *.cshtml* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="37860-177">You can also use a relative path to specify views in different directories without the *.cshtml* extension.</span></span> <span data-ttu-id="37860-178">Wewnątrz `HomeController`, można powrócić *indeksu* widok z *Zarządzaj* widoków ze ścieżką względną:</span><span class="sxs-lookup"><span data-stu-id="37860-178">Inside the `HomeController`, you can return the *Index* view of your *Manage* views with a relative path:</span></span>

```csharp
return View("../Manage/Index");
```

<span data-ttu-id="37860-179">Podobnie można określić bieżącego katalogu kontrolera specyficznych z ". /" prefiksu:</span><span class="sxs-lookup"><span data-stu-id="37860-179">Similarly, you can indicate the current controller-specific directory with the "./" prefix:</span></span>

```csharp
return View("./About");
```

<span data-ttu-id="37860-180">[Widoki częściowe](xref:mvc/views/partial) i [wyświetlić składniki](xref:mvc/views/view-components) używa mechanizmów odnajdywania podobne (ale nie są identyczne).</span><span class="sxs-lookup"><span data-stu-id="37860-180">[Partial views](xref:mvc/views/partial) and [view components](xref:mvc/views/view-components) use similar (but not identical) discovery mechanisms.</span></span>

<span data-ttu-id="37860-181">Można dostosować domyślnej Konwencji dla jak widoki znajdują się w aplikacji przy użyciu niestandardowego [IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span><span class="sxs-lookup"><span data-stu-id="37860-181">You can customize the default convention for how views are located within the app by using a custom [IViewLocationExpander](/aspnet/core/api/microsoft.aspnetcore.mvc.razor.iviewlocationexpander).</span></span>

<span data-ttu-id="37860-182">Widok odnajdywania zależy od tego, wyszukiwanie Wyświetl pliki według nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="37860-182">View discovery relies on finding view files by file name.</span></span> <span data-ttu-id="37860-183">Jeśli źródłowy system plików jest rozróżniana wielkość liter, nazwy widoku są prawdopodobnie wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="37860-183">If the underlying file system is case sensitive, view names are probably case sensitive.</span></span> <span data-ttu-id="37860-184">Zgodność w różnych systemach operacyjnych wielkość liter między kontrolera i nazwy akcji i skojarzony widok folderów i plików.</span><span class="sxs-lookup"><span data-stu-id="37860-184">For compatibility across operating systems, match case between controller and action names and associated view folders and file names.</span></span> <span data-ttu-id="37860-185">Jeśli wystąpi błąd, którego nie można odnaleźć pliku widoku podczas pracy z systemem plików z uwzględnieniem wielkości liter, upewnij się, zgodność między plikiem żądany widok i nazwa pliku rzeczywista widok wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="37860-185">If you encounter an error that a view file can't be found while working with a case-sensitive file system, confirm that the casing matches between the requested view file and the actual view file name.</span></span>

<span data-ttu-id="37860-186">Postępuj zgodnie z najlepszym rozwiązaniem organizowania struktury plików widoki, aby odzwierciedlić relacje widoków utrzymanie i przejrzystości, akcje i kontrolery.</span><span class="sxs-lookup"><span data-stu-id="37860-186">Follow the best practice of organizing the file structure for your views to reflect the relationships among controllers, actions, and views for maintainability and clarity.</span></span>

## <a name="passing-data-to-views"></a><span data-ttu-id="37860-187">Przekazywanie danych do widoków</span><span class="sxs-lookup"><span data-stu-id="37860-187">Passing data to views</span></span>

<span data-ttu-id="37860-188">Dane można przekazać do widoków przy użyciu kilku metod.</span><span class="sxs-lookup"><span data-stu-id="37860-188">You can pass data to views using several approaches.</span></span> <span data-ttu-id="37860-189">Najbardziej niezawodna podejściem jest określenie [modelu](xref:mvc/models/model-binding) typu w widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-189">The most robust approach is to specify a [model](xref:mvc/models/model-binding) type in the view.</span></span> <span data-ttu-id="37860-190">Ten model jest często określana jako *viewmodel*.</span><span class="sxs-lookup"><span data-stu-id="37860-190">This model is commonly referred to as a *viewmodel*.</span></span> <span data-ttu-id="37860-191">Wystąpienie typu viewmodel są przekazywane do widoku z akcji.</span><span class="sxs-lookup"><span data-stu-id="37860-191">You pass an instance of the viewmodel type to the view from the action.</span></span>

<span data-ttu-id="37860-192">Aby przekazać dane do widoku przy użyciu viewmodel umożliwia widok, aby móc korzystać z *silne* sprawdzania typu.</span><span class="sxs-lookup"><span data-stu-id="37860-192">Using a viewmodel to pass data to a view allows the view to take advantage of *strong* type checking.</span></span> <span data-ttu-id="37860-193">*Silne wpisywanie* (lub *jednoznacznie*) oznacza, że każdy zmiennej i stałej ma jawnie zdefiniowanych typów (na przykład `string`, `int`, lub `DateTime`).</span><span class="sxs-lookup"><span data-stu-id="37860-193">*Strong typing* (or *strongly-typed*) means that every variable and constant has an explicitly defined type (for example, `string`, `int`, or `DateTime`).</span></span> <span data-ttu-id="37860-194">Ważność typy używane w widoku jest sprawdzany w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="37860-194">The validity of types used in a view is checked at compile time.</span></span>

<span data-ttu-id="37860-195">[Visual Studio](https://www.visualstudio.com/vs/) i [Visual Studio Code](https://code.visualstudio.com/) członków klasy jednoznacznie przy użyciu funkcji o nazwie [IntelliSense](/visualstudio/ide/using-intellisense).</span><span class="sxs-lookup"><span data-stu-id="37860-195">[Visual Studio](https://www.visualstudio.com/vs/) and [Visual Studio Code](https://code.visualstudio.com/) list strongly-typed class members using a feature called [IntelliSense](/visualstudio/ide/using-intellisense).</span></span> <span data-ttu-id="37860-196">Aby wyświetlić właściwości viewmodel, należy wpisać nazwę zmiennej viewmodel, a następnie kropki (`.`).</span><span class="sxs-lookup"><span data-stu-id="37860-196">When you want to see the properties of a viewmodel, type the variable name for the viewmodel followed by a period (`.`).</span></span> <span data-ttu-id="37860-197">Dzięki temu można napisać kod szybciej z mniejszą liczbą błędów.</span><span class="sxs-lookup"><span data-stu-id="37860-197">This helps you write code faster with fewer errors.</span></span>

<span data-ttu-id="37860-198">Określ model przy użyciu `@model` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="37860-198">Specify a model using the `@model` directive.</span></span> <span data-ttu-id="37860-199">Użyj modelu o `@Model`:</span><span class="sxs-lookup"><span data-stu-id="37860-199">Use the model with `@Model`:</span></span>

```cshtml
@model WebApplication1.ViewModels.Address

<h2>Contact</h2>
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="37860-200">Aby zapewnić modelu widoku, kontrolera przekazuje ją jako parametr:</span><span class="sxs-lookup"><span data-stu-id="37860-200">To provide the model to the view, the controller passes it as a parameter:</span></span>

```csharp
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";

    var viewModel = new Address()
    {
        Name = "Microsoft",
        Street = "One Microsoft Way",
        City = "Redmond",
        State = "WA",
        PostalCode = "98052-6399"
    };

    return View(viewModel);
}
```

<span data-ttu-id="37860-201">Nie ma żadnych ograniczeń na typy modelu, umożliwiające do widoku.</span><span class="sxs-lookup"><span data-stu-id="37860-201">There are no restrictions on the model types that you can provide to a view.</span></span> <span data-ttu-id="37860-202">Firma Microsoft zaleca używanie **P**zwykły **O**ld **C**LR **O**viewmodels obiektu (POCO) z zachowaniem żadnych (metody), zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="37860-202">We recommend using **P**lain **O**ld **C**LR **O**bject (POCO) viewmodels with little or no behavior (methods) defined.</span></span> <span data-ttu-id="37860-203">Zazwyczaj klasy viewmodel albo są przechowywane w *modele* folderu lub oddzielnej *ViewModels* folder w katalogu głównym aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-203">Usually, viewmodel classes are either stored in the *Models* folder or a separate *ViewModels* folder at the root of the app.</span></span> <span data-ttu-id="37860-204">*Adres* viewmodel używane w powyższym przykładzie jest viewmodel POCO, przechowywane w pliku o nazwie *Address.cs*:</span><span class="sxs-lookup"><span data-stu-id="37860-204">The *Address* viewmodel used in the example above is a POCO viewmodel stored in a file named *Address.cs*:</span></span>

```csharp
namespace WebApplication1.ViewModels
{
    public class Address
    {
        public string Name { get; set; }
        public string Street { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string PostalCode { get; set; }
    }
}
```

> [!NOTE]
> <span data-ttu-id="37860-205">Nic nie uniemożliwia przy użyciu tej samej klasy dla użytkownika typy viewmodel i z typów modelu biznesowych.</span><span class="sxs-lookup"><span data-stu-id="37860-205">Nothing prevents you from using the same classes for both your viewmodel types and your business model types.</span></span> <span data-ttu-id="37860-206">Jednak przy użyciu osobnych modeli umożliwia widoków się różnić, niezależnie od logiki biznesowej i dane dostępu do części aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37860-206">However, using separate models allows your views to vary independently from the business logic and data access parts of your app.</span></span> <span data-ttu-id="37860-207">Rozdzielenie modeli i viewmodels oferuje również korzyści w zakresie zabezpieczeń używania modeli [modelu powiązania](xref:mvc/models/model-binding) i [weryfikacji](xref:mvc/models/validation) dla danych przesyłanych do aplikacji przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37860-207">Separation of models and viewmodels also offers security benefits when models use [model binding](xref:mvc/models/model-binding) and [validation](xref:mvc/models/validation) for data sent to the app by the user.</span></span>


<a name="VD_VB"></a>

### <a name="weakly-typed-data-viewdata-and-viewbag"></a><span data-ttu-id="37860-208">Słabą danych (ViewData i obiekt ViewBag)</span><span class="sxs-lookup"><span data-stu-id="37860-208">Weakly-typed data (ViewData and ViewBag)</span></span>

<span data-ttu-id="37860-209">Uwaga: `ViewBag` nie jest dostępna na stronach Razor.</span><span class="sxs-lookup"><span data-stu-id="37860-209">Note: `ViewBag` isn't available in the Razor Pages.</span></span>

<span data-ttu-id="37860-210">Oprócz widoków z silnie typizowanych widoki mają dostęp do *słabą kontrolą* (nazywane również *typowaniem luźnym*) zbierania danych.</span><span class="sxs-lookup"><span data-stu-id="37860-210">In addition to strongly-typed views, views have access to a *weakly-typed* (also called *loosely-typed*) collection of data.</span></span> <span data-ttu-id="37860-211">W odróżnieniu od typów silne *słabe typy* (lub *luźno typy*) oznacza, że nie jawnie zadeklarować typ danych.</span><span class="sxs-lookup"><span data-stu-id="37860-211">Unlike strong types, *weak types* (or *loose types*) means that you don't explicitly declare the type of data you're using.</span></span> <span data-ttu-id="37860-212">Zbieranie danych, słabą kontrolą służy do przekazywania niewielkich ilości danych do i z widoków i kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="37860-212">You can use the collection of weakly-typed data for passing small amounts of data in and out of controllers and views.</span></span>

| <span data-ttu-id="37860-213">Przekazywanie danych pomiędzy...</span><span class="sxs-lookup"><span data-stu-id="37860-213">Passing data between a ...</span></span>                        | <span data-ttu-id="37860-214">Przykład</span><span class="sxs-lookup"><span data-stu-id="37860-214">Example</span></span>                                                                        |
| ------------------------------------------------- | ------------------------------------------------------------------------------ |
| <span data-ttu-id="37860-215">Kontrolerem i widokiem</span><span class="sxs-lookup"><span data-stu-id="37860-215">Controller and a view</span></span>                             | <span data-ttu-id="37860-216">Wypełnianie listy rozwijanej z danymi.</span><span class="sxs-lookup"><span data-stu-id="37860-216">Populating a dropdown list with data.</span></span>                                          |
| <span data-ttu-id="37860-217">Wyświetl i [widoku układu](xref:mvc/views/layout)</span><span class="sxs-lookup"><span data-stu-id="37860-217">View and a [layout view](xref:mvc/views/layout)</span></span>   | <span data-ttu-id="37860-218">Ustawienie  **\<title >** zawartości elementu w widoku układu z widoku pliku.</span><span class="sxs-lookup"><span data-stu-id="37860-218">Setting the **\<title>** element content in the layout view from a view file.</span></span>  |
| <span data-ttu-id="37860-219">[Widok częściowy](xref:mvc/views/partial) i widoku</span><span class="sxs-lookup"><span data-stu-id="37860-219">[Partial view](xref:mvc/views/partial) and a view</span></span> | <span data-ttu-id="37860-220">Element widget wyświetlający dane oparte na sieci Web, który użytkownik zażądał.</span><span class="sxs-lookup"><span data-stu-id="37860-220">A widget that displays data based on the webpage that the user requested.</span></span>      |

<span data-ttu-id="37860-221">Ta kolekcja można odwoływać się przy użyciu jednej `ViewData` lub `ViewBag` właściwości kontrolery i widoki.</span><span class="sxs-lookup"><span data-stu-id="37860-221">This collection can be referenced through either the `ViewData` or `ViewBag` properties on controllers and views.</span></span> <span data-ttu-id="37860-222">`ViewData` Właściwości jest słownikiem słabą kontrolą obiektów.</span><span class="sxs-lookup"><span data-stu-id="37860-222">The `ViewData` property is a dictionary of weakly-typed objects.</span></span> <span data-ttu-id="37860-223">`ViewBag` Właściwość jest otokę `ViewData` zapewnia właściwości dynamicznych odpowiadającego `ViewData` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="37860-223">The `ViewBag` property is a wrapper around `ViewData` that provides dynamic properties for the underlying `ViewData` collection.</span></span>

<span data-ttu-id="37860-224">`ViewData`i `ViewBag` są dynamicznie rozwiązane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="37860-224">`ViewData` and `ViewBag` are dynamically resolved at runtime.</span></span> <span data-ttu-id="37860-225">Ponieważ nie oferują sprawdzanie typów w czasie kompilacji, są zazwyczaj bardziej podatnych niż przy użyciu viewmodel.</span><span class="sxs-lookup"><span data-stu-id="37860-225">Since they don't offer compile-time type checking, both are generally more error-prone than using a viewmodel.</span></span> <span data-ttu-id="37860-226">Z tego powodu niektórzy deweloperzy wolą minimalny zestaw lub nigdy nie należy używać `ViewData` i `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="37860-226">For that reason, some developers prefer to minimally or never use `ViewData` and `ViewBag`.</span></span>


<a name="VD"></a>

<span data-ttu-id="37860-227">**ViewData**</span><span class="sxs-lookup"><span data-stu-id="37860-227">**ViewData**</span></span>

<span data-ttu-id="37860-228">`ViewData`jest [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) dostępne za pośrednictwem obiektu `string` kluczy.</span><span class="sxs-lookup"><span data-stu-id="37860-228">`ViewData` is a [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary) object accessed through `string` keys.</span></span> <span data-ttu-id="37860-229">Danych dotyczących ciągu mogą być przechowywane i używane bezpośrednio, bez konieczności rzutowanie, ale należy rzutować innych `ViewData` obiektu wartości do określonych typów, po ich wyodrębnieniu.</span><span class="sxs-lookup"><span data-stu-id="37860-229">String data can be stored and used directly without the need for a cast, but you must cast other `ViewData` object values to specific types when you extract them.</span></span> <span data-ttu-id="37860-230">Można użyć `ViewData` do przekazywania danych z kontrolerów, widoków i w obrębie widoków, w tym [widoki częściowe](xref:mvc/views/partial) i [układów](xref:mvc/views/layout).</span><span class="sxs-lookup"><span data-stu-id="37860-230">You can use `ViewData` to pass data from controllers to views and within views, including [partial views](xref:mvc/views/partial) and [layouts](xref:mvc/views/layout).</span></span>

<span data-ttu-id="37860-231">Poniżej przedstawiono przykład, która ustawia wartości pozdrowienia i przy użyciu adresu `ViewData` w akcji:</span><span class="sxs-lookup"><span data-stu-id="37860-231">The following is an example that sets values for a greeting and an address using `ViewData` in an action:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewData["Greeting"] = "Hello";
    ViewData["Address"]  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

<span data-ttu-id="37860-232">Praca z danymi w widoku:</span><span class="sxs-lookup"><span data-stu-id="37860-232">Work with the data in a view:</span></span>

```cshtml
@{
    // Since Address isn't a string, it requires a cast.
    var address = ViewData["Address"] as Address;
}

@ViewData["Greeting"] World!

<address>
    @address.Name<br>
    @address.Street<br>
    @address.City, @address.State @address.PostalCode
</address>
```

<span data-ttu-id="37860-233">**Obiekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="37860-233">**ViewBag**</span></span>

<span data-ttu-id="37860-234">Uwaga: `ViewBag` nie jest dostępna na stronach Razor.</span><span class="sxs-lookup"><span data-stu-id="37860-234">Note: `ViewBag` isn't available in the Razor Pages.</span></span>

<span data-ttu-id="37860-235">`ViewBag`jest [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) obiekt, który umożliwia dynamiczne dostęp do obiektów przechowywanych w `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="37860-235">`ViewBag` is a [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata) object that provides dynamic access to the objects stored in `ViewData`.</span></span> <span data-ttu-id="37860-236">`ViewBag`może być bardziej wygodne do pracy, ponieważ nie wymaga rzutowania.</span><span class="sxs-lookup"><span data-stu-id="37860-236">`ViewBag` can be more convenient to work with, since it doesn't require casting.</span></span> <span data-ttu-id="37860-237">Poniższy przykład przedstawia użycie `ViewBag` z takiego samego wyniku jako przy użyciu `ViewData` powyżej:</span><span class="sxs-lookup"><span data-stu-id="37860-237">The following example shows how to use `ViewBag` with the same result as using `ViewData` above:</span></span>

```csharp
public IActionResult SomeAction()
{
    ViewBag.Greeting = "Hello";
    ViewBag.Address  = new Address()
    {
        Name = "Steve",
        Street = "123 Main St",
        City = "Hudson",
        State = "OH",
        PostalCode = "44236"
    };

    return View();
}
```

```cshtml
@ViewBag.Greeting World!

<address>
    @ViewBag.Address.Name<br>
    @ViewBag.Address.Street<br>
    @ViewBag.Address.City, @ViewBag.Address.State @ViewBag.Address.PostalCode
</address>
```

<span data-ttu-id="37860-238">**Przy użyciu elementów ViewBag, ViewData a jednocześnie**</span><span class="sxs-lookup"><span data-stu-id="37860-238">**Using ViewData and ViewBag simultaneously**</span></span>

<span data-ttu-id="37860-239">Uwaga: `ViewBag` nie jest dostępna na stronach Razor.</span><span class="sxs-lookup"><span data-stu-id="37860-239">Note: `ViewBag` isn't available in the Razor Pages.</span></span>

<span data-ttu-id="37860-240">Ponieważ `ViewData` i `ViewBag` odwoływać się do tego samego podstawowego `ViewData` kolekcji, można użyć zarówno `ViewData` i `ViewBag` i mieszać i dopasowywać między nimi podczas odczytywania i zapisywania wartości.</span><span class="sxs-lookup"><span data-stu-id="37860-240">Since `ViewData` and `ViewBag` refer to the same underlying `ViewData` collection, you can use both `ViewData` and `ViewBag` and mix and match between them when reading and writing values.</span></span>

<span data-ttu-id="37860-241">Ustawić za pomocą tytuł `ViewBag` i przy użyciu opisu `ViewData` w górnej części *About.cshtml* widoku:</span><span class="sxs-lookup"><span data-stu-id="37860-241">Set the title using `ViewBag` and the description using `ViewData` at the top of an *About.cshtml* view:</span></span>

```cshtml
@{
    Layout = "/Views/Shared/_Layout.cshtml";
    ViewBag.Title = "About Contoso";
    ViewData["Description"] = "Let us tell you about Contoso's philosophy and mission.";
}
```

<span data-ttu-id="37860-242">Właściwości do odczytu, ale wstecznego stosowania `ViewData` i `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="37860-242">Read the properties but reverse the use of `ViewData` and `ViewBag`.</span></span> <span data-ttu-id="37860-243">W *_Layout.cshtml* plików, Uzyskaj za pomocą tytuł `ViewData` i Uzyskaj za pomocą opis `ViewBag`:</span><span class="sxs-lookup"><span data-stu-id="37860-243">In the *_Layout.cshtml* file, obtain the title using `ViewData` and obtain the description using `ViewBag`:</span></span>

```cshtml
<!DOCTYPE html>
<html lang="en">
<head>
    <title>@ViewData["Title"]</title>
    <meta name="description" content="@ViewBag.Description">
    ...
```

<span data-ttu-id="37860-244">Należy pamiętać, że ciągów nie wymagają rzutowanie dla `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="37860-244">Remember that strings don't require a cast for `ViewData`.</span></span> <span data-ttu-id="37860-245">Można użyć `@ViewData["Title"]` bez rzutowania.</span><span class="sxs-lookup"><span data-stu-id="37860-245">You can use `@ViewData["Title"]` without casting.</span></span>

<span data-ttu-id="37860-246">Za pomocą obu `ViewData` i `ViewBag` w tej samej pracy czas, jak mieszania i dopasowywanie odczytywanie i zapisywanie właściwości.</span><span class="sxs-lookup"><span data-stu-id="37860-246">Using both `ViewData` and `ViewBag` at the same time works, as does mixing and matching reading and writing the properties.</span></span> <span data-ttu-id="37860-247">Następujący kod znaczników jest renderowany:</span><span class="sxs-lookup"><span data-stu-id="37860-247">The following markup is rendered:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>About Contoso</title>
    <meta name="description" content="Let us tell you about Contoso's philosophy and mission.">
    ...
```

<span data-ttu-id="37860-248">**Podsumowanie różnic między ViewData i obiekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="37860-248">**Summary of the differences between ViewData and ViewBag**</span></span>

 <span data-ttu-id="37860-249">`ViewBag`nie jest dostępna na stronach Razor.</span><span class="sxs-lookup"><span data-stu-id="37860-249">`ViewBag` isn't available in the Razor Pages.</span></span>

* `ViewData`
  * <span data-ttu-id="37860-250">Pochodną [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), co powoduje słownika właściwości, które mogą być przydatne, takich jak `ContainsKey`, `Add`, `Remove`, i `Clear`.</span><span class="sxs-lookup"><span data-stu-id="37860-250">Derives from [ViewDataDictionary](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.viewdatadictionary), so it has dictionary properties that can be useful, such as `ContainsKey`, `Add`, `Remove`, and `Clear`.</span></span>
  * <span data-ttu-id="37860-251">Klucze w słowniku są ciągi, więc spacji jest dozwolony.</span><span class="sxs-lookup"><span data-stu-id="37860-251">Keys in the dictionary are strings, so whitespace is allowed.</span></span> <span data-ttu-id="37860-252">Przykład:`ViewData["Some Key With Whitespace"]`</span><span class="sxs-lookup"><span data-stu-id="37860-252">Example: `ViewData["Some Key With Whitespace"]`</span></span>
  * <span data-ttu-id="37860-253">Dowolny typ innych niż `string` musi być rzutowane w widoku, aby użyć `ViewData`.</span><span class="sxs-lookup"><span data-stu-id="37860-253">Any type other than a `string` must be cast in the view to use `ViewData`.</span></span>
* `ViewBag`
  * <span data-ttu-id="37860-254">Pochodną [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), więc umożliwia tworzenie dynamicznych właściwości, używając zapisu kropkowego (`@ViewBag.SomeKey = <value or object>`), a Rzutowanie nie jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="37860-254">Derives from [DynamicViewData](/aspnet/core/api/microsoft.aspnetcore.mvc.viewfeatures.internal.dynamicviewdata), so it allows the creation of dynamic properties using dot notation (`@ViewBag.SomeKey = <value or object>`), and no casting is required.</span></span> <span data-ttu-id="37860-255">Składnia `ViewBag` umożliwia szybsze do dodania do widoków i kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="37860-255">The syntax of `ViewBag` makes it quicker to add to controllers and views.</span></span>
  * <span data-ttu-id="37860-256">Łatwiejsze do sprawdzenia wartości null.</span><span class="sxs-lookup"><span data-stu-id="37860-256">Simpler to check for null values.</span></span> <span data-ttu-id="37860-257">Przykład:`@ViewBag.Person?.Name`</span><span class="sxs-lookup"><span data-stu-id="37860-257">Example: `@ViewBag.Person?.Name`</span></span>

<span data-ttu-id="37860-258">**Kiedy należy używać ViewData lub obiekt ViewBag**</span><span class="sxs-lookup"><span data-stu-id="37860-258">**When to use ViewData or ViewBag**</span></span>

<span data-ttu-id="37860-259">Zarówno `ViewData` i `ViewBag` są równie prawidłowy podejścia do przekazywania niewielkich ilości danych między kontrolery i widoki.</span><span class="sxs-lookup"><span data-stu-id="37860-259">Both `ViewData` and `ViewBag` are equally valid approaches for passing small amounts of data among controllers and views.</span></span> <span data-ttu-id="37860-260">Wybór który bazuje na preferencji.</span><span class="sxs-lookup"><span data-stu-id="37860-260">The choice of which one to use is based on preference.</span></span> <span data-ttu-id="37860-261">Można mieszać i dopasowywać `ViewData` i `ViewBag` obiektów, jednak kod jest łatwiej odczytywać i obsługa o jeden z nich korzystać.</span><span class="sxs-lookup"><span data-stu-id="37860-261">You can mix and match `ViewData` and `ViewBag` objects, however, the code is easier to read and maintain with one approach used consistently.</span></span> <span data-ttu-id="37860-262">W obu przypadkach efekt są dynamicznie rozpoznane w czasie wykonywania i w związku z tym podatne na powodujące błędy podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="37860-262">Both approaches are dynamically resolved at runtime and thus prone to causing runtime errors.</span></span> <span data-ttu-id="37860-263">Niektóre zespoły rozwoju ich uniknięcie.</span><span class="sxs-lookup"><span data-stu-id="37860-263">Some development teams avoid them.</span></span>

### <a name="dynamic-views"></a><span data-ttu-id="37860-264">Widoki dynamiczne</span><span class="sxs-lookup"><span data-stu-id="37860-264">Dynamic views</span></span>

<span data-ttu-id="37860-265">Widoki, które nie deklaruje modelu typu przy użyciu `@model` , ale mają wystąpienie modelu, przekazany do nich (na przykład `return View(Address);`) można odwoływać się właściwości wystąpienia dynamicznie:</span><span class="sxs-lookup"><span data-stu-id="37860-265">Views that don't declare a model type using `@model` but that have a model instance passed to them (for example, `return View(Address);`) can reference the instance's properties dynamically:</span></span>

```cshtml
<address>
    @Model.Street<br>
    @Model.City, @Model.State @Model.PostalCode<br>
    <abbr title="Phone">P:</abbr> 425.555.0100
</address>
```

<span data-ttu-id="37860-266">Ta funkcja zapewnia elastyczność, ale nie oferuje ochronę kompilacji i technologii IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="37860-266">This feature offers flexibility but doesn't offer compilation protection or IntelliSense.</span></span> <span data-ttu-id="37860-267">Jeśli właściwość nie istnieje, generowania strony sieci Web nie powiedzie się w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="37860-267">If the property doesn't exist, webpage generation fails at runtime.</span></span>

## <a name="more-view-features"></a><span data-ttu-id="37860-268">Więcej funkcji widoku</span><span class="sxs-lookup"><span data-stu-id="37860-268">More view features</span></span>

<span data-ttu-id="37860-269">[Pomocników tagów](xref:mvc/views/tag-helpers/intro) ułatwiają dodawanie zachowania po stronie serwera do istniejącego tagów HTML.</span><span class="sxs-lookup"><span data-stu-id="37860-269">[Tag Helpers](xref:mvc/views/tag-helpers/intro) make it easy to add server-side behavior to existing HTML tags.</span></span> <span data-ttu-id="37860-270">Przy użyciu pomocników tagów uniknąć konieczności pisanie kodu niestandardowego lub pomocników w obrębie widoków.</span><span class="sxs-lookup"><span data-stu-id="37860-270">Using Tag Helpers avoids the need to write custom code or helpers within your views.</span></span> <span data-ttu-id="37860-271">Pomocników tagów dotyczą jako atrybuty elementów HTML i są ignorowane przez edytory, które nie może ich przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="37860-271">Tag helpers are applied as attributes to HTML elements and are ignored by editors that can't process them.</span></span> <span data-ttu-id="37860-272">Dzięki temu można edytować i renderowania kodu znaczników widoku w różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="37860-272">This allows you to edit and render view markup in a variety of tools.</span></span>

<span data-ttu-id="37860-273">Generowanie niestandardowego kodu znaczników HTML może zostać osiągnięty przy wiele wbudowanych pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="37860-273">Generating custom HTML markup can be achieved with many built-in HTML Helpers.</span></span> <span data-ttu-id="37860-274">Bardziej złożonej logice interfejsu użytkownika mogą być obsługiwane przez [wyświetlania składników](xref:mvc/views/view-components).</span><span class="sxs-lookup"><span data-stu-id="37860-274">More complex user interface logic can be handled by [View Components](xref:mvc/views/view-components).</span></span> <span data-ttu-id="37860-275">Składniki w widoku Podaj tego samego SoC tego kontrolery i widoki oferty.</span><span class="sxs-lookup"><span data-stu-id="37860-275">View components provide the same SoC that controllers and views offer.</span></span> <span data-ttu-id="37860-276">Mogą one, eliminując konieczność stosowania akcjami i widokami, które zajmują się dane używane przez wspólne elementy interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37860-276">They can eliminate the need for actions and views that deal with data used by common user interface elements.</span></span>

<span data-ttu-id="37860-277">Podobnie jak wiele innych aspektów platformy ASP.NET Core, widoki pomocy technicznej [iniekcji zależności](xref:fundamentals/dependency-injection), tak aby być usługi [do widoków](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="37860-277">Like many other aspects of ASP.NET Core, views support [dependency injection](xref:fundamentals/dependency-injection), allowing services to be [injected into views](xref:mvc/views/dependency-injection).</span></span>