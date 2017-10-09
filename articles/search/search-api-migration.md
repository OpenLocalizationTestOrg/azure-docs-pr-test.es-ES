---
title: "aaaUpgrading toohello API de REST de servicio de búsqueda de Azure versión 01-09-2016 | Documentos de Microsoft"
description: "Actualizar toohello API de REST de servicio de búsqueda de Azure versión 2016-09-01"
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
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="49865-103">Actualizar toohello API de REST de servicio de búsqueda de Azure versión 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="49865-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="49865-104">Si usa la versión 2015-02-28 o 2015-02-28-versión preliminar de hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artículo le ayudará a actualizar la aplicación toouse Hola siguiente disponible con carácter general versión de API, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="49865-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="49865-105">Versión 2016-09-01 de API de REST de hello contiene algunos cambios de versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="49865-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="49865-106">Se trata principalmente de cambios compatibles con versiones anteriores, por lo que cambiar el código apenas debe exigir esfuerzo, según la versión que utilizaba antes.</span><span class="sxs-lookup"><span data-stu-id="49865-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="49865-107">Vea [tooupgrade pasos](#UpgradeSteps) para obtener instrucciones sobre cómo toochange la versión nueva de API de código toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="49865-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="49865-108">La instancia de servicio de búsqueda de Azure es compatible con varias versiones de API de REST, incluidas hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="49865-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="49865-109">Puede continuar toouse una versión cuando ya no es Hola más reciente, pero se recomienda que migre la versión más reciente de código toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="49865-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="49865-110">Novedades de la versión 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="49865-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="49865-111">Versión 2016-09-01 es Hola segunda versión de disponibilidad general de hello API de REST de servicio de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="49865-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="49865-112">Entre las nuevas características de esta versión de API se incluyen:</span><span class="sxs-lookup"><span data-stu-id="49865-112">New features in this API version include:</span></span>

* <span data-ttu-id="49865-113">[Analizadores personalizados](https://aka.ms/customanalyzers), que permiten un control de tootake sobre el proceso de Hola de convertir texto en tokens indizables y permite realizar búsquedos.</span><span class="sxs-lookup"><span data-stu-id="49865-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="49865-114">[Almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md) y [almacenamiento de tablas Azure](search-howto-indexing-azure-tables.md) indizadores, que le permiten tooeasily importación datos del almacenamiento de Azure en búsqueda de Azure en una programación o a petición.</span><span class="sxs-lookup"><span data-stu-id="49865-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="49865-115">[Asignaciones de campo](search-indexer-field-mappings.md), que le permiten toocustomize cómo indizadores importación datos de búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="49865-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="49865-116">ETag, que le permiten tooupdate Hola definiciones de índices, los indizadores y orígenes de datos de una manera segura para simultaneidad.</span><span class="sxs-lookup"><span data-stu-id="49865-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="49865-117">Tooupgrade de pasos</span><span class="sxs-lookup"><span data-stu-id="49865-117">Steps tooupgrade</span></span>
<span data-ttu-id="49865-118">Si va a actualizar desde la versión 2015-02-28, probablemente no tendrá toomake ningún código de tooyour de cambios, excepto el número de versión de hello toochange.</span><span class="sxs-lookup"><span data-stu-id="49865-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="49865-119">situaciones solo de Hello en el que podría necesitar toochange código cuando son:</span><span class="sxs-lookup"><span data-stu-id="49865-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="49865-120">Se produce un error en el código cuando se devuelven propiedades no reconocidas en una respuesta de la API.</span><span class="sxs-lookup"><span data-stu-id="49865-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="49865-121">De forma predeterminada, la aplicación debe omitir propiedades que no comprende.</span><span class="sxs-lookup"><span data-stu-id="49865-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="49865-122">El código conserva las solicitudes de API y trata de tooresend ellos toohello nueva versión de API.</span><span class="sxs-lookup"><span data-stu-id="49865-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="49865-123">Por ejemplo, esto podría suceder si la aplicación continúa tokens de continuación procedentes de la API de búsqueda de hello (para obtener más información, busque `@search.nextPageParameters` en hello [referencia de la API de búsqueda](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="49865-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="49865-124">Si cualquiera de estas situaciones aplica tooyou, a continuación, deberá toochange el código en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="49865-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="49865-125">De lo contrario, ningún cambio debería ser necesario a menos que desee toostart con hello [nuevas características](#WhatsNew) de versión 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="49865-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="49865-126">Si va a actualizar desde la versión 2015-02-28-versión preliminar, Hola anterior también se aplica, pero también debe tener en cuenta que algunas características de vista previa no están disponibles en la versión 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="49865-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="49865-127">El indizador de Azure Blob Storage admite archivos CSV y blobs que contengan matrices JSON.</span><span class="sxs-lookup"><span data-stu-id="49865-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="49865-128">Sinónimos</span><span class="sxs-lookup"><span data-stu-id="49865-128">Synonyms</span></span>
* <span data-ttu-id="49865-129">Consultas de tipo "Más resultados similares"</span><span class="sxs-lookup"><span data-stu-id="49865-129">"More like this" queries</span></span>

<span data-ttu-id="49865-130">Si el código usa estas características, no será capaz de tooupgrade too2016-09-01, sin quitar el uso de ellos.</span><span class="sxs-lookup"><span data-stu-id="49865-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49865-131">Por favor, recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluar, y no deben usarse en entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="49865-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="49865-132">Conclusión</span><span class="sxs-lookup"><span data-stu-id="49865-132">Conclusion</span></span>
<span data-ttu-id="49865-133">Si necesita obtener más información sobre el uso de hello API de REST de servicio de búsqueda de Azure, vea Hola actualizado recientemente [referencia de la API](https://msdn.microsoft.com/library/azure/dn798935.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="49865-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="49865-134">Agradecemos sus comentarios sobre Azure Search.</span><span class="sxs-lookup"><span data-stu-id="49865-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="49865-135">Si tiene problemas, puede tooask libre nos para obtener ayuda sobre hello [foro de MSDN de búsqueda de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="49865-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="49865-136">Si va a hacer una pregunta sobre Azure buscarlo en StackOverflow, asegúrese de que tootag con `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="49865-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="49865-137">Gracias por usar Búsqueda de Azure.</span><span class="sxs-lookup"><span data-stu-id="49865-137">Thank you for using Azure Search!</span></span>

