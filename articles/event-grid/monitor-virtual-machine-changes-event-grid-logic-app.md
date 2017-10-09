---
title: "Cambie la máquina virtual aaaMonitor - Logic Apps & cuadrícula de eventos de Azure | Documentos de Microsoft"
description: "Compruebe si hay cambios de configuración en las máquinas virtuales (VM) mediante el uso de Azure Event Grid y Logic Apps"
keywords: "aplicaciones lógicas, cuadrículas de eventos, máquina virtual, VM"
services: logic-apps
author: ecfan
manager: anneta
ms.assetid: 
ms.workload: logic-apps
ms.service: logic-apps
ms.topic: article
ms.date: 08/16/2017
ms.author: LADocs; estfan
ms.openlocfilehash: f0633e598be6e7880a310e6f8e64f6738cc692b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-changes-with-azure-event-grid-and-logic-apps"></a>Supervisión de los cambios en máquinas virtuales con Azure Event Grid y Logic Apps

Puede iniciar automáticamente el [flujo de trabajo de una aplicación lógica](../logic-apps/logic-apps-what-are-logic-apps.md) cuando se producen eventos específicos en recursos de Azure o de otros fabricantes. Estos recursos pueden publicar esos eventos tooan [cuadrícula de eventos Azure](../event-grid/overview.md). A su vez, la cuadrícula de eventos de Hola inserta esos toosubscribers de eventos que tienen las colas, webhook, o [centros de eventos](../event-hubs/event-hubs-what-is-event-hubs.md) como puntos de conexión. Como suscriptor, puede esperar la aplicación lógica de los eventos de la cuadrícula de eventos de hello antes de ejecutar flujos de trabajo automatizados tareas tooperform - sin que escribir ningún código.

Por ejemplo, incluimos algunos eventos que publicadores pueden enviar toosubscribers a través del servicio Hola cuadrícula de eventos de Azure:

* Crear, leer, actualizar o eliminar un recurso. Por ejemplo, puede supervisar los cambios que podrían incurrir en gastos en su suscripción de Azure y afectar a la facturación. 
* Agregar o quitar a una persona de una suscripción de Azure.
* La aplicación realiza una acción concreta.
* Aparece un nuevo mensaje en una cola.

Este tutorial crea una aplicación de lógica que supervisa la máquina virtual de tooa de cambios y envía mensajes de correo electrónico sobre dichos cambios. Cuando se crea una aplicación de lógica con una suscripción de eventos para un recurso de Azure, flujo de eventos de ese recurso a través de una aplicación de lógica de toohello de cuadrícula de eventos. Hola tutorial le guía por la creación de esta aplicación lógica:

![Introducción: Supervisión de los cambios en máquinas virtuales con Azure Event Grid y Logic Apps](./media/monitor-virtual-machine-changes-event-grid-logic-app/monitor-virtual-machine-event-grid-logic-app-overview.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una aplicación lógica que supervisa eventos procedentes de una cuadrícula de eventos.
> * Incorporar una condición que comprueba específicamente cambios en la máquina virtual.
> * Enviar un mensaje de correo electrónico cuando la máquina virtual cambia.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta de correo electrónico de [cualquier proveedor de correo electrónico que sea compatible con Azure Logic Apps](../connectors/apis-list.md), como Office 365 Outlook, Outlook.com o Gmail, para el envío de notificaciones. Este tutorial usa Office 365 Outlook.

* Una [máquina virtual](https://azure.microsoft.com/services/virtual-machines). Si aún no lo ha hecho, cree una máquina virtual siguiendo un [tutorial para crear una máquina virtual](https://docs.microsoft.com/azure/virtual-machines/). máquina virtual de toomake Hola publicar eventos, se [no es necesario toodo nada](../event-grid/overview.md).

## <a name="create-a-logic-app-that-monitors-events-from-an-event-grid"></a>Creación de una aplicación lógica que supervisa eventos procedentes de una cuadrícula de eventos

En primer lugar, cree una aplicación de la lógica y agregar un desencadenador de la cuadrícula de eventos que supervisa el grupo de recursos de hello para la máquina virtual. 

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com). 

2. En hello esquina superior izquierda del menú de Azure principal hello, elija **New** > **integración empresarial** > **aplicación lógica**.

   ![Creación de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/azure-portal-create-logic-app.png)

3. Crear la aplicación lógica con valores de hello especificados en hello en la tabla siguiente:

   ![Proporcione los detalles de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/create-logic-app-for-event-grid.png)

   | Configuración | Valor sugerido | Descripción | 
   | ------- | --------------- | ----------- | 
   | **Name** | *{nombre-de-la-aplicación-lógica}* | Proporcione un nombre único de aplicación lógica. | 
   | **Suscripción** | *{su-suscripción-de-Azure}* | Seleccione Hola misma suscripción de Azure para todos los servicios en este tutorial. | 
   | **Grupos de recursos** | *{su-grupo-de-recursos-de-Azure}* | Seleccione Hola mismo grupo de recursos de Azure para todos los servicios en este tutorial. | 
   | **Ubicación** | *{su-región-de-Azure}* | Seleccione Hola misma región para todos los servicios en este tutorial. | 
   | | | 

4. Cuando esté listo, seleccione **Pin toodashboard**y elija **crear**.

   Ahora ha creado un recurso de Azure para la aplicación lógica. 
   Después de Azure implementa la lógica de aplicación, Hola lógica el Diseñador de aplicaciones muestra plantillas para los patrones comunes para que pueda empezar a más rápido.

   > [!NOTE] 
   > Cuando se selecciona **toodashboard Pin**, la aplicación lógica se abre automáticamente en el Diseñador de aplicaciones de la lógica. En caso contrario, puede buscarla y abrirla manualmente.

5. Ahora elija una plantilla de aplicación lógica. En **Plantillas**, elija **Aplicación lógica en blanco** para que pueda crear la aplicación lógica desde el principio.

   ![Selección de la plantilla de aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/choose-logic-app-template.png)

   Hola lógica el Diseñador de aplicaciones muestra ahora [ *conectores* ](../connectors/apis-list.md) y [ *desencadenadores* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) que puede usar toostart la aplicación lógica y también acciones que puede agregar después de una tarea de tooperform de desencadenador. Un desencadenador es un evento que crea una instancia de aplicación lógica e inicia el flujo de trabajo de la aplicación lógica. 
   Necesita un desencadenador en la aplicación de lógica como primer elemento de Hola.

6. En el cuadro de búsqueda de hello, escriba "cuadrícula de eventos" como filtro. Seleccione este desencadenador: **Azure Event Grid - On a resource event**

   ![Seleccione este desencadenador: "Azure Event Grid - On a resource event"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger.png)

7. Cuando se le solicite, inicie sesión en tooAzure cuadrícula de eventos con sus credenciales de Azure.

   ![Inicie sesión con sus credenciales de Azure](./media/monitor-virtual-machine-changes-event-grid-logic-app/sign-in-event-grid.png)

   > [!NOTE]
   > Si iniciaste sesión con una cuenta Microsoft personal, como @outlook.com o @hotmail.com, desencadenador de cuadrícula de eventos de hello no aparezcan correctamente. Como alternativa, elija [conectar con entidad de servicio](/azure-resource-manager/resource-group-create-service-principal-portal.md), o autenticarse como un miembro del programa Hola a Azure Active Directory que está asociada la suscripción de Azure, por ejemplo, *nombre de usuario* @emailoutlook.onmicrosoft.com.

8. Suscribirse ahora los eventos de toopublisher de aplicación lógica. Se proporcionan detalles de Hola para su suscripción a eventos como se especifica en hello en la tabla siguiente:

   ![Proporcione detalles de la suscripción de eventos](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details-generic.png)

   | Configuración | Valor sugerido | Descripción | 
   | ------- | --------------- | ----------- | 
   | **Suscripción** | *{suscripción-de-Azure-de-la-máquina-virtual}* | Seleccione la suscripción de Azure del publicador de eventos de Hola. Para este tutorial, seleccione Hola suscripción de Azure para la máquina virtual. | 
   | **Tipo de recurso** | Microsoft.Resources.resourceGroups | Seleccione el tipo de recurso del publicador de eventos de Hola. Para este tutorial, seleccione Hola valor especificado para que la aplicación lógica supervisa solo los grupos de recursos. | 
   | **Nombre de recurso** | *{nombre-del-grupo-de-recursos-de-la-máquina-virtual}* | Seleccione el nombre del recurso del Editor de Hola. Para este tutorial, seleccione el nombre de Hola Hola del grupo de recursos para la máquina virtual. | 
   | Para configuraciones opcionales, elija **Mostrar opciones avanzadas**. | *{ver descripciones}* | * **Filtro de prefijo**: en este tutorial, deje esta opción vacía. comportamiento predeterminado de Hello coincide con todos los valores. Sin embargo, puede especificar una cadena de prefijo como un filtro, por ejemplo, una ruta de acceso y un parámetro para un recurso concreto. <p>* **Filtro de sufijo**: en este tutorial, deje esta opción vacía. comportamiento predeterminado de Hello coincide con todos los valores. Sin embargo, puede especificar una cadena de sufijo como un filtro, por ejemplo, una extensión de nombre de archivo, si desea solo determinados tipos de archivos.<p>* **Nombre de la suscripción**: proporcione un nombre único para la suscripción a eventos. |
   | | | 

   Cuando haya terminado, el desencadenador de Event Grid podría parecerse a este ejemplo:
   
   ![Detalles del desencadenador de cuadrícula de eventos de ejemplo](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-trigger-details.png)

9. Guarde la aplicación lógica. En la barra de herramientas del diseñador hello, elija **guardar**. toocollapse y ocultar los detalles de una acción en la aplicación lógica, elija barra de título de la acción de Hola.

   ![Guardado de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save.png)

   Cuando se guarda la aplicación lógica con un desencadenador de la cuadrícula de eventos, Azure crea automáticamente una suscripción de eventos para el recurso de tooyour seleccionado de aplicación lógica. Por lo que al recurso Hola publica una cuadrícula de eventos de eventos toohello, dicha cuadrícula de eventos inserta automáticamente aplicación lógica de hello eventos tooyour. Este evento desencadena la lógica de aplicación, a continuación, crea y ejecuta una instancia de flujo de trabajo de Hola que defina en los pasos siguientes.

La aplicación lógica está ahora en vivo y escucha tooevents de cuadrícula de eventos de hello, pero no hace nada hasta que agregue el flujo de trabajo de acciones toohello. 

## <a name="add-a-condition-that-checks-for-virtual-machine-changes"></a>Incorporación de una condición que comprueba los cambios de la máquina virtual

toorun el flujo de trabajo de aplicación lógica sólo cuando se produce un evento específico, agregar una condición que se comprueba para la máquina virtual "operaciones de escritura". Cuando esta condición sea true, la aplicación lógica envía que enviar por correo electrónico con detalles acerca de la máquina virtual de hello actualizado.

1. En el Diseñador de lógica de aplicación, en el desencadenador de cuadrícula de eventos de hello, elija **nuevo paso** > **agregar una condición**.

   ![Agregar una aplicación de lógica de condición tooyour](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-add-condition-step.png)

   Hola lógica de aplicación diseñador agrega un flujo de trabajo de tooyour condición vacío, incluidos toofollow de rutas de acceso de acción en función de si la condición de hello es true o false.

   ![Condición vacía](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-add-empty-condition.png)

2. Hola **condición** cuadro, elija **editar en el modo avanzado**.
Escriba esta expresión:

   `@equals(triggerBody()?['data']['operationName'], 'Microsoft.Compute/virtualMachines/write')`

   Ahora, la condición es similar a este ejemplo:

   ![Condición vacía](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-expression.png)

   Esta expresión comprueba los eventos de hello `body` para un `data` objeto donde hello `operationName` propiedad es hello `Microsoft.Compute/virtualMachines/write` operación. 
   Más información sobre el [Esquema de eventos de la cuadrícula de eventos](../event-grid/event-schema.md).

3. tooprovide una descripción para la condición de hello, elija hello **puntos suspensivos** (**...** ) en forma de condición de hello, a continuación, elija **cambiar el nombre de**.

   > [!NOTE] 
   > Hello ejemplos más adelante en este tutorial también proporcionan descripciones para los pasos de flujo de trabajo de aplicación de lógica de Hola.

4. Ahora elija **editar en modo básico** para que la expresión de hello resuelve automáticamente como se muestra:

   ![Condición de aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-1.png)

5. Guarde la aplicación lógica.

## <a name="send-email-when-your-virtual-machine-changes"></a>Envío de un mensaje de correo electrónico cuando la máquina virtual cambia

Ahora, agregue un [ *acción* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) para que obtenga un correo electrónico cuando Hola especifica la condición es true.

1. En la condición de hello **si es true** cuadro, elija **agregar una acción**.

   ![Agregar una acción para cuando la condición se cumpla](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-condition-2.png)

2. En el cuadro de búsqueda de hello, escriba "email" como filtro. En función de su proveedor de correo electrónico, busque y seleccione conector coincidente Hola. A continuación, seleccione la acción "enviar correo electrónico" de hello para el conector. Por ejemplo: 

   * Para un Azure cuenta profesional o educativa, conector de Outlook de Office 365 Hola select. 
   * Para las cuentas de Microsoft personales, seleccione el conector de Outlook.com de Hola. 
   * Las cuentas de Gmail, seleccione el conector de Gmail de Hola. 

   Vamos a toocontinue con el conector de Outlook de Office 365 Hola. 
   Si utiliza un proveedor diferente, Hola Hola pasos permanecen iguales, pero la interfaz de usuario sería diferente. 

   ![Seleccione la acción "send email"](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email.png)

3. Si ya no tiene una conexión para el proveedor de correo electrónico, inicie sesión en la cuenta de correo electrónico de tooyour cuando se le pregunte para la autenticación.

4. Se proporcionan detalles para correo electrónico de hello como se especifica en hello en la tabla siguiente:

   ![Acción de correo electrónico vacía](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-empty-email-action.png)

   > [!TIP]
   > tooselect de los campos disponibles en el flujo de trabajo, haga clic en un cuadro de edición por lo que ese hello **contenido dinámico** lista abre o elija **agregar contenido dinámico**. Para más campos, elija **ver más** para cada sección de la lista de Hola. Hola tooclose **contenido dinámico** elija **agregar contenido dinámico**.

   | Configuración | Valor sugerido | Descripción | 
   | ------- | --------------- | ----------- | 
   | **To** | *{dirección-de-correo electrónico-del-destinatario}* |Escriba la dirección de correo electrónico del destinatario de Hola. Para realizar pruebas, puede usar su propia dirección de correo electrónico. | 
   | **Asunto** | Recurso actualizado: **Asunto**| Introduzca el contenido de Hola de asunto del correo electrónico Hola. En este tutorial, escriba Hola sugiere texto y del evento select hello **asunto** campo. En este caso, el asunto del correo electrónico incluye nombre hello para el recurso de hello actualizado (máquina virtual). | 
   | **Cuerpo** | Grupo de recursos: **Tema** <p>Tipo de evento: **Tipo de evento**<p>Identificador del evento: **ID**<p>Hora: **Hora del evento** | Introducir contenido de hello en el cuerpo del correo electrónico Hola. En este tutorial, escriba Hola sugiere texto y del evento select hello **tema**, **tipo de evento**, **identificador**, y **hora del evento** campos para que el correo electrónico incluye el nombre del grupo de recursos de hello, tipo de evento, marca de tiempo del evento e Id. de evento de actualización de Hola. <p>tooadd líneas en blanco en el contenido, presione MAYÚS + ENTRAR. | 
   | | | 

   > [!NOTE] 
   > Si selecciona un campo que representa una matriz, Hola diseñador agrega automáticamente un **para cada** trazo alrededor de la acción de Hola que hace referencia la matriz de Hola. De este modo, la aplicación lógica realiza la acción en cada elemento de la matriz.

   Ahora, la acción de correo electrónico podría parecerse a este ejemplo:

   ![Seleccione tooinclude de salidas de correo electrónico](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-send-email-details.png)

   Y la aplicación lógica terminada podría parecerse a este ejemplo:

   ![Aplicación lógica terminada](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-completed.png)

5. Guarde la aplicación lógica. toocollapse y ocultar detalles de cada acción en la aplicación lógica, elija la barra de título de la acción de Hola.

   ![Guardado de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-event-grid-save-completed.png)

   La aplicación lógica ahora está activa, pero espera para la máquina virtual de tooyour de cambios antes de hacer nada. 
   tootest la lógica de aplicación, para seguir toohello próxima sección.

## <a name="test-your-logic-app-workflow"></a>Comprobación del flujo de trabajo de la aplicación lógica

1. toocheck que la aplicación lógica está obteniendo Hola eventos especificados, actualice la máquina virtual. 

   Por ejemplo, puede cambiar el tamaño de la máquina virtual en el portal de Azure de Hola o [cambiar el tamaño de la máquina virtual con Azure PowerShell](../virtual-machines/windows/resize-vm.md). 

   Transcurridos unos instantes, debería recibir un correo electrónico. Por ejemplo:

   ![Correo electrónico acerca de la actualización de una máquina virtual](./media/monitor-virtual-machine-changes-event-grid-logic-app/email.png)

2. Hola tooreview se ejecuta e historial de desencadenador para la aplicación lógica, en el menú de aplicación lógica, elija **Introducción**. tooview más detalles acerca de una ejecución, elija fila hello para el que se ejecutan.

   ![Historial de ejecuciones de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history.png)

3. entradas de hello tooview y los resultados de cada paso, expanda paso Hola que desea tooreview. Esta información puede ayudarle a diagnosticar y depurar los problemas de la aplicación lógica.
 
   ![Detalles del historial de ejecución de la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/logic-app-run-history-details.png)

Enhorabuena, ha creado y ejecutado una aplicación lógica que supervisa los eventos del recurso mediante una cuadrícula de eventos y le envía por correo electrónico un mensaje cuando se producen esos eventos. También ha aprendido cómo puede crear fácilmente flujos de trabajo que automatizan los procesos y a integrar sistemas y servicios en la nube.

## <a name="clean-up-resources"></a>Limpieza de recursos

Este tutorial utiliza recursos y realiza acciones que generan gastos en su suscripción de Azure. Por lo que cuando haya terminado con el tutorial de Hola y de prueba, asegúrese de que se deshabilite o elimine todos los recursos cuando no se desea tooincur cargos.

Puede detener la aplicación lógica de ejecución y enviar correo electrónico sin eliminar la aplicación hello. En el menú de la aplicación lógica, elija **Overview** (Información general). En la barra de herramientas de hello, elija **deshabilitar**.

![Desactive la aplicación lógica](./media/monitor-virtual-machine-changes-event-grid-logic-app/turn-off-disable-logic-app.png)

## <a name="faq"></a>P+F

**P**: ¿Qué otras tareas de supervisión de máquinas virtuales puedo realizar con cuadrículas de eventos y aplicaciones lógicas? </br>
**R**: Puede supervisar otros cambios de configuración, por ejemplo:

* Una máquina virtual obtiene derechos de control de acceso basado en roles (RBAC).
* El grupo de seguridad de red de tooa (NSG) en una interfaz de red (NIC), se realizan cambios.
* Los discos para una máquina virtual se agregan o se quitan.
* Una dirección IP pública se asigna la NIC de tooa máquina virtual.

## <a name="next-steps"></a>Pasos siguientes

* [Información general sobre la cuadrícula de eventos](../event-grid/overview.md)
* [Conceptos sobre la cuadrícula de eventos](../event-grid/concepts.md)
* [Inicio rápido: Creación y enrutamiento de eventos personalizados con Azure Event Grid](../event-grid/custom-event-quickstart.md)
* [Esquema de eventos de Event Grid](../event-grid/event-schema.md)
* [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)
* [Creación de flujos de trabajo de aplicación lógica con plantillas predefinidas](../logic-apps/logic-apps-use-logic-app-templates.md)