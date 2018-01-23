---
title: "Dodawanie modelu do aplikacji stron Razor przy użyciu programu Visual Studio dla komputerów Mac"
author: rick-anderson
description: "Dodawanie modelu do aplikacji stron Razor w ASP.NET Core za pomocą programu Visual Studio dla komputerów Mac"
ms.author: riande
manager: wpickett
ms.date: 08/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages-mac/model
ms.openlocfilehash: 7b1b2d54e9c68b0a6f2b1355726d0d1cb484f69e
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="adding-a-model-to-a-razor-pages-app-in-aspnet-core-with-visual-studio-for-mac"></a><span data-ttu-id="e2867-103">Dodawanie modelu do aplikacji stron Razor w ASP.NET Core za pomocą programu Visual Studio dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="e2867-103">Adding a model to a Razor Pages app in ASP.NET Core with Visual Studio for Mac</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="e2867-104">Dodawanie modelu danych</span><span class="sxs-lookup"><span data-stu-id="e2867-104">Add a data model</span></span>

* <span data-ttu-id="e2867-105">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **RazorPagesMovie** projektu, a następnie wybierz **Dodaj** > **nowy Folder**.</span><span class="sxs-lookup"><span data-stu-id="e2867-105">In Solution Explorer, right-click the **RazorPagesMovie** project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="e2867-106">Nazwa folderu *modele*.</span><span class="sxs-lookup"><span data-stu-id="e2867-106">Name the folder *Models*.</span></span>
* <span data-ttu-id="e2867-107">Kliknij prawym przyciskiem myszy *modele* folder, a następnie wybierz **Dodaj** > **nowy plik**.</span><span class="sxs-lookup"><span data-stu-id="e2867-107">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span>
* <span data-ttu-id="e2867-108">W **nowy plik** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="e2867-108">In the **New File** dialog:</span></span>

  * <span data-ttu-id="e2867-109">Wybierz **ogólne** w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="e2867-109">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="e2867-110">Wybierz **pustą klasę** w słabe center.</span><span class="sxs-lookup"><span data-stu-id="e2867-110">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="e2867-111">Nazwa klasy **film** i wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="e2867-111">Name the class **Movie** and select **New**.</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]
[!INCLUDE[model 2a](../../includes/RP/model2a.md)]

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

<span data-ttu-id="e2867-112">Kliknij prawym przyciskiem myszy red linii o dowolnym kształcie, na przykład `MovieContext` w wierszu `services.AddDbContext<MovieContext>(options =>`.</span><span class="sxs-lookup"><span data-stu-id="e2867-112">Right click on a red squiggly line, for example `MovieContext` in the line `services.AddDbContext<MovieContext>(options =>`.</span></span> <span data-ttu-id="e2867-113">Wybierz **Quick Fix > przy użyciu RazorPagesMovie.Models;**.</span><span class="sxs-lookup"><span data-stu-id="e2867-113">Select **Quick Fix > using RazorPagesMovie.Models;**.</span></span> <span data-ttu-id="e2867-114">Dodaje programu Visual studio za pomocą instrukcji.</span><span class="sxs-lookup"><span data-stu-id="e2867-114">Visual studio adds the using statement.</span></span>

<span data-ttu-id="e2867-115">Skompiluj projekt, aby sprawdzić, czy nie zawiera błędów.</span><span class="sxs-lookup"><span data-stu-id="e2867-115">Build the project to verify you don't have any errors.</span></span>

![Tworzenie strony](model/red.png)

### <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="e2867-117">Entity Framework Core NuGet pakietów dla migracji</span><span class="sxs-lookup"><span data-stu-id="e2867-117">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="e2867-118">Narzędzia EF dla interfejsu wiersza polecenia (CLI) są dostępne w [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span><span class="sxs-lookup"><span data-stu-id="e2867-118">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="e2867-119">Aby zainstalować ten pakiet, należy dodać go do `DotNetCliToolReference` kolekcji w *.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="e2867-119">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file.</span></span> <span data-ttu-id="e2867-120">**Uwaga:** należy zainstalować ten pakiet, edytując *.csproj* pliku; nie można użyć `install-package` polecenia lub graficznego interfejsu użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="e2867-120">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span>

<span data-ttu-id="e2867-121">Aby edytować *.csproj* pliku:</span><span class="sxs-lookup"><span data-stu-id="e2867-121">To edit a *.csproj* file:</span></span>

* <span data-ttu-id="e2867-122">Wybierz **pliku** > **Otwórz**, a następnie wybierz *.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="e2867-122">Select **File** > **Open**, and then select the *.csproj* file.</span></span>
* <span data-ttu-id="e2867-123">Wybierz **opcje**.</span><span class="sxs-lookup"><span data-stu-id="e2867-123">Select **Options**.</span></span>
* <span data-ttu-id="e2867-124">Zmień **Otwórz za pomocą** do **Edytor kodu źródłowego**.</span><span class="sxs-lookup"><span data-stu-id="e2867-124">Change **Open with** to **Source Code Editor**.</span></span>

![Edytuj plik csproj](model/csproj.png)

<span data-ttu-id="e2867-126">Dodaj `Microsoft.EntityFrameworkCore.Tools.DotNet` narzędzia odwołanie do drugiego  **\<ItemGroup >**:</span><span class="sxs-lookup"><span data-stu-id="e2867-126">Add the `Microsoft.EntityFrameworkCore.Tools.DotNet` tool reference to the second **\<ItemGroup>**:</span></span>

[!code-xml[Main](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?range=12-16&highlight=4)]

[!INCLUDE[model3](../../includes/RP/model3.md)]
[!INCLUDE[model 4x](../../includes/RP/model4x.md)]

[!INCLUDE[model 4 exit](../../includes/RP/model4exit.md)]

[!INCLUDE[model 4](../../includes/RP/model4.md)]

### <a name="add-the-pagesmovies-files-to-the-project"></a><span data-ttu-id="e2867-127">Dodaj pliki stron/filmów do projektu</span><span class="sxs-lookup"><span data-stu-id="e2867-127">Add the Pages/Movies files to the project</span></span>

* <span data-ttu-id="e2867-128">W programie Visual Studio, kliknij prawym przyciskiem myszy *stron* i wybierz polecenie **Dodaj > Dodaj istniejący Folder**.</span><span class="sxs-lookup"><span data-stu-id="e2867-128">In Visual Studio, Right-click the *Pages* folder and select **Add > Add existing Folder**.</span></span>
* <span data-ttu-id="e2867-129">Wybierz *filmy* folderu.</span><span class="sxs-lookup"><span data-stu-id="e2867-129">Select the *Movies* folder.</span></span>
* <span data-ttu-id="e2867-130">W *Chosse plików do uwzględnienia w projekcie* okno dialogowe, wybierz opcję **obejmują wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="e2867-130">In the *Chosse files to include in the project* dialog, select **Include All**.</span></span>

<span data-ttu-id="e2867-131">Następny samouczek wyjaśnia plików utworzonych przez funkcję szkieletów.</span><span class="sxs-lookup"><span data-stu-id="e2867-131">The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="e2867-132">[Poprzedni: Wprowadzenie](xref:tutorials/razor-pages-mac/razor-pages-start)
[dalej: szkieletu stron Razor](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="e2867-132">[Previous: Getting Started](xref:tutorials/razor-pages-mac/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>