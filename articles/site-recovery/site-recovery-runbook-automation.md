---
title: "Automatización de Azure los planes toorecovery aaaAdd runbooks en Azure Site Recovery | Documentos de Microsoft"
description: "Obtenga información sobre cómo Azure Site Recovery puede ayudarle a ampliar los planes de recuperación mediante Azure Automation. Obtenga información acerca de cómo toocomplete complejo tareas durante la recuperación tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Agregar planes de toorecovery de runbooks de automatización de Azure
En este artículo se describe cómo se integra Azure Site Recovery con toohelp de automatización de Azure extiende los planes de recuperación. Los planes de recuperación pueden organizar la recuperación de máquinas virtuales protegidas con Site Recovery. Planes de recuperación de trabajo para la nube secundaria tooa de replicación tanto para tooAzure de replicación. Planes de recuperación también ayudan a realizar la recuperación de hello **coherentes y precisos**, **repetible**, y **automatizada**. Si la conmutación por error el tooAzure de las máquinas virtuales, la integración con automatización de Azure amplía los planes de recuperación. Puede usar tooexecute runbooks, que ofrecen las tareas de automatización eficaz.

Si es nuevo tooAzure automatización, puede [registrarse](https://azure.microsoft.com/services/automation/) y [descargar scripts de muestra](https://azure.microsoft.com/documentation/scripts/). Para obtener más información y toolearn cómo tooorchestrate tooAzure de recuperación mediante el uso de [planes de recuperación](https://azure.microsoft.com/blog/?p=166264), consulte [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

En este artículo se explica cómo integrar runbooks de Azure Automation en los planes de recuperación. Se usan tareas básicas de ejemplos tooautomate que anteriormente requerían intervención manual. También se describe cómo tooconvert una tooa de recuperación de varios pasos con un solo clic acción de recuperación.

## <a name="customize-hello-recovery-plan"></a>Personalizar plan de recuperación de Hola
1. Vaya toohello **Site Recovery** hoja de recursos del plan de recuperación. En este ejemplo, el plan de recuperación de hello tiene tooit agregado dos de las máquinas virtuales, para la recuperación. toobegin adición de un runbook, haga clic en hello **personalizar** ficha.

    ![Haga clic en el botón Personalizar de Hola](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Haga clic con el botón derecho en **Grupo 1: Iniciar** y luego seleccione **Agregar acción posterior**.

    ![Clic con el botón derecho en Grupo 1: Iniciar y adición de acción posterior](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Haga clic en **Elegir un script**.

4. En hello **actualizar acción** hoja, la secuencia de comandos de nombre hello **Hello World**.

    ![módulo de acción de actualización de Hola](media/site-recovery-runbook-automation-new/update-rp.png)

5. Escriba un nombre de cuenta de Automation.
    >[!NOTE]
    > Hola cuenta de automatización puede estar en cualquier región de Azure. Hola cuenta de automatización debe estar en hello misma suscripción como almacén de Azure Site Recovery Hola.

6. En la cuenta de Automation, seleccione un runbook. Este runbook es el script de Hola que se ejecuta durante la ejecución de Hola Hola del plan de recuperación, después de la recuperación de hello del primer grupo de Hola.

7. script de Hola toosave, haga clic en **Aceptar**. script de Hola se agrega demasiado**grupo 1: pasos posteriores a la**.

    ![Acción posterior Grupo 1: Iniciar](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Consideraciones para agregar un script

* Opciones de demasiado**eliminar un paso** o **actualizar script de Hola**, haga clic en el script de Hola.
* Una secuencia de comandos puede ejecutar en Azure durante la conmutación por error desde un tooAzure de la máquina local. También puede ejecutarse en Azure como una secuencia de comandos del sitio primario antes del cierre, durante la conmutación por recuperación de máquina local de Azure tooan.
* Cuando se ejecuta un script, inserta un contexto del plan de recuperación. Hola de ejemplo siguiente muestra una variable de contexto:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Hello en la tabla siguiente enumera Hola nombre y una descripción de cada variable de contexto de Hola.

    | **Nombre de la variable** | **Descripción** |
    | --- | --- |
    | RecoveryPlanName |nombre de Hello del plan de Hola que se va a ejecutar. Esta variable le ayuda a realizar diferentes acciones basadas en nombre del plan de recuperación de Hola. También puede volver a usar script de Hola. |
    | FailoverType |Especifica si la conmutación por error de hello es una prueba, planeada o no planeada. |
    | FailoverDirection |Especifica si la recuperación es sitio primario o secundario de tooa. |
    | GroupID |Identifica el número de grupo de hello en el plan de recuperación de hello cuando se ejecuta el plan de Hola. |
    | VmMap |Una matriz de todas las máquinas virtuales en el grupo de Hola. |
    | Clave de VMMap |Clave única (GUID) para cada máquina virtual. Su Hola igual Hola Id. de Azure Virtual Machine Manager (VMM) de Hola de máquina virtual, si procede. |
    | SubscriptionId |Id. de suscripción de Azure de Hola Hola a máquina virtual en el que se creó. |
    | RoleName |nombre de Hola de hello VM de Azure que se va a recuperar. |
    | CloudServiceName |nombre de servicio de nube de Azure Hola que Hola a VM en la que se creó. |
    | ResourceGroupName|nombre del grupo de recursos de Azure Hola que Hola a VM en la que se creó. |
    | RecoveryPointId|marca de tiempo de Hola para cuando se recupera Hola máquina virtual. |

* Asegúrese de que esa cuenta de automatización de hello tiene Hola siguientes módulos:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Todos los módulos deben ser de versiones compatibles. Un tooensure de manera sencilla que todos los módulos sean compatibles es versiones más recientes de hello toouse de todos los módulos de Hola.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Obtener acceso a todas las máquinas virtuales de hello VMMap en un bucle
Usar hello siguiendo tooloop de código en todas las máquinas virtuales de hello VMMap Microsoft:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hola recursos grupo nombre de rol de valores de nombre y están vacíos al script de Hola es un grupo de arranque de acción previa tooa. valores de Hello se llenan solo si se realiza correctamente Hola máquinas virtuales de ese grupo de conmutación por error. script de Hola es una acción posterior a la del grupo de arranque de Hola.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Use Hola mismo runbook de automatización en varios planes de recuperación

Puede usar un solo script en varios planes de recuperación gracias a las variables externas. Puede usar [las variables de automatización de Azure](../automation/automation-variables.md) toostore parámetros que se pueden pasar en una recuperación del plan de ejecución. Al agregar el nombre del plan de recuperación de hello como una variable de toohello de prefijo, puede crear variables individuales para cada plan de recuperación. A continuación, utilice las variables de hello como parámetros. Puede cambiar un parámetro sin cambiar el script de Hola, pero todavía cambio Hola Hola forma funciona de la secuencia de comandos.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Uso de una variable de cadena simple en un script de runbook

En este ejemplo, una secuencia de comandos toma la entrada de Hola de un grupo de seguridad de red (NSG) y aplica toohello las máquinas virtuales de un plan de recuperación.

Para hello toodetect de script se ejecuta el plan de recuperación, use el contexto del plan de recuperación de hello:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply un NSG existente, debe conocer el nombre NSG de Hola y nombre del grupo de recursos de hello NSG. Use estas variables como entradas para los scripts del plan de recuperación. toodo esto, cree dos variables Hola activos de automatización de la cuenta. Agregar nombre de Hola Hola del plan de recuperación que va a crear parámetros de Hola para que un nombre de variable de toohello de prefijo.

1. Crear un nombre de variable toostore hello NSG. Agregar un nombre de variable de prefijo toohello mediante nombre de Hola Hola del plan de recuperación.

    ![Creación de una variable de nombre de NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Crear nombre de grupo de recursos de un NSG de hello toostore variable. Agregar un nombre de variable de prefijo toohello mediante nombre de Hola Hola del plan de recuperación.

    ![Creación de un nombre de grupo de recursos de NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  En el script de Hola, utilice Hola siguiendo los valores de variable de referencia código tooget hello:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Utilice variables de hello en el interfaz de red de hello runbook tooapply hello NSG toohello de Hola conmutó por error máquinas virtuales:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Para cada plan de recuperación, crear variables independientes para que se puede volver a usar script de Hola. Agregar un prefijo mediante el nombre del plan de recuperación de Hola. Para obtener un script completo, to-end para este escenario, vea [agregar un tooVMs NSG e IP públicas durante la conmutación por error de prueba de un plan de recuperación de Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Usar una variable complejo toostore más información

Considere un escenario en el que desea que un tooturn script único en una IP pública en máquinas virtuales específicas. En otro escenario, le podría interesar tooapply NSG diferentes en diferentes máquinas virtuales (no en todas las máquinas virtuales). Puede crear un script que se pueda volver a usar para cualquier plan de recuperación. Cada plan de recuperación puede tener un número variable de máquinas virtuales. Por ejemplo, una recuperación de SharePoint tiene dos servidores front-end. Una aplicación básica de línea de negocio (LOB) tiene solo un servidor front-end. No puede crear variables independientes para cada plan de recuperación. 

En el siguiente ejemplo de Hola, se utiliza una técnica nuevo y cree una [complejo de variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) en los activos de cuenta de automatización de Azure Hola. Para ello se especifican varios valores. Debe usar Azure PowerShell toocomplete Hola pasos:

1. En PowerShell, inicie sesión en tooyour suscripción de Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. parámetros de hello toostore, crear Hola complejo variable mediante nombre de Hola Hola del plan de recuperación:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. En esta variable complejo, **VMDetails** es hello Id. de máquina virtual para hello protegido la máquina virtual. Id. de máquina virtual, del tooget Hola Hola portal de Azure, ver las propiedades VM Hola. Hello captura de pantalla siguiente muestra una variable que almacena los detalles de Hola de dos máquinas virtuales:

    ![Usar hello Id. de máquina virtual como Hola GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Use esta variable en el runbook. Si Hola indica el que GUID de la VM se encuentra en el contexto del plan de recuperación de hello, hello NSG se aplican en hello VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. En su runbook, recorrer las máquinas virtuales de Hola de contexto del plan de recuperación de Hola. Compruebe si existe Hola VM en **$VMDetailsObj**. Si existe, obtener acceso a propiedades de Hola de Hola tooapply variable Hola NSG:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Puede usar Hola mismo script para los planes de recuperación diferente. Escriba los parámetros diferentes mediante el almacenamiento de valor de Hola que corresponde el plan de recuperación de tooa en distintas variables.

## <a name="sample-scripts"></a>Scripts de ejemplo

tooyour secuencias de comandos de ejemplo toodeploy cuenta de automatización, haga clic en hello **implementar tooAzure** botón.

[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Para obtener otro ejemplo, vea Hola después de vídeo. Muestra cómo toorecover una tooAzure de aplicación de WordPress de dos niveles:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Recursos adicionales
* [Cuenta de ejecución del servicio Azure Automation](../automation/automation-sec-configure-azure-runas-account.md)
* [Información general sobre Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "Información general sobre Azure Automation")
* [Scripts de ejemplo de Azure Automation](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Scripts de ejemplo de Azure Automation")
