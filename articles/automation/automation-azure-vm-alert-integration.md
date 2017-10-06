---
title: "aaa\"corregir las alertas de la máquina virtual de Azure con Runbooks de automatización | Documentos de Microsoft\""
description: "En este artículo se muestra cómo las alertas toointegrate Máquina Virtual de Azure con runbooks de automatización de Azure y auto-corregir problemas"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Escenario de Automatización de Azure: corrección de las alertas de la máquina virtual de Azure
Automatización de Azure y máquinas virtuales de Azure ha publicado una nueva característica permitiéndole runbooks de automatización de toorun las alertas de tooconfigure Máquina Virtual (VM). Esta nueva capacidad le permite tooautomatically realizar correcciones de estándar en las alertas de tooVM de respuesta, como reiniciar o detener Hola máquina virtual.

Anteriormente, durante la creación de la regla de alerta de VM podía demasiado[especificar un webhook de automatización](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook en orden toorun Hola runbook cada vez que desencadene Hola alerta. Sin embargo, esto requiere trabajo de hello toodo de creación de runbook de hello, crear webhook Hola Hola runbook y, a continuación, copiar y pegar hello webhook durante la creación de la regla de alerta. Con esta nueva versión, el proceso de hello es mucho más fácil porque directamente, puede elegir un runbook de una lista durante la creación de la regla de alerta, y puede elegir una cuenta de automatización que se ejecuten runbook Hola o crear fácilmente una cuenta.

En este artículo, agregaremos muestra lo fácil que es tooset una alerta de la máquina virtual de Azure y configurar una toorun de runbook de automatización siempre que desencadena la alerta de Hola. Escenarios de ejemplo incluyen reiniciar una máquina virtual cuando el uso de memoria de hello supera determinado umbral debido tooan aplicación Hola VM con una pérdida de memoria, o detener una máquina virtual al tiempo de usuario de hello CPU ha sido por debajo de % 1 de última hora y no está en uso. También explicaremos cómo Hola automatiza la creación de una entidad de servicio en la automatización cuenta simplifica el uso de Hola de runbooks en Azure corrección de alerta.

## <a name="create-an-alert-on-a-vm"></a>Creación de una alerta para una máquina virtual
Realizar Hola siguientes pasos tooconfigure una alerta toolaunch un runbook cuando se ha alcanzado el umbral.

> [!NOTE]
> En esta versión solo se admiten máquinas virtuales de V2 y pronto se agregará el soporte técnico para máquinas virtuales clásicas.  
> 
> 

1. Inicie sesión en toohello portal de Azure y haga clic en **máquinas virtuales**.  
2. Seleccione una de las máquinas virtuales.  Hello hoja de panel de máquina virtual aparecerá y Hola **configuración** derecha tooits de hoja.  
3. De hello **configuración** hoja bajo Seleccione de la sección de supervisión de hello **reglas de alerta**.
4. En hello **reglas de alerta** hoja, haga clic en **Agregar alerta**.

Esto abrirá hello **agregar una regla de alerta** hoja, donde puede configurar las condiciones de Hola de alerta de Hola y elegir entre una o todas estas opciones: enviar correo electrónico toosomeone, utilice un sistema de alerta tooanother webhook tooforward hello, o ejecutar un runbook de automatización problema de respuesta intento tooremediate Hola.

## <a name="configure-a-runbook"></a>Configuración de un runbook
Seleccione tooconfigure un toorun runbook cuando se cumpla el umbral de alerta de VM de hello, **Runbook de automatización**. Hola **configurar runbook** hoja, puede seleccionar toorun de runbook de Hola y Hola automatización cuenta toorun Hola runbook en.

![Configuración de un runbook de automatización y creación de una nueva cuenta de automatización](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Para esta versión puede elegir entre tres runbooks que proporciona el servicio de hello: reiniciar VM, detener la máquina virtual o VM quitar (eliminar).  Hola tooselect capacidad otros runbooks o uno de sus propios runbooks estará disponible en futuras versiones.
> 
> 

![Toochoose de runbooks desde](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Después de seleccionar uno de los runbooks disponibles Hola tres, Hola **cuenta de automatización** aparece la lista desplegable y puede seleccionar una automatización cuenta Hola runbook se ejecutará como. Runbooks necesita toorun en contexto de Hola de un [cuenta de automatización](automation-security-overview.md) que se encuentra en su suscripción de Azure. Puede seleccionar una cuenta de automatización que ya haya creado o puede crear una nueva.

Hola runbooks que se proporcionan autenticar tooAzure con una entidad de servicio. Si elige toorun Hola runbook en una de las cuentas de automatización existentes, se creará automáticamente servicio Hola principal para usted. Si elige una nueva cuenta de automatización toocreate, a continuación, se creará automáticamente cuenta hello y entidad de servicio de Hola. En ambos casos, también se creará dos recursos Hola cuenta de automatización: un activo de certificado denominado **AzureRunAsCertificate** y un recurso de conexión denominado **AzureRunAsConnection**. Hola runbooks usará **AzureRunAsConnection** tooauthenticate con Azure en acción de administración de orden tooperform Hola contra Hola máquina virtual.

> [!NOTE]
> entidad de servicio de Hola se crea en el ámbito de la suscripción de Hola y se asigna el rol de colaborador de Hola. Este rol es necesario para hello cuenta toohave permiso toorun Automation runbooks toomanage máquinas virtuales de Azure.  creación de Hello de una cuenta de automatización o una entidad de servicio es un evento único. Una vez que se crean, puede usar ese runbooks de toorun cuenta otras alertas de la máquina virtual de Azure.
> 
> 

Al hacer clic en **Aceptar** alerta Hola está configurado y si seleccionó Hola opción toocreate una nueva cuenta de automatización, se crea junto con la entidad de servicio de Hola.  Esta operación puede tardar unos segundos toocomplete.  

![Runbook que se está configurando](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Una vez finalizada la configuración de hello verán el nombre de Hola de hello runbook aparecen en hello **agregar una regla de alerta** hoja.

![Runbook configurado](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Haga clic en **Aceptar** en hello **agregar una regla de alerta** hello y hoja de regla de alerta se va a crear y activar si la máquina virtual de hello está en un estado de ejecución.

### <a name="enable-or-disable-a-runbook"></a>Habilitamiento o deshabilitamiento de un runbook
Si tiene un runbook configurado para una alerta, puede deshabilitarlo sin quitar la configuración de runbook de Hola. Esto permite alerta de hello tookeep ejecutando y es posible probar algunas de las reglas de alerta de hello y, a continuación, volver a habilitar Hola runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Creación de un Runbook que funciona con una alerta de Azure
Cuando se elige un runbook como parte de una regla de alerta de Azure, Hola runbook debe lógica toohave toomanage Hola datos de alertas que se pasan tooit.  Cuando se configura un runbook en una regla de alerta, se crea un webhook de hello runbook; ese webhook es toostart usado Hola runbook cada desencadenadores de alerta de Hola de tiempo.  Hola llamada real toostart Hola runbook es una dirección URL webhook de toohello de solicitud HTTP POST. cuerpo de saludo de solicitud POST de hello contiene un objeto con formato JSON que contiene propiedades útiles relacionados toohello alerta.  Como puede ver a continuación, los datos de alertas de hello contienen detalles como el Id. de suscripción, resourceGroupName, resourceName y resourceType.

### <a name="example-of-alert-data"></a>Ejemplo de datos de alerta
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Cuando Hola servicio de webhook de automatización recibe Hola HTTP POST extrae datos de alertas de Hola y pasa toohello runbook hello WebhookData runbook parámetro de entrada.  A continuación se muestra un runbook de ejemplo que muestre cómo Hola WebhookData parámetro toouse y extraer datos de alertas de Hola y usar toomanage Hola recursos de Azure que desencadenó la alerta de Hola.

### <a name="example-runbook"></a>Runbook de ejemplo
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Resumen
Al configurar una alerta en una máquina virtual de Azure, ahora tiene Hola capacidad tooeasily configurar una automatización de runbook tooautomatically realizar acción correctora cuando se desencadena la alerta de Hola. En esta versión, puede elegir entre toorestart runbooks, detener o eliminar una máquina virtual según el escenario de alerta. Se trata de principio simplemente Hola de habilitar escenarios donde se controlan las acciones de hello (notificaciones, solución de problemas, corrección) que se realizará automáticamente cuando se desencadena una alerta.

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks gráficos, consulte [mi primer runbook gráfico](automation-first-runbook-graphical.md)
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md)
* toolearn más información acerca de los tipos de runbook, sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md)

