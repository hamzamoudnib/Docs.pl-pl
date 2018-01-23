---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: "Tworzenie punktu końcowego OData v3 z składnika Web API 2 | Dokumentacja firmy Microsoft"
author: MikeWasson
description: "Open Data Protocol (OData) to protokół dostępu do danych w sieci Web. OData zapewnia jednolity sposób struktury danych, wysyłać zapytania o dane i manipulowanie danymi..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: cb466124aacf6b13c1ade22ad8b865b83e6351e2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="d2abd-104">Tworzenie punktu końcowego OData v3 z składnika Web API 2</span><span class="sxs-lookup"><span data-stu-id="d2abd-104">Creating an OData v3 Endpoint with Web API 2</span></span>
====================
<span data-ttu-id="d2abd-105">przez [Wasson Jan](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d2abd-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d2abd-106">Pobieranie ukończone projektu</span><span class="sxs-lookup"><span data-stu-id="d2abd-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="d2abd-107">[Open Data Protocol](http://www.odata.org/) (OData) to protokół dostępu do danych w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d2abd-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="d2abd-108">OData zapewnia jednolity sposób struktury danych, wysyłać zapytania o dane i manipulowania zestawu danych za pośrednictwem operacji CRUD (tworzenia, odczytu, aktualizacji i usuwania).</span><span class="sxs-lookup"><span data-stu-id="d2abd-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="d2abd-109">OData obsługuje zarówno formaty JSON, jak i AtomPub (XML).</span><span class="sxs-lookup"><span data-stu-id="d2abd-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="d2abd-110">OData definiuje również sposób uwidaczniać metadane dotyczące danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="d2abd-111">Klienci mogą używać metadanych do wykrywania informacji o typie i relacje dla zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
> 
> <span data-ttu-id="d2abd-112">ASP.NET Web API ułatwia tworzenie punktu końcowego OData dla zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="d2abd-113">Można kontrolować, obsługuje punkt końcowy dokładnie operacje OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="d2abd-114">Może obsługiwać wiele punktów końcowych OData, wraz z systemem innym niż OData punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="d2abd-115">Masz pełną kontrolę nad model danych, logika biznesowa zaplecza i warstwy danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d2abd-116">Używane w samouczku wersje oprogramowania</span><span class="sxs-lookup"><span data-stu-id="d2abd-116">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="d2abd-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d2abd-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="d2abd-118">Składnik Web API 2</span><span class="sxs-lookup"><span data-stu-id="d2abd-118">Web API 2</span></span>
> - <span data-ttu-id="d2abd-119">OData w wersji 3</span><span class="sxs-lookup"><span data-stu-id="d2abd-119">OData Version 3</span></span>
> - <span data-ttu-id="d2abd-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d2abd-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="d2abd-121">Web fiddler debugowanie serwera Proxy (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="d2abd-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
> 
> <span data-ttu-id="d2abd-122">Dodano obsługę OData interfejsu API sieci Web w [platformy ASP.NET i zaktualizuj 2012.2 narzędzia sieci Web](https://go.microsoft.com/fwlink/?LinkId=282650).</span><span class="sxs-lookup"><span data-stu-id="d2abd-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="d2abd-123">Ten samouczek nie korzysta jednak funkcja szkieletów, który został dodany w programie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d2abd-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>


<span data-ttu-id="d2abd-124">W tym samouczku utworzysz prosty punktu końcowego OData, którego klienci mogą wykonywać kwerendę.</span><span class="sxs-lookup"><span data-stu-id="d2abd-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="d2abd-125">Zostanie również utworzona klienta C# dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d2abd-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="d2abd-126">Po ukończeniu tego samouczka następnego zestawu samouczki pokazują, jak dodać więcej funkcji, łącznie z relacjami jednostek, akcje, i wybierz Rozwiń $/ $.</span><span class="sxs-lookup"><span data-stu-id="d2abd-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="d2abd-127">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2abd-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="d2abd-128">Dodawanie modelu jednostki</span><span class="sxs-lookup"><span data-stu-id="d2abd-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="d2abd-129">Dodawanie kontrolera OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="d2abd-130">Dodaj EDM i tras</span><span class="sxs-lookup"><span data-stu-id="d2abd-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="d2abd-131">Inicjatora bazy danych (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="d2abd-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="d2abd-132">Eksploracja punktu końcowego OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="d2abd-133">Formaty serializacji OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="d2abd-134">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2abd-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="d2abd-135">W tym samouczku utworzysz punktu końcowego OData, który obsługuje podstawowe operacje CRUD.</span><span class="sxs-lookup"><span data-stu-id="d2abd-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="d2abd-136">Punkt końcowy uwidoczni pojedynczego zasobu, listę produktów.</span><span class="sxs-lookup"><span data-stu-id="d2abd-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="d2abd-137">Kolejnych samouczkach spowoduje dodanie więcej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d2abd-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="d2abd-138">Uruchom program Visual Studio i wybierz **nowy projekt** ze strony początkowej.</span><span class="sxs-lookup"><span data-stu-id="d2abd-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="d2abd-139">Lub z **pliku** menu, wybierz opcję **nowy** , a następnie **projektu**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="d2abd-140">W **szablony** okienku wybierz **zainstalowane szablony** i rozwiń węzeł Visual C#.</span><span class="sxs-lookup"><span data-stu-id="d2abd-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="d2abd-141">W obszarze **Visual C#**, wybierz pozycję **Web**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="d2abd-142">Wybierz **aplikacji sieci Web ASP.NET** szablonu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="d2abd-143">W **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **pusty** szablonu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="d2abd-144">W obszarze &quot;. Dodaj foldery i podstawowe odwołania dla... &quot;, sprawdź **interfejsu API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="d2abd-145">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="d2abd-146">Dodawanie modelu jednostki</span><span class="sxs-lookup"><span data-stu-id="d2abd-146">Add an Entity Model</span></span>

<span data-ttu-id="d2abd-147">A *modelu* jest obiekt, który reprezentuje dane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2abd-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="d2abd-148">W tym samouczku potrzebujemy modelu, który reprezentuje produkt.</span><span class="sxs-lookup"><span data-stu-id="d2abd-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="d2abd-149">Model odnosi się do naszej OData typu jednostki.</span><span class="sxs-lookup"><span data-stu-id="d2abd-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="d2abd-150">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy folder modeli.</span><span class="sxs-lookup"><span data-stu-id="d2abd-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="d2abd-151">Wybierz z menu kontekstowego **Dodaj** następnie wybierz **klasy**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="d2abd-152">W **Dodaj nowy** elementu okna dialogowego, nazwa klasy &quot;produktu&quot;.</span><span class="sxs-lookup"><span data-stu-id="d2abd-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="d2abd-153">Według Konwencji klasy modeli są umieszczane w folderze modeli.</span><span class="sxs-lookup"><span data-stu-id="d2abd-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="d2abd-154">Nie trzeba wykonywać tę Konwencję do własnych projektów, ale użyjemy go do celów tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d2abd-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>


<span data-ttu-id="d2abd-155">W pliku Product.cs Dodaj następującą definicję klasy:</span><span class="sxs-lookup"><span data-stu-id="d2abd-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="d2abd-156">Właściwość Identyfikatora będzie klucza jednostki.</span><span class="sxs-lookup"><span data-stu-id="d2abd-156">The ID property will be the entity key.</span></span> <span data-ttu-id="d2abd-157">Klienci mogą wykonywać kwerendę produktów według identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="d2abd-157">Clients can query products by ID.</span></span> <span data-ttu-id="d2abd-158">To pole będzie także klucz podstawowy w wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="d2abd-159">Teraz skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="d2abd-159">Build the project now.</span></span> <span data-ttu-id="d2abd-160">W następnym kroku użyjemy szkieletów Visual Studio, niektóre używającej odbicia można znaleźć typu produktu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="d2abd-161">Dodawanie kontrolera OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-161">Add an OData Controller</span></span>

<span data-ttu-id="d2abd-162">A *kontrolera* jest klasa, która obsługuje żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2abd-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="d2abd-163">Należy zdefiniować osobnego kontrolera dla każdej jednostki w przypadku usługi OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="d2abd-164">W tym samouczku utworzymy pojedynczy kontroler.</span><span class="sxs-lookup"><span data-stu-id="d2abd-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="d2abd-165">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy folder kontrolery.</span><span class="sxs-lookup"><span data-stu-id="d2abd-165">In Solution Explorer, right-click the the Controllers folder.</span></span> <span data-ttu-id="d2abd-166">Wybierz **Dodaj** , a następnie wybierz **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="d2abd-167">W **Dodawanie szkieletu** okno dialogowe, wybierz opcję &quot;Web Kontroler interfejsu API 2 OData z akcjami używający narzędzia Entity Framework&quot;.</span><span class="sxs-lookup"><span data-stu-id="d2abd-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="d2abd-168">W **Dodaj kontroler** okna dialogowego, nazwy kontrolera "ProductsController".</span><span class="sxs-lookup"><span data-stu-id="d2abd-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="d2abd-169">Wybierz &quot;używać asynchronicznych akcji kontrolera&quot; wyboru.</span><span class="sxs-lookup"><span data-stu-id="d2abd-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="d2abd-170">W **modelu** listy rozwijanej wybierz klasy produktu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="d2abd-171">Kliknij przycisk **nowy kontekst danych...**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="d2abd-171">Click the **New data context...** button.</span></span> <span data-ttu-id="d2abd-172">Pozostaw nazwę domyślną dla typu kontekstu danych, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="d2abd-173">W oknie dialogowym Dodaj kontroler, aby dodać kontroler, kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="d2abd-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="d2abd-174">Uwaga: Jeśli zostanie wyświetlony komunikat o błędzie komunikat &quot;wystąpił błąd podczas pobierania typu... &quot;, upewnij się, że projekt programu Visual Studio zostały utworzone po dodaniu klasy produktu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="d2abd-175">Rusztowania używa odbicia można znaleźć klasy.</span><span class="sxs-lookup"><span data-stu-id="d2abd-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="d2abd-176">Rusztowania dodaje dwa pliki kodu do projektu:</span><span class="sxs-lookup"><span data-stu-id="d2abd-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="d2abd-177">Products.cs definiuje kontrolera interfejsu API sieci Web, który implementuje punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="d2abd-178">ProductServiceContext.cs udostępnia metody do badania podstawowej bazy danych przy użyciu programu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d2abd-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="d2abd-179">Dodaj EDM i tras</span><span class="sxs-lookup"><span data-stu-id="d2abd-179">Add the EDM and Route</span></span>

<span data-ttu-id="d2abd-180">W Eksploratorze rozwiązań rozwiń aplikacji\_Uruchom folderu i Otwórz plik o nazwie WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="d2abd-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="d2abd-181">Ta klasa zawiera kod konfiguracji interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d2abd-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="d2abd-182">Zastąp ten kod poniżej:</span><span class="sxs-lookup"><span data-stu-id="d2abd-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="d2abd-183">Ten kod wykonuje dwie czynności:</span><span class="sxs-lookup"><span data-stu-id="d2abd-183">This code does two things:</span></span>

- <span data-ttu-id="d2abd-184">Tworzy jednostki danych modelu (EDM) dla punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="d2abd-185">Dodaje trasę dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d2abd-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="d2abd-186">EDM jest abstrakcyjny modelu danych.</span><span class="sxs-lookup"><span data-stu-id="d2abd-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="d2abd-187">EDM służy do tworzenia dokument metadanych i określić identyfikatory URI usługi.</span><span class="sxs-lookup"><span data-stu-id="d2abd-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="d2abd-188">**ODataConventionModelBuilder** tworzy EDM przy użyciu zestawu domyślnych konwencji nazewnictwa EDM.</span><span class="sxs-lookup"><span data-stu-id="d2abd-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="d2abd-189">Ta metoda wymaga co najmniej kodu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-189">This approach requires the least code.</span></span> <span data-ttu-id="d2abd-190">Jeśli chcesz mieć większą kontrolę nad EDM, możesz użyć **element ODataModelBuilder** klasy można utworzyć przez dodanie jawnie właściwości, kluczy i właściwości nawigacji EDM.</span><span class="sxs-lookup"><span data-stu-id="d2abd-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="d2abd-191">**EntitySet** metoda dodaje zestaw jednostek do EDM:</span><span class="sxs-lookup"><span data-stu-id="d2abd-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="d2abd-192">Ciąg "Produktów" Określa nazwę zestawu jednostek.</span><span class="sxs-lookup"><span data-stu-id="d2abd-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="d2abd-193">Nazwa kontrolera musi odpowiadać nazwie zestawu jednostek.</span><span class="sxs-lookup"><span data-stu-id="d2abd-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="d2abd-194">W tym samouczku zestaw jednostek ma nazwę "Produkty" i nazwie kontrolera `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="d2abd-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="d2abd-195">Jeśli użytkownik o nazwie "ProductSet" Zestaw jednostek, czy nazwa kontrolera `ProductSetController`.</span><span class="sxs-lookup"><span data-stu-id="d2abd-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="d2abd-196">Należy pamiętać, że punkt końcowy może mieć wiele zestawów jednostek.</span><span class="sxs-lookup"><span data-stu-id="d2abd-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="d2abd-197">Wywołanie **EntitySet&lt;T&gt;**  dla każdej jednostki ustawiona, a następnie zdefiniuj odpowiedniego kontrolera.</span><span class="sxs-lookup"><span data-stu-id="d2abd-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="d2abd-198">**MapODataRoute** metoda dodaje trasę dla punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="d2abd-199">Pierwszym parametrem jest przyjazną nazwę dla trasy.</span><span class="sxs-lookup"><span data-stu-id="d2abd-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="d2abd-200">Klienci usługi nie ma tę nazwę.</span><span class="sxs-lookup"><span data-stu-id="d2abd-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="d2abd-201">Drugi parametr jest prefiksem identyfikatora URI dla punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d2abd-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="d2abd-202">Biorąc pod uwagę ten kod, identyfikator URI dla zestawu jednostek produktów jest http://*hostname*  /odata/produktów.</span><span class="sxs-lookup"><span data-stu-id="d2abd-202">Given this code, the URI for the Products entity set is http://*hostname*/odata/Products.</span></span> <span data-ttu-id="d2abd-203">Aplikacja może mieć więcej niż jeden punkt końcowy OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="d2abd-204">Dla każdego punktu końcowego, należy wywołać **MapODataRoute** i podaj nazwę unikatową trasę i unikatowy prefiks identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="d2abd-204">For each endpoint, call **MapODataRoute** and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="d2abd-205">Inicjatora bazy danych (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="d2abd-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="d2abd-206">W tym kroku użyjesz programu Entity Framework do inicjatora bazy danych o dane testowe.</span><span class="sxs-lookup"><span data-stu-id="d2abd-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="d2abd-207">Ten krok jest opcjonalny, ale dzięki temu można od razu przetestować punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="d2abd-208">Z **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki**, a następnie wybierz pozycję **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-208">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d2abd-209">W oknie Konsola Menedżera pakietów wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d2abd-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="d2abd-210">Spowoduje to dodanie do folderu o nazwie migracji i o nazwie Configuration.cs pliku kodu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="d2abd-211">Otwórz ten plik i Dodaj następujący kod do `Configuration.Seed` metody.</span><span class="sxs-lookup"><span data-stu-id="d2abd-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="d2abd-212">W oknie konsoli Menedżera pakietów wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d2abd-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="d2abd-213">Te polecenia generowania kodu, który utworzy bazę danych, a następnie wykonuje kodu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="d2abd-214">Eksploracja punktu końcowego OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="d2abd-215">W tej sekcji użyjemy [debugowanie serwera Proxy sieci Web Fiddler](http://www.fiddler2.com) do wysyłania żądań do punktu końcowego i sprawdź, czy wiadomości odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d2abd-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="d2abd-216">Pomoże to zrozumieć możliwości punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="d2abd-217">W programie Visual Studio naciśnij klawisz F5, aby rozpocząć debugowania.</span><span class="sxs-lookup"><span data-stu-id="d2abd-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="d2abd-218">Domyślnie program Visual Studio Otwiera przeglądarkę, aby `http://localhost:*port*`, gdzie *portu* jest numerem portu skonfigurowanego w ustawieniach projektu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="d2abd-219">Można zmienić numer portu w ustawieniach projektu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="d2abd-220">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="d2abd-221">W oknie właściwości wybierz **Web**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="d2abd-222">Wprowadź numer portu w ramach **adres Url projektu**.</span><span class="sxs-lookup"><span data-stu-id="d2abd-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="d2abd-223">Dokument usługi</span><span class="sxs-lookup"><span data-stu-id="d2abd-223">Service Document</span></span>

<span data-ttu-id="d2abd-224">*Dokument usługi* znajduje się lista zestawów jednostek dla punktu końcowego OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="d2abd-225">Aby uzyskać dokumentu usługi, Wyślij żądanie GET z głównym identyfikatorem URI usługi.</span><span class="sxs-lookup"><span data-stu-id="d2abd-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="d2abd-226">Przy użyciu programu Fiddler, wprowadź następujący identyfikator URI w **Composer** kartę: `http://localhost:port/odata/`, gdzie *portu* numer portu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="d2abd-227">Kliknij przycisk **Execute** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d2abd-227">Click the **Execute** button.</span></span> <span data-ttu-id="d2abd-228">Fiddler wysyła żądanie HTTP GET do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2abd-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="d2abd-229">Powinna zostać wyświetlona odpowiedź na liście sesji w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d2abd-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="d2abd-230">Jeśli wszystko działa kod stanu będzie 200.</span><span class="sxs-lookup"><span data-stu-id="d2abd-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="d2abd-231">Kliknij dwukrotnie pozycję na liście sesji w sieci Web, aby wyświetlić szczegóły komunikatu odpowiedzi na karcie inspektorzy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d2abd-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="d2abd-232">Nieprzetworzona komunikat odpowiedzi HTTP powinien wyglądać podobnie do następującego:</span><span class="sxs-lookup"><span data-stu-id="d2abd-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="d2abd-233">Domyślnie interfejsu API sieci Web zwraca dokumentu usługi w formacie AtomPub.</span><span class="sxs-lookup"><span data-stu-id="d2abd-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="d2abd-234">Aby poprosić o JSON, Dodaj następujący nagłówek do żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="d2abd-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="d2abd-235">Odpowiedź HTTP zawiera teraz ładunek JSON:</span><span class="sxs-lookup"><span data-stu-id="d2abd-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="d2abd-236">Dokument metadanych usługi</span><span class="sxs-lookup"><span data-stu-id="d2abd-236">Service Metadata Document</span></span>

<span data-ttu-id="d2abd-237">*Dokument metadanych usługi* opisano model danych usługi przy użyciu języka XML zwanej języka definicji schematu koncepcyjnego (CSDL).</span><span class="sxs-lookup"><span data-stu-id="d2abd-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="d2abd-238">Dokument metadanych zawiera struktury danych w usłudze i może służyć do generowania kodu klienta.</span><span class="sxs-lookup"><span data-stu-id="d2abd-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="d2abd-239">Aby uzyskać ten dokument metadanych, Wyślij żądanie GET `http://localhost:port/odata/$metadata`.</span><span class="sxs-lookup"><span data-stu-id="d2abd-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="d2abd-240">Oto metadanych dla punktu końcowego przedstawiona w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d2abd-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="d2abd-241">Zestaw jednostek</span><span class="sxs-lookup"><span data-stu-id="d2abd-241">Entity Set</span></span>

<span data-ttu-id="d2abd-242">Aby uzyskać zestaw jednostek produktów, Wyślij żądanie GET `http://localhost:port/odata/Products`.</span><span class="sxs-lookup"><span data-stu-id="d2abd-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="d2abd-243">Jednostka</span><span class="sxs-lookup"><span data-stu-id="d2abd-243">Entity</span></span>

<span data-ttu-id="d2abd-244">Aby uzyskać indywidualnych produktów, Wyślij żądanie GET `http://localhost:port/odata/Products(1)`, gdzie "1" jest identyfikatora produktu.</span><span class="sxs-lookup"><span data-stu-id="d2abd-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="d2abd-245">Formaty serializacji OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-245">OData Serialization Formats</span></span>

<span data-ttu-id="d2abd-246">OData obsługuje wiele formatów serializacji:</span><span class="sxs-lookup"><span data-stu-id="d2abd-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="d2abd-247">Protokołu Atom (XML)</span><span class="sxs-lookup"><span data-stu-id="d2abd-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="d2abd-248">JSON "jasny" (zostanie wprowadzony w OData v3)</span><span class="sxs-lookup"><span data-stu-id="d2abd-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="d2abd-249">JSON "pełny" (OData v2)</span><span class="sxs-lookup"><span data-stu-id="d2abd-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="d2abd-250">Domyślnie interfejsu API sieci Web w formacie AtomPubJSON "jasny".</span><span class="sxs-lookup"><span data-stu-id="d2abd-250">By default, Web API uses AtomPubJSON "light" format.</span></span> 

<span data-ttu-id="d2abd-251">Aby uzyskać AtomPub format, ustaw nagłówek Accept "application/atom + xml".</span><span class="sxs-lookup"><span data-stu-id="d2abd-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="d2abd-252">Oto przykład treści odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="d2abd-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="d2abd-253">Zostanie wyświetlony niedogodność widocznych w formacie Atom: jest znacznie pełniejszą niż lekka serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="d2abd-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="d2abd-254">Jednak jeśli klienta, która obsługuje usługę AtomPub, klient może preferować tego formatu w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="d2abd-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="d2abd-255">Oto JSON światła wersji tego samego obiektu:</span><span class="sxs-lookup"><span data-stu-id="d2abd-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="d2abd-256">Format JSON światła została wprowadzona w wersji 3 protokołu OData.</span><span class="sxs-lookup"><span data-stu-id="d2abd-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="d2abd-257">W celu zapewnienia zgodności z poprzednimi wersjami starszego formatu JSON "pełny" może żądać klient.</span><span class="sxs-lookup"><span data-stu-id="d2abd-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="d2abd-258">Aby zażądać informacji pełnej JSON, ustawić nagłówek Accept `application/json;odata=verbose`.</span><span class="sxs-lookup"><span data-stu-id="d2abd-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="d2abd-259">Oto pełne wersji:</span><span class="sxs-lookup"><span data-stu-id="d2abd-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="d2abd-260">Ten format przekazuje więcej metadanych w treści odpowiedzi, które można dodać znaczne obciążenie w czasie całej sesji.</span><span class="sxs-lookup"><span data-stu-id="d2abd-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="d2abd-261">Ponadto dodaje poziom pośredni zawijania obiekt we właściwości o nazwie "d".</span><span class="sxs-lookup"><span data-stu-id="d2abd-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2abd-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d2abd-262">Next Steps</span></span>

- [<span data-ttu-id="d2abd-263">Dodawanie relacji jednostki</span><span class="sxs-lookup"><span data-stu-id="d2abd-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="d2abd-264">Dodaj akcje OData</span><span class="sxs-lookup"><span data-stu-id="d2abd-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="d2abd-265">Wywoływanie usługi OData z klienta .NET</span><span class="sxs-lookup"><span data-stu-id="d2abd-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)