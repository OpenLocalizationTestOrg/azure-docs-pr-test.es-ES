---
title: "aaaCreate una máquina virtual (clásica) con varias NIC - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual (clásica) con varias NIC con hello Azure interfaz de línea de comandos (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Crear una máquina virtual (clásica) con varias NIC con hello Azure CLI 1.0

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales. Varias NIC permiten la separación de tipos de tráfico a través de las NIC. Por ejemplo, una que NIC puede comunicarse con hello Internet, mientras que otra solo se comunica con los recursos internos no conectado toohello Internet. tráfico de red de Hello capacidad tooseparate entre varios NIC es necesario para muchos dispositivos virtuales red, por ejemplo, la entrega de aplicaciones y soluciones de optimización de la WAN.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo tooperform estos pasos con hello [modelo de implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.

## <a name="prerequisites"></a>Requisitos previos
Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario. toocreate Hola a estos recursos, completados los pasos que siguen. Crear una red virtual, siga los pasos de Hola Hola [crear una red virtual](virtual-networks-create-vnet-classic-cli.md) artículo.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Hola back-end de implementar las máquinas virtuales
Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:

* **Cuenta de almacenamiento en discos de datos**. Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium. Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.
* **NIC**. Cada VM tendrá dos NIC, una para el acceso de la base de datos y otra para la administración.
* **Conjunto de disponibilidad**. Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.

### <a name="step-1---start-your-script"></a>Paso 1: inicio del script
Puede descargar script de Hola intensiva de errores completa utilizado [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Hola completa siguiendo los pasos toochange Hola script toowork en su entorno:

1. Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Paso 2: creación de los recursos necesarios para las máquinas virtuales
1. Cree un nuevo servicio en la nube para todas las máquinas virtuales de back-end. Uso de Hola de aviso de hello `$backendCSName` variable nombre de grupo de recursos de hello, y `$location` para hello región de Azure.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Crear una cuenta de almacenamiento premium para hello SO y toobe de discos de datos utilizado por el suyo máquinas virtuales.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>Paso 3: crear máquinas virtuales con varias NIC
1. Iniciar un bucle toocreate varias máquinas virtuales, en función de hello `numberOfVMs` variables.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Para cada máquina virtual, especifique el nombre de Hola y dirección IP de cada uno de hello dos NIC.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Crear Hola máquina virtual. Observa Hola del uso de hello `--nic-config` parámetro, que contiene una lista de todas las NIC con nombre, la subred y la dirección IP.

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. Cree dos discos de datos por cada máquina virtual.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Paso 4: secuencia de comandos de ejecución Hola
Ahora que has descargado y cambia según sus necesidades, ejecutar copia Hola Hola de toocreate de secuencia de comandos de script de Hola finalizar máquinas virtuales de la base de datos con varias NIC.

1. Guarde el script y ejecútelo desde su terminal de **Bash** . Verá Hola iniciales de salida, tal y como se muestra a continuación.

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. Después de unos minutos, finalizará la ejecución de Hola y verá que el resto de Hola de salida de hello tal y como se muestra a continuación.

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
