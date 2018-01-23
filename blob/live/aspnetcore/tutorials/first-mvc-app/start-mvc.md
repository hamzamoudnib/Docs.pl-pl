---
title: Wprowadzenie do platformy ASP.NET Core MVC i Visual Studio
author: rick-anderson
description: Wprowadzenie do platformy ASP.NET Core MVC i Visual Studio
ms.author: riande
manager: wpickett
ms.date: 10/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/start-mvc
ms.openlocfilehash: a55b0b2a52856755b89e8ae6a2598c713f1d436d
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-mvc-and-visual-studio"></a><span data-ttu-id="8f60d-103">Wprowadzenie do platformy ASP.NET Core MVC i Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f60d-103">Getting started with ASP.NET Core MVC and Visual Studio</span></span>

<span data-ttu-id="8f60d-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8f60d-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[consider RP](../../includes/razor.md)]

<span data-ttu-id="8f60d-105">Istnieją 3 wersje tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="8f60d-105">There are 3 versions of this tutorial:</span></span>

* <span data-ttu-id="8f60d-106">System macOS: [tworzenie aplikacji platformy ASP.NET Core MVC za pomocą programu Visual Studio dla komputerów Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="8f60d-106">macOS: [Create an ASP.NET Core MVC app with Visual Studio for Mac](xref:tutorials/first-mvc-app-mac/start-mvc)</span></span>
* <span data-ttu-id="8f60d-107">System Windows: [utworzyć platformy ASP.NET Core aplikacji MVC za pomocą programu Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="8f60d-107">Windows: [Create an ASP.NET Core MVC app with Visual Studio](xref:tutorials/first-mvc-app/start-mvc)</span></span>
* <span data-ttu-id="8f60d-108">System macOS, Linux i Windows: [tworzenie aplikacji platformy ASP.NET Core MVC z kodem Visual Studio](xref:tutorials/first-mvc-app-xplat/start-mvc)</span><span class="sxs-lookup"><span data-stu-id="8f60d-108">macOS, Linux, and Windows: [Create an ASP.NET Core MVC app with Visual Studio Code](xref:tutorials/first-mvc-app-xplat/start-mvc)</span></span>

## <a name="install-visual-studio-and-net-core"></a><span data-ttu-id="8f60d-109">Zainstaluj oprogramowanie .NET Core i Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f60d-109">Install Visual Studio and .NET Core</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8f60d-110">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8f60d-110">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8f60d-111">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8f60d-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="8f60d-112">Install Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="8f60d-112">Install Visual Studio Community 2017.</span></span> <span data-ttu-id="8f60d-113">Wybierz pobieranie społeczności.</span><span class="sxs-lookup"><span data-stu-id="8f60d-113">Select the Community download.</span></span> <span data-ttu-id="8f60d-114">Jeśli masz program Visual Studio 2017 r zainstalowany, Pomiń ten krok.</span><span class="sxs-lookup"><span data-stu-id="8f60d-114">Skip this step if you have Visual Studio 2017 installed.</span></span>

* [<span data-ttu-id="8f60d-115">Visual Studio 2017 głównej strony Instalatora</span><span class="sxs-lookup"><span data-stu-id="8f60d-115">Visual Studio 2017 Home page installer</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="8f60d-116">Uruchom Instalatora, a następnie wybierz następujące obciążenia:</span><span class="sxs-lookup"><span data-stu-id="8f60d-116">Run the installer and select the following workloads:</span></span>

* <span data-ttu-id="8f60d-117">**ASP.NET i sieć web development** (w obszarze **sieci Web & chmurze**)</span><span class="sxs-lookup"><span data-stu-id="8f60d-117">**ASP.NET and web development** (under **Web & Cloud**)</span></span>
* <span data-ttu-id="8f60d-118">**Programowanie wieloplatformowych .NET core** (w obszarze **inne procesami**)</span><span class="sxs-lookup"><span data-stu-id="8f60d-118">**.NET Core cross-platform development** (under **Other Toolsets**)</span></span>

![**ASP.NET i sieci web development ** (w obszarze ** & sieci Web chmury **)](start-mvc/_static/web_workload.png)

![* *.NET core cross-cross-platfrom Programowanie ** (w obszarze ** inne procesami **)](start-mvc/_static/x_plat_wl.png)

---

## <a name="create-a-web-app"></a><span data-ttu-id="8f60d-121">Tworzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="8f60d-121">Create a web app</span></span>

<span data-ttu-id="8f60d-122">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**.</span><span class="sxs-lookup"><span data-stu-id="8f60d-122">From Visual Studio, select  **File > New > Project**.</span></span>

![Plik > Nowy > Projekt](start-mvc/_static/alt_new_project.png)

<span data-ttu-id="8f60d-124">Zakończenie **nowy projekt** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="8f60d-124">Complete the **New Project** dialog:</span></span>

* <span data-ttu-id="8f60d-125">W okienku po lewej stronie wybierz **.NET Core**</span><span class="sxs-lookup"><span data-stu-id="8f60d-125">In the left pane, tap **.NET Core**</span></span>
* <span data-ttu-id="8f60d-126">W środkowym okienku wybierz **aplikacji sieci Web platformy ASP.NET Core (.NET Core)**</span><span class="sxs-lookup"><span data-stu-id="8f60d-126">In the center pane, tap **ASP.NET Core Web Application (.NET Core)**</span></span>
* <span data-ttu-id="8f60d-127">Nazwa projektu "MvcMovie" (należy nazwa projektu "MvcMovie", po skopiowaniu kodu przestrzeni nazw będą zgodne.)</span><span class="sxs-lookup"><span data-stu-id="8f60d-127">Name the project "MvcMovie" (It's important to name the project "MvcMovie" so when you copy code, the namespace will match.)</span></span>
* <span data-ttu-id="8f60d-128">Wybierz **OK**</span><span class="sxs-lookup"><span data-stu-id="8f60d-128">Tap **OK**</span></span>

![<span data-ttu-id="8f60d-129">Okno dialogowe nowego projektu, .net core w okienku po lewej stronie sieci web platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8f60d-129">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project2.png)


# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8f60d-130">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8f60d-130">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="8f60d-131">Zakończenie **nowej platformy ASP.NET Core aplikacji sieci Web (.NET Core) — MvcMovie** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="8f60d-131">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="8f60d-132">W polu listy rozwijanej selektora wersja wybierz **platformy ASP.NET Core 2.-**</span><span class="sxs-lookup"><span data-stu-id="8f60d-132">In the version selector drop-down box select **ASP.NET Core 2.-**</span></span>
* <span data-ttu-id="8f60d-133">Wybierz **Application(Model-View-Controller) w sieci Web**</span><span class="sxs-lookup"><span data-stu-id="8f60d-133">Select **Web Application(Model-View-Controller)**</span></span>
* <span data-ttu-id="8f60d-134">Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f60d-134">Tap **OK**.</span></span>

![<span data-ttu-id="8f60d-135">Okno dialogowe nowego projektu, .net core w okienku po lewej stronie sieci web platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="8f60d-135">New project dialog, .Net core in left pane, ASP.NET Core web</span></span> ](start-mvc/_static/new_project22.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8f60d-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8f60d-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="8f60d-137">Zakończenie **nowej platformy ASP.NET Core aplikacji sieci Web (.NET Core) — MvcMovie** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="8f60d-137">Complete the **New ASP.NET Core Web Application (.NET Core) - MvcMovie** dialog:</span></span>

* <span data-ttu-id="8f60d-138">W naciśnij pola rozwijanego selektora wersji **ASP.NET Core 1.1**</span><span class="sxs-lookup"><span data-stu-id="8f60d-138">In the version selector drop-down box tap **ASP.NET Core 1.1**</span></span>
* <span data-ttu-id="8f60d-139">Wybierz **aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="8f60d-139">Tap **Web Application**</span></span>
* <span data-ttu-id="8f60d-140">Zachowaj ustawienie domyślne **bez uwierzytelniania**</span><span class="sxs-lookup"><span data-stu-id="8f60d-140">Keep the default **No Authentication**</span></span>
* <span data-ttu-id="8f60d-141">Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f60d-141">Tap **OK**.</span></span>

![Nowa aplikacja sieci web platformy ASP.NET Core](start-mvc/_static/p3.png)

---

<span data-ttu-id="8f60d-143">Visual Studio używany domyślny szablon projektu MVC, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="8f60d-143">Visual Studio used a default template for the MVC project you just created.</span></span> <span data-ttu-id="8f60d-144">Masz aplikację pracy z teraz wpisując nazwę projektu i wybierając kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="8f60d-144">You have a working app right now by entering a project name and selecting a few options.</span></span> <span data-ttu-id="8f60d-145">Jest to projekt starter proste i jest dobrym miejscem do rozpoczęcia,</span><span class="sxs-lookup"><span data-stu-id="8f60d-145">This is a simple starter project, and it's a good place to start,</span></span>

<span data-ttu-id="8f60d-146">Wybierz **F5** do uruchomienia aplikacji w trybie debugowania lub **Ctrl-F5** w trybie bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="8f60d-146">Tap **F5** to run the app in debug mode or **Ctrl-F5** in non-debug mode.</span></span>
<!-- These images are also used by uid: tutorials/first-mvc-app-xplat/start-mvc -->
![uruchomionej aplikacji](start-mvc/_static/1.png)

* <span data-ttu-id="8f60d-148">Uruchamia program Visual Studio [usług IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) i uruchamia aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f60d-148">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="8f60d-149">Należy zauważyć, że na pasku adresu `localhost:port#` i nie coś, takich jak `example.com`.</span><span class="sxs-lookup"><span data-stu-id="8f60d-149">Notice that the address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="8f60d-150">Jest to spowodowane tym `localhost` jest standardowa nazwa hosta komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="8f60d-150">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="8f60d-151">Gdy program Visual Studio tworzy projekt sieci web, losowy port jest używany dla serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="8f60d-151">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="8f60d-152">Powyższy obraz numer portu to 5000.</span><span class="sxs-lookup"><span data-stu-id="8f60d-152">In the image above, the port number is 5000.</span></span> <span data-ttu-id="8f60d-153">Adres URL w przeglądarce przedstawiono `localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="8f60d-153">The URL in the browser shows `localhost:5000`.</span></span> <span data-ttu-id="8f60d-154">Po uruchomieniu aplikacji zostanie wyświetlony inny numer portu.</span><span class="sxs-lookup"><span data-stu-id="8f60d-154">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="8f60d-155">Uruchamianie aplikacji z **Ctrl + F5** (tryb-debug) pozwala wprowadzać zmiany kodu, Zapisz plik, Odśwież przeglądarkę i zobaczyć zmiany kodu.</span><span class="sxs-lookup"><span data-stu-id="8f60d-155">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="8f60d-156">Wielu deweloperów preferowane jest w trybie bez debugowania szybko uruchomić aplikację i zobaczyć zmiany.</span><span class="sxs-lookup"><span data-stu-id="8f60d-156">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>
* <span data-ttu-id="8f60d-157">Możesz uruchomić aplikację w trybie bez debugowania z lub debugowania **debugowania** element menu:</span><span class="sxs-lookup"><span data-stu-id="8f60d-157">You can launch the app in debug or non-debug mode from the **Debug** menu item:</span></span>

![Debugowanie menu](start-mvc/_static/debug_menu.png)

* <span data-ttu-id="8f60d-159">Można debugować aplikacji, naciskając pozycję **usług IIS Express** przycisku</span><span class="sxs-lookup"><span data-stu-id="8f60d-159">You can debug the app by tapping the **IIS Express** button</span></span>

![Usługi IIS Express](start-mvc/_static/iis_express.png)

<span data-ttu-id="8f60d-161">Domyślny szablon umożliwia pracy **macierzystego o** i **skontaktuj się z** łącza.</span><span class="sxs-lookup"><span data-stu-id="8f60d-161">The default template gives you working **Home, About** and **Contact** links.</span></span> <span data-ttu-id="8f60d-162">Powyższy obraz przeglądarki nie wyświetla tych łączy.</span><span class="sxs-lookup"><span data-stu-id="8f60d-162">The browser image above doesn't show these links.</span></span> <span data-ttu-id="8f60d-163">W zależności od rozmiaru przeglądarki konieczne może być kliknij ikonę nawigacji, aby je wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="8f60d-163">Depending on the size of your browser, you might need to click the navigation icon to show them.</span></span>

![Ikona nawigacji w prawym górnym rogu](start-mvc/_static/2.png)

<span data-ttu-id="8f60d-165">Podczas uruchamiania w trybie debugowania, naciśnij przycisk **Shift-F5** można zatrzymać debugowania.</span><span class="sxs-lookup"><span data-stu-id="8f60d-165">If you were running in debug mode, tap **Shift-F5** to stop debugging.</span></span>

<span data-ttu-id="8f60d-166">W następnej części tego samouczka możemy Dowiedz się więcej o MVC i rozpocząć pisanie kodu.</span><span class="sxs-lookup"><span data-stu-id="8f60d-166">In the next part of this tutorial, we'll learn about MVC and start writing some code.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="8f60d-167">Next</span><span class="sxs-lookup"><span data-stu-id="8f60d-167">Next</span></span>](adding-controller.md)  