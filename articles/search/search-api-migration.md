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
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Actualizar toohello API de REST de servicio de búsqueda de Azure versión 2016-09-01
Si usa la versión 2015-02-28 o 2015-02-28-versión preliminar de hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artículo le ayudará a actualizar la aplicación toouse Hola siguiente disponible con carácter general versión de API, 2016-09-01.

Versión 2016-09-01 de API de REST de hello contiene algunos cambios de versiones anteriores. Se trata principalmente de cambios compatibles con versiones anteriores, por lo que cambiar el código apenas debe exigir esfuerzo, según la versión que utilizaba antes. Vea [tooupgrade pasos](#UpgradeSteps) para obtener instrucciones sobre cómo toochange la versión nueva de API de código toouse Hola.

> [!NOTE]
> La instancia de servicio de búsqueda de Azure es compatible con varias versiones de API de REST, incluidas hello más reciente. Puede continuar toouse una versión cuando ya no es Hola más reciente, pero se recomienda que migre la versión más reciente de código toouse Hola.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Novedades de la versión 2016-09-01
Versión 2016-09-01 es Hola segunda versión de disponibilidad general de hello API de REST de servicio de búsqueda de Azure. Entre las nuevas características de esta versión de API se incluyen:

* [Analizadores personalizados](https://aka.ms/customanalyzers), que permiten un control de tootake sobre el proceso de Hola de convertir texto en tokens indizables y permite realizar búsquedos.
* [Almacenamiento de blobs de Azure](search-howto-indexing-azure-blob-storage.md) y [almacenamiento de tablas Azure](search-howto-indexing-azure-tables.md) indizadores, que le permiten tooeasily importación datos del almacenamiento de Azure en búsqueda de Azure en una programación o a petición.
* [Asignaciones de campo](search-indexer-field-mappings.md), que le permiten toocustomize cómo indizadores importación datos de búsqueda de Azure.
* ETag, que le permiten tooupdate Hola definiciones de índices, los indizadores y orígenes de datos de una manera segura para simultaneidad. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Tooupgrade de pasos
Si va a actualizar desde la versión 2015-02-28, probablemente no tendrá toomake ningún código de tooyour de cambios, excepto el número de versión de hello toochange. situaciones solo de Hello en el que podría necesitar toochange código cuando son:

* Se produce un error en el código cuando se devuelven propiedades no reconocidas en una respuesta de la API. De forma predeterminada, la aplicación debe omitir propiedades que no comprende.
* El código conserva las solicitudes de API y trata de tooresend ellos toohello nueva versión de API. Por ejemplo, esto podría suceder si la aplicación continúa tokens de continuación procedentes de la API de búsqueda de hello (para obtener más información, busque `@search.nextPageParameters` en hello [referencia de la API de búsqueda](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Si cualquiera de estas situaciones aplica tooyou, a continuación, deberá toochange el código en consecuencia. De lo contrario, ningún cambio debería ser necesario a menos que desee toostart con hello [nuevas características](#WhatsNew) de versión 2016-09-01.

Si va a actualizar desde la versión 2015-02-28-versión preliminar, Hola anterior también se aplica, pero también debe tener en cuenta que algunas características de vista previa no están disponibles en la versión 2016-09-01:

* El indizador de Azure Blob Storage admite archivos CSV y blobs que contengan matrices JSON.
* Sinónimos
* Consultas de tipo "Más resultados similares"

Si el código usa estas características, no será capaz de tooupgrade too2016-09-01, sin quitar el uso de ellos.

> [!IMPORTANT]
> Por favor, recuerde que las versiones preliminares de las API están pensadas para realizar pruebas y evaluar, y no deben usarse en entornos de producción.
> 
> 

## <a name="conclusion"></a>Conclusión
Si necesita obtener más información sobre el uso de hello API de REST de servicio de búsqueda de Azure, vea Hola actualizado recientemente [referencia de la API](https://msdn.microsoft.com/library/azure/dn798935.aspx) en MSDN.

Agradecemos sus comentarios sobre Azure Search. Si tiene problemas, puede tooask libre nos para obtener ayuda sobre hello [foro de MSDN de búsqueda de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) o [StackOverflow](http://stackoverflow.com/). Si va a hacer una pregunta sobre Azure buscarlo en StackOverflow, asegúrese de que tootag con `azure-search`.

Gracias por usar Búsqueda de Azure.

