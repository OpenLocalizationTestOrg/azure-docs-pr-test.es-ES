---
title: "Herramientas de análisis de transmisiones de Azure para Visual Studio aaaUse | Documentos de Microsoft"
description: "Tutorial: Introducción para hello Azure Stream Analytics Tools para Visual Studio"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Uso de herramientas de Azure Stream Analytics para Visual Studio
## <a name="introduction"></a>Introducción
En este tutorial, aprenderá cómo análisis de flujo de toouse Azure Tools para Visual Studio toocreate, crear, probar localmente, administrar y depurar los trabajos de análisis de transmisiones. 

Después de completar este tutorial, estará capacitado para lo siguiente:
* Familiarícese con las herramientas de Stream Analytics para Visual Studio.
* Configurar e implementar un trabajo de Stream Analytics.
* Probar el trabajo localmente con datos de ejemplo local.
* Usar la supervisión de tootroubleshoot de problemas.
* Exportar tooprojects de trabajos existente.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:
* Complete los pasos de Hola que preceden a "Crear un trabajo de análisis de transmisiones" Hola [compila una solución de IoT mediante tutorial de análisis de transmisiones](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Use Visual Studio 2015, Visual Studio 2013 Update 4 o Visual Studio 2012. Se admiten las ediciones Enterprise (Ultimate y Premium), Professional y Community. No se admite la edición Express. Visual Studio 2017 no se admite. 
* Hola utilice Azure SDK para .NET versión 2.7.1 o una versión posterior. Instalar mediante hello [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Instalar hello [herramientas de análisis de secuencia para Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Creación de un trabajo de Stream Analytics
1. En Visual Studio, haga clic en hello **archivo** menú y seleccione **nuevo proyecto**. 

2. En lista de plantillas de Hola Hola izquierda, seleccione **análisis de transmisiones** y, a continuación, haga clic en **aplicación de Azure Stream Analytics**.

3. Escriba proyecto hello **nombre**, **ubicación**, y **nombre de la solución** tal como hace para otros proyectos.

    ![Ventana Nuevo proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Un proyecto de **peaje** se ha generado en el **Explorador de soluciones**.

    ![El proyecto de peaje se ha generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Elija la suscripción correcta Hola
1. En Visual Studio, haga clic en hello **vista** menú y abra **Explorador de servidores**.

2. Inicie sesión con su cuenta de Azure. 

## <a name="define-hello-input-sources"></a>Definir orígenes de entrada de Hola
1.  En **el Explorador de soluciones**, expanda hello **entradas** nodo y el nombre **Input.json** demasiado**EntryStream.json**. Haga doble clic en **EntryStream.json**.
2.  Hola **Alias de entrada** es ahora **EntryStream**. alias de Hola de entrada se utiliza en la secuencia de comandos de consulta de Hola. 
3.  En **Tipo de origen**, seleccione **Flujo de datos**.
4.  En **Origen**, seleccione **Centro de eventos**.
5.  En **Namespace de Bus de servicio**, seleccione hello **TollData** opción.
6.  En **Nombre del centro de eventos**, seleccione **entrada**.
7.  En **nombre de directiva de centro de eventos**, seleccione **RootManageSharedAccessKey** (Hola el valor predeterminado).
8.  En **Formato de serialización de eventos**, seleccione **Json**. 
9.  En **Codificación**, seleccione **UTF-8**. La configuración debe ser similar Hola siguiente captura de pantalla:

    ![Ventana de entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Asistente de hello toofinish, haga clic en **guardar**. Ahora puede agregar otro flujo de salida de hello de toocreate de origen de entrada. Menú contextual hello **entradas** nodo y seleccione **nuevo elemento**.

    ![Nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. En la ventana de hello, seleccione **entrada de análisis de flujo de Azure**y cambiar hello **nombre** demasiado**ExitStream.json**. Haga clic en **Agregar**.

    ![Ventana Agregar nuevo elemento](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Haga doble clic en **ExitStream.json** proyecto Hola y Hola seguimiento mismo pasos tal y como lo hizo para el flujo de entrada de Hola. Ser seguro tooenter **salir** para hello **nombre centro de eventos** tal y como se muestra en la siguiente captura de pantalla de hello:

    ![Ventana ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Ahora ha definido dos flujos de entrada:

    ![Flujos de entrada y salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    A continuación, agregue la entrada de datos de referencia para el archivo de blob de Hola que contiene datos de registro del automóvil.

13. Menú contextual hello **entradas** nodo Hola proyecto y, a continuación, Hola seguimiento mismo pasos tal y como lo hizo para las entradas de la secuencia de Hola. En **Alias de entrada**, escriba **Registro** y en **Tipo de origen**, seleccione **Datos de referencia**.

    ![Ventana Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. En **cuenta de almacenamiento**, seleccione hello **tolldata** opción. En **Contenedor**, seleccione **tolldata** y, en **Patrón de ruta de acceso**, escriba **registration.json**. Este nombre de archivo distingue mayúsculas de minúsculas, por lo que asegúrese de escribirlo en minúsculas.
15. Asistente de hello toofinish, haga clic en **guardar**.

Ahora se definen todas las entradas de Hola.

## <a name="define-hello-output"></a>Definir la salida de hello
1.  En **el Explorador de soluciones**, expanda hello **entradas** nodo y haga doble clic en **Output.json**.

2.  En **Alias de salida**, escriba **salida**. 
3.  En **Receptor**, seleccione **SQL Database**.
4.  En **Base de datos**, seleccione **TollDataDB**.
5.  En **Nombre de usuario**, escriba **tolladmin**. 
6.  En **Contraseña**, escriba **123toll!**.
7.  En **Tabla**, escriba **TollDataRefJoin**.
8.  Haga clic en **Guardar**.

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Creación de una consulta de Stream Analytics
Este tutorial trata tooanswer varias cuestiones empresariales que están relacionados tootoll datos. Además, crea las consultas de análisis de transmisiones que se pueden usar en las respuestas de análisis de transmisiones tooprovide relevantes.
Antes de empezar su primer trabajo de análisis de transmisiones, vamos a examinar una sintaxis de consulta simple hello y escenario.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Introducción toohello lenguaje de consulta de análisis de transmisiones
Supongamos que necesita el número de hello toocount de vehículos que entran en una cabina de peaje. Dado que este ejemplo es una secuencia continua de eventos, deberá toodefine un período de tiempo. Modificar hello toobe de pregunta "¿cuántos vehículos escriba una cabina de peaje cada tres minutos?" Este toocount de manera son ser datos conoce el recuento de saltos de tamaño constante de hello tooas.

Un vistazo a la consulta de análisis de transmisiones de Hola que responda a esta pregunta:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Análisis de transmisiones usa un lenguaje de consulta que es similar a SQL y agrega algunas extensiones toospecify relacionados con el tiempo aspectos de hello consulta.

Para obtener más información, consulte [administración del tiempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) y [ventana](https://msdn.microsoft.com/library/azure/dn835019.aspx) construcciones que se usan en consultas de Hola de MSDN.

Ahora que ha escrito la primera consulta de análisis de transmisiones, es el tiempo tootest lo. Utilizar archivos de datos de ejemplo de Hola ubicados en la carpeta TollApp Hola siguiendo la ruta de acceso:

..\TollApp\TollApp\Data

Esta carpeta contiene Hola siguientes archivos:
*   Entry.json
*   Exit.json
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Número de Hola de vehículos puestos una cabina de peaje
En el proyecto de hello, haga doble clic en **Script.asaql** tooopen script de Hola Hola **Editor de consultas**. Copie y pegue el script de Hola en la sección anterior de hello en editor de Hola. Hola Editor de consultas admite IntelliSense, colorear la sintaxis y el marcador de error de Hola.

![Editor de consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Probar las consultas de Stream Analytics localmente

1. toocompile Hola consulta toosee si se produce un error de sintaxis, haga clic en proyecto de Hola y seleccione **generar**. 

2. toovalidate esta consulta con datos de ejemplo, puede usar datos de ejemplo local. Haga clic en la entrada de Hola y seleccione **Agregar entrada local**.

    ![Agregar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. En la ventana emergente de hello, seleccione datos de ejemplo de Hola desde la ruta de acceso local. Haga clic en **Guardar**.

    ![Agregar ventana de entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Un archivo denominado **local_EntryStream.json** se agrega automáticamente la carpeta de entradas de tooyour.

    ![Carpeta de archivos de tooinputs agregado](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. Hola **Editor de consultas**, haga clic en **ejecutar localmente**. O bien, puede presionar la tecla F5 de Hola.

    ![Ejecución en modo local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Resultado de la ejecución local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Presione cualquier resultado de hello tooview clave Hola **ASA Local ejecutar resultado** ventana de Visual Studio. 

    ![Ventana Resultado de la ejecución local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Haga clic en **abrir la carpeta de resultados** archivos de salida de hello toocheck tanto en formato CSV y JSON.

    ![Resultado de abrir la carpeta de resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Datos de entrada de ejemplo Hola
También puede datos de entrada de ejemplo de archivo local tooa de orígenes de entrada. 
1. Haga clic en el archivo de configuración de entrada de Hola y seleccione **datos de ejemplo**. 

   ![Datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Por el momento solo puede usar como ejemplo el centro de eventos o IoT Hub. No se admiten otros orígenes de entrada.

2. En la ventana emergente de hello, escriba datos de ejemplo de Hola utiliza la ruta de acceso local toosave Hola. Haga clic en **Ejemplo**.

    ![Ventana de datos de ejemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Puede ver el progreso Hola Hola **salida** ventana. 

    ![Ventana de salida](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Enviar una tooAzure de consultas de análisis de transmisiones
1. Hola **Editor de consultas**, haga clic en **enviar tooAzure** en el editor de script de Hola.

    ![Enviar tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Seleccione **Crear un trabajo de Azure Stream Analytics**. Escriba hello **nombre del trabajo**, seleccione hello correcto y **suscripción**. Haga clic en **Enviar**.

    ![Ventana Enviar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Iniciar un trabajo
Ahora que se crea el trabajo, se abre automáticamente la vista de trabajos de Hola. 
1. Hola toostart de trabajo, haga clic en hello **flecha verde** botón.

    ![Iniciar un trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Seleccione la configuración predeterminada de Hola y haga clic en **iniciar**.
 
    ![Ventana Iniciar trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    trabajo de Hello **estado** cambia demasiado**ejecutando**, y **eventos de entrada** y **eventos de salida** aparecen.

    ![Estado de ejecución en Resumen del trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Comprobar los resultados de hello en Visual Studio
1. En Visual Studio, abra **Explorador de servidores** contextual hello y **TollDataRefJoin** tabla.
2. Seleccione **mostrar datos de tabla** toosee salida de hello de su trabajo.
   
    ![Selección de Mostrar datos de tabla en el Explorador de servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Visualice las métricas de trabajo de Hola
En **Job Metrics** (Métricas de trabajo) se pueden encontrar algunas estadísticas básicas de trabajo. 

![Ventana Métricas de trabajo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Trabajo de Hola de lista en el Explorador de servidores
En el **Explorador de servidores**, haga clic en **Trabajos de Stream Analytics** y, después, haga clic en **Actualizar**. trabajo de Hello aparece bajo **trabajos de análisis de transmisiones**.

![Los trabajos de Stream Analytics aparecen en el Explorador de servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Vista de trabajos de hello abierto
vista de trabajos de hello tooopen, expanda el nodo de trabajo y haga doble clic hello **trabajo vista** nodo.

![Nodo Vista de trabajos](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Exportar un proyecto de tooa de trabajo existente
Hay dos maneras puede exportar un proyecto de tooa de trabajo existente.

En **Explorador de servidores**, nodo de trabajo contextual Hola Hola **trabajos de análisis de transmisiones** nodo y seleccione **exportar tooNew proyecto de análisis de transmisiones**.

![Exportar tooNew proyecto de análisis de transmisiones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

se genera el proyecto de Hello en **el Explorador de soluciones**.

![Proyecto generado en el Explorador de soluciones](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
También puede usar la vista de trabajos de Hola y haga clic en **generar proyecto**.

![Generar el proyecto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Problemas conocidos y limitaciones
 
- No hay ninguna compatibilidad para la salida de Power BI y la salida de Azure Date Lake Store.
- No hay ninguna compatibilidad con el editor para agregar o cambiar las funciones definidas por el usuario de JavaScript.

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
