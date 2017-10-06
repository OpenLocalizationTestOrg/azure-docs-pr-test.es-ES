---
title: "aaaSet el monitor de eventos con los concentradores de eventos de Azure para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Supervisar eventos de tooreceive de flujos de datos y enviar eventos para las aplicaciones lógicas de Azure con los concentradores de eventos de Azure"
services: logic-apps
keywords: "flujo de datos, supervisión de eventos, centros de eventos"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Supervisar, recibir y enviar eventos con el conector de los centros de eventos de Hola

tooset un monitor de eventos para que pueda detectar eventos, eventos de recepción y enviar eventos, la aplicación lógica conectarse tooan [concentrador de eventos de Azure](https://azure.microsoft.com/services/event-hubs) desde la aplicación lógica. Obtenga más información acerca de los [Centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Requisitos

* Tendrá que toohave una [concentrador de eventos y espacio de nombres de los centros de eventos](../event-hubs/event-hubs-create.md) en Azure. Obtenga información acerca de [cómo toocreate un espacio de nombres de los centros de eventos y el centro de eventos](../event-hubs/event-hubs-create.md). 

* toouse [cualquier conector](https://docs.microsoft.com/azure/connectors/apis-list) en la aplicación lógica, tiene toocreate una aplicación lógica en primer lugar. Obtenga información acerca de [cómo una aplicación de la lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Comprobar los permisos del espacio de nombres de los centros de eventos y buscar la cadena de conexión de Hola

Para su tooaccess de aplicación lógica de cualquier servicio, tendrá que toocreate una [ *conexión* ](./connectors-overview.md) entre su lógica hello y aplicación de servicio, si no lo ha hecho ya. Esta conexión se autoriza a los datos de tooaccess de aplicación lógica.
Para su tooaccess de aplicación lógica el centro de eventos, deberá toohave **administrar** permisos y la cadena de conexión de hello para el espacio de nombres de los centros de eventos.

toocheck sus permisos y la cadena de conexión de get hello, siga estos pasos.

1.  Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure"). 

2.  Vaya a los centros de eventos de tooyour *espacio de nombres*, no Hola centro de eventos específicos. En la hoja de espacio de nombres de hello, en **configuración**, elija **directivas de acceso compartido**. En **Notificaciones**, compruebe que tenga permisos de **Administrador** para ese espacio de nombres.

    ![Administrar los permisos del espacio de nombres del Event Hub](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  cadena de conexión de hello toocopy de espacio de nombres de los centros de eventos de hello, elija **RootManageSharedAccessKey**. Siguiente tooyour principal clave de cadena de conexión, elija el botón Copiar de Hola.

    ![Copie la cadena de conexión del espacio de nombres de los Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm si la cadena de conexión está asociada con el espacio de nombres de los centros de eventos o con un concentrador de eventos específicos, comprobar la cadena de conexión de Hola Hola `EntityPath` parámetro. Si encuentra este parámetro, cadena de conexión de hello es para un centro de eventos específicos "entidad" y no es Hola cadena correcta toouse con la aplicación lógica.

4.  Ahora cuando se le pide credenciales después de agregar una aplicación centros de eventos desencadenador o acción tooyour lógica, puede conectar el espacio de nombres de tooyour centros de eventos. Asigne un nombre a la conexión, escriba la cadena de conexión de Hola que ha copiado y elija **crear**.

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Después de crear la conexión, nombre de la conexión de hello debe aparecer en el desencadenador de centros de eventos de Hola o acción. 
    A continuación, puede continuar con Hola otros pasos de la aplicación lógica.

    ![Conexión del espacio de nombres de los Event Hubs creada](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Iniciar el flujo de trabajo cuando el Event Hub recibe eventos nuevos

Un [*desencadenador*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que inicia un flujo de trabajo en la aplicación lógica. Para iniciar un flujo de trabajo cuando se envían eventos nuevos tooyour concentrador de eventos, siga estos pasos para agregar el desencadenador de Hola que detecta este evento.

1.  Hola [portal de Azure](https://portal.azure.com "portal de Azure"), vaya tooyour la aplicación lógica existente o cree una aplicación de lógica en blanco.

2.  En cuadro de búsqueda de Hola para hello diseñador la lógica de aplicación, escriba `event hubs` para el filtro. Seleccione este desencadenador: **Cuando los eventos estén disponibles en el Event Hub**

    ![Seleccione el desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Si aún no tiene un espacio de nombres de los centros de eventos de tooyour de conexión, se te pedirá toocreate ahora esta conexión. Asigne un nombre a la conexión y escriba la cadena de conexión de hello para el espacio de nombres de los centros de eventos. 
    Si es necesario, obtenga información acerca de [cómo toofind la cadena de conexión](#permissions-connection-string).

    ![Ingrese la cadena de conexión para el espacio de nombres de los Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Después de crear la conexión de hello, Hola configuración de hello **cuando un evento en disponibles en un centro de eventos** aparecen de desencadenador.

    ![Configuración del desencadenador para cuando el Event Hub reciba eventos nuevos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Escriba o seleccione el nombre Hola Hola concentrador de eventos que desea toomonitor. Seleccione la frecuencia de Hola y de intervalo para la frecuencia con la que desea que toocheck Hola concentrador de eventos.

    > [!TIP]
    > toooptionally seleccionar un grupo de consumidores para leer los eventos, elija **Mostrar opciones avanzadas**. 

    ![Especificar Event Hub o grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Ya ha configurado un desencadenador toostart un flujo de trabajo para la aplicación lógica. 
    La aplicación lógica comprueba Hola especificado en función de la programación de Hola que establezca el concentrador de eventos. 
    Si la aplicación busca nuevos eventos de hello concentrador de eventos, el desencadenador de hello ejecuta otras acciones o desencadenadores en la aplicación lógica.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Enviar eventos tooyour concentrador de eventos desde la aplicación lógica

Una [*acción*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica. Después de agregar una aplicación de lógica de desencadenador tooyour, puede agregar un operaciones tooperform de acción con los datos generados por este desencadenador. toosend un tooyour de evento concentrador de eventos de la aplicación lógica, siga estos pasos.

1.  En el Diseñador de aplicaciones lógicas, bajo el desencadenador de la aplicación lógica, elija **Nuevo paso** > **Agregar una acción**.

    ![Haga clic en "Nuevo paso" y en "Agregar una acción"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Ahora puede buscar y seleccionar un tooperform de acción. 
    Aunque puede seleccionar cualquier acción, en este ejemplo, queremos eventos de toosend de acción de hello centros de eventos.

2.  En el cuadro de búsqueda de hello, escriba `event hubs` para el filtro.
Seleccione esta acción: **Enviar evento**

    ![Seleccione la acción "Event Hubs: Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Escriba los detalles de hello necesario de evento de hello, como nombre de Hola para hello concentrador de eventos donde desea que los eventos de hello toosend. Escriba otros detalles acerca del evento hello, como el contenido para ese evento opcionales.

    > [!TIP]
    > toooptionally especificar partición del concentrador de eventos de Hola donde toosend Hola eventos, elija **Mostrar opciones avanzadas**. 

    ![Escriba el nombre del Event Hub y los detalles opcionales del evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Guarde los cambios.

    ![Guardado de la aplicación lógica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    Ahora ha configurado un toosend de eventos de acción de la aplicación lógica. 

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/eventhubs/). 

## <a name="get-help"></a>Obtener ayuda

tooask preguntas y responder a preguntas, consulte ¿Qué otros usuarios de aplicaciones de la lógica de Azure están realizando, visitan hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar la lógica de aplicaciones y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de las aplicaciones lógicas](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

*  [Encuentre otros conectores para Azure Logic apps](./apis-list.md)