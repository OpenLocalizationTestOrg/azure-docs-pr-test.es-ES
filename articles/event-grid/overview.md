---
title: "información general de cuadrícula de eventos de aaaAzure"
description: Describe Azure Event Grid y sus conceptos.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Una cuadrícula de eventos de tooAzure de introducción

Cuadrícula de eventos de Azure permite tooeasily crear aplicaciones con las arquitecturas basadas en eventos. Seleccione Hola recursos de Azure que desee toosubscribe a y proporcionar un controlador de eventos de Hola o WebHook extremo toosend Hola evento. Event Grid tiene compatibilidad integrada para eventos procedentes de los servicios de Azure, como los blobs de almacenamiento y los grupos de recursos. Event Grid también tiene soporte personalizado para aplicaciones y eventos de otros fabricantes, con temas personalizados y webhooks personalizados. 

Puede usar filtros tooroute eventos específicos toodifferent puntos de conexión, los puntos de conexión de multidifusión toomultiple y asegúrese de que los eventos se entregan de forma confiable. Event Grid también tiene compatibilidad integrada para eventos personalizados y de terceros.

Para la versión de vista previa de hello, admite la cuadrícula de eventos **westus2** y **westcentralus** ubicaciones. Se agregarán otras regiones.

Este artículo ofrece información general sobre Azure Event Grid. Si desea que tooget a trabajar con la cuadrícula de eventos, vea [ruta y crear eventos personalizados con la cuadrícula de eventos de Azure](custom-event-quickstart.md).

![Modelo funcional de Event Grid](./media/overview/event-grid-functional-model.png)

Actualmente, Blob Storage no está disponible públicamente como publicador.

## <a name="concepts"></a>Conceptos

Hay cinco conceptos en Azure Event Grid que le permiten empezar a trabajar:

* **Eventos**: ¿qué ha ocurrido?
* **Orígenes de eventos/publicadores** : si se ha producido el evento de Hola.
* **Temas** -Hola donde publicadores envían eventos de punto de conexión.
* **Suscripciones a eventos** -eventos de tooroute de mecanismo de punto de conexión o integradas hello, a veces toomultiple controladores. También se utilizan suscripciones de eventos de entrada de filtro de toointelligently de controladores.
* **Controladores de eventos** : Hola aplicación o servicio reaccionando eventos toohello.

Para más información acerca de estos conceptos, consulte [Conceptos en Azure Event Grid](concepts.md).

## <a name="capabilities"></a>Capacidades

Estas son algunas de las principales características de Hola de cuadrícula de eventos de Azure:

* **Simplicidad** -punto y haga clic en eventos de tooaim del controlador de eventos de tooany de recursos de Azure o el punto de conexión.
* **Filtrado avanzado** -filtro de evento tooensure de ruta de acceso de publicación de evento o tipo de controladores de eventos sólo reciban los eventos relevantes.
* **Distribución ramificada** -suscribirse toohello de varios puntos de conexión mismo toosend de eventos copia de hello eventos tooas muchos lugares según sea necesario.
* **Confiabilidad** -utilizar reintento de 24 horas con tooensure de retroceso exponencial se entregan eventos.
* **Pago por evento** : paga solo para la cantidad de hello utilizar cuadrícula de eventos.
* **Alto rendimiento**: cree cargas de trabajo de gran volumen en Event Grid con soporte para millones de eventos por segundo.
* **Eventos integrados**: desarrolle y ejecute rápidamente con eventos integrados definidos por el recurso.
* **Eventos personalizados**: use la ruta, el filtrado y la entrega confiable de eventos personalizados de Event Grid en su aplicación.

## <a name="built-in-publisher-and-handler-integration"></a>Integración incorporada del publicador y el controlador

Azure ofrece compatibilidad de eventos integrada con numerosos servicios, incluidos tanto publicadores como controladores.

### <a name="publishers"></a>Publicadores

Actualmente, hello servicios de Azure siguientes tienen publicador integrada compatibilidad con la cuadrícula de eventos:

* Grupos de recursos (operaciones de administración)
* Suscripciones de Azure (operaciones de administración)
* Centros de eventos
* Temas personalizados

Otros servicios de Azure se agregarán este año.

### <a name="handlers"></a>Controladores

Actualmente, hello servicios de Azure siguientes tienen controlador integrados compatibilidad con la cuadrícula de eventos: 

* Funciones de Azure
* Logic Apps
* Azure Automation
* WebHooks

Otros servicios de Azure se agregarán este año.

## <a name="what-can-i-do-with-event-grid"></a>¿Qué puedo hacer con Event Grid?

Azure Event Grid proporciona varias funcionalidades que mejoran considerablemente el trabajo sin servidor, la automatización de operaciones y la integración: 

### <a name="serverless-application-architectures"></a>Arquitecturas de aplicación sin servidor

![Aplicación sin servidor](./media/overview/serverless_web_app.png)

Event Grid conecta orígenes de datos y controladores de eventos. Por ejemplo, usar un análisis de imágenes de toorun de función sin servidor cada vez que una nueva foto agrega contenedor de almacenamiento de blobs de tooa desencadenador tooinstantly de cuadrícula de eventos. 

### <a name="ops-automation"></a>Automatización de operaciones

![Automatización de operaciones](./media/overview/Ops_automation.png)

Cuadrícula de eventos permite la automatización de toospeed y simplificar el cumplimiento de directivas. Por ejemplo, Event Grid puede enviar una notificación a Azure Automation cuando se crea una máquina virtual o cuando se pone en marcha una instancia de SQL Database. Estos eventos se pueden utilizar tooautomatically Compruebe que las configuraciones de servicio son compatibles, poner metadatos en herramientas de operations, máquinas virtuales de etiqueta o elementos de trabajo de archivo.

### <a name="application-integration"></a>Integración de aplicaciones

![Integración de aplicaciones](./media/overview/app_integration.png)

Event Grid conecta su aplicación con otros servicios. Por ejemplo, puede crear un tema personalizado toosend tooEvent de datos de eventos de la aplicación cuadrícula y aprovechar las ventajas de su entrega confiable, avanzada de enrutamiento y la integración directa con Azure. Como alternativa, puede usar la cuadrícula de eventos con datos en cualquier parte, de las aplicaciones lógicas tooprocess sin escribir código. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>¿En qué se diferencia Event Grid de otros servicios de integración de Azure?

Event Grid es un panel posterior de eventos que habilita la programación orientada a eventos y reactiva. Está totalmente integrado con los servicios de Azure y puede integrarse con servicios de terceros. mensajes de bienvenida del evento contiene información de Hola que necesita tooreact toochanges en aplicaciones y servicios. Cuadrícula de eventos no es una canalización de datos y no entrega objeto real Hola que se ha actualizado.

Service Bus se adapta perfectamente a aplicaciones empresariales tradicionales que requieren transacciones, ordenación, detección de duplicados y coherencia inmediata. Event Grid está diseñado para la velocidad, la escala, la amplitud y el bajo costo en un modelo reactivo. Resulta idóneo tooserverless arquitectura.

Event Grid complementa otros servicios de Azure como Logic Apps y Event Hubs. Desencadenadores de la cuadrícula de eventos Hola toobegin de aplicación lógica de su flujo de trabajo. Los concentradores de eventos funciona con cuadrícula de eventos, permitiéndole tooreact tooevents de captura de los centros de eventos y canalizaciones de entrada y de transformación de datos de compilación.

## <a name="how-much-does-event-grid-cost"></a>¿Cuánto cuesta Event Grid?

Azure Event Grid usa un modelo de precios de pago por evento, por lo que solo se paga por lo que usa.

Cuadrícula de eventos cuesta 0,60 $ por cada millón de operaciones (0,30 USD durante la vista previa) y Hola primero 100.000 operación al mes son gratuitas. Estas operaciones se definen como eventos de entrada, coincidencia avanzada, intentos de entrega y llamadas de administración.  Pueden encontrar más detalles en hello [página de precios](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Pasos siguientes

* [Crear y suscribirse a eventos toocustom](custom-event-quickstart.md) comenzar de inmediato y empezar a enviar su propio punto de conexión de tooany de eventos personalizados mediante Inicio rápido de hello cuadrícula de eventos de Azure.
* [Con las aplicaciones lógicas como un controlador de eventos](monitor-virtual-machine-changes-event-grid-logic-app.md) un tutorial sobre la creación de una aplicación con las aplicaciones lógicas tooreact tooevents inserta con cuadrícula de eventos.
* [Referencia de la API de REST de Event Grid](/rest/api/eventgrid)  
  Proporciona información más técnica sobre Hola cuadrícula de eventos de Azure y una referencia para administrar suscripciones a eventos, enrutamiento y filtrado.
