---
title: "aaaCreate una regla de equilibrador de carga de Azure para un clúster"
description: "Configurar los puertos de tooopen de un equilibrador de carga de Azure para el clúster de Azure Service Fabric."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Abrir puertos para un clúster de Service Fabric

equilibrador de carga de Hello implementado con el clúster de Azure Service Fabric dirige el tráfico tooyour aplicación que se ejecuta en un nodo. Si cambia su toouse de aplicación un puerto diferente, debe exponer dicho puerto (o enrutar un puerto diferente) Hola equilibrador de carga de Azure.

Cuando implementa la tooAzure de clúster de tejido de servicio, se crea automáticamente un equilibrador de carga. Si no tiene un equilibrador de carga, consulte [Creación de un equilibrador de carga orientado a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurar Service Fabric

La aplicación de Service Fabric **ServiceManifest.xml** el archivo de configuración define los puntos de conexión de hello toouse de espera de la aplicación. Después de que el archivo de configuración de hello ha sido actualizada toodefine un punto de conexión, equilibrador de carga de hello debe ser actualizada tooexpose ese (o a diferentes) puerto. Para obtener más información sobre cómo toocreate Hola extremo de tejido de servicio, consulte [configurar un punto de conexión](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Creación de una regla de equilibrador de carga

Una regla de equilibrador de carga se abre un puerto de conexión a internet y reenvía el puerto del nodo interno de tráfico toohello utilizado por la aplicación. Si no tiene un equilibrador de carga, consulte [Creación de un equilibrador de carga orientado a Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

regla toocreate un equilibrador de carga, necesita hello toocollect siguiente información:

- Nombre del equilibrador de carga.
- Grupo de recursos de hello equilibrador de carga y clúster de service fabric.
- Puerto externo.
- Puerto interno.

## <a name="azure-cli"></a>CLI de Azure
>[!NOTE]
>Si necesita toodetermine Hola nombre del equilibrador de carga de hello, utilice este get tooquickly de comando una lista de todos los grupos de recursos de hello asociado y equilibradores de carga.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Basta con un único comando toocreate una regla de equilibrador de carga con hello **CLI de Azure**. Solo tiene tooknow tanto nombre Hola de carga de hello equilibrador y recursos toocreate de grupo una nueva regla.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hola comando de CLI de Azure tiene unos parámetros que se describen en hello en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `--backend-port`  | aplicación de tejido de Hello puerto Hola servicio está escuchando. |
| `--frontend-port` | Hola Hola de puerto cargar equilibrador expone para las conexiones externas. |
| `-lb-name` | nombre de Hola de hello cargar equilibrador toochange. |
| `-g`       | grupo de recursos de Hello con equilibrador de carga de Hola y clúster de service fabric. |
| `-n`       | Hola elegido el nombre de regla de Hola. |


>[!NOTE]
>Para obtener más información sobre cómo toocreate un equilibrador de carga con hello CLI de Azure, consulte [crear un equilibrador de carga con hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Si necesita toodetermine Hola nombre del equilibrador de carga de hello, use este get tooquickly de comando una lista de todos los equilibradores de carga y grupos de recursos asociados.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell es un poco más complicado que Hola CLI de Azure. Conceptualmente, hacer Hola siguiendo los pasos toocreate una regla.

1. Obtener el equilibrador de carga de Hola de Azure.
2. Cree una regla.
3. Agregar equilibrador de carga de hello regla toohello.
4. Actualizar el equilibrador de carga de Hola.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Con respecto a hello `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` expone representa Hola puerto Hola equilibrador de carga para las conexiones externas y hello `-BackendPort` representa Hola puerto Hola tejido del servicio de aplicaciones está escuchando.

>[!NOTE]
>Para obtener más información sobre cómo toocreate un equilibrador de carga con PowerShell, vea [crear un equilibrador de carga con PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

