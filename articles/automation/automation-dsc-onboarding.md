---
title: "máquinas de aaaOnboarding para la administración mediante el DSC de automatización de Azure | Documentos de Microsoft"
description: "¿Cómo toosetup los equipos para la administración con DSC de automatización de Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Incorporación de máquinas para administrarlas con DSC de Automatización de Azure

## <a name="why-manage-machines-with-azure-automation-dsc"></a>¿Por qué administrar máquinas con DSC de Automatización de Azure?

Al igual que [Configuración de estado deseado de PowerShell](https://technet.microsoft.com/library/dn249912.aspx), Configuración de estado deseado de Automatización de Azure es un servicio de administración de configuración, sencillo pero eficaz, para los nodos de DSC (máquinas físicas y virtuales) en cualquier centro de datos local o en la nube. Permite la escalabilidad en miles de máquinas de forma rápida y sencilla desde una ubicación central y segura. Puede incorporar fácilmente máquinas, asignar configuraciones declarativas de ellos así como ver informes que muestra cada equipo del estado de toohello deseado de cumplimiento especificado. capa de administración de Hello DSC de automatización de Azure es tooDSC qué nivel de administración de la automatización de Azure de hello tooPowerShell de secuencia de comandos. En otras palabras, en hello igual que automatización de Azure le ayuda a administrar los scripts de PowerShell, también le ayuda a administrar las configuraciones de DSC. toolearn más información acerca de las ventajas de hello del uso de DSC de automatización de Azure, consulte [información general de DSC de automatización de Azure](automation-dsc-overview.md).

DSC de automatización de Azure puede ser usado toomanage una variedad de máquinas:

* Azure Virtual Machines (clásico)
* Máquinas virtuales de Azure
* Máquinas virtuales de Amazon Web Services (AWS)
* Máquinas físicas y virtuales con Windows locales o en una nube que no sea Azure/AWS
* Máquinas físicas y virtuales con Linux locales, en Azure o en una nube que no sea Azure

Además, si no estás listo toomanage configuración de la máquina de nube de hello, DSC de automatización de Azure también puede utilizarse como un punto de conexión solo informe. Esto le permite tooset (push) de configuración deseada a través de DSC local y ver detalles informes enriquecidos sobre la conformidad de nodo con hello deseado estado en automatización de Azure.

Hola las secciones siguientes describen cómo se puede incorporar cada tipo de máquina tooAzure DSC de automatización.

## <a name="azure-virtual-machines-classic"></a>Azure Virtual Machines (clásico)

Con DSC de automatización de Azure, puede incorporadas fácilmente máquinas virtuales de Azure (clásico) para la administración de configuración con el portal de Azure de Hola o PowerShell. Bajo el paraguas de Hola y sin que un administrador tenga tooremote en hello VM, Hola extensión de configuración de estado deseado de Azure VM registra Hola VM con el DSC de automatización de Azure. Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, pasos tootrack su progreso o solucionar problemas se proporcionan en hello [ **incorporación de la máquina virtual de Azure de solución de problemas de** ](#troubleshooting-azure-virtual-machine-onboarding)sección más adelante.

### <a name="azure-portal"></a>Azure Portal

Hola [portal de Azure](http://portal.azure.com/), haga clic en **examinar** -> **máquinas virtuales (clásicas)**. Seleccione Hola VM de Windows que desee tooonboard. En la hoja de la máquina virtual Hola panel, haga clic en **toda la configuración de** -> **extensiones** -> **agregar**  ->   **DSC de automatización de Azure** -> **crear**. Escriba hello [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necesarios para el caso de uso, clave de registro de la cuenta de automatización y dirección URL de registro y, opcionalmente, un toohello de tooassign de configuración de nodo VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

dirección URL de registro de hello toofind y clave para la máquina hello tooonboard de cuenta de automatización de hello, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Máquinas virtuales de Azure

DSC de automatización de Azure permite incorporadas fácilmente máquinas virtuales de Azure para la administración de configuración, utilizando Hola portal de Azure, plantillas del Administrador de recursos de Azure o PowerShell. Bajo el paraguas de Hola y sin que un administrador tenga tooremote en hello VM, Hola extensión de configuración de estado deseado de Azure VM registra Hola VM con el DSC de automatización de Azure. Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, pasos tootrack su progreso o solucionar problemas se proporcionan en hello [ **incorporación de la máquina virtual de Azure de solución de problemas de** ](#troubleshooting-azure-virtual-machine-onboarding)sección más adelante.

### <a name="azure-portal"></a>Azure Portal

Hola [portal de Azure](https://portal.azure.com/), navegue toohello cuenta de automatización de Azure donde desee tooonboard las máquinas virtuales. En el panel de la cuenta de automatización de hello, haga clic en **nodos** -> **agregar Azure VM**.

En **seleccionar máquinas virtuales tooonboard**, seleccione uno o más Azure virtual máquinas tooonboard.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

En **configurar datos de registro**, escriba Hola [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necesarios para el caso de uso y, opcionalmente, un toohello de tooassign de configuración de nodo máquina virtual.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Plantillas de Azure Resource Manager

Se pueden implementar máquinas virtuales de Azure e incorporado tooAzure DSC de automatización a través de plantillas del Administrador de recursos de Azure. Vea [configurar una máquina virtual a través de la extensión de DSC y DSC de automatización de Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para una plantilla de ejemplo que onboards un tooAzure VM DSC de automatización existente. toofind Hola clave y el registro de dirección URL de registro tomada como entrada en esta plantilla, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.

### <a name="powershell"></a>PowerShell

Hola [AzureRmAutomationDscNode Register](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet puede ser tooonboard usa máquinas virtuales Hola portal de Azure a través de PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>Máquinas virtuales de Amazon Web Services (AWS)

Puede incorporadas fácilmente máquinas virtuales de Amazon Web Services para la administración de configuración de DSC de automatización de Azure con hello AWS DSC Toolkit. Puede aprender más sobre el Kit de herramientas de hello [aquí](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Máquinas físicas y virtuales con Windows locales o en una nube que no sea Azure/AWS

Máquinas de Windows locales y máquinas de Windows en las nubes distintas de Azure (como Amazon Web Services) también pueden ser incorporadas tooAzure DSC de automatización, siempre y cuando tienen acceso de salida toohello internet, a través de unos pocos pasos sencillos:

1. Crear seguro Hola de versión más reciente de [WMF 5](http://aka.ms/wmf5latest) está instalado en equipos de hello desea tooonboard tooAzure DSC de automatización.
2. Siga las instrucciones de Hola de sección [ **generar DSC metaconfiguraciones** ](#generating-dsc-metaconfigurations) a continuación toogenerate una carpeta que contenga Hola necesarios metaconfiguraciones de DSC.
3. Aplicar de forma remota máquinas de toohello de metaconfiguración Hola DSC de PowerShell que desee tooonboard. **máquina de Hello este comando se ejecuta desde debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Si no se puede aplicar Hola DSC de PowerShell metaconfiguraciones de forma remota, copie la carpeta de metaconfiguraciones de hello en el paso 2 en cada máquina tooonboard. A continuación, llame a **Set-DscLocalConfigurationManager** localmente en cada máquina tooonboard.
5. Uso de hello portal de Azure o cmdlets, compruebe que Hola máquinas tooonboard ahora aparecen como nodos registrado en la cuenta de automatización de Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Máquinas físicas y virtuales con Linux locales, en Azure o en una nube que no sea Azure

Los equipos Linux locales, máquinas de Linux en Azure, y máquinas de Linux en nubes de distintas de Azure también pueden ser incorporadas tooAzure DSC de automatización, siempre y cuando tienen acceso de salida toohello internet, a través de unos pocos pasos sencillos:

1. Crear seguro Hola de versión más reciente de [configuración de estado deseado de PowerShell para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado en equipos de hello desea tooonboard tooAzure DSC de automatización.
2. Si hello [valores predeterminados del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) coincide con el caso de uso, y desea tooonboard máquinas como lo **ambos** la extracción y tooAzure DSC de automatización de informes:

   + En cada tooAzure de tooonboard de máquina de Linux DSC de automatización, use tooonboard Register.py con hello tiene como valor predeterminado en el Administrador de configuración Local de DSC de PowerShell:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind Hola registro clave y el registro de dirección URL para la cuenta de automatización, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.

     Si hello tiene como valor predeterminado en Administrador de configuración Local de DSC de PowerShell **hacer** **no** coincide con el caso de uso, o quiere tooonboard equipos de forma que solo tooAzure DSC de automatización de informes, pero no de extracción configuración o módulos de PowerShell de él, siga los pasos 3 a 6. En caso contrario, continúe directamente toostep 6.

3. Siga las instrucciones de Hola Hola [ **generar DSC metaconfiguraciones** ](#generating-dsc-metaconfigurations) sección toogenerate una carpeta que contiene metaconfiguraciones de DSC de Hola que sea necesitado.
4. Aplicar de forma remota máquinas de toohello de metaconfiguración Hola DSC de PowerShell que desee tooonboard:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

máquina de Hello este comando se ejecuta desde debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado.

1. Si no se puede aplicar hello metaconfiguraciones de DSC de PowerShell de forma remota, para cada tooonboard de máquina Linux, copie máquina de hello metaconfiguración correspondiente toothat de carpeta de hello en el paso 5 en el equipo de Linux Hola. A continuación, llame a `SetDscLocalConfigurationManager.py` localmente en cada equipo Linux desea tooonboard tooAzure DSC de automatización:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Uso de hello portal de Azure o cmdlets, compruebe que Hola máquinas tooonboard ahora aparecen como nodos registrado en la cuenta de automatización de Azure.

## <a name="generating-dsc-metaconfigurations"></a>Generación de metaconfiguraciones de DSC

toogenerically incorporar cualquier máquina tooAzure DSC de automatización, un [metaconfiguración de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) puede ser generado que, cuando aplica, indica el agente de hello DSC en hello máquina toopull desde o tooAzure DSC de automatización de informes. DSC metaconfiguraciones de DSC de automatización de Azure se pueden generar utilizando una configuración de DSC de PowerShell o cmdlets de PowerShell de automatización de Azure de Hola.

> [!NOTE]
> Metaconfiguraciones de DSC contienen Hola secretos necesitados tooonboard una cuenta de automatización para la administración de máquina tooan. Asegúrese de tooproperly seguro proteger cualquier metaconfiguraciones DSC que creas o eliminarlos tras su uso.

### <a name="using-a-dsc-configuration"></a>Uso de una configuración de DSC

1. Abra Hola PowerShell ISE como administrador en un equipo en su entorno local. máquina de Hello debe tener la versión más reciente de Hola de [WMF 5](http://aka.ms/wmf5latest) instalado.
2. Copie Hola siguiente secuencia de comandos localmente. Este script contiene una configuración de DSC de PowerShell para crear metaconfiguraciones y un tookick comando desactivar la creación de hello metaconfiguración.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Rellene la clave de registro de hello y la dirección URL para la cuenta de automatización, así como los nombres de Hola de hello máquinas tooonboard. Todos los demás parámetros son opcionales. toofind Hola registro clave y el registro de dirección URL para la cuenta de automatización, vea hello [ **proteger el registro** ](#secure-registration) sección más adelante.
4. Si desea Hola máquinas tooreport DSC estado información tooAzure DSC de automatización, pero no de extracción configuración o módulos de PowerShell, establezca hello **ReportOnly** tootrue de parámetro.
5. Ejecutar script de Hola. Ahora debería tener una carpeta denominada **DscMetaConfigs** en el directorio de trabajo, que contiene hello metaconfiguraciones de DSC de PowerShell para hello máquinas tooonboard (como administrador):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Uso de cmdlets de automatización de Azure Hola

Si los valores predeterminados de administrador de configuración Local de DSC de PowerShell de hello coincide con el caso de uso, y desea tooonboard máquinas tal que se extraiga de y tooAzure DSC de automatización de informes, Hola cmdlets de automatización de Azure proporcionan un método simplificado de generar Hola DSC metaconfiguraciones necesitado:

1. Abra la consola de PowerShell de Hola o PowerShell ISE como administrador en un equipo en su entorno local.
2. Conectar con el Administrador de recursos de tooAzure **AzureRmAccount agregar**
3. Descargue metaconfiguraciones de DSC de PowerShell de Hola para máquinas Hola desea tooonboard de hello automatización cuenta toowhich que desea que los nodos de tooonboard:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Ahora debería tener una carpeta denominada ***DscMetaConfigs***, que contiene hello metaconfiguraciones de DSC de PowerShell para hello máquinas tooonboard (como administrador):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Registro seguro

Máquinas pueden incorporar de manera segura tooan cuenta de automatización de Azure a través del protocolo de registro de WMF 5 DSC hello, que permite a un nodo tooauthenticate tooa V2 extracción de DSC de PowerShell o informes servidor DSC (incluida la DSC de automatización de Azure). nodo Hola registra el servidor toohello en un **dirección URL de registro**, autenticación mediante un **clave de registro**. Durante el registro, nodo de hello DSC y servidor de extracción de DSC/informes negocian un certificado único para este toouse de nodo de registro posterior a la del servidor de toohello autenticación. Este proceso impide que los nodos incorporados se suplanten entre sí, como por ejemplo si un nodo está afectado y se comporta de forma malintencionada. Después del registro, clave de registro de hello no se utiliza para la autenticación de nuevo y se elimina del nodo de Hola.

Puede obtener información de hello necesaria para el protocolo de registro de hello DSC de hello **administrar claves** hoja en el portal de vista previa de Hola. Abra esta hoja haciendo clic en el icono de llave hello en hello **Essentials** panel para hello cuenta de automatización.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* Dirección URL de registro es el campo de dirección URL de hello en la hoja de administrar claves de Hola.
* Clave de registro es Hola clave de acceso principal o clave de acceso secundaria en la hoja de administrar claves de Hola. Se puede usar cualquiera de las dos.

Para lograr una mayor seguridad, pueden volver a generar las claves de acceso principal y secundaria de Hola de una cuenta de automatización en cualquier momento (en hello **administrar claves** hoja) registros de nodo futuras de tooprevent mediante claves anteriores.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Solución de problemas de incorporación de máquinas virtuales de Azure

DSC de Automatización de Azure permite incorporar fácilmente máquinas virtuales de Azure con Windows para la administración de configuraciones. Bajo el paraguas de hello, Hola extensión de configuración de estado deseado de Azure VM es tooregister usado hello VM con el DSC de automatización de Azure. Puesto que Hola extensión de configuración de estado deseado de VM de Azure se ejecuta de forma asincrónica, seguimiento de su progreso y solucionar problemas de su ejecución pueden ser importantes.

> [!NOTE]
> Cualquier método de incorporación una tooAzure de VM en Windows Azure DSC de automatización que usa la extensión de la configuración de estado deseado de Azure VM Hola podría tardar hasta hora tooan Hola nodo tooshow seguridad como está registrado en automatización de Azure. Esto es debido a la instalación de toohello de Windows Management Framework 5.0 en hello VM por extensión de DSC de VM de Azure de hello, que es necesario tooonboard Hola VM tooAzure DSC de automatización.

tootroubleshoot o la vista estado de Hola de extensión de la configuración de estado deseado de Azure VM, en el portal de Azure de Hola Hola vaya toohello VM está incorporado, a continuación, haga clic -> **toda la configuración de** -> **extensiones**   ->  **DSC**. Para obtener más detalles, puede hacer clic en **Ver estado detallado**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Expiración y repetición del registro del certificado

Después de registrar una máquina como un nodo de DSC de DSC de automatización de Azure, hay una serie de motivos por qué puede que necesite tooreregister ese nodo Hola futura:

* Tras el registro, cada nodo negocia automáticamente un certificado único para la autenticación que expira después de un año. Actualmente, Hola protocolo de registro de DSC de PowerShell no puede renovar certificados automáticamente cuando expirarán, por lo que tiene nodos de hello tooreregister después de la hora de un año. Antes de volver a registrar, asegúrese de que cada nodo ejecute Windows Management Framework 5.0 RTM. Si expira el certificado de autenticación de un nodo y no se registra el nodo de hello, nodo de hello será no se puede toocommunicate con automatización de Azure y se marcará como "No responde". Volver a registrar realiza 90 días o menor de tiempo de expiración del certificado de hello, o en cualquier momento después de la fecha de expiración del certificado de hello, dará como resultado un nuevo certificado que se va a generar y usar.
* toochange cualquier [valores del Administrador de configuración Local de DSC de PowerShell](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que se establecieron durante el registro inicial del nodo de hello, como ConfigurationMode. Actualmente, estos valores de agente DSC solo pueden cambiarse mediante un nuevo registro. una excepción de Hello es Hola configuración de nodo asignada toohello nodo, esto puede cambiarse en el DSC de automatización de Azure directamente.

Volver a registrar puede realizarse en hello igual registró nodo Hola inicialmente, mediante cualquiera de los métodos de incorporación de hello descrita en este documento. No es necesario toounregister un nodo de DSC de automatización de Azure antes de volver a registrarlo.

## <a name="related-articles"></a>Artículos relacionados

* [Información general de DSC de Automatización de Azure](automation-dsc-overview.md)
* [Cmdlets de DSC de Automatización de Azure](/powershell/module/azurerm.automation/#automation)
* [Precios de DSC de Automatización de Azure](https://azure.microsoft.com/pricing/details/automation/)
