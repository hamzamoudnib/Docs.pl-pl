---
title: "Konfiguracja modułu Core programu ASP.NET"
author: guardrex
description: "Jak skonfigurować moduł platformy ASP.NET Core do obsługi aplikacji platformy ASP.NET Core."
keywords: "Platformy ASP.NET Core ancm, moduł core, usługi iis, rejestrowanie stdout, zmiennej środowiskowej, env-var, subapplication, subapp, appoffline, app_offline, 502, schematu"
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: article
ms.assetid: 5de0c8f7-50ce-4e2c-b3d4-a1bd9fdfcff5
ms.technology: aspnet
ms.prod: asp.net-core
uid: hosting/aspnet-core-module
ms.openlocfilehash: 277e63a5663aca622e8252d6c6be1671e57cbf68
ms.sourcegitcommit: 44a62f59d4db39d685c4487a0345a486be18d7c7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="92ed3-104">Konfiguracja modułu Core programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="92ed3-104">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="92ed3-105">Przez [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), i [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="92ed3-105">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="92ed3-106">Ten dokument zawiera szczegółowe informacje na temat konfigurowania modułu Core ASP.NET do obsługi aplikacji platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="92ed3-106">This document provides details on how to configure the ASP.NET Core Module for hosting ASP.NET Core applications.</span></span> <span data-ttu-id="92ed3-107">Aby obejrzeć wprowadzenie do platformy ASP.NET Core moduł i instrukcje dotyczące instalacji, zobacz [Przegląd platformy ASP.NET Core modułu](xref:fundamentals/servers/aspnet-core-module).</span><span class="sxs-lookup"><span data-stu-id="92ed3-107">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

## <a name="configuration-via-webconfig"></a><span data-ttu-id="92ed3-108">Konfiguracji za pomocą pliku web.config</span><span class="sxs-lookup"><span data-stu-id="92ed3-108">Configuration via web.config</span></span>

<span data-ttu-id="92ed3-109">Moduł platformy ASP.NET Core jest skonfigurowana za pośrednictwem witryny lub aplikacji *web.config* plików i ma własną `aspNetCore` sekcji konfiguracji w ramach `system.webServer`.</span><span class="sxs-lookup"><span data-stu-id="92ed3-109">The ASP.NET Core Module is configured via a site or application *web.config* file and has its own `aspNetCore` configuration section within `system.webServer`.</span></span> <span data-ttu-id="92ed3-110">Oto przykład *web.config* pliku `Microsoft.NET.Sdk.Web` zapewni zestawu SDK, gdy projekt zostanie opublikowany dla [wdrożenia zależne od framework](https://docs.microsoft.com/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) z symbole zastępcze `processPath` i `arguments`:</span><span class="sxs-lookup"><span data-stu-id="92ed3-110">Here's an example *web.config* file that the `Microsoft.NET.Sdk.Web` SDK will provide when the project is published for a [framework-dependent deployment](https://docs.microsoft.com/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) with placeholders for the `processPath` and `arguments`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="%LAUNCHER_PATH%" 
        arguments="%LAUNCHER_ARGS%" 
        stdoutLogEnabled="false" 
        stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

<span data-ttu-id="92ed3-111">*Web.config* w poniższym przykładzie jest przeznaczony dla [niezależne wdrożenia](https://docs.microsoft.com/dotnet/articles/core/deploying/#self-contained-deployments-scd) do [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="92ed3-111">The *web.config* example below is for a [self-contained deployment](https://docs.microsoft.com/dotnet/articles/core/deploying/#self-contained-deployments-scd) to the [Azure App Service](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="92ed3-112">Aby uzyskać więcej informacji, zobacz [publikowania w usługach IIS](xref:publishing/iis).</span><span class="sxs-lookup"><span data-stu-id="92ed3-112">For more information, see [Publishing to IIS](xref:publishing/iis).</span></span> <span data-ttu-id="92ed3-113">Zobacz [konfiguracji aplikacji podrzędne](xref:publishing/iis#configuration-of-sub-applications) ważne uwagi dotyczące konfiguracji *web.config* plików w aplikacjach podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="92ed3-113">See [Configuration of sub-applications](xref:publishing/iis#configuration-of-sub-applications) for an important note pertaining to the configuration of *web.config* files in sub-applications.</span></span>

```xml
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
        stdoutLogEnabled="false" 
        stdoutLogFile="\\?\%home%\LogFiles\stdout" />
  </system.webServer>
</configuration>
```

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="92ed3-114">Atrybuty elementu aspNetCore</span><span class="sxs-lookup"><span data-stu-id="92ed3-114">Attributes of the aspNetCore element</span></span>

| <span data-ttu-id="92ed3-115">Atrybut</span><span class="sxs-lookup"><span data-stu-id="92ed3-115">Attribute</span></span> | <span data-ttu-id="92ed3-116">Opis</span><span class="sxs-lookup"><span data-stu-id="92ed3-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92ed3-117">processPath</span><span class="sxs-lookup"><span data-stu-id="92ed3-117">processPath</span></span> | <p><span data-ttu-id="92ed3-118">Atrybut wymaganych parametrów.</span><span class="sxs-lookup"><span data-stu-id="92ed3-118">Required string attribute.</span></span></p><p><span data-ttu-id="92ed3-119">Ścieżka do pliku wykonywalnego, który uruchamia proces nasłuchiwanie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="92ed3-119">Path to the executable that will launch a process listening for HTTP requests.</span></span> <span data-ttu-id="92ed3-120">Ścieżki względne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="92ed3-120">Relative paths are supported.</span></span> <span data-ttu-id="92ed3-121">Jeśli ścieżka zaczyna się od '.', ścieżka jest traktowany jako względem katalogu głównego witryny.</span><span class="sxs-lookup"><span data-stu-id="92ed3-121">If the path begins with '.', the path is considered to be relative to the site root.</span></span></p><p><span data-ttu-id="92ed3-122">Nie ma żadnej wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="92ed3-122">There is no default value.</span></span></p> |
| <span data-ttu-id="92ed3-123">argumenty</span><span class="sxs-lookup"><span data-stu-id="92ed3-123">arguments</span></span> | <p><span data-ttu-id="92ed3-124">Opcjonalny atrybut ciągu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-124">Optional string attribute.</span></span></p><p><span data-ttu-id="92ed3-125">Argumenty plik wykonywalny określony w **processPath**.</span><span class="sxs-lookup"><span data-stu-id="92ed3-125">Arguments to the executable specified in **processPath**.</span></span></p><p><span data-ttu-id="92ed3-126">Wartością domyślną jest ciąg pusty.</span><span class="sxs-lookup"><span data-stu-id="92ed3-126">The default value is an empty string.</span></span></p> |
| <span data-ttu-id="92ed3-127">startupTimeLimit</span><span class="sxs-lookup"><span data-stu-id="92ed3-127">startupTimeLimit</span></span> | <p><span data-ttu-id="92ed3-128">Opcjonalny atrybut całkowity.</span><span class="sxs-lookup"><span data-stu-id="92ed3-128">Optional integer attribute.</span></span></p><p><span data-ttu-id="92ed3-129">Czas w sekundach, oczekiwania modułu dla pliku wykonywalnego do uruchomienia procesu nasłuchiwanie na porcie.</span><span class="sxs-lookup"><span data-stu-id="92ed3-129">Duration in seconds that the module will wait for the executable to start a process listening on the port.</span></span> <span data-ttu-id="92ed3-130">Po przekroczeniu tego limitu czasu, moduł będzie kasowanie procesu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-130">If this time limit is exceeded, the module will kill the process.</span></span> <span data-ttu-id="92ed3-131">Moduł spróbuje ponownie uruchomić proces, kiedy odbierze żądanie nowej i będzie podejmować próby ponownego uruchomienia procesu dla kolejnych żądań przychodzących, chyba że aplikacja nie może uruchomić **rapidFailsPerMinute** numer razy w ciągu ostatniej minuty stopniowego.</span><span class="sxs-lookup"><span data-stu-id="92ed3-131">The module will attempt to launch the process again when it receives a new request and will continue to attempt to restart the process on subsequent incoming requests unless the application fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="92ed3-132">Wartość domyślna to 120.</span><span class="sxs-lookup"><span data-stu-id="92ed3-132">The default value is 120.</span></span></p> |
| <span data-ttu-id="92ed3-133">shutdownTimeLimit</span><span class="sxs-lookup"><span data-stu-id="92ed3-133">shutdownTimeLimit</span></span> | <p><span data-ttu-id="92ed3-134">Opcjonalny atrybut całkowity.</span><span class="sxs-lookup"><span data-stu-id="92ed3-134">Optional integer attribute.</span></span></p><p><span data-ttu-id="92ed3-135">Czas w sekundach, dla których moduł będzie oczekiwał na plik wykonywalny jest bezpiecznie zamknąć po *app_offline.htm* Wykryto plik.</span><span class="sxs-lookup"><span data-stu-id="92ed3-135">Duration in seconds for which the module will wait for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p><p><span data-ttu-id="92ed3-136">Wartość domyślna to 10.</span><span class="sxs-lookup"><span data-stu-id="92ed3-136">The default value is 10.</span></span></p> |
| <span data-ttu-id="92ed3-137">rapidFailsPerMinute</span><span class="sxs-lookup"><span data-stu-id="92ed3-137">rapidFailsPerMinute</span></span> | <p><span data-ttu-id="92ed3-138">Opcjonalny atrybut całkowity.</span><span class="sxs-lookup"><span data-stu-id="92ed3-138">Optional integer attribute.</span></span></p><p><span data-ttu-id="92ed3-139">Określa liczbę powtórzeń procesu w **processPath** może awarii na minutę.</span><span class="sxs-lookup"><span data-stu-id="92ed3-139">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="92ed3-140">Po przekroczeniu tego limitu modułu przestanie uruchamiania procesu w pozostałej części minutę.</span><span class="sxs-lookup"><span data-stu-id="92ed3-140">If this limit is exceeded, the module will stop launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="92ed3-141">Wartość domyślna to 10.</span><span class="sxs-lookup"><span data-stu-id="92ed3-141">The default value is 10.</span></span></p> |
| <span data-ttu-id="92ed3-142">RequestTimeout</span><span class="sxs-lookup"><span data-stu-id="92ed3-142">requestTimeout</span></span> | <p><span data-ttu-id="92ed3-143">Atrybut opcjonalny timespan.</span><span class="sxs-lookup"><span data-stu-id="92ed3-143">Optional timespan attribute.</span></span></p><p><span data-ttu-id="92ed3-144">Określa okres czasu, dla którego moduł platformy ASP.NET Core będzie oczekiwał na odpowiedź z procesu nasłuchiwanie ASPNETCORE_PORT %.</span><span class="sxs-lookup"><span data-stu-id="92ed3-144">Specifies the duration for which the ASP.NET Core Module will wait for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="92ed3-145">Wartość domyślna to "00: 02:00".</span><span class="sxs-lookup"><span data-stu-id="92ed3-145">The default value is "00:02:00".</span></span></p><p><span data-ttu-id="92ed3-146">`requestTimeout` Muszą być określone w pełnych minutach, w przeciwnym razie domyślne 2 minuty.</span><span class="sxs-lookup"><span data-stu-id="92ed3-146">The `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> |
| <span data-ttu-id="92ed3-147">stdoutLogEnabled</span><span class="sxs-lookup"><span data-stu-id="92ed3-147">stdoutLogEnabled</span></span> | <p><span data-ttu-id="92ed3-148">Opcjonalny logiczny atrybut.</span><span class="sxs-lookup"><span data-stu-id="92ed3-148">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="92ed3-149">Jeśli PRAWDA, **stdout** i **stderr** dla określonym w procesie **processPath** nastąpi przekierowanie do określonego w pliku **stdoutLogFile**.</span><span class="sxs-lookup"><span data-stu-id="92ed3-149">If true, **stdout** and **stderr** for the process specified in **processPath** will be redirected to the file specified in **stdoutLogFile**.</span></span></p><p><span data-ttu-id="92ed3-150">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="92ed3-150">The default value is false.</span></span></p> |
| <span data-ttu-id="92ed3-151">stdoutLogFile</span><span class="sxs-lookup"><span data-stu-id="92ed3-151">stdoutLogFile</span></span> | <p><span data-ttu-id="92ed3-152">Opcjonalny atrybut ciągu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-152">Optional string attribute.</span></span></p><p><span data-ttu-id="92ed3-153">Określa ścieżkę względną lub bezwzględną, dla którego **stdout** i **stderr** z określonym w procesie **processPath** będą rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="92ed3-153">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span> <span data-ttu-id="92ed3-154">Ścieżki względne są względem katalogu głównego witryny.</span><span class="sxs-lookup"><span data-stu-id="92ed3-154">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="92ed3-155">Dowolną ścieżkę, rozpoczynając od '.' będzie względem katalogu głównego witryny i innych ścieżek będą traktowane jako ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="92ed3-155">Any path starting with '.' will be relative to the site root and all other paths will be treated as absolute paths.</span></span> <span data-ttu-id="92ed3-156">Wszystkie foldery w ścieżce musi istnieć w kolejności dla modułu utworzyć plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="92ed3-156">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="92ed3-157">Identyfikator procesu sygnatury czasowej (*yyyyMdhms*) i rozszerzenie pliku (*log*) podkreślenia ograniczniki są dodawane do ostatniego segment **stdoutLogFile** podane.</span><span class="sxs-lookup"><span data-stu-id="92ed3-157">The process ID, timestamp (*yyyyMdhms*), and file extension (*.log*) with underscore delimiters are added to the last segment of the **stdoutLogFile** provided.</span></span></p><p><span data-ttu-id="92ed3-158">Wartość domyślna to `aspnetcore-stdout`.</span><span class="sxs-lookup"><span data-stu-id="92ed3-158">The default value is `aspnetcore-stdout`.</span></span></p> |
| <span data-ttu-id="92ed3-159">forwardWindowsAuthToken</span><span class="sxs-lookup"><span data-stu-id="92ed3-159">forwardWindowsAuthToken</span></span> | <span data-ttu-id="92ed3-160">prawda lub fałsz.</span><span class="sxs-lookup"><span data-stu-id="92ed3-160">true or false.</span></span></p><p><span data-ttu-id="92ed3-161">Jeśli PRAWDA, token będą przekazywane do procesu podrzędnego nasłuchiwanie ASPNETCORE_PORT % jako nagłówek "MS-ASPNETCORE-WINAUTHTOKEN" na żądanie.</span><span class="sxs-lookup"><span data-stu-id="92ed3-161">If true, the token will be forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="92ed3-162">Jest odpowiedzialny za ten proces może wywołać funkcji CloseHandle: ten token na żądanie.</span><span class="sxs-lookup"><span data-stu-id="92ed3-162">It is the responsibility of that process to call CloseHandle on this token per request.</span></span></p><p><span data-ttu-id="92ed3-163">Wartość domyślna to true.</span><span class="sxs-lookup"><span data-stu-id="92ed3-163">The default value is true.</span></span></p> |
| <span data-ttu-id="92ed3-164">disableStartUpErrorPage</span><span class="sxs-lookup"><span data-stu-id="92ed3-164">disableStartUpErrorPage</span></span> | <span data-ttu-id="92ed3-165">prawda lub fałsz.</span><span class="sxs-lookup"><span data-stu-id="92ed3-165">true or false.</span></span></p><p><span data-ttu-id="92ed3-166">Jeśli PRAWDA, **502.5 — niepowodzenie procesu** strona zostanie pominięta i na stronie kod stanu 502 w Twojej *web.config* mają wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="92ed3-166">If true, the **502.5 - Process Failure** page will be suppressed, and the 502 status code page configured in your *web.config* will take precedence.</span></span></p><p><span data-ttu-id="92ed3-167">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="92ed3-167">The default value is false.</span></span></p> |

### <a name="setting-environment-variables"></a><span data-ttu-id="92ed3-168">Ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="92ed3-168">Setting environment variables</span></span>

<span data-ttu-id="92ed3-169">Moduł platformy ASP.NET Core pozwala określić zmiennych środowiskowych dla procesu, który został określony w `processPath` atrybutu, określając je w co najmniej jednej `environmentVariable` elementy podrzędne `environmentVariables` elementu kolekcji, w obszarze `aspNetCore` elementu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-169">The ASP.NET Core Module allows you specify environment variables for the process specified in the `processPath` attribute by specifying them in one or more `environmentVariable` child elements of an `environmentVariables` collection element under the `aspNetCore` element.</span></span> <span data-ttu-id="92ed3-170">Zmienne środowiskowe w tej sekcji mają pierwszeństwo względem systemu zmiennych środowiskowych dla procesu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-170">Environment variables set in this section take precedence over system environment variables for the process.</span></span>

<span data-ttu-id="92ed3-171">W poniższym przykładzie ustawia dwie zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="92ed3-171">The example below sets two environment variables.</span></span> <span data-ttu-id="92ed3-172">`ASPNETCORE_ENVIRONMENT`konfiguruje środowisko aplikacji `Development`.</span><span class="sxs-lookup"><span data-stu-id="92ed3-172">`ASPNETCORE_ENVIRONMENT` will configure the application's environment to `Development`.</span></span> <span data-ttu-id="92ed3-173">Deweloper może tymczasowo Ustaw tę wartość *web.config* pliku, aby wymusić [strona wyjątek dewelopera](xref:fundamentals/error-handling) załadować podczas debugowania aplikacji wyjątek.</span><span class="sxs-lookup"><span data-stu-id="92ed3-173">A developer may temporarily set this value in the *web.config* file in order to force the [developer exception page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="92ed3-174">`CONFIG_DIR`jest przykład zmiennej środowiska użytkownika, gdy projektanta został zapisany kod, który odczyta wartość przy uruchamianiu do utworzenia ścieżkę, aby można było załadować pliku konfiguracyjnego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92ed3-174">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that will read the value on startup to form a path in order to load the app's configuration file.</span></span>

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

## <a name="appofflinehtm"></a><span data-ttu-id="92ed3-175">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="92ed3-175">app_offline.htm</span></span>

<span data-ttu-id="92ed3-176">Jeśli możesz umieścić plik o nazwie *app_offline.htm* w głównym katalogu aplikacji sieci web, moduł platformy ASP.NET Core będzie próbować bezpiecznie zamknięcia aplikacji i Zatrzymaj przetwarzanie przychodzących żądań.</span><span class="sxs-lookup"><span data-stu-id="92ed3-176">If you place a file with the name *app_offline.htm* at the root of a web application directory, the ASP.NET Core Module will attempt to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="92ed3-177">Jeśli aplikacja jest nadal uruchomiona `shutdownTimeLimit` liczbę sekund, moduł platformy ASP.NET Core będzie kill uruchomionego procesu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-177">If the app is still running after `shutdownTimeLimit` number of seconds, the ASP.NET Core Module will kill the running process.</span></span>

<span data-ttu-id="92ed3-178">Gdy *app_offline.htm* plik jest obecny, moduł platformy ASP.NET Core będzie odpowiadał na żądania przez odsyła zawartość *app_offline.htm* pliku.</span><span class="sxs-lookup"><span data-stu-id="92ed3-178">While the *app_offline.htm* file is present, the ASP.NET Core Module will respond to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="92ed3-179">Raz *app_offline.htm* plik zostanie usunięty, przy następnym żądaniu ładuje aplikacji, która następnie odpowiada na żądania.</span><span class="sxs-lookup"><span data-stu-id="92ed3-179">Once the *app_offline.htm* file is removed, the next request loads the application, which then responds to requests.</span></span>

## <a name="start-up-error-page"></a><span data-ttu-id="92ed3-180">Strona błędu uruchamiania</span><span class="sxs-lookup"><span data-stu-id="92ed3-180">Start-up error page</span></span>

<span data-ttu-id="92ed3-181">Jeśli moduł platformy ASP.NET Core nie można uruchomić procesu zaplecza lub uruchamia proces wewnętrznej bazy danych, ale nie może nasłuchiwać na porcie skonfigurowanym, zostanie wyświetlona strona kod stanu HTTP 502.5.</span><span class="sxs-lookup"><span data-stu-id="92ed3-181">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, you will see an HTTP 502.5 status code page.</span></span> <span data-ttu-id="92ed3-182">Aby pominąć tę stronę i przywrócić domyślną stronę kodową stan 502 usług IIS, należy użyć `disableStartUpErrorPage` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-182">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="92ed3-183">Aby uzyskać więcej informacji na temat konfigurowania niestandardowych komunikatów o błędach, zobacz [błędy HTTP `<httpErrors>` ](https://docs.microsoft.com/iis/configuration/system.webServer/httpErrors/).</span><span class="sxs-lookup"><span data-stu-id="92ed3-183">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](https://docs.microsoft.com/iis/configuration/system.webServer/httpErrors/).</span></span>

![502 stanu strony](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="92ed3-185">Tworzenie dziennika i Przekierowanie</span><span class="sxs-lookup"><span data-stu-id="92ed3-185">Log creation and redirection</span></span>

<span data-ttu-id="92ed3-186">Moduł platformy ASP.NET Core przekierowuje `stdout` i `stderr` dzienniki na dysku, jeśli ustawisz `stdoutLogEnabled` i `stdoutLogFile` atrybuty `aspNetCore` elementu.</span><span class="sxs-lookup"><span data-stu-id="92ed3-186">The ASP.NET Core Module redirects `stdout` and `stderr` logs to disk if you set the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element.</span></span> <span data-ttu-id="92ed3-187">Wszystkie foldery w `stdoutLogFile` ścieżka musi istnieć w kolejności dla modułu utworzyć plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="92ed3-187">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="92ed3-188">Rozszerzenia znaczników czasu i plików zostaną dodane automatycznie, gdy plik dziennika jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="92ed3-188">A timestamp and file extension will be added automatically when the log file is created.</span></span> <span data-ttu-id="92ed3-189">Dzienniki nie są obracane, chyba że występuje procesu recykling/ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="92ed3-189">Logs are not rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="92ed3-190">Jest odpowiedzialny za dostawcy usług hostingowych, aby ograniczyć miejsce na dysku korzystać z dzienników.</span><span class="sxs-lookup"><span data-stu-id="92ed3-190">It is the responsibility of the hoster to limit the disk space the logs consume.</span></span> <span data-ttu-id="92ed3-191">Przy użyciu `stdout` dziennika jest zalecane tylko uzyskać informacje o rozwiązywaniu problemów z uruchamianiem aplikacji, a nie do celów rejestracji ogólnego zastosowania.</span><span class="sxs-lookup"><span data-stu-id="92ed3-191">Using the `stdout` log is only recommended for troubleshooting application startup issues and not for general application logging purposes.</span></span>

<span data-ttu-id="92ed3-192">Nazwa pliku dziennika składa się przez dołączenie Identyfikatora PID, sygnatura czasowa procesu (*yyyyMdhms*) i rozszerzenie pliku (*log*) do ostatni segment `stdoutLogFile` ścieżki (zazwyczaj *stdout* ) rozdzielane znakami podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="92ed3-192">The log file name is composed by appending the process ID (PID), timestamp (*yyyyMdhms*), and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="92ed3-193">Na przykład jeśli `stdoutLogFile` ścieżka kończy się *stdout*, nazwa pliku ma dziennika dla aplikacji za pomocą identyfikatora PID 10652 utworzonego na 8/10/2017 w dniu 12:05:02 *stdout_10652_20178101252.log*.</span><span class="sxs-lookup"><span data-stu-id="92ed3-193">For example if the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 10652 created on 8/10/2017 at 12:05:02 has the file name *stdout_10652_20178101252.log*.</span></span>

<span data-ttu-id="92ed3-194">Poniżej przedstawiono przykładowe `aspNetCore` element, który konfiguruje `stdout` rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="92ed3-194">Here's a sample `aspNetCore` element that configures `stdout` logging.</span></span> <span data-ttu-id="92ed3-195">`stdoutLogFile` Ścieżka pokazano w przykładzie jest odpowiednia dla usługi Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="92ed3-195">The `stdoutLogFile` path shown in the example is appropriate for the Azure App Service.</span></span> <span data-ttu-id="92ed3-196">Ścieżkę lokalną lub ścieżkę do udziału sieciowego jest dopuszczalne do lokalnego logowania.</span><span class="sxs-lookup"><span data-stu-id="92ed3-196">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="92ed3-197">Upewnij się, że tożsamość puli aplikacji ma uprawnienia do zapisu w podanej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="92ed3-197">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```
<span data-ttu-id="92ed3-198">Zobacz [konfiguracji za pomocą pliku web.config](#configuration-via-webconfig) przykład `aspNetCore` element *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="92ed3-198">See [Configuration via web.config](#configuration-via-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="92ed3-199">Moduł platformy ASP.NET Core z programem IIS konfiguracji udostępnionej</span><span class="sxs-lookup"><span data-stu-id="92ed3-199">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="92ed3-200">Instalator platformy ASP.NET Core modułu jest uruchamiany z uprawnieniami **systemu** konta.</span><span class="sxs-lookup"><span data-stu-id="92ed3-200">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="92ed3-201">Ponieważ lokalne konto systemowe ma uprawnienia do modyfikowania dla ścieżki udziału, który jest używany przez konfiguracji udostępnionej usług IIS, Instalator nastąpi trafienie dostępu błąd podczas próby skonfigurowania ustawienia modułu w  *applicationHost.config* w udziale.</span><span class="sxs-lookup"><span data-stu-id="92ed3-201">Because the local system account does not have modify permission for the share path which is used by the IIS Shared Configuration, the installer will hit an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span>

<span data-ttu-id="92ed3-202">Nieobsługiwany obejściem jest wyłączenie konfiguracji udostępnionej usług IIS, uruchom Instalatora, eksportowanie zaktualizowanego *applicationHost.config* plików do udziału, a następnie ponownie włącz konfiguracji udostępnionej usług IIS.</span><span class="sxs-lookup"><span data-stu-id="92ed3-202">The unsupported workaround is to disable the IIS Shared Configuration, run the installer, export the updated *applicationHost.config* file to the share, and re-enable the IIS Shared Configuration.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="92ed3-203">Moduł, schematów i konfiguracji lokalizacje plików</span><span class="sxs-lookup"><span data-stu-id="92ed3-203">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="92ed3-204">Moduł</span><span class="sxs-lookup"><span data-stu-id="92ed3-204">Module</span></span>

<span data-ttu-id="92ed3-205">**Usługi IIS (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="92ed3-205">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="92ed3-206">%Windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="92ed3-206">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="92ed3-207">%Windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="92ed3-207">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="92ed3-208">**Usługi IIS Express (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="92ed3-208">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="92ed3-209">%ProgramFiles%\iis Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="92ed3-209">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="92ed3-210">% ProgramFiles (x86) %\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="92ed3-210">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="92ed3-211">Schemat</span><span class="sxs-lookup"><span data-stu-id="92ed3-211">Schema</span></span>

<span data-ttu-id="92ed3-212">**USŁUGI IIS**</span><span class="sxs-lookup"><span data-stu-id="92ed3-212">**IIS**</span></span>

   * <span data-ttu-id="92ed3-213">%Windir%\System32\inetsrv\config\schema\aspnetcore_schema.XML</span><span class="sxs-lookup"><span data-stu-id="92ed3-213">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="92ed3-214">**Usługi IIS Express**</span><span class="sxs-lookup"><span data-stu-id="92ed3-214">**IIS Express**</span></span>

   * <span data-ttu-id="92ed3-215">%ProgramFiles%\iis Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="92ed3-215">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="92ed3-216">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="92ed3-216">Configuration</span></span>

<span data-ttu-id="92ed3-217">**USŁUGI IIS**</span><span class="sxs-lookup"><span data-stu-id="92ed3-217">**IIS**</span></span>

   * <span data-ttu-id="92ed3-218">%Windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="92ed3-218">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="92ed3-219">**Usługi IIS Express**</span><span class="sxs-lookup"><span data-stu-id="92ed3-219">**IIS Express**</span></span>

   * <span data-ttu-id="92ed3-220">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="92ed3-220">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="92ed3-221">Możesz wyszukać *aspnetcore.dll* w *applicationHost.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="92ed3-221">You can search for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="92ed3-222">Dla usług IIS Express *applicationHost.config* plik nie istnieje domyślnie.</span><span class="sxs-lookup"><span data-stu-id="92ed3-222">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="92ed3-223">Plik jest tworzony w *{katalog główny aplikacji}\.vs\config* po rozpoczęciu żadnego projektu aplikacji sieci web w rozwiązaniu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92ed3-223">The file is created at *{application root}\.vs\config* when you start any web application project in the Visual Studio solution.</span></span>