---
title: "aaaStarting un runbook de automatización de Azure con un webhook | Documentos de Microsoft"
description: "Webhook que permite a un cliente toostart un runbook en automatización de Azure desde una llamada HTTP.  Este artículo se describe cómo toocreate un webhook y cómo toocall una toostart un runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Inicio de un runbook de Azure Automation con un webhook
A *webhook* permite toostart un runbook determinado en la automatización de Azure a través de una única solicitud HTTP. Esto permite a servicios externos, como Visual Studio Team Services, GitHub, análisis de registros de Microsoft Operations Management Suite o aplicaciones personalizadas toostart runbooks sin necesidad de implementar una solución completa mediante Hola API de automatización de Azure.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

Puede comparar webhooks tooother métodos para iniciar un runbook [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Detalles de un webhook
Hello tabla siguiente describe las propiedades de Hola que se deben configurar para un webhook.

| Propiedad | Descripción |
|:--- |:--- |
| Nombre |Puede proporcionar cualquier nombre que desee para un webhook, puesto que esto es no expone a toohello cliente.  Solo se utiliza para tooidentify Hola runbook de automatización de Azure. <br>  Como práctica recomendada, debe prestar hello webhook un cliente de toohello relacionados de nombre que va a usar. |
| URL |dirección URL de Hola de hello webhook es que un cliente llama a un runbook de hello toostart HTTP POST de dirección única Hola vinculado toohello webhook.  Se genera automáticamente al crear el webhook Hola.  No se puede especificar una dirección URL personalizada. <br> <br>  dirección URL de Hello contiene un token de seguridad que permita Hola runbook toobe invocado por un sistema de terceros con ninguna autenticación adicional. Por este motivo, debe tratarse como una contraseña.  Por motivos de seguridad, puede solo Hola de vista que se crea la dirección URL en el portal de Azure en hello tiempo hello webhook Hola. Tenga en cuenta Hola URL en una ubicación segura para un uso futuro. |
| Fecha de expiración |Al igual que un certificado, cada webhook tiene una fecha de caducidad en la que ya no se puede usar.  Esta fecha de expiración se puede modificar una vez creado el webhook Hola. |
| habilitado |Al crearse, los webhooks se habilitan de forma predeterminada.  Si se establece tooDisabled, entonces no hay ningún cliente será toouse capaz de él.  Puede establecer hello **habilitado** propiedad al crear webhook Hola o en cualquier momento una vez se crea. |

### <a name="parameters"></a>parameters
Un webhook puede definir valores para parámetros de runbook que se usan al iniciar runbook Hola por ese webhook. Hola webhook debe incluir valores para todos los parámetros obligatorios de runbook de Hola y puede incluir valores para los parámetros opcionales. Incluso después de crear hello webhoook se puede modificar un webhook de tooa del valor configurado de parámetro. Varios webhooks vinculados tooa único runbook puede utilizar distintos valores de parámetros.

Cuando un cliente inicia un runbook mediante un webhook, no pueden invalidar los valores de parámetro hello definidos en hello webhook.  datos de tooreceive del cliente de hello, Hola runbook puede aceptar un único parámetro denominado **$WebhookData** del tipo [objeto] que contiene datos de ese cliente hello incluye en la solicitud POST de Hola.

![Propiedades de Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Hola **$WebhookData** objeto tendrá Hola propiedades siguientes:

| Propiedad | Descripción |
|:--- |:--- |
| WebhookName |nombre de Hola de hello webhook. |
| RequestHeader |Tabla hash que contiene Hola encabezados de solicitud POST de Hola entrante. |
| RequestBody |cuerpo de Hola de solicitud POST de Hola entrante.  Esto conservará todo el formato como cadena de JSON, XML o datos codificados de formulario. Hola runbook debe escribirse toowork con formato de datos de Hola que se espera. |

No hay ninguna configuración de Hola webhook requiere toosupport Hola **$WebhookData** parámetro, y Hola runbook no es necesario tooaccept lo.  Si runbook hello no define el parámetro hello, se omite cualquier información de solicitud de hello enviados desde el cliente de Hola.

Si especifica un valor para $WebhookData al crear webhook hello, ese valor será reemplazada cuando hello webhook inicia runbook de hello con datos de saludo de solicitud de envío del cliente de hello, incluso si el cliente hello no incluye ningún dato en el cuerpo de la solicitud de Hola.  Si se inicia un runbook con $WebhookData mediante un método que no sea un webhook, puede proporcionar un valor para $Webhookdata que reconocerá Hola runbook.  Este valor debe ser un objeto con hello mismo [propiedades](#details-of-a-webhook) como $Webhookdata para dicho runbook Hola correctamente puede trabajar con ella como si estaba trabajando con WebhookData real pasado por un webhook.

Por ejemplo, si se están iniciando Hola siguientes runbook de hello Portal de Azure y desea toopass algunos WebhookData de ejemplo para las pruebas, ya que WebhookData es un objeto, se debe pasar como JSON en hello interfaz de usuario.

![Parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Para hello anteriormente runbook, si tienes Hola propiedades para el parámetro de hello WebhookData siguientes:

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

A continuación, pasaría Hola siguiente valor JSON en hello interfaz de usuario para el parámetro de Hola WebhookData:  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![Iniciar el parámetro WebhookData de la interfaz de usuario](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> valores de Hello de todos los parámetros de entrada se registran con el trabajo del runbook Hola.  Esto significa que cualquier entrada proporcionada por cliente hello en solicitud de webhook Hola será tooanyone registran y están disponible con el trabajo de automatización de toohello de acceso.  Por este motivo, debe tener cuidado en cómo incluir información confidencial en las llamadas de webhook.
>

## <a name="security"></a>Seguridad
seguridad de Hola de un webhook se basa en privacidad Hola de su dirección URL que contiene un token de seguridad que permita toobe invocada. Automatización de Azure no realiza ninguna autenticación en la solicitud de hello siempre y cuando se pone a dirección URL correcta de toohello. Por esta razón, no debe usarse webhooks para runbooks que realizan funciones muy confidenciales sin usar un medio alternativo de validación de solicitud de saludo.

Puede incluir lógica dentro de hello runbook toodetermine que se llamó por un webhook activando hello **WebhookName** propiedad del parámetro hello $WebhookData. Hola runbook podría realizar otras validación buscando información específica de hello **RequestHeader** o **RequestBody** propiedades.

Otra estrategia es toohave Hola runbook realizar una validación de una condición externa cuando recibe una solicitud de webhook.  Por ejemplo, considere la posibilidad de un runbook que llama a GitHub cada vez que hay un nuevo repositorio de GitHub de tooa de confirmación.  Hola runbook se conecten toovalidate tooGitHub que realmente solo se hubiera producido una confirmación nuevo antes de continuar.

## <a name="creating-a-webhook"></a>Creación de un webhook
Usar hello siguiendo el procedimiento toocreate un nuevo runbook de tooa de webhook vinculado en hello portal de Azure.

1. De hello **hoja de Runbooks** Hola portal de Azure, haga clic en runbook Hola que Hola webhook iniciará tooview su hoja de detalle.
2. Haga clic en **Webhook** en parte superior de Hola Hola de hello hoja tooopen **Webhook agregar** hoja. <br>
   ![Botón Webhooks](media/automation-webhooks/webhooks-button.png)
3. Haga clic en **crear nueva webhook** tooopen hello **Crear hoja de webhook**.
4. Especifique un **nombre**, **fecha de expiración** de webhook de Hola y si debe habilitarse. Vea [Detalles de un webhook](#details-of-a-webhook) para más información sobre estas propiedades.
5. Haga clic en el icono de copiar hello y presione Ctrl + C toocopy Hola URL del webhook Hola.  A continuación, guárdela en un lugar seguro.  **Una vez creado el webhook hello, no se puede recuperar la dirección URL de hello nuevo.** <br>
   ![Dirección URL de webhook](media/automation-webhooks/copy-webhook-url.png)
6. Haga clic en **parámetros** tooprovide valores para parámetros de runbook de Hola.  Si Hola runbook tiene parámetros obligatorios, a continuación, no será capaz de toocreate hello webhook a menos que se proporcionan valores.
7. Haga clic en **crear** toocreate hello webhook.

## <a name="using-a-webhook"></a>Uso de un webhook
toouse un webhook una vez creada, la aplicación cliente debe emitir una solicitud HTTP POST con dirección URL de Hola Hola webhook.  sintaxis de Hola de hello webhook será Hola siguiendo el formato.

    http://<Webhook Server>/token?=<Token Value>

Hola cliente recibirá uno de los siguientes códigos de retorno de solicitud POST Hola de Hola.  

| Código | Texto | Descripción |
|:--- |:--- |:--- |
| 202 |Accepted |se aceptó la solicitud de Hola y Hola runbook se puso en cola correctamente. |
| 400 |Bad Request |no se aceptó la solicitud de Hola para uno de hello siguientes motivos. <ul> <li>Hola webhook ha expirado.</li> <li>Hola webhook está deshabilitada.</li> <li>símbolo (token) de Hello en dirección URL de hello no es válido.</li>  </ul> |
| 404 |No encontrado |no se aceptó la solicitud de Hola para uno de hello siguientes motivos. <ul> <li>no se encontró el webhook Hola.</li> <li>no se encontró el runbook de Hola.</li> <li>no se encontró la cuenta de Hello.</li>  </ul> |
| 500 |Internal Server Error |dirección URL de Hello era válida, pero se produjo un error.  Vuelva a enviar la solicitud de saludo. |

Suponiendo que la solicitud de hello es correcta, respuesta de webhook Hola contiene Id. de trabajo de hello en formato JSON como se indica a continuación. Contendrá un identificador de trabajo único, pero permite el formato JSON de Hola para posibles mejoras futuras.

    {"JobIds":["<JobId>"]}  

Hola cliente no puede determinar cuando se completa el trabajo del runbook de Hola o su estado de finalización de hello webhook.  Puede determinar esta información con el Id. de trabajo de hello con otro método como [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o hello [API de automatización de Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Ejemplo
Hola de ejemplo siguiente usa Windows PowerShell toostart un runbook con un webhook.  Tenga en cuenta que cualquier lenguaje que pueda realizar una solicitud HTTP puede utilizar un webhook; Windows PowerShell se usa aquí simplemente como ejemplo.

Hola runbook está esperando una lista de máquinas virtuales con formato JSON en el cuerpo de saludo de solicitud de Hola. También incluiremos información sobre quién está iniciando runbook Hola y Hola fecha se está iniciando en el encabezado de saludo de solicitud de Hola.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Hello siguiente imagen muestra información de encabezado de hello (con un [Fiddler](http://www.telerik.com/fiddler) seguimiento) de esta solicitud. Esto incluye los encabezados estándar de una solicitud HTTP en suma toohello personalizado de fecha y de encabezados que se agregan.  Cada uno de estos valores es runbook toohello disponible en hello **RequestHeaders** propiedad de **WebhookData**.

![Botón Webhooks](media/automation-webhooks/webhook-request-headers.png)

Hello siguiente imagen muestra cuerpo de saludo de solicitud de hello (con un [Fiddler](http://www.telerik.com/fiddler) seguimiento) que es toohello disponibles runbook Hola **RequestBody** propiedad de **WebhookData**. Dado tenía el formato de Hola que se incluía en el cuerpo de saludo de solicitud de Hola, esto se formatea como JSON.     

![Botón Webhooks](media/automation-webhooks/webhook-request-body.png)

Hello siguiente imagen muestra hello solicitud que se envían desde Windows PowerShell y respuesta resultante Hola.  Id. de trabajo de Hola se extrae de la respuesta de Hola y cadena tooa convertido.

![Botón Webhooks](media/automation-webhooks/webhook-request-response.png)

Hello runbook de ejemplo siguiente acepta la solicitud de ejemplo de Hola anterior e inicia máquinas virtuales de hello especificadas en el cuerpo de la solicitud de saludo.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>A partir de runbooks en alertas de respuesta de tooAzure
Habilitado Webhook runbooks pueden ser utilizado tooreact demasiado[alertas Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Recursos de Azure se pueden supervisar mediante la recopilación de estadísticas de hello como rendimiento, disponibilidad y el uso con la Ayuda de Hola de alertas de Azure. Puede recibir una alerta basada en los eventos o las métricas de supervisión para los recursos de Azure. Actualmente, las cuentas de automatización solo admiten métricas. Cuando valor Hola de una métrica especificada supera el umbral de hello asignados o si se desencadena el evento Hola configurado, a continuación, se envía una notificación toohello administradores o coadministradores tooresolve Hola alerta de servicio, para obtener más información sobre las métricas y eventos consulte demasiado[ Alertas de Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Además de usar las alertas de Azure como un sistema de notificación, puede comenzar runbooks en tooalerts de respuesta. Automatización de Azure ofrece Hola capacidad toorun habilitado webhook runbooks con alertas de Azure. Cuando se supera una métrica Hola configurado valor de umbral, a continuación, se activa regla de alerta de Hola y desencadenadores Hola webhook de automatización que a su vez ejecuta runbook Hola.

![Webhooks](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Contexto de alerta
Considere la posibilidad de un recurso de Azure como una máquina virtual, es el uso de CPU de esta máquina de métrica de rendimiento clave de Hola. Si el uso de CPU de hello es 100% o más de una determinada cantidad durante un período largo de tiempo, puede el problema hello toofix de toorestart Hola máquina virtual. Esto se puede resolver mediante la configuración de una máquina virtual de toohello de regla de alerta y porcentaje de CPU como su métrica de toma de esta regla. Porcentaje de CPU aquí solo se toma como un ejemplo, pero hay muchas otras métricas que se puede configurar tooyour Azure recursos y reiniciando la máquina virtual de hello es una acción que es realizada toofix este problema, puede configurar Hola runbook tootake otras acciones.

Cuando se activa esta regla de alerta de Hola y desencadenadores Hola runbook habilitado webhook, envía Hola contexto de alerta toohello runbook. [Contexto de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene los detalles incluidos **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** y **marca de tiempo** que son necesarios para el recurso de Hola Hola runbook tooidentify en el que va a tener acción. Alerta de contexto se incrusta en la parte del cuerpo Hola de hello **WebhookData** objeto runbook toohello enviado y puede tener acceso mediante **Webhook.RequestBody** propiedad

### <a name="example"></a>Ejemplo
Crear una máquina virtual de Azure en su suscripción y asociar un [alerta métrica del porcentaje de CPU de toomonitor](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Durante la creación de alerta de Hola Asegúrese de que se rellene el campo de webhook de hello con dirección URL de Hola de webhook de Hola que se generó durante la creación de hello webhook.

Hello runbook de ejemplo siguiente se desencadena cuando se activa regla de alerta de Hola y recopila los parámetros de contexto de alerta de Hola que son necesarios para el recurso de Hola Hola runbook tooidentify en el que va a tener acción.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Pasos siguientes
* Para obtener detalles sobre las distintas formas toostart un runbook, consulte [a partir de un Runbook](automation-starting-a-runbook.md).
* Para obtener información sobre Hola ver estado de un Runbook Job, consulte demasiado[ejecución de un Runbook en automatización de Azure](automation-runbook-execution.md).
* toolearn toouse acción tootake de automatización de Azure en alertas de Azure, vea [corregir las alertas de VM de Azure con Runbooks de automatización](automation-azure-vm-alert-integration.md).
