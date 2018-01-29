---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: "Za pomocą suwaka z automatycznego odświeżania strony (C#) | Dokumentacja firmy Microsoft"
author: wenz
description: "Kontrolka suwaka w zestawie narzędzi kontroli AJAX zapewnia graficznego suwaka, które można zmieniać za pomocą myszy. Istnieje możliwość automatycznie Księguj suwaka..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: f6291f4162b3069a6316a60b4b29f82f55121aac
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2017
---
<a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="9e59c-104">Za pomocą suwaka z automatycznego odświeżania strony (C#)</span><span class="sxs-lookup"><span data-stu-id="9e59c-104">Using the Slider Control With Auto-Postback (C#)</span></span>
====================
<span data-ttu-id="9e59c-105">przez [Wenz Chrześcijańskie](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="9e59c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="9e59c-106">[Pobierz kod](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) lub [pobierania plików PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="9e59c-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="9e59c-107">Kontrolka suwaka w zestawie narzędzi kontroli AJAX zapewnia graficznego suwaka, które można zmieniać za pomocą myszy.</span><span class="sxs-lookup"><span data-stu-id="9e59c-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="9e59c-108">Istnieje możliwość zmiany autopostback suwaka po jego wartość.</span><span class="sxs-lookup"><span data-stu-id="9e59c-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="9e59c-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9e59c-109">Overview</span></span>

<span data-ttu-id="9e59c-110">Kontrolka suwaka w zestawie narzędzi kontroli AJAX zapewnia graficznego suwaka, które można zmieniać za pomocą myszy.</span><span class="sxs-lookup"><span data-stu-id="9e59c-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="9e59c-111">Istnieje możliwość zmiany autopostback suwaka po jego wartość.</span><span class="sxs-lookup"><span data-stu-id="9e59c-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="9e59c-112">Kroki</span><span class="sxs-lookup"><span data-stu-id="9e59c-112">Steps</span></span>

<span data-ttu-id="9e59c-113">W celu suwak automatycznego odświeżania strony na zmianę, obu polach tekstowych wymagają atrybutu `AutoPostBack="true"`: pola tekstowego, który ma zostać suwak sam i pola tekstowego, która przechowuje pozycji suwaka.</span><span class="sxs-lookup"><span data-stu-id="9e59c-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="9e59c-114">Oto wymagane znacznika, w tym:</span><span class="sxs-lookup"><span data-stu-id="9e59c-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="9e59c-115">`SliderExtender` Formantu w zestawie narzędzi programu ASP.NET AJAX kontroli przypisuje funkcji suwak w polach tekstowych:</span><span class="sxs-lookup"><span data-stu-id="9e59c-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="9e59c-116">Element label dodatkowe później będzie służyć do poinformowania użytkownika odświeżania strony:</span><span class="sxs-lookup"><span data-stu-id="9e59c-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="9e59c-117">Na koniec `ScriptManager` ładowany formant programu ASP.NET AJAX JavaScript wymagane dla kontroli zestawu narzędzi do pracy:</span><span class="sxs-lookup"><span data-stu-id="9e59c-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="9e59c-118">Teraz suwak jest przesyłanie ponownie; po stronie serwera to zdarzenie może być przechwycono i reagować:</span><span class="sxs-lookup"><span data-stu-id="9e59c-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


<span data-ttu-id="9e59c-119">[![Przesunięcie suwaka wyzwala odświeżania strony](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9e59c-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="9e59c-120">Przesunięcie suwaka wyzwala odświeżania strony ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="9e59c-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>


<span data-ttu-id="9e59c-121">[![Później Data zmiany są zapisywane w etykiecie](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9e59c-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="9e59c-122">Później, Data zmiany są zapisywane w etykiecie ([kliknij, aby wyświetlić obraz w pełnym rozmiarze](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9e59c-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="9e59c-123">Dalej</span><span class="sxs-lookup"><span data-stu-id="9e59c-123">Next</span></span>](databinding-the-slider-control-cs.md)