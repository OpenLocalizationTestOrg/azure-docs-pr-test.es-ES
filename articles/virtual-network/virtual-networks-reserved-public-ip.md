---
title: "aaaManage Azure reservado de direcciones IP (clásico) - PowerShell | Documentos de Microsoft"
description: "Comprender las direcciones IP reservadas (clásico) y cómo toomanage mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Direcciones IP reservadas (clásico)

> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI de Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Plantilla](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (clásico)](virtual-networks-reserved-public-ip.md)

Las direcciones IP en Azure se dividen en dos categorías: dinámicas y reservadas. Las direcciones IP públicas administradas por Azure son dinámicas de forma predeterminada. Ese decir Hola dirección IP usada para un servicio de nube determinado (VIP) o tooaccess que una máquina virtual o instancia de rol directamente (ILPIP) puede cambiar de tiempo tootime, cuando los recursos se apague o detenidos (desasignados).

direcciones IP de tooprevent cambie, puede reservar una dirección IP. Direcciones IP reservadas se puede utilizar como una VIP, asegurarse de esa dirección IP de Hola para servicio de nube de hello sigue siendo Hola mismo, incluso cuando los recursos se cierran o detenida (desasignada). Además, puede convertir existente IP dinámicas que se utiliza como una dirección IP de tooa reservado de VIP.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo tooreserve una estática pública IP dirección utilizando Hola [modelo de implementación del Administrador de recursos](virtual-network-ip-addresses-overview-arm.md).

direcciones toolearn más información acerca de IP en Azure, lea hello [direcciones IP](virtual-network-ip-addresses-overview-classic.md) artículo.

## <a name="when-do-i-need-a-reserved-ip"></a>¿Cuándo se necesita una IP reservada?
* **Desea tooensure que Hola IP está reservada en su suscripción**. Si desea tooreserve una dirección IP que no se libera de su suscripción bajo ninguna circunstancia, debe usar una IP pública reservada.  
* **Desea que su toostay IP con el servicio de nube incluso a través detenido o desasignado (máquinas virtuales) del estado**. Si desea que su toobe servicio acceso mediante una dirección IP que no cambia, incluso cuando la nube de máquinas virtuales en hello servicio se hayan cerrado o detener (desasignado).
* **Desea que el tráfico saliente desde Azure use una dirección IP predecible de tooensure**. Puede que tenga el tráfico local firewall configurado tooallow solo desde direcciones IP específicas. Al reservar una dirección IP, sabrá que la IP de origen de Hola de direcciones y no es necesario tooupdate las reglas del firewall debido a cambios IP tooan.

## <a name="faq"></a>P+F
1. ¿Puedo usar una IP reservada para todos los servicios de Azure? <br>
    No. Las IP reservadas solo pueden usarse para máquinas virtuales y roles de instancia del servicio en la nube que se hayan expuesto a través de una VIP.
2. ¿Cuántas direcciones IP reservadas puedo tener? <br>
    Para obtener más información, vea hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.
3. ¿Hay un cargo por las IP reservadas? <br>
    A veces. Para obtener más detalles, consulte hello [detalles de precios de la dirección de IP reservada](http://go.microsoft.com/fwlink/?LinkID=398482) página.
4. ¿Cómo se reserva una dirección IP? <br>
    Puede usar PowerShell, hello [API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o hello [portal de Azure](https://portal.azure.com) tooreserve una dirección IP en una región de Azure. Una dirección IP reservada es suscripción tooyour asociado.
5. ¿Puedo usar una IP reservada con redes virtuales basadas en grupos de afinidad? <br>
    No. Las IP reservadas solo se admiten en redes virtuales regionales. Las IP reservadas no se admiten para redes virtuales asociadas a grupos de afinidad. Para obtener más información sobre cómo asociar una red virtual a una región o un grupo de afinidad, vea hello [acerca de las redes virtuales regionales y grupos de afinidad](virtual-networks-migrate-to-regional-vnet.md) artículo.

## <a name="manage-reserved-vips"></a>Administración de VIP reservadas

Asegúrese de que haya instalado y configurado PowerShell siguiendo los pasos de Hola Hola [instalar y configurar PowerShell](/powershell/azure/overview) artículo. 

Para poder usar direcciones IP reservadas, se debe agregar suscripción tooyour. toocreate una dirección IP reservada del grupo de Hola de IP pública de direcciones disponibles en hello *Central US* ubicación, ejecute el siguiente comando de hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

Sin embargo, tenga en cuenta que no puede especificar qué IP se va a reservar. tooview ¿qué direcciones IP están reservadas en su suscripción, ejecute hello siguiente comando de PowerShell y observe los valores de hello en *ReservedIPName* y *dirección*:

```powershell
Get-AzureReservedIP
```

Resultado esperado:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Cuando se crea una dirección IP reservada con PowerShell, no puede especificar una dirección IP Hola reservado de recursos grupo toocreate en. Azure lo coloca automáticamente en un grupo de recursos llamado *Default-Networking*. Si crea la dirección IP de hello reservado mediante hello [portal de Azure](http://portal.azure.com), puede especificar cualquier grupo de recursos que elija. Si creas Hola reservado IP en un grupo de recursos distinto de *predeterminado redes* sin embargo, cada vez que se hace referencia a Hola dirección IP reservada con comandos como `Get-AzureReservedIP` y `Remove-AzureReservedIP`, debe hacer referencia el nombre de hello *Nombre del grupo de recursos reservados-ip-nombre del grupo*.  Por ejemplo, si creas una IP reservada denominada *myReservedIP* en un grupo de recursos denominado *myResourceGroup*, debe hacer referencia a nombre Hola de IP de hello reservado como *myResourceGroup de grupo myReservedIP*.   

Una vez que se reserva una dirección IP, permanece asociado tooyour suscripción hasta que la elimine. toodelete una dirección IP reservada, Hola ejecución siguiente comando de PowerShell:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Reservar la dirección IP de Hola de un servicio de nube existente
Puede reservar dirección IP de Hola de un servicio de nube existente mediante la adición de hello `-ServiceName` parámetro. dirección IP de hello tooreserve de un servicio de nube *TestService* en hello *Central US* ubicación, ejecute el siguiente comando de PowerShell de hello:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Asociar un reservada IP tooa nuevo servicio de nube
Hello siguiente script crea una dirección de IP reservada nuevas, a continuación, lo asocia el nuevo servicio de nube tooa denominado *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Cuando se crea un toouse IP reservada con un servicio de nube, seguir haciendo referencia toohello VM mediante el uso de *VIP:&lt;número de puerto >* para las comunicaciones entrantes. Reservar una dirección IP no significa que puede conectarse directamente toohello máquina virtual. Hello IP reservada se asigna en la nube toohello servicio ese hello en la máquina virtual se ha implementado en. Si desea tooconnect tooa máquina virtual por medio de IP directamente, deberá tooconfigure una IP pública a nivel de instancia. Una dirección IP pública de nivel de instancia es un tipo de IP pública (denominado un ILPIP) que se asigna directamente tooyour máquina virtual. No se puede reservar. Para obtener más información, lea hello [IP pública de nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) artículo.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Eliminación de una dirección IP reservada de una implementación en ejecución
una dirección IP reservada tooremove agregado tooa nuevo servicio en la nube, ejecute el siguiente comando de PowerShell de hello:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Quitar una dirección IP reservada de una implementación en ejecución no quita la reserva de Hola desde su suscripción. Simplemente libera Hola IP toobe utilizado por otro recurso de la suscripción.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Asociar un tooa IP reservada ejecutando implementación
Hello siguientes comandos crean un servicio de nube denominado *TestService2* con una nueva máquina virtual denominada *TestVM2*. Hola existente reservado IP denominado *MyReservedIP* es, a continuación, el servicio en la nube toohello asociado.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Asociar un servicio de nube de tooa IP reservado mediante un archivo de configuración de servicio
También puede asociar un servicio de nube de tooa IP reservado mediante un archivo de configuración (CSCFG) de servicio. Hello xml de ejemplo siguiente muestra cómo tooconfigure una toouse de servicio de nube una VIP reservada denominado *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Pasos siguientes
* Comprender cómo [el direccionamiento IP](virtual-network-ip-addresses-overview-classic.md) funciona en el modelo de implementación clásica de Hola.
* Obtenga más información acerca de las [direcciones IP privadas reservadas](virtual-networks-reserved-private-ip.md).
* Obtenga más información acerca de las [direcciones IP públicas de nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md).

