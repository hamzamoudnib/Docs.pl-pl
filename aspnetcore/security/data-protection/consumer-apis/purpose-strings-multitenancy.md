---
title: "Cel ciągów platformy ASP.NET Core"
author: rick-anderson
description: "W tym dokumencie przedstawiono cel ciąg hierarchii i obsługi wielu dzierżawców w powiązaniu z interfejsami API ochrony danych platformy ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/purpose-strings-multitenancy
ms.openlocfilehash: e7b08df32069cf1243630accda82eb6250594c53
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="purpose-hierarchy-and-multi-tenancy-in-aspnet-core"></a><span data-ttu-id="10a7f-103">Cel hierarchii i obsługi wielu dzierżawców w ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="10a7f-103">Purpose hierarchy and multi-tenancy in ASP.NET Core</span></span>

<span data-ttu-id="10a7f-104">Ponieważ `IDataProtector` jest również niejawnie `IDataProtectionProvider`, celów można połączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="10a7f-104">Since an `IDataProtector` is also implicitly an `IDataProtectionProvider`, purposes can be chained together.</span></span> <span data-ttu-id="10a7f-105">W tym sensie `provider.CreateProtector([ "purpose1", "purpose2" ])` jest odpowiednikiem `provider.CreateProtector("purpose1").CreateProtector("purpose2")`.</span><span class="sxs-lookup"><span data-stu-id="10a7f-105">In this sense, `provider.CreateProtector([ "purpose1", "purpose2" ])` is equivalent to `provider.CreateProtector("purpose1").CreateProtector("purpose2")`.</span></span>

<span data-ttu-id="10a7f-106">Dzięki temu niektóre ciekawe hierarchicznych za pośrednictwem systemu ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="10a7f-106">This allows for some interesting hierarchical relationships through the data protection system.</span></span> <span data-ttu-id="10a7f-107">W przykładzie wcześniejszych [Contoso.Messaging.SecureMessage](purpose-strings.md#data-protection-contoso-purpose), składnik SecureMessage można wywołać `provider.CreateProtector("Contoso.Messaging.SecureMessage")` raz początkowych i zbuforuj wynik do prywatnej `_myProvide` pola.</span><span class="sxs-lookup"><span data-stu-id="10a7f-107">In the earlier example of [Contoso.Messaging.SecureMessage](purpose-strings.md#data-protection-contoso-purpose), the SecureMessage component can call `provider.CreateProtector("Contoso.Messaging.SecureMessage")` once up-front and cache the result into a private `_myProvide` field.</span></span> <span data-ttu-id="10a7f-108">Przyszłe funkcje ochrony można będzie utworzyć za pomocą wywołania `_myProvider.CreateProtector("User: username")`, a te funkcje ochrony mają być używane do zabezpieczania poszczególnych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="10a7f-108">Future protectors can then be created via calls to `_myProvider.CreateProtector("User: username")`, and these protectors would be used for securing the individual messages.</span></span>

<span data-ttu-id="10a7f-109">To również można odwrócić.</span><span class="sxs-lookup"><span data-stu-id="10a7f-109">This can also be flipped.</span></span> <span data-ttu-id="10a7f-110">Należy rozważyć jednej aplikacji logicznej hosty, które można skonfigurować wiele dzierżaw (rozsądne wydaje system CMS) i każdego dzierżawcy z własnym systemem zarządzania uwierzytelniania i stanu.</span><span class="sxs-lookup"><span data-stu-id="10a7f-110">Consider a single logical application which hosts multiple tenants (a CMS seems reasonable), and each tenant can be configured with its own authentication and state management system.</span></span> <span data-ttu-id="10a7f-111">Aplikacja parasola ma jednego dostawcy wzorca i wywołuje `provider.CreateProtector("Tenant 1")` i `provider.CreateProtector("Tenant 2")` własną izolowanego wycinek systemu ochrony danych umożliwiają każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="10a7f-111">The umbrella application has a single master provider, and it calls `provider.CreateProtector("Tenant 1")` and `provider.CreateProtector("Tenant 2")` to give each tenant its own isolated slice of the data protection system.</span></span> <span data-ttu-id="10a7f-112">Dzierżawcy może następnie pochodzi własnych indywidualnych funkcji ochrony na podstawie własnych potrzeb, ale niezależnie od tego, jaką próbują oni nie można utworzyć funkcji ochrony, które powodują kolizję z innymi dzierżawami w systemie.</span><span class="sxs-lookup"><span data-stu-id="10a7f-112">The tenants could then derive their own individual protectors based on their own needs, but no matter how hard they try they cannot create protectors which collide with any other tenant in the system.</span></span> <span data-ttu-id="10a7f-113">Graficznie jest reprezentowane jako poniżej.</span><span class="sxs-lookup"><span data-stu-id="10a7f-113">Graphically, this is represented as below.</span></span>

![Obsługa wielu dzierżawców celów](purpose-strings-multitenancy/_static/purposes-multi-tenancy.png)

>[!WARNING]
> <span data-ttu-id="10a7f-115">Przy założeniu parasola formanty aplikacji, które interfejsy API są dostępne dla poszczególnych dzierżawców i dzierżawcy nie wykonania dowolnego kodu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="10a7f-115">This assumes the umbrella application controls which APIs are available to individual tenants and that tenants cannot execute arbitrary code on the server.</span></span> <span data-ttu-id="10a7f-116">Dzierżawca może uruchomić kod z dowolnego, można wykonują prywatnej odbicia przerwanie gwarancje izolacji, czy można po prostu bezpośrednio odczytywać materiał klucza głównego i pochodzić niezależnie od podkluczy chcą.</span><span class="sxs-lookup"><span data-stu-id="10a7f-116">If a tenant can execute arbitrary code, they could perform private reflection to break the isolation guarantees, or they could just read the master keying material directly and derive whatever subkeys they desire.</span></span>

<span data-ttu-id="10a7f-117">System ochrony danych faktycznie używa sortowania wielu dzierżawców w domyślnej konfiguracji poza pole.</span><span class="sxs-lookup"><span data-stu-id="10a7f-117">The data protection system actually uses a sort of multi-tenancy in its default out-of-the-box configuration.</span></span> <span data-ttu-id="10a7f-118">Domyślnie materiał klucza głównego są przechowywane w folderze profilu konta procesu roboczego użytkownika (lub w rejestrze, dla tożsamości puli aplikacji usług IIS).</span><span class="sxs-lookup"><span data-stu-id="10a7f-118">By default master keying material is stored in the worker process account's user profile folder (or the registry, for IIS application pool identities).</span></span> <span data-ttu-id="10a7f-119">Ale faktycznie dość często, aby używać jednego konta do uruchamiania wielu aplikacji, a w związku z tym te aplikacje pojawiłyby udostępnianie wzorca materiału klucza.</span><span class="sxs-lookup"><span data-stu-id="10a7f-119">But it's actually fairly common to use a single account to run multiple applications, and thus all these applications would end up sharing the master keying material.</span></span> <span data-ttu-id="10a7f-120">Aby rozwiązać ten problem, system ochrony danych automatycznie wstawia identyfikator unikatowy dla poszczególnych aplikacji jako pierwszy element w łańcuchu ogólnego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="10a7f-120">To solve this, the data protection system automatically inserts a unique-per-application identifier as the first element in the overall purpose chain.</span></span> <span data-ttu-id="10a7f-121">Ten cel niejawne służy do [izolowania aplikacji poszczególnych](xref:security/data-protection/configuration/overview#per-application-isolation) od siebie nawzajem skutecznie traktując każdej aplikacji jako taki sam jak powyższy obraz wygląda unikatowy dzierżawy w systemie i proces tworzenia ochrony.</span><span class="sxs-lookup"><span data-stu-id="10a7f-121">This implicit purpose serves to [isolate individual applications](xref:security/data-protection/configuration/overview#per-application-isolation) from one another by effectively treating each application as a unique tenant within the system, and the protector creation process looks identical to the image above.</span></span>