---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: "Tworzenie parametrów połączenia i pracy z bazy danych LocalDB programu SQL Server | Dokumentacja firmy Microsoft"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 25d1c1c9954baaca9ef91eff3dd3c853930a5893
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="f49e3-102">Tworzenie parametrów połączenia i pracy z bazy danych LocalDB programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="f49e3-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>
====================
<span data-ttu-id="f49e3-103">Przez [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="f49e3-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="f49e3-104">Tworzenie parametrów połączenia i pracy z bazy danych LocalDB programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="f49e3-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="f49e3-105">`MovieDBContext` Obsługuje klasy utworzone zadanie łączenia z bazą danych i mapowanie `Movie` obiektów do rekordów bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f49e3-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="f49e3-106">Jedno pytanie, który może poprosić o jest jednak sposób Określ bazę danych, które będą łączyć się.</span><span class="sxs-lookup"><span data-stu-id="f49e3-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="f49e3-107">Faktycznie nie trzeba określać bazę danych do użycia, domyślnie zostanie ustawiona przy użyciu programu Entity Framework [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="f49e3-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="f49e3-108">W tej sekcji jawnie dodamy parametry połączenia w *Web.config* pliku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f49e3-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="f49e3-109">SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="f49e3-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="f49e3-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) jest wersja programu SQL Server Express aparat bazy danych rozpoczyna się na żądanie, która działa w trybie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f49e3-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="f49e3-111">LocalDB działa w trybie wykonywania specjalnych programu SQL Server Express, który umożliwia pracę z bazami danych jako *.mdf* plików.</span><span class="sxs-lookup"><span data-stu-id="f49e3-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="f49e3-112">Zazwyczaj są przechowywane pliki bazy danych LocalDB w *aplikacji\_danych* folderu projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="f49e3-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="f49e3-113">SQL Server Express nie jest zalecane do użycia w aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f49e3-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="f49e3-114">LocalDB w szczególności nie stosuje się do produkcji z aplikacją sieci web, ponieważ nie jest przeznaczony do pracy z usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="f49e3-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="f49e3-115">Niemniej jednak bazy danych LocalDB można łatwo migracji do programu SQL Server lub SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f49e3-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="f49e3-116">W programie Visual Studio 2017 r. LocalDB jest instalowany domyślnie z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f49e3-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="f49e3-117">Domyślnie program Entity Framework wyszukuje ciąg połączenia o nazwie takiej jak klasa kontekst obiektu (`MovieDBContext` dla tego projektu).</span><span class="sxs-lookup"><span data-stu-id="f49e3-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="f49e3-118">Aby uzyskać więcej informacji, zobacz [parametry połączenia serwera SQL dla aplikacji sieci Web ASP.NET](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="f49e3-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="f49e3-119">Otwórz katalog główny aplikacji *Web.config* pliku pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f49e3-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="f49e3-120">(Nie *Web.config* w pliku *widoków* folderu.)</span><span class="sxs-lookup"><span data-stu-id="f49e3-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="f49e3-121">Znajdź `<connectionStrings>` elementu:</span><span class="sxs-lookup"><span data-stu-id="f49e3-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="f49e3-122">Dodaj następujące parametry połączenia do `<connectionStrings>` element *Web.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="f49e3-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="f49e3-123">W poniższym przykładzie przedstawiono część *Web.config* plik o nowe parametry połączenia dodany:</span><span class="sxs-lookup"><span data-stu-id="f49e3-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="f49e3-124">Parametry połączenia dwóch są bardzo podobne.</span><span class="sxs-lookup"><span data-stu-id="f49e3-124">The two connection strings are very similar.</span></span> <span data-ttu-id="f49e3-125">Pierwszy ciąg połączenia o nazwie `DefaultConnection` i jest używana dla bazy danych członkostwa w celu kontrolowania, kto może uzyskać dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f49e3-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="f49e3-126">Określa ciąg połączenia został dodany, bazy danych LocalDB *Movie.mdf* znajduje się w *aplikacji\_danych* folderu.</span><span class="sxs-lookup"><span data-stu-id="f49e3-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="f49e3-127">Firma Microsoft nie będzie używać bazy danych członkostwa w tym samouczku, aby uzyskać więcej informacji na członkostwo, uwierzytelniania i zabezpieczeń, zobacz Moje samouczek [tworzenie aplikacji ASP.NET MVC z uwierzytelniania i bazy danych SQL i wdrożyć w usłudze Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="f49e3-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="f49e3-128">Nazwa ciągu połączenia musi być zgodna nazwa [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="f49e3-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="f49e3-129">Faktycznie nie trzeba było dodać `MovieDBContext` parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="f49e3-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="f49e3-130">Jeśli nie określisz parametry połączenia programu Entity Framework utworzy bazy danych LocalDB w katalogu użytkowników z w pełni kwalifikowana nazwa [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) klasy (w tym przypadku `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="f49e3-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="f49e3-131">Można określić nazwę bazy danych niczego Ci się podoba, jak długo ma *. MDF* sufiks.</span><span class="sxs-lookup"><span data-stu-id="f49e3-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="f49e3-132">Na przykład można nazwę bazy danych *MyFilms.mdf*.</span><span class="sxs-lookup"><span data-stu-id="f49e3-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="f49e3-133">Następnie będzie utworzyć nowy `MoviesController` klasy, która służy do wyświetlania danych filmu i Zezwalaj użytkownikom na tworzenie nowych list filmu.</span><span class="sxs-lookup"><span data-stu-id="f49e3-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f49e3-134">[Poprzednie](adding-a-model.md)
[dalej](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="f49e3-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>