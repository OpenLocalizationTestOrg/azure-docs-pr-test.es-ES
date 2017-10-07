---
title: "aaaAvailability establece el tutorial para máquinas virtuales de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello conjuntos de disponibilidad para máquinas virtuales de Linux en Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>¿Cómo se establece toouse disponibilidad


En este tutorial, obtendrá información sobre cómo la disponibilidad de hello tooincrease y la confiabilidad de las soluciones de la máquina Virtual en Azure con una capacidad de llamar conjuntos de disponibilidad. Conjuntos de disponibilidad Asegúrese de que las máquinas virtuales se implementan en Azure se distribuyen entre varios clústeres de hardware aislados de Hola. Esto garantiza que, si se produce un error de hardware o software dentro de Azure, solo un subjuego de las máquinas virtuales se verán afectado y que la solución general permanecerá disponible y en funcionamiento desde la perspectiva de Hola de los clientes de usarlo.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear un conjunto de disponibilidad
> * Crear una máquina virtual en un conjunto de disponibilidad
> * Comprobar los tamaños de máquina virtual disponibles


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Información general sobre conjuntos de disponibilidad

Un conjunto de disponibilidad es una capacidad de agrupación lógica que puede usar en Azure tooensure que los recursos de máquina virtual de Hola que se coloca dentro de él están aislados entre sí cuando se implementan en un centro de datos de Azure. Azure garantiza que las máquinas virtuales se coloca dentro de un conjunto de disponibilidad que se ejecute en varios servidores físicos de hello, proceso racks, unidades de almacenamiento y conmutadores de red. Esto garantiza que en caso de hello de un error hardware o software de Azure, solo un subconjunto de las máquinas virtuales se verán afectado, y la aplicación global se mantienen actualizados y continuar a toobe tooyour disponibles clientes. Usar conjuntos de disponibilidad es una capacidad fundamental tooleverage cuando desee que las soluciones de nube confiable toobuild.

Veamos una solución basada en máquina virtual típica en la podría haber 4 servidores web front-end y usar 2 máquinas virtuales de back-end que hospedan una base de datos. Con Azure, desearía toodefine dos conjuntos de disponibilidad antes de implementar las máquinas virtuales: conjunto de disponibilidad de uno para la capa de "web" de Hola y un conjunto de disponibilidad de nivel de "database" Hola. Cuando se crea una nueva máquina virtual, a continuación, puede especificar el conjunto como una máquina virtual de parámetro toohello az crear comandos y Azure automáticamente asegurará de que hello las máquinas virtuales que cree en hello disponible de la disponibilidad de hello conjunto están aislados entre varios recursos de hardware físico. Esto significa que si el hardware físico de Hola que uno de su servidor Web o máquinas virtuales del servidor de base de datos se ejecuta en tiene un problema, sabe que Hola otras instancias de servidor Web y máquinas virtuales de la base de datos seguirá ejecutándose correctamente porque están en un hardware diferente.

Debe utilizar siempre los conjuntos de disponibilidad cuando desee que las soluciones basadas en VM confiable toodeploy dentro de Azure.


## <a name="create-an-availability-set"></a>Crear un conjunto de disponibilidad

Puede crear el conjunto de disponibilidad mediante [az vm availability-set create](/cli/azure/vm/availability-set#create). En este ejemplo, establecemos ambos en número de dominios de actualización y error en hello *2* para el conjunto con nombre de la disponibilidad de hello *myAvailabilitySet* en hello *myResourceGroupAvailability*grupo de recursos.

Cree un grupo de recursos.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Conjuntos de disponibilidad permiten tooisolate recursos entre "dominios de error" y "Actualizar dominios". Un **dominio de error** representa una colección aislada de recursos de almacenamiento, red y servidor. En el anterior ejemplo de Hola, indicamos que queremos que toobe distribuida en al menos dos dominios de error cuando se implementan máquinas virtuales de nuestro conjunto de nuestra disponibilidad. También especificamos que queremos que nuestro conjunto de disponibilidad se distribuya entre dos **dominios de actualización**.  Dos dominios de actualización Asegúrese de que, cuando Azure lleva a cabo las actualizaciones de software nuestros recursos de máquina virtual estén aislados, evitar todo el software Hola ejecutando debajo de la máquina virtual desde la que se está actualizando en hello mismo tiempo.

## <a name="configure-virtual-network"></a>Configuración de una red virtual
Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual. Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Crear recursos de red
Cree la red virtual con el comando [az network vnet create](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con una subred denominada *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
Las NIC virtuales se crean con el comando [az network nic create](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea tres NIC virtuales. (Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos). Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Creación de VM dentro de un conjunto de disponibilidad

Las máquinas virtuales deben crearse dentro de hello disponibilidad conjunto toomake seguro de que se distribuyen correctamente a través de hardware de Hola. No se puede agregar un grupo de disponibilidad de tooan VM establecer después de crearlo. 

Cuando se crea una máquina virtual mediante [crear vm az](/cli/azure/vm#create) especificar Hola conjunto de disponibilidad mediante hello `--availability-set` nombre del parámetro toospecify Hola Hola del conjunto de disponibilidad.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Ahora tenemos dos máquinas virtuales en nuestro conjunto de disponibilidad recién creado. Hola mismo porque están en el conjunto de disponibilidad, Azure asegurará de que las máquinas virtuales de Hola y todos sus recursos (incluidos los discos de datos) se distribuyen a través de hardware físico aislado. Esta distribución ayuda a garantizar una mayor disponibilidad de nuestra solución de máquina virtual.

Único lo que se puede encontrar a medida que agregue las máquinas virtuales es que un determinado tamaño de máquina virtual ya no está disponible toouse dentro de su conjunto de disponibilidad. Este problema puede suceder si ya no es suficiente tooadd capacidad conservando el conjunto de disponibilidad de hello aislamiento reglas Hola exige. Puede comprobar toosee qué tamaños de máquina virtual son toouse disponible dentro de un grupo de disponibilidad que se establecen a través de hello `--availability-set list-sizes` parámetro.

## <a name="check-for-available-vm-sizes"></a>Comprobación de los tamaños de VM disponibles 

Puede agregar más máquinas virtuales toohello conjunto de disponibilidad posteriormente, pero necesita tooknow qué tamaños de máquinas virtuales están disponibles en el hardware de Hola. Use [lista-tamaños del conjunto de disponibilidad de máquinas virtuales az](/cli/azure/availability-set#list-sizes) toolist todos los tamaños disponibles de hello en hardware de Hola de clúster para el conjunto de disponibilidad de Hola.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Crear un conjunto de disponibilidad
> * Crear una máquina virtual en un conjunto de disponibilidad
> * Comprobar los tamaños de máquina virtual disponibles

Avanzar toohello toolearn de tutorial siguiente sobre conjuntos de escalas de máquina virtual.

> [!div class="nextstepaction"]
> [Creación de un conjunto de escalado de máquinas virtuales](tutorial-create-vmss.md)

