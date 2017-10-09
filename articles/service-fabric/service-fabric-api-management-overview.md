---
title: "aaaAzure Service Fabric con información general de administración de API | Documentos de Microsoft"
description: "Este artículo es una toousing Introducción administración de API de Azure como una puerta de enlace tooyour tejido de servicio de aplicaciones."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Información general de Service Fabric con Azure API Management

Aplicaciones de nube suelen necesitan una tooprovide de front-end de la puerta de enlace un único punto de entrada para los usuarios, dispositivos u otras aplicaciones. En Service Fabric, una puerta de enlace puede ser cualquier servicio sin estado como una [aplicación ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) u otro servicio designado para la entrada de tráfico, como [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/) o [Azure API Management](https://docs.microsoft.com/azure/api-management/).

Este artículo es una toousing Introducción administración de API de Azure como una puerta de enlace tooyour tejido de servicio de aplicaciones. Administración de API se integra directamente con Service Fabric, permitiéndole toopublish API con un amplio conjunto de servicios de enrutamiento reglas tooyour back-end Service Fabric. 

## <a name="architecture"></a>Arquitectura
Una arquitectura de Service Fabric común utiliza una aplicación de página web que realice llamadas HTTP de servicios tooback-end que exponen HTTP APIs. Hola [aplicación de ejemplo de iniciación de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) muestra un ejemplo de esta arquitectura.

En este escenario, un servicio web sin estado actúa como puerta de enlace de Hola de hello aplicación Service Fabric. Este enfoque requiere toowrite un servicio web que puede a proxy HTTP solicita servicios tooback-end, como se muestra en hello siguiente diagrama:

![Información general de la topología de Service Fabric con Azure API Management][sf-web-app-stateless-gateway]

Cuando las aplicaciones crezcan en complejidad, por lo que Hola puertas de enlace que se deben presentar una API delante innumerables servicios back-end. Administración de API de Azure está diseñado toohandle API complejas con las reglas de enrutamiento, control de acceso, limitación de velocidad, supervisión, el registro de eventos y las respuestas en caché con el mínimo esfuerzo por su parte. Administración de API de Azure admite la detección de servicios de Service Fabric, resolución de la partición, y ruta de réplica selección toointelligently directamente solicita servicios tooback-end Service Fabric para que no tenga toowrite su propia puerta de enlace de API sin estado. 

En este escenario, hello web que UI todavía se sirve a través de un servicio web, mientras se administran y se enruta a través de administración de API de Azure, como se muestra en hello siguiente diagrama llamadas a la API de HTTP:

![Información general de la topología de Service Fabric con Azure API Management][sf-apim-web-app]

## <a name="application-scenarios"></a>Escenarios de aplicación

Los servicios de Service Fabric pueden ser con o sin estado, y pueden tener particiones con uno de los tres esquemas: singleton, intervalo de Int-64 y con nombre. La resolución del punto de conexión de servicio requiere identificar una partición específica de una instancia de servicio específica. Al resolver un extremo de un servicio, ambos Hola de nombre de la instancia de servicio (por ejemplo, `fabric:/myapp/myservice`) también se debe especificar la partición específica de hello del servicio de hello, salvo en caso de hello de partición de singleton.

Azure API Management puede usarse con cualquier combinación de servicios con o sin estado y cualquier esquema de partición.

## <a name="send-traffic-tooa-stateless-service"></a>Enviar tráfico tooa sin estado servicio

En el caso más simple de hello, el tráfico se reenvía tooa instancia de servicio sin estado. tooachieve, una operación de administración de API contiene una directiva de procesamiento de entrada con un tejido de servicio back-end que asigna la instancia de servicio sin estado específico de tooa en hello Service Fabric back-end. Las solicitudes enviadas toothat servicio se envían tooa réplica aleatorio de la instancia de servicio sin estado Hola.

#### <a name="example"></a>Ejemplo
Hola siguiendo el escenario, una aplicación de Service Fabric contiene un servicio sin estado denominado `fabric:/app/fooservice`, que expone una API HTTP interno. nombre de instancia de servicio de Hello es conocido y puede estar codificado de forma rígida directamente en la directiva de procesamiento de entrada de la administración de API de Hola. 

![Información general de la topología de Service Fabric con Azure API Management][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Enviar tráfico tooa con estado servicio

Escenario de servicio sin estado toohello similar, el tráfico que puede reenviarse tooa instancia de servicio con estado. En este caso, una operación de administración de API contiene una directiva de procesamiento de entrada con un tejido de servicio back-end que asigna una partición específica de tooa de solicitud de un determinado *stateful* instancia del servicio. partición de Hello toomap calcula cada toois de solicitud a través de un método de lambda con alguna entrada de solicitud HTTP entrante hello, como un valor de ruta de acceso de dirección URL de Hola. Hola directiva puede ser configurado toosend solicitudes toohello réplica principal sólo, o tooa aleatorio réplica para las operaciones de lectura.

#### <a name="example"></a>Ejemplo

Hola siguiendo el escenario, una aplicación de Service Fabric contiene un servicio con estado con particiones denominado `fabric:/app/userservice` que expone una API HTTP interno. nombre de instancia de servicio de Hello es conocido y puede estar codificado de forma rígida directamente en la directiva de procesamiento de entrada de la administración de API de Hola.  

Hello servicio tiene particiones mediante el esquema de partición de hello Int64 con dos particiones y un intervalo de claves que abarca `Int64.MinValue` demasiado`Int64.MaxValue`. Directiva de back-end de Hello calcula una clave de partición dentro de ese intervalo mediante la conversión de hello `id` valor proporcionado en el entero de 64 bits de la tooa de ruta de acceso de solicitud con hello dirección URL, aunque cualquier algoritmo puede ser la clave de partición de hello usado toocompute aquí. 

![Información general de la topología de Service Fabric con Azure API Management][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Enviar tráfico de servicios sin estado toomultiple

En escenarios más avanzados, puede definir una operación de administración de API que asigna las solicitudes toomore que la instancia de un servicio. En este caso, cada operación contiene una directiva que asigna las solicitudes de instancia de servicio específico de tooa basándose en valores de hello solicitud HTTP de entrada, por ejemplo, la cadena de ruta de acceso o la consulta de la dirección URL de hello y, en caso de hello de servicios con estado, una partición dentro de la instancia de servicio de Hola . 

tooachieve esto, una administración de API de operación contiene una directiva de procesamiento de entrada con un tejido de servicio back-end que asigna la instancia de servicio sin estado tooa en función de los valores recuperados de la solicitud HTTP entrante Hola Hola Service Fabric back-end. Instancia de servicio de tooa de las solicitudes se envían tooa réplica aleatorio de la instancia de servicio de Hola.

#### <a name="example"></a>Ejemplo

En este ejemplo, se crea una nueva instancia de servicio sin estado para cada usuario de una aplicación con un nombre generado dinámicamente utilizando Hola siguiente fórmula:
 
 - `fabric:/app/users/<username>`

 Cada servicio tiene un nombre único, pero los nombres de hello no se conocen por adelantado porque se crean servicios de Hola en respuesta toouser o administrador de entrada y, por tanto, no puede ser codificados de forma rígida en las directivas APIM o las reglas de enrutamiento. En su lugar, se genera el nombre hello de hello servicio toowhich toosend una solicitud en la definición de la directiva de back-end de Hola de hello `name` valor proporcionado en la ruta de acceso de solicitud de dirección URL de Hola. Por ejemplo:

  - Una solicitud demasiado`/api/users/foo` es instancia tooservice enrutado`fabric:/app/users/foo`
  - Una solicitud demasiado`/api/users/bar` es instancia tooservice enrutado`fabric:/app/users/bar`

![Información general de la topología de Service Fabric con Azure API Management][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Enviar tráfico de servicios con estado toomultiple

Ejemplo de servicio sin estado toohello similar, una administración de API que se puede asignar la operación solicita toomore que uno **stateful** instancia de servicio, en cuyo caso también puede necesitar tooperform una resolución de partición para cada servicio con estado instancia.

tooachieve esto, una administración de API de operación contiene una directiva de procesamiento de entrada con un tejido de servicio back-end que asigna la instancia de servicio con estado tooa en función de los valores recuperados de la solicitud HTTP entrante Hola Hola Service Fabric back-end. Además toomapping una instancia de servicio de solicitud toospecific, solicitud de hello también puede ser asignado tooa partición específica dentro de la instancia de servicio de hello y, opcionalmente, réplica principal de tooeither Hola o una réplica secundaria aleatoria dentro de la partición de Hola.

#### <a name="example"></a>Ejemplo

En este ejemplo, se crea una nueva instancia de servicio con estado para cada usuario de la aplicación hello con un nombre generado dinámicamente utilizando Hola siguiente fórmula:
 
 - `fabric:/app/users/<username>`

 Cada servicio tiene un nombre único, pero los nombres de hello no se conocen por adelantado porque se crean servicios de Hola en respuesta toouser o administrador de entrada y, por tanto, no puede ser codificados de forma rígida en las directivas APIM o las reglas de enrutamiento. En su lugar, se genera el nombre hello de hello servicio toowhich toosend una solicitud en la definición de la directiva de back-end de Hola de hello `name` ruta de acceso de solicitud de dirección URL de Hola de valor proporcionado. Por ejemplo:

  - Una solicitud demasiado`/api/users/foo` es instancia tooservice enrutado`fabric:/app/users/foo`
  - Una solicitud demasiado`/api/users/bar` es instancia tooservice enrutado`fabric:/app/users/bar`

Cada instancia de servicio también tiene particiones mediante el esquema de partición de hello Int64 con dos particiones y un intervalo de claves que abarca `Int64.MinValue` demasiado`Int64.MaxValue`. Directiva de back-end de Hello calcula una clave de partición dentro de ese intervalo mediante la conversión de hello `id` valor proporcionado en el entero de 64 bits de la tooa de ruta de acceso de solicitud con hello dirección URL, aunque cualquier algoritmo puede ser la clave de partición de hello usado toocompute aquí. 

![Información general de la topología de Service Fabric con Azure API Management][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Pasos siguientes

Siga hello [Guía de inicio rápido](service-fabric-api-management-quick-start.md) tooset seguridad su primer tejido de servicio de clúster con las solicitudes de administración de API y el flujo a través de servicios de administración de API tooyour.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png