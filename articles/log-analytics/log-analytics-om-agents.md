---
title: "aaaConnect Operations Manager tooLog análisis | Documentos de Microsoft"
description: "toomaintain la inversión realizada en System Center Operations Manager y usar amplió las capacidades con análisis de registros, puede integrar Operations Manager con el área de trabajo OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Conectar Operations Manager tooLog análisis
toomaintain la inversión realizada en System Center Operations Manager y usar amplió las capacidades con análisis de registros, puede integrar Operations Manager con el área de trabajo OMS.  Esto permite aprovechar las oportunidades de Hola de OMS mientras continúa toouse Operations Manager para:

* Continuar supervisar el estado de saludo de los servicios de TI con Operations Manager
* Mantener la integración con sus soluciones ITSM compatibles con la administración de incidentes y problemas
* Administrar el ciclo de vida de Hola de local tooon agentes implementados y máquinas virtuales de nube pública IaaS que se supervisa con Operations Manager

Integración con System Center Operations Manager agrega estrategia de operaciones de servicio de valor tooyour usando Hola velocidad y eficacia de OMS en recopilar, almacenar y analizar datos de Operations Manager.  OMS le ayuda a correlacionar y trabajo hacia la identificación de los errores de Hola de problemas y así como la exposición las repeticiones para admitir el proceso de administración de problema existente.   Hola flexibilidad de hello motor tooexamine rendimiento, eventos y alerta de datos de búsqueda, con paneles muy completos y reporting capacidades tooexpose estos datos de maneras significativas, muestra intensidad Hola OMS aporta en como complemento para Operations Manager.

agentes de Hello reporting toohello grupo de administración de Operations Manager recopilan datos de los servidores basados en orígenes de datos de análisis de registros de Hola y soluciones que haya habilitado en su suscripción de OMS.  Según se ha habilitado la solución de hello, datos de estas soluciones son que cualquiera envía directamente desde un servidor de administración de Operations Manager toohello OMS servicio web, o debido a Hola volumen de datos recopilados en el sistema administrado con agente hello, se envían directamente servicio web de hello agente tooOMS. servidor de administración de Hello reenvía los datos de OMS Hola directamente toohello OMS web servicio; nunca se escribe toohello OperationsManager o OperationsManagerDW base de datos.  Cuando un servidor de administración pierde la conexión con el servicio web OMS de hello, almacena en caché datos de hello localmente hasta que la comunicación se restablece con OMS.  Si el servidor de administración de hello está sin conexión debido a mantenimiento tooplanned o una interrupción imprevista, otro servidor de administración en el grupo de administración de hello reanuda la conectividad con OMS.  

Hello siguiente diagrama muestra conexión Hola entre servidores de administración de Hola y los agentes en un grupo de administración de System Center Operations Manager y OMS, incluidos los puertos y la dirección de Hola.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de la red Internet, los servidores de administración pueden ser información de configuración de tooreceive de tooconnect configurado toohello puerta de enlace de OMS y enviar los datos recopilados dependiendo de la solución de Hola que ha habilitado.  Para obtener más información y pasos acerca de cómo tooconfigure su toocommunicate de grupo de administración de Operations Manager a través de un servicio de OMS toohello de puerta de enlace de OMS, consulte [conectar tooOMS de equipos con hello puerta de enlace de OMS](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Requisitos del sistema
Antes de comenzar, revise Hola después tooverify detalles cumplen los requisitos previos.

* OMS solo admite Operations Manager 2016, Operations Manager 2012 SP1 UR6 y versiones posteriores y Operations Manager 2012 R2 UR2 y versiones posteriores.  Se agregó compatibilidad con proxy en Operations Manager 2012 SP1 UR7 y Operations Manager 2012 R2 UR3.
* Todos los agentes de Operations Manager deben cumplir los requisitos mínimos de compatibilidad. Asegúrese de que los agentes son actualización mínima Hola, en caso contrario, puede producir un error de tráfico de agente de Windows y muchos errores podrían llenar el registro de sucesos de Operations Manager de Hola.
* Una suscripción de OMS.  Para más información, consulte [Introducción a Log Analytics](log-analytics-get-started.md).

### <a name="network"></a>Red
información de Hola por debajo de la lista Hola proxy y firewall de información de configuración requerida para el agente de Operations Manager de hello, servidores de administración y toocommunicate de la consola de operaciones con OMS.  El tráfico de cada componente es saliente desde el servicio OMS de toohello de red.     

|Recurso | Número de puerto| Omitir inspección de HTTP|  
|---------|------|-----------------------|  
|**Agent**|||  
|\*.ods.opinsights.azure.com| 443 |yes|  
|\*.oms.opinsights.azure.com| 443|Sí|  
|\*blob.core.windows.net| 443|Sí|  
|\*.azure-automation.net| 443|Sí|  
|**Servidor de administración**|||  
|\*.service.opinsights.azure.com| 443||  
|\*blob.core.windows.net| 443| Sí|  
|\*.ods.opinsights.azure.com| 443| Sí|  
|*.azure-automation.net | 443| Sí|  
|**TooOMS de consola de Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 y 443||  
|\*.microsoft.com| 80 y 443||  
|\*.microsoftonline.com| 80 y 443||  
|\*.mms.microsoft.com| 80 y 443||  
|login.windows.net| 80 y 443||  


## <a name="connecting-operations-manager-toooms"></a>Conectar tooOMS de Operations Manager
Realizar Hola según serie de pasos tooconfigure su tooone de tooconnect del grupo de administración de Operations Manager de las áreas de trabajo OMS.

1. En la consola de Operations Manager de hello, seleccione hello **administración** área de trabajo.
2. Expanda el nodo de Operations Management Suite hello y haga clic en **conexión**.
3. Haga clic en hello **registrar tooOperations Management Suite** vínculo.
4. En hello **Asistente para incorporación a Operations Management Suite: autenticación** página, escriba la dirección de correo electrónico de Hola o el número de teléfono y la contraseña de cuenta de administrador de Hola que está asociado a su suscripción de OMS y haga clic en  **Inicie sesión en**.
5. Una vez haya autenticado correctamente, en hello **Asistente para incorporación a Operations Management Suite: seleccionar área de trabajo** , es solicita tooselect el área de trabajo OMS.  Si tiene más de un área de trabajo, seleccione Hola área de trabajo que desee tooregister con grupo de administración de Operations Manager Hola de lista desplegable de hello y, a continuación, haga clic en **siguiente**.
   
   > [!NOTE]
   > Operations Manager solo admite un área de trabajo de OMS a la vez. conexión de Hola y equipos de Hola que eran tooOMS registrados con el área de trabajo anterior Hola se quitan de OMS.
   > 
   > 
6. En hello **Asistente para incorporación a Operations Management Suite: resumen** página, confirme la configuración predeterminada y si son correctos, haga clic en **crear**.
7. En hello **Asistente para incorporación a Operations Management Suite: finalizar** página, haga clic en **cerrar**.

### <a name="add-agent-managed-computers"></a>Adición de equipos administrados por agente
Después de configurar la integración con el área de trabajo OMS, esto solo establece una conexión con OMS, no se recopilan datos de los agentes de hello tooyour grupo de administración de informes. Esto no será posible hasta que configure qué equipos específicos administrados por agente recopilan los datos para Log Analytics. Puede seleccionar objetos de equipo de hello individualmente o puede seleccionar un grupo que contenga objetos de equipo de Windows. No puede seleccionar un grupo que contenga instancias de otra clase, como discos lógicos o bases de datos SQL.

1. Consola de Operations Manager Hola abra y seleccione hello **administración** área de trabajo.
2. Expanda el nodo de Operations Management Suite hello y haga clic en **conexión**.
3. Haga clic en hello **agregar un grupo de equipos** vínculo situado bajo Hola acciones encabezado Hola lado derecho del panel de Hola.
4. Hola **búsqueda de equipos** cuadro de diálogo, puede buscar equipos o grupos supervisados por Operations Manager. Seleccione tooOMS tooonboard equipos o grupos, haga clic en **agregar**y, a continuación, haga clic en **Aceptar**.

Puede ver los equipos y grupos configuran toocollect datos del nodo de equipos administrados de hello en Operations Management Suite en hello **administración** área de trabajo de la consola del operador Hola.  Desde aquí puede agregar o quitar equipos y grupos según sea necesario.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Configurar el proxy de OMS en la consola del operador Hola
Realizar Hola siguientes pasos si es un servidor proxy interno entre el grupo de administración de Hola y el servicio web de OMS.  Esta configuración se administra centralmente desde el grupo de administración de Hola y los sistemas distribuidos tooagent administrados se incluyen en los datos de toocollect de ámbito de Hola para OMS.  Esto es beneficioso para cuando determinadas soluciones omisión los datos de envío y de servidor de administración de hello directamente tooOMS servicio web.

1. Consola de Operations Manager Hola abra y seleccione hello **administración** área de trabajo.
2. Expanda Operations Management Suite y haga clic en **Conexiones**.
3. Hola vista conexión a OMS, haga clic en **configurar servidor Proxy**.
4. En **Asistente para Operations Management Suite: servidor Proxy** página, seleccione **usar un tooaccess de servidor proxy hello Operations Management Suite**, y a continuación, escriba la dirección URL de hello con número de puerto de hello, por ejemplo, http:// corpproxy:80 y, a continuación, haga clic en **finalizar**.

Si el servidor proxy requiere autenticación, lleve a cabo los pasos del siguiente hello tooconfigure credenciales y la configuración que necesitan los equipos de toomanaged toopropagate que informa tooOMS Hola grupo de administración.

1. Consola de Operations Manager Hola abra y seleccione hello **administración** área de trabajo.
2. En **RunAs Configuration**, seleccione **Perfiles**.
3. Abra hello **System Center como Proxy del perfil Advisor** perfil.
4. Hola Ejecutar Asistente para perfiles, haga clic en toouse de agregar una cuenta de ejecución. Puede crear una [cuenta de ejecución](https://technet.microsoft.com/library/hh321655.aspx) o usar una existente. Esta cuenta debe toohave toopass de permisos suficientes a través del servidor de proxy de Hola.
5. tooset Hola toomanage de cuenta, elija **una clase seleccionada, un grupo o un objeto**, haga clic en **seleccionar...** y, después, en **Agrupar**. Hola tooopen **grupo búsqueda** cuadro.
6. Busque y seleccione **Microsoft System Center Advisor Monitoring Server Group**(Grupo de servidores de supervisión de Microsoft System Center Advisor).  Haga clic en **Aceptar** después de seleccionar Hola de hello grupo tooclose **grupo búsqueda** cuadro.
7. Haga clic en **Aceptar** tooclose hello **agregar una cuenta de ejecución** cuadro.
8. Haga clic en **guardar** toocomplete Hola asistente y guarde los cambios.

Después de que se crea la conexión de Hola y configurar los agentes se recopilar y notificar datos tooOMS, hello siguiente configuración se aplica en el grupo de administración de hello, no necesariamente en orden:

* Cuenta de ejecución de Hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** se crea.  Está asociado con el perfil de identificación de hello **Microsoft System Center Advisor ejecutar como Blob de perfil** y está destinado a dos clases - **servidor de recopilación de** y **el grupo de administración de Operations Manager** .
* Se crean dos conectores.  en primer lugar se denomina Hello **Microsoft.SystemCenter.Advisor.DataConnector** y se configura automáticamente con una suscripción que reenvíe todas las alertas generadas desde instancias de todas las clases de tooOMS de grupo de administración de hello registro Análisis. es el segundo conector de Hello **Advisor Connector**, que es responsable de comunicarse con el servicio web OMS y uso compartido de datos.
* Agentes y grupos que seleccionó toocollect datos en el grupo de administración de Hola se agrega toohello **grupo de servidor de supervisión de Microsoft System Center Advisor**.

## <a name="management-pack-updates"></a>Actualizaciones del módulo de administración
Una vez completada la configuración, grupo de administración de Operations Manager Hola establece una conexión con hello servicio OMS.  servidor de administración de Hola se sincroniza con el servicio web de Hola y recibir información de configuración actualizada en forma de Hola de módulos de administración para soluciones de Hola que haya habilitado que se integran con Operations Manager.   Operations Manager busca actualizaciones para estos módulos de administración y los descargará e importará automáticamente cuando estén disponibles.  Hay dos reglas en particular que controlan este comportamiento:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -actualiza los módulos de administración de OMS base Hola. Se ejecuta cada 12 horas de forma predeterminada.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** : Actualiza los módulos de administración de las soluciones habilitados en el área de trabajo. Se ejecuta cada cinco (5) minutos de forma predeterminada.

Puede invalidar estas dos reglas tooeither evitar descarga automática mediante la deshabilitación o modificar la frecuencia de hello para la frecuencia con hello servidor de administración se sincroniza con OMS toodetermine si un nuevo módulo de administración está disponible y se debe descargar.  Siga los pasos de hello [cómo tooOverride una regla o Monitor](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **frecuencia** parámetro con un valor en segundos toochange Hola programación de sincronización o modificar hello **habilitado**  reglas de hello toodisable de parámetros.  Hola de destino reemplaza tooall objetos de clase grupo de administración de Operations Manager.

Si desea toocontinue siguiendo el proceso de control de cambio existente para controlar las versiones del módulo de administración en el grupo de administración de producción, puede deshabilitar las reglas de Hola y habilitarlas durante determinadas horas cuando se permiten las actualizaciones. Si tiene un desarrollo o un grupo de administración de preguntas y respuestas en su entorno y tiene conectividad toohello Internet, puede configurar ese grupo de administración con un toosupport de área de trabajo OMS este escenario.  Esto permite tooreview y evaluar las versiones iterativo Hola Hola OMS de módulos de administración antes de liberarlos al grupo de administración de producción.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Cambiar un tooa de grupo de Operations Manager nueva área de trabajo de OMS
1. Inicie sesión en la suscripción de OMS tooyour y cree un área de trabajo en [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Consola de Operations Manager Hola abierto con una cuenta que sea miembro del rol de administradores de Operations Manager de Hola y Hola seleccione **administración** área de trabajo.
3. Expanda Operations Management Suite y seleccione **Conexiones**.
4. Seleccione hello **volver a configurar la operación Management Suite** vínculo en hello middle-lado del panel de Hola.
5. Siga hello **Asistente para incorporación a Operations Management Suite** y escriba el número de teléfono o dirección de correo electrónico de Hola y la contraseña de cuenta de administrador de Hola que está asociado a la nueva área de trabajo OMS.
   
   > [!NOTE]
   > Hola **Asistente para incorporación a Operations Management Suite: seleccionar área de trabajo** página presenta Hola área de trabajo existente que está en uso.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Validación de la integración de Operations Manager con OMS
Hay varias maneras diferentes, puede comprobar que la integración de administrador de OMS tooOperations es correcta.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>integración de tooconfirm Hola portal de OMS
1. En el portal de OMS de hello, haga clic en hello **configuración** icono
2. Seleccione **Connected Sources**(Orígenes conectados).
3. En la tabla Hola Hola sección de System Center Operations Manager, debería ver el nombre de Hola Hola del grupo de administración aparecen con el número de Hola de agentes y el estado cuando se recibió por última vez datos.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Hola Nota **Id. de área de trabajo** valor bajo Hola izquierda de la página de configuración de Hola.  Lo validará con el grupo de administración de Operations Manager a continuación.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>integración de tooconfirm desde la consola del operador Hola
1. Consola de Operations Manager Hola abra y seleccione hello **administración** área de trabajo.
2. Seleccione **módulos de administración** y Hola **buscar:** cuadro de texto escriba **Advisor** o **Intelligence**.
3. Según soluciones de Hola que haya habilitado, verá un módulo de administración correspondiente aparece en los resultados de búsqueda de Hola.  Por ejemplo, si ha habilitado la solución de administración de alertas de hello, el módulo de administración de hello administración de alertas de Microsoft System Center Advisor es en la lista de Hola.
4. De hello **supervisión** ver, navegar toohello **Suite\Health estado de las operaciones de administración** vista.  Seleccione un servidor de administración con hello **estado del servidor de administración** panel y en hello **vista de detalle** panel confirmar el valor de hello para la propiedad **URI del servicio de autenticación** coincide con el Id. de área de trabajo de OMS Hola.
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Eliminación de la integración con OMS
Cuando ya no se requiere la integración entre el grupo de administración de Operations Manager y el área de trabajo OMS, hay varios pasos necesarios tooproperly remove Hola conexión y configuración de grupo de administración de Hola. Hello procedimiento siguiente tiene actualizar el área de trabajo OMS mediante la eliminación de referencia de Hola de su grupo de administración, elimine los conectores de OMS hello y, a continuación, elimine los módulos de administración compatible con OMS.   

Módulos de administración de soluciones de Hola que haya habilitado que se integran con Operations Manager y Hola administración módulos toosupport requiere integración con hello servicio OMS no se puede eliminar fácilmente Hola grupo de administración.  Esto es porque algunos de los módulos de administración de OMS Hola tienen dependencias en otros módulos de administración relacionados.  módulos de administración de toodelete si tuviera una dependencia en otros módulos de administración, descargue el script de Hola [quitar un módulo de administración con dependencias](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) desde el centro de scripts de TechNet.  

1. Abra Hola Shell de comandos de Operations Manager con una cuenta que sea miembro del rol de administradores de Operations Manager Hola.
   
    > [!WARNING]
    > Asegúrese de dispone de ningún módulo de administración personalizado con hello word asesor o IntelligencePack en nombre de hello antes de continuar, en caso contrario Hola pasos eliminarlos Hola grupo de administración.
    > 

2. Hola shell desde línea de comandos, escriba`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Después, escriba `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. módulos de los módulos de administración restantes que tienen una dependencia en otra administración de System Center Advisor tooremove, usar script de Hola *RecursiveRemove.ps1* descargó desde Hola centro de scripts de TechNet.  
 
    > [!NOTE]
    > No elimine los módulos de administración de Microsoft System Center Advisor o Microsoft System Center Advisor interno de Hola.  
    >  

5. Abra la consola de operador de Operations Manager de hello con una cuenta que sea miembro del rol de administradores de Operations Manager Hola.
6. En **administración**, seleccione hello **módulos de administración** nodo y en hello **buscar:** , escriba **Advisor** y compruebe Hola módulos de administración siguientes se importan de todos modos en el grupo de administración:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Internal
7. En el portal de OMS de hello, haga clic en hello **configuración** icono.
8. Seleccione **Connected Sources**(Orígenes conectados).
9. En la tabla Hola Hola sección de System Center Operations Manager, verá el nombre de Hola Hola grupo de administración que desee tooremove de área de trabajo de Hola.  En la columna de hello **últimos datos**, haga clic en **quitar**.  
   
    > [!NOTE]
    > Hola **quitar** vínculo no estará disponible hasta que transcurridos 14 días si no hay ninguna actividad ha detectado en el grupo de administración conectado Hola.  
    > 

10. Aparecerá una ventana que le pide que tooconfirm que desea tooproceed con la eliminación de Hola.  Haga clic en **Sí** tooproceed. 

toodelete Hola dos conectores - Microsoft.SystemCenter.Advisor.DataConnector y el conector de Advisor, Guardar script de PowerShell de hello siguiente tooyour equipo y se ejecutan con hello en los ejemplos siguientes:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> equipo Hola de que ejecutar este script, si no es un servidor de administración, debe tener el shell de comandos de Operations Manager Hola instalado, dependiendo de la versión de Hola de su grupo de administración.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

En hello futuras si tiene intención de volver a conectar el grupo tooan OMS área de trabajo administración, debe importar toore hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` archivo de módulo de administración del paquete acumulativo de actualizaciones más reciente de hello aplica tooyour grupo de administración.  Puede encontrar este archivo en hello `%ProgramFiles%\Microsoft System Center 2012` o hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` carpeta.

## <a name="next-steps"></a>Pasos siguientes
funcionalidad de tooadd y recopilar datos, vea [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).


