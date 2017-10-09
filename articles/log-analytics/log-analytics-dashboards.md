---
title: un panel personalizado en Azure Log Analytics aaaCreate | Documentos de Microsoft
description: "Esta guía le ayudará a comprender cómo los paneles de análisis de registros pueden mostrar todas las búsquedas de registros guardadas, lo que proporciona una sola lente tooview su entorno."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Creación de un panel personalizado para usarse en Log Analytics

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, no puede crear nuevos paneles o editar otros paneles. 

Esta guía le ayudará a comprender cómo los paneles de análisis de registros pueden mostrar todas las búsquedas de registros guardadas, lo que proporciona una sola lente tooview su entorno.

![Panel de ejemplo](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Todos los paneles personalizados Hola que cree en el portal de OMS hello también están disponibles en hello aplicación móvil de OMS. Vea Hola después de páginas para obtener más información acerca de las aplicaciones de Hola.

* [Aplicación móvil de OMS de hello Microsoft Store](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Aplicación móvil de OMS en Apple iTunes](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobile dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>¿Cómo creo mi panel?
toobegin, página de información general de OMS toohello vaya. Verá hello **Mi panel** icono de hello izquierda. Haga clic en él toodrill hacia abajo en el panel.

![Información general](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Adición de un mosaico
En los paneles, los mosaicos se generan a partir de las búsquedas de registros guardadas. OMS incluye muchas búsquedas de registros guardadas de creación previa, para que pueda empezar inmediatamente. Pasos siguientes de Hola de utilizar dicho esquema cómo toobegin.

Hola vista Mi panel, simplemente haga clic en **personalizar** tooenter en el modo personalizar.

![Gráfica](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 panel de Hola que se abre en el lado derecho de Hola de página de Hola muestran todas las búsquedas de registros guardadas del área de trabajo. toovisualize buscar un registro guardado como un icono, mantenga el mouse sobre una búsqueda guardada y, a continuación, haga clic en hello **más** símbolos.

![Agregar mosaicos 1](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Al hacer clic en hello **más** de símbolos, aparece un icono nuevo en hello vista Mi panel.

![Agregar mosaicos 2](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Editar un mosaico
Hola vista Mi panel, simplemente haga clic en **personalizar** tooenter en el modo personalizar. Haga clic en el icono de hello desea tooedit. el panel derecho Hola cambia tooedit y ofrece una selección de opciones:

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Editar mosaico](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Visualizaciones de mosaico
Hay tres tipos de toochoose de visualizaciones de mosaico desde:

| tipo de gráfico | qué hace |
| --- | --- |
| ![Gráfico de barras](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas como un gráfico de barras, o una lista de resultados por un campo en función de si la búsqueda de registros agrega los resultados por un campo o no. |
| ![métrica](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Muestra el número total de resultados de la búsqueda de registros como número en un icono. Mosaicos de métrica permiten tooset un umbral que hará resaltar el mosaico de hello cuando se alcanza el umbral de Hola. |
| ![line](./media/log-analytics-dashboards/oms-dashboards-line.png) |Muestra una escala de tiempo de los resultados de búsquedas de registros guardadas con los valores en forma de gráfico de líneas. |

### <a name="threshold"></a>Umbral
Puede crear un umbral en un mosaico mediante la visualización métrica Hola. Seleccione en toocreate un valor de umbral en el icono de Hola. Elija si mosaico de hello toohighlight al valor de hello está por encima o debajo del umbral de hello elegido, a continuación, establezca el valor por debajo del umbral de Hola.

## <a name="organizing-hello-dashboard"></a>Organización Hola panel
tooorganize el panel, navegue a vista de toohello Mi panel y haga clic en **personalizar** tooenter en el modo personalizar. Haga clic y arrastre el icono de Hola que desee toomove y muévalo toowhere desea que su toobe de mosaico.

![Organizar el panel](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Quitar un mosaico
tooremove un icono, navegue a vista de toohello Mi panel y haga clic en **personalizar** tooenter en el modo personalizar. Icono de hello SELECT que desee tooremove, y después en el panel derecho Hola seleccione **Quitar icono**.

![Quitar un mosaico](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Pasos siguientes
* Crear [alertas](log-analytics-alerts.md) en las notificaciones de toogenerate de análisis de registros y tooremediate problemas.
