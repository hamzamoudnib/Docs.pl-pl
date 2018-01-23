---
title: "Pomocników tagów w platformy ASP.NET Core"
author: rick-anderson
description: "Poznaj pomocników tagów są i sposobu ich używania w ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 7/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/tag-helpers/intro
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 003a22d4b0d9400f3e9effe0892d2d7e03704cde
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-tag-helpers-in-aspnet-core"></a><span data-ttu-id="23895-103">Wprowadzenie do pomocników tagów w platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="23895-103">Introduction to Tag Helpers in ASP.NET Core</span></span> 

<span data-ttu-id="23895-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="23895-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="what-are-tag-helpers"></a><span data-ttu-id="23895-105">Co to są pomocników tagów?</span><span class="sxs-lookup"><span data-stu-id="23895-105">What are Tag Helpers?</span></span>

<span data-ttu-id="23895-106">Pomocników tagów włączyć kod po stronie serwera do tworzenia i renderowania elementów HTML w plikach Razor.</span><span class="sxs-lookup"><span data-stu-id="23895-106">Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="23895-107">Na przykład wbudowana `ImageTagHelper` dołączyć do nazwy obrazu numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="23895-107">For example, the built-in `ImageTagHelper` can append a version number to the image name.</span></span> <span data-ttu-id="23895-108">Przy każdej zmianie obrazu serwera generuje nową wersję unikatowy dla obrazu, więc klienci dotrą do pobrania bieżącego obrazu (zamiast starych obrazu pamięci podręcznej).</span><span class="sxs-lookup"><span data-stu-id="23895-108">Whenever the image changes, the server generates a new unique version for the image, so clients are guaranteed to get the current image (instead of a stale cached image).</span></span> <span data-ttu-id="23895-109">Istnieje wiele wbudowanych pomocników tagów do wykonywania typowych zadań — takich jak tworzenie formularzy, łącza, ładowanie zasobów i pakietów więcej — i jeszcze bardziej dostępne w publicznych repozytoriach usługi GitHub i NuGet.</span><span class="sxs-lookup"><span data-stu-id="23895-109">There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.</span></span> <span data-ttu-id="23895-110">Pomocników tagów są tworzone w języku C# i ich elementami docelowymi na podstawie nazwy elementu, atrybutu nazwy lub tagu nadrzędnym elementów HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-110">Tag Helpers are authored in C#, and they target HTML elements based on element name, attribute name, or parent tag.</span></span> <span data-ttu-id="23895-111">Na przykład wbudowana `LabelTagHelper` celem może być HTML `<label>` elementu podczas `LabelTagHelper` atrybutów są stosowane.</span><span class="sxs-lookup"><span data-stu-id="23895-111">For example, the built-in `LabelTagHelper` can target the HTML `<label>` element when the `LabelTagHelper` attributes are applied.</span></span> <span data-ttu-id="23895-112">Jeśli znasz [pomocników HTML](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), pomocników tagów zmniejszyć jawne przejścia między HTML i C# w widokach Razor.</span><span class="sxs-lookup"><span data-stu-id="23895-112">If you're familiar with [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers), Tag Helpers reduce the explicit transitions between HTML and C# in Razor views.</span></span> <span data-ttu-id="23895-113">W wielu przypadkach pomocników HTML Podaj informacje o innym podejściu do określonych pomocniczego znacznika, ale ważne jest, aby rozpoznać pomocników tagów nie zastępują pomocników HTML, a nie ma tagu pomocnika dla każdego pomocnika kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-113">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers do not replace HTML Helpers and there is not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="23895-114">[W porównaniu do pomocników HTML pomocników tagów](#tag-helpers-compared-to-html-helpers) wyjaśniono różnice bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="23895-114">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span>

## <a name="what-tag-helpers-provide"></a><span data-ttu-id="23895-115">Podaj pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-115">What Tag Helpers provide</span></span>

<span data-ttu-id="23895-116">**Środowisko programistyczne HTML przyjaznego** najbardziej części znaczników Razor przy użyciu pomocników tagów wygląda jak standardowy HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-116">**An HTML-friendly development experience** For the most part, Razor markup using Tag Helpers looks like standard HTML.</span></span> <span data-ttu-id="23895-117">Projektanci frontonu conversant HTML/CSS/JavaScript można edytować Razor bez uzyskiwania składni Razor C#.</span><span class="sxs-lookup"><span data-stu-id="23895-117">Front-end designers conversant with HTML/CSS/JavaScript can edit Razor without learning C# Razor syntax.</span></span>

<span data-ttu-id="23895-118">**Bogate środowisko funkcji IntelliSense do tworzenia znaczników HTML i Razor** jest natomiast sharp do pomocników HTML, poprzednie podejście do tworzenia znaczników w widokach Razor po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="23895-118">**A rich IntelliSense environment for creating HTML and Razor markup** This is in sharp contrast to HTML Helpers, the previous approach to server-side creation of markup in Razor views.</span></span> <span data-ttu-id="23895-119">[W porównaniu do pomocników HTML pomocników tagów](#tag-helpers-compared-to-html-helpers) wyjaśniono różnice bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="23895-119">[Tag Helpers compared to HTML Helpers](#tag-helpers-compared-to-html-helpers) explains the differences in more detail.</span></span> <span data-ttu-id="23895-120">[Obsługę funkcji IntelliSense dla pomocników tagów](#intellisense-support-for-tag-helpers) opisano środowisko IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="23895-120">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) explains the IntelliSense environment.</span></span> <span data-ttu-id="23895-121">Deweloperzy nawet ze składni Razor C# są bardziej wydajnej pracy przy użyciu pomocników tagów niż pisanie kodu C# Razor znaczników.</span><span class="sxs-lookup"><span data-stu-id="23895-121">Even developers experienced with Razor C# syntax are more productive using Tag Helpers than writing C# Razor markup.</span></span>

<span data-ttu-id="23895-122">**Można dokonać bardziej wydajną i może wygenerować bardziej niezawodne, niezawodne i kodu za pomocą informacje są dostępne tylko na serwerze** na przykład w przeszłości mantra na aktualizowanie obrazów była zmiana nazwy obrazu po zmianie obraz.</span><span class="sxs-lookup"><span data-stu-id="23895-122">**A way to make you more productive and able to produce more robust, reliable, and maintainable code using information only available on the server** For example, historically the mantra on updating images was to change the name of the image when you change the image.</span></span> <span data-ttu-id="23895-123">Obrazy mają być buforowane agresywnie ze względu na wydajność, a jeśli nie zmienisz nazwę obrazu ryzyka klientom pobieranie starych kopii.</span><span class="sxs-lookup"><span data-stu-id="23895-123">Images should be aggressively cached for performance reasons, and unless you change the name of an image, you risk clients getting a stale copy.</span></span> <span data-ttu-id="23895-124">W przeszłości po obraz był edytowany, nazwa ma zostać zmienione, a każde odwołanie do obrazu w aplikacji sieci web nie trzeba aktualizować.</span><span class="sxs-lookup"><span data-stu-id="23895-124">Historically, after an image was edited, the name had to be changed and each reference to the image in the web app needed to be updated.</span></span> <span data-ttu-id="23895-125">Nie tylko jest to bardzo pracę znacznym, jest również podatna (można pominąć odwołanie, przypadkowo wprowadź nieprawidłowy ciąg znaków, itp.) Wbudowane `ImageTagHelper` można wykonać tej operacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="23895-125">Not only is this very labor intensive, it's also error prone (you could miss a reference, accidentally enter the wrong string, etc.) The built-in `ImageTagHelper` can do this for you automatically.</span></span> <span data-ttu-id="23895-126">`ImageTagHelper` Dołączyć wersję numer do nazwy obrazu, więc przy każdej zmianie obrazu serwera automatycznie generuje nową wersję unikatowy dla obrazu.</span><span class="sxs-lookup"><span data-stu-id="23895-126">The `ImageTagHelper` can append a version number to the image name, so whenever the image changes, the server automatically generates a new unique version for the image.</span></span> <span data-ttu-id="23895-127">Klienci dotrą do pobrania bieżącego obrazu.</span><span class="sxs-lookup"><span data-stu-id="23895-127">Clients are guaranteed to get the current image.</span></span> <span data-ttu-id="23895-128">Ten oszczędności niezawodności i instalacyjne pochodzą zasadniczo wolnego przy użyciu `ImageTagHelper`.</span><span class="sxs-lookup"><span data-stu-id="23895-128">This robustness and labor savings comes essentially free by using the `ImageTagHelper`.</span></span>

<span data-ttu-id="23895-129">Większość wbudowanych pomocników tagów target istniejących elementów HTML i udostępniania atrybutów po stronie serwera dla elementu.</span><span class="sxs-lookup"><span data-stu-id="23895-129">Most of the built-in Tag Helpers target existing HTML elements and provide server-side attributes for the element.</span></span> <span data-ttu-id="23895-130">Na przykład `<input>` element używany w wielu widoków *widoków/konta* folder zawiera `asp-for` atrybut, który wyodrębnia nazwa właściwości określonego modelu do renderowanego kodu HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-130">For example, the `<input>` element used in many of the views in the *Views/Account* folder contains the `asp-for` attribute, which extracts the name of the specified model property into the rendered HTML.</span></span> <span data-ttu-id="23895-131">Następujący kod Razor:</span><span class="sxs-lookup"><span data-stu-id="23895-131">The following Razor markup:</span></span>

```cshtml
<label asp-for="Email"></label>
```

<span data-ttu-id="23895-132">Generuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="23895-132">Generates the following HTML:</span></span>

```cshtml
<label for="Email">Email</label>
```

<span data-ttu-id="23895-133">`asp-for` Atrybutu jest udostępniana przez `For` właściwości w `LabelTagHelper`.</span><span class="sxs-lookup"><span data-stu-id="23895-133">The `asp-for` attribute is made available by the `For` property in the `LabelTagHelper`.</span></span> <span data-ttu-id="23895-134">Zobacz [tworzenia pomocników tagów](authoring.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="23895-134">See [Authoring Tag Helpers](authoring.md) for more information.</span></span>

## <a name="managing-tag-helper-scope"></a><span data-ttu-id="23895-135">Zarządzanie zakresem pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="23895-135">Managing Tag Helper scope</span></span>

<span data-ttu-id="23895-136">Zakres pomocników tagów jest kontrolowany przy użyciu kombinacji `@addTagHelper`, `@removeTagHelper`i "!" Wypisz znaków.</span><span class="sxs-lookup"><span data-stu-id="23895-136">Tag Helpers scope is controlled by a combination of `@addTagHelper`, `@removeTagHelper`, and the "!" opt-out character.</span></span>

<a name="add-helper-label"></a>

### <a name="addtaghelper-makes-tag-helpers-available"></a><span data-ttu-id="23895-137">`@addTagHelper`udostępnia pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-137">`@addTagHelper` makes Tag Helpers available</span></span>

<span data-ttu-id="23895-138">Jeśli tworzenie nowej aplikacji sieci web platformy ASP.NET Core o nazwie *AuthoringTagHelpers* (z bez uwierzytelniania), następujące *Views/_ViewImports.cshtml* plik zostanie dodany do projektu:</span><span class="sxs-lookup"><span data-stu-id="23895-138">If you create a new ASP.NET Core web app named *AuthoringTagHelpers* (with no authentication), the following *Views/_ViewImports.cshtml* file will be added to your project:</span></span>

[!code-cshtml[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=2&range=2-3)]

<span data-ttu-id="23895-139">`@addTagHelper` Dyrektywy udostępnia pomocników tagów do widoku.</span><span class="sxs-lookup"><span data-stu-id="23895-139">The `@addTagHelper` directive makes Tag Helpers available to the view.</span></span> <span data-ttu-id="23895-140">W tym przypadku jest plik widoku *Views/_ViewImports.cshtml*, która domyślnie jest dziedziczona przez wszystkie pliki widoku w *widoków* folder i podkatalogów; udostępnianie pomocników tagów.</span><span class="sxs-lookup"><span data-stu-id="23895-140">In this case, the view file is *Views/_ViewImports.cshtml*, which by default is inherited by all view files in the *Views* folder and sub-directories; making Tag Helpers available.</span></span> <span data-ttu-id="23895-141">Powyższy kod używa składni symbol wieloznaczny ("\*"), aby określić, że pomocników tagów w określonym zestawie (*Microsoft.AspNetCore.Mvc.TagHelpers*) będą dostępne dla każdego pliku widoku w *widoków* katalogu lub podkatalogu.</span><span class="sxs-lookup"><span data-stu-id="23895-141">The code above uses the wildcard syntax ("\*") to specify that all Tag Helpers in the specified assembly (*Microsoft.AspNetCore.Mvc.TagHelpers*) will be available to every view file in the *Views* directory or sub-directory.</span></span> <span data-ttu-id="23895-142">Pierwszy parametr po `@addTagHelper` określa pomocników tagów, aby załadować (używamy "\*" dla pomocników tagów), a drugi parametr "Microsoft.AspNetCore.Mvc.TagHelpers" Określa zestaw zawierający pomocników tagów.</span><span class="sxs-lookup"><span data-stu-id="23895-142">The first parameter after `@addTagHelper` specifies the Tag Helpers to load (we are using "\*" for all Tag Helpers), and the second parameter "Microsoft.AspNetCore.Mvc.TagHelpers" specifies the assembly containing the Tag Helpers.</span></span> <span data-ttu-id="23895-143">*Microsoft.AspNetCore.Mvc.TagHelpers* jest zestawu dla wbudowanych pomocników tagów Core ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="23895-143">*Microsoft.AspNetCore.Mvc.TagHelpers* is the assembly for the built-in ASP.NET Core Tag Helpers.</span></span>

<span data-ttu-id="23895-144">Aby udostępnić wszystkie pomocników tagów w tym projekcie (co powoduje zestawu o nazwie *AuthoringTagHelpers*), należy użyć następujących:</span><span class="sxs-lookup"><span data-stu-id="23895-144">To expose all of the Tag Helpers in this project (which creates an assembly named *AuthoringTagHelpers*), you would use the following:</span></span>

[!code-cshtml[Main](../../../mvc/views/tag-helpers/authoring/sample/AuthoringTagHelpers/src/AuthoringTagHelpers/Views/_ViewImportsCopy.cshtml?highlight=3)]

<span data-ttu-id="23895-145">Jeśli projekt zawiera `EmailTagHelper` z domyślnej przestrzeni nazw (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), można podać w pełni kwalifikowana nazwa (FQN) pomocnika tagów:</span><span class="sxs-lookup"><span data-stu-id="23895-145">If your project contains an `EmailTagHelper` with the default namespace (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), you can provide the fully qualified name (FQN) of the Tag Helper:</span></span>

```cshtml
@using AuthoringTagHelpers
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.EmailTagHelper, AuthoringTagHelpers
```

<span data-ttu-id="23895-146">Aby dodać pomocnika tagów do widoku, używając FQN, należy najpierw dodać FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), a następnie nazwy zestawu (*AuthoringTagHelpers*).</span><span class="sxs-lookup"><span data-stu-id="23895-146">To add a Tag Helper to a view using an FQN, you first add the FQN (`AuthoringTagHelpers.TagHelpers.EmailTagHelper`), and then the assembly name (*AuthoringTagHelpers*).</span></span> <span data-ttu-id="23895-147">Większość deweloperów wolą używać "\*" znaków wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="23895-147">Most developers prefer to use the  "\*" wildcard syntax.</span></span> <span data-ttu-id="23895-148">Składnia symbol wieloznaczny umożliwia Wstaw symbol wieloznaczny "\*" jako sufiks w FQN.</span><span class="sxs-lookup"><span data-stu-id="23895-148">The wildcard syntax allows you to insert the wildcard character "\*" as the suffix in an FQN.</span></span> <span data-ttu-id="23895-149">Na przykład następujące dyrektywy zostanie wyświetlone `EmailTagHelper`:</span><span class="sxs-lookup"><span data-stu-id="23895-149">For example, any of the following directives will bring in the `EmailTagHelper`:</span></span>

```cshtml
@addTagHelper AuthoringTagHelpers.TagHelpers.E*, AuthoringTagHelpers
@addTagHelper AuthoringTagHelpers.TagHelpers.Email*, AuthoringTagHelpers
```

<span data-ttu-id="23895-150">Jak wspomniano wcześniej, dodawanie `@addTagHelper` dyrektywy do *Views/_ViewImports.cshtml* pliku udostępnia pomocnika tagów do wszystkich plików widoku w *widoków* katalogu i podkatalogów.</span><span class="sxs-lookup"><span data-stu-id="23895-150">As mentioned previously, adding the `@addTagHelper` directive to the *Views/_ViewImports.cshtml* file makes the Tag Helper available to all view files in the *Views* directory and sub-directories.</span></span> <span data-ttu-id="23895-151">Można użyć `@addTagHelper` dyrektywy w plikach określony widok, aby wyrazić zgodę na udostępnianie pomocnika tagów tylko tych widoków.</span><span class="sxs-lookup"><span data-stu-id="23895-151">You can use the `@addTagHelper` directive in specific view files if you want to opt-in to exposing the Tag Helper to only those views.</span></span>

<a name="remove-razor-directives-label"></a>

### <a name="removetaghelper-removes-tag-helpers"></a><span data-ttu-id="23895-152">`@removeTagHelper`Usuwa pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-152">`@removeTagHelper` removes Tag Helpers</span></span>

<span data-ttu-id="23895-153">`@removeTagHelper` Ma takie same parametry dwóch jako `@addTagHelper`, i usuwa pomocnika Tag, które zostały wcześniej dodane.</span><span class="sxs-lookup"><span data-stu-id="23895-153">The `@removeTagHelper` has the same two parameters as `@addTagHelper`, and it removes a Tag Helper that was previously added.</span></span> <span data-ttu-id="23895-154">Na przykład `@removeTagHelper` stosowane do określonego widoku powoduje usunięcie określonego pomocnika tagów z widoku.</span><span class="sxs-lookup"><span data-stu-id="23895-154">For example, `@removeTagHelper` applied to a specific view removes the specified Tag Helper from the view.</span></span> <span data-ttu-id="23895-155">Przy użyciu `@removeTagHelper` w *Views/Folder/_ViewImports.cshtml* pliku usuwa określonego pomocnika Tag ze wszystkich widoków *folderu*.</span><span class="sxs-lookup"><span data-stu-id="23895-155">Using `@removeTagHelper` in a *Views/Folder/_ViewImports.cshtml* file removes the specified Tag Helper from all of the views in *Folder*.</span></span>

### <a name="controlling-tag-helper-scope-with-the-viewimportscshtml-file"></a><span data-ttu-id="23895-156">Kontrolowanie zakresu pomocnika tagów z *_ViewImports.cshtml* pliku</span><span class="sxs-lookup"><span data-stu-id="23895-156">Controlling Tag Helper scope with the *_ViewImports.cshtml* file</span></span>

<span data-ttu-id="23895-157">Możesz dodać *_ViewImports.cshtml* do dowolnego folderu widoku oraz widoku aparat stosuje dyrektywy z obu tego pliku i *Views/_ViewImports.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="23895-157">You can add a *_ViewImports.cshtml* to any view folder, and the view engine applies the directives from both that file and the *Views/_ViewImports.cshtml* file.</span></span> <span data-ttu-id="23895-158">Jeśli dodano pustą *Views/Home/_ViewImports.cshtml* plik *Home* widoków, nie może istnieć bez zmian, ponieważ *_ViewImports.cshtml* plik jest dodatek.</span><span class="sxs-lookup"><span data-stu-id="23895-158">If you added an empty *Views/Home/_ViewImports.cshtml* file for the *Home* views, there would be no change because the *_ViewImports.cshtml* file is additive.</span></span> <span data-ttu-id="23895-159">Wszelkie `@addTagHelper` dyrektywy dodać do *Views/Home/_ViewImports.cshtml* pliku (które nie są w domyślnym *Views/_ViewImports.cshtml* pliku) wystawi tych pomocników tagów do widoków tylko w *Home* folderu.</span><span class="sxs-lookup"><span data-stu-id="23895-159">Any `@addTagHelper` directives you add to the *Views/Home/_ViewImports.cshtml* file (that are not in the default *Views/_ViewImports.cshtml* file) would expose those Tag Helpers to views only in the *Home* folder.</span></span>

<a name="opt-out"></a>

### <a name="opting-out-of-individual-elements"></a><span data-ttu-id="23895-160">Rezygnacja z poszczególne elementy</span><span class="sxs-lookup"><span data-stu-id="23895-160">Opting out of individual elements</span></span>

<span data-ttu-id="23895-161">Możesz wyłączyć pomocnika tagów znakiem Wypisz pomocnika tagów na poziomie elementu ("!").</span><span class="sxs-lookup"><span data-stu-id="23895-161">You can disable a Tag Helper at the element level with the Tag Helper opt-out character ("!").</span></span> <span data-ttu-id="23895-162">Na przykład `Email` Weryfikacja jest wyłączona w `<span>` znakiem Wypisz pomocnika tagów:</span><span class="sxs-lookup"><span data-stu-id="23895-162">For example, `Email` validation is disabled in the `<span>` with the Tag Helper opt-out character:</span></span>

```cshtml
<!span asp-validation-for="Email" class="text-danger"></!span>
```

<span data-ttu-id="23895-163">Należy zastosować znak Wypisz pomocnika tagów do otwarcia i zamknięcia tagu.</span><span class="sxs-lookup"><span data-stu-id="23895-163">You must apply the Tag Helper opt-out character to the opening and closing tag.</span></span> <span data-ttu-id="23895-164">(Edytorze programu Visual Studio automatycznie dodaje znak rezygnacji tag zamykający podczas dodawania do tagu otwierającego).</span><span class="sxs-lookup"><span data-stu-id="23895-164">(The Visual Studio editor automatically adds the opt-out character to the closing tag when you add one to the opening tag).</span></span> <span data-ttu-id="23895-165">Po dodaniu znak rezygnacji z elementem i atrybuty pomocnika tagów nie są już wyświetlani charakterystyczne czcionki.</span><span class="sxs-lookup"><span data-stu-id="23895-165">After you add the opt-out character, the element and Tag Helper attributes are no longer displayed in a distinctive font.</span></span>

<a name="prefix-razor-directives-label"></a>

### <a name="using-taghelperprefix-to-make-tag-helper-usage-explicit"></a><span data-ttu-id="23895-166">Przy użyciu `@tagHelperPrefix` dokonanie jawnego użycia Pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="23895-166">Using `@tagHelperPrefix` to make Tag Helper usage explicit</span></span>

<span data-ttu-id="23895-167">`@tagHelperPrefix` Dyrektywy pozwala na określenie Ciąg prefiksu tagu, aby włączyć obsługę pomocnika tagów i użycia Pomocnika tagów jawnego.</span><span class="sxs-lookup"><span data-stu-id="23895-167">The `@tagHelperPrefix` directive allows you to specify a tag prefix string to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> <span data-ttu-id="23895-168">Na przykład można dodać następujących znaczników *Views/_ViewImports.cshtml* pliku:</span><span class="sxs-lookup"><span data-stu-id="23895-168">For example, you could add the following markup to the *Views/_ViewImports.cshtml* file:</span></span>

```cshtml
@tagHelperPrefix th:
```
<span data-ttu-id="23895-169">Na poniższej ilustracji kodu ustawiono prefiks tagu Pomocnika `th:`, dlatego tylko tych elementów przy użyciu prefiksu `th:` obsługuje pomocników tagów (włączone pomocnika tagów elementy mają charakterystyczne czcionki).</span><span class="sxs-lookup"><span data-stu-id="23895-169">In the code image below, the Tag Helper prefix is set to `th:`, so only those elements using the prefix `th:` support Tag Helpers (Tag Helper-enabled elements have a distinctive font).</span></span> <span data-ttu-id="23895-170">`<label>` i `<input>` elementy mają prefiks tagu pomocnika i obsługują pomocnika tagów, podczas `<span>` nie ma elementu.</span><span class="sxs-lookup"><span data-stu-id="23895-170">The `<label>` and `<input>` elements have the Tag Helper prefix and are Tag Helper-enabled, while the `<span>` element does not.</span></span>

![obraz](intro/_static/thp.png)

<span data-ttu-id="23895-172">Tym samym zasady hierarchii, które dotyczą `@addTagHelper` dotyczą również `@tagHelperPrefix`.</span><span class="sxs-lookup"><span data-stu-id="23895-172">The same hierarchy rules that apply to `@addTagHelper` also apply to `@tagHelperPrefix`.</span></span>

## <a name="intellisense-support-for-tag-helpers"></a><span data-ttu-id="23895-173">Obsługę funkcji IntelliSense dla pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-173">IntelliSense support for Tag Helpers</span></span>

<span data-ttu-id="23895-174">Podczas tworzenia nowej aplikacji sieci web ASP.NET w programie Visual Studio, dodaje pakiet NuGet "Microsoft.AspNetCore.Razor.Tools".</span><span class="sxs-lookup"><span data-stu-id="23895-174">When you create a new ASP.NET web app in Visual Studio, it adds the NuGet package "Microsoft.AspNetCore.Razor.Tools".</span></span> <span data-ttu-id="23895-175">To jest pakiet, który dodaje narzędzia pomocnika tagów.</span><span class="sxs-lookup"><span data-stu-id="23895-175">This is the package that adds Tag Helper tooling.</span></span>

<span data-ttu-id="23895-176">Należy wziąć pod uwagę pisania kodu HTML `<label>` elementu.</span><span class="sxs-lookup"><span data-stu-id="23895-176">Consider writing an HTML `<label>` element.</span></span> <span data-ttu-id="23895-177">Jak wprowadzasz `<l` w edytorze programu Visual Studio, IntelliSense wyświetla zgodnych elementów:</span><span class="sxs-lookup"><span data-stu-id="23895-177">As soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![obraz](intro/_static/label.png)

<span data-ttu-id="23895-179">Nie tylko możesz uzyskasz pomocy HTML, ale ikony ("@" symbol with "<>" poniżej).</span><span class="sxs-lookup"><span data-stu-id="23895-179">Not only do you get HTML help, but the icon (the "@" symbol with "<>" under it).</span></span>

![obraz](intro/_static/tagSym.png)

<span data-ttu-id="23895-181">identyfikuje element zgodnie z celem pomocników tagów.</span><span class="sxs-lookup"><span data-stu-id="23895-181">identifies the element as targeted by Tag Helpers.</span></span> <span data-ttu-id="23895-182">Czysty elementów HTML (takie jak `fieldset`) wyświetlana ikona "<>".</span><span class="sxs-lookup"><span data-stu-id="23895-182">Pure HTML elements (such as the `fieldset`) display the "<>" icon.</span></span>

<span data-ttu-id="23895-183">Czystym kodem HTML `<label>` tagów wyświetla tagu HTML (za pomocą domyślnego motywu kolorów Visual Studio) czcionką brązowy atrybutów na czerwono, i atrybutu wartości w kolorze niebieskim.</span><span class="sxs-lookup"><span data-stu-id="23895-183">A pure HTML `<label>` tag displays the HTML tag (with the default Visual Studio color theme) in a brown font, the attributes in red, and the attribute values in blue.</span></span>

![obraz](intro/_static/LableHtmlTag.png)

<span data-ttu-id="23895-185">Po wprowadzeniu `<label`, IntelliSense wyświetla dostępne atrybuty HTML/CSS oraz atrybutów docelowe pomocnika tagów:</span><span class="sxs-lookup"><span data-stu-id="23895-185">After you enter `<label`, IntelliSense lists the available HTML/CSS attributes and the Tag Helper-targeted attributes:</span></span>

![obraz](intro/_static/labelattr.png)

<span data-ttu-id="23895-187">Instrukcji IntelliSense pozwala na wprowadzenie klawisz tab, aby wykonać instrukcję, określając wybraną wartość:</span><span class="sxs-lookup"><span data-stu-id="23895-187">IntelliSense statement completion allows you to enter the tab key to complete the statement with the selected value:</span></span>

![obraz](intro/_static/stmtcomplete.png)

<span data-ttu-id="23895-189">Zaraz po wprowadzeniu atrybut pomocnika tagów zmiana czcionki tagów i atrybutów.</span><span class="sxs-lookup"><span data-stu-id="23895-189">As soon as a Tag Helper attribute is entered, the tag and attribute fonts change.</span></span> <span data-ttu-id="23895-190">Przy użyciu domyślnej programu Visual Studio "Blue" lub "Jasny" Kolor motywu, czcionka jest pogrubiona purpurowy.</span><span class="sxs-lookup"><span data-stu-id="23895-190">Using the default Visual Studio "Blue" or "Light" color theme, the font is bold purple.</span></span> <span data-ttu-id="23895-191">Jeśli używasz motywu "Ciemny" czcionka jest pogrubiona jest.</span><span class="sxs-lookup"><span data-stu-id="23895-191">If you're using the "Dark" theme the font is bold teal.</span></span> <span data-ttu-id="23895-192">Obrazy w tym dokumencie zostały pobrane przy użyciu domyślnego motywu.</span><span class="sxs-lookup"><span data-stu-id="23895-192">The images in this document were taken using the default theme.</span></span>

![obraz](intro/_static/labelaspfor2.png)

<span data-ttu-id="23895-194">Visual Studio można wprowadzić *CompleteWord* skrótów (Ctrl + spacja jest [domyślne](https://docs.microsoft.com/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) wewnątrz podwójnych cudzysłowów (""), i wszystko jest teraz w języku C#, tak jak będzie w klasie C#.</span><span class="sxs-lookup"><span data-stu-id="23895-194">You can enter the Visual Studio *CompleteWord* shortcut (Ctrl +spacebar is the [default](https://docs.microsoft.com/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio) inside the double quotes (""), and you are now in C#, just like you would be in a C# class.</span></span> <span data-ttu-id="23895-195">IntelliSense wyświetla wszystkie metody i właściwości w modelu strony.</span><span class="sxs-lookup"><span data-stu-id="23895-195">IntelliSense displays all the methods and properties on the page model.</span></span> <span data-ttu-id="23895-196">Metody i właściwości są dostępne, ponieważ typ właściwości jest `ModelExpression`.</span><span class="sxs-lookup"><span data-stu-id="23895-196">The methods and properties are available because the property type is `ModelExpression`.</span></span> <span data-ttu-id="23895-197">Na poniższej ilustracji, 'M I edytowanie `Register` widoku, więc `RegisterViewModel` jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="23895-197">In the image below, I'm editing the `Register` view, so the `RegisterViewModel` is available.</span></span>

![obraz](intro/_static/intellemail.png)

<span data-ttu-id="23895-199">Funkcja IntelliSense wyświetla listę właściwości i metod modelu na stronie.</span><span class="sxs-lookup"><span data-stu-id="23895-199">IntelliSense lists the properties and methods available to the model on the page.</span></span> <span data-ttu-id="23895-200">Bogate środowisko funkcji IntelliSense pomaga wybrać klasę CSS:</span><span class="sxs-lookup"><span data-stu-id="23895-200">The rich IntelliSense environment helps you select the CSS class:</span></span>

![obraz](intro/_static/iclass.png)

![obraz](intro/_static/intel3.png)

## <a name="tag-helpers-compared-to-html-helpers"></a><span data-ttu-id="23895-203">W porównaniu do pomocników HTML pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-203">Tag Helpers compared to HTML Helpers</span></span>

<span data-ttu-id="23895-204">Dołącz pomocników tagów do elementów HTML w widokach Razor podczas [pomocników HTML](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) są wywoływane jako metody oraz HTML w widoku Razor.</span><span class="sxs-lookup"><span data-stu-id="23895-204">Tag Helpers attach to HTML elements in Razor views, while [HTML Helpers](http://stephenwalther.com/archive/2009/03/03/chapter-6-understanding-html-helpers) are invoked as methods interspersed with HTML in Razor views.</span></span> <span data-ttu-id="23895-205">Należy wziąć pod uwagę następujące znaczników Razor, który tworzy element label kodu HTML z klasy CSS "podpis":</span><span class="sxs-lookup"><span data-stu-id="23895-205">Consider the following Razor markup, which creates an HTML label with the CSS class "caption":</span></span>

```cshtml
@Html.Label("FirstName", "First Name:", new {@class="caption"})
```

<span data-ttu-id="23895-206">W (`@`) informuje symbolu Razor jest to początek kodu.</span><span class="sxs-lookup"><span data-stu-id="23895-206">The at (`@`) symbol tells Razor this is the start of code.</span></span> <span data-ttu-id="23895-207">Następne dwa parametry ("Imię" i "imię:") są ciągami, więc [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) nie może pomóc.</span><span class="sxs-lookup"><span data-stu-id="23895-207">The next two parameters ("FirstName" and "First Name:") are strings, so [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) can't help.</span></span> <span data-ttu-id="23895-208">Ostatni argument:</span><span class="sxs-lookup"><span data-stu-id="23895-208">The last argument:</span></span>

```cshtml
new {@class="caption"}
```

<span data-ttu-id="23895-209">Obiektu anonimowego jest używana do reprezentowania atrybutów.</span><span class="sxs-lookup"><span data-stu-id="23895-209">Is an anonymous object used to represent attributes.</span></span> <span data-ttu-id="23895-210">Ponieważ **klasy** jest zarezerwowanym słowem kluczowym języka C#, użyj `@` symbolu, aby wymusić C#, aby zinterpretować "@class=" jako symbolu (nazwa właściwości).</span><span class="sxs-lookup"><span data-stu-id="23895-210">Because **class** is a reserved keyword in C#, you use the `@` symbol to force C# to interpret "@class=" as a symbol (property name).</span></span> <span data-ttu-id="23895-211">Do projektanta frontonu (ktoś zapoznać się z kodu HTML/CSS/JavaScript i innych technologii klienta, ale nie znasz języka C# i Razor), większość wiersza jest obca.</span><span class="sxs-lookup"><span data-stu-id="23895-211">To a front-end designer (someone familiar with HTML/CSS/JavaScript and other client technologies but not familiar with C# and Razor), most of the line is foreign.</span></span> <span data-ttu-id="23895-212">Cały wiersz musi być utworzony za pomocą pomoc od IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="23895-212">The entire line must be authored with no help from IntelliSense.</span></span>

<span data-ttu-id="23895-213">Przy użyciu `LabelTagHelper`, można zapisać znacznika tej samej:</span><span class="sxs-lookup"><span data-stu-id="23895-213">Using the `LabelTagHelper`, the same markup can be written as:</span></span>

![obraz](intro/_static/label2.png)

<span data-ttu-id="23895-215">Z wersją pomocnika tagów, jak wprowadzasz `<l` w edytorze programu Visual Studio, IntelliSense wyświetla zgodnych elementów:</span><span class="sxs-lookup"><span data-stu-id="23895-215">With the Tag Helper version, as soon as you enter `<l` in the Visual Studio editor, IntelliSense displays matching elements:</span></span>

![obraz](intro/_static/label.png)

<span data-ttu-id="23895-217">IntelliSense ułatwia pisanie cały wiersz.</span><span class="sxs-lookup"><span data-stu-id="23895-217">IntelliSense helps you write the entire line.</span></span> <span data-ttu-id="23895-218">`LabelTagHelper` Domyślnie ustawienie zawartość `asp-for` atrybutu "Imię"; wartość ("imię") Konwertuje liter formatu właściwości do zdania składa się z nazwy właściwości z miejsca, w którym występuje każdego nowego wielką literą.</span><span class="sxs-lookup"><span data-stu-id="23895-218">The `LabelTagHelper` also defaults to setting the content of the `asp-for` attribute value ("FirstName") to "First Name"; It converts camel-cased properties to a sentence composed of the property name with a space where each new upper-case letter occurs.</span></span> <span data-ttu-id="23895-219">W znaczniku następujące:</span><span class="sxs-lookup"><span data-stu-id="23895-219">In the following markup:</span></span>

![obraz](intro/_static/label2.png)

<span data-ttu-id="23895-221">generuje:</span><span class="sxs-lookup"><span data-stu-id="23895-221">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">First Name</label>
```

<span data-ttu-id="23895-222">Formatu — z uwzględnieniem wielkości liter liter zdanie zawartości nie jest używany, jeśli Dodawanie zawartości do `<label>`.</span><span class="sxs-lookup"><span data-stu-id="23895-222">The camel-cased to sentence-cased content is not used if you add content to the `<label>`.</span></span> <span data-ttu-id="23895-223">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="23895-223">For example:</span></span>

![obraz](intro/_static/1stName.png)

<span data-ttu-id="23895-225">generuje:</span><span class="sxs-lookup"><span data-stu-id="23895-225">generates:</span></span>

```cshtml
<label class="caption" for="FirstName">Name First</label>
```

<span data-ttu-id="23895-226">Na poniższej ilustracji kodu przedstawiono formularz część *Views/Account/Register.cshtml* widoku Razor wygenerowane z szablonu MVC starszych 4.5.x ASP.NET uwzględnionych w programie Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="23895-226">The following code image shows the Form portion of the *Views/Account/Register.cshtml* Razor view generated from the legacy ASP.NET 4.5.x MVC template included with Visual Studio 2015.</span></span>

![obraz](intro/_static/regCS.png)

<span data-ttu-id="23895-228">Edytor programu Visual Studio Wyświetla kodu C# za pomocą szare tła.</span><span class="sxs-lookup"><span data-stu-id="23895-228">The Visual Studio editor displays C# code with a grey background.</span></span> <span data-ttu-id="23895-229">Na przykład `AntiForgeryToken` pomocnika kodu HTML:</span><span class="sxs-lookup"><span data-stu-id="23895-229">For example, the `AntiForgeryToken` HTML Helper:</span></span>

```cshtml
@Html.AntiForgeryToken()
```

<span data-ttu-id="23895-230">zostanie wyświetlony z szare tła.</span><span class="sxs-lookup"><span data-stu-id="23895-230">is displayed with a grey background.</span></span> <span data-ttu-id="23895-231">Większość znaczników w widoku rejestru jest C#.</span><span class="sxs-lookup"><span data-stu-id="23895-231">Most of the markup in the Register view is C#.</span></span> <span data-ttu-id="23895-232">Porównać równoważne podejścia, przy użyciu pomocników tagów:</span><span class="sxs-lookup"><span data-stu-id="23895-232">Compare that to the equivalent approach using Tag Helpers:</span></span>

![obraz](intro/_static/regTH.png)

<span data-ttu-id="23895-234">Kod znaczników jest znacznie bardziej przejrzysty i łatwiejsze do odczytu, edytowanie i obsługa niż metody pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-234">The markup is much cleaner and easier to read, edit, and maintain than the HTML Helpers approach.</span></span> <span data-ttu-id="23895-235">Kod C# jest ograniczone do minimum, który serwer musi znać.</span><span class="sxs-lookup"><span data-stu-id="23895-235">The C# code is reduced to the minimum that the server needs to know about.</span></span> <span data-ttu-id="23895-236">W edytorze programu Visual Studio są wyświetlane znaczników objęci pomocnika tagów charakterystyczne czcionki.</span><span class="sxs-lookup"><span data-stu-id="23895-236">The Visual Studio editor displays markup targeted by a Tag Helper in a distinctive font.</span></span>

<span data-ttu-id="23895-237">Należy wziąć pod uwagę *E-mail* grupy:</span><span class="sxs-lookup"><span data-stu-id="23895-237">Consider the *Email* group:</span></span>

[!code-csharp[Main](intro/sample/Register.cshtml?range=12-18)]

<span data-ttu-id="23895-238">Każdego z atrybutów "asp —" ma wartość "E-mail", ale "E-mail" nie jest ciągiem.</span><span class="sxs-lookup"><span data-stu-id="23895-238">Each of the "asp-" attributes has a value of "Email", but "Email" is not a string.</span></span> <span data-ttu-id="23895-239">W tym kontekście "E-mail" jest C# wyrażenie właściwości modelu dla `RegisterViewModel`.</span><span class="sxs-lookup"><span data-stu-id="23895-239">In this context, "Email" is the C# model expression property for the `RegisterViewModel`.</span></span>

<span data-ttu-id="23895-240">Edytor programu Visual Studio ułatwia pisanie **wszystkie** z kodu znaczników w ujęciu pomocnika Tag formularza rejestru, podczas gdy program Visual Studio udostępnia pomoc dla większości kodu w ujęciu pomocników HTML.</span><span class="sxs-lookup"><span data-stu-id="23895-240">The Visual Studio editor helps you write **all** of the markup in the Tag Helper approach of the register form, while Visual Studio provides no help for most of the code in the HTML Helpers approach.</span></span> <span data-ttu-id="23895-241">[Obsługę funkcji IntelliSense dla pomocników tagów](#intellisense-support-for-tag-helpers) przechodzi do szczegółów na temat pracy z pomocników tagów w edytorze programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23895-241">[IntelliSense support for Tag Helpers](#intellisense-support-for-tag-helpers) goes into detail on working with Tag Helpers in the Visual Studio editor.</span></span>

## <a name="tag-helpers-compared-to-web-server-controls"></a><span data-ttu-id="23895-242">Pomocników tagów w porównaniu do kontrolki serwera sieci Web</span><span class="sxs-lookup"><span data-stu-id="23895-242">Tag Helpers compared to Web Server Controls</span></span>

* <span data-ttu-id="23895-243">Pomocników tagów nie należy do użytkownika element, do którego są one związane z; po prostu uczestniczą w czasie renderowania elementów i zawartości.</span><span class="sxs-lookup"><span data-stu-id="23895-243">Tag Helpers don't own the element they're associated with; they simply participate in the rendering of the element and content.</span></span> <span data-ttu-id="23895-244">ASP.NET [kontrolki serwera sieci Web](https://msdn.microsoft.com/library/7698y1f0.aspx) zadeklarowany i wywoływane na stronie.</span><span class="sxs-lookup"><span data-stu-id="23895-244">ASP.NET [Web Server controls](https://msdn.microsoft.com/library/7698y1f0.aspx) are declared and invoked on a page.</span></span>

* <span data-ttu-id="23895-245">[Formanty serwera sieci Web](https://msdn.microsoft.com/library/zsyt68f1.aspx) mają cykl nieuproszczony może utrudnić opracowywania i debugowania.</span><span class="sxs-lookup"><span data-stu-id="23895-245">[Web Server controls](https://msdn.microsoft.com/library/zsyt68f1.aspx) have a non-trivial lifecycle that can make developing and debugging difficult.</span></span>

* <span data-ttu-id="23895-246">Formanty serwera sieci Web umożliwiają dodawanie funkcji do elementów modelu DOM (Document Object) klienta za pomocą formantu klienta.</span><span class="sxs-lookup"><span data-stu-id="23895-246">Web Server controls allow you to add functionality to the client Document Object Model (DOM) elements by using a client control.</span></span> <span data-ttu-id="23895-247">Pomocników tagów nie ma żadnych modelu DOM.</span><span class="sxs-lookup"><span data-stu-id="23895-247">Tag Helpers have no DOM.</span></span>

* <span data-ttu-id="23895-248">Formanty serwera sieci Web obejmują wykrywanie automatyczne przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="23895-248">Web Server controls include automatic browser detection.</span></span> <span data-ttu-id="23895-249">Pomocników tagów nie korzystają z nie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="23895-249">Tag Helpers have no knowledge of the browser.</span></span>

* <span data-ttu-id="23895-250">Wiele pomocników tagów może działać na tym samym elemencie (zobacz [pomocnika tagów unikanie konfliktów](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/authoring#avoiding-tag-helper-conflicts) ) podczas zwykle nie można utworzyć kontrolki serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="23895-250">Multiple Tag Helpers can act on the same element (see [Avoiding Tag Helper conflicts](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/authoring#avoiding-tag-helper-conflicts) ) while you typically can't compose Web Server controls.</span></span>

* <span data-ttu-id="23895-251">Pomocników tagów można tagu i zawartość elementów HTML, które jest zakresem, ale nie bezpośrednio modyfikować dowolne inne na stronie.</span><span class="sxs-lookup"><span data-stu-id="23895-251">Tag Helpers can modify the tag and content of HTML elements that they're scoped to, but don't directly modify anything else on a page.</span></span> <span data-ttu-id="23895-252">Formanty serwera sieci Web mają szerszym zakresie i mogą wykonywać akcje, które mają wpływ na inne części strony; Włączanie niezamierzone skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="23895-252">Web Server controls have a less specific scope and can perform actions that affect other parts of your page; enabling unintended side effects.</span></span>

* <span data-ttu-id="23895-253">Formanty serwera sieci Web umożliwia konwertowanie ciągów na obiekty konwertery typu.</span><span class="sxs-lookup"><span data-stu-id="23895-253">Web Server controls use type converters to convert strings into objects.</span></span> <span data-ttu-id="23895-254">Z pomocników tagów pracy natywnie w języku C#, dzięki czemu nie trzeba konwersja typu.</span><span class="sxs-lookup"><span data-stu-id="23895-254">With Tag Helpers, you work natively in C#, so you don't need to do type conversion.</span></span>

* <span data-ttu-id="23895-255">Serwer sieci Web steruje użyciem [System.ComponentModel](https://docs.microsoft.com/dotnet/api/system.componentmodel) do zaimplementowania zachowania czasu wykonywania i czasu projektowania, składników i kontrolek.</span><span class="sxs-lookup"><span data-stu-id="23895-255">Web Server controls use [System.ComponentModel](https://docs.microsoft.com/dotnet/api/system.componentmodel) to implement the run-time and design-time behavior of components and controls.</span></span> <span data-ttu-id="23895-256">`System.ComponentModel`zawiera klasy podstawowe i interfejsy dla wykonania atrybutów i typy konwerterów, powiązanie z danymi źródeł i licencjonowania składników.</span><span class="sxs-lookup"><span data-stu-id="23895-256">`System.ComponentModel` includes the base classes and interfaces for implementing attributes and type converters, binding to data sources, and licensing components.</span></span> <span data-ttu-id="23895-257">Natomiast który do pomocników tagów, które zwykle pochodzi od `TagHelper`i `TagHelper` klasy podstawowej przedstawia tylko dwie metody `Process` i `ProcessAsync`.</span><span class="sxs-lookup"><span data-stu-id="23895-257">Contrast that to Tag Helpers, which typically derive from `TagHelper`, and the `TagHelper` base class exposes only two methods, `Process` and `ProcessAsync`.</span></span>

## <a name="customizing-the-tag-helper-element-font"></a><span data-ttu-id="23895-258">Dostosowywanie czcionki element pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="23895-258">Customizing the Tag Helper element font</span></span>

<span data-ttu-id="23895-259">Możesz dostosować czcionki i kolorowania z **narzędzia** > **opcje** > **środowiska** > **czcionek Kolory i**:</span><span class="sxs-lookup"><span data-stu-id="23895-259">You can customize the font and colorization from **Tools** > **Options** > **Environment** > **Fonts and Colors**:</span></span>

![obraz](intro/_static/fontoptions2.png)

## <a name="additional-resources"></a><span data-ttu-id="23895-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="23895-261">Additional Resources</span></span>

* [<span data-ttu-id="23895-262">Tworzenie pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="23895-262">Authoring Tag Helpers</span></span>](authoring.md)
* [<span data-ttu-id="23895-263">Praca z formularzy</span><span class="sxs-lookup"><span data-stu-id="23895-263">Working with Forms </span></span>](../working-with-forms.md)
* <span data-ttu-id="23895-264">[TagHelperSamples w serwisie GitHub](https://github.com/dpaquette/TagHelperSamples) zawiera przykłady pomocnika tagów do pracy z [Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="23895-264">[TagHelperSamples on GitHub](https://github.com/dpaquette/TagHelperSamples) contains Tag Helper samples for working with [Bootstrap](http://getbootstrap.com/).</span></span>

<!--
* [Working with Forms ](xref:mvc/views/working-with-forms)
-->