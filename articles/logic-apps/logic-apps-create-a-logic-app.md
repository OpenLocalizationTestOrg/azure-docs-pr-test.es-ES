---
title: "aaaCreate el primer flujo de trabajo entre aplicaciones de nube y servicios en la nube: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Automatización de los procesos empresariales en escenarios de integración de aplicaciones empresariales (EAI) e integración de sistemas en Azure Logic Apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "flujo de trabajo, aplicaciones de nube, servicios en la nube, procesos empresariales, integración de sistemas, integración de aplicaciones empresariales, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Crear su primera aplicación de lógica de procesos de tooautomate de flujo de trabajo entre las aplicaciones de nube y servicios en la nube

Puede automatizar los procesos empresariales de manera más fácil y rápida cuando crea y ejecuta flujos de trabajo con [Azure Logic Apps](logic-apps-what-are-logic-apps.md), sin necesidad de escribir ningún código. Este primer ejemplo muestra cómo toocreate fuente de un flujo de trabajo de aplicación lógica básica que comprueba una RSS para el nuevo contenido en un sitio Web. Cuando aparezcan nuevos artículos de fuente de distribución del sitio Web de hello, aplicación de lógica de hello envía correo electrónico desde una cuenta de Outlook o Gmail.

toocreate y ejecutar una aplicación de lógica, necesita estos elementos:

* Una suscripción de Azure. Si no tiene una suscripción, puede [comenzar con una cuenta de Azure gratuita](https://azure.microsoft.com/free/). También puede [registrarse para obtener una suscripción de pago por uso](https://azure.microsoft.com/pricing/purchase-options/).

  Su suscripción de Azure se usa para facturar el uso de la aplicación lógica. Aprenda cómo funciona el [medidor de uso](../logic-apps/logic-apps-pricing.md) y los [precios](https://azure.microsoft.com/pricing/details/logic-apps) en Azure Logic Apps.

Además, para este ejemplo se necesitan estos elementos:

* Una cuenta de Outlook.com, Office 365 Outlook o Gmail.

    > [!TIP]
    > Si tiene una [cuenta de Microsoft](https://account.microsoft.com/account) personal, tiene una cuenta de Outlook.com. También, si tiene una cuenta de Azure profesional o educativa, tiene una cuenta de **Office 365 Outlook**.

* Un vínculo tooa la fuente RSS del sitio Web. Este ejemplo utiliza hello [fuente RSS para artículos destacados de sitio Web de CNN.com Hola](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Adición de un desencadenador que inicie el flujo de trabajo

A [ *desencadenador* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es un evento que se inicia el flujo de trabajo de aplicación lógica y es Hola primer elemento que necesita la aplicación lógica.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").

2. Desde el menú de la izquierda hello, elegir **nuevo** > **integración empresarial** > **aplicación lógica** tal y como se muestra aquí:

     ![Portal de Azure, Nuevo, Enterprise Integration, Logic App](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > También puede elegir **New**, a continuación, en el cuadro de búsqueda de hello, escriba `logic app`, y presione ENTRAR. A continuación, elija **Logic App** > **Crear**.

3. Asigne un nombre a la aplicación lógica y seleccione su suscripción de Azure. Ahora, cree o seleccione un grupo de recursos de Azure, que le ayuda a organizar y administrar los recursos de Azure relacionados. Por último, seleccione la ubicación de centro de datos de Hola para hospedar la aplicación lógica. Cuando esté listo, elija **Pin toodashboard** y, a continuación, **crear**.

     ![Detalles de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Cuando se selecciona **toodashboard Pin**, la aplicación lógica aparece en hello Azure panel después de la implementación y se abre automáticamente. Si la aplicación lógica no aparece en panel de hello, vaya a hello **todos los recursos** icono, elija **vea más**y seleccione la aplicación lógica. O, en el menú de la izquierda hello, elija **más servicios**. En **Enterprise Integration**, elija **Logic Apps** y seleccione su aplicación lógica.

4. Cuando se abre la aplicación lógica para hello primera vez, Hola lógica de aplicación diseñador muestra plantillas que puede usar tooget iniciado. Por ahora, elija **Aplicación lógica en blanco** para que pueda crear la aplicación lógica desde el principio.

    Hello lógica de aplicación diseñador se abre y muestra los servicios disponibles y *desencadenadores* que puede usar en la aplicación lógica.

5. En el cuadro de búsqueda de hello, escriba `RSS`y seleccione este desencadenador: **RSS - cuando se publica un elemento de fuente** 

    ![Desencadenador de RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Especifique el vínculo de Hola de fuente RSS del sitio Web de Hola que desea tootrack. 

     También puede cambiar la **frecuencia** y el **intervalo**. 
     Esta configuración determina la frecuencia con que la aplicación lógica busca nuevos elementos y devuelve todos los elementos encontrados durante ese intervalo de tiempo.

     En este ejemplo, vamos a comprobar cada día para casos superiores registra el sitio Web CNN toohello.

     ![Configuración del desencadenador con la fuente RSS, la frecuencia y el intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Por ahora, guarde el trabajo. (En la barra de comandos del Diseñador de hello, elija **guardar**.)

   ![Guardado de la aplicación lógica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Cuando guarda, poner en marcha la aplicación lógica, pero en la actualidad, la aplicación lógica sólo busca nuevos elementos en hello Especifica fuente RSS. 
   toomake se activa en este ejemplo más útil, que agregamos una acción que realiza la aplicación lógica el desencadenador after.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Agregar una acción que responde el desencadenador de tooyour

Una [*acción*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) es una tarea realizada por el flujo de trabajo de la aplicación lógica. Después de agregar una aplicación de lógica de desencadenador tooyour, puede agregar un operaciones tooperform de acción con los datos generados por este desencadenador. En nuestro ejemplo, ahora se agregue una acción que envía el correo electrónico cuando aparezcan nuevos artículos en la fuente de RSS del sitio Web de Hola.

1. En el Diseñador de hello, en el desencadenador, elija **nuevo paso** > **agregar una acción** tal y como se muestra aquí:

   ![Agregar una acción](media/logic-apps-create-a-logic-app/add-new-action.png)

   Hola diseñador muestra [conectores disponibles](../connectors/apis-list.md) para que pueda seleccionar una acción tooperform cuando se activa el desencadenador.

2. En función de su cuenta de correo electrónico, siga los pasos de Hola para Outlook o Gmail.

   * correo electrónico toosend de su cuenta de Outlook, en el cuadro de búsqueda de hello, escriba `outlook`. En **Servicios**, elija **Outlook.com** para cuentas de Microsoft personales, o elija **Office 365 Outlook** para cuentas de Azure profesionales o educativas. 
   En **Acciones**, seleccione **Enviar un correo electrónico**.

       ![Selección de la acción "Enviar un correo electrónico" de Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * correo electrónico toosend de su cuenta de Gmail, en el cuadro de búsqueda de hello, escriba `gmail`. 
   En **Acciones**, seleccione **Enviar un correo electrónico**.

       ![Selección de "Gmail: Enviar un correo electrónico"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Cuando se le pidan las credenciales, inicie sesión con hello username y password para su cuenta de correo electrónico. 

4. Proporcionar detalles de Hola para esta acción, como la dirección de correo electrónico de destino de hello y elegir parámetros Hola Hola datos tooinclude del correo electrónico de hello, por ejemplo:

   ![Seleccione tooinclude de datos de correo electrónico](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Si eligió Outlook, la aplicación lógica podría parecerse a este ejemplo:

    ![Aplicación lógica completada](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Guarde los cambios. (En la barra de comandos del Diseñador de hello, elija **guardar**.)

6. Ahora puede ejecutar manualmente la aplicación lógica para realizar pruebas. En la barra de comandos del Diseñador de hello, elija **ejecutar**. En caso contrario, puede dejar que la aplicación lógica comprobar Hola especificado fuente RSS basada en programación de Hola que configuró.

   Si la aplicación lógica busca nuevos elementos, aplicación de lógica de hello envía correo electrónico que incluirá los datos seleccionados. 
   Si no se encuentra ningún elemento nuevo, la aplicación lógica omite la acción de Hola que envía un correo electrónico.

7. toomonitor y comprobación de la aplicación lógica de ejecución de la y desencadenar historial, en el menú de aplicación lógica, eligen **Introducción**.

   ![Supervisión y visualización del historial de ejecución y desencadenamiento de la aplicación lógica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Si no encuentra datos Hola que espera, en la barra de comandos de hello, pruebe a elegir **actualizar**.

   toolearn más información sobre el estado de la aplicación lógica o ejecute y desencadenar historial o toodiagnose la aplicación lógica, consulte [solucionar problemas de la aplicación lógica](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > La aplicación lógica continúa ejecutándose hasta que desactiva la aplicación. Elija tooturn desactivar la aplicación por ahora, en el menú de aplicación lógica, **Introducción**. En la barra de comandos de hello, elija **deshabilitar**.

Enhorabuena, acaba de configurar y ejecutar la primera aplicación lógica básica. También ha aprendido cómo puede crear fácilmente flujos de trabajo que automatizan los procesos, y a integrar aplicaciones de nube y servicios en la nube sin necesidad de código.

## <a name="manage-your-logic-app"></a>Administración de la aplicación lógica

toomanage la aplicación, puede realizar tareas como comprobar el estado de hello, editar, ver el historial, desactivar o eliminar la aplicación lógica.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").

2. En el menú de la izquierda hello, elija **más servicios**. En **Enterprise Integration**, elija **Logic Apps**. Seleccione la aplicación lógica. 

   En el menú de la aplicación de lógica de hello, puede encontrar estas tareas de administración de aplicación lógica:

   |Tarea|Pasos| 
   |:---|:---| 
   | Ver el estado de la aplicación, el historial de ejecución e información general| Elija **Overview** (Información general).| 
   | Editar la aplicación | Elija **Diseñador de aplicación lógica**. | 
   | Ver la definición JSON del flujo de trabajo de la aplicación | Elija **Vista de código de aplicación lógica**. | 
   | Ver las operaciones realizadas en la aplicación lógica | Elija **Registro de actividad**. | 
   | Ver las versiones pasadas de la aplicación lógica | Elija **Versiones**. | 
   | Desactivar la aplicación temporalmente | Elija **Introducción**, a continuación, en la barra de comandos de hello, elija **deshabilitar**. | 
   | Eliminar la aplicación | Elija **Introducción**, a continuación, en la barra de comandos de hello, elija **eliminar**. Escriba el nombre de la aplicación lógica y elija **Eliminar**. | 

## <a name="get-help"></a>Obtener ayuda

tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

*  [Adición de condiciones y ejecución de flujos de trabajo](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Plantillas de aplicaciones lógicas](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Creación de aplicaciones lógicas a partir de plantillas de Azure Resource Manager](../logic-apps/logic-apps-arm-provision.md)
