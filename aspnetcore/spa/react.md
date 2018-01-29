---
title: "Należy użyć szablonu projektu w bibliotece React."
author: SteveSandersonMS
description: "Dowiedz się, jak rozpocząć pracę z szablonu projektu platformy ASP.NET Core jednostronicowej aplikacji JEDNOSTRONICOWEJ release candidate dla platformy React i utworzyć platformy react aplikacji."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react
ms.openlocfilehash: 5978094083a098a771f5dca103434ea8fcce7777
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="use-the-react-project-template-release-candidate"></a><span data-ttu-id="ef82c-103">Należy użyć szablonu projektu platformy React (w wersji release candidate)</span><span class="sxs-lookup"><span data-stu-id="ef82c-103">Use the React project template (release candidate)</span></span>

> [!NOTE]
> <span data-ttu-id="ef82c-104">Ta dokumentacja nie jest o wydanych szablonu projektu platformy React.</span><span class="sxs-lookup"><span data-stu-id="ef82c-104">This documentation isn't about the released React project template.</span></span> <span data-ttu-id="ef82c-105">**Ta dokumentacja dotyczy wersji release candidate szablonu platformy React.**</span><span class="sxs-lookup"><span data-stu-id="ef82c-105">**This documentation is about the release candidate of the React template.**</span></span> <span data-ttu-id="ef82c-106">Mamy nadzieję, należy wysłać wersji wydanej w wczesne 2018.</span><span class="sxs-lookup"><span data-stu-id="ef82c-106">We hope to ship the released version in early 2018.</span></span>

<span data-ttu-id="ef82c-107">Zaktualizowany szablon projektu platformy React udostępnia dogodny punkt początkowy dla platformy ASP.NET Core aplikacji przy użyciu platformy React i [utworzyć platformy react aplikacji](https://github.com/facebookincubator/create-react-app) konwencje (CRA) do zaimplementowania rozbudowanego klienta interfejsu użytkownika (UI).</span><span class="sxs-lookup"><span data-stu-id="ef82c-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="ef82c-108">Szablon jest odpowiednikiem Tworzenie projektu platformy ASP.NET Core do działania jako zaplecza interfejsu API i standardowe projektu CRA zareagować na działanie jako interfejsu użytkownika, ale z elastycznością obsługi zarówno w projekcie jednej aplikacji, które mogą być wbudowane i opublikowane jako pojedyncza jednostka.</span><span class="sxs-lookup"><span data-stu-id="ef82c-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="ef82c-109">Tworzenie nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ef82c-109">Create a new app</span></span>

<span data-ttu-id="ef82c-110">Aby rozpocząć, upewnij się, które zostały [zainstalowany zaktualizowany szablon projektu platformy React](xref:spa/index#installation).</span><span class="sxs-lookup"><span data-stu-id="ef82c-110">To get started, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span> <span data-ttu-id="ef82c-111">Te instrukcje nie dotyczą poprzedniego szablonu projektu platformy React objęte .NET Core 2.0.x zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ef82c-111">These instructions don't apply to the previous React project template included in the .NET Core 2.0.x SDK.</span></span>

<span data-ttu-id="ef82c-112">Utwórz nowy projekt z wiersza polecenia przy użyciu polecenia `dotnet new react` w pustych katalogów.</span><span class="sxs-lookup"><span data-stu-id="ef82c-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="ef82c-113">Na przykład poniższe polecenia Utwórz aplikację w *— nowy — aplikacji my* katalogu i przełącznika do tego katalogu:</span><span class="sxs-lookup"><span data-stu-id="ef82c-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="ef82c-114">Uruchamianie aplikacji z programu Visual Studio lub platformy .NET Core interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="ef82c-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="ef82c-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ef82c-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="ef82c-116">Otwórz wygenerowany *.csproj* pliku i uruchom aplikację w zwykły stamtąd.</span><span class="sxs-lookup"><span data-stu-id="ef82c-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="ef82c-117">Proces kompilacji przywraca npm zależności przy pierwszym uruchomieniu, co może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ef82c-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="ef82c-118">Kolejne kompilacje są znacznie szybsze.</span><span class="sxs-lookup"><span data-stu-id="ef82c-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="ef82c-119">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="ef82c-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="ef82c-120">Upewnij się, masz zmienną środowiskową o nazwie `ASPNETCORE_Environment` o wartości `Development`.</span><span class="sxs-lookup"><span data-stu-id="ef82c-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="ef82c-121">W systemie Windows (w monity-PowerShell), uruchom `SET ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="ef82c-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="ef82c-122">W systemie Linux lub macOS Uruchom `export ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="ef82c-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="ef82c-123">Uruchom `dotnet build` można zweryfikować aplikacji kompilacje poprawnie.</span><span class="sxs-lookup"><span data-stu-id="ef82c-123">Run `dotnet build` to verify your app builds correctly.</span></span> <span data-ttu-id="ef82c-124">Przy pierwszym uruchomieniu procesu kompilacji przywraca npm zależności, co może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ef82c-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="ef82c-125">Kolejne kompilacje są znacznie szybsze.</span><span class="sxs-lookup"><span data-stu-id="ef82c-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="ef82c-126">Uruchom `dotnet run` do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef82c-126">Run `dotnet run` to start the app.</span></span>

---

<span data-ttu-id="ef82c-127">Szablon projektu tworzy aplikację platformy ASP.NET Core i aplikacji platformy React.</span><span class="sxs-lookup"><span data-stu-id="ef82c-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="ef82c-128">Aplikacja platformy ASP.NET Core jest przeznaczona do użycia dla dostępu do danych, autoryzację i inne problemy po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="ef82c-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="ef82c-129">Aplikacja platformy React, znajdującej się w *ClientApp* podkatalogu, jest przeznaczona do użycia dla wszystkich problemów w zakresie interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ef82c-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="ef82c-130">Dodawanie stron, obrazy, style, modułów, itp.</span><span class="sxs-lookup"><span data-stu-id="ef82c-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="ef82c-131">*ClientApp* katalog jest standardowych aplikacji CRA reagować.</span><span class="sxs-lookup"><span data-stu-id="ef82c-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="ef82c-132">Można znaleźć w oficjalnej [dokumentacji CRA](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ef82c-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="ef82c-133">Niewielkich różnic między aplikacją platformy React, utworzony przez ten szablon i utworzonym przez CRA jednak możliwości aplikacji nie uległy zmianie.</span><span class="sxs-lookup"><span data-stu-id="ef82c-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="ef82c-134">Utworzona przez szablon aplikacja zawiera [Bootstrap](https://getbootstrap.com/)— na podstawie układu i prosty przykład routingu.</span><span class="sxs-lookup"><span data-stu-id="ef82c-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="ef82c-135">Instalowanie pakietów npm</span><span class="sxs-lookup"><span data-stu-id="ef82c-135">Install npm packages</span></span>

<span data-ttu-id="ef82c-136">Aby zainstalować pakiety innych firm npm, przy użyciu wiersza polecenia w *ClientApp* podkatalogu.</span><span class="sxs-lookup"><span data-stu-id="ef82c-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="ef82c-137">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ef82c-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="ef82c-138">Publikowanie i wdrażanie</span><span class="sxs-lookup"><span data-stu-id="ef82c-138">Publish and deploy</span></span>

<span data-ttu-id="ef82c-139">W rozwoju aplikacji jest uruchamiany w trybie zoptymalizowane pod kątem wygody deweloperów.</span><span class="sxs-lookup"><span data-stu-id="ef82c-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="ef82c-140">Na przykład pakiety JavaScript obejmują map źródeł (tak, aby podczas debugowania, możesz zobaczyć kodu).</span><span class="sxs-lookup"><span data-stu-id="ef82c-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="ef82c-141">Aplikacja oczekuje JavaScript, HTML i CSS pliku zmiany na dysku i automatycznie rekompiluje i ponowne załadowanie po wykryciu tych plików, zmiany.</span><span class="sxs-lookup"><span data-stu-id="ef82c-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="ef82c-142">W środowisku produkcyjnym obsługiwać wersji aplikacji jest zoptymalizowany pod kątem wydajności.</span><span class="sxs-lookup"><span data-stu-id="ef82c-142">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="ef82c-143">To jest skonfigurowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ef82c-143">This is configured to happen automatically.</span></span> <span data-ttu-id="ef82c-144">Podczas publikowania, konfiguracja kompilacji emituje zminimalizowany, kompilacji transpiled kodu po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="ef82c-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="ef82c-145">W przeciwieństwie do kompilacji programowanie kompilacji produkcyjnym nie wymaga Node.js do zainstalowania na serwerze.</span><span class="sxs-lookup"><span data-stu-id="ef82c-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="ef82c-146">Można użyć standardowego [metody wdrażania i hostingu ASP.NET Core](xref:host-and-deploy/index).</span><span class="sxs-lookup"><span data-stu-id="ef82c-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="ef82c-147">Uruchom serwer CRA niezależnie</span><span class="sxs-lookup"><span data-stu-id="ef82c-147">Run the CRA server independently</span></span>

<span data-ttu-id="ef82c-148">Projekt jest skonfigurowany do uruchamiania własnego wystąpienia serwera wdrożeniowego CRA w tle po uruchomieniu aplikacji platformy ASP.NET Core w trybie projektowania.</span><span class="sxs-lookup"><span data-stu-id="ef82c-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="ef82c-149">Ta opcja jest przydatna, ponieważ oznacza to, że nie trzeba ręcznie uruchomić oddzielny serwer.</span><span class="sxs-lookup"><span data-stu-id="ef82c-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="ef82c-150">Brak wadą tego ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="ef82c-150">There's a drawback to this default setup.</span></span> <span data-ttu-id="ef82c-151">Po każdej zmianie kodu C# i ASP.NET podstawowych aplikacja musi ponownie uruchomić, CRA serwer zostanie ponownie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="ef82c-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="ef82c-152">Kilka sekund, należy rozpocząć tworzenie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="ef82c-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="ef82c-153">Jeśli wprowadzania częste zmiany kodu C# i nie chcesz czekać na ponowne uruchomienie serwera CRA, uruchom serwer CRA zewnętrznie, niezależnie od procesu ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ef82c-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="ef82c-154">Aby to zrobić:</span><span class="sxs-lookup"><span data-stu-id="ef82c-154">To do so:</span></span>

1. <span data-ttu-id="ef82c-155">W wierszu polecenia, przełącz się do *ClientApp* podkatalogu, a następnie uruchom serwera wdrożeniowego CRA:</span><span class="sxs-lookup"><span data-stu-id="ef82c-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="ef82c-156">Zmodyfikuj do korzystania z zewnętrznego wystąpienia serwera CRA zamiast uruchamiania jednego z jego własnej aplikacji platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ef82c-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="ef82c-157">W Twojej *uruchamiania* klasy, Zastąp `spa.UseReactDevelopmentServer` wywołania z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ef82c-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="ef82c-158">Po uruchomieniu aplikacji platformy ASP.NET Core, nie będzie on uruchomienia serwera CRA.</span><span class="sxs-lookup"><span data-stu-id="ef82c-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="ef82c-159">Zamiast niego jest używana wystąpienia, które zostanie uruchomione ręcznie.</span><span class="sxs-lookup"><span data-stu-id="ef82c-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="ef82c-160">Dzięki temu może uruchomić i ponownie uruchom szybciej.</span><span class="sxs-lookup"><span data-stu-id="ef82c-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="ef82c-161">Nie jest już oczekuje dla aplikacji platformy React odbudować zawsze.</span><span class="sxs-lookup"><span data-stu-id="ef82c-161">It's no longer waiting for your React app to rebuild each time.</span></span>