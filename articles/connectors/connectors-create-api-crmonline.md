---
title: "aaaConnect tooDynamics 365 (con conexión) de las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Crear la lógica de flujos de trabajo de aplicación que Administración entidades (online) de Dynamics 365 a través de la API proporcionada por el conector de Dynamics 365 Hola Hola"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Conectar tooDynamics 365 de flujos de trabajo de aplicación lógica

Con las aplicaciones lógicas, puede conectarse tooDynamics 365 (con conexión) y crear flujos empresariales útiles que crean registros, actualizan los elementos o devuelven una lista de registros. Con el conector de hello Dynamics 365, puede:

* Genera el flujo de negocios basado en datos de hello que obtendrá de Dynamics 365 (con conexión).
* Use las acciones que obtención una respuesta y, a continuación, tome salida de hello disponibles para las demás acciones. Por ejemplo, cuando se actualice un elemento en Dynamics 365 (en línea), puede enviar un correo electrónico mediante Office 365.

Este tema muestra cómo toocreate una lógica de aplicación que crea una tarea en Dynamics 365 cada vez que se crea un nuevo cliente potencial en Dynamics 365.

## <a name="prerequisites"></a>Requisitos previos
* Una cuenta de Azure.
* Una cuenta de Dynamics 365 (en línea).

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Creación de una tarea cuando se crea un nuevo cliente potencial en Dynamics 365

1.  [Inicie sesión en tooAzure](https://portal.azure.com).

2.  En el cuadro de búsqueda de Azure de hello, escriba `Logic apps`, y presione ENTRAR.

      ![Búsqueda de Logic Apps](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  En **Logic Apps**, haga clic en **Agregar**.

      ![Agregar LogicApp](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  aplicación de lógica de hello toocreate, Hola completa **nombre**, **suscripción**, **grupo de recursos**, y **ubicación** campos y, a continuación, haga clic en  **Crear**.

5.  Seleccione la aplicación lógica de la nueva Hola. Cuando aparezca el Hola **se implementó correctamente** notificación, haga clic en **actualizar**.

6.  En **Herramientas de desarrollo**, haga clic en **Diseñador de aplicación lógica**. En la lista de plantillas de hello, haga clic en **en blanco de lógica de aplicación**.

7.  En el cuadro de búsqueda de hello, escriba `Dynamics 365`. Desde Hola Dynamics 365 desencadena la lista, seleccione **Dynamics 365: cuando se crea un registro**.

8.  Si está toosign solicitada en tooDynamics 365, hágalo ahora.

9.  En detalles de desencadenador de hello, escriba Hola siguiente información:

  * **Nombre de la organización**. Seleccione la instancia de Dynamics 365 de Hola que desee toolisten de aplicación lógica de Hola a.

  * **Nombre de entidad**. Seleccione la entidad de Hola que desee toolisten a. Este evento actúa como una aplicación de lógica de desencadenador toostart Hola. 
  En este tutorial está seleccionado **Leads**.

  * **¿Con qué frecuencia desea toocheck para elementos?** Estos valores se configuran la frecuencia con aplicación de lógica de hello busca desencadenador toohello relacionadas de las actualizaciones. saludo predeterminado es toocheck actualizaciones cada tres minutos.

    * **Frecuencia**. Seleccione segundos, minutos, horas o días.

    * **Intervalo**. Escriba Hola número de segundos, minutos, horas o días en los que desee toopass antes de la siguiente comprobación de Hola.

      ![Detalles del desencadenador de aplicación lógica](./media/connectors-create-api-crmonline/trigger-details.png)

10. Haga clic en **Nuevo paso** y, a continuación, en **Agregar una acción**.

11. En el cuadro de búsqueda de hello, escriba `Dynamics 365`. En la lista de acciones de hello, seleccione **Dynamics 365: crear un nuevo registro**.

12. Escriba Hola siguiente información:

    * **Nombre de la organización**. Seleccione la instancia de hello Dynamics 365 donde desea que el registro de hello flujo toocreate Hola. 
    Observe que esta instancia no tiene toobe Hola misma instancia donde se desencadena el evento de Hola de.

    * **Nombre de entidad**. Seleccione la entidad de Hola que desea toocreate un registro cuando se desencadene el evento de Hola. 
    En este tutorial está seleccionado **Tasks**.

13. Haga clic en hello **asunto** cuadro que aparece. De hello contenido lista dinámica que aparece, puede seleccionar cualquiera de estos campos:

    * **Apellido**. Al seleccionar este campo inserta last name de Hola de hello responsable campo Asunto Hola tarea hello, cuando se crea el registro de la tarea de Hola.
    * **Tema**. Seleccionar este campo inserciones Hola tema campo cliente potencial de hello en el campo de asunto de hello para la tarea hello, cuando se crea registro de tareas de Hola. 
    Haga clic en **tema** tooadd ese toohello **asunto** cuadro.

      ![Creación de detalles del nuevo registro en la aplicación lógica](./media/connectors-create-api-crmonline/create-record-details.png)

14. En la barra de herramientas del Diseñador de la aplicación lógica hello, haga clic en **guardar**.

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. Hola toostart lógica de aplicación, haga clic en **ejecutar**.

    ![Guardado en la barra de herramientas del Diseñador de aplicación lógica](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Ahora cree un registro de cliente potencial en Dynamics 365 para Ventas y podrá ver el flujo en acción.

## <a name="set-advanced-options-for-a-logic-app-step"></a>Establecimiento de opciones avanzadas para un paso de aplicación lógica

toospecify cómo toofilter datos en un paso de aplicación lógica, haga clic en **Mostrar opciones avanzadas** en ese paso, a continuación, agregue un filtro o un pedido por consulta.

Por ejemplo, puede usar un filtro consulta tooget sólo las cuentas activas y se ordena por nombre de la cuenta de hello. tooperform esta tarea, escriba la consulta de filtro de OData de hello `statuscode eq 1`y seleccione **nombre de la cuenta** de lista de contenido dinámico de Hola. Para más información consulte: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) y [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Opciones avanzadas de la aplicación lógica](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Procedimientos recomendados al usar las opciones avanzadas

Cuando se agrega un campo de valor tooa, debe coincidir con el tipo de campo de hello si escribe un valor o seleccione un valor de la lista de contenido dinámico de Hola.

Tipo de campo  |Cómo toouse  |Donde toofind  |Nombre  |Tipo de datos  
---------|---------|---------|---------|---------
Campos de texto|Los campos de texto requieren una sola línea de texto o contenido dinámico que sea un campo de tipo texto. Algunos ejemplos son campos de categoría y subcategoría de Hola.|Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos |categoría |Línea de texto única        
Campos numéricos enteros | Algunos campos requieren un número entero o un contenido dinámico que sea un campo de tipo numérico entero. Algunos ejemplos son Porcentaje completado y Duración. |Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos |percentcomplete |Número entero         
Campos de fecha | Algunos campos, requieren una fecha escrita en formato mm/dd/aaaa o contenido dinámico que sea un campo de tipo de fecha. Algunos ejemplos son fecha de creación, fecha de inicio, inicio real, último periodo de retención, finalización real y fecha de vencimiento. | Configuración > personalizaciones > Personalizar Hola sistema > entidades > tareas > campos |createdon |Fecha y hora
Campos que requieren un identificador de registro y un tipo de búsqueda |Algunos campos que hacen referencia a otro registro de entidad requieren Id. de registro de hello y tipo de búsqueda de Hola. |Configuración > personalizaciones > Personalizar Hola sistema > entidades > cuenta > campos  | accountid  | Clave principal

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Más ejemplos de campos que requieren tanto un identificador de registro como un tipo de búsqueda
Expandir en la tabla anterior de hello, presentamos más ejemplos de campos que no funcionan con los valores seleccionados de la lista de contenido dinámico de Hola. En su lugar, estos campos requieren tanto un Id. y búsqueda de tipo de registro especificado en los campos de hello en PowerApps.  
* Propietario y Tipo de propietario. campo de propietario de Hello debe ser un identificador válido usuario o equipo de registro. Hola, tipo de propietario debe ser **systemusers** o **equipos**.
* Cliente y Tipo de cliente. campo de cliente Hello debe ser una cuenta válida o póngase en contacto con el identificador de registro. Hola, tipo de propietario debe ser **cuentas** o **contactos**.
* Referente a y Tipo referente a. Hola en relación con el campo debe ser un identificador de registro válido, como una cuenta o póngase en contacto con el identificador de registro. Hello en relación con tipo debe ser Hola búsqueda para registro de hello, como **cuentas** o **contactos**.

Hello siguiente ejemplo de acción de creación de tarea agrega un registro de cuenta que se corresponde el Id. de registro de toohello agregar toohello con respecto a los campos de tarea hello.

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-account.png)

En este ejemplo también asigna a hello tooa específico usuario de la tarea en función de Id. de usuario de Hola

![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind un registro del identificador, consulte los pasos de la sección de Hola: *encuentra el Id. de registro de hello*

## <a name="find-hello-record-id"></a>Encuentra el Id. de registro de hello

1. Abra un registro, como un registro de cuenta.

2. En la barra de herramientas de hello acciones, haga clic en **emergente** ![registro emergente](./media/connectors-create-api-crmonline/popout-record.png).
O bien, en barra de herramientas de acciones de hello, toocopy Hola dirección URL completa en el programa de correo electrónico predeterminado, haga clic en **correo electrónico un vínculo**.

   Id. de registro de Hello se muestra entre Hola 7b y %7 %d) la codificación de caracteres de la dirección URL de Hola.

   ![Identificador de registro de flujo y tipo de cuenta](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Solución de problemas
tootroubleshoot un paso con errores en una aplicación de lógica, ver detalles de estado de Hola de evento Hola.

1. En **Logic Apps**, seleccione la aplicación lógica y haga clic en **Información general**. 

   Hola área de resumen se muestra y proporciona Hola ejecutar el estado de aplicación lógica de hello. 

   ![Estado de ejecución de la aplicación lógica](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview obtener más información acerca de todas las ejecuciones de error, haga clic en hello no se pudo eventos. tooexpand un paso con errores, haga clic en ese paso.

   ![Expansión del paso con errores](./media/connectors-create-api-crmonline/tshoot2.png)

   detalles de pasos de Hello aparecen y pueden ayudar a solucionar Hola causa del error de Hola.

   ![Detalles del paso con errores](./media/connectors-create-api-crmonline/tshoot3.png)

Para más información sobre cómo solucionar problemas de las aplicaciones lógicas, consulte [Diagnóstico de errores de aplicaciones lógicas](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/crm/). 

## <a name="next-steps"></a>Pasos siguientes
Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).
