---
title: "Kompilacja widoku razor i wstępnej kompilacji"
author: rick-anderson
description: "Dokument odwołanie wyjaśniający, jak włączyć kompilacji widoku MVC Razor i wstępnej kompilacji w aplikacji platformy ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 12/13/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/view-compilation
ms.openlocfilehash: 87989455c2fb6b5a922c7fb6133aa3e8cef42c88
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="razor-view-compilation-and-precompilation-in-aspnet-core"></a><span data-ttu-id="af4ff-103">Kompilacja widoku razor i wstępnej kompilacji w ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="af4ff-103">Razor view compilation and precompilation in ASP.NET Core</span></span>

<span data-ttu-id="af4ff-104">Przez [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="af4ff-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="af4ff-105">Widokami razor są kompilowane w czasie wykonywania, gdy widok jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="af4ff-105">Razor views are compiled at runtime when the view is invoked.</span></span> <span data-ttu-id="af4ff-106">ASP.NET podstawowe 1.1.0 i wyższe można opcjonalnie widokami Razor skompilować i wdrożyć je z aplikacją&mdash;proces znany jako wstępnej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="af4ff-106">ASP.NET Core 1.1.0 and higher can optionally compile Razor views and deploy them with the app&mdash;a process known as precompilation.</span></span> <span data-ttu-id="af4ff-107">Szablony projektów platformy ASP.NET Core 2.x domyślnie włączone wstępnej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="af4ff-107">The ASP.NET Core 2.x project templates enable precompilation by default.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af4ff-108">Wstępnej kompilacji widoku razor jest obecnie niedostępna podczas wykonywania [niezależne wdrożenia (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) w programie ASP.NET 2.0 Core.</span><span class="sxs-lookup"><span data-stu-id="af4ff-108">Razor view precompilation is currently unavailable when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span> <span data-ttu-id="af4ff-109">Funkcja będzie dostępna dla SCDs, gdy zwalnia 2.1.</span><span class="sxs-lookup"><span data-stu-id="af4ff-109">The feature will be available for SCDs when 2.1 releases.</span></span> <span data-ttu-id="af4ff-110">Aby uzyskać więcej informacji, zobacz [widoku kompilacja zakończy się niepowodzeniem, podczas kompilowania między dla systemu Linux w systemie Windows](https://github.com/aspnet/MvcPrecompilation/issues/102).</span><span class="sxs-lookup"><span data-stu-id="af4ff-110">For more information, see [View compilation fails when cross-compiling for Linux on Windows](https://github.com/aspnet/MvcPrecompilation/issues/102).</span></span>

<span data-ttu-id="af4ff-111">Kwestie do rozważenia wstępnej kompilacji:</span><span class="sxs-lookup"><span data-stu-id="af4ff-111">Precompilation considerations:</span></span>

* <span data-ttu-id="af4ff-112">Prekompilowanie widoków powoduje mniejsze opublikowanego pakietu i skrócić czas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="af4ff-112">Precompiling views results in a smaller published bundle and faster startup time.</span></span>
* <span data-ttu-id="af4ff-113">Nie można edytować pliki Razor prekompilowanie widoków.</span><span class="sxs-lookup"><span data-stu-id="af4ff-113">You can't edit Razor files after you precompile views.</span></span> <span data-ttu-id="af4ff-114">Edytowany widoków nie będzie znajdować się w opublikowanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="af4ff-114">The edited views won't be present in the published bundle.</span></span> 

<span data-ttu-id="af4ff-115">Aby wdrożyć prekompilowany widoków:</span><span class="sxs-lookup"><span data-stu-id="af4ff-115">To deploy precompiled views:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="af4ff-116">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="af4ff-116">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="af4ff-117">Jeśli projekt jest przeznaczony dla środowiska .NET Framework, zawierać odwołanie do pakietu [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span><span class="sxs-lookup"><span data-stu-id="af4ff-117">If your project targets .NET Framework, include a package reference to [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span></span>

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

<span data-ttu-id="af4ff-118">Jeśli projekt jest przeznaczony dla platformy .NET Core, żadne zmiany nie są niezbędne.</span><span class="sxs-lookup"><span data-stu-id="af4ff-118">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="af4ff-119">Szablony projektów platformy ASP.NET Core 2.x ustawiane niejawnie `MvcRazorCompileOnPublish` do `true` domyślnie oznacza tego węzła można bezpiecznie usunąć z *.csproj* pliku.</span><span class="sxs-lookup"><span data-stu-id="af4ff-119">The ASP.NET Core 2.x project templates implicitly set `MvcRazorCompileOnPublish` to `true` by default, which means this node can be safely removed from the *.csproj* file.</span></span> <span data-ttu-id="af4ff-120">Jeśli wolisz można jawne, nie powoduje żadnych problemów w ustawieniu `MvcRazorCompileOnPublish` właściwości `true`.</span><span class="sxs-lookup"><span data-stu-id="af4ff-120">If you prefer to be explicit, there's no harm in setting the `MvcRazorCompileOnPublish` property to `true`.</span></span> <span data-ttu-id="af4ff-121">Następujące *.csproj* przykładzie wyróżniono tego ustawienia:</span><span class="sxs-lookup"><span data-stu-id="af4ff-121">The following *.csproj* sample highlights this setting:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish2.csproj?highlight=5)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="af4ff-122">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="af4ff-122">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="af4ff-123">Ustaw `MvcRazorCompileOnPublish` do `true`i zawiera odwołanie do pakietu `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`.</span><span class="sxs-lookup"><span data-stu-id="af4ff-123">Set `MvcRazorCompileOnPublish` to `true`, and include a package reference to `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`.</span></span> <span data-ttu-id="af4ff-124">Następujące *.csproj* przykładzie wyróżniono te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="af4ff-124">The following *.csproj* sample highlights these settings:</span></span>

[!code-xml[Main](view-compilation\sample\MvcRazorCompileOnPublish.csproj?highlight=5,12)]

---

<span data-ttu-id="af4ff-125">Przygotowanie aplikacji dla [wdrożenia zależne od framework](/dotnet/core/deploying/#framework-dependent-deployments-fdd) , wykonując polecenie, takie jak wymienione poniżej w katalogu głównym projektu:</span><span class="sxs-lookup"><span data-stu-id="af4ff-125">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) by executing a command such as the following at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="af4ff-126">A *< project_name >. PrecompiledViews.dll* zawierający skompilowanych widokami Razor, jest generowany po wstępnej kompilacji zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="af4ff-126">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor views, is produced when precompilation succeeds.</span></span> <span data-ttu-id="af4ff-127">Na przykład poniższy zrzut ekranu przedstawia zawartość *Index.cshtml* wewnątrz *WebApplication1.PrecompiledViews.dll*:</span><span class="sxs-lookup"><span data-stu-id="af4ff-127">For example, the screenshot below depicts the contents of *Index.cshtml* inside of *WebApplication1.PrecompiledViews.dll*:</span></span>

![Widokami razor wewnątrz biblioteki DLL](view-compilation/_static/razor-views-in-dll.png)