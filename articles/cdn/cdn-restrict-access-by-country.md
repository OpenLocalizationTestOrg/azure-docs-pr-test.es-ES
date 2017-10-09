---
title: "contenido de CDN de Azure por país aaaRestrict | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorestrict acceso tooyour CDN de Azure contenido con Hola la característica filtrado de replicación geográfica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="dbda5-103">Restricción del contenido de la red CDN de Azure por país</span><span class="sxs-lookup"><span data-stu-id="dbda5-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="dbda5-104">Información general</span><span class="sxs-lookup"><span data-stu-id="dbda5-104">Overview</span></span>
<span data-ttu-id="dbda5-105">Cuando un usuario solicita el contenido, de forma predeterminada, se sirve contenido de hello, independientemente de donde usuario Hola efectúe esta solicitud de.</span><span class="sxs-lookup"><span data-stu-id="dbda5-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="dbda5-106">En algunos casos, puede que desee toorestrict tener acceso al contenido de tooyour por país.</span><span class="sxs-lookup"><span data-stu-id="dbda5-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="dbda5-107">Este tema se explica cómo hello toouse **filtrado geográfica** característica en orden tooconfigure Hola servicio tooallow o bloquear el acceso por país.</span><span class="sxs-lookup"><span data-stu-id="dbda5-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbda5-108">productos de Verizon y Akamai Hola proporcionan Hola la misma funcionalidad de filtrado de replicación geográfica, pero tiene una pequeña diferencia en los códigos de país te admiten.</span><span class="sxs-lookup"><span data-stu-id="dbda5-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="dbda5-109">Vea el paso 3 para un diferencias toohello de vínculo.</span><span class="sxs-lookup"><span data-stu-id="dbda5-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="dbda5-110">Para obtener información acerca de las consideraciones que se aplican tooconfiguring este tipo de restricción, vea hello [consideraciones](cdn-restrict-access-by-country.md#considerations) sección final Hola de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbda5-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Filtrado por país](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="dbda5-112">Paso 1: Definir la ruta de acceso de directorio de Hola</span><span class="sxs-lookup"><span data-stu-id="dbda5-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="dbda5-113">Seleccione el punto de conexión en el portal de Hola y esta característica se encuentra ficha filtrado geográfica de hello en hello toofind de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="dbda5-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="dbda5-114">Al configurar un filtro de país, debe especificar a los usuarios de hello ruta de acceso relativa toohello ubicación toowhich se permitirá o denegará el acceso.</span><span class="sxs-lookup"><span data-stu-id="dbda5-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="dbda5-115">Puede aplicar el filtrado geográfico para todos los archivos mediante "/" o carpetas seleccionadas especificando las rutas de acceso de directorio "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="dbda5-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="dbda5-116">También puede aplicar filtrado geográfica tooa archivo único mediante la especificación de archivo hello y, omitiendo Hola barra diagonal "/ imágenes/ciudad.png".</span><span class="sxs-lookup"><span data-stu-id="dbda5-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="dbda5-117">Filtro de ruta de acceso del directorio de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dbda5-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="dbda5-118">Paso 2: Definir la acción de hello: bloquear o permitir</span><span class="sxs-lookup"><span data-stu-id="dbda5-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="dbda5-119">**Bloquear:** a los usuarios de hello especificaron se denegarán países tooassets de acceso solicitado desde esa ruta de acceso de recursiva.</span><span class="sxs-lookup"><span data-stu-id="dbda5-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="dbda5-120">Si no se han configurado otras opciones de filtrado de país para esa ubicación, a continuación, se permitirá acceso a todos los demás usuarios.</span><span class="sxs-lookup"><span data-stu-id="dbda5-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="dbda5-121">**Permitir:** solo los usuarios de hello especificaron países podrán tooassets de acceso solicitado desde esa ruta de acceso de recursiva.</span><span class="sxs-lookup"><span data-stu-id="dbda5-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="dbda5-122">Paso 3: Definir países Hola</span><span class="sxs-lookup"><span data-stu-id="dbda5-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="dbda5-123">Seleccione los países Hola que desee tooblock o permiten la ruta de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbda5-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="dbda5-124">Por ejemplo, regla de Hola de bloqueo /Photos/Estrasburgo/filtrará archivos incluidos:</span><span class="sxs-lookup"><span data-stu-id="dbda5-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="dbda5-125">Códigos de país</span><span class="sxs-lookup"><span data-stu-id="dbda5-125">Country codes</span></span>
<span data-ttu-id="dbda5-126">Hola **filtrado geográfica** característica utiliza país códigos toodefine Hola países desde la que pueden permitir o bloquear una solicitud para un directorio seguro.</span><span class="sxs-lookup"><span data-stu-id="dbda5-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="dbda5-127">Encontrará Hola códigos de país de [códigos de país de CDN de Azure](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbda5-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="dbda5-128"><a id="considerations"></a>Consideraciones</span><span class="sxs-lookup"><span data-stu-id="dbda5-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="dbda5-129">Puede tardar minutos too90 Verizon, o un par de minutos con Akamai, para cambios tooyour país configuración tootake efecto del filtrado.</span><span class="sxs-lookup"><span data-stu-id="dbda5-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="dbda5-130">Esta característica no admite caracteres comodín (por ejemplo, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="dbda5-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="dbda5-131">configuración de filtrado de replicación geográfica de Hello asociado a la ruta de acceso relativa de hello será la ruta de acceso de toothat de aplica de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="dbda5-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="dbda5-132">Solo una regla puede ser aplicada toohello misma ruta de acceso relativa (no se puede crear varios filtros de país que toohello punto misma ruta de acceso relativa.</span><span class="sxs-lookup"><span data-stu-id="dbda5-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="dbda5-133">Sin embargo, una carpeta puede tener varios filtros de país.</span><span class="sxs-lookup"><span data-stu-id="dbda5-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="dbda5-134">Esto es debido a toohello recursiva naturaleza de los filtros de país.</span><span class="sxs-lookup"><span data-stu-id="dbda5-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="dbda5-135">En otras palabras, se puede asignar un filtro de país diferente a una subcarpeta de una carpeta configurada previamente.</span><span class="sxs-lookup"><span data-stu-id="dbda5-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

