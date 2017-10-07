---
title: "acción de consulta de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general de la acción de consulta de Hola para realizar acciones como matriz de filtro."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Introducción a la acción de consulta de Hola
Mediante la acción de consulta de hello, puede trabajar con lotes y matrices tooaccomplish los flujos de trabajo:

* Crear una tarea para todos los registros de alta prioridad desde una base de datos.
* Guardar todos los datos adjuntos en PDF de correos electrónicos en un blob de Azure.

tooget se hayan iniciado mediante la acción de consulta de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Use la acción de consulta de Hola
Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica. [Más información acerca de las acciones](connectors-overview.md).  

acción de consulta de Hello tiene actualmente una operación, denominada matriz de filtro de hello, que se expone en el Diseñador de Hola. Esto permite tooquery una matriz y devolver un conjunto de resultados filtrados.

Este es el procedimiento para agregarlo en una aplicación lógica:

1. Seleccione hello **nuevo paso** botón.
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de búsqueda de la acción de hello, escriba **filtro** hello toolist **matriz filtro** acción.
   
    ![Seleccione la acción de consulta de Hola](./media/connectors-native-query/using-action-1.png)
4. Seleccione un toofilter de matriz. (hello captura de pantalla siguiente muestra hello matriz de resultados de búsqueda de Twitter.)
5. Crear una condición tooevaluate en cada elemento. (Hola siguiente captura de pantalla de filtros de tweets de usuarios que tienen más de 100 seguidores).
   
    ![Acción de consulta de hello completa](./media/connectors-native-query/using-action-2.png)
   
    acción de Hello darán como resultado una nueva matriz que contiene solo los resultados que cumplen los requisitos de filtro de Hola.
6. Haga clic en la esquina superior izquierda de Hola de hello toosave de barra de herramientas y la lógica aplicación guardará ambos y publicar (activar).

## <a name="query-action"></a>Acción de consulta
A continuación encontrará los detalles de hello para la acción de hello admitido por este conector. Conector de Hello tiene una acción posible.

| Acción | Description |
| --- | --- |
| Filter array |Evalúa una condición para cada elemento de una matriz y devuelve los resultados de Hola |

## <a name="action-details"></a>Detalles de la acción
acción de consulta de Hello incluye una acción posible. Hello en las tablas siguientes se describen Hola necesarios y campos de entrada opcionales para acción de Hola y detalles salida correspondientes Hola que están asociados con el uso de la acción de Hola.

### <a name="filter-array"></a>Filter array
los siguientes Hola son campos de entrada para la acción de hello, que realiza una solicitud de salida HTTP.
Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| De* |De |Hola matriz toofilter |
| Condición* |donde |Hola tooevaluate de condición para cada elemento |

<br>

### <a name="output-details"></a>Detalles de salida
siguiente Hola es detalles de salida de respuesta HTTP Hola.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| Matriz filtrada |array |Una matriz que contiene un objeto de cada resultado filtrado |

## <a name="next-steps"></a>Pasos siguientes
Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md). Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).

