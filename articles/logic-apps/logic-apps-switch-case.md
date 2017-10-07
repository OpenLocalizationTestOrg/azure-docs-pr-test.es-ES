---
title: "instrucción aaaSwitch para distintas acciones en las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Elija tooperform acciones diferentes en las aplicaciones lógicas basadas en valores de expresión mediante una instrucción switch"
services: logic-apps
keywords: "Instrucción switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Diferentes acciones en Logic Apps con una instrucción switch

Al crear un flujo de trabajo, tendrá a menudo tootake diferentes acciones basadas en valor de Hola de un objeto o una expresión. Por ejemplo, es recomendable su toobehave de aplicación lógica diferente en función de código de estado de Hola de una solicitud HTTP, como una opción seleccionada en un correo electrónico.

Puede usar un tooimplement de la instrucción switch en estos escenarios. La aplicación lógica puede evaluar un símbolo (token) o una expresión y elegir el caso de Hola Hola Hola de tooexecute valor mismo acciones especificadas. Un solo caso debe coincidir con la instrucción switch de Hola.

> [!TIP]
> Al igual que todos los lenguajes de programación, la instrucción switch solo admite los operadores de igualdad. Utilice una instrucción de condición si necesita otros operadores relacionales, como "mayor que".
> comportamiento de ejecución determinista tooensure, casos deben contener un valor único y estático en lugar de símbolos (tokens) dinámico o una expresión.

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure activa. Si no tiene una suscripción de Azure activa, [cree una cuenta gratuita](https://azure.microsoft.com/free/) o pruebe [Logic Apps gratis](https://tryappservice.azure.com/).
- [Conocimientos básicos acerca de Logic Apps](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Agregar un flujo de trabajo de tooyour de instrucción switch

tooshow el funcionamiento de una instrucción switch, en este ejemplo se crea una aplicación de lógica que supervisa los archivos cargan tooDropbox. Cuando se cargan los nuevos archivos de hello, aplicación de lógica de hello envía aprobador de tooan de correo electrónico que elige si tootransfer tooSharePoint de esos archivos. aplicación Hello usa una instrucción switch que lleva a cabo diferentes acciones basadas en el valor de Hola que Hola selecciona aprobador.

1. Cree una aplicación lógica y seleccione el desencadenador **Dropbox - Cuando se crea un archivo** (Dropbox - Cuando se crea un archivo).

   ![Uso del desencadenador Dropbox - Cuando se crea un archivo](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. En el desencadenador de hello, agregue esta acción: **Outlook.com - enviar correo electrónico de aprobación**

   > [!TIP]
   > Logic Apps también admite escenarios de enviar un correo electrónico de aprobación desde una cuenta de Office 365 Outlook.

   - Si no tiene una conexión existente, se le pedirá toocreate uno.
   - Rellene los campos de hello necesario. Por ejemplo, en **a**, especifique la dirección de correo electrónico de hello para el envío de correo electrónico de aprobador Hola.
   - En **Opciones de usuario**, escriba `Approve, Reject`.

   ![Configuración de la conexión](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Agregue una instrucción switch.

   - Seleccione **+ Nuevo paso** > **... Más** > **Agregar un caso de conmutador**. 
   - Ahora queremos tooselect Hola acción tooperform en función de hello `SelectedOptions` de salida de hello *enviar correo electrónico de aprobación* acción. 
   Este campo se encuentra en hello **agregar contenido dinámico** selector.
   - Use *caso 1* toohandle cuando selecciona Aprobador hello `Approve`.
     - Si se aprueba, copie Hola original archivo tooSharePoint en línea con hello [ **SharePoint Online - crear archivo** acción](../connectors/connectors-create-api-sharepointonline.md).
     - Agregar otra acción los usuarios de mayúsculas toonotify Hola que está disponible en SharePoint un nuevo archivo.
   - Agregar otro toohandle mayúscula cuando el usuario selecciona `Reject`.
     - Si rechaza, envíe un correo electrónico de notificación que le informa de otros aprobadores que se rechazó el archivo de Hola y no es necesaria realizar ninguna otra acción.
   - `SelectedOptions`proporciona solo dos opciones, por lo que podemos dejar hello **predeterminado** caso vacía.

   ![Instrucción switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Una instrucción switch tiene al menos un caso en caso de adición toohello predeterminado.

4. Después de la instrucción switch de hello, eliminar Hola original tooDropbox de archivo cargado mediante la adición de esta acción: **Dropbox - eliminar archivo**

5. Guarde la aplicación lógica. Probar la aplicación mediante la carga de un archivo tooDropbox. En breve recibirá un correo electrónico de aprobación. Seleccione una opción y observar el comportamiento de Hola.

   > [!TIP]
   > Consulte cómo demasiado[supervisar las aplicaciones lógicas](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Comprender el código de hello detrás de las instrucciones switch

Ahora que ha creado correctamente una aplicación de lógica mediante una instrucción switch, echemos un vistazo a la definición de código de hello detrás de la instrucción switch de Hola.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`es el nombre de saludo de la instrucción switch de hello, que puede cambiar el nombre para mejorar la legibilidad. 
* `"type": "Switch"`indica que la acción de hello es una instrucción switch. 
* `"expression"`es la opción seleccionada del aprobador hello en este ejemplo y se evalúa con respecto a cada caso declarado más adelante en la definición de Hola. 
* `"cases"` puede contener cualquier número de casos. Para cada caso, `"Case *"` es nombre predeterminado de Hola de caso de hello, que puede cambiar el nombre para mejorar la legibilidad. 
`"case"`Especifica la etiqueta case hello, que usar expresiones de conmutador para la comparación de Hola y debe ser un valor único y constante. Si ninguno de los casos de hello coincide con la expresión switch hello, acciones en el `"default"` se ejecutan.

## <a name="get-help"></a>Obtener ayuda

tooask preguntas y responder a preguntas, consulte ¿Qué otros usuarios de aplicaciones de la lógica de Azure están realizando, visitan hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de cómo demasiado[agregar condiciones](logic-apps-use-logic-app-features.md)
- Aprenda sobre el [control de errores y las excepciones](logic-apps-exception-handling.md).
- Conozca más [funcionalidades del lenguaje de flujo de trabajo](logic-apps-author-definitions.md).