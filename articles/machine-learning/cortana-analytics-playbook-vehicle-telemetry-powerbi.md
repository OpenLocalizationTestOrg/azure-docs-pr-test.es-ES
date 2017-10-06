---
title: "transformación de aaaPower panel de BI para mantenimiento de vehículo y dirigir - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Instrucciones de configuración del panel de Power BI para la plantilla de la solución Análisis de telemetría de vehículos
Esto **menú** vincula toohello capítulos en esta guía. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Hola solución de análisis de telemetría de vehículo muestra cómo concesiones de coches, los fabricantes de automóviles y compañías de seguros pueden aprovechar las capacidades de Hola de inteligencia de Cortana toogain en tiempo real y predicción obtener información detallada en el mantenimiento de vehículo y dirigir las mejoras del toodrive hábitos de cliente en el área de hello experiencia, departamento de I+d y campañas de marketing. Este documento contiene instrucciones paso a paso acerca de cómo puede configurar informes de Power BI de Hola y el panel una vez implementada la solución hello en su suscripción. 

## <a name="prerequisites"></a>Requisitos previos
1. Implementar hello [análisis de telemetría](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solución  
2. [Instalar Microsoft Power BI Desktop.](http://www.microsoft.com/download/details.aspx?id=45331)
3. Una [suscripción de Azure](https://azure.microsoft.com/pricing/free-trial/). Si no tiene una suscripción de Azure, comience con una suscripción gratis de Azure.
4. Cuenta de Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Componentes de Cortana Intelligence Suite
Como parte de la plantilla de solución de análisis de telemetría de vehículo hello, Hola después de los servicios de inteligencia de Cortana se implementa en su suscripción.

* **Centro de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.
* **Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.
* **Aprendizaje automático** para la detección de anomalías en tiempo real y toogain predictiva visión de procesamiento por lotes.
* **HDInsight** tootransform aprovechado datos a escala
* **Factoría de datos** controla la orquestación, programación, administración de recursos y la supervisión de la canalización de procesamiento por lotes de Hola.

**Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo. 

solución de Hello utiliza dos orígenes de datos diferentes: **simulan las señales de vehículo y conjunto de datos de diagnóstico** y **catálogo vehículo**.

Se incluye un simulador telemático del vehículo como parte de esta solución. Se emite información de diagnóstico y señales de estado toohello correspondiente del vehículo hello y conducir patrón en un momento dado en el tiempo. 

Hello vehículo catálogo es una asignación referencia conjunto de datos que contienen Niv toomodel

## <a name="power-bi-dashboard-preparation"></a>Preparación de panel de Power BI
### <a name="setup-power-bi-real-time-dashboard"></a>Configuración del panel de Power BI en tiempo real

**Iniciar la aplicación de panel en tiempo real de hello** cuando se haya completado la implementación de hello, debe seguir las instrucciones de funcionamiento de hello Manual

* Descargue la aplicación de panel en tiempo real RealtimeDashboardApp.zip y descomprímala.
*  En la carpeta descomprimida de hello, abra el archivo de configuración de aplicación 'RealtimeDashboardApp.exe.config' appSettings de reemplazo para las conexiones de servicio de Eventhub, almacenamiento de blobs y aprendizaje automático con valores de hello en hello Manual de las instrucciones de funcionamiento y guarde los cambios.
* Ejecute la aplicación RealtimeDashboardApp.exe. Una ventana de inicio de sesión se emergente, proporcione sus credenciales de Power BI válidos y haga clic en hello **Accept** botón. A continuación, la aplicación hello iniciará toorun.

   ![Inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permisos de panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Sitio Web de tooPowerBI de inicio de sesión y crear un panel en tiempo real.

Ahora, está listo tooconfigure panel de Power BI Hola con toogain visualizaciones enriquecidas en tiempo real y transformación de la visión de predicción en mantenimiento de vehículo y dirigir. Tardará aproximadamente 45 minutos tooan hora toocreate Hola todos los informes y configurar panel Hola. 

### <a name="configure-power-bi-reports"></a>Configuración de informes de Power BI
informes en tiempo real de Hola y el panel de hello tardan aproximadamente toocomplete 30 y 45 minutos. Examinar demasiado[http://powerbi.com](http://powerbi.com) e inicio de sesión.

![Inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Se genera un nuevo conjunto de datos en Power BI. Haga clic en hello **ConnectedCarsRealtime** conjunto de datos.

![Seleccione conjunto de datos en tiempo real de automóviles conectados.](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Guardar informe en blanco de hello mediante **Ctrl + s**.

![Guardar el informe en blanco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Proporcione el nombre del informe *Análisis de telemetría del vehículo en tiempo real - Informes*.

![Proporcione el nombre del informe](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Informes en tiempo real
Hay tres informes en tiempo real en esta solución:

1. Vehículos en funcionamiento
2. Vehículos que requieren mantenimiento
3. Estadísticas de estado de los vehículos

Puede elegir tooconfigure todos los informes en tiempo real tres de Hola o detenerse después de cualquier fase y continuar toohello la siguiente sección de configuración de informes de lote de Hola. Le recomendamos que todos los toocreate Hola tres informes visión completa de hello toovisualize de ruta de acceso en tiempo real de Hola de solución de Hola.  

### <a name="1-vehicles-in-operation"></a>1. Vehículos en funcionamiento
Haga doble clic en **página 1** y cambie su nombre demasiado "Vehículos en la operación"  
    ![Automóviles conectados: Vehículos en funcionamiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Seleccione el campo **vin** en **Campos** y elija el tipo de visualización como **“Tarjeta”**.  

Se crea la visualización de tarjeta como se muestra en la ilustración.  
    ![Automóviles conectados - Seleccionar vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione **city** y **vin** en los campos. Cambiar visualización demasiado**"Map"**. Arrastre **vin** al área de valores. Arrastre **city** de campos demasiado**leyenda** área.   
    ![Automóviles conectados - Visualización de tarjeta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Seleccione **formato** sección **visualizaciones**, haga clic en **título** y cambiar hello **texto** demasiado**"vehículos en operación por ciudad"**.  
    ![Automóviles conectados: Vehículos en funcionamiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

La visualización final tiene el aspecto que se muestra en la ilustración.    
    ![Automóviles conectados - Visualización final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione **City** y **Niv**, cambie el tipo de visualización demasiado**gráfico de columnas agrupadas**. Asegúrese de que el campo **city** esté en el área **Eje** y **vin** en el área **Valor**.  

Ordene el gráfico por **“Recuento de vin”**.  
    ![Automóviles conectados - Recuento de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Gráfico de cambio **título** demasiado**"Vehículos en operación por ciudad"**  

Haga clic en hello **formato** sección, a continuación, seleccione **colores de datos**, haga clic en hello **"En"** demasiado**mostrar todo**  
    ![Automóviles conectados: Mostrar todos los colores de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Cambiar el color de Hola de ciudad individual haciendo clic en el icono de color.  
    ![Automóviles conectados - Cambiar colores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione la visualización **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **city** al área **Eje**, el campo **Model** al área **Leyenda** y el campo **vin** al área **Valor**.  
    ![Automóviles conectados: Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Automóviles conectados: Representación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Reorganice toda la visualización de esta página como se muestra en la ilustración.  
    ![Automóviles conectados - Visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Informes en tiempo real de Hola "Vehículos en la operación" se configuró correctamente. Puede continuar informes en tiempo real de toocreate Hola siguiente o deténgase aquí y configuración de panel de Hola. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Vehículos que requieren mantenimiento
Haga clic en ![agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nuevo informe, cámbiele el nombre demasiado**"Vehículos que requieren mantenimiento"**

![Automóviles conectados - Vehículos que requieren mantenimiento](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Seleccione **Niv** del campo y cambiar el tipo de visualización demasiado**tarjeta**.  
    ![Automóviles conectados: Visualización de tarjeta vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Tenemos un campo denominado "MaintenanceLabel" en el conjunto de datos de Hola. Este campo puede tener un valor de "0" o "1". Se establece mediante el modelo de aprendizaje automático de Azure Hola suministrados como parte de la solución y se integran con la ruta de acceso en tiempo real de Hola. valor de Hola "1" indica que un vehículo requiere mantenimiento. 

tooadd una **de nivel de página** filtro para mostrar datos de vehículos, que requieren mantenimiento: 

1. Hola arrastre **"MaintenanceLabel"** campo **filtros de nivel de página**.  
   ![Automóviles conectados - Filtros de nivel de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Haga clic en el menú **Filtrado básico** que se encuentra en la parte inferior del filtro de nivel de página MaintenanceLabel.  
   ![Automóviles conectados - Filtrado básico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Establezca su valor de filtro demasiado**"1"**    
   ![Automóviles conectados - Valor de filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione **Gráfico de columnas agrupadas** en Visualizaciones.  
![Automóviles conectados - Visualización de tarjeta vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Automóviles conectados - Gráfico de columnas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Campo de arrastre **modelo** en **eje** área, **Niv** demasiado**valor** área. Después, ordene la visualización por **Recuento de vin**.  Gráfico de cambio **título** demasiado**"Vehículos que requiere el modelo de mantenimiento"**  

Arrastre los campos **vin** a **Saturación de color**, que se encuentra en la sección **Campos** ![Campos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) de la pestaña **Visualización**.  
![Automóviles conectados - Saturación de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Cambie **Colores de datos** en las visualizaciones de la sección **Formato**.  
Cambie el color mínimo a: **F2C812**  
Cambie el color máximo a: **FF6300**  
![Automóviles conectados - Cambios de color](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Automóviles conectados - Nuevos colores de visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione **Gráfico de columnas agrupadas** en Visualizaciones, arrastre el campo **vin** al área **Valor** y arrastre el campo **city** al área **Eje**. Ordene el gráfico por **“Recuento de vin”**. Gráfico de cambio **título** demasiado**"Vehículos que requiere el mantenimiento por ciudad"**   
![Automóviles conectados - Vehículos que requieren mantenimiento por ciudad](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Haga clic en nueva visualización de hello área en blanco tooadd.  

Seleccione **tarjeta de varias filas** visualización de visualizaciones, arrastre **modelo** y **Niv** en hello **campos** área.  
![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Reorganizar todo de visualización de hello, informe final hello tiene el siguiente aspecto:  
![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Informes en tiempo real de Hola "Vehículos necesidad de mantenimiento" se configuró correctamente. Puede continuar informes en tiempo real de toocreate Hola siguiente o deténgase aquí y configuración de panel de Hola. 

### <a name="3-vehicles-health-statistics"></a>3. Estadísticas de estado de los vehículos
Haga clic en ![agregar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nuevos informes, cambiar el nombre demasiado**"Las estadísticas de estado de vehículos"**  

Seleccione **medidor** visualización de visualizaciones, a continuación, arrastre hello **velocidad** campo **, valor mínimo, máximo valor** áreas.  
![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Cambiar la agregación predeterminada de Hola de **velocidad** en **valor área** demasiado**promedio** 

Cambiar la agregación predeterminada de Hola de **velocidad** en **área mínimo** demasiado**mínimo**

Cambiar la agregación predeterminada de Hola de **velocidad** en **área máximo** demasiado**máximo**

![Automóviles conectados - Tarjeta de varias filas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Cambiar el nombre de hello **medidor título** demasiado**"Promedio de velocidad"** 

![Automóviles conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Haga clic en nueva visualización de hello área en blanco tooadd.  

Del mismo modo, agregue un **Indicador** para el **aceite medio del motor**, el **combustible medio** y la **temperatura media del motor**.  

Cambiar agregación predeterminada de Hola de campos de cada medidor según por encima de los pasos descritos en **"Promedio de velocidad"** del medidor.

![Automóviles conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Haga clic en nueva visualización de hello área en blanco tooadd.

Seleccione **línea y gráfico de columnas agrupadas** de visualizaciones, a continuación, arrastre **City** campo **eje compartido**, arrastre **velocidad**, **campos tirepressure y engineoil** en **valores de columna** área, cambiar su tipo de agregación demasiado**Media**. 

Hola arrastre **engineTemperature** campo **valores de las líneas** área, también cambian el tipo de agregación de hello**promedio**. 

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Gráfico de cambio hello **título** demasiado**"Promedio velocidad, tire presión, petróleo de motor y temperatura del motor"**.  

![Automóviles conectados - Campos de visualizaciones](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Haga clic en nueva visualización de hello área en blanco tooadd.

Seleccione **Treemap** visualización de visualizaciones, arrastre hello **modelo** campo hello **grupo** área y arrastre Hola campo  **MaintenanceProbability** en hello **valores** área.

Gráfico de cambio hello **título** demasiado**"Que requiere el mantenimiento de modelos de vehículo"**.

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Haga clic en nueva visualización de hello área en blanco tooadd.

Seleccione **gráfico de barras apiladas 100%** de visualización, arrastre hello **city** campo hello **eje** área y arrastre hello **MaintenanceProbability**, **RecallProbability** campos en hello **valor** área.

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Haga clic en **formato**, seleccione **colores de datos**, conjunto hello y **MaintenanceProbability** toohello valor de color **"F2C80F"**.

Hola de cambio **título** de hello gráfico demasiado**"Probabilidad de vehículo mantenimiento y recuerde by City"**.

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Haga clic en nueva visualización de hello área en blanco tooadd.

Seleccione **gráfico de áreas** de visualización de visualizaciones, arrastre hello **modelo** campo hello **eje** área y arrastre hello **engineOil, tirepressure, velocidad y MaintenanceProbability** campos en hello **valores** área. Cambiar el tipo de agregación también**"Medio"**. 

![Automóviles conectados - Cambiar tipo de agregación](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Cambiar el título de hello del gráfico de hello demasiado**"Promedio de petróleo motor, probabilidad presión, velocidad y el mantenimiento de neumáticos modelo"**.

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Haga clic en nueva visualización de hello área en blanco tooadd:

1. Seleccione la visualización **Gráfico de dispersión** en Visualizaciones.
2. Hola arrastre **modelo** campo hello **detalles** y **leyenda** área.
3. Hola arrastre **combustible** campo hello **eje x** área, cambiar las agregaciones de hello también**Media**.
4. Arrastre **engineTemparature** en **área de eje y**, cambiar las agregaciones de hello también**promedio**
5. Hola arrastre **Niv** campo hello **tamaño** área.

![Automóviles conectados - Agregar nueva visualización](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Gráfico de cambio hello **título** demasiado**"Medias de combustible y temperatura del motor por modelo"**.

![Automóviles conectados - Cambiar el título del gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

Hola final será informe tal y como se muestra a continuación.

![Automóviles conectados - Informe final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Visualizaciones de PIN de panel en tiempo real de hello informes toohello
Crear un panel en blanco, haga clic en el icono de hello más tooDashboards siguiente. Puede asignarle el nombre "Panel de análisis de telemetría de vehículos".

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Visualización de PIN Hola de Hola por encima del panel de toohello de informes. 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

panel de Hello debe ser similar al siguiente cuando todos los Hola se crean tres informes y Hola correspondiente visualizaciones están anclados toohello panel. Si no ha creado todos los informes de hello, el panel podría ser diferente. 

![Automóviles conectados - Panel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

¡Enhorabuena! Ha creado correctamente la API de REST de Hola. A medida que continúa tooexecute CarEventGenerator.exe y RealtimeDashboardApp.exe, debería ver actualizaciones directas en el panel de Hola. Tardará hello toocomplete too15 unos 10 minutos que siga los pasos.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Configuración del panel de procesamiento por lotes de Power BI
> [!NOTE]
> Se tarda aproximadamente dos horas (de realización correcta de Hola de implementación de hello) de ejecución de toofinish la canalización de procesamiento por lotes de tooend de final de hello y procesar un período de año de datos generados. Por lo que espere hello toofinish antes de continuar con los pasos siguientes de Hola de procesamiento. 
> 
> 

**Descargar el archivo del diseñador Hola Power BI**

* Un archivo del Diseñador de Power BI configurado previamente se incluye como parte de la implementación de hello las instrucciones de funcionamiento Manual
* Busque 2. Panel de procesamiento por lotes de instalación Power BI puede descargar plantilla de Power BI de hello para el panel de procesamiento por lotes llamado **ConnectedCarsPbiReport.pbix**.
* Guarde localmente.

**Configuración de informes de Power BI**

* Archivo del diseñador abra hello '**ConnectedCarsPbiReport.pbix**' con Power BI Desktop. Si ya no tiene, instala Hola Power BI Desktop desde [instalación de Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Haga clic en hello **editar consultas**.

![Edición de la consulta de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Haga doble clic en hello **origen**.

![Establecimiento de origen de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Actualizar la cadena de conexión de servidor con hello Azure SQL server que se obtuvo suministrado como parte de la implementación de Hola.  Buscar en las instrucciones de funcionamiento de hello Manual en 

    4. Azure SQL Database
    
    * Servidor: somethingsrv.database.windows.net
    * Base de datos: connectedcar
    * Nombre de usuario: username
    * Contraseña: Puede administrar la contraseña de SQL Server desde Azure Portal

* Establezca **Base de datos** como *connectedcar*.

![Establecimiento de la base de datos Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Haga clic en **Aceptar**.
* Verá **credencial de Windows** ficha seleccionada de forma predeterminada, también cambian**las credenciales de la base de datos** haciendo clic en **base de datos** ficha a la derecha.
* Proporcionar hello **nombre de usuario** y **contraseña** de la base de datos de SQL Azure que se especificó durante la instalación de su implementación.

![Introduzca las credenciales de la base de datos](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Haga clic en **Conectar**
* Repita Hola por encima de los pasos para cada uno de hello tres restantes consultas presentes en el panel derecho y, a continuación, actualice los detalles de conexión de origen de datos de Hola.
* Haga clic en **Cerrar y cargar**. Los conjuntos de datos de archivo de Power BI Desktop son tablas de base de datos de Azure tooSQL conectado.
* **Cierre** el archivo de Power BI Desktop

![Cierre Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Haga clic en **guardar** botón toosave Hola cambiará. 

Ya ha configurado todos los informes de hello correspondiente toohello ruta de procesamiento por lotes de solución de Hola. 

## <a name="upload-toopowerbicom"></a>Cargar demasiado*powerbi.com*
1. Navegue toohello portal de web de Power BI en http://powerbi.com e inicio de sesión.
2. Haga clic en **Obtener datos**  
3. Cargar archivo de Power BI Desktop Hola.  
4. tooupload, haga clic en **obtener datos -> archivos Get -> archivo Local**  
5. Navegue toohello **"**ConnectedCarsPbiReport.pbix**"**  
6. Una vez cargado el archivo hello, será tooyour atrás navegar de un área de trabajo de Power BI.  

Se crearán un conjunto de datos, un informe y un panel en blanco.  

Gráficos de PIN tooa nuevo panel denominado **panel de análisis de telemetría de vehículo** en **Power BI**. Haga clic en panel en blanco Hola creado anteriormente y, a continuación, navegue toohello **informes** sección, haga clic Hola recién cargado el informe.  

![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Tenga en cuenta Hola informe tiene seis páginas:**  
Página 1: Densidad de vehículos  
Página 2: Estado de vehículos en tiempo real  
Página 3: Vehículos conducidos de forma agresiva   
Página 4: Vehículos retirados  
Página 5: Vehículos conducidos con un consumo eficiente  
Página 6: Logotipo de Contoso  

![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Desde la página 3**, anclar siguiente hello:  

1. Recuento de vin  
   ![Automóviles conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Vehículos que se han conducido de forma agresiva por modelo: gráfico de cascada   
   ![Telemetría del vehículo - Anclar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Desde la página 5**, anclar siguiente hello: 

1. Recuento de vin    
   ![Telemetría del vehículo - Anclar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Vehículos con ahorro de combustible por modelo: gráfico de columnas agrupadas   
   ![Telemetría del vehículo - Anclar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**En la página 4**, anclar siguiente hello:  

1. Recuento de vin  
   ![Telemetría del vehículo - Anclar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Vehículos retirados por ciudad y modelo: gráfico de rectángulos   
   ![Telemetría del vehículo - Anclar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Página 6**, anclar siguiente hello:  

1. Logotipo de Contoso Motors  
   ![Telemetría del vehículo - Anclar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Organizar Hola panel**  

1. Vaya a Panel de toohello
2. Mantenga el mouse sobre cada gráfico y cambie su nombre en función de nomenclatura de hello proporcionadas en hello panel completa de las siguientes imágenes. Mover gráficos Hola alrededor toolook como Hola panel siguiente.  
   ![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetría de vehículos Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Si ha creado todos los informes de hello como se ha mencionado en este documento, hello final panel completado debería parecerse Hola figura siguiente. 

![Telemetría del vehículo - Organizar panel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

¡Enhorabuena! Se han creado correctamente los informes de Hola y Hola toogain de panel en tiempo real, predicción y transformación de la visión de lote en el estado de vehículo y dirigir.  
