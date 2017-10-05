---
title: "Actualización de API de REST del servicio Azure Search versión 2016-09-01 | Microsoft Docs"
description: "Actualización de API de REST del Servicio Azure Search versión 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="6462d-103">Actualización de API de REST del Servicio Azure Search versión 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="6462d-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="6462d-104">Si usa la versión 2015-02-28 o 2015-02-28-Preview de [API de REST del servicio Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artículo le ayudará a actualizar la aplicación para que use la siguiente versión de API disponible con carácter general, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="6462d-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="6462d-105">La versión 2016-09-01 de la API de REST contiene algunos cambios con respecto a versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="6462d-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="6462d-106">Se trata principalmente de cambios compatibles con versiones anteriores, por lo que cambiar el código apenas debe exigir esfuerzo, según la versión que utilizaba antes.</span><span class="sxs-lookup"><span data-stu-id="6462d-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="6462d-107">Vea [Pasos para actualizar](#UpgradeSteps), a fin de obtener instrucciones sobre cómo cambiar el código para usar la nueva versión de API.</span><span class="sxs-lookup"><span data-stu-id="6462d-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="6462d-108">La instancia del servicio Azure Search es compatible con varias versiones de API de REST, incluida la más reciente.</span><span class="sxs-lookup"><span data-stu-id="6462d-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="6462d-109">Puede seguir usando una versión aunque no sea la más reciente, pero es recomendable que migre el código para usar la versión más actualizada.</span><span class="sxs-lookup"><span data-stu-id="6462d-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="6462d-110">Novedades de la versión 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="6462d-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="6462d-111">La versión 2016-09-01 es la segunda versión disponible con carácter general de API de REST del servicio Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6462d-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="6462d-112">Entre las nuevas características de esta versión de API se incluyen:</span><span class="sxs-lookup"><span data-stu-id="6462d-112">New features in this API version include:</span></span>

* <span data-ttu-id="6462d-113">[Analizadores personalizados](https://aka.ms/customanalyzers), que le permiten tomar el control sobre el proceso de conversión de texto en tokens que se pueden indizar y buscar.</span><span class="sxs-lookup"><span data-stu-id="6462d-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="6462d-114">Indizadores de [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) y [Azure Table Storage](search-howto-indexing-azure-tables.md), que permiten importar fácilmente datos del almacenamiento de Azure en Azure Search según una programación o a petición.</span><span class="sxs-lookup"><span data-stu-id="6462d-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="6462d-115">[Asignaciones de campo](search-indexer-field-mappings.md), que permiten personalizar cómo los indizadores importan datos en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6462d-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="6462d-116">Etiquetas ETag, que permiten actualizar las definiciones de índices, los indizadores y los orígenes de datos con seguridad de simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="6462d-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="6462d-117">Pasos para actualizar</span><span class="sxs-lookup"><span data-stu-id="6462d-117">Steps to upgrade</span></span>
<span data-ttu-id="6462d-118">Si va a actualizar desde la versión 2015-02-28, probablemente no tenga que realizar cambios en el código, excepto para cambiar el número de versión.</span><span class="sxs-lookup"><span data-stu-id="6462d-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="6462d-119">Las únicas situaciones en las que puede que tenga que modificar el código ocurren si:</span><span class="sxs-lookup"><span data-stu-id="6462d-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="6462d-120">Se produce un error en el código cuando se devuelven propiedades no reconocidas en una respuesta de la API.</span><span class="sxs-lookup"><span data-stu-id="6462d-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="6462d-121">De forma predeterminada, la aplicación debe omitir propiedades que no comprende.</span><span class="sxs-lookup"><span data-stu-id="6462d-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="6462d-122">El código conserva las solicitudes de API e intenta volver a enviarlas a la nueva versión de API.</span><span class="sxs-lookup"><span data-stu-id="6462d-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="6462d-123">Por ejemplo, esto podría suceder si la aplicación conserva tokens de continuación devueltos por la API de búsqueda (para más información, busque `@search.nextPageParameters` en la [referencia de la API de búsqueda](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="6462d-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="6462d-124">Si alguna de estas situaciones se le presenta, debe cambiar el código en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="6462d-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="6462d-125">De lo contrario, no debe ser necesario efectuar ningún cambio a menos que quiera empezar a usar las [nuevas características](#WhatsNew) de la versión 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="6462d-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="6462d-126">Si va a actualizar desde la versión 2015-02-28-Preview, lo anterior también se aplica, pero además debe tener en cuenta que algunas características de vista previa no están disponibles en la versión 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="6462d-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="6462d-127">El indizador de Azure Blob Storage admite archivos CSV y blobs que contengan matrices JSON.</span><span class="sxs-lookup"><span data-stu-id="6462d-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="6462d-128">Sinónimos</span><span class="sxs-lookup"><span data-stu-id="6462d-128">Synonyms</span></span>
* <span data-ttu-id="6462d-129">Consultas de tipo "Más resultados similares"</span><span class="sxs-lookup"><span data-stu-id="6462d-129">"More like this" queries</span></span>

<span data-ttu-id="6462d-130">Si el código usa estas características, no podrá actualizar a 2016-09-01 sin quitar el uso de las mismas.</span><span class="sxs-lookup"><span data-stu-id="6462d-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6462d-131">Por favor, recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluar, y no deben usarse en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="6462d-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="6462d-132">Conclusión</span><span class="sxs-lookup"><span data-stu-id="6462d-132">Conclusion</span></span>
<span data-ttu-id="6462d-133">Si necesita más información sobre el uso de API de REST del servicio Azure Search, vea la [Referencia de API](https://msdn.microsoft.com/library/azure/dn798935.aspx) recién actualizada en MSDN.</span><span class="sxs-lookup"><span data-stu-id="6462d-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="6462d-134">Agradecemos sus comentarios sobre Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6462d-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="6462d-135">Si tiene algún problema, no dude en pedirnos ayuda en el [foro de MSDN sobre Azure Search](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="6462d-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="6462d-136">Si va a hacer una pregunta sobre Azure Search en StackOverflow, asegúrese de etiquetarla con `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="6462d-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="6462d-137">Gracias por usar Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="6462d-137">Thank you for using Azure Search!</span></span>

