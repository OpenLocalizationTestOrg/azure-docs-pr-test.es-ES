---
title: "aaaConnect Windows equipos tooAzure análisis de registros | Documentos de Microsoft"
description: "Este artículo muestra los equipos con Windows hello pasos tooconnect hello en su toohello de infraestructura local servicio de análisis de registros mediante el uso de una versión personalizada de hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Conecta el servicio de análisis de registros de toohello de equipos de Windows en Azure

Este artículo muestra los pasos de hello tooconnect equipos de Windows en las áreas de trabajo de tooOMS de infraestructura local mediante el uso de una versión personalizada de hello Microsoft Monitoring Agent (MMA). Es necesario tooinstall y conectar a agentes para todos los equipos de Hola que desea tooonboard en orden para ellos el servicio de análisis de registros de toosend datos toohello y tooview y actuar en los datos. Cada agente puede informar toomultiple áreas de trabajo.

Puede instalar los agentes a través del programa de instalación, a través de la línea de comandos o utilizando Configuración de estado deseado (DSC) en Automatización de Azure.  

>[!NOTE]
Para máquinas virtuales que se ejecutan en Azure, puede simplificar la instalación utilizando hello [extensión de máquina virtual](log-analytics-azure-vm-extension.md).

En los equipos con conectividad a Internet, el agente de hello usa Hola conexión toohello Internet toosend datos tooOMS. Para equipos que no tiene conectividad a Internet, puede usar un servidor proxy o hello [puerta de enlace de OMS](log-analytics-oms-gateway.md).

Conectar su tooOMS de equipos de Windows es sencillo con tres sencillos pasos:

1. Descargar el archivo de instalación de agente de Hola Hola portal de OMS
2. Instalar a agente de hello mediante el método de Hola que elija
3. Configurar el agente de Hola o agregar áreas de trabajo adicionales, si es necesario

Hello siguiente diagrama muestra hello relación entre los equipos de Windows y OMS después de que haya instalado y configurado los agentes.

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de la red Internet, puede configurar su toohello de tooconnect equipos puerta de enlace de OMS. Para obtener más información y pasos acerca de cómo tooconfigure su toocommunicate de servidores a través de un servicio de OMS toohello de puerta de enlace de OMS, consulte [conectar tooOMS de equipos con hello puerta de enlace de OMS](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Requisitos del sistema y configuración necesaria
Antes de instalar o implementar a agentes, revise Hola después tooensure detalles cumple los requisitos de Hola.

- Hola OMS MMA solo se puede instalar en equipos que ejecutan Windows Server 2008 SP 1 o posterior o Windows 7 SP1 o posterior.
- Necesita una suscripción de Azure.  Para más información, consulte [Introducción a Log Analytics](log-analytics-get-started.md).
- Cada equipo de Windows debe ser capaz de tooconnect toohello Internet mediante HTTPS o toohello puerta de enlace de OMS. Esta conexión puede ser directa a través de un proxy, o a través de hello puerta de enlace de OMS.
- Puede instalar Hola OMS MMA en equipos independientes, servidores y máquinas virtuales. Si desea tooconnect tooOMS de máquinas virtuales hospedadas en Azure, consulte [tooLog de máquinas virtuales de Azure conectarse análisis](log-analytics-azure-vm-extension.md).
- agente de Hello debe toouse el puerto TCP 443 de distintos recursos.

### <a name="network"></a>Red

Para Windows agentes tooconnect tooand caja registradora con servicio OMS hello, deben tener acceso a los recursos toonetwork, incluidos los números de puerto de Hola y direcciones URL de dominio.

- Para los servidores proxy, debe tooensure que Hola recursos se configuran en la configuración del agente de servidor de proxy correspondiente.
- Para los firewalls que restringen el acceso toohello Internet, se o los ingenieros de red necesitan tooconfigure su tooOMS de acceso de firewall toopermit. No es necesario realizar ninguna acción en la configuración del agente.

Hello en la tabla siguiente muestra los recursos necesarios para la comunicación.

>[!NOTE]
>Algunos de hello recursos siguientes mencionan a visión operativa, lo que era un nombre para el análisis de registros anterior.

| Recurso del agente | Puertos | Omitir inspección de HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sí |
| *.oms.opinsights.azure.com | 443 | Sí |
| *.blob.core.windows.net | 443 | Sí |
| *.azure-automation.net | 443 | Sí |



## <a name="download-hello-agent-setup-file-from-oms"></a>Descargar el archivo de instalación de agente de Hola de OMS
1. Portal de OMS de hello, en hello **Introducción** página, haga clic en hello **configuración** icono.  Haga clic en hello **orígenes conectados** ficha situada en la parte superior de Hola.  
    ![Pestaña Connected Sources (Orígenes conectados)](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Haga clic en **servidores Windows** y, a continuación, haga clic en **Download Windows Agent** archivo de tooyour aplicables equipo procesador tipo toodownload hello el programa de instalación.
3. En hello derecha de **Id. de área de trabajo**, haga clic en el icono de copiar de Hola y pegue el identificador hello en el Bloc de notas.
4. En hello derecha de **Primary Key**, haga clic en el icono de copiar de Hola y pegue la clave de hello en el Bloc de notas.     

## <a name="install-hello-agent-using-setup"></a>Instalación de agentes de hello mediante el programa de instalación
1. Ejecutar agente de hello tooinstall el programa de instalación en un equipo que desea toomanage.
2. En la página de bienvenida de hello, haga clic en **siguiente**.
3. En la página términos de licencia de hello, lea el contrato de licencia de hello y, a continuación, haga clic en **acepto**.
4. En la página de la carpeta de destino de hello, cambiar o mantener la carpeta de instalación predeterminada de hello y, a continuación, haga clic en **siguiente**.
5. En la página de opciones de instalación del agente de hello, puede elegir tooconnect Hola agente tooAzure Log Analytics (OMS), Operations Manager, o puede dejar que las opciones de hello en blanco si desea que tooconfigure Hola agente más tarde. Haga clic en **Siguiente**.   
    - Si ha elegido tooconnect tooAzure Log Analytics (OMS), pegue hello **Id. de área de trabajo** y **clave de área de trabajo (clave principal)** que ha copiado en el Bloc de notas en el procedimiento anterior de hello y, a continuación, haga clic en  **Siguiente**.  
        ![pegar identificador del área de trabajo y clave principal](./media/log-analytics-windows-agents/connect-workspace.png)
    - Si ha elegido tooconnect tooOperations Manager, escriba Hola **nombre del grupo de administración**, **Management Server** nombre, y **puerto del servidor de administración**y, a continuación, haga clic en **Siguiente**. En la página de la cuenta de acción del agente de hello, elija la cuenta de sistema Local de Hola o una cuenta de dominio local y, a continuación, haga clic en **siguiente**.  
        ![configuración del grupo de administración](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. En la página Listo tooInstall hello, revise las selecciones realizadas y, a continuación, haga clic en **instalar**.
7. En hello completó correctamente la configuración de página, haga clic en **finalizar**.
8. Cuando haya finalizado, Hola **Microsoft Monitoring Agent** aparece en **el Panel de Control**. Puede revisar la configuración no existe y comprobar que el agente Hola esté conectado tooOperational visión (OMS). Cuando tooOMS conectados, Hola agente muestra un mensaje que indica: **Hola Microsoft Monitoring Agent se ha conectado correctamente toohello servicio de Microsoft Operations Management Suite.**

## <a name="configure-proxy-settings"></a>Configuración de los valores de proxy

Puede usar Hola después de la configuración de proxy de procedimiento tooconfigure de hello Microsoft Monitoring Agent mediante el Panel de Control. Necesita toouse este procedimiento para cada servidor. Si tiene muchos servidores que necesite tooconfigure, le resultará más fácil toouse una secuencia de comandos tooautomate este proceso. Si es así, vea el procedimiento siguiente hello [tooconfigure configuración de proxy para Microsoft Monitoring Agent mediante un script de Hola](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>configuración de proxy de tooconfigure de hello Microsoft Monitoring Agent mediante el Panel de Control
1. Abra el **Panel de control**.
2. Abra **Microsoft Monitoring Agent**.
3. Haga clic en hello **configuración de Proxy** ficha.  
    ![Pestaña Configuración de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Seleccione **utilizar un servidor proxy** y escriba la dirección URL de Hola y número de puerto, si hay alguna toohello necesario, de forma similar en el ejemplo se muestran. Si el servidor proxy requiere autenticación, escriba Hola username y password tooaccess Hola servidor proxy.


### <a name="verify-agent-connectivity-toooms"></a>Compruebe tooOMS de conectividad del agente

Puede comprobar fácilmente si los agentes se comunican con OMS mediante Hola siguiendo el procedimiento:

1.  En el equipo de hello con el agente de Windows hello, abra el Panel de Control.
2.  Abra Microsoft Monitoring Agent.
3.  Haga clic en la pestaña de hello Azure Log Analytics (OMS).
4.  En la columna de estado de hello, debería ver que ese agente Hola conectado correctamente el servicio de Operations Management Suite toohello.

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>configuración de proxy de tooconfigure para Microsoft Monitoring Agent mediante un script de Hola
Copie Hola siguiente ejemplo, actualícelo con el entorno de tooyour específico de información, guárdelo con una extensión de nombre de archivo PS1 y, a continuación, ejecute el script de Hola en cada equipo que se conecta directamente a servicio OMS toohello.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Instalar a agente de hello mediante la línea de comandos de Hola
- Modificar y, a continuación, usar hello siguiente a agente de hello tooinstall de ejemplo mediante la línea de comandos de Hola. ejemplo de Hola realiza una instalación completamente silenciosa.

    >[!NOTE]
    Si desea tooupgrade un agente, debe toouse Hola análisis de registros de API de scripting. Vea Hola siguiente sección tooupgrade un agente.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

agente de Hello utiliza IExpress como su Self-extractor con hello `/c` comando. Puede ver los modificadores de línea de comandos de hello en [modificadores de línea de comandos para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) y, a continuación, actualización Hola toosuit de ejemplo a sus necesidades.

|Opciones específicas de MMA                   |Notas         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = el área de trabajo de configurar Hola agente tooreport tooa                |
|OPINSIGHTS_WORKSPACE_ID                | Id. de área de trabajo (guid) para hello tooadd de área de trabajo                    |
|OPINSIGHTS_WORKSPACE_KEY               | Tooinitially de uso clave de área de trabajo se autentican con el área de trabajo de Hola |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Especificar el entorno de nube de Hola donde se encuentra el área de trabajo de Hola <br> 0 = nube comercial de Azure (valor predeterminado) <br> 1= Azure Government |
|OPINSIGHTS_PROXY_URL               | URI de hello proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Nombre de usuario tooaccess un proxy autenticado |
|OPINSIGHTS_PROXY_PASSWORD               | Contraseña tooaccess un proxy autenticado |

>[!NOTE]
límite de longitud de línea de comandos de hello posicionamiento de tooavoid de IExpress, instalar agente Hola con ningún área de trabajo configurado y, a continuación, utilizar una configuración de tooset de secuencia de comandos para el área de trabajo de Hola.

>[!NOTE]
Si se produce un `Command line option syntax error.` al usar hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parámetro, puede usar Hola siguiente solución alternativa:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Incorporación de un área de trabajo mediante un script
Agregar un área de trabajo con API de scripting del agente de análisis de registros de Hola Hola siguiente ejemplo:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd un área de trabajo en Azure para el gobierno de Estados Unidos, Hola de uso después de ejemplo de secuencia de comandos:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Si ha usado la línea de comandos de Hola o script previamente tooinstall o configurar el agente de hello, `EnableAzureOperationalInsights` ha sido reemplazado por `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Instalar a agente de hello con DSC en automatización de Azure

Puede usar Hola sigue la secuencia de comandos en el ejemplo se tooinstall Hola agente con DSC en automatización de Azure. ejemplo de Hola instala Hola agente de 64 bits, identificado por hello `URI` valor. También puede utilizar la versión de 32 bits de hello reemplazando el valor del URI Hola. Hola URI para ambas versiones son:

- Agente de Windows de 64 bits: https://go.microsoft.com/fwlink/?LinkId=828603
- Agente de Windows de 32 bits: https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
Este ejemplo de script y procedimiento no actualizará un agente existente.

1. Importar hello xPSDesiredStateConfiguration módulo de DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) en automatización de Azure.  
2.  En Azure Automation, cree los recursos de variable *OPSINSIGHTS_WS_ID* y *OPSINSIGHTS_WS_KEY*. Establecer *OPSINSIGHTS_WS_ID* Id. de área de trabajo de análisis de registros de OMS tooyour y establecer *OPSINSIGHTS_WS_KEY* toohello clave principal del área de trabajo.
3.  Usar hello siguiente script y guárdelo como MMAgent.ps1
4.  Modificar y, a continuación, usar hello siguiente a agente de Hola de tooinstall de ejemplo con DSC en automatización de Azure. Importar MMAgent.ps1 en automatización de Azure mediante la interfaz de automatización de Azure de Hola o el cmdlet.
5.  Asignar una configuración de toohello de nodo. Dentro de 15 minutos, nodo de hello comprueba su configuración y Hola MMA se inserta el nodo toohello.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Obtener el valor de ProductId más reciente de Hola

Hola `ProductId value` en hello MMAgent.ps1 script es la versión del agente tooeach único. Cuando se publica una versión actualizada de cada agente, Hola ProductId valor cambia. Por lo tanto, cuando Hola ProductId cambia de hello futuro, puede averiguar la versión de agente de hello mediante un script sencillo. Una vez que la última versión del agente Hola instalado en un servidor de prueba, puede usar Hola siguiente valor de ProductId de secuencia de comandos tooget Hola instalado. Con el último valor de ProductId hello, puede actualizar el valor de Hola Hola MMAgent.ps1 script.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Configuración de un agente de forma manual o incorporación de áreas de trabajo adicionales
Si instaló a agentes pero no los ha configurado o si desea que las áreas de trabajo de hello agente tooreport toomultiple, puede usar Hola después información tooenable un agente o volver a configurarlo. Después de configurar al agente de hello, se registrará con el servicio del agente de Hola y le proporcionará información de configuración necesaria y módulos de administración que contienen información de la solución.

1. Después de instalar Microsoft Monitoring Agent hello, abra **el Panel de Control**.
2. Abra **Microsoft Monitoring Agent** y, a continuación, haga clic en hello **Azure Log Analytics (OMS)** ficha.   
3. Haga clic en **agregar** tooopen hello **agregar un área de trabajo de análisis de registro** cuadro.
4. Hola pegar **Id. de área de trabajo** y **clave de área de trabajo (clave principal)** que ha copiado en el Bloc de notas en un procedimiento anterior para el área de trabajo de Hola que desee tooadd y, a continuación, haga clic en **Aceptar**.  
    ![configurar Visión operativa](./media/log-analytics-windows-agents/add-workspace.png)

Después de recopilar datos de los equipos supervisados por el agente de hello, número de Hola de equipos supervisados por OMS aparecerá en el portal de OMS de hello en hello **orígenes conectados** ficha **configuración** como  **Servidores conectados**.


## <a name="toodisable-an-agent"></a>toodisable un agente
1. Después de instalar el agente de hello, abra **el Panel de Control**.
2. Abra el agente de supervisión de Microsoft y, a continuación, haga clic en hello **Azure Log Analytics (OMS)** ficha.
3. Seleccione un área de trabajo y haga clic en **Quitar**. Repita este paso para el resto de áreas de trabajo.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Opcionalmente, configure el grupo de administración de agentes tooreport tooan Operations Manager

Si usa Operations Manager en su infraestructura de TI, también puede utilizar el agente MMA Hola como un agente de Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>grupo de administración de Operations Manager de tooconfigure MMA agentes tooreport tooan
1.  En el equipo de Hola donde está instalado el agente de hello, abra **el Panel de Control**.  
2.  Abra **Microsoft Monitoring Agent** y, a continuación, haga clic en hello **Operations Manager** ficha.  
    ![Pestaña Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)
3.  Si los servidores de Operations Manager tienen integración con Active Directory, haga clic en **Actualizar automáticamente asignaciones de grupos de administración desde AD DS**.
4.  Haga clic en **agregar** tooopen hello **agregar un grupo de administración** cuadro de diálogo.  
    ![Agregar un grupo de administración de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  En **nombre del grupo de administración** cuadro, escriba un nombre Hola de su grupo de administración.
6.  Hola **servidor de administración principal** cuadro, escribe el nombre del equipo de Hola Hola principal del servidor de administración.
7.  Hola **puerto del servidor de administración** cuadro de número de puerto TCP de tipo hello.
8.  En **cuenta de acción del agente**, elija la cuenta de sistema Local de Hola o una cuenta de dominio local.
9.  Haga clic en **Aceptar** tooclose hello **agregar un grupo de administración** cuadro de diálogo y, a continuación, haga clic en **Aceptar** tooclose hello **propiedades de agente de supervisión de Microsoft**cuadro de diálogo.


## <a name="next-steps"></a>Pasos siguientes

- [Adición de soluciones de análisis de registros desde la Galería de soluciones de hello](log-analytics-add-solutions.md) tooadd funcionalidad y recopilar datos.
