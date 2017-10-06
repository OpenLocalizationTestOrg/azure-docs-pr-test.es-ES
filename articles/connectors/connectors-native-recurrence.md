---
title: "desencadenador de periodicidad de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general de desencadenador de periodicidad de hello y cómo toouse con una aplicación de Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a>Empezar a trabajar con el desencadenador de periodicidad de Hola
Mediante el uso de desencadenador de periodicidad de hello, puede crear flujos de trabajo eficaces en la nube de Hola.

Por ejemplo, puede:

* Programar un toorun de flujo de trabajo un procedimiento almacenado SQL cada día.
* Enviar por correo electrónico un resumen de todos los tweets dentro de la última semana acerca de un determinado hashtag Hola.

tooget a usar el desencadenador de periodicidad de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-a-recurrence-trigger"></a>Uso de un desencadenador de periodicidad
Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica. [Más información sobre los desencadenadores](connectors-overview.md).

Este es un ejemplo de secuencia de cómo tooset una una periodicidad desencadenar en una aplicación de lógica:

1. Agregar hello **periodicidad** desencadenador como primer paso en una aplicación de la lógica de Hola.
2. Rellenar los parámetros de hello para el intervalo de periodicidad de saludo.

aplicación de la lógica de Hello ahora inicia una ejecución después de cada intervalo de tiempo.

![Desencadenador HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a>Detalles del desencadenador
desencadenador de periodicidad de Hello tiene Hola propiedades que puede configurar siguientes.

Active una aplicación lógica después de un intervalo de tiempo especificado.
Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Frecuencia* |frequency |unidad de Hola de tiempo: `Second`, `Minute`, `Hour`, `Day`, o `Year`. |
| Intervalo* |interval |intervalo de saludo de hello dada la frecuencia de repetición de Hola. |
| Zona horaria |timeZone |Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria. |
| Hora de inicio |startTime |hora de inicio de Hello en [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations). |

<br>

## <a name="next-steps"></a>Pasos siguientes
Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md). Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).

