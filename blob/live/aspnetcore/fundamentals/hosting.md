---
title: Hosting w platformy ASP.NET Core
author: guardrex
description: "Więcej informacji na temat hosta sieci web w ASP.NET Core, która jest odpowiedzialna za uruchamianie i okresem istnienia zarządzania aplikacjami."
ms.author: riande
manager: wpickett
ms.date: 09/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/hosting
ms.openlocfilehash: 7f6712073002b73ca4ddd7586718c81e62cacbc2
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="hosting-in-aspnet-core"></a><span data-ttu-id="49624-103">Hosting w platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="49624-103">Hosting in ASP.NET Core</span></span>

<span data-ttu-id="49624-104">Przez [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="49624-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="49624-105">Aplikacje platformy ASP.NET Core skonfigurować i uruchomić *hosta*.</span><span class="sxs-lookup"><span data-stu-id="49624-105">ASP.NET Core apps configure and launch a *host*.</span></span> <span data-ttu-id="49624-106">Host jest odpowiedzialny za zarządzanie uruchamiania i okresem istnienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-106">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="49624-107">Co najmniej hosta konfiguruje serwer i potoku przetwarzania żądań.</span><span class="sxs-lookup"><span data-stu-id="49624-107">At a minimum, the host configures a server and a request processing pipeline.</span></span>

## <a name="setting-up-a-host"></a><span data-ttu-id="49624-108">Konfigurowanie hosta</span><span class="sxs-lookup"><span data-stu-id="49624-108">Setting up a host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-109">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="49624-110">Utwórz hosta za pomocą wystąpienia [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="49624-110">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="49624-111">Jest to najczęściej wykonywane w punkcie wejścia aplikacji, `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="49624-111">This is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="49624-112">W szablonach projektu `Main` znajduje się w *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="49624-112">In the project templates, `Main` is located in *Program.cs*.</span></span> <span data-ttu-id="49624-113">Typowe *Program.cs* wywołania [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) do rozpoczęcia konfigurowania hosta:</span><span class="sxs-lookup"><span data-stu-id="49624-113">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to start setting up a host:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1DotNetCore2.0App/Program.cs?name=snippet_Main)]

<span data-ttu-id="49624-114">`CreateDefaultBuilder`wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="49624-114">`CreateDefaultBuilder` performs the following tasks:</span></span>

* <span data-ttu-id="49624-115">Konfiguruje [Kestrel](servers/kestrel.md) jako serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="49624-115">Configures [Kestrel](servers/kestrel.md) as the web server.</span></span> <span data-ttu-id="49624-116">Aby Kestrel domyślnych opcji, zobacz [Kestrel opcje sekcji Kestrel implementacja serwera sieci web platformy ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span><span class="sxs-lookup"><span data-stu-id="49624-116">For the Kestrel default options, see [the Kestrel options section of Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel#kestrel-options).</span></span>
* <span data-ttu-id="49624-117">Ustawia głównego zawartości w ścieżce zwracanej przez [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span><span class="sxs-lookup"><span data-stu-id="49624-117">Sets the content root to the path returned by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory).</span></span>
* <span data-ttu-id="49624-118">Konfiguracja opcjonalna obciążeń z:</span><span class="sxs-lookup"><span data-stu-id="49624-118">Loads optional configuration from:</span></span>
  * <span data-ttu-id="49624-119">*appsettings.json*.</span><span class="sxs-lookup"><span data-stu-id="49624-119">*appsettings.json*.</span></span>
  * <span data-ttu-id="49624-120">*appsettings.{Environment}.json*.</span><span class="sxs-lookup"><span data-stu-id="49624-120">*appsettings.{Environment}.json*.</span></span>
  * <span data-ttu-id="49624-121">[Klucze tajne użytkownika](xref:security/app-secrets) po uruchomieniu aplikacji `Development` środowiska.</span><span class="sxs-lookup"><span data-stu-id="49624-121">[User secrets](xref:security/app-secrets) when the app runs in the `Development` environment.</span></span>
  * <span data-ttu-id="49624-122">Zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="49624-122">Environment variables.</span></span>
  * <span data-ttu-id="49624-123">Argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="49624-123">Command-line arguments.</span></span>
* <span data-ttu-id="49624-124">Konfiguruje [rejestrowanie](xref:fundamentals/logging/index) dla danych wyjściowych konsoli i debugowania.</span><span class="sxs-lookup"><span data-stu-id="49624-124">Configures [logging](xref:fundamentals/logging/index) for console and debug output.</span></span> <span data-ttu-id="49624-125">Dostęp do rejestrów uwzględniających [filtrowania dziennika](xref:fundamentals/logging/index#log-filtering) reguły określone w sekcji konfiguracji rejestrowania *appsettings.json* lub *appsettings. { Środowisko} JSON* pliku.</span><span class="sxs-lookup"><span data-stu-id="49624-125">Logging includes [log filtering](xref:fundamentals/logging/index#log-filtering) rules specified in a Logging configuration section of an *appsettings.json* or *appsettings.{Environment}.json* file.</span></span>
* <span data-ttu-id="49624-126">Podczas uruchamiania za usług IIS, umożliwia [integracji usług IIS](xref:host-and-deploy/iis/index).</span><span class="sxs-lookup"><span data-stu-id="49624-126">When running behind IIS, enables [IIS integration](xref:host-and-deploy/iis/index).</span></span> <span data-ttu-id="49624-127">Konfiguruje serwer nasłuchuje na przy użyciu portu i ścieżki bazowej [platformy ASP.NET Core modułu](xref:fundamentals/servers/aspnet-core-module).</span><span class="sxs-lookup"><span data-stu-id="49624-127">Configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="49624-128">Moduł tworzy zwrotny serwer proxy między usługami IIS a Kestrel.</span><span class="sxs-lookup"><span data-stu-id="49624-128">The module creates a reverse proxy between IIS and Kestrel.</span></span> <span data-ttu-id="49624-129">Konfiguruje również aplikacji na [przechwytywania błędy uruchamiania](#capture-startup-errors).</span><span class="sxs-lookup"><span data-stu-id="49624-129">Also configures the app to [capture startup errors](#capture-startup-errors).</span></span> <span data-ttu-id="49624-130">Dla opcji domyślnych usług IIS, zobacz [IIS opcje sekcji hosta platformy ASP.NET Core w systemie Windows z programem IIS](xref:host-and-deploy/iis/index#iis-options).</span><span class="sxs-lookup"><span data-stu-id="49624-130">For the IIS default options, see [the IIS options section of Host ASP.NET Core on Windows with IIS](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="49624-131">*Zawartości głównego* Określa, gdzie hosta wyszukuje pliki zawartości, takich jak pliki widoku MVC.</span><span class="sxs-lookup"><span data-stu-id="49624-131">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="49624-132">Po uruchomieniu aplikacji w folderze głównym projektu folderu głównego projektu jest używany jako główny zawartości.</span><span class="sxs-lookup"><span data-stu-id="49624-132">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="49624-133">Jest to wartość domyślna używana w [programu Visual Studio](https://www.visualstudio.com/) i [dotnet nowe szablony](/dotnet/core/tools/dotnet-new).</span><span class="sxs-lookup"><span data-stu-id="49624-133">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="49624-134">Aby uzyskać więcej informacji o konfiguracji aplikacji, zobacz [konfiguracji w programie ASP.NET Core](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="49624-134">For more information on app configuration, see [Configuration in ASP.NET Core](xref:fundamentals/configuration/index).</span></span>

> [!NOTE]
> <span data-ttu-id="49624-135">Alternatywą wobec przy użyciu statycznych `CreateDefaultBuilder` metody tworzenia hosta z [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) jest to obsługiwane podejście z platformy ASP.NET Core 2.x.</span><span class="sxs-lookup"><span data-stu-id="49624-135">As an alternative to using the static `CreateDefaultBuilder` method, creating a host from [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) is a supported approach with ASP.NET Core 2.x.</span></span> <span data-ttu-id="49624-136">Aby uzyskać więcej informacji zobacz kartę 1.x platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="49624-136">For more information, see the ASP.NET Core 1.x tab.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-138">Utwórz hosta za pomocą wystąpienia [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span><span class="sxs-lookup"><span data-stu-id="49624-138">Create a host using an instance of [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder).</span></span> <span data-ttu-id="49624-139">Tworzenie hosta jest zwykle wykonywany w punkcie wejścia aplikacji, `Main` metody.</span><span class="sxs-lookup"><span data-stu-id="49624-139">Creating a host is typically performed in the app's entry point, the `Main` method.</span></span> <span data-ttu-id="49624-140">W szablonach projektu `Main` znajduje się w *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="49624-140">In the project templates, `Main` is located in *Program.cs*:</span></span>

[!code-csharp[Main](../common/samples/WebApplication1/Program.cs)]

<span data-ttu-id="49624-141">`WebHostBuilder`wymaga [serwera, który implementuje IServer](servers/index.md).</span><span class="sxs-lookup"><span data-stu-id="49624-141">`WebHostBuilder` requires a [server that implements IServer](servers/index.md).</span></span> <span data-ttu-id="49624-142">Wbudowane serwery są [Kestrel](servers/kestrel.md) i [HTTP.sys](servers/httpsys.md) (przed wydaniem programu ASP.NET 2.0 Core została wywołana HTTP.sys [WebListener](xref:fundamentals/servers/weblistener)).</span><span class="sxs-lookup"><span data-stu-id="49624-142">The built-in servers are [Kestrel](servers/kestrel.md) and [HTTP.sys](servers/httpsys.md) (prior to the release of ASP.NET Core 2.0, HTTP.sys was called [WebListener](xref:fundamentals/servers/weblistener)).</span></span> <span data-ttu-id="49624-143">W tym przykładzie [— metoda rozszerzenia UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) Określa serwer Kestrel.</span><span class="sxs-lookup"><span data-stu-id="49624-143">In this example, the [UseKestrel extension method](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) specifies the Kestrel server.</span></span>

<span data-ttu-id="49624-144">*Zawartości głównego* Określa, gdzie hosta wyszukuje pliki zawartości, takich jak pliki widoku MVC.</span><span class="sxs-lookup"><span data-stu-id="49624-144">The *content root* determines where the host searches for content files, such as MVC view files.</span></span> <span data-ttu-id="49624-145">Domyślny element zawartości są uzyskiwane dla `UseContentRoot` przez [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span><span class="sxs-lookup"><span data-stu-id="49624-145">The default content root is obtained for `UseContentRoot` by [Directory.GetCurrentDirectory](/dotnet/api/system.io.directory.getcurrentdirectory?view=netcore-1.1).</span></span> <span data-ttu-id="49624-146">Po uruchomieniu aplikacji w folderze głównym projektu folderu głównego projektu jest używany jako główny zawartości.</span><span class="sxs-lookup"><span data-stu-id="49624-146">When the app is started from the project's root folder, the project's root folder is used as the content root.</span></span> <span data-ttu-id="49624-147">Jest to wartość domyślna używana w [programu Visual Studio](https://www.visualstudio.com/) i [dotnet nowe szablony](/dotnet/core/tools/dotnet-new).</span><span class="sxs-lookup"><span data-stu-id="49624-147">This is the default used in [Visual Studio](https://www.visualstudio.com/) and the [dotnet new templates](/dotnet/core/tools/dotnet-new).</span></span>

<span data-ttu-id="49624-148">Do używania serwera IIS jako zwrotny serwer proxy, należy wywołać [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) w ramach tworzenia hosta.</span><span class="sxs-lookup"><span data-stu-id="49624-148">To use IIS as a reverse proxy, call [UseIISIntegration](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderiisextensions) as part of building the host.</span></span> <span data-ttu-id="49624-149">`UseIISIntegration`nie Konfiguruj *serwera*, takiej jak [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) jest.</span><span class="sxs-lookup"><span data-stu-id="49624-149">`UseIISIntegration` doesn't configure a *server*, like [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) does.</span></span> <span data-ttu-id="49624-150">`UseIISIntegration`Konfiguruje serwer nasłuchuje na przy użyciu portu i ścieżki bazowej [moduł platformy ASP.NET Core](xref:fundamentals/servers/aspnet-core-module) utworzyć zwrotnego serwera proxy między Kestrel i IIS.</span><span class="sxs-lookup"><span data-stu-id="49624-150">`UseIISIntegration` configures the base path and port the server listens on when using the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to create a reverse proxy between Kestrel and IIS.</span></span> <span data-ttu-id="49624-151">Aby używać usług IIS z platformy ASP.NET Core `UseKestrel` i `UseIISIntegration` musi być określona.</span><span class="sxs-lookup"><span data-stu-id="49624-151">To use IIS with ASP.NET Core, `UseKestrel` and `UseIISIntegration` must be specified.</span></span> <span data-ttu-id="49624-152">`UseIISIntegration`aktywuje tylko podczas uruchamiania usług IIS lub usług IIS Express.</span><span class="sxs-lookup"><span data-stu-id="49624-152">`UseIISIntegration` only activates when running behind IIS or IIS Express.</span></span> <span data-ttu-id="49624-153">Aby uzyskać więcej informacji, zobacz [wprowadzenie do platformy ASP.NET Core modułu](xref:fundamentals/servers/aspnet-core-module) i [odwołania konfiguracji platformy ASP.NET Core modułu](xref:host-and-deploy/aspnet-core-module).</span><span class="sxs-lookup"><span data-stu-id="49624-153">For more information, see [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

<span data-ttu-id="49624-154">Minimalny wdrożenia, który konfiguruje hosta (a aplikacji platformy ASP.NET Core) obejmuje określenie serwera i konfiguracji Potok żądań aplikacji:</span><span class="sxs-lookup"><span data-stu-id="49624-154">A minimal implementation that configures a host (and an ASP.NET Core app) includes specifying a server and configuration of the app's request pipeline:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .Configure(app =>
    {
        app.Run(context => context.Response.WriteAsync("Hello World!"));
    })
    .Build();

host.Run();
```

---

<span data-ttu-id="49624-155">Podczas konfigurowania hosta, [Konfiguruj](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) i [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) można przedstawić metody.</span><span class="sxs-lookup"><span data-stu-id="49624-155">When setting up a host, [Configure](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderextensions.configure?view=aspnetcore-1.1) and [ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.configureservices?view=aspnetcore-1.1) methods can be provided.</span></span> <span data-ttu-id="49624-156">Jeśli `Startup` jest określona, muszą być zdefiniowane `Configure` metody.</span><span class="sxs-lookup"><span data-stu-id="49624-156">If a `Startup` class is specified, it must define a `Configure` method.</span></span> <span data-ttu-id="49624-157">Aby uzyskać więcej informacji, zobacz [uruchamiania aplikacji w ASP.NET Core](startup.md).</span><span class="sxs-lookup"><span data-stu-id="49624-157">For more information, see [Application Startup in ASP.NET Core](startup.md).</span></span> <span data-ttu-id="49624-158">Wiele wywołań `ConfigureServices` dołączyć do siebie.</span><span class="sxs-lookup"><span data-stu-id="49624-158">Multiple calls to `ConfigureServices` append to one another.</span></span> <span data-ttu-id="49624-159">Wiele wywołań `Configure` lub `UseStartup` na `WebHostBuilder` zastąpić poprzednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="49624-159">Multiple calls to `Configure` or `UseStartup` on the `WebHostBuilder` replace previous settings.</span></span>

## <a name="host-configuration-values"></a><span data-ttu-id="49624-160">Wartości konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="49624-160">Host configuration values</span></span>

<span data-ttu-id="49624-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) zależy od następujących metod można ustawić wartości konfiguracji hosta:</span><span class="sxs-lookup"><span data-stu-id="49624-161">[WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder) relies on the following approaches to set the host configuration values:</span></span>

* <span data-ttu-id="49624-162">Konfiguracja Konstruktora hosta, która zawiera zmienne środowiskowe w formacie `ASPNETCORE_{configurationKey}`.</span><span class="sxs-lookup"><span data-stu-id="49624-162">Host builder configuration, which includes environment variables with the format `ASPNETCORE_{configurationKey}`.</span></span> <span data-ttu-id="49624-163">Na przykład `ASPNETCORE_URLS`.</span><span class="sxs-lookup"><span data-stu-id="49624-163">For example, `ASPNETCORE_URLS`.</span></span>
* <span data-ttu-id="49624-164">Jawne metod, takich jak `CaptureStartupErrors`.</span><span class="sxs-lookup"><span data-stu-id="49624-164">Explicit methods, such as `CaptureStartupErrors`.</span></span>
* <span data-ttu-id="49624-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) i skojarzony klucz.</span><span class="sxs-lookup"><span data-stu-id="49624-165">[UseSetting](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder.usesetting) and the associated key.</span></span> <span data-ttu-id="49624-166">Podczas ustawiania wartości z `UseSetting`, wartość jest ustawiona jako ciąg, niezależnie od typu.</span><span class="sxs-lookup"><span data-stu-id="49624-166">When setting a value with `UseSetting`, the value is set as a string regardless of the type.</span></span>

<span data-ttu-id="49624-167">Host używa jednego z tych opcji ustawia wartość ostatnio.</span><span class="sxs-lookup"><span data-stu-id="49624-167">The host uses whichever option sets a value last.</span></span> <span data-ttu-id="49624-168">Aby uzyskać więcej informacji, zobacz [konfiguracji zastąpiona](#overriding-configuration) w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="49624-168">For more information, see [Overriding configuration](#overriding-configuration) in the next section.</span></span>

### <a name="capture-startup-errors"></a><span data-ttu-id="49624-169">Przechwyć błędy uruchamiania</span><span class="sxs-lookup"><span data-stu-id="49624-169">Capture Startup Errors</span></span>

<span data-ttu-id="49624-170">To ustawienie określa przechwytywania błędy uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="49624-170">This setting controls the capture of startup errors.</span></span>

<span data-ttu-id="49624-171">**Klucz**: captureStartupErrors</span><span class="sxs-lookup"><span data-stu-id="49624-171">**Key**: captureStartupErrors</span></span>  
<span data-ttu-id="49624-172">**Typ**: *bool* (`true` lub `1`)</span><span class="sxs-lookup"><span data-stu-id="49624-172">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="49624-173">**Domyślne**: Domyślnie `false` chyba, że aplikacja jest uruchamiana z Kestrel za usług IIS, gdzie wartość domyślna to `true`.</span><span class="sxs-lookup"><span data-stu-id="49624-173">**Default**: Defaults to `false` unless the app runs with Kestrel behind IIS, where the default is `true`.</span></span>  
<span data-ttu-id="49624-174">**Ustawić za pomocą**:`CaptureStartupErrors`</span><span class="sxs-lookup"><span data-stu-id="49624-174">**Set using**: `CaptureStartupErrors`</span></span>  
<span data-ttu-id="49624-175">**Zmienna środowiskowa**:`ASPNETCORE_CAPTURESTARTUPERRORS`</span><span class="sxs-lookup"><span data-stu-id="49624-175">**Environment variable**: `ASPNETCORE_CAPTURESTARTUPERRORS`</span></span>

<span data-ttu-id="49624-176">Gdy `false`, błędy podczas wynik uruchomienia na hoście został zakończony.</span><span class="sxs-lookup"><span data-stu-id="49624-176">When `false`, errors during startup result in the host exiting.</span></span> <span data-ttu-id="49624-177">Gdy `true`, host przechwytuje wyjątków podczas uruchamiania i podejmie próbę uruchomienia serwera.</span><span class="sxs-lookup"><span data-stu-id="49624-177">When `true`, the host captures exceptions during startup and attempts to start the server.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-178">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-178">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .CaptureStartupErrors(true)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-179">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-179">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .CaptureStartupErrors(true)
    ...
```

---

### <a name="content-root"></a><span data-ttu-id="49624-180">Główny zawartości</span><span class="sxs-lookup"><span data-stu-id="49624-180">Content Root</span></span>

<span data-ttu-id="49624-181">To ustawienie określa, gdzie platformy ASP.NET Core rozpocznie się wyszukiwanie plików zawartości, np. widoków MVC.</span><span class="sxs-lookup"><span data-stu-id="49624-181">This setting determines where ASP.NET Core begins searching for content files, such as MVC views.</span></span> 

<span data-ttu-id="49624-182">**Klucz**: contentRoot</span><span class="sxs-lookup"><span data-stu-id="49624-182">**Key**: contentRoot</span></span>  
<span data-ttu-id="49624-183">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-183">**Type**: *string*</span></span>  
<span data-ttu-id="49624-184">**Domyślna**: domyślne do folderu, w którym znajduje się zestaw aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-184">**Default**: Defaults to the folder where the app assembly resides.</span></span>  
<span data-ttu-id="49624-185">**Ustawić za pomocą**:`UseContentRoot`</span><span class="sxs-lookup"><span data-stu-id="49624-185">**Set using**: `UseContentRoot`</span></span>  
<span data-ttu-id="49624-186">**Zmienna środowiskowa**:`ASPNETCORE_CONTENTROOT`</span><span class="sxs-lookup"><span data-stu-id="49624-186">**Environment variable**: `ASPNETCORE_CONTENTROOT`</span></span>

<span data-ttu-id="49624-187">Główny zawartości jest również używany jako podstawowa ścieżka dla [ustawienia sieci Web głównego](#web-root).</span><span class="sxs-lookup"><span data-stu-id="49624-187">The content root is also used as the base path for the [Web Root setting](#web-root).</span></span> <span data-ttu-id="49624-188">Jeśli ścieżka nie istnieje, host nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="49624-188">If the path doesn't exist, the host fails to start.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-189">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-189">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseContentRoot("c:\\mywebsite")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-190">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-190">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseContentRoot("c:\\mywebsite")
    ...
```

---

### <a name="detailed-errors"></a><span data-ttu-id="49624-191">Błędy szczegółowe</span><span class="sxs-lookup"><span data-stu-id="49624-191">Detailed Errors</span></span>

<span data-ttu-id="49624-192">Określa, czy szczegółowe błędy, które mają być przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="49624-192">Determines if detailed errors should be captured.</span></span>

<span data-ttu-id="49624-193">**Klucz**: detailedErrors</span><span class="sxs-lookup"><span data-stu-id="49624-193">**Key**: detailedErrors</span></span>  
<span data-ttu-id="49624-194">**Typ**: *bool* (`true` lub `1`)</span><span class="sxs-lookup"><span data-stu-id="49624-194">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="49624-195">**Domyślna**: false</span><span class="sxs-lookup"><span data-stu-id="49624-195">**Default**: false</span></span>  
<span data-ttu-id="49624-196">**Ustawić za pomocą**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="49624-196">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="49624-197">**Zmienna środowiskowa**:`ASPNETCORE_DETAILEDERRORS`</span><span class="sxs-lookup"><span data-stu-id="49624-197">**Environment variable**: `ASPNETCORE_DETAILEDERRORS`</span></span>

<span data-ttu-id="49624-198">Po włączeniu (lub gdy <a href="#environment">środowiska</a> ma ustawioną wartość `Development`), aplikacji znajdują się szczegółowe wyjątki.</span><span class="sxs-lookup"><span data-stu-id="49624-198">When enabled (or when the <a href="#environment">Environment</a> is set to `Development`), the app captures detailed exceptions.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-199">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-199">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-200">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-200">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseSetting(WebHostDefaults.DetailedErrorsKey, "true")
    ...
```

---

### <a name="environment"></a><span data-ttu-id="49624-201">Środowisko</span><span class="sxs-lookup"><span data-stu-id="49624-201">Environment</span></span>

<span data-ttu-id="49624-202">Ustawia środowisko aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-202">Sets the app's environment.</span></span>

<span data-ttu-id="49624-203">**Klucz**: środowiska</span><span class="sxs-lookup"><span data-stu-id="49624-203">**Key**: environment</span></span>  
<span data-ttu-id="49624-204">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-204">**Type**: *string*</span></span>  
<span data-ttu-id="49624-205">**Domyślna**: produkcji</span><span class="sxs-lookup"><span data-stu-id="49624-205">**Default**: Production</span></span>  
<span data-ttu-id="49624-206">**Ustawić za pomocą**:`UseEnvironment`</span><span class="sxs-lookup"><span data-stu-id="49624-206">**Set using**: `UseEnvironment`</span></span>  
<span data-ttu-id="49624-207">**Zmienna środowiskowa**:`ASPNETCORE_ENVIRONMENT`</span><span class="sxs-lookup"><span data-stu-id="49624-207">**Environment variable**: `ASPNETCORE_ENVIRONMENT`</span></span>

<span data-ttu-id="49624-208">Środowisko można ustawić dowolną wartość.</span><span class="sxs-lookup"><span data-stu-id="49624-208">The environment can be set to any value.</span></span> <span data-ttu-id="49624-209">Wartości zdefiniowane w ramach obejmują `Development`, `Staging`, i `Production`.</span><span class="sxs-lookup"><span data-stu-id="49624-209">Framework-defined values include `Development`, `Staging`, and `Production`.</span></span> <span data-ttu-id="49624-210">Wartości nie jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="49624-210">Values aren't case sensitive.</span></span> <span data-ttu-id="49624-211">Domyślnie *środowiska* są odczytywane z `ASPNETCORE_ENVIRONMENT` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="49624-211">By default, the *Environment* is read from the `ASPNETCORE_ENVIRONMENT` environment variable.</span></span> <span data-ttu-id="49624-212">Korzystając z [programu Visual Studio](https://www.visualstudio.com/), zmienne środowiskowe może być ustawiona w *launchSettings.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="49624-212">When using [Visual Studio](https://www.visualstudio.com/), environment variables may be set in the *launchSettings.json* file.</span></span> <span data-ttu-id="49624-213">Aby uzyskać więcej informacji, zobacz [Praca w środowiskach wielu](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="49624-213">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-214">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-214">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseEnvironment("Development")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-215">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-215">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseEnvironment("Development")
    ...
```

---

### <a name="hosting-startup-assemblies"></a><span data-ttu-id="49624-216">Zestawy uruchomienia hostingu</span><span class="sxs-lookup"><span data-stu-id="49624-216">Hosting Startup Assemblies</span></span>

<span data-ttu-id="49624-217">Ustawia hostingu zestawy uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-217">Sets the app's hosting startup assemblies.</span></span>

<span data-ttu-id="49624-218">**Klucz**: hostingStartupAssemblies</span><span class="sxs-lookup"><span data-stu-id="49624-218">**Key**: hostingStartupAssemblies</span></span>  
<span data-ttu-id="49624-219">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-219">**Type**: *string*</span></span>  
<span data-ttu-id="49624-220">**Domyślna**: pusty ciąg</span><span class="sxs-lookup"><span data-stu-id="49624-220">**Default**: Empty string</span></span>  
<span data-ttu-id="49624-221">**Ustawić za pomocą**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="49624-221">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="49624-222">**Zmienna środowiskowa**:`ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span><span class="sxs-lookup"><span data-stu-id="49624-222">**Environment variable**: `ASPNETCORE_HOSTINGSTARTUPASSEMBLIES`</span></span>

<span data-ttu-id="49624-223">Ciąg rozdzielany średnikami obsługi zestawów uruchamiania załadować podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="49624-223">A semicolon-delimited string of hosting startup assemblies to load on startup.</span></span> <span data-ttu-id="49624-224">Ta funkcja jest nowa w programie ASP.NET 2.0 Core.</span><span class="sxs-lookup"><span data-stu-id="49624-224">This feature is new in ASP.NET Core 2.0.</span></span>

<span data-ttu-id="49624-225">Mimo że konfiguracja domyślnie przyjmowana jest wartość pustego ciągu, hostingu zestawy uruchamiania zawsze należy uwzględniać zestawu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-225">Although the configuration value defaults to an empty string, the hosting startup assemblies always include the app's assembly.</span></span> <span data-ttu-id="49624-226">Jeśli zostały podane zestawy uruchomienia hostingu, są one dodane do zestawu aplikacji ładowania, gdy aplikacja tworzy jego wspólne usługi podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="49624-226">When hosting startup assemblies are provided, they're added to the app's assembly for loading when the app builds its common services during startup.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-227">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.HostingStartupAssembliesKey, "assembly1;assembly2")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-228">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-228">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-229">Ta funkcja jest niedostępna w ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="49624-229">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prefer-hosting-urls"></a><span data-ttu-id="49624-230">Preferowane jest Hosting adresy URL</span><span class="sxs-lookup"><span data-stu-id="49624-230">Prefer Hosting URLs</span></span>

<span data-ttu-id="49624-231">Wskazuje, czy host powinien nasłuchiwać adresy URL skonfigurowano `WebHostBuilder` zamiast ustawień skonfigurowanych z `IServer` implementacji.</span><span class="sxs-lookup"><span data-stu-id="49624-231">Indicates whether the host should listen on the URLs configured with the `WebHostBuilder` instead of those configured with the `IServer` implementation.</span></span>

<span data-ttu-id="49624-232">**Klucz**: preferHostingUrls</span><span class="sxs-lookup"><span data-stu-id="49624-232">**Key**: preferHostingUrls</span></span>  
<span data-ttu-id="49624-233">**Typ**: *bool* (`true` lub `1`)</span><span class="sxs-lookup"><span data-stu-id="49624-233">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="49624-234">**Domyślna**: true</span><span class="sxs-lookup"><span data-stu-id="49624-234">**Default**: true</span></span>  
<span data-ttu-id="49624-235">**Ustawić za pomocą**:`PreferHostingUrls`</span><span class="sxs-lookup"><span data-stu-id="49624-235">**Set using**: `PreferHostingUrls`</span></span>  
<span data-ttu-id="49624-236">**Zmienna środowiskowa**:`ASPNETCORE_PREFERHOSTINGURLS`</span><span class="sxs-lookup"><span data-stu-id="49624-236">**Environment variable**: `ASPNETCORE_PREFERHOSTINGURLS`</span></span>

<span data-ttu-id="49624-237">Ta funkcja jest nowa w programie ASP.NET 2.0 Core.</span><span class="sxs-lookup"><span data-stu-id="49624-237">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-238">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-238">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .PreferHostingUrls(false)
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-239">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-239">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-240">Ta funkcja jest niedostępna w ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="49624-240">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="prevent-hosting-startup"></a><span data-ttu-id="49624-241">Zapobiegaj Hosting uruchamiania</span><span class="sxs-lookup"><span data-stu-id="49624-241">Prevent Hosting Startup</span></span>

<span data-ttu-id="49624-242">Uniemożliwia automatyczne ładowanie hosting zestawy uruchamiania, tym hosting zestawy uruchamiania konfigurowane za pomocą zestawu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-242">Prevents the automatic loading of hosting startup assemblies, including hosting startup assemblies configured by the app's assembly.</span></span> <span data-ttu-id="49624-243">Zobacz [dodać aplikacji funkcje z zewnętrznych zestawu za pomocą IHostingStartup](xref:host-and-deploy/ihostingstartup) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="49624-243">See [Add app features from an external assembly using IHostingStartup](xref:host-and-deploy/ihostingstartup) for more information.</span></span>

<span data-ttu-id="49624-244">**Klucz**: preventHostingStartup</span><span class="sxs-lookup"><span data-stu-id="49624-244">**Key**: preventHostingStartup</span></span>  
<span data-ttu-id="49624-245">**Typ**: *bool* (`true` lub `1`)</span><span class="sxs-lookup"><span data-stu-id="49624-245">**Type**: *bool* (`true` or `1`)</span></span>  
<span data-ttu-id="49624-246">**Domyślna**: false</span><span class="sxs-lookup"><span data-stu-id="49624-246">**Default**: false</span></span>  
<span data-ttu-id="49624-247">**Ustawić za pomocą**:`UseSetting`</span><span class="sxs-lookup"><span data-stu-id="49624-247">**Set using**: `UseSetting`</span></span>  
<span data-ttu-id="49624-248">**Zmienna środowiskowa**:`ASPNETCORE_PREVENTHOSTINGSTARTUP`</span><span class="sxs-lookup"><span data-stu-id="49624-248">**Environment variable**: `ASPNETCORE_PREVENTHOSTINGSTARTUP`</span></span>

<span data-ttu-id="49624-249">Ta funkcja jest nowa w programie ASP.NET 2.0 Core.</span><span class="sxs-lookup"><span data-stu-id="49624-249">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-250">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-250">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting(WebHostDefaults.PreventHostingStartupKey, "true")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-251">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-251">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-252">Ta funkcja jest niedostępna w ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="49624-252">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="server-urls"></a><span data-ttu-id="49624-253">Adresy URL serwerów</span><span class="sxs-lookup"><span data-stu-id="49624-253">Server URLs</span></span>

<span data-ttu-id="49624-254">Wskazuje adresy IP lub adresy hostów, porty i protokoły, które serwer powinien nasłuchiwać żądań.</span><span class="sxs-lookup"><span data-stu-id="49624-254">Indicates the IP addresses or host addresses with ports and protocols that the server should listen on for requests.</span></span>

<span data-ttu-id="49624-255">**Klucz**: adresy URL</span><span class="sxs-lookup"><span data-stu-id="49624-255">**Key**: urls</span></span>  
<span data-ttu-id="49624-256">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-256">**Type**: *string*</span></span>  
<span data-ttu-id="49624-257">**Domyślna**: http://localhost: 5000</span><span class="sxs-lookup"><span data-stu-id="49624-257">**Default**: http://localhost:5000</span></span>  
<span data-ttu-id="49624-258">**Ustawić za pomocą**:`UseUrls`</span><span class="sxs-lookup"><span data-stu-id="49624-258">**Set using**: `UseUrls`</span></span>  
<span data-ttu-id="49624-259">**Zmienna środowiskowa**:`ASPNETCORE_URLS`</span><span class="sxs-lookup"><span data-stu-id="49624-259">**Environment variable**: `ASPNETCORE_URLS`</span></span>

<span data-ttu-id="49624-260">Ustaw rozdzielonych średnikami (;) lista adresów URL prefiksy powinny odpowiadać serwera.</span><span class="sxs-lookup"><span data-stu-id="49624-260">Set to a semicolon-separated (;) list of URL prefixes to which the server should respond.</span></span> <span data-ttu-id="49624-261">Na przykład `http://localhost:123`.</span><span class="sxs-lookup"><span data-stu-id="49624-261">For example, `http://localhost:123`.</span></span> <span data-ttu-id="49624-262">Użyj "\*" Aby wskazać, że serwer powinien nasłuchiwać żądań adresy IP lub nazwa hosta przy użyciu określonego portu i protokołu (na przykład `http://*:5000`).</span><span class="sxs-lookup"><span data-stu-id="49624-262">Use "\*" to indicate that the server should listen for requests on any IP address or hostname using the specified port and protocol (for example, `http://*:5000`).</span></span> <span data-ttu-id="49624-263">Protokół (`http://` lub `https://`) musi być dołączony do każdego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="49624-263">The protocol (`http://` or `https://`) must be included with each URL.</span></span> <span data-ttu-id="49624-264">Obsługiwane formaty różnią się między serwerami.</span><span class="sxs-lookup"><span data-stu-id="49624-264">Supported formats vary between servers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-265">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-265">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

<span data-ttu-id="49624-266">Kestrel ma własny interfejs API konfiguracji punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="49624-266">Kestrel has its own endpoint configuration API.</span></span> <span data-ttu-id="49624-267">Aby uzyskać więcej informacji, zobacz [Kestrel implementacja serwera sieci web platformy ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span><span class="sxs-lookup"><span data-stu-id="49624-267">For more information, see [Kestrel web server implementation in ASP.NET Core](xref:fundamentals/servers/kestrel?tabs=aspnetcore2x#endpoint-configuration).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-268">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-268">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseUrls("http://*:5000;http://localhost:5001;https://hostname:5002")
    ...
```

---

### <a name="shutdown-timeout"></a><span data-ttu-id="49624-269">Limit czasu zamykania</span><span class="sxs-lookup"><span data-stu-id="49624-269">Shutdown Timeout</span></span>

<span data-ttu-id="49624-270">Określa czas oczekiwania na zamknięcie hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="49624-270">Specifies the amount of time to wait for the web host to shutdown.</span></span>

<span data-ttu-id="49624-271">**Klucz**: shutdownTimeoutSeconds</span><span class="sxs-lookup"><span data-stu-id="49624-271">**Key**: shutdownTimeoutSeconds</span></span>  
<span data-ttu-id="49624-272">**Typ**: *int*</span><span class="sxs-lookup"><span data-stu-id="49624-272">**Type**: *int*</span></span>  
<span data-ttu-id="49624-273">**Domyślna**: 5</span><span class="sxs-lookup"><span data-stu-id="49624-273">**Default**: 5</span></span>  
<span data-ttu-id="49624-274">**Ustawić za pomocą**:`UseShutdownTimeout`</span><span class="sxs-lookup"><span data-stu-id="49624-274">**Set using**: `UseShutdownTimeout`</span></span>  
<span data-ttu-id="49624-275">**Zmienna środowiskowa**:`ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span><span class="sxs-lookup"><span data-stu-id="49624-275">**Environment variable**: `ASPNETCORE_SHUTDOWNTIMEOUTSECONDS`</span></span>

<span data-ttu-id="49624-276">Mimo że akceptuje klucz *int* z `UseSetting` (na przykład `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), `UseShutdownTimeout` przyjmuje — metoda rozszerzenia `TimeSpan`.</span><span class="sxs-lookup"><span data-stu-id="49624-276">Although the key accepts an *int* with `UseSetting` (for example, `.UseSetting(WebHostDefaults.ShutdownTimeoutKey, "10")`), the `UseShutdownTimeout` extension method takes a `TimeSpan`.</span></span> <span data-ttu-id="49624-277">Ta funkcja jest nowa w programie ASP.NET 2.0 Core.</span><span class="sxs-lookup"><span data-stu-id="49624-277">This feature is new in ASP.NET Core 2.0.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-278">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-278">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseShutdownTimeout(TimeSpan.FromSeconds(10))
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-279">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-279">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-280">Ta funkcja jest niedostępna w ASP.NET Core 1.x.</span><span class="sxs-lookup"><span data-stu-id="49624-280">This feature is unavailable in ASP.NET Core 1.x.</span></span>

---

### <a name="startup-assembly"></a><span data-ttu-id="49624-281">Zestaw startowy</span><span class="sxs-lookup"><span data-stu-id="49624-281">Startup Assembly</span></span>

<span data-ttu-id="49624-282">Określa zestaw do wyszukania `Startup` klasy.</span><span class="sxs-lookup"><span data-stu-id="49624-282">Determines the assembly to search for the `Startup` class.</span></span>

<span data-ttu-id="49624-283">**Klucz**: startupAssembly</span><span class="sxs-lookup"><span data-stu-id="49624-283">**Key**: startupAssembly</span></span>  
<span data-ttu-id="49624-284">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-284">**Type**: *string*</span></span>  
<span data-ttu-id="49624-285">**Domyślna**: zestaw aplikacji</span><span class="sxs-lookup"><span data-stu-id="49624-285">**Default**: The app's assembly</span></span>  
<span data-ttu-id="49624-286">**Ustawić za pomocą**:`UseStartup`</span><span class="sxs-lookup"><span data-stu-id="49624-286">**Set using**: `UseStartup`</span></span>  
<span data-ttu-id="49624-287">**Zmienna środowiskowa**:`ASPNETCORE_STARTUPASSEMBLY`</span><span class="sxs-lookup"><span data-stu-id="49624-287">**Environment variable**: `ASPNETCORE_STARTUPASSEMBLY`</span></span>

<span data-ttu-id="49624-288">Zestaw o nazwie (`string`) lub typu (`TStartup`) można odwoływać się.</span><span class="sxs-lookup"><span data-stu-id="49624-288">The assembly by name (`string`) or type (`TStartup`) can be referenced.</span></span> <span data-ttu-id="49624-289">Jeśli wiele `UseStartup` metody są nazywane, pierwszeństwo ma ostatnią.</span><span class="sxs-lookup"><span data-stu-id="49624-289">If multiple `UseStartup` methods are called, the last one takes precedence.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-290">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-290">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseStartup<TStartup>()
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-291">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-291">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseStartup("StartupAssemblyName")
    ...
```

```csharp
var host = new WebHostBuilder()
    .UseStartup<TStartup>()
    ...
```

---

### <a name="web-root"></a><span data-ttu-id="49624-292">Główny sieci Web</span><span class="sxs-lookup"><span data-stu-id="49624-292">Web Root</span></span>

<span data-ttu-id="49624-293">Ustawia ścieżkę względną do statycznego zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-293">Sets the relative path to the app's static assets.</span></span>

<span data-ttu-id="49624-294">**Klucz**: webroot</span><span class="sxs-lookup"><span data-stu-id="49624-294">**Key**: webroot</span></span>  
<span data-ttu-id="49624-295">**Typ**: *ciągu*</span><span class="sxs-lookup"><span data-stu-id="49624-295">**Type**: *string*</span></span>  
<span data-ttu-id="49624-296">**Domyślne**: Jeśli nie jest określony, wartością domyślną jest "(Content Root)/wwwroot", jeśli ścieżka istnieje.</span><span class="sxs-lookup"><span data-stu-id="49624-296">**Default**: If not specified, the default is "(Content Root)/wwwroot", if the path exists.</span></span> <span data-ttu-id="49624-297">Jeśli ścieżka nie istnieje, jest używany dostawca pliku zerowa.</span><span class="sxs-lookup"><span data-stu-id="49624-297">If the path doesn't exist, then a no-op file provider is used.</span></span>  
<span data-ttu-id="49624-298">**Ustawić za pomocą**:`UseWebRoot`</span><span class="sxs-lookup"><span data-stu-id="49624-298">**Set using**: `UseWebRoot`</span></span>  
<span data-ttu-id="49624-299">**Zmienna środowiskowa**:`ASPNETCORE_WEBROOT`</span><span class="sxs-lookup"><span data-stu-id="49624-299">**Environment variable**: `ASPNETCORE_WEBROOT`</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-300">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-300">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseWebRoot("public")
    ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-301">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-301">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
var host = new WebHostBuilder()
    .UseWebRoot("public")
    ...
```

---

## <a name="overriding-configuration"></a><span data-ttu-id="49624-302">Zastępowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="49624-302">Overriding configuration</span></span>

<span data-ttu-id="49624-303">Użyj [konfiguracji](xref:fundamentals/configuration/index) Aby skonfigurować hosta.</span><span class="sxs-lookup"><span data-stu-id="49624-303">Use [Configuration](xref:fundamentals/configuration/index) to configure the host.</span></span> <span data-ttu-id="49624-304">W poniższym przykładzie konfiguracja hosta jest opcjonalnie określić w *hosting.json* pliku.</span><span class="sxs-lookup"><span data-stu-id="49624-304">In the following example, host configuration is optionally specified in a *hosting.json* file.</span></span> <span data-ttu-id="49624-305">Wszelkie konfiguracja została załadowana z *hosting.json* plik może być zastąpiona przez argumenty wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="49624-305">Any configuration loaded from the *hosting.json* file may be overridden by command-line arguments.</span></span> <span data-ttu-id="49624-306">Zbudowany konfiguracji (w `config`) służy do konfigurowania hosta z `UseConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="49624-306">The built configuration (in `config`) is used to configure the host with `UseConfiguration`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-307">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-307">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="49624-308">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="49624-308">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="49624-309">Zastępowanie konfiguracji dostarczonych przez `UseUrls` z *hosting.json* config argument pierwszą, wiersza polecenia config drugi:</span><span class="sxs-lookup"><span data-stu-id="49624-309">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        BuildWebHost(args).Run();
    }

    public static IWebHost BuildWebHost(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();
    }
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-310">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-310">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-311">*hosting.json*:</span><span class="sxs-lookup"><span data-stu-id="49624-311">*hosting.json*:</span></span>

```json
{
    urls: "http://*:5005"
}
```

<span data-ttu-id="49624-312">Zastępowanie konfiguracji dostarczonych przez `UseUrls` z *hosting.json* config argument pierwszą, wiersza polecenia config drugi:</span><span class="sxs-lookup"><span data-stu-id="49624-312">Overriding the configuration provided by `UseUrls` with *hosting.json* config first, command-line argument config second:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("hosting.json", optional: true)
            .AddCommandLine(args)
            .Build();

        var host = new WebHostBuilder()
            .UseUrls("http://*:5000")
            .UseConfiguration(config)
            .UseKestrel()
            .Configure(app =>
            {
                app.Run(context => 
                    context.Response.WriteAsync("Hello, World!"));
            })
            .Build();

        host.Run();
    }
}
```

---

> [!NOTE]
> <span data-ttu-id="49624-313">[UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) — metoda rozszerzenia nie jest obecnie stanie podczas analizowania sekcji konfiguracji zwrócony przez `GetSection` (na przykład `.UseConfiguration(Configuration.GetSection("section"))`.</span><span class="sxs-lookup"><span data-stu-id="49624-313">The [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) extension method isn't currently capable of parsing a configuration section returned by `GetSection` (for example, `.UseConfiguration(Configuration.GetSection("section"))`.</span></span> <span data-ttu-id="49624-314">`GetSection` — Metoda filtruje klucze konfiguracji do sekcji żądanie, jednak nie pozostawia nazwy sekcji kluczy (na przykład `section:urls`, `section:environment`).</span><span class="sxs-lookup"><span data-stu-id="49624-314">The `GetSection` method filters the configuration keys to the section requested but leaves the section name on the keys (for example, `section:urls`, `section:environment`).</span></span> <span data-ttu-id="49624-315">`UseConfiguration` Metoda oczekuje klucze do dopasowania `WebHostBuilder` kluczy (na przykład `urls`, `environment`).</span><span class="sxs-lookup"><span data-stu-id="49624-315">The `UseConfiguration` method expects the keys to match the `WebHostBuilder` keys (for example, `urls`, `environment`).</span></span> <span data-ttu-id="49624-316">Występowanie nazwy sekcji kluczy uniemożliwia wartości w sekcji Konfigurowanie hosta.</span><span class="sxs-lookup"><span data-stu-id="49624-316">The presence of the section name on the keys prevents the section's values from configuring the host.</span></span> <span data-ttu-id="49624-317">Ten problem zostanie rozwiązany w kolejnej wersji.</span><span class="sxs-lookup"><span data-stu-id="49624-317">This issue will be addressed in an upcoming release.</span></span> <span data-ttu-id="49624-318">Aby uzyskać więcej informacji i rozwiązania problemu, zobacz [przekazywanie Sekcja konfiguracyjna do WebHostBuilder.UseConfiguration używa kluczy pełna](https://github.com/aspnet/Hosting/issues/839).</span><span class="sxs-lookup"><span data-stu-id="49624-318">For more information and workarounds, see [Passing configuration section into WebHostBuilder.UseConfiguration uses full keys](https://github.com/aspnet/Hosting/issues/839).</span></span>

<span data-ttu-id="49624-319">Aby określić hosta, uruchom na określony adres URL, żądaną wartość mogą zostać przekazane w wierszu polecenia z podczas wykonywania `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="49624-319">To specify the host run on a particular URL, the desired value can be passed in from a command prompt when executing `dotnet run`.</span></span> <span data-ttu-id="49624-320">Argument wiersza polecenia zastępuje `urls` wartość z *hosting.json* pliku, a serwer nasłuchuje na porcie 8080:</span><span class="sxs-lookup"><span data-stu-id="49624-320">The command-line argument overrides the `urls` value from the *hosting.json* file, and the server listens on port 8080:</span></span>

```console
dotnet run --urls "http://*:8080"
```

## <a name="starting-the-host"></a><span data-ttu-id="49624-321">Uruchamianie hosta</span><span class="sxs-lookup"><span data-stu-id="49624-321">Starting the host</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="49624-322">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="49624-322">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="49624-323">**Uruchom**</span><span class="sxs-lookup"><span data-stu-id="49624-323">**Run**</span></span>

<span data-ttu-id="49624-324">`Run` Metoda uruchamiania aplikacji sieci web i blokuje wątek wywołujący do czasu zamknięcia hosta:</span><span class="sxs-lookup"><span data-stu-id="49624-324">The `Run` method starts the web app and blocks the calling thread until the host is shutdown:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="49624-325">**Start**</span><span class="sxs-lookup"><span data-stu-id="49624-325">**Start**</span></span>

<span data-ttu-id="49624-326">Uruchom hosta w sposób nieblokujące przez wywołanie jego `Start` metody:</span><span class="sxs-lookup"><span data-stu-id="49624-326">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="49624-327">Jeśli listę adresów URL są przekazywane do `Start` metody go nasłuchuje na określone adresy URL:</span><span class="sxs-lookup"><span data-stu-id="49624-327">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>

```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

<span data-ttu-id="49624-328">Inicjowanie i uruchomić nowy host, przy użyciu wstępnie skonfigurowane ustawienia domyślne aplikacji `CreateDefaultBuilder` przy użyciu metody statycznej wygody.</span><span class="sxs-lookup"><span data-stu-id="49624-328">The app can initialize and start a new host using the pre-configured defaults of `CreateDefaultBuilder` using a static convenience method.</span></span> <span data-ttu-id="49624-329">Te metody uruchomienia serwera bez dane wyjściowe konsoli i z [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) poczekaj, aż podział (Ctrl-C/sigint — lub sigterm —):</span><span class="sxs-lookup"><span data-stu-id="49624-329">These methods start the server without console output and with [WaitForShutdown](/dotnet/api/microsoft.aspnetcore.hosting.webhostextensions.waitforshutdown) wait for a break (Ctrl-C/SIGINT or SIGTERM):</span></span>

<span data-ttu-id="49624-330">**Start (RequestDelegate aplikacji)**</span><span class="sxs-lookup"><span data-stu-id="49624-330">**Start(RequestDelegate app)**</span></span>

<span data-ttu-id="49624-331">Rozpoczynać `RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="49624-331">Start with a `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start(app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-332">Tworzenie żądania w przeglądarce, aby `http://localhost:5000` odpowiedź "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="49624-332">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="49624-333">`WaitForShutdown`bloki aż do wystawienia podział (Ctrl-C/sigint — lub sigterm —).</span><span class="sxs-lookup"><span data-stu-id="49624-333">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="49624-334">Aplikacja jest wyświetlana `Console.WriteLine` komunikat i czeka na keypress zakończyć.</span><span class="sxs-lookup"><span data-stu-id="49624-334">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="49624-335">**Start (ciąg adresu url, RequestDelegate aplikacji)**</span><span class="sxs-lookup"><span data-stu-id="49624-335">**Start(string url, RequestDelegate app)**</span></span>

<span data-ttu-id="49624-336">Uruchom przy użyciu adresu URL i `RequestDelegate`:</span><span class="sxs-lookup"><span data-stu-id="49624-336">Start with a URL and `RequestDelegate`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", app => app.Response.WriteAsync("Hello, World!")))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-337">Tworzy wynik, w postaci **Start (aplikacja RequestDelegate)**, z wyjątkiem aplikacji odpowiada na `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="49624-337">Produces the same result as **Start(RequestDelegate app)**, except the app responds on `http://localhost:8080`.</span></span>

<span data-ttu-id="49624-338">**Start (akcji<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="49624-338">**Start(Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="49624-339">Użyj wystąpienia `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) do używania oprogramowania pośredniczącego routingu:</span><span class="sxs-lookup"><span data-stu-id="49624-339">Use an instance of `IRouteBuilder` ([Microsoft.AspNetCore.Routing](https://www.nuget.org/packages/Microsoft.AspNetCore.Routing/)) to use routing middleware:</span></span>

```csharp
using (var host = WebHost.Start(router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-340">Użyj następujących żądań przeglądarki z przykładem:</span><span class="sxs-lookup"><span data-stu-id="49624-340">Use the following browser requests with the example:</span></span>

| <span data-ttu-id="49624-341">Żądanie</span><span class="sxs-lookup"><span data-stu-id="49624-341">Request</span></span>                                    | <span data-ttu-id="49624-342">Odpowiedź</span><span class="sxs-lookup"><span data-stu-id="49624-342">Response</span></span>                                 |
| ------------------------------------------ | ---------------------------------------- |
| `http://localhost:5000/hello/Martin`       | <span data-ttu-id="49624-343">Witaj, pole!</span><span class="sxs-lookup"><span data-stu-id="49624-343">Hello, Martin!</span></span>                           |
| `http://localhost:5000/buenosdias/Catrina` | <span data-ttu-id="49624-344">Buenos dias, Catrina!</span><span class="sxs-lookup"><span data-stu-id="49624-344">Buenos dias, Catrina!</span></span>                    |
| `http://localhost:5000/throw/ooops!`       | <span data-ttu-id="49624-345">Zgłasza wyjątek z ciągiem "ooops!"</span><span class="sxs-lookup"><span data-stu-id="49624-345">Throws an exception with string "ooops!"</span></span> |
| `http://localhost:5000/throw`              | <span data-ttu-id="49624-346">Zgłasza wyjątek z ciągiem "Uh Niestety!"</span><span class="sxs-lookup"><span data-stu-id="49624-346">Throws an exception with string "Uh oh!"</span></span> |
| `http://localhost:5000/Sante/Kevin`        | <span data-ttu-id="49624-347">Sante, Jan!</span><span class="sxs-lookup"><span data-stu-id="49624-347">Sante, Kevin!</span></span>                            |
| `http://localhost:5000`                    | <span data-ttu-id="49624-348">Cześć ludzie!</span><span class="sxs-lookup"><span data-stu-id="49624-348">Hello World!</span></span>                             |

<span data-ttu-id="49624-349">`WaitForShutdown`bloki aż do wystawienia podział (Ctrl-C/sigint — lub sigterm —).</span><span class="sxs-lookup"><span data-stu-id="49624-349">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="49624-350">Aplikacja jest wyświetlana `Console.WriteLine` komunikat i czeka na keypress zakończyć.</span><span class="sxs-lookup"><span data-stu-id="49624-350">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="49624-351">**Start (ciągu adresu url, Akcja<IRouteBuilder> routeBuilder)**</span><span class="sxs-lookup"><span data-stu-id="49624-351">**Start(string url, Action<IRouteBuilder> routeBuilder)**</span></span>

<span data-ttu-id="49624-352">Użyj adresu URL i wystąpienie `IRouteBuilder`:</span><span class="sxs-lookup"><span data-stu-id="49624-352">Use a URL and an instance of `IRouteBuilder`:</span></span>

```csharp
using (var host = WebHost.Start("http://localhost:8080", router => router
    .MapGet("hello/{name}", (req, res, data) => 
        res.WriteAsync($"Hello, {data.Values["name"]}!"))
    .MapGet("buenosdias/{name}", (req, res, data) => 
        res.WriteAsync($"Buenos dias, {data.Values["name"]}!"))
    .MapGet("throw/{message?}", (req, res, data) => 
        throw new Exception((string)data.Values["message"] ?? "Uh oh!"))
    .MapGet("{greeting}/{name}", (req, res, data) => 
        res.WriteAsync($"{data.Values["greeting"]}, {data.Values["name"]}!"))
    .MapGet("", (req, res, data) => res.WriteAsync("Hello, World!"))))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-353">Tworzy wynik, w postaci **Start (akcji<IRouteBuilder> routeBuilder)**, z wyjątkiem aplikacji odpowiada na `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="49624-353">Produces the same result as **Start(Action<IRouteBuilder> routeBuilder)**, except the app responds at `http://localhost:8080`.</span></span>

<span data-ttu-id="49624-354">**StartWith (akcji<IApplicationBuilder> aplikacji)**</span><span class="sxs-lookup"><span data-stu-id="49624-354">**StartWith(Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="49624-355">Podaj delegat konfigurujący `IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="49624-355">Provide a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith(app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-356">Tworzenie żądania w przeglądarce, aby `http://localhost:5000` odpowiedź "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="49624-356">Make a request in the browser to `http://localhost:5000` to receive the response "Hello World!"</span></span> <span data-ttu-id="49624-357">`WaitForShutdown`bloki aż do wystawienia podział (Ctrl-C/sigint — lub sigterm —).</span><span class="sxs-lookup"><span data-stu-id="49624-357">`WaitForShutdown` blocks until a break (Ctrl-C/SIGINT or SIGTERM) is issued.</span></span> <span data-ttu-id="49624-358">Aplikacja jest wyświetlana `Console.WriteLine` komunikat i czeka na keypress zakończyć.</span><span class="sxs-lookup"><span data-stu-id="49624-358">The app displays the `Console.WriteLine` message and waits for a keypress to exit.</span></span>

<span data-ttu-id="49624-359">**StartWith (ciągu adresu url, Akcja<IApplicationBuilder> aplikacji)**</span><span class="sxs-lookup"><span data-stu-id="49624-359">**StartWith(string url, Action<IApplicationBuilder> app)**</span></span>

<span data-ttu-id="49624-360">Podaj adres URL i delegat konfigurujący `IApplicationBuilder`:</span><span class="sxs-lookup"><span data-stu-id="49624-360">Provide a URL and a delegate to configure an `IApplicationBuilder`:</span></span>

```csharp
using (var host = WebHost.StartWith("http://localhost:8080", app => 
    app.Use(next => 
    {
        return async context => 
        {
            await context.Response.WriteAsync("Hello World!");
        };
    })))
{
    Console.WriteLine("Use Ctrl-C to shutdown the host...");
    host.WaitForShutdown();
}
```

<span data-ttu-id="49624-361">Tworzy wynik, w postaci **StartWith (akcji<IApplicationBuilder> aplikacji)**, z wyjątkiem aplikacji odpowiada na `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="49624-361">Produces the same result as **StartWith(Action<IApplicationBuilder> app)**, except the app responds on `http://localhost:8080`.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="49624-362">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="49624-362">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="49624-363">**Uruchom**</span><span class="sxs-lookup"><span data-stu-id="49624-363">**Run**</span></span>

<span data-ttu-id="49624-364">`Run` Metoda uruchamiania aplikacji sieci web i blokuje wątek wywołujący, dopóki nie zostanie zamknięta hosta:</span><span class="sxs-lookup"><span data-stu-id="49624-364">The `Run` method starts the web app and blocks the calling thread until the host is shut down:</span></span>

```csharp
host.Run();
```

<span data-ttu-id="49624-365">**Start**</span><span class="sxs-lookup"><span data-stu-id="49624-365">**Start**</span></span>

<span data-ttu-id="49624-366">Uruchom hosta w sposób nieblokujące przez wywołanie jego `Start` metody:</span><span class="sxs-lookup"><span data-stu-id="49624-366">Run the host in a non-blocking manner by calling its `Start` method:</span></span>

```csharp
using (host)
{
    host.Start();
    Console.ReadLine();
}
```

<span data-ttu-id="49624-367">Jeśli listę adresów URL są przekazywane do `Start` metody go nasłuchuje na określone adresy URL:</span><span class="sxs-lookup"><span data-stu-id="49624-367">If a list of URLs is passed to the `Start` method, it listens on the URLs specified:</span></span>


```csharp
var urls = new List<string>()
{
    "http://*:5000",
    "http://localhost:5001"
};

var host = new WebHostBuilder()
    .UseKestrel()
    .UseStartup<Startup>()
    .Start(urls.ToArray());

using (host)
{
    Console.ReadLine();
}
```

---

## <a name="ihostingenvironment-interface"></a><span data-ttu-id="49624-368">Interfejs IHostingEnvironment</span><span class="sxs-lookup"><span data-stu-id="49624-368">IHostingEnvironment interface</span></span>

<span data-ttu-id="49624-369">[Interfejsu IHostingEnvironment](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) zawiera informacje o aplikacji sieci web środowiska macierzystego.</span><span class="sxs-lookup"><span data-stu-id="49624-369">The [IHostingEnvironment interface](/aspnet/core/api/microsoft.aspnetcore.hosting.ihostingenvironment) provides information about the app's web hosting environment.</span></span> <span data-ttu-id="49624-370">Użyj [iniekcji konstruktora](xref:fundamentals/dependency-injection) uzyskanie `IHostingEnvironment` aby można było używać ich właściwości i metody rozszerzenia:</span><span class="sxs-lookup"><span data-stu-id="49624-370">Use [constructor injection](xref:fundamentals/dependency-injection) to obtain the `IHostingEnvironment` in order to use its properties and extension methods:</span></span>

```csharp
public class CustomFileReader
{
    private readonly IHostingEnvironment _env;

    public CustomFileReader(IHostingEnvironment env)
    {
        _env = env;
    }

    public string ReadFile(string filePath)
    {
        var fileProvider = _env.WebRootFileProvider;
        // Process the file here
    }
}
```

<span data-ttu-id="49624-371">A [podejście oparte na Konwencji](xref:fundamentals/environments#startup-conventions) może służyć do konfigurowania aplikacji podczas uruchamiania, na podstawie środowiska.</span><span class="sxs-lookup"><span data-stu-id="49624-371">A [convention-based approach](xref:fundamentals/environments#startup-conventions) can be used to configure the app at startup based on the environment.</span></span> <span data-ttu-id="49624-372">Możesz też wprowadzić `IHostingEnvironment` do `Startup` konstruktora do użycia w `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="49624-372">Alternatively, inject the `IHostingEnvironment` into the `Startup` constructor for use in `ConfigureServices`:</span></span>

```csharp
public class Startup
{
    public Startup(IHostingEnvironment env)
    {
        HostingEnvironment = env;
    }

    public IHostingEnvironment HostingEnvironment { get; }

    public void ConfigureServices(IServiceCollection services)
    {
        if (HostingEnvironment.IsDevelopment())
        {
            // Development configuration
        }
        else
        {
            // Staging/Production configuration
        }

        var contentRootPath = HostingEnvironment.ContentRootPath;
    }
}
```

> [!NOTE]
> <span data-ttu-id="49624-373">Oprócz `IsDevelopment` — metoda rozszerzenia, `IHostingEnvironment` oferuje `IsStaging`, `IsProduction`, i `IsEnvironment(string environmentName)` metody.</span><span class="sxs-lookup"><span data-stu-id="49624-373">In addition to the `IsDevelopment` extension method, `IHostingEnvironment` offers `IsStaging`, `IsProduction`, and `IsEnvironment(string environmentName)` methods.</span></span> <span data-ttu-id="49624-374">Zobacz [Praca w środowiskach wielu](xref:fundamentals/environments) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="49624-374">See [Working with multiple environments](xref:fundamentals/environments) for details.</span></span>

<span data-ttu-id="49624-375">`IHostingEnvironment` Usługi także mogą zostać dodane bezpośrednio do `Configure` metody do konfigurowania potoku przetwarzania:</span><span class="sxs-lookup"><span data-stu-id="49624-375">The `IHostingEnvironment` service can also be injected directly into the `Configure` method for setting up the processing pipeline:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // In Development, use the developer exception page
        app.UseDeveloperExceptionPage();
    }
    else
    {
        // In Staging/Production, route exceptions to /error
        app.UseExceptionHandler("/error");
    }

    var contentRootPath = env.ContentRootPath;
}
```

<span data-ttu-id="49624-376">`IHostingEnvironment`mogą zostać dodane do `Invoke` metody podczas tworzenia niestandardowego [oprogramowanie pośredniczące](xref:fundamentals/middleware#writing-middleware):</span><span class="sxs-lookup"><span data-stu-id="49624-376">`IHostingEnvironment` can be injected into the `Invoke` method when creating custom [middleware](xref:fundamentals/middleware#writing-middleware):</span></span>

```csharp
public async Task Invoke(HttpContext context, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        // Configure middleware for Development
    }
    else
    {
        // Configure middleware for Staging/Production
    }

    var contentRootPath = env.ContentRootPath;
}
```

## <a name="iapplicationlifetime-interface"></a><span data-ttu-id="49624-377">Interfejs IApplicationLifetime</span><span class="sxs-lookup"><span data-stu-id="49624-377">IApplicationLifetime interface</span></span>

<span data-ttu-id="49624-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) umożliwia działań po uruchamiania i wyłączania.</span><span class="sxs-lookup"><span data-stu-id="49624-378">[IApplicationLifetime](/aspnet/core/api/microsoft.aspnetcore.hosting.iapplicationlifetime) allows for post-startup and shutdown activities.</span></span> <span data-ttu-id="49624-379">Anulowanie tokenów używany do rejestrowania są trzy właściwości w interfejsie `Action` metod, które definiują zdarzenia uruchamiania i wyłączania.</span><span class="sxs-lookup"><span data-stu-id="49624-379">Three properties on the interface are cancellation tokens used to register `Action` methods that define startup and shutdown events.</span></span> <span data-ttu-id="49624-380">Istnieje również `StopApplication` metody.</span><span class="sxs-lookup"><span data-stu-id="49624-380">There's also a `StopApplication` method.</span></span>

| <span data-ttu-id="49624-381">Token anulowania</span><span class="sxs-lookup"><span data-stu-id="49624-381">Cancellation Token</span></span>    | <span data-ttu-id="49624-382">Wyzwalane podczas &#8230;</span><span class="sxs-lookup"><span data-stu-id="49624-382">Triggered when&#8230;</span></span> |
| --------------------- | --------------------- |
| `ApplicationStarted`  | <span data-ttu-id="49624-383">Host pełni została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="49624-383">The host has fully started.</span></span> |
| `ApplicationStopping` | <span data-ttu-id="49624-384">Host wykonuje łagodne zamykanie.</span><span class="sxs-lookup"><span data-stu-id="49624-384">The host is performing a graceful shutdown.</span></span> <span data-ttu-id="49624-385">Żądania mogą nadal być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="49624-385">Requests may still be processing.</span></span> <span data-ttu-id="49624-386">Bloki zamknięcia aż do zakończenia tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="49624-386">Shutdown blocks until this event completes.</span></span> |
| `ApplicationStopped`  | <span data-ttu-id="49624-387">Host jest kończonych łagodne zamykanie.</span><span class="sxs-lookup"><span data-stu-id="49624-387">The host is completing a graceful shutdown.</span></span> <span data-ttu-id="49624-388">Wszystkie żądania powinna zostać przetworzona.</span><span class="sxs-lookup"><span data-stu-id="49624-388">All requests should be processed.</span></span> <span data-ttu-id="49624-389">Bloki zamknięcia aż do zakończenia tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="49624-389">Shutdown blocks until this event completes.</span></span> |

| <span data-ttu-id="49624-390">Metoda</span><span class="sxs-lookup"><span data-stu-id="49624-390">Method</span></span>            | <span data-ttu-id="49624-391">Akcja</span><span class="sxs-lookup"><span data-stu-id="49624-391">Action</span></span>                                           |
| ----------------- | ------------------------------------------------ |
| `StopApplication` | <span data-ttu-id="49624-392">Zakończenie żądania bieżącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49624-392">Requests termination of the current application.</span></span> |

```csharp
public class Startup 
{
    public void Configure(IApplicationBuilder app, IApplicationLifetime appLifetime) 
    {
        appLifetime.ApplicationStarted.Register(OnStarted);
        appLifetime.ApplicationStopping.Register(OnStopping);
        appLifetime.ApplicationStopped.Register(OnStopped);

        Console.CancelKeyPress += (sender, eventArgs) =>
        {
            appLifetime.StopApplication();
            // Don't terminate the process immediately, wait for the Main thread to exit gracefully.
            eventArgs.Cancel = true;
        };
    }

    private void OnStarted()
    {
        // Perform post-startup activities here
    }

    private void OnStopping()
    {
        // Perform on-stopping activities here
    }

    private void OnStopped()
    {
        // Perform post-stopped activities here
    }
}
```

## <a name="troubleshooting-systemargumentexception"></a><span data-ttu-id="49624-393">Rozwiązywanie problemów z System.ArgumentException</span><span class="sxs-lookup"><span data-stu-id="49624-393">Troubleshooting System.ArgumentException</span></span>

<span data-ttu-id="49624-394">**Dotyczy tylko platformy ASP.NET Core 2.0**</span><span class="sxs-lookup"><span data-stu-id="49624-394">**Applies to ASP.NET Core 2.0 Only**</span></span>

<span data-ttu-id="49624-395">Host może zostać utworzony przez wstrzykiwanie `IStartup` bezpośrednio do kontenera iniekcji zależności zamiast wywoływania `UseStartup` lub `Configure`:</span><span class="sxs-lookup"><span data-stu-id="49624-395">A host may be built by injecting `IStartup` directly into the dependency injection container rather than calling `UseStartup` or `Configure`:</span></span>

```csharp
services.AddSingleton<IStartup, Startup>();
```

<span data-ttu-id="49624-396">Jeśli host jest wbudowana w ten sposób, może wystąpić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="49624-396">If the host is built this way, the following error may occur:</span></span>

```
Unhandled Exception: System.ArgumentException: A valid non-empty application name must be provided.
```

<span data-ttu-id="49624-397">Dzieje się tak dlatego [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (bieżącego zestawu) jest wymagane do skanowania pod kątem `HostingStartupAttributes`.</span><span class="sxs-lookup"><span data-stu-id="49624-397">This occurs because the [applicationName(ApplicationKey)](/aspnet/core/api/microsoft.aspnetcore.hosting.webhostdefaults#Microsoft_AspNetCore_Hosting_WebHostDefaults_ApplicationKey) (the current assembly) is required to scan for `HostingStartupAttributes`.</span></span> <span data-ttu-id="49624-398">Jeśli aplikacja ręcznie injects `IStartup` do kontenera iniekcji zależności, Dodaj następujące wywołanie do `WebHostBuilder` o podanej nazwie zestawu:</span><span class="sxs-lookup"><span data-stu-id="49624-398">If the app manually injects `IStartup` into the dependency injection container, add the following call to `WebHostBuilder` with the assembly name specified:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .UseSetting("applicationName", "<Assembly Name>")
    ...
```

<span data-ttu-id="49624-399">Możesz też dodać manekina `Configure` do `WebHostBuilder`, który określa `applicationName`(`ApplicationKey`) automatycznie:</span><span class="sxs-lookup"><span data-stu-id="49624-399">Alternatively, add a dummy `Configure` to the `WebHostBuilder`, which sets the `applicationName`(`ApplicationKey`) automatically:</span></span>

```csharp
WebHost.CreateDefaultBuilder(args)
    .Configure(_ => { })
    ...
```

<span data-ttu-id="49624-400">**Uwaga**: jest to tylko wymagane wraz z wydaniem programu ASP.NET 2.0 rdzeni i tylko wtedy gdy aplikacja nie wywołać `UseStartup` lub `Configure`.</span><span class="sxs-lookup"><span data-stu-id="49624-400">**NOTE**: This is only required with the ASP.NET Core 2.0 release and only when the app doesn't call `UseStartup` or `Configure`.</span></span>

<span data-ttu-id="49624-401">Aby uzyskać więcej informacji, zobacz [anonsów: Microsoft.Extensions.PlatformAbstractions została usunięta (komentarz)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) i [próbki StartupInjection](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span><span class="sxs-lookup"><span data-stu-id="49624-401">For more information, see [Announcements: Microsoft.Extensions.PlatformAbstractions has been removed (comment)](https://github.com/aspnet/Announcements/issues/237#issuecomment-323786938) and the [StartupInjection sample](https://github.com/aspnet/Hosting/blob/8377d226f1e6e1a97dabdb6769a845eeccc829ed/samples/SampleStartups/StartupInjection.cs).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49624-402">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="49624-402">Additional resources</span></span>

* [<span data-ttu-id="49624-403">Hosting w systemie Windows z usługami IIS</span><span class="sxs-lookup"><span data-stu-id="49624-403">Host on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="49624-404">Hosting w systemie Linux z Nginx</span><span class="sxs-lookup"><span data-stu-id="49624-404">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="49624-405">Hosting w systemie Linux z Apache</span><span class="sxs-lookup"><span data-stu-id="49624-405">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* [<span data-ttu-id="49624-406">Host usługi systemu Windows</span><span class="sxs-lookup"><span data-stu-id="49624-406">Host in a Windows Service</span></span>](xref:host-and-deploy/windows-service)