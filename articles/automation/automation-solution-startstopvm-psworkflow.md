---
title: "aaaStarting y la detención máquinas virtuales con automatización de Azure: flujo de trabajo de PowerShell | Documentos de Microsoft"
description: "Versión gráfica del escenario de automatización de Azure incluidos runbooks toostart y detener máquinas virtuales clásicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Escenario de Automatización de Azure: inicio y detención de máquinas virtuales
Este escenario de automatización de Azure incluye runbooks toostart y detener máquinas virtuales clásicas.  Puede usar este escenario para cualquiera de hello siguientes:  

* Usar runbooks de hello sin modificaciones en su propio entorno.
* Modificar la funcionalidad de tooperform personalizado de hello runbooks.  
* Llame a runbooks Hola desde otro runbook como parte de una solución global.
* Utilizar runbooks hello como tutoriales toolearn runbook conceptos de creación.

> [!div class="op_single_selector"]
> * [Gráfico](automation-solution-startstopvm-graphical.md)
> * [Flujo de trabajo de PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

Se trata de hello versión de runbook de flujo de trabajo de PowerShell de este escenario. Está también disponible mediante [runbooks gráficos](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Introducción al escenario de Hola
Este escenario consta de dos runbooks de flujo de trabajo de PowerShell que puede descargar desde Hola siguientes vínculos.  Vea hello [versión gráfica](automation-solution-startstopvm-graphical.md) de este escenario para runbooks gráficos toohello de vínculos.

| Runbook | Vínculo | Tipo | Description |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Inicio de máquinas virtuales de Azure clásicas](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Flujo de trabajo de PowerShell |Inicia todas las máquinas virtuales clásicas en una suscripción de Azure o en todas las máquinas virtuales con un nombre de servicio determinado. |
| Stop-AzureVMs |[Detención de máquinas virtuales de Azure clásicas](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Flujo de trabajo de PowerShell |Detiene todas las máquinas virtuales de una cuenta de automatización o todas las máquinas virtuales con un nombre de servicio determinado. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalar y configurar el escenario de Hola
### <a name="1-install-hello-runbooks"></a>1. Instalar runbooks Hola
Después de descargar runbooks hello, puede importarlos mediante el procedimiento de hello en [importar un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Descripción de Hola de revisión y los requisitos
Hola runbooks incluye el texto de ayuda comentados que incluye una descripción y los recursos necesarios.  También puede obtener Hola la misma información de este artículo.

### <a name="3-configure-assets"></a>3. Configuración de activos
Hola runbooks requieren Hola después de activos que se deben crear y rellenar con los valores adecuados.

| Tipo de recurso | Nombre de recurso | Description |
|:--- |:--- |:--- |:--- |
| Credential: |AzureCredential |Contiene las credenciales para una cuenta que tenga autoridad toostart y detener las máquinas virtuales en hello suscripción de Azure.  Como alternativa, puede especificar otro recurso de credencial en hello **credencial** parámetro de hello **Add-AzureAccount** actividad. |
| Variable |AzureSubscriptionId |Contiene el Id. de suscripción de Hola de su suscripción de Azure. |

## <a name="using-hello-scenario"></a>Uso de escenario de Hola
### <a name="parameters"></a>parameters
Hola runbooks tienen Hola parámetros siguientes.  Tiene que proporcionar valores para los parámetros obligatorios y opcionalmente puede proporcionar valores para otros parámetros dependiendo de sus necesidades.

| Parámetro | Escriba | Obligatorio | Descripción |
|:--- |:--- |:--- |:--- |
| ServiceName |cadena |No |Si se proporciona un valor, todas las máquinas virtuales con ese nombre de servicio se inician o se detienen.  Si no se proporciona ningún valor, todas las máquinas virtuales clásicas Hola suscripción de Azure está iniciadas o detenidas. |
| AzureSubscriptionIdAssetName |cadena |No |Contiene el nombre hello de hello [activo de variable](#installing-and-configuring-the-scenario) que contiene el identificador de la suscripción de Hola de su suscripción de Azure.  Si no se especifica un valor, se usa *AzureSubscriptionId* . |
| AzureCredentialAssetName |cadena |No |Contiene el nombre hello de hello [activo de credencial](#installing-and-configuring-the-scenario) que contiene las credenciales de Hola para hello runbook toouse.  Si no se especifica un valor, se usa *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>A partir de hello runbooks
Puede usar cualquiera de los métodos de hello en [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md) toostart cualquiera de hello runbooks en este escenario.

Siga los comandos del ejemplo de Hola usa Windows PowerShell toorun **StartAzureVMs** toostart todas las máquinas virtuales con el nombre del servicio de hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Salida
Hola runbooks le [un mensaje de salida](automation-runbook-output-and-messages.md) para cada máquina virtual que indica Hola o no inicio o la instrucción stop se envió correctamente.  También puede buscar una cadena concreta en hello toodetermine Hola resultado para cada runbook.  se muestran cadenas de resultado posible de Hola en hello en la tabla siguiente.

| Runbook | Condición | Message |
|:--- |:--- |:--- |
| Start-AzureVMs |La máquina virtual ya se está ejecutando. |MyVM ya se está ejecutando. |
| Start-AzureVMs |La solicitud de inicio de la máquina virtual ha enviado correctamente. |Se ha iniciado MyVM. |
| Start-AzureVMs |Se produjo un error en la solicitud de inicio de la máquina virtual |MyVM no pudo toostart |
| Stop-AzureVMs |La máquina virtual ya se ha detenido |MyVM ya se ha detenido. |
| Stop-AzureVMs |La solicitud de detención de la máquina virtual ha enviado correctamente |Se ha detenido MyVM |
| Stop-AzureVMs |Se produjo un error en la solicitud de detención de la máquina virtual |MyVM no pudo toostop |

Por ejemplo, hello siguiente fragmento de código desde un runbook intentará toostart todas las máquinas virtuales con el nombre del servicio de hello *MyServiceName*.  Si cualquiera de Hola inicia por error de las solicitudes, se pueden realizar acciones de error.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Desglose detallado
Aquí te mostramos un análisis detallado de hello runbooks en este escenario.  Puede utilizar esta información tooeither personalizar Hola runbooks o simplemente toolearn de ellos para la creación de sus propios escenarios de automatización.

### <a name="parameters"></a>parameters
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hello flujo de trabajo se inicia mediante la obtención de valores de hello para hello [parámetros de entrada](#using-the-scenario).  Si no se proporcionan nombres de activos de Hola se utilizan nombres predeterminados.

### <a name="output"></a>Salida
    # Returns strings with status messages
    [OutputType([String])]

Esta línea declara que la salida de hello de hello runbook será una cadena.  Esto no es necesario, pero es una práctica recomendada para cuando se utiliza Hola runbook como un [runbook secundario](automation-child-runbooks.md) para que un runbook primario sepan salida de hello escriba tooexpect.

### <a name="authentication"></a>Autenticación
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

en las líneas siguientes Hola establecer hello [credenciales](automation-credentials.md) y suscripción de Azure que se usará para el resto de Hola de runbook de Hola.
En primer lugar se utilice **Get-AutomationPSCredential** tooget activos de Hola que contiene las credenciales de hello con acceso toostart y deje de máquinas virtuales en hello suscripción de Azure. **Agregar-AzureAccount** , a continuación, usa este credenciales de hello tooset activo.  salida de Hello se asigna la variable ficticia tooa para que no se incluye en la salida de hello runbook.  

activo de variable de saludo con suscripción de hello Id. a continuación, se recupera con **Get-AutomationVariable** y suscripción Hola establecido con **Select-AzureSubscription**.

### <a name="get-vms"></a>Get VMs
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** es tooretrieve usado Hola Hola runbook funcionará con las máquinas virtuales.  Si se proporciona un valor en hello **ServiceName** variable, sólo hello las máquinas virtuales con ese nombre de servicio se recuperan de entrada.  Si **ServiceName** está vacío, se recuperan todas las máquinas virtuales.

### <a name="startstop-virtual-machines-and-send-output"></a>Inicio o detención de máquinas virtuales y envío de resultados
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

en las líneas siguientes Hola paso a paso a través de cada máquina virtual.  En primer lugar Hola **PowerState** de hello máquina virtual está activado toosee si ya está en ejecución o detenido, dependen de runbook de Hola.  Si ya está en estado de destino de hello, se envía un mensaje toooutput y Hola runbook finaliza.  Si no es así, a continuación, **Start-AzureVM** o **Stop-AzureVM** es tooattempt usado toostart o detener Hola máquina virtual con el resultado de hello de variable de hello solicitud tooa almacenado.  Se envía un mensaje, a continuación, especificar toooutput si toostart de solicitud de Hola o detención se envió correctamente.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más acerca de cómo trabajar con runbooks secundarios, vea [runbooks secundarios en automatización de Azure](automation-child-runbooks.md)
* solucionar problemas de mensajes durante la ejecución de un runbook y toohelp de registro de salida de toolearn más información sobre, consulte [Runbook salida y mensajes en automatización de Azure](automation-runbook-output-and-messages.md)

