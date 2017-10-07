---
title: "aaaCreate una máquina Virtual de SQL Server en Azure PowerShell (Administrador de recursos) | Documentos de Microsoft"
description: "Ofrece pasos y scripts de PowerShell para crear una máquina virtual de Azure con imágenes de la galería de máquinas virtuales de SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Información general
Este tutorial muestra cómo toocreate una sola máquina virtual de Azure utilizando Hola **Azure Resource Manager** modelo de implementación mediante cmdlets de PowerShell de Azure. En este tutorial, creamos una sola máquina virtual con una sola unidad de disco de una imagen en hello Galería de SQL. Se creará nuevos proveedores de almacenamiento de hello, red y recursos de proceso que se usará para la máquina virtual de Hola. Si ya dispone de proveedores existentes para cualquiera de estos recursos, puede usarlos en su lugar.

Si necesita hello versión básica de este tema, consulte [aprovisionar una máquina virtual de SQL Server con PowerShell de Azure clásico](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Requisitos previos
Para este tutorial, necesitará:

* una cuenta de Azure y una suscripción antes de empezar. Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview), versión 1.4.0 (mínima) o posterior (en este tutorial se usa la versión 1.5.0).
  * tooretrieve su versión, escriba **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configuración de su suscripción
Abra Windows PowerShell y establecer acceso tooyour cuenta de Azure ejecutando el siguiente cmdlet de Hola. Se le presentará un inicio de sesión en la pantalla tooenter sus credenciales. Use Hola mismo correo electrónico y la contraseña que usa toosign en toohello portal de Azure.

    Add-AzureRmAccount

Tras iniciar sesión correctamente en verá parte de la información en pantalla que incluye SubscriptionId Hola con la que ha iniciado sesión en. Se trata de una suscripción de hello en el que se crearán los recursos de Hola para este tutorial a menos que cambie tooa otra suscripción. Si tiene varios identificadores de suscripción, ejecute hello siguiente cmdlet tooreturn una lista de todos los identificadores de suscripción:

    Get-AzureRmSubscription

toochange tooanother Id. de suscripción, ejecute hello siguiente cmdlet con el Id. de suscripción deseado.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definición de variables de imagen
facilidad de uso de toosimplify y la comprensión del script de Hola completado de este tutorial, se iniciará mediante la definición de una serie de variables. Cambiar los valores de parámetro de hello como considere oportuno, pero tenga cuidado de nomenclatura restricciones relacionadas tooname longitudes y caracteres especiales al modificar los valores de hello proporcionados.

### <a name="location-and-resource-group"></a>Ubicación y grupo de recursos
Use dos variables toodefine Hola datos hello y área de grupo de recursos en la que se crearán Hola otros recursos para la máquina virtual de Hola.

Puede modificarlo como quiera y, a continuación, ejecute hello después cmdlets tooinitialize estas variables.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Propiedades de almacenamiento
Usar hello siguientes variables toodefine Hola hello y cuenta de tipo de almacenamiento de toobe de almacenamiento utilizado por la máquina virtual de Hola.

Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables. Tenga en cuenta que en este ejemplo se usa [Almacenamiento premium](../../../storage/common/storage-premium-storage.md), que es el recomendado para cargas de trabajo de producción. Para más información sobre esta guía y para otras recomendaciones, consulte [Prácticas recomendadas para mejorar el rendimiento para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Propiedades de red
Usar hello siguiendo la interfaz de red de las variables toodefine Hola, método de asignación de hello TCP/IP, nombre de red virtual de hello, nombre de subred virtual de hello, Hola intervalo de direcciones IP para la red virtual de hello, Hola intervalo de direcciones IP para la subred de Hola y Hola toobe de etiqueta de nombre de dominio público utilizado por red hello en la máquina virtual de Hola.

Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Propiedades de máquina virtual
Usar hello después el nombre de máquina virtual de variables toodefine Hola, nombre de equipo de hello, tamaño de máquina virtual de Hola y nombre del disco de sistema operativo de hello para la máquina virtual de Hola.

Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Propiedades de la imagen
Usar hello siguientes variables toodefine Hola imagen toouse para la máquina virtual de Hola. En este ejemplo, se utiliza la imagen de SQL Server 2016 Enterprise Hola.

Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Tenga en cuenta que puede obtener una lista completa de las ofertas de la imagen de SQL Server con el comando Get-AzureRmVMImageOffer hello:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

Y puede ver Hola SKU disponibles para una oferta con el comando Get-AzureRmVMImageSku Hola. Hello siguiente comando muestra todas las SKU disponibles para hello **SQL2014SP1 WS2012R2** ofrecen.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
Con el modelo de implementación del Administrador de recursos de hello, Hola primer objeto que se crea es grupo de recursos de Hola. Usaremos hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate un grupo de recursos de Azure y sus recursos con recursos de Hola grupo nombre y ubicación definida por las variables de hello inicializado anteriormente.

Ejecute hello siguiente cmdlet toocreate su nuevo grupo de recursos.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
máquina virtual de Hello requiere recursos de almacenamiento para el disco del sistema operativo de Hola y hello datos de SQL Server y los archivos de registro. Por motivos de simplicidad, crearemos un único disco para ambos. Puede adjuntar discos adicionales posteriormente mediante hello [Azure Agregar disco](/powershell/module/azure/add-azuredisk) cmdlet en orden tooplace los datos de SQL Server y los archivos de registro en discos dedicados. Usaremos hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate un almacenamiento estándar de la cuenta en el nuevo grupo de recursos y con nombre de cuenta de almacenamiento de hello, el nombre de Sku de almacenamiento y la ubicación definido mediante variables de Hola que inicializado anteriormente.

Ejecute hello siguiente cmdlet toocreate la nueva cuenta de almacenamiento.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Crear recursos de red
máquina virtual de Hello requiere un número de recursos de red para la conectividad de red.

* Cada máquina virtual requiere una red virtual.
* Una red virtual debe tener al menos una subred definida.
* Una interfaz de red debe definirse con una dirección IP privada o pública.

### <a name="create-a-virtual-network-subnet-configuration"></a>Creación de una configuración de subred de una red virtual
Comenzaremos por crear una configuración de subred para la red virtual. En nuestro tutorial, se creará una subred de forma predeterminada con hello [AzureRmVirtualNetworkSubnetConfig New](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. Nuestra configuración de subred de red virtual se creará con el prefijo de nombre y la dirección de la subred de hello definido mediante las variables de hello inicializado anteriormente.

> [!NOTE]
> Puede definir propiedades adicionales de configuración de subred de red virtual de hello mediante este cmdlet, pero que está más allá del ámbito de Hola de este tutorial.
>
>

Ejecute hello siguiente cmdlet toocreate la configuración de subred virtual.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Crear una red virtual
A continuación, se creará la red virtual con hello [AzureRmVirtualNetwork New](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. Se creará la red virtual en el nuevo grupo de recursos con nombre hello, la ubicación y el prefijo de dirección definida mediante variables de Hola que inicializado anteriormente y usar la configuración de subred de Hola que definió en el paso anterior de Hola.

Ejecute hello siguiente cmdlet toocreate la red virtual.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Crear dirección IP pública de Hola
Ahora que tenemos nuestro red virtual definido, necesitamos tooconfigure una dirección IP para la máquina virtual de toohello de conectividad. Para este tutorial, creamos una dirección IP pública mediante toosupport conectividad a Internet de direccionamiento IP dinámica. Usaremos hello [AzureRmPublicIpAddress New](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Hola dirección IP pública en hello recursos grupo creado anteriormente y con nombre de hello, ubicación, método de asignación y etiqueta de nombre de dominio DNS definido mediante Hola variables que haya inicializado anteriormente.

> [!NOTE]
> Puede definir propiedades adicionales de la dirección IP pública Hola con este cmdlet, pero que está más allá del ámbito de Hola de este tutorial inicial. También puede crear una dirección privada o una dirección con una dirección estática, pero que también sea más allá del ámbito de Hola de este tutorial.
>
>

Ejecute hello siguiente cmdlet toocreate la dirección IP pública.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Crear la interfaz de red de Hola
Ahora estamos interfaz de red de hello toocreate preparado que va a usar de la máquina virtual. Usaremos hello [AzureRmNetworkInterface New](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nuestra interfaz de red en grupo de recursos de Hola que creó anteriormente y con nombre de hello, ubicación, subred y la dirección IP pública definido anteriormente.

Ejecute hello siguiente cmdlet toocreate la interfaz de red.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Configuración de un objeto de VM
Ahora que tenemos los recursos de almacenamiento y de red definidos, estamos listos toodefine los recursos de proceso para la máquina virtual de Hola. En nuestro tutorial, se especificará tamaño de máquina virtual de Hola y diversas propiedades de sistema operativo, especificar la interfaz de red de Hola que creamos previamente, definir el almacenamiento de blobs y, a continuación, especifique el disco del sistema operativo de Hola.

### <a name="create-hello-vm-object"></a>Crear objeto de máquina virtual de Hola
Empezaremos especificando el tamaño de la máquina virtual de Hola. Para este tutorial, vamos a especificar un DS13. Usaremos hello [AzureRmVMConfig New](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate un objeto de máquina virtual puede configurarse con nombre de Hola y el tamaño definido mediante las variables de hello inicializado anteriormente.

Ejecute hello después el objeto de máquina virtual de cmdlet toocreate Hola.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Crear un nombre de credencial objeto toohold hello y una contraseña para las credenciales de administrador local de Hola
Antes de que podemos establecer las propiedades de sistema operativo de la máquina virtual de Hola Hola, necesitamos sus credenciales de hello toosupply para la cuenta de administrador local de hello como una cadena segura. tooaccomplish, usaremos hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Ejecutar el siguiente cmdlet de hello y, en la ventana de solicitud de credenciales de Windows PowerShell de hello, escriba Hola toouse nombre y una contraseña para la cuenta de administrador local de hello en la máquina virtual de Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Establecer las propiedades de sistema operativo de hello para la máquina virtual de Hola
Ahora estamos propiedades del sistema operativo preparado tooset hello de la máquina virtual. Usaremos hello [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset Hola tipo de sistema operativo como Windows, requieren hello [agente de máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique ese Hola habilita automáticamente actualizar y establecer nombre de máquina virtual de hello, nombre de equipo de Hola y la credencial de hello mediante las variables de hello inicializado anteriormente.

Ejecute hello después de las propiedades de sistema operativo de cmdlet tooset hello para la máquina virtual.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Agregar una máquina virtual Hola red interfaz toohello
A continuación, se agregará la interfaz de red de Hola que creamos previamente toohello virtual machine. Usaremos hello [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interfaz de red de cmdlet tooadd hello mediante la variable de interfaz de red de Hola que definió anteriormente.

Ejecute hello siguiendo la interfaz de red de cmdlet tooset hello para la máquina virtual.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Establecer ubicación de almacenamiento de blobs de Hola de hello toobe de disco utilizado por la máquina virtual de Hola
A continuación, se establecerá la ubicación de almacenamiento de blobs de Hola de hello toobe de disco utilizado por máquina virtual de hello mediante variables de Hola que definió anteriormente.

Ejecute hello después de la ubicación de almacenamiento de blobs de cmdlet tooset Hola.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Establecer propiedades de disco de máquina virtual de Hola de sistema operativo de Hola
A continuación, se establecerá sistema de operativo Hola propiedades de disco de máquina virtual de Hola. Usaremos hello [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify de cmdlet que Hola de sistema operativo de la máquina virtual de hello procederán de una imagen, tooset tooread solo el almacenamiento en caché (porque se está instalando SQL Server en hello mismo disco) y definir nombre de la máquina virtual de Hola y disco del sistema operativo Hola definido mediante variables de Hola que hemos definido anteriormente.

Ejecute hello siguientes propiedades del disco de sistema operativo cmdlet tooset hello para la máquina virtual.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Especifique la imagen de la plataforma de hello para la máquina virtual de Hola
El último paso de configuración es la imagen de la plataforma toospecify hello para la máquina virtual. En nuestro tutorial, usamos la imagen de SQL Server 2016 CTP más reciente de Hola. Usaremos hello [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse esta imagen tal como se define mediante variables de Hola que definió anteriormente.

Ejecute hello siguiente cmdlet toospecify la imagen de la plataforma de hello para la máquina virtual.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Crear hello VM de SQL
Ahora que ha terminado de pasos de configuración de hello, está listo toocreate Hola virtual machine. Usaremos hello [AzureRmVM New](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Hola máquina virtual a través variables Hola que hemos definido.

Ejecute hello siguiente cmdlet toocreate la máquina virtual.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

se crea la máquina virtual de Hola. Observe que se crea una cuenta de almacenamiento estándar para el diagnóstico de arranque porque Hola la cuenta de almacenamiento para el disco de la máquina virtual Hola especificada es una cuenta de almacenamiento premium.

Ahora puede ver esta máquina en hello Azure Portal toosee [su dirección IP pública y su nombre de dominio completo](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Script de ejemplo
Hello siguiente secuencia de comandos contiene script de PowerShell de hello completo para este tutorial. Supone que ya tiene el programa de instalación Hola suscripción de Azure toouse con hello **agregar AzureRmAccount** y **seleccione AzureRmSubscription** comandos.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Pasos siguientes
Después de crear la máquina virtual de hello, está listo tooconnect toohello máquina con conectividad RDP y el programa de instalación. Para obtener más información, consulte [conectar tooa Máquina Virtual de SQL Server en Azure (Administrador de recursos)](virtual-machines-windows-sql-connect.md).

