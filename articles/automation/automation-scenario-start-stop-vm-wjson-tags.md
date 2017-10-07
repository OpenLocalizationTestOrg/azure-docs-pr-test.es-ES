---
title: "estado de máquina virtual de Azure de etiquetas con formato JSON tooschedule aaaUse | Documentos de Microsoft"
description: "Este artículo demuestra cómo toouse JSON cadenas en la programación de hello tooautomate de etiquetas de cierre e inicio de máquina virtual."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Escenario de automatización de Azure: usar con formato JSON etiquetas toocreate una programación para la máquina virtual de Azure inicio y apagado
A menudo, los clientes desean tooschedule inicio de Hola y cierre de las máquinas virtuales toohelp reducir los costos de suscripción o admitir requisitos empresariales y técnicos.

Hello siguiente escenario permite tooset seguridad automatizada inicio y cierre de las máquinas virtuales mediante el uso de una etiqueta denominada programación con un nivel de máquina virtual en Azure o el nivel de grupo de recursos. Esta programación puede configurarse en domingo tooSaturday con un tiempo de inicio y la hora de cierre.

Tenemos algunas opciones disponibles de forma inmediata. Entre ellos se incluyen los siguientes:

* [Conjuntos de escalas de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) con valores de escalado automático que le permiten tooscale o alejar.
* [Laboratorios de desarrollo y pruebas](../devtest-lab/devtest-lab-overview.md) servicio, que ofrece la capacidad integrada de Hola de programación de operaciones de inicio y cierre.

Sin embargo, estas opciones solo admiten escenarios específicos y no puede ser aplicada tooinfrastructure como-servicio (IaaS) las máquinas virtuales.

Una vez Hola etiqueta programación aplicada tooa grupo de recursos, también es tooall aplicado las máquinas virtuales dentro de ese grupo de recursos. Si una programación también está directamente aplicado tooa VM, última programación de hello tiene prioridad en hello siguiendo el orden:

1. Grupo de recursos de programación tooa aplicado
2. Programar el grupo de recursos de tooa aplicados y máquina virtual en el grupo de recursos de Hola
3. Máquina virtual de programación aplica tooa

Este escenario básicamente toma una cadena JSON con un formato especificado y lo agrega como valor de Hola para una etiqueta denominada programación. A continuación, un runbook enumera todos los grupos de recursos y máquinas virtuales e identifica programaciones de Hola para cada máquina virtual basándose en los escenarios de hello enumerados anteriormente. A continuación recorre en bucle hello las máquinas virtuales que tienen programaciones que se adjunta y se evalúa como la acción que debe realizarse. Por ejemplo, determina que las máquinas virtuales necesitan toobe detener, apagar o tenga en cuenta.

Estos runbooks autenticar mediante hello [cuenta de identificación de Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Descargar runbooks de hello para el escenario de Hola
Este escenario consta de cuatro runbooks de flujo de trabajo de PowerShell que puede descargar desde hello [Galería de TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) o hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repositorio para este proyecto.

| Runbook | Descripción |
| --- | --- |
| Test-ResourceSchedule |Comprueba la programación de cada máquina virtual y realiza inicio según la programación de Hola o cierre. |
| Add-ResourceSchedule |Agrega Hola programación etiqueta tooa VM o grupo de recursos. |
| Update-ResourceSchedule |Modifica la etiqueta de programación de hello existente si se reemplaza por una nueva. |
| Remove-ResourceSchedule |Quita la etiqueta de la programación de Hola desde un máquina virtual o grupo de recursos. |

## <a name="install-and-configure-this-scenario"></a>Instalación y configuración de este escenario
### <a name="install-and-publish-hello-runbooks"></a>Instalar y publicar runbooks Hola
Después de descargar runbooks hello, puede importar utilizando el procedimiento de hello en [crear o importar un runbook en automatización de Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Publique cada Runbook después de que se hayan importado correctamente en la cuenta de Automatización.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Agregar un runbook de toohello ResourceSchedule de prueba de programación
Siga estos programación de hello tooenable de pasos de runbook de prueba ResourceSchedule Hola. Se trata de runbook de Hola que comprueba las máquinas virtuales que se debe iniciar, apagar, o dejarlos como están.

1. De hello portal de Azure, abra su cuenta de automatización y, a continuación, haga clic en hello **Runbooks** icono.
2. En hello **prueba ResourceSchedule** hoja, haga clic en hello **programaciones** icono.
3. En hello **programaciones** hoja, haga clic en **agregar una programación**.
4. En hello **programaciones** hoja, seleccione **vincular un runbook de programación tooyour**. A continuación, seleccione **Crear una programación nueva**.
5. En hello **nueva programación** hoja, escriba el nombre de Hola de esta programación, por ejemplo: *HourlyExecution*.
6. Para las programaciones de hello **iniciar**, establezca Hola inicio tiempo tooan hora incremento.
7. Seleccione **Periodicidad** y, en **Recur every interval** (Repetir cada intervalo), seleccione **1 hora**.
8. Compruebe que **caducidad del conjunto de** se establece demasiado**No**y, a continuación, haga clic en **crear** toosave al nuevo esquema.
9. En hello **programación Runbook** hoja de opciones, seleccione **parámetros y parámetros de ejecución**. Hola prueba ResourceSchedule **parámetros** hoja, escriba el nombre de Hola de su suscripción en hello **SubscriptionName** campo.  Esto es Hola único parámetro necesario para runbook Hola.  Cuando haya terminado, haga clic en **Aceptar**.

programación de runbook de Hello debería parecerse a la siguiente de hello cuando se completan:

![Runbook Test-ResourceSchedule configurado](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Hola formato cadena JSON
Esta solución básicamente toma JSON de cadena con un formato especificado y lo agrega como valor de Hola para una etiqueta llamada Schedule. A continuación, un runbook enumera todos los grupos de recursos y máquinas virtuales e identifica programaciones de Hola para cada máquina virtual.

Hola runbook itera sobre máquinas virtuales de Hola que tienen programaciones asociadas y comprueba qué acciones deben ejecutarse. Hola te mostramos un ejemplo de cómo se deben dar formato soluciones hello:

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Información detallada sobre esta estructura:

1. formato de Hola de esta estructura JSON es toowork optimizada de limitación de 256 caracteres de Hola de un valor de etiqueta única en Azure.
2. *TzId* representa Hola zona horaria de la máquina virtual de Hola. Este identificador puede obtenerse mediante la clase TimeZoneInfo .NET de hello en una sesión de PowerShell:**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones en PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Días de la semana se representan con un valor numérico de cero toosix. Hola valor cero es igual al domingo.
   * hora de inicio Hello se representa una con hello **S** atributo y su valor está en un formato de 24 horas.
   * hora de finalización o apagado Hello se representa una con hello **E** atributo y su valor está en un formato de 24 horas.

     Si hello **S** y **E** atributos tienen un valor de cero (0), la máquina virtual de Hola se quedará en su estado actual en tiempo de Hola de evaluación.
3. Si desea que la evaluación tooskip para un día concreto de la semana de hello, no agregue una sección para ese día de la semana de Hola. Hola se evalúa el siguiente ejemplo, solo lunes y hello otros días de la semana de Hola se pasan por alto:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Etiquetado de máquinas virtuales o grupos de recursos
tooshut hacia abajo de las máquinas virtuales, deberá tootag hello las máquinas virtuales o grupos de recursos de hello en el que se encuentren. No se evalúan las máquinas virtuales que no tienen una etiqueta Schedule. Por lo tanto, estas no se iniciarán ni apagarán.

Hay dos grupos de recursos de maneras tootag o máquinas virtuales con esta solución. Puede hacerlo directamente desde el portal de Hola. O bien, puede usar Hola agregar ResourceSchedule y ResourceSchedule de actualización, Remove-ResourceSchedule runbooks.

### <a name="tag-through-hello-portal"></a>Etiqueta a través del portal de Hola
Siga estos pasos tootag una máquina virtual o el grupo de recursos en el portal de hello:

1. Aplanar la cadena JSON de Hola y compruebe que no hay espacios en blanco.  La cadena JSON debe tener este aspecto:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Seleccione hello **etiqueta** icono para una máquina virtual o un recurso de grupo tooapply esta programación.

   ![Opción de etiqueta de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Las etiquetas se definen siguiendo un par clave/valor. Tipo de **programación** en hello **clave** campo y, a continuación, pegue cadena JSON de Hola Hola **valor** campo. Haga clic en **Guardar**. La nueva etiqueta debería aparecer ahora en la lista de Hola de etiquetas para el recurso.

   ![Etiqueta Schedule de máquina virtual](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Etiquetado en PowerShell
Todos los runbooks importados contienen información de ayuda al principio de Hola de script de Hola que describe cómo tooexecute Hola runbooks directamente desde PowerShell. Puede llamar a runbooks de agregar ScheduleResource y ScheduleResource de actualización de Hola de PowerShell. Para ello, pasando los parámetros necesarios que le permiten etiqueta de programación de hello toocreate o update en un máquina virtual o grupo de recursos fuera de portal de Hola.

toocreate, agregar y eliminar etiquetas a través de PowerShell, primero debe demasiado[configurar el entorno de PowerShell para Azure](/powershell/azure/overview). Después de completar el programa de instalación de hello, puede continuar con hello pasos.

### <a name="create-a-schedule-tag-with-powershell"></a>Creación de una etiqueta Schedule con PowerShell
1. Abra una sesión de PowerShell. A continuación, usar hello después tooauthenticate de ejemplo con su cuenta de ejecución y toospecify una suscripción:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Defina una tabla hash de programación. Este es un ejemplo de cómo debe estar conformada:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Definir parámetros de Hola que requieren Hola runbook. En el siguiente ejemplo de Hola que estamos usando como objetivo una máquina virtual:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Si está etiquetado de un grupo de recursos, quite hello *VMName* parámetro de hash de hello $params tabla como sigue:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Ejecute hello ResourceSchedule agregar runbook con hello sigue parámetros toocreate Hola programación etiqueta:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate una etiqueta de máquina virtual o el grupo de recursos, ejecute hello **ResourceSchedule actualización** runbook con hello parámetros siguientes:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Eliminación de una etiqueta Schedule con PowerShell
1. Abra una sesión de PowerShell y ejecute hello después tooauthenticate con su cuenta de ejecución y tooselect y especifique una suscripción:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Definir parámetros de Hola que requieren Hola runbook. En el siguiente ejemplo de Hola que estamos usando como objetivo una máquina virtual:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Si elimina una etiqueta de un grupo de recursos, quitar hello *VMName* parámetro de hash de hello $params tabla como sigue:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Execute (etiqueta) Hola Remove-ResourceSchedule runbook tooremove Hola programación:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate una etiqueta de máquina virtual o el grupo de recursos, ejecute hello Remove-ResourceSchedule runbook con hello parámetros siguientes:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Se recomienda que supervise proactivamente Estos runbooks (y los Estados de máquina virtual de hello) tooverify que las máquinas virtuales que se apague y se inicia en consecuencia.
>

detalles de hello tooview de hello ResourceSchedule prueba runbook trabajo Hola portal de Azure, seleccione hello **trabajos** icono de runbook de Hola. parámetros de entrada de Hello trabajo proporciona resúmenes hello y salida de hello streaming, además toogeneral información sobre el trabajo de Hola y las excepciones que se hayan producido.

Hola **resumen del trabajo** incluye mensajes de secuencias de salida, advertencia y error de Hola. Seleccione hello **salida** icono tooview resultados de ejecución de un runbook Hola detallados.

![Salida de Test-ResourceSchedule](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Pasos siguientes
* tooget a trabajar con runbooks de flujo de trabajo de PowerShell, consulte [mi primer runbook de flujo de trabajo de PowerShell](automation-first-runbook-textual.md).
* toolearn más información acerca de los tipos de runbook y sus ventajas y limitaciones, consulte [tipos de runbook de automatización de Azure](automation-runbook-types.md).
* Para más información sobre las características de compatibilidad con scripts de PowerShell, consulte [Announcing Native PowerShell Script Support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)(Anuncio de la compatibilidad nativa con scripts de PowerShell en Automatización de Azure).
* toolearn más información sobre el registro de runbook y salida, vea [Runbook salida y mensajes en automatización de Azure](automation-runbook-output-and-messages.md).
* más información acerca de una cuenta de identificación de Azure y cómo tooauthenticate sus runbooks mediante el uso de, consulte toolearn [autenticar runbooks con Azure cuenta de ejecución](automation-sec-configure-azure-runas-account.md).
