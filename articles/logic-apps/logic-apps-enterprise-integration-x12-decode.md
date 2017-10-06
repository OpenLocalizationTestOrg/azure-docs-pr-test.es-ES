---
title: mensajes de aaaDecode X12 - Azure Logic Apps | Documentos de Microsoft
description: "Validar EDI y generar confirmaciones con descodificador de mensaje de Hola X12 Hola paquete de integración empresarial para las aplicaciones lógicas de Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a>Descodificar X12 mensajes para las aplicaciones lógicas de Azure con hello paquete de integración empresarial

Con el conector de mensaje de Hola Decode X12, puede validar sobres Hola contra un acuerdo entre socios comerciales, validar EDI y propiedades específicas del partner, dividir intercambios en conjuntos de transacciones o conservar todos intercambios y generar confirmaciones de transacciones procesadas. toouse este conector, debe agregar Hola conector tooan existente desencadenador en la aplicación lógica.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una cuenta de Azure; puede crear una [gratuita](https://azure.microsoft.com/free)
* Una [cuenta de integración](logic-apps-enterprise-integration-create-integration-account.md) que ya esté definida y asociada a su suscripción de Azure. Debe tener un conector integración cuenta toouse Hola Decode X12 mensaje.
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.
* Un [contrato X12](logic-apps-enterprise-integration-x12.md) ya definido en su cuenta de integración

## <a name="decode-x12-messages"></a>Descodificación de mensajes X12

1. [Creación de una aplicación lógica](logic-apps-create-a-logic-app.md).

2. Conector de mensaje de Hola Decode X12 no tiene desencadenadores, por lo que debe agregar un desencadenador para iniciar la aplicación lógica, como un desencadenador de la solicitud. Hola diseñador la lógica de aplicación, agregar un desencadenador y, a continuación, agregar una aplicación de lógica de tooyour de acción.

3.  En el cuadro de búsqueda de hello, escriba "x12" para el filtro. Seleccione **X12 - Decode X12 message** (X12 – Descodificación de mensajes X12).
   
    ![Búsqueda de "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. Si previamente no creó ninguna conexión de cuenta de integración de tooyour, se te pedirá toocreate ahora esa conexión. Nombre de la conexión y seleccione cuenta de integración de Hola que desea tooconnect. 

    ![Proporcionar los detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    Aquellas propiedades con un asterisco son obligatorias.

    | Propiedad | Detalles |
    | --- | --- |
    | Nombre de la conexión * |Escriba cualquier nombre para la conexión. |
    | Cuenta de integración* |Escriba un nombre para la cuenta de integración. Asegúrese de que la aplicación de cuenta y la lógica de integración están en hello misma ubicación de Azure. |

5.  Cuando haya terminado, los detalles de la conexión deben tener un aspecto similar ejemplo toothis. toofinish crear la conexión, elija **crear**.
   
    ![detalles de conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. Una vez creada la conexión, como se muestra en este ejemplo, seleccione toodecode de mensaje de archivo sin formato de hello X12.

    ![creación de la conexión de la cuenta de integración](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    Por ejemplo:

    ![Seleccione el mensaje de archivo plano X12 para descodificar](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a>Detalles de X12 Decode

Conector de descodificación de Hello X12 lleva a cabo estas tareas:

* Valida sobre hello en el acuerdo de socio comercial
* Valida propiedades EDI y específicas del asociado.
  * Validación estructural de EDI y validación de esquema extendido
  * Validación de la estructura de Hola de sobres de intercambio de Hola.
  * Validación de esquemas de sobres de hello en el esquema de control de Hola.
  * Validación de esquema de los elementos de datos de conjuntos de transacciones de hello en el esquema de mensaje de Hola.
  * Validación de EDI realizada en los elementos de datos del conjunto de transacciones 
* Comprueba que los números de control de conjunto de intercambio, grupo y transacción hello no sean duplicados
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
* Genera una confirmación técnica o funcional (si esta opción está configurada).
  * Se genera una confirmación técnica como resultado de la validación del encabezado. Hola confirmación técnica informa del estado Hola Hola del procesamiento de un encabezado de intercambio y finalizador mediante receptor de direcciones de Hola.
  * Se genera una confirmación funcional como resultado de la validación del cuerpo. confirmación funcional Hello notifica cada error al procesar Hola recibió el documento

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/x12/). 

## <a name="next-steps"></a>Pasos siguientes
[Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial") 

