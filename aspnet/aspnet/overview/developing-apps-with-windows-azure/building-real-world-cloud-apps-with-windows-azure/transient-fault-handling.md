---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: "Wystąpienia błędu przejściowego obsługi (Tworzenie aplikacji w chmurze rzeczywistych z platformy Azure) | Dokumentacja firmy Microsoft"
author: MikeWasson
description: "Kompilowanie rzeczywistych World aplikacje w chmurze z Azure Książka elektroniczna jest oparta na prezentacji opracowane przez Scott Guthrie. Wyjaśniono 13 wzorców i rozwiązań, które może on..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/03/2015
ms.topic: article
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: b743b04789c5e5ebf5ab922cf34a516a16a6d356
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="3bc74-104">Obsługa (Tworzenie aplikacji w chmurze rzeczywistych z platformy Azure) wystąpienia błędu przejściowego</span><span class="sxs-lookup"><span data-stu-id="3bc74-104">Transient Fault Handling (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="3bc74-105">przez [Wasson Jan](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Dykstra niestandardowy](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="3bc74-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="3bc74-106">[Pobieranie napraw projektu](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) lub [Pobierz książkę E](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="3bc74-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="3bc74-107">**Tworzenia rzeczywistych aplikacji w chmurze platformy Azure** Książka elektroniczna opiera się na prezentacji opracowane przez Scott Guthrie.</span><span class="sxs-lookup"><span data-stu-id="3bc74-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="3bc74-108">Wyjaśniono 13 wzorców i wskazówki, które mogą pomóc Ci się pomyślnie, tworzenie aplikacji sieci web dla chmury.</span><span class="sxs-lookup"><span data-stu-id="3bc74-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="3bc74-109">Informacje o Książka elektroniczna, zobacz [pierwszy rozdział](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3bc74-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="3bc74-110">Podczas projektowania aplikacji w chmurze rzeczywistych, jeden czynności, które trzeba myśleć o jest sposób obsługi przerw w działaniu usługi tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="3bc74-110">When you're designing a real world cloud app, one of the things you have to think about is how to handle temporary service interruptions.</span></span> <span data-ttu-id="3bc74-111">Ten problem jest unikatowo ważne w aplikacji w chmurze, ponieważ jesteś tak zależny od połączenia sieciowego i usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-111">This issue is uniquely important in cloud apps because you're so dependent on network connections and external services.</span></span> <span data-ttu-id="3bc74-112">Często można uzyskać małego błędami występującymi, które są zazwyczaj samonaprawiania i jeśli nie jest przygotowany do obsługi inteligentnie, będzie skutkować zły środowisko w dla klientów.</span><span class="sxs-lookup"><span data-stu-id="3bc74-112">You can frequently get little glitches that are typically self-healing, and if you aren't prepared to handle them intelligently, they'll result in a bad experience for your customers.</span></span>

## <a name="causes-of-transient-failures"></a><span data-ttu-id="3bc74-113">Przyczyny błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="3bc74-113">Causes of transient failures</span></span>

<span data-ttu-id="3bc74-114">W środowisku chmury, które można znaleźć, nie powiodło się i usunąć połączenia z bazą danych nastąpić okresowo.</span><span class="sxs-lookup"><span data-stu-id="3bc74-114">In the cloud environment you'll find that failed and dropped database connections happen periodically.</span></span> <span data-ttu-id="3bc74-115">Wynika to z częściowo jest przechodzenia przez więcej usług równoważenia obciążenia w porównaniu do środowiska lokalnego, w której mają bezpośredniego połączenia fizycznego serwera sieci web i serwera bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-115">That's partly because you're going through more load balancers compared to the on-premises environment where your web server and database server have a direct physical connection.</span></span> <span data-ttu-id="3bc74-116">Ponadto czasami w przypadku, gdy użytkownik jest zależna od usługi wielodostępne zobaczysz wywołania get service wolniej lub upłynął limit czasu ponieważ ktoś inny, który korzysta z usługi jest naciśnięcie silnie.</span><span class="sxs-lookup"><span data-stu-id="3bc74-116">Also, sometimes when you're dependent on a multi-tenant service you'll see calls to the service get slower or time out because someone else who uses the service is hitting it heavily.</span></span> <span data-ttu-id="3bc74-117">W innych przypadkach może być użytkownik, który jest zbyt często naciśnięcie usługi, a usługa celowo ogranicza możesz — nie zezwala na połączenia — Aby uniknąć negatywnego wpływu na innych dzierżaw usługi.</span><span class="sxs-lookup"><span data-stu-id="3bc74-117">In other cases you might be the user who is hitting the service too frequently, and the service deliberately throttles you – denies connections – in order to prevent you from adversely affecting other tenants of the service.</span></span>

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a><span data-ttu-id="3bc74-118">Użyj inteligentne logiki ponawiania/wycofania celu złagodzenia skutków błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="3bc74-118">Use smart retry/back-off logic to mitigate the effect of transient failures</span></span>

<span data-ttu-id="3bc74-119">Zamiast generowania wyjątku i wyświetlanie nie jest dostępna lub błąd strony do klienta, może rozpoznać błędów, które mają zwykle charakter przejściowy, i automatycznie ponów próbę wykonania operacji, które spowodowały błąd, w nadzieję który przed długo będzie pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3bc74-119">Instead of throwing an exception and displaying a not available or error page to your customer, you can recognize errors that are typically transient, and automatically retry the operation that resulted in the error, in hopes that before long you'll be successful.</span></span> <span data-ttu-id="3bc74-120">W większości przypadków operacji powiedzie się w drugim spróbuj i będzie można odzyskać z błąd bez klientów mających dotąd pamiętać, że wystąpił problem.</span><span class="sxs-lookup"><span data-stu-id="3bc74-120">Most of the time the operation will succeed on the second try, and you'll recover from the error without the customer ever having been aware that there was a problem.</span></span>

<span data-ttu-id="3bc74-121">Istnieje kilka metod, które można zaimplementować Logika ponawiania inteligentne.</span><span class="sxs-lookup"><span data-stu-id="3bc74-121">There are several ways you can implement smart retry logic.</span></span>

- <span data-ttu-id="3bc74-122">Microsoft Patterns &amp; grupa rozwiązań ma [bloku aplikacji obsługi błędów przejściowych](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) wykonuje wszystko dla Ciebie Jeśli używasz ADO.NET dla dostępu do bazy danych SQL (nie za pośrednictwem programu Entity Framework).</span><span class="sxs-lookup"><span data-stu-id="3bc74-122">The Microsoft Patterns &amp; Practices group has a [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) that does everything for you if you're using ADO.NET for SQL Database access (not through Entity Framework).</span></span> <span data-ttu-id="3bc74-123">Wystarczy ustawić zasady dla ponownych prób — ile razy, aby ponowić próbę wykonania kwerendy lub polecenia i jak długo czekać między prób — a zawijania programu SQL kodu w *przy użyciu* bloku.</span><span class="sxs-lookup"><span data-stu-id="3bc74-123">You just set a policy for retries – how many times to retry a query or command and how long to wait between tries – and wrap your SQL code in a *using* block.</span></span>

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    <span data-ttu-id="3bc74-124">Obsługuje również TFH [pamięci podręcznej na roli Azure](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) i [usługi Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="3bc74-124">TFH also supports [Azure In-Role Cache](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) and [Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span>
- <span data-ttu-id="3bc74-125">Korzystając z programu Entity Framework zwykle nie są pracy bezpośrednio z połączeniami SQL, więc nie można użyć tego pakietu wzorców i rozwiązania, ale Entity Framework 6 kompilacje tego rodzaju Logika ponawiania bezpośrednio w ramach.</span><span class="sxs-lookup"><span data-stu-id="3bc74-125">When you use the Entity Framework you typically aren't working directly with SQL connections, so you can't use this Patterns and Practices package, but Entity Framework 6 builds this kind of retry logic right into the framework.</span></span> <span data-ttu-id="3bc74-126">W podobny sposób określić strategii ponownych prób, a następnie EF używa tej strategii zawsze, gdy uzyskuje dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-126">In a similar way you specify the retry strategy, and then EF uses that strategy whenever it accesses the database.</span></span>

    <span data-ttu-id="3bc74-127">Aby użyć tej funkcji w aplikacji rozwiązać, musimy wykonać jest dodać klasę pochodzącą z *DbConfiguration* i Włącz logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="3bc74-127">To use this feature in the Fix It app, all we have to do is add a class that derives from *DbConfiguration* and turn on the retry logic.</span></span>

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    <span data-ttu-id="3bc74-128">Wyjątki bazy danych SQL, identyfikujące w ramach jako błędy zwykle charakter przejściowy kodem przedstawionym nakazuje EF do maksymalnie 3 razy, ponów operację z wykładniczego wycofywania opóźnienia między ponownych prób i maksymalne opóźnienie 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="3bc74-128">For SQL Database exceptions that the framework identifies as typically transient errors, the code shown instructs EF to retry the operation up to 3 times, with an exponential back-off delay between retries, and a maximum delay of 5 seconds.</span></span> <span data-ttu-id="3bc74-129">Wykładniczej wycofania oznacza, że po każdym nie powiodło się ponownej próbie go będzie oczekiwał na dłuższy okres czasu przed podjęciem ponownej próby.</span><span class="sxs-lookup"><span data-stu-id="3bc74-129">Exponential back-off means that after each failed retry it will wait for a longer period of time before trying again.</span></span> <span data-ttu-id="3bc74-130">W przypadku awarii trzech prób w wierszu, zgłosi wyjątek.</span><span class="sxs-lookup"><span data-stu-id="3bc74-130">If three tries in a row fail, it will throw an exception.</span></span> <span data-ttu-id="3bc74-131">Poniższej sekcji o podziałów obwodu wyjaśnia, dlaczego chcesz wykładniczej wycofania i ograniczoną liczbę ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="3bc74-131">The following section about circuit breakers explains why you want exponential back-off and a limited number of retries.</span></span>

    <span data-ttu-id="3bc74-132">Może utrzymać podobne problemy, jeśli używasz usługi Azure Storage, zgodnie z aplikacji Usuń nie dla obiektów blob i interfejsu API programu .NET magazynu klienta już implementuje ten sam rodzaj logiki.</span><span class="sxs-lookup"><span data-stu-id="3bc74-132">You can have similar issues when you're using the Azure Storage service, as the Fix It app does for Blobs, and the .NET storage client API already implements the same kind of logic.</span></span> <span data-ttu-id="3bc74-133">Wystarczy określić zasady ponawiania lub jeszcze nie masz to zrobić w przypadku modyfikowania ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-133">You just specify the retry policy, or you don't even have to do that if you're happy with the default settings.</span></span>

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a><span data-ttu-id="3bc74-134">Podziałów obwodu</span><span class="sxs-lookup"><span data-stu-id="3bc74-134">Circuit breakers</span></span>

<span data-ttu-id="3bc74-135">Istnieje kilka przyczyn, dlaczego nie chcesz, aby ponowić próbę zbyt wiele razy za pośrednictwem zbyt długiego okresu:</span><span class="sxs-lookup"><span data-stu-id="3bc74-135">There are several reasons why you don't want to retry too many times over too long a period:</span></span>

- <span data-ttu-id="3bc74-136">Za dużo użytkowników trwale ponawianie żądań zakończonych niepowodzeniem może zostać obniżona obsługi innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3bc74-136">Too many users persistently retrying failed requests might degrade other users' experience.</span></span> <span data-ttu-id="3bc74-137">Jeśli miliony osób są wszystkie wprowadzeniem powtarzane ponawiania żądań może być zajmowania kolejki wysyłania usług IIS i uniemożliwia obsługę żądań, które go w przeciwnym razie może obsłużyć pomyślnie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bc74-137">If millions of people are all making repeated retry requests you could be tying up IIS dispatch queues and preventing your app from servicing requests that it otherwise could handle successfully.</span></span>
- <span data-ttu-id="3bc74-138">Jeśli ponawia Wszyscy z powodu błędu usługi może być tak wiele żądań w kolejce Usługa pobiera rozpływową, podczas jej uruchamiania odzyskać.</span><span class="sxs-lookup"><span data-stu-id="3bc74-138">If everyone is retrying due to a service failure, there could be so many requests queued up that the service gets flooded when it starts to recover.</span></span>
- <span data-ttu-id="3bc74-139">Jeśli istnieje okno czasu usługa używa do ograniczania jest błąd z powodu dławienia, ciągłego ponownych prób można Przenieś okno i spowodować, ograniczenie kontynuować.</span><span class="sxs-lookup"><span data-stu-id="3bc74-139">If the error is due to throttling and there's a window of time the service uses for throttling, continued retries could move that window out and cause the throttling to continue.</span></span>
- <span data-ttu-id="3bc74-140">Konieczne może być użytkownikiem oczekiwanie na stronie sieci web do renderowania.</span><span class="sxs-lookup"><span data-stu-id="3bc74-140">You might have a user waiting for a web page to render.</span></span> <span data-ttu-id="3bc74-141">Wprowadzania osób oczekiwania zbyt długo może więcej irytujących tego stosunkowo szybko udzielanie porad je, aby spróbować ponownie później.</span><span class="sxs-lookup"><span data-stu-id="3bc74-141">Making people wait too long might be more annoying that relatively quickly advising them to try again later.</span></span>

<span data-ttu-id="3bc74-142">Wykładniczej wycofania rozwiązuje część tego problemu przez ograniczenie częstotliwości ponownych prób, które usługi można uzyskać z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3bc74-142">Exponential back-off addresses some of these issue by limiting the frequency of retries a service can get from your application.</span></span> <span data-ttu-id="3bc74-143">Ale również musi być *podziałów obwodu*: oznacza to, że w pewnym ponów próg aplikacji zatrzymuje ponawianie próby i przejście innych działań, takich jak jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="3bc74-143">But you also need to have *circuit breakers*: this means that at a certain retry threshold your app stops retrying and takes some other action, such as one of the following:</span></span>

- <span data-ttu-id="3bc74-144">Niestandardowe rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="3bc74-144">Custom fallback.</span></span> <span data-ttu-id="3bc74-145">Jeśli nie można pobrać giełdowy z Reuters, może być możesz pobrać go z Bloomberg; lub jeśli nie można pobrać danych z bazy danych, może być możesz pobrać go z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3bc74-145">If you can't get a stock price from Reuters, maybe you can get it from Bloomberg; or if you can't get data from the database, maybe you can get it from cache.</span></span>
- <span data-ttu-id="3bc74-146">Nie w trybie dyskretnym.</span><span class="sxs-lookup"><span data-stu-id="3bc74-146">Fail silent.</span></span> <span data-ttu-id="3bc74-147">Jeśli potrzebujesz z usługi nie jest all-or-nothing dla aplikacji, po prostu zwracanie wartości null nie można pobrać danych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-147">If what you need from a service isn't all-or-nothing for your app, just return null when you can't get the data.</span></span> <span data-ttu-id="3bc74-148">Jeśli wyświetlasz zadania napraw go, a usługa Blob nie odpowiada, można wyświetlić szczegóły zadania bez obrazu.</span><span class="sxs-lookup"><span data-stu-id="3bc74-148">If you're displaying a Fix It task and the Blob service isn't responding, you could display the task details without the image.</span></span>
- <span data-ttu-id="3bc74-149">Szybko się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3bc74-149">Fail fast.</span></span> <span data-ttu-id="3bc74-150">Błąd użytkownika, aby uniknąć przepełnienia usługę za pomocą ponów próbę wykonania żądania, które mogą powodować zakłócenia dla innych użytkowników lub rozszerzyć okna ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="3bc74-150">Error out the user to avoid flooding the service with retry requests which could cause service disruption for other users or extend a throttling window.</span></span> <span data-ttu-id="3bc74-151">Można wyświetlić przyjazny komunikat ". Spróbuj ponownie później".</span><span class="sxs-lookup"><span data-stu-id="3bc74-151">You can display a friendly "try again later" message.</span></span>

<span data-ttu-id="3bc74-152">Nie ma żadnych zasad ponawiania rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="3bc74-152">There is no one-size-fits-all retry policy.</span></span> <span data-ttu-id="3bc74-153">Można ponowić próbę więcej razy, a następnie zaczekaj już w procesie roboczym asynchroniczne tła niż w przypadku w aplikacji sieci web synchronicznego, gdy użytkownik jest oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="3bc74-153">You can retry more times and wait longer in an asynchronous background worker process than you would in a synchronous web app where a user is waiting for a response.</span></span> <span data-ttu-id="3bc74-154">Można poczekać już między kolejnymi próbami usługa relacyjnej bazy danych niż w przypadku dla usługi pamięć podręczna.</span><span class="sxs-lookup"><span data-stu-id="3bc74-154">You can wait longer between retries for a relational database service than you would for a cache service.</span></span> <span data-ttu-id="3bc74-155">Poniżej przedstawiono niektóre przykładowe zalecane ponów zasady dają pogląd, jak numery mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="3bc74-155">Here are some sample recommended retry policies to give you an idea of how the numbers might vary.</span></span> <span data-ttu-id="3bc74-156">("Fast pierwszy" oznacza brak opóźnienia przed pierwszym ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="3bc74-156">("Fast First" means no delay before the first retry.</span></span>

![Zasady ponawiania próbki](transient-fault-handling/_static/image1.png)

<span data-ttu-id="3bc74-158">Wskazówki zasady ponawiania bazy danych SQL, zobacz [Rozwiązywanie błędów przejściowych i błędów połączenia bazy danych SQL](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/).</span><span class="sxs-lookup"><span data-stu-id="3bc74-158">For SQL Database retry policy guidance, see [Troubleshoot transient faults and connection errors to SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/).</span></span>

## <a name="summary"></a><span data-ttu-id="3bc74-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3bc74-159">Summary</span></span>

<span data-ttu-id="3bc74-160">Ponów próbę/wycofania strategii może sprawić, że tymczasowe błędy niewidoczne do odbiorcy w większości przypadków i firma Microsoft udostępnia struktury, których można zminimalizować pracy realizację strategii, czy używasz ADO.NET Entity Framework i platformy Azure Usługa magazynu.</span><span class="sxs-lookup"><span data-stu-id="3bc74-160">A retry/back-off strategy can help make temporary errors invisible to the customer most of the time, and Microsoft provides frameworks that you can use to minimize your work implementing a strategy whether you're using ADO.NET, Entity Framework, or the Azure Storage service.</span></span>

<span data-ttu-id="3bc74-161">W [następnego rozdziału](distributed-caching.md), wyjaśniono, jak poprawić wydajność i niezawodność przy użyciu rozproszonej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3bc74-161">In the [next chapter](distributed-caching.md), we'll look at how to improve performance and reliability by using distributed caching.</span></span>

## <a name="resources"></a><span data-ttu-id="3bc74-162">Resources</span><span class="sxs-lookup"><span data-stu-id="3bc74-162">Resources</span></span>

<span data-ttu-id="3bc74-163">Aby uzyskać więcej informacji, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="3bc74-163">For more information, see the following resources:</span></span>

<span data-ttu-id="3bc74-164">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="3bc74-164">Documentation</span></span>

- <span data-ttu-id="3bc74-165">[Najlepsze rozwiązania dotyczące projektowania usług na dużą skalę na usług w chmurze Azure](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc74-165">[Best Practices for the Design of Large-Scale Services on Azure Cloud Services](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx).</span></span> <span data-ttu-id="3bc74-166">Oficjalny dokument przez moduły SIMM znaku i Michael Thomassy.</span><span class="sxs-lookup"><span data-stu-id="3bc74-166">White paper by Mark Simms and Michael Thomassy.</span></span> <span data-ttu-id="3bc74-167">Podobnie jak seria przed uszkodzeniami, ale przechodzi w szczegółowe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="3bc74-167">Similar to the Failsafe series but goes into more how-to details.</span></span> <span data-ttu-id="3bc74-168">Zobacz sekcję Telemetrii i informacji diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="3bc74-168">See the Telemetry and Diagnostics section.</span></span>
- <span data-ttu-id="3bc74-169">[Przed uszkodzeniami: Wskazówki dotyczące architektury chmury odporność](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc74-169">[Failsafe: Guidance for Resilient Cloud Architectures](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx).</span></span> <span data-ttu-id="3bc74-170">Oficjalny dokument Mercuri wytłoków, Ulrich Homann i Andrew Townhill.</span><span class="sxs-lookup"><span data-stu-id="3bc74-170">White paper by Marc Mercuri, Ulrich Homann, and Andrew Townhill.</span></span> <span data-ttu-id="3bc74-171">Wersja strony sieci Web seria filmów przed uszkodzeniami.</span><span class="sxs-lookup"><span data-stu-id="3bc74-171">Web page version of the FailSafe video series.</span></span>
- <span data-ttu-id="3bc74-172">[Microsoft Patterns and Practices - Azure wskazówki](https://msdn.microsoft.com/library/dn568099.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc74-172">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="3bc74-173">Zobacz ponawiania wzorzec, wzorzec przełożonego agenta harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="3bc74-173">See Retry pattern, Scheduler Agent Supervisor pattern.</span></span>
- <span data-ttu-id="3bc74-174">[Odporność na uszkodzenia w bazie danych Azure SQL](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc74-174">[Fault-tolerance in Azure SQL Database](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx).</span></span> <span data-ttu-id="3bc74-175">Wpis w blogu przez Tony Petrossian.</span><span class="sxs-lookup"><span data-stu-id="3bc74-175">Blog post by Tony Petrossian.</span></span>
- <span data-ttu-id="3bc74-176">[Entity Framework - połączenia odporności / Logika ponawiania próby](https://msdn.microsoft.com/data/dn456835).</span><span class="sxs-lookup"><span data-stu-id="3bc74-176">[Entity Framework - Connection Resiliency / Retry Logic](https://msdn.microsoft.com/data/dn456835).</span></span> <span data-ttu-id="3bc74-177">Jak używać i dostosować błędu przejściowego obsługi funkcji programu Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="3bc74-177">How to use and customize the transient fault handling feature of Entity Framework 6.</span></span>
- <span data-ttu-id="3bc74-178">[Elastyczność połączenia i przechwytywaniu polecenia Entity Framework w aplikacji platformy ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span><span class="sxs-lookup"><span data-stu-id="3bc74-178">[Connection Resiliency and Command Interception with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="3bc74-179">Czwarty w serii dziewięć części samouczka przedstawiono sposób ustawienia odporności funkcji Połączenia programów EF 6 dla bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="3bc74-179">Fourth in a nine-part tutorial series, shows how to set up the EF 6 connection resilience feature for SQL Database.</span></span>

<span data-ttu-id="3bc74-180">Wideo</span><span class="sxs-lookup"><span data-stu-id="3bc74-180">Videos</span></span>

- <span data-ttu-id="3bc74-181">[Przed uszkodzeniami: Tworzenie usługi w chmurze skalowalności, odporności](https://channel9.msdn.com/Series/FailSafe).</span><span class="sxs-lookup"><span data-stu-id="3bc74-181">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="3bc74-182">Seria dziewięć części Ulrich Homann, Mercuri wytłoków i moduły SIMM znaku.</span><span class="sxs-lookup"><span data-stu-id="3bc74-182">Nine-part series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="3bc74-183">Przedstawia informacje o szczegółowo pojęcia i architektury zasad w sposób bardzo dostępny i interesujące z wątków z doświadczenia zespół Advisory klienta firmy Microsoft (CAT) z konkretnymi klientami.</span><span class="sxs-lookup"><span data-stu-id="3bc74-183">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="3bc74-184">Zawiera omówienie podziałów obwód w epizodu 3, zaczynając od 40:55.</span><span class="sxs-lookup"><span data-stu-id="3bc74-184">See the discussion of circuit breakers in episode 3 starting at 40:55.</span></span>
- <span data-ttu-id="3bc74-185">[Kompilowanie Big: Wnioski uzyskane od klientów platformy Azure — część II](https://channel9.msdn.com/Events/Build/2012/3-030).</span><span class="sxs-lookup"><span data-stu-id="3bc74-185">[Building Big: Lessons learned from Azure customers - Part II](https://channel9.msdn.com/Events/Build/2012/3-030).</span></span> <span data-ttu-id="3bc74-186">Moduły SIMM znacznik omówiono projektowania dla błędu przejściowego odporność obsługi i wszystkie instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="3bc74-186">Mark Simms talks about designing for failure, transient fault handling, and instrumenting everything.</span></span>

<span data-ttu-id="3bc74-187">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="3bc74-187">Code sample</span></span>

- <span data-ttu-id="3bc74-188">[Podstawy usługi na platformie Azure w chmurze](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="3bc74-188">[Cloud Service Fundamentals in Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="3bc74-189">Przykładowa aplikacja utworzone przez Microsoft Azure zespół doradczy klientów który demonstruje sposób użycia [Enterprise biblioteki przejściowy błąd obsługi bloku](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH).</span><span class="sxs-lookup"><span data-stu-id="3bc74-189">Sample application created by the Microsoft Azure Customer Advisory Team that demonstrates how to use the [Enterprise Library Transient Fault Handling Block](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH).</span></span> <span data-ttu-id="3bc74-190">Aby uzyskać więcej informacji, zobacz [chmury usługi podstawy Warstwa dostępu do danych — Obsługa błędów przejściowych](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bc74-190">For more information, see [Cloud Service Fundamentals Data Access Layer – Transient Fault Handling](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx).</span></span> <span data-ttu-id="3bc74-191">TFH jest zalecane dla dostępu do bazy danych za pomocą ADO.NET bezpośrednio (bez użycia programu Entity Framework).</span><span class="sxs-lookup"><span data-stu-id="3bc74-191">TFH is recommended for database access using ADO.NET directly (without using Entity Framework).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="3bc74-192">[Poprzednie](monitoring-and-telemetry.md)
[dalej](distributed-caching.md)</span><span class="sxs-lookup"><span data-stu-id="3bc74-192">[Previous](monitoring-and-telemetry.md)
[Next](distributed-caching.md)</span></span>