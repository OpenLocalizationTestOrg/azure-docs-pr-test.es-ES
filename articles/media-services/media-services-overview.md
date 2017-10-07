---
title: "información general de servicios multimedia de aaaAzure | Documentos de Microsoft"
description: "En este tema se proporciona información general de Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Introducción a Azure Media Services 

Servicios de multimedia de Microsoft Azure es una plataforma extensible basada en la nube que permite a los desarrolladores toobuild medios escalable administración y entrega de las aplicaciones. Servicios multimedia se basa en las API de REST que permiten toosecurely cargar, almacenar, codificar y empaquetar contenido de audio o vídeo a petición y en vivo streaming entrega toovarious para clientes de (por ejemplo, televisión, PC y dispositivos móviles).

Puede crear flujos de trabajo de un extremo a otro usando solamente Media Services. También puede elegir toouse componentes de terceros para algunas partes del flujo de trabajo. Por ejemplo, codifique mediante un codificador de terceros. A continuación, cargue, proteja, empaquete y entregue con Media Services.

Puede elegir toostream su contenido en vivo o entregar contenido a petición. tema de Hello también incluye vínculos a temas relevantes de tooother.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
Puede ver las rutas de aprendizaje de Azure Media Services aquí:

* [Flujo de trabajo de streaming en vivo de Azure Media Services](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Flujo de trabajo de streaming a petición de AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Requisitos previos

toostart con servicios multimedia de Azure, como tener Hola siguiente:

* Una cuenta de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com).
* Una cuenta de Azure Media Services. Para obtener más información, consulte [Creación de una cuenta](media-services-portal-create-account.md).
* (Opcional) Configurar el entorno de desarrollo. Elija .NET o API de REST para el entorno de desarrollo. Para obtener más información, consulte [Configuración del entorno](media-services-dotnet-how-to-use.md).

    Además, obtenga información acerca de cómo demasiado[conectarse mediante programación tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Un punto de conexión de streaming estándar o premium en estado iniciado.  Para más información, consulte [Administración de puntos de conexión de streaming](media-services-portal-manage-streaming-endpoints.md).

## <a name="sdks-and-tools"></a>SDK y herramientas

soluciones de servicios multimedia de toobuild, puede utilizar:

* [API de REST de Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Uno de los SDK de cliente disponibles hello:
    * [SDK de Servicios multimedia de Azure para .NET](https://github.com/Azure/azure-sdk-for-media-services)
    * [SDK de Azure para Java](https://github.com/Azure/azure-sdk-for-java)
    * [SDK de Azure para PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Azure Media Services para Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (es decir, una versión de un SDK de Node.js que no sea de Microsoft. Se mantiene por una Comunidad y actualmente no tiene una cobertura del 100% de hello AMS APIs).
* Herramientas existentes:
    * [Azure Portal](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (El Explorador de Azure Media Services (AMSE) es una aplicación Winforms/C# para Windows)

## <a name="concepts-and-overview"></a>Introducción y conceptos
Para conocer los conceptos de Azure Media Services, consulte [Conceptos](media-services-concepts.md).

Para un cómo-tooseries que le presenta componentes principales de hello tooall de servicios multimedia de Azure, consulte [tutoriales paso a paso de Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Esta serie tiene una buena información general sobre conceptos y realiza las tareas de hello AMSE herramienta toodemonstrate AMS. La herramienta AMSE es una herramienta de Windows. Esta herramienta es compatible con la mayoría de las tareas de hello puede lograr mediante programación con [AMS SDK para .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK para Java](https://github.com/Azure/azure-sdk-for-java), o [Azure SDK para PHP](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Escenarios admitidos y disponibilidad de Media Services en centros de datos

Para más información, consulte [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md) (Escenarios y disponibilidad de Media Services en centros de datos).

## <a name="service-level-agreement-sla"></a>Contrato de nivel de servicio (SLA)

* Garantizamos la disponibilidad del 99,9% de las transacciones de API de REST para la codificación de Media Services.
* Para el streaming, atenderemos correctamente las solicitudes de servicio con una garantía de disponibilidad del 99,9 % para el contenido multimedia existente cuando se adquiera un punto de conexión de streaming estándar o premium.
* Para los canales de Live, se garantiza que ejecuta canales no tenga conectividad externa al menos un 99,9% de tiempo de Hola.
* Para la protección de contenido, se garantiza que se correctamente completará las solicitudes de clave al menos un 99,9% de tiempo de Hola.
* De indizador, se procesará correctamente las solicitudes de tarea del indizador que se procesa con una codificación reservado unidad 99,9% de tiempo de Hola.

Para obtener más información, consulte el [Contrato de nivel de servicio (SLA) de Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Para obtener información acerca de la disponibilidad en centros de datos, vea hello [Avaiability](scenarios-and-availability.md#availability) sección.

## <a name="support"></a>Soporte técnico

[Soporte técnico de Azure](https://azure.microsoft.com/support/options/) proporciona opciones de soporte técnico para Azure, incluido Media Services.

## <a name="provide-feedback"></a>Envío de comentarios

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
