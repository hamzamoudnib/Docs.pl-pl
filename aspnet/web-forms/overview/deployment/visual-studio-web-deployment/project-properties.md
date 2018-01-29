---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: "Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: właściwości projektu | Dokumentacja firmy Microsoft"
author: tdykstra
description: "Ta seria samouczek pokazuje, jak wdrożyć platformy ASP.NET (publikowanie) aplikacji do aplikacji sieci Web usługi aplikacji Azure lub innego dostawcy hostingu sieci web przez używane..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: 85b6dbcc8d40c168a49513ef6b549f9ec7fa5097
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-web-deployment-using-visual-studio-project-properties"></a><span data-ttu-id="791ec-103">Wdrażanie sieci Web ASP.NET przy użyciu programu Visual Studio: właściwości projektu</span><span class="sxs-lookup"><span data-stu-id="791ec-103">ASP.NET Web Deployment using Visual Studio: Project Properties</span></span>
====================
<span data-ttu-id="791ec-104">przez [Dykstra niestandardowy](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="791ec-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="791ec-105">Pobierz początkowego projektu</span><span class="sxs-lookup"><span data-stu-id="791ec-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="791ec-106">Ta seria samouczek pokazuje, jak wdrożyć platformy ASP.NET (publikowanie) aplikacji do aplikacji sieci Web usługi aplikacji Azure lub innego dostawcy hostingu sieci web za pomocą programu Visual Studio 2012 lub Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="791ec-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="791ec-107">Aby uzyskać informacje dotyczące serii, zobacz [pierwszy samouczek z tej serii](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="791ec-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="791ec-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="791ec-108">Overview</span></span>

<span data-ttu-id="791ec-109">Niektóre opcje wdrażania są skonfigurowane we właściwościach projektu, które są przechowywane w pliku projektu ( *.csproj* lub *vbproj* pliku).</span><span class="sxs-lookup"><span data-stu-id="791ec-109">Some deployment options are configured in project properties that are stored in the project file (the *.csproj* or *.vbproj* file).</span></span> <span data-ttu-id="791ec-110">W większości przypadków domyślne wartości tych ustawień są, co ma, ale może użyć **właściwości projektu** wbudowane interfejsu użytkownika w Visual Studio, aby pracować przy użyciu tych ustawień, jeśli trzeba je zmienić.</span><span class="sxs-lookup"><span data-stu-id="791ec-110">In most cases, the default values of these settings are what you want, but you can use the **Project Properties** UI built into Visual Studio to work with these settings if you have to change them.</span></span> <span data-ttu-id="791ec-111">W tym samouczku można przejrzeć ustawienia wdrażania **właściwości projektu**.</span><span class="sxs-lookup"><span data-stu-id="791ec-111">In this tutorial you review the deployment settings in **Project Properties**.</span></span> <span data-ttu-id="791ec-112">Można również utworzyć pliku symbolu zastępczego, który powoduje, że pusty folder, który można wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="791ec-112">You also create a placeholder file that causes an empty folder to be deployed.</span></span>

## <a name="configure-deployment-settings-in-the-project-properties-window"></a><span data-ttu-id="791ec-113">Konfigurowanie ustawień wdrażania w oknie właściwości projektu</span><span class="sxs-lookup"><span data-stu-id="791ec-113">Configure deployment settings in the project properties window</span></span>

<span data-ttu-id="791ec-114">Większość ustawień, które mają wpływ na co się dzieje podczas wdrażania znajdują się w profilu publikowania, jak można zauważyć w następujących samouczkach.</span><span class="sxs-lookup"><span data-stu-id="791ec-114">Most settings that affect what happens during deployment are included in the publish profile, as you'll see in the following tutorials.</span></span> <span data-ttu-id="791ec-115">Kilka ustawień, które należy zwrócić uwagę znajdują się w **pakowania/publikowania** karty **właściwości projektu** okna.</span><span class="sxs-lookup"><span data-stu-id="791ec-115">A few settings that you should be aware of are located in the **Package/Publish** tabs of the **Project Properties** window.</span></span> <span data-ttu-id="791ec-116">Te ustawienia są określone dla każdej konfiguracji kompilacji — to znaczy może mieć różne ustawienia dla kompilacji wydania niż liczba kupionych dla kompilacji debugowania.</span><span class="sxs-lookup"><span data-stu-id="791ec-116">These settings are specified for each build configuration — that is, you can have different settings for a Release build than you have for a Debug build.</span></span>

<span data-ttu-id="791ec-117">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **ContosoUniversity** projektu, zaznacz **właściwości**, a następnie wybierz **pakowaniu/publikowaniu Web**kartę.</span><span class="sxs-lookup"><span data-stu-id="791ec-117">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Properties**, and then select the **Package/Publish Web** tab.</span></span>

![Karta pakowaniu/publikowaniu Web](project-properties/_static/image1.png)

<span data-ttu-id="791ec-119">Po wyświetleniu okna domyślnie wyświetlane ustawienia dla jednego z tych konfiguracji kompilacji jest obecnie aktywna dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="791ec-119">When the window is displayed, it defaults to showing settings for whichever build configuration is currently active for the solution.</span></span> <span data-ttu-id="791ec-120">Jeśli **konfiguracji** pole nie wskazuje **aktywny (wersja)**, wybierz pozycję **wersji** Aby wyświetlić ustawienia konfiguracji kompilacji wydania.</span><span class="sxs-lookup"><span data-stu-id="791ec-120">If the **Configuration** box does not indicate **Active (Release)**, select **Release** in order to display settings for the Release build configuration.</span></span> <span data-ttu-id="791ec-121">Poniżej przedstawiono wdrażania kompilacjami wydania ze środowiskami testowego i produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="791ec-121">You'll deploy Release builds to both your test and production environments.</span></span>

![Wybieranie konfiguracji kompilacji wydania](project-properties/_static/image2.png)

<span data-ttu-id="791ec-123">Z **aktywny (wersja)** lub **wersji** zaznaczone, zobacz wartości, które są efektywne w przypadku wdrażania przy użyciu konfiguracji kompilacji wydania:</span><span class="sxs-lookup"><span data-stu-id="791ec-123">With **Active (Release)** or **Release** selected, you see the values that are effective when you deploy using the Release build configuration:</span></span>

- <span data-ttu-id="791ec-124">W **elementy do wdrożenia** okno, **tylko pliki potrzebne do uruchomienia aplikacji** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="791ec-124">In the **Items to deploy** box, **Only files needed to run the application** is selected.</span></span> <span data-ttu-id="791ec-125">Inne opcje są **wszystkie pliki w tym projekcie** lub **wszystkie pliki w tym folderze projektu**.</span><span class="sxs-lookup"><span data-stu-id="791ec-125">Other options are **All files in this project** or **All files in this project folder**.</span></span> <span data-ttu-id="791ec-126">Pozostawić wybór domyślny, bez zmian można uniknąć, wdrażanie plików kodu źródłowego, np.</span><span class="sxs-lookup"><span data-stu-id="791ec-126">By leaving the default selection unchanged you avoid deploying source code files, for example.</span></span> <span data-ttu-id="791ec-127">To ustawienie jest powód, dlaczego foldery zawierające pliki binarne programu SQL Server Compact musiały być dołączony do projektu.</span><span class="sxs-lookup"><span data-stu-id="791ec-127">This setting is the reason why the folders that contain the SQL Server Compact binary files had to be included in the project.</span></span> <span data-ttu-id="791ec-128">Aby uzyskać więcej informacji o tym ustawieniu, zobacz **Dlaczego nie wszystkie pliki w folderze projektu wdrożony?** w [ASP.NET sieci Web aplikacji projektu wdrożenia — często zadawane pytania](https://msdn.microsoft.com/library/ee942158.aspx).</span><span class="sxs-lookup"><span data-stu-id="791ec-128">For more information about this setting, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx).</span></span>
- <span data-ttu-id="791ec-129">**Symbole debugowania Wyklucz wygenerowany** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="791ec-129">**Exclude generated debug symbols** is selected.</span></span> <span data-ttu-id="791ec-130">Nie można debugowania używania tej konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="791ec-130">You won't be debugging when you use this build configuration.</span></span>
- <span data-ttu-id="791ec-131">**Obejmują wszystkie baz danych skonfigurowanych na karcie pakowanie/publikowanie SQL** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="791ec-131">**Include all databases configured in Package/Publish SQL tab** is selected.</span></span> <span data-ttu-id="791ec-132">Określa, czy program Visual Studio wdroży baz danych, a także pliki.</span><span class="sxs-lookup"><span data-stu-id="791ec-132">Specifies whether Visual Studio will deploy databases as well as files.</span></span> <span data-ttu-id="791ec-133">Mimo że pole wyboru etykiety uwagi tylko **Pakuj/Publikuj SQL** kartę, czyszczenie tego pola wyboru spowoduje również wyłączenie wdrażania bazy danych, skonfigurowanego w profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="791ec-133">Although the check box label only mentions the **Package/Publish SQL** tab, clearing this check box would also disable database deployment that is configured in the publish profile.</span></span> <span data-ttu-id="791ec-134">Użytkownik będzie można grozi to który później, pole wyboru musi pozostać zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="791ec-134">You will be doing that later, so the check box must remain selected.</span></span> <span data-ttu-id="791ec-135">**Pakuj/Publikuj SQL** karcie jest używana do publikowania metodę, która nie będzie używany w tych samouczkach starszej wersji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="791ec-135">The **Package/Publish SQL** tab is used for a legacy database publishing method that you won't be using in these tutorials.</span></span>
- <span data-ttu-id="791ec-136">**Ustawienia pakietu wdrażania Web** sekcja nie ma zastosowania, ponieważ używasz jednym kliknięciem publikowania w tych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="791ec-136">The **Web Deployment Package Settings** section does not apply because you're using one-click publish in these tutorials.</span></span>

<span data-ttu-id="791ec-137">Zmień **konfiguracji** pole listy rozwijanej do debugowania, aby wyświetlić ustawienia domyślne dla kompilacji debugowania.</span><span class="sxs-lookup"><span data-stu-id="791ec-137">Change the **Configuration** drop-down box to Debug to see the default settings for Debug builds.</span></span> <span data-ttu-id="791ec-138">Wartości są takie same, z wyjątkiem **Wyklucz wygenerowano symbole debugowania** jest wyczyszczone, dzięki czemu można debugować po wdrożeniu kompilacji debugowania.</span><span class="sxs-lookup"><span data-stu-id="791ec-138">The values are the same, except **Exclude generated debug symbols** is cleared so that you can debug when you deploy a Debug build.</span></span>

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a><span data-ttu-id="791ec-139">Upewnij się, że Elmah folder zostanie wdrożona</span><span class="sxs-lookup"><span data-stu-id="791ec-139">Make sure that the Elmah folder gets deployed</span></span>

<span data-ttu-id="791ec-140">Jak przedstawiono w samouczku poprzedniej [pakietu Elmah NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) zapewnia funkcje Błąd rejestrowania i raportowania.</span><span class="sxs-lookup"><span data-stu-id="791ec-140">As you saw in the previous tutorial, the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) provides functionality for error logging and reporting.</span></span> <span data-ttu-id="791ec-141">W aplikacji Contoso University Elmah został skonfigurowany do przechowywania szczegóły błędu w folderze o nazwie *Elmah*:</span><span class="sxs-lookup"><span data-stu-id="791ec-141">In the Contoso University application Elmah has been configured to store error details in a folder named *Elmah*:</span></span>

![Elmah folder](project-properties/_static/image3.png)

<span data-ttu-id="791ec-143">Wykluczenie określonych plików lub folderów z wdrożenia jest typowym wymaganiem; innym przykładem może być folderu, w którym użytkownicy mogą przekazać pliki do.</span><span class="sxs-lookup"><span data-stu-id="791ec-143">Excluding specific files or folders from deployment is a common requirement; another example would be a folder that users can upload files to.</span></span> <span data-ttu-id="791ec-144">Nie ma plików dziennika lub przekazać pliki, które zostały utworzone w środowisku projektowania wdrożenia do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="791ec-144">You don't want log files or uploaded files that were created in your development environment to be deployed to production.</span></span> <span data-ttu-id="791ec-145">A jeśli wdrażasz aktualizacji w środowisku produkcyjnym nie chcesz, aby proces wdrażania, aby usunąć pliki, które istnieją w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="791ec-145">And if you are deploying an update to production you don't want the deployment process to delete files that exist in production.</span></span> <span data-ttu-id="791ec-146">(W zależności od tego, jak ustawisz opcję wdrażania, jeśli istnieje plik w lokacji docelowej, ale nie w lokacji źródłowej, podczas wdrażania, narzędzie Web Deploy spowoduje usunięcie go z docelowego).</span><span class="sxs-lookup"><span data-stu-id="791ec-146">(Depending on how you set a deployment option, if a file exists in the destination site but not the source site when you deploy, Web Deploy deletes it from the destination.)</span></span>

<span data-ttu-id="791ec-147">Jak przedstawiono wcześniej w tym samouczku **elementy do wdrożenia** opcji **pakowaniu/publikowaniu Web** ustawiono kartę **tylko pliki potrzebne do uruchomienia tej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="791ec-147">As you saw earlier in this tutorial, the **Items to deploy** option in the **Package/Publish Web** tab is set to **Only Files Needed to run this application**.</span></span> <span data-ttu-id="791ec-148">W związku z tym plików dziennika, które są tworzone przez Elmah rozwijany nie zostanie wdrożony, czyli ma nastąpić.</span><span class="sxs-lookup"><span data-stu-id="791ec-148">As a result, log files that are created by Elmah in development will not be deployed, which is what you want to happen.</span></span> <span data-ttu-id="791ec-149">(Zostać wdrożony, zostałyby do uwzględnienia w projekcie i ich **Akcja kompilacji** musi mieć ustawioną właściwość **zawartości**.</span><span class="sxs-lookup"><span data-stu-id="791ec-149">(To be deployed, they would have to be included in the project and their **Build Action** property would have to be set to **Content**.</span></span> <span data-ttu-id="791ec-150">Aby uzyskać więcej informacji, zobacz **Dlaczego nie wszystkie pliki w folderze projektu wdrożony?** w [ASP.NET sieci Web aplikacji projektu wdrożenia — często zadawane pytania](https://msdn.microsoft.com/library/ee942158.aspx)).</span><span class="sxs-lookup"><span data-stu-id="791ec-150">For more information, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx)).</span></span> <span data-ttu-id="791ec-151">Jednak narzędzia Web Deploy nie utworzy folder w lokacji docelowej, chyba że istnieje co najmniej jeden plik, aby skopiować na nią.</span><span class="sxs-lookup"><span data-stu-id="791ec-151">However, Web Deploy will not create a folder in the destination site unless there's at least one file to copy to it.</span></span> <span data-ttu-id="791ec-152">W związku z tym należy dodać *.txt* plik do folderu na działanie jako symbolu zastępczego, dzięki czemu będzie można skopiować folderu.</span><span class="sxs-lookup"><span data-stu-id="791ec-152">Therefore, you'll add a *.txt* file to the folder to act as a placeholder so that the folder will be copied.</span></span>

<span data-ttu-id="791ec-153">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy *Elmah* folderu, wybierz opcję **Dodaj nowy element**i Utwórz plik tekstowy o nazwie *Placeholder.txt*.</span><span class="sxs-lookup"><span data-stu-id="791ec-153">In **Solution Explorer**, right-click the *Elmah* folder, select **Add New Item**, and create a text file named *Placeholder.txt*.</span></span> <span data-ttu-id="791ec-154">Umieść w nim następujący tekst: "Jest to plik symbolu zastępczego, aby upewnić się, że folder zostanie wdrożona".</span><span class="sxs-lookup"><span data-stu-id="791ec-154">Put the following text in it: "This is a placeholder file to ensure that the folder gets deployed."</span></span> <span data-ttu-id="791ec-155">I Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="791ec-155">and save the file.</span></span> <span data-ttu-id="791ec-156">To wszystko, musisz wykonać, aby mieć pewność, że program Visual Studio wdroży tego pliku i folderu w, ponieważ **Akcja kompilacji** właściwość *.txt* plików ma ustawioną wartość **zawartości**domyślnie.</span><span class="sxs-lookup"><span data-stu-id="791ec-156">That's all you have to do in order to make sure that Visual Studio deploys this file and the folder it's in, because the **Build Action** property of *.txt* files is set to **Content** by default.</span></span>

## <a name="summary"></a><span data-ttu-id="791ec-157">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="791ec-157">Summary</span></span>

<span data-ttu-id="791ec-158">Ukończono wszystkie zadania konfiguracji wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="791ec-158">You have now completed all of the deployment set-up tasks.</span></span> <span data-ttu-id="791ec-159">W następnym samouczku możesz wdrożyć witrynę Contoso University do środowiska testowego i przetestować go brak.</span><span class="sxs-lookup"><span data-stu-id="791ec-159">In the next tutorial, you'll deploy the Contoso University site to the test environment and test it there.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="791ec-160">[Poprzednie](web-config-transformations.md)
[dalej](deploying-to-iis.md)</span><span class="sxs-lookup"><span data-stu-id="791ec-160">[Previous](web-config-transformations.md)
[Next](deploying-to-iis.md)</span></span>