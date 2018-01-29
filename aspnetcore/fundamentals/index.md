---
title: Podstawowe informacje na temat platformy ASP.NET Core
author: rick-anderson
description: "Poznaj podstawowe pojęcia do tworzenia aplikacji platformy ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 09/30/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/index
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d977c13eb5f4cbe8bac261733bdc747e6c19b2a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="65394-103">Podstawowe informacje na temat platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="65394-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="65394-104">Aplikacja platformy ASP.NET Core jest aplikacji konsoli, która tworzy serwer sieci web w jego `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="65394-104">An ASP.NET Core application is a console app that creates a web server in its `Main` method:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="65394-105">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="65394-105">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

<span data-ttu-id="65394-106">`Main` Wywołuje metodę `WebHost.CreateDefaultBuilder`, który jest zgodny ze wzorcem Konstruktor do tworzenia host aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-106">The `Main` method invokes `WebHost.CreateDefaultBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="65394-107">Konstruktor ma metody, które definiują serwera sieci web (na przykład `UseKestrel`) i Klasa początkowa (`UseStartup`).</span><span class="sxs-lookup"><span data-stu-id="65394-107">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="65394-108">W powyższym przykładzie [Kestrel](xref:fundamentals/servers/kestrel) automatycznie jest przydzielany serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-108">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="65394-109">Host sieci web platformy ASP.NET Core próbuje uruchomić na serwerze IIS, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="65394-109">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="65394-110">Inne serwery w sieci web, takich jak [HTTP.sys](xref:fundamentals/servers/httpsys), mogą być używane przez wywołanie metody odpowiednie rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="65394-110">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="65394-111">`UseStartup`znajduje się w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="65394-111">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="65394-112">`IWebHostBuilder`, zwracany typ `WebHost.CreateDefaultBuilder` wywołania, udostępnia wiele metod opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="65394-112">`IWebHostBuilder`, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="65394-113">Oto niektóre z tych metod `UseHttpSys` do hostowania aplikacji w pliku HTTP.sys i `UseContentRoot` służący do określania zawartości katalogu.</span><span class="sxs-lookup"><span data-stu-id="65394-113">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="65394-114">`Build` i `Run` metody Konstruuj `IWebHost` obiekt, który hostuje aplikację i rozpoczyna nasłuchiwanie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="65394-114">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="65394-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="65394-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs)]

<span data-ttu-id="65394-116">`Main` Używa metody `WebHostBuilder`, który jest zgodny ze wzorcem Konstruktor do tworzenia host aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-116">The `Main` method uses `WebHostBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="65394-117">Konstruktor ma metody, które definiują serwera sieci web (na przykład `UseKestrel`) i Klasa początkowa (`UseStartup`).</span><span class="sxs-lookup"><span data-stu-id="65394-117">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="65394-118">W powyższym przykładzie [Kestrel](xref:fundamentals/servers/kestrel) używany jest serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-118">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="65394-119">Inne serwery w sieci web, takich jak [WebListener](xref:fundamentals/servers/weblistener), mogą być używane przez wywołanie metody odpowiednie rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="65394-119">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="65394-120">`UseStartup`znajduje się w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="65394-120">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="65394-121">`WebHostBuilder`udostępnia wiele metod opcjonalne, w tym `UseIISIntegration` dla hostingu w usługach IIS i usług IIS Express i `UseContentRoot` służący do określania zawartości katalogu.</span><span class="sxs-lookup"><span data-stu-id="65394-121">`WebHostBuilder` provides many optional methods, including `UseIISIntegration` for hosting in IIS and IIS Express and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="65394-122">`Build` i `Run` metody Konstruuj `IWebHost` obiekt, który hostuje aplikację i rozpoczyna nasłuchiwanie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="65394-122">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

---

## <a name="startup"></a><span data-ttu-id="65394-123">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="65394-123">Startup</span></span>

<span data-ttu-id="65394-124">`UseStartup` Metoda `WebHostBuilder` Określa `Startup` klasy dla aplikacji:</span><span class="sxs-lookup"><span data-stu-id="65394-124">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="65394-125">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="65394-125">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="65394-126">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="65394-126">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

---

<span data-ttu-id="65394-127">`Startup` Klasa jest służącego do określania potoku żądania obsługi i konfigurowana żadnych usług wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="65394-127">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="65394-128">`Startup` Klasy musi być publiczny i może zawierać następujących metod:</span><span class="sxs-lookup"><span data-stu-id="65394-128">The `Startup` class must be public and contain the following methods:</span></span>

```csharp
public class Startup
{
    // This method gets called by the runtime. Use this method
    // to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // This method gets called by the runtime. Use this method
    // to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

<span data-ttu-id="65394-129">`ConfigureServices`definiuje [usług](#dependency-injection-services) używany przez aplikację (na przykład ASP.NET Core MVC, Entity Framework Core, tożsamość).</span><span class="sxs-lookup"><span data-stu-id="65394-129">`ConfigureServices` defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="65394-130">`Configure`definiuje [oprogramowanie pośredniczące](xref:fundamentals/middleware) dla żądania potoku.</span><span class="sxs-lookup"><span data-stu-id="65394-130">`Configure` defines the [middleware](xref:fundamentals/middleware) for the request pipeline.</span></span>

<span data-ttu-id="65394-131">Aby uzyskać więcej informacji, zobacz [uruchamiania aplikacji](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="65394-131">For more information, see [Application startup](xref:fundamentals/startup).</span></span>

## <a name="content-root"></a><span data-ttu-id="65394-132">Główny zawartości</span><span class="sxs-lookup"><span data-stu-id="65394-132">Content root</span></span>

<span data-ttu-id="65394-133">Główny zawartości jest ścieżki podstawowej do dowolnej zawartości używany przez aplikację, takich jak widoki, [stron Razor](xref:mvc/razor-pages/index)i zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="65394-133">The content root is the base path to any content used by the app, such as views, [Razor Pages](xref:mvc/razor-pages/index), and static assets.</span></span> <span data-ttu-id="65394-134">Domyślnie zawartości główny jest taka sama jak podstawowa ścieżka aplikacji dla pliku wykonywalnego hosting aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65394-134">By default, the content root is the same as application base path for the executable hosting the app.</span></span>

## <a name="web-root"></a><span data-ttu-id="65394-135">Główny sieci Web</span><span class="sxs-lookup"><span data-stu-id="65394-135">Web root</span></span>

<span data-ttu-id="65394-136">Katalog główny aplikacji sieci web jest katalog projektu zawierającego zasoby publiczne, statyczne, takie jak CSS, JavaScript i plików obrazów.</span><span class="sxs-lookup"><span data-stu-id="65394-136">The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="65394-137">Iniekcji zależności (usługi)</span><span class="sxs-lookup"><span data-stu-id="65394-137">Dependency Injection (Services)</span></span>

<span data-ttu-id="65394-138">Usługa jest składnikiem, który jest przeznaczony do wspólnego wykorzystania w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65394-138">A service is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="65394-139">Usługi są udostępniane za pomocą [iniekcji zależności (Podpisane)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="65394-139">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="65394-140">Platformy ASP.NET Core zawiera natywny **I**nWymagana **o**f **C**kontenera kontrolne (IoC), który obsługuje [iniekcji konstruktora](xref:mvc/controllers/dependency-injection#constructor-injection) domyślnie.</span><span class="sxs-lookup"><span data-stu-id="65394-140">ASP.NET Core includes a native **I**nversion **o**f **C**ontrol (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="65394-141">W razie potrzeby można zastąpić domyślny kontener macierzystego.</span><span class="sxs-lookup"><span data-stu-id="65394-141">You can replace the default native container if you wish.</span></span> <span data-ttu-id="65394-142">Oprócz korzyści luźne powiązanie, Podpisane sprawia, że usługi dostępne w całej aplikacji (na przykład [rejestrowanie](xref:fundamentals/logging/index)).</span><span class="sxs-lookup"><span data-stu-id="65394-142">In addition to its loose coupling benefit, DI makes services available throughout your app (for example, [logging](xref:fundamentals/logging/index)).</span></span>

<span data-ttu-id="65394-143">Aby uzyskać więcej informacji, zobacz [iniekcji zależności](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="65394-143">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="65394-144">Oprogramowanie pośredniczące</span><span class="sxs-lookup"><span data-stu-id="65394-144">Middleware</span></span>

<span data-ttu-id="65394-145">W ASP.NET Core redagowania Twojego żądania potoku przy użyciu [oprogramowanie pośredniczące](xref:fundamentals/middleware).</span><span class="sxs-lookup"><span data-stu-id="65394-145">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware).</span></span> <span data-ttu-id="65394-146">Oprogramowanie pośredniczące platformy ASP.NET Core wykonuje asynchroniczne logiki na `HttpContext` , a następnie wywołuje następne oprogramowanie pośredniczące w sekwencji lub bezpośrednio kończy żądanie.</span><span class="sxs-lookup"><span data-stu-id="65394-146">ASP.NET Core middleware performs asynchronous logic on an `HttpContext` and then either invokes the next middleware in the sequence or terminates the request directly.</span></span> <span data-ttu-id="65394-147">Składnik oprogramowania pośredniczącego o nazwie "XYZ" jest dodawany przez wywołanie `UseXYZ` — metoda rozszerzenia w `Configure` metody.</span><span class="sxs-lookup"><span data-stu-id="65394-147">A middleware component called "XYZ" is added by invoking an `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="65394-148">Platformy ASP.NET Core zawiera bogaty zestaw wbudowanych oprogramowania pośredniczącego:</span><span class="sxs-lookup"><span data-stu-id="65394-148">ASP.NET Core comes with a rich set of built-in middleware:</span></span>

* [<span data-ttu-id="65394-149">Pliki statyczne</span><span class="sxs-lookup"><span data-stu-id="65394-149">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="65394-150">Routing</span><span class="sxs-lookup"><span data-stu-id="65394-150">Routing</span></span>](xref:fundamentals/routing)
* [<span data-ttu-id="65394-151">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="65394-151">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="65394-152">Oprogramowanie pośredniczące kompresji odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="65394-152">Response Compression Middleware</span></span>](xref:performance/response-compression)
* [<span data-ttu-id="65394-153">Oprogramowanie pośredniczące ponownego zapisywania adresów URL</span><span class="sxs-lookup"><span data-stu-id="65394-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)

<span data-ttu-id="65394-154">[OWIN](http://owin.org)— oparte na oprogramowaniu pośredniczącym jest dostępne dla aplikacji platformy ASP.NET Core, a można pisać własne niestandardowe oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="65394-154">[OWIN](http://owin.org)-based middleware is available for ASP.NET Core apps, and you can write your own custom middleware.</span></span>

<span data-ttu-id="65394-155">Aby uzyskać więcej informacji, zobacz [oprogramowanie pośredniczące](xref:fundamentals/middleware) i [interfejsu Open Web dla platformy .NET (OWIN)](xref:fundamentals/owin).</span><span class="sxs-lookup"><span data-stu-id="65394-155">For more information, see [Middleware](xref:fundamentals/middleware) and [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="environments"></a><span data-ttu-id="65394-156">Środowisk</span><span class="sxs-lookup"><span data-stu-id="65394-156">Environments</span></span>

<span data-ttu-id="65394-157">Środowiskach, na przykład "Programowanie" i "Production", są pojęcie pierwszą klasą w ASP.NET Core i można ustawić za pomocą zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="65394-157">Environments, such as "Development" and "Production", are a first-class notion in ASP.NET Core and can be set using environment variables.</span></span>

<span data-ttu-id="65394-158">Aby uzyskać więcej informacji, zobacz [Praca w środowiskach wielu](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="65394-158">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="configuration"></a><span data-ttu-id="65394-159">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="65394-159">Configuration</span></span>

<span data-ttu-id="65394-160">Platformy ASP.NET Core wykorzystuje model konfiguracji na podstawie par nazwa wartość.</span><span class="sxs-lookup"><span data-stu-id="65394-160">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="65394-161">Model konfiguracji nie jest oparty na `System.Configuration` lub *web.config*. Konfiguracja uzyskuje ustawienia z zestawu uporządkowanych dostawców konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="65394-161">The configuration model isn't based on `System.Configuration` or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="65394-162">Dostawców wbudowanych konfiguracji obsługuje wiele formatów (XML, JSON, INI) i zmiennych środowiskowych w celu włączenia konfiguracji opartej na środowisku.</span><span class="sxs-lookup"><span data-stu-id="65394-162">The built-in configuration providers support a variety of file formats (XML, JSON, INI) and environment variables to enable environment-based configuration.</span></span> <span data-ttu-id="65394-163">Można również napisać własny dostawców niestandardowych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="65394-163">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="65394-164">Aby uzyskać więcej informacji, zobacz [konfiguracji](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="65394-164">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="logging"></a><span data-ttu-id="65394-165">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="65394-165">Logging</span></span>

<span data-ttu-id="65394-166">Platformy ASP.NET Core obsługuje interfejs API rejestrowania, który współpracuje z różnych dostawców rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="65394-166">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="65394-167">Dostawców wbudowanych obsługuje wysyłania dzienników do jednego lub więcej miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="65394-167">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="65394-168">Można platform rejestrowania innych firm.</span><span class="sxs-lookup"><span data-stu-id="65394-168">Third-party logging frameworks can be used.</span></span>

[<span data-ttu-id="65394-169">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="65394-169">Logging</span></span>](xref:fundamentals/logging/index)

## <a name="error-handling"></a><span data-ttu-id="65394-170">Obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="65394-170">Error handling</span></span>

<span data-ttu-id="65394-171">Platformy ASP.NET Core ma wbudowane funkcje obsługi błędów w aplikacji, w tym strony wyjątek developer, niestandardowe strony błędów stron kodowych statycznych stanu i uruchamiania obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="65394-171">ASP.NET Core has built-in features for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="65394-172">Aby uzyskać więcej informacji, zobacz [obsługi błędu](xref:fundamentals/error-handling).</span><span class="sxs-lookup"><span data-stu-id="65394-172">For more information, see [Error Handling](xref:fundamentals/error-handling).</span></span>

## <a name="routing"></a><span data-ttu-id="65394-173">Routing</span><span class="sxs-lookup"><span data-stu-id="65394-173">Routing</span></span>

<span data-ttu-id="65394-174">Platformy ASP.NET Core oferuje funkcje routingu żądań aplikacji do obsługi trasy.</span><span class="sxs-lookup"><span data-stu-id="65394-174">ASP.NET Core offers features for routing of app requests to route handlers.</span></span>

<span data-ttu-id="65394-175">Aby uzyskać więcej informacji, zobacz [Routing](xref:fundamentals/routing).</span><span class="sxs-lookup"><span data-stu-id="65394-175">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="file-providers"></a><span data-ttu-id="65394-176">Plik dostawców</span><span class="sxs-lookup"><span data-stu-id="65394-176">File providers</span></span>

<span data-ttu-id="65394-177">Platformy ASP.NET Core abstracts dostępu do systemu plików przy użyciu dostawców pliku, który zapewnia wspólny interfejs do pracy z plikami na różnych platformach.</span><span class="sxs-lookup"><span data-stu-id="65394-177">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="65394-178">Aby uzyskać więcej informacji, zobacz [dostawców pliku](xref:fundamentals/file-providers).</span><span class="sxs-lookup"><span data-stu-id="65394-178">For more information, see [File Providers](xref:fundamentals/file-providers).</span></span>

## <a name="static-files"></a><span data-ttu-id="65394-179">Pliki statyczne</span><span class="sxs-lookup"><span data-stu-id="65394-179">Static files</span></span>

<span data-ttu-id="65394-180">Oprogramowanie pośredniczące plików statycznych służy plików statycznych, takich jak HTML, CSS, obrazu i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="65394-180">Static files middleware serves static files, such as HTML, CSS, image, and JavaScript.</span></span>

<span data-ttu-id="65394-181">Aby uzyskać więcej informacji, zobacz [Praca z pliki statyczne](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="65394-181">For more information, see [Working with static files](xref:fundamentals/static-files).</span></span>

## <a name="hosting"></a><span data-ttu-id="65394-182">Hosting</span><span class="sxs-lookup"><span data-stu-id="65394-182">Hosting</span></span>

<span data-ttu-id="65394-183">Aplikacje platformy ASP.NET Core skonfigurować i uruchomić *hosta*, który jest odpowiedzialny za zarządzanie uruchamiania i okresem istnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65394-183">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="65394-184">Aby uzyskać więcej informacji, zobacz [hostingu](xref:fundamentals/hosting).</span><span class="sxs-lookup"><span data-stu-id="65394-184">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

## <a name="session-and-application-state"></a><span data-ttu-id="65394-185">Stan sesji i aplikacji</span><span class="sxs-lookup"><span data-stu-id="65394-185">Session and application state</span></span>

<span data-ttu-id="65394-186">Stan sesji jest funkcją platformy ASP.NET Core, który służy do zapisywania i przechowywania danych użytkownika, gdy użytkownik będzie przeglądać aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-186">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span>

<span data-ttu-id="65394-187">Aby uzyskać więcej informacji, zobacz [sesji i stan aplikacji](xref:fundamentals/app-state).</span><span class="sxs-lookup"><span data-stu-id="65394-187">For more information, see [Session and application state](xref:fundamentals/app-state).</span></span>

## <a name="servers"></a><span data-ttu-id="65394-188">Serwery</span><span class="sxs-lookup"><span data-stu-id="65394-188">Servers</span></span>

<span data-ttu-id="65394-189">Model hostowania w programie ASP.NET Core bezpośrednio nie nasłuchuje żądań.</span><span class="sxs-lookup"><span data-stu-id="65394-189">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="65394-190">Model hostowania polega na implementację serwera HTTP do przekazywania żądań do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65394-190">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="65394-191">Przekazane żądanie jest zawijany jako zestaw obiektów funkcji, które są dostępne za pośrednictwem interfejsów.</span><span class="sxs-lookup"><span data-stu-id="65394-191">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="65394-192">Serwer sieci web zarządzany, i platform, w nazwie zawiera platformy ASP.NET Core [Kestrel](xref:fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="65394-192">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="65394-193">Kestrel jest często wykonywane za produkcyjnym serwerem sieci web, takich jak [IIS](https://www.iis.net/) lub [Nginx](http://nginx.org).</span><span class="sxs-lookup"><span data-stu-id="65394-193">Kestrel is often run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org).</span></span> <span data-ttu-id="65394-194">Kestrel może działać jako serwer graniczny.</span><span class="sxs-lookup"><span data-stu-id="65394-194">Kestrel can be run as an edge server.</span></span>

<span data-ttu-id="65394-195">Aby uzyskać więcej informacji, zobacz [serwerów](xref:fundamentals/servers/index) i następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="65394-195">For more information, see [Servers](xref:fundamentals/servers/index) and the following topics:</span></span>

* [<span data-ttu-id="65394-196">Kestrel</span><span class="sxs-lookup"><span data-stu-id="65394-196">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="65394-197">Moduł ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="65394-197">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* <span data-ttu-id="65394-198">[Sterownik HTTP.sys](xref:fundamentals/servers/httpsys) (wcześniej nazywanych [WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="65394-198">[HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="65394-199">Lokalizacja i globalizacja</span><span class="sxs-lookup"><span data-stu-id="65394-199">Globalization and localization</span></span>

<span data-ttu-id="65394-200">Tworzenie wielu języków witryny sieci Web za pomocą platformy ASP.NET Core umożliwia witrynę tak, aby uzyskać dostęp do większej liczby osób.</span><span class="sxs-lookup"><span data-stu-id="65394-200">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="65394-201">Platformy ASP.NET Core udostępnia usługi i oprogramowanie pośredniczące dla lokalizowanie do różnych języków i kultur.</span><span class="sxs-lookup"><span data-stu-id="65394-201">ASP.NET Core provides services and middleware for localizing into different languages and cultures.</span></span>

<span data-ttu-id="65394-202">Aby uzyskać więcej informacji, zobacz [lokalizacja i globalizacja](xref:fundamentals/localization).</span><span class="sxs-lookup"><span data-stu-id="65394-202">For more information, see [Globalization and localization](xref:fundamentals/localization).</span></span>

## <a name="request-features"></a><span data-ttu-id="65394-203">Funkcje na żądanie</span><span class="sxs-lookup"><span data-stu-id="65394-203">Request features</span></span>

<span data-ttu-id="65394-204">Szczegóły implementacji serwera sieci Web związanych z żądaniami HTTP i odpowiedzi są zdefiniowane w interfejsach.</span><span class="sxs-lookup"><span data-stu-id="65394-204">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="65394-205">Te interfejsy są używane przez implementacje serwera i oprogramowanie pośredniczące do tworzenia i modyfikowania procesu hostingu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65394-205">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="65394-206">Aby uzyskać więcej informacji, zobacz [żądania funkcji](xref:fundamentals/request-features).</span><span class="sxs-lookup"><span data-stu-id="65394-206">For more information, see [Request Features](xref:fundamentals/request-features).</span></span>

## <a name="open-web-interface-for-net-owin"></a><span data-ttu-id="65394-207">Otwórz interfejs sieci Web dla platformy .NET (OWIN)</span><span class="sxs-lookup"><span data-stu-id="65394-207">Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="65394-208">Platformy ASP.NET Core obsługuje interfejsu Open Web dla platformy .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="65394-208">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="65394-209">OWIN umożliwia aplikacjom sieci web jest całkowicie niezależna od serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-209">OWIN allows web apps to be decoupled from web servers.</span></span>

<span data-ttu-id="65394-210">Aby uzyskać więcej informacji, zobacz [interfejsu Open Web dla platformy .NET (OWIN)](xref:fundamentals/owin).</span><span class="sxs-lookup"><span data-stu-id="65394-210">For more information, see [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="websockets"></a><span data-ttu-id="65394-211">Protokół WebSockets</span><span class="sxs-lookup"><span data-stu-id="65394-211">WebSockets</span></span>

<span data-ttu-id="65394-212">[Protokół WebSocket](https://wikipedia.org/wiki/WebSocket) jest to protokół umożliwiający kanały dwukierunkowej komunikacji trwałego za pośrednictwem połączeń TCP.</span><span class="sxs-lookup"><span data-stu-id="65394-212">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="65394-213">Służy do aplikacji, takich jak rozmowa, giełdowych, gier i dowolnym wymaganych w czasie rzeczywistym funkcji w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-213">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="65394-214">Platformy ASP.NET Core obsługuje funkcje gniazda sieci web.</span><span class="sxs-lookup"><span data-stu-id="65394-214">ASP.NET Core supports web socket features.</span></span>

<span data-ttu-id="65394-215">Aby uzyskać więcej informacji, zobacz [Websocket](xref:fundamentals/websockets).</span><span class="sxs-lookup"><span data-stu-id="65394-215">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="65394-216">Microsoft.AspNetCore.All metapackage</span><span class="sxs-lookup"><span data-stu-id="65394-216">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="65394-217">[Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage dla platformy ASP.NET Core obejmuje:</span><span class="sxs-lookup"><span data-stu-id="65394-217">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="65394-218">Wszystkie obsługiwane pakiety przez zespół platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="65394-218">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="65394-219">Wszystkie obsługiwane pakiety przez Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="65394-219">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="65394-220">Zależności wewnętrzne i firm 3rd używane przez Entity Framework Core i ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="65394-220">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="65394-221">Aby uzyskać więcej informacji, zobacz [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span><span class="sxs-lookup"><span data-stu-id="65394-221">For more information, see [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="65394-222">Środowisko uruchomieniowe platformy .NET core a .NET Framework</span><span class="sxs-lookup"><span data-stu-id="65394-222">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="65394-223">Aplikacja platformy ASP.NET Core można kierować środowiska uruchomieniowego .NET Core lub .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="65394-223">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="65394-224">Aby uzyskać więcej informacji, zobacz [wybór między .NET Core i .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="65394-224">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="65394-225">Wybór między usługą platformy ASP.NET Core i ASP.NET</span><span class="sxs-lookup"><span data-stu-id="65394-225">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="65394-226">Aby uzyskać więcej informacji dotyczących wybierania pomiędzy platformy ASP.NET Core i ASP.NET, zobacz [wybór między platformy ASP.NET Core i ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span><span class="sxs-lookup"><span data-stu-id="65394-226">For more information on choosing between ASP.NET Core and ASP.NET, see [Choose between ASP.NET Core and ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span></span>