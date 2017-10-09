---
title: "aaaCreate vistas tooanalyze datos de análisis de registros de OMS | Documentos de Microsoft"
description: "Diseñador de vistas de análisis de registros permite toocreate personalizado vistas que se muestran en el portal OMS y Azure hello y contienen diferentes visualizaciones de datos en el repositorio OMS Hola. En este artículo encontrará información general del Diseñador de vistas, y procedimientos para crear y editar vistas personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Usar vistas personalizadas de toocreate de diseñador de vistas de análisis de registros
Hola Diseñador de vistas en [análisis de registros](log-analytics-overview.md) permite toocreate vistas personalizadas en la consola de OMS de Hola que contienen diferentes visualizaciones de datos en el repositorio OMS Hola. En este artículo encontrará información general del Diseñador de vistas, y procedimientos para crear y editar vistas personalizadas.

Estos son otros de los artículos disponibles sobre el Diseñador de vistas:

* [Icono referencia](log-analytics-view-designer-tiles.md) -referencia de configuración de Hola para cada uno de hello iconos toouse disponible en sus vistas personalizadas.
* [Referencia de elemento de visualización](log-analytics-view-designer-parts.md) -referencia de configuración de Hola para cada uno de hello iconos toouse disponible en sus vistas personalizadas.

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, se deben escribir consultas en todas las vistas en hello [nuevo lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas las vistas que se crearon antes de que se actualizó el área de trabajo de hello será automáticamente convertido.

## <a name="concepts"></a>Conceptos
Vistas creadas con el Diseñador de vistas de hello contienen elementos de hello en hello en la tabla siguiente.

| Elemento | Descripción |
|:--- |:--- |
| Icono |Se muestra en el panel de información general de análisis de registro principal Hola.  Incluye un resumen visual de información de hello contenida en hello vista personalizada.  Los distintos tipos de mosaico proporcionan diferentes visualizaciones de registros en el repositorio OMS Hola.  Haga clic en Hola Hola de tooopen icono vista personalizada. |
| Vista personalizada |Aparece cuando Hola usuario hace clic en el icono de Hola.  Contiene uno o varios elementos de visualización. |
| Elementos de visualización |Visualización de datos en el repositorio OMS de hello en función de uno o varios [búsquedas de registro](log-analytics-log-searches.md).  Mayoría de las partes incluye un encabezado que proporciona una visualización de alto nivel y una lista de resultados principales de Hola.  Tipos de diferentes partes proporcionan diferentes visualizaciones de registros en el repositorio OMS Hola.  Haga clic en elementos de hello parte tooperform una búsqueda de registros proporciona un registro detallado. |

![Información general del Diseñador de vistas](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Agregar área de trabajo de diseñador de vistas tooyour
Mientras está en el Diseñador de vistas en la vista previa, debe agregarse el área de trabajo de tooyour seleccionando **características de vista previa** en hello **configuración** sección del portal de OMS Hola.

![Habilitación de la versión preliminar](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Creación y edición de vistas
### <a name="create-a-new-view"></a>Creación de vistas
Abra una nueva vista en hello **Diseñador de vistas** haciendo clic en el Diseñador de vistas de hello disponer en mosaico en el panel principal de OMS de Hola.

![Icono del Diseñador de vistas](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Edición vistas existentes
tooedit una vista existente en el Diseñador de vistas, Hola Abrir vista haciendo clic en su icono en el panel principal de OMS de Hola Hola.  A continuación, haga clic en hello **editar** botón tooopen Hola vista Hola Diseñador de vistas.

![Edición de un icono](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Clonación de vistas existentes
Cuando se clona una vista, crea una nueva vista y lo abre en el Diseñador de vistas de Hola.  nueva vista de Hello tendrá Hola mismo nombre como Hola original con el final de toohello anexado "Copiar" de la misma.  tooclone una vista, abra Hola vista existente, haga clic en su icono en el panel principal de OMS de Hola.  A continuación, haga clic en hello **clon** botón tooopen Hola vista Hola Diseñador de vistas.

![Clonación de una vista](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Eliminación de vistas existentes
toodelete una vista existente, Hola Abrir vista haciendo clic en su icono en el panel principal de OMS de Hola.  A continuación, haga clic en hello **editar** tooopen Hola vista Hola Diseñador de vistas y haga clic en **Eliminar vista**.

![Eliminación de una vista](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Exportación de vistas existentes
Puede exportar un archivo JSON de tooa de vista que se puede importar a otra área de trabajo o usar en un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport una vista existente, Hola Abrir vista haciendo clic en su icono en el panel principal de OMS de Hola.  A continuación, haga clic en hello **exportar** botón toocreate un archivo en la carpeta de descarga del explorador de Hola.  nombre de Hello del archivo hello será el nombre de Hola de hello vista con la extensión de hello *omsview*.

![Exportación de una vista](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importación de vistas existentes
Puede importar un archivo *omsview* que haya exportado desde otro grupo de administración.  tooimport una vista existente, primero cree una nueva vista.  A continuación, haga clic en hello **importación** botón y seleccione hello *omsview* archivo.  configuración de Hello en el archivo hello se copiarán en la vista existente de Hola.

![Exportación de una vista](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Uso del Diseñador de vistas
Hola Diseñador de vistas tiene tres paneles.  Hola **diseño** panel representa la vista personalizada de Hola.  Al agregar iconos y elementos de hello **Control** panel toohello **diseño** panel son agrega vista toohello.  Hola **propiedades** panel mostrará las propiedades de hello para el icono de Hola o una parte seleccionada.

![Ver diseñador](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Configuración de iconos de vistas
Una vista personalizada solo puede tener un único icono.  Seleccione hello **icono** ficha hello **Control** panel tooview Hola actual icono o seleccione uno alternativo.  Hola **propiedades** panel mostrará las propiedades de Hola para mosaico actual Hola.  Configurar las propiedades del icono de hello según toohello información detallada en hello [icono referencia](log-analytics-view-designer-tiles.md) y haga clic en **aplicar** toosave cambios.

### <a name="configure-visualization-parts"></a>Configuración de elementos de visualización
Una vista puede incluir cualquier número de elementos de visualización.  Seleccione hello **vista** tooadd toohello vista de elemento de ficha y, a continuación, en una visualización.  Hola **propiedades** panel mostrará las propiedades de Hola de parte de hello seleccionado.  Configurar vista Hola propiedades según toohello información detallan en hello [referencia de elemento de visualización](log-analytics-view-designer-parts.md) y haga clic en **aplicar** toosave cambios.

### <a name="delete-a-visualization-part"></a>Eliminación de elementos de visualización
Puede quitar un elemento de visualización de hello vista haciendo clic en hello **X** botón de Hola la esquina superior derecha de la parte de Hola.

### <a name="rearrange-visualization-parts"></a>Reorganización de elementos de visualización
Las vistas solo tienen una fila de elementos de visualización.  Reorganizar los elementos existentes en una vista haciendo clic en ellos y arrastrándolos tooa nueva ubicación.

## <a name="next-steps"></a>Pasos siguientes
* Agregar [iconos](log-analytics-view-designer-tiles.md) tooyour de vista personalizada.
* Agregar [elementos de visualización](log-analytics-view-designer-parts.md) tooyour de vista personalizada.
