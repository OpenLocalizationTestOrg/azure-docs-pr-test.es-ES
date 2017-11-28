---
title: "Límites de aaaScheduler y los valores predeterminados"
description: "Límites del programador y valores predeterminados"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="6b892-103">Límites del programador y valores predeterminados</span><span class="sxs-lookup"><span data-stu-id="6b892-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="6b892-104">Aceleradores, valores predeterminados, límites y cuotas de Programador</span><span class="sxs-lookup"><span data-stu-id="6b892-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="6b892-105">Hola x-ms-request-id encabezado</span><span class="sxs-lookup"><span data-stu-id="6b892-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="6b892-106">Cada solicitud realizada contra Hola servicio programador devuelve un encabezado de respuesta denominado**x-ms-request-id**. Este encabezado contiene un valor opaco que identifica de forma única solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="6b892-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="6b892-107">Si una solicitud es constantemente por error y se ha comprobado que Hola está formulada correctamente, puede usar este tooMicrosoft de error de valor tooreport Hola.</span><span class="sxs-lookup"><span data-stu-id="6b892-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="6b892-108">En el informe, incluya el valor de Hola de tiempo aproximado de x-ms-request-id, Hola se realizó dicha solicitud hello, Hola identificador de suscripción de hello, colección de trabajos y trabajo y Hola tipo de operación que Hola solicitud intenta realizar.</span><span class="sxs-lookup"><span data-stu-id="6b892-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b892-109">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6b892-109">See Also</span></span>
 [<span data-ttu-id="6b892-110">¿Qué es Programador?</span><span class="sxs-lookup"><span data-stu-id="6b892-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="6b892-111">Conceptos, terminología y jerarquía de entidades de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6b892-112">Empezar a usar a Scheduler en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="6b892-113">Planes y facturación en Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6b892-114">Referencia de API de REST de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6b892-115">Referencia de cmdlets de PowerShell de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6b892-116">Alta disponibilidad y confiabilidad de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6b892-117">Autenticación de salida de Programador de Azure</span><span class="sxs-lookup"><span data-stu-id="6b892-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

