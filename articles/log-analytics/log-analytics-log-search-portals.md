---
title: "aaaPortals para crear y editar consultas de registros de análisis de registros de Azure | Documentos de Microsoft"
description: "Este artículo describen los portales de Hola que puede usar en Azure Log Analytics toocreate y editar búsquedas de registros."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Portales para la creación y edición de consultas de registros en Azure Log Analytics

> [!NOTE]
> Este artículo describe portales en análisis de registros de Azure mediante el lenguaje de consulta nueva Hola.  Puede obtener más información sobre el nuevo lenguaje de Hola y obtener Hola procedimiento tooupgrade el área de trabajo en [actualizar la búsqueda de registros de toonew de área de trabajo de análisis de registros de Azure](log-analytics-log-search-upgrade.md).  
>
> Si el área de trabajo no se ha actualizado toohello nuevo lenguaje de consulta, se debe hacer referencia demasiado[buscar datos mediante búsquedas de registros de análisis de registros](log-analytics-log-searches.md) para obtener información sobre la versión actual de Hola de portal de la búsqueda de registro de hello.

Usar búsquedas de registros en diversos lugares a lo largo de los datos de análisis de registros tooretrieve de área de trabajo de Hola.  Para crear y editar consultas de realmente además tooworking interactivamente con devuelve datos sin embargo, tiene dos opciones que se describen a continuación.  

## <a name="log-search-portal"></a>Portal de búsqueda de registros
portal de la búsqueda de registro de Hello es accesible desde Hola portal de Azure o el portal de OMS Hola.  Es adecuado para la creación de consultas básicas que se pueden crear en una sola línea.  portal de la búsqueda de registros de Hola se puede utilizar sin necesidad de iniciar un portal externo y se puede usar una variedad de funciones de tooperform con búsquedas de registros como crear reglas de alerta, crear grupos de equipos y exportación de resultados de Hola de consulta de Hola.  

portal de la búsqueda de registro de Hello proporciona varias características para Editar consulta Hola sin tener un conocimiento completo de lenguaje de consulta de Hola.  Puede obtener un resumen de estas características de [crear búsquedas de registros de análisis de registros de Azure mediante el portal de la búsqueda de registro de hello](log-analytics-log-search-log-search-portal.md).


![Portal de búsqueda de registros](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>Portal de análisis avanzado
portal de análisis avanzado de Hello es un portal dedicado que proporciona funcionalidad avanzada no está disponible en el portal de la búsqueda de registro de hello.  Características incluyen la capacidad de hello tooedit una consulta en varias líneas, selectivamente ejecutar código, Intellisense sensible al contexto y el análisis inteligente.  portal de análisis avanzado de Hello es más adecuado para diseñar las consultas más complejas que se guarda como una búsqueda de registros o copiarlo y pegar en otros elementos de análisis de registros.  Inicie el portal de análisis avanzado de Hola desde un vínculo en el portal de la búsqueda de registro de hello.

![Portal de análisis avanzado](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


Debido a sus características avanzadas, normalmente deberá usar portal de análisis avanzado de hello como la herramienta principal para crear y editar las consultas.  Una vez que haya determinado que consulta Hola funciona según lo previsto, a continuación, copie y péguelo en otra parte, como el portal de la búsqueda de registros de Hola o diseñador de vistas.  Dado Hola Advanced Analytics portal es compatible con las consultas con varias líneas no obstante, es necesario en cuenta el siguiente hello tootake al copiar una consulta desde este portal.

- Los comentarios deben quitarse de consulta de hello antes de que haya copiado y pegado en otra ubicación.  Puede hacer un comentario a una línea mediante la inclusión de dos barras diagonales (//) delante.  Si pega una consulta de varias líneas en una sola línea, se quitan los saltos de línea.  Si los comentarios se incluyen, todos los caracteres después de comentario del primer Hola se consideran parte del comentario de Hola.


## <a name="next-steps"></a>Pasos siguientes

- Ver un tutorial sobre el uso de hello [portal de la búsqueda de registro](log-analytics-log-search-log-search-portal.md) o hello [portal Advanced Analytics](https://go.microsoft.com/fwlink/?linkid=856587) toocreate consultas.
- Desproteger un [tutorial sobre cómo escribir consultas](https://go.microsoft.com/fwlink/?linkid=856078) utilizando Hola nuevo lenguaje de consulta.
