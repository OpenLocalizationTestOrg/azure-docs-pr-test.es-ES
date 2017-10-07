---
title: mensajes EDIFACT aaaDecode - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar confirmaciones con descodificador de mensaje de saludo EDIFACT Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Descodificar mensajes EDIFACT para las aplicaciones lógicas de Azure con hello paquete de integración empresarial

Con el conector de mensaje de Hola descodificar EDIFACT, puede validar EDI y propiedades específicas del partner, dividir intercambios en conjuntos de transacciones o conservar todos intercambios y generar confirmaciones de transacciones procesadas. toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector de mensaje integración cuenta toouse Hola descodificar EDIFACT. 
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato EDIFACT](logic-apps-enterprise-integration-edifact.md) ya definido en la cuenta de integración.

## <a name="decode-edifact-messages"></a>Descodificación de mensajes EDIFACT

1. [Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola EDIFACT descodificar no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3. En el cuadro de búsqueda de hello, escriba "EDIFACT" como filtro. Seleccione **Descodificar mensaje EDIFACT**.
   
    ![buscar EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect.
   
    ![crear cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

4. Cuando haya terminado toofinish crear la conexión, elija **crear**. Los detalles de la conexión deben tener un aspecto similar ejemplo toothis:

    ![detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. Una vez creada la conexión, como se muestra en este ejemplo, seleccione toodecode de mensaje de archivo sin formato de EDIFACT Hola.

    ![creación de la conexión de la cuenta de integración](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    Por ejemplo:

    ![Selección del mensaje de archivo plano EDIFACT para descodificar](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a>Detalles de descodificador de EDIFACT

Hola descodificar EDIFACT conector lleva a cabo estas tareas: 

* Valida el sobre de hello en el acuerdo de socio comercial.
* Hola acuerdo se resuelve haciendo coincidir el calificador de remitente de hello & identificador y calificador de receptor & identificador.
* Divide un intercambio en varias transacciones al intercambio de hello tiene más de una transacción en función del contrato de hello opciones de configuración de recepción.
* Desensambla el intercambio de Hola.
* Valida las propiedades de EDI y específicas del asociado, lo que incluye:
  * Validación de la estructura de envoltura de intercambio de Hola
  * Validación de esquemas de sobres de hello en el esquema de control hello
  * Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola
  * Validación de EDI realizada en los elementos de datos del conjunto de transacciones
* Comprueba que números de control de conjunto de intercambio, grupo y transacción hello no sean duplicados (si está configurado) 
  * Comprueba el número de control de intercambio de hello en los intercambios recibidos anteriormente. 
  * Comprueba el número de control de grupo de hello con los otros números de control de grupo en el intercambio de Hola. 
  * Comprueba el número de control del conjunto de transacciones de hello en otros números de control de conjunto de transacciones de ese grupo.
* Hola Intercambio en conjuntos de transacciones se divide o conserva todo el intercambio hello:
  * Divide el intercambio como conjuntos de transacciones (suspende conjuntos de transacciones en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones. 
  acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.
  * Divide el intercambio como conjuntos de transacciones (suspende el intercambio en caso de error): divide el intercambio en conjuntos de transacciones y analiza cada conjunto de transacciones. 
  Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.
  * Conservar intercambio: suspender conjuntos de transacciones en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes. 
  acción de descodificación de Hello X12 envía solo esos conjuntos de transacciones que no superan la validación demasiado`badMessages`y genera Hola transacciones restantes se establece demasiado`goodMessages`.
  * Conservar intercambio: suspender intercambio en caso de error: conservar intercambio de Hola y proceso Hola todo el intercambio por lotes. 
  Si una o más conjuntos de transacciones en la validación de un error de intercambio de hello, acción de descodificación de hello X12 genera conjuntos de todas las transacciones de hello en dicho intercambio demasiado`badMessages`.
* Genera una confirmación técnica (control) o funcional (si esta opción está configurada).
  * Una confirmación técnica o hello CONTRL ACK informa de los resultados de Hola de una comprobación sintáctica del intercambio de hello completo recibido.
  * Una confirmación funcional confirma la aceptación o el rechazo de un intercambio recibido o un grupo

## <a name="view-swagger-file"></a>Ver el archivo de Swagger
detalles de Swagger de tooview hello para el conector de saludo EDIFACT, vea [EDIFACT](/connectors/edifact/).

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

