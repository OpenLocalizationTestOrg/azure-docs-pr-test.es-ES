---
title: aaaHow toomonitor un servicio en la nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor servicios en la nube mediante el uso de hello portal de Azure clásico."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>Cómo tooMonitor los servicios de nube
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

Puede supervisar `key` métricas de rendimiento de los servicios de nube en hello portal de Azure clásico. Puede establecer Hola nivel de supervisión toominimal y detallado para cada rol de servicio y puede personalizar Hola pantallas de supervisión. Los datos de supervisión detallada se almacenan en una cuenta de almacenamiento, que puede tener acceso fuera de hello portal. 

Pantallas de supervisión en el portal de Azure clásico Hola son altamente configurables. Puede elegir las métricas de hello desea toomonitor en la lista de métricas de hello en hello **Monitor** página y puede elegir qué tooplot métricas en gráficos de métricas en hello **Monitor** hello y página de panel. 

## <a name="concepts"></a>Conceptos
De forma predeterminada, la supervisión mínima se proporciona para un nuevo servicio de nube mediante contadores de rendimiento recopilado desde el sistema operativo del host Hola para instancias de roles de hello (máquinas virtuales). las métricas mínimas de Hello son limitado tooCPU porcentaje, datos de entrada, datos de salida, el rendimiento de lectura de disco y velocidad de escritura en disco. Mediante la configuración de supervisión detallada, puede recibir métricas adicionales basadas en datos de rendimiento dentro de máquinas virtuales de hello (instancias de rol). las métricas detalladas de Hello permiten un análisis más preciso de los problemas que se producen durante las operaciones de aplicación.

De forma predeterminada los datos de contador de rendimiento de instancias de rol se muestrean y transfieren de la instancia de rol de hello en intervalos de 3 minutos. Cuando se habilita la supervisión detallada, datos del contador de rendimiento sin procesar de Hola se agregan para cada instancia de rol y en todas las instancias de rol para cada rol a intervalos de 5 minutos, 1 hora y 12 horas. Hola se purgan los datos agregados después de 10 días.

Después de habilitar la supervisión detallada, Hola agregan datos de supervisión se almacenan en tablas en la cuenta de almacenamiento. tooenable detallado de supervisión para un rol, debe configurar una cadena de conexión de diagnóstico que se vincula toohello cuenta de almacenamiento. Puede utilizar cuentas de almacenamiento diferentes para roles diferentes.

Habilitar aumenta supervisión detallado relacionados con los costos de almacenamiento toodata almacenamiento, transferencia de datos y transacciones de almacenamiento. La supervisión mínima no requiere una cuenta de almacenamiento. datos de Hola para las métricas de Hola que se exponen en el nivel de supervisión mínima Hola no se almacenan en la cuenta de almacenamiento, incluso si configura hello tooverbose nivel de supervisión.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Configuración de la supervisión para los servicios en la nube
Usar hello siguiendo los procedimientos tooconfigure detallada o mínima de supervisión en hello portal de Azure clásico. 

### <a name="before-you-begin"></a>Antes de empezar
* Crear un *clásico* Hola de toostore de cuenta de almacenamiento los datos de supervisión. Puede utilizar cuentas de almacenamiento diferentes para roles diferentes. Para obtener más información, consulte [cómo toocreate una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Active Diagnósticos de Azure en sus roles de servicios en la nube. Consulte [Configuración de Diagnósticos para servicios en la nube](cloud-services-dotnet-diagnostics.md).

Asegúrese de que está presente en la configuración de rol de hello cadena de conexión de diagnósticos de Hola. No se puede activar la supervisión detallada hasta que habilitar los diagnósticos de Azure e incluye una cadena de conexión de diagnóstico en la configuración de rol de Hola.   

> [!NOTE]
> Proyectos destinados a Azure SDK 2.5 no incluía automáticamente cadena de conexión de diagnósticos de hello en la plantilla de proyecto de Hola. Para estos proyectos, deberá toomanually Agregar configuración de rol de la conexión cadena Hola diagnósticos toohello.
> 
> 

**toomanually Agregar configuración de tooRole de cadena de conexión de diagnóstico**

1. Proyecto de servicio de nube de hello abierta en Visual Studio
2. Haga doble clic en hello **rol** tooopen Hola Diseñador de roles y seleccione hello **configuración** ficha
3. Busque un ajuste llamado **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Si esta opción no está presente, haga clic en hello **Agregar configuración** tooadd de botón, cambios y configuración de toohello Hola tipo para hello nuevo valor demasiado**ConnectionString**
5. Establezca el valor de Hola para saludo de la cadena de conexión haciendo clic en hello **...**  botón. Se abrirá un cuadro de diálogo que permite tooselect una cuenta de almacenamiento.
   
    ![Configuración de Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>Hola toochange tooverbose nivel de supervisión o mínima
1. Hola [portal de Azure clásico](https://manage.windowsazure.com/), abra hello **configurar** página de implementación del servicio de nube de Hola.
2. En **Nivel**, haga clic en **Detallado** o **Mínimo**. 
3. Haga clic en **Guardar**.

Una vez activada la supervisión detallada, debe comenzar a ver Hola datos supervisados en portal de Azure clásico de Hola durante la hora de Hola.

datos del contador de rendimiento sin procesar de Hola y datos de supervisión agregados se almacenan en la cuenta de almacenamiento de hello en tablas calificada por Id. de implementación de Hola para roles de Hola. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Recepción de alertas de métricas de servicios en la nube
Puede recibir alertas basadas en las métricas de supervisión de los servicios en la nube. En hello **Management Services** Hola de página del portal de Azure clásico, es posible crear una regla tootrigger una alerta cuando la métrica de Hola que elija alcance un valor que especifique. También puede elegir toohave enviada correo electrónico cuando se desencadene la alerta de Hola. Para obtener más información, consulte [Recepción notificaciones de alerta y administración de reglas de alerta en Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Cómo: agregar la tabla de métricas de métricas toohello
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), abra hello **Monitor** página de servicio en la nube Hola.
   
    De forma predeterminada, la tabla de métricas de Hola muestra un subconjunto de métricas disponibles Hola. ilustración de Hello muestra métricas detallado de hello predeterminado para un servicio de nube, que es el contador de rendimiento de Memoria\mbytes disponibles toohello limitada, con datos agregados en nivel de rol de Hola. Use **agregar métricas** tooselect adicionales agregado y las métricas de nivel de rol toomonitor en Hola portal de Azure clásico.
   
    ![Visualización detallada](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tabla de métricas de tooadd métricas toohello:
   
   1. Haga clic en **agregar métricas** tooopen **elegir métricas**, como se muestra a continuación.
      
       métrica disponibles primera Hello es tooshow expandido opciones que están disponibles. Para cada métrica, opción de hello superior muestra los datos de supervisión agregados para todos los roles. Además, puede elegir toodisplay datos para los roles individuales.
      
       ![Agregar métricas](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect métricas toodisplay
      
      * Haga clic en hello flecha abajo por Hola tooexpand métrica Hola opciones de supervisión.
      * Hola seleccione casilla de verificación para cada opción que desee toodisplay de supervisión.
        
        Pueden mostrar hasta las métricas de too50 en la tabla de métricas de Hola.
        
        > [!TIP]
        > En la supervisión detallada, lista de métricas de hello puede contener docenas de métricas. toodisplay una barra de desplazamiento, mantenga el mouse sobre el lado derecho de Hola Hola del cuadro de diálogo. lista de hello toofilter, haga clic en el icono de búsqueda de Hola y escribir texto en el cuadro de búsqueda de hello, tal y como se muestra a continuación.
        > 
        > 
        
        ![Búsqueda de Agregar métricas](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Después de haber seleccionado las métricas, haga clic en la marca de verificación.
   
    Hello las métricas seleccionadas se agregan toohello tabla de métricas, tal y como se muestra a continuación.
   
    ![supervisar métricas](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete una métrica de la tabla de métricas de hello, haga clic en tooselect de métrica de hello y, a continuación, haga clic en **eliminar métrica**. ( **Eliminar métrica** solo se verá si se ha seleccionado una métrica).

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tabla de métricas de tooadd métricas personalizadas toohello
Hola **detallado** nivel de supervisión proporciona una lista de las métricas de predeterminada que se pueden supervisar en el portal de Hola. Además toothese puede supervisar los contadores de rendimiento definidos por la aplicación a través del portal de Hola o de métricas personalizadas.

Hello siguientes pasos se supone que ha activado **detallado** nivel de supervisión y ha configurado los contadores de rendimiento personalizados de toocollect y transferencia de aplicación. 

contadores de rendimiento personalizados de hello toodisplay en Hola portal necesita una configuración hello tooupdate en wad-control-container:

1. Abra el blob wad-control-container de hello en la cuenta de almacenamiento de diagnósticos. Puede usar Visual Studio o cualquier otro toodo del explorador de almacenamiento esto.
   
    ![Explorador de servidores de Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Navegar por ruta de acceso de blob de hello usando el patrón de hello **DeploymentId/RoleName/RoleInstance** toofind configuración de hello para la instancia de rol. 
   
    ![Explorador de almacenamiento de Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Descargar el archivo de configuración de hello para la instancia de rol y actualizar tooinclude todos los contadores de rendimiento personalizados. Por ejemplo toomonitor *Bytes de escritura de disco/s* para hello *unidad C* agregue Hola siguiente bajo **PerformanceCounters\Subscriptions** nodo
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Guardar cambios de Hola y toohello atrás del archivo de configuración Hola carga misma ubicación sobrescribir Hola archivo existente en el blob de Hola.
5. Pasar al modo de tooVerbose Hola configuración del portal de Azure clásico. Si ya estaban en el modo detallado tendrá tootoggle tooverbose de toominimal y viceversa.
6. contador de rendimiento personalizado de Hello ahora estará disponible en hello **agregar métricas** cuadro de diálogo. 

## <a name="how-to-customize-hello-metrics-chart"></a>Cómo: personalizar el gráfico de métricas de Hola
1. En la tabla de métricas de hello, seleccione too6 tooplot de métricas en el gráfico de métricas de Hola. tooselect una métrica, haga clic en la casilla de hello en su lado izquierdo. tooremove una métrica del gráfico de métricas de hello, desactive la casilla correspondiente en la tabla de métricas de Hola.
   
    Al seleccionar las métricas en la tabla de métricas de hello, las métricas de Hola se agregan toohello gráfico de métricas. En una pantalla estrecha, un **n más** lista desplegable contiene los encabezados de métricas que no caben mostrar hello.
2. tooswitch entre mostrar valores absolutos (el eje Y muestra) y los valores relativos (valor final solo para cada métrica) seleccione relativa o absoluta en parte superior de hello del gráfico de Hola.
   
    ![Relative o Absolute](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. gráfico de métricas de toochange Hola tiempo intervalo hello muestra, seleccionar 1 hora, 24 horas o 7 días a la parte superior de hello del gráfico de Hola.
   
    ![Periodo de la pantalla de supervisión](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    En el gráfico de métricas de panel de hello, método de hello para las métricas de trazado es diferente. Un conjunto de métricas estándar está disponible, y las métricas se agregan o quitan seleccionando encabezado métrica Hola.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>gráfico de métricas de toocustomize hello en el panel de Hola
1. Abra Panel de Hola Hola servicio de nube.
2. Agregar o quitar métricas del gráfico de hello:
   
   * tooplot una casilla de verificación Hola métrica, seleccione Nuevo para la métrica de hello en los encabezados del gráfico Hola. ¿En una pantalla estrecha, haga clic en hello abajo por  ***n* ? las métricas** tooplot no se puede mostrar un área de encabezado del gráfico de métricas Hola.
   * toodelete una métrica que se traza en el gráfico de hello, Hola desactive casilla en su encabezado.
   
3. Alterne entre las pantallas **Relativo** y **Absoluto**.
4. Elija una hora, 24 horas o 7 días a partir de datos toodisplay.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Cómo: obtener acceso a los datos de supervisión detallada fuera Hola portal de Azure clásico
Los datos de supervisión detallada se almacenan en tablas en las cuentas de almacenamiento de Hola que especifique para cada rol. Para cada implementación del servicio en la nube, seis tablas se crean para el rol de Hola. Se crean dos tablas en cada intervalo (5 minutos, 1 hora y 12 horas). Una de estas tablas almacena las agregaciones de nivel de rol; Hola otras agregaciones de almacenes de la tabla de instancias de rol. 

los nombres de tabla Hola tienen Hola siguiendo el formato:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

donde:

* *deploymentID* es hello GUID asignado toohello implementación del servicio de nube
* *aggregation_interval* = 5M, 1H o 12H
* agregados a nivel de rol = R
* agregados de las instancias de rol = RI

Por ejemplo, hello en las tablas siguientes podrían almacenar datos de supervisión detallada que se agregan a intervalos de 1 hora:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
