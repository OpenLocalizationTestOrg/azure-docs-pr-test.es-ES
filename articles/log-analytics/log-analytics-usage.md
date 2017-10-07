---
title: "uso de datos de aaaAnalyze en análisis de registros | Documentos de Microsoft"
description: "Usar el panel de uso de hello en análisis de registros tooview cuántos datos se enviaran a servicio de análisis de registros toohello y solucionar el motivo por el que se envían grandes cantidades de datos."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Análisis del uso de datos en Log Analytics
Análisis de registros incluyen información sobre la cantidad de Hola de datos recopilados, que los equipos envían datos de Hola y Hola distintos tipos de datos que se envían.  Hola de uso **uso de análisis de registro** cantidad de hello toosee de panel de datos envía toohello servicio de análisis de registros. panel de Hello muestra la cantidad de datos y la cantidad de datos se recopila por cada solución de los equipos envían.

## <a name="understand-hello-usage-dashboard"></a>Comprender el panel de uso de Hola
Hola **uso de análisis de registros** panel muestra hello siguiente información:

- Volumen de datos
    - Data volume over time (Volumen de datos con el tiempo), en función del ámbito temporal actual
    - Data volume by solution (Volumen de datos por solución)
    - Data not associated with a computer (Datos no asociados a un equipo)
- Equipos
    - Computers sending data (Equipos que envían datos)
    - Computers with no data in last 24 hours (Equipos sin datos en las últimas 24 horas)
- Offerings (Ofertas)
    - Insight and Analytics nodes (Nodos Insight y Analytics)
    - Automation and Control nodes (Nodos Automation y Control)
    - Security nodes (Nodos de seguridad)
- Rendimiento
    - Tiempo que tarda datos toocollect e índice
- Lista de consultas

![panel de uso](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork con datos de uso
1. Si aún no lo ha hecho, inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su suscripción de Azure.
2. En hello **concentrador** menú, haga clic en **más servicios** y en la lista de Hola de recursos, escriba **análisis de registros**. Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Log Analytics**.  
    ![Menú central de Azure](./media/log-analytics-usage/hub.png)
3. Hola **análisis de registros** panel muestra una lista de las áreas de trabajo. Seleccione un área de trabajo.
4. Hola *área de trabajo* panel, haga clic en **uso de análisis de registros**.
5. En hello **uso de análisis de registro** panel, haga clic en **tiempo: últimas 24 horas** intervalo de tiempo de toochange Hola.  
    ![Intervalo de tiempo](./media/log-analytics-usage/time.png)
6. Hojas de categoría de uso de Hola de vista que muestran las áreas que le interesa. Elija una hoja y, a continuación, haga clic en un elemento en él tooview más detalles en [búsqueda de registros](log-analytics-log-searches.md).  
    ![Hoja de uso de datos de ejemplo](./media/log-analytics-usage/blade.png)
7. En el panel de búsqueda de registros de hello, revise los resultados de Hola que se devuelven desde la búsqueda de Hola.  
    ![Búsqueda de registros de uso de ejemplo](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Creación de una alerta cuando la colección de datos es mayor de lo esperado
Esta sección se describe cómo toocreate una alerta si:
- El volumen de datos supera una cantidad especificada.
- Volumen de datos es tooexceed predicho una cantidad especificada.

Las [alertas](log-analytics-alerts-creating.md) de Log Analytics utilizan consultas de búsqueda. Hello consulta siguiente tiene un resultado cuando hay más de 100 GB de datos recopilados en hello últimas 24 horas:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Hello consulta siguiente utiliza una simple toopredict fórmulas cuando se enviarán más de 100 GB de datos en un día: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert en un volumen de datos diferentes, cambio Hola 100 Hola consulta toohello número de GB desee tooalert en.

Siga los pasos de hello descritos en [crear una regla de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) toobe una notificación cuando la recopilación de datos es mayor de lo esperado.

Al crear la alerta de hello para la primera consulta Hola--cuando hay más de 100 GB de datos en 24 horas, establezca el:
- **Nombre** demasiado*volumen de datos mayor que 100 GB en 24 horas*
- **Gravedad** demasiado*advertencia*
- **Consulta de búsqueda** demasiado`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Período de tiempo** demasiado*24 horas*.
- **Frecuencia de alerta** toobe una hora desde que los datos de uso de hello sólo se actualizan una vez por hora.
- **Generar alerta basada en** toobe *número de resultados*
- **Número de resultados** toobe *mayor que 0*

Siga los pasos de hello descritos en [agregar acciones tooalert reglas](log-analytics-alerts-actions.md) configurar una acción de correo electrónico, webhook o runbook de regla de alerta de Hola.

Al crear alerta de hello para la segunda consulta Hola--cuando se prevé que va a haber más de 100 GB de datos en 24 horas, establezca el:
- **Nombre** demasiado*toogreater de 100 GB de espera un volumen de datos en 24 horas*
- **Gravedad** demasiado*advertencia*
- **Consulta de búsqueda** demasiado`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Período de tiempo** demasiado*3 horas*.
- **Frecuencia de alerta** toobe una hora desde que los datos de uso de hello sólo se actualizan una vez por hora.
- **Generar alerta basada en** toobe *número de resultados*
- **Número de resultados** toobe *mayor que 0*

Cuando reciba una alerta, realice los pasos de Hola Hola después tootroubleshoot sección ¿por qué uso es mayor de lo esperado.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Solución del problema de un uso mayor de lo esperado
Hola uso panel le ayudará a tooidentify ¿por qué uso (y, por tanto, los costos) es mayor que esperaba.

Un mayor uso está provocado por una de estas causas o por ambas:
- Más datos de lo esperado que se envían tooLog análisis
- Nodos más de lo esperado enviar datos tooLog análisis

### <a name="check-if-there-is-more-data-than-expected"></a>Compruebe si hay más datos de lo esperado 
Hay dos secciones claves de la página de uso de Hola que ayudan a identificar cuál es la causa hello toobe mayoría de datos recopilado.

Hola *volumen de datos con el tiempo* gráfico muestra el volumen total de los datos enviados de Hola y equipos de hello enviar Hola mayoría de los datos. gráfico de Hello en la parte superior de hello permite toosee si aumenta el uso de la generalidad de los datos, permanece constante o decreciente. lista de Hola de equipos muestra los equipos de hello 10 enviar Hola mayoría de los datos.

Hola *volumen de datos por solución* gráfico muestra el volumen de Hola de datos que se envían con cada solución y soluciones de hello enviar Hola mayoría de los datos. gráfico de Hello en la parte superior de hello muestra volumen total de Hola de datos que se envían con cada solución con el tiempo. Esta información permite tooidentify si una solución está enviando más datos, acerca de la misma cantidad de datos, o menos datos con el tiempo de Hola. lista de Hola de soluciones muestra soluciones Hola 10 enviar Hola mayoría de los datos. 

Estos dos gráficos muestran todos los datos. Algunos datos son facturables, mientras que otros son gratis. toofocus únicamente con los datos es facturables, modifique la consulta de hello en tooinclude de página de búsqueda de hello `IsBillable=true`.  

![gráficos de volumen de datos](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Mire hello *volumen de datos con el tiempo* gráfico. soluciones de hello toosee y tipos de datos que va a enviar Hola mayoría de los datos para un equipo específico, haga clic en nombre de hello del equipo de Hola. Haga clic en nombre de hello del primer equipo de hello en lista de Hola.

En la siguiente captura de pantalla de Hola Hola *administración de registros / rendimiento* tipo de datos está enviando Hola mayoría de los datos para el equipo de Hola. 

![volumen de datos a un equipo](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

A continuación, vuelva atrás toohello *uso* panel y mire hello *volumen de datos por solución* gráfico. equipos de hello toosee enviar Hola mayoría de los datos para una solución, haga clic en nombre de Hola de solución de hello en lista de Hola. Haga clic en el nombre de Hola de primera solución de hello en lista de Hola. 

En la siguiente captura de pantalla de hello, se confirma que hello *acmetomcat* equipo esté enviando Hola mayoría de los datos para la solución de administración de registros de Hola.

![volumen de datos a una solución](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Si es necesario, realizar tooidentify grandes volúmenes dentro de un tipo de datos o solución de análisis adicionales. Entre las consultas de ejemplo se incluyen:

+ Solución **Security**
  - `Type=SecurityEvent | measure count() by EventID`
+ Solución **Log Management**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Tipo de datos **Perf**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Tipo de datos **Event**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Tipo de datos **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Tipo de datos de **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Usar hello siguiente pasos tooreduce Hola volumen de los registros recopilados:

| Origen del mayor volumen de datos | ¿Cómo tooreduce volumen de datos |
| -------------------------- | ------------------------- |
| Eventos de seguridad            | Seleccione los [eventos de seguridad común o mínima](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/). <br> Cambiar los eventos de toocollect solamente es necesario de directiva de auditoría de seguridad de Hola. En concreto, revise Hola necesidad toocollect eventos <br> - [auditar plataforma de filtrado](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [auditar registro](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [auditar sistema de archivos](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [auditar objeto de kernel](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [auditar manipulación de identificadores](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [auditar almacenamiento extraíble](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| contadores de rendimiento       | Cambie la [configuración de los contadores de rendimiento](log-analytics-data-sources-performance-counters.md) para: <br> -Reduzca la frecuencia de Hola de colección <br> - Reducir el número de contadores de rendimiento |
| Registros de eventos                 | Cambie la [configuración del registro de eventos](log-analytics-data-sources-windows-events.md) para: <br> -Reducir el número de Hola de registros de eventos recopilados <br> - Recopilar solo los niveles de eventos necesarios Por ejemplo, no recopile eventos de nivel de *información*. |
| syslog                     | Cambie la [configuración de syslog](log-analytics-data-sources-syslog.md) para: <br> -Reducir el número de hello de servicios recopilada <br> - Recopilar solo los niveles de eventos necesarios Por ejemplo, no recopile eventos de nivel de *información* y *depuración*. |
| AzureDiagnostics           | Cambie la colección de registros de recursos para: <br> -Reducir el número de Hola de recursos envío registros tooLog análisis <br> - Recopilar solo los registros necesarios |
| Datos de la solución de los equipos que no tienen solución Hola | Use [solución destinatarios](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect datos de solo requiere grupos de equipos. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Comprobar si hay más nodos de lo esperado
Si se encuentra en hello *por nodo (OMS)* tarifa, a continuación, se le cobra según el número de Hola de nodos y las soluciones que se usa. Puede ver cuántos nodos de cada oferta que se usan en hello *ofertas* sección del panel de uso de Hola.

![panel de uso](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Haga clic en **ver todos...**  lista completa de hello tooview de equipos que envían datos de oferta de hello seleccionada.

Use [solución destinatarios](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect datos de solo requiere grupos de equipos.


## <a name="next-steps"></a>Pasos siguientes
* Vea [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) toolearn cómo toouse Hola buscar idioma. Puede usar análisis adicionales de tooperform de las consultas de búsqueda de datos de uso de Hola.
* Siga los pasos de hello descritos en [crear una regla de alerta](log-analytics-alerts-creating.md#create-an-alert-rule) se cumple toobe una notificación cuando un criterio de búsqueda
* Use [solución destinatarios](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect datos de solo requiere grupos de equipos
* Seleccione los [eventos de seguridad común o mínima](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/).
* Cambie la [configuración de los contadores de rendimiento](log-analytics-data-sources-performance-counters.md).
* Cambie la [configuración del registro de eventos](log-analytics-data-sources-windows-events.md).
* Cambie la [configuración de syslog](log-analytics-data-sources-syslog.md).
