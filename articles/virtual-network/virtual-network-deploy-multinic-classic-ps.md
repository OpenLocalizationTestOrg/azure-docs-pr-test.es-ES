---
title: "aaaCreate una máquina virtual (clásica) con varias NIC - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual (clásica) con varias NIC con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Crear una VM (clásica) con varias NIC mediante PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales. Varias NIC permiten la separación de tipos de tráfico a través de las NIC. Por ejemplo, una que NIC puede comunicarse con hello Internet, mientras que otra solo se comunica con los recursos internos no conectado toohello Internet. tráfico de red de Hello capacidad tooseparate entre varios NIC es necesario para muchos dispositivos virtuales red, por ejemplo, la entrega de aplicaciones y soluciones de optimización de la WAN.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md). Este artículo incluye el uso de modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Obtenga información acerca de cómo tooperform estos pasos con hello [modelo de implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.

## <a name="prerequisites"></a>Requisitos previos

Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario. toocreate Hola a estos recursos, completados los pasos que siguen. Crear una red virtual, siga los pasos de Hola Hola [crear una red virtual](virtual-networks-create-vnet-classic-netcfg-ps.md) artículo.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Crear máquinas virtuales de back-end de Hola
Hola que dependen de las máquinas virtuales de back-end durante la creación de hello de hello recursos siguientes:

* **Subred de back-end**. servidores de base de datos de Hello va a formar parte de una subred independiente, toosegregate tráfico. script de Hola siguiente espera este tooexist de subred en una red virtual denominada *WTestVnet*.
* **Cuenta de almacenamiento en discos de datos**. Para mejorar el rendimiento, los discos de datos de hello en los servidores de base de datos de hello usará la tecnología de estado sólido (SSD) de la unidad, que requiere una cuenta de almacenamiento premium. Asegúrese de hello seguro implementar almacenamiento premium de toosupport de ubicación de Azure.
* **Conjunto de disponibilidad**. Todos los servidores de base de datos se agregarán tooa único conjunto de disponibilidad, tooensure al menos una de las máquinas virtuales de hello está en funcionamiento durante el mantenimiento.

### <a name="step-1---start-your-script"></a>Paso 1: inicio del script
Puede descargar Hola script completo de PowerShell usa [aquí](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Siga los pasos de hello debajo toochange Hola script toowork en su entorno.

1. Cambiar valores de hello de hello las variables siguientes basadas en el grupo de recursos existente implementado anteriormente en [requisitos previos](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Cambiar los valores de hello de hello las variables siguientes basadas en valores de hello desea toouse para la implementación de back-end.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Paso 2: creación de los recursos necesarios para las máquinas virtuales
Deberá toocreate un nuevo servicio de nube y un almacenamiento de cuenta para los discos de datos de Hola para todas las máquinas virtuales. También necesitará toospecify una imagen y una cuenta de administrador local para hello las máquinas virtuales. toocreate estos recursos, completar Hola lo siguiente:

1. Cree un nuevo servicio en la nube.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Cree una cuenta de Almacenamiento premium.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Conjunto de la cuenta de almacenamiento Hola creada anteriormente como cuenta de almacenamiento actual de Hola para su suscripción.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Seleccione una imagen para hello máquina virtual.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Establecer las credenciales de cuenta de administrador local de Hola.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Paso 3: crear máquinas virtuales
Deberá toouse un bucle toocreate tal y como muchas máquinas virtuales como desee y crear Hola necesarios NIC y las máquinas virtuales en el bucle de Hola. Hola toocreate NIC y las máquinas virtuales, ejecute hello pasos.

1. Iniciar un `for` Hola de bucle toorepeat comandos toocreate una máquina virtual y dos NIC como tantas veces como sea necesario, basados en el valor de Hola de hello `$numberOfVMs` variable.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Crear un `VMConfig` objeto que especifica la imagen de hello, el tamaño y el conjunto de disponibilidad para VM Hola.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Hola aprovisionar máquinas virtuales como una máquina virtual de Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Establezca el valor predeterminado de hello NIC y asignar una dirección IP estática.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Agregue una segunda NIC para cada máquina virtual.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Crear discos de toodata para cada máquina virtual.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Crear cada máquina virtual y al final Hola bucle.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Paso 4: secuencia de comandos de ejecución Hola
Ahora que has descargado y cambiaron el script de Hola según sus necesidades, ejecución secuencia de comandos de base de datos de back-end de hello toocreate máquinas virtuales con varias NIC.

1. Guardar el script y ejecútelo desde hello **PowerShell** símbolo del sistema, o **PowerShell ISE**. Verá Hola iniciales de salida, tal y como se muestra a continuación.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Rellene la información de hello necesaria en el símbolo del sistema de hello las credenciales y haga clic en **Aceptar**. se devuelve la salida de Hello siguiente.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
