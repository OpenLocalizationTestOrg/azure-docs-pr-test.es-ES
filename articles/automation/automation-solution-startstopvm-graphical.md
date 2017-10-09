---
title: "Gráfico aaaStarting y detener las máquinas virtuales - | Documentos de Microsoft"
description: "Versión de flujo de trabajo de PowerShell del escenario de automatización de Azure incluidos runbooks toostart y detener máquinas virtuales clásicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
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

Se trata de una versión de runbook gráfico Hola de este escenario. Está también disponible con [los runbooks de flujo de trabajo de PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Introducción al escenario de Hola
Este escenario consta de dos dos runbooks gráficos que puede descargar desde Hola siguientes vínculos.  Vea hello [versión de flujo de trabajo de PowerShell](automation-solution-startstopvm-psworkflow.md) de este escenario para vínculos toohello runbooks de flujo de trabajo de PowerShell.

| Runbook | Vínculo | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Runbook gráfico de inicio de máquinas virtuales clásicas de Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Gráfico |Inicia todas las máquinas virtuales clásicas de una suscripción de Azure o todas las máquinas virtuales con un nombre de servicio determinado. |
| StopAzureClassicVM |[Runbook gráfico de detención de máquinas virtuales clásicas de Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Gráfico |Detiene todas las máquinas virtuales de una cuenta de automatización o todas las máquinas virtuales con un nombre de servicio determinado. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalar y configurar el escenario de Hola
### <a name="1-install-hello-runbooks"></a>1. Instalar runbooks Hola
Después de descargar runbooks hello, puede importarlos mediante el procedimiento de hello en [runbook gráfico procedimientos](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Descripción de Hola de revisión y los requisitos
Hola runbooks incluyen una actividad denominada **Léame** que incluye una descripción y los recursos necesarios.  Puede ver esta información si selecciona hello **Léame** hello actividad y, a continuación, **secuencia de comandos de flujo de trabajo** parámetro.  También puede obtener Hola la misma información de este artículo.

### <a name="3-configure-assets"></a>3. Configuración de activos
Hola runbooks requieren Hola después de activos que se deben crear y rellenar con los valores adecuados.  nombres de Hello están el valor predeterminado.  Puede utilizar activos con nombres diferentes si especifica esos nombres en hello [parámetros de entrada](#using-the-runbooks) al iniciar runbook Hola.

| Tipo de recurso | Nombre predeterminado | Descripción |
|:--- |:--- |:--- |:--- |
| [Credential:](automation-credentials.md) |AzureCredential |Contiene las credenciales para una cuenta que tenga autoridad toostart y detener las máquinas virtuales en hello suscripción de Azure. |
| [Variable](automation-variables.md) |AzureSubscriptionId |Contiene el Id. de suscripción de Hola de su suscripción de Azure. |

## <a name="using-hello-scenario"></a>Uso de escenario de Hola
### <a name="parameters"></a>parameters
Hello runbooks cada tener hello [parámetros de entrada](automation-starting-a-runbook.md#runbook-parameters).  Tiene que proporcionar valores para los parámetros obligatorios y opcionalmente puede proporcionar valores para otros parámetros dependiendo de sus necesidades.

| Parámetro | Escriba | Obligatorio | Descripción |
|:--- |:--- |:--- |:--- |
| ServiceName |cadena |No |Si se proporciona un valor, todas las máquinas virtuales con ese nombre de servicio se inician o se detienen.  Si no se proporciona ningún valor, todas las máquinas virtuales clásicas Hola suscripción de Azure está iniciadas o detenidas. |
| AzureSubscriptionIdAssetName |cadena |No |Contiene el nombre hello de hello [activo de variable](#installing-and-configuring-the-scenario) que contiene el identificador de la suscripción de Hola de su suscripción de Azure.  Si no se especifica un valor, se usa *AzureSubscriptionId* . |
| AzureCredentialAssetName |cadena |No |Contiene el nombre hello de hello [activo de credencial](#installing-and-configuring-the-scenario) que contiene las credenciales de Hola para hello runbook toouse.  Si no se especifica un valor, se usa *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>A partir de hello runbooks
Puede usar cualquiera de los métodos de hello en [a partir de un runbook en automatización de Azure](automation-starting-a-runbook.md) toostart cualquiera de hello runbooks en este artículo.

Siga los comandos del ejemplo de Hola usa Windows PowerShell toorun **StartAzureClassicVM** toostart todas las máquinas virtuales con el nombre del servicio de hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Salida
Hola runbooks le [un mensaje de salida](automation-runbook-output-and-messages.md) para cada máquina virtual que indica Hola o no inicio o la instrucción stop se envió correctamente.  También puede buscar una cadena concreta en hello toodetermine Hola resultado para cada runbook.  se muestran cadenas de resultado posible de Hola en hello en la tabla siguiente.

| Runbook | Condición | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |La máquina virtual ya se está ejecutando |MyVM ya se está ejecutando. |
| StartAzureClassicVM |La solicitud de inicio de la máquina virtual ha enviado correctamente |Se ha iniciado MyVM |
| StartAzureClassicVM |Se produjo un error en la solicitud de inicio de la máquina virtual |MyVM no pudo toostart |
| StopAzureClassicVM |La máquina virtual ya se está ejecutando |MyVM ya se ha detenido. |
| StopAzureClassicVM |La solicitud de inicio de la máquina virtual ha enviado correctamente |Se ha iniciado MyVM |
| StopAzureClassicVM |Se produjo un error en la solicitud de inicio de la máquina virtual |MyVM no pudo toostart |

Aquí te mostramos una imagen del uso de hello **StartAzureClassicVM** como un [runbook secundario](automation-child-runbooks.md) en un gráfico de ejemplo.  Esto utiliza vínculos condicionales Hola Hola en la tabla siguiente.

| Vínculo | Criterios |
|:--- |:--- |
| Vínculo de éxito |$ActivityOutput['StartAzureClassicVM'] -like "\* se ha iniciado" |
| Vínculo de error |$ActivityOutput['StartAzureClassicVM'] -notlike "\* se ha iniciado" |

![Ejemplo de runbook secundario](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Desglose detallado
Aquí te mostramos un análisis detallado de hello runbooks en este escenario.  Puede utilizar esta información tooeither personalizar Hola runbooks o simplemente toolearn de ellos para la creación de sus propios escenarios de automatización.

### <a name="authentication"></a>Autenticación
![Autenticación](media/automation-solution-startstopvm/graphical-authentication.png)

Hola runbook empieza por hello de actividades tooset [credenciales](automation-credentials.md) y suscripción de Azure que se usará para el resto de Hola de runbook de Hola.

Hola primero dos actividades, **obtener Id. de suscripción** y **obtener credenciales de Azure**, recuperar hello [activos](#installing-the-runbook) que se usan las siguientes dos actividades de Hola.  Esas actividades podrían especificar directamente los activos de Hola, pero tienen nombres de activos de Hola.  Puesto que permitimos Hola usuario toospecify esos nombres en hello [parámetros de entrada](#using-the-runbooks), necesitamos estos activos de hello tooretrieve actividades con un nombre especificado por un parámetro de entrada.

**Agregar-AzureAccount** Hola de conjuntos de credenciales que se utilizará para el resto de Hola de runbook de Hola.  activo de credencial de Hola que recupera de **obtener credenciales de Azure** debe tener acceso toostart y detener las máquinas virtuales en hello suscripción de Azure.  suscripción que se usa Hello está activada de forma **Select-AzureSubscription** que utiliza el Id. de suscripción de Hola de **obtener Id. de suscripción**.

### <a name="get-virtual-machines"></a>Obtención de máquinas virtuales
![Get VMs](media/automation-solution-startstopvm/graphical-getvms.png)

Hola runbook necesita toodetermine las máquinas virtuales que va a trabajar y si ya se inició o detuvo (en función de runbook de hello).   Uno de dos actividades recuperará hello las máquinas virtuales.  **Obtener máquinas virtuales en el servicio de** se ejecutará si hello *ServiceName* parámetro de entrada para hello runbook contiene un valor.  **Obtener todas las máquinas virtuales** se ejecutará si hello *ServiceName* parámetro de entrada para hello runbook no contiene un valor.  Esta lógica se realiza mediante vínculos condicionales Hola delante de cada actividad.

Ambas actividades usan hello **Get-AzureVM** cmdlet.  **Obtener todas las máquinas virtuales** usa hello **ListAllVMs** parámetro establece tooreturn todas las máquinas virtuales.  **Obtener máquinas virtuales en el servicio de** usa hello **GetVMByServiceAndVMName** parámetro establecido y proporciona hello **ServiceName** parámetro de entrada para hello **ServiceName**parámetro.  

### <a name="merge-vms"></a>Combinación de máquinas virtuales
![Combinación de máquinas virtuales](media/automation-solution-startstopvm/graphical-mergevms.png)

Hola **máquinas virtuales de mezcla** actividad es necesario tooprovide entrada demasiado**Start-AzureVM** que necesita ser nombre Hola y el nombre de servicio de hello toostart de máquinas virtuales.  Dichos datos pueden provenir de **Get All VMs** o de **Get VMs in Service**, pero **Start-AzureVM** sólo puede especificar una actividad para su entrada.   

escenario de Hello es toocreate **máquinas virtuales mezcla** que ejecuta hello **Write-Output** cmdlet.  Hola **InputObject** parámetro de cmdlet es una expresión de PowerShell que combina la entrada de Hola de actividades de hello dos anteriores.  Solo se ejecutará una de esas actividades, por lo que solo se espera un conjunto de resultados.  **Start-AzureVM** puede utilizar estos resultados para sus parámetros de entrada.

### <a name="startstop-virtual-machines"></a>Inicio y detención de máquinas virtuales
![Start VMs](media/automation-solution-startstopvm/graphical-startvm.png) ![Stop VMs](media/automation-solution-startstopvm/graphical-stopvm.png)

Función runbook hello, las siguientes actividades de Hola intente toostart o detener Hola runbook mediante **Start-AzureVM** o **Stop-AzureVM**.  Puesto que la actividad hello está precedido por un vínculo de canalización, se ejecutará una vez para cada objeto devuelto desde **máquinas virtuales de mezcla**.  Hola vínculo es condicional para que solo se ejecutará la actividad hello si hello *RunningState* de hello máquina virtual está *detenido* para **Start-AzureVM** y  *Iniciar* para **Stop-AzureVM**. Si esta condición no se cumple, a continuación, **notificar iniciada** o **notificar ya se detuvo** es ejecutar toosend un mensaje mediante **Write-Output**.

### <a name="send-output"></a>Enviar los resultados
![Notify Start VMs](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notify Stop VMs](media/automation-solution-startstopvm/graphical-notifystop.png)

paso final de Hola Hola runbook es toosend salida si Hola inicio o solicitud de detención para cada máquina virtual se envió correctamente. Hay otro **Write-Output** actividad para cada una, y se determina que uno toorun con vínculos condicionales.  Se ejecutarán **Notify VM Started** o **Notify VM Stopped** si el valor de *OperationStatus* es *Succeeded* (correcto).  Si *OperationStatus* es cualquier otro valor, a continuación, **Notificar error tooStart** o **tooStop Notificar error** se ejecuta.

## <a name="next-steps"></a>Pasos siguientes
* [Creación gráfica en Automatización de Azure](automation-graphical-authoring-intro.md)
* [Runbooks secundarios en la Automatización de Azure](automation-child-runbooks.md)
* [Salidas de runbook y mensajes en la Automatización de Azure](automation-runbook-output-and-messages.md)
