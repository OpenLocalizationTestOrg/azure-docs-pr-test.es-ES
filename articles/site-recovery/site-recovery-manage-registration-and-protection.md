---
title: "servidores de aaaRemove y deshabilite la protección | Documentos de Microsoft"
description: "Este artículo describe cómo almacén toounregister servidores de recuperación del sitio y que toodisable protección para máquinas virtuales y servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Quitar servidores y deshabilitar la protección

Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR). servicio de Hello organiza la replicación, conmutación por error y recuperación de máquinas virtuales y servidores físicos. Máquinas pueden ser replicada tooAzure o centro de datos local secundario tooa. Para obtener una introducción rápida, lea [¿Qué es Site Recovery?](site-recovery-overview.md)

Este artículo describe cómo toounregister servidores de servicios de recuperación de un almacén en hello portal de Azure y cómo se protege toodisable protección para máquinas con Site Recovery.

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Anulación del registro de un servidor de configuración conectado

Si replica máquinas virtuales de VMware o tooAzure de servidores físicos de Windows o Linux, puede anular el registro un servidor de configuración conectado desde un almacén como sigue:

1. Deshabilite la protección de la máquina. En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.
2. Anule la asociación de todas las directivas. En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **directivas de replicación**, haga doble clic en hello directiva asociada. Servidor de configuración contextual hello > **desasociar**.
3. Retire cualquier proceso local o servidores de destino maestros adicionales. En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **servidores de configuración**, servidor de Hola de menú contextual > **Eliminar**.
4. Eliminar el servidor de configuración de Hola.
5. Desinstalar manualmente el servicio de movilidad de hello ejecutando en el servidor de destino maestro hello (se trata de cualquier otro servidor o servidor de configuración de hello en ejecución).
6. Desinstale todos los servidores de procesos adicionales.
7. Desinstale el servidor de configuración de Hola.
8. En el servidor de configuración de hello, desinstale la instancia de Hola de MySQL que se instaló con Site Recovery.
9. En el registro de Hola Hola del servidor de configuración eliminar la clave de hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Anulación del registro de un servidor de configuración no conectado

Si replica máquinas virtuales de VMware o tooAzure de servidores físicos de Windows o Linux, puede anular el registro un servidor de configuración no conectada desde un almacén como sigue:

1. Deshabilite la protección de la máquina. En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**. Seleccione **dejar de administrar Hola máquina**.
2. Retire cualquier proceso local o servidores de destino maestros adicionales. En **infraestructura del sitio de recuperación** > **para VMWare & máquinas físicas** > **servidores de configuración**, servidor de Hola de menú contextual > **Eliminar**.
3. Eliminar el servidor de configuración de Hola.
4. Desinstalar manualmente el servicio de movilidad de hello ejecutando en el servidor de destino maestro hello (se trata de cualquier otro servidor o servidor de configuración de hello en ejecución).
5. Desinstale todos los servidores de procesos adicionales.
6. Desinstale el servidor de configuración de Hola.
7. En el servidor de configuración de hello, desinstale la instancia de Hola de MySQL que se instaló con Site Recovery.
8. En el registro de Hola Hola del servidor de configuración eliminar la clave de hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Anulación del registro de un servidor VMM conectado

Como práctica recomendada, se recomienda que anule el registro de servidor VMM hello cuando se ha conectado tooAzure. Esto garantiza que en los servidores VMM hello (y en otros servidores VMM a nubes emparejadas) se borra la configuración correctamente. Debe quitar un servidor no conectado solo si hay un problema permanente con la conectividad. Si no está conectado el servidor VMM hello, será necesario toomanually ejecutar un tooclean script la configuración.

1. Detener la replicación de máquinas virtuales en nubes en el servidor VMM que desee tooremove Hola.
2. Eliminar cualquier asignación de red utilizado por las nubes en el servidor VMM que desee toodelete Hola. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **asignación de red**, haga clic en la asignación de red hello >  **Eliminar**.
3. Desvincular directivas de replicación de las nubes en el servidor VMM que desee tooremove Hola.  En **infraestructura del sitio de recuperación** > **para System Center VMM** >  **directivas de replicación**, haga doble clic en directiva de hello asociado. Pulse el botón derecho en la nube hello > **desasociar**.
4. Eliminar servidor VMM de Hola o un nodo activo de VMM. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **servidores VMM**, servidor de hello contextual >  **Eliminar**.
5. Desinstalar Hola proveedor de forma manual en el servidor VMM Hola. Si tiene un clúster, quítelo de todos los nodos.
6. Si replica tooAzure, quite manualmente el agente de servicios de recuperación de Microsoft de Hola de hosts de Hyper-V en nubes de hello eliminado.



### <a name="unregister-an-unconnected-vmm-server"></a>Anulación del registro de un servidor VMM desconectado

1. Detener la replicación de máquinas virtuales en nubes en el servidor VMM que desee tooremove Hola.
2. Eliminar cualquier asignación de red utilizado por las nubes en servidores VMM de Hola que desee toodelete. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **asignación de red**, haga clic en la asignación de red hello >  **Eliminar**.
3. Tenga en cuenta Id. de Hola Hola del servidor de VMM.
4. Desvincular directivas de replicación de las nubes en el servidor VMM que desee tooremove Hola.  En **infraestructura del sitio de recuperación** > **para System Center VMM** >  **directivas de replicación**, haga doble clic en directiva de hello asociado. Pulse el botón derecho en la nube hello > **desasociar**.
5. Eliminar servidor VMM de Hola o un nodo activo. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **servidores VMM**, servidor de hello contextual >  **Eliminar**.
6. Descargue y ejecute hello [script de limpieza](http://aka.ms/asr-cleanup-script-vmm) en servidor VMM Hola. Abra PowerShell con hello **ejecutar como administrador** opción, la directiva de ejecución de toochange hello para el ámbito de hello predeterminado (LocalMachine). En el script de Hola, especificar el identificador de Hola de hello servidor VMM que desee tooremove. script de Hola quita el registro y la información del servidor de Hola de emparejamiento de nube.
5. Ejecutar script de limpieza de hello en otros servidores VMM que contienen las nubes que se emparejan con nubes en el servidor VMM que desee tooremove Hola.
6. Ejecutar script de limpieza de Hola en cualquier otros pasivo VMM nodos del clúster que tengan Hola que proveedor instalado.
7. Desinstalar Hola proveedor de forma manual en el servidor VMM Hola. Si tiene un clúster, quítelo de todos los nodos.
8. Si replicar tooAzure, se puede quitar al agente de servicios de recuperación de Microsoft hello desde hosts de Hyper-V en nubes de hello eliminado.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Anulación del registro de un host Hyper-V en un sitio de Hyper-V

Los hosts Hyper-V que no están administrados por VMM se reúnen en un sitio de Hyper-V. Puede eliminar un host en un sitio Hyper-V de la forma siguiente:

1. Deshabilite la replicación para máquinas virtuales de Hyper-V ubicadas en el host de Hola.
2. Anular la asociación de las directivas para el sitio de Hyper-V de Hola. En **infraestructura del sitio de recuperación** > **para sitios de Hyper-V** >  **directivas de replicación**, haga doble clic en directiva de hello asociado. Sitio de hello contextual > **desasociar**.
3. Elimine los hosts de Hyper-V. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **Hosts de Hyper-V**, servidor de hello contextual >  **Eliminar**.
4. Eliminar sitio Hola Hyper-V después de han eliminados todos los hosts del mismo. En **infraestructura del sitio de recuperación** > **para System Center VMM** > **sitios de Hyper-V**, sitio de hello contextual >  **Eliminar**.
5. Ejecute hello siguiente secuencia de comandos en cada host de Hyper-V que se haya quitado. script de Hola limpia la configuración en el servidor de Hola y anula el registro del almacén de Hola.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Deshabilitación de la protección de una máquina virtual de VMware o un servidor físico

1. En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.
2. En **Remove Machine** (Quitar máquina), seleccione una de estas opciones:
    - **Deshabilite la protección de máquina de hello (recomendado)**. Utilice este toostop opción replicar máquina Hola. La configuración de Site Recovery se limpiará automáticamente. Solo verá esta opción en hello siguientes circunstancias:
        - **Se cambia el tamaño de volumen de la máquina virtual de Hola**: cuando cambia el tamaño de un saludo del volumen virtual máquina entra en un estado crítico. Seleccione esta opción de la protección de toodisables conservando los puntos de recuperación en Azure. Al habilitar la protección de máquina de Hola de nuevo, datos de hello para el volumen de hello cambia de tamaño serán tooAzure transferido.
        - **Se ha ejecutado recientemente una conmutación por error**: una vez ejecutado un tootest de conmutación por error en su entorno, seleccione este toostart opción proteger máquinas locales de nuevo. Deshabilita cada máquina virtual y, a continuación, necesita tooenable protección para ellos nuevo. Deshabilitar máquina Hola con esta configuración no afecta a la máquina virtual de réplica hello en Azure. No desinstale el servicio de movilidad de saludo de la máquina de Hola.
    - **Detener administración de máquina de hello**. Si selecciona esta opción, solo se quitará máquina Hola del almacén de Hola. No se verá afectada la configuración de protección local para la máquina de Hola. configuración de tooremove de máquina de Hola y máquina de hello tooremove de hello suscripción de Azure, necesita una configuración de hello tooclean, desinstale el servicio de movilidad de Hola.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Deshabilitación de la protección de una máquina virtual de Hyper-V en una nube VMM

1. En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.
2. En **Remove Machine** (Quitar máquina), seleccione una de estas opciones:

    - **Deshabilite la protección de máquina de hello (recomendado)**. Utilice este toostop opción replicar máquina Hola. La configuración de Site Recovery se limpiará automáticamente.
    - **Detener administración de máquina de hello**. Si selecciona esta opción, solo se quitará máquina Hola del almacén de Hola. No se verá afectada la configuración de protección local para la máquina de Hola. configuración de tooremove de máquina de Hola y máquina de hello tooremove de hello suscripción de Azure, necesita tooclean Hola una configuración de seguridad manualmente, mediante instrucciones de hello siguientes. Tenga en cuenta que si selecciona la máquina virtual de toodelete hello y sus discos duros, deberá quitarse de ubicación de destino de Hola.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Limpiar la configuración de protección - sitio secundario de VMM de replicación tooa

Si seleccionó **detener administración de máquina de hello** y que replicar tooa sitio secundario, ejecute este script en hello servidor principal tooclean la configuración de Hola de máquina virtual principal de Hola. En la consola VMM Hola haga clic en consola de PowerShell VMM Hola PowerShell botón tooopen Hola. Reemplace SQLVM1 por nombre de saludo de la máquina virtual.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. En el servidor VMM secundario de hello ejecute este tooclean script la configuración de hello para la máquina virtual secundaria de hello:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. En el servidor VMM secundario de hello, actualizar máquinas virtuales de hello en el servidor de host de Hyper-V de hello, de modo que hello VM secundaria obtiene volvió a detectar en la consola VMM Hola.
4. Hola anteriormente pasos borrar la configuración de replicación de hello en el servidor VMM Hola. Si desea que la replicación de toostop para la máquina virtual de hello, ejecutar la siguiente secuencia de comandos al final de Hola Hola máquinas virtuales principales y secundarias. Reemplace SQLVM1 por nombre de saludo de la máquina virtual.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Limpiar la configuración de protección - tooAzure de replicación

1. Si seleccionó **detener administración de máquina de hello** y replicar tooAzure, ejecute este script Hola servidor VMM de origen, con PowerShell desde la consola VMM Hola.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hola anteriormente pasos borrar la configuración de replicación de hello en servidor VMM Hola. replicación de toostop para la máquina virtual de hello ejecutando en el servidor de host de Hyper-V de hello, ejecute este script. Reemplace SQLVM1 por nombre de hello de la máquina virtual y host01.contoso.com con el nombre de saludo del servidor de host de Hyper-V de Hola.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Deshabilitación de la protección de una máquina virtual de Hyper-V en un sitio de Hyper-V

Utilice este procedimiento si replica máquinas virtuales de Hyper-V tooAzure sin un servidor VMM.

1. En **elementos protegidos** > **replican elementos**, máquina de hello contextual > **eliminar**.
2. En **quitar máquina**, puede seleccionar Hola siguientes opciones:

   - **Deshabilite la protección de máquina de hello (recomendado)**. Utilice este toostop opción replicar máquina Hola. La configuración de Site Recovery se limpiará automáticamente.
   - **Detener administración de máquina de hello**. Si selecciona esta opción máquina Hola solo se quitará del almacén de Hola. No se verá afectada la configuración de protección local para la máquina de Hola. configuración de tooremove de máquina de Hola y tooremove Hola virtual machine de hello suscripción de Azure, necesita tooclean Hola una configuración de seguridad manualmente. Si selecciona la máquina virtual de toodelete hello y sus discos duros se quitarán de la ubicación de destino de Hola.
3. Si seleccionó **detener administración de máquina de hello**, ejecute este script en el servidor de host de Hyper-V de origen de hello, la replicación de tooremove para la máquina virtual de Hola. Reemplace SQLVM1 por nombre de saludo de la máquina virtual.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
