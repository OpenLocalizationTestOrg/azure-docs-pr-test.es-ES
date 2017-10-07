---
title: "aaaAdd condiciones e iniciar flujos de trabajo: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Controle la ejecución de flujos de trabajo en Azure Logic Apps mediante la incorporación de lógica condicional, desencadenadores, acciones y parámetros."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Uso de las características de aplicaciones lógicas

En un [tema anterior](../logic-apps/logic-apps-create-a-logic-app.md), creó su primera aplicación lógica. toocontrol flujo de trabajo de la aplicación lógica, puede especificar diferentes rutas de acceso para su toorun de aplicación lógica y cómo demasiado procesar datos en las matrices, colecciones y lotes. Puede incluir estos elementos en el flujo de trabajo de la aplicación lógica:

* Las condiciones y las instrucciones [switch](../logic-apps/logic-apps-switch-case.md) permiten que la aplicación lógica ejecute distintas acciones en función de que se cumplan determinadas condiciones.

* Los [bucles](../logic-apps/logic-apps-loops-and-scopes.md) permiten que la aplicación lógica ejecute pasos varias veces. Por ejemplo, puede repetir acciones en una matriz si usa un bucle **For_each**. También puede repetir acciones hasta que se cumpla una condición si usa un bucle **Until**.

* [Ámbitos](../logic-apps/logic-apps-loops-and-scopes.md) permiten agrupar serie de acciones juntos, por ejemplo, control de excepciones de tooimplement.

* [Anulando](../logic-apps/logic-apps-loops-and-scopes.md) permite que la aplicación lógica iniciar flujos de trabajo independientes para los elementos en una matriz cuando se usa hello **SplitOn** comando.

En este tema se presentan otros conceptos de creación de la aplicación lógica:

* Vista tooedit una aplicación existente de la lógica de código
* Opciones para iniciar un flujo de trabajo

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Condiciones: ejecutan pasos solo después de que se cumpla una condición

toohave la aplicación lógica ejecutar pasos solo cuando los datos cumplen determinados criterios, puede agregar una condición que compara los datos de flujo de trabajo de hello en campos específicos o valores.

Por ejemplo, suponga que tiene una aplicación lógica que le envía demasiados correos electrónicos para entradas en la fuente RSS de un sitio web. Puede agregar una condición para que la aplicación lógica envía correo electrónico únicamente cuando Hola de nuevo registrar pertenece tooa determinada categoría.

1. Hola [portal de Azure](https://portal.azure.com), busque y abra la aplicación lógica en el Diseñador de la lógica de aplicación.

2. Agregar una ubicación de flujo de trabajo de toohello de condición que desea. 

   condición de hello tooadd entre los pasos existentes en el flujo de trabajo de aplicación de lógica de hello, Mover puntero de hello sobre flecha Hola donde desea que la condición de hello tooadd. 
   Elija hello **signo** (**+**), a continuación, elija **agregar una condición**. Por ejemplo:

   ![Agregar condición toologic aplicación](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Si desea tooadd una condición de final de hello del flujo de trabajo actual, vaya toohello inferior de la aplicación lógica y elija **+ nuevo paso**.

3. Definir condición de Hola. Especificar el campo de origen de Hola que desea tooevaluate, Hola operación tooperform y el valor del objetivo de Hola o campo. tooadd existente campos condición tooyour, elegir hello **agregar lista de contenido dinámico**.

   Por ejemplo:

   ![Edición de una condición en modo básico](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Esta es la condición completa hello:

   ![Condición completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > condición de hello toodefine en el código, elija **editar en el modo avanzado**. Por ejemplo:
   > 
   > ![Edición de la condición en el código](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. En **Sí si** y **si NO**, agregar Hola pasos tooperform en función de si se cumple la condición de Hola.

   Por ejemplo:

   ![Condición con las trayectoria en caso de AFIRMATIVO y NEGATIVO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Puede arrastrar acciones existentes en hello **Sí si** y **si NO** las rutas de acceso.

5. Cuando haya terminado, guarde la aplicación lógica.

Ahora obtendrá los correos electrónicos sólo cuando Hola entradas cumplen la condición.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Repetición de acciones de una lista con forEach

bucle forEach de Hello especifica un toorepeat de matriz una acción sobre él. Si no es una matriz, se produce un error en el flujo de Hola. Por ejemplo, si tiene action1 que genera una matriz de mensajes y desea toosend cada mensaje, puede incluir esta instrucción forEach en Propiedades de saludo de la acción:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Editar definición de código de hello para una aplicación de lógica

Aunque tienen Hola diseñador la lógica de aplicación, puede editar directamente el código de hello que define una aplicación de la lógica.

1. En la barra de comandos de hello, elija **vista código**.

    Un completo editor abre y muestra la definición de hello editó.

    ![vista Código](media/logic-apps-use-logic-app-features/codeview.png)

    En el editor de texto hello, puede copiar y pegar cualquier número de las acciones de hello misma lógica de aplicación o entre aplicaciones lógicas. 
    Puede agregar o quitar secciones completas de definición de hello también fácilmente, y también pueden compartir las definiciones con otros.

2. las modificaciones, elija a toosave **guardar**.

## <a name="parameters"></a>parameters

Algunas funcionalidades de Logic Apps solo están disponibles en la vista de código, como, por ejemplo, los parámetros. Parámetros que sea fácil tooreuse valores a lo largo de la aplicación lógica. Por ejemplo, si tiene una dirección de correo electrónico que desea utilizar en varias acciones, debe definirla como un parámetro.

Parámetros son buenos para extraer los valores que son muy toochange probable. Son especialmente útiles cuando necesite toooverride parámetros en entornos diferentes. toolearn toooverride los parámetros basados en el entorno, vea [crear definiciones de aplicación lógica](../logic-apps/logic-apps-author-definitions.md) y [documentación de la API de REST](https://docs.microsoft.com/rest/api/logic).

Este ejemplo se muestra cómo tooupdate la aplicación lógica existente para que puedan utilizar parámetros de término de consulta de Hola.

1. En la vista de código, busque hello `parameters : {}` objeto y agregar un `currentFeedUrl` objeto:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Vaya toohello `When_a_feed-item_is_published` acción, buscar hello `queries` sección y reemplace el valor de la consulta de hello con:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin dos o más cadenas, también puede usar hello `concat` función. 
    Por ejemplo, `"@concat('#',parameters('currentFeedUrl'))"` funciona igual Hola como Hola anterior.

3.  Cuando termine, seleccione **Guardar**. 

    Ahora puede cambiar fuente pasando una dirección URL diferente a través de Hola RSS del sitio Web de hello `currentFeedURL` objeto.

Obtenga más información sobre [cómo definiciones de aplicación lógica de tooauthor](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Inicio de flujos de trabajo de aplicación lógica

Tener distintas opciones para iniciar el flujo de trabajo de hello definido en la aplicación lógica. Siempre puede iniciar un flujo de trabajo a petición en hello [portal de Azure].

### <a name="recurrence-triggers"></a>Desencadenadores periódicos

Un desencadenador periódico se ejecuta en un intervalo que especifique. Cuando el desencadenador de hello tiene lógica condicional, desencadenador Hola determina si el flujo de trabajo de hello debe toorun. Un desencadenador indica que debe ejecutar el flujo de trabajo de hello devolviendo un `200` código de estado. Flujo de trabajo de hello necesita toorun, desencadenador de hello devuelve un `202` código de estado.

### <a name="callback-using-rest-apis"></a>Devolución de llamada mediante las API de REST

toostart un flujo de trabajo, servicios pueden llamar a un punto de conexión de la aplicación lógica. Este tipo de lógica aplicación a petición, elija a toostart **ejecutar ahora** en la barra de comandos de Hola. Vea [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md) (Inicio de flujos de trabajo mediante llamadas a puntos de conexión de aplicación lógica como desencadenadores). 

<!-- Shared links -->
[portal de Azure]: https://portal.azure.com

## <a name="next-steps"></a>Pasos siguientes

* [Instrucciones switch](../logic-apps/logic-apps-switch-case.md) 
* [Bucles, ámbitos y desagrupación](../logic-apps/logic-apps-loops-and-scopes.md)
* [Creación de definiciones de aplicación lógica](../logic-apps/logic-apps-author-definitions.md)