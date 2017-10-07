---
title: "Hola aaaDeploy servicio de movilidad de recuperación de sitio con el DSC de automatización de Azure | Documentos de Microsoft"
description: "Describe cómo implementar toouse DSC de automatización de Azure tooautomatically servicio de movilidad de recuperación del sitio de Azure de Hola y el agente de Azure para VM de VMware y tooAzure de replicación del servidor físico"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Implementar el servicio de movilidad Hola con DSC de automatización de Azure para la replicación de máquina virtual
En Operations Management Suite, le proporcionamos una completa solución de copia de seguridad y recuperación ante desastres que puede usar como parte de su plan de continuidad empresarial.

Comenzamos este viaje con Hyper-V usando Réplica de Hyper-V. Pero tenemos toosupport expandido una instalación heterogénea porque los clientes tienen varias plataformas e hipervisores en sus nubes.

Si se ejecutan cargas de trabajo de VMware o en servidores físicos de hoy en día, un servidor de administración ejecuta todos de hello componentes de Azure Site Recovery en su entorno toohandle Hola comunicación y datos de replicación con Azure, cuando Azure es el destino.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Implementar el servicio de movilidad de recuperación de sitio de hello mediante DSC de automatización
Para comenzar, vamos a realizar un desglose rápido de lo que hace este servidor de administración.

servidor de administración de Hello ejecuta varios roles de servidor. Uno de ellos es el de *configuración*, que coordina la comunicación y administra los procesos de replicación y recuperación de datos.

Además, Hola *proceso* rol actúa como una puerta de enlace de replicación. Esta función recibe datos de replicación de máquinas de origen protegido, optimiza con almacenamiento en caché, la compresión y cifrado y, a continuación, lo envía tooan cuenta de almacenamiento de Azure. Una de las funciones hello para el rol de proceso de hello también es toopush instalación de las máquinas de tooprotected de servicio de movilidad de Hola y realizar la detección automática de máquinas virtuales de VMware.

Si se produce una conmutación por recuperación de Azure, Hola *destino maestro* rol controlará los datos de replicación de hello como parte de esta operación.

Para las máquinas de hello protegido, se basan en Hola *servicio de movilidad*. Este componente está implementado tooevery máquina (VM de VMware o servidor físico) que desea tooreplicate tooAzure. Captura escrituras de datos en la máquina de Hola y reenvía el servidor de administración de toohello (rol de proceso).

Cuando está trabajando con la continuidad del negocio, es importante toounderstand las cargas de trabajo, la infraestructura y los componentes de hello implicados. A continuación, puede cumplir los requisitos de hello para el objetivo de tiempo de recuperación (RTO) y objetivo de punto de recuperación (RPO). En este contexto, servicio de movilidad de hello es tooensuring clave que se protegen las cargas de trabajo tal como se esperaría.

De modo que, ¿cómo puede garantizar, de una forma optimizada, que dispone de una configuración protegida confiable con la ayuda de algunos componentes de Operations Management Suite?

Este artículo proporciona un ejemplo de cómo puede usar Azure Automation estado configuración deseado (DSC), junto con la recuperación del sitio, tooensure que:

* servicio de movilidad de Hola y el agente de máquina virtual de Azure son máquinas con Windows toohello implementados que desea tooprotect.
* servicio de movilidad de Hola y el agente de máquina virtual de Azure siempre se ejecutan cuando Azure es el destino de replicación de Hola.

## <a name="prerequisites"></a>Requisitos previos
* Un programa de instalación de repositorio toostore Hola necesario
* Un tooregister de frase de contraseña de repositorio toostore Hola necesario con el servidor de administración de Hola

  > [!NOTE]
  > Se genera una frase de contraseña única para cada servidor de administración. Si va a toodeploy varios servidores de administración, tiene tooensure ese Hola correcto de frase de contraseña se almacena en el archivo de hello passphrase.txt.
  >
  >
* Windows Management Framework (WMF) 5.0 instalado en los equipos de Hola que quiere tooenable de protección (un requisito para DSC de automatización)

  > [!NOTE]
  > Si desea que las máquinas de DSC para Windows toouse que tienen WMF 4.0 instalado, vea la sección de hello [DSC de uso en entornos desconectados](## Use DSC in disconnected environments).
  

servicio de movilidad de Hello puede instalarse mediante la línea de comandos de Hola y acepta varios argumentos. Por eso necesita los archivos binarios de toohave Hola (después de extraer el programa de instalación) y almacenarlas en un lugar donde se pueden recuperar mediante el uso de una configuración DSC.

## <a name="step-1-extract-binaries"></a>Paso 1: Extracción de los archivos binarios
1. archivos de hello tooextract que necesite para este programa de instalación, busque toohello después de directorio en el servidor de administración:

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    En esta carpeta, debería ver un archivo MSI denominado:

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    Usar hello después de instalador de hello tooextract de comando:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Seleccione todos los archivos y enviarlos tooa de carpeta comprimida (zip).

Ahora dispone de los archivos binarios de Hola que necesita el programa de instalación de tooautomate Hola de hello servicio de movilidad mediante el uso de DSC de automatización.

### <a name="passphrase"></a>Frase de contraseña
A continuación, deberá toodetermine donde desea tooplace esta carpeta comprimida. Puede usar una cuenta de almacenamiento de Azure, como se muestra más adelante, toostore Hola frase de contraseña que necesita para el programa de instalación de Hola. agente de Hello, a continuación, se registrará con el servidor de administración de hello como parte del proceso de Hola.

frase de contraseña de Hola que obtuvo al implementar el servidor de administración de Hola se puede guardar archivo de texto tooa como passphrase.txt.

Coloque la carpeta comprimida de Hola y Hola frase de contraseña en un contenedor dedicado Hola cuenta de almacenamiento de Azure.

![Ubicación de la carpeta](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Si prefiere tookeep estos archivos en un recurso compartido de la red, puede hacerlo. Solo necesita tooensure que el recurso de hello DSC que se va a usar más adelante tiene acceso y puede obtener el programa de instalación de Hola y la frase de contraseña.

## <a name="step-2-create-hello-dsc-configuration"></a>Paso 2: Crear la configuración de hello DSC
el programa de instalación de Hello depende de WMF 5.0. Para hello máquina toosuccessfully aplicar configuración de Hola a través de DSC de automatización, WMF 5.0 debe toobe presente.

entorno de Hello usa Hola siguiente configuración de DSC de ejemplo:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
configuración Hola hará lo siguiente de hello:

* variables de Hello indicará configuración Hola donde tooget Hola binarios para el servicio de movilidad de Hola y el agente de máquina virtual de Azure de hello, que tooget Hola frase de contraseña, y donde toostore Hola de salida.
* Hello configuración importará recursos xPSDesiredStateConfiguration DSC de hello, para que pueda utilizar `xRemoteFile` archivos de hello toodownload del repositorio de Hola.
* configuración de Hello creará un directorio donde desea que los archivos binarios de toostore Hola.
* recurso archive de Hello extraerá archivos Hola desde la carpeta comprimida de Hola.
* recursos de instalación de paquete de Hola instalarán el servicio de movilidad de Hola de hello UNIFIEDAGENT. Instalador del archivo EXE con argumentos específicos de Hola. (las variables de Hola que construcción argumentos Hola necesitan tooreflect toobe cambiar su entorno).
* paquete de Hello AzureAgent recurso instalará el agente de máquina virtual de Azure hello, que se recomienda en cada máquina virtual que se ejecuta en Azure. agente de máquina virtual de Azure de Hello también hace posible tooadd extensiones toohello VM después de la conmutación por error.
* Hello servicio o los recursos garantizará que Hola relacionados con servicios de movilidad y hello servicios de Azure se ejecutan siempre.

Guardar configuración de hello como **ASRMobilityService**.

> [!NOTE]
> Recuerde tooreplace hello CSIP en el servidor de administración reales de configuración tooreflect hello, para que se conectará correctamente hello agente y usará la frase de contraseña correcta Hola.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Paso 3: Cargar tooAutomation DSC
Como configuración de hello DSC realizados importará un módulo de recursos de DSC necesario (xPSDesiredStateConfiguration), deberá tooimport ese módulo en la automatización de antes de cargar la configuración de hello DSC.

Inicio de sesión tooyour cuenta de automatización, examinar demasiado**activos** > **módulos**y haga clic en **explorar la galería**.

Aquí puede buscar Hola módulo e importarlo tooyour cuenta.

![Importar el módulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Cuando termine esta operación, ir tooyour máquina donde haya módulos de Azure Resource Manager Hola instalados y continuar tooimport Hola que acaba de crear la configuración de DSC.

### <a name="import-cmdlets"></a>Cmdlets de importación
En PowerShell, inicie sesión en tooyour suscripción de Azure. Modificar el entorno de hello cmdlets tooreflect y capturar información de su cuenta de automatización en una variable:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Cargar configuración de hello tooAutomation DSC mediante Hola siguiente cmdlet:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Compilar Hola configuración de DSC de automatización
A continuación, necesita toocompile Hola una configuración de DSC de automatización, para que pueda empezar tooregister nodos tooit. Lograr ejecutando Hola siguiente cmdlet:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Esto puede tardar unos minutos, ya que básicamente está implementando el servicio de extracción de DSC de hello configuración toohello hospedado.

Después de compilar la configuración de hello, puede recuperar información del trabajo de hello mediante PowerShell (Get-AzureRmAutomationDscCompilationJob) o mediante el uso de hello [portal de Azure](https://portal.azure.com/).

![Recuperar trabajo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Ahora ha publicado y cargar su tooAutomation de configuración de DSC DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Paso 4: Incorporar máquinas tooAutomation DSC
> [!NOTE]
> Uno de los requisitos previos de Hola para completar este escenario es que los equipos de Windows se actualizan con la versión más reciente de Hola de WMF. Puede descargar e instalar la versión correcta de Hola para su plataforma de hello [centro de descarga de](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Ahora creará una metaconfig de DSC que se aplicarán tooyour nodos. toosucceed con esto, debe tooretrieve Hola extremo hello y dirección URL de clave principal para la cuenta de automatización seleccionada en Azure. Puede encontrar estos valores en **claves** en hello **toda la configuración de** hoja para hello cuenta de automatización.

![Valores clave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

En este ejemplo, tiene un servidor físico de Windows Server 2012 R2 que desea que tooprotect mediante el uso de Site Recovery.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Busque todas las operaciones de cambio de nombre de archivo en el registro de hello pendientes
Antes de iniciar tooassociate Hola server con el punto de conexión de hello DSC de automatización, se recomienda que compruebe las todas las operaciones de cambio de nombre de archivo en el registro de hello pendientes. Puede impedir que el programa de instalación de hello finalizase debido tooa reinicio pendiente.

Ejecute hello después tooverify de cmdlet que no hay ningún reinicio pendiente en el servidor de hello:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Si esto se muestra vacía, son tooproceed Aceptar. De lo contrario, se debe solucionar este problema, reinicie el equipo servidor de Hola durante una ventana de mantenimiento.

configuración de Hola de tooapply en servidor hello, iniciar PowerShell Integrated Scripting Environment (ISE) de Hola y ejecute la siguiente secuencia de comandos de Hola. Esto es básicamente una configuración local DSC que se indique a tooregister de motor de administrador de configuración Local de hello con hello servicio DSC de automatización y recuperar la configuración específica de hello (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Esta configuración producirá Hola Administrador de configuración Local tooregister motor propio con DSC de automatización. También determinará cómo debe funcionar el motor de hello, lo que debería hacer si no hay un desfase de la configuración (ApplyAndAutoCorrect) y cómo debe continuar con la configuración de hello si es necesario reiniciar.

Después de ejecutar este script, nodo de hello debe comenzar tooregister con DSC de automatización.

![Registro del nodo en curso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Si vuelve toohello portal de Azure, puede ver ese nodo recién registrado Hola ahora ha aparecido en el portal de Hola.

![Nodo registrado en el portal de Hola](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

En el servidor de hello, puede ejecutar Hola después PowerShell tooverify de cmdlet que Hola nodo se ha registrado correctamente:

```powershell
Get-DscLocalConfigurationManager
```

Después de configuración de hello toohello extraída y aplicado server, puede comprobarlo ejecutando Hola siguiente cmdlet:

```powershell
Get-DscConfigurationStatus
```

salida de Hello muestra que ese servidor Hola extrajo correctamente su configuración:

![Salida](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Además, el programa de instalación del servicio de movilidad de hello tiene su propio registro que se pueden encontrar en *SystemDrive*\ProgramData\ASRSetupLogs.

¡Ya está! Ahora ha implementado y registrado el servicio de movilidad Hola Hola máquina que tooprotect mediante el uso de Site Recovery. DSC se asegurará de que siempre están ejecutando los servicios de hello necesario.

![Implementación correcta](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Después de que el servidor de administración de hello detecta una implementación correcta hello, puede configurar la protección y habilitar la replicación en la máquina de hello mediante el uso de Site Recovery.

## <a name="use-dsc-in-disconnected-environments"></a>Uso de DCS en entornos desconectados
Si los equipos no están conectado toohello Internet, puede confiar en DSC toodeploy y configurar el servicio de movilidad de hello en las cargas de trabajo de Hola que desea tooprotect.

Puede crear una instancia de su propio servidor de extracción de DSC en su entorno tooessentially proporcionar Hola mismas capacidades que obtendrá de DSC de automatización. Es decir, los clientes de hello extraerá configuración hello (después de registrarla) toohello DSC extremo. Sin embargo, otra opción es toomanually inserción Hola DSC configuración tooyour las máquinas, tanto local como remotamente.

Tenga en cuenta que en este ejemplo, es un parámetro agregado hello como nombre del equipo. archivos remotos Hola se encuentran en un recurso compartido remoto debe ser accesible por máquinas de Hola que desea tooprotect. final de Hello del script de Hola aplica la configuración de hello y, a continuación, inicia el equipo de destino de tooapply Hola DSC configuración toohello.

### <a name="prerequisites"></a>Requisitos previos
Asegúrese de que ese módulo de PowerShell de hello xPSDesiredStateConfiguration está instalado. Para las máquinas de Windows está instalado WMF 5.0, puede instalar el módulo xPSDesiredStateConfiguration de hello ejecutando Hola siguiente cmdlet de equipos de destino de hello:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

También puede descargar y guardar el módulo de Hola por si tuviera que toodistribute lo tooWindows máquinas que tengan WMF 4.0. Ejecute este cmdlet en una máquina donde esté presente PowerShellGet (WMF 5.0):

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

También para WMF 4.0, asegúrese de que hello [actualización de Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) se instala en equipos de Hola.

Hello configuración siguiente se puede insertar tooWindows máquinas que tengan WMF 5.0 y WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Si desea tooinstantiate su propio servidor de extracción de DSC en sus capacidades de hello toomimic de red corporativa que puede obtener de DSC de automatización, vea [configurar un servidor de extracción de DSC web](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Opcional: Implementación de una configuración de DSC mediante una plantilla de Azure Resource Manager
En este artículo se centra en cómo puede crear su propio tooautomatically de configuración de DSC implementar hello Azure VM Agent--y servicio de movilidad de Hola y asegúrese de que se ejecutan en máquinas de Hola que desea tooprotect. También tenemos una plantilla de administrador de recursos de Azure que implementará esta DSC configuración tooa cuenta nueva o existente automatización de Azure. plantilla de Hello usará activos de automatización de toocreate de parámetros de entrada que contienen las variables de Hola para su entorno.

Después de implementar la plantilla de hello, simplemente puede consultar toostep 4 en esta guía tooonboard las máquinas.

plantilla Hola hará lo siguiente de hello:

1. Usar una cuenta existente de Automatización o crear una nueva
2. Aceptar los parámetros de entrada de:
   * ASRRemoteFile--ubicación hello en el que haya almacenado el programa de instalación del servicio de movilidad de Hola
   * ASRPassphrase: ubicación de Hola que haya almacenado el archivo de hello passphrase.txt
   * ASRCSEndpoint--dirección IP de saludo del servidor de administración
3. Importar el módulo de PowerShell de hello xPSDesiredStateConfiguration
4. Crear y compilar la configuración de DSC Hola

Hola todos los pasos anteriores se realizará en el orden correcto de hello, para que pueda comenzar la incorporación de las máquinas para la protección.

plantilla de Hello, con instrucciones para la implementación, se encuentra en [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Implementar la plantilla de hello mediante PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Pasos siguientes
Después de implementar los agentes de servicios de movilidad de hello, también puede [habilitar la replicación](site-recovery-vmware-to-azure.md) para las máquinas virtuales de Hola.
