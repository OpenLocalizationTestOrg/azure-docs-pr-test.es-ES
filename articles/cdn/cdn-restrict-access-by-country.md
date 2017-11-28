---
title: "Restricción del contenido de la red CDN de Azure por país | Microsoft Docs"
description: "Aprenda cómo restringir el acceso a su contenido de la red CDN de Azure mediante la característica Filtrado geográfico."
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
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="79a10-103">Restricción del contenido de la red CDN de Azure por país</span><span class="sxs-lookup"><span data-stu-id="79a10-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="79a10-104">Información general</span><span class="sxs-lookup"><span data-stu-id="79a10-104">Overview</span></span>
<span data-ttu-id="79a10-105">Cuando un usuario solicita su contenido, de forma predeterminada, el contenido se proporciona sin tener en cuenta el lugar desde el que el usuario realizó esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="79a10-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="79a10-106">En algunos casos, puede que desee restringir el acceso al contenido por país.</span><span class="sxs-lookup"><span data-stu-id="79a10-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="79a10-107">En este tema se explica cómo configurar la característica **Filtrado geográfico** para permitir o bloquear el acceso por país.</span><span class="sxs-lookup"><span data-stu-id="79a10-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79a10-108">Los productos de Verizon y Akamai proporcionan la misma funcionalidad de filtrado geográfico, pero difieren ligeramente en los códigos de país que admiten.</span><span class="sxs-lookup"><span data-stu-id="79a10-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="79a10-109">Vaya al Paso 3 para obtener un vínculo a las diferencias.</span><span class="sxs-lookup"><span data-stu-id="79a10-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="79a10-110">Para más información acerca de las consideraciones que se aplican a la configuración de este tipo de restricción, consulte la sección [Consideraciones](cdn-restrict-access-by-country.md#considerations) al final del tema.</span><span class="sxs-lookup"><span data-stu-id="79a10-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Filtrado por país](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="79a10-112">Paso 1: Definir la ruta de acceso al directorio</span><span class="sxs-lookup"><span data-stu-id="79a10-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="79a10-113">Seleccione el punto de conexión en el portal y busque la pestaña Filtrado geográfico en la navegación de la izquierda para buscar esta característica.</span><span class="sxs-lookup"><span data-stu-id="79a10-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="79a10-114">Al configurar un filtro de país, debe especificar la ruta de acceso relativa a la ubicación a la que se les permitirá o denegará el acceso a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="79a10-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="79a10-115">Puede aplicar el filtrado geográfico para todos los archivos mediante "/" o carpetas seleccionadas especificando las rutas de acceso de directorio "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="79a10-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="79a10-116">También puede aplicar el filtrado geográfica en un único archivo al especificar el archivo y omitiendo la barra diagonal "/pictures/city.png".</span><span class="sxs-lookup"><span data-stu-id="79a10-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="79a10-117">Filtro de ruta de acceso del directorio de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="79a10-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="79a10-118">Paso 2: Definir la acción: bloquear o permitir</span><span class="sxs-lookup"><span data-stu-id="79a10-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="79a10-119">**Bloquear** : a los usuarios de los países especificados se les denegará el acceso a los activos solicitados desde esa ruta recursiva.</span><span class="sxs-lookup"><span data-stu-id="79a10-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="79a10-120">Si no se han configurado otras opciones de filtrado de país para esa ubicación, a continuación, se permitirá acceso a todos los demás usuarios.</span><span class="sxs-lookup"><span data-stu-id="79a10-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="79a10-121">**Permitir** : solo los usuarios de los países especificados podrán tener acceso a los recursos solicitados desde esa ruta recursiva.</span><span class="sxs-lookup"><span data-stu-id="79a10-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="79a10-122">Paso 3: Definir los países</span><span class="sxs-lookup"><span data-stu-id="79a10-122">Step 3: Define the countries</span></span>
<span data-ttu-id="79a10-123">Seleccione los países que desee bloquear o permitir para la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="79a10-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="79a10-124">Por ejemplo, la regla de bloqueo /Fotos/Estrasburgo/ filtrará los archivos, incluidos:</span><span class="sxs-lookup"><span data-stu-id="79a10-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="79a10-125">Códigos de país</span><span class="sxs-lookup"><span data-stu-id="79a10-125">Country codes</span></span>
<span data-ttu-id="79a10-126">La característica **Filtrado geográfico** usa códigos de país para definir los países desde los que se permitirá o bloqueará una solicitud para un directorio protegido.</span><span class="sxs-lookup"><span data-stu-id="79a10-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="79a10-127">Encontrará los códigos de país en [Azure CDN Country Codes](https://msdn.microsoft.com/library/mt761717.aspx) (Códigos de países en la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="79a10-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="79a10-128"><a id="considerations"></a>Consideraciones</span><span class="sxs-lookup"><span data-stu-id="79a10-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="79a10-129">Es posible que los cambios en la configuración del filtro de país tarden 90 minutos en el caso de Verizon, o un par de minutos en el de Akamai, en surtir efecto.</span><span class="sxs-lookup"><span data-stu-id="79a10-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="79a10-130">Esta característica no admite caracteres comodín (por ejemplo, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="79a10-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="79a10-131">La configuración de filtrado geográfico asociada a la ruta de acceso relativa se aplicará de forma recursiva a esa ruta.</span><span class="sxs-lookup"><span data-stu-id="79a10-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="79a10-132">Solo se puede aplicar una regla a la misma ruta de acceso relativa (no se pueden crear varios filtros de país que señalen a la misma ruta de acceso relativa).</span><span class="sxs-lookup"><span data-stu-id="79a10-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="79a10-133">Sin embargo, una carpeta puede tener varios filtros de país.</span><span class="sxs-lookup"><span data-stu-id="79a10-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="79a10-134">Esto se debe a la naturaleza recursiva de los filtros de país.</span><span class="sxs-lookup"><span data-stu-id="79a10-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="79a10-135">En otras palabras, se puede asignar un filtro de país diferente a una subcarpeta de una carpeta configurada previamente.</span><span class="sxs-lookup"><span data-stu-id="79a10-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

