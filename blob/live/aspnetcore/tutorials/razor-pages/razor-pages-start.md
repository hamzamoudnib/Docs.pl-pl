---
title: Wprowadzenie do platformy ASP.NET Core stron Razor
author: rick-anderson
description: Wprowadzenie do platformy ASP.NET Core stron Razor
ms.author: riande
manager: wpickett
ms.date: 12/22/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/razor-pages-start
ms.openlocfilehash: 69a5bc439130ffacf2d267c79b1a6b0347171e49
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="get-started-with-razor-pages-in-aspnet-core"></a><span data-ttu-id="3daf6-103">Rozpoczynanie pracy z Razor strony platformy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3daf6-103">Get started with Razor Pages in ASP.NET Core</span></span>

<span data-ttu-id="3daf6-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3daf6-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="3daf6-105">Ten samouczek zawiera podstawowe informacje dotyczące tworzenia aplikacji sieci web platformy ASP.NET Core Razor strony.</span><span class="sxs-lookup"><span data-stu-id="3daf6-105">This tutorial teaches the basics of building an ASP.NET Core Razor Pages web app.</span></span> <span data-ttu-id="3daf6-106">Stron razor jest zalecanym sposobem tworzenia interfejsu użytkownika dla aplikacji sieci web w ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3daf6-106">Razor Pages is the recommended way to build UI for web apps in ASP.NET Core.</span></span>

<span data-ttu-id="3daf6-107">Istnieją trzy wersje tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="3daf6-107">There are three versions of this tutorial:</span></span>

* <span data-ttu-id="3daf6-108">Systemu Windows: W tym samouczku</span><span class="sxs-lookup"><span data-stu-id="3daf6-108">Windows: This tutorial</span></span>
* <span data-ttu-id="3daf6-109">System MacOS: [wprowadzenie stron Razor przy użyciu programu Visual Studio dla komputerów Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="3daf6-109">MacOS: [Getting started with Razor Pages with Visual Studio for Mac](xref:tutorials/razor-pages-mac/razor-pages-start)</span></span>
* <span data-ttu-id="3daf6-110">System macOS, Linux i Windows: [wprowadzenie Razor strony platformy ASP.NET Core z kodem Visual Studio](xref:tutorials/razor-pages-vsc/razor-pages-start)</span><span class="sxs-lookup"><span data-stu-id="3daf6-110">macOS, Linux, and Windows: [Getting started with Razor Pages in ASP.NET Core with Visual Studio Code](xref:tutorials/razor-pages-vsc/razor-pages-start)</span></span>

<span data-ttu-id="3daf6-111">[Wyświetlić lub pobrać przykładowy kod](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) ([sposobu pobierania](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3daf6-111">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3daf6-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3daf6-112">Prerequisites</span></span>

[!INCLUDE[install 2.0](../../includes/install2.0.md)]

## <a name="create-a-razor-web-app"></a><span data-ttu-id="3daf6-113">Tworzenie aplikacji sieci web Razor</span><span class="sxs-lookup"><span data-stu-id="3daf6-113">Create a Razor web app</span></span>

* <span data-ttu-id="3daf6-114">W programie Visual Studio **pliku** menu, wybierz opcję **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="3daf6-114">From the Visual Studio **File** menu, select **New** > **Project**.</span></span>
* <span data-ttu-id="3daf6-115">Utwórz nową aplikację sieci Web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3daf6-115">Create a new ASP.NET Core Web Application.</span></span> <span data-ttu-id="3daf6-116">Nazwij projekt **RazorPagesMovie**.</span><span class="sxs-lookup"><span data-stu-id="3daf6-116">Name the project **RazorPagesMovie**.</span></span> <span data-ttu-id="3daf6-117">Ważne jest, aby nazwa projektu *RazorPagesMovie* , przestrzenie nazw będzie dopasowania, gdy użytkownik kopiowanie/wklejanie kodu.</span><span class="sxs-lookup"><span data-stu-id="3daf6-117">It's important to name the project *RazorPagesMovie* so the namespaces will match when you copy/paste code.</span></span>
  <span data-ttu-id="3daf6-118">![nową aplikację sieci Web Core ASP.NET](../../mvc/razor-pages/index/_static/np.png)</span><span class="sxs-lookup"><span data-stu-id="3daf6-118">![new ASP.NET Core Web Application](../../mvc/razor-pages/index/_static/np.png)</span></span>
* <span data-ttu-id="3daf6-119">Wybierz **ASP.NET Core 2.0** w listy rozwijanej, a następnie wybierz **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="3daf6-119">Select **ASP.NET Core 2.0** in the dropdown, and then select **Web Application**.</span></span>

  [!INCLUDE[install 2.0](../../includes/dotnetcore-on-dotnetfx-vs.md)]

<span data-ttu-id="3daf6-120">Szablon programu Visual Studio tworzy projekt starter:</span><span class="sxs-lookup"><span data-stu-id="3daf6-120">The Visual Studio template creates a starter project:</span></span>

![Eksplorator rozwiązań](razor-pages-start/_static/se.png)

<span data-ttu-id="3daf6-122">Naciśnij klawisz **F5** do uruchomienia aplikacji w trybie debugowania lub **Ctrl-F5** działać bez dołączanie debugera</span><span class="sxs-lookup"><span data-stu-id="3daf6-122">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger</span></span>

![Strona główna lub indeks](razor-pages-start/_static/home.png)

* <span data-ttu-id="3daf6-124">Uruchamia program Visual Studio [usług IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) i uruchamia aplikację.</span><span class="sxs-lookup"><span data-stu-id="3daf6-124">Visual Studio starts [IIS Express](https://docs.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your app.</span></span> <span data-ttu-id="3daf6-125">Pokazuje pasek adresu `localhost:port#` i nie coś, takich jak `example.com`.</span><span class="sxs-lookup"><span data-stu-id="3daf6-125">The address bar shows `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="3daf6-126">Jest to spowodowane tym `localhost` jest standardowa nazwa hosta komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3daf6-126">That's because `localhost` is the standard hostname for your local computer.</span></span> <span data-ttu-id="3daf6-127">Localhost obsługują tylko żądania sieci web z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3daf6-127">Localhost only serves web requests from the local computer.</span></span> <span data-ttu-id="3daf6-128">Gdy program Visual Studio tworzy projekt sieci web, losowy port jest używany dla serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="3daf6-128">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="3daf6-129">Na poprzedniej ilustracji numer portu to 5000.</span><span class="sxs-lookup"><span data-stu-id="3daf6-129">In the preceding image, the port number is 5000.</span></span> <span data-ttu-id="3daf6-130">Po uruchomieniu aplikacji zostanie wyświetlony inny numer portu.</span><span class="sxs-lookup"><span data-stu-id="3daf6-130">When you run the app, you'll see a different port number.</span></span>
* <span data-ttu-id="3daf6-131">Uruchamianie aplikacji z **Ctrl + F5** (tryb-debug) pozwala wprowadzać zmiany kodu, Zapisz plik, Odśwież przeglądarkę i zobaczyć zmiany kodu.</span><span class="sxs-lookup"><span data-stu-id="3daf6-131">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="3daf6-132">Wielu deweloperów preferowane jest w trybie bez debugowania szybko uruchomić aplikację i zobaczyć zmiany.</span><span class="sxs-lookup"><span data-stu-id="3daf6-132">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

[!INCLUDE[razor-pages-start](../../includes/RP/razor-pages-start.md)]

>[!div class="step-by-step"]
[<span data-ttu-id="3daf6-133">Następnie: Dodawanie modelu</span><span class="sxs-lookup"><span data-stu-id="3daf6-133">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)

>[!div class="step-by-step"]
[<span data-ttu-id="3daf6-134">Następnie: Dodawanie modelu</span><span class="sxs-lookup"><span data-stu-id="3daf6-134">Next: Adding a model</span></span>](xref:tutorials/razor-pages/model)