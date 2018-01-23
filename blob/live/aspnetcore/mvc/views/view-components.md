---
title: "Składniki w widoku"
author: rick-anderson
description: "Składniki w widoku mają gdziekolwiek się, że logika renderowania wielokrotnego użytku."
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/view-components
ms.openlocfilehash: 2d93dcee102009661af708b9a9066e8af0bdbb17
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="view-components"></a><span data-ttu-id="184d6-103">Składniki w widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-103">View components</span></span>

<span data-ttu-id="184d6-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="184d6-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="184d6-105">[Wyświetlić lub pobrać przykładowy kod](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([sposobu pobierania](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="184d6-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="introducing-view-components"></a><span data-ttu-id="184d6-106">Wprowadzenie do składników widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-106">Introducing view components</span></span>

<span data-ttu-id="184d6-107">Nowy do platformy ASP.NET Core MVC, widok składniki są podobne do widoków częściowych, ale są one bardziej wydajne.</span><span class="sxs-lookup"><span data-stu-id="184d6-107">New to ASP.NET Core MVC, view components are similar to partial views, but they are much more powerful.</span></span> <span data-ttu-id="184d6-108">Składniki w widoku nie używaj wiązania modelu i tylko zależą od podane podczas wywoływania w nim danych.</span><span class="sxs-lookup"><span data-stu-id="184d6-108">View components don’t use model binding, and only depend on the data you provide when calling into it.</span></span> <span data-ttu-id="184d6-109">Składnik widoku:</span><span class="sxs-lookup"><span data-stu-id="184d6-109">A view component:</span></span>

* <span data-ttu-id="184d6-110">Renderuje fragmentu, a nie całej odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="184d6-110">Renders a chunk rather than a whole response</span></span>
* <span data-ttu-id="184d6-111">Obejmuje takie same separacji z uwagi i korzyści z testowania znaleziono między kontrolerem a widokiem</span><span class="sxs-lookup"><span data-stu-id="184d6-111">Includes the same separation-of-concerns and testability benefits found between a controller and view</span></span>
* <span data-ttu-id="184d6-112">Może mieć parametrów i logika biznesowa</span><span class="sxs-lookup"><span data-stu-id="184d6-112">Can have parameters and business logic</span></span>
* <span data-ttu-id="184d6-113">Zazwyczaj jest wywoływany z stronę układu</span><span class="sxs-lookup"><span data-stu-id="184d6-113">Is typically invoked from a layout page</span></span>

<span data-ttu-id="184d6-114">Składniki w widoku mają gdziekolwiek się, że masz logiki renderowania wielokrotnego użytku, które jest zbyt złożony widoku częściowego, takich jak:</span><span class="sxs-lookup"><span data-stu-id="184d6-114">View components are intended anywhere you have reusable rendering logic that is too complex for a partial view, such as:</span></span>

* <span data-ttu-id="184d6-115">Menu dynamiczne nawigacji</span><span class="sxs-lookup"><span data-stu-id="184d6-115">Dynamic navigation menus</span></span>
* <span data-ttu-id="184d6-116">Chmura znaczników (gdzie zapytanie bazy danych)</span><span class="sxs-lookup"><span data-stu-id="184d6-116">Tag cloud (where it queries the database)</span></span>
* <span data-ttu-id="184d6-117">Panel logowania</span><span class="sxs-lookup"><span data-stu-id="184d6-117">Login panel</span></span>
* <span data-ttu-id="184d6-118">Koszyk</span><span class="sxs-lookup"><span data-stu-id="184d6-118">Shopping cart</span></span>
* <span data-ttu-id="184d6-119">Ostatnio opublikowanych artykułów.</span><span class="sxs-lookup"><span data-stu-id="184d6-119">Recently published articles</span></span>
* <span data-ttu-id="184d6-120">Zawartość paska bocznego w typowych blogu</span><span class="sxs-lookup"><span data-stu-id="184d6-120">Sidebar content on a typical blog</span></span>
* <span data-ttu-id="184d6-121">Panel logowania, który będzie renderowany na każdej stronie i Pokaż łącza Wyloguj się lub zaloguj w zależności od dziennika w stanie użytkownika</span><span class="sxs-lookup"><span data-stu-id="184d6-121">A login panel that would be rendered on every page and show either the links to log out or log in, depending on the log in state of the user</span></span>

<span data-ttu-id="184d6-122">Składnik widoku składa się z dwóch części: klasy (zwykle pochodną [ViewComponent](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.viewcomponent)) i wynik zwraca (zazwyczaj widok).</span><span class="sxs-lookup"><span data-stu-id="184d6-122">A view component consists of two parts: the class (typically derived from [ViewComponent](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.viewcomponent)) and the result it returns (typically a view).</span></span> <span data-ttu-id="184d6-123">Podobnie jak kontrolerów składnika Widok może być POCO, ale większość deweloperów będą korzystać z metod i właściwości dostępne przez wynikających z `ViewComponent`.</span><span class="sxs-lookup"><span data-stu-id="184d6-123">Like controllers, a view component can be a POCO, but most developers will want to take advantage of the methods and properties available by deriving from `ViewComponent`.</span></span>

## <a name="creating-a-view-component"></a><span data-ttu-id="184d6-124">Tworzenie widoku składnika</span><span class="sxs-lookup"><span data-stu-id="184d6-124">Creating a view component</span></span>

<span data-ttu-id="184d6-125">Ta sekcja zawiera ogólne wymagania można utworzyć składnika widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-125">This section contains the high-level requirements to create a view component.</span></span> <span data-ttu-id="184d6-126">W dalszej części tego artykułu możemy Sprawdź każdy krok szczegółowo i utworzyć składnika widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-126">Later in the article, we'll examine each step in detail and create a view component.</span></span>

### <a name="the-view-component-class"></a><span data-ttu-id="184d6-127">Widok klasy składnika</span><span class="sxs-lookup"><span data-stu-id="184d6-127">The view component class</span></span>

<span data-ttu-id="184d6-128">Widok klasy składnika mogą być tworzone przez jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="184d6-128">A view component class can be created by any of the following:</span></span>

* <span data-ttu-id="184d6-129">Wyprowadzanie z *ViewComponent*</span><span class="sxs-lookup"><span data-stu-id="184d6-129">Deriving from *ViewComponent*</span></span>
* <span data-ttu-id="184d6-130">Dekoracji klasy z `[ViewComponent]` atrybutu lub tworzenia klasy pochodnej z klasy z `[ViewComponent]` atrybutu</span><span class="sxs-lookup"><span data-stu-id="184d6-130">Decorating a class with the `[ViewComponent]` attribute, or deriving from a class with the `[ViewComponent]` attribute</span></span>
* <span data-ttu-id="184d6-131">Tworzenie klasy, której nazwa kończy się sufiksem *ViewComponent*</span><span class="sxs-lookup"><span data-stu-id="184d6-131">Creating a class where the name ends with the suffix *ViewComponent*</span></span>

<span data-ttu-id="184d6-132">Podobnie jak kontrolerów widok składniki muszą być publiczne, -nested i nieabstrakcyjnej klasy.</span><span class="sxs-lookup"><span data-stu-id="184d6-132">Like controllers, view components must be public, non-nested, and non-abstract classes.</span></span> <span data-ttu-id="184d6-133">Nazwa składnika widoku jest nazwą klasy wraz z sufiksem "ViewComponent" usunięte.</span><span class="sxs-lookup"><span data-stu-id="184d6-133">The view component name is the class name with the "ViewComponent" suffix removed.</span></span> <span data-ttu-id="184d6-134">Można również ją jawnie określić przy użyciu `ViewComponentAttribute.Name` właściwości.</span><span class="sxs-lookup"><span data-stu-id="184d6-134">It can also be explicitly specified using the `ViewComponentAttribute.Name` property.</span></span>

<span data-ttu-id="184d6-135">Widok klasy składnika:</span><span class="sxs-lookup"><span data-stu-id="184d6-135">A view component class:</span></span>

* <span data-ttu-id="184d6-136">W pełni obsługuje konstruktora [iniekcji zależności](../../fundamentals/dependency-injection.md)</span><span class="sxs-lookup"><span data-stu-id="184d6-136">Fully supports constructor [dependency injection](../../fundamentals/dependency-injection.md)</span></span>

* <span data-ttu-id="184d6-137">Nie uczestniczy w cyklu życia kontrolera, co oznacza, nie można użyć [filtry](../controllers/filters.md) w składniku widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-137">Does not take part in the controller lifecycle, which means you can't use [filters](../controllers/filters.md) in a view component</span></span>

### <a name="view-component-methods"></a><span data-ttu-id="184d6-138">Wyświetlanie składnika metod</span><span class="sxs-lookup"><span data-stu-id="184d6-138">View component methods</span></span>

<span data-ttu-id="184d6-139">Składnik widoku definiuje swojej logiki w `InvokeAsync` metodę zwracającą `IViewComponentResult`.</span><span class="sxs-lookup"><span data-stu-id="184d6-139">A view component defines its logic in an `InvokeAsync` method that returns an `IViewComponentResult`.</span></span> <span data-ttu-id="184d6-140">Parametry pochodzi bezpośrednio z wywołania składnika widoku, nie z wiązania modelu.</span><span class="sxs-lookup"><span data-stu-id="184d6-140">Parameters come directly from invocation of the view component, not from model binding.</span></span> <span data-ttu-id="184d6-141">Składnik widoku nigdy nie obsługuje bezpośrednio żądanie.</span><span class="sxs-lookup"><span data-stu-id="184d6-141">A view component never directly handles a request.</span></span> <span data-ttu-id="184d6-142">Zazwyczaj składnikiem widoku inicjuje modelu i przekazuje je do widoku, wywołując `View` metody.</span><span class="sxs-lookup"><span data-stu-id="184d6-142">Typically, a view component initializes a model and passes it to a view by calling the `View` method.</span></span> <span data-ttu-id="184d6-143">Podsumowując Wyświetl metody składników:</span><span class="sxs-lookup"><span data-stu-id="184d6-143">In summary, view component methods:</span></span>

* <span data-ttu-id="184d6-144">Zdefiniuj `InvokeAsync` metodę zwracającą`IViewComponentResult`</span><span class="sxs-lookup"><span data-stu-id="184d6-144">Define an `InvokeAsync` method that returns an `IViewComponentResult`</span></span>
* <span data-ttu-id="184d6-145">Zazwyczaj inicjuje modelu i przekazuje je do widoku, wywołując `ViewComponent` `View` — metoda</span><span class="sxs-lookup"><span data-stu-id="184d6-145">Typically initializes a model and passes it to a view by calling the `ViewComponent` `View` method</span></span>
* <span data-ttu-id="184d6-146">Parametry pochodzą z wywołania metody HTTP nie znajduje się nie wiązanie modelu</span><span class="sxs-lookup"><span data-stu-id="184d6-146">Parameters come from the calling method, not HTTP, there is no model binding</span></span>
* <span data-ttu-id="184d6-147">To nie jest dostępny bezpośrednio jako punkt końcowy HTTP, ich wywołania w kodzie (zazwyczaj w widoku).</span><span class="sxs-lookup"><span data-stu-id="184d6-147">Are not reachable directly as an HTTP endpoint, they are invoked from your code (usually in a view).</span></span> <span data-ttu-id="184d6-148">Składnik widoku nigdy nie obsługuje żądania</span><span class="sxs-lookup"><span data-stu-id="184d6-148">A view component never handles a request</span></span>
* <span data-ttu-id="184d6-149">Są przeciążone w sygnaturze, a nie wszystkie szczegóły z bieżącego żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="184d6-149">Are overloaded on the signature rather than any details from the current HTTP request</span></span>

### <a name="view-search-path"></a><span data-ttu-id="184d6-150">Ścieżki wyszukiwania widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-150">View search path</span></span>

<span data-ttu-id="184d6-151">Środowisko uruchomieniowe wyszukuje widoku w następujących ścieżkach:</span><span class="sxs-lookup"><span data-stu-id="184d6-151">The runtime searches for the view in the following paths:</span></span>

   * <span data-ttu-id="184d6-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="184d6-152">Views/\<controller_name>/Components/\<view_component_name>/\<view_name></span></span>
   * <span data-ttu-id="184d6-153">Views/Shared/Components/\<view_component_name>/\<view_name></span><span class="sxs-lookup"><span data-stu-id="184d6-153">Views/Shared/Components/\<view_component_name>/\<view_name></span></span>

<span data-ttu-id="184d6-154">Domyślna nazwa widoku dla składnika widoku to *domyślne*, co oznacza, że plik widoku zazwyczaj będzie miała nazwę *Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="184d6-154">The default view name for a view component is *Default*, which means your view file will typically be named *Default.cshtml*.</span></span> <span data-ttu-id="184d6-155">Można określić nazwę inny widok, podczas tworzenia składnika wynik widoku lub podczas wywoływania metody `View` metody.</span><span class="sxs-lookup"><span data-stu-id="184d6-155">You can specify a different view name when creating the view component result or when calling the `View` method.</span></span>

<span data-ttu-id="184d6-156">Firma Microsoft zaleca, nazwa pliku widoku *Default.cshtml* i użyj *widoków/Shared/składniki/\<view_component_name > /\<view_name >* ścieżki.</span><span class="sxs-lookup"><span data-stu-id="184d6-156">We recommend you name the view file *Default.cshtml* and use the *Views/Shared/Components/\<view_component_name>/\<view_name>* path.</span></span> <span data-ttu-id="184d6-157">`PriorityList` Składnik widoku używany w tym przykładzie używa *Views/Shared/Components/PriorityList/Default.cshtml* widoku składnika widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-157">The `PriorityList` view component used in this sample uses *Views/Shared/Components/PriorityList/Default.cshtml* for the view component view.</span></span>

## <a name="invoking-a-view-component"></a><span data-ttu-id="184d6-158">Wywoływanie składnika widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-158">Invoking a view component</span></span>

<span data-ttu-id="184d6-159">Aby użyć widoku składnika, wywołaj następujące wewnątrz widoku:</span><span class="sxs-lookup"><span data-stu-id="184d6-159">To use the view component, call the following inside a view:</span></span>

```cshtml
@Component.InvokeAsync("Name of view component", <anonymous type containing parameters>)
```

<span data-ttu-id="184d6-160">Parametry zostaną przekazane do `InvokeAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="184d6-160">The parameters will be passed to the `InvokeAsync` method.</span></span> <span data-ttu-id="184d6-161">`PriorityList` Składnika widoku opracowane w artykule jest wywoływany z *Views/Todo/Index.cshtml* widoku pliku.</span><span class="sxs-lookup"><span data-stu-id="184d6-161">The `PriorityList` view component developed in the article is invoked from the *Views/Todo/Index.cshtml* view file.</span></span> <span data-ttu-id="184d6-162">Poniższa `InvokeAsync` metoda jest wywoływana z dwoma parametrami:</span><span class="sxs-lookup"><span data-stu-id="184d6-162">In the following, the `InvokeAsync` method is called with two parameters:</span></span>

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

## <a name="invoking-a-view-component-as-a-tag-helper"></a><span data-ttu-id="184d6-163">Wywoływanie składnika widoku jako pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="184d6-163">Invoking a view component as a Tag Helper</span></span>

<span data-ttu-id="184d6-164">Dla platformy ASP.NET Core 1.1 i wyższych, można wywołać składnika widoku jako [pomocnika tagów](xref:mvc/views/tag-helpers/intro):</span><span class="sxs-lookup"><span data-stu-id="184d6-164">For ASP.NET Core 1.1 and higher, you can invoke a view component as a [Tag Helper](xref:mvc/views/tag-helpers/intro):</span></span>

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="184d6-165">Pascal — z uwzględnieniem wielkości liter klasy i metody parametrów dla pomocników tagów są przekształcane na ich [obniżyć przypadku kebab](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span><span class="sxs-lookup"><span data-stu-id="184d6-165">Pascal-cased class and method parameters for Tag Helpers are translated into their [lower kebab case](https://stackoverflow.com/questions/11273282/whats-the-name-for-dash-separated-case/12273101).</span></span> <span data-ttu-id="184d6-166">Używa pomocnika tagów do wywołania składnika widoku `<vc></vc>` elementu.</span><span class="sxs-lookup"><span data-stu-id="184d6-166">The Tag Helper to invoke a view component uses the `<vc></vc>` element.</span></span> <span data-ttu-id="184d6-167">Składnik widoku określono w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="184d6-167">The view component is specified as follows:</span></span>

```cshtml
<vc:[view-component-name]
  parameter1="parameter1 value"
  parameter2="parameter2 value">
</vc:[view-component-name]>
```

<span data-ttu-id="184d6-168">Uwaga: Aby można było używać składnika widoku jako pomocnika tagów, należy zarejestrować zestawu zawierającego przy użyciu składnika widoku `@addTagHelper` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="184d6-168">Note: In order to use a View Component as a Tag Helper, you must register the assembly containing the View Component using the `@addTagHelper` directive.</span></span> <span data-ttu-id="184d6-169">Na przykład, jeśli składnik widoku znajduje się w zestawie o nazwie "MyWebApp", Dodaj następujące dyrektywy `_ViewImports.cshtml` pliku:</span><span class="sxs-lookup"><span data-stu-id="184d6-169">For example, if your View Component is in an assembly called "MyWebApp", add the following directive to the `_ViewImports.cshtml` file:</span></span>

```cshtml
@addTagHelper *, MyWebApp
```

<span data-ttu-id="184d6-170">Można zarejestrować składnika widoku jako pomocnika tagów do każdego pliku, który odwołuje się do składnika widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-170">You can register a View Component as a Tag Helper to any file that references the View Component.</span></span> <span data-ttu-id="184d6-171">Zobacz [Zarządzanie zakresu pomocnika tagów](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) Aby uzyskać więcej informacji na temat rejestrowania pomocników tagów.</span><span class="sxs-lookup"><span data-stu-id="184d6-171">See [Managing Tag Helper Scope](xref:mvc/views/tag-helpers/intro#managing-tag-helper-scope) for more information on how to register Tag Helpers.</span></span>

<span data-ttu-id="184d6-172">`InvokeAsync` Metodę używaną w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="184d6-172">The `InvokeAsync` method used in this tutorial:</span></span>

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="184d6-173">W znaczniku pomocnika tagów:</span><span class="sxs-lookup"><span data-stu-id="184d6-173">In Tag Helper markup:</span></span>

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexTagHelper.cshtml?range=37-38)]

<span data-ttu-id="184d6-174">W powyższym przykładowym `PriorityList` staje się widok składnika `priority-list`.</span><span class="sxs-lookup"><span data-stu-id="184d6-174">In the sample above, the `PriorityList` view component becomes `priority-list`.</span></span> <span data-ttu-id="184d6-175">Parametry do składnika widoku są przekazywane jako atrybuty w przypadku kebab niższa.</span><span class="sxs-lookup"><span data-stu-id="184d6-175">The parameters to the view component are passed as attributes in lower kebab case.</span></span>

### <a name="invoking-a-view-component-directly-from-a-controller"></a><span data-ttu-id="184d6-176">Wywoływanie składnika widoku bezpośrednio z kontrolerem</span><span class="sxs-lookup"><span data-stu-id="184d6-176">Invoking a view component directly from a controller</span></span>

<span data-ttu-id="184d6-177">Widok składniki zwykle są wywoływane z widoku, ale można ich wywoływać bezpośrednio z metody kontrolera.</span><span class="sxs-lookup"><span data-stu-id="184d6-177">View components are typically invoked from a view, but you can invoke them directly from a controller method.</span></span> <span data-ttu-id="184d6-178">Podczas wyświetlania składników nie definiują punktów końcowych, takie jak kontrolerów, można łatwo zaimplementować akcji kontrolera, która zwraca zawartość `ViewComponentResult`.</span><span class="sxs-lookup"><span data-stu-id="184d6-178">While view components do not define endpoints like controllers, you can easily implement a controller action that returns the content of a `ViewComponentResult`.</span></span>

<span data-ttu-id="184d6-179">W tym przykładzie składnik widoku jest wywoływany bezpośrednio z kontrolerem:</span><span class="sxs-lookup"><span data-stu-id="184d6-179">In this example, the view component is called directly from the controller:</span></span>

[!code-csharp[Main](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

## <a name="walkthrough-creating-a-simple-view-component"></a><span data-ttu-id="184d6-180">Wskazówki: Tworzenie składnika prosty widok</span><span class="sxs-lookup"><span data-stu-id="184d6-180">Walkthrough: Creating a simple view component</span></span>

<span data-ttu-id="184d6-181">[Pobierz](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), tworzenia i testowania kodu początkowego.</span><span class="sxs-lookup"><span data-stu-id="184d6-181">[Download](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/view-components/sample), build and test the starter code.</span></span> <span data-ttu-id="184d6-182">Jest proste projektu z `Todo` kontrolera, który wyświetla listę *Todo* elementów.</span><span class="sxs-lookup"><span data-stu-id="184d6-182">It's a simple project with a `Todo` controller that displays a list of *Todo* items.</span></span>

![Lista ToDos](view-components/_static/2dos.png)

### <a name="add-a-viewcomponent-class"></a><span data-ttu-id="184d6-184">Dodaj klasę ViewComponent</span><span class="sxs-lookup"><span data-stu-id="184d6-184">Add a ViewComponent class</span></span>

<span data-ttu-id="184d6-185">Utwórz *ViewComponents* folderu i dodaj następującą `PriorityListViewComponent` klasy:</span><span class="sxs-lookup"><span data-stu-id="184d6-185">Create a *ViewComponents* folder and add the following `PriorityListViewComponent` class:</span></span>

[!code-csharp[Main](view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponent1.cs?name=snippet1)]

<span data-ttu-id="184d6-186">Uwagi o kodzie:</span><span class="sxs-lookup"><span data-stu-id="184d6-186">Notes on the code:</span></span>

* <span data-ttu-id="184d6-187">Widok klas składników mogą być zawarte w **żadnych** folderu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="184d6-187">View component classes can be contained in **any** folder in the project.</span></span>
* <span data-ttu-id="184d6-188">Klasa name PriorityList**ViewComponent** kończy się sufiksem **ViewComponent**, środowisko wykonawcze będzie używać ciągu "PriorityList" podczas odwoływania się do składnika klasy z widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-188">Because the class name PriorityList**ViewComponent** ends with the suffix **ViewComponent**, the runtime will use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="184d6-189">I będzie wyjaśnić, że bardziej szczegółowo później.</span><span class="sxs-lookup"><span data-stu-id="184d6-189">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="184d6-190">`[ViewComponent]` Atrybutu można zmienić nazwę używaną do odwołania składnika widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-190">The `[ViewComponent]` attribute can change the name used to reference a view component.</span></span> <span data-ttu-id="184d6-191">Na przykład firma Microsoft może mieć o nazwie klasy `XYZ` i stosowane `ViewComponent` atrybutu:</span><span class="sxs-lookup"><span data-stu-id="184d6-191">For example, we could have named the class `XYZ` and applied the `ViewComponent` attribute:</span></span>

  ```csharp
  [ViewComponent(Name = "PriorityList")]
     public class XYZ : ViewComponent
     ```

* <span data-ttu-id="184d6-192">`[ViewComponent]` Atrybut powyżej informuje selektor składnika Widok, aby użyć nazwy `PriorityList` podczas wyszukiwania dla widoków skojarzone ze składnikiem i aby użyć ciągu "PriorityList" podczas odwoływania się do składnika klasy z widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-192">The `[ViewComponent]` attribute above tells the view component selector to use the name `PriorityList` when looking for the views associated with the component, and to use the string "PriorityList" when referencing the class component from a view.</span></span> <span data-ttu-id="184d6-193">I będzie wyjaśnić, że bardziej szczegółowo później.</span><span class="sxs-lookup"><span data-stu-id="184d6-193">I'll explain that in more detail later.</span></span>
* <span data-ttu-id="184d6-194">Używany przez składnik [iniekcji zależności](../../fundamentals/dependency-injection.md) udostępnić kontekstu danych.</span><span class="sxs-lookup"><span data-stu-id="184d6-194">The component uses [dependency injection](../../fundamentals/dependency-injection.md) to make the data context available.</span></span>
* <span data-ttu-id="184d6-195">`InvokeAsync`udostępnia metodę, która może zostać wywołana z widoku, a może zająć dowolnej liczby argumentów.</span><span class="sxs-lookup"><span data-stu-id="184d6-195">`InvokeAsync` exposes a method which can be called from a view, and it can take an arbitrary number of arguments.</span></span>
* <span data-ttu-id="184d6-196">`InvokeAsync` Metoda zwraca zbiór `ToDo` elementów, które spełniają `isDone` i `maxPriority` parametrów.</span><span class="sxs-lookup"><span data-stu-id="184d6-196">The `InvokeAsync` method returns the set of `ToDo` items that satisfy the `isDone` and `maxPriority` parameters.</span></span>

### <a name="create-the-view-component-razor-view"></a><span data-ttu-id="184d6-197">Tworzenie widoku Razor składnika widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-197">Create the view component Razor view</span></span>

* <span data-ttu-id="184d6-198">Utwórz *widoków/Shared/składniki* folderu.</span><span class="sxs-lookup"><span data-stu-id="184d6-198">Create the *Views/Shared/Components* folder.</span></span> <span data-ttu-id="184d6-199">Ten folder **musi** nosić *składniki*.</span><span class="sxs-lookup"><span data-stu-id="184d6-199">This folder **must** be named *Components*.</span></span>

* <span data-ttu-id="184d6-200">Utwórz *widoków/Shared/składniki/PriorityList* folderu.</span><span class="sxs-lookup"><span data-stu-id="184d6-200">Create the *Views/Shared/Components/PriorityList* folder.</span></span> <span data-ttu-id="184d6-201">Nazwa tego folderu muszą być zgodne, nazwa klasy części widoku lub nazwę klasy minus sufiks (jeśli mamy po Konwencji i używana *ViewComponent* sufiksu w nazwie klasy).</span><span class="sxs-lookup"><span data-stu-id="184d6-201">This folder name must match the name of the view component class, or the name of the class minus the suffix (if we followed convention and used the *ViewComponent* suffix in the class name).</span></span> <span data-ttu-id="184d6-202">Jeśli używasz `ViewComponent` atrybutu, nazwa klasy musi do dopasowania nazwy atrybutu.</span><span class="sxs-lookup"><span data-stu-id="184d6-202">If you used the `ViewComponent` attribute, the class name would need to match the attribute designation.</span></span>

* <span data-ttu-id="184d6-203">Utwórz *Views/Shared/Components/PriorityList/Default.cshtml* widoku Razor:[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span><span class="sxs-lookup"><span data-stu-id="184d6-203">Create a *Views/Shared/Components/PriorityList/Default.cshtml* Razor view: [!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/Default1.cshtml)]</span></span>
    
   <span data-ttu-id="184d6-204">W widoku Razor przyjmuje listę `TodoItem` i wyświetla je.</span><span class="sxs-lookup"><span data-stu-id="184d6-204">The Razor view takes a list of `TodoItem` and displays them.</span></span> <span data-ttu-id="184d6-205">Jeśli składnik widoku `InvokeAsync` — metoda nie przeszło nazwę widoku (w naszym przykładzie) *domyślne* jest używany dla nazwy widoku przez Konwencję.</span><span class="sxs-lookup"><span data-stu-id="184d6-205">If the view component `InvokeAsync` method doesn't pass the name of the view (as in our sample), *Default* is used for the view name by convention.</span></span> <span data-ttu-id="184d6-206">W dalszej części samouczka I opisano sposób przekazywania nazwy widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-206">Later in the tutorial, I'll show you how to pass the name of the view.</span></span> <span data-ttu-id="184d6-207">Aby zastąpić stylem domyślnym dla określonego kontrolera, Dodaj widok do folderu określonego kontrolera widoku (na przykład *Views/Todo/Components/PriorityList/Default.cshtml)*.</span><span class="sxs-lookup"><span data-stu-id="184d6-207">To override the default styling for a specific controller, add a view to the controller-specific view folder (for example *Views/Todo/Components/PriorityList/Default.cshtml)*.</span></span>
    
    <span data-ttu-id="184d6-208">Jeśli składnik widoku jest specyficzne dla kontrolera, można dodać go do folderu kontrolera specyficznych (*Views/Todo/Components/PriorityList/Default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="184d6-208">If the view component is controller-specific, you can add it to the controller-specific folder (*Views/Todo/Components/PriorityList/Default.cshtml*).</span></span>

* <span data-ttu-id="184d6-209">Dodaj `div` zawierającym wywołanie składnika listy Priorytet do dołu *Views/Todo/index.cshtml* pliku:</span><span class="sxs-lookup"><span data-stu-id="184d6-209">Add a `div` containing a call to the priority list component to the bottom of the *Views/Todo/index.cshtml* file:</span></span>

    [!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFirst.cshtml?range=34-38)]

<span data-ttu-id="184d6-210">Kod znaczników `@await Component.InvokeAsync` przedstawiono składnię wywoływania wyświetlania składników.</span><span class="sxs-lookup"><span data-stu-id="184d6-210">The markup `@await Component.InvokeAsync` shows the syntax for calling view components.</span></span> <span data-ttu-id="184d6-211">Pierwszy argument jest nazwa składnika, którą chcemy udostępnić wywołania lub zadzwoń.</span><span class="sxs-lookup"><span data-stu-id="184d6-211">The first argument is the name of the component we want to invoke or call.</span></span> <span data-ttu-id="184d6-212">Kolejne parametry są przekazywane do składnika.</span><span class="sxs-lookup"><span data-stu-id="184d6-212">Subsequent parameters are passed to the component.</span></span> <span data-ttu-id="184d6-213">`InvokeAsync`może być dowolną liczbę argumentów.</span><span class="sxs-lookup"><span data-stu-id="184d6-213">`InvokeAsync` can take an arbitrary number of arguments.</span></span>

<span data-ttu-id="184d6-214">Testowanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="184d6-214">Test the app.</span></span> <span data-ttu-id="184d6-215">Na poniższej ilustracji przedstawiono listy rzeczy do zrobienia, a elementy o priorytecie:</span><span class="sxs-lookup"><span data-stu-id="184d6-215">The following image shows the ToDo list and the priority items:</span></span>

![elementy listy i priorytet ToDo](view-components/_static/pi.png)

<span data-ttu-id="184d6-217">Możesz także wywołać bezpośrednio z kontrolera składnika widoku:</span><span class="sxs-lookup"><span data-stu-id="184d6-217">You can also call the view component directly from the controller:</span></span>

[!code-csharp[Main](view-components/sample/ViewCompFinal/Controllers/ToDoController.cs?name=snippet_IndexVC)]

![priorytet elementy z IndexVC akcji](view-components/_static/indexvc.png)

### <a name="specifying-a-view-name"></a><span data-ttu-id="184d6-219">Określanie nazwy widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-219">Specifying a view name</span></span>

<span data-ttu-id="184d6-220">Składnik złożonego widoku może należy określić widok z systemem innym niż domyślny, w niektórych warunkach.</span><span class="sxs-lookup"><span data-stu-id="184d6-220">A complex view component might need to specify a non-default view under some conditions.</span></span> <span data-ttu-id="184d6-221">Poniższy kod przedstawia sposób określania widoku "PVC" z `InvokeAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="184d6-221">The following code shows how to specify the "PVC" view  from the `InvokeAsync` method.</span></span> <span data-ttu-id="184d6-222">Aktualizacja `InvokeAsync` metoda `PriorityListViewComponent` klasy.</span><span class="sxs-lookup"><span data-stu-id="184d6-222">Update the `InvokeAsync` method in the `PriorityListViewComponent` class.</span></span>

[!code-csharp[Main](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityListViewComponentFinal.cs?highlight=4,5,6,7,8,9&range=28-39)]

<span data-ttu-id="184d6-223">Kopiuj *Views/Shared/Components/PriorityList/Default.cshtml* pliku do widoku o nazwie *Views/Shared/Components/PriorityList/PVC.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="184d6-223">Copy the *Views/Shared/Components/PriorityList/Default.cshtml* file to a view named *Views/Shared/Components/PriorityList/PVC.cshtml*.</span></span> <span data-ttu-id="184d6-224">Dodaj nagłówek wskazuje, że widok PVC jest używany.</span><span class="sxs-lookup"><span data-stu-id="184d6-224">Add a heading to indicate the PVC view is being used.</span></span>

[!code-cshtml[Main](../../mvc/views/view-components/sample/ViewCompFinal/Views/Shared/Components/PriorityList/PVC.cshtml?highlight=3)]

<span data-ttu-id="184d6-225">Aktualizacja *Views/TodoList/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="184d6-225">Update *Views/TodoList/Index.cshtml*:</span></span>

<!-- Views/TodoList/Index.cshtml is never imported, so change to test tutorial -->

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexFinal.cshtml?range=35)]

<span data-ttu-id="184d6-226">Uruchom aplikację i zweryfikować PVC widoku.</span><span class="sxs-lookup"><span data-stu-id="184d6-226">Run the app and verify PVC view.</span></span>

![Priorytet widoku składnika](view-components/_static/pvc.png)

<span data-ttu-id="184d6-228">Jeśli widok PVC nie są odtwarzane, sprawdź, czy są wywoływanie składnika widoku priorytet wynosi 4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="184d6-228">If the PVC view is not rendered, verify you are calling the view component with a priority of 4 or higher.</span></span>

### <a name="examine-the-view-path"></a><span data-ttu-id="184d6-229">Sprawdź ścieżkę widoku</span><span class="sxs-lookup"><span data-stu-id="184d6-229">Examine the view path</span></span>

* <span data-ttu-id="184d6-230">Zmień parametr priorytet do trzech lub mniej, aby widok priorytet nie są zwracane.</span><span class="sxs-lookup"><span data-stu-id="184d6-230">Change the priority parameter to three or less so the priority view is not returned.</span></span>
* <span data-ttu-id="184d6-231">Tymczasowo zmień nazwę *Views/Todo/Components/PriorityList/Default.cshtml* do *1Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="184d6-231">Temporarily rename the *Views/Todo/Components/PriorityList/Default.cshtml* to *1Default.cshtml*.</span></span>
* <span data-ttu-id="184d6-232">Testowanie aplikacji, zostanie wyświetlony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="184d6-232">Test the app, you'll get the following error:</span></span>

   ```
   An unhandled exception occurred while processing the request.
   InvalidOperationException: The view 'Components/PriorityList/Default' was not found. The following locations were searched:
   /Views/ToDo/Components/PriorityList/Default.cshtml
   /Views/Shared/Components/PriorityList/Default.cshtml
   EnsureSuccessful
   ```

* <span data-ttu-id="184d6-233">Kopiuj *Views/Todo/Components/PriorityList/1Default.cshtml* do *Views/Shared/Components/PriorityList/Default.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="184d6-233">Copy *Views/Todo/Components/PriorityList/1Default.cshtml* to *Views/Shared/Components/PriorityList/Default.cshtml*.</span></span>
* <span data-ttu-id="184d6-234">Niektóre znaczników, aby dodać *Shared* Todo widoku składnika widoku, aby wskazać widoku pochodzi z *Shared* folderu.</span><span class="sxs-lookup"><span data-stu-id="184d6-234">Add some markup to the *Shared* Todo view component view to indicate the view is from the *Shared* folder.</span></span>
* <span data-ttu-id="184d6-235">Test **Shared** widok składnika.</span><span class="sxs-lookup"><span data-stu-id="184d6-235">Test the **Shared** component view.</span></span>

![Dane wyjściowe zadania z widoku składnika współużytkowanego](view-components/_static/shared.png)

### <a name="avoiding-magic-strings"></a><span data-ttu-id="184d6-237">Unikanie magic ciągów</span><span class="sxs-lookup"><span data-stu-id="184d6-237">Avoiding magic strings</span></span>

<span data-ttu-id="184d6-238">Jeśli chcesz skompilować bezpieczeństwa czasu, nazwy składnika ustalony widoku można zastąpić nazwę klasy.</span><span class="sxs-lookup"><span data-stu-id="184d6-238">If you want compile time safety, you can replace the hard-coded view component name with the class name.</span></span> <span data-ttu-id="184d6-239">Utwórz widok składnika sufiksu "ViewComponent":</span><span class="sxs-lookup"><span data-stu-id="184d6-239">Create the view component without the "ViewComponent" suffix:</span></span>

[!code-csharp[Main](../../mvc/views/view-components/sample/ViewCompFinal/ViewComponents/PriorityList.cs?highlight=10&range=5-35)]

<span data-ttu-id="184d6-240">Dodaj `using` oświadczenie do użytkownika Razor wyświetlanie plików i używanie `nameof` operator:</span><span class="sxs-lookup"><span data-stu-id="184d6-240">Add a `using` statement to your Razor view file, and use the `nameof` operator:</span></span>

[!code-cshtml[Main](view-components/sample/ViewCompFinal/Views/Todo/IndexNameof.cshtml?range=1-6,33-)]

## <a name="additional-resources"></a><span data-ttu-id="184d6-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="184d6-241">Additional Resources</span></span>

* [<span data-ttu-id="184d6-242">Wstrzykiwanie zależności do widoków</span><span class="sxs-lookup"><span data-stu-id="184d6-242">Dependency injection into views</span></span>](dependency-injection.md)