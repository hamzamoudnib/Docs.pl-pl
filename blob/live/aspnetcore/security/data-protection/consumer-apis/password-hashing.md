---
title: "Tworzenia skrótu hasła"
author: rick-anderson
description: "Tym dokumencie wyjaśniono, jak skrótu hasła przy użyciu platformy ASP.NET Core interfejsy API ochrony danych."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/password-hashing
ms.openlocfilehash: e97d17b5f6de2e0ddcde6d51618675388b43911a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2018
---
# <a name="password-hashing"></a><span data-ttu-id="2aba9-103">Tworzenia skrótu hasła</span><span class="sxs-lookup"><span data-stu-id="2aba9-103">Password Hashing</span></span>

<span data-ttu-id="2aba9-104">Bazy danych ochrony kodu zawiera pakiet *Microsoft.AspNetCore.Cryptography.KeyDerivation* zawierającą funkcje kryptograficzne klucza pochodnego.</span><span class="sxs-lookup"><span data-stu-id="2aba9-104">The data protection code base includes a package *Microsoft.AspNetCore.Cryptography.KeyDerivation* which contains cryptographic key derivation functions.</span></span> <span data-ttu-id="2aba9-105">Ten pakiet jest składnikiem autonomiczny, nie ma żadnych zależności w pozostałej części systemu ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="2aba9-105">This package is a standalone component and has no dependencies on the rest of the data protection system.</span></span> <span data-ttu-id="2aba9-106">Można całkowicie niezależnie.</span><span class="sxs-lookup"><span data-stu-id="2aba9-106">It can be used completely independently.</span></span> <span data-ttu-id="2aba9-107">Źródło istnieje równolegle z podstawowej jako udogodnienie kod ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="2aba9-107">The source exists alongside the data protection code base as a convenience.</span></span>

<span data-ttu-id="2aba9-108">Pakiet zawiera obecnie metody `KeyDerivation.Pbkdf2` umożliwiającą tworzenie skrótu hasła przy użyciu [algorytm PBKDF2](https://tools.ietf.org/html/rfc2898#section-5.2).</span><span class="sxs-lookup"><span data-stu-id="2aba9-108">The package currently offers a method `KeyDerivation.Pbkdf2` which allows hashing a password using the [PBKDF2 algorithm](https://tools.ietf.org/html/rfc2898#section-5.2).</span></span> <span data-ttu-id="2aba9-109">Ten interfejs API jest bardzo podobne do istniejących .NET Framework [Rfc2898DeriveBytes typu](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), ale istnieją trzy ważne różnice:</span><span class="sxs-lookup"><span data-stu-id="2aba9-109">This API is very similar to the .NET Framework's existing [Rfc2898DeriveBytes type](https://docs.microsoft.com/dotnet/api/system.security.cryptography.rfc2898derivebytes), but there are three important distinctions:</span></span>

1. <span data-ttu-id="2aba9-110">`KeyDerivation.Pbkdf2` Metoda obsługuje korzystanie z wielu PRFs (obecnie `HMACSHA1`, `HMACSHA256`, i `HMACSHA512`), podczas gdy `Rfc2898DeriveBytes` obsługuje tylko typ `HMACSHA1`.</span><span class="sxs-lookup"><span data-stu-id="2aba9-110">The `KeyDerivation.Pbkdf2` method supports consuming multiple PRFs (currently `HMACSHA1`, `HMACSHA256`, and `HMACSHA512`), whereas the `Rfc2898DeriveBytes` type only supports `HMACSHA1`.</span></span>

2. <span data-ttu-id="2aba9-111">`KeyDerivation.Pbkdf2` Metody wykrywa bieżący system operacyjny i próbuje wybierz najbardziej zoptymalizowanego wdrożenia standardowego, zapewniając dużo wyższą wydajność w pewnych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="2aba9-111">The `KeyDerivation.Pbkdf2` method detects the current operating system and attempts to choose the most optimized implementation of the routine, providing much better performance in certain cases.</span></span> <span data-ttu-id="2aba9-112">(W systemie Windows 8 zapewnia około 10 x przepływność `Rfc2898DeriveBytes`.)</span><span class="sxs-lookup"><span data-stu-id="2aba9-112">(On Windows 8, it offers around 10x the throughput of `Rfc2898DeriveBytes`.)</span></span>

3. <span data-ttu-id="2aba9-113">`KeyDerivation.Pbkdf2` Metoda wymaga obiekt wywołujący, aby określić wszystkie parametry (soli, PRF i liczby iteracji).</span><span class="sxs-lookup"><span data-stu-id="2aba9-113">The `KeyDerivation.Pbkdf2` method requires the caller to specify all parameters (salt, PRF, and iteration count).</span></span> <span data-ttu-id="2aba9-114">`Rfc2898DeriveBytes` Typu zapewnia te wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="2aba9-114">The `Rfc2898DeriveBytes` type provides default values for these.</span></span>

[!code-csharp[Main](password-hashing/samples/passwordhasher.cs)]

<span data-ttu-id="2aba9-115">Zobacz kod źródłowy dla tożsamości ASP.NET Core `PasswordHasher` typ, do rzeczywistych przypadek użycia.</span><span class="sxs-lookup"><span data-stu-id="2aba9-115">See the source code for ASP.NET Core Identity's `PasswordHasher` type for a real-world use case.</span></span>