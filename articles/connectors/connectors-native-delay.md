---
title: "un retraso en las aplicaciones lógicas aaaAdd | Documentos de Microsoft"
description: "Información general de hello retraso y retraso-hasta que las acciones y cómo toouse con una aplicación de Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Empezar a trabajar con hello retraso y retraso-hasta acciones
Mediante el uso de retraso de Hola y "retraso-hasta" acciones, puede completar los escenarios de flujo de trabajo.

Por ejemplo, puede:

* Espere hasta que actualice un estado de día de la semana toosend por correo electrónico.
* Flujo de trabajo de hello de retraso hasta que una llamada HTTP tiene toofinish de tiempo antes de reanudar y recuperar el resultado de hello.

tooget se hayan iniciado mediante la acción de retraso de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Usar acciones de retraso de Hola
Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica. [Más información acerca de las acciones](connectors-overview.md).

Este es un ejemplo de secuencia de cómo toouse un retraso paso a paso en una aplicación de lógica:

1. Después de agregar un desencadenador, haga clic en **nuevo paso** tooadd una acción.
2. Busque **retraso** toobring las acciones de retraso de Hola. En este ejemplo, se seleccionará **Delay**.
   
    ![Acciones de retraso](./media/connectors-native-delay/using-action-1.png)
3. Siga cualquiera de retraso de hello acción propiedades tooconfigure Hola.
   
    ![Configuración de retraso](./media/connectors-native-delay/using-action-2.png)
4. Haga clic en **guardar** toopublish y activar la aplicación de la lógica de hello.

## <a name="action-details"></a>Detalles de la acción
desencadenador de periodicidad de Hello tiene Hola propiedades que se pueden configurar siguientes.

### <a name="delay-action"></a>Acción de retraso
Ejecute este Hola de retrasos de acción para un intervalo de tiempo determinado.
Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Recuento* |count |número de Hola de toodelay de unidades de tiempo |
| Unidad* |unit |unidad de Hola de tiempo: `Second`, `Minute`, `Hour`, o`Day` |

<br>

### <a name="delay-until-action"></a>Acción de retraso hasta
Esta acción retrasa Hola ejecutar hasta una fecha u hora especificada.
Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Año* |timestamp |Hola toodelay año hasta (GMT) |
| Mes* |timestamp |Hola toodelay mes hasta (GMT) |
| Día* |timestamp |Hola toodelay día hasta (GMT) |

<br>

## <a name="next-steps"></a>Pasos siguientes
Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md). Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).

