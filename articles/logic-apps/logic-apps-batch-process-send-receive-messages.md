---
title: "aaaBatch procesar mensajes como un grupo o una colección - Azure Logic Apps | Documentos de Microsoft"
description: "Envío y recepción de mensajes para el procesamiento por lotes en Logic Apps"
keywords: lote, proceso por lotes
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a>Envío, recepción y procesamiento por lotes de mensajes en Logic Apps

tooprocess mensajes en grupos, puede enviar datos elementos, o los mensajes, tooa *lote*y, a continuación, procesar los elementos como un lote. Este enfoque es útil cuando desea toomake seguro de elementos de datos se agrupan de forma específica y se procesan. 

Puede crear aplicaciones de lógica que reciben elementos como un lote mediante el uso de hello **lote** desencadenador. A continuación, puede crear aplicaciones de lógica que envían elementos tooa lote mediante hello **lote** acción.

Este tema muestra cómo puede compilar una solución de procesamiento por lotes mediante la realización de estas tareas: 

* [Cree una aplicación de lógica que reciba y recopile elementos como lote](#batch-receiver). Esta aplicación de lógica de "receptor de lote" especifica toomeet de criterios de nombre y la versión del lote Hola antes de aplicación lógica de hello receptor libera y procesa los elementos. 

* [Crear una aplicación de lógica que envía el lote de elementos tooa](#batch-sender). Esta aplicación de lógica de "remitente de lote" especifica dónde toosend elementos, que deben ser una aplicación existente de lógica de receptor de lote. Puede especificar una clave única, como un número de cliente, demasiado "partition" o dividir por lotes de destino de hello en subconjuntos basándose en esa clave. De este modo, todos los elementos con esa clave se recopilarán y procesarán juntos. 

## <a name="requirements"></a>Requisitos

toofollow en este ejemplo, necesita estos elementos:

* Una suscripción de Azure. Si no tiene una suscripción, puede [comenzar con una cuenta de Azure gratuita](https://azure.microsoft.com/free/). También puede [registrarse para obtener una suscripción de pago por uso](https://azure.microsoft.com/pricing/purchase-options/).

* Conocimientos básicos sobre [cómo las aplicaciones lógicas toocreate](../logic-apps/logic-apps-create-a-logic-app.md) 

* Una cuenta de correo electrónico con cualquier [proveedor de correo electrónico compatible con Azure Logic Apps](../connectors/apis-list.md)

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a>Creación de aplicaciones lógicas que reciben mensajes como lote

Para poder enviar lotes de mensajes tooa, primero debe crear una aplicación de la lógica de "receptor de lote" con hello **lote** desencadenador. De este modo, puede seleccionar esta aplicación de lógica de receptor, al crear una aplicación de lógica de remitente de Hola. Para un receptor de hello, especifique el nombre del lote de hello, criterios de versión y otras opciones. 

Deben conocer las aplicaciones lógicas de remitente donde los elementos toosend, mientras que las aplicaciones lógicas de receptor no es necesario tooknow nada sobre remitentes de Hola.

1. Hola [portal de Azure](https://portal.azure.com), cree una aplicación de lógica con este nombre: "BatchReceiver" 

2. En el Diseñador de aplicaciones de lógica, agregar hello **lote** desencadenador, que inicia el flujo de trabajo de aplicación lógica. En el cuadro de búsqueda de hello, escriba "por lotes" como filtro. Seleccione este desencadenador: **Batch: Mensajes de Batch**

   ![Agregar desencadenador de lotes](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. Proporcione un nombre para el lote de Hola y especificar los criterios para liberar el lote de hello, por ejemplo:

   * **Nombre de lote**: Hola nombre utilizado tooidentify Hola por lotes, que es "TestBatch" en este ejemplo.
   * **Número de mensajes**: Hola número de mensajes toohold como un lote antes de soltar el procesamiento, que es "5" en este ejemplo.

   ![Proporcionar detalles del desencadenador de lotes](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. Agregar otra acción que envía un correo electrónico cuando se activa el desencadenador de lote de Hola. Cada lote de Hola de tiempo tiene cinco elementos, aplicación de lógica de hello envía un correo electrónico.

   1. En el desencadenador de lote de hello, elija **+ nuevo paso** > **agregar una acción**.

   2. En el cuadro de búsqueda de hello, escriba "email" como filtro.
   En función de su proveedor de correo electrónico, seleccione un conector de correo electrónico.
   
      Por ejemplo, si tiene una cuenta profesional o educativa, seleccione Hola conector de Outlook de Office 365. 
      Si tiene una cuenta de Gmail, seleccione el conector de Gmail de Hola.

   3. Seleccione esta acción para el conector: **{*proveedor de correo electrónico*} - Enviar un correo electrónico**

      Por ejemplo:

      ![Seleccione la acción "Enviar un correo electrónico" para el proveedor de correo electrónico](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. Si anteriormente no creó una conexión para su proveedor de correo electrónico, proporcione sus credenciales de correo electrónico para la autenticación cuando se le soliciten. Obtenga más información sobre la [autenticación de sus credenciales de correo electrónico](../logic-apps/logic-apps-create-a-logic-app.md).

6. Establecer las propiedades de hello para la acción de Hola que acaba de agregar.

   * Hola **a** cuadro, escriba la dirección de correo electrónico del destinatario de Hola. 
   Para realizar pruebas, puede usar su propia dirección de correo electrónico.

   * Hola **asunto** cuadro cuando hello **contenido dinámico** aparece en la lista, seleccione hello **nombre de la partición** campo.

     ![En lista de "Contenido dinámico" Hola, seleccione "Nombre de partición"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     En una sección posterior, puede especificar una clave de partición única que divide Hola por lotes de destino en lógica establece toowhere puede enviar mensajes. 
     Cada conjunto tiene un número único generado por la aplicación de lógica de hello remitente. 
     Esta funcionalidad le permite usar un único lote con varios subconjuntos y definir cada subconjunto con nombre hello proporcionada por usted.

   * Hola **cuerpo** cuadro cuando hello **contenido dinámico** aparece en la lista, seleccione hello **Id. de mensaje** campo.

     ![En "Cuerpo", seleccione "Id. del mensaje"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     Como entrada de hello para la acción de correo electrónico de envío de Hola es una matriz, Diseñador de hello agrega automáticamente un **para cada** trazo alrededor de hello **enviar un correo electrónico** acción. 
     Este bucle realiza la acción interna de hello en cada elemento de lote de Hola. 
     Por lo tanto, con elementos de toofive del conjunto Hola de desencadenador de lote, dispone de cinco mensajes de correo electrónico que se activa cada desencadenador de Hola de tiempo.

7.  Ahora que ha creado una aplicación lógica receptora de lotes, guárdela.

    ![Guardado de la aplicación lógica](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a>Crear aplicaciones de lógica que envían mensajes tooa lote

Ahora cree una o más aplicaciones de lógica que envían elementos toohello lote definido por la aplicación de lógica de receptor de hello. Para el remitente de hello, especificar aplicación lógica de receptor de Hola y nombre de lote, el contenido del mensaje y las opciones de configuración. También puede proporcionar un lote de hello toodivide clave de partición única en elementos de toocollect de subconjuntos con esa clave.

Deben conocer las aplicaciones lógicas de remitente donde los elementos toosend, mientras que las aplicaciones lógicas de receptor no es necesario tooknow nada sobre remitentes de Hola.

1. Cree otra aplicación lógica con este nombre: "BatchSender".

   1. En el cuadro de búsqueda de hello, escriba "recurrence" como filtro. 
   Seleccione este desencadenador: **Programación: Periodicidad**

      ![Agregar desencadenador de Hola "Periodicidad de la programación"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. Establezca frecuencia de Hola y la aplicación de lógica de intervalo toorun Hola remitente cada minuto.

      ![Establecer la frecuencia y el intervalo del desencadenador Periodicidad](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. Agregar un nuevo paso para enviar mensajes tooa lote.

   1. En el desencadenador de periodicidad de hello, elija **+ nuevo paso** > **agregar una acción**.

   2. En el cuadro de búsqueda de hello, escriba "por lotes" como filtro. 

   3. Seleccione esta acción: **enviar mensajes toobatch: elija un flujo de trabajo de las aplicaciones lógicas con el desencadenador de lote**

      ![Seleccione "Enviar mensajes toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. Ahora seleccione la aplicación lógica "BatchReceiver" que creó anteriormente, que ahora aparece como una acción.

      ![Seleccionar aplicación lógica "receptora de lotes"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > lista de Hello también muestra cualquier otra aplicación de lógica que tienen desencadenadores de lote.

3. Establecer las propiedades de lote de Hola.

   * **Nombre de lote**: nombre del lote Hola definido por la aplicación de lógica de receptor de hello, que es "TestBatch" en este ejemplo y se valida en tiempo de ejecución.

     > [!IMPORTANT]
     > Asegúrese de que no cambie el nombre del lote de hello, que debe coincidir con el nombre de lote de hello especificado por la aplicación de lógica de hello receptor.
     > Cambiar nombre de lote de Hola hace que el remitente de hello toofail de aplicación lógica.

   * **Contenido del mensaje**: Hola contenido del mensaje que desea toosend. 
   En este ejemplo, agregue esta expresión que inserciones Hola fecha y hora actuales en el mensaje de bienvenida de contenido que enviar toohello lote:

     1. Cuando Hola **contenido dinámico** aparece en la lista, elija **expresión**. 
     2. Escriba la expresión de hello **utcnow()**y elija **Aceptar**. 

        ![En "Contenido del mensaje", elija "Expresión". Escriba "utcnow()".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. Ahora debe configurar una partición para el lote de Hola. En la acción "BatchReceiver" Hola, elija **Mostrar opciones avanzadas**.

   * **Nombre de partición**: una toouse de clave de partición único opcional para dividir el lote de destino de Hola. En este ejemplo, agregue una expresión que genera un número aleatorio entre uno y cinco.
   
     1. Cuando Hola **contenido dinámico** aparece en la lista, elija **expresión**.
     2. Escriba esta expresión: **rand(1,6)**

        ![Establecer una partición para el lote de destino](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        Esta función **rand** genera un número comprendido entre uno y cinco. 
        Por tanto, va a dividir este lote en cinco particiones numeradas, que esta expresión establece dinámicamente.

   * **Id. de mensaje**: un identificador de mensaje opcional que es un GUID generado cuando está vacío. 
   En este ejemplo, deje este cuadro en blanco.

5. Guarde la aplicación lógica. La aplicación de la lógica de remitente parece ejemplo toothis similar:

   ![Guardar la aplicación lógica remitente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a>Comprobación de las aplicaciones lógicas

tootest el procesamiento por lotes de la solución, deje las aplicaciones lógicas que se ejecuta durante unos minutos. Pronto, empezar a recibir mensajes de correo electrónico en los grupos de cinco, todo ello con hello misma clave de partición.

La aplicación de la lógica de BatchSender ejecuta cada minuto, genera un número aleatorio entre uno y cinco y utiliza este número, generado como clave de partición de hello para el lote de destino de Hola dónde se envían los mensajes. Cada vez que el lote de hello tiene cinco elementos con hello misma clave de partición, la aplicación de la lógica de BatchReceiver se activa y envía el correo electrónico para cada mensaje.

> [!IMPORTANT]
> Cuando haya terminado de pruebas, asegúrese de que deshabilitar el envío de mensajes de Hola BatchSender lógica aplicación toostop y evitar la sobrecarga de la Bandeja de entrada.

## <a name="next-steps"></a>Pasos siguientes

* [Generar definiciones de aplicación lógica mediante el uso de JSON](../logic-apps/logic-apps-author-definitions.md)
* [Cree una aplicación sin servidor en Visual Studio con Azure Logic Apps y Functions](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [Control de excepciones y registro de errores para aplicaciones lógicas](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
