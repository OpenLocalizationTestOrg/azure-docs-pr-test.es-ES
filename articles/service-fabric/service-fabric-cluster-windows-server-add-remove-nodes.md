---
title: "aaaAdd o quitar nodos tooa independiente clúster de Service Fabric | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd o quitar nodos tooan Azure Service Fabric clúster en una máquina física o virtual ejecuta Windows Server, que puede ser local o en cualquier nube."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Agregar o quitar el clúster de Service Fabric como nodos tooa independiente que se ejecuta en Windows Server
Una vez haya [creó el clúster de Service Fabric independientes en equipos con Windows Server](service-fabric-cluster-creation-for-windows-server.md), pueden cambiar sus necesidades empresariales y tal vez necesite tooadd o quitar nodos tooyour clúster. Este artículo proporciona los pasos detallados tooachieve esto. Tenga en cuenta que no se permite agregar o eliminar nodos en los clústeres de desarrollo local.

## <a name="add-nodes-tooyour-cluster"></a>Agregar nodos tooyour clúster
1. Hola preparar la máquina virtual u otro equipo que desee tooadd tooyour clúster siguiendo los pasos de hello mencionados en hello [Hola de preparar máquinas toomeet requisitos previos de hello para la implementación de clúster](service-fabric-cluster-creation-for-windows-server.md) sección
2. Identificar qué dominio de error y el dominio de actualización son tooadd continuo que esta máquina virtual/máquina
3. Escritorio remoto (RDP) en hello VM u otro equipo que desea que el clúster de toohello tooadd
4. Copia o [Descargar paquete de independiente de Hola para Service Fabric para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina y descomprima el paquete de Hola
5. Ejecutar Powershell con privilegios elevados y vaya toohello ubicación del paquete descomprimida Hola
6. Ejecute hello *AddNode.ps1* secuencia de comandos con parámetros de Hola que describen Hola nuevo nodo tooadd. ejemplo de Hola siguiente agrega un nuevo nodo denominado VM5, con el tipo NodeType0 y una dirección IP 182.17.34.52, en UD1 y fd: / dc1/r0. Hola *ExistingClusterConnectionEndPoint* ya está un extremo de conexión para un nodo de clúster existente de hello, que puede ser la dirección IP de Hola de *cualquier* nodo de clúster de Hola.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Una vez que el script de Hola finaliza su ejecución, puede comprobar si se ha agregado el nuevo nodo de hello ejecutando hello [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.

7. tooensure coherencia a través de varios nodos en clúster de hello, debe iniciar una actualización de la configuración. Ejecutar [ServiceFabricClusterConfiguration Get](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Hola archivo de configuración más reciente y agregar Hola recién agregado nodo demasiado sección "Nodos". También se recomienda tooalways tiene la configuración de clúster más reciente de hello disponible en caso de Hola que necesita un clúster con hello tooredploy misma configuración.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric. Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Agregar nodos tooclusters configurado con seguridad de Windows que usan gMSA.
En clústeres configurados con cuentas de servicio administradas de grupo (gMSA)(https://technet.microsoft.com/library/hh831782.aspx), se puede agregar un nuevo nodo mediante una actualización de configuración:
1. Ejecutar [ServiceFabricClusterConfiguration Get](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) en cualquiera de los nodos existentes de hello tooget Hola archivo de configuración más reciente y agregar los detalles acerca del nuevo nodo de hello desea tooadd en sección Hola "nodos". Asegúrese de que el nuevo nodo de hello forma parte del programa Hola misma cuenta administrada de grupo. Esta cuenta debe ser un administrador en todos los equipos.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric. Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Agregar clúster de tooyour de tipos de nodo
En Ordenar tooadd un nuevo tipo de nodo, modifique su configuración tooinclude Hola nuevo tipo de nodo en la sección "NodeTypes" en "Propiedades" y empezar a una configuración de actualización mediante [ServiceFabricClusterConfigurationUpgrade de inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Una vez completada la actualización de hello, puede agregar el nuevo clúster de nodos tooyour con este tipo de nodo.

## <a name="remove-nodes-from-your-cluster"></a>Eliminación de nodos del clúster
Puede quitarse un nodo de un clúster con una actualización de la configuración, en hello siguiente manera:

1. Ejecutar [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) archivo de configuración más reciente de tooget hello y *quitar* nodo Hola desde la sección "Nodos".
Agregar Hola "NodesToBeRemoved" parámetro demasiado "el programa de instalación" sección dentro de la sección "FabricSettings". Hola "valor" debe ser una lista separada por comas de nombres de nodo de los nodos que necesitan toobe quitar.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Ejecutar [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) actualización de hello toobegin.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric. Como alternativa, puede ejecutar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> La eliminación de nodos puede iniciar varias actualizaciones. Algunos nodos se marcan con `IsSeedNode=”true”` etiqueta y se pueden identificar consultando clúster Hola manifiesto mediante `Get-ServiceFabricClusterManifest`. Eliminación de estos nodos puede tardar más que otros debido a que los nodos de valor de inicialización de hello tendrán toobe mueven en tales escenarios. clúster de Hello debe mantener un mínimo de 3 nodos de tipo de nodo principal.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Eliminación de tipos de nodo del clúster
Antes de quitar un tipo de nodo, compruebe de nuevo si hay nodos que hacen referencia a tipo de nodo de Hola. Quite estos nodos antes de quitar el tipo de nodo correspondiente Hola. Una vez que se quitan todos los nodos correspondientes, puede quitar Hola NodeType de configuración de clúster de Hola y empezar a una configuración de actualización mediante [ServiceFabricClusterConfigurationUpgrade inicio](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Sustitución de los nodos principales del clúster
reemplazo de Hola de nodos principales debe ser realizada un nodo tras otra, en lugar de quitar y, a continuación, agregarlos en lotes.


## <a name="next-steps"></a>Pasos siguientes
* [Opciones de configuración de clústeres de Windows independientes](service-fabric-cluster-manifest.md)
* [Protección de un clúster de Windows independiente mediante certificados](service-fabric-windows-cluster-x509-security.md)
* [Creación de un clúster de Service Fabric independiente con VM de Azure con Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)

