---
uid: mvc/overview/getting-started/database-first-development/publish-to-azure
title: Publikowanie witryny MVC Database First Azure | Dokumentacja firmy Microsoft
author: tfitzmac
description: "Przy użyciu MVC, Entity Framework i szkieletów ASP.NET, można utworzyć aplikacji sieci web, która zapewnia interfejs do istniejącej bazy danych. Ten samouczek seri..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/22/2014
ms.topic: article
ms.assetid: 7131f1c1-cef3-4396-ab44-ed4519676546
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/publish-to-azure
msc.type: authoredcontent
ms.openlocfilehash: eadc0f2b08df29f80fe53d03cf88cd3cdcecfb12
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="publish-mvc-database-first-site-to-azure"></a><span data-ttu-id="61334-104">Publikowanie MVC bazy danych pierwszej lokacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="61334-104">Publish MVC Database First site to Azure</span></span>
====================
<span data-ttu-id="61334-105">przez [FitzMacken niestandardowy](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="61334-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="61334-106">Przy użyciu MVC, Entity Framework i szkieletów ASP.NET, można utworzyć aplikacji sieci web, która zapewnia interfejs do istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="61334-107">Ta seria samouczka przedstawiono sposób automatycznego generowania kodu, która umożliwia użytkownikom wyświetlanie, edytowanie, tworzenie i Usuń dane, które znajdują się w tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="61334-108">Wygenerowany kod odnosi się do kolumn w tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="61334-109">Ta część serii koncentruje się na publikowania aplikacji sieci web i bazy danych do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-109">This part of the series focuses on publishing the web app and database to Azure.</span></span> <span data-ttu-id="61334-110">W tym temacie, aby dowiedzieć się więcej na temat publikowania aplikacji sieci web i bazy danych, ale do rzeczywistego wykonania czynności, które należy uruchomić na początku tego samouczka można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="61334-110">You can read this topic to learn about publishing a web app and database, but to actually perform the steps you must start at the beginning of the tutorial.</span></span> <span data-ttu-id="61334-111">Zobacz [wprowadzenie](setting-up-database.md).</span><span class="sxs-lookup"><span data-stu-id="61334-111">See [Getting Started](setting-up-database.md).</span></span>


## <a name="deploy-your-web-app-on-azure"></a><span data-ttu-id="61334-112">Wdrażanie aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="61334-112">Deploy your web app on Azure</span></span>

<span data-ttu-id="61334-113">Potrzebne jest konto platformy Azure do ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="61334-113">You need an Azure account to complete this tutorial:</span></span>

- <span data-ttu-id="61334-114">Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) — otrzymasz kredyt służy do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu kredytu możesz zachować konto i korzystać z bezpłatnych usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-114">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="61334-115">Możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) -subskrypcji Your MSDN otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-115">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

<span data-ttu-id="61334-116">Aby opublikować aplikację sieci web, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="61334-116">To publish your web app, right-click the project and select **Publish**.</span></span>

![Publikowanie witryny](publish-to-azure/_static/image1.png)

<span data-ttu-id="61334-118">Wybierz witryny sieci Web platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-118">Select Microsoft Azure Websites.</span></span>

![Wybierz pozycję Azure](publish-to-azure/_static/image2.png)

<span data-ttu-id="61334-120">Jeśli użytkownik nie jest zalogowany na platformie Azure, podaj poświadczenia konta Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-120">If you are not signed in to Azure, provide your Azure account credentials.</span></span> <span data-ttu-id="61334-121">Następnie wybierz nowy, aby utworzyć nową aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="61334-121">Then, select New to create a new web app.</span></span>

![nową lokację](publish-to-azure/_static/image3.png)

<span data-ttu-id="61334-123">Utworzyć unikatową nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="61334-123">Create a unique name for your web app.</span></span> <span data-ttu-id="61334-124">Jeśli zostanie wyświetlony zielony znacznik wyboru z prawej strony pola Nazwa będzie wiadomo się, że nazwa jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="61334-124">You will know the name is unique if you see a green check mark to the right of the name field.</span></span> <span data-ttu-id="61334-125">Wybierz region aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="61334-125">Select a region for your web app.</span></span> <span data-ttu-id="61334-126">Wybierz **Utwórz nowy serwer** dla bazy danych i podaj nazwę użytkownika i hasło dla nowego serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-126">Select **Create new server** for the database, and provide a user name and password for this new database server.</span></span> <span data-ttu-id="61334-127">Gdy skończysz, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="61334-127">When finished, click **Create**.</span></span>

![Tworzenie witryny](publish-to-azure/_static/image4.png)

<span data-ttu-id="61334-129">Wartości połączenia są teraz gotowe.</span><span class="sxs-lookup"><span data-stu-id="61334-129">Your connection values are now all set.</span></span> <span data-ttu-id="61334-130">Możesz pozostawić te wartości bez zmian.</span><span class="sxs-lookup"><span data-stu-id="61334-130">You can leave these values unchanged.</span></span>

![Połączenia](publish-to-azure/_static/image5.png)

<span data-ttu-id="61334-132">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="61334-132">Click **Next**.</span></span>

<span data-ttu-id="61334-133">W przypadku ustawień, powiadomienia, że dwa połączenia z bazą danych są określone — ApplicationDBContext i ContosoUniversityDataEntities.</span><span class="sxs-lookup"><span data-stu-id="61334-133">For Settings, notice that two database connections are specified - ApplicationDBContext and ContosoUniversityDataEntities.</span></span> <span data-ttu-id="61334-134">ApplicationDBContext jest połączenie dla tabel konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="61334-134">ApplicationDBContext is the connection for user account tables.</span></span> <span data-ttu-id="61334-135">Te wartości Pokaż tylko ciągi połączenia dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-135">These values only show the connection strings for the databases.</span></span> <span data-ttu-id="61334-136">Nie oznacza to, że te bazy danych zostanie opublikowana, podczas publikowania witryny.</span><span class="sxs-lookup"><span data-stu-id="61334-136">It does not mean that these databases will be published when you publish your site.</span></span> <span data-ttu-id="61334-137">Po zakończeniu publikowania aplikacji sieci web, będą publikować projektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-137">You will publish your database project after you have finished publishing the web app.</span></span>

![](publish-to-azure/_static/image6.png)

<span data-ttu-id="61334-138">Wielokropek (...) obok połączenie z bazą danych zawiera szczegółowe informacje o parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="61334-138">The ellipsis (...) next to the database connection shows you the details of the connection string.</span></span> <span data-ttu-id="61334-139">Kliknij przycisk wielokropka obok ContosoUniversityDataEntities.</span><span class="sxs-lookup"><span data-stu-id="61334-139">Click the ellipsis next to ContosoUniversityDataEntities.</span></span>

![](publish-to-azure/_static/image7.png)

<span data-ttu-id="61334-140">Zanotuj nazwę serwera bazy danych i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-140">Note the name of the database server and the database.</span></span> <span data-ttu-id="61334-141">Nazwa serwera jest generowany losowo.</span><span class="sxs-lookup"><span data-stu-id="61334-141">The server name is randomly generated.</span></span> <span data-ttu-id="61334-142">Nazwa bazy danych jest prosta nazwa witryny za pomocą  **\_db** dołączane.</span><span class="sxs-lookup"><span data-stu-id="61334-142">The database name is simple the name of your site with **\_db** appended.</span></span> <span data-ttu-id="61334-143">Obie nazwy będą potrzebne później podczas publikowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-143">You will need both names later when you publish your database.</span></span>

<span data-ttu-id="61334-144">Kliknij przycisk **OK** aby zamknąć okno ciąg połączenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-144">Click **OK** to close the database connection string window.</span></span>

<span data-ttu-id="61334-145">W oknie Publikowanie w sieci Web kliknij **dalej** Aby wyświetlić podgląd.</span><span class="sxs-lookup"><span data-stu-id="61334-145">In the Publish Web window, click **Next** to see the preview.</span></span>

![](publish-to-azure/_static/image8.png)

<span data-ttu-id="61334-146">Można kliknąć, aby uruchomić Podgląd, aby wyświetlić listę plików do opublikowania.</span><span class="sxs-lookup"><span data-stu-id="61334-146">You can click Start Preview to see a list of the files to publish.</span></span> <span data-ttu-id="61334-147">Ponieważ jest to po raz pierwszy po opublikowaniu tej witryny, listy jest każdego odpowiedniego pliku w projekcie.</span><span class="sxs-lookup"><span data-stu-id="61334-147">Since this is the first time you have published this site, the list is every relevant file in the project.</span></span>

<span data-ttu-id="61334-148">Kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="61334-148">Click **Publish**.</span></span>

<span data-ttu-id="61334-149">W okienku dane wyjściowe zostaną wyświetlone wynik publikacji.</span><span class="sxs-lookup"><span data-stu-id="61334-149">The Output pane will display the result of your publication.</span></span>

![](publish-to-azure/_static/image9.png)

<span data-ttu-id="61334-150">Po opublikowaniu witryna jest immedialely uruchamiane w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="61334-150">After publication, the site is immedialely launched in a web browser.</span></span> <span data-ttu-id="61334-151">Witryna została wdrożona i można zarejestrować nowego użytkownika do witryny; Jednak tabele w projekcie ContosoUniversityData nie jeszcze zostały opublikowane.</span><span class="sxs-lookup"><span data-stu-id="61334-151">Your site has been deployed and you can register a new user to the site; however, your tables in the ContosoUniversityData project have not yet been published.</span></span> <span data-ttu-id="61334-152">Po kliknięciu na liście studentów łącza zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="61334-152">If you click on the List of students link you will receive an error.</span></span>

## <a name="publish-database-to-sql-azure"></a><span data-ttu-id="61334-153">Publikowanie bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="61334-153">Publish database to SQL Azure</span></span>

<span data-ttu-id="61334-154">Przed publikowania bazy danych, należy się upewnić, czy komputer lokalny może połączyć się z serwerem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-154">Before publishing your database, you must make sure your local computer can connect to the database server.</span></span> <span data-ttu-id="61334-155">Ogranicza zapory dla serwera bazy danych, które maszyny można podłączyć do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-155">The firewall for your database server restricts which machines can connect to the database.</span></span> <span data-ttu-id="61334-156">Należy dodać adres IP komputera do dozwolonych adresów IP dla zapory.</span><span class="sxs-lookup"><span data-stu-id="61334-156">You need to add the IP address of your computer to the allowed IP addresses for the firewall.</span></span>

<span data-ttu-id="61334-157">Zaloguj się do konta platformy Azure za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-157">Login to your Azure account through the Azure portal.</span></span>

<span data-ttu-id="61334-158">Wybierz nową bazę danych i wybierz **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="61334-158">Select your new database and select **Manage**.</span></span>

![Zarządzanie](publish-to-azure/_static/image10.png)

<span data-ttu-id="61334-160">Należy skonfigurować serwer bazy danych umożliwia nawiązywanie połączeń z komputera.</span><span class="sxs-lookup"><span data-stu-id="61334-160">You must configure your database server to allow connections from your computer.</span></span> <span data-ttu-id="61334-161">Po wybraniu Zarządzaj należy dodać bieżącego adresu IP, jako dozwolone na serwerze bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-161">When you select Manage, you are asked to add the current IP address as permitted to the database server.</span></span> <span data-ttu-id="61334-162">Wybierz opcję Tak.</span><span class="sxs-lookup"><span data-stu-id="61334-162">Select Yes.</span></span>

![Dodaj adres ip](publish-to-azure/_static/image11.png)

<span data-ttu-id="61334-164">Istnieje ryzyko, że adres IP dodanym w poprzednim kroku nie jest tylko adres IP, który należy skonfigurować dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="61334-164">There is a chance that the IP address you added in the previous step is not the only IP address you need to configure for connections.</span></span> <span data-ttu-id="61334-165">Możesz spróbować zalogować się do bazy danych, aby sprawdzić, czy połączenia są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="61334-165">You can attempt to login to the database to see if the connections have been properly set up.</span></span> <span data-ttu-id="61334-166">Podaj użytkownika i hasła utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="61334-166">Provide the user and password you created earlier.</span></span>

![Logowanie](publish-to-azure/_static/image12.png)

<span data-ttu-id="61334-168">Jeśli zostanie wyświetlony komunikat o błędzie, należy dodać inny adres IP.</span><span class="sxs-lookup"><span data-stu-id="61334-168">If you receive an error message, you need to add another IP address.</span></span> <span data-ttu-id="61334-169">Kliknij komunikat o błędzie, aby zobaczyć bardziej szczegółowe informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="61334-169">Click the error message to see more details about error.</span></span> <span data-ttu-id="61334-170">W szczegółach zobaczysz adres IP, który należy dodać.</span><span class="sxs-lookup"><span data-stu-id="61334-170">In the details you will see the IP address that you need to add.</span></span> <span data-ttu-id="61334-171">Należy pamiętać, ten adres IP.</span><span class="sxs-lookup"><span data-stu-id="61334-171">Note this IP address.</span></span>

![niedozwolone](publish-to-azure/_static/image13.png)

<span data-ttu-id="61334-173">Zamknij to okno logowania, a następnie wróć do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-173">Close this login window, and return to the Azure portal.</span></span>

<span data-ttu-id="61334-174">Przejdź do pulpitu nawigacyjnego dla Twojej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-174">Navigate to the Dashboard for your database.</span></span> <span data-ttu-id="61334-175">Kliknij przycisk **Zarządzaj dozwolonymi adresami IP**.</span><span class="sxs-lookup"><span data-stu-id="61334-175">Click **Manage allowed IP addresses**.</span></span>

![Zarządzanie adresami ip](publish-to-azure/_static/image14.png)

<span data-ttu-id="61334-177">Teraz należy dodać adres IP z komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="61334-177">You must now add the IP address from the error message.</span></span> <span data-ttu-id="61334-178">Zmiana zakresu dozwolonych adresów IP, aby uwzględnić z komunikat o błędzie albo dodać ten adres IP jako oddzielny wpis.</span><span class="sxs-lookup"><span data-stu-id="61334-178">Either change the range of allowed IP addresses to include the one from the error message, or add that IP address as a separate entry.</span></span>

![Dodaj nowy adres](publish-to-azure/_static/image15.png)

<span data-ttu-id="61334-180">Zapisz zmiany w dozwolonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="61334-180">Save the change to allowed IP addresses.</span></span>

<span data-ttu-id="61334-181">Kliknij przycisk Zarządzaj, a następnie spróbuj ponownie zalogować się do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-181">Click Manage, and try logging in again to the database.</span></span> <span data-ttu-id="61334-182">Konieczne może być Poczekaj kilka minut, zanim dozwolone adresy IP są poprawnie skonfigurowane dla zapory.</span><span class="sxs-lookup"><span data-stu-id="61334-182">You may need to wait a few minutes before the allowed IP addresses are correctly configured for the firewall.</span></span> <span data-ttu-id="61334-183">Jeśli możesz pomyślnie zalogować się w bazie danych, możesz Ukończono konfigurowanie połączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="61334-183">When you can successfully log in the database, you have finished setting up your connection to the database.</span></span>

<span data-ttu-id="61334-184">To okno zarządzania można pozostaw otwarte, ponieważ w wyniku wdrożenia bazy danych będzie sprawdzać wkrótce.</span><span class="sxs-lookup"><span data-stu-id="61334-184">You can leave this management window open because you will check the result of your database deployment shortly.</span></span>

<span data-ttu-id="61334-185">Wróć do projektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-185">Return to your database project.</span></span> <span data-ttu-id="61334-186">Kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="61334-186">Right-click the project and select **Publish**.</span></span>

![Publikowanie bazy danych](publish-to-azure/_static/image16.png)

<span data-ttu-id="61334-188">W oknie publikowania bazy danych, wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="61334-188">In the Publish Database window, select **Edit**.</span></span>

![Edytuj](publish-to-azure/_static/image17.png)

<span data-ttu-id="61334-190">Podaj nazwę serwera bazy danych i poświadczeń uwierzytelniania dla serwera.</span><span class="sxs-lookup"><span data-stu-id="61334-190">Provide the name of the database server and your authentication credentials for the server.</span></span> <span data-ttu-id="61334-191">Po podaniu poświadczenia, wybierz bazę danych utworzoną z listy dostępnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="61334-191">After providing the credentials, select the database you created from the list of available databases.</span></span> <span data-ttu-id="61334-192">Domyślnie Visual Studio ustawia nazwę pola bazy danych do nazwy projektu, który nie może być taka sama jak bazy danych, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="61334-192">By default, Visual Studio sets the name of the database field to the name of your project which might not be the same as the database you created.</span></span>

![](publish-to-azure/_static/image18.png)

<span data-ttu-id="61334-193">Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="61334-193">Click OK.</span></span>

<span data-ttu-id="61334-194">Prawdopodobnie można zapisać tego profilu, aby można opublikować aktualizacje w przyszłości, bez konieczności ponownego wprowadzania wszystkich informacji o połączeniu.</span><span class="sxs-lookup"><span data-stu-id="61334-194">You will probably want to save this profile so you can publish updates in the future without re-entering all of the connection information.</span></span> <span data-ttu-id="61334-195">Wybierz **Utwórz profil**.</span><span class="sxs-lookup"><span data-stu-id="61334-195">Select **Create Profile**.</span></span>

![Zapisywanie profilu](publish-to-azure/_static/image19.png)

<span data-ttu-id="61334-197">W projekcie o nazwie zostanie utworzony plik **ContosoUniversityData.publish.xml**.</span><span class="sxs-lookup"><span data-stu-id="61334-197">It will create a file in your project named **ContosoUniversityData.publish.xml**.</span></span> <span data-ttu-id="61334-198">Przy następnym, którą chcesz opublikować bazy danych na platformie Azure, po prostu załadować tego profilu.</span><span class="sxs-lookup"><span data-stu-id="61334-198">The next time you want to publish the database to Azure, simply load that profile.</span></span>

<span data-ttu-id="61334-199">Teraz, kliknij przycisk **publikowania** utworzyć bazę danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-199">Now, click **Publish** to create the database on Azure.</span></span>

![Publikowanie](publish-to-azure/_static/image20.png)

<span data-ttu-id="61334-201">Po uruchomieniu przez pewien czas, publikowania wyniki są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="61334-201">After running for a while, the publishing results are displayed.</span></span>

![wyniki](publish-to-azure/_static/image21.png)

<span data-ttu-id="61334-203">Teraz można przejść wstecz do portalu zarządzania dla Twojej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="61334-203">Now, you can go back to the management portal for your database.</span></span> <span data-ttu-id="61334-204">Odśwież widok projektu i należy zauważyć, że zostały wdrożone 3 tabel z danymi wstępnie wypełnione.</span><span class="sxs-lookup"><span data-stu-id="61334-204">Refresh the design view, and notice the 3 tables with pre-filled data have been deployed.</span></span>

![nowe tabele](publish-to-azure/_static/image22.png)

<span data-ttu-id="61334-206">Teraz można przystąpić do testowania aplikacji sieci web, który jest wdrożony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="61334-206">Now you are ready to test the web app that is deployed to Azure.</span></span> <span data-ttu-id="61334-207">Przejdź do aplikacji sieci web na platformie Azure (na przykład http://contosositeexample.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="61334-207">Navigate to the web app on Azure (such as http://contosositeexample.azurewebsites.net/).</span></span> <span data-ttu-id="61334-208">Kliknij łącze do listy studentów i powinien zostać wyświetlony widok indeksu dla uczniów lub studentów.</span><span class="sxs-lookup"><span data-stu-id="61334-208">Click the link for List of students and you should see the index view for students.</span></span>

![Widok](publish-to-azure/_static/image23.png)

<span data-ttu-id="61334-210">Czasami połączenia i bazy danych należy trochę czasu na zostać prawidłowo skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="61334-210">Occasionally, the database and connection need a little time to be properly configured.</span></span> <span data-ttu-id="61334-211">Jeśli wystąpi błąd, zaczekaj kilka minut, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="61334-211">If you receive an error, wait a few minutes and then try again.</span></span>

## <a name="conclusion"></a><span data-ttu-id="61334-212">Wniosek</span><span class="sxs-lookup"><span data-stu-id="61334-212">Conclusion</span></span>

<span data-ttu-id="61334-213">Ta seria podać prosty przykład sposobu generowanie kodu na podstawie istniejącej bazy danych, która umożliwia użytkownikom edytowanie, aktualizowanie, tworzenie i usuwanie danych.</span><span class="sxs-lookup"><span data-stu-id="61334-213">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="61334-214">ASP.NET MVC 5, Entity Framework i ASP.NET szkieletów on użyty do utworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="61334-214">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span>

<span data-ttu-id="61334-215">Przykład wprowadzające programowanie Code First, zobacz [wprowadzenie do platformy ASP.NET MVC 5](../introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="61334-215">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span>

<span data-ttu-id="61334-216">Na przykład bardziej zaawansowanych, zobacz [tworzenia modelu danych struktury jednostek dla aplikacji ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="61334-216">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="61334-217">Należy pamiętać, że API DbContext, służące do pracy z danymi w pierwszym bazy danych jest taki sam jak interfejs API, można użyć do pracy z danymi w Code First.</span><span class="sxs-lookup"><span data-stu-id="61334-217">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="61334-218">Nawet jeśli zamierzasz użyć pierwszej bazy danych, można poznać sposoby obsługi złożonych scenariuszy, takich jak odczytywanie i aktualizowanie danych powiązanych konfliktów współbieżności, i z kodu pierwszy samouczek.</span><span class="sxs-lookup"><span data-stu-id="61334-218">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="61334-219">Jedyną różnicą jest w sposób tworzenia bazy danych, klasa kontekstu i klas jednostek.</span><span class="sxs-lookup"><span data-stu-id="61334-219">The only difference is in how the database, context class, and entity classes are created.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="61334-220">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="61334-220">Previous</span></span>](enhancing-data-validation.md)