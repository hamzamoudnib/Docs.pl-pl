---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Edytowanie kodu formularzy sieci Web ASP.NET w programie Visual Studio 2013 | Dokumentacja firmy Microsoft
author: Erikre
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/03/2014
ms.topic: article
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 8714f673cb0434189ca23d2dda14035d8652a051
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a><span data-ttu-id="13442-102">Kod edycji ASP.NET Web Forms w programie Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="13442-102">Code Editing ASP.NET Web Forms in Visual Studio 2013</span></span>
====================
<span data-ttu-id="13442-103">Przez [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="13442-103">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="13442-104">Na wielu stronach formularza sieci Web ASP.NET pisania kodu w języku Visual Basic, C# lub innego języka.</span><span class="sxs-lookup"><span data-stu-id="13442-104">In many ASP.NET Web Form pages, you write code in Visual Basic, C#, or another language.</span></span> <span data-ttu-id="13442-105">Edytor kodu w programie Visual Studio może pomóc szybko napisać kod jednocześnie pomaga uniknąć błędów.</span><span class="sxs-lookup"><span data-stu-id="13442-105">The code editor in Visual Studio can help you write code quickly while helping you avoid errors.</span></span> <span data-ttu-id="13442-106">Ponadto Edytor umożliwia sposoby tworzenia kodu wielokrotnego użytku pomagają zmniejszyć ilość pracy, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="13442-106">In addition, the editor provides ways for you to create reusable code to help reduce the amount of work you need to do.</span></span>

<span data-ttu-id="13442-107">W tym przewodniku przedstawiono różne funkcje edytora kodu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13442-107">This walkthrough illustrates various features of the Visual Studio code editor.</span></span>

<span data-ttu-id="13442-108">W tym przewodniku przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="13442-108">During this walkthrough, you will learn how to:</span></span>

- <span data-ttu-id="13442-109">Popraw błędy kodowania w tekście.</span><span class="sxs-lookup"><span data-stu-id="13442-109">Correct inline coding errors.</span></span>
- <span data-ttu-id="13442-110">Refaktoryzuj i Zmień nazwę kodu.</span><span class="sxs-lookup"><span data-stu-id="13442-110">Refactor and rename code.</span></span>
- <span data-ttu-id="13442-111">Zmiana nazwy zmiennych i obiektów.</span><span class="sxs-lookup"><span data-stu-id="13442-111">Rename variables and objects.</span></span>
- <span data-ttu-id="13442-112">Wstawianie wstawek kodu.</span><span class="sxs-lookup"><span data-stu-id="13442-112">Insert code snippets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13442-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13442-113">Prerequisites</span></span>


<span data-ttu-id="13442-114">W celu przeprowadzenia tego instruktażu potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="13442-114">In order to complete this walkthrough, you will need:</span></span>

- <span data-ttu-id="13442-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) lub [programu Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span><span class="sxs-lookup"><span data-stu-id="13442-115">[Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) or [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span> <span data-ttu-id="13442-116">.NET Framework jest instalowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="13442-116">The .NET Framework is installed automatically.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="13442-117">Microsoft Visual Studio 2013 i programu Microsoft Visual Studio Express 2013 for Web będzie często określane jako Visual Studio w tej serii samouczka.</span><span class="sxs-lookup"><span data-stu-id="13442-117">Microsoft Visual Studio 2013 and Microsoft Visual Studio Express 2013 for Web will often be referred to as Visual Studio throughout this tutorial series.</span></span>  
    >   
    > <span data-ttu-id="13442-118">Jeśli używasz programu Visual Studio w tym przewodniku przyjęto założenie, że wybrano **projektowanie witryn sieci Web** kolekcję ustawień przy pierwszym uruchomieniu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13442-118">If you are using Visual Studio, this walkthrough assumes that you selected the **Web Development** collection of settings the first time that you started Visual Studio.</span></span> <span data-ttu-id="13442-119">Aby uzyskać więcej informacji, zobacz [porady: Wybierz ustawienia środowiska sieci Web Development](https://msdn.microsoft.com/library/ff521558.aspx).</span><span class="sxs-lookup"><span data-stu-id="13442-119">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

 <span data-ttu-id="13442-120">Aby obejrzeć wprowadzenie do platformy ASP.NET i Visual Studio, zobacz [tworzenia podstawowego strony formularzy sieci Web programu ASP.NET 4.5 w programie Visual Studio 2013](creating-a-basic-web-forms-page.md).</span><span class="sxs-lookup"><span data-stu-id="13442-120">For an introduction to Visual Studio and ASP.NET, see [Creating a basic ASP.NET 4.5 Web Forms page in Visual Studio 2013](creating-a-basic-web-forms-page.md).</span></span>   
 

## <a name="creating-a-web-application-project-and-a-page"></a><span data-ttu-id="13442-121">Tworzenie projektu aplikacji sieci Web i strony</span><span class="sxs-lookup"><span data-stu-id="13442-121">Creating a Web application project and a Page</span></span>

<a id="sectionToggle0"></a>

<span data-ttu-id="13442-122">W tej części przewodnika utworzysz projekt aplikacji sieci Web i Dodaj nową stronę do niego.</span><span class="sxs-lookup"><span data-stu-id="13442-122">In this part of the walkthrough, you will create a Web application project and add a new page to it.</span></span>

### <a name="to-create-a-web-application-project"></a><span data-ttu-id="13442-123">Aby utworzyć projekt aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="13442-123">To create a Web application project</span></span>

1. <span data-ttu-id="13442-124">Otwórz program Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13442-124">Open Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="13442-125">Na **pliku** menu, wybierz opcję **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="13442-125">On the **File** menu, select **New Project**.</span></span>  
    <span data-ttu-id="13442-126">![Menu Plik](code-editing-in-web-forms-pages/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="13442-126">![File Menu](code-editing-in-web-forms-pages/_static/image1.png)</span></span>

    <span data-ttu-id="13442-127">**Nowy projekt** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13442-127">The **New Project** dialog box appears.</span></span>
3. <span data-ttu-id="13442-128">Wybierz **szablony**  - &gt; **Visual C#**  - &gt; **Web** grupy szablonów po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="13442-128">Select the **Templates** -&gt; **Visual C#** -&gt; **Web** templates group on the left.</span></span>
4. <span data-ttu-id="13442-129">Wybierz **aplikacji sieci Web ASP.NET** szablonu w środkowej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="13442-129">Choose the **ASP.NET Web Application** template in the center column.</span></span>
5. <span data-ttu-id="13442-130">Nazwij swój projekt ***BasicWebApp*** i kliknij przycisk **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="13442-130">Name your project ***BasicWebApp*** and click the **OK** button.</span></span>   
<span data-ttu-id="13442-131">![Okno dialogowe Nowy projekt](code-editing-in-web-forms-pages/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="13442-131">![New Project dialog box](code-editing-in-web-forms-pages/_static/image2.png)</span></span>
6. <span data-ttu-id="13442-132">Następnie wybierz pozycję **formularzy sieci Web** szablon i kliknij przycisk **OK** przycisk, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="13442-132">Next, select the **Web Forms** template and click the **OK** button to create the project.</span></span>  
<span data-ttu-id="13442-133">![Okno dialogowe Nowy projekt ASP.NET](code-editing-in-web-forms-pages/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="13442-133">![New ASP.NET Project dialog box](code-editing-in-web-forms-pages/_static/image3.png)</span></span>  

    <span data-ttu-id="13442-134">Program Visual Studio tworzy nowy projekt, który zawiera wbudowane funkcje, oparty na szablonie formularzy sieci Web.</span><span class="sxs-lookup"><span data-stu-id="13442-134">Visual Studio creates a new project that includes prebuilt functionality based on the Web Forms template.</span></span>


## <a name="creating-a-new-aspnet-web-forms-page"></a><span data-ttu-id="13442-135">Tworzenie nowej strony formularzy sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="13442-135">Creating a new ASP.NET Web Forms Page</span></span>


<span data-ttu-id="13442-136">Podczas tworzenia nowej aplikacji formularzy sieci Web, przy użyciu **aplikacji sieci Web ASP.NET** szablon projektu Visual Studio dodaje strony ASP.NET (strony formularzy sieci Web), o nazwie *Default.aspx*oraz jak kilka innych plików i foldery.</span><span class="sxs-lookup"><span data-stu-id="13442-136">When you create a new Web Forms application using the **ASP.NET Web Application** project template, Visual Studio adds an ASP.NET page (Web Forms page) named *Default.aspx*, as well as several other files and folders.</span></span> <span data-ttu-id="13442-137">Można użyć *Default.aspx* strony jako stronę główną dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="13442-137">You can use the *Default.aspx* page as the home page for your Web application.</span></span> <span data-ttu-id="13442-138">Jednak w ramach tego przewodnika, utworzysz i pracować z nowej strony.</span><span class="sxs-lookup"><span data-stu-id="13442-138">However, for this walkthrough, you will create and work with a new page.</span></span>

### <a name="to-add-a-page-to-the-web-application"></a><span data-ttu-id="13442-139">Aby dodać stronę do aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="13442-139">To add a page to the Web application</span></span>


1. <span data-ttu-id="13442-140">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nazwę aplikacji sieci Web (w tym samouczku, nazwa aplikacji jest **BasicWebSite**), a następnie kliknij przycisk **Dodaj**  - &gt; **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="13442-140">In **Solution Explorer**, right-click the Web application name (in this tutorial the application name is **BasicWebSite**), and then click **Add** -&gt; **New Item**.</span></span>   
<span data-ttu-id="13442-141">**Dodaj nowy element** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13442-141">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="13442-142">Wybierz **Visual C#**  - &gt; **Web** grupy szablonów po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="13442-142">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="13442-143">Następnie wybierz opcję **formularza sieci Web** ze środka listy i nadaj mu nazwę *FirstWebPage.aspx*.</span><span class="sxs-lookup"><span data-stu-id="13442-143">Then, select **Web Form** from the middle list and name it *FirstWebPage.aspx*.</span></span>   
    <span data-ttu-id="13442-144">![Dodaj nowy element — okno dialogowe](code-editing-in-web-forms-pages/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="13442-144">![Add New Item dialog box](code-editing-in-web-forms-pages/_static/image4.png)</span></span>
3. <span data-ttu-id="13442-145">Kliknij przycisk **Dodaj** można dodać strony formularzy sieci Web do projektu.</span><span class="sxs-lookup"><span data-stu-id="13442-145">Click **Add** to add the Web Forms page to your project.</span></span>  
 <span data-ttu-id="13442-146">Visual Studio utworzy nową stronę i otwarcie go.</span><span class="sxs-lookup"><span data-stu-id="13442-146">Visual Studio creates the new page and opens it.</span></span>
4. <span data-ttu-id="13442-147">Następnie ustaw nowej strony jako stronę startową domyślne.</span><span class="sxs-lookup"><span data-stu-id="13442-147">Next, set this new page as the default startup page.</span></span> <span data-ttu-id="13442-148">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nową stronę o nazwie *FirstWebPage.aspx* i wybierz **Ustaw jako stronę startową**.</span><span class="sxs-lookup"><span data-stu-id="13442-148">In **Solution Explorer**, right-click the new page named *FirstWebPage.aspx* and select **Set As Start Page**.</span></span> <span data-ttu-id="13442-149">Podczas następnego uruchomienia tej aplikacji do naszej postęp testu zostaną automatycznie wyświetlone tym nową stronę w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="13442-149">The next time you run this application to test our progress, you will automatically see this new page in the browser.</span></span>


## <a name="correcting-inline-coding-errors"></a><span data-ttu-id="13442-150">Korygowanie wbudowanego błędy kodowania</span><span class="sxs-lookup"><span data-stu-id="13442-150">Correcting Inline Coding Errors</span></span>


<span data-ttu-id="13442-151">Edytor kodu w programie Visual Studio pomaga uniknąć błędów, jak napisać kod, a jeśli wprowadzono Błąd edytora kodu pomaga poprawić ten błąd.</span><span class="sxs-lookup"><span data-stu-id="13442-151">The code editor in Visual Studio helps you to avoid errors as you write code, and if you have made an error, the code editor helps you to correct the error.</span></span> <span data-ttu-id="13442-152">W tej części przewodnika zapisze wiersz kodu zilustrowanie funkcji korekcji błędów w edytorze.</span><span class="sxs-lookup"><span data-stu-id="13442-152">In this part of the walkthrough, you will write a line of code that illustrate the error correction features in the editor.</span></span>

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a><span data-ttu-id="13442-153">Aby poprawić błędy kodowania proste w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13442-153">To correct simple coding errors in Visual Studio</span></span>


1. <span data-ttu-id="13442-154">W **projekt** wyświetlić, kliknij dwukrotnie pustej strony, aby utworzyć program obsługi **obciążenia** zdarzenia dla strony.</span><span class="sxs-lookup"><span data-stu-id="13442-154">In **Design** view, double-click the blank page to create a handler for the **Load** event for the page.</span></span>   
<span data-ttu-id="13442-155">Używasz programu obsługi zdarzeń tylko jako miejsce do pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="13442-155">You are using the event handler only as a place to write some code.</span></span>
2. <span data-ttu-id="13442-156">Wewnątrz obsługi, wpisz następujące polecenie, która zawiera błąd i naciśnij klawisz **ENTER**:</span><span class="sxs-lookup"><span data-stu-id="13442-156">Inside the handler, type the following line that contains an error and press **ENTER**:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

 <span data-ttu-id="13442-157">Po naciśnięciu **ENTER**, edytora kodu umieszcza zielonego i czerwonego podkreślenia (często wywołać &quot;dowolnym kształcie&quot; wierszy) w obszarach kodu, które mają problemy.</span><span class="sxs-lookup"><span data-stu-id="13442-157">When you press **ENTER**, the code editor places green and red underlines (commonly call &quot;squiggly&quot; lines) under areas of the code that have issues.</span></span> <span data-ttu-id="13442-158">Zielony podkreślenie wskazuje ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="13442-158">A green underline indicates a warning.</span></span> <span data-ttu-id="13442-159">Czerwone podkreślenie wskazuje błąd, który należy naprawić.</span><span class="sxs-lookup"><span data-stu-id="13442-159">A red underline indicates an error that you must fix.</span></span> 

    <span data-ttu-id="13442-160">Umieść kursor `myStr` Aby wyświetlić etykietkę narzędzia, który informuje o ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="13442-160">Hold the mouse pointer over `myStr` to see a tooltip that tells you about the warning.</span></span> <span data-ttu-id="13442-161">Ponadto wskaźnik myszy nad czerwonym podkreśleniem, aby wyświetlić komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="13442-161">Also, hold your mouse pointer over the red underline to see the error message.</span></span>

    <span data-ttu-id="13442-162">Poniższa ilustracja przedstawia przykładowy kod podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="13442-162">The following image shows the code with the underlines.</span></span>

    <span data-ttu-id="13442-163">![Witamy tekst w widoku Projekt](code-editing-in-web-forms-pages/_static/image5.png "Witamy tekst w widoku Projekt")</span><span class="sxs-lookup"><span data-stu-id="13442-163">![Welcome text in Design view](code-editing-in-web-forms-pages/_static/image5.png "Welcome text in Design view")</span></span>  
 <span data-ttu-id="13442-164">Błąd muszą zostać usunięte przez dodanie średnikiem `;` do końca wiersza.</span><span class="sxs-lookup"><span data-stu-id="13442-164">The error must be fixed by adding a semicolon `;` to the end of the line.</span></span> <span data-ttu-id="13442-165">Ostrzeżenie po prostu powiadamia użytkownika, aby nie były używane `myStr` jeszcze zmiennej.</span><span class="sxs-lookup"><span data-stu-id="13442-165">The warning simply notifies you that you haven't used the `myStr` variable yet.</span></span>  

    > [!NOTE] 
    > 
    > <span data-ttu-id="13442-166">Możesz wyświetlić bieżący kod formatowania ustawień w Visual Studio, wybierając **narzędzia**  - &gt; **opcje**  - &gt; **czcionek i Kolory**.</span><span class="sxs-lookup"><span data-stu-id="13442-166">You view your current code formatting settings in Visual Studio by selecting **Tools** -&gt; **Options** -&gt; **Fonts and Colors**.</span></span>


## <a name="refactoring-and-renaming"></a><span data-ttu-id="13442-167">Refaktoryzacja i zmiana nazwy</span><span class="sxs-lookup"><span data-stu-id="13442-167">Refactoring and Renaming</span></span>

<span data-ttu-id="13442-168">Refaktoryzacja jest metodologia oprogramowania, która obejmuje restrukturyzacji swój kod, aby ułatwić zrozumienie i obsługa, zachowując jego funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="13442-168">Refactoring is a software methodology that involves restructuring your code to make it easier to understand and to maintain, while preserving its functionality.</span></span> <span data-ttu-id="13442-169">Prosty przykład może być napisać kod w obsłudze zdarzeń można pobrać danych z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13442-169">A simple example might be that you write code in an event handler to get data from a database.</span></span> <span data-ttu-id="13442-170">Podczas opracowywania strony odkrywasz, trzeba uzyskać dostęp do danych z wielu różnych obsługi.</span><span class="sxs-lookup"><span data-stu-id="13442-170">As you develop your page, you discover that you need to access the data from several different handlers.</span></span> <span data-ttu-id="13442-171">W związku z tym Refaktoryzuj kodu strony tworzenia metody dostępu do danych na stronie i wstawianie wywołania metody w obsłudze.</span><span class="sxs-lookup"><span data-stu-id="13442-171">Therefore, you refactor the page's code by creating a data-access method in the page and inserting calls to the method in the handlers.</span></span>

<span data-ttu-id="13442-172">Edytor kodu zawiera narzędzia, które ułatwiają wykonywanie różnych zadań refaktoryzacji.</span><span class="sxs-lookup"><span data-stu-id="13442-172">The code editor includes tools to help you perform various refactoring tasks.</span></span> <span data-ttu-id="13442-173">W tym przewodniku będzie działać z dwóch metod refaktoryzacji: zmiana nazwy zmiennych i wyodrębniania metody.</span><span class="sxs-lookup"><span data-stu-id="13442-173">In this walkthrough, you will work with two refactoring techniques: renaming variables and extracting methods.</span></span> <span data-ttu-id="13442-174">Inne opcje refaktoryzacji obejmują hermetyzując pól, podwyższania poziomu zmiennych lokalnych do parametrów metod i zarządzania parametry metody.</span><span class="sxs-lookup"><span data-stu-id="13442-174">Other refactoring options include encapsulating fields, promoting local variables to method parameters, and managing method parameters.</span></span> <span data-ttu-id="13442-175">Dostępność tych opcji refaktoryzacji zależy od lokalizacji w kodzie.</span><span class="sxs-lookup"><span data-stu-id="13442-175">The availability of these refactoring options depends on the location in the code.</span></span>

### <a name="refactoring-code"></a><span data-ttu-id="13442-176">Refaktoryzacji kodu</span><span class="sxs-lookup"><span data-stu-id="13442-176">Refactoring Code</span></span>

<span data-ttu-id="13442-177">Typowy scenariusz refaktoryzacji jest utworzenie (extract) metody z kodu, który znajduje się wewnątrz innego elementu członkowskiego, takich jak metody.</span><span class="sxs-lookup"><span data-stu-id="13442-177">A common refactoring scenario is to create (extract) a method from code that is inside another member, such as a method.</span></span> <span data-ttu-id="13442-178">Zmniejsza rozmiar oryginalnego elementu i sprawia, że kod wyodrębnionego wielokrotnego użytku.</span><span class="sxs-lookup"><span data-stu-id="13442-178">This reduces the size of the original member and makes the extracted code reusable.</span></span>

<span data-ttu-id="13442-179">W tej części przewodnika będą napisanie kodu, proste, a następnie Wyodrębnij metodę z niego.</span><span class="sxs-lookup"><span data-stu-id="13442-179">In this part of the walkthrough, you will write some simple code, and then extract a method from it.</span></span> <span data-ttu-id="13442-180">Refaktoryzacja jest obsługiwana dla C#, więc będzie można utworzyć stronę, która używa języka C# jako języka programowania.</span><span class="sxs-lookup"><span data-stu-id="13442-180">Refactoring is supported for C#, so you will create a page that uses C# as its programming language.</span></span>

### <a name="to-extract-a-method-in-a-c-page"></a><span data-ttu-id="13442-181">Aby wyodrębnić metody na stronie C#</span><span class="sxs-lookup"><span data-stu-id="13442-181">To extract a method in a C# page</span></span>

1. <span data-ttu-id="13442-182">Przełącz się do **projekt** widoku.</span><span class="sxs-lookup"><span data-stu-id="13442-182">Switch to **Design** view.</span></span>
2. <span data-ttu-id="13442-183">W **przybornika**, z **standardowe** karcie, przeciągnij [przycisk](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) kontrolki na stronie.</span><span class="sxs-lookup"><span data-stu-id="13442-183">In the **Toolbox**, from the **Standard** tab, drag a [Button](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) control onto the page.</span></span>
3. <span data-ttu-id="13442-184">Kliknij dwukrotnie **przycisk** formantu, aby utworzyć uchwytu dla jego [kliknij](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) zdarzenia, a następnie dodaj następujący wyróżniony kod:</span><span class="sxs-lookup"><span data-stu-id="13442-184">Double-click the **Button** control to create a handler for its [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) event, and then add the following highlighted code:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

 <span data-ttu-id="13442-185">Kod tworzy **ArrayList** obiektu, używa go załadować z wartościami pętlę, a następnie używa innego pętli do wyświetlenia zawartości **ArrayList** obiektu.</span><span class="sxs-lookup"><span data-stu-id="13442-185">The code creates an **ArrayList** object, uses a loop to load it with values, and then uses another loop to display the contents of the **ArrayList** object.</span></span>
4. <span data-ttu-id="13442-186">Naciśnij klawisz **CTRL + F5** do uruchomienia strony, a następnie kliknij przycisk **przycisk** aby upewnić się, że wyświetlone następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="13442-186">Press **CTRL+F5** to run the page, and then click the **button** to make sure that you see the following output:</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. <span data-ttu-id="13442-187">Powrócić do edytora kodu, a następnie wybierz następujące wiersze do obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="13442-187">Return to the code editor, and then select the following lines in the event handler.</span></span>   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. <span data-ttu-id="13442-188">Kliknij prawym przyciskiem myszy zaznaczenie, kliknij przycisk **Refaktoryzuj**, a następnie wybierz pozycję **Wyodrębnij metodę**.</span><span class="sxs-lookup"><span data-stu-id="13442-188">Right-click the selection, click **Refactor**, and then choose **Extract Method**.</span></span> 

    <span data-ttu-id="13442-189">**Wyodrębnij metodę** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13442-189">The **Extract Method** dialog box appears.</span></span>
7. <span data-ttu-id="13442-190">W **nową nazwę metody** wpisz **DisplayArray**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="13442-190">In the **New Method Name** box, type **DisplayArray**, and then click **OK**.</span></span> 

    <span data-ttu-id="13442-191">Edytor kodu tworzy nową metodę o nazwie `DisplayArray`i umieszcza wywołanie do nowej metody w **kliknij** obsługi którym pierwotnie pętli.</span><span class="sxs-lookup"><span data-stu-id="13442-191">The code editor creates a new method named `DisplayArray`, and puts a call to the new method in the **Click** handler where the loop was originally.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. <span data-ttu-id="13442-192">Naciśnij klawisz **CTRL + F5** ponownie uruchomić stronę, a następnie kliknij przycisk **przycisk**.</span><span class="sxs-lookup"><span data-stu-id="13442-192">Press **CTRL+F5** to run the page again, and click the **button**.</span></span>

    <span data-ttu-id="13442-193">Strona działa tak samo, tak jak poprzednio.</span><span class="sxs-lookup"><span data-stu-id="13442-193">The page functions the same as it did before.</span></span> <span data-ttu-id="13442-194">`DisplayArray` Metoda może być teraz wywołania z dowolnego miejsca w klasie strony.</span><span class="sxs-lookup"><span data-stu-id="13442-194">The `DisplayArray` method can now be call from anywhere in the page class.</span></span>

## <a name="renaming-variables"></a><span data-ttu-id="13442-195">Zmiana nazwy zmiennych</span><span class="sxs-lookup"><span data-stu-id="13442-195">Renaming Variables</span></span>

<span data-ttu-id="13442-196">Podczas pracy z obiektów, a także zmienne, można zmienić ich nazwy po ich są już przywoływane w kodzie.</span><span class="sxs-lookup"><span data-stu-id="13442-196">When you work with variables, as well as objects, you might want to rename them after they are already referenced in your code.</span></span> <span data-ttu-id="13442-197">Zmiana nazwy zmiennych i obiektów może jednak spowodować kodu Jeśli pominiesz zmiana nazwy jedno z odwołań.</span><span class="sxs-lookup"><span data-stu-id="13442-197">However, renaming variables and objects can cause the code to break if you miss renaming one of the references.</span></span> <span data-ttu-id="13442-198">W związku z tym umożliwia refaktoryzacji wykonaj zmianie nazwy.</span><span class="sxs-lookup"><span data-stu-id="13442-198">Therefore, you can use refactoring to perform the renaming.</span></span>

### <a name="to-use-refactoring-to-rename-a-variable"></a><span data-ttu-id="13442-199">Aby użyć refaktoryzacji można zmienić nazwy zmiennej</span><span class="sxs-lookup"><span data-stu-id="13442-199">To use refactoring to rename a variable</span></span>


1. <span data-ttu-id="13442-200">W **kliknij** program obsługi zdarzeń, znajdź następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="13442-200">In the **Click** event handler, locate the following line:</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. <span data-ttu-id="13442-201">Kliknij prawym przyciskiem myszy nazwę zmiennej `alist`, wybierz **Refaktoryzuj**, a następnie wybierz pozycję **zmienić**.</span><span class="sxs-lookup"><span data-stu-id="13442-201">Right-click the variable name `alist`, choose **Refactor**, and then choose **Rename**.</span></span>

    <span data-ttu-id="13442-202">**Zmienić** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13442-202">The **Rename** dialog box appears.</span></span>
3. <span data-ttu-id="13442-203">W **nową nazwę** wpisz **ArrayList1** i upewnij się, że **podgląd zmian odwołanie** pole wyboru zostało zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="13442-203">In the **New name** box, type **ArrayList1** and make sure the **Preview reference changes** checkbox has been selected.</span></span> <span data-ttu-id="13442-204">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="13442-204">Then click **OK**.</span></span>

    <span data-ttu-id="13442-205">**Podgląd zmian** okno dialogowe zostanie wyświetlone i wyświetla drzewa, który zawiera wszystkie odwołania do zmiennej, która jest zmieniana.</span><span class="sxs-lookup"><span data-stu-id="13442-205">The **Preview Changes** dialog box appears, and displays a tree that contains all references to the variable that you are renaming.</span></span>
4. <span data-ttu-id="13442-206">Kliknij przycisk **Zastosuj** zamknąć **podgląd zmian** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13442-206">Click **Apply** to close the **Preview Changes** dialog box.</span></span>

    <span data-ttu-id="13442-207">Zmienne odwołujące się specjalnie do wybranego wystąpienia są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="13442-207">The variables that refer specifically to the instance that you selected are renamed.</span></span> <span data-ttu-id="13442-208">Zauważ, że zmienna `alist` w następującym wierszu nie zostaje zmieniona.</span><span class="sxs-lookup"><span data-stu-id="13442-208">Note, however, that the variable `alist` in the following line is not renamed.</span></span>

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    <span data-ttu-id="13442-209">Zmienna `alist` w danym wierszu nie zostaje zmieniona, ponieważ nie reprezentuje taką samą wartość jak zmienna `alist` którego nazwa została zmieniona.</span><span class="sxs-lookup"><span data-stu-id="13442-209">The variable `alist` in this line is not renamed because it does not represent the same value as the variable `alist` that you renamed.</span></span> <span data-ttu-id="13442-210">Zmienna `alist` w `DisplayArray` deklaracja jest zmienną lokalną dla tej metody.</span><span class="sxs-lookup"><span data-stu-id="13442-210">The variable `alist` in the `DisplayArray` declaration is a local variable for that method.</span></span> <span data-ttu-id="13442-211">Przedstawiono to, że można zmienić nazwy zmiennych przy użyciu refaktoryzacji różni się od po prostu wykonywanie akcji Znajdź i Zamień w edytorze; Refaktoryzacja zmiany nazwy zmiennych o wiedzy semantykę zmiennej, która działa z.</span><span class="sxs-lookup"><span data-stu-id="13442-211">This illustrates that using refactoring to rename variables is different than simply performing a find-and-replace action in the editor; refactoring renames variables with knowledge of the semantics of the variable that it is working with.</span></span>


## <a name="inserting-snippets"></a><span data-ttu-id="13442-212">Wstawianie wstawek</span><span class="sxs-lookup"><span data-stu-id="13442-212">Inserting Snippets</span></span>

<span data-ttu-id="13442-213">Ponieważ istnieje wiele zadań kodowania, które deweloperzy formularzy sieci Web często konieczne jest wykonanie, edytora kodu zawiera bibliotekę wstawki lub bloków kodu przedpisanych.</span><span class="sxs-lookup"><span data-stu-id="13442-213">Because there are many coding tasks that Web Forms developers frequently need to perform, the code editor provides a library of snippets, or blocks of prewritten code.</span></span> <span data-ttu-id="13442-214">Na stronie można wstawić tych fragmentów.</span><span class="sxs-lookup"><span data-stu-id="13442-214">You can insert these snippets into your page.</span></span>

<span data-ttu-id="13442-215">Każdego języka używanego w programie Visual Studio ma niewielkie różnice w sposób wstawiania wstawki kodu.</span><span class="sxs-lookup"><span data-stu-id="13442-215">Each language that you use in Visual Studio has slight differences in the way you insert code snippets.</span></span> <span data-ttu-id="13442-216">Aby dowiedzieć się, jak wstawianie fragmentów, zobacz [Visual Basic IntelliSense — wstawki programu](https://msdn.microsoft.com/library/18yz4be4.aspx).</span><span class="sxs-lookup"><span data-stu-id="13442-216">For information about inserting snippets, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx).</span></span> <span data-ttu-id="13442-217">Aby dowiedzieć się, jak wstawianie fragmenty kodu języka Visual C#, zobacz [Visual C# — wstawki](https://msdn.microsoft.com/library/z41h7fat.aspx).</span><span class="sxs-lookup"><span data-stu-id="13442-217">For information about inserting snippets in Visual C#, see [Visual C# Code Snippets](https://msdn.microsoft.com/library/z41h7fat.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13442-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13442-218">Next Steps</span></span>

<span data-ttu-id="13442-219">W tym przewodniku ma przedstawiono podstawowe funkcje programu Visual Studio 2010 edytora kodu poprawianie błędów w kodzie, refaktoryzacji kodu, zmiana nazwy zmiennych i wstawiania wstawki kodu w kodzie.</span><span class="sxs-lookup"><span data-stu-id="13442-219">This walkthrough has illustrated the basic features of the Visual Studio 2010 code editor for correcting errors in your code, refactoring code, renaming variables, and inserting code snippets into your code.</span></span> <span data-ttu-id="13442-220">Dodatkowe funkcje w edytorze ułatwia projektowanie aplikacji szybkie i łatwe.</span><span class="sxs-lookup"><span data-stu-id="13442-220">Additional features in the editor can make application development fast and easy.</span></span> <span data-ttu-id="13442-221">Na przykład możesz chcieć:</span><span class="sxs-lookup"><span data-stu-id="13442-221">For example, you might want to:</span></span>

- <span data-ttu-id="13442-222">Więcej informacji na temat funkcji IntelliSense, takich jak modyfikowanie opcji IntelliSense, zarządzanie fragmentów kodu i wyszukiwanie wstawki kodu w trybie online.</span><span class="sxs-lookup"><span data-stu-id="13442-222">Learn more about the features of IntelliSense, such as modifying IntelliSense options, managing code snippets, and searching for code snippets online.</span></span> <span data-ttu-id="13442-223">Aby uzyskać więcej informacji, zobacz [za pomocą funkcji IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span><span class="sxs-lookup"><span data-stu-id="13442-223">For more information, see [Using IntelliSense](https://msdn.microsoft.com/library/hcw1s69b.aspx).</span></span>
- <span data-ttu-id="13442-224">Dowiedz się, jak utworzyć własne wstawki kodu.</span><span class="sxs-lookup"><span data-stu-id="13442-224">Learn how to create your own code snippets.</span></span> <span data-ttu-id="13442-225">Aby uzyskać więcej informacji, zobacz [tworzenie i przy użyciu fragmentów kodu IntelliSense](https://msdn.microsoft.com/library/ms165392.aspx)</span><span class="sxs-lookup"><span data-stu-id="13442-225">For more information, see [Creating and Using IntelliSense Code Snippets](https://msdn.microsoft.com/library/ms165392.aspx)</span></span>
- <span data-ttu-id="13442-226">Dowiedz się więcej na temat funkcji specyficznych dla języka Visual Basic, fragmentów kodu IntelliSense, takie jak dostosowywanie fragmenty kodu i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="13442-226">Learn more about the Visual Basic-specific features of IntelliSense code snippets, such as customizing the snippets and troubleshooting.</span></span> <span data-ttu-id="13442-227">Aby uzyskać więcej informacji, zobacz [Visual Basic IntelliSense — wstawki programu](https://msdn.microsoft.com/library/18yz4be4.aspx)</span><span class="sxs-lookup"><span data-stu-id="13442-227">For more information, see [Visual Basic IntelliSense Code Snippets](https://msdn.microsoft.com/library/18yz4be4.aspx)</span></span>
- <span data-ttu-id="13442-228">Dowiedz się więcej na temat języka C# — funkcje IntelliSense, takie jak wstawki refaktoryzacji i kod.</span><span class="sxs-lookup"><span data-stu-id="13442-228">Learn more about the C#-specific features of IntelliSense, such as refactoring and code snippets.</span></span> <span data-ttu-id="13442-229">Aby uzyskać więcej informacji, zobacz [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span><span class="sxs-lookup"><span data-stu-id="13442-229">For more information, see [Visual C# IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).</span></span>