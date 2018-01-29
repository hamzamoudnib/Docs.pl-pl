
<span data-ttu-id="4057c-101">Omówione zostaną następujące czynności [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) w następnym samouczku.</span><span class="sxs-lookup"><span data-stu-id="4057c-101">We'll cover [DataAnnotations](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) in the next tutorial.</span></span> <span data-ttu-id="4057c-102">[Wyświetlić](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) Określa atrybut, co ma być wyświetlany dla nazwy pola (w tym przypadku "Data wydania" zamiast "ReleaseDate").</span><span class="sxs-lookup"><span data-stu-id="4057c-102">The [Display](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.modelbinding.metadata.displaymetadata) attribute specifies what to display for the name of a field (in this case "Release Date" instead of "ReleaseDate").</span></span> <span data-ttu-id="4057c-103">[DataType](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) atrybut określa typ danych (Data), co nie jest wyświetlane w polu informacje o godzinie.</span><span class="sxs-lookup"><span data-stu-id="4057c-103">The [DataType](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date), so the time information stored in the field isn't displayed.</span></span>

<span data-ttu-id="4057c-104">Przejdź do `Movies` kontrolera i umieść wskaźnik myszy nad **Edytuj** łącze, aby wyświetlić docelowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="4057c-104">Browse to the `Movies` controller and hold the mouse pointer over an **Edit** link to see the target URL.</span></span>

![Okna przeglądarki z myszą łącza edycji i link jest wyświetlany adres Url http://localhost:1234/filmów/Edit/5](../../tutorials/first-mvc-app/controller-methods-views/_static/edit7.png)

<span data-ttu-id="4057c-106">**Edytuj**, **szczegóły**, i **usunąć** łącza są generowane przez pomocnika Tag kotwicy MVC Core w *Views/Movies/Index.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="4057c-106">The **Edit**, **Details**, and **Delete** links are generated by the Core MVC Anchor Tag Helper in the *Views/Movies/Index.cshtml* file.</span></span>

[!code-HTML[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/IndexOriginal.cshtml?highlight=1-3&range=46-50)]

<span data-ttu-id="4057c-107">[Pomocnicy tagów](xref:mvc/views/tag-helpers/intro) umożliwiają uczestniczenie kodu po stronie serwera w tworzeniu i renderowaniu elementów HTML w plikach Razor.</span><span class="sxs-lookup"><span data-stu-id="4057c-107">[Tag Helpers](xref:mvc/views/tag-helpers/intro) enable server-side code to participate in creating and rendering HTML elements in Razor files.</span></span> <span data-ttu-id="4057c-108">W powyższym kodzie `AnchorTagHelper` dynamicznie generuje kod HTML `href` wartość atrybutu z identyfikator metody i tras akcji kontrolera. Możesz użyć **Wyświetl źródło** z ulubionych przeglądarki lub użyj narzędzia dla deweloperów do sprawdzenia wygenerowanego kodu znaczników.</span><span class="sxs-lookup"><span data-stu-id="4057c-108">In the code above, the `AnchorTagHelper` dynamically generates the HTML `href` attribute value from the controller action method and route id. You use **View Source** from your favorite browser or use the developer tools to examine the generated markup.</span></span> <span data-ttu-id="4057c-109">Poniżej przedstawiono fragment wygenerowanego kodu HTML:</span><span class="sxs-lookup"><span data-stu-id="4057c-109">A portion of the generated HTML is shown below:</span></span>

```html
 <td>
    <a href="/Movies/Edit/4"> Edit </a> |
    <a href="/Movies/Details/4"> Details </a> |
    <a href="/Movies/Delete/4"> Delete </a>
</td>
```

<span data-ttu-id="4057c-110">Odwołaj format [routingu](xref:mvc/controllers/routing) w *Startup.cs* pliku:</span><span class="sxs-lookup"><span data-stu-id="4057c-110">Recall the format for [routing](xref:mvc/controllers/routing) set in the *Startup.cs* file:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=snippet_1&highlight=5)]

<span data-ttu-id="4057c-111">Tłumaczy platformy ASP.NET Core `http://localhost:1234/Movies/Edit/4` na żądanie, aby `Edit` metody akcji `Movies` kontrolera z parametrem `Id` 4.</span><span class="sxs-lookup"><span data-stu-id="4057c-111">ASP.NET Core translates `http://localhost:1234/Movies/Edit/4` into a request to the `Edit` action method of the `Movies` controller with the parameter `Id` of 4.</span></span> <span data-ttu-id="4057c-112">(Metod kontrolera są również znane jako metody akcji).</span><span class="sxs-lookup"><span data-stu-id="4057c-112">(Controller methods are also known as action methods.)</span></span>

<span data-ttu-id="4057c-113">[Pomocników tagów](xref:mvc/views/tag-helpers/intro) są jednym z najpopularniejszych nowe funkcje programu ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4057c-113">[Tag Helpers](xref:mvc/views/tag-helpers/intro) are one of the most popular new features in ASP.NET Core.</span></span> <span data-ttu-id="4057c-114">Zobacz [dodatkowe zasoby](#additional-resources) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4057c-114">See [Additional resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="4057c-115">Otwórz `Movies` kontrolera i sprawdź, czy dwa `Edit` metody akcji.</span><span class="sxs-lookup"><span data-stu-id="4057c-115">Open the `Movies` controller and examine the two `Edit` action methods.</span></span> <span data-ttu-id="4057c-116">Poniższy kod przedstawia `HTTP GET Edit` metodę, która pobiera filmu i wypełnienie formularza edycji generowane przez *Edit.cshtml* pliku Razor.</span><span class="sxs-lookup"><span data-stu-id="4057c-116">The following code shows the `HTTP GET Edit` method, which fetches the movie and populates the edit form generated by the *Edit.cshtml* Razor file.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MC1.cs?name=snippet_edit1)]

<span data-ttu-id="4057c-117">Poniższy kod przedstawia `HTTP POST Edit` metodę, która przetwarza wartości oczekujących na opublikowanie film:</span><span class="sxs-lookup"><span data-stu-id="4057c-117">The following code shows the `HTTP POST Edit` method, which processes the posted movie values:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MC1.cs?name=snippet_edit2)]

<span data-ttu-id="4057c-118">`[Bind]` Atrybut jest jednym ze sposobów ochrony przed [zbyt księgowej](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost).</span><span class="sxs-lookup"><span data-stu-id="4057c-118">The `[Bind]` attribute is one way to protect against [over-posting](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost).</span></span> <span data-ttu-id="4057c-119">Powinna zawierać tylko właściwości w `[Bind]` atrybut, który chcesz zmienić.</span><span class="sxs-lookup"><span data-stu-id="4057c-119">You should only include properties in the `[Bind]` attribute that you want to change.</span></span> <span data-ttu-id="4057c-120">Zobacz [chronić kontroler z nadmiernego publikowanie](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4057c-120">See [Protect your controller from over-posting](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application) for more information.</span></span> <span data-ttu-id="4057c-121">[ViewModels](http://rachelappel.com/use-viewmodels-to-manage-data-amp-organize-code-in-asp-net-mvc-applications/) zapewnić alternatywne podejście, aby uniknąć nadmiernego publikowanie.</span><span class="sxs-lookup"><span data-stu-id="4057c-121">[ViewModels](http://rachelappel.com/use-viewmodels-to-manage-data-amp-organize-code-in-asp-net-mvc-applications/) provide an alternative approach to prevent over-posting.</span></span>

<span data-ttu-id="4057c-122">Zwróć uwagę, drugi `Edit` metody akcji jest poprzedzony `[HttpPost]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="4057c-122">Notice the second `Edit` action method is preceded by the `[HttpPost]` attribute.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MC1.cs?name=snippet_edit2&highlight=4)]

<span data-ttu-id="4057c-123">`HttpPost` Atrybut określa, że to `Edit` można wywołać metody *tylko* dla `POST` żądań.</span><span class="sxs-lookup"><span data-stu-id="4057c-123">The `HttpPost` attribute specifies that this `Edit` method can be invoked *only* for `POST` requests.</span></span> <span data-ttu-id="4057c-124">Można zastosować `[HttpGet]` pierwszy dla atrybutu Edytuj metodę, ale nie jest to niezbędne ponieważ `[HttpGet]` jest ustawieniem domyślnym.</span><span class="sxs-lookup"><span data-stu-id="4057c-124">You could apply the `[HttpGet]` attribute to the first edit method, but that's not necessary because `[HttpGet]` is the default.</span></span>

<span data-ttu-id="4057c-125">`ValidateAntiForgeryToken` Atrybutów jest używane do [zapobiegania fałszowaniu żądania](xref:security/anti-request-forgery) i wraz z tokenu zabezpieczającego przed sfałszowaniem wygenerowany w pliku widok edycji (*Views/Movies/Edit.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="4057c-125">The `ValidateAntiForgeryToken` attribute is used to [prevent forgery of a request](xref:security/anti-request-forgery) and is paired up with an anti-forgery token generated in the edit view file (*Views/Movies/Edit.cshtml*).</span></span> <span data-ttu-id="4057c-126">Edytuj plik widoku generuje token zabezpieczający przed sfałszowaniem z [pomocnika Tag formularza](xref:mvc/views/working-with-forms).</span><span class="sxs-lookup"><span data-stu-id="4057c-126">The edit view file generates the anti-forgery token with the [Form Tag Helper](xref:mvc/views/working-with-forms).</span></span>

[!code-HTML[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/Edit.cshtml?range=9)]

<span data-ttu-id="4057c-127">[Pomocnika Tag formularza](xref:mvc/views/working-with-forms) generuje token zabezpieczający przed sfałszowaniem ukryte, który musi być zgodna `[ValidateAntiForgeryToken]` wygenerowany token zabezpieczający przed sfałszowaniem w `Edit` filmy kontrolera.</span><span class="sxs-lookup"><span data-stu-id="4057c-127">The [Form Tag Helper](xref:mvc/views/working-with-forms) generates a hidden anti-forgery token that must match the `[ValidateAntiForgeryToken]` generated anti-forgery token in the `Edit` method of the Movies controller.</span></span> <span data-ttu-id="4057c-128">Aby uzyskać więcej informacji, zobacz [żądania przed sfałszowaniem](xref:security/anti-request-forgery).</span><span class="sxs-lookup"><span data-stu-id="4057c-128">For more information, see [Anti-Request Forgery](xref:security/anti-request-forgery).</span></span>

<span data-ttu-id="4057c-129">`HttpGet Edit` Metoda przyjmuje filmu `ID` parametru wyszukuje filmu przy użyciu programu Entity Framework `SingleOrDefaultAsync` metody i zwraca wybrany film do widoku edycji.</span><span class="sxs-lookup"><span data-stu-id="4057c-129">The `HttpGet Edit` method takes the movie `ID` parameter, looks up the movie using the Entity Framework `SingleOrDefaultAsync` method, and returns the selected movie to the Edit view.</span></span> <span data-ttu-id="4057c-130">Jeśli nie można odnaleźć film, `NotFound` (HTTP 404) jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="4057c-130">If a movie cannot be found, `NotFound` (HTTP 404) is returned.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MC1.cs?name=snippet_edit1)]

<span data-ttu-id="4057c-131">Podczas tworzenia widoku edycji systemu szkieletów zbadane `Movie` klasy i kodu do renderowania `<label>` i `<input>` elementy dla każdej właściwości klasy.</span><span class="sxs-lookup"><span data-stu-id="4057c-131">When the scaffolding system created the Edit view, it examined the `Movie` class and created code to render `<label>` and `<input>` elements for each property of the class.</span></span> <span data-ttu-id="4057c-132">W poniższym przykładzie pokazano widok edycji został wygenerowany przez system szkieletów Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4057c-132">The following example shows the Edit view that was generated by the Visual Studio scaffolding system:</span></span>

[!code-HTML[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Movies/EditCopy.cshtml?highlight=1)]

<span data-ttu-id="4057c-133">Zwróć uwagę, jak szablon widoku ma `@model MvcMovie.Models.Movie` instrukcji w górnej części pliku.</span><span class="sxs-lookup"><span data-stu-id="4057c-133">Notice how the view template has a `@model MvcMovie.Models.Movie` statement at the top of the file.</span></span> <span data-ttu-id="4057c-134">`@model MvcMovie.Models.Movie`Określa, czy widok oczekuje modelu widoku szablonu typu `Movie`.</span><span class="sxs-lookup"><span data-stu-id="4057c-134">`@model MvcMovie.Models.Movie` specifies that the view expects the model for the view template to be of type `Movie`.</span></span>

<span data-ttu-id="4057c-135">Kod z utworzonym szkieletem korzysta kilka metod pomocnika tagów usprawnić kod znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="4057c-135">The scaffolded code uses several Tag Helper methods to streamline the HTML markup.</span></span> <span data-ttu-id="4057c-136">[Pomocnika tagów etykiety](xref:mvc/views/working-with-forms) Wyświetla nazwę pola ("Title", "ReleaseDate", "Rodzaju" lub "Price").</span><span class="sxs-lookup"><span data-stu-id="4057c-136">The - [Label Tag Helper](xref:mvc/views/working-with-forms) displays the name of the field ("Title", "ReleaseDate", "Genre", or "Price").</span></span> <span data-ttu-id="4057c-137">[Pomocnika Tag danych wejściowych](xref:mvc/views/working-with-forms) renderowania kodu HTML `<input>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4057c-137">The [Input Tag Helper](xref:mvc/views/working-with-forms) renders an HTML `<input>` element.</span></span> <span data-ttu-id="4057c-138">[Pomocnika tagów weryfikacji](xref:mvc/views/working-with-forms) wyświetla komunikaty weryfikacji skojarzony z tą właściwością.</span><span class="sxs-lookup"><span data-stu-id="4057c-138">The [Validation Tag Helper](xref:mvc/views/working-with-forms) displays any validation messages associated with that property.</span></span>

<span data-ttu-id="4057c-139">Uruchom aplikację i przejdź do `/Movies` adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4057c-139">Run the application and navigate to the `/Movies` URL.</span></span> <span data-ttu-id="4057c-140">Kliknij przycisk **Edytuj** łącza.</span><span class="sxs-lookup"><span data-stu-id="4057c-140">Click an **Edit** link.</span></span> <span data-ttu-id="4057c-141">W przeglądarce Wyświetl źródło strony.</span><span class="sxs-lookup"><span data-stu-id="4057c-141">In the browser, view the source for the page.</span></span> <span data-ttu-id="4057c-142">Wygenerowany kod HTML pod kątem `<form>` elementu są wyświetlane poniżej.</span><span class="sxs-lookup"><span data-stu-id="4057c-142">The generated HTML for the `<form>` element is shown below.</span></span>

[!code-HTML[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Views/Shared/edit_view_source.html?highlight=1,6,10,17,24,28)]

<span data-ttu-id="4057c-143">`<input>` Elementy znajdują się w `HTML <form>` element których `action` ustawiono atrybut do wysłania do `/Movies/Edit/id` adresu URL.</span><span class="sxs-lookup"><span data-stu-id="4057c-143">The `<input>` elements are in an `HTML <form>` element whose `action` attribute is set to post to the `/Movies/Edit/id` URL.</span></span> <span data-ttu-id="4057c-144">Dane formularza zostaną opublikowane na serwerze po `Save` kliknięciu przycisku.</span><span class="sxs-lookup"><span data-stu-id="4057c-144">The form data will be posted to the server when the `Save` button is clicked.</span></span> <span data-ttu-id="4057c-145">Ostatni wiersz przed tagiem zamykającym `</form>` element zawiera ukrytego [XSRF](xref:security/anti-request-forgery) token generowane przez [pomocnika Tag formularza](xref:mvc/views/working-with-forms).</span><span class="sxs-lookup"><span data-stu-id="4057c-145">The last line before the closing `</form>` element shows the hidden [XSRF](xref:security/anti-request-forgery) token generated by the [Form Tag Helper](xref:mvc/views/working-with-forms).</span></span>

## <a name="processing-the-post-request"></a><span data-ttu-id="4057c-146">Przetwarzanie żądania POST</span><span class="sxs-lookup"><span data-stu-id="4057c-146">Processing the POST Request</span></span>

<span data-ttu-id="4057c-147">Poniżej przedstawiono listę `[HttpPost]` wersji `Edit` metody akcji.</span><span class="sxs-lookup"><span data-stu-id="4057c-147">The following listing shows the `[HttpPost]` version of the `Edit` action method.</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Controllers/MC1.cs?name=snippet_edit2)]

<span data-ttu-id="4057c-148">`[ValidateAntiForgeryToken]` Weryfikuje ukrytego atrybutu [XSRF](xref:security/anti-request-forgery) token wygenerowana przez generator token zabezpieczający przed sfałszowaniem w [pomocnika Tag formularza](xref:mvc/views/working-with-forms)</span><span class="sxs-lookup"><span data-stu-id="4057c-148">The `[ValidateAntiForgeryToken]` attribute validates the hidden [XSRF](xref:security/anti-request-forgery) token generated by the anti-forgery token generator in the [Form Tag Helper](xref:mvc/views/working-with-forms)</span></span>

<span data-ttu-id="4057c-149">[Modelu powiązania](xref:mvc/models/model-binding) systemu przyjmuje wartości przesłanego formularza i tworzy `Movie` obiekt, który jest przekazywany jako `movie` parametru.</span><span class="sxs-lookup"><span data-stu-id="4057c-149">The [model binding](xref:mvc/models/model-binding) system takes the posted form values and creates a `Movie` object that's passed as the `movie` parameter.</span></span> <span data-ttu-id="4057c-150">`ModelState.IsValid` Metoda sprawdza, czy dane dostarczone w formie może służyć do modyfikowania (edycji lub aktualizacji) `Movie` obiektu.</span><span class="sxs-lookup"><span data-stu-id="4057c-150">The `ModelState.IsValid` method verifies that the data submitted in the form can be used to modify (edit or update) a `Movie` object.</span></span> <span data-ttu-id="4057c-151">Jeśli dane są prawidłowe są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="4057c-151">If the data is valid it's saved.</span></span> <span data-ttu-id="4057c-152">Dane zaktualizowane movie (edytowanych) są zapisywane w bazie danych przez wywołanie metody `SaveChangesAsync` metody kontekst bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4057c-152">The updated (edited) movie data is saved to the database by calling the `SaveChangesAsync` method of database context.</span></span> <span data-ttu-id="4057c-153">Po zapisaniu danych, kod przekierowuje użytkownika do `Index` metody akcji `MoviesController` klasy, która wyświetla kolekcję film, w tym tylko zmiany.</span><span class="sxs-lookup"><span data-stu-id="4057c-153">After saving the data, the code redirects the user to the `Index` action method of the `MoviesController` class, which displays the movie collection, including the changes just made.</span></span>

<span data-ttu-id="4057c-154">Przed opublikowania formularza do serwera, weryfikacji po stronie klienta sprawdza reguł sprawdzania poprawności w polach.</span><span class="sxs-lookup"><span data-stu-id="4057c-154">Before the form is posted to the server, client side validation checks any validation rules on the fields.</span></span> <span data-ttu-id="4057c-155">Jeśli wystąpią jakieś błędy sprawdzania poprawności, zostanie wyświetlony komunikat o błędzie i formularz nie jest opublikowane.</span><span class="sxs-lookup"><span data-stu-id="4057c-155">If there are any validation errors, an error message is displayed and the form isn't posted.</span></span> <span data-ttu-id="4057c-156">Jeśli JavaScript jest wyłączona, nie będziesz mieć weryfikacji po stronie klienta, ale serwer wykryje opublikowanych wartości, które nie są prawidłowe, a wartości formularza zostanie wyświetlony ponownie, z komunikatów o błędach.</span><span class="sxs-lookup"><span data-stu-id="4057c-156">If JavaScript is disabled, you won't have client side validation but the server will detect the posted values that are not valid, and the form values will be redisplayed with error messages.</span></span> <span data-ttu-id="4057c-157">Później w samouczku omówione [sprawdzania poprawności modelu](xref:mvc/models/validation) bardziej szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="4057c-157">Later in the tutorial we examine [Model Validation](xref:mvc/models/validation) in more detail.</span></span> <span data-ttu-id="4057c-158">[Pomocnika tagów weryfikacji](xref:mvc/views/working-with-forms) w *Views/Movies/Edit.cshtml* widok szablonu zajmuje się wyświetlanie odpowiednie komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="4057c-158">The [Validation Tag Helper](xref:mvc/views/working-with-forms) in the *Views/Movies/Edit.cshtml* view template takes care of displaying appropriate error messages.</span></span>

![Edytowanie widoku: wyjątek niepoprawną wartość ceny ABC określają, czy pole Cena musi być liczbą.](../../tutorials/first-mvc-app/controller-methods-views/_static/val.png)

<span data-ttu-id="4057c-161">Wszystkie `HttpGet` metod w kontrolerze filmu wykonaj podobnego wzorca.</span><span class="sxs-lookup"><span data-stu-id="4057c-161">All the `HttpGet` methods in the movie controller follow a similar pattern.</span></span> <span data-ttu-id="4057c-162">Otrzymują obiektu movie (lub listę obiektów, w przypadku `Index`) oraz przekazania obiektu (model) do widoku.</span><span class="sxs-lookup"><span data-stu-id="4057c-162">They get a movie object (or list of objects, in the case of `Index`), and pass the object (model) to the view.</span></span> <span data-ttu-id="4057c-163">`Create` Metoda przekazuje obiekt pusty film, aby `Create` widoku.</span><span class="sxs-lookup"><span data-stu-id="4057c-163">The `Create` method passes an empty movie object to the `Create` view.</span></span> <span data-ttu-id="4057c-164">Wszystkie metody, które tworzenia, edytowania, usuwania lub modyfikację danych należy więc w `[HttpPost]` przeciążenia metody.</span><span class="sxs-lookup"><span data-stu-id="4057c-164">All the methods that create, edit, delete, or otherwise modify data do so in the `[HttpPost]` overload of the method.</span></span> <span data-ttu-id="4057c-165">Modyfikowanie danych w `HTTP GET` metody stanowi zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="4057c-165">Modifying data in an `HTTP GET` method is a security risk.</span></span> <span data-ttu-id="4057c-166">Modyfikowanie danych w `HTTP GET` metody również narusza HTTP najlepszych rozwiązań i architektury [REST](http://rest.elkstein.org/) wzorca, który określa, że żądania GET nie należy zmienić stan aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4057c-166">Modifying data in an `HTTP GET` method also violates HTTP best practices and the architectural [REST](http://rest.elkstein.org/) pattern, which specifies that GET requests shouldn't change the state of your application.</span></span> <span data-ttu-id="4057c-167">Innymi słowy wykonanie operacji GET powinny być bezpieczne operację, która nie ma skutków ubocznych i nie modyfikuje danych trwałych.</span><span class="sxs-lookup"><span data-stu-id="4057c-167">In other words, performing a GET operation should be a safe operation that has no side effects and doesn't modify your persisted data.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4057c-168">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4057c-168">Additional resources</span></span>

* [<span data-ttu-id="4057c-169">Globalizacja i lokalizacja</span><span class="sxs-lookup"><span data-stu-id="4057c-169">Globalization and localization</span></span>](xref:fundamentals/localization)
* [<span data-ttu-id="4057c-170">Wprowadzenie do pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="4057c-170">Introduction to Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="4057c-171">Tworzenie pomocników tagów</span><span class="sxs-lookup"><span data-stu-id="4057c-171">Authoring Tag Helpers</span></span>](xref:mvc/views/tag-helpers/authoring)
* [<span data-ttu-id="4057c-172">Ochrona przed fałszerstwem żądań</span><span class="sxs-lookup"><span data-stu-id="4057c-172">Anti-Request Forgery</span></span>](xref:security/anti-request-forgery)
* <span data-ttu-id="4057c-173">Ochrona kontroler z [zbyt księgowej](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application)</span><span class="sxs-lookup"><span data-stu-id="4057c-173">Protect your controller from [over-posting](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application)</span></span>
* [<span data-ttu-id="4057c-174">ViewModels</span><span class="sxs-lookup"><span data-stu-id="4057c-174">ViewModels</span></span>](http://rachelappel.com/use-viewmodels-to-manage-data-amp-organize-code-in-asp-net-mvc-applications/)
* [<span data-ttu-id="4057c-175">Pomocnik Tag formularza</span><span class="sxs-lookup"><span data-stu-id="4057c-175">Form Tag Helper</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="4057c-176">Pomocnik tagu wejściowego</span><span class="sxs-lookup"><span data-stu-id="4057c-176">Input Tag Helper</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="4057c-177">Etykieta pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="4057c-177">Label Tag Helper</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="4057c-178">Wybierz pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="4057c-178">Select Tag Helper</span></span>](xref:mvc/views/working-with-forms)
* [<span data-ttu-id="4057c-179">Sprawdzanie poprawności pomocnika tagów</span><span class="sxs-lookup"><span data-stu-id="4057c-179">Validation Tag Helper</span></span>](xref:mvc/views/working-with-forms)