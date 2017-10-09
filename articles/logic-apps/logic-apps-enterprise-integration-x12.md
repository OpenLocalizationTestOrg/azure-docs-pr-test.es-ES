---
title: "mensajes de aaaX12 para la integración de enterprise B2B - Azure Logic Apps | Documentos de Microsoft"
description: "Intercambie mensajes X12 en formato EDI para la integración empresarial B2B con Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>Intercambio de mensajes X12 para la integración empresarial con aplicaciones lógicas

Para poder intercambiar mensajes X12 para Azure Logic Apps, debe crear un contrato X12 y almacenarlo en su cuenta de integración. Estos son los pasos de Hola para saber cómo toocreate una X12 acuerdo.

> [!NOTE]
> Esta página incluye características de hello X12 para las aplicaciones lógicas de Azure. Para más información, consulte [EDIFACT](logic-apps-enterprise-integration-edifact.md).

## <a name="before-you-start"></a>Antes de comenzar

Aquí es elementos de Hola que necesita:

* Una [cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md) que ya esté definida y asociada a su suscripción de Azure
* Al menos dos [socios](../logic-apps/logic-apps-enterprise-integration-partners.md) que se definen en su cuenta de integración y configurado con el identificador hello X12 en **las identidades de negocio**    
* Obligatoria [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) para cargar tooyour [cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md)

Después de [crear una cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md), [agregar socios](logic-apps-enterprise-integration-partners.md)y tener un [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que desea toouse, puede crear un X12 acuerdo siguiendo estos pasos.

## <a name="create-an-x12-agreement"></a>Creación de un contrato X12

1.  Inicie sesión en toohello [portal de Azure](http://portal.azure.com "portal de Azure"). En el menú izquierdo de hello, seleccione **más servicios**. 

    > [!TIP]
    > Si no ve **más servicios**, es posible que tenga menú de hello tooexpand en primer lugar. Hola parte superior de hello contraído menú, seleccione **menú de mostrar**.

    ![En el menú izquierdo, seleccione "Más servicios"](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  En el cuadro de búsqueda de hello, escriba "integración" como filtro. En la lista de resultados de hello, seleccione **cuentas de integración**.  

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. Hola **cuentas de integración** hoja que se abre, cuenta de integración de hello seleccione donde desea que el acuerdo de hello tooadd.
Si no ve ninguna, [créela](../logic-apps/logic-apps-enterprise-integration-accounts.md "Información completa sobre las cuentas de integración").

    ![Seleccionar cuenta de integración donde toocreate Hola acuerdo](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. Seleccione **Introducción**, a continuación, seleccione hello **contratos** icono. Si no tiene un icono de acuerdos, agregar icono hello en primer lugar. 

    ![Elección del icono "Acuerdos"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. En la hoja de contratos de Hola que se abre, elija **agregar**.

    ![Elección de "Agregar"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. En **Agregar**, escriba un valor en **Nombre** para el contrato. Para el tipo de contrato de hello, seleccione **X12**. Seleccione hello **socio del Host**, **identidad del Host**, **socio invitado**, y **identidad Invitado** para el acuerdo. Para obtener la propiedad, vea la tabla de hello en este paso.

    ![Especificación de los detalles del contrato](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | Propiedad | Descripción |
    | --- | --- |
    | Nombre |Nombre del contrato de Hola |
    | Tipo de contrato | Debe ser X12 |
    | Host Partner (Partner anfitrión) |Un contrato tiene asociado un partner anfitrión e invitado. el socio del host de Hello representa la organización de Hola que configura el acuerdo de Hola. |
    | Host Identity (Identidad anfitriona) |Un identificador para el socio del host de Hola |
    | Guest Partner (Partner invitado) |Un contrato tiene asociado un partner anfitrión e invitado. Socio invitado de Hello representa la organización de hello encargado de negocio con el socio del host de Hola. |
    | Guest Identity |Un identificador para el socio invitado de Hola |
    | Receive Settings (Configuración de recepción) |Estas propiedades aplican tooall los mensajes recibidos por un acuerdo. |
    | Send Settings (Configuración de envío) |Estas propiedades aplican tooall los mensajes enviados por un acuerdo. |  

  > [!NOTE]
  > Resolución de X12 acuerdo depende de la coincidencia calificador de remitente de Hola e identificador y calificador de receptor de hello e identificador definido en socio de Hola y el mensaje entrante. Si cambian estos valores para que el socio, actualizar acuerdo de hello demasiado.

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configuración de la forma en que su contrato controla los mensajes recibidos

Ahora que ha establecido las propiedades del acuerdo de hello, puede configurar cómo este contrato identifica y controla los mensajes entrantes recibidos del socio a través de este contrato.

1.  En **Agregar**, seleccione **Configuración de recepción**.
Configurar estas propiedades basándose en el acuerdo de socio de Hola que intercambia mensajes con usted. Para obtener descripciones de propiedad, vea las tablas de hello en esta sección.

    **Configuración de recepción** se divide en las siguientes secciones: Identificadores, Reconocimiento, Esquemas, Sobres, Números de control, Validaciones y Configuración interna.

2. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora, el contrato es listo toohandle entrante los mensajes que cumplen tooyour la configuración seleccionada.

### <a name="identifiers"></a>Identifiers (Identificadores)

![Establezca las propiedades de identificadores](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| Propiedad | Descripción |
| --- | --- |
| ISA1 (Authorization Qualifier) (ISA1 (calificador de autorización)) |Seleccione valor del calificador de autorización de Hola de lista desplegable de Hola. |
| ISA2 |Opcional. Escriba el valor de la información de autorización. Si el valor de hello introducido para ISA1 es distinto de 00, introduzca un carácter alfanumérico como mínimo y un máximo de 10. |
| ISA3 (Security Qualifier) (ISA3 (calificador de seguridad)) |Seleccione valor del calificador de seguridad de Hola de lista desplegable de Hola. |
| ISA4 |Opcional. Escriba el valor de información de seguridad de Hola. Si el valor de hello introducido para ISA3 es distinto de 00, introduzca un carácter alfanumérico como mínimo y un máximo de 10. |

### <a name="acknowledgment"></a>Acknowledgement (Confirmación)

![Establezca las propiedades de confirmación](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| Propiedad | Descripción |
| --- | --- |
| TA1 expected (TA1 esperada) |Devuelve un remitente de intercambio de confirmación técnica toohello |
| FA expected (FA esperada) |Devuelve un remitente de intercambio de toohello de confirmación funcional. A continuación, seleccione si desea que las confirmaciones de hello 997 o 999, basada en la versión de esquema de Hola |
| Include AK2/IK2 Loop (Incluir bucle AK2/IK2) |Habilita la generación de bucles AK2 en confirmaciones funcionales para conjuntos de transacciones aceptadas |

### <a name="schemas"></a>Esquemas

Seleccione un esquema para cada tipo de transacción (ST1) y aplicación de remitente (GS2). Hola recibir canalización desensambla el mensaje entrante de hello haciendo coincidir los valores de hello para ST1 y GS2 mensaje entrante de Hola y Hola los valores que se establecen aquí y el esquema de Hola de mensaje entrante de Hola con el esquema de Hola que configure aquí.

![Seleccione un esquema](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| Propiedad | Descripción |
| --- | --- |
| Versión |Seleccione la versión de hello X12 |
| Transaction Type (ST01) (Tipo de transacción (ST01)) |Seleccione el tipo de transacción de Hola |
| Sender Application (GS02) (Aplicación remitente (GS02)) |Seleccione la aplicación del remitente Hola |
| Esquema |Seleccione el archivo de esquema de Hola que quiera toouse. Los esquemas se agregan tooyour cuenta de integración. |

> [!NOTE]
> Configurar Hola necesario [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que es cargado tooyour [cuenta integración](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Envelopes (Sobres)

![Especificar el separador de hello en un conjunto de transacciones: Elegir identificador estándar o separador de repeticiones](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| Propiedad | Descripción |
| --- | --- |
| ISA11 Usage (Uso de ISA11) |Especifica Hola separador toouse en un conjunto de transacciones: <p>Seleccione **identificador estándar** toouse un punto (.) para la notación decimal, en lugar de notación decimal de hello del documento de entrada de Hola Hola EDI la canalización de recepción. <p>Seleccione **separador de repeticiones** toospecify separador de Hola para las repeticiones de un elemento de datos simple o una estructura de datos repetidas. Por ejemplo, normalmente hello acento circunflejo (^) se utiliza como separador de repeticiones de Hola. Para los esquemas HIPAA, sólo puede utilizar acento circunflejo Hola. |

### <a name="control-numbers"></a>Control Numbers (Números de control)

![Seleccione cómo toohandle controlar duplicados en números](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| Propiedad | Descripción |
| --- | --- |
| Disallow Interchange Control Number duplicates (No permitir duplicados del número de control de intercambio) |Bloquee los intercambios duplicados. Comprueba el número de control de intercambio de hello (ISA13) para el número de control de intercambio de hello recibido. Si se detecta una coincidencia, Hola recibir canalización no procesa el intercambio de Hola. Puede especificar Hola número de días para realizar la comprobación de hello especificando un valor para *comprobar isa13 duplicados cada (días)*. |
| Disallow Group control number duplicates (No permitir duplicados del número de control de grupo) |Bloquee los intercambios con números de control de grupo duplicados. |
| Disallow Transaction set control number duplicates (No permitir duplicados del número de control del conjunto de transacciones) |Bloquee los intercambios con números de control de conjunto de transacciones duplicados. |

### <a name="validations"></a>Validations (Validaciones)

![Establezca las propiedades de validación de mensajes recibidos](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

Cuando haya completado cada fila de validación, se agrega otra automáticamente. Si no se especifica ninguna regla, validación usa fila de Hola "Default".

| Propiedad | Descripción |
| --- | --- |
| Message Type (Tipo de mensaje) |Seleccione el tipo de mensaje de Hola EDI. |
| EDI Validation (Validación de EDI) |Realizar la validación EDI en tipos de datos definidos por el del esquema de hello EDI propiedades, las restricciones de longitud, elementos de datos vacíos y separadores finales. |
| Extended Validation (Validación extendida) |Si el tipo de datos de hello no es EDI, validación en requisito de elemento de datos de Hola y permite la repetición, enumeraciones y datos de validación de longitud de elemento (mín./máx.). |
| Allow Leading/Trailing Zeroes (Permitir ceros a la izquierda/finales) |Conserve los caracteres de espacio y cero iniciales o finales adicionales. No los quite. |
| Recortar ceros iniciales y finales |Quite los caracteres de espacio y cero iniciales o finales. |
| Trailing Separator Policy (Directiva de separador final) |Genere separadores finales. <p>Seleccione **no permite** tooprohibit los delimitadores finales y separadores en hello recibieron el intercambio. Si el intercambio de hello tiene delimitadores y separadores finales, intercambio de Hola se declara no válido. <p>Seleccione **opcional** tooaccept intercambios con o sin delimitadores y separadores finales. <p>Seleccione **obligatorio** al intercambio de hello debe tener delimitadores y separadores finales. |

### <a name="internal-settings"></a>Internal Settings (Configuración interna)

![Seleccione la configuración interna](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| Propiedad | Descripción |
| --- | --- |
| Convertir formato decimal implícito "Nn" tooa base 10 valor numérico |Convierte a un número EDI especificado con el formato de Hola "Nn" en un valor numérico de base 10 |
| Create empty XML tags if trailing separators are allowed (Crear etiquetas XML vacías si se permiten separadores finales) |Seleccione este remitente de intercambio de casilla de verificación toohave Hola incluyen vacía etiquetas XML para los separadores finales. |
| Dividir intercambio como conjuntos de transacciones: suspender conjuntos de transacciones en caso de error|Analiza cada conjunto de transacciones en un intercambio en un documento XML independiente aplicando el conjunto de transacciones de toohello Hola sobre adecuado. Suspende solo las transacciones de Hola donde se produce un error en la validación de Hola. |
| Dividir intercambio como conjuntos de transacciones: suspender intercambio en caso de error|Analiza cada conjunto de transacciones en un intercambio en un documento XML independiente aplicando el sobre adecuado Hola. Se suspende todo el intercambio cuando uno o varios conjuntos de transacciones de intercambio de hello no superan la validación. | 
| Conservar intercambio: suspender conjuntos de transacciones en caso de error |Intercambio de hello permanecen intactos, crea un documento XML para todo el intercambio por lotes Hola. Solo conjuntos de transacciones de Hola que no superan la validación, mientras continúa tooprocess se suspende todos los demás conjuntos de transacciones. |
| Conservar intercambio: suspender intercambio en caso de error |Intercambio de hello permanecen intactos, crea un documento XML para todo el intercambio por lotes Hola. Se suspende todo el intercambio hello cuando uno o varios conjuntos de transacciones de intercambio de hello no superan la validación. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configuración de la forma en que su contrato envía mensajes

Puede configurar cómo este contrato identifica y controla los mensajes salientes que envían a tooyour asociado a través de este contrato.

1.  En **Agregar**, seleccione **Send Settings** (Configuración de envío).
Configure estas propiedades en función del contrato con el asociado con el que intercambia mensajes. Para obtener descripciones de propiedad, vea las tablas de hello en esta sección.

    **Configuración de envío** se organiza en las siguientes secciones: Identificadores, Reconocimiento, Esquemas, Sobres, Juegos de caracteres y separadores, Números de control y Validación.

2. Cuando haya terminado, asegúrese de toosave seguro de la configuración eligiendo **Aceptar**.

Ahora el contrato es listo toohandle los mensajes que se ajustan tooyour seleccionado configuración salientes.

### <a name="identifiers"></a>Identifiers (Identificadores)

![Establezca las propiedades de identificadores](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| Propiedad | Descripción |
| --- | --- |
| ISA1 (Authorization Qualifier) (ISA1 (calificador de autorización)) |Seleccione valor del calificador de autorización de Hola de lista desplegable de Hola. |
| ISA2 |Escriba el valor de la información de autorización. Si el valor especificado es distinto de 00, especifique como mínimo un carácter alfanumérico y, como máximo, diez. |
| ISA3 (Security Qualifier) (ISA3 (calificador de seguridad)) |Seleccione valor del calificador de seguridad de Hola de lista desplegable de Hola. |
| ISA4 |Escriba el valor de información de seguridad de Hola. Si este valor es distinto de 00, en el cuadro de texto de hello valor (ISA4), a continuación, escriba un mínimo de caracteres alfanuméricos y un máximo de 10. |

### <a name="acknowledgment"></a>Acknowledgement (Confirmación)

![Establezca las propiedades de confirmación](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propiedad | Descripción |
| --- | --- |
| TA1 expected (TA1 esperada) |Devolver un remitente de intercambio de confirmación técnica (TA1) toohello. Esta configuración especifica a ese socio del host Hola que está enviando solicitudes de mensaje de Hola una confirmación del socio de invitado de hello en el acuerdo de Hola. Hola socio del host en función de la configuración de recepción de hello del acuerdo de Hola espera recibir dichas confirmaciones. |
| FA expected (FA esperada) |Devolver un remitente de intercambio de confirmación funcional (FA) toohello. Seleccione si desea Hola 997 o 999 confirmaciones, basadas en las versiones de esquema de Hola que está trabajando. Hola socio del host en función de la configuración de recepción de hello del acuerdo de Hola espera recibir dichas confirmaciones. |
| FA Version (Versión de FA) |Seleccione la versión de Hola FA |

### <a name="schemas"></a>Esquemas

![Seleccionar esquema toouse](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| Propiedad | Descripción |
| --- | --- |
| Versión |Seleccione la versión de hello X12 |
| Transaction Type (ST01) (Tipo de transacción (ST01)) |Seleccione el tipo de transacción de Hola |
| Esquema |Seleccione Hola esquema toouse. Los esquemas se encuentran en la cuenta de integración. Si selecciona primero un esquema, este configura automáticamente la versión y el tipo de transacción  |

> [!NOTE]
> Configurar Hola necesario [esquema](../logic-apps/logic-apps-enterprise-integration-schemas.md) que es cargado tooyour [cuenta integración](../logic-apps/logic-apps-enterprise-integration-accounts.md).

### <a name="envelopes"></a>Envelopes (Sobres)

![Especificar el separador de hello en un conjunto de transacciones: Elegir identificador estándar o separador de repeticiones](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| Propiedad | Descripción |
| --- | --- |
| ISA11 Usage (Uso de ISA11) |Especifica Hola separador toouse en un conjunto de transacciones: <p>Seleccione **identificador estándar** toouse un punto (.) para la notación decimal, en lugar de notación decimal de hello del documento de entrada de Hola Hola EDI la canalización de recepción. <p>Seleccione **separador de repeticiones** toospecify separador de Hola para las repeticiones de un elemento de datos simple o una estructura de datos repetidas. Por ejemplo, normalmente hello acento circunflejo (^) se utiliza como separador de repeticiones de Hola. Para los esquemas HIPAA, sólo puede utilizar acento circunflejo Hola. |

### <a name="control-numbers"></a>Control Numbers (Números de control)

![Especifique las propiedades de número de control](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| Propiedad | Descripción |
| --- | --- |
| Control version number (ISA12) (Número de versión de control (ISA12)) |Seleccione la versión de Hola de hello X12 estándar |
| Usage Indicator (ISA15) (Indicador de uso (ISA15)) |Seleccione el contexto de Hola de un intercambio.  valores de Hello son información, datos de producción, o datos de prueba |
| Esquema |Genera los segmentos ST para un intercambio codificado en X12 que envía toohello canalización de envío y saludo GS |
| GS1 |Opcional, seleccione un valor para el código funcional de Hola de lista desplegable de Hola |
| GS2 |Opcional, remitente de la aplicación |
| GS3 |Opcional, receptor de la aplicación |
| GS4 |Opcional, seleccione CCYYMMDD (SSAAMMDD) o YYMMDD (AAMMDD). |
| GS5 |Opcional, seleccione HHMM, HHMMSS o HHMMSSdd. |
| GS7 |Opcional, seleccione un valor para Agencia responsable de Hola de lista desplegable de Hola |
| GS8 |Opcional, versión del documento de Hola |
| Interchange Control Number (ISA13) (Número de control de intercambio (ISA13)) |Necesario, escriba un intervalo de valores para el número de control de intercambio de Hola. Escriba un valor numérico: 1 como mínimo y 999999999 como máximo |
| Group Control Number (GS06) (Número de control de grupo (GS06)) |Necesario, escriba un intervalo de números para número de control de grupo de Hola. Escriba un valor numérico: 1 como mínimo y 999999999 como máximo |
| Transaction Set Control Number (ST02) (Número de control de conjunto de transacciones (ST02)) |Necesario, escriba un intervalo de números de hello número de Control de conjunto de transacciones. Escriba un intervalo de valores numéricos: 1 como mínimo y 999999999 como máximo. |
| Prefijo |Opcional, designado para el intervalo de Hola de números de control de conjunto de transacciones utilizados en la confirmación. Escriba un valor numérico para dos campos centrales hello y un valor alfanumérico (si lo desea) para los campos de prefijo y sufijo de Hola. campos centrales Hola son obligatorios y contienen Hola valores mínimo y máximo para el número de control de Hola |
| Sufijo |Opcional, designado para el intervalo de Hola de números de control de conjunto de transacciones utilizados en una confirmación. Escriba un valor numérico para dos campos centrales hello y un valor alfanumérico (si lo desea) para los campos de prefijo y sufijo de Hola. campos centrales Hola son obligatorios y contienen Hola valores mínimo y máximo para el número de control de Hola |

### <a name="character-sets-and-separators"></a>Character Sets and Separators (Juegos de caracteres y separadores)

Aparte de juego de caracteres de hello, puede especificar un conjunto diferente de delimitadores para cada tipo de mensaje. Si no se especifica un juego de caracteres para un esquema de mensaje dado, se utiliza el juego de caracteres predeterminado de Hola.

![Especifique los delimitadores para tipos de mensaje](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| Propiedad | Descripción |
| --- | --- |
| Toobe de conjunto de caracteres utilizado |propiedades de hello toovalidate, seleccione hello X12 juego de caracteres. Opciones de Hello son básico, ampliado y UTF8. |
| Esquema |Seleccione un esquema de la lista desplegable de Hola. Después de completar cada fila, se agrega automáticamente una nueva. Para el esquema seleccionado de hello, los separadores de hello seleccione establecen que desea toouse, en función de hello siguientes descripciones de separador. |
| Tipo de entrada |Seleccione un tipo de entrada de lista desplegable de Hola. |
| Separador de componentes |elementos de datos compuestos tooseparate, escriba un único carácter. |
| Separador de elementos de datos |tooseparate elementos de datos simples dentro de los elementos de datos compuesto, escriba un único carácter. |
| Carácter de reemplazo |Escriba un carácter de sustitución que se usa para reemplazar todos los caracteres separadores en datos de carga de hello al generar mensajes de bienvenida X12 saliente. |
| Terminador de segmento |final de hello tooindicate de un segmento EDI, escriba un único carácter. |
| Sufijo |Seleccione el carácter de Hola que se usa con el identificador de segmento de Hola. Si designa un sufijo, Hola elemento de datos del terminador de segmento puede estar vacío. Si el terminador de segmento de Hola se deja vacío, debe designar un sufijo. |

> [!TIP]
> valores de caracteres especiales de tooprovide, editar acuerdo hello como JSON y proporcionan un valor ASCII Hola carácter especial de Hola.

### <a name="validation"></a>Validación

![Establezca las propiedades de validación para enviar mensajes](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

Cuando haya completado cada fila de validación, se agrega otra automáticamente. Si no se especifica ninguna regla, validación usa fila de Hola "Default".

| Propiedad | Descripción |
| --- | --- |
| Message Type (Tipo de mensaje) |Seleccione el tipo de mensaje de Hola EDI. |
| EDI Validation (Validación de EDI) |Realizar la validación EDI en tipos de datos definidos por el del esquema de hello EDI propiedades, las restricciones de longitud, elementos de datos vacíos y separadores finales. |
| Extended Validation (Validación extendida) |Si el tipo de datos de hello no es EDI, validación en requisito de elemento de datos de Hola y permite la repetición, enumeraciones y datos de validación de longitud de elemento (mín./máx.). |
| Allow Leading/Trailing Zeroes (Permitir ceros a la izquierda/finales) |Conserve los caracteres de espacio y cero iniciales o finales adicionales. No los quite. |
| Recortar ceros iniciales y finales |Quite los ceros iniciales o finales. |
| Trailing Separator Policy (Directiva de separador final) |Genere separadores finales. <p>Seleccione **no permite** tooprohibit los delimitadores finales y separadores en hello envían el intercambio. Si el intercambio de hello tiene delimitadores y separadores finales, intercambio de Hola se declara no válido. <p>Seleccione **opcional** toosend intercambios con o sin delimitadores y separadores finales. <p>Seleccione **obligatorio** si intercambio Hola enviado debe tener delimitadores y separadores finales. |

## <a name="find-your-created-agreement"></a>Búsqueda del contrato creado

1.  Cuando termine de establecer las propiedades de acuerdo, en hello **agregar** hoja, elija **Aceptar** toofinish crear acuerdo y hoja de cuenta de la integración de tooyour devuelto.

    Ahora el contrato recién agregado aparece en la lista **Acuerdos**.

2.  También puede ver los contratos en la información general de la cuenta de integración. En la hoja de la cuenta de integración, elija **Introducción**, a continuación, seleccione hello **contratos** icono.

    ![Elija "Acuerdos" icono tooview todos los contratos](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Swagger de hello de vista
Vea hello [swagger detalles](/connectors/x12/). 

## <a name="learn-more"></a>Más información
* [Obtener más información sobre Hola paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  

