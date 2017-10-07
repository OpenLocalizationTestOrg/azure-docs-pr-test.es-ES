---
title: "tooPower de datos de análisis de registros de aaaExport BI | Documentos de Microsoft"
description: "Power BI es un servicio de análisis empresarial basado en la nube de Microsoft que proporciona unos excelentes informes y visualizaciones para el análisis de los distintos conjuntos de datos.  Análisis de registros pueden exportar continuamente datos desde el repositorio de OMS de hello en Power BI lo que permite aprovechar sus visualizaciones y herramientas de análisis.  Este artículo describe cómo tooconfigure las consultas de análisis de registros que exportan tooPower BI automáticamente a intervalos regulares."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Exportar datos de análisis de registros tooPower BI

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, este proceso de exportación de datos de análisis de registros tooPower BI dejará de funcionar.  Se deshabilitarán las programaciones existentes creadas antes de actualizar. 
>
> Después de la actualización, usa Azure Log Analytics Hola misma plataforma que Application Insights y usar Hola mismo proceso tooPower de consultas de análisis de registros tooexport BI como [Hola proceso tooexport Application Insights consulta tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  O bien puede exportar consulta hello mediante la consola de análisis de hello tal y como se describe en ese artículo, o puede seleccionar hello **Power BI** situado en la parte superior de Hola de pantalla de bienvenida en el portal de la búsqueda de registro de hello.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) es un servicio de análisis empresarial basado en la nube de Microsoft que proporciona unos excelentes informes y visualizaciones para el análisis de los distintos conjuntos de datos.  Análisis de registros pueden exportar automáticamente datos de repositorio de OMS de hello en Power BI lo que permite aprovechar sus visualizaciones y herramientas de análisis.

Al configurar Power BI con análisis de registros, puede crear consultas de registro que exportan sus conjuntos de datos de resultados toocorresponding en Power BI.  exportación y consulta de hello continúa tooautomatically ejecutar según una programación que definen el conjunto de datos de tookeep Hola seguridad toodate con datos más recientes de hello recopilados por el análisis de registro.

![Análisis de registro tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Programaciones de Power BI
A *Power BI programación* incluye una búsqueda de registros que exporta un conjunto de datos de hello OMS repositorio tooa correspondiente conjunto de datos en Power BI y una programación que define la frecuencia con esta búsqueda se ejecuta el conjunto de datos de Hola a tookeep actual.

campos de Hello en el conjunto de datos de hello coincidirá con propiedades de Hola de registros de hello devueltos por la búsqueda de registros de Hola.  Si búsqueda Hola devuelve registros de diferentes tipos, a continuación, el conjunto de datos de hello incluirá todas propiedades Hola de cada uno de hello incluyen tipos de registro.  

> [!NOTE]
> Es un toouse de práctica recomendada una consulta de búsqueda de registros que devuelve los datos sin procesar como tooperforming lugar cualquier consolidación mediante comandos como [medida](log-analytics-search-reference.md#measure).  Puede realizar los cálculos y agregación en Power BI de los datos sin procesar de Hola.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>Conexión tooPower de área de trabajo OMS BI
Antes de poder exportar de análisis de registros tooPower BI, debe conectar su cuenta de Power BI tooyour de área de trabajo OMS mediante Hola siguiendo el procedimiento.  

1. En la consola de OMS hello, haga clic en hello **configuración** icono.
2. Seleccione **Cuentas**.
3. Hola **información del área de trabajo** sección, haga clic **conectar tooPower cuenta BI**.
4. Escriba las credenciales de Hola de su cuenta de Power BI.

## <a name="create-a-power-bi-schedule"></a>Creación de una programación de Power BI
Crear una programación de Power BI para cada conjunto de datos mediante Hola siguiendo el procedimiento.

1. En la consola de OMS hello, haga clic en hello **Log Search** icono.
2. Escriba en una consulta nueva o seleccione una búsqueda guardada que devuelve Hola datos que desea tooexport demasiado**Power BI**.  
3. Haga clic en hello **Power BI** situado en la parte superior de Hola de Hola Hola de tooopen página **Power BI** cuadro de diálogo.
4. Proporcionar información de hello en hello siguiente de la tabla y haga clic en **guardar**.

| Propiedad | Descripción |
|:--- |:--- |
| Nombre |Nombre tooidentify Hola programar ver lista de Hola de programaciones de Power BI. |
| Búsqueda guardada |Hola toorun de búsqueda de registro.  Puede seleccionar la consulta actual de Hola o seleccione una búsqueda guardada existente en el cuadro de lista desplegable de Hola. |
| Schedule |¿Con qué frecuencia hello toorun Guardar búsqueda y exportación de conjunto de datos de toohello Power BI.  Hola valor debe ser entre 15 minutos y 24 horas. |
| Nombre del conjunto de datos |nombre de Hello del conjunto de datos de hello en Power BI.  Se creará si no existe y se actualizará si ya existe. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Visualización y eliminación de programaciones de Power BI
Ver la lista de Hola de programaciones de BI de energía existentes con hello siguiendo el procedimiento.

1. En la consola de OMS hello, haga clic en hello **configuración** icono.
2. Seleccione **Power BI**.

Además programación toohello detalles de hello, número de Hola de veces que Hola programación se ha ejecutado en hello semana pasada y se muestran el estado de Hola de hello última sincronización.  Si la sincronización de hello errores, puede hacer clic en hello vínculo toorun una búsqueda de registro de registros con los detalles de error de Hola.

Puede quitar una programación, haga clic en hello **X** en hello **Quitar columna**.  Puede deshabilitar una programación seleccionando **Desactivar**.  toomodify una programación debe quitarlo y volver a crearla con la nueva configuración de Hola.

![Programaciones de Power BI](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Tutorial de ejemplo
Hello siguiente sección le guía a través de un ejemplo de creación de una programación de Power BI y usando su conjunto de datos toocreate un informe sencillo.  En este ejemplo, todos los datos de rendimiento para un conjunto de equipos son exportado tooPower BI y, a continuación, un gráfico de líneas se crea toodisplay utilización del procesador.

### <a name="create-log-search"></a>Creación de la búsqueda de registros
Comenzamos creando una búsqueda de registros de datos de Hola que queremos que el conjunto de datos de toosend toohello.  En este ejemplo, utilizaremos una consulta que devuelve todos los datos de rendimiento de los equipos cuyo nombre empieza por *srv*.  

![Programaciones de Power BI](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Creación de una búsqueda de Power BI
Hacemos clic en hello **Power BI** botón cuadro de diálogo de tooopen Hola Power BI y proporcionar información de hello necesario.  Se desea este toorun búsqueda una vez por hora y crear un conjunto de datos denominado *Contoso Perf*.  Puesto que ya se ha abierto de búsqueda de Hola que crea datos de Hola que deseamos, mantenemos predeterminado Hola de *usar consulta de búsqueda actual* para **búsqueda guardada**.

![Búsqueda de Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Comprobación de una búsqueda de Power BI
tooverify que creamos programación Hola correctamente, se ver lista de Hola de Power BI búsquedas en hello **configuración** el icono Panel de OMS Hola.  Se espere unos minutos y esta vista se actualiza hasta que informa de que se ha ejecutado la sincronización de Hola.

![Búsqueda de Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Compruebe el conjunto de datos de hello en Power BI
Se registran en la cuenta en [powerbi.microsoft.com](http://powerbi.microsoft.com/) y desplácese demasiado**conjuntos de datos** final Hola del panel izquierdo de Hola.  Podemos ver que hello *Contoso Perf* conjunto de datos se muestra que indica que la exportación se ha ejecutado correctamente.

![Conjunto de datos de Power BI](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Creación de un informe basado en el conjunto de datos
Seleccionamos hello **Contoso Perf** conjunto de datos y, a continuación, haga clic en **resultados** en hello **campos** panel campos Hola de hello tooview derecho que forman parte de este conjunto de datos.  toocreate una utilización del procesador de línea gráfico que se muestra para cada equipo, llevamos a cabo Hola siguientes acciones.

1. Seleccione la visualización del gráfico de línea de saludo.
2. Arrastre **ObjectName** demasiado**filtro de nivel de informe** y compruebe **procesador**.
3. Arrastre **CounterName** demasiado**filtro de nivel de informe** y compruebe **% Processor Time**.
4. Arrastre **CounterValue** demasiado**valores**.
5. Arrastre **equipo** demasiado**leyenda**.
6. Arrastre **TimeGenerated** demasiado**eje**.

Podemos ver que ese gráfico de líneas Hola resultante se muestra con datos Hola nuestro conjunto de datos.

![Gráfico de líneas de Power BI](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Guardar informe de Hola
Se guarde el informe de hello haciendo clic en hello guarda situado en la parte superior de Hola de pantalla de bienvenida y validar que ahora aparece en la sección de informes de hello en el panel izquierdo de Hola.

![Informes de Power BI](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) toobuild consultas que se pueden exportan tooPower BI.
* Obtenga más información sobre [Power BI](http://powerbi.microsoft.com) toobuild visualizaciones en función de las exportaciones de análisis de registros.
