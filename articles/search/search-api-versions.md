---
title: "versiones de aaaAPI de búsqueda de Azure | Documentos de Microsoft"
description: "Directiva de versiones para la biblioteca de cliente de API de REST de búsqueda de Azure y Hola Hola .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Versiones de API en Búsqueda de Azure
Azure Search implementa las actualizaciones de características de forma regular. A veces, pero no siempre, estas actualizaciones requieren nos toopublish una nueva versión de la compatibilidad con versiones anteriores de API toopreserve. Publicar una nueva versión permite toocontrol y cuándo y cómo integrar las actualizaciones del servicio de búsqueda en el código.

Como norma, intentamos toopublish nuevas versiones solo cuando sea necesario, ya que puede implicar algún tooupgrade esfuerzo su versión de toouse una nueva API de código. Solo se publicará una versión nueva si necesitamos toochange algunos aspectos de la API de hello en ningún modo que perjudique la compatibilidad con versiones anteriores. Esto puede suceder debido a las características de tooexisting correcciones o debido a nuevas características que cambiar el área de superficie de API existente.

Seguimos Hola misma regla para actualizaciones del SDK. Hola SDK de búsqueda de Azure sigue hello [control de versiones semántico](http://semver.org/) reglas, lo que significa que su versión consta de tres partes: principal, secundaria y (por ejemplo, 1.1.0) del número de compilación. Se liberará una nueva versión principal de hello SDK solo en caso de cambios que interrumpen la compatibilidad con versiones anteriores. Para actualizaciones de características de no separación, aumentaremos versión secundaria de Hola y de correcciones de errores se aumentará solo versión de compilación de Hola.

> [!NOTE]
> La instancia de servicio de búsqueda de Azure es compatible con varias versiones de API de REST, incluidas hello más reciente. Puede continuar toouse una versión cuando ya no es Hola más reciente, pero se recomienda que migre la versión más reciente de código toouse Hola. Cuando se utiliza la API de REST de Hola, debe especificar versión de API de hello en cada solicitud realizada a través del parámetro de versión de la api de Hola. Cuando se usa Hola .NET SDK, versión de Hola de hello SDK usa determina versión correspondiente de Hola de hello API de REST. Si usas un SDK anterior, puede continuar toorun ese código sin cambios aunque servicio hello es la versión de toosupport actualizada una API más recientes.

## <a name="snapshot-of-current-versions"></a>Instantánea de las versiones actuales
A continuación se muestra una instantánea de hello las versiones actuales de tooAzure de interfaces de programación todos búsqueda.

| Interfaces | Versión principal más reciente | Estado |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |Disponibilidad general, lanzado en noviembre de 2016 |
| [Versión preliminar del SDK de .NET](https://aka.ms/search-sdk-preview) |2.0-preview |Versión preliminar , publicada en agosto de 2016 |
| [API de REST de servicio](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Disponibilidad general |
| [Versión preliminar de la API de REST de servicio](search-api-2015-02-28-preview.md) |2015-02-28-Preview |Vista previa |
| [SDK de administración de .NET](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Disponibilidad general |
| [API de REST de administración](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Disponibilidad general |

Para las API de REST, incluidos Hola hello `api-version` en cada llamada, es necesario. Esto hace fácil tootarget una versión específica, como una API de vista previa. Hello ejemplo siguiente se muestra cómo Hola `api-version` se especifica el parámetro:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Aunque cada solicitud tiene un `api-version`, le recomendamos que use Hola misma versión para todas las solicitudes de API. Esto ocurre especialmente cuando las nuevas versiones de API incorporan atributos u operaciones que las versiones anteriores no reconocen. Debe evitarse la mezcla de versiones de API, ya que puede tener consecuencias no deseadas.
>
> Hola API de REST de servicios y API de REST de administración son versionar de forma independiente entre sí. Cualquier semejanza entre los números de versión es mera coincidencia.

Disponible con carácter general (o GA) API puede usarse en producción y está sujeto tooAzure contratos de nivel de servicio. Versiones de vista previa tienen características experimentales que no son siempre tooa migrados GA versión. **Se recomienda encarecidamente no usar una versión preliminar de API en aplicaciones de producción.**

## <a name="about-preview-and-generally-available-versions"></a>Acerca de las versiones preliminar y de disponibilidad general
Búsqueda de Azure siempre previamente libera características experimentales a través de la API de REST de hello en primer lugar, a continuación, a través de las versiones preliminares de hello .NET SDK.

Características de vista previa no se garantiza que toobe migrado tooa GA versión. Mientras que las características en una versión de GA se consideran estable y es poco probable toochange con excepción de Hola de mejoras y correcciones de compatibilidad pequeños, características de vista previa están disponibles para pruebas y la experimentación con el fin de Hola de recabar comentarios en Diseño e implementación.

Sin embargo, dado que las características de vista previa son toochange de asunto, se recomienda no escribir código de producción que tome una dependencia en las versiones preliminares. Si está utilizando una versión anterior de la vista previa, se recomienda migrar versión de toohello disponible con carácter general (GA).

Para hello .NET SDK: Guía de migración de código puede encontrarse en [actualización Hola .NET SDK](search-dotnet-sdk-migration.md).

Disponibilidad general significa que búsqueda de Azure está ahora en el contrato de nivel de servicio (SLA) de Hola. Hello SLA puede encontrarse en [contratos de nivel de servicio de búsqueda de Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
