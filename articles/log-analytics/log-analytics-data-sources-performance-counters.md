---
title: "aaaCollect y analizar los contadores de rendimiento de análisis de registros de Azure | Documentos de Microsoft"
description: "Contadores de rendimiento se recopilan del rendimiento de análisis de registros tooanalyze en los agentes de Windows y Linux.  Este artículo describe cómo tooconfigure recopilación del rendimiento de contadores a agentes de Windows y Linux, detalles de la se almacenan en el repositorio de OMS de Hola y cómo tooanalyze ellas en el portal de OMS Hola."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Orígenes de datos de rendimiento de Windows y Linux en Log Analytics
Contadores de rendimiento de Windows y Linux proporcionan una visión general de rendimiento de Hola de componentes de hardware, sistemas operativos y aplicaciones.  Análisis de registros pueden recopilar los contadores de rendimiento a intervalos frecuentes para el análisis casi en tiempo Real (NRT) suma tooaggregating los datos de rendimiento para análisis de término más e informes.

![Contadores de rendimiento](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Configuración de contadores de rendimiento
Configurar contadores de rendimiento en el portal de OMS Hola de hello [menú datos de configuración de análisis de registro](log-analytics-data-sources.md#configuring-data-sources).

Al configurar Windows o los contadores de rendimiento de Linux para una nueva área de trabajo OMS, se le ofrece Hola opción tooquickly crea varios contadores comunes.  Aparecen con una tooeach siguiente casilla de verificación.  Asegúrese de que todos los contadores que desea tooinitially crean se comprueban y, a continuación, haga clic en **agregar Hola seleccionado los contadores de rendimiento**.

Para los contadores de rendimiento de Windows, puede elegir una instancia específica para cada contador de rendimiento. Contadores de rendimiento de Linux, instancia de Hola de cada contador que elija aplica tooall contadores de secundarios de contador de hello primario. Hello tabla siguiente muestran instancias comunes Hola contadores de rendimiento de Linux y Windows tooboth disponible.

| Nombre de instancia | Descripción |
| --- | --- |
| \_Total |Total de todas las instancias de Hola |
| \* |Todas las instancias |
| (/&#124;/var) |Coincide con las instancias con nombre: / o /var |

### <a name="windows-performance-counters"></a>Contadores de rendimiento de Windows

![Configuración de contadores de rendimiento de Windows](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Siga este tooadd procedimiento un nuevo toocollect de contador de rendimiento de Windows.

1. Nombre del tipo hello del contador de hello en el cuadro de texto hello en formato de hello *\counter objeto (instancia)*.  Cuando empiece a escribir, aparece una lista de contadores comunes coincidentes.  Puede seleccionar un contador de hello lista o escriba en uno de sus propios.  También puede devolver todas las instancias de un contador determinado, para lo que debe especificar *objeto\contador*.  

    Al recopilar los contadores de rendimiento de SQL Server de instancias con nombre, todos con nombre comienzan de contadores de instancia por *MSSQL$* y seguido Hola nombre de instancia de Hola.  Por ejemplo, toocollect Hola frecuencia de aciertos de caché de registro de contador en todas las bases de datos de objeto de rendimiento de base de datos de Hola para SQL con nombre de instancia INST2, especifique `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Haga clic en  **+**  o presione **ENTRAR** lista toohello de tooadd Hola contadores.
3. Cuando se agrega un contador, utiliza Hola predeterminado de 10 segundos para su **intervalo de muestreo**.  Puede cambiar este valor más alto tooa de too1800 segundos (30 minutos) si desea que los requisitos de almacenamiento de tooreduce Hola de hello recopilan los datos de rendimiento.
4. Cuando haya terminado de agregar contadores, haga clic en hello **guardar** situado en la parte superior de Hola de configuración de hello pantalla toosave Hola.

### <a name="linux-performance-counters"></a>Contadores de rendimiento de Linux

![Configuración de contadores de rendimiento de Linux](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Siga este tooadd procedimiento un nuevo toocollect de contador de rendimiento de Linux.

1. De forma predeterminada, todos los cambios de configuración se insertan automáticamente agentes tooall.  Para los agentes de Linux, un archivo de configuración se envía el recopilador de datos de toohello Fluentd.  Si desea que este archivo manualmente en cada agente de Linux toomodify, a continuación, desactive la casilla de hello *aplicar la siguiente máquinas de Linux de configuración toomy* y seguir las instrucciones de Hola a continuación.
2. Nombre del tipo hello del contador de hello en el cuadro de texto hello en formato de hello *\counter objeto (instancia)*.  Cuando empiece a escribir, aparece una lista de contadores comunes coincidentes.  Puede seleccionar un contador de hello lista o escriba en uno de sus propios.  
3. Haga clic en  **+**  o presione **ENTRAR** lista de tooadd Hola contadores toohello de otros contadores para el objeto de Hola.
4. Hola a todos los contadores para un uso del objeto mismo **intervalo de muestreo**.  valor predeterminado de Hello es 10 segundos.  Cambie este valor más alto tooa de too1800 segundos (30 minutos) si desea que los requisitos de almacenamiento de tooreduce Hola de hello recopilan los datos de rendimiento.
5. Cuando haya terminado de agregar contadores, haga clic en hello **guardar** situado en la parte superior de Hola de configuración de hello pantalla toosave Hola.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Configuración de contadores de rendimiento de Linux en el archivo de configuración
En lugar de configurar los contadores de rendimiento de Linux mediante el portal de OMS hello, tiene opción de hello de la edición de archivos de configuración de agente de Linux Hola.  Toocollect de las métricas de rendimiento se controlan mediante la configuración de hello en **/etcetera/opt/microsoft/omsagent/\<Id. de área de trabajo\>/conf/omsagent.conf**.

Cada objeto o categoría de toocollect de las métricas de rendimiento debe definirse en el archivo de configuración de hello como una sola `<source>` elemento. sintaxis de Hello sigue siguiente patrón de Hola.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


parámetros de Hello en este elemento se describen en hello en la tabla siguiente.

| parameters | Descripción |
|:--|:--|
| object\_name | Nombre del objeto de colección de Hola. |
| instance\_regex |  A *expresión regular* definir qué toocollect de instancias. Hola valor: `.*` especifica todas las instancias. métricas de procesador toocollect para solo hello \_instancia Total, podría especificar `_Total`. métricas de procesador toocollect solo hello instancias crond o sshd, puede especificar: ' (crond\|sshd)`. |
| counter\_name\_regex | A *expresión regular* definir qué toocollect contadores (para el objeto de hello). toocollect todos los contadores para el objeto de hello, especifique: `.*`. toocollect solo intercambio contadores de espacio para el objeto de memoria de hello, por ejemplo, puede especificar:`.+Swap.+` |
| interval | Frecuencia con que Hola se recopilan los contadores del objeto. |


Hello tabla siguiente enumeran Hola objetos y contadores que puede especificar en el archivo de configuración de Hola.  Hay contadores adicionales disponibles para determinadas aplicaciones, como se describe en [Collect performance counters for Linux applications in Log Analytics](log-analytics-data-sources-linux-applications.md) (Recopilación de contadores de rendimiento para aplicaciones de Linux en Log Analytics).

| Nombre de objeto | Nombre del contador |
|:--|:--|
| Disco lógico | % de Inodes libres |
| Disco lógico | % de espacio libre |
| Disco lógico | % de Inodes usados |
| Disco lógico | % espacio usado |
| Disco lógico | Bytes de lectura de disco/s  |
| Disco lógico | Lecturas de disco/s  |
| Disco lógico | Transferencias de disco/s |
| Disco lógico |  Bytes de escritura en disco/s |
| Disco lógico | Escrituras en disco/s |
| Disco lógico | Megabytes libres |
| Disco lógico | Bytes de disco lógico/s |
| Memoria | % de memoria disponible |
| Memoria | % de espacio de intercambio disponible |
| Memoria | % de memoria usada |
| Memoria | % de espacio de intercambio usado |
| Memoria | MB de memoria disponibles |
| Memoria | Intercambio de MB disponibles |
| Memoria | Lecturas de página/s |
| Memoria | Escrituras de página/s |
| Memoria | Páginas/s |
| Memoria | Espacio de intercambio de MB usado |
| Memoria | MB de memoria usados |
| Red | Número total de bytes transmitidos |
| Red | Número total de bytes recibidos |
| Red | Número total de bytes |
| Red | Número total de paquetes transmitidos |
| Red | Número total de paquetes recibidos |
| Red | Errores de Rx totales |
| Red | Errores de Tx totales |
| Red | Colisiones totales |
| Disco físico | Prom. Segundos de disco/lecturas |
| Disco físico | Prom. Segundos de disco/transferencias |
| Disco físico | Prom. Segundos de disco/escrituras |
| Disco físico | Bytes de disco físico/s |
| Proceso | Porcentaje de tiempo con privilegios |
| Proceso | Porcentaje de tiempo de usuario |
| Proceso | Kilobytes de memoria usados |
| Proceso | Memoria compartida virtual |
| Procesador | % de tiempo de DPC |
| Procesador | % de tiempo de inactividad |
| Procesador | % de tiempo de interrupción |
| Procesador | % de tiempo de espera de E/S |
| Procesador | % de tiempo bueno |
| Procesador | % de tiempo con privilegios |
| Procesador | % de tiempo de procesador |
| Procesador | % de tiempo de usuario |
| Sistema | Memoria física libre |
| Sistema | Espacio libre en archivos de paginación |
| Sistema | Memoria virtual libre |
| Sistema | Procesos |
| Sistema | Tamaño almacenado en archivos de paginación |
| Sistema | Tiempo de actividad |
| Sistema | Usuarios |


Esta es la configuración de predeterminada de Hola para las métricas de rendimiento.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Colección de datos
Log Analytics recopila todos los contadores de rendimiento especificados en su intervalo de ejemplo en todos los agentes que tengan dicho contador instalado.  no se agregan los datos de Hola y los datos sin procesar de Hola están disponibles en todas las vistas de búsqueda de registro durante Hola especificado por su suscripción de OMS.

## <a name="performance-record-properties"></a>Propiedades de registros de rendimiento
Registros de rendimiento tienen un tipo de **rendimiento** y que tienen propiedades de hello en hello en la tabla siguiente.

| Propiedad | Descripción |
|:--- |:--- |
| Equipo |Equipo que Hola eventos se recopilaron de. |
| CounterName |Nombre del contador de rendimiento de Hola |
| CounterPath |Ruta de acceso completa del contador de hello en forma de hello \\ \\ \<equipo >\\objeto (instancia)\\contador. |
| CounterValue |Valor numérico del contador de Hola. |
| InstanceName |Nombre de instancia de evento Hola.  Vacío si no hay instancias. |
| ObjectName |Nombre del objeto de rendimiento de Hola |
| SourceSystem |Tipo de datos del agente Hola se recopilaron de. <br><br>OpsManager: agente de Windows, ya sea una conexión directa o SCOM <br> Linux: todos los agentes de Linux.  <br> AzureStorage: Diagnósticos de Azure |
| TimeGenerated |Se muestrean los datos de Hola de fecha y hora. |

## <a name="sizing-estimates"></a>Estimaciones de tamaño
 Una estimación aproximada para la recopilación de un contador determinado a intervalos de 10 segundos es de aproximadamente 1 MB por día y por instancia.  Puede calcular los requisitos de almacenamiento de Hola de un contador determinado con hello después de la fórmula.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Búsquedas de registros con registros de rendimiento
Hello tabla siguiente proporciona diferentes ejemplos de búsquedas de registros que recuperar registros de rendimiento.

| Consultar | Descripción |
|:--- |:--- |
| Type=Perf |Todos los datos de rendimiento |
| Type=Perf Computer="MyComputer" |Todos los datos de rendimiento de un equipo concreto |
| Type=Perf CounterName="Current Disk Queue Length" |Todos los datos de rendimiento de un contador concreto |
| Type=Perf (ObjectName=Processor) CounterName="% Processor Time" InstanceName=_Total &#124; measure Avg(Average) as AVGCPU  by Computer |Uso medio de CPU en todos los equipos |
| Type=Perf (CounterName="% Processor Time") &#124;  measure max(Max) by Computer |Uso máximo de CPU en todos los equipos |
| Type=Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" &#124; measure Avg(Average) by InstanceName |Promedio de longitud de cola de disco actual en todas las instancias de Hola de un equipo determinado |
| Type=Perf CounterName="DiskTransfers/sec" &#124; measure percentile95(Average) by Computer |Percentil 95 de transferencias de disco por segundo en todos los equipos |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  &#124; measure avg(CounterValue) by Computer Interval 1HOUR |Promedio por hora de uso de CPU en todos los equipos |
| Type=Perf Computer="MyComputer" CounterName=%* InstanceName=_Total &#124; measure percentile70(CounterValue) by CounterName Interval 1HOUR |Percentil 70 por hora de cada contador de porcentaje % para un equipo concreto |
| Type=Perf CounterName="% Processor Time" InstanceName="_Total"  (Computer="MyComputer") &#124; measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR |Promedio, mínimo, máximo y percentil 75 por hora de uso de CPU de un equipo específico |
| Type=Perf ObjectName="MSSQL$INST2:Databases" InstanceName=master | Todos los datos de rendimiento de rendimiento de la base de datos de hello objeto de base de datos maestra Hola Hola con el nombre de instancia de SQL Server INST2.  

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, Hola por encima de las consultas cambiaría toohello siguiente.

> | Consultar | Descripción |
|:--- |:--- |
| Perf |Todos los datos de rendimiento |
| Perf &#124; where Computer == "MyComputer" |Todos los datos de rendimiento de un equipo concreto |
| Perf &#124; where CounterName == "Current Disk Queue Length" |Todos los datos de rendimiento de un contador concreto |
| Perf &#124; where ObjectName == "Processor" and CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AVGCPU = avg(Average) by Computer |Uso medio de CPU en todos los equipos |
| Perf &#124; where CounterName == "% Processor Time" &#124; summarize AggregatedValue = max(Max) by Computer |Uso máximo de CPU en todos los equipos |
| Perf &#124; where ObjectName == "LogicalDisk" and CounterName == "Current Disk Queue Length" and Computer == "MyComputerName" &#124; summarize AggregatedValue = avg(Average) by InstanceName |Promedio de longitud de cola de disco actual en todas las instancias de Hola de un equipo determinado |
| Perf &#124; where CounterName == "DiskTransfers/sec" &#124; summarize AggregatedValue = percentile(Average, 95) by Computer |Percentil 95 de transferencias de disco por segundo en todos los equipos |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" &#124; summarize AggregatedValue = avg(CounterValue) by bin(TimeGenerated, 1h), Computer |Promedio por hora de uso de CPU en todos los equipos |
| Perf &#124; where Computer == "MyComputer" and CounterName startswith_cs "%" and InstanceName == "_Total" &#124; summarize AggregatedValue = percentile(CounterValue, 70) by bin(TimeGenerated, 1h), CounterName | Percentil 70 por hora de cada contador de porcentaje % para un equipo concreto |
| Perf &#124; where CounterName == "% Processor Time" and InstanceName == "_Total" and Computer == "MyComputer" &#124; summarize ["min(CounterValue)"] = min(CounterValue), ["avg(CounterValue)"] = avg(CounterValue), ["percentile75(CounterValue)"] = percentile(CounterValue, 75), ["max(CounterValue)"] = max(CounterValue) by bin(TimeGenerated, 1h), Computer |Promedio, mínimo, máximo y percentil 75 por hora de uso de CPU de un equipo específico |
| Perf &#124; where ObjectName == "MSSQL$INST2:Databases" and InstanceName == "master" | Todos los datos de rendimiento de rendimiento de la base de datos de hello objeto de base de datos maestra Hola Hola con el nombre de instancia de SQL Server INST2.  

## <a name="viewing-performance-data"></a>Visualización de datos de rendimiento
Cuando se ejecuta una búsqueda de registros de datos de rendimiento, Hola **lista** se muestra de forma predeterminada.  tooview Hola datos en forma gráfica, haga clic en **métricas**.  Para una vista gráfica detallada, haga clic en hello  **+**  siguiente contador tooa.  

![Vista Métricas contraída](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

tooaggregate los datos de rendimiento en una búsqueda de registros, vea [agregación de métricas de petición y la visualización de OMS](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Pasos siguientes
* [Recopilación de contadores de rendimiento desde aplicaciones de Linux](log-analytics-data-sources-linux-applications.md), lo que incluye MySQL y Apache HTTP Server.
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.  
* Exportar los datos recopilados demasiado[Power BI](log-analytics-powerbi.md) para análisis y visualizaciones adicionales.
