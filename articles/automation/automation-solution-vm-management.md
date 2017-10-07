---
title: "aaaStart o detener las máquinas virtuales durante la solución de poca actividad [vista previa] | Documentos de Microsoft"
description: "soluciones de administración de máquinas virtuales de Hello inicia y detiene las máquinas virtuales de administrador de recursos de Azure según una programación y supervisar de forma proactiva de análisis de registros."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Inicio o detención de máquinas virtuales fuera de las horas de trabajo [versión preliminar] en Automation

Hola iniciar o detener las máquinas virtuales durante la solución de poca actividad [vista previa] se inicia y detiene las máquinas virtuales de Azure Resource Manager según una programación definida por el usuario y proporciona una visión general de éxito de Hola de trabajos de automatización de Hola que iniciar y detener las máquinas virtuales con OMS Análisis de registros.  

## <a name="prerequisites"></a>Requisitos previos

- Hola runbooks trabajar con un [cuenta de identificación de Azure](automation-offering-get-started.md#authentication-methods).  Hola cuenta de ejecución es el método de autenticación de hello preferida ya que utiliza autenticación de certificado en lugar de una contraseña que puede expirar o cambian con frecuencia.  

- Esta solución sólo puede administrar las máquinas virtuales que se encuentran en hello misma suscripción que donde reside la cuenta de automatización de Hola.  

- Esta solución solo implementa toohello después de regiones de Azure - sudeste de Australia, este de EE., sudeste de Asia y Europa occidental.  Hola runbooks que administran la programación de la máquina virtual de hello puede tener como destino las máquinas virtuales en cualquier región.  

- notificaciones de correo electrónico toosend cuando Hola iniciar y detener runbooks de la máquina virtual completa, es necesaria una suscripción de clase empresarial de Office 365.  

## <a name="solution-components"></a>Componentes de soluciones

Esta solución consta de hello recursos que se va a importar y agregan la cuenta de automatización tooyour siguientes.

### <a name="runbooks"></a>Runbooks

Runbook | Description|
--------|------------|
CleanSolution-MS-Mgmt-VM | Este runbook quitará todos los contenidos recursos y las programaciones cuando salen de solución de hello toodelete desde su suscripción.|  
SendMailO365-MS-Mgmt | Este Runbook envía un correo electrónico a través de Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Este runbook está previsto toostart las máquinas virtuales (ambos clásico y ARM en función de las máquinas virtuales) que reside en una determinada lista de grupos de recursos de Azure.
StopByResourceGroup-MS-Mgmt-VM | Este runbook está previsto toostop las máquinas virtuales (ambos clásico y ARM en función de las máquinas virtuales) que reside en una determinada lista de grupos de recursos de Azure.|
<br>

### <a name="variables"></a>variables

Variable | Description|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Especifica si los Runbooks StartByResourceGroup-MS-Mgmt-VM y StopByResourceGroup-MS-Mgmt-VM pueden enviar notificaciones por correo electrónico cuando finalicen.  Seleccione **True** tooenable y **False** toodisable alertas de correo electrónico. El valor predeterminado es **False**.| 
Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Escriba VM nombres toobe excluida de la operación de administración; Separe los nombres con cuadro sin espacios en blanco. Los valores distinguen mayúsculas de minúsculas y admiten caracteres comodín (asterisco).|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que se puede anexa toohello a partir del cuerpo de mensaje de correo electrónico de Hola.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica el nombre de Hola de hello cuenta de automatización que contenga un runbook de correo electrónico de Hola.  **No modifique esta variable.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Especifica el nombre de Hola de runbook de correo electrónico de Hola.  Se utiliza por hello StartByResourceGroup-MS-Mgmt-VM y correo electrónico de StopByResourceGroup-MS-Mgmt-VM runbooks toosend.  **No modifique esta variable.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica el nombre de Hola Hola del grupo de recursos que contenga un runbook de correo electrónico de Hola.  **No modifique esta variable.**|
StartByResourceGroup SendMailO365 EmailSubject MS Mgmt | Especifica el texto hello para la línea de asunto Hola de correo electrónico de Hola.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica Hola destinatarios de correo electrónico de Hola.  Separe los diversos nombres mediante punto y coma (;).|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Escriba VM nombres toobe excluida de la operación de administración; Separe los nombres con cuadro sin espacios en blanco. Los valores distinguen mayúsculas de minúsculas y admiten caracteres comodín (asterisco).  El valor predeterminado (asterisco) incluirá todos los grupos de recursos de suscripción de Hola.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica la suscripción de Hola que contiene toobe de máquinas virtuales administrada por esta solución.  Debe tratarse de Hola misma suscripción donde reside la cuenta de automatización de esta solución Hola.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Escriba VM nombres toobe excluida de la operación de administración; Separe los nombres con cuadro sin espacios en blanco. Los valores distinguen mayúsculas de minúsculas y admiten caracteres comodín (asterisco).|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que se puede anexa toohello a partir del cuerpo de mensaje de correo electrónico de Hola.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica el nombre de Hola de hello cuenta de automatización que contenga un runbook de correo electrónico de Hola.  **No modifique esta variable.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica el nombre de Hola Hola del grupo de recursos que contenga un runbook de correo electrónico de Hola.  **No modifique esta variable.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Especifica el texto hello para la línea de asunto Hola de correo electrónico de Hola.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica Hola destinatarios de correo electrónico de Hola.  Separe los diversos nombres mediante punto y coma (;).|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Escriba VM nombres toobe excluida de la operación de administración; Separe los nombres con cuadro sin espacios en blanco. Los valores distinguen mayúsculas de minúsculas y admiten caracteres comodín (asterisco).  El valor predeterminado (asterisco) incluirá todos los grupos de recursos de suscripción de Hola.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica la suscripción de Hola que contiene toobe de máquinas virtuales administrada por esta solución.  Debe tratarse de Hola misma suscripción donde reside la cuenta de automatización de esta solución Hola.|  
<br>

### <a name="schedules"></a>Programaciones

Schedule | Description|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Programación de runbook de StartByResourceGroup, que lleva a cabo el inicio de Hola de las máquinas virtuales administradas por esta solución. Cuando se crea, el valor predeterminado es zona de horaria tooUTC.|
StopByResourceGroup-Schedule-MS-Mgmt | Programación de runbook de StopByResourceGroup, que realiza el cierre de Hola de las máquinas virtuales administradas por esta solución. Cuando se crea, el valor predeterminado es zona de horaria tooUTC.|

### <a name="credentials"></a>Credenciales

Credential: | Description|
-----------|------------|
O365Credential | Especifica un correo electrónico toosend de cuenta de usuario de válido Office 365.  Se requiere únicamente si la variable SendMailO365-IsSendEmail-MS-Mgmt se establece demasiado**True**.

## <a name="configuration"></a>Configuración

Realizar Hola siguiendo los pasos tooadd Hola iniciar o detener las máquinas virtuales durante horas de poca actividad [vista previa] solución tooyour cuenta de automatización y, a continuación, configurar soluciones de hello variables toocustomize Hola.

1. En la pantalla de inicio Hola Hola portal de Azure, seleccione hello **Marketplace** icono.  Si el icono de hello ya no está anclado tooyour-pantalla Inicio, en panel de navegación izquierdo de hello, seleccione **nuevo**.  
2. En la hoja de Marketplace de hello, escriba **iniciar VM** en el cuadro de búsqueda de Hola y solución de hello, a continuación, seleccione **iniciar o detener las máquinas virtuales durante horas de poca actividad [vista previa]** en los resultados de búsqueda de Hola.  
3. Hola **iniciar o detener las máquinas virtuales durante horas de poca actividad [vista previa]** hoja para hello seleccionado solución, revise la información de resumen de hello y, a continuación, haga clic en **crear**.  
4. Hola **Agregar solución** hoja aparece donde son tooconfigure solicitadas Hola solución antes de importarlo en su suscripción de automatización.<br><br> ![Hoja Agregar solución de administración de VM](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  En hello **Agregar solución** hoja, seleccione **área de trabajo** y aquí se selecciona un área de trabajo OMS que está vinculado toohello misma suscripción de Azure que Hola cuenta de automatización está en o crea una nueva área de trabajo OMS.  Si no tiene un área de trabajo OMS, puede seleccionar **crear nueva área de trabajo** y en hello **área de trabajo de OMS** hoja realizar siguiente hello: 
   - Especifique un nombre para el nuevo hello **área de trabajo de OMS**.
   - Seleccione un **suscripción** toolink tooby selección de lista desplegable de hello si predeterminado Hola seleccionado no es adecuado.
   - Para **Grupo de recursos**, puede crear un nuevo grupo de recursos o seleccionar uno existente.  
   - Seleccione una **ubicación**.  Actualmente existen Hola únicas ubicaciones a las proporcionadas para la selección de **sudeste de Australia**, **UU**, **sudeste de Asia**, y **Europa occidental**.
   - Seleccione un **plan de tarifa**.  solución de Hola se ofrece en dos niveles: liberar y niveles de pago de OMS.  nivel gratis Hello tiene un límite de cantidad de Hola de datos recopilados diariamente, período de retención y minutos de tiempo de ejecución del trabajo de runbook.  Hola OMS niveles de pago no tiene un límite de cantidad de Hola de datos recopilados diariamente.  

        > [!NOTE]
        > Aunque Hola independiente niveles de pago se muestra como una opción, no es aplicable.  Si selecciona y continuar con la creación de hello de esta solución en su suscripción, se producirá un error.  Esto se solucionará cuando se lance oficialmente la solución.<br>Si usa esta solución, solo se emplearán minutos de trabajo e ingesta de registros de automatización.  solución de Hello no agrega entorno adicional de tooyour de nodos OMS.  

6. Después de proporcionar información de hello necesario en hello **área de trabajo OMS** hoja, haga clic en **crear**.  Mientras se comprueba la información de Hola y crea el área de trabajo de hello, puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola.  Se devolverá toohello **Agregar solución** hoja.  
7. En hello **Agregar solución** hoja, seleccione **cuenta de automatización**.  Si va a crear una nueva área de trabajo OMS, será necesario tooalso crear una nueva cuenta de automatización que se asociará con hello nueva área de trabajo OMS especificado anteriormente, incluida su suscripción de Azure, el grupo de recursos y la región.  Puede seleccionar **crear una cuenta de automatización** y en hello **cuenta de automatización agregar** hoja, proporciona Hola siguiente: 
  - Hola **nombre** , escriba el nombre de Hola de hello cuenta de automatización.

    Todas las demás opciones se rellenan automáticamente basándose en el área de trabajo OMS de hello seleccionado y no se puede modificar estas opciones.  Una cuenta de identificación de Azure es método de autenticación predeterminado de Hola de runbooks Hola incluidos en esta solución.  Una vez que pulses **Aceptar**, se validan las opciones de configuración de Hola y Hola cuenta de automatización se crea.  Puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola. 

    Si no, puede seleccionar una cuenta de ejecución de Automation existente.  Tenga en cuenta que cuenta Hola seleccionada ya no puede ser vinculado tooanother área de trabajo OMS, en caso contrario, un mensaje se presentan en hello hoja tooinform.  Si ya está vinculado, se necesita tooselect una cuenta de identificación de automatización diferente o cree uno nuevo.<br><br> ![Automatización de la cuenta ya vinculado tooOMS área de trabajo](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Por último, en hello **Agregar solución** hoja, seleccione **configuración** hello y **parámetros** aparece hoja.  En hello **parámetros** hoja, se le pedirá que:  
   - Especificar hello **nombres de grupo de recursos de destino**, que es un nombre de grupo de recursos que contiene toobe de máquinas virtuales administrada por esta solución.  Puede especificar más de un nombre y separarlos con punto y coma (los valores distinguen mayúsculas de minúsculas).  Se admite el uso de un carácter comodín si desea tootarget máquinas virtuales en todos los grupos de recursos en la suscripción de Hola.
   - Seleccione un **programación** que es una repetición de fecha y hora para hello de detener la máquina virtual en hello y a partir de grupos de recursos de destino.  De forma predeterminada, programación de hello es zona de horaria toohello configurado UTC y no está disponible al seleccionar una región diferente.  Si lo desea zona de horaria específica de tooconfigure Hola programación tooyour después de configurar la solución de hello, consulte [modificar programación de inicio y cierre de hello](#modifying-the-startup-and-shutdown-schedule) a continuación.    

10. Una vez haya completado el saludo inicial configuración necesaria para la solución de hello, seleccione **crear**.  Se validarán toda la configuración y, a continuación, tratará de solución de hello toodeploy en su suscripción.  Este proceso puede tardar unos segundos toocomplete y se puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola. 

## <a name="collection-frequency"></a>Frecuencia de recopilación

Datos de flujo de trabajo y de registro del trabajo automatización es ingestión en el repositorio de OMS Hola cada cinco minutos.  

## <a name="using-hello-solution"></a>Uso de solución de Hola

Cuando se agrega la solución de administración de máquinas virtuales de hello, en su Hola de área de trabajo OMS **StartStopVM vista** mosaico se agregarán tooyour panel de OMS.  Este icono muestra un recuento y una representación gráfica de los trabajos de runbooks de hello para la solución de Hola que han iniciado y se han completado correctamente.<br><br> ![Icono de StartStopVM View](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png) (Ver StartStopVM) de administración de VM  

En su cuenta de automatización, puede acceder y administrar soluciones de hello seleccionando hello **soluciones** icono y, a continuación, desde hello **soluciones** hoja, selección de solución de hello **[inicio-Stop-VM Área de trabajo]** de lista de Hola.<br><br> ![Lista de soluciones de Automation](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Si selecciona solución Hola aparecerá hello **Start-Stop-VM [Workspace]** hoja de la solución, donde puede revisar detalles importantes como hello **StartStopVM** disponer en mosaico, al igual que en el área de trabajo OMS, que muestra un recuento y una representación gráfica de los trabajos de runbooks de hello para la solución de Hola que han iniciado y se han completado correctamente.<br><br> ![Hoja de solución de máquina virtual de Automation](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Desde aquí también puede abrir el área de trabajo OMS y realizar análisis de registros de trabajos de Hola de otras.  Simplemente haga clic en **toda la configuración de**y en hello **configuración** hoja, seleccione **inicio rápido** y, a continuación, en hello **inicio rápido** seleccione hoja  **Portal de OMS**.   Se abrirá una nueva pestaña o una nueva sesión de explorador y se presentará el espacio de trabajo de OMS asociado con la cuenta de Automation y la suscripción.  


### <a name="configuring-e-mail-notifications"></a>Configuración de notificaciones por correo electrónico

las notificaciones de correo electrónico de tooenable cuando hello iniciar y detienen runbooks de máquina virtual completa, necesitará toomodify Hola **O365Credential** de credenciales y como mínimo, Hola siguientes variables:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

Hola tooconfigure **O365Credential** de credenciales, lleve a cabo Hola pasos:

1. En su cuenta de automatización, haga clic en **toda la configuración de** en parte superior de Hola de ventana hello. 
2. En hello **configuración** hoja en la sección de hello **recursos de automatización**, seleccione **activos**. 
3. En hello **activos** hoja, seleccione hello **credencial** icono y de hello **credencial** hoja, seleccione hello **O365Credential**.  
4. Escriba un nombre de usuario de Office 365 válido y una contraseña y, a continuación, haga clic en **guardar** toosave los cambios.  

las variables de hello tooconfigure indicadas anteriormente, lleve a cabo Hola pasos:

1. En su cuenta de automatización, haga clic en **toda la configuración de** en parte superior de Hola de ventana hello. 
2. En hello **configuración** hoja en la sección de hello **recursos de automatización**, seleccione **activos**. 
3. En hello **activos** hoja, seleccione hello **Variables** icono y de hello **Variables** hoja, seleccione variable Hola mencionado anteriormente y, a continuación, modificar su valor siguiente Hola Descripción de lo especificado en hello [variable](##variables) sección anterior.  
4. Haga clic en **guardar** variable toohello de toosave Hola cambios.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Modificar programación de inicio y cierre de Hola

Administrar programación de inicio y cierre de hello en esta solución sigue Hola mismo pasos tal como se describe en [programar un runbook en automatización de Azure](automation-schedules.md).  Recuerde que no se puede modificar la configuración de programación de Hola.  Necesitará toodisable Hola programación existente y, a continuación, cree uno nuevo y, a continuación, vincular toohello **StartByResourceGroup-MS-Mgmt-VM** o **StopByResourceGroup-MS-Mgmt-VM** runbook que desee Hola programar tooapply a.   

## <a name="log-analytics-records"></a>Registros de Log Analytics

Automatización crea dos tipos de registros en el repositorio OMS Hola.

### <a name="job-logs"></a>Registros de trabajo

Propiedad | Description|
----------|----------|
Autor de llamada |  Quién inició la operación de Hola.  Los valores posibles son una dirección de correo electrónico o el sistema para los trabajos programados.|
Categoría | Clasificación de tipo hello de datos.  Para la automatización, el valor de hello es JobLogs.|
CorrelationId | GUID que es el Id. de correlación de trabajo de runbook de Hola Hola.|
JobId | GUID que es el Id. de trabajo de runbook de Hola Hola.|
operationName | Especifica el tipo de saludo de operación realizada en Azure.  Para la automatización, el valor de hello será trabajo.|
resourceId | Especifica el tipo de recurso de hello en Azure.  Para la automatización, el valor de hello es cuenta de automatización de hello asociada Hola runbook.|
ResourceGroup | Especifica el nombre del grupo de recursos de Hola de trabajo de runbook de Hola.|
ResourceProvider | Especifica Hola servicio de Azure que proporciona recursos de hello puede implementar y administrar.  Para la automatización, valor de hello es la automatización de Azure.|
ResourceType | Especifica el tipo de recurso de hello en Azure.  Para la automatización, el valor de hello es cuenta de automatización de hello asociada Hola runbook.|
resultType | estado de Hola de trabajo de runbook de Hola.  Los valores posibles son:<br>Started<br>Stopped<br>Suspended<br>Con error<br>- Correcto|
resultDescription | Describe el estado de resultado del trabajo de runbook de Hola.  Los valores posibles son:<br>- Se inicia el trabajo<br>- Error del trabajo<br>- Trabajo completado|
RunbookName | Especifica el nombre de Hola de runbook de Hola.|
SourceSystem | Especifica el sistema de origen de Hola para los datos de hello enviados.  Para la automatización, será el valor de hello: OpsManager|
StreamType | Especifica el tipo de saludo de evento. Los valores posibles son:<br>- Detallado<br>- Salida<br>error<br>Warning (Advertencia)|
SubscriptionId | Especifica el Id. de suscripción de Hola de trabajo de Hola.
Hora | Fecha y hora cuando se ejecuta el trabajo del runbook de Hola.|


### <a name="job-streams"></a>Transmisiones de trabajo

Propiedad | Description|
----------|----------|
Autor de llamada |  Quién inició la operación de Hola.  Los valores posibles son una dirección de correo electrónico o el sistema para los trabajos programados.|
Categoría | Clasificación de tipo hello de datos.  Para la automatización, el valor de hello es JobStreams.|
JobId | GUID que es el Id. de trabajo de runbook de Hola Hola.|
operationName | Especifica el tipo de saludo de operación realizada en Azure.  Para la automatización, el valor de hello será trabajo.|
ResourceGroup | Especifica el nombre del grupo de recursos de Hola de trabajo de runbook de Hola.|
resourceId | Especifica el identificador de recurso de hello en Azure.  Para la automatización, el valor de hello es cuenta de automatización de hello asociada Hola runbook.|
ResourceProvider | Especifica Hola servicio de Azure que proporciona recursos de hello puede implementar y administrar.  Para la automatización, valor de hello es la automatización de Azure.|
ResourceType | Especifica el tipo de recurso de hello en Azure.  Para la automatización, el valor de hello es cuenta de automatización de hello asociada Hola runbook.|
resultType | se generó el resultado de Hello de trabajo de runbook de hello en el suceso Hola Hola.  Los valores posibles son:<br>- En curso|
resultDescription | Incluye el flujo de salida de hello de runbook de Hola.|
RunbookName | nombre de Hola de runbook de Hola.|
SourceSystem | Especifica el sistema de origen de Hola para los datos de hello enviados.  Para la automatización, el valor de hello será OpsManager|
StreamType | tipo de Hola de flujo de trabajo. Los valores posibles son:<br>progreso<br>- Salida<br>Warning (Advertencia)<br>Error<br>DEBUG<br>- Detallado|
Hora | Fecha y hora cuando se ejecuta el trabajo del runbook de Hola.|

Cuando se realiza cualquier búsqueda de registros que devuelve los registros de categoría de **JobLogs** o **JobStreams**, puede seleccionar hello **JobLogs** o **JobStreams** vista que muestra un conjunto de iconos resumir las actualizaciones de hello devueltas por la búsqueda de Hola.

## <a name="sample-log-searches"></a>Búsquedas de registros de ejemplo

Hello tabla siguiente proporciona búsquedas de registros de ejemplo para registros de trabajos recopilados por esta solución. 

Consultar | Description|
----------|----------|
Buscar trabajos del Runbook StartVM que se hayan completado correctamente | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Buscar trabajos del Runbook StopVM que se hayan completado correctamente | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Mostrar estado del trabajo con el tiempo para los Runbooks StartVM y StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Quitar solución Hola

Si decide que ya no necesita toouse Hola solución cualquier aún más, puede eliminarla del Hola cuenta de automatización.  Al eliminar la solución de hello solo quitará Hola runbooks, no eliminará programaciones de Hola o las variables que se crearon cuando se agregó la solución de Hola.  Esos recursos deberá toodelete manualmente si no se está usando con otros runbooks.  

toodelete Hola solución, lleve a cabo Hola pasos:

1.  En su cuenta de automatización, seleccione hello **soluciones** icono.  
2.  En hello **soluciones** hoja, solución de hello seleccione **Start-Stop-VM [Workspace]**.  En hello **VMManagementSolution [Workspace]** hoja, en haga clic en el menú de hello **eliminar**.<br><br> ![Eliminación de la solución de administración de máquinas virtuales](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  Hola **Eliminar solución** ventana, confirme que desea toodelete Hola solución.
4.  Mientras se comprueba la información de Hola y solución de Hola se elimina, puede realizar un seguimiento de su progreso en **notificaciones** en el menú de Hola.  Se devolverá toohello **VMManagementSolution [Workspace]** hoja después de hello proceso tooremove solución comienza.  

cuenta de automatización de Hola y el área de trabajo OMS no se eliminarán como parte de este proceso.  Si no desea que el área de trabajo de tooretain Hola OMS, deberá toomanually eliminarlo.  Esto puede realizarse también de hello portal de Azure.   En la página de inicio del Hola Hola portal de Azure, seleccione **análisis de registros** y, a continuación, en hello **análisis de registros** hoja, área de trabajo de hello seleccione y haga clic en **eliminar** en el menú de Hola hoja de configuración de área de trabajo de Hola.  
      
## <a name="next-steps"></a>Pasos siguientes

- toolearn más información acerca de cómo las consultas de búsqueda diferente de tooconstruct y revisión Hola automatización trabajo registros con análisis de registros, vea [búsquedas de registro de análisis de registros](../log-analytics/log-analytics-log-searches.md)
- más información acerca de la ejecución de un runbook, cómo toomonitor runbook trabajos y otros detalles técnicos, consulte toolearn [realizar un seguimiento de un trabajo de runbook](automation-runbook-execution.md)
- toolearn más información sobre análisis de registros de OMS y orígenes de la colección de datos, vea [datos de almacenamiento de Azure recopilar en información general de análisis de registros](../log-analytics/log-analytics-azure-storage.md)






   

