---
title: "Buforuj pomocnika tagów w podstawowej platformy ASP.NET MVC"
author: pkellner
description: "Pokazuje, jak pracować z pamięci podręcznej pomocnika tagów"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: dfd9c3c0c4e50a99e4f8703b01bd9b384930b87a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="68e83-103">Buforuj pomocnika tagów w podstawowej platformy ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="68e83-103">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="68e83-104">Przez [Kellner Peterowi](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="68e83-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="68e83-105">Pamięć podręczna pomocnika tagów umożliwia znacznie zwiększyć wydajność aplikacji platformy ASP.NET Core buforując zawartość wewnętrzna dostawcy platformy ASP.NET Core w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-105">The Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="68e83-106">Domyślnie ustawia aparat widoku Razor `expires-after` do 20 minut.</span><span class="sxs-lookup"><span data-stu-id="68e83-106">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="68e83-107">Następujący kod Razor buforuje daty/godziny:</span><span class="sxs-lookup"><span data-stu-id="68e83-107">The following Razor markup caches the date/time:</span></span>

```cshtml
<cache>@DateTime.Now</cache>
```

<span data-ttu-id="68e83-108">Pierwsze żądanie do strony zawierającej `CacheTagHelper` wyświetli bieżącej daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="68e83-108">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="68e83-109">Dodatkowe żądania zostaną wyświetlone wartość w pamięci podręcznej, dopóki bufor wygasa (domyślnie 20 minut) lub jest wykluczony przez wykorzystania pamięci.</span><span class="sxs-lookup"><span data-stu-id="68e83-109">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="68e83-110">Można ustawić czas trwania pamięci podręcznej z następującymi atrybutami:</span><span class="sxs-lookup"><span data-stu-id="68e83-110">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="68e83-111">Buforuj atrybuty pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="68e83-111">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="68e83-112">włączone</span><span class="sxs-lookup"><span data-stu-id="68e83-112">enabled</span></span>    


| <span data-ttu-id="68e83-113">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-113">Attribute Type</span></span>    | <span data-ttu-id="68e83-114">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-114">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="68e83-115">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="68e83-115">boolean</span></span>           | <span data-ttu-id="68e83-116">wartość "prawda" (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="68e83-116">"true" (default)</span></span>  |
|                   | <span data-ttu-id="68e83-117">"false"</span><span class="sxs-lookup"><span data-stu-id="68e83-117">"false"</span></span>   |


<span data-ttu-id="68e83-118">Określa, czy zawartość ujęty w pamięci podręcznej pomocnika tagów są buforowane.</span><span class="sxs-lookup"><span data-stu-id="68e83-118">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="68e83-119">Wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="68e83-119">The default is `true`.</span></span>  <span data-ttu-id="68e83-120">Jeśli ustawiono `false` tego pomocnika tagów pamięci podręcznej nie wpłyną buforowania na renderowanych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="68e83-120">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="68e83-121">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-121">Example:</span></span>

```cshtml
<cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="68e83-122">expires-on</span><span class="sxs-lookup"><span data-stu-id="68e83-122">expires-on</span></span> 

| <span data-ttu-id="68e83-123">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-123">Attribute Type</span></span>    | <span data-ttu-id="68e83-124">Przykładowa wartość</span><span class="sxs-lookup"><span data-stu-id="68e83-124">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="68e83-125">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="68e83-125">DateTimeOffset</span></span>    | <span data-ttu-id="68e83-126">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="68e83-126">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="68e83-127">Ustawia datę wygaśnięcia bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="68e83-127">Sets an absolute expiration date.</span></span> <span data-ttu-id="68e83-128">Poniższy przykład będą buforowane zawartość pamięci podręcznej pomocnika tagów do 5:02 PM 29 stycznia 2025.</span><span class="sxs-lookup"><span data-stu-id="68e83-128">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="68e83-129">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-129">Example:</span></span>

```cshtml
<cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="68e83-130">expires-after</span><span class="sxs-lookup"><span data-stu-id="68e83-130">expires-after</span></span>

| <span data-ttu-id="68e83-131">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-131">Attribute Type</span></span>    | <span data-ttu-id="68e83-132">Przykładowa wartość</span><span class="sxs-lookup"><span data-stu-id="68e83-132">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="68e83-133">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="68e83-133">TimeSpan</span></span>    | <span data-ttu-id="68e83-134">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="68e83-134">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="68e83-135">Ustawia czas od pierwszego żądania, aby buforować zawartość.</span><span class="sxs-lookup"><span data-stu-id="68e83-135">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="68e83-136">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-136">Example:</span></span>

```cshtml
<cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="68e83-137">Przedłużanie wygasa</span><span class="sxs-lookup"><span data-stu-id="68e83-137">expires-sliding</span></span>

| <span data-ttu-id="68e83-138">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-138">Attribute Type</span></span>    | <span data-ttu-id="68e83-139">Przykładowa wartość</span><span class="sxs-lookup"><span data-stu-id="68e83-139">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="68e83-140">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="68e83-140">TimeSpan</span></span>    | <span data-ttu-id="68e83-141">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="68e83-141">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="68e83-142">Ustawia czas, który wykluczyć wpisu pamięci podręcznej, jeśli nie uzyska dostępu.</span><span class="sxs-lookup"><span data-stu-id="68e83-142">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="68e83-143">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-143">Example:</span></span>

```cshtml
<cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="68e83-144">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="68e83-144">vary-by-header</span></span>

| <span data-ttu-id="68e83-145">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-145">Attribute Type</span></span>    | <span data-ttu-id="68e83-146">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-146">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-147">String</span><span class="sxs-lookup"><span data-stu-id="68e83-147">String</span></span>            | <span data-ttu-id="68e83-148">"User-Agent"</span><span class="sxs-lookup"><span data-stu-id="68e83-148">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="68e83-149">"User-Agent,content-encoding"</span><span class="sxs-lookup"><span data-stu-id="68e83-149">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="68e83-150">Akceptuje wartości jeden nagłówek lub rozdzielaną przecinkami listę wartości nagłówka, które mogą powodować odświeżenie pamięci podręcznej po zmianie.</span><span class="sxs-lookup"><span data-stu-id="68e83-150">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="68e83-151">Poniższy przykład monitoruje wartość nagłówka `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="68e83-151">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="68e83-152">Przykład będzie buforowanie zawartości dla każdego innego `User-Agent` przedstawiony na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e83-152">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="68e83-153">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-153">Example:</span></span>

```cshtml
<cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="68e83-154">różnią się przez zapytanie</span><span class="sxs-lookup"><span data-stu-id="68e83-154">vary-by-query</span></span>

| <span data-ttu-id="68e83-155">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-155">Attribute Type</span></span>    | <span data-ttu-id="68e83-156">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-156">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-157">String</span><span class="sxs-lookup"><span data-stu-id="68e83-157">String</span></span>            | <span data-ttu-id="68e83-158">"Przechowuj"</span><span class="sxs-lookup"><span data-stu-id="68e83-158">"Make"</span></span>                |
|                   | <span data-ttu-id="68e83-159">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="68e83-159">"Make,Model"</span></span> |

<span data-ttu-id="68e83-160">Akceptuje wartości jeden nagłówek lub rozdzielaną przecinkami listę wartości nagłówka, które mogą powodować odświeżenie pamięci podręcznej po zmianie wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="68e83-160">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="68e83-161">Poniższy przykład analizuje wartości `Make` i `Model`.</span><span class="sxs-lookup"><span data-stu-id="68e83-161">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="68e83-162">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-162">Example:</span></span>

```cshtml
<cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="68e83-163">różnią się przez trasy</span><span class="sxs-lookup"><span data-stu-id="68e83-163">vary-by-route</span></span>

| <span data-ttu-id="68e83-164">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-164">Attribute Type</span></span>    | <span data-ttu-id="68e83-165">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-165">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-166">String</span><span class="sxs-lookup"><span data-stu-id="68e83-166">String</span></span>            | <span data-ttu-id="68e83-167">"Przechowuj"</span><span class="sxs-lookup"><span data-stu-id="68e83-167">"Make"</span></span>                |
|                   | <span data-ttu-id="68e83-168">"Make,Model"</span><span class="sxs-lookup"><span data-stu-id="68e83-168">"Make,Model"</span></span> |

<span data-ttu-id="68e83-169">Akceptuje wartości jeden nagłówek lub rozdzielaną przecinkami listę wartości nagłówka, które mogą powodować odświeżenie pamięci podręcznej podczas zmiany wartości parametru danych trasy.</span><span class="sxs-lookup"><span data-stu-id="68e83-169">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="68e83-170">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-170">Example:</span></span>

<span data-ttu-id="68e83-171">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="68e83-171">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="68e83-172">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="68e83-172">*Index.cshtml*</span></span>

```cshtml
<cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="68e83-173">różnią się przez cookie</span><span class="sxs-lookup"><span data-stu-id="68e83-173">vary-by-cookie</span></span>

| <span data-ttu-id="68e83-174">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-174">Attribute Type</span></span>    | <span data-ttu-id="68e83-175">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-175">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-176">String</span><span class="sxs-lookup"><span data-stu-id="68e83-176">String</span></span>            | <span data-ttu-id="68e83-177">".AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="68e83-177">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="68e83-178">".AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="68e83-178">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="68e83-179">Akceptuje wartości jeden nagłówek lub rozdzielaną przecinkami listę wartości nagłówka, które mogą powodować odświeżenie pamięci podręcznej podczas zmiany (s) wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="68e83-179">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="68e83-180">Poniższy przykład analizuje plik cookie skojarzone z tożsamością ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="68e83-180">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="68e83-181">Gdy użytkownik jest uwierzytelniany żądania plik cookie należy ustawić wartość, która wyzwala odświeżania pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-181">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="68e83-182">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-182">Example:</span></span>

```cshtml
<cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="68e83-183">różnią się przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="68e83-183">vary-by-user</span></span>

| <span data-ttu-id="68e83-184">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-184">Attribute Type</span></span>    | <span data-ttu-id="68e83-185">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-185">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-186">Boolean</span><span class="sxs-lookup"><span data-stu-id="68e83-186">Boolean</span></span>             | <span data-ttu-id="68e83-187">wartość "prawda"</span><span class="sxs-lookup"><span data-stu-id="68e83-187">"true"</span></span>                  |
|                     | <span data-ttu-id="68e83-188">wartość "false" (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="68e83-188">"false" (default)</span></span> |

<span data-ttu-id="68e83-189">Określa, czy pamięć podręczna powinni resetować po zmianie zalogowanego użytkownika (lub jej podmiot kontekstu zabezpieczeń).</span><span class="sxs-lookup"><span data-stu-id="68e83-189">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="68e83-190">Bieżący użytkownik jest także znana jako podmiot zabezpieczeń kontekstu żądania i mogą być wyświetlane w widoku Razor odwołując `@User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="68e83-190">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="68e83-191">Poniższy przykład analizuje aktualnie zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="68e83-191">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="68e83-192">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-192">Example:</span></span>

```cshtml
<cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="68e83-193">Za pomocą tego atrybutu przechowuje zawartość w pamięci podręcznej za pomocą logowania i wyloguj się cyklu.</span><span class="sxs-lookup"><span data-stu-id="68e83-193">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="68e83-194">Korzystając z `vary-by-user="true"`, działania logowania i wyloguj się unieważnia pamięci podręcznej dla tego uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="68e83-194">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="68e83-195">Pamięć podręczna jest unieważniona, ponieważ nowa wartość unikatowy plik cookie jest generowany podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="68e83-195">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="68e83-196">Pamięci podręcznej jest utrzymywana dla anonimowego stanu pliki cookie nie istnieje lub utracił ważność.</span><span class="sxs-lookup"><span data-stu-id="68e83-196">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="68e83-197">Oznacza to, gdy żaden użytkownik nie jest zalogowany, będzie przechowywany pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-197">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="68e83-198">różnią się przez</span><span class="sxs-lookup"><span data-stu-id="68e83-198">vary-by</span></span>

| <span data-ttu-id="68e83-199">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-199">Attribute Type</span></span>    | <span data-ttu-id="68e83-200">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-200">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-201">String</span><span class="sxs-lookup"><span data-stu-id="68e83-201">String</span></span>             | <span data-ttu-id="68e83-202">"@Model"</span><span class="sxs-lookup"><span data-stu-id="68e83-202">"@Model"</span></span>                 |


<span data-ttu-id="68e83-203">Umożliwia dostosowanie pobiera buforowane dane.</span><span class="sxs-lookup"><span data-stu-id="68e83-203">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="68e83-204">Gdy obiekt odwołuje się zmian wartości atrybutu ciąg, zawartości pamięci podręcznej pomocnika tagów jest aktualizowana.</span><span class="sxs-lookup"><span data-stu-id="68e83-204">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="68e83-205">Często ciągów wartości modelu są przypisane do tego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="68e83-205">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="68e83-206">Efektywne oznacza to, że aktualizacja dowolną z wartości z połączonych unieważnia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-206">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="68e83-207">W poniższym przykładzie założono metody renderowania widoku sum wartość całkowita dwóch parametrów trasy, `myParam1` i `myParam2`i zwraca go jako właściwość pojedynczego modelu.</span><span class="sxs-lookup"><span data-stu-id="68e83-207">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="68e83-208">Po zmianie tej sumy zawartości pamięci podręcznej pomocnika tagów jest renderowany i ponownie buforowany.</span><span class="sxs-lookup"><span data-stu-id="68e83-208">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="68e83-209">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-209">Example:</span></span>

<span data-ttu-id="68e83-210">Akcja:</span><span class="sxs-lookup"><span data-stu-id="68e83-210">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="68e83-211">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="68e83-211">*Index.cshtml*</span></span>

```cshtml
<cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="68e83-212">priorytet</span><span class="sxs-lookup"><span data-stu-id="68e83-212">priority</span></span>

| <span data-ttu-id="68e83-213">Typ atrybutu</span><span class="sxs-lookup"><span data-stu-id="68e83-213">Attribute Type</span></span>    | <span data-ttu-id="68e83-214">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="68e83-214">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="68e83-215">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="68e83-215">CacheItemPriority</span></span>  | <span data-ttu-id="68e83-216">"High"</span><span class="sxs-lookup"><span data-stu-id="68e83-216">"High"</span></span>                   |
|                    | <span data-ttu-id="68e83-217">"Low"</span><span class="sxs-lookup"><span data-stu-id="68e83-217">"Low"</span></span> |
|                    | <span data-ttu-id="68e83-218">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="68e83-218">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="68e83-219">"Normal"</span><span class="sxs-lookup"><span data-stu-id="68e83-219">"Normal"</span></span> |

<span data-ttu-id="68e83-220">Zawiera wskazówki wykluczenia pamięci podręcznej do dostawcy wbudowanej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-220">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="68e83-221">Wyklucz serwer sieci web `Low` najpierw buforować wpisów, gdy jest wykorzystanie pamięci.</span><span class="sxs-lookup"><span data-stu-id="68e83-221">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="68e83-222">Przykład:</span><span class="sxs-lookup"><span data-stu-id="68e83-222">Example:</span></span>

```cshtml
<cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</cache>
```

<span data-ttu-id="68e83-223">`priority` Atrybutu nie gwarantuje określony poziom przechowywania w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-223">The `priority` attribute does not guarantee a specific level of cache retention.</span></span> <span data-ttu-id="68e83-224">`CacheItemPriority`jest tylko sugestię.</span><span class="sxs-lookup"><span data-stu-id="68e83-224">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="68e83-225">Ustawienie tego atrybutu na `NeverRemove` nie gwarantuje, że zawsze zachowywania pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="68e83-225">Setting this attribute to `NeverRemove` does not guarantee that the cache will always be retained.</span></span> <span data-ttu-id="68e83-226">Zobacz [dodatkowe zasoby](#additional-resources) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="68e83-226">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="68e83-227">Pomocnik Tag pamięci podręcznej jest zależna od [pamięci podręcznej usługi](xref:performance/caching/memory).</span><span class="sxs-lookup"><span data-stu-id="68e83-227">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="68e83-228">Pamięci podręcznej pomocnika tagów dodaje usługę, jeśli nie został dodany.</span><span class="sxs-lookup"><span data-stu-id="68e83-228">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68e83-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="68e83-229">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>