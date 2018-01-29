---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: "Sprawdzanie poprawności z idataerrorinfo — interfejs (C#) | Dokumentacja firmy Microsoft"
author: StephenWalther
description: "Stephen Walther przedstawiono sposób wyświetlania niestandardowych komunikatów o błędach zaimplementowanie idataerrorinfo — interfejs klasy modelu."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: c04088c576481e4a91676d7e6962c03b56e7a8a4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="68ea6-103">Sprawdzanie poprawności z idataerrorinfo — interfejs (C#)</span><span class="sxs-lookup"><span data-stu-id="68ea6-103">Validating with the IDataErrorInfo Interface (C#)</span></span>
====================
<span data-ttu-id="68ea6-104">przez [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="68ea6-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="68ea6-105">Stephen Walther przedstawiono sposób wyświetlania niestandardowych komunikatów o błędach zaimplementowanie idataerrorinfo — interfejs klasy modelu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>


<span data-ttu-id="68ea6-106">Celem tego samouczka jest wyjaśniono jeden z nich do przeprowadzania weryfikacji w aplikacji platformy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="68ea6-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="68ea6-107">Sposób zapobiec ktoś przesyłania formularza HTML bez podawania wartości wymaganych pól formularza.</span><span class="sxs-lookup"><span data-stu-id="68ea6-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="68ea6-108">W tym samouczku Dowiedz się jak przeprowadzić weryfikacji za pomocą interfejsu IErrorDataInfo.</span><span class="sxs-lookup"><span data-stu-id="68ea6-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="68ea6-109">Założenia</span><span class="sxs-lookup"><span data-stu-id="68ea6-109">Assumptions</span></span>

<span data-ttu-id="68ea6-110">W tym samouczku I Użyj bazy danych MoviesDB i filmy tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68ea6-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="68ea6-111">Ta tabela zawiera następujące kolumny:</span><span class="sxs-lookup"><span data-stu-id="68ea6-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>


| <span data-ttu-id="68ea6-112">**Nazwa kolumny**</span><span class="sxs-lookup"><span data-stu-id="68ea6-112">**Column Name**</span></span> | <span data-ttu-id="68ea6-113">**Typ danych**</span><span class="sxs-lookup"><span data-stu-id="68ea6-113">**Data Type**</span></span> | <span data-ttu-id="68ea6-114">**Dopuszcza wartości null**</span><span class="sxs-lookup"><span data-stu-id="68ea6-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68ea6-115">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="68ea6-115">Id</span></span> | <span data-ttu-id="68ea6-116">int</span><span class="sxs-lookup"><span data-stu-id="68ea6-116">Int</span></span> | <span data-ttu-id="68ea6-117">False</span><span class="sxs-lookup"><span data-stu-id="68ea6-117">False</span></span> |
| <span data-ttu-id="68ea6-118">Tytuł</span><span class="sxs-lookup"><span data-stu-id="68ea6-118">Title</span></span> | <span data-ttu-id="68ea6-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="68ea6-119">Nvarchar(100)</span></span> | <span data-ttu-id="68ea6-120">False</span><span class="sxs-lookup"><span data-stu-id="68ea6-120">False</span></span> |
| <span data-ttu-id="68ea6-121">Dyrektor</span><span class="sxs-lookup"><span data-stu-id="68ea6-121">Director</span></span> | <span data-ttu-id="68ea6-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="68ea6-122">Nvarchar(100)</span></span> | <span data-ttu-id="68ea6-123">False</span><span class="sxs-lookup"><span data-stu-id="68ea6-123">False</span></span> |
| <span data-ttu-id="68ea6-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="68ea6-124">DateReleased</span></span> | <span data-ttu-id="68ea6-125">DataGodzina</span><span class="sxs-lookup"><span data-stu-id="68ea6-125">DateTime</span></span> | <span data-ttu-id="68ea6-126">False</span><span class="sxs-lookup"><span data-stu-id="68ea6-126">False</span></span> |


<span data-ttu-id="68ea6-127">W tym samouczku używam programu Entity Framework firmy Microsoft do generowania klasy modelu mojej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68ea6-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="68ea6-128">Klasa filmu generowane przez program Entity Framework jest wyświetlany na rysunku 1.</span><span class="sxs-lookup"><span data-stu-id="68ea6-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>


<span data-ttu-id="68ea6-129">[![Jednostka film](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="68ea6-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="68ea6-130">**Rysunek 01**: jednostki Movie ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="68ea6-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="68ea6-131">Aby dowiedzieć się więcej o korzystaniu z programu Entity Framework do generowania klasy modelu z bazy danych, zobacz temat zatytułowany Moje samouczek: Tworzenie klasy modelu Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="68ea6-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>


## <a name="the-controller-class"></a><span data-ttu-id="68ea6-132">Klasa kontrolera</span><span class="sxs-lookup"><span data-stu-id="68ea6-132">The Controller Class</span></span>

<span data-ttu-id="68ea6-133">Możemy użyć kontrolera głównej do listy filmów i Utwórz nowości.</span><span class="sxs-lookup"><span data-stu-id="68ea6-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="68ea6-134">Kod dla tej klasy są zawarte w wyświetlania 1.</span><span class="sxs-lookup"><span data-stu-id="68ea6-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="68ea6-135">**Wyświetlanie listy 1 - Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="68ea6-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="68ea6-136">Klasy kontrolera głównej w 1 Lista zawiera dwa działania Create().</span><span class="sxs-lookup"><span data-stu-id="68ea6-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="68ea6-137">Pierwszą akcją Wyświetla formularza HTML służący do tworzenia nowych filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="68ea6-138">Drugiej akcji Create() wykonuje rzeczywiste Wstaw nowe filmu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="68ea6-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="68ea6-139">Drugiej akcji Create() jest wywoływana po przesłaniu formularza wyświetlany przez pierwszą akcją Create() do serwera.</span><span class="sxs-lookup"><span data-stu-id="68ea6-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="68ea6-140">Zwróć uwagę, że drugiej akcji Create() zawiera następujące wiersze kodu:</span><span class="sxs-lookup"><span data-stu-id="68ea6-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="68ea6-141">Właściwość IsValid zwraca wartość false, gdy występuje błąd weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="68ea6-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="68ea6-142">W takim przypadku widok Utwórz zawierający formularz HTML do tworzenia filmu zostanie wyświetlony ponownie.</span><span class="sxs-lookup"><span data-stu-id="68ea6-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="68ea6-143">Tworzenie klasy częściowe</span><span class="sxs-lookup"><span data-stu-id="68ea6-143">Creating a Partial Class</span></span>

<span data-ttu-id="68ea6-144">Klasa film jest generowany przez program Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="68ea6-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="68ea6-145">Można wyświetlić kod klasy filmu Rozwiń plik MoviesDBModel.edmx w oknie Eksploratora rozwiązań i Otwórz plik MoviesDBModel.Designer.cs w edytorze kodu (patrz rysunek 2).</span><span class="sxs-lookup"><span data-stu-id="68ea6-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>


<span data-ttu-id="68ea6-146">[![Kod dla obiekt filmu](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="68ea6-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="68ea6-147">**Rysunek 02**: kod dla obiekt filmu ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="68ea6-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>


<span data-ttu-id="68ea6-148">Klasa film jest klasy częściowej.</span><span class="sxs-lookup"><span data-stu-id="68ea6-148">The Movie class is a partial class.</span></span> <span data-ttu-id="68ea6-149">Oznacza to, że możemy dodać innej klasy częściowe o takiej samej nazwie, aby rozszerzyć funkcjonalność klasy filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="68ea6-150">Dodamy logiki sprawdzania poprawności do nowej klasy częściowej.</span><span class="sxs-lookup"><span data-stu-id="68ea6-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="68ea6-151">Dodaj klasę wyświetlania 2 do folderu modeli.</span><span class="sxs-lookup"><span data-stu-id="68ea6-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="68ea6-152">**Wyświetlanie listy 2 - Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="68ea6-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="68ea6-153">Należy zauważyć, że klasa wyświetlania 2 zawiera *częściowe* modyfikator.</span><span class="sxs-lookup"><span data-stu-id="68ea6-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="68ea6-154">Wszystkie metody lub właściwości, które można dodać do tej klasy staną się częścią klasy filmu generowane przez program Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="68ea6-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="68ea6-155">Dodawanie OnChanging i metody częściowe OnChanged</span><span class="sxs-lookup"><span data-stu-id="68ea6-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="68ea6-156">Entity Framework, generując klasę jednostki, Entity Framework dodaje metody częściowe do klasy automatycznie.</span><span class="sxs-lookup"><span data-stu-id="68ea6-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="68ea6-157">Entity Framework generuje OnChanging i OnChanged metody częściowe, które odpowiadają każdej właściwości klasy.</span><span class="sxs-lookup"><span data-stu-id="68ea6-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="68ea6-158">W przypadku klasy filmu programu Entity Framework utworzy następujących metod:</span><span class="sxs-lookup"><span data-stu-id="68ea6-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="68ea6-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="68ea6-159">OnIdChanging</span></span>
- <span data-ttu-id="68ea6-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="68ea6-160">OnIdChanged</span></span>
- <span data-ttu-id="68ea6-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="68ea6-161">OnTitleChanging</span></span>
- <span data-ttu-id="68ea6-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="68ea6-162">OnTitleChanged</span></span>
- <span data-ttu-id="68ea6-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="68ea6-163">OnDirectorChanging</span></span>
- <span data-ttu-id="68ea6-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="68ea6-164">OnDirectorChanged</span></span>
- <span data-ttu-id="68ea6-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="68ea6-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="68ea6-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="68ea6-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="68ea6-167">Metoda OnChanging jest wywoływana prawo, zanim odpowiadających im właściwości zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="68ea6-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="68ea6-168">Metoda OnChanged jest wywoływana prawej, po zmianie właściwości.</span><span class="sxs-lookup"><span data-stu-id="68ea6-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="68ea6-169">Można korzystać z tych metod częściowych Dodaj logikę sprawdzania poprawności do klasy filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="68ea6-170">Aktualizacja klasy filmu w 3 wyświetlania sprawdza, czy tytuł i dyrektora przypisano niepusty wartości.</span><span class="sxs-lookup"><span data-stu-id="68ea6-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="68ea6-171">Metoda częściowa to metoda zdefiniowana w klasie, która nie jest wymagane do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="68ea6-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="68ea6-172">Jeśli nie implementować metodę częściową kompilator usuwa podpis metody i wszystkie wywołania metody, więc są Brak kosztów czasu wykonywania skojarzony z metody częściowej.</span><span class="sxs-lookup"><span data-stu-id="68ea6-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="68ea6-173">W Visual Studio edytorze kodu, można dodać metody częściowej wpisując słowo kluczowe *częściowe* następuje spacja, aby wyświetlić listę częściowe do zaimplementowania.</span><span class="sxs-lookup"><span data-stu-id="68ea6-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>


<span data-ttu-id="68ea6-174">**Wyświetlanie listy 3 - Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="68ea6-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="68ea6-175">Na przykład, Jeśli spróbujesz przypisać pusty ciąg dla właściwości Title, następnie komunikat o błędzie jest przypisany do słownika o nazwie \_błędy.</span><span class="sxs-lookup"><span data-stu-id="68ea6-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="68ea6-176">W tym momencie faktycznie nie powoduje żadnych zmian pustego ciągu można przypisać do właściwości tytuł i błąd zostanie dodany do prywatnego \_pola błędy.</span><span class="sxs-lookup"><span data-stu-id="68ea6-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="68ea6-177">Musimy zaimplementować interfejsu idataerrorinfo — Aby udostępnić te błędy weryfikacji do platformę ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="68ea6-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="68ea6-178">Implementowanie idataerrorinfo — interfejs</span><span class="sxs-lookup"><span data-stu-id="68ea6-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="68ea6-179">Idataerrorinfo — interfejs został częścią programu .NET framework od pierwszej wersji.</span><span class="sxs-lookup"><span data-stu-id="68ea6-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="68ea6-180">Ten interfejs jest bardzo prosty interfejs:</span><span class="sxs-lookup"><span data-stu-id="68ea6-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="68ea6-181">Jeśli klasa implementuje interfejs idataerrorinfo —, platforma ASP.NET MVC zostanie użyty ten interfejs, podczas tworzenia wystąpienia klasy.</span><span class="sxs-lookup"><span data-stu-id="68ea6-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="68ea6-182">Na przykład kontroler głównej akcji Create() akceptuje wystąpienia klasy film:</span><span class="sxs-lookup"><span data-stu-id="68ea6-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="68ea6-183">Platforma ASP.NET MVC tworzy wystąpienie filmu przekazany do akcji Create() za pomocą integratora modelu (DefaultModelBinder).</span><span class="sxs-lookup"><span data-stu-id="68ea6-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="68ea6-184">Integrator modelu jest odpowiedzialny za tworzenie wystąpienia obiektu filmu przez powiązanie pola formularza HTML do wystąpienia obiektu filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="68ea6-185">DefaultModelBinder wykrywa, czy klasa implementuje interfejs idataerrorinfo —.</span><span class="sxs-lookup"><span data-stu-id="68ea6-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="68ea6-186">Jeśli klasa implementuje ten interfejs integratora modelu wywołuje indeksatora IDataErrorInfo.this dla każdej właściwości klasy.</span><span class="sxs-lookup"><span data-stu-id="68ea6-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="68ea6-187">Jeśli indeksatora zwraca komunikat o błędzie integratora modelu dodaje ten komunikat o błędzie do modelowania stanu automatycznie.</span><span class="sxs-lookup"><span data-stu-id="68ea6-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="68ea6-188">DefaultModelBinder sprawdza również właściwość IDataErrorInfo.Error.</span><span class="sxs-lookup"><span data-stu-id="68ea6-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="68ea6-189">Ta właściwość jest przeznaczona do reprezentowania błędy sprawdzania poprawności określonego niż właściwość skojarzonego z klasą.</span><span class="sxs-lookup"><span data-stu-id="68ea6-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="68ea6-190">Na przykład można wymuszać reguły sprawdzania poprawności, która zależy od wartości wielu właściwości klasy filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="68ea6-191">W takim przypadku zwróci błąd sprawdzania poprawności z właściwości błędu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="68ea6-192">Zaktualizowano klasy filmu w listę 4 implementuje interfejs idataerrorinfo —.</span><span class="sxs-lookup"><span data-stu-id="68ea6-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="68ea6-193">**Wyświetlanie listy 4 - Models\Movie.cs (implementuje idataerrorinfo —)**</span><span class="sxs-lookup"><span data-stu-id="68ea6-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="68ea6-194">W przypadku wyświetlania 4 sprawdza właściwości indeksatora \_kolekcji błędów, aby zobaczyć, czy zawiera klucz, który odpowiada nazwie właściwości przekazany do indeksatora.</span><span class="sxs-lookup"><span data-stu-id="68ea6-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="68ea6-195">Jeśli nie było weryfikacji błędu skojarzony z właściwością, zwracany jest pustym ciągiem.</span><span class="sxs-lookup"><span data-stu-id="68ea6-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="68ea6-196">Nie należy modyfikować kontrolera głównej w dowolny sposób, aby użyć zmodyfikowane klasy filmu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="68ea6-197">Strona wyświetlona na rysunku 3 przedstawiono, co się stanie, gdy została wprowadzona żadna wartość dla pola formularza tytuł lub dyrektor.</span><span class="sxs-lookup"><span data-stu-id="68ea6-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>


<span data-ttu-id="68ea6-198">[![Automatyczne tworzenie metod akcji](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="68ea6-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="68ea6-199">**Rysunek 03**: formularza z brakujące wartości ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="68ea6-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>


<span data-ttu-id="68ea6-200">Należy zauważyć, sprawdzania poprawności wartości DateReleased automatycznie.</span><span class="sxs-lookup"><span data-stu-id="68ea6-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="68ea6-201">Ponieważ właściwość DateReleased nie akceptuje wartości NULL, DefaultModelBinder generuje błąd sprawdzania poprawności dla tej właściwości automatycznie, gdy nie ma wartości.</span><span class="sxs-lookup"><span data-stu-id="68ea6-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="68ea6-202">Jeśli chcesz zmodyfikować komunikat o błędzie dla właściwości DateReleased, a następnie należy utworzyć niestandardowego integratora modelu.</span><span class="sxs-lookup"><span data-stu-id="68ea6-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="68ea6-203">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="68ea6-203">Summary</span></span>

<span data-ttu-id="68ea6-204">W tym samouczku przedstawiono sposób idataerrorinfo — interfejs umożliwia generowanie komunikatów o błędach weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="68ea6-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="68ea6-205">Po pierwsze utworzyliśmy częściowej klasy film, rozszerzający funkcje klasy częściowej filmu generowane przez program Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="68ea6-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="68ea6-206">Następnie dodano logikę weryfikacji filmu klasy OnTitleChanging() OnDirectorChanging() częściowe metod i.</span><span class="sxs-lookup"><span data-stu-id="68ea6-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="68ea6-207">Na koniec wprowadziliśmy idataerrorinfo — interfejs, aby udostępnić te komunikatów dotyczących sprawdzania poprawności na platformę ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="68ea6-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="68ea6-208">[Poprzednie](performing-simple-validation-cs.md)
[dalej](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="68ea6-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>