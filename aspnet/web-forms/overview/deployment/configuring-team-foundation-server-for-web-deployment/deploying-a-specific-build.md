---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: "Wdrażanie określonej kompilacji | Dokumentacja firmy Microsoft"
author: jrjlee
description: "W tym temacie opisano sposób wdrażania pakietów sieci web i skryptów bazy danych z określonych ostatniej kompilacji do nowego miejsca docelowego, takich jak środowiska tymczasowym czy produkcyjnym..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: be1000f0cbc2f509f5014789c2bc47ce2b12fb2f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="deploying-a-specific-build"></a><span data-ttu-id="21ece-103">Wdrażanie określonej kompilacji</span><span class="sxs-lookup"><span data-stu-id="21ece-103">Deploying a Specific Build</span></span>
====================
<span data-ttu-id="21ece-104">przez [Lewandowski Jason](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="21ece-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="21ece-105">Pobierz plik PDF</span><span class="sxs-lookup"><span data-stu-id="21ece-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="21ece-106">W tym temacie opisano, jak wdrażać pakiety sieci web i skryptów bazy danych z określonych ostatniej kompilacji do nowego miejsca docelowego, takich jak środowisku tymczasowym czy produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="21ece-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>


<span data-ttu-id="21ece-107">Ten temat jest częścią serii samouczków na podstawie tych wymagań związanych z przedsiębiorstwa wdrażaniem fikcyjnej firmy o nazwie firmy Fabrikam, Inc. Ten samouczek serii używa przykładowe rozwiązanie & #x 2014; [rozwiązania z menedżerem skontaktuj się z](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; do reprezentowania aplikacji sieci web z realistyczne poziom złożoności, w tym aplikacji ASP.NET MVC 3, systemu Windows Usługi Communication Foundation (WCF), a projekt bazy danych.</span><span class="sxs-lookup"><span data-stu-id="21ece-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="21ece-108">Istotą te samouczki metody wdrażania opiera się na podejście pliku projektu podziału opisane w [opis pliku projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), w które procesem kompilacji i wdrażania są kontrolowane przez dwa pliki projektu & #x 2014; IE ne instrukcjami kompilacji, które są stosowane do każdego środowiska docelowego i jeden zawierający ustawienia kompilacji i wdrożenia określonego środowiska.</span><span class="sxs-lookup"><span data-stu-id="21ece-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="21ece-109">W czasie kompilacji pliku projektu określonego środowiska jest scalany pliku projektu niezależny od środowiska pełny zestaw instrukcji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="21ece-110">Omówienie zadań</span><span class="sxs-lookup"><span data-stu-id="21ece-110">Task Overview</span></span>

<span data-ttu-id="21ece-111">Do tej pory tematy w tym zestawie samouczek koncentruje się na temat sposobu tworzenia, pakowanie i wdrażanie aplikacji sieci web i baz danych jako część pojedynczy krok lub zautomatyzowanego procesu.</span><span class="sxs-lookup"><span data-stu-id="21ece-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="21ece-112">Jednak w niektórych typowych scenariuszy, należy wybrać zasoby, które można wdrożyć z listy kompilacji w folderze upuszczania.</span><span class="sxs-lookup"><span data-stu-id="21ece-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="21ece-113">Innymi słowy ostatniej kompilacji nie może być kompilacji, który chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="21ece-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="21ece-114">Rozważmy scenariusz ciągłej integracji (CI) opisana w poprzedniej sekcji, [tworzenie kompilacji definicji czy obsługuje wdrożenia](creating-a-build-definition-that-supports-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="21ece-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="21ece-115">Po utworzeniu definicję kompilacji w Team Foundation Server (TFS) 2010.</span><span class="sxs-lookup"><span data-stu-id="21ece-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="21ece-116">Za każdym razem, gdy dewelopera sprawdza kod do programu TFS, Team Build będzie kompilacji kodu, tworzenie pakietów sieci web i skryptów bazy danych jako część procesu kompilacji, uruchom wszystkie testy jednostkowe i wdrażanie zasobów w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="21ece-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="21ece-117">W zależności od zasad przechowywania skonfigurowane podczas tworzenia definicji kompilacji TFS zachowują pewną liczbę poprzednich wersjach.</span><span class="sxs-lookup"><span data-stu-id="21ece-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="21ece-118">Załóżmy, że zostało wykonane weryfikacji i sprawdzania poprawności testów na jednym z tych kompilacje w środowisku testowym i wszystko jest gotowe do wdrożenia aplikacji w środowisku przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="21ece-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="21ece-119">Tymczasem deweloperzy mogą mieć zaewidencjonowany nowy kod.</span><span class="sxs-lookup"><span data-stu-id="21ece-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="21ece-120">Nie chcesz ponownie skompiluj rozwiązanie, a następnie wdrożyć do środowiska pomostowego, a nie chcesz wdrożyć ostatniej kompilacji w środowisku przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="21ece-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="21ece-121">Zamiast tego którą chcesz wdrożyć określonej kompilacji, które zostały sprawdzone i zatwierdzone na serwerach testowym.</span><span class="sxs-lookup"><span data-stu-id="21ece-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="21ece-122">W tym celu należy sprawdzić, gdzie można znaleźć pakietów sieci web i skryptów bazy danych, które wygenerowanych przez kompilację określonych aparat kompilacji firmy Microsoft (MSBuild).</span><span class="sxs-lookup"><span data-stu-id="21ece-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="21ece-123">Zastępowanie właściwości OutputRoot</span><span class="sxs-lookup"><span data-stu-id="21ece-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="21ece-124">W [przykładowe rozwiązanie](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), *Publish.proj* pliku deklaruje właściwość o nazwie **OutputRoot**.</span><span class="sxs-lookup"><span data-stu-id="21ece-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="21ece-125">Jak wynika z nazwy, to folderu głównego, który zawiera wszystkie elementy, które generuje procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="21ece-126">W *Publish.proj* pliku widać, że **OutputRoot** właściwość odwołuje się do lokalizacji głównej dla wszystkich zasobów wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21ece-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="21ece-127">**OutputRoot** jest nazwą właściwości często używane.</span><span class="sxs-lookup"><span data-stu-id="21ece-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="21ece-128">Pliki projektu Visual C# i Visual Basic również zadeklarować tej właściwości do przechowywania katalog główny dla wszystkich plików wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>


[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]


<span data-ttu-id="21ece-129">Jeśli chcesz, aby plik projektu do wdrażania pakietów sieci web i skryptów bazy danych z innej lokalizacji & #x 2014; takich jak dane wyjściowe poprzedniego kompilacji TFS & #x 2014; musisz po prostu zastąpić **OutputRoot** właściwości.</span><span class="sxs-lookup"><span data-stu-id="21ece-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="21ece-130">Wartość właściwości należy ustawić do folderu odpowiednich kompilacji na serwerze programu Team Build.</span><span class="sxs-lookup"><span data-stu-id="21ece-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="21ece-131">Jeśli podczas uruchamiania programu MSBuild w wierszu polecenia, można określić wartość dla **OutputRoot** jako argument wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="21ece-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]


<span data-ttu-id="21ece-132">W praktyce, czy też chcesz pominąć **kompilacji** docelowej & #x 2014; nie ma żadnych punktu tworzenia rozwiązania, jeśli nie zamierzasz korzystać z danych wyjściowych kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="21ece-133">Można to zrobić, określając obiektów docelowych, które chcesz wykonać z poziomu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="21ece-133">You could do this by specifying the targets you want to execute from the command line:</span></span>


[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]


<span data-ttu-id="21ece-134">Jednak w większości przypadków należy do tworzenia logiki wdrożenia do definicji kompilacji TFS.</span><span class="sxs-lookup"><span data-stu-id="21ece-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="21ece-135">Dzięki temu użytkownicy z **kolejka kompilacji** uprawnień, aby wyzwolić wdrożenie z żadnej instalacji programu Visual Studio z połączeniem z serwerem TFS.</span><span class="sxs-lookup"><span data-stu-id="21ece-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="21ece-136">Tworzenie definicji kompilacji do wdrożenia w określonej kompilacji</span><span class="sxs-lookup"><span data-stu-id="21ece-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="21ece-137">Następna procedura opisuje sposób tworzenia definicji kompilacji, która umożliwia użytkownikom wyzwalacza wdrożenia w środowisku przemieszczania za pomocą jednego polecenia.</span><span class="sxs-lookup"><span data-stu-id="21ece-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="21ece-138">W takim przypadku nie ma definicji kompilacji zbudowaniem niczego & #x 2014; możesz po prostu go do wykonania w pliku projektu niestandardowej logiki wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21ece-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="21ece-139">*Publish.proj* plik zawiera logikę warunkową, z pominięciem **kompilacji** docelowych, jeśli plik jest uruchomiona w Team Build.</span><span class="sxs-lookup"><span data-stu-id="21ece-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="21ece-140">Jest to możliwe dzięki wbudowanej oceny **BuildingInTeamBuild** właściwość, która jest automatycznie ustawiana **true** po uruchomieniu pliku projektu w Team Build.</span><span class="sxs-lookup"><span data-stu-id="21ece-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="21ece-141">W związku z tym można pominąć proces kompilacji i wystarczy uruchomić plik projektu do kompilacji istniejącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21ece-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="21ece-142">**Aby utworzyć definicję kompilacji, aby wyzwolić wdrożenie ręcznie**</span><span class="sxs-lookup"><span data-stu-id="21ece-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="21ece-143">W programie Visual Studio 2010 w **Team Explorer** okna, rozwiń węzeł projektu zespołowego, kliknij prawym przyciskiem myszy **kompilacje**, a następnie kliknij przycisk **nową definicję kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="21ece-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="21ece-144">Na **ogólne** karcie, nadaj nazwę definicji kompilacji (na przykład **DeployToStaging**) i opcjonalny opis.</span><span class="sxs-lookup"><span data-stu-id="21ece-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="21ece-145">Na **wyzwalacza** wybierz opcję **ręcznego — zaewidencjonowania nie wyzwalają nowej kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="21ece-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="21ece-146">Na **kompilacji domyślne** karcie **Kopiuj dane wyjściowe kompilacji do następującego folderu docelowego** wpisz ścieżkę Universal Naming Convention (UNC) z folderu docelowego (na przykład  **\\TFSBUILD\Drops**).</span><span class="sxs-lookup"><span data-stu-id="21ece-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="21ece-147">Na **procesu** karcie **pliku procesu kompilacji** listy rozwijanej, pozostaw **DefaultTemplate.xaml** wybrane.</span><span class="sxs-lookup"><span data-stu-id="21ece-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="21ece-148">Jest to jeden z szablonów domyślnych procesów kompilacji, które zostaną dodane do wszystkich nowych projektów zespołowych.</span><span class="sxs-lookup"><span data-stu-id="21ece-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="21ece-149">W **parametrów procesu kompilacji** tabeli, kliknij przycisk **elementów do kompilacji** wiersza, a następnie kliknij przycisk **wielokropka** przycisku.</span><span class="sxs-lookup"><span data-stu-id="21ece-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="21ece-150">W **elementów do kompilacji** okno dialogowe, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="21ece-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="21ece-151">W **elementów typu** listy rozwijanej wybierz **pliki projektu MSBuild**.</span><span class="sxs-lookup"><span data-stu-id="21ece-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="21ece-152">Przejdź do lokalizacji pliku projektu niestandardowe, z którym można kontrolować proces wdrażania, wybierz plik, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="21ece-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="21ece-153">W **elementów do kompilacji** okno dialogowe, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="21ece-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="21ece-154">W **parametrów procesu kompilacji** tabeli, a następnie rozwiń **zaawansowane** sekcji.</span><span class="sxs-lookup"><span data-stu-id="21ece-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="21ece-155">W **argumenty programu MSBuild** wiersz, określ lokalizację pliku projektu określonego środowiska i dodać symbol zastępczy dla lokalizacji folderu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="21ece-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="21ece-156">Należy zastąpić **OutputRoot** wartość za każdym razem, gdy kolejka kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="21ece-157">Ten temat znajdują się w następnej procedurze.</span><span class="sxs-lookup"><span data-stu-id="21ece-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="21ece-158">Kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="21ece-158">Click **Save**.</span></span>

<span data-ttu-id="21ece-159">Gdy wyzwolić kompilację, musisz zaktualizować **OutputRoot** właściwości, aby wskazywał kompilacji, którą chcesz wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="21ece-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="21ece-160">**Aby wdrożyć określonej kompilacji z definicji kompilacji**</span><span class="sxs-lookup"><span data-stu-id="21ece-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="21ece-161">W **Team Explorer** okna, kliknij prawym przyciskiem myszy definicję kompilacji, a następnie kliknij przycisk **Tworzenie nowej kolejki**.</span><span class="sxs-lookup"><span data-stu-id="21ece-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="21ece-162">W **kolejka kompilacji** na okna dialogowego **parametry** karcie, rozwiń **zaawansowane** sekcji.</span><span class="sxs-lookup"><span data-stu-id="21ece-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="21ece-163">W **argumenty programu MSBuild** wiersz, zastąp wartość **OutputRoot** właściwość o lokalizację folderu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="21ece-164">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="21ece-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="21ece-165">Należy uwzględnić kreskę ułamkową odwróconą na końcu ścieżki do folderu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="21ece-166">Kliknij przycisk **kolejki**.</span><span class="sxs-lookup"><span data-stu-id="21ece-166">Click **Queue**.</span></span>

<span data-ttu-id="21ece-167">Gdy kolejka kompilacji, plik projektu zostanie wdrożona skryptów bazy danych i sieci web pakiety z folderu przechowywania kompilacji podana w **OutputRoot** właściwości.</span><span class="sxs-lookup"><span data-stu-id="21ece-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="21ece-168">Wniosek</span><span class="sxs-lookup"><span data-stu-id="21ece-168">Conclusion</span></span>

<span data-ttu-id="21ece-169">W tym temacie opisano sposób publikowania zasobów wdrożenia, takie jak pakiety sieci web i skryptów bazy danych, z poprzedniej określonej kompilacji przy użyciu modelu wdrażania pliku projektu podziału.</span><span class="sxs-lookup"><span data-stu-id="21ece-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="21ece-170">Go wyjaśniono sposób przesłonięcia **OutputRoot** właściwości i jak włączyć logiki wdrożenia do TFS definicji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="21ece-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="21ece-171">Dalsze informacje</span><span class="sxs-lookup"><span data-stu-id="21ece-171">Further Reading</span></span>

<span data-ttu-id="21ece-172">Aby uzyskać więcej informacji na temat tworzenia definicje kompilacji, zobacz [utworzyć podstawową definicję kompilacji](https://msdn.microsoft.com/library/ms181716.aspx) i [Definiowanie procesu kompilacji](https://msdn.microsoft.com/library/ms181715.aspx).</span><span class="sxs-lookup"><span data-stu-id="21ece-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="21ece-173">Aby uzyskać więcej pomocy w przypadku kompilacji usługi kolejkowania wiadomości, zobacz [kolejki kompilację](https://msdn.microsoft.com/library/ms181722.aspx).</span><span class="sxs-lookup"><span data-stu-id="21ece-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="21ece-174">[Poprzednie](creating-a-build-definition-that-supports-deployment.md)
[dalej](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="21ece-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>