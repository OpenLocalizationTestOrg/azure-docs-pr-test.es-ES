---
title: "aaaLearn cómo toouse Hola conector MQ en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conecte tooan local o servidor MQ de Azure de su toobrowse de flujo de trabajo de aplicación lógica, recibir y enviar mensajes tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Conectar tooan servidor MQ de IBM desde las aplicaciones lógicas mediante el conector MQ Hola 

Microsoft Connector for MQ envía y recupera mensajes almacenados en un servidor MQ local o en Azure. Este conector incluye un cliente de Microsoft MQ que se comunica con un servidor IBM MQ remoto a través de una red TCP/IP. Este documento es un conector MQ starter guía toouse Hola. Se recomienda empezar examinando un único mensaje en una cola y, a continuación, intentar Hola otras acciones.    

conector MQ Hola incluye Hola siguientes acciones. No hay desencadenadores.

-   Examinar un único mensaje sin eliminar los mensajes de bienvenida de hello servidor MQ de IBM
-   Examinar un lote de mensajes sin eliminar los mensajes de saludo de hello servidor MQ de IBM
-   Recibir un mensaje único y eliminar mensajes de bienvenida de Hola servidor MQ de IBM
-   Recibir un lote de mensajes y eliminar mensajes de saludo de hello servidor MQ de IBM
-   Enviar un toohello de mensaje único servidor MQ de IBM 

## <a name="prerequisites"></a>Requisitos previos

* Si usa un servidor local de MQ, [instalar la puerta de enlace de datos de hello local](../logic-apps/logic-apps-gateway-install.md) en un servidor dentro de la red. Si Hola MQ Server está públicamente disponible o está disponible dentro de Azure, puerta de enlace de datos de hello no se utilicen o requerido.

    > [!NOTE]
    > servidor de Hola donde hello puerta de enlace de datos local se instala también debe tener .net Framework 4.6 instalado para hello MQ conector toofunction.

* Crear recursos de Azure para puerta de enlace de datos de local de hello - hello [configurar conexión de puerta de enlace de datos de hello](../logic-apps/logic-apps-gateway-connection.md).

* Versiones oficialmente compatibles con IBM WebSphere MQ:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Creación de una aplicación lógica

1. Hola **Azure iniciar panel**, seleccione  **+**  (signo más), **Web y móvil**y, a continuación, **aplicación lógica**. 
2. Escriba hello **nombre**, como MQTestApp, **suscripción**, **grupo de recursos**, y **ubicación** (usar ubicación Hola donde hello conexión de puerta de enlace de datos local está configurado). Seleccione **Pin toodashboard**y seleccione **crear**.  
![Creación de la aplicación lógica](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Incorporación de un desencadenador

> [!NOTE]
> Hola MQ conector no tiene los desencadenadores. Por lo tanto, use otro toostart desencadenador la aplicación lógica, como hello **periodicidad** desencadenador. 

1. Hola **el Diseñador de aplicaciones de la lógica de** se abre, seleccione **periodicidad** en lista de hello del modo habitual.
2. Seleccione **editar** dentro de hello desencadenador de periodicidad. 
3. Conjunto hello **frecuencia** demasiado**día**, conjunto hello y **intervalo** demasiado**7**. 

## <a name="browse-a-single-message"></a>Examen de un único mensaje
1. Seleccione **+ Nuevo paso** y **Agregar una acción**.
2. En el cuadro de búsqueda de hello, escriba `mq`y, a continuación, seleccione **MQ - examinar mensajes**.  
![Examen de un mensaje](media/connectors-create-api-mq/Browse_message.png)

3. Si no hay una conexión de MQ existente, a continuación, crear la conexión de hello:  

    1. Seleccione **conectar a través de puerta de enlace de datos local**y especifique las propiedades de saludo del servidor MQ.  
    Para **Server**, puede especificar nombre del servidor MQ hello, o escriba dirección IP de hello seguido por un número de puerto hello y dos puntos. 
    2. Hola **puerta de enlace** lista desplegable muestra las conexiones de puerta de enlace existentes que se han configurado. Seleccione la puerta de enlace.
    3. Cuando haya terminado, seleccione **Crear**. La conexión tiene un aspecto similar siguiente toohello:   
    ![Propiedades de la conexión](media/connectors-create-api-mq/Connection_Properties.png)

4. En Propiedades de la acción de hello, puede:  

    * Hola de uso **cola** propiedad tooaccess otro nombre de cola a la que se define en la conexión de Hola
    * Hola de uso **MessageId**, **CorrelationId**, **GroupId**y otro toobrowse de propiedades para un mensaje basándose en Propiedades de mensaje de Hola diferentes MQ
    * Establecer **IncludeInfo** demasiado**True** tooinclude información de mensaje adicional en la salida de hello. O bien, establezca esta opción demasiado**False** toonot incluir información de los mensajes adicionales en el resultado de hello.
    * Escriba un **tiempo de espera** toodetermine valor cuánto toowait para un tooarrive de mensaje en una cola vacía. Si no se especifica nada, se recupera el primer mensaje de Hola de cola de hello y no hay ningún tiempo de espera empleado para un mensaje tooappear.  
    ![Propiedades de Browse message](media/connectors-create-api-mq/Browse_message_Props.png)

5. Haga clic en **Guardar** para guardar los cambios y en **Ejecutar** para ejecutar la aplicación lógica:  
![Guardar y ejecutar](media/connectors-create-api-mq/Save_Run.png)

6. Después de unos segundos, se muestran los pasos de Hola de hello ejecutar y puede mirar la salida de hello. Seleccione Hola marca de verificación verde toosee detalles de cada paso. Seleccione **ver resultados sin formato** toosee detalles adicionales en hello los datos de salida.  
![Salida de Browse message](media/connectors-create-api-mq/Browse_message_output.png)  

    Salida sin procesar:  
    ![Salida sin procesar de Browse message](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Cuando Hola **IncludeInfo** opción se establece tootrue, se muestra hello después de salida:  
![IncludeInfo de Browse message](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Examen de varios mensajes
Hola **examinar mensajes** acción incluye una **BatchSize** opción tooindicate cuántos mensajes se deben devolver desde la cola de Hola.  Si **BatchSize** se deja en blanco, se devuelven todos los mensajes. Hola devuelve el resultado es una matriz de mensajes.

1. Al agregar hello **examinar mensajes** acción, conexión primera Hola que está configurado de manera predeterminada. Seleccione **cambiar conexión** toocreate una conexión nueva, o seleccione otra conexión.

2. salida de Hello de examinar mensajes de muestra:  
![Salida de Browse message](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Recepción de un único mensaje
Hola **recibir mensaje** acción ha Hola mismo entradas y salidas como hello **examinar mensajes** acción. Cuando se usa **recibir mensaje**, mensaje de bienvenida se elimina de la cola de Hola.

## <a name="receive-multiple-messages"></a>Recepción de varios mensajes
Hola **recibir mensajes** acción ha Hola mismo entradas y salidas como hello **examinar mensajes** acción. Cuando se usa **recibir mensajes**, se eliminan mensajes de saludo de cola de Hola.

Si no hay ningún mensaje en cola Hola al realizar un examen o una operación de recepción, se produce un error en la paso Hola con hello después de salida:  
![Error de ausencia de mensajes en MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Envío de un mensaje
1. Al agregar hello **enviar mensaje** acción, conexión primera Hola que está configurado de manera predeterminada. Seleccione **cambiar conexión** toocreate una conexión nueva, o seleccione otra conexión. Hola válido **tipos de mensaje** son **datagrama**, **respuesta**, o **solicitar**.  
![Propiedades de Send message](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Hello salida del mensaje de envío Hola siguiente aspecto:  
![Salida de Send message](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/mq/).

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).
