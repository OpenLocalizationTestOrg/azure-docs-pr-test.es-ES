---
title: "listas de control de acceso al extremo de Azure aaaManage | PowerShell | Clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage ACL con PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Administrar listas de control de acceso de punto de conexión mediante PowerShell en el modelo de implementación clásica de Hola
Puede crear y administrar listas de Control de acceso (ACL) de red para extremos usando Azure PowerShell o en hello Portal de administración. En este tema, encontrará procedimientos para realizar tareas comunes de ACL mediante PowerShell. Hola Consulte lista de Azure PowerShell cmdlets [Cmdlets de administración de Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Para obtener más información acerca de las ACL, consulte [Acerca de las listas de control de acceso (ACL) de red](virtual-networks-acl.md). Si desea toomanage su ACL mediante el uso de hello Portal de administración, consulte [cómo tooSet extremos tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Administrar las ACL de red mediante Azure PowerShell
Puede utilizar toocreate de cmdlets de PowerShell de Azure, quitar y configurar (establecer) listas de Control de acceso (ACL) de red. Hemos incluido ejemplos de algunas maneras de hello que puede configurar una ACL mediante PowerShell.

tooretrieve obtener una lista completa de cmdlets de PowerShell de ACL de hello, puede utilizar cualquiera de los siguientes Hola:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Crear una ACL de red con reglas que permitan el acceso desde una subred remota
ejemplo de Hola siguiente ilustra un toocreate forma una nueva ACL que contiene las reglas. A continuación, se aplica esta ACL tooa extremo de máquina virtual. las reglas de ACL de Hello en el siguiente ejemplo de Hola permitirá el acceso desde una subred remota. toocreate una nueva ACL de red con reglas de permiso para una subred remota, abra un ISE de PowerShell de Azure. Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.

1. Crear el nuevo objeto de ACL de red Hola.
   
        $acl1 = New-AzureAclConfig
2. Establezca una regla que permita el acceso desde una subred remota. En el ejemplo de Hola a continuación, establecer reglas *100* (que tiene prioridad sobre la regla 200 y versiones posterior) subred remota de hello tooallow *10.0.0.0/8* acceso toohello extremo de máquina virtual. Reemplace los valores de hello con sus propios requisitos de configuración. nombre de Hola "SharePoint ACL config" debe reemplazarse con el nombre descriptivo de Hola que desea toocall esta regla.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Para otras reglas adicionales, repita el cmdlet hello, reemplazando los valores de hello con sus propios requisitos de configuración. Ser seguro toochange Hola regla número tooreflect Hola pedido en el que desea Hola reglas toobe aplicado. número de regla de Hello menor tiene prioridad sobre número mayor de Hola.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. A continuación, puede crear un nuevo extremo (Add) o establecer hello ACL para un extremo existente (Set). En este ejemplo, agregaremos que un nuevo extremo de máquina virtual denominado "web" y actualizar extremo de máquina virtual de hello con hello configuración de ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. A continuación, combinar los cmdlets de Hola y ejecute el script de Hola. En este ejemplo, hello cmdlets combinados sería similar al siguiente:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Quitar una regla de ACL de red que permita el acceso desde una subred remota
ejemplo de Hola siguiente ilustra un tooremove forma una regla de ACL de red.  reglas de tooremove una regla de ACL de red con permiso para una subred remota, abra un ISE de PowerShell de Azure. Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.

1. Primer paso es objeto de ACL de red tooget hello para el extremo de máquina virtual de Hola. A continuación, podrá quitar regla de ACL de Hola. En este caso, la estamos quitando por el identificador de regla. Esto solo quitará Hola de Id. de regla 0 de hello ACL. No elimina el objeto de ACL de Hola de extremo de máquina virtual de Hola.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. A continuación, debe aplicar el extremo de máquina virtual de toohello de objeto de ACL de red de Hola y actualizar la máquina virtual de Hola.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Quitar una ACL de red de un extremo de máquina virtual
En determinados escenarios, conviene tooremove un objeto de ACL de red desde un punto de conexión de máquina virtual. toodo que abra un ISE de PowerShell de Azure. Copie y pegue el script de Hola a continuación, configurar script de Hola con sus propios valores y, a continuación, ejecute el script de Hola.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Pasos siguientes
[¿Qué es una lista de control de acceso (ACL) de red?](virtual-networks-acl.md)

