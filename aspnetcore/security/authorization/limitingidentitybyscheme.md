---
title: "Autoryzowanie z określonym schematem - platformy ASP.NET Core"
author: rick-anderson
description: "W tym artykule wyjaśniono, jak ograniczyć tożsamości do określonego schematu podczas pracy z wielu metod uwierzytelniania."
ms.author: riande
manager: wpickett
ms.date: 10/12/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/limitingidentitybyscheme
ms.openlocfilehash: 099dba1a4235ef62ea298748645b99e2d6d12d44
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="authorize-with-a-specific-scheme"></a><span data-ttu-id="791b2-103">Autoryzowanie z określonego systemu</span><span class="sxs-lookup"><span data-stu-id="791b2-103">Authorize with a specific scheme</span></span>

<span data-ttu-id="791b2-104">W niektórych scenariuszach, takich jak aplikacje jednostronicowe (źródła) jest często wiele metod uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="791b2-104">In some scenarios, such as Single Page Applications (SPAs), it's common to use multiple authentication methods.</span></span> <span data-ttu-id="791b2-105">Na przykład aplikacji mogą używać uwierzytelniania opartego na pliku cookie do logowania i uwierzytelniania elementu nośnego JWT dla żądań JavaScript.</span><span class="sxs-lookup"><span data-stu-id="791b2-105">For example, the app may use cookie-based authentication to log in and JWT bearer authentication for JavaScript requests.</span></span> <span data-ttu-id="791b2-106">W niektórych przypadkach aplikacja może mieć wiele wystąpień program obsługi uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="791b2-106">In some cases, the app may have multiple instances of an authentication handler.</span></span> <span data-ttu-id="791b2-107">Na przykład dwa obsługi pliku cookie, których jedna zawiera podstawowej tożsamości, a drugi jest tworzony podczas zostało wyzwolone uwierzytelnianie wieloskładnikowe (MFA).</span><span class="sxs-lookup"><span data-stu-id="791b2-107">For example, two cookie handlers where one contains a basic identity and one is created when a multi-factor authentication (MFA) has been triggered.</span></span> <span data-ttu-id="791b2-108">Mogą być wyzwalane MFA, ponieważ użytkownik zażądał operacji, która wymaga dodatkowych zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="791b2-108">MFA may be triggered because the user requested an operation that requires extra security.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="791b2-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="791b2-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="791b2-110">Schemat uwierzytelniania nosi nazwę po skonfigurowaniu usługi uwierzytelniania podczas uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="791b2-110">An authentication scheme is named when the authentication service is configured during authentication.</span></span> <span data-ttu-id="791b2-111">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="791b2-111">For example:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Code omitted for brevity

    services.AddAuthentication()
        .AddCookie(options => {
            options.LoginPath = "/Account/Unauthorized/";
            options.AccessDeniedPath = "/Account/Forbidden/";
        })
        .AddJwtBearer(options => {
            options.Audience = "http://localhost:5001/";
            options.Authority = "http://localhost:5000/";
        });
```

<span data-ttu-id="791b2-112">W powyższym kodzie dwóch metod obsługi uwierzytelniania zostały dodane: jeden dla plików cookie i jeden dla elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="791b2-112">In the preceding code, two authentication handlers have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="791b2-113">Określanie domyślnego schematu powoduje `HttpContext.User` ustawiona do tej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="791b2-113">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="791b2-114">W razie potrzeby nie jest to zachowanie można ją wyłączyć, wywołując bez parametrów formę `AddAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="791b2-114">If that behavior isn't desired, disable it by invoking the parameterless form of `AddAuthentication`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="791b2-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="791b2-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="791b2-116">Schematy uwierzytelniania są nazywane po skonfigurowaniu uwierzytelniania middlewares podczas uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="791b2-116">Authentication schemes are named when authentication middlewares are configured during authentication.</span></span> <span data-ttu-id="791b2-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="791b2-117">For example:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // Code omitted for brevity

    app.UseCookieAuthentication(new CookieAuthenticationOptions()
    {
        AuthenticationScheme = "Cookie",
        LoginPath = "/Account/Unauthorized/",
        AccessDeniedPath = "/Account/Forbidden/",
        AutomaticAuthenticate = false
    });
    
    app.UseJwtBearerAuthentication(new JwtBearerOptions()
    {
        AuthenticationScheme = "Bearer",
        AutomaticAuthenticate = false,
        Audience = "http://localhost:5001/",
        Authority = "http://localhost:5000/",
        RequireHttpsMetadata = false
    });
```

<span data-ttu-id="791b2-118">W powyższym kodzie dodano dwa middlewares uwierzytelniania: jeden dla plików cookie i jeden dla elementu nośnego.</span><span class="sxs-lookup"><span data-stu-id="791b2-118">In the preceding code, two authentication middlewares have been added: one for cookies and one for bearer.</span></span>

>[!NOTE]
><span data-ttu-id="791b2-119">Określanie domyślnego schematu powoduje `HttpContext.User` ustawiona do tej tożsamości.</span><span class="sxs-lookup"><span data-stu-id="791b2-119">Specifying the default scheme results in the `HttpContext.User` property being set to that identity.</span></span> <span data-ttu-id="791b2-120">W razie potrzeby nie jest to zachowanie można ją wyłączyć, ustawiając `AuthenticationOptions.AutomaticAuthenticate` właściwości `false`.</span><span class="sxs-lookup"><span data-stu-id="791b2-120">If that behavior isn't desired, disable it by setting the `AuthenticationOptions.AutomaticAuthenticate` property to `false`.</span></span>

---

## <a name="selecting-the-scheme-with-the-authorize-attribute"></a><span data-ttu-id="791b2-121">Wybieranie schemat w atrybucie autoryzacji</span><span class="sxs-lookup"><span data-stu-id="791b2-121">Selecting the scheme with the Authorize attribute</span></span>

<span data-ttu-id="791b2-122">W punkcie autoryzacji aplikacja wskazuje obsługi, który ma być używane.</span><span class="sxs-lookup"><span data-stu-id="791b2-122">At the point of authorization, the app indicates the handler to be used.</span></span> <span data-ttu-id="791b2-123">Wybierz program obsługi, z którym autoryzacji przez przekazanie rozdzielana przecinkami lista schematy uwierzytelniania do aplikacji `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="791b2-123">Select the handler with which the app will authorize by passing a comma-delimited list of authentication schemes to `[Authorize]`.</span></span> <span data-ttu-id="791b2-124">`[Authorize]` Atrybut Określa schemat uwierzytelniania lub systemów do użycia niezależnie od tego, czy domyślny został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="791b2-124">The `[Authorize]` attribute specifies the authentication scheme or schemes to use regardless of whether a default is configured.</span></span> <span data-ttu-id="791b2-125">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="791b2-125">For example:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="791b2-126">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="791b2-126">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="791b2-127">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="791b2-127">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = AuthSchemes)]
public class MixedController : Controller
    // Requires the following imports:
    // using Microsoft.AspNetCore.Authentication.Cookies;
    // using Microsoft.AspNetCore.Authentication.JwtBearer;
    private const string AuthSchemes =
        CookieAuthenticationDefaults.AuthenticationScheme + "," +
        JwtBearerDefaults.AuthenticationScheme;
```

---

<span data-ttu-id="791b2-128">W powyższym przykładzie zarówno pliku cookie i elementu nośnego Uruchom i mieć możliwość Utwórz i Dołącz tożsamości dla bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="791b2-128">In the preceding example, both the cookie and bearer handlers run and have a chance to create and append an identity for the current user.</span></span> <span data-ttu-id="791b2-129">Umożliwia określenie tylko jednego schematu, odpowiedni obsługi jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="791b2-129">By specifying a single scheme only, the corresponding handler runs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="791b2-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="791b2-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
[Authorize(AuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="791b2-131">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="791b2-131">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
[Authorize(ActiveAuthenticationSchemes = 
    JwtBearerDefaults.AuthenticationScheme)]
public class MixedController : Controller
```

---

<span data-ttu-id="791b2-132">W powyższym kodzie tylko obsługi ze schematem "Bearer" działa.</span><span class="sxs-lookup"><span data-stu-id="791b2-132">In the preceding code, only the handler with the "Bearer" scheme runs.</span></span> <span data-ttu-id="791b2-133">Wszystkie tożsamości oparte na pliku cookie są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="791b2-133">Any cookie-based identities are ignored.</span></span>

## <a name="selecting-the-scheme-with-policies"></a><span data-ttu-id="791b2-134">Wybieranie schematu przy użyciu zasad</span><span class="sxs-lookup"><span data-stu-id="791b2-134">Selecting the scheme with policies</span></span>

<span data-ttu-id="791b2-135">Jeśli wolisz określić żądany schemat w [zasad](xref:security/authorization/policies), można ustawić `AuthenticationSchemes` kolekcji podczas dodawania zasad:</span><span class="sxs-lookup"><span data-stu-id="791b2-135">If you prefer to specify the desired schemes in [policy](xref:security/authorization/policies), you can set the `AuthenticationSchemes` collection when adding your policy:</span></span>

```csharp
services.AddAuthorization(options =>
{
    options.AddPolicy("Over18", policy =>
    {
        policy.AuthenticationSchemes.Add(JwtBearerDefaults.AuthenticationScheme);
        policy.RequireAuthenticatedUser();
        policy.Requirements.Add(new MinimumAgeRequirement());
    });
});
```

<span data-ttu-id="791b2-136">W powyższym przykładzie zasad "Over18" jest uruchamiana tylko dla tożsamości utworzony przez program obsługi "Bearer".</span><span class="sxs-lookup"><span data-stu-id="791b2-136">In the preceding example, the "Over18" policy only runs against the identity created by the "Bearer" handler.</span></span> <span data-ttu-id="791b2-137">Użyj zasad przez ustawienie `[Authorize]` atrybutu `Policy` właściwości:</span><span class="sxs-lookup"><span data-stu-id="791b2-137">Use the policy by setting the `[Authorize]` attribute's `Policy` property:</span></span>

```csharp
[Authorize(Policy = "Over18")]
public class RegistrationController : Controller
```