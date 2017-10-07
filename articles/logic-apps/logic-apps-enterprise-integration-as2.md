---
title: "mensajes de aaaAS2 para la integración de enterprise B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Intercambio de mensajes AS2 para la integración empresarial B2B con Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Intercambio de mensajes AS2 para la integración empresarial con las aplicaciones lógicas

Para poder intercambiar mensajes AS2 para Azure Logic Apps, debe crear un contrato AS2 y almacenarlo en la cuenta de integración. Estos son los pasos de Hola para saber cómo toocreate un AS2 acuerdo.

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una [cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md) que ya esté definida y asociada a su suscripción de Azure
* Al menos dos [socios](logic-apps-enterprise-integration-partners.md) que ya definidos en su cuenta de integración y configurado con el calificador de hello AS2 en **las identidades de negocio**

> [!NOTE]
> Cuando se crea un acuerdo, contenido de hello en el archivo del contrato de hello debe coincidir con tipo de contrato de Hola.    

Cuando haya [creado una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md) y [agregado los asociados](logic-apps-enterprise-integration-partners.md), siga estos pasos para generar un contrato AS2.

## <a name="create-an-as2-agreement"></a>Creación de un contrato AS2

1.  Inicie sesión en toohello [portal de Azure](http://portal.azure.com "portal de Azure").  

2.  En el menú izquierdo de hello, seleccione **más servicios**. En el cuadro de búsqueda de hello, escriba **integración** como filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.

    > [!TIP]
    > Si no ve **más servicios**, es posible que tenga menú de hello tooexpand en primer lugar. Hola parte superior de hello contraído menú, seleccione **menú de mostrar**.

    ![Más servicios, filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. Hola **cuentas de integración** hoja que se abre, cuenta de integración de hello seleccione donde desea que el acuerdo de hello toocreate.
Si no ve ninguna, [créela](../logic-apps/logic-apps-enterprise-integration-accounts.md "Información completa sobre las cuentas de integración").  

    ![Seleccionar cuenta de integración de Hola donde toocreate Hola acuerdo](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Elija hello **contratos** icono. Si no tiene un icono de acuerdos, agregar icono hello en primer lugar.

    ![Elección del icono "Acuerdos"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. En la hoja de contratos de Hola que se abre, elija **agregar**.

    ![Elección de "Agregar"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. En **Agregar**, escriba un valor en **Nombre** para el contrato. Para el **Tipo de contrato**, seleccione **AS2**. Seleccione hello **socio del Host**, **identidad del Host**, **socio invitado**, y **identidad Invitado** para el acuerdo.

    ![Especificación de los detalles del contrato](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Propiedad | Descripción |
    | --- | --- |
    | Nombre |Nombre del contrato de Hola |
    | Tipo de contrato | Debe ser AS2 |
    | Host Partner (Partner anfitrión) |Un contrato tiene asociado un partner anfitrión e invitado. el socio del host de Hello representa la organización de Hola que configura el acuerdo de Hola. |
    | Host Identity (Identidad anfitriona) |Un identificador para el socio del host de Hola |
    | Guest Partner (Partner invitado) |Un contrato tiene asociado un partner anfitrión e invitado. Socio invitado de Hello representa la organización de hello encargado de negocio con el socio del host de Hola. |
    | Guest Identity |Un identificador para el socio invitado de Hola |
    | Receive Settings (Configuración de recepción) |Estas propiedades aplican tooall los mensajes recibidos por un acuerdo. |
    | Send Settings (Configuración de envío) |Estas propiedades aplican tooall los mensajes enviados por un acuerdo. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuración de la forma en que su contrato controla los mensajes recibidos

Ahora que ha establecido las propiedades del acuerdo de hello, puede configurar cómo este contrato identifica y controla los mensajes entrantes recibidos del socio a través de este contrato.

1.  En **Agregar**, seleccione **Configuración de recepción**.
Configurar estas propiedades basándose en el acuerdo de socio de Hola que intercambia mensajes con usted. Para obtener descripciones de propiedad, vea la tabla de hello en esta sección.

    ![Selección de "Configuración de recepción"](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Si lo desea, puede invalidar propiedades de Hola de mensajes entrantes seleccionando **invalidar propiedades de mensajes**.

3. toorequire todos los toobe mensajes entrantes firmados, seleccione **debe firmarse el mensaje**. De hello **certificado** lista, seleccione una existente [certificado público del socio invitado](../logic-apps/logic-apps-enterprise-integration-certificates.md) para validar la firma de hello en mensajes de saludo. O bien, crear certificado de hello, si no tiene uno.

4.  toorequire todos los toobe mensajes entrantes cifrada, seleccione **debe cifrarse el mensaje**. De hello **certificado** lista, seleccione una existente [certificado privado de host asociado](../logic-apps/logic-apps-enterprise-integration-certificates.md) para descifrar los mensajes entrantes. O bien, crear certificado de hello, si no tiene uno.

5. Seleccione toorequire mensajes toobe comprimido, **debe comprimirse el mensaje**.

6. Seleccione una notificación de disposición de mensaje sincrónico (MDN) para los mensajes recibidos, toosend **enviar MDN**.

7. toosend firman MDN para los mensajes recibidos, seleccionados **enviar MDN firmado**.

8. toosend MDN asíncronos para los mensajes recibidos, seleccione **enviar MDN asincrónico**.

9. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora, el contrato es listo toohandle entrante los mensajes que cumplen tooyour la configuración seleccionada.

| Propiedad | Descripción |
| --- | --- |
| Override message properties |Indica que se pueden invalidar las propiedades de los mensajes recibidos. |
| Message should be signed |Requiere toobe mensajes firmado digitalmente. Configurar certificado público socio de hello invitado para comprobar la firma.  |
| Message should be encrypted |Requiere toobe mensajes cifrado. Los mensajes sin cifrado se rechazan. Configurar certificado privado socio de hello host para el descifrado de mensajes de saludo.  |
| Message should be compressed |Requiere toobe mensajes comprimido. Los mensajes sin comprimir se rechazan. |
| MDN Text (Texto de MDN) |Hola predeterminado message disposition notification (MDN) toobe envía toohello remitente del mensaje. |
| Send MDN (Enviar MDN) |Requiere toobe MDN enviado. |
| Send signed MDN (Enviar MDN firmada) |Requiere toobe MDN firmado. |
| MIC Algorithm (Algoritmo de MIC) |Seleccione Hola algoritmo toouse para firmar los mensajes. |
| Send asynchronous MDN (Enviar MDN asincrónica) | Requiere toobe de mensajes que se envían de forma asincrónica. |
| URL | Especificar dirección URL de Hola donde toosend Hola MDN. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuración de la forma en que su contrato envía mensajes

Puede configurar cómo este contrato identifica y controla los mensajes salientes que envían a tooyour asociados a través de este contrato.

1.  En **Agregar**, seleccione **Send Settings** (Configuración de envío).
Configurar estas propiedades basándose en el acuerdo de socio de Hola que intercambia mensajes con usted. Para obtener descripciones de propiedad, vea la tabla de hello en esta sección.

    ![Establecer las propiedades de "Configuración de envío" hello](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend mensajes firmados tooyour socio comercial, seleccione **habilitar la firma del mensaje**. Para firmar los mensajes de Hola, Hola **algoritmo MIC** lista, seleccione hello *certificado privado de host asociado algoritmo MIC*. Y en hello **certificado** lista, seleccione una existente [certificado privado de host socio](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend mensajes cifrados toohello socio comercial, seleccione **Habilitar cifrado de mensajes**. Para cifrar los mensajes de Hola, Hola **algoritmo de cifrado** lista, seleccione hello *algoritmo de certificado público de socio comercial invitado*.
Y en hello **certificado** lista, seleccione una existente [certificado público del socio invitado](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. mensaje de saludo toocompress, seleccione **Habilitar compresión de mensajes**.

5. encabezado de toounfold Hola HTTP content-type en una sola línea, seleccione **expandir encabezados HTTP**.

6. tooreceive MDN sincrónicos para hello envían mensajes, seleccionados **solicitar MDN**.

7. tooreceive firman MDN para los mensajes de Hola enviado, seleccionados **solicitar MDN firmado**.

8. tooreceive MDN asíncronos para hello envían mensajes, seleccionados **solicitar MDN asíncrono**. Si selecciona esta opción, escriba la dirección de URL de Hola para donde toosend Hola MDN.

9. toorequire sin repudio de recepción, seleccione **habilitar NRR**.  

10. toospecify toouse de formato de algoritmo MIC de Hola o iniciar sesión en hello saliente encabezados del mensaje de Hola AS2 o MDN, seleccione **formato de algoritmo SHA2**.  

11. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora el contrato es listo toohandle los mensajes que se ajustan tooyour seleccionado configuración salientes.

| Propiedad | Descripción |
| --- | --- |
| Enable message signing (Habilitar firma de mensajes) |Requiere que todos los mensajes que se envían desde Hola acuerdo toobe firmado. |
| MIC Algorithm (Algoritmo de MIC) |Hola toouse algoritmo para firmar los mensajes. Configura el certificado privado de socio de host de hello algoritmo MIC para la firma de mensajes de saludo. |
| Certificate |Seleccione hello toouse de certificado para firmar los mensajes. Configura Hola host asociado privada certificado para firmar mensajes de saludo. |
| Enable message encryption (Habilitar el cifrado de mensajes) |Exige que se cifren todos los mensajes enviados desde el contrato. Configura el algoritmo de hello invitado asociado certificado público para el cifrado de mensajes de saludo. |
| Algoritmo de cifrado |Hola toouse de algoritmo de cifrado para cifrar mensajes. Configura el certificado público socio de hello invitado para cifrar los mensajes de Hola. |
| Certificate |mensajes de saludo certificado toouse tooencrypt. Configura el certificado privado socio de hello invitado para cifrar los mensajes de Hola. |
| Habilitar la compresión de mensajes |Exige que se compriman todos los mensajes enviados desde el contrato. |
| Unfold HTTP headers (Expandir encabezados HTTP) |Coloca el encabezado de tipo de contenido HTTP de hello en una sola línea. |
| Request MDN (Solicitar MDN) |Exige una MDN para todos los mensajes enviados desde el contrato. |
| Request signed MDN (Solicitar MDN firmada) |Requiere que todos los MDN que se envían a otro contrato toothis toobe firmado. |
| Request asynchronous MDN (Solicitar MDN asíncrona) |Es necesario el acuerdo de toothis de toobe enviar MDN asincrónico. |
| URL |Especificar dirección URL de Hola donde toosend Hola MDN. |
| Enable NRR (Habilitar NRR) |Requiere repudio de recepción (NRR), un atributo de comunicación que proporciona evidencia de que los datos Hola se recibió como dirigido. |
| Formato del algoritmo SHA2 |Seleccionar algoritmo formato toouse en Hola MIC o iniciar sesión en hello encabezados del mensaje de bienvenida de AS2 o MDN salientes |

## <a name="find-your-created-agreement"></a>Búsqueda del contrato creado

1.  Cuando termine de establecer las propiedades de acuerdo, en hello **agregar** hoja, elija **Aceptar** toofinish crear acuerdo y hoja de cuenta de la integración de tooyour devuelto.

    Ahora el contrato recién agregado aparece en la lista **Acuerdos**.

2.  También puede ver los contratos en la información general de la cuenta de integración. En la hoja de la cuenta de integración, elija **Introducción**, a continuación, seleccione hello **contratos** icono. 

    ![Elija "Acuerdos" icono tooview todos los contratos](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/as2/). 

## <a name="next-steps"></a>Pasos siguientes
* [Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  
