---
title: "planes de toorecovery de runbooks de automatización de Azure de aaaAdd en el portal clásico de hello | Documentos de Microsoft"
description: "Este artículo describe cómo Azure Site Recovery ahora permite tooextend planes de recuperación mediante tareas de automatización de Azure toocomplete complejas durante la recuperación tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Agregar planes de toorecovery de runbooks de automatización de Azure en el portal clásico de Hola
Este tutorial describe cómo se integra Azure Site Recovery con automatización de Azure tooprovide extensibilidad toorecovery planes. Planes de recuperación pueden coordinar la recuperación de las máquinas virtuales protegidos con Azure Site Recovery para la nube de toosecondary de replicación y los escenarios de replicación tooAzure. También ayudan a realizar la recuperación de hello **coherentes y precisos**, **repetible**, y **automatizada**. Si conmuta por error el tooAzure de máquinas virtuales, integración con automatización de Azure extiende los planes de recuperación y proporciona capacidad tooexecute runbooks, por lo que las tareas de automatización eficaz.

Si aún no ha oído hablar de Azure Automation, suscríbase [aquí](https://azure.microsoft.com/services/automation/) y descargue sus scripts de ejemplo [aquí](https://azure.microsoft.com/documentation/scripts/). Obtenga más información sobre [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) y cómo tiene previsto tooorchestrate tooAzure de recuperación mediante la recuperación de [aquí](https://azure.microsoft.com/blog/?p=166264).

En este breve tutorial, veremos cómo se pueden integrar runbooks de Azure Automation en planes de recuperación. Agregaremos información automatizar tareas sencillas que anteriormente requerían la intervención manual y vea cómo tooconvert un múltiples recuperación paso a paso una acción de recuperación con un solo clic. También veremos cómo puede solucionar problemas de un script sencillo si algo va mal.

## <a name="protect-hello-application-tooazure"></a>Proteger Hola aplicación tooAzure
Comenzaremos con una aplicación simple que consta de dos máquinas virtuales. En este caso, tenemos una aplicación HRweb de Fabrikam. Servidor front-end de HRweb Fabrikam y Fabrikam-Hrweb-back-end están protegidos con dos máquinas virtuales que hello tooAzure con Azure Site Recovery. máquinas virtuales tooprotect Hola que con Azure Site Recovery, siga los pasos de Hola a continuación.

1. Habilite la protección para las máquinas virtuales.
2. Asegúrese de que las máquinas virtuales Hola ha completado la replicación inicial y se replica.
3. Espere a que finalice la replicación inicial de Hola y Hola estado de replicación dice protegidos.

## ![](media/site-recovery-runbook-automation/01.png)
En este tutorial, se creará un plan de recuperación para hello Fabrikam HRweb aplicación toofailover Hola aplicación tooAzure. A continuación, se integrará con un runbook que va a crear un punto de conexión en hello conmutado por páginas de web tooserve de máquina virtual de Azure en el puerto 80.

En primer lugar, vamos a crear un plan de recuperación para nuestra aplicación.

## <a name="create-hello-recovery-plan"></a>Crear plan de recuperación de Hola
toorecover Hola aplicación tooAzure, deberá toocreate un plan de recuperación.
Uso de un plan de recuperación, puede especificar el orden de Hola de recuperación de las máquinas virtuales. máquina virtual de Hello colocado en el grupo 1 se recuperar e inicie primero y, a continuación, seguirá la máquina virtual de hello en el grupo 2.

Crear un plan de recuperación como el siguiente.

![](media/site-recovery-runbook-automation/12.png)

más información acerca de los planes de recuperación, lea la documentación de tooread [aquí](https://msdn.microsoft.com/library/azure/dn788799.aspx "aquí").

A continuación, vamos a crear Hola artefactos necesarios en la automatización de Azure.

## <a name="create-hello-automation-account-and-its-assets"></a>Crear cuenta de automatización de Hola y de sus activos
Es necesario un runbooks toocreate de cuenta de automatización de Azure. Si no dispone de una cuenta, vaya pestaña de automatización tooAzure denotado por ![](media/site-recovery-runbook-automation/02.png)y crear una nueva cuenta.

1. Conceda a cuenta de hello un tooidentify nombre con.
2. Especifique una región geográfica donde desea que la cuenta de hello tooplace.

Se recomienda tooplace cuenta de hello en hello misma región que el almacén de hello ASR.

![](media/site-recovery-runbook-automation/03.png)

A continuación, cree Hola después activos en hello cuenta.

### <a name="add-a-subscription-name-as-asset"></a>Incorporación de un nombre de suscripción como activo
1. Agregar una nueva configuración ![](media/site-recovery-runbook-automation/04.png) en Hola activos de automatización de Azure y seleccione demasiado![](media/site-recovery-runbook-automation/05.png)
2. Seleccione el tipo de variable de hello como **cadena**
3. Especifique el nombre de la variable como **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Especifique el nombre real de la suscripción de Azure como valor de la variable Hola.

   ![](media/site-recovery-runbook-automation/07_1.png)

Puede identificar el nombre hello de su suscripción desde la página de configuración de Hola de su cuenta en hello portal de Azure.

### <a name="add-an-azure-login-credential-as-asset"></a>Incorporación de una credencial de inicio de sesión de Azure como activo
Automatización de Azure usa la suscripción de Azure PowerShell tooconnect toothe y funciona en los artefactos de hello no existe. Para ello, deberá autenticarse con su cuenta de Microsoft o una cuenta profesional o educativa.
Puede almacenar las credenciales de cuenta de hello en un toobe asset utilizado de manera segura por runbook Hola.

1. Agregar una nueva configuración ![](media/site-recovery-runbook-automation/04.png) en Hola activos de automatización de Azure y seleccione![](media/site-recovery-runbook-automation/09.png)
2. Seleccione el tipo de credencial de hello como **credenciales de Windows PowerShell**
3. Especificar nombre de hello como **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Especifique Hola username y password toosign en con.

Ahora ambas configuraciones están disponibles en los activos.

![](media/site-recovery-runbook-automation/11.png)

Para obtener más información acerca de cómo se proporciona tooconnect tooyour suscripción a través de PowerShell [aquí](/powershell/azure/overview).

A continuación, creará un runbook en automatización de Azure que puede agregar un punto de conexión de máquina virtual de front-end Hola después de la conmutación por error.

## <a name="azure-automation-context"></a>Contexto de automatización de Azure
ASR pasa un toohelp de runbook de contexto toohello variable escribir scripts deterministas. Uno podría argumentar que los nombres de Hola de servicio en la nube de Hola y Hola Máquina Virtual son predecibles, pero no ocurre que no siempre es caso Hola poseer toocertain escenarios como Hola uno donde podría haber cambiado el nombre de hello del nombre de la máquina virtual de hello debido caracteres de toounsupported en Azure. Por lo tanto, esta información se pasa el plan de recuperación de toohello ASR como parte del programa Hola a *contexto*.

A continuación se muestra un ejemplo del aspecto de la variable de contexto de Hola.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


tabla de Hello siguiente contiene el nombre y una descripción para cada variable de contexto de Hola.

| **Nombre de la variable** | **Descripción** |
| --- | --- |
| RecoveryPlanName |Nombre del plan que se va a ejecutar. Ayuda a realizar acciones en función de nombre usando Hola mismo script |
| FailoverType |Especifica si se prueba Hola conmutación por error, planeada o no planeada. |
| FailoverDirection |Especifique si la recuperación es tooprimary o base de datos secundaria |
| GroupID |Identifique el número de grupo de hello en el plan de recuperación de hello cuando se ejecuta el plan de Hola |
| VmMap |Matriz de todas las máquinas virtuales de hello en el grupo de Hola |
| Clave de VMMap |Clave única (GUID) para cada máquina virtual. Ha Hola igual que Hola Id. de máquina virtual de Hola de VMM, si procede. |
| RoleName |Nombre de máquina virtual de Azure que se va a recuperar de hello |
| CloudServiceName |Nombre de servicio en la nube Azure bajo qué Hola se crea la máquina virtual. |

Hola de tooidentify VmMap Key en el contexto de hello también puede ir a página de propiedades de máquina virtual de toohello en ASR y mire Hola propiedad VM GUID.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Creación de un runbook de Automatización
Ahora cree tooopen puerto 80 de hello runbook en la máquina virtual de front-end Hola.

1. Crear un nuevo runbook en la cuenta de automatización de Azure con el nombre de Hola Hola **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Navegue toohello vista autor de runbook de Hola y entrar en modo de borrador de Hola.
3. Especifique primero toouse variable hello como contexto de plan de recuperación de Hola

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. A continuación conectar suscripción toohello con nombre de credencial y la suscripción de Hola

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Tenga en cuenta que usar hello Azure activos: **AzureCredential** y **AzureSubscriptionName** aquí.
5. Ahora, especifique los detalles de punto de conexión de Hola y Hola GUID de la máquina virtual de hello para el que desea que el punto de conexión de tooexpose Hola. En esta máquina virtual front-end de hello mayúsculas.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Esto especifica Hola protocolo de extremo de Azure, puerto local en hello VM y su puerto público asignada. Estas variables son parámetros requieren por hello Azure comandos que agregue tooVMs de puntos de conexión. Hola VMGUID contiene Hola GUID de la máquina virtual de hello en que necesita toooperate.
6. script de Hola ahora extraer contexto Hola para hello tiene el GUID de la VM y crear un punto de conexión en la máquina virtual de hello hace referencia a él.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Una vez completado, publicación de aciertos ![](media/site-recovery-runbook-automation/20.png) tooallow su toobe de secuencia de comandos disponible para su ejecución.

secuencia de comandos completa Hola se indica a continuación para su referencia

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Agregar plan de recuperación de hello script toohello
Una vez que el script de Hola esté listo, puede agregarlo toohello plan de recuperación que creó anteriormente.

1. En el plan de recuperación de Hola que ha creado, elija tooadd una secuencia de comandos después del grupo 2. ![](media/site-recovery-runbook-automation/15.png)
2. Especifique un nombre de script. Esto es simplemente un nombre descriptivo para esta secuencia de comandos para que se muestra en el plan de recuperación de Hola.
3. En secuencias de comandos de tooAzure de conmutación por error de hello: seleccione el nombre de cuenta de automatización de Azure de Hola.
4. Hola Runbooks de Azure, seleccione runbook Hola que crearon.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Scripts principales
Cuando se está ejecutando un tooAzure de conmutación por error, también puede elegir tooexecute secuencias de comandos principal. Estas secuencias de comandos se ejecutarán en el servidor VMM de Hola durante la conmutación por error.
Los scripts principales solo están disponibles solo para las fases de preapagado y postapagado. Esto es porque esperamos Hola sitio primario toobe normalmente no está disponible cuando se produzca un desastre.
Durante una conmutación por error no planeada, solo si decide no participar en para las operaciones del sitio primario, tratará de scripts del lado principal de hello toorun. Si no son accesibles o tiempo de espera, conmutación por error de hello continuará toorecover Hola máquinas virtuales.
Secuencias de comandos principales están sin disponibles para sitios de VMware/físicas/Hyper-v sin tooAzure VMM protegido - mientras se tooAzure de conmutación por error.
Sin embargo, cuando se conmutación por recuperación de tooon locales de Azure, secuencias de comandos principal (Runbooks) puede utilizarse para todos los destinos excepto VMware.

## <a name="test-hello-recovery-plan"></a>Plan de recuperación de Hola de prueba
Cuando haya agregado el plan de hello runbook toohello puede iniciar una conmutación por error de prueba y verlo en acción. Siempre es recomendable toorun un tootest de conmutación por error de prueba de su plan de recuperación, hello y aplicación, tooensure que no hay ningún error.

1. Seleccione el plan de recuperación de hello e iniciar una conmutación por error de prueba.
2. Durante la ejecución del plan de hello, puede ver si ha ejecutado runbook Hola o no a través de su estado.

   ![](media/site-recovery-runbook-automation/17.png)
3. También puede ver Hola el estado de ejecución de runbook en la página de trabajos de automatización de Azure Hola Hola runbook detallado.

   ![](media/site-recovery-runbook-automation/18.png)
4. Una vez completada la conmutación por error de hello, además de resultado de la ejecución de runbook de hello, puede ver si la ejecución de hello es correcta o no por visitar la página de la máquina virtual de Azure de Hola y examinando los puntos de conexión de Hola.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Scripts de ejemplo
Mientras se pasará a través de automatizar uno normalmente utiliza la tarea de agregar una máquina virtual de Azure de extremo tooan en este tutorial, se podría hacer que un número de otras tareas de automatización eficaz mediante la automatización de Azure. Microsoft y Hola Comunidad de automatización de Azure proporcionan runbooks de ejemplo que puede ayudarle a empezar a crear sus propias soluciones y runbooks de utilidad, que puede utilizar como bloques de creación para las tareas de automatización más grandes. Comenzar a usarlos de galería de Hola y generar planes de recuperación de un solo clic eficaz para las aplicaciones con Azure Site Recovery.

## <a name="additional-resources"></a>Recursos adicionales
[Información general sobre Automatización de Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "Información general sobre Automatización de Azure")

[Scripts de Automatización de Azure de ejemplo](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de Automatización de Azure de ejemplo")
