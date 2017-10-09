---
title: aaaCreate B2B solutions - Azure Logic Apps | Documentos de Microsoft
description: "Recibir datos en las aplicaciones lógicas mediante las características de hello B2B Hola paquete de integración empresarial"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a>Recibir datos en las aplicaciones lógicas con características de B2B Hola Hola paquete de integración empresarial

Después de crear una cuenta de la integración con socios comerciales y acuerdos, está listo toocreate un flujo de trabajo de toobusiness (B2B) para la aplicación lógica con hello [paquete de integración empresarial](logic-apps-enterprise-integration-overview.md).

## <a name="prerequisites"></a>Requisitos previos

toouse Hola AS2 y X12 acciones, debe tener una cuenta de integración empresarial. Obtenga información acerca de [toocreate una integración de Enterprise cuenta y cómo](../logic-apps/logic-apps-enterprise-integration-accounts.md).

## <a name="create-a-logic-app-with-b2b-connectors"></a>Creación de una aplicación lógica con conectores B2B

Siga estos aplicación lógica de toocreate un B2B de pasos que usa Hola AS2 y X12 datos tooreceive de acciones de un socio comercial:

1. Crear una aplicación de lógica, a continuación, [vincular su cuenta de integración de aplicaciones tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).

2. Agregar un **solicitar - se recibe la solicitud HTTP de un cuando** aplicación lógica de desencadenador tooyour.

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. Hola tooadd **descodificar AS2** acción, seleccione **agregar una acción**.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. toofilter todos los toohello de acciones que desea, escriba la palabra Hola **as2** en el cuadro de búsqueda de Hola.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. Seleccione hello **AS2 - mensaje AS2 descodificar** acción.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. Agregar hello **cuerpo** que desea toouse como entrada. En este ejemplo, seleccione el cuerpo de saludo de solicitud HTTP de Hola que desencadenadores Hola aplicación lógica. O escriba una expresión que se dirige encabezados Hola Hola **ENCABEZADOS** campo:

    @triggerOutputs()['headers']

7. Agregar Hola necesario **encabezados** para AS2, que puede encontrar en los encabezados de solicitud de hello HTTP. En este ejemplo, seleccione los encabezados de Hola de solicitud HTTP de hello esa aplicación de lógica de hello de desencadenador.

8. Ahora, agregue la acción del mensaje Hola Decode X12. Seleccione **Add an action**(Agregar una acción).

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. toofilter todos los toohello de acciones que desea, escriba la palabra Hola **x12** en el cuadro de búsqueda de Hola.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. Seleccione hello **X12-descodificar X12 mensaje** acción.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. Ahora debe especificar la acción de entrada toothis Hola. Esta entrada es la salida de hello de acción de AS2 anterior Hola.

    contenido real del mensaje de Hola está en un objeto JSON y está codificada en base64, por lo que debe especificar una expresión como entrada de Hola. 
    Escriba Hola siguiente expresión en hello **X12 planos mensaje de archivo tooDECODE** campo de entrada:
    
    @base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])

    Ahora, agregue pasos de datos de hello X12 toodecode reciben de hello socio comercial y los elementos en un objeto JSON de salida. 
    se ha recibido el asociado de hello toonotify que Hola datos, se puede volver a enviar una respuesta que contiene Hola notificación de disposición de mensaje AS2 (MDN) en una acción de respuesta HTTP.

12. Hola tooadd **respuesta** acción, elija **agregar una acción**.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. toofilter todos los toohello de acciones que desea, escriba la palabra Hola **respuesta** en el cuadro de búsqueda de Hola.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. Seleccione hello **respuesta** acción.

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. tooaccess Hola MDN de salida de hello de hello **mensaje Decode X12** acción, respuesta de conjunto hello **cuerpo** campo con esta expresión:

    @base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. Guarde el trabajo.

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

Con esto, ya ha terminado de configurar la aplicación lógica de B2B. En una aplicación real, le podría interesar toostore Hola descodificados X12 datos en un línea de negocio (LOB) aplicación o almacén de datos. tooconnect sus propias aplicaciones LOB y usar estas API en la aplicación lógica, puede agregar más acciones o escribir API personalizadas.

## <a name="features-and-use-cases"></a>Características y casos de uso

* Hola AS2 y X12 descodificar y codificar acciones permiten intercambiar datos entre los socios comerciales mediante el uso de protocolos estándar del sector en las aplicaciones lógicas.
* datos de tooexchange con socios comerciales, puede usar AS2 y X12 con o sin entre sí.
* Hola B2B acciones ayudarle a crear los socios comerciales y acuerdos fácilmente en su cuenta de integración y usarlos en una aplicación de lógica.
* Al ampliar la aplicación lógica con otras acciones, podrá enviar y recibir datos entre otras aplicaciones y servicios como Salesforce.

## <a name="learn-more"></a>Más información
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md)
