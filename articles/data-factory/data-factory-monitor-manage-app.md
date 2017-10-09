---
title: aaaMonitor y administrar las canalizaciones de datos - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomonitor de aplicación de supervisión y administración y administrar las canalizaciones y los generadores de datos de Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Supervisar y administrar las canalizaciones de factoría de datos de Azure mediante la aplicación de supervisión y administración de hello
> [!div class="op_single_selector"]
> * [Uso de Azure Portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Uso de la aplicación de supervisión y administración](data-factory-monitor-manage-app.md)
>
>

Este artículo describe cómo toouse Hola toomonitor de aplicación de supervisión y administración, administrar y depurar las canalizaciones de factoría de datos. También se proporciona información sobre cómo toocreate alertas tooget una notificación cuando se produzcan errores. Puede empezar con el uso de la aplicación hello por ver Hola después de vídeo:

> [!NOTE]
> interfaz de usuario de Hola que se muestra en hello vídeo puede no coincidir lo que se ve en el portal de Hola. Es ligeramente más antiguo, pero conceptos permanecen Hola mismo. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Inicie la aplicación de supervisión y administración de hello
Hola toolaunch Monitor y la aplicación de administración, haga clic en hello **Monitor & administrar** icono hello **factoría de datos** hoja de la factoría de datos.

![Icono página principal de hello factoría de datos de supervisión](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Debería ver aplicación de supervisión y administración de hello abrir en una ventana independiente.  

![Aplicación de supervisión y administración](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Si ve ese explorador web de hello está atascado en "Autorizar …", desactive hello **bloquear las cookies de terceros y datos de sitio** casilla de verificación--o mantener aún seleccionada, cree una excepción para **login.microsoftonline.com** y, a continuación, vuelva a intentarlo tooopen Hola aplicación.


En la lista de ventanas de la actividad de hello en el panel central de hello, verá una ventana de actividad para cada ejecución de una actividad. Por ejemplo, si tiene Hola actividad programada toorun cada hora durante cinco horas, verá cinco ventanas de la actividad asociadas a segmentos de datos de cinco. Si no ve las ventanas de la actividad en la lista de hello en parte inferior de hello, Hola siguientes:
 
- Hola de actualización **hora de inicio** y **hora de finalización** filtros en Hola toomatch superior Hola inicio y finalización de la canalización y, a continuación, haga clic en hello **aplicar** botón.  
- lista de ventanas de la actividad de Hello no se actualiza automáticamente. Haga clic en hello **actualizar** botón de barra de herramientas Hola Hola **Windows actividad** lista.  

Si no tiene un tootest de aplicación de la factoría de datos de estos pasos con, Hola tutorial: [copiar los datos de almacenamiento de blobs tooSQL con factoría de datos de la base de datos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Entender la aplicación de supervisión y administración de hello
Hay tres pestañas de hello izquierda: **Resource Explorer**, **vistas de supervisión de**, y **alertas**. primera pestaña de Hello (**Resource Explorer**) está activada de forma predeterminada.

### <a name="resource-explorer"></a>Explorador de recursos
Se ve Hola siguiente:

* Hola Resource Explorer **vista de árbol** en el panel izquierdo de Hola.
* Hola **vista de diagrama** en parte superior de hello en el panel central de Hola.
* Hola **Windows actividad** lista final hello en el panel central de Hola.
* Hola **propiedades**, **Explorer de la ventana de actividad**, y **Script** fichas en el panel derecho de Hola.

En el Explorador de recursos, verá todos los recursos (canalizaciones, los conjuntos de datos, servicios vinculados) de la factoría de datos de hello en una vista de árbol. Al seleccionar un objeto en el Explorador de recursos:

* Hola asociado factoría de datos de entidad se resalta en hello vista de diagrama.
* [Asociados de ventanas de la actividad](data-factory-scheduling-and-execution.md) se resaltan en la lista de ventanas de la actividad de hello en parte inferior de Hola.  
* propiedades Hola del objeto seleccionado Hola se muestran en la ventana de propiedades de hello en el panel derecho de Hola.
* se muestra la definición JSON del objeto seleccionado Hola Hola, si procede. Por ejemplo: un servicio vinculado, un conjunto de datos o una canalización.

![Explorador de recursos](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Vea hello [ejecución y programación](data-factory-scheduling-and-execution.md) artículo para obtener información conceptual detallada sobre las ventanas de actividad.

### <a name="diagram-view"></a>Vista de diagrama
Hola vista de diagrama de una factoría de datos proporciona un único panel de vidrio toomonitor y administrar una factoría de datos y sus activos. Cuando se selecciona una entidad de factoría de datos (conjunto de datos y canalización) en la vista de diagrama de hello:

* entidad de factoría de datos de Hello está seleccionado en la vista de árbol de Hola.
* Hola asociado actividad windows se resaltan en la lista de ventanas de la actividad de Hola.
* propiedades de Hello del objeto seleccionado Hola se muestran en la ventana de propiedades de Hola.

Cuando se habilita la canalización de hello (no en un estado pausado), se muestra con una línea verde:

![Canalización en ejecución](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Puede pausar, reanudar o finalizar una canalización seleccionándolo en la vista de diagrama de Hola y con los botones de hello en la barra de comandos de Hola.

![Pausar y reanudar en la barra de comandos de Hola](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Hay tres botones de barra de comandos de la canalización de Hola Hola vista de diagrama. Puede usar la canalización de hello segundo botón toopause Hola. Pausar Hola actividades en ejecución, no termina y les permite continuar toocompletion. tercer botón de Hola detiene la canalización de Hola y finaliza su ejecución de actividades existentes. botón primera Hola reanuda la canalización de Hola. Cuando la canalización está en pausa, se cambia el color de Hola de canalización de Hola. Por ejemplo, una canalización en pausa es similar en hello después de imagen: 

![Canalización en pausa](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Puede seleccionar varias canalizaciones de dos o más mediante el uso de la tecla Ctrl de Hola. Puede usar botones de barra de comandos hello toopause/reanudar varias canalizaciones a la vez.

También puede hacer clic una canalización y seleccione las opciones toosuspend, reanudar o finalizar una canalización. 

![Menú contextual de la canalización](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Haga clic en hello **canalización abierto** opción toosee todas las actividades de hello en la canalización de Hola. 

![Menú Abrir canalización](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

En la vista de la canalización de hello abierto, verá todas las actividades de canalización de Hola. En este ejemplo, solamente hay una actividad: la actividad de copia. 

![Canalización abierta](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo realizar copias toohello vista anterior, haga clic en nombre de generador de datos de hello en el menú de la ruta de navegación de hello en la parte superior de Hola.

En la vista de la canalización de hello, cuando se selecciona un conjunto de datos de salida o al mover el mouse sobre el conjunto de datos de salida de hello, vea ventana emergente de actividad Windows hello para ese conjunto de datos.

![Ventana emergente Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Puede hacer clic en los detalles de toosee de ventana de una actividad para él en hello **propiedades** ventana en el panel derecho de Hola.

![Propiedades de la ventana de actividad](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

En el panel derecho de hello, cambie toohello **Explorer de la ventana de actividad** ficha toosee más detalles.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Consulte también **resuelve las variables** para cada intento de ejecución de una actividad en hello **intentos** sección.

![Variables resueltas](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Cambiar toohello **Script** ficha Definición de script toosee Hola JSON para el objeto seleccionado de Hola.   

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

Puede ver las ventanas de actividad en tres lugares:

* Hola ventanas emergentes Hola vista de diagrama (panel central) de la actividad.
* Hola Explorador de la ventana de actividad en el panel derecho de Hola.
* lista de ventanas de la actividad de Hello en el panel inferior de Hola.

En la ventana emergente de ventanas de la actividad de Hola y el Explorador de ventana de actividad, puede desplazarse a toohello la semana anterior y Hola semanas siguientes mediante el uso de Hola flechas izquierda y derecha.

![Flechas izquierda/derecha de Activity Window Explorer (Explorador de ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

En parte inferior de Hola de hello vista de diagrama, verá estos botones: Acercar, alejar, Zoom tooFit, Zoom 100%, diseño de bloqueo. Hola **diseño de bloqueo** botón impide que se muevan accidentalmente tablas y canalizaciones en hello vista de diagrama. Está activado de forma predeterminada. Puede desactivarla y mover las entidades en el diagrama de Hola. Cuando se lo desactiva, puede utilizar las canalizaciones y tablas de hello último botón tooautomatically posición. También puede acercar o alejar mediante el uso de la rueda del mouse de Hola.

![Comandos de ampliación de la vista de diagrama](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Lista Activity Windows (Ventanas de actividad)
Hola actividad Windows lista Hola parte inferior del panel central de hello muestra todas las ventanas de actividad de conjunto de datos de Hola que seleccionó en el Explorador de recursos de Hola o hello vista de diagrama. De forma predeterminada, lista de hello está en orden descendente, lo que significa que aparece la ventana de actividad más reciente de hello en la parte superior de Hola.

![Lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Esta lista no se actualiza automáticamente, por lo que el botón de actualización de uso hello en toomanually de barra de herramientas de hello actualizarlo.  

Ventanas de la actividad pueden estar en uno de hello siguientes estados:

<table>
<tr>
    <th align="left">Estado</th><th align="left">Subestado</th><th align="left">Description</th>
</tr>
<tr>
    <td rowspan="8">En espera</td><td>ScheduleTime</td><td>no se ha llegado el momento de Hola para toorun de ventana de actividad de Hola.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>dependencias de nivel superior de Hello no están preparadas.</td>
</tr>
<tr>
<td>ComputeResources</td><td>recursos de proceso de Hello no están disponibles.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Todas las instancias de actividad de hello están ocupadas ejecutando otras ventanas de la actividad.</td>
</tr>
<tr>
<td>ActivityResume</td><td>actividad Hello está en pausa y no puede ejecutar windows de la actividad de hello hasta que se reanude.</td>
</tr>
<tr>
<td>Retry</td><td>se vuelve a intentar la ejecución de la actividad de Hola.</td>
</tr>
<tr>
<td>Validación</td><td>Aún no ha iniciado la validación.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La validación es toobe espera vuelve a intentar.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>Validación en curso.</td>
</tr>
<td>-</td>
<td>ventana de actividad de saludo se está procesando.</td>
</tr>
<tr>
<td rowspan="4">Con error</td><td>TimedOut</td><td>ejecución de la actividad de Hello ha tardado más de las permitidas por actividad hello.</td>
</tr>
<tr>
<td>Canceled</td><td>ventana de actividad de Hello fue cancelada por acción del usuario.</td>
</tr>
<tr>
<td>Validación</td><td>Error de validación.</td>
</tr>
<tr>
<td>-</td><td>ventana de actividad de Hello no pudo toobe generado o validar.</td>
</tr>
<td>Ready</td><td>-</td><td>ventana de actividad de Hello está listo para su uso.</td>
</tr>
<tr>
<td>Skipped</td><td>-</td><td>ventana de actividad de Hello no se procesa.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>Una ventana de actividad utiliza tooexist con un estado diferente, pero se ha restablecido.</td>
</tr>
</table>


Al hacer clic en una ventana de actividad en la lista de hello, puede ver detalles sobre él en hello **el Explorador de Windows de actividad** o hello **propiedades** ventana en hello derecho.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Actualizar las ventanas de actividad
detalles de Hello no se actualizan automáticamente, así que usa Hola actualización botón (Hola segundo) en la lista de windows de toomanually actualización Hola actividad de la barra de comandos de Hola.  

### <a name="properties-window"></a>Ventana Propiedades
ventana de propiedades de Hello es en panel de hello más a la derecha de la aplicación de supervisión y administración de hello.

![Ventana Propiedades](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Muestra propiedades de elemento de Hola que seleccionó en hello Explorador de recursos (vista de árbol), vista de diagrama o la lista de ventanas de la actividad.

### <a name="activity-window-explorer"></a>Activity Window Explorer
Hola **actividad ventana Explorer** ventana está en el panel de hello más a la derecha de la aplicación de supervisión y administración de hello. Muestra detalles acerca de la ventana de actividad de Hola que seleccionó en la ventana emergente de ventanas de la actividad de Hola o una lista de ventanas de la actividad de Hola.

![Activity Window Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Puede cambiar la ventana de actividad de tooanother haciendo clic en él en la vista de calendario de hello en la parte superior de Hola. También puede usar los botones de flecha derecha o flecha izquierda hello en ventanas de la actividad de hello toosee superior de hello semana anterior u Hola semanas siguientes.

Puede usar botones de barra de herramientas de hello en ventana de actividad de hello toorerun del panel de la parte inferior Hola o actualizar los detalles de hello en el panel de Hola.

### <a name="script"></a>Script
Puede usar hello **Script** Hola de tooview ficha Definición JSON de hello seleccionado entidad de la factoría de datos (el servicio vinculado, el conjunto de datos o la canalización).

![Pestaña de script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Vistas de uso del sistema
Supervisión y administración de la aplicación Hello incluye vistas del sistema pregenerado (**ventanas de la actividad reciente**, **no se pudo ventanas de la actividad**, **ventanas de la actividad en curso**) que Permitir ventanas de la actividad reciente/error/en curso de tooview de la factoría de datos.

Cambiar toohello **vistas de supervisión de** ficha izquierda Hola haciendo clic en él.

![Pestaña Vistas de supervisión](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Actualmente, hay tres vistas del sistema compatibles. Seleccione una opción toosee ventanas de la actividad reciente, windows de una actividad con errores o ventanas de la actividad en curso en lista de ventanas de la actividad de hello (en hello parte inferior del panel central de hello).

Cuando selecciona hello **ventanas de la actividad reciente** opción, verá todas las ventanas de la actividad reciente en orden descendente de hello **último intento tiempo**.

Puede usar hello **no se pudo ventanas de la actividad** ver toosee error de todas las ventanas de la actividad en la lista de Hola. Seleccione una ventana de actividad con errores en hello lista toosee obtener información detallada sobre él en hello **propiedades** ventana o hello **Explorer de la ventana de actividad**. También puede descargar los registros de una ventana de actividad con error.

## <a name="sort-and-filter-activity-windows"></a>Ordenado y filtrado de las ventanas de actividad
Hola de cambio **hora de inicio** y **hora de finalización** configuración de ventanas de la actividad de toofilter la barra de comandos de Hola. Después de cambiar la hora de inicio de Hola y hora de finalización, haga clic en hello botón siguiente toohello final tiempo toorefresh Hola ventanas de la actividad.

![Horas de inicio y finalización](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Actualmente, todas las horas están en formato UTC en la aplicación de supervisión y administración de hello.
>
>

Hola **lista de ventanas de la actividad**, haga clic en nombre de Hola de una columna (por ejemplo: estado).

![Menú de columna de la lista Activity Windows (Ventanas de actividad)](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Puede hacer siguiente hello:

* Ordenar en orden ascendente.
* Ordenar en orden descendente.
* Filtrar por uno o más valores (Ready [Listo], Waiting [En espera], etc.).

Cuando se especifica un filtro en una columna, verá el botón de filtro de hello habilitado para esa columna, lo que indica que los valores de hello en columna de hello son valores filtrados.

![Filtrar una columna de la lista de ventanas de la actividad de Hola](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Puede usar Hola mismos filtros de tooclear de la ventana emergente. tooclear todos los filtros de la lista de ventanas de la actividad de hello, haga clic en el botón Borrar filtro de hello en la barra de comandos de Hola.

![Borrar todos los filtros de la lista de ventanas de la actividad de Hola](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Acciones por lotes
### <a name="rerun-selected-activity-windows"></a>Volver a ejecutar las ventanas de actividad seleccionadas
Seleccione una ventana de actividad, haga clic en hello flecha abajo en el primer botón de barra de comandos hello y seleccione **vuelva a ejecutar** / **vuelva a ejecutar con en dirección ascendente de canalización**. Cuando selecciona hello **vuelva a ejecutar con en dirección ascendente de canalización** opción, vuelve a ejecutar todas las ventanas de nivel superior de actividad.
    ![Volver a ejecutar una ventana de actividad](./media/data-factory-monitor-manage-app/ReRunSlice.png)

También puede seleccionar varias ventanas de la actividad en la lista de Hola y volver a ejecutarlos en hello mismo tiempo. Conviene ventanas de la actividad toofilter acuerdos con el estado de hello (por ejemplo: **error**)--y, a continuación, vuelva a ejecutar windows de la actividad de hello no se pudo después de corregir el problema de Hola que provoca Hola actividad windows toofail. Vea Hola pasos de la sección para obtener más información acerca del filtrado de windows de la actividad en la lista de Hola.  

### <a name="pauseresume-multiple-pipelines"></a>Pausar y reanudar varias canalizaciones
Puede realizar una selección múltiple canalizaciones de dos o más mediante el uso de la tecla Ctrl de Hola. Puede usar los botones de barra de comandos de hello (que se resaltan en el rectángulo rojo Hola Hola después de la imagen) toopause/reanudar ellos.

![Pausar y reanudar en la barra de comandos de Hola](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Creación de alertas
Hola **alertas** página le permite crear una alerta y ver, editar o eliminar las alertas existentes. También puede habilitar o deshabilitar una alerta. toosee Hola página de alertas, haga clic en hello **alertas** ficha.

![Pestaña Alertas](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate una alerta
1. Haga clic en **Agregar alerta** tooadd una alerta. Vea hello **detalles** página.

    ![Crear alertas: página de detalles](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Especificar hello **nombre** y **descripción** alerta hello y haga clic en **siguiente**. Debería ver Hola **filtros** página.

    ![Crear alertas: página de filtros](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Seleccione hello **eventos**, **estado**, y **subestado** (opcional) que desea toocreate un servicio de factoría de datos de alertas para y haga clic en **siguiente**. Debería ver Hola **destinatarios** página.

    ![Crear alertas: página de destinatarios](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Seleccione hello **los administradores de suscripciones de correo electrónico** opción o escriba una **correo electrónico de administrador adicional**y haga clic en **finalizar**. Debería ver la alerta de hello en la lista de Hola.

    ![Lista de alertas](./media/data-factory-monitor-manage-app/AlertsList.png)

En la lista de alertas de hello, utilice los botones de Hola que están asociados a Hola alerta tooedit/delete/deshabilitar/Habilitar una alerta.

### <a name="eventstatussubstatus"></a>Evento/estado/subestado
Hello tabla siguiente proporciona Hola lista de eventos disponibles y Estados (y sub-estados).

| Nombre del evento | Estado | Subestado |
| --- | --- | --- |
| Ejecución de actividad iniciada |Started |Iniciando |
| Ejecución de actividad finalizada |Correcto |Correcto |
| Ejecución de actividad finalizada |Con error |Asignación de recursos errónea<br/><br/>Ejecución con errores<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| Creación de clúster de HDI a petición iniciada |Started |-|
| Creación correcta de clúster de HDI a petición |Correcto |-|
| Clúster de HDI a petición eliminado |Correcto |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, eliminar o deshabilitar una alerta

Usar hello después tooedit botones (resaltados en rojo), eliminar o deshabilitar una alerta.

![Botones de alertas](./media/data-factory-monitor-manage-app/AlertButtons.png)
