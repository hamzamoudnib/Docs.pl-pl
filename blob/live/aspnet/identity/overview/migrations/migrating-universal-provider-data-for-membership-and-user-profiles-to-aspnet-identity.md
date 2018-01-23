---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: "Migrowanie danych uniwersalnych dostawcy dla członkostwa i profilów użytkownika dla tożsamości ASP.NET (C#) | Dokumentacja firmy Microsoft"
author: rustd
description: "W tym samouczku opisano kroki, które są niezbędne do przeprowadzenia migracji użytkowników i danych roli i danych profilów użytkowników utworzone przy użyciu dostawców uniwersalnych z istniejącej aplikacji..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/13/2013
ms.topic: article
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: e00bcfc111425d5dd26c7ff341eaf87fd969e089
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a><span data-ttu-id="c8b91-103">Migrowanie danych uniwersalnych dostawcy dla członkostwa i profilów użytkownika dla tożsamości ASP.NET (C#)</span><span class="sxs-lookup"><span data-stu-id="c8b91-103">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity (C#)</span></span>
====================
<span data-ttu-id="c8b91-104">przez [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Roberta Mcmurraya](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)</span><span class="sxs-lookup"><span data-stu-id="c8b91-104">by [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://github.com/Rick-Anderson), [Robert McMurray](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)</span></span>

> <span data-ttu-id="c8b91-105">W tym samouczku opisano kroki, które są niezbędne do migracji użytkowników i dane roli i danych profilów użytkowników utworzone przy użyciu dostawców uniwersalnych istniejącej aplikacji do modelu tożsamości ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c8b91-105">This tutorial describes the steps that are necessary to migrate user and role data and user profile data created using Universal Providers of an existing application to the ASP.NET Identity model.</span></span> <span data-ttu-id="c8b91-106">Podejście powieść do migracji danych profilu użytkownika mogą być używane w aplikacji przy użyciu również członkostwa SQL.</span><span class="sxs-lookup"><span data-stu-id="c8b91-106">The approach mentioned here to migrate user profile data can be used in an application with SQL membership as well.</span></span>


<span data-ttu-id="c8b91-107">Wraz z wydaniem programu Visual Studio 2013, ASP.NET team wprowadzono nowy system ASP.NET Identity i więcej o tej wersji [tutaj](../../index.md).</span><span class="sxs-lookup"><span data-stu-id="c8b91-107">With the release of Visual Studio 2013, the ASP.NET team introduced a new ASP.NET Identity system, and you can read more about that release [here](../../index.md).</span></span> <span data-ttu-id="c8b91-108">Po tego artykułu, aby przeprowadzić migrację aplikacji sieci web z [członkostwa SQL do nowego systemu tożsamości](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md), w tym artykule przedstawiono kroki, aby przeprowadzić migrację istniejących aplikacji, które należy wykonać modelu dostawców do zarządzania użytkownikami i rola w nowym modelu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c8b91-108">Following up on the article to migrate web applications from [SQL Membership to the new Identity system](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md), this article illustrates the steps to migrate existing applications that follow the Providers model for user and role management to the new Identity model.</span></span> <span data-ttu-id="c8b91-109">Fokus w tym samouczku będą się głównie na temat migracji dane profilu użytkownika, aby bezproblemowo Połącz je w nowym systemie.</span><span class="sxs-lookup"><span data-stu-id="c8b91-109">The focus of this tutorial will be primarily on migrating the user profile data to seamlessly hook it into the new system.</span></span> <span data-ttu-id="c8b91-110">Migrowanie informacje użytkownika i roli są podobne do członkostwa SQL.</span><span class="sxs-lookup"><span data-stu-id="c8b91-110">Migrating user and role information is similar for SQL membership.</span></span> <span data-ttu-id="c8b91-111">Podejście do migracji danych profilu można w aplikacji z również członkostwa SQL.</span><span class="sxs-lookup"><span data-stu-id="c8b91-111">The approach followed to migrate profile data can be used in an application with SQL membership as well.</span></span>

<span data-ttu-id="c8b91-112">Na przykład Rozpoczniemy z aplikacją sieci web utworzony za pomocą programu Visual Studio 2012, który korzysta z modelu dostawców.</span><span class="sxs-lookup"><span data-stu-id="c8b91-112">As an example, we will start with a web app created using Visual Studio 2012 which uses the Providers model.</span></span> <span data-ttu-id="c8b91-113">Firma Microsoft będzie, a następnie dodaj kod do zarządzania profilami, zarejestruj użytkownika, dodać dane profilu dla użytkowników, migracji schemat bazy danych, a następnie Zmień aplikację do korzystania z systemu tożsamości użytkownika i roli zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c8b91-113">We'll then add code for profile management, register a user, add profile data for the users, migrate the database schema, and then change the application to use the Identity system for user and role management.</span></span> <span data-ttu-id="c8b91-114">Jako test migracji użytkowników utworzone przy użyciu dostawców uniwersalnych powinny mieć możliwość logowania i nowych użytkowników powinny mieć możliwość rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="c8b91-114">As a test of migration, users created using Universal Providers should be able to log in and new users should be able to register.</span></span>

> [!NOTE]
> <span data-ttu-id="c8b91-115">Znajduje się pełny przykład w [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations).</span><span class="sxs-lookup"><span data-stu-id="c8b91-115">You can find the complete sample at [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations).</span></span>


## <a name="profile-data-migration-summary"></a><span data-ttu-id="c8b91-116">Podsumowanie migracji danych profilu</span><span class="sxs-lookup"><span data-stu-id="c8b91-116">Profile data migration summary</span></span>

<span data-ttu-id="c8b91-117">Przed rozpoczęciem z migracja, poinformuj nas przyjrzeć się obsługi przechowywania danych profilu w modelu dostawców.</span><span class="sxs-lookup"><span data-stu-id="c8b91-117">Before starting with the migrations, let us look at the experience of storing profile data in the Providers model.</span></span> <span data-ttu-id="c8b91-118">Dane profilu dla aplikacji, które użytkownicy mogą być przechowywane na wiele sposobów, najczęściej między nimi są przy użyciu dostawców wbudowanych profilu dostarczanego wraz z dostawców uniwersalnych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-118">Profile data for application users can be stored in multiple ways, the most common among them being using the inbuilt profile providers shipped along with the Universal Providers.</span></span> <span data-ttu-id="c8b91-119">Obejmuje kroki</span><span class="sxs-lookup"><span data-stu-id="c8b91-119">The steps would include</span></span>

1. <span data-ttu-id="c8b91-120">Dodaj klasę, która ma właściwości używany do przechowywania danych profilu.</span><span class="sxs-lookup"><span data-stu-id="c8b91-120">Add a class that has properties used to store Profile data.</span></span>
2. <span data-ttu-id="c8b91-121">Dodaj klasę, która rozszerza "ProfileBase" i implementuje metody w celu uzyskania powyższe dane profilu dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-121">Add a class that extends 'ProfileBase' and implements methods to get the above profile data for the user.</span></span>
3. <span data-ttu-id="c8b91-122">Włącz przy użyciu domyślnego dostawcy profilu w *web.config* plików i zdefiniuj klasy zadeklarowanej w kroku &#2; ma być używana podczas uzyskiwania dostępu do informacji o profilu.</span><span class="sxs-lookup"><span data-stu-id="c8b91-122">Enable using default profile providers in the *web.config* file and define the class declared in step #2 to be used in accessing profile information.</span></span>

<span data-ttu-id="c8b91-123">Informacje o profilu jest przechowywana jako serializacji xml i dane binarne w tabeli "Profilów" w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-123">The profile information is stored as serialized xml and binary data in the 'Profiles' table in the database.</span></span>

<span data-ttu-id="c8b91-124">Po przeprowadzeniu migracji aplikacji do użycia w nowym systemie tożsamości platformy ASP.NET, informacje o profilu jest zdeserializować i przechowywane jako właściwości klasy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-124">After migrating the application to use the new ASP.NET Identity system, the profile information is deserialized and stored as properties on the user class.</span></span> <span data-ttu-id="c8b91-125">Każda właściwość następnie mogą być mapowane na kolumny w tabeli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-125">Each property can then be mapped onto columns in the user table.</span></span> <span data-ttu-id="c8b91-126">W tym miejscu zaletą jest, że właściwości można pracować bezpośrednio za pomocą klasy użytkownika oprócz nie ma potrzeby serializacji/deserializacji danych informacji jednocześnie, gdy uzyskuje do niej dostęp.</span><span class="sxs-lookup"><span data-stu-id="c8b91-126">The advantage here is that the properties can be worked on directly using the user class in addition to not having to serialize/deserialize data information each time when accessing it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c8b91-127">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c8b91-127">Getting Started</span></span>

1. <span data-ttu-id="c8b91-128">Tworzenie nowej aplikacji formularzy sieci Web programu ASP.NET 4.5 w programie Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="c8b91-128">Create a new ASP.NET 4.5 Web Forms application in Visual Studio 2012.</span></span> <span data-ttu-id="c8b91-129">Bieżący przykładzie użyto szablonu formularzy sieci Web, ale można również użyć aplikacji MVC.</span><span class="sxs-lookup"><span data-stu-id="c8b91-129">The current sample uses the Web Forms template, but you could use MVC Application as well.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. <span data-ttu-id="c8b91-130">Utwórz nowy folder modeli, można zapisać informacji o profilu</span><span class="sxs-lookup"><span data-stu-id="c8b91-130">Create a new folder 'Models' to store profile information</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. <span data-ttu-id="c8b91-131">Na przykład Daj nam przechowywania daty urodzenia, miasta, wysokości i wagi użytkownika w profilu.</span><span class="sxs-lookup"><span data-stu-id="c8b91-131">As an example, let us store the date of birth, city, height and weight of the user in profile.</span></span> <span data-ttu-id="c8b91-132">Wysokość i wagi są przechowywane jako niestandardowej klasy o nazwie "PersonalStats".</span><span class="sxs-lookup"><span data-stu-id="c8b91-132">The height and weight are stored as a custom class called 'PersonalStats'.</span></span> <span data-ttu-id="c8b91-133">Do przechowywania i pobierania profilu, potrzebujemy klasę, która rozszerza "ProfileBase".</span><span class="sxs-lookup"><span data-stu-id="c8b91-133">To store and retrieve the profile, we need a class that extends 'ProfileBase'.</span></span> <span data-ttu-id="c8b91-134">Umożliwia utworzenie nowej klasy "AppProfile", aby uzyskać i przechowywać informacje o profilu.</span><span class="sxs-lookup"><span data-stu-id="c8b91-134">Let's create a new class 'AppProfile' to get and store profile information.</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. <span data-ttu-id="c8b91-135">Włącz profil *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="c8b91-135">Enable profile in the *web.config* file.</span></span> <span data-ttu-id="c8b91-136">Wprowadź nazwę klasy, która ma być używany do przechowywania/pobierania informacji o użytkowniku utworzonego w kroku #3.</span><span class="sxs-lookup"><span data-stu-id="c8b91-136">Enter the class name to be used to store/retrieve user information created in step #3.</span></span>

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. <span data-ttu-id="c8b91-137">Dodawanie strony formularzy sieci web w folderze "Konto", aby pobrać dane profilu użytkownika i zapisze go.</span><span class="sxs-lookup"><span data-stu-id="c8b91-137">Add a web forms page in 'Account' folder to get the profile data from the user and store it.</span></span> <span data-ttu-id="c8b91-138">Kliknij prawym przyciskiem myszy projekt i wybierz opcję "Dodaj nowy element".</span><span class="sxs-lookup"><span data-stu-id="c8b91-138">Right click on project and select 'Add new Item'.</span></span> <span data-ttu-id="c8b91-139">Dodawanie nowej strony formularzy sieci Web z strony wzorcowej "AddProfileData.aspx".</span><span class="sxs-lookup"><span data-stu-id="c8b91-139">Add a new webforms page with master page 'AddProfileData.aspx'.</span></span> <span data-ttu-id="c8b91-140">Skopiuj następujące w sekcji "Znacznika":</span><span class="sxs-lookup"><span data-stu-id="c8b91-140">Copy the following in the 'MainContent' section:</span></span>

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

 <span data-ttu-id="c8b91-141">Dodaj następujący kod w kodzie:</span><span class="sxs-lookup"><span data-stu-id="c8b91-141">Add the following code in the code behind:</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

 <span data-ttu-id="c8b91-142">Dodaj obszar nazw, w których AppProfile zdefiniowana jest klasa, aby usunąć błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c8b91-142">Add the namespace under which AppProfile class is defined to remove the compilation errors.</span></span>
6. <span data-ttu-id="c8b91-143">Uruchom aplikację i utworzenie nowego użytkownika z nazwą użytkownika "**olduser".**</span><span class="sxs-lookup"><span data-stu-id="c8b91-143">Run the app and create a new user with username '**olduser'.**</span></span> <span data-ttu-id="c8b91-144">Przejdź do strony "AddProfileData" i Dodaj informacje o profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-144">Navigate to the 'AddProfileData' page and add profile information for the user.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

<span data-ttu-id="c8b91-145">Aby sprawdzić, czy dane są przechowywane jako serializacji xml w tabeli "Profilów" w oknie Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="c8b91-145">You can verify that the data is stored as serialized xml in the 'Profiles' table using the Server Explorer window.</span></span> <span data-ttu-id="c8b91-146">W programie Visual Studio z menu "Widok" Wybierz "Eksploratora serwera".</span><span class="sxs-lookup"><span data-stu-id="c8b91-146">In Visual Studio, from 'View' menu, choose 'Server Explorer'.</span></span> <span data-ttu-id="c8b91-147">Powinien być połączenia danych dla bazy danych zdefiniowanych w *web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="c8b91-147">There should be a data connection for the database defined in the *web.config* file.</span></span> <span data-ttu-id="c8b91-148">Kliknięcie połączenie danych pokazuje pod różnych kategorii.</span><span class="sxs-lookup"><span data-stu-id="c8b91-148">Clicking on the data connection shows different sub categories.</span></span> <span data-ttu-id="c8b91-149">Rozwiń węzeł "Tabele" Pokaż różnych tabel w bazie danych, a następnie kliknij prawym przyciskiem "Profilów" i wybierz opcję "Pokaż tabeli danych" do wyświetlania danych profilu przechowywane w tabeli profilów.</span><span class="sxs-lookup"><span data-stu-id="c8b91-149">Expand 'Tables' to show the different tables in your database, then right click on 'Profiles' and choose 'Show Table Data' to view the profile data stored in the Profiles table.</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a><span data-ttu-id="c8b91-150">Migrowanie schematu bazy danych</span><span class="sxs-lookup"><span data-stu-id="c8b91-150">Migrating database schema</span></span>

<span data-ttu-id="c8b91-151">Aby istniejąca baza danych działa w systemie tożsamości, musimy zaktualizować schemat w bazie danych tożsamości do obsługi pola, które dodano do oryginalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-151">To make the existing database work with the Identity system, we need to update the schema in the Identity database to support the fields we added to the original database.</span></span> <span data-ttu-id="c8b91-152">Można to zrobić za pomocą skryptów SQL, aby utworzyć nowe tabele i skopiuj istniejące informacje.</span><span class="sxs-lookup"><span data-stu-id="c8b91-152">This can be done using SQL scripts to create new tables and copy the existing information.</span></span> <span data-ttu-id="c8b91-153">W oknie "Eksploratora serwera" rozwiń parametru "DefaultConnection" do wyświetlenia w tabelach.</span><span class="sxs-lookup"><span data-stu-id="c8b91-153">In the 'Server Explorer' window, expand the 'DefaultConnection' to display the tables.</span></span> <span data-ttu-id="c8b91-154">Kliknij prawym przyciskiem myszy kliknij tabele i wybierz pozycję "Nowe zapytanie"</span><span class="sxs-lookup"><span data-stu-id="c8b91-154">Right click Tables and select 'New Query'</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

<span data-ttu-id="c8b91-155">Wklej skrypt SQL z [https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="c8b91-155">Paste the SQL script from [https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) and run it.</span></span> <span data-ttu-id="c8b91-156">Jeśli połączenia "DefaultConnection" zostanie odświeżona, możemy stwierdzić, że nowe tabele są dodawane.</span><span class="sxs-lookup"><span data-stu-id="c8b91-156">If the 'DefaultConnection' is refreshed, we can see that the new tables are added.</span></span> <span data-ttu-id="c8b91-157">Można sprawdzić danych wewnątrz tabel, aby zobaczyć, że dane zostały poddane migracji.</span><span class="sxs-lookup"><span data-stu-id="c8b91-157">You can check the data inside the tables to see that the information has been migrated.</span></span>

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a><span data-ttu-id="c8b91-158">Migrowanie aplikacji do korzystania z tożsamości platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="c8b91-158">Migrating the application to use ASP.NET Identity</span></span>

1. <span data-ttu-id="c8b91-159">Instalowanie pakietów Nuget potrzebne dla tożsamości ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c8b91-159">Install the Nuget packages needed for ASP.NET Identity:</span></span>

    - <span data-ttu-id="c8b91-160">Microsoft.AspNet.Identity.EntityFramework</span><span class="sxs-lookup"><span data-stu-id="c8b91-160">Microsoft.AspNet.Identity.EntityFramework</span></span>
    - <span data-ttu-id="c8b91-161">Microsoft.AspNet.Identity.Owin</span><span class="sxs-lookup"><span data-stu-id="c8b91-161">Microsoft.AspNet.Identity.Owin</span></span>
    - <span data-ttu-id="c8b91-162">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="c8b91-162">Microsoft.Owin.Host.SystemWeb</span></span>
    - <span data-ttu-id="c8b91-163">Microsoft.Owin.Security.Facebook</span><span class="sxs-lookup"><span data-stu-id="c8b91-163">Microsoft.Owin.Security.Facebook</span></span>
    - <span data-ttu-id="c8b91-164">Microsoft.Owin.Security.Google</span><span class="sxs-lookup"><span data-stu-id="c8b91-164">Microsoft.Owin.Security.Google</span></span>
    - <span data-ttu-id="c8b91-165">Microsoft.Owin.Security.MicrosoftAccount</span><span class="sxs-lookup"><span data-stu-id="c8b91-165">Microsoft.Owin.Security.MicrosoftAccount</span></span>
    - <span data-ttu-id="c8b91-166">Microsoft.Owin.Security.Twitter</span><span class="sxs-lookup"><span data-stu-id="c8b91-166">Microsoft.Owin.Security.Twitter</span></span>

 <span data-ttu-id="c8b91-167">Więcej informacji na temat zarządzania pakietami Nuget można znaleźć [tutaj](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)</span><span class="sxs-lookup"><span data-stu-id="c8b91-167">More information on managing Nuget packages can be found [here](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)</span></span>
2. <span data-ttu-id="c8b91-168">Aby pracować z istniejących danych w tabeli, należy utworzyć klasy modelu, które mapowania tabeli, a Podłączanie w systemie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c8b91-168">To work with existing data in the table, we need to create model classes which map back to the tables and hook them up in the Identity system.</span></span> <span data-ttu-id="c8b91-169">W ramach umowy tożsamości klasy modelu albo powinien implementować interfejsów zdefiniowanych w bibliotece dll Identity.Core lub rozszerzyć istniejącą implementacją tych interfejsów, które są dostępne w Microsoft.AspNet.Identity.EntityFramework.</span><span class="sxs-lookup"><span data-stu-id="c8b91-169">As part of the Identity contract, the model classes should either implement the interfaces defined in the Identity.Core dll or can extend the existing implementation of these interfaces available in Microsoft.AspNet.Identity.EntityFramework.</span></span> <span data-ttu-id="c8b91-170">Firma Microsoft będzie używać istniejących klas dla roli, logowania użytkowników i oświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-170">We will be using the existing classes for role, user logins and user claims.</span></span> <span data-ttu-id="c8b91-171">Należy użyć użytkownika niestandardowego dla naszej próbki.</span><span class="sxs-lookup"><span data-stu-id="c8b91-171">We need to use a custom user for our sample.</span></span> <span data-ttu-id="c8b91-172">Kliknij prawym przyciskiem myszy projekt i Utwórz nowy folder "IdentityModels".</span><span class="sxs-lookup"><span data-stu-id="c8b91-172">Right click on the project and create new folder 'IdentityModels'.</span></span> <span data-ttu-id="c8b91-173">Dodaj nową klasę "User", jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c8b91-173">Add a new 'User' class as shown below:</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

 <span data-ttu-id="c8b91-174">Zauważ, że ProfileInfo teraz jest właściwością klasy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c8b91-174">Notice that the 'ProfileInfo' is now a property on the user class.</span></span> <span data-ttu-id="c8b91-175">Dlatego możemy użyć klasy użytkownika bezpośrednio pracować z danymi profilu.</span><span class="sxs-lookup"><span data-stu-id="c8b91-175">Hence we can use the user class to directly work with profile data.</span></span>

<span data-ttu-id="c8b91-176">Skopiuj pliki w **IdentityModels** i **IdentityAccount** folderów ze źródła pobierania ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/ UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ).</span><span class="sxs-lookup"><span data-stu-id="c8b91-176">Copy the files in the **IdentityModels** and **IdentityAccount** folders from the download source ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ).</span></span> <span data-ttu-id="c8b91-177">Mają one pozostałe klasy modelu i nowych stron wymaganych dla użytkowników i zarządzania rolami przy użyciu interfejsów API tożsamości ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c8b91-177">These have the remaining model classes and the new pages needed for user and role management using the ASP.NET Identity APIs.</span></span> <span data-ttu-id="c8b91-178">Podejście, używane jest podobny do członkostwa SQL i szczegółowy opis można znaleźć [tutaj](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md).</span><span class="sxs-lookup"><span data-stu-id="c8b91-178">The approach used is similar to the SQL Membership and the detailed explanation can be found [here](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md).</span></span>

## <a name="copying-profile-data-to-the-new-tables"></a><span data-ttu-id="c8b91-179">Kopiowanie danych profilu do nowych tabel</span><span class="sxs-lookup"><span data-stu-id="c8b91-179">Copying Profile data to the new tables</span></span>

<span data-ttu-id="c8b91-180">Jak wspomniano wcześniej, musimy deserializacji danych xml w tabelach profile i zapisze go w kolumnach tabeli AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="c8b91-180">As mentioned earlier, we need to deserialize the xml data in the Profiles tables and store it in the columns of the AspNetUsers table.</span></span> <span data-ttu-id="c8b91-181">Nowe kolumny zostały utworzone w tabeli użytkowników w poprzednim kroku, tak aby pozostało do wypełnienia tych kolumn niezbędnych danych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-181">The new columns were created in the users table in the previous step so all that is left is to populate those columns with the necessary data.</span></span> <span data-ttu-id="c8b91-182">W tym celu użyjemy aplikacji konsoli, w którym jest uruchamiane jeden raz, aby wypełnić nowo utworzony kolumn w tabeli użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c8b91-182">To do this, we will use a console application which is run once to populate the newly created columns in the users table.</span></span>

1. <span data-ttu-id="c8b91-183">Utwórz nową aplikację konsoli w istniejącym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c8b91-183">Create a new console application in the exiting solution.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. <span data-ttu-id="c8b91-184">Zainstaluj najnowszą wersję pakietu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c8b91-184">Install the latest version of the Entity Framework package.</span></span>
3. <span data-ttu-id="c8b91-185">Dodaj aplikację sieci web utworzone powyżej jako odwołanie do aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="c8b91-185">Add the web application created above as a reference to the console application.</span></span> <span data-ttu-id="c8b91-186">Aby zrobić to kliknij prawym przyciskiem myszy projekt, a następnie "Dodaj odwołania", następnie rozwiązania, następnie kliknij na projekt i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="c8b91-186">To do this right click on Project, then 'Add References', then Solution, then click on the project and click OK.</span></span>
4. <span data-ttu-id="c8b91-187">Kopiuj poniżej kod w klasie Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c8b91-187">Copy the below code in the Program.cs class.</span></span> <span data-ttu-id="c8b91-188">Tę logikę odczytuje dane profilu dla każdego użytkownika, serializuje go jako obiekt "ProfileInfo" i zapisuje je w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-188">This logic reads profile data for each user, serializes it as 'ProfileInfo' object and stores it back to the database.</span></span>

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

 <span data-ttu-id="c8b91-189">Niektóre modele są definiowane w folderze "IdentityModels" projektu aplikacji sieci web, więc należy dołączyć odpowiednie przestrzenie nazw.</span><span class="sxs-lookup"><span data-stu-id="c8b91-189">Some of the models used are defined in the 'IdentityModels' folder of the web application project, so you must include the corresponding namespaces.</span></span>
5. <span data-ttu-id="c8b91-190">Powyższy kod działa na plik bazy danych w aplikacji\_utworzyć folderu dane projektu aplikacji sieci web w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="c8b91-190">The above code works on the database file in the App\_Data folder of the web application project created in the previous steps.</span></span> <span data-ttu-id="c8b91-191">Aby odwołać, który, należy zaktualizować parametry połączenia w pliku app.config aplikacji konsoli przy użyciu parametrów połączenia w pliku web.config aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c8b91-191">To reference that, update the connection string in the app.config file of the console application with the connection string in the web.config of the web application.</span></span> <span data-ttu-id="c8b91-192">Ponadto podaj pełną ścieżkę fizyczną we właściwości 'AttachDbFilename'.</span><span class="sxs-lookup"><span data-stu-id="c8b91-192">Also provide the complete physical path in the 'AttachDbFilename' property.</span></span>
6. <span data-ttu-id="c8b91-193">Otwórz wiersz polecenia i przejdź do folderu bin powyżej aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="c8b91-193">Open a command prompt and navigate to the bin folder of the above console application.</span></span> <span data-ttu-id="c8b91-194">Uruchom plik wykonywalny i przejrzyj dane wyjściowe dziennika, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="c8b91-194">Run the executable and review the log output as shown in the following image.</span></span>  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. <span data-ttu-id="c8b91-195">Otwórz tabelę "AspNetUsers" w Eksploratorze serwera i sprawdź dane w nowych kolumn, które posiadają właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8b91-195">Open the 'AspNetUsers' table in the Server Explorer and verify the data in the new columns that hold the properties.</span></span> <span data-ttu-id="c8b91-196">One powinien być zaktualizowany o wartości odpowiednich właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8b91-196">They should be updated with the corresponding property values.</span></span>

## <a name="verify-functionality"></a><span data-ttu-id="c8b91-197">Sprawdzenie działania</span><span class="sxs-lookup"><span data-stu-id="c8b91-197">Verify functionality</span></span>

<span data-ttu-id="c8b91-198">Użyj strony nowo dodanego członkostwo, które są implementowane za pomocą ASP.NET Identity logowania użytkownika z utrzymując bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c8b91-198">Use the newly added membership pages that are implemented using ASP.NET Identity to login a user from the old database.</span></span> <span data-ttu-id="c8b91-199">Użytkownik powinien mieć możliwość Zaloguj się za pomocą tych samych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c8b91-199">The user should be able to log in using the same credentials.</span></span> <span data-ttu-id="c8b91-200">Inne funkcje, takie jak dodawanie OAuth, tworzenie nowego użytkownika, zmiana haseł, Dodawanie ról, spróbuj dodać użytkowników do ról, itp.</span><span class="sxs-lookup"><span data-stu-id="c8b91-200">Try the other functionalities like adding OAuth, creating a new user, changing a password, adding roles, add users to roles, etc.</span></span>

<span data-ttu-id="c8b91-201">Dane profilu dla użytkownika starych i nowych użytkowników, należy pobrać i przechowywane w tabeli użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c8b91-201">The Profile data for the old user and the new users should be retrieved and stored in the users table.</span></span> <span data-ttu-id="c8b91-202">Nie jest już starej tabeli ma być utworzone odwołanie.</span><span class="sxs-lookup"><span data-stu-id="c8b91-202">The old table should no longer be referenced.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c8b91-203">Wniosek</span><span class="sxs-lookup"><span data-stu-id="c8b91-203">Conclusion</span></span>

<span data-ttu-id="c8b91-204">Tego artykułu opisano proces migrowanie aplikacji sieci web, które używane modelu dostawcy dla członkostwa w produkcie ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="c8b91-204">The article described the process of migrating web applications that used the provider model for membership to ASP.NET Identity.</span></span> <span data-ttu-id="c8b91-205">Artykuł opisane również migrację danych profilu dla użytkowników być punktem zaczepienia systemu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c8b91-205">The article additionally outlined migrating profile data for users to be hooked into the Identity system.</span></span> <span data-ttu-id="c8b91-206">Zostaw komentarze poniżej pytania i problemów napotkanych podczas migracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8b91-206">Please leave comments below for questions and issues encountered when you migrate your app.</span></span>

<span data-ttu-id="c8b91-207">*Dzięki użyciu Rick Anderson i Roberta Mcmurraya do przeglądania tego artykułu.*</span><span class="sxs-lookup"><span data-stu-id="c8b91-207">*Thanks to Rick Anderson and Robert McMurray for reviewing the article.*</span></span>