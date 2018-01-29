---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: "Wysyłanie wiadomości E-mail z sieci Web ASP.NET stron witryny (Razor) | Dokumentacja firmy Microsoft"
author: tfitzmac
description: "W tym rozdziale opisano sposób wysyłania wiadomości e-mail automatycznych z witryny sieci Web."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: c5878c3bc468daef050dcebee99f64441066409a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="1dabd-103">Wysyłanie wiadomości E-mail z witryny sieci Web platformy ASP.NET (Razor) stron</span><span class="sxs-lookup"><span data-stu-id="1dabd-103">Sending Email from an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="1dabd-104">przez [FitzMacken niestandardowy](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1dabd-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1dabd-105">W tym artykule opisano sposób używania stron sieci Web platformy ASP.NET (Razor), Wyślij wiadomość e-mail z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1dabd-105">This article explains how to send an email message from a website when you use ASP.NET Web Pages (Razor).</span></span>
> 
> <span data-ttu-id="1dabd-106">Zawartość:</span><span class="sxs-lookup"><span data-stu-id="1dabd-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="1dabd-107">Jak wysłać wiadomość e-mail z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1dabd-107">How to send an email message from your website.</span></span>
> - <span data-ttu-id="1dabd-108">Jak dołączyć plik do wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-108">How to attach a file to an email message.</span></span>
> 
> <span data-ttu-id="1dabd-109">Jest to funkcja ASP.NET, wprowadzona w artykule:</span><span class="sxs-lookup"><span data-stu-id="1dabd-109">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="1dabd-110">`WebMail` Pomocnika.</span><span class="sxs-lookup"><span data-stu-id="1dabd-110">The `WebMail` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1dabd-111">Używane w samouczku wersje oprogramowania</span><span class="sxs-lookup"><span data-stu-id="1dabd-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1dabd-112">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1dabd-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1dabd-113">W tym samouczku współdziała również z programu ASP.NET Web Pages 2.</span><span class="sxs-lookup"><span data-stu-id="1dabd-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a><span data-ttu-id="1dabd-114">Wysyłanie wiadomości E-mail z witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="1dabd-114">Sending Email Messages from Your Website</span></span>

<span data-ttu-id="1dabd-115">Istnieją różne rodzaje powodów dlaczego może być konieczne do wysyłania wiadomości e-mail z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1dabd-115">There are all sorts of reasons why you might need to send email from your website.</span></span> <span data-ttu-id="1dabd-116">Potwierdzenie wiadomości mogą wysyłać do użytkowników lub może wysyłać powiadomienia do siebie (na przykład, który został zarejestrowany przez nowego użytkownika.) `WebMail` Pomocnika umożliwia łatwe wysyłanie wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-116">You might send confirmation messages to users, or you might send notifications to yourself (for example, that a new user has registered.) The `WebMail` helper makes it easy for you to send email.</span></span>

<span data-ttu-id="1dabd-117">Aby użyć `WebMail` pomocnika, musisz mieć dostęp do serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-117">To use the `WebMail` helper, you have to have access to an SMTP server.</span></span> <span data-ttu-id="1dabd-118">(Oznacza SMTP *Simple Mail Transfer Protocol*.) Serwer SMTP to serwer poczty e-mail, który tylko przesyła dalej wiadomości do serwera adresata &#8212; jest wychodzący po stronie wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-118">(SMTP stands for *Simple Mail Transfer Protocol*.) An SMTP server is an email server that only forwards messages to the recipient's server &#8212; it's the outbound side of email.</span></span> <span data-ttu-id="1dabd-119">Jeśli używasz dostawcy usług hosta dla witryny sieci Web, ich prawdopodobnie skonfiguruj można za pomocą poczty e-mail i ich pomagają stwierdzić, co to jest nazwa serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-119">If you use a hosting provider for your website, they probably set you up with email and they can tell you what your SMTP server name is.</span></span> <span data-ttu-id="1dabd-120">Podczas pracy w sieci firmowej, administratorem lub działem IT można zwykle można uzyskać informacje dotyczące serwera SMTP, który można użyć.</span><span class="sxs-lookup"><span data-stu-id="1dabd-120">If you're working inside a corporate network, an administrator or your IT department can usually give you the information about an SMTP server that you can use.</span></span> <span data-ttu-id="1dabd-121">Jeśli pracujesz w domu, nawet można przetestować go przy użyciu dostawcy zwykłej poczty e-mail, który można podać nazwę serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-121">If you're working at home, you might even be able to test using your ordinary email provider, who can tell you the name of their SMTP server.</span></span> <span data-ttu-id="1dabd-122">Zazwyczaj potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="1dabd-122">You typically need:</span></span>

- <span data-ttu-id="1dabd-123">Nazwa serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-123">The name of the SMTP server.</span></span>
- <span data-ttu-id="1dabd-124">Numer portu.</span><span class="sxs-lookup"><span data-stu-id="1dabd-124">The port number.</span></span> <span data-ttu-id="1dabd-125">To jest prawie zawsze 25.</span><span class="sxs-lookup"><span data-stu-id="1dabd-125">This is almost always 25.</span></span> <span data-ttu-id="1dabd-126">Usługodawcy mogą jednak wymagają użycia portu 587.</span><span class="sxs-lookup"><span data-stu-id="1dabd-126">However, your ISP may require you to use port 587.</span></span> <span data-ttu-id="1dabd-127">Jeśli korzystasz z bezpiecznego secure sockets layer (SSL) do obsługi poczty e-mail, może być konieczne innego portu.</span><span class="sxs-lookup"><span data-stu-id="1dabd-127">If you are using secure sockets layer (SSL) for email, you might need a different port.</span></span> <span data-ttu-id="1dabd-128">Skontaktuj się z dostawcą poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-128">Check with your email provider.</span></span>
- <span data-ttu-id="1dabd-129">Poświadczenia (nazwa użytkownika, hasło).</span><span class="sxs-lookup"><span data-stu-id="1dabd-129">Credentials (user name, password).</span></span>

<span data-ttu-id="1dabd-130">W tej procedurze utworzysz dwie strony.</span><span class="sxs-lookup"><span data-stu-id="1dabd-130">In this procedure, you create two pages.</span></span> <span data-ttu-id="1dabd-131">Pierwsza strona ma formularz, który umożliwia użytkownikom, podaj opis, tak, jakby były wypełnieniu formularza obsługi technicznej.</span><span class="sxs-lookup"><span data-stu-id="1dabd-131">The first page has a form that lets users enter a description, as if they were filling in a technical-support form.</span></span> <span data-ttu-id="1dabd-132">Pierwsza strona prześle informacje do drugiej strony.</span><span class="sxs-lookup"><span data-stu-id="1dabd-132">The first page submits its information to a second page.</span></span> <span data-ttu-id="1dabd-133">Na drugiej stronie kod wyodrębnia dane użytkownika i wysyła wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-133">In the second page, code extracts the user's information and sends an email message.</span></span> <span data-ttu-id="1dabd-134">Wyświetla komunikat potwierdzający Odebrano raport o problemie.</span><span class="sxs-lookup"><span data-stu-id="1dabd-134">It also displays a message confirming that the problem report has been received.</span></span>

![[Obraz]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> <span data-ttu-id="1dabd-136">Aby zachować w tym przykładzie jest proste, inicjuje kod `WebMail` pomocnika prawej strony, której używasz.</span><span class="sxs-lookup"><span data-stu-id="1dabd-136">To keep this example simple, the code initializes the `WebMail` helper right in the page where you use it.</span></span> <span data-ttu-id="1dabd-137">Jednak dla rzeczywistych witryn sieci Web, jest zorientować się wprowadzić kod inicjujący następująco w pliku globalnego, dzięki czemu można zainicjować `WebMail` pomocnika dla wszystkich plików w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1dabd-137">However, for real websites, it's a better idea to put initialization code like this in a global file, so that you initialize the `WebMail` helper for all files in your website.</span></span> <span data-ttu-id="1dabd-138">Aby uzyskać więcej informacji, zobacz [Dostosowywanie zachowanie całej witryny ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span><span class="sxs-lookup"><span data-stu-id="1dabd-138">For more information, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers).</span></span>


1. <span data-ttu-id="1dabd-139">Utwórz nową witrynę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1dabd-139">Create a new website.</span></span>
2. <span data-ttu-id="1dabd-140">Dodaj nową stronę o nazwie *EmailRequest.cshtml* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="1dabd-140">Add a new page named *EmailRequest.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    <span data-ttu-id="1dabd-141">Zwróć uwagę, że `action` ustawiono atrybut elementu form *ProcessRequest.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="1dabd-141">Notice that the `action` attribute of the form element has been set to *ProcessRequest.cshtml*.</span></span> <span data-ttu-id="1dabd-142">Oznacza to, że formularz zostanie przesłany do tej strony, a nie do bieżącej strony.</span><span class="sxs-lookup"><span data-stu-id="1dabd-142">This means that the form will be submitted to that page instead of back to the current page.</span></span>
3. <span data-ttu-id="1dabd-143">Dodaj nową stronę o nazwie *ProcessRequest.cshtml* witryny sieci Web i Dodaj następujący kod i kod znaczników:</span><span class="sxs-lookup"><span data-stu-id="1dabd-143">Add a new page named *ProcessRequest.cshtml* to the website and add the following code and markup:</span></span>   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    <span data-ttu-id="1dabd-144">W kodzie można pobrać wartości pola formularza, które zostały przesłane do strony.</span><span class="sxs-lookup"><span data-stu-id="1dabd-144">In the code, you get the values of the form fields that were submitted to the page.</span></span> <span data-ttu-id="1dabd-145">Następnie wywołaj `WebMail` przez pomocnika `Send` metody do tworzenia i wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-145">You then call the `WebMail` helper's `Send` method to create and send the email message.</span></span> <span data-ttu-id="1dabd-146">W tym przypadku wartości do użycia składają się z tekstu, który można łączyć z wartościami, które zostały przesłane z formularza.</span><span class="sxs-lookup"><span data-stu-id="1dabd-146">In this case, the values to use are made up of text that you concatenate with the values that were submitted from the form.</span></span>

    <span data-ttu-id="1dabd-147">Kod na tej stronie znajduje się wewnątrz `try/catch` bloku.</span><span class="sxs-lookup"><span data-stu-id="1dabd-147">The code for this page is inside a `try/catch` block.</span></span> <span data-ttu-id="1dabd-148">Jeśli z jakiegokolwiek powodu, próba wysłania wiadomości e-mail nie działa (na przykład, te ustawienia są prawo), kod w `catch` blok uruchamia i ustawia `errorMessage` zmiennej, aby wskazywał błąd, który wystąpił.</span><span class="sxs-lookup"><span data-stu-id="1dabd-148">If for any reason the attempt to send an email doesn't work (for example, the settings aren't right), the code in the `catch` block runs and sets the `errorMessage` variable to the error that has occurred.</span></span> <span data-ttu-id="1dabd-149">(Aby uzyskać więcej informacji na temat `try/catch` bloków lub `<text>` tagów, zobacz [wprowadzenie do platformy ASP.NET Web Pages programowania przy użyciu składni Razor](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span><span class="sxs-lookup"><span data-stu-id="1dabd-149">(For more information about `try/catch` blocks or the `<text>` tag, see [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)</span></span>

    <span data-ttu-id="1dabd-150">W treści strony Jeśli `errorMessage` zmiennej jest pusty (wartość domyślna), użytkownik zobaczy następujący komunikat, który wiadomość e-mail została wysłana.</span><span class="sxs-lookup"><span data-stu-id="1dabd-150">In the body of the page, if the `errorMessage` variable is empty (the default), the user sees a message that the email message has been sent.</span></span> <span data-ttu-id="1dabd-151">Jeśli `errorMessage` zmienna jest ustawiona na wartość true, użytkownik widzi na komunikat, że wystąpił problem podczas wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="1dabd-151">If the `errorMessage` variable is set to true, the user sees a message that there's been a problem sending the message.</span></span>

    <span data-ttu-id="1dabd-152">Należy zauważyć, że w części strony, która wyświetla komunikat o błędzie, jest dodatkowy test: `if(debuggingFlag)`.</span><span class="sxs-lookup"><span data-stu-id="1dabd-152">Notice that in the portion of the page that displays an error message, there's an additional test: `if(debuggingFlag)`.</span></span> <span data-ttu-id="1dabd-153">Jest to zmienna ustawioną na true, jeśli wystąpiły problemy podczas wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-153">This is a variable that you can set to true if you're having trouble sending email.</span></span> <span data-ttu-id="1dabd-154">Gdy `debuggingFlag` ma wartość true, a w przypadku problem podczas wysyłania wiadomości e-mail, wyświetlony komunikat o błędzie dodatkowe pokazujący, niezależnie od platformy ASP.NET został zgłoszony podczas próby wysłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-154">When `debuggingFlag` is true, and if there's a problem sending email, an additional error message is displayed that shows whatever ASP.NET has reported when it tried to send the email message.</span></span> <span data-ttu-id="1dabd-155">Ostrzeżenie odpowiedniego, choć: komunikaty o błędach, które program ASP.NET zgłasza, jeśli nie można wysłać wiadomości e-mail mogą być ogólne.</span><span class="sxs-lookup"><span data-stu-id="1dabd-155">Fair warning, though: the error messages that ASP.NET reports when it can't send an email message can be generic.</span></span> <span data-ttu-id="1dabd-156">Na przykład jeśli program ASP.NET nie może skontaktować się z serwerem SMTP (na przykład, ponieważ wprowadzone wystąpił błąd w nazwie serwera), błąd `Failure sending mail`.</span><span class="sxs-lookup"><span data-stu-id="1dabd-156">For example, if ASP.NET can't contact the SMTP server (for example, because you made an error in the server name), the error is `Failure sending mail`.</span></span>

    > [!NOTE] 
    > 
    > <span data-ttu-id="1dabd-157">**Ważne** Jeśli wyświetlony komunikat o błędzie z obiektu wyjątku (`ex` w kodzie), czy *nie* rutynowo przekazywać wiadomości za pośrednictwem użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="1dabd-157">**Important** When you get an error message from an exception object (`ex` in the code), do *not* routinely pass that message through to users.</span></span> <span data-ttu-id="1dabd-158">Obiekty wyjątków często zawierają informacje, czy użytkownicy nie powinien być widoczny i które może nawet być luki w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="1dabd-158">Exception objects often include information that users should not see and that can even be a security vulnerability.</span></span> <span data-ttu-id="1dabd-159">Dlatego ten kod zawiera zmienną `debuggingFlag` który jest używany jako przełącznik, aby wyświetlić komunikat o błędzie i dlaczego zmiennej domyślnie jest ustawiona na wartość false.</span><span class="sxs-lookup"><span data-stu-id="1dabd-159">That's why this code includes the variable `debuggingFlag` that's used as a switch to display the error message, and why the variable by default is set to false.</span></span> <span data-ttu-id="1dabd-160">Należy ustawić tej zmiennej na true (i w związku z tym wyświetlony komunikat o błędzie) *tylko* Jeśli występuje problem z wysyłaniem wiadomości e-mail należy do debugowania.</span><span class="sxs-lookup"><span data-stu-id="1dabd-160">You should set that variable to true (and therefore display the error message) *only* if you're having a problem with sending email and you need to debug.</span></span> <span data-ttu-id="1dabd-161">Po rozwiązaniu problemów, ustaw `debuggingFlag` ponownie na wartość false.</span><span class="sxs-lookup"><span data-stu-id="1dabd-161">Once you have fixed any problems, set `debuggingFlag` back to false.</span></span>

    <span data-ttu-id="1dabd-162">Zmodyfikuj następujące e-mail powiązane ustawienia w kodzie:</span><span class="sxs-lookup"><span data-stu-id="1dabd-162">Modify the following email related settings in the code:</span></span>

    - <span data-ttu-id="1dabd-163">Ustaw `your-SMTP-host` na nazwę serwera SMTP, który ma dostęp do.</span><span class="sxs-lookup"><span data-stu-id="1dabd-163">Set `your-SMTP-host` to the name of the SMTP server that you have access to.</span></span>
    - <span data-ttu-id="1dabd-164">Ustaw `your-user-name-here` do nazwy użytkownika dla konta serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-164">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="1dabd-165">Ustaw `your-account-password` hasło dla konta serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-165">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="1dabd-166">Ustaw `your-email-address-here` na adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-166">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="1dabd-167">Jest to komunikat jest wysyłany z adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-167">This is the email address that the message is sent from.</span></span> <span data-ttu-id="1dabd-168">(Niektóre dostawców poczty e-mail nie umożliwiają określenie innej `From` adresów, a następnie użyje swoją nazwę użytkownika jako `From` adresu.)</span><span class="sxs-lookup"><span data-stu-id="1dabd-168">(Some email providers don't let you specify a different `From` address and will use your user name as the `From` address.)</span></span>

    > [!TIP] 
    > 
    > <a id="configuring_email_settings"></a>
    > ### <a name="configuring-email-settings"></a><span data-ttu-id="1dabd-169">Konfigurowanie ustawień poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="1dabd-169">Configuring Email Settings</span></span>
    > 
    > <span data-ttu-id="1dabd-170">Może stanowić wyzwanie czasami, aby upewnić się, że masz prawa ustawienia serwera SMTP, numer portu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="1dabd-170">It can be a challenge sometimes to make sure you have the right settings for the SMTP server, port number, and so on.</span></span> <span data-ttu-id="1dabd-171">Poniżej przedstawiono kilka wskazówek:</span><span class="sxs-lookup"><span data-stu-id="1dabd-171">Here are a few tips:</span></span>
    > 
    > - <span data-ttu-id="1dabd-172">Nazwa serwera SMTP jest często przypominać `smtp.provider.com` lub `smtp.provider.net`.</span><span class="sxs-lookup"><span data-stu-id="1dabd-172">The SMTP server name is often something like `smtp.provider.com` or `smtp.provider.net`.</span></span> <span data-ttu-id="1dabd-173">Jeśli jednak publikowania witryny dostawcy hostingu, nazwę serwera SMTP w tym momencie może być `localhost`.</span><span class="sxs-lookup"><span data-stu-id="1dabd-173">However, if you publish your site to a hosting provider, the SMTP server name at that point might be `localhost`.</span></span> <span data-ttu-id="1dabd-174">Jest to spowodowane po opublikowaniu, witryna jest hostowana na serwerze dostawcy, z serwerem poczty e-mail może być lokalny z punktu widzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1dabd-174">This is because after you've published and your site is running on the provider's server, the email server might be local from the perspective of your application.</span></span> <span data-ttu-id="1dabd-175">Ta zmiana nazwy serwera może oznaczać, że trzeba zmienić nazwę serwera SMTP w trakcie procesu publikowania.</span><span class="sxs-lookup"><span data-stu-id="1dabd-175">This change in server names might mean you have to change the SMTP server name as part of your publishing process.</span></span>
    > - <span data-ttu-id="1dabd-176">Numer portu jest zwykle 25.</span><span class="sxs-lookup"><span data-stu-id="1dabd-176">The port number is usually 25.</span></span> <span data-ttu-id="1dabd-177">Jednak niektóre dostawców wymagają użycia portu 587 lub pewne inne porty.</span><span class="sxs-lookup"><span data-stu-id="1dabd-177">However, some providers require you to use port 587 or some other port.</span></span>
    > - <span data-ttu-id="1dabd-178">Upewnij się, że używasz prawidłowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1dabd-178">Make sure that you use the right credentials.</span></span> <span data-ttu-id="1dabd-179">Po opublikowaniu lokacji do dostawcy hostingu, Użyj poświadczeń, które dostawcy specjalnie wskazuje, czy do obsługi poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-179">If you've published your site to a hosting provider, use the credentials that the provider has specifically indicated are for email.</span></span> <span data-ttu-id="1dabd-180">Te mogą się różnić od poświadczeń używanych do opublikowania.</span><span class="sxs-lookup"><span data-stu-id="1dabd-180">These might be different from the credentials you use to publish.</span></span>
    > - <span data-ttu-id="1dabd-181">Czasami nie potrzebujesz poświadczeń w ogóle.</span><span class="sxs-lookup"><span data-stu-id="1dabd-181">Sometimes you don't need credentials at all.</span></span> <span data-ttu-id="1dabd-182">Przy wysyłaniu wiadomości e-mail za pomocą osobistego usługodawca Internetowy dostawcę poczty e-mail może być już wiesz, swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="1dabd-182">If you're sending email using your personal ISP, your email provider might already know your credentials.</span></span> <span data-ttu-id="1dabd-183">Po opublikowaniu, może być konieczne przy użyciu innych poświadczeń niż podczas testowania na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1dabd-183">After you publish, you might need to use different credentials than when you test on your local computer.</span></span>
    > - <span data-ttu-id="1dabd-184">Jeśli Twój dostawca e-mail używa szyfrowania, należy ustawić `WebMail.EnableSsl` do `true`.</span><span class="sxs-lookup"><span data-stu-id="1dabd-184">If your email provider uses encryption, you have to set `WebMail.EnableSsl` to `true`.</span></span>
4. <span data-ttu-id="1dabd-185">Uruchom *EmailRequest.cshtml* strony w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="1dabd-185">Run the *EmailRequest.cshtml* page in a browser.</span></span> <span data-ttu-id="1dabd-186">(Upewnij się, że strona jest zaznaczona w **pliki** obszar roboczy przed jej uruchomieniem.)</span><span class="sxs-lookup"><span data-stu-id="1dabd-186">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
5. <span data-ttu-id="1dabd-187">Wprowadź nazwę i opis problemu, a następnie kliknij przycisk **przesyłania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1dabd-187">Enter your name and a problem description, and then click the **Submit** button.</span></span> <span data-ttu-id="1dabd-188">Są przekierowywane do *ProcessRequest.cshtml* strony, który potwierdza wiadomości i które wysyła do Ciebie wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-188">You're redirected to the *ProcessRequest.cshtml* page, which confirms your message and which sends you an email message.</span></span> 

    ![[Obraz]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a><span data-ttu-id="1dabd-190">Wysłanie pliku za pomocą poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="1dabd-190">Sending a File Using Email</span></span>

<span data-ttu-id="1dabd-191">Można również wysłać pliki, które są dołączone do wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-191">You can also send files that are attached to email messages.</span></span> <span data-ttu-id="1dabd-192">W tej procedurze Utwórz plik tekstowy i dwie strony HTML.</span><span class="sxs-lookup"><span data-stu-id="1dabd-192">In this procedure, you create a text file and two HTML pages.</span></span> <span data-ttu-id="1dabd-193">Użyjesz plik jako załącznik wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-193">You'll use the text file as an email attachment.</span></span>

1. <span data-ttu-id="1dabd-194">W witrynie sieci Web, Dodaj nowy plik tekstowy i nadaj mu nazwę *mojplik.txt*.</span><span class="sxs-lookup"><span data-stu-id="1dabd-194">In the website, add a new text file and name it *MyFile.txt*.</span></span>
2. <span data-ttu-id="1dabd-195">Skopiuj poniższy tekst i wklej go w pliku:</span><span class="sxs-lookup"><span data-stu-id="1dabd-195">Copy the following text and paste it in the file:</span></span> 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. <span data-ttu-id="1dabd-196">Utwórz stronę o nazwie *SendFile.cshtml* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="1dabd-196">Create a page named *SendFile.cshtml* and add the following markup:</span></span> 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. <span data-ttu-id="1dabd-197">Utwórz stronę o nazwie *ProcessFile.cshtml* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="1dabd-197">Create a page named *ProcessFile.cshtml* and add the following markup:</span></span> 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. <span data-ttu-id="1dabd-198">Modyfikowanie powiązanych ustawień w kodzie w przykładzie poczty e-mail następujące:</span><span class="sxs-lookup"><span data-stu-id="1dabd-198">Modify the following email related settings in the code from the example:</span></span>

    - <span data-ttu-id="1dabd-199">Ustaw `your-SMTP-host` na nazwę serwera SMTP, który ma dostęp do.</span><span class="sxs-lookup"><span data-stu-id="1dabd-199">Set `your-SMTP-host` to the name of an SMTP server that you have access to.</span></span>
    - <span data-ttu-id="1dabd-200">Ustaw `your-user-name-here` do nazwy użytkownika dla konta serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-200">Set `your-user-name-here` to the user name for your SMTP server account.</span></span>
    - <span data-ttu-id="1dabd-201">Ustaw `your-email-address-here` na adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-201">Set `your-email-address-here` to your own email address.</span></span> <span data-ttu-id="1dabd-202">Jest to komunikat jest wysyłany z adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-202">This is the email address that the message is sent from.</span></span>
    - <span data-ttu-id="1dabd-203">Ustaw `your-account-password` hasło dla konta serwera SMTP.</span><span class="sxs-lookup"><span data-stu-id="1dabd-203">Set `your-account-password` to the password for your SMTP server account.</span></span>
    - <span data-ttu-id="1dabd-204">Ustaw `target-email-address-here` na adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="1dabd-204">Set `target-email-address-here` to your own email address.</span></span> <span data-ttu-id="1dabd-205">(Jak przed, czy zwykle wysłać wiadomość e-mail do innej osoby, ale do testowania, możesz go wysłać do siebie).</span><span class="sxs-lookup"><span data-stu-id="1dabd-205">(As before, you'd normally send an email to someone else, but for testing, you can send it to yourself.)</span></span>
6. <span data-ttu-id="1dabd-206">Uruchom *SendFile.cshtml* strony w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="1dabd-206">Run the *SendFile.cshtml* page in a browser.</span></span>
7. <span data-ttu-id="1dabd-207">Wprowadź nazwę, wiersz tematu i nazwę pliku tekstowego, aby dołączyć (*mojplik.txt*).</span><span class="sxs-lookup"><span data-stu-id="1dabd-207">Enter your name, a subject line, and the name of the text file to attach (*MyFile.txt*).</span></span>
8. <span data-ttu-id="1dabd-208">Kliknij przycisk `Submit` przycisku.</span><span class="sxs-lookup"><span data-stu-id="1dabd-208">Click the `Submit` button.</span></span> <span data-ttu-id="1dabd-209">Jak wcześniej, są przekierowywane do *ProcessFile.cshtml* strony, który potwierdza wiadomości i które wysyła do Ciebie wiadomość e-mail z załączony plik.</span><span class="sxs-lookup"><span data-stu-id="1dabd-209">As before, you're redirected to the *ProcessFile.cshtml* page, which confirms your message and which sends you an email message with the attached file.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="1dabd-210">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1dabd-210">Additional Resources</span></span>


- [<span data-ttu-id="1dabd-211">Przewodnik rozwiązywania problemów ze wzorcem ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="1dabd-211">ASP.NET Web Pages (Razor) Troubleshooting Guide</span></span>](https://go.microsoft.com/fwlink/?LinkId=253001)
- [<span data-ttu-id="1dabd-212">Protokół Simple Mail Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="1dabd-212">Simple Mail Transfer Protocol</span></span>](https://msdn.microsoft.com/library/aa480435.aspx)
- [<span data-ttu-id="1dabd-213">Dostosowywanie zachowania całej witryny dla stron sieci Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1dabd-213">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)