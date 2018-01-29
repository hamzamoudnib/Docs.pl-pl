---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: "Dodawanie nowej kategorii do DropDownList przy użyciu interfejsu użytkownika jQuery | Dokumentacja firmy Microsoft"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2012
ms.topic: article
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: de661616ff3ca83052ae74d3ae6810d014aff764
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="ed593-102">Dodawanie nowej kategorii do DropDownList przy użyciu interfejsu użytkownika jQuery</span><span class="sxs-lookup"><span data-stu-id="ed593-102">Adding a New Category to the DropDownList using jQuery UI</span></span>
====================
<span data-ttu-id="ed593-103">Przez [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="ed593-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="ed593-104">Kod HTML `Select` tag jest idealny dla prezentowanie dane stałej kategorii, ale często konieczne jest dodanie nowej kategorii.</span><span class="sxs-lookup"><span data-stu-id="ed593-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="ed593-105">Załóżmy, że chcemy, aby dodać genre "Opera" do kategorii w naszej bazie danych?</span><span class="sxs-lookup"><span data-stu-id="ed593-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="ed593-106">W tej sekcji użyjemy jQuery interfejsu użytkownika można dodać okno dialogowe, które możemy użyć, aby dodać nową kategorię.</span><span class="sxs-lookup"><span data-stu-id="ed593-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="ed593-107">Na poniższym obrazie pokazano, jak interfejsu użytkownika będą obecne w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ed593-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="ed593-108">Gdy użytkownik wybierze **Dodaj nowe Genre** łącza, wyskakujące okno dialogowe monituje użytkownika o nazwę nowej genre (i opcjonalnie opis).</span><span class="sxs-lookup"><span data-stu-id="ed593-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="ed593-109">Obraz poniżej Pokaż **dodać Genre** podręczne okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ed593-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="ed593-110">Po wprowadzeniu nową nazwę genre i **zapisać** przycisk jest naciśnięty, wykonywane są następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed593-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="ed593-111">Wywołanie AJAX przesyła dane do metody Create kontrolera Genre, co nowego genre jest zapisywany w bazie danych i zwraca nowy rodzaju informacje (genre nazwy i Identyfikatora) jako JSON.</span><span class="sxs-lookup"><span data-stu-id="ed593-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="ed593-112">JavaScript dodaje nowe dane genre do listy wyboru.</span><span class="sxs-lookup"><span data-stu-id="ed593-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="ed593-113">JavaScript sprawia, że nowe genre wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="ed593-113">JavaScript makes the new genre the selected item.</span></span>

 <span data-ttu-id="ed593-114">Na ilustracji poniżej **Opera** został dodany do bazy danych i wybrana w **Genre** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ed593-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="ed593-115">Otwórz *Views\StoreManager\Create.cshtml* plików i Zastąp znaczników genre następujące następujący kod:</span><span class="sxs-lookup"><span data-stu-id="ed593-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="ed593-116">`_ChooseGenre` Widoku częściowego będzie zawierać całą logikę umożliwiającą dołączenie JavaScript i jQuery używane do implementowania nowej funkcji genre Dodaj.</span><span class="sxs-lookup"><span data-stu-id="ed593-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="ed593-117">Firma Microsoft ma zakończonego kod będzie prosty w tym samym z wykonawcy interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ed593-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="ed593-118">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *Views\StoreManager* i wybierz polecenie **Dodaj**, następnie **widoku**.</span><span class="sxs-lookup"><span data-stu-id="ed593-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="ed593-119">W **nazwy widoku** danych wejściowych, wprowadź `_ChooseGenre` następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ed593-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="ed593-120">Zastąp kod znaczników w *Views\StoreManager\\_ChooseGenre.cshtml* pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="ed593-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="ed593-121">Pierwszy wiersz deklaruje możemy przekazywane w `Album` jako nasz model, dokładnie tak samo modelu odnaleziony w widoku Tworzenie instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ed593-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="ed593-122">Następnych kilku wierszy są **etykiety** pomocnika znaczników.</span><span class="sxs-lookup"><span data-stu-id="ed593-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="ed593-123">Następnego wiersza jest **DropDownList** wywołać pomocnika, dokładnie tak samo jak oryginalne widoku Utwórz.</span><span class="sxs-lookup"><span data-stu-id="ed593-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="ed593-124">Dodaje następnego wiersza łącze o nazwie `Add New Genre`, i style go jak przycisk.</span><span class="sxs-lookup"><span data-stu-id="ed593-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="ed593-125">Wiersz zawierający `ValidationMessageFor` jest kopiowana bezpośrednio z tworzenia widoku.</span><span class="sxs-lookup"><span data-stu-id="ed593-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="ed593-126">Następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="ed593-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="ed593-127">Tworzy DZIEL ukrytego, o identyfikatorze `genreDialog`.</span><span class="sxs-lookup"><span data-stu-id="ed593-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="ed593-128">Używamy jQuery do Podłączanie naszych **dodać Genre** okno dialogowe z Identyfikatorem `genreDialog` w tym div.</span><span class="sxs-lookup"><span data-stu-id="ed593-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="ed593-129">Ostatnie dwa tagi skryptu zawiera łącza do plików JavaScript, które będą używane do implementowania nowej funkcji genre Dodaj.</span><span class="sxs-lookup"><span data-stu-id="ed593-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="ed593-130">*/Scripts/chooseGenre.js* pliku została podana dla Ciebie w projekcie zostaną omówione ją później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="ed593-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="ed593-131">Uruchom aplikację i wybierz polecenie **Dodaj nowe Genre** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed593-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="ed593-132">W **dodać Genre** okna dialogowego wprowadź **Opera** w **nazwa** pola wejściowego.</span><span class="sxs-lookup"><span data-stu-id="ed593-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="ed593-133">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed593-133">Click the **Save** button.</span></span> <span data-ttu-id="ed593-134">Wywołanie AJAX kategorii Opera tworzy następnie wypełnia listy rozwijanej z Opera i ustawia Opera jako wybranego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="ed593-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="ed593-135">Wprowadź wykonawcy, tytuł i cen, a następnie wybierz **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed593-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="ed593-136">Po wprowadzeniu cen mniejszej niż $8.99 nowy album pojawi się u góry widoku indeksu.</span><span class="sxs-lookup"><span data-stu-id="ed593-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="ed593-137">Sprawdź, czy nowy wpis albumu został zapisany w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="ed593-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="ed593-138">Spróbuj utworzyć nowy genre z tylko jedną literę.</span><span class="sxs-lookup"><span data-stu-id="ed593-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="ed593-139">Poniższy kod w *Models\Genre.cs* plik Ustawia minimalną i maksymalną długość nazwy rodzaju.</span><span class="sxs-lookup"><span data-stu-id="ed593-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="ed593-140">Sprawdzanie poprawności po stronie klienta zgłasza, że należy wprowadzić ciąg od 2 do 20 znaków.</span><span class="sxs-lookup"><span data-stu-id="ed593-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="ed593-141">Badanie jak Genre nowe jest dodawany do bazy danych i listy wybierz.</span><span class="sxs-lookup"><span data-stu-id="ed593-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="ed593-142">Otwórz *Scripts\chooseGenre.js* pliku i sprawdź, czy kod.</span><span class="sxs-lookup"><span data-stu-id="ed593-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="ed593-143">Drugi wiersz używa Identyfikatora `genreDialog` Aby utworzyć okno dialogowe na znacznik div w *Views\StoreManager\\_ChooseGenre.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="ed593-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="ed593-144">Większość nazwane parametry to wymaga dodatkowych objaśnień.</span><span class="sxs-lookup"><span data-stu-id="ed593-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="ed593-145">`autoOpen` Parametr ma wartość false, wybierając **utworzyć Genre** przycisku spowoduje otwarcie dialogu jawnie (to jest opisany w ostatnim).</span><span class="sxs-lookup"><span data-stu-id="ed593-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="ed593-146">Okno dialogowe ma dwa przyciski **zapisać** i **anulować**.</span><span class="sxs-lookup"><span data-stu-id="ed593-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="ed593-147">**Anulować** kliknięcie przycisku powoduje zamknięcie okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ed593-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="ed593-148">Poniższy kod przedstawia **zapisać** przycisk funkcji.</span><span class="sxs-lookup"><span data-stu-id="ed593-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="ed593-149">`var createGenreForm` Wybrano `createGenreForm` identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="ed593-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="ed593-150">`createGenreForm` Identyfikator został ustawiony w poniższym kodzie w *Views\Genre\\_CreateGenre.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="ed593-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="ed593-151">[Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) przeciążenia pomocnika używany w *Views\Genre\\_CreateGenre.cshtml* pliku generuje kod HTML z atrybutem akcji zawierający adres URL przesyłania formularza.</span><span class="sxs-lookup"><span data-stu-id="ed593-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="ed593-152">Można to sprawdzić wyświetlanie albumów tworzenia strony w przeglądarce, a, wybierając źródło Pokaż w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ed593-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="ed593-153">Następujący kod przedstawia wygenerowanego kodu HTML zawierający tag formularza.</span><span class="sxs-lookup"><span data-stu-id="ed593-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="ed593-154">JQuery `$.post` wiersza wykonuje wywołanie AJAX atrybut akcji (`/StoreManager/Create`) i przekazuje dane z **utworzyć Genre** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ed593-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="ed593-155">Dane składa się z nazwy dla rodzaju nowy i opcjonalny opis.</span><span class="sxs-lookup"><span data-stu-id="ed593-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="ed593-156">Jeśli wywołanie AJAX zakończy się pomyślnie, Nowa nazwa genre i wartości są dodawane do znaczników wybierz, a nowe genre ma ustawioną wartość wybranej wartości.</span><span class="sxs-lookup"><span data-stu-id="ed593-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="ed593-157">Ponieważ jest to dynamicznie generowanym znaczników, użytkownik nie widzi nowej opcji wybierz wyświetlając źródła w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ed593-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="ed593-158">Widać nowy HTML przy użyciu narzędzi deweloperskich programu Internet Explorer 9 F12.</span><span class="sxs-lookup"><span data-stu-id="ed593-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="ed593-159">Aby wyświetlić nową opcję Wybierz, w programie Internet Explorer 9, naciśnij klawisz F12, aby uruchomić narzędzia deweloperskie F12.</span><span class="sxs-lookup"><span data-stu-id="ed593-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="ed593-160">Przejdź do tworzenia strony i dodać określonego rodzaju nowy, aby nowe genre jest zaznaczony na liście wybierz genre.</span><span class="sxs-lookup"><span data-stu-id="ed593-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="ed593-161">W narzędziach developer F12:</span><span class="sxs-lookup"><span data-stu-id="ed593-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="ed593-162">Wybierz kartę HTML.</span><span class="sxs-lookup"><span data-stu-id="ed593-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="ed593-163">Kliknij ikonę odświeżania.</span><span class="sxs-lookup"><span data-stu-id="ed593-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="ed593-164">W polu wyszukiwania wprowadź GenreID.</span><span class="sxs-lookup"><span data-stu-id="ed593-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="ed593-165">Korzystając z ikony w dalej</span><span class="sxs-lookup"><span data-stu-id="ed593-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
 <span data-ttu-id="ed593-166">Przejdź do następującego tagu wybierz:</span><span class="sxs-lookup"><span data-stu-id="ed593-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="ed593-167">Rozwiń ostatnią wartość opcji.</span><span class="sxs-lookup"><span data-stu-id="ed593-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="ed593-168">Poniższy kod w *Scripts\chooseGenre.js* pliku przedstawiono **Dodaj nowe Genre** połączeniu Zdarzenie kliknięcia przycisku i jak **Dodaj nowe Genre** jest okno dialogowe utworzony.</span><span class="sxs-lookup"><span data-stu-id="ed593-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="ed593-169">Pierwszy wiersz tworzy funkcję kliknij dołączony do **Dodaj nowe Genre** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ed593-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="ed593-170">Następujący kod z Views\StoreManager\\_ChooseGenre.cshtml pliku pokazuje sposób **Dodaj nowe Genre** utworzeniu przycisk:</span><span class="sxs-lookup"><span data-stu-id="ed593-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="ed593-171">Metoda load tworzy i otwiera okno dialogowe Dodawanie Genre i wywołuje jQuery `parse` dlatego sprawdzanie poprawności klienta jest wykonywane na dane wprowadzane w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="ed593-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="ed593-172">W tej sekcji mają przedstawiono sposób tworzenia okna dialogowego, który może służyć do dodania nowych danych kategorii do listy wyboru.</span><span class="sxs-lookup"><span data-stu-id="ed593-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="ed593-173">Można użyć tej samej procedury, można utworzyć interfejsu użytkownika, aby dodać nowy wykonawcy do listy wyboru wykonawcy.</span><span class="sxs-lookup"><span data-stu-id="ed593-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="ed593-174">W tym samouczku udzielił Omówienie pracy z Pomocnik kodu HTML programu ASP.NET MVC **DropDownList**.</span><span class="sxs-lookup"><span data-stu-id="ed593-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="ed593-175">Aby uzyskać dodatkowe informacje na temat pracy z **DropDownList**, zobacz sekcję odwołań do dodawania poniżej.</span><span class="sxs-lookup"><span data-stu-id="ed593-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="ed593-176">Prosimy o kontakt czy został pomocne w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ed593-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="ed593-177">Rick.Anderson[at]Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ed593-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="ed593-178">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="ed593-178">Additional References</span></span>

- <span data-ttu-id="ed593-179">[ASP.NET MVC — kaskadowych w listy rozwijanej wymieniono samouczek](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) przez [Radu enuca o](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="ed593-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="ed593-180">[Wybrana](http://harvesthq.github.com/chosen/) wtyczkę A JavaScript, która obsługuje wielokrotnego wyboru i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="ed593-180">[Chosen](http://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="ed593-181">Współautorzy</span><span class="sxs-lookup"><span data-stu-id="ed593-181">Contributors</span></span>

- [<span data-ttu-id="ed593-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="ed593-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="ed593-183">Jean Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="ed593-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="ed593-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="ed593-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="ed593-185">Osoby dokonujące przeglądu</span><span class="sxs-lookup"><span data-stu-id="ed593-185">Reviewers</span></span>

- <span data-ttu-id="ed593-186">Jean Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="ed593-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="ed593-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="ed593-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="ed593-188">Jan Pope</span><span class="sxs-lookup"><span data-stu-id="ed593-188">Mike Pope</span></span>
- <span data-ttu-id="ed593-189">Tomasz Dykstra</span><span class="sxs-lookup"><span data-stu-id="ed593-189">Tom Dykstra</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="ed593-190">Poprzednie</span><span class="sxs-lookup"><span data-stu-id="ed593-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)