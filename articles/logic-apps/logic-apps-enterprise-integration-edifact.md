---
title: "mensajes de aaaEDIFACT para la integración de enterprise B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Intercambio de mensajes EDIFACT en formato EDI para la integración empresarial B2B con Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>Intercambio de mensajes EDIFACT para la integración empresarial con las aplicaciones lógicas

Para poder intercambiar mensajes EDIFACT para Azure Logic Apps, debe crear un contrato EDIFACT y almacenarlo en la cuenta de integración. Estos son los pasos de Hola para saber cómo toocreate un acuerdo EDIFACT.

> [!NOTE]
> Esta página incluye características EDIFACT de Hola para las aplicaciones lógicas de Azure. Para obtener más información, consulte [X12](logic-apps-enterprise-integration-x12.md).

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una [cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md) que ya esté definida y asociada a su suscripción de Azure  
* Al menos dos [asociados](logic-apps-enterprise-integration-partners.md) que ya estén definidos en su cuenta de integración.

> [!NOTE]
> Cuando se crean un acuerdo, el contenido de hello en los mensajes de Hola que recibe o envía tooand del socio de hello debe coincidir con el tipo de contrato de Hola.

Cuando haya [creado una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md) y [agregado los asociados](logic-apps-enterprise-integration-partners.md), siga estos pasos para generar un contrato EDIFACT.

## <a name="create-an-edifact-agreement"></a>Creación de un acuerdo EDIFACT 

1.  Inicie sesión en toohello [portal de Azure](http://portal.azure.com "portal de Azure"). En el menú izquierdo de hello, seleccione **más servicios**.

    > [!TIP]
    > Si no ve **más servicios**, es posible que tenga menú de hello tooexpand en primer lugar. Hola parte superior de hello contraído menú, seleccione **menú de mostrar**.

    ![En el menú izquierdo, seleccione "Más servicios"](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. En el cuadro de búsqueda de hello, escriba "integración" para el filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. Hola **cuentas de integración** hoja que se abre, cuenta de integración de hello seleccione donde desea que el acuerdo de hello toocreate.
Si no ve ninguna, [créela](../logic-apps/logic-apps-enterprise-integration-accounts.md "Información completa sobre las cuentas de integración").  

    ![Seleccionar cuenta de integración donde toocreate Hola acuerdo](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Elija hello **contratos** icono. Si no tiene un icono de acuerdos, agregar icono hello en primer lugar.   

    ![Elección del icono "Acuerdos"](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. En la hoja de contratos de Hola que se abre, elija **agregar**.

    ![Elección de "Agregar"](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. En **Agregar**, escriba un valor en **Nombre** para el contrato. Para el **Tipo de contrato**, seleccione **EDIFACT**. Seleccione hello **socio del Host**, **identidad del Host**, **socio invitado**, y **identidad Invitado** para el acuerdo.

    ![Especificación de los detalles del contrato](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | Propiedad | Descripción |
    | --- | --- |
    | Nombre |Nombre del contrato de Hola |
    | Tipo de contrato | Debe ser EDIFACT |
    | Host Partner (Partner anfitrión) |Un contrato tiene asociado un partner anfitrión e invitado. el socio del host de Hello representa la organización de Hola que configura el acuerdo de Hola. |
    | Host Identity (Identidad anfitriona) |Un identificador para el socio del host de Hola |
    | Guest Partner (Partner invitado) |Un contrato tiene asociado un partner anfitrión e invitado. Socio invitado de Hello representa la organización de hello encargado de negocio con el socio del host de Hola. |
    | Guest Identity |Un identificador para el socio invitado de Hola |
    | Receive Settings (Configuración de recepción) |Estas propiedades aplican tooall los mensajes recibidos por un acuerdo. |
    | Send Settings (Configuración de envío) |Estas propiedades aplican tooall los mensajes enviados por un acuerdo. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuración de la forma en que su contrato controla los mensajes recibidos

Ahora que ha establecido las propiedades del acuerdo de hello, puede configurar cómo este contrato identifica y controla los mensajes entrantes recibidos del socio a través de este contrato.

1.  En **Agregar**, seleccione **Configuración de recepción**.
Configurar estas propiedades basándose en el acuerdo de socio de Hola que intercambia mensajes con usted. Para obtener descripciones de propiedad, vea las tablas de hello en esta sección.

    **Configuración de recepción** se divide en las siguientes secciones: Identificadores, Confirmación, Esquemas, Números de control, Validaciones y Configuración interna.

    ![Selección de "Configuración de recepción"](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora, el contrato es listo toohandle entrante los mensajes que cumplen tooyour la configuración seleccionada.

### <a name="identifiers"></a>Identifiers (Identificadores)

| Propiedad | Descripción |
| --- | --- |
| UNB6.1 (contraseña de referencia del destinatario) |Escriba un valor alfanumérico de entre 1 y 14 caracteres. |
| UNB6.2 (calificador de referencia del destinatario) |Escriba un valor alfanumérico con un carácter como mínimo y dos como máximo. |

### <a name="acknowledgments"></a>Agradecimientos

| Propiedad | Descripción |
| --- | --- |
| Receipt of Message (CONTRL) (Recepción del mensaje [CONTRL]) |Seleccione este tooreturn casilla un remitente de intercambio de toohello de confirmación (CONTRL) técnico. confirmación de Hola se envía el remitente de intercambio de toohello basándose en hello configuración de envío para el acuerdo de Hola. |
| Acknowledgement (CONTRL) (Confirmación [CONTRL]) |Seleccione este tooreturn casilla (CONTRL) confirmación toohello intercambio remitente Hola confirmación funcional se envía remitente de intercambio de toohello basándose en hello configuración de envío para el acuerdo de Hola. |

### <a name="schemas"></a>Esquemas

| Propiedad | Descripción |
| --- | --- |
| UNH2.1 (TYPE) (UNH2.1 [TIPO]) |Seleccione un tipo de conjunto de transacciones. |
| UNH2.2 (VERSION) (UNH2.2 [VERSIÓN]) |Escriba el número de versión de mensaje de Hola. (Como mínimo un carácter; tres caracteres como máximo). |
| UNH2.3 (RELEASE) (UNH2.3 [LANZAMIENTO]) |Escriba el número de versión de mensaje de Hola. (Como mínimo un carácter; tres caracteres como máximo). |
| UNH2.5 (ASSOCIATED ASSIGNED CODE) (UNH2.5 [CÓDIGO ASIGNADO ASOCIADO]) |Escriba el código de hello asignado. (Seis caracteres como máximo. Debe ser alfanumérico). |
| UNG2.1 (APP SENDER ID) (UNG2.1 [ID. DE REMITENTE DE APLICACIÓN]) |Escriba un valor alfanumérico con un carácter como mínimo y 35 como máximo. |
| UNG2.2 (APP SENDER CODE QUALIFIER) (UNG2.2 [CALIFICADOR DE CÓDIGO DE REMITENTE DE APLICACIÓN]) |Escriba un valor alfanumérico con un máximo de cuatro caracteres. |
| Esquema |Seleccione Hola cargado previamente esquema desee toouse desde su cuenta de integración asociado. |

### <a name="control-numbers"></a>Control Numbers (Números de control)
| Propiedad | Descripción |
| --- | --- |
| Disallow Interchange Control Number duplicates (No permitir duplicados del número de control de intercambio) |tooblock los intercambios duplicados, se selecciona esta propiedad. Si se selecciona, Hola EDIFACT descodificar acción comprueba que el número de control de intercambio de hello (UNB5) para el intercambio de hello recibido no coincide con un número de control de intercambio de los procesados previamente. Si se detecta una coincidencia, no se procesa el intercambio de Hola. |
| Check for duplicate UNB5 every (days) (Comprobar UNB5 duplicados cada [días]) |Si ha elegido toodisallow números de control de intercambio duplicado, puede especificar Hola número de días al comprobar tooperform Hola proporcionando el valor adecuado de Hola para esta configuración. |
| Disallow Group control number duplicates (No permitir duplicados del número de control de grupo) |tooblock intercambios con números de control de grupo duplicados (UNG5), seleccione esta propiedad. |
| Disallow Transaction set control number duplicates (No permitir duplicados del número de control del conjunto de transacciones) |tooblock intercambios con una transacción duplicada conjunto de números de control (UNH1), seleccione esta propiedad. |
| EDIFACT Acknowledgement Control Number (Número de control de confirmación EDIFACT) |conjunto de transacciones de Hola de toodesignate a los números de referencia para su uso en una confirmación, escriba un valor para el prefijo de hello, un intervalo de números de referencia y un sufijo. |

### <a name="validations"></a>Validations (Validaciones)

Cuando haya completado cada fila de validación, se agrega otra automáticamente. Si no se especifica ninguna regla, validación usa fila de Hola "Default".

| Propiedad | Descripción |
| --- | --- |
| Message Type (Tipo de mensaje) |Seleccione el tipo de mensaje de Hola EDI. |
| EDI Validation (Validación de EDI) |Realizar la validación EDI en tipos de datos definidos por el del esquema de hello EDI propiedades, las restricciones de longitud, elementos de datos vacíos y separadores finales. |
| Extended Validation (Validación extendida) |Si el tipo de datos de hello no es EDI, validación en requisito de elemento de datos de Hola y permite la repetición, enumeraciones y datos de validación de longitud de elemento (mín./máx.). |
| Allow Leading/Trailing Zeroes (Permitir ceros a la izquierda/finales) |Conserve los caracteres de espacio y cero iniciales o finales adicionales. No los quite. |
| Recortar ceros iniciales y finales |Quite los caracteres de espacio y cero iniciales o finales. |
| Trailing Separator Policy (Directiva de separador final) |Genere separadores finales. <p>Seleccione **no permite** tooprohibit los delimitadores finales y separadores en hello recibieron el intercambio. Si el intercambio de hello tiene delimitadores y separadores finales, intercambio de Hola se declara no válido. <p>Seleccione **opcional** tooaccept intercambios con o sin delimitadores y separadores finales. <p>Seleccione **obligatorio** al intercambio de hello recibido debe tener delimitadores y separadores finales. |

### <a name="internal-settings"></a>Internal Settings (Configuración interna)

| Propiedad | Descripción |
| --- | --- |
| Create empty XML tags if trailing separators are allowed (Crear etiquetas XML vacías si se permiten separadores finales) |Seleccione este remitente de intercambio de casilla de verificación toohave Hola incluyen vacía etiquetas XML para los separadores finales. |
| Dividir intercambio como conjuntos de transacciones: suspender conjuntos de transacciones en caso de error|Analiza cada conjunto de transacciones en un intercambio en un documento XML independiente aplicando el conjunto de transacciones de toohello Hola sobre adecuado. Suspender Hola de solo los conjuntos de transacciones que no superan la validación. |
| Dividir intercambio como conjuntos de transacciones: suspender intercambio en caso de error|Analiza cada conjunto de transacciones en un intercambio en un documento XML independiente aplicando el sobre adecuado Hola. Suspender el intercambio completo de hello cuando uno o varios conjuntos de transacciones de intercambio de hello no superan la validación. | 
| Conservar intercambio: suspender conjuntos de transacciones en caso de error |Intercambio de hello permanecen intactos, crea un documento XML para todo el intercambio por lotes Hola. Suspender Hola de solo los conjuntos de transacciones que no superan la validación, mientras continúa tooprocess establece todas las demás transacciones. |
| Conservar intercambio: suspender intercambio en caso de error |Intercambio de hello permanecen intactos, crea un documento XML para todo el intercambio por lotes Hola. Suspender el intercambio completo de hello cuando uno o varios conjuntos de transacciones de intercambio de hello no superan la validación. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuración de la forma en que su contrato envía mensajes

Puede configurar cómo este contrato identifica y controla los mensajes salientes que envían a tooyour asociados a través de este contrato.

1.  En **Agregar**, seleccione **Send Settings** (Configuración de envío).
Configure estas propiedades en función del contrato con el asociado con el que intercambia mensajes. Para obtener descripciones de propiedad, vea las tablas de hello en esta sección.

    **Send Settings** (Configuración de envío) se organiza en las siguientes secciones: Identificadores, Confirmación, Esquemas, Sobres, Juegos de caracteres y separadores, Números de control y Validaciones.

    !["Send Settings" (Configuración de envío)](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora el contrato es listo toohandle los mensajes que se ajustan tooyour seleccionado configuración salientes.

### <a name="identifiers"></a>Identifiers (Identificadores)

| Propiedad | Descripción |
| --- | --- |
| UNB1.2 (Syntax version) (UNB1.2 [versión de sintaxis]) |Seleccione un valor entre **1** y **4**. |
| UNB2.3 (Sender Reverse Routing Address) (UNB2.3 [dirección de enrutamiento inverso del remitente]) |Escriba un valor alfanumérico con un carácter como mínimo y 14 como máximo. |
| UNB3.3 (Recipient Reverse Routing Address) (UNB3.3 [dirección de enrutamiento inverso del destinatario]) |Escriba un valor alfanumérico con un carácter como mínimo y 14 como máximo. |
| UNB6.1 (contraseña de referencia del destinatario) |Escriba un valor alfanumérico con un carácter como mínimo y 14 caracteres como máximo. |
| UNB6.2 (calificador de referencia del destinatario) |Escriba un valor alfanumérico con un carácter como mínimo y dos como máximo. |
| UNB7 (Application Reference ID) (UNB7 [Identificador de referencia de solicitud]) |Escriba un valor alfanumérico con un carácter como mínimo y 14 como máximo. |

### <a name="acknowledgment"></a>Acknowledgement (Confirmación)
| Propiedad | Descripción |
| --- | --- |
| Receipt of Message (CONTRL) (Recepción del mensaje [CONTRL]) |Seleccione esta casilla si el socio comercial de hello hospedado espera tooreceive una confirmación técnica (CONTRL). Esta configuración especifica a dicho socio hospedado de hello, que envía mensajes de bienvenida, solicita una confirmación del socio invitado de Hola. |
| Acknowledgement (CONTRL) (Confirmación [CONTRL]) |Seleccione esta casilla si el socio comercial de hello hospedado espera tooreceive una confirmación funcional (CONTRL). Esta configuración especifica a dicho socio hospedado de hello, que envía mensajes de bienvenida, solicita una confirmación del socio invitado de Hola. |
| Generate SG1/SG4 loop for accepted transaction sets (Generar bucle SG1/SG4 en los conjuntos de transacciones aceptadas) |Si ha elegido toorequest una confirmación funcional, seleccione esta casilla de verificación tooforce la generación de bucles SG1/SG4 en confirmaciones CONTRL funcionales para conjuntos de transacciones aceptados. |

### <a name="schemas"></a>Esquemas
| Propiedad | Descripción |
| --- | --- |
| UNH2.1 (TYPE) (UNH2.1 [TIPO]) |Seleccione un tipo de conjunto de transacciones. |
| UNH2.2 (VERSION) (UNH2.2 [VERSIÓN]) |Escriba el número de versión de mensaje de Hola. |
| UNH2.3 (RELEASE) (UNH2.3 [LANZAMIENTO]) |Escriba el número de versión de mensaje de Hola. |
| Esquema |Seleccione Hola esquema toouse. Los esquemas se encuentran en la cuenta de integración. tooaccess los esquemas, vincular primero la aplicación de la lógica de la cuenta tooyour integración. |

### <a name="envelopes"></a>Envelopes (Sobres)
| Propiedad | Descripción |
| --- | --- |
| UNB8 (Processing Priority Code) (UNB8 [Código de prioridad de procesamiento]) |Escriba un valor alfabético con un solo carácter. |
| UNB10 (Communication Agreement) (UNB10 [Acuerdo de comunicaciones]) |Escriba un valor alfanumérico con un carácter como mínimo y 40 como máximo. |
| UNB11 (Test Indicator) (UNB11 [Indicador de prueba]) |Seleccione este tooindicate casilla de verificación que Hola Intercambio generado tenga datos de prueba |
| Aplicar segmento UNA (notificación del servicio) |Seleccione este toogenerate casilla un segmento UNA para toobe de intercambio de hello enviado. |
| Aplicar segmentos UNG (encabezado de grupo funcional) |Seleccione este toocreate casilla segmentos de agrupación en el encabezado de grupo funcional de Hola Hola mensajes enviados toohello invitado asociado. Hello valores son toocreate usado hello UNG segmentos: <p>En el caso de **UNG1**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de seis caracteres. <p>En el caso de **UNG2.1**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de 35 caracteres. <p>En el caso de **UNG2.2**, escriba un valor alfanumérico con un máximo de cuatro caracteres. <p>En el caso de **UNG3.1**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de 35 caracteres. <p>En el caso de **UNG3.2**, escriba un valor alfanumérico con un máximo de cuatro caracteres. <p>En el caso de **UNG6**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de tres. <p>En el caso de **UNG7.1**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de tres caracteres. <p>En el caso de **UNG7.2**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de tres caracteres. <p>En el caso de **UNG7.3**, escriba un valor alfanumérico con un mínimo de un carácter y un máximo de seis caracteres. <p>En el caso de **UNG8**, escriba un valor alfanumérico con un carácter como mínimo y 14 caracteres como máximo. |

### <a name="character-sets-and-separators"></a>Character Sets and Separators (Juegos de caracteres y separadores)

Aparte de juego de caracteres de hello, puede especificar un conjunto diferente de toobe delimitadores utilizado para cada tipo de mensaje. Si no se especifica un juego de caracteres para un esquema de mensaje dado, se utiliza el juego de caracteres predeterminado de Hola.

| Propiedad | Descripción |
| --- | --- |
| UNB1.1 (System Identifier) (UNB1.1 [Identificador del sistema]) |Seleccione Hola de caracteres EDIFACT establece toobe aplicado en hello intercambio de salida. |
| Esquema |Seleccione un esquema de la lista desplegable de Hola. Después de completar cada fila, se agrega automáticamente una nueva. Para el esquema seleccionado de hello, los separadores de hello seleccione establecen que desea toouse, en función de hello siguientes descripciones de separador. |
| Tipo de entrada |Seleccione un tipo de entrada de lista desplegable de Hola. |
| Separador de componentes |elementos de datos compuestos tooseparate, escriba un único carácter. |
| Separador de elementos de datos |tooseparate elementos de datos simples dentro de los elementos de datos compuesto, escriba un único carácter. |
| Terminador de segmento |final de hello tooindicate de un segmento EDI, escriba un único carácter. |
| Sufijo |Seleccione el carácter de Hola que se usa con el identificador de segmento de Hola. Si designa un sufijo, Hola elemento de datos del terminador de segmento puede estar vacío. Si el terminador de segmento de Hola se deja vacío, debe designar un sufijo. |

### <a name="control-numbers"></a>Control Numbers (Números de control)
| Propiedad | Descripción |
| --- | --- |
| UNB5 (Interchange Control Number) (UNB5 [Número de control de intercambio]) |Escriba un prefijo, un intervalo de valores para el número de control de intercambio de Hola y un sufijo. Estos valores son toogenerate usa un intercambio saliente. sufijo y prefijo de hello son opcionales, mientras que el número de control de hello es obligatorio. número de control de Hola se incrementa para cada mensaje nuevo; prefijo de Hola y el sufijo continúan Hola mismo. |
| UNG5 (Group Control Number) (UNG5 [Número de control de grupo]) |Escriba un prefijo, un intervalo de valores para el número de control de intercambio de Hola y un sufijo. Estos valores se usan número de control de grupo de toogenerate Hola. sufijo y prefijo de hello son opcionales, mientras que el número de control de hello es obligatorio. número de control de Hola se incrementa para cada nuevo mensaje hasta que se alcanza el valor máximo de hello; prefijo de Hola y el sufijo continúan Hola mismo. |
| UNH1 (Message Header Reference Number) (UNH1 [Número de referencia de encabezado de mensaje]) |Escriba un prefijo, un intervalo de valores para el número de control de intercambio de Hola y un sufijo. Estos valores se usan número de referencia de encabezado de mensaje de Hola de toogenerate. sufijo y prefijo de hello son opcionales, mientras que el número de referencia de hello es obligatorio. número de referencia de Hola se incrementa para cada mensaje nuevo; prefijo de Hola y el sufijo continúan Hola mismo. |

### <a name="validations"></a>Validations (Validaciones)

Cuando haya completado cada fila de validación, se agrega otra automáticamente. Si no se especifica ninguna regla, validación usa fila de Hola "Default".

| Propiedad | Descripción |
| --- | --- |
| Message Type (Tipo de mensaje) |Seleccione el tipo de mensaje de Hola EDI. |
| EDI Validation (Validación de EDI) |Realizar la validación EDI en tipos de datos tal como se define en las propiedades EDI de hello del esquema de hello, las restricciones de longitud, elementos de datos vacíos y separadores finales. |
| Extended Validation (Validación extendida) |Si el tipo de datos de hello no es EDI, validación en requisito de elemento de datos de Hola y permite la repetición, enumeraciones y datos de validación de longitud de elemento (mín./máx.). |
| Allow Leading/Trailing Zeroes (Permitir ceros a la izquierda/finales) |Conserve los caracteres de espacio y cero iniciales o finales adicionales. No los quite. |
| Recortar ceros iniciales y finales |Quite los ceros iniciales o finales. |
| Trailing Separator Policy (Directiva de separador final) |Genere separadores finales. <p>Seleccione **no permite** tooprohibit los delimitadores finales y separadores en hello envían el intercambio. Si el intercambio de hello tiene delimitadores y separadores finales, intercambio de Hola se declara no válido. <p>Seleccione **opcional** toosend intercambios con o sin delimitadores y separadores finales. <p>Seleccione **obligatorio** si intercambio Hola enviado debe tener delimitadores y separadores finales. |

## <a name="find-your-created-agreement"></a>Búsqueda del contrato creado

1.  Cuando termine de establecer las propiedades de acuerdo, en hello **agregar** hoja, elija **Aceptar** toofinish crear acuerdo y hoja de cuenta de la integración de tooyour devuelto.

    Ahora el contrato recién agregado aparece en la lista **Acuerdos**.

2.  También puede ver los contratos en la información general de la cuenta de integración. En la hoja de la cuenta de integración, elija **Introducción**, a continuación, seleccione hello **contratos** icono. 

    ![Elija "Acuerdos" icono tooview todos los contratos](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Ver el archivo de Swagger
detalles de Swagger de tooview hello para el conector de saludo EDIFACT, vea [EDIFACT](/connectors/edifact/).

## <a name="learn-more"></a>Más información
* [Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  

