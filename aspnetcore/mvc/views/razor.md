---
title: "Odwołania do składni razor dla platformy ASP.NET Core"
author: rick-anderson
description: "Więcej informacji o składni Razor znaczników do osadzania kodu na serwerze do stron sieci Web."
ms.author: riande
manager: wpickett
ms.date: 10/18/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/razor
ms.openlocfilehash: abdbb8112533d42f81180abad52f5ee86e3b280f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="razor-syntax-for-aspnet-core"></a><span data-ttu-id="89c51-103">Składnia razor dla platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="89c51-103">Razor syntax for ASP.NET Core</span></span>

<span data-ttu-id="89c51-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [MULLENA Taylora](https://twitter.com/ntaylormullen), i [Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="89c51-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="89c51-105">Razor jest składnię znaczników osadzanie kodu na serwerze w witrynach sieci Web.</span><span class="sxs-lookup"><span data-stu-id="89c51-105">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="89c51-106">Składnia Razor składa się z Razor znaczników, C# i HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-106">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="89c51-107">Pliki zawierające Razor zazwyczaj mają *.cshtml* rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="89c51-107">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="89c51-108">Renderowanie kodu HTML</span><span class="sxs-lookup"><span data-stu-id="89c51-108">Rendering HTML</span></span>

<span data-ttu-id="89c51-109">Domyślny język Razor jest HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-109">The default Razor language is HTML.</span></span> <span data-ttu-id="89c51-110">Renderowanie kodu HTML, z znaczników Razor nie różni się od renderowania kodu HTML z pliku HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-110">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span> <span data-ttu-id="89c51-111">Kod znaczników HTML w *.cshtml* pliki Razor jest renderowany na serwerze bez zmian.</span><span class="sxs-lookup"><span data-stu-id="89c51-111">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="89c51-112">Składnia razor</span><span class="sxs-lookup"><span data-stu-id="89c51-112">Razor syntax</span></span>

<span data-ttu-id="89c51-113">Razor obsługuje C# i używa `@` symbol przejście z kodu HTML dla C#.</span><span class="sxs-lookup"><span data-stu-id="89c51-113">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="89c51-114">Razor ocenia wyrażeń C# i renderuje je w danych wyjściowych HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-114">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="89c51-115">Gdy `@` następuje symbol [Razor zastrzeżone słowa kluczowego](#razor-reserved-keywords), jego przejścia do znaczników specyficzne dla elementu Razor.</span><span class="sxs-lookup"><span data-stu-id="89c51-115">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="89c51-116">W przeciwnym wypadku przejścia do zwykłego C#.</span><span class="sxs-lookup"><span data-stu-id="89c51-116">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="89c51-117">Wyjścia `@` symboli w znaczniku Razor, należy użyć drugiej `@` symboli:</span><span class="sxs-lookup"><span data-stu-id="89c51-117">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="89c51-118">Renderowanie kodu HTML za pomocą jednej `@` symboli:</span><span class="sxs-lookup"><span data-stu-id="89c51-118">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="89c51-119">Atrybuty HTML i zawartości zawierającego adresy e-mail nie Traktuj `@` symbol jako znak przejścia.</span><span class="sxs-lookup"><span data-stu-id="89c51-119">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="89c51-120">W poniższym przykładzie adresy e-mail są niezmienione przez Razor analizy:</span><span class="sxs-lookup"><span data-stu-id="89c51-120">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="89c51-121">Niejawne wyrażenia Razor</span><span class="sxs-lookup"><span data-stu-id="89c51-121">Implicit Razor expressions</span></span>

<span data-ttu-id="89c51-122">Niejawne wyrażenia Razor rozpoczynać `@` następuje kod w języku C#:</span><span class="sxs-lookup"><span data-stu-id="89c51-122">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="89c51-123">Z wyjątkiem C# `await` — słowo kluczowe, niejawnego wyrażenia nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="89c51-123">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="89c51-124">Jeśli wyczyść Kończenie instrukcji C#, mogą wymieszaniu spacji:</span><span class="sxs-lookup"><span data-stu-id="89c51-124">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="89c51-125">Wyrażenia niejawnego **nie** zawiera typami ogólnymi C#, jako znak wewnątrz nawiasów (`<>`) są interpretowane jako tagu HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-125">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="89c51-126">Następujący kod jest **nie** prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="89c51-126">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="89c51-127">Poprzedni kod generowany jest błąd kompilatora podobny do jednego z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="89c51-127">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="89c51-128">Element "int" nie został zamknięty.</span><span class="sxs-lookup"><span data-stu-id="89c51-128">The "int" element wasn't closed.</span></span> <span data-ttu-id="89c51-129">Wszystkie elementy muszą być albo samodzielnie zamknięcie lub ma zgodnego tagu końcowego.</span><span class="sxs-lookup"><span data-stu-id="89c51-129">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="89c51-130">Nie można przekonwertować grupy metod "GenericMethod" na typ "object" Niedelegowany.</span><span class="sxs-lookup"><span data-stu-id="89c51-130">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="89c51-131">Czy zamierzasz wywołać metodę? "</span><span class="sxs-lookup"><span data-stu-id="89c51-131">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="89c51-132">Wywołania metody rodzajowe muszą być ujęte w [jawne wyrażenie Razor](#explicit-razor-expressions) lub [blok kodu Razor](#razor-code-blocks).</span><span class="sxs-lookup"><span data-stu-id="89c51-132">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="89c51-133">Jawne wyrażenia Razor</span><span class="sxs-lookup"><span data-stu-id="89c51-133">Explicit Razor expressions</span></span>

<span data-ttu-id="89c51-134">Jawne Razor wyrażeń składają się z `@` symbol o zrównoważonym nawiasu.</span><span class="sxs-lookup"><span data-stu-id="89c51-134">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="89c51-135">Do renderowania czas ostatniego tygodnia, jest używany następujący kod Razor:</span><span class="sxs-lookup"><span data-stu-id="89c51-135">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="89c51-136">Zawartość w `@()` nawias jest obliczany i renderowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="89c51-136">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="89c51-137">Ogólnie wyrażenia niejawnego, opisane w poprzedniej sekcji, nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="89c51-137">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="89c51-138">W poniższym kodzie tydzień nie jest odejmowany od bieżącego czasu:</span><span class="sxs-lookup"><span data-stu-id="89c51-138">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="89c51-139">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-139">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="89c51-140">Jawne wyrażenia może służyć do łączenia tekstu w wyniku wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="89c51-140">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="89c51-141">Bez jawnego wyrażenia `<p>Age@joe.Age</p>` jest traktowany jak adres e-mail i `<p>Age@joe.Age</p>` jest renderowany.</span><span class="sxs-lookup"><span data-stu-id="89c51-141">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="89c51-142">Gdy zapisywane jako wyrażenie jawne `<p>Age33</p>` jest renderowany.</span><span class="sxs-lookup"><span data-stu-id="89c51-142">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>


<span data-ttu-id="89c51-143">Jawne wyrażenia może zostać użyty do renderowania dane wyjściowe metody rodzajowe w *.cshtml* plików.</span><span class="sxs-lookup"><span data-stu-id="89c51-143">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="89c51-144">W wyrażeniu niejawne znak wewnątrz nawiasów (`<>`) są interpretowane jako tagu HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-144">In an implicit expression, the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="89c51-145">Następujący kod znaczników jest **nie** Razor prawidłowy:</span><span class="sxs-lookup"><span data-stu-id="89c51-145">The following markup is **not** valid Razor:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="89c51-146">Poprzedni kod generowany jest błąd kompilatora podobny do jednego z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="89c51-146">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="89c51-147">Element "int" nie został zamknięty.</span><span class="sxs-lookup"><span data-stu-id="89c51-147">The "int" element wasn't closed.</span></span> <span data-ttu-id="89c51-148">Wszystkie elementy muszą być albo samodzielnie zamknięcie lub ma zgodnego tagu końcowego.</span><span class="sxs-lookup"><span data-stu-id="89c51-148">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="89c51-149">Nie można przekonwertować grupy metod "GenericMethod" na typ "object" Niedelegowany.</span><span class="sxs-lookup"><span data-stu-id="89c51-149">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="89c51-150">Czy zamierzasz wywołać metodę? "</span><span class="sxs-lookup"><span data-stu-id="89c51-150">Did you intend to invoke the method?\`</span></span> 
 
 <span data-ttu-id="89c51-151">Następujący kod przedstawia sposób poprawne zapisu tego kodu.</span><span class="sxs-lookup"><span data-stu-id="89c51-151">The following markup shows the correct way write this code.</span></span> <span data-ttu-id="89c51-152">Kod jest zapisywany jako jawne wyrażenie:</span><span class="sxs-lookup"><span data-stu-id="89c51-152">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="89c51-153">Kodowanie wyrażenia</span><span class="sxs-lookup"><span data-stu-id="89c51-153">Expression encoding</span></span>

<span data-ttu-id="89c51-154">Wyrażenia języka C#, określających ciąg są kodowania HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-154">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="89c51-155">C# wyrażeń określających `IHtmlContent` są renderowane za pomocą `IHtmlContent.WriteTo`.</span><span class="sxs-lookup"><span data-stu-id="89c51-155">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="89c51-156">C# wyrażeń, które nie zwrócą `IHtmlContent` jest konwertowana na ciąg przez `ToString` i kodowany przed ich są renderowane.</span><span class="sxs-lookup"><span data-stu-id="89c51-156">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="89c51-157">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-157">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="89c51-158">Kod HTML jest wyświetlany w przeglądarce jako:</span><span class="sxs-lookup"><span data-stu-id="89c51-158">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="89c51-159">`HtmlHelper.Raw`dane wyjściowe nie jest zakodowany, ale renderowany jako kod znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-159">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="89c51-160">Przy użyciu `HtmlHelper.Raw` unsanitized użytkownika dane wejściowe stanowi zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="89c51-160">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="89c51-161">Dane wejściowe użytkownika może zawierać złośliwego kodu JavaScript lub inne luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="89c51-161">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="89c51-162">Trudno jest oczyszczania danych wejściowych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89c51-162">Sanitizing user input is difficult.</span></span> <span data-ttu-id="89c51-163">Unikaj używania `HtmlHelper.Raw` z danych wejściowych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89c51-163">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="89c51-164">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-164">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="89c51-165">Bloki kodu razor</span><span class="sxs-lookup"><span data-stu-id="89c51-165">Razor code blocks</span></span>

<span data-ttu-id="89c51-166">Bloki kodu razor rozpoczynać `@` i znajdują się wewnątrz `{}`.</span><span class="sxs-lookup"><span data-stu-id="89c51-166">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="89c51-167">W przeciwieństwie do wyrażenia nie jest renderowany kodu C# wewnątrz bloków kodu.</span><span class="sxs-lookup"><span data-stu-id="89c51-167">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="89c51-168">Bloki kodu i wyrażenia w widoku o tym samym zakresie i są zdefiniowane w kolejności:</span><span class="sxs-lookup"><span data-stu-id="89c51-168">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="89c51-169">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-169">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="89c51-170">Niejawne przejścia</span><span class="sxs-lookup"><span data-stu-id="89c51-170">Implicit transitions</span></span>

<span data-ttu-id="89c51-171">Jest to domyślny język w bloku kodu C#, ale strona Razor można przejść do HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-171">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="89c51-172">Jawne przejścia rozdzielanego</span><span class="sxs-lookup"><span data-stu-id="89c51-172">Explicit delimited transition</span></span>

<span data-ttu-id="89c51-173">Aby zdefiniować podsekcji bloku kodu, które mają renderować kod HTML, Otocz znaków do renderowania elementu Razor  **\<tekst >** tagu:</span><span class="sxs-lookup"><span data-stu-id="89c51-173">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="89c51-174">Tej metody można użyć do renderowania kodu HTML, który nie jest ujęta w tagu HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-174">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="89c51-175">Bez tagu HTML lub Razor występuje błąd w czasie wykonywania Razor.</span><span class="sxs-lookup"><span data-stu-id="89c51-175">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="89c51-176">**\<Tekst >** tag jest przydatne do kontroli odstępu podczas renderowania zawartości:</span><span class="sxs-lookup"><span data-stu-id="89c51-176">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="89c51-177">Tylko zawartość między  **\<tekst >** renderowania tagu.</span><span class="sxs-lookup"><span data-stu-id="89c51-177">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="89c51-178">Nie spacji przed lub po  **\<tekst >** tag jest wyświetlany w danych wyjściowych HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-178">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="89c51-179">Jawne wiersz przejścia z @:</span><span class="sxs-lookup"><span data-stu-id="89c51-179">Explicit Line Transition with @:</span></span>

<span data-ttu-id="89c51-180">Aby renderować rest całego wiersza jako HTML w bloku kodu, należy użyć `@:` składni:</span><span class="sxs-lookup"><span data-stu-id="89c51-180">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="89c51-181">Bez `@:` w kodzie, generowany jest błąd w czasie wykonywania Razor.</span><span class="sxs-lookup"><span data-stu-id="89c51-181">Without the `@:` in the code, a Razor runtime error is generated.</span></span>

<span data-ttu-id="89c51-182">Ostrzeżenie: Dodatkowy `@` znaki w pliku Razor może spowodować błędy kompilatora Przyczyna w instrukcji w dalszej części tego bloku.</span><span class="sxs-lookup"><span data-stu-id="89c51-182">Warning: Extra `@` characters in a Razor file can cause cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="89c51-183">Te błędy kompilatora może być trudne do zrozumienia, ponieważ błędu występuje przed zgłoszonego błędu.</span><span class="sxs-lookup"><span data-stu-id="89c51-183">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span> <span data-ttu-id="89c51-184">Ten błąd jest typowe po łączenie wielu niejawnej/jawnej wyrażenia w bloku kodu pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="89c51-184">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="89c51-185">Struktury sterujące</span><span class="sxs-lookup"><span data-stu-id="89c51-185">Control Structures</span></span>

<span data-ttu-id="89c51-186">Struktury sterujące stanowią rozszerzenie bloków kodu.</span><span class="sxs-lookup"><span data-stu-id="89c51-186">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="89c51-187">Wszystkie aspekty bloki kodu (przechodzenia do znaczników, wbudowane C#) również dotyczą następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="89c51-187">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="89c51-188">Warunkowe instrukcje @if, else if, #else i@switch</span><span class="sxs-lookup"><span data-stu-id="89c51-188">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="89c51-189">`@if`Formanty po uruchomieniu kodu:</span><span class="sxs-lookup"><span data-stu-id="89c51-189">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="89c51-190">`else`i `else if` nie wymagają `@` symboli:</span><span class="sxs-lookup"><span data-stu-id="89c51-190">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="89c51-191">Następujący kod przedstawia sposób użycia instrukcji switch:</span><span class="sxs-lookup"><span data-stu-id="89c51-191">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="89c51-192">Zapętlenie @for, @foreach, @while, i @do podczas</span><span class="sxs-lookup"><span data-stu-id="89c51-192">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="89c51-193">HTML opartego na szablonie można renderować z pętli instrukcji sterowania.</span><span class="sxs-lookup"><span data-stu-id="89c51-193">Templated HTML can be rendered with looping control statements.</span></span> <span data-ttu-id="89c51-194">Do renderowania listy osób:</span><span class="sxs-lookup"><span data-stu-id="89c51-194">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="89c51-195">Obsługiwane są następujące instrukcje pętli:</span><span class="sxs-lookup"><span data-stu-id="89c51-195">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="89c51-196">Złożone@using</span><span class="sxs-lookup"><span data-stu-id="89c51-196">Compound @using</span></span>

<span data-ttu-id="89c51-197">W języku C# `using` instrukcji służy do zapewnienia obiekt jest usunięty.</span><span class="sxs-lookup"><span data-stu-id="89c51-197">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="89c51-198">W elemencie Razor ten sam mechanizm służy do tworzenia pomocników HTML, która zawiera dodatkową zawartość.</span><span class="sxs-lookup"><span data-stu-id="89c51-198">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="89c51-199">W poniższym kodzie pomocników HTML renderowania tagu form z `@using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="89c51-199">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="89c51-200">Można wykonywać działania na poziomie zakresu za pomocą [pomocników tagów](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="89c51-200">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="89c51-201">@try, catch, finally</span><span class="sxs-lookup"><span data-stu-id="89c51-201">@try, catch, finally</span></span>

<span data-ttu-id="89c51-202">Obsługa wyjątków jest podobny do języka C#:</span><span class="sxs-lookup"><span data-stu-id="89c51-202">Exception handling is similar to C#:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="89c51-203">Razor ma możliwość ochrony sekcje krytyczne w instrukcjach blokady:</span><span class="sxs-lookup"><span data-stu-id="89c51-203">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="89c51-204">Komentarze</span><span class="sxs-lookup"><span data-stu-id="89c51-204">Comments</span></span>

<span data-ttu-id="89c51-205">Razor obsługuje komentarze języka C# i HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-205">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="89c51-206">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-206">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="89c51-207">Komentarz razor są usuwane przez serwer przed wyświetleniem strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="89c51-207">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="89c51-208">Używa razor `@*  *@` ograniczającej komentarze.</span><span class="sxs-lookup"><span data-stu-id="89c51-208">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="89c51-209">Poniższy kod jest oznaczone jako komentarz, dlatego serwer nie renderowania żadnych znaczników:</span><span class="sxs-lookup"><span data-stu-id="89c51-209">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="89c51-210">Dyrektyw</span><span class="sxs-lookup"><span data-stu-id="89c51-210">Directives</span></span>

<span data-ttu-id="89c51-211">Dyrektywy razor są reprezentowane przez niejawnego wyrażenia następujące zastrzeżone słowa kluczowe `@` symbolu.</span><span class="sxs-lookup"><span data-stu-id="89c51-211">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="89c51-212">Dyrektywy zwykle zmienia sposób widok jest analizowana lub umożliwia korzystanie z różnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="89c51-212">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="89c51-213">Opis sposobu Razor generuje kod dla widoku ułatwia zrozumienie, jak działają dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="89c51-213">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-html[Main](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="89c51-214">Kod generuje klasę podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="89c51-214">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="89c51-215">Dalszej części tego artykułu, w sekcji [wyświetlanie klasy Razor C# wygenerowany dla widoku](#viewing-the-razor-c-class-generated-for-a-view) opisano sposób wyświetlania tego wygenerowanej klasy.</span><span class="sxs-lookup"><span data-stu-id="89c51-215">Later in this article, the section [Viewing the Razor C# class generated for a view](#viewing-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

### <a name="using"></a>@using

<span data-ttu-id="89c51-216">`@using` Dodaje dyrektywy języka C# `using` dyrektywy do wygenerowanego widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-216">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="89c51-217">`@model` Dyrektywa określa typ modelu przekazywane do widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-217">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="89c51-218">W aplikacji ASP.NET Core MVC utworzone za pomocą poszczególnych kont użytkowników *Views/Account/Login.cshtml* widok zawiera następujące oświadczenie modelu:</span><span class="sxs-lookup"><span data-stu-id="89c51-218">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="89c51-219">Wygenerowana klasa dziedziczy `RazorPage<dynamic>`:</span><span class="sxs-lookup"><span data-stu-id="89c51-219">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="89c51-220">Przedstawia razor `Model` właściwości do uzyskiwania dostępu do modelu przekazywane do widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-220">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="89c51-221">`@model` Dyrektywa określa typ tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="89c51-221">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="89c51-222">Określa dyrektywy `T` w `RazorPage<T>` czy wygenerowanej klasy który widok jest pochodną.</span><span class="sxs-lookup"><span data-stu-id="89c51-222">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="89c51-223">Jeśli `@model` dyrektywy jest określony, `Model` właściwość jest typu `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="89c51-223">If the `@model` directive iisn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="89c51-224">Wartość modelu jest przekazywany z kontrolera do widoku.</span><span class="sxs-lookup"><span data-stu-id="89c51-224">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="89c51-225">Aby uzyskać więcej informacji, zobacz [silnie typizowane modeli i @model — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="89c51-225">For more information, see [Strongly typed models and the @model keyword.</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="89c51-226">`@inherits` Dyrektywy umożliwia pełną kontrolę nad klasa dziedziczy widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-226">The `@inherits` directive provides full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="89c51-227">Następujący kod jest typu niestandardowego Razor strony:</span><span class="sxs-lookup"><span data-stu-id="89c51-227">The following code is a custom Razor page type:</span></span>

[!code-csharp[Main](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="89c51-228">`CustomText` Jest wyświetlany w widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-228">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="89c51-229">Kod Renderuje poniższy kod HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-229">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="89c51-230">`@model`i `@inherits` mogą być używane w jednym widoku.</span><span class="sxs-lookup"><span data-stu-id="89c51-230">`@model` and `@inherits` can be used in the same view.</span></span> <span data-ttu-id="89c51-231">`@inherits`mogą znajdować się w *_ViewImports.cshtml* pliku, który importuje widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-231">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[Main](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="89c51-232">Następujący kod jest przykładem silnie typizowanego widoku:</span><span class="sxs-lookup"><span data-stu-id="89c51-232">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="89c51-233">Jeśli "rick@contoso.com" jest przekazywany w modelu widoku generuje następujący kod znaczników HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-233">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject


<span data-ttu-id="89c51-234">`@inject` Dyrektywy umożliwia stronę Razor do dodania usługi z [kontenera usług](xref:fundamentals/dependency-injection) w widoku.</span><span class="sxs-lookup"><span data-stu-id="89c51-234">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="89c51-235">Aby uzyskać więcej informacji, zobacz [iniekcji zależności do widoków](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="89c51-235">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="89c51-236">`@functions` Dyrektywy umożliwia Razor strony do dodania do widoku zawartości na poziomie funkcji:</span><span class="sxs-lookup"><span data-stu-id="89c51-236">The `@functions` directive enables a Razor Page to add function-level content to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="89c51-237">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="89c51-237">For example:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="89c51-238">Kod generuje następujący kod znaczników HTML:</span><span class="sxs-lookup"><span data-stu-id="89c51-238">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="89c51-239">Następujący kod jest wygenerowana klasa Razor C#:</span><span class="sxs-lookup"><span data-stu-id="89c51-239">The following code is the generated Razor C# class:</span></span>

[!code-csharp[Main](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="89c51-240">`@section` Dyrektywa jest używany w połączeniu z [układu](xref:mvc/views/layout) umożliwiające widoków do renderowania zawartości w innej części strony HTML.</span><span class="sxs-lookup"><span data-stu-id="89c51-240">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="89c51-241">Aby uzyskać więcej informacji, zobacz [sekcje](xref:mvc/views/layout#layout-sections-label).</span><span class="sxs-lookup"><span data-stu-id="89c51-241">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="tag-helpers"></a><span data-ttu-id="89c51-242">Pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="89c51-242">Tag Helpers</span></span>

<span data-ttu-id="89c51-243">Istnieją trzy dyrektywy, które odnoszą się do [pomocników tagów](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="89c51-243">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="89c51-244">Dyrektywy</span><span class="sxs-lookup"><span data-stu-id="89c51-244">Directive</span></span> | <span data-ttu-id="89c51-245">Funkcja</span><span class="sxs-lookup"><span data-stu-id="89c51-245">Function</span></span> |
| --------- | -------- |
| [@addTagHelper](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="89c51-246">Udostępnia pomocników tagów do widoku.</span><span class="sxs-lookup"><span data-stu-id="89c51-246">Makes Tag Helpers available to a view.</span></span> |
| [@removeTagHelper](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="89c51-247">Usuwa pomocników tagów, które wcześniej dodano z widoku.</span><span class="sxs-lookup"><span data-stu-id="89c51-247">Removes Tag Helpers previously added from a view.</span></span> |
| [@tagHelperPrefix](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="89c51-248">Określa prefiks tagu, aby włączyć obsługę pomocnika tagów i użycia Pomocnika tagów jawnego.</span><span class="sxs-lookup"><span data-stu-id="89c51-248">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="89c51-249">Razor zastrzeżone słowa kluczowe</span><span class="sxs-lookup"><span data-stu-id="89c51-249">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="89c51-250">Słowa kluczowe razor</span><span class="sxs-lookup"><span data-stu-id="89c51-250">Razor keywords</span></span>

* <span data-ttu-id="89c51-251">Strona (wymaga platformy ASP.NET Core 2.0 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="89c51-251">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="89c51-252">— funkcje</span><span class="sxs-lookup"><span data-stu-id="89c51-252">functions</span></span>
* <span data-ttu-id="89c51-253">dziedziczy</span><span class="sxs-lookup"><span data-stu-id="89c51-253">inherits</span></span>
* <span data-ttu-id="89c51-254">model</span><span class="sxs-lookup"><span data-stu-id="89c51-254">model</span></span>
* <span data-ttu-id="89c51-255">sekcja</span><span class="sxs-lookup"><span data-stu-id="89c51-255">section</span></span>
* <span data-ttu-id="89c51-256">Pomocnik (nie są obecnie obsługiwane przez program ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="89c51-256">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="89c51-257">Słowa kluczowe razor będą miały zmienione znaczenie z `@(Razor Keyword)` (na przykład `@(functions)`).</span><span class="sxs-lookup"><span data-stu-id="89c51-257">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="89c51-258">Słowa kluczowe języka C# Razor</span><span class="sxs-lookup"><span data-stu-id="89c51-258">C# Razor keywords</span></span>

* <span data-ttu-id="89c51-259">case</span><span class="sxs-lookup"><span data-stu-id="89c51-259">case</span></span>
* <span data-ttu-id="89c51-260">do</span><span class="sxs-lookup"><span data-stu-id="89c51-260">do</span></span>
* <span data-ttu-id="89c51-261">default</span><span class="sxs-lookup"><span data-stu-id="89c51-261">default</span></span>
* <span data-ttu-id="89c51-262">dla</span><span class="sxs-lookup"><span data-stu-id="89c51-262">for</span></span>
* <span data-ttu-id="89c51-263">foreach</span><span class="sxs-lookup"><span data-stu-id="89c51-263">foreach</span></span>
* <span data-ttu-id="89c51-264">if</span><span class="sxs-lookup"><span data-stu-id="89c51-264">if</span></span>
* <span data-ttu-id="89c51-265">else</span><span class="sxs-lookup"><span data-stu-id="89c51-265">else</span></span>
* <span data-ttu-id="89c51-266">lock</span><span class="sxs-lookup"><span data-stu-id="89c51-266">lock</span></span>
* <span data-ttu-id="89c51-267">— przełącznik</span><span class="sxs-lookup"><span data-stu-id="89c51-267">switch</span></span>
* <span data-ttu-id="89c51-268">Spróbuj</span><span class="sxs-lookup"><span data-stu-id="89c51-268">try</span></span>
* <span data-ttu-id="89c51-269">CATCH</span><span class="sxs-lookup"><span data-stu-id="89c51-269">catch</span></span>
* <span data-ttu-id="89c51-270">finally</span><span class="sxs-lookup"><span data-stu-id="89c51-270">finally</span></span>
* <span data-ttu-id="89c51-271">korzystanie</span><span class="sxs-lookup"><span data-stu-id="89c51-271">using</span></span>
* <span data-ttu-id="89c51-272">while</span><span class="sxs-lookup"><span data-stu-id="89c51-272">while</span></span>

<span data-ttu-id="89c51-273">Słowa kluczowe języka C# Razor musi być podwójne anulowanie z `@(@C# Razor Keyword)` (na przykład `@(@case)`).</span><span class="sxs-lookup"><span data-stu-id="89c51-273">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="89c51-274">Pierwszy `@` specjalne analizator Razor.</span><span class="sxs-lookup"><span data-stu-id="89c51-274">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="89c51-275">Drugi `@` specjalne analizatora składni języka C#.</span><span class="sxs-lookup"><span data-stu-id="89c51-275">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="89c51-276">Zastrzeżone słowa kluczowe, które nie są używane przez Razor</span><span class="sxs-lookup"><span data-stu-id="89c51-276">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="89c51-277">— przestrzeń nazw</span><span class="sxs-lookup"><span data-stu-id="89c51-277">namespace</span></span>
* <span data-ttu-id="89c51-278">class</span><span class="sxs-lookup"><span data-stu-id="89c51-278">class</span></span>

## <a name="viewing-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="89c51-279">Wyświetlanie klasy Razor C# wygenerowany dla widoku</span><span class="sxs-lookup"><span data-stu-id="89c51-279">Viewing the Razor C# class generated for a view</span></span>

<span data-ttu-id="89c51-280">Dodaj następujące klasy do projektu programu ASP.NET MVC rdzeni:</span><span class="sxs-lookup"><span data-stu-id="89c51-280">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[Main](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="89c51-281">Zastąpienie `RazorTemplateEngine` dodane przez MVC z `CustomTemplateEngine` klasy:</span><span class="sxs-lookup"><span data-stu-id="89c51-281">Override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[Main](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="89c51-282">Ustaw punkt przerwania na `return csharpDocument` instrukcja `CustomTemplateEngine`.</span><span class="sxs-lookup"><span data-stu-id="89c51-282">Set a break point on the `return csharpDocument` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="89c51-283">Po przerwaniu wykonywania programu w punkcie przerwania, Wyświetl wartość `generatedCode`.</span><span class="sxs-lookup"><span data-stu-id="89c51-283">When program execution stops at the break point, view the value of `generatedCode`.</span></span>

![Widok wizualizatora tekst generatedCode](razor/_static/tvr.png)

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="89c51-285">Widok wyszukiwania i rozróżniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="89c51-285">View lookups and case sensitivity</span></span>

<span data-ttu-id="89c51-286">Aparat widoku Razor wykonuje wyszukiwanie z uwzględnieniem wielkości liter dla widoków.</span><span class="sxs-lookup"><span data-stu-id="89c51-286">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="89c51-287">Jednak rzeczywista wyszukiwania jest określany przez źródłowy system plików:</span><span class="sxs-lookup"><span data-stu-id="89c51-287">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="89c51-288">Źródło opartych na pliku:</span><span class="sxs-lookup"><span data-stu-id="89c51-288">File based source:</span></span> 
  * <span data-ttu-id="89c51-289">W systemach operacyjnych w systemach plików bez uwzględniania wielkości liter (na przykład system Windows) plik fizyczny dostawcy wyszukiwania są bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="89c51-289">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="89c51-290">Na przykład `return View("Test")` powoduje dopasowań dla */Views/Home/Test.cshtml*, */Views/home/test.cshtml*i inne wariant wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="89c51-290">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="89c51-291">W systemach plików z uwzględnieniem wielkości liter (na przykład, Linux, OS x i z `EmbeddedFileProvider`), wyszukiwanie jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="89c51-291">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="89c51-292">Na przykład `return View("Test")` dopasowań w szczególności */Views/Home/Test.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="89c51-292">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="89c51-293">Wstępnie skompilowana widoków: podstawowych ASP.NET 2.0 i nowsze, wyszukiwania prekompilowanego widoków nie uwzględnia wielkości liter we wszystkich systemach operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="89c51-293">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="89c51-294">Zachowanie jest takie same jak zachowanie dostawcy plików fizycznych w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="89c51-294">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="89c51-295">Jeśli dwa widoki prekompilowany różnią się tylko wielkością liter, wynik wyszukiwania jest deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="89c51-295">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="89c51-296">Deweloperzy są zachęcani do pasuje do wielkości liter nazwy plików i katalogów, aby wielkość liter w wyrazie:</span><span class="sxs-lookup"><span data-stu-id="89c51-296">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

    * <span data-ttu-id="89c51-297">Nazwy obszaru, kontrolera i akcji.</span><span class="sxs-lookup"><span data-stu-id="89c51-297">Area, controller, and action names.</span></span> 
    * <span data-ttu-id="89c51-298">Stron razor.</span><span class="sxs-lookup"><span data-stu-id="89c51-298">Razor Pages.</span></span>
    
<span data-ttu-id="89c51-299">Wielkości liter, gwarantuje, że wdrożeń znaleźć swoje opinie, niezależnie od źródłowy system plików.</span><span class="sxs-lookup"><span data-stu-id="89c51-299">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>