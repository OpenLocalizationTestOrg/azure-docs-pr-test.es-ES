---
title: "información general de las funciones de aaaAzure | Documentos de Microsoft"
description: "Comprender cómo toouse funciones de Azure toooptimize asincrónicas las cargas de trabajo en minutos."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Las funciones de un tooAzure de introducción  
Las funciones de Azure es una solución para ejecutar fácilmente pequeños fragmentos de código, o "funciones", en la nube de Hola. Puede escribir solo el código de hello que necesarios para el problema de hello en cuestión, sin preocuparse un toorun de infraestructura de aplicación o hello todo lo. Functions puede hacer que el desarrollo sea aún más productivo y, además, le permite utilizar el lenguaje de desarrollo que prefiera, como C#, F#, Node.js, Python o PHP. Solo paga por tiempo Hola que se ejecuta el código y confiar en Azure tooscale según sea necesario. Azure Functions le permite desarrollar aplicaciones en Microsoft Azure.

Este tema proporciona información general de alto nivel de Azure Functions. Si desea que right toojump y empezar a trabajar con funciones de Azure, comience con [crear su primera función Azure](functions-create-first-azure-function.md). Si desea obtener más información técnica acerca de las funciones, vea hello [material de referencia](functions-reference.md).

## <a name="features"></a>Características
Estas son algunas características clave de Azure Functions:

* **Elección del lenguaje**: escriba funciones con C#, F#, Node.js, Python, PHP, batch, bash o cualquier archivo ejecutable.
* **Modelo de precios de pago por uso** : paga solo para hello tiempo dedicado a ejecutar el código. Consulte el hospedaje de consumo de hello planear opción Hola [precios sección](#pricing).  
* **Traiga sus propias dependencias** : Funciones de Azure admite NuGet y NPM, para que pueda usar sus bibliotecas favoritas.  
* **Seguridad integrada** : proteja las funciones desencadenadas por HTTP con los proveedores de OAuth como Azure Active Directory, Facebook, Google, Twitter y cuenta Microsoft.  
* **Integración simplificada** : fácil aprovechamiento de los servicios de Azure y ofertas de software como servicio (SaaS). Vea hello [sección integraciones](#integrations) algunos ejemplos.  
* **Desarrollo flexible** : código de la derecha de funciones en el portal de Hola o configurar la integración continua e implementar el código a través de GitHub, Visual Studio Team Services y otros [admite herramientas de desarrollo](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Código abierto** -tiempo de ejecución de funciones de hello es código abierto y [disponible en GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>¿Qué puedo hacer con las funciones?
Las funciones de Azure son una excelente solución para el procesamiento de datos, integración de sistemas, trabajar con Hola internet de cosas (IoT) y compilar API simples y microservicios. Considere la posibilidad de funciones para tareas como imagen o procesamiento de pedidos, el mantenimiento de los archivos, o para las tareas que desea toorun según una programación. 

Funciones proporciona tooget plantillas para trabajar con escenarios clave, incluidos Hola siguientes:

* **BlobTrigger** -blobs en almacenamiento de Azure de proceso cuando se agregan toocontainers. Esta función se puede usar para cambiar el tamaño de las imágenes.
* **EventHubTrigger** -responder tooevents entregados tooan concentrador de eventos de Azure. Especialmente útil en escenarios de Internet de las cosas, procesamiento del flujo de trabajo o de la experiencia del usuario y en instrumentación de aplicaciones.
* **Webhook genérico** : procesar las solicitudes HTTP de webhook de cualquier servicio que admita webhooks.
* **GitHub webhook** -tooevents responden que se producen en los repositorios de GitHub. Para ver un ejemplo, consulte [Creación de un webhook o una función de API de Azure](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -desencadenar la ejecución del código de hello mediante una solicitud HTTP.
* **QueueTrigger** -responder toomessages a medida que llegan en una cola de almacenamiento de Azure. Para obtener un ejemplo, vea [crea una función de Azure que enlaza tooan servicio de Azure](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -conectar su tooother código servicios o los servicios locales escucha toomessage las colas de Azure. 
* **ServiceBusTopicTrigger** -conectar su tooother de código en los servicios locales suscribiéndose tootopics o de servicios de Azure. 
* **TimerTrigger** : ejecutar limpieza u otras tareas de lote dentro de una programación predefinida. Para ver un ejemplo, consulte [Creación de una función de Azure de procesamiento de eventos](functions-create-an-event-processing-function.md).

Azure admite funciones *desencadenadores*, que son formas toostart la ejecución del código, y *enlaces*, que es formas toosimplify de codificación para los datos de entrada y salidos. Para obtener una descripción detallada de los desencadenadores de Hola y enlaces que proporciona funciones de Azure, consulte [referencia del programador de desencadenadores y los enlaces de funciones de Azure](functions-triggers-bindings.md).

## <a name="integrations"></a>Integraciones
Azure Functions se integra con diversos servicios de Azure y de terceros. Dichos servicios pueden desencadenar una función e iniciar su ejecución, o bien servir de entrada y salida del código. Hola siguiendo las integraciones de servicio es compatibles con las funciones de Azure. 

* Azure Cosmos DB
* Centros de eventos de Azure 
* Aplicaciones móviles de Azure (tablas)
* Centros de notificaciones de Azure
* Azure Service Bus (colas y temas)
* Almacenamiento de Azure (blob, colas y tablas) 
* GitHub (webhooks)
* Local (mediante el Bus de servicio)
* Twilio (mensajes SMS)

## <a name="pricing"></a>¿Cuánto cuesta Funciones de Azure?
Las funciones de Azure tiene dos tipos de planes de precios, elija Hola que mejor se adapte a sus necesidades: 

* **Plan de consumo** : si se ejecuta la función, Azure proporciona todos los recursos de cálculo necesarios Hola de. No tienes tooworry acerca de la administración de recursos y solo se paga por el tiempo de presentación que se ejecuta el código. 
* **Plan del Servicio de aplicaciones** : se ejecutan las funciones igual que aplicaciones web, móviles y de API. Cuando ya usan el servicio de aplicación para las demás aplicaciones, puede ejecutar las funciones en hello mismo plan sin costo adicional alguno. 

Están los detalles de precios completos en hello [página de precios de las funciones](https://azure.microsoft.com/pricing/details/functions/). Para obtener más información acerca de cómo ampliar las funciones, vea [cómo tooscale funciones de Azure](functions-scale.md).

## <a name="next-steps"></a>Pasos siguientes
* [Creación de su primera función de Azure](functions-create-first-azure-function.md)  
  Comenzar de inmediato y crear la primera función con inicio rápido de hello las funciones de Azure. 
* [Azure Functions developer reference](functions-reference.md)  
  Proporciona información más técnica sobre el tiempo de ejecución de hello las funciones de Azure y una referencia para las funciones de codificación y la definición de desencadenadores y los enlaces.
* [Testing Azure Functions](functions-test-a-function.md)  
  describe las diversas herramientas y técnicas para probar sus funciones.
* [¿Cómo tooscale las funciones de Azure](functions-scale.md)  
  Se tratan los planes de servicio disponibles con las funciones de Azure, incluido el plan de hospedaje de consumo de Hola y cómo toochoose Hola plan adecuado. 
* [¿Qué es Servicios de aplicaciones de Azure?](../app-service/app-service-value-prop-what-is.md)  
  Las funciones de Azure aprovecha la plataforma de servicio de aplicaciones de Azure de hello para la funcionalidad básica como implementaciones, variables de entorno y diagnósticos. 

