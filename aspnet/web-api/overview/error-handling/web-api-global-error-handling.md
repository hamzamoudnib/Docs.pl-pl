---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: "Globalne obsługi błędów w ASP.NET Web API 2 | Dokumentacja firmy Microsoft"
author: davidmatson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/03/2014
ms.topic: article
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: c593c56ba3d0ee8ebf6dc425408d2c3b91c83f93
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
<a name="global-error-handling-in-aspnet-web-api-2"></a><span data-ttu-id="48ff5-102">Globalne obsługi błędów w ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="48ff5-102">Global Error Handling in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="48ff5-103">przez [Matson Dominik](https://github.com/davidmatson), [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="48ff5-103">by [David Matson](https://github.com/davidmatson), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

<span data-ttu-id="48ff5-104">Obecnie nie istnieje łatwy sposób w interfejsie API sieci Web do logowania się lub globalnie obsługi błędów.</span><span class="sxs-lookup"><span data-stu-id="48ff5-104">Today there's no easy way in Web API to log or handle errors globally.</span></span> <span data-ttu-id="48ff5-105">Niektórych z nieobsługiwanych wyjątków mogą być przetwarzane przez [filtry wyjątków](exception-handling.md), ale liczbę przypadków mogących filtry wyjątków nie może obsłużyć.</span><span class="sxs-lookup"><span data-stu-id="48ff5-105">Some unhandled exceptions can be processed via [exception filters](exception-handling.md), but there are a number of cases that exception filters can't handle.</span></span> <span data-ttu-id="48ff5-106">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="48ff5-106">For example:</span></span>

1. <span data-ttu-id="48ff5-107">Wyjątki generowane z konstruktorami kontrolera.</span><span class="sxs-lookup"><span data-stu-id="48ff5-107">Exceptions thrown from controller constructors.</span></span>
2. <span data-ttu-id="48ff5-108">Wyjątków zgłaszanych przez programy obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="48ff5-108">Exceptions thrown from message handlers.</span></span>
3. <span data-ttu-id="48ff5-109">Wyjątki generowane podczas routingu.</span><span class="sxs-lookup"><span data-stu-id="48ff5-109">Exceptions thrown during routing.</span></span>
4. <span data-ttu-id="48ff5-110">Wyjątki generowane podczas serializacji treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="48ff5-110">Exceptions thrown during response content serialization .</span></span>

<span data-ttu-id="48ff5-111">Chcemy prosty i spójny sposób logowania i (jeśli będzie to możliwe) przekazać te wyjątki.</span><span class="sxs-lookup"><span data-stu-id="48ff5-111">We want to provide a simple, consistent way to log and handle (where possible) these exceptions.</span></span> 

<span data-ttu-id="48ff5-112">Istnieją dwa główne przypadki do obsługi wyjątków, wtedy, gdy możemy wysłać odpowiedź o błędzie i dziennik wyjątku jest przypadek, w którym wszystkie możemy.</span><span class="sxs-lookup"><span data-stu-id="48ff5-112">There are two major cases for handling exceptions, the case where we are able to send an error response and the case where all we can do is log the exception.</span></span> <span data-ttu-id="48ff5-113">Jest przykład drugim przypadku, gdy wyjątek w trakcie przesyłania strumieniowego zawartości odpowiedzi; w takim przypadku jest za późno wysłać nowy komunikat odpowiedzi, ponieważ kod stanu, nagłówki i zawartość częściowa już przeszły przez sieć, dlatego firma Microsoft po prostu przerwać połączenie.</span><span class="sxs-lookup"><span data-stu-id="48ff5-113">An example for the latter case is when an exception is thrown in the middle of streaming response content; in that case it is too late to send a new response message since the status code, headers, and partial content have already gone across the wire, so we simply abort the connection.</span></span> <span data-ttu-id="48ff5-114">Mimo że nie mogą być obsługiwane wyjątek, który zwróci nowy komunikat odpowiedzi, nadal obsługuje się rejestrowania wyjątku.</span><span class="sxs-lookup"><span data-stu-id="48ff5-114">Even though the exception can't be handled to produce a new response message, we still support logging the exception.</span></span> <span data-ttu-id="48ff5-115">W przypadkach, gdy zostanie wykryte, błąd zostanie zwrócona odpowiedź o błędzie odpowiednie jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="48ff5-115">In cases where we can detect an error, we can return an appropriate error response as shown in the following:</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a><span data-ttu-id="48ff5-116">Istniejące opcje</span><span class="sxs-lookup"><span data-stu-id="48ff5-116">Existing Options</span></span>

<span data-ttu-id="48ff5-117">Oprócz [filtry wyjątków](exception-handling.md), [programy obsługi komunikatów](../advanced/http-message-handlers.md) można obecnie przestrzegać wszystkich odpowiedzi na poziomie 500, ale działający na tych odpowiedzi jest trudne, ponieważ mają kontekstu o pierwotnego błędu.</span><span class="sxs-lookup"><span data-stu-id="48ff5-117">In addition to [exception filters](exception-handling.md), [message handlers](../advanced/http-message-handlers.md) can be used today to observe all 500-level responses, but acting on those responses is difficult, as they lack context about the original error.</span></span> <span data-ttu-id="48ff5-118">Programy obsługi wiadomości ma niektóre te same ograniczenia co filtry wyjątków dotyczących przypadków, które może obsłużyć ich. Podczas interfejsu API sieci Web jest Infrastruktura śledzenia, który przechwytuje warunki błędów Infrastruktura śledzenia w celach diagnostycznych i jest nie zaprojektowane lub przeznaczony do uruchamiania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="48ff5-118">Message handlers also have some of the same limitations as exception filters regarding the cases they can handle.While Web API does have tracing infrastructure that captures error conditions the tracing infrastructure is for diagnostics purposes and is not designed or suited for running in production environments.</span></span> <span data-ttu-id="48ff5-119">Globalne wyjątków, obsługa i rejestrowanie powinna być usług, które można uruchomić w środowisku produkcyjnym i być podłączane do istniejących rozwiązań monitorowania (na przykład [ELMAH](https://code.google.com/p/elmah/) ).</span><span class="sxs-lookup"><span data-stu-id="48ff5-119">Global exception handling and logging should be services that can run during production and be plugged into existing monitoring solutions (for example, [ELMAH](https://code.google.com/p/elmah/) ).</span></span>

### <a name="solution-overview"></a><span data-ttu-id="48ff5-120">Omówienie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="48ff5-120">Solution Overview</span></span>

 <span data-ttu-id="48ff5-121">Firma Microsoft udostępnia dwie nowe usługi użytkownik replaceable [interfejsu IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) i IExceptionHandler, aby zalogować się i obsługi nieobsługiwanych wyjątków.</span><span class="sxs-lookup"><span data-stu-id="48ff5-121">We provide two new user-replaceable services, [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) and IExceptionHandler, to log and handle unhandled exceptions.</span></span> <span data-ttu-id="48ff5-122">Usługi są bardzo podobne z dwóch głównych różnic:</span><span class="sxs-lookup"><span data-stu-id="48ff5-122">The services are very similar, with two main differences:</span></span>

1. <span data-ttu-id="48ff5-123">Firma Microsoft obsługuje rejestracji wielu rejestratorów wyjątek, ale tylko jeden wyjątek obsługi.</span><span class="sxs-lookup"><span data-stu-id="48ff5-123">We support registering multiple exception loggers but only a single exception handler.</span></span>
2. <span data-ttu-id="48ff5-124">Wyjątek rejestratorów zawsze uzyskać wywołana, nawet jeśli firma Microsoft zamierzasz przerwać połączenie.</span><span class="sxs-lookup"><span data-stu-id="48ff5-124">Exception loggers always get called, even if we're about to abort the connection.</span></span> <span data-ttu-id="48ff5-125">Tylko programy obsługi wyjątków uzyskać wywoływana, gdy będziemy mogli nadal wybierz które komunikat odpowiedzi do odesłania.</span><span class="sxs-lookup"><span data-stu-id="48ff5-125">Exception handlers only get called when we're still able to choose which response message to send.</span></span>

<span data-ttu-id="48ff5-126">Obie te usługi zapewniają dostęp do kontekstu wyjątku zawierający informacje z punktu, w których wykryto wyjątek, szczególnie [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), zgłoszony wyjątek i wyjątek źródła (szczegóły poniżej).</span><span class="sxs-lookup"><span data-stu-id="48ff5-126">Both services provide access to an exception context containing relevant information from the point where the exception was detected, particularly the [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), the [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), the thrown exception and the exception source (details below).</span></span>

### <a name="design-principles"></a><span data-ttu-id="48ff5-127">Zasady projektowania</span><span class="sxs-lookup"><span data-stu-id="48ff5-127">Design Principles</span></span>

1. <span data-ttu-id="48ff5-128">**Nie zmian, które psuły** , ponieważ ta funkcja jest dodawany w wersji pomocniczej, jest ważne ograniczenia wpływające na rozwiązanie, który nie istnieć żadne zmiany podziału, albo wpisz umów lub w celu zachowania.</span><span class="sxs-lookup"><span data-stu-id="48ff5-128">**No breaking changes** Because this functionality is being added in a minor release, one important constraint impacting the solution is that there be no breaking changes, either to type contracts or to behavior.</span></span> <span data-ttu-id="48ff5-129">To ograniczenie wykluczyć pewne Oczyszczanie chcielibyśmy to zostało zrobione w istniejących bloki catch Włączanie wyjątków w odpowiedzi 500.</span><span class="sxs-lookup"><span data-stu-id="48ff5-129">This constraint ruled out some cleanup we would like to have done in terms of existing catch blocks turning exceptions into 500 responses.</span></span> <span data-ttu-id="48ff5-130">To dodatkowe oczyszczanie jest coś, co możemy warto uwzględnić w kolejnych wersji głównej.</span><span class="sxs-lookup"><span data-stu-id="48ff5-130">This additional cleanup is something we might consider for a subsequent major release.</span></span> <span data-ttu-id="48ff5-131">Jeśli jest to ważne należy oddawać głosy na go w [głos użytkownika ASP.NET Web API](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception).</span><span class="sxs-lookup"><span data-stu-id="48ff5-131">If this is important to you please vote on it at [ASP.NET Web API user voice](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception).</span></span>
2. <span data-ttu-id="48ff5-132">**Zachowaniu spójności z interfejsu API sieci Web tworzy** składnika Web API potoku filtru jest doskonałym sposobem obsługi dotyczy kompleksowymi elastyczność stosowania logikę w zakresie określonych akcji, kontrolera specyficznych lub globalnego.</span><span class="sxs-lookup"><span data-stu-id="48ff5-132">**Maintaining consistency with Web API constructs** Web API's filter pipeline is a great way to handle cross-cutting concerns with the flexibility of applying the logic at an action-specific, controller-specific or global scope.</span></span> <span data-ttu-id="48ff5-133">Filtry, w tym filtry wyjątków zawsze mieć kontekstów akcji i kontrolera, nawet wtedy, gdy zarejestrowana w zakresie globalnym.</span><span class="sxs-lookup"><span data-stu-id="48ff5-133">Filters, including exception filters, always have action and controller contexts, even when registered at the global scope.</span></span> <span data-ttu-id="48ff5-134">Istnieje kontraktu ma sens dla filtrów, że oznacza to, że filtry wyjątków, nawet o zakresie globalnym te nie są dobrze dla niektórych wyjątków, obsługa przypadkach, takich jak wyjątki od obsługi komunikatów, których brak kontekstu akcji lub kontrolera.</span><span class="sxs-lookup"><span data-stu-id="48ff5-134">That contract makes sense for filters, but it means that exception filters, even globally scoped ones, aren't a good fit for some exception handling cases, such as exceptions from message handlers, where no action or controller context exists.</span></span> <span data-ttu-id="48ff5-135">Jeśli chcemy użyć elastyczne zakres zapewnianej przez filtry dla obsługi wyjątków, potrzebujemy jeszcze filtry wyjątków.</span><span class="sxs-lookup"><span data-stu-id="48ff5-135">If we want to use the flexible scoping afforded by filters for exception handling, we still need exception filters.</span></span> <span data-ttu-id="48ff5-136">Ale jeśli trzeba obsłużyć wyjątek poza kontekstu kontrolera, również potrzebujemy konstrukcję oddzielne do obsługi błędów pełnej globalnej (coś bez kontrolera akcji i kontekstu kontekstu ograniczenia).</span><span class="sxs-lookup"><span data-stu-id="48ff5-136">But if we need to handle exception outside of a controller context, we also need a separate construct for full global error handling (something without the controller context and action context constraints).</span></span>

### <a name="when-to-use"></a><span data-ttu-id="48ff5-137">Kiedy używać</span><span class="sxs-lookup"><span data-stu-id="48ff5-137">When to Use</span></span>

- <span data-ttu-id="48ff5-138">Rejestratory wyjątek to rozwiązanie, aby wyświetlać wszystkie nieobsługiwany wyjątek zgłoszony przez interfejs API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="48ff5-138">Exception loggers are the solution to seeing all unhandled exception caught by Web API.</span></span>
- <span data-ttu-id="48ff5-139">Programy obsługi wyjątków są w zakresie dostosowywania wszystkich możliwych odpowiedzi na nieobsługiwanych wyjątków zgłoszony przez interfejs API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="48ff5-139">Exception handlers are the solution for customizing all possible responses to unhandled exceptions caught by Web API.</span></span>
- <span data-ttu-id="48ff5-140">Filtry wyjątków są najlepszym rozwiązaniem dla przetwarzania podzbioru nieobsługiwany wyjątki związane z określonych akcji lub kontrolera.</span><span class="sxs-lookup"><span data-stu-id="48ff5-140">Exception filters are the easiest solution for processing the subset unhandled exceptions related to a specific action or controller.</span></span>

### <a name="service-details"></a><span data-ttu-id="48ff5-141">Szczegóły usługi</span><span class="sxs-lookup"><span data-stu-id="48ff5-141">Service Details</span></span>

 <span data-ttu-id="48ff5-142">Interfejsy usługi rejestrowania i obsługi wyjątków są również metody asynchroniczne proste podjęcia odpowiednich kontekstach:</span><span class="sxs-lookup"><span data-stu-id="48ff5-142">The exception logger and handler service interfaces are simple async methods taking the respective contexts:</span></span> 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 <span data-ttu-id="48ff5-143">Firma Microsoft udostępnia również klasy podstawowe dla obu tych interfejsów.</span><span class="sxs-lookup"><span data-stu-id="48ff5-143">We also provide base classes for both of these interfaces.</span></span> <span data-ttu-id="48ff5-144">Zastępowanie metody core (synchronizacji lub async) jest wszystkie wymagane do logowania lub obsługiwać na zalecanej razy.</span><span class="sxs-lookup"><span data-stu-id="48ff5-144">Overriding the core (sync or async) methods is all that is required to log or handle at the recommended times.</span></span> <span data-ttu-id="48ff5-145">Do rejestrowania, `ExceptionLogger` klasy podstawowej zapewni, że podstawowa metoda rejestrowania jest wywołany tylko raz dla każdego wyjątku (nawet jeśli później propaguje dodatkowo górę stosu wywołań i zostanie przechwycony ponownie).</span><span class="sxs-lookup"><span data-stu-id="48ff5-145">For logging, the `ExceptionLogger` base class will ensure that the core logging method is only called once for each exception (even if it later propagates further up the call stack and is caught again).</span></span> <span data-ttu-id="48ff5-146">`ExceptionHandler` Klasy podstawowej wywoła podstawowej obsługi metody tylko dla wyjątków w górnej części stosu wywołań, ignorowanie starszych zagnieżdżone bloki catch.</span><span class="sxs-lookup"><span data-stu-id="48ff5-146">The `ExceptionHandler` base class will call the core handling method only for exceptions at the top of the call stack, ignoring legacy nested catch blocks.</span></span> <span data-ttu-id="48ff5-147">(Uproszczonej wersji tych klas podstawowych są w dodatku poniżej). Zarówno `IExceptionLogger` i `IExceptionHandler` otrzymywać informacje o wyjątku za pośrednictwem `ExceptionContext`.</span><span class="sxs-lookup"><span data-stu-id="48ff5-147">(Simplified versions of these base classes are in the appendix below.) Both `IExceptionLogger` and `IExceptionHandler` receive information about the exception via an `ExceptionContext`.</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

<span data-ttu-id="48ff5-148">Gdy struktura wywołuje moduł rejestrujący wyjątku lub obsługi wyjątków, zawsze będą zapewniać `Exception` i `Request`.</span><span class="sxs-lookup"><span data-stu-id="48ff5-148">When the framework calls an exception logger or an exception handler, it will always provide an `Exception` and a `Request`.</span></span> <span data-ttu-id="48ff5-149">Z wyjątkiem testy jednostkowe, zawsze będzie ona `RequestContext`.</span><span class="sxs-lookup"><span data-stu-id="48ff5-149">Except for unit testing, it will also always provide a `RequestContext`.</span></span> <span data-ttu-id="48ff5-150">Będzie ona rzadko `ControllerContext` i `ActionContext` (tylko w przypadku wywoływania z bloku catch dla filtry wyjątków).</span><span class="sxs-lookup"><span data-stu-id="48ff5-150">It will rarely provide a `ControllerContext` and `ActionContext` (only when calling from the catch block for exception filters).</span></span> <span data-ttu-id="48ff5-151">Bardzo rzadko zapewni `Response`(tylko w niektórych przypadkach usług IIS, gdy środku do zapisania w odpowiedzi).</span><span class="sxs-lookup"><span data-stu-id="48ff5-151">It will very rarely provide a `Response`(only in certain IIS cases when in the middle of trying to write the response).</span></span> <span data-ttu-id="48ff5-152">Należy pamiętać, że niektóre z tych właściwości może być `null` zależy od użytkownika, aby wyszukać `null` przed uzyskaniem dostępu do członków klasy wyjątku.`CatchBlock`</span><span class="sxs-lookup"><span data-stu-id="48ff5-152">Note that because some of these properties may be `null` it is up to the consumer to check for `null` before accessing members of the exception class.`CatchBlock`</span></span> <span data-ttu-id="48ff5-153">jest ciąg wskazujący, który blok catch był wyświetlany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="48ff5-153">is a string indicating which catch block saw the exception.</span></span> <span data-ttu-id="48ff5-154">Ciągi bloku catch są następujące:</span><span class="sxs-lookup"><span data-stu-id="48ff5-154">The catch block strings are as follows:</span></span>

- <span data-ttu-id="48ff5-155">HttpServer (metoda SendAsync)</span><span class="sxs-lookup"><span data-stu-id="48ff5-155">HttpServer (SendAsync method)</span></span>
- <span data-ttu-id="48ff5-156">HttpControllerDispatcher (metoda SendAsync)</span><span class="sxs-lookup"><span data-stu-id="48ff5-156">HttpControllerDispatcher (SendAsync method)</span></span>
- <span data-ttu-id="48ff5-157">HttpBatchHandler (metoda SendAsync)</span><span class="sxs-lookup"><span data-stu-id="48ff5-157">HttpBatchHandler (SendAsync method)</span></span>
- <span data-ttu-id="48ff5-158">IExceptionFilter (przetwarzanie klasy ApiController w potoku filtru wyjątków w ExecuteAsync)</span><span class="sxs-lookup"><span data-stu-id="48ff5-158">IExceptionFilter (ApiController's processing of the exception filter pipeline in ExecuteAsync)</span></span>
- <span data-ttu-id="48ff5-159">OWIN host:</span><span class="sxs-lookup"><span data-stu-id="48ff5-159">OWIN host:</span></span>

    - <span data-ttu-id="48ff5-160">HttpMessageHandlerAdapter.BufferResponseContentAsync (do buforowania danych wyjściowych)</span><span class="sxs-lookup"><span data-stu-id="48ff5-160">HttpMessageHandlerAdapter.BufferResponseContentAsync (for buffering output)</span></span>
    - <span data-ttu-id="48ff5-161">HttpMessageHandlerAdapter.CopyResponseContentAsync (do strumienia wyjściowego)</span><span class="sxs-lookup"><span data-stu-id="48ff5-161">HttpMessageHandlerAdapter.CopyResponseContentAsync (for streaming output)</span></span>
- <span data-ttu-id="48ff5-162">Host sieci Web:</span><span class="sxs-lookup"><span data-stu-id="48ff5-162">Web host:</span></span>

    - <span data-ttu-id="48ff5-163">HttpControllerHandler.WriteBufferedResponseContentAsync (do buforowania danych wyjściowych)</span><span class="sxs-lookup"><span data-stu-id="48ff5-163">HttpControllerHandler.WriteBufferedResponseContentAsync (for buffering output)</span></span>
    - <span data-ttu-id="48ff5-164">HttpControllerHandler.WriteStreamedResponseContentAsync (do strumienia wyjściowego)</span><span class="sxs-lookup"><span data-stu-id="48ff5-164">HttpControllerHandler.WriteStreamedResponseContentAsync (for streaming output)</span></span>
    - <span data-ttu-id="48ff5-165">HttpControllerHandler.WriteErrorResponseContentAsync (w przypadku awarii w błąd odzyskiwania w trybie buforowane dane wyjściowe)</span><span class="sxs-lookup"><span data-stu-id="48ff5-165">HttpControllerHandler.WriteErrorResponseContentAsync (for failures in error recovery under buffered output mode)</span></span>

<span data-ttu-id="48ff5-166">Lista ciągów bloku catch jest również dostępny za pośrednictwem właściwości statycznego tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="48ff5-166">The list of catch block strings is also available via static readonly properties.</span></span> <span data-ttu-id="48ff5-167">(Ciągu bloku catch core znajdują się na statycznych ExceptionCatchBlocks; pozostałe pojawiają się na jednej klasy statycznej każdego hosta sieci web i OWIN).`IsTopLevelCatchBlock`</span><span class="sxs-lookup"><span data-stu-id="48ff5-167">(The core catch block string are on the static ExceptionCatchBlocks; the remainder appear on one static class each for OWIN and web host).`IsTopLevelCatchBlock`</span></span> <span data-ttu-id="48ff5-168">jest przydatne w przypadku następujących zalecanych wzorzec obsługi wyjątków tylko u góry stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="48ff5-168">is helpful for following the recommended pattern of handling exceptions only at the top of the call stack.</span></span> <span data-ttu-id="48ff5-169">Zamiast włączania wyjątków w odpowiedzi 500, wszędzie tam, gdzie występuje zagnieżdżony blok catch, program obsługi wyjątku pozwolić wyjątki propagację aż do ich temat, aby była widoczna przez hosta.</span><span class="sxs-lookup"><span data-stu-id="48ff5-169">Rather than turning exceptions into 500 responses anywhere a nested catch block occurs, an exception handler can let exceptions propagate until they are about to be seen by the host.</span></span>

<span data-ttu-id="48ff5-170">Oprócz `ExceptionContext`, Rejestrator pobiera jednej więcej informacji za pomocą pełnego `ExceptionLoggerContext`:</span><span class="sxs-lookup"><span data-stu-id="48ff5-170">In addition to the `ExceptionContext`, a logger gets one more piece of information via the full `ExceptionLoggerContext`:</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

<span data-ttu-id="48ff5-171">Drugą właściwością `CanBeHandled`, umożliwia rejestratora do identyfikowania wyjątek, który nie mogą być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="48ff5-171">The second property, `CanBeHandled`, allows a logger to identify an exception that cannot be handled.</span></span> <span data-ttu-id="48ff5-172">Gdy połączenie ma być przerwane i mogą być wysyłane nie nowy komunikat odpowiedzi, rejestratorów zostanie wywołana, ale program obsługi zostanie ***nie*** można wywołać i rejestratorów może zidentyfikować ten scenariusz z tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="48ff5-172">When the connection is about to be aborted and no new response message can be sent, the loggers will be called but the handler will ***not*** be called, and the loggers can identify this scenario from this property.</span></span>

<span data-ttu-id="48ff5-173">W dodatkowej `ExceptionContext`, program obsługi pobiera jeden więcej właściwości można ustawić na pełny `ExceptionHandlerContext` do obsługi wyjątku:</span><span class="sxs-lookup"><span data-stu-id="48ff5-173">In additional to the `ExceptionContext`, a handler gets one more property it can set on the full `ExceptionHandlerContext` to handle the exception:</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

<span data-ttu-id="48ff5-174">Program obsługi wyjątku wskazuje, czy wyjątek jest obsługiwany dzięki ustawieniu `Result` wynik akcji dla właściwości (na przykład [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [ StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx), lub niestandardowy wyników).</span><span class="sxs-lookup"><span data-stu-id="48ff5-174">An exception handler indicates that it has handled an exception by setting the `Result` property to an action result (for example, an [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx), or a custom result).</span></span> <span data-ttu-id="48ff5-175">Jeśli `Result` właściwość ma wartość null, jest nieobsługiwany wyjątek i pierwotny wyjątek zostanie zgłoszony ponownie.</span><span class="sxs-lookup"><span data-stu-id="48ff5-175">If the `Result` property is null, the exception is unhandled and the original exception will be re-thrown.</span></span>

<span data-ttu-id="48ff5-176">Wyjątki w górnej części stosu wywołań Wybraliśmy dodatkowy krok, aby upewnić się, że odpowiedź jest odpowiedni dla wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48ff5-176">For exceptions at the top of the call stack, we took an extra step to ensure the response is appropriate for API callers.</span></span> <span data-ttu-id="48ff5-177">Jeśli wyjątek propaguje do hosta, wywołujący zobaczy żółty ekran lub niektórych innych hostów podane odpowiedzi, który jest zwykle HTML i zazwyczaj nie właściwą odpowiedź błąd interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="48ff5-177">If the exception propagates up to the host, the caller would see the yellow screen of death or some other host provided response which is typically HTML and not usually an appropriate API error response.</span></span> <span data-ttu-id="48ff5-178">W takich przypadkach uruchamia wynik inną niż null i tylko wtedy, gdy jawnie Ustawia program obsługi wyjątku niestandardowych z powrotem do `null` (nieobsługiwany) zostanie wyjątek propagowane do hosta.</span><span class="sxs-lookup"><span data-stu-id="48ff5-178">In these cases, the Result starts out non-null, and only if a custom exception handler explicitly sets it back to `null` (unhandled) will the exception propagate to the host.</span></span> <span data-ttu-id="48ff5-179">Ustawienie `Result` do `null` w takich przypadkach może być przydatne w przypadku dwóch scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="48ff5-179">Setting `Result` to `null` in such cases can be useful for two scenarios:</span></span>

1. <span data-ttu-id="48ff5-180">OWIN hostowana interfejsu API sieci Web, z wyjątkiem niestandardowych obsługi oprogramowania pośredniczącego w zarejestrowany przed/poza interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="48ff5-180">OWIN hosted Web API with custom exception handling middleware registered before/outside Web API.</span></span>
2. <span data-ttu-id="48ff5-181">Debugowanie lokalne za pośrednictwem przeglądarki, gdzie żółty ekran jest rzeczywiście przydatne odpowiedzi na nieobsługiwany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="48ff5-181">Local debugging via a browser, where the yellow screen of death is actually a helpful response for an unhandled exception.</span></span>

<span data-ttu-id="48ff5-182">Rejestratory wyjątków i programy obsługi wyjątków firma Microsoft nie wykonuj żadnych czynności do odzyskania, jeśli Rejestrator lub obsługi samego zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="48ff5-182">For both exception loggers and exception handlers, we don't do anything to recover if the logger or handler itself throws an exception.</span></span> <span data-ttu-id="48ff5-183">(Inne niż co wyjątek propagację, pozostaw opinii u dołu tej strony, jeśli masz lepszym rozwiązaniem.) Kontrakt dla rejestratorów wyjątków i programy obsługi jest czy powinna zezwala wyjątki propagacji do ich wywołań; w przeciwnym razie wyjątek właśnie rozpropaguje, często aż do hosta, co powoduje błąd HTML (na przykład ASP. Ekran żółty przez sieć) są wysyłane do klienta (która zazwyczaj nie jest opcją preferowaną dla wywołań interfejsu API, które JSON lub XML).</span><span class="sxs-lookup"><span data-stu-id="48ff5-183">(Other than letting the exception propagate, leave feedback at the bottom of this page if you have a better approach.) The contract for exception loggers and handlers is that they should not let exceptions propagate up to their callers; otherwise, the exception will just propagate, often all the way to the host resulting in an HTML error (like the ASP.NET's yellow screen) being sent back to the client (which usually isn't the preferred option for API callers that expect JSON or XML).</span></span>

## <a name="examples"></a><span data-ttu-id="48ff5-184">Przykłady</span><span class="sxs-lookup"><span data-stu-id="48ff5-184">Examples</span></span>

### <a name="tracing-exception-logger"></a><span data-ttu-id="48ff5-185">Śledzenie Rejestrator wyjątku</span><span class="sxs-lookup"><span data-stu-id="48ff5-185">Tracing Exception Logger</span></span>

<span data-ttu-id="48ff5-186">Rejestrator wyjątku poniżej wysyłać dane wyjątek do skonfigurowana źródła śledzenia (w tym oknie danych wyjściowych debugowania w programie Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="48ff5-186">The exception logger below send exception data to configured Trace sources (including the Debug output window in Visual Studio).</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a><span data-ttu-id="48ff5-187">Obsługa wyjątków komunikat błędu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="48ff5-187">Custom Error Message Exception Handler</span></span>

<span data-ttu-id="48ff5-188">Następujące poniżej generuje odpowiedzi błędu niestandardowego do klientów, w tym adres e-mail kontaktu z działem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="48ff5-188">The following below produces a custom error response to clients, including an email address for contacting support.</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a><span data-ttu-id="48ff5-189">Rejestrowanie filtry wyjątków</span><span class="sxs-lookup"><span data-stu-id="48ff5-189">Registering Exception Filters</span></span>

<span data-ttu-id="48ff5-190">Użycie szablonu projektu "Platformy ASP.NET MVC 4 aplikacji sieci Web" Aby utworzyć projekt, umieść kod konfiguracji interfejsu API sieci Web wewnątrz `WebApiConfig` klasy w *aplikacji/_uruchom* folderu:</span><span class="sxs-lookup"><span data-stu-id="48ff5-190">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, in the *App/_Start* folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a><span data-ttu-id="48ff5-191">Dodatek: Szczegóły klasy podstawowej</span><span class="sxs-lookup"><span data-stu-id="48ff5-191">Appendix: Base Class Details</span></span>

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]