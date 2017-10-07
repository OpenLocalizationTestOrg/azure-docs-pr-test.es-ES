---
title: Almacenamiento Premium de Azure con SQL Server aaaUse | Documentos de Microsoft
description: "En este artículo usa recursos creados con el modelo de implementación clásica de Hola y proporciona una orientación sobre el uso de almacenamiento Premium de Azure con SQL Server que se ejecutan en máquinas virtuales de Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Usar el almacenamiento Premium de Azure con SQL Server en máquinas virtuales
## <a name="overview"></a>Información general
[Almacenamiento Premium de Azure](../../../storage/common/storage-premium-storage.md) es Hola siguiente generación de almacenamiento que proporciona baja latencia y alto rendimiento de E/S. Funciona mejor para cargas de trabajo intensivas clave de E/S, como [máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/)de SQL Server en IaaS.

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Este artículo proporciona orientación para migrar una máquina Virtual con SQL Server toouse almacenamiento Premium y planeación. Esto incluye pasos relacionados con la infraestructura de Azure (redes, almacenamiento) y la máquina virtual invitada de Windows. ejemplo de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) local se muestra una migración de tooend final integrales de cómo mejora toomove mayor ventaja de tootake de las máquinas virtuales de almacenamiento SSD con PowerShell.

Es importante toounderstand Hola-to-end proceso usando almacenamiento Premium de Azure con SQL Server en máquinas virtuales de IAAS. En ella se incluye:

* Identificación de los requisitos previos de hello toouse almacenamiento Premium.
* Ejemplos de implementación de SQL Server en IaaS tooPremium almacenamiento para nuevas implementaciones.
* Ejemplos de migración de implementaciones existentes, tanto servidores independientes como implementaciones mediante grupos de disponibilidad AlwaysOn de SQL.
* Enfoques de migración posibles.
* Muestra los pasos de Azure, Windows y SQL Server para la migración de Hola de una implementación existente siempre en el ejemplo de end-to-end.

Para obtener información general sobre SQL Server en máquinas virtuales de Azure, consulte [SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Autor:** Daniel Sol **Revisores técnicos:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Requisitos previos para el almacenamiento Premium
Hay varios requisitos previos para usar el almacenamiento Premium.

### <a name="machine-size"></a>Tamaño de la máquina
Para usar almacenamiento Premium debe toouse DS serie máquinas virtuales (VM). Si no ha utilizado las máquinas de la serie DS en el servicio de nube antes, debe eliminar Hola existente VM, mantener Hola adjuntada discos y, a continuación, crear un nuevo servicio de nube antes de volver a Hola VM como DS * tamaño de rol. Para más información sobre los tamaños de las máquinas virtuales, consulte [Tamaños de máquinas virtuales y servicios en la nube de Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Servicios en la nube
Solo puede usar máquinas virtuales DS* con almacenamiento Premium cuando se crean en un servicio en la nube nuevo. Si usas SQL Server Always On en Azure, Hola siempre escucha hará referencia dirección toohello Azure interno o externo IP del equilibrador de carga que está asociada a un servicio de nube. En este artículo se centra en cómo toomigrate manteniendo la disponibilidad en este escenario.

> [!NOTE]
> Una serie DS * debe ser Hola primera máquina virtual que está implementado toohello nuevo servicio de nube.
>
>

### <a name="regional-vnets"></a>Redes virtuales regionales
Para las máquinas virtuales de DS * debe configurar Hola red Virtual (VNET) hospeda el toobe de las máquinas virtuales regional. Este Hola "amplía" red virtual es toobe tooallow Hola de máquinas virtuales más grande aprovisionado en otros clústeres y permitir la comunicación entre ellos. En la siguiente captura de pantalla de hello, hello ubicación resaltada muestra redes virtuales regionales, mientras que el primer resultado de hello muestra una red virtual "estrecha".

![RegionalVNET][1]

Puede generar un tooa de toomigrate del vale de soporte técnico de Microsoft red virtual regional, Microsoft realizará un cambio, a continuación, toocomplete Hola migración tooregional de redes virtuales, cambie la propiedad hello AffinityGroup configuración de red de Hola. Primero debe exportar Hola configuración de red en PowerShell y, a continuación, reemplace hello **AffinityGroup** propiedad Hola **VirtualNetworkSite** elemento con un **ubicación** propiedad. Especifique `Location = XXXX` donde `XXXX` es una región de Azure. A continuación, importar configuración nueva de Hola.

Por ejemplo, tenga en cuenta Hola siguiente configuración de red virtual:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove este tooa red virtual regional en Europa occidental, cambiar hello toohello de configuración siguientes:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Cuentas de almacenamiento
Deberá toocreate una nueva cuenta de almacenamiento que está configurada para el almacenamiento Premium. Tenga en cuenta que use Hola de almacenamiento Premium está establecida en la cuenta de almacenamiento de hello, no en discos duros virtuales individuales, sin embargo, cuando se usa una VM de serie DS * puede adjuntar VHD desde cuentas de almacenamiento estándar y Premium. Puede considerar esta opción si no desea tooplace Hola VHD de SO en toohello cuenta de almacenamiento Premium.

siguiente Hello **New-AzureStorageAccountPowerShell** comando con hello "Premium_LRS" **tipo** crea una cuenta de almacenamiento Premium:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Configuración de la caché de los VHD
Hola principal diferencia entre la creación de discos que forman parte de una cuenta de almacenamiento Premium es configuración de caché de disco de Hola. En el caso de discos de volumen de datos de SQL Server, se recomienda usar "**Read Caching**". Para volúmenes de registro de transacciones, configuración de caché de disco de hello debe establecerse demasiado '**ninguno**'. Esto es diferente de las recomendaciones de hello las cuentas de almacenamiento estándar.

Una vez que se han adjuntado Hola discos duros virtuales, no se puede modificar la configuración de caché de Hola. ¿Necesita toodetach y volver a adjuntar Hola VHD con una configuración de memoria caché actualizada.

### <a name="windows-storage-spaces"></a>Espacios de almacenamiento de Windows
Puede usar [espacios de almacenamiento de Windows](https://technet.microsoft.com/library/hh831739.aspx) como lo hizo con almacenamiento estándar anterior, esto le permitirá toomigrate una máquina virtual que ya se utiliza espacios de almacenamiento. ejemplo de Hola en [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (paso 9 y siguientes) se muestra hello tooextract de código de Powershell e importar una máquina virtual con varios discos duros virtuales conectados.

Grupos de almacenamiento se usan con un rendimiento tooenhance de cuenta de almacenamiento de Azure estándar y reducen la latencia. Pueden resultarle útiles las pruebas de los grupos de almacenamiento con el almacenamiento Premium para implementaciones nuevas, pero agregan una complejidad adicional con la configuración del almacenamiento.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>¿Cómo toofind qué discos virtuales de Azure se asignan grupos de toostorage
Tal y como se ofrecen recomendaciones de configuración de caché diferente para VHD adjunto, podría decidir toocopy Hola discos duros virtuales tooa cuenta de almacenamiento Premium. Sin embargo, cuando se vuelva a adjuntarlos toohello la serie DS nueva máquina virtual, tendrá que configuración de la caché de tooalter Hola. Resulta más sencillo Hola tooapply que almacenamiento Premium recomienda configuración de la caché cuando tienes VHD independiente para Hola de datos de SQL archivos y registro archivos (en lugar de un solo disco duro virtual que contiene).

> [!NOTE]
> Si tiene archivos de datos y de registro de SQL Server en el mismo volumen, Hola almacenamiento en caché de la opción que elija depende de los patrones de acceso de E/S de Hola para las cargas de trabajo de la base de datos de Hola. Solo las pruebas pueden demostrar qué opción de caché es más adecuada para este escenario.
>
>

Sin embargo, si usa espacios de almacenamiento de Windows que se compone de varios discos duros virtuales deberá toolook en su tooidentify scripts original que ha adjuntado discos duros virtuales están en qué grupo específico, por lo que se pueden establecer opciones de caché de hello en consecuencia para cada disco.

Si no tiene original tooshow disponibles de script qué discos duros virtuales se asignan toohello bloque de almacenamiento, puede usar Hola después de asignación de grupo de pasos toodetermine Hola/almacenamiento en disco.

Para cada disco, use Hola pasos:

1. Obtención de una lista de discos conectados tooVM con hello **Get-AzureVM** comando:

    Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. Tenga en cuenta Hola Diskname y LUN.

    ![DisknameAndLUN][2]
3. Escritorio remoto en hello máquina virtual. A continuación, vaya demasiado**administración de equipos** | **el Administrador de dispositivos** | **unidades de disco**. Examine las propiedades de Hola de cada uno de hello 'Microsoft 'discos virtuales

    ![VirtualDiskProperties][3]
4. aquí el número de LUN Hello es un número LUN de toohello de referencia que especifique al adjuntar Hola VHD toohello máquina virtual.
5. Para hello 'Disco Virtual de Microsoft' vaya toohello **detalles** ficha, a continuación, en hello **propiedad** lista, vaya demasiado**clave Driver**. Hola **valor**, Hola Nota **desplazamiento**, que es 0002 Hola siguiente captura de pantalla. Hola 0002 denota hello PhysicalDisk2 que Hola referencias del grupo de almacenamiento.

    ![VirtualDiskPropertyDetails][4]
6. Para cada grupo de almacenamiento, volcado out Hola asociados discos:

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Ahora puede usar este tooassociate de información de discos duros virtuales tooPhysical discos en grupos de almacenamiento conectados.

Una vez que ha asignado los discos duros virtuales tooPhysical discos en grupos de almacenamiento, a continuación, puede separar y cópielos en tooa cuenta de almacenamiento Premium, a continuación, deberá asociarlas con configuración de caché correcto Hola. Vea ejemplo de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), los pasos del 8 al 12. Estos pasos muestran cómo tooextract un archivo VHD conectado a la máquina virtual disco configuración tooa CSV, copiar discos duros virtuales de hello, modificar opciones de caché de configuración de disco de Hola y por último, volver a implementar Hola VM como una serie DS VM con hello todos los discos conectados.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Ancho de banda del almacenamiento de la VM y rendimiento del almacenamiento del VHD
cantidad de Hola de rendimiento de almacenamiento depende de hello tamaño de VM de DS * especificado y Hola tamaños de disco duro virtual. máquinas virtuales de Hello tienen diferentes compensaciones por número de Hola de discos duros virtuales que se pueden adjuntar y Hola ancho de banda máximo, admitirán (MB/s). Los números de ancho de banda determinado hello, consulte [Máquina Virtual y tamaños de servicio de nube de Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

El aumento de IOPS se consigue con tamaños de disco mayores. Debe tenerlo en cuenta al considerar la ruta de acceso de la migración. Para obtener más información, [ver tabla de Hola para los tipos de disco y e/s por segundo](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Por último, tenga en cuenta que las máquinas virtuales admiten diferentes anchos de banda de disco máximos para todos los discos conectados. Bajo una carga alta, podría saturar el ancho de banda máximo en disco de hello disponible para ese tamaño de rol de máquina virtual. Por ejemplo un Standard_DS14 admitirán la too512MB/s; por lo tanto, con tres discos P30 podría saturar el ancho de banda de disco de Hola de hello máquina virtual. Pero en este ejemplo, se puede superar el límite de rendimiento de hello según la combinación de Hola de lectura y escritura IOs.

## <a name="new-deployments"></a>Nuevas implementaciones
Hola dos secciones siguientes muestran cómo se puede implementar tooPremium almacenamiento de VM de SQL Server. Como se mencionó antes, no es necesario necesariamente tooplace el disco del sistema operativo de hello en almacenamiento Premium. Puede elegir toodo de esto si tiene previsto tooplace las cargas de trabajo intensivas de E/S en hello VHD de sistema operativo.

Hola primer ejemplo demuestra el uso de imágenes de la Galería de Azure existente. Hello segundo ejemplo muestra cómo toouse una máquina virtual personalizada de la imagen que tiene en una cuenta de almacenamiento estándar existente.

> [!NOTE]
> En estos ejemplos se supone que ya ha creado una red virtual regional.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Crear una nueva máquina virtual con almacenamiento Premium con una imagen de la Galería
ejemplo de Hola siguiente muestra cómo tooplace Hola VHD de SO en almacenamiento premium y adjuntar VHD de almacenamiento Premium. Sin embargo, puede ubicar el disco del sistema operativo hello en una cuenta de almacenamiento estándar y, a continuación, adjuntar discos duros virtuales que residen en una cuenta de almacenamiento Premium. Se muestran ambos escenarios.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Paso 1: Crear una cuenta de almacenamiento Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Paso 2: Crear un nuevo servicio en la nube
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Paso 3: Reservar una VIP de servicio en la nube (opcional)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Paso 4: Crear un contenedor de máquinas virtuales
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Paso 5: Colocar el VHD del sistema operativo en el almacenamiento estándar o Premium
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Paso 6: Crear una máquina virtual
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Crear un nuevo toouse VM almacenamiento Premium con una imagen personalizada
Este escenario muestra dónde tiene imágenes personalizadas que residen en una cuenta de almacenamiento estándar. Como se mencionó si desea tooplace Hola VHD de sistema operativo en almacenamiento Premium debe toocopy Hola imagen que existe en la cuenta de almacenamiento estándar hello y transferirlas tooa almacenamiento Premium antes de poder utilizarlo. Si tiene una imagen local, puede usar este método toocopy directamente toohello cuenta de almacenamiento Premium.

#### <a name="step-1-create-storage-account"></a>Paso 1: Crear una cuenta de almacenamiento
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Paso 2: Crear un servicio en la nube
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Paso 3: Usar una imagen existente
Puede usar una imagen existente. También puede [captar la imagen de una máquina existente](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Máquina de hello tenga en cuenta que la imagen no tiene toobe DS * máquina. Una vez que tenga la imagen de hello, Hola siguientes pasos muestran cómo toocopy se toohello cuenta de almacenamiento Premium con hello **AzureStorageBlobCopy inicio** commandlet de PowerShell.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Paso 4: Copiar un blob entre cuentas de almacenamiento
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Paso 5: Comprobar periódicamente el estado de copia
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Paso 6: Agregar disco de imagen en tooAzure repositorio de suscripción
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Es posible que, aunque los informes de estado de hello como correcto, todavía podrían obtener un error de concesión de disco. En este caso, espere unos 10 minutos.
>
>

#### <a name="step-7--build-hello-vm"></a>Paso 7: Crear Hola VM
Aquí está generando Hola VM de la imagen y asociar dos VHD de almacenamiento Premium:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Implementaciones existentes que no usan grupos de disponibilidad AlwaysOn
> [!NOTE]
> Para las implementaciones existentes, primero consulte hello [requisitos previos](#prerequisites-for-premium-storage) sección de este tema.
>
>

Existen diferentes consideraciones para las implementaciones de SQL Server que no usan grupos de disponibilidad AlwaysOn y para las que los usan. Si no se usa siempre en y tiene un servidor SQL Server independiente existente, puede actualizar tooPremium almacenamiento mediante una nueva cuenta de servicio y el almacenamiento en nube. Considere la posibilidad de hello siguientes opciones:

* **Crear una nueva máquina virtual de SQL Server**. Puede crear una nueva máquina virtual de SQL Server que use una cuenta de almacenamiento Premium, como se documenta en Nuevas implementaciones. A continuación, haga una copia de seguridad y restaure las bases de datos de usuario y la configuración de SQL Server. Hello aplicación necesitará toobe actualiza tooreference Hola nuevo SQL Server si se tiene acceso interna o externamente. Necesitaría toocopy todos los objetos "fuera de la base de datos' como si está realizando una migración de en paralelo (SxS) de SQL Server. Esto incluye objetos tales como inicios de sesión, certificados y servidores vinculados.
* **Migrar una máquina virtual de SQL Server existente**. Esto requerirá desconectar Hola VM de SQL Server, a continuación, transferir tooa nuevo servicio en la nube, que incluye la copia de todos su toohello de discos duros virtuales conectado cuenta de almacenamiento Premium. Cuando Hola VM se pone en línea, aplicación hello hará referencia a nombre de host del servidor hello como antes. Tenga en cuenta que tamaño Hola de disco existente de hello afectarán a las características de rendimiento de Hola. Por ejemplo, un disco de 400 GB obtiene redondea tooa P20. Si sabe que no requieren ese rendimiento del disco, a continuación, puede volver a crear Hola máquina virtual como una VM de la serie DS y adjuntar VHD de almacenamiento Premium de especificación de tamaño/rendimiento Hola que necesita. A continuación, podría separar y adjuntar los archivos de base de datos SQL de Hola.

> [!NOTE]
> Al copiar los discos VHD de hello debe ser consciente del tamaño de hello, según el tamaño de hello en cuenta qué tipo de disco de almacenamiento Premium se dividen en, esto determina la especificación de rendimiento de disco. Tamaño de Azure será de ida y vuelta de toohello más cercano de disco, por lo que si tiene un disco de GB 400, esto se redondeará hasta tooa P20. Dependiendo de los requisitos de E/S existentes de hello VHD de sistema operativo, no tendrá que toomigrate esta tooa cuenta de almacenamiento Premium.
>
>

Si se tiene acceso a SQL Server externamente, VIP de servicio de nube de hello cambiará. También tendrá dos puntos finales tooupdate, ACL y DNS configuración.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Implementaciones existentes que usan grupos de disponibilidad AlwaysOn
> [!NOTE]
> Para las implementaciones existentes, primero consulte hello [requisitos previos](#prerequisites-for-premium-storage) sección de este tema.
>
>

En esta sección, examinaremos, en primer lugar, la forma en que AlwaysOn interactúa con las redes de Azure. A continuación, se interrumpirá hacia abajo las migraciones en escenarios de tootwo: las migraciones que puede tolerar cierto tiempo de inactividad y migraciones donde debe lograr tiempo de inactividad mínimo.

Los grupos de disponibilidad AlwaysOn de SQL Server locales usan un agente de escucha local que registra un nombre DNS virtual junto con una dirección IP que comparten uno o varios servidores SQL Server. Cuando los clientes se conectan que se enrutan a través de hello del agente de escucha IP toohello principal de SQL Server. Éste es el servidor de Hola que posee el recurso siempre IP hello en ese momento.

![DeploymentsUseAlways On][6]

En Microsoft Azure puede tener solo una IP dirección asignada tooa NIC en hello VM, en orden tooachieve Hola misma capa de abstracción como locales, Azure emplea la dirección IP de hello asignado equilibradores de carga de toohello internas y externas (ILB/ELB). recurso de IP de Hola que se comparte entre los servidores de Hola se establece toohello mismo IP como hello ILB/ELB. Esta información se publica en hello DNS y tráfico del cliente se pasa a través de réplica de SQL Server principal de hello ILB/ELB toohello. Hola ILB/ELB sabe que SQL Server es principal, ya que utiliza recursos de sondeos tooprobe Hola siempre IP. En el ejemplo anterior de hello, sondea cada nodo que tiene un extremo al que hace referencia Hola ELB/ILB, lo que responde es Hola principal de SQL Server.

> [!NOTE]
> Hello ILB y ELB tienen asignado tooa servicio de nube de Azure específica, por lo tanto, cualquier migración a la nube en Azure, significará que más probable es que ese Hola que cambiará IP del equilibrador de carga.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migración de implementaciones de AlwaysOn que permiten cierto tiempo de inactividad
Hay dos estrategias toomigrate siempre en las implementaciones que permiten cierto tiempo de inactividad:

1. **Agregar más tooan réplicas secundarias existentes siempre en clúster**
2. **Migrar tooa nuevo siempre en clúster**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Agregar más tooan réplicas secundarias existentes siempre en clúster
Una estrategia es tooadd más secundarias toohello siempre en el grupo de disponibilidad. Estos elementos en un nuevo servicio de nube es necesario tooadd y actualizar el agente de escucha de hello con hello IP de equilibrador de carga nueva.

##### <a name="points-of-downtime"></a>Puntos de tiempo de inactividad:
* Validación de clústeres.
* Pruebas de las conmutaciones por error de AlwaysOn en los elementos secundarios nuevos.

Si usas grupos de almacenamiento de Windows dentro de hello VM para un mayor rendimiento de E/S, a continuación, estos se desconectará durante una validación de clúster completa. prueba de validación de Hello es necesaria cuando agregue nodos toohello clúster. tiempo de Hola que tarda la prueba de hello toorun puede variar, por lo que debe probar esto en su tooget del entorno de prueba representativo un tiempo aproximado de cuánto se tardará.

Debe aprovisionar que puede realizar la conmutación por error manual y chaos pruebas en hello recién agregado funciones de alta disponibilidad de AlwaysOn de nodos tooensure según lo previsto.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Se deben detener todas las instancias de SQL Server que se usan los grupos de almacenamiento de hello antes de hello la validación se ejecuta.
>
> ##### <a name="high-level-steps"></a>Pasos de alto nivel
>

1. Cree dos nuevos servidores SQL Server en el nuevo servicio en la nube con el almacenamiento Premium conectado.
2. Copie las de copias de seguridad completas y restáurelas con **NORECOVERY**.
3. Copie los objetos dependientes “fuera de la base de datos de usuario”, como los inicios de sesión, etc.
4. Cree un equilibrador de carga interno nuevo (ILB) o use un equilibrador de carga externo (ELB) y, a continuación, configure los extremos de carga equilibrada en ambos nodos nuevos.

   > [!NOTE]
   > Compruebe que todos los nodos tienen la configuración de punto de conexión correcto Hola antes de continuar
   >
   >
5. Detener toohello de acceso de usuario/aplicaciones SQL Server (si utiliza grupos de almacenamiento).
6. Detenga los servicios del motor de SQL Server en todos los nodos (si usa grupos de almacenamiento).
7. Agregar nueva toocluster de nodos y ejecute la validación completa.
8. Una vez que la validación sea correcta, inicie todos los servicios de SQL Server.
9. Haga una copia de seguridad de los registros de transacciones y restaure las bases de datos de usuario.
10. Agregue nuevos nodos en hello siempre en el grupo de disponibilidad y coloque la replicación en **sincrónica**.
11. Agregar IP de hello el recurso de dirección de hello servicio de nube nuevo ILB/ELB a través de PowerShell para AlwaysOn tomando como ejemplo de varios sitios de Hola Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). En los clústeres de Windows, establecer hello **posibles propietarios** de hello **dirección IP** recursos toohello nuevos nodos anteriores. Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Tooone de conmutación por error de nuevos nodos de Hola.
13. Realizar Hola nuevos nodos asociados de conmutación por error automática y probar las conmutaciones por error.
14. Quite los nodos originales del grupo de disponibilidad.

##### <a name="advantages"></a>Ventajas
* Puede ser nuevos servidores de SQL comprobado (SQL Server y aplicación) antes de que se agregan tooAlways en.
* Puede cambiar el tamaño de la máquina virtual de Hola y personalizar requisitos exactos de hello almacenamiento tooyour. Sin embargo, sería beneficioso tookeep todas las rutas de acceso de archivo SQL Hola Hola igual.
* Puede controlar cuando se inicia la transferencia Hola de toohello de las copias de seguridad de base de datos de hello las réplicas secundarias. Esto difiere del uso de Azure **AzureStorageBlobCopy inicio** commandlet toocopy discos duros virtuales, ya que es una copia asincrónica.

##### <a name="disadvantages"></a>Desventajas
* Al utilizar grupos de almacenamiento de Windows, hay un tiempo de inactividad de clúster durante Hola validación de clúster completa para los nodos adicionales de hello nueva.
* Según Hola versión de SQL Server y número existente de Hola de réplicas secundarias, podría no ser capaz de tooadd varias réplicas secundarias sin quitar réplicas secundarias existentes.
* Podría haber mucho tiempo de transferencia de datos SQL al configurar los elementos secundarios de Hola.
* Hay costos adicionales durante la migración cuando se tienen máquinas nuevas que se ejecutan en paralelo.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Migrar tooa nuevo siempre en clúster
Otra estrategia es toocreate un nuevo siempre en clúster con completamente nuevos nodos en el nuevo servicio de nube y, a continuación, toouse de los clientes de Hola de redirección.

##### <a name="points-of-downtime"></a>Puntos de tiempo de inactividad
No hay tiempo de inactividad cuando la transferencia de aplicaciones y usuarios toohello nuevo siempre en agente de escucha. tiempo de inactividad de Hello depende de:

* Hola tiempo toodatabases de copias de seguridad de registro de transacciones final toorestore en los nuevos servidores.
* Hola tiempo tooupdate aplicaciones toouse nueva siempre en escucha de cliente.

##### <a name="advantages"></a>Ventajas
* Puede probar el entorno de producción real de hello, SQL Server, y cambios de compilación del sistema operativo.
* Tiene dispositivos de almacenamiento de hello opción toocustomize hello y toopotentially reducir el tamaño de máquina virtual. Esto podría reducir los costos.
* Puede actualizar su compilación o versión de SQL Server durante este proceso. También puede actualizar Hola sistema operativo.
* Hola que anterior siempre clúster puede actuar como un destino de reversión sólido.

##### <a name="disadvantages"></a>Desventajas
* Nombre DNS de hello toochange del agente de escucha de hello necesita si desea que ambos clústeres siempre en ejecución de forma simultánea. Esto agrega administración sobrecarga durante la migración de hello como las cadenas de la aplicación de cliente deben reflejar el nuevo nombre de agente de escucha Hola.
* Debe implementar un mecanismo de sincronización entre Hola dos entornos tookeep como cerrar como requisitos de sincronización final de hello toominimize posibles antes de la migración.
* Se agrega costes durante la migración mientras se tiene que ejecutar de nuevo entorno de Hola.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migración de las implementaciones de AlwaysOn para reducir el tiempo de inactividad al mínimo
Hay dos estrategias para migrar las implementaciones de AlwaysOn de tal modo que el tiempo de inactividad sea mínimo:

1. **Usar un elemento secundario existente: sitio único**
2. **Usar una réplica de un elemento secundario existente: multisitio**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Usar un elemento secundario existente: sitio único
Una estrategia de tiempo de inactividad mínimo es tootake una existente en la nube secundaria y quítelo del servicio de nube de hello actual. A continuación, copie hello toohello de discos duros virtuales nueva cuenta de almacenamiento Premium y cree Hola VM Hola nuevo servicio en nube. A continuación, actualice el agente de escucha de hello en clústeres y la conmutación por error.

##### <a name="points-of-downtime"></a>Puntos de tiempo de inactividad
* No hay tiempo de inactividad cuando se actualiza el nodo final de hello con el extremo de equilibrio de carga de Hola.
* La reconexión del cliente podría retrasarse en función de la configuración de cliente/DNS.
* No hay tiempo de inactividad adicional si elige tootake Hola siempre clúster grupo sin conexión tooswap las direcciones IP de Hola. Puede evitar esto mediante el uso de una dependencia OR y propietarios posibles para hello agregó el recurso de dirección IP. Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Cuando quiera Hola toopartake nodo agregado en como siempre en Failover Partner, deberá tooadd un extremo de Azure con un toohello de referencia de carga equilibrada establece. Cuando ejecute hello **Add-AzureEndpoint** comando toodo, tooremain actual de conexiones abierta, pero el nuevo agente de escucha de conexiones toohello no será capaz de toobe establecida hasta que haya actualizado el equilibrador de carga de Hola. En las pruebas Esto se toolast encontrada 90-120 segundos, se debe probar.
>
>

##### <a name="advantages"></a>Ventajas
* No se incurre en más gastos durante la migración.
* Migración uno a uno.
* Menor complejidad.
* Admite una mayor IOPS en los SKU de almacenamiento Premium. Cuando Hola discos desasociados de hello VM y copian toohello nuevo servicio en la nube, un 3rd party herramienta puede ser tamaño de disco duro virtual de hello tooincrease usado, que proporciona un mayor rendimiento. Para aumentar el tamaño del VHD, consulte este [debate de foro](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Desventajas
* Hay una pérdida temporal de alta disponibilidad y recuperación ante desastres durante la migración.
* Tal y como se trata de una migración de 1:1, tendrá que toouse es un tamaño mínimo de máquina virtual que vaya a admitir el número de discos duros virtuales, por lo que quizás no pueda toodownsize las máquinas virtuales.
* Este escenario utilizaría hello Azure **AzureStorageBlobCopy inicio** commandlet, que es asincrónico. No hay ningún contrato de nivel de servicio cuando finaliza la copia. tiempo de Hola de hello copias varía, aunque esto depende de espera en cola que también dependerá de cantidad de Hola de tootransfer de datos. el tiempo de copia de Hello aumenta si transferencia Hola va tooanother centro de datos de Azure que admite el almacenamiento de Premium en otra región. Si solo tiene 2 nodos, tenga en cuenta una mitigación posibles en caso de que copia Hola tarda más en las pruebas. Esto podría incluir Hola después ideas.
  * Agregar un nodo 3rd temporal de SQL Server para alta disponibilidad antes de la migración de hello acordada tiempo de inactividad.
  * Ejecutar migración Hola fuera de Azure mantenimiento programado.
  * Asegúrese de que ha configurado correctamente el cuórum de clúster.  

##### <a name="high-level-steps"></a>Pasos de alto nivel
Este documento no muestra un ejemplo de tooend final completa, sin embargo Hola [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) proporciona detalles que pueden ser aprovechado tooperform esto.

![MinimalDowntime][8]

* Configuración de disco de recopilación y quitar un nodo hello (no elimine VHD conectados).
* Cree una cuenta de almacenamiento Premium y copiar discos duros virtuales de hello cuenta de almacenamiento estándar
* Crear nuevo servicio de nube y volver a implementar Hola SQL2 VM en ese servicio en la nube. Crear hello VM con hello copian los VHD de sistema operativo original y adjuntar Hola copia discos duros virtuales.
* Configure ILB/ELB y agregue extremos.
* Actualice el agente de escucha de una de las siguientes maneras:
  * Tomar Hola siempre está en el grupo sin conexión y actualización Hola siempre en agente de escucha con ILB nuevo / dirección IP de ELB.
  * O bien, agregar el recurso de dirección IP de Hola de nuevo en la nube servicio ILB/ELB a través de PowerShell en clústeres de Windows. A continuación, conjunto Hola posibles propietarios de toohello de recurso de dirección IP de hello migran nodo, SQL2 y establecerla como la dependencia OR Hola nombre de red. Consulte la sección 'Agregar recurso de dirección IP en la misma subred' de Hola de hello [apéndice](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Compruebe a los clientes de toohello de configuración/propagación DNS.
* Migre la máquina virtual SQL1 y siga los pasos del 2 al 4.
* Si usa los pasos 5ii, a continuación, agregue SQL1 como un posible propietario de hello agrega el recurso de dirección IP
* Pruebe las conmutaciones por error.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Usar una réplica de un elemento secundario existente: multisitio
Si tienes nodos en más de un centro de datos Azure (DC) o si tiene un entorno híbrido, puede usar una configuración de AlwaysOn en este tiempo de inactividad de toominimize de entorno.

enfoque de Hello es toochange Hola siempre en sincronización tooSynchronous para hello local o controlador de dominio secundario de Azure y, a continuación, conmutación por error sobre toothat SQL Server. A continuación, copie Hola discos duros virtuales tooa cuenta de almacenamiento Premium y volver a implementar la máquina de hello en un nuevo servicio de nube. Actualizar el agente de escucha de hello y, a continuación, realizar conmutación por recuperación.

##### <a name="points-of-downtime"></a>Puntos de tiempo de inactividad
tiempo de inactividad de Hello está formada por toofailover toohello alternativa DC de hello tiempo y viceversa. También depende de la configuración de cliente/DNS, y la reconexión del cliente podría retrasarse.
Considere la posibilidad de hello siguiente ejemplo de una configuración híbrida Always On:

![MultiSite1][9]

##### <a name="advantages"></a>Ventajas
* Puede usar la infraestructura existente.
* Tener Hola Hola de actualización de toopre opción almacenamiento de Azure en hello Azure DR DC en primer lugar.
* puede volver a configurar Hola almacenamiento de Azure DR DC.
* Se produce un mínimo de dos conmutaciones por error durante la migración, excluidas las conmutaciones por error de prueba.
* No necesita datos de SQL Server toomove con copia de seguridad y restauración.

##### <a name="disadvantages"></a>Desventajas
* Según tooSQL de acceso de cliente servidor, puede haber una mayor latencia cuando SQL Server se ejecuta en una aplicación de toohello de controlador de dominio alternativa.
* tiempo de copia de Hola de almacenamiento de discos duros virtuales tooPremium podría ser largo. Esto podría afectar a la decisión sobre si tookeep Hola nodo Hola grupo de disponibilidad. Tenga en cuenta esto cuando la carga se ejecuta durante la migración de Hola de trabajo intensivas de registro es necesario, ya que el nodo principal Hola tendrá tookeep Hola transacciones sin replicar en su registro de transacciones. En consecuencia, este podría aumentar de forma significativa.
* Este escenario utilizaría hello Azure **AzureStorageBlobCopy inicio** commandlet, que es asincrónico. No hay ningún contrato de nivel de servicio al finalizar. Hello tiempo de hello copias varía, aunque esto depende de espera en cola, también dependerá de cantidad de Hola de tootransfer de datos. Por lo tanto, sólo tiene un nodo en el centro de datos 2, debe seguir los pasos de mitigación en caso de que copia Hola tarda más en las pruebas. Esto podría incluir Hola después ideas.
  * Agregar un nodo SQL 2nd temporal para alta disponibilidad antes de la migración de hello acordada tiempo de inactividad.
  * Ejecutar migración Hola fuera de Azure mantenimiento programado.
  * Asegúrese de que ha configurado correctamente el cuórum de clúster.

Este escenario se supone que ha documentado la instalación y saber cómo se asigna almacenamiento hello en toomake ordenar los cambios de configuración de la caché de disco óptimo.

##### <a name="high-level-steps"></a>Pasos de alto nivel
![Multisite2][10]

* Asegúrese de Hola local / alternar Hola de controlador de dominio de Azure SQL Server principal y configurarlo como Hola otro asociado de conmutación por error automática (AFP).
* Recopilar la información de configuración de disco SQL2 y quitar un nodo hello (no eliminar adjuntos discos duros virtuales).
* Cree una cuenta de almacenamiento Premium y copiar discos duros virtuales de hello cuenta de almacenamiento estándar.
* Crear un nuevo servicio de nube y cree Hola SQL2 VM con los discos de almacenamiento de bonificaciones adjuntados.
* Configure ILB/ELB y agregue extremos.
* Hola de actualización siempre en agente de escucha con ILB nuevo / ELB IP dirección y prueba failover.
* Compruebe la configuración de DNS de Hola.
* Cambiar hello tooSQL2 AFP y, a continuación, migrar SQL1 y vaya a través de los pasos del 2 al 5.
* Pruebe las conmutaciones por error.
* Cambiar tooSQL1 atrás Hola AFP y SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Apéndice: Migrar a un almacenamiento de la funcionalidad de multisitio siempre en clúster tooPremium
resto de Hola de este tema proporciona un ejemplo detallado de conversión de un almacenamiento tooPremium multisitio siempre en clúster. También convierte Hola agente de escucha del uso de un equilibrador de carga interno de tooan (ELB) de equilibrador de carga externo (ILB).

### <a name="environment"></a>Environment
* Windows 2k12 / SQL 2k12
* 1 archivo de base de datos en SP
* 2 grupos de almacenamiento por nodo

![Appendix1][11]

### <a name="vm"></a>Máquina virtual
En este ejemplo vamos toodemonstrate mover desde un tooILB ELB. ELB no estaba disponible antes de ILB, por lo que aquí indica cómo Hola a tooswitch toothis durante la migración.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>Los pasos anteriores: Conectar tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Paso 1: Crear una cuenta de almacenamiento y un servicio en la nube nuevos
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Paso 2: Hola de aumento permitida errores en los recursos<Optional>
En determinados recursos que pertenecen tooyour grupo de disponibilidad AlwaysOn hay límites en cuántos errores que pueden producirse en un tiempo, donde el servicio de clúster de Hola tratará de grupo de recursos de hello toorestart. Se recomienda que aumentar este mientras se recorrer a través de este procedimiento, ya que si no lo hace manualmente conmutaciones por error de conmutación por error y se desencadena al apagar máquinas pueden obtener el límite de toothis cerrar.

Podría ser tolerancia de error de hello toodouble prudente, toodo esto en el Administrador de clústeres de conmutación por error, consulte toohello propiedades Hola Always On del grupo de recursos:

![Appendix3][13]

Cambiar hello too6 máximo de errores.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Paso 3: Agregar el recurso de dirección IP para el grupo de clústeres <Optional>
Si tiene sólo una dirección IP para hello grupo de clúster y se trata de subred de toohello alineado en la nube, tenga cuidado, si accidentalmente realizar sin conexión todos los nodos de clúster en la nube de hello en que red, a continuación, el recurso de clúster IP de Hola y nombre de red de clúster no será capaz de toocome en línea. Hola eventos de esto impedirá que actualiza tooother los recursos de clúster.

#### <a name="step-4-dns-configuration"></a>Paso 4: Configuración de DNS
tooimplement una transición sin problemas depende de cómo se va DNS utilizan y actualizan.
Cuando se instala siempre en, crea un grupo de recursos de clúster de Windows, si abre el Administrador de clústeres de conmutación por error, verá que como mínimo tendrá tres recursos, Hola dos que Hola documento hace referencia tooare:

* Nombre de red virtual (VNN): se trata de hello DNS nombre de ese cliente conectarse toowhen que deseaba un tooconnect tooSQL servidores a través de AlwaysOn.
* El recurso de dirección IP: se trata de Hola de direcciones IP que asociado hello VNN, puede tener más de uno y en una configuración multisitio tendrá una dirección IP por subred del sitio.

Cuando se recuperar registros DNS de hello asociados con el agente de escucha de Hola y se trata de tooconnect tooeach tooSQL conexión Server, controlador de SQL Server Client Hola siempre en había asociado dirección IP, a continuación se explican algunos de los factores que pueden influir en esto.

Hello número simultáneos de registros de DNS que están asociados con el nombre de agente de escucha de hello depende no solo de número de Hola de direcciones IP asociadas, pero hello ' RegisterAllIpProviders'setting en el clúster de conmutación por error para hello recursos siempre ON VNN.

Cuando se implementa de AlwaysOn en Azure hay pasos diferentes toocreate Hola agente de escucha y las direcciones IP, tiene toomanually configurar hello 'RegisterAllIpProviders' too1, esto es diferente tooan local siempre en la implementación donde ya se ha establecido too1.

Si 'RegisterAllIpProviders' es 0, sólo verá registro DNS en DNS asociado Hola agente de escucha:

![Appendix4][14]

Si “RegisterAllIpProviders” es 1:

![Appendix5][15]

siguiente de código de Hello se volcar Hola configuración VNN y se establecen automáticamente, por favor, tenga en cuenta que para hello Cambiar efecto tootake necesitará tootake hello VNN sin conexión y en línea volver a activarlo, este tomar Hola agente de escucha sin conexión que producen cliente conectividad interrupción.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

En un paso posterior de la migración se necesitarán tooupdate Hola siempre escucha de con una dirección IP actualizada que hará referencia a un equilibrador de carga, esto implica una eliminación de recursos de dirección IP y las sumas. Después de la actualización IP de hello, deberá tooensure Hola nueva dirección IP se ha actualizado en la zona DNS y que los clientes de Hola son actualizar su caché DNS local.

Si los clientes residen en un segmento de red diferente y hacer referencia a un servidor DNS diferente, deberá tooconsider lo que sucede con transferencia de zona DNS durante la migración de hello, como hello aplicación volver a conectarse se restringirá tiempo por Hola al menos el tiempo de transferencia de zona de las nuevas direcciones IP para el agente de escucha de Hola. Si está en la restricción del tiempo, debe analizar y probar forzando una transferencia de zona incremental con los equipos de Windows, y también coloca Hola DNS tooa registros de host reducir tiempo tooLive (TTL), para actualizan los clientes de Hola. Para más información, consulte las [transferencias de zona incrementales](https://technet.microsoft.com/library/cc958973.aspx) y [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Hola predeterminado TTL de registro DNS que está asociado con hello escucha en Always On en Azure es 1.200 segundos. Es recomendable tooreduce esto si se encuentra en la restricción del tiempo durante la actualización de los clientes de migración tooensure Hola sus DNS con la dirección IP de hello actualiza una dirección para el agente de escucha de Hola. Puede ver y modificar configuración de hello mediante el volcado de configuración de Hola Hola VNN:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Tenga en cuenta, Hola Hola inferior 'HostRecordTTL', se producirá una mayor cantidad de tráfico DNS.

##### <a name="client-application-settings"></a>Configuración de la aplicación cliente
Si la aplicación de cliente SQL es compatible con .NET Framework 4.5 de Hola SQLClient; a continuación, puede usar ' MULTISUBNETFAILOVER = TRUE' palabra clave, se recomienda hacer esto toobe aplicada tal y como permite para tooSQL de conexión más rápido siempre en el grupo de disponibilidad durante la conmutación por error. Enumera todas las direcciones IP asociadas con hello siempre en agente de escucha en paralelo y realiza una velocidad de reintento de conexión TCP más agresiva durante una conmutación por error.

Para obtener más información sobre la configuración de hello anterior, vea [palabra clave MultiSubnetFailover y características asociadas con](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Consulte también [Compatibilidad de SqlClient para la alta disponibilidad y la recuperación ante desastres](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Paso 5: Configuración del cuórum de clúster
Como va toobe sacar al menos un servidor de SQL hacia abajo a la vez, debe modificar la configuración de quórum de clúster de hello, si usa el testigo de recurso compartido de archivos (FSW) con 2 nodos, debe establecer la mayoría de nodo de hello quórum tooallow y utilizar el voto dinámico y se trata de tooallow para un pie de tooremain de nodo único.

    Set-ClusterQuorum -NodeMajority  

Para obtener más información sobre la administración y configuración de quórum de clúster de hello, visite [configurar y administrar Hola quórum en un clúster de conmutación por error de Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Paso 6: Extraer los extremos y las ACL existentes
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Guardar estos archivos de texto tooa.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Paso 7: Cambiar los asociados de conmutación por error y los modos de replicación
Si tiene más de 2 servidores SQL Server, se debe cambiar la conmutación por error de Hola de otra base de datos secundaria en otro controlador de dominio o local 'too'Synchronous y que sea un asociado de conmutación por error automática (AFP), por lo que mantener la alta disponibilidad al tiempo que se va a realizar cambios. Puede hacerlo a través de TSQL o modificarlo mediante SSMS:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Paso 8: Quitar la VM secundaria del servicio en la nube
Debe prepararse toomigrate un nodo secundario en la nube en primer lugar, si se trata actualmente principal, debe iniciar una conmutación por error manual.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Paso 9: Cambiar la configuración de la caché de disco en el archivo CSV y guardarla
Para volúmenes de datos se debe establecer tooREADONLY.

Para volúmenes de registro de transacciones se debe establecer tooNONE.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Paso 10: Copiar los VHD
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Puede comprobar estado de la copia de Hola de hello discos duros virtuales toohello cuenta de almacenamiento Premium:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Espere hasta que todos se registren como correctos.

Para obtener información sobre blobs individuales:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Paso 11: Registrar el disco del sistema operativo
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Paso 12: Importar el elemento secundario en el nuevo servicio en la nube
código de Hello siguiente también se agregan Hola de usos opción aquí se puede importar la máquina de Hola y utilizar hello conservable VIP.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Paso 13: Crear ILB en SVC en la nube nuevo y agregar extremos de carga equilibrada y ACL
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Paso 14: Actualizar AlwaysOn
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Quitar ahora Hola antiguo servicio en la nube dirección IP.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Paso 15: Comprobar actualizaciones de DNS
Ahora debe comprobar los servidores DNS en sus redes de cliente de SQL Server y asegúrese de que la agrupación en clústeres se agregado Hola registro host adicionales para hello agrega dirección IP. Si no han actualizado los servidores DNS, considere la posibilidad de forzar a una transferencia de zona DNS y asegúrese de que los clientes en la subred ahí hello sean tooresolve pueda tooboth siempre en direcciones IP, por lo que no es necesario toowait para la replicación automática de DNS.

#### <a name="step-16-reconfigure-always-on"></a>Paso 16: Reconfigurar AlwaysOn
En este momento espere Hola secundaria ese nodo que fue migrado toofully volver a sincronizar con el nodo local de Hola y cambie el nodo de replicación toosynchronous y hacerla AFP Hola.  

#### <a name="step-17-migrate-second-node"></a>Paso 17: Migrar el nodo secundario
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Paso 18: Cambiar la configuración de la caché de disco en el archivo CSV y guardarla
Para volúmenes de datos se debe establecer tooREADONLY.

Para volúmenes de registro de transacciones se debe establecer tooNONE.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Paso 19: Crear una nueva cuenta de almacenamiento independiente para el nodo secundario
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Paso 20: Copiar los VHD
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Puede comprobar el estado de copia de disco duro virtual de Hola para todos los discos duros virtuales: ForEach ($disk en $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. EtiquetaDeDisco $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Espere hasta que todos se registren como correctos.

Para obtener información sobre blobs individuales:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Paso 21: Registrar el disco del sistema operativo
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Paso 22: Agregar extremos de carga equilibrada y ACL
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Paso 23: Probar la conmutación por error
Ahora debe permitir que Hola migrados nodo sincronizar con hello local siempre en el nodo, lo coloca en modo de replicación toosynchronous y espere hasta que se sincronicen. A continuación, migra conmutación por error de local toohello primer nodo que es AFP Hola. Una vez que ha funcionado, cambio Hola migrado por última vez nodo toohello AFP.

Debe probar las conmutaciones por error entre todos los nodos y se ejecutan aunque pruebas chaos tooensure las conmutaciones por error de trabajo como se esperaba y en un tiempo manor.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Paso 24: Reponer la configuración del cuórum de clúster / TTL de DNS / asociados de conmutación por error / configuración de sincronización
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Agregar un recurso de dirección IP en la misma subred
Si tiene sólo 2 servidores SQL Server y desea toomigrate les tooa nuevo servicio en la nube, pero desea tookeep cambiarlas en Hola misma subred, puede evitar teniendo el agente de escucha de hello toodelete sin conexión Hola siempre original en la dirección IP y agregar Hola nueva dirección IP. Si va a migrar subred tooanother hello las máquinas virtuales que no necesitará toodo esto como habrá una red de clúster adicionales que hacen referencia a esa subred.

Una vez que haya llevado Hola migra la base de datos secundaria y agrega nuevo recurso de dirección IP hello para el nuevo servicio de nube Hola antes de conmutación por error Hola primario existente, debe completar estos pasos en hello Administrador de clústeres de conmutación por error:

tooadd en dirección IP, vea hello [apéndice](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), paso 14.

1. Para el recurso de dirección IP actual de hello, cambiar propietario posible de hello too'Existing principal de SQL Server ", en el ejemplo de Hola a continuación, 'dansqlams4':

    ![Appendix13][23]
2. Para el recurso de dirección IP nueva hello, cambiar Hola posible propietario too'Migrated SQL Server secundario ', en el ejemplo de Hola a continuación, 'dansqlams5':

    ![Appendix14][24]
3. Una vez que se establece puede conmutar por error y, cuando se migra el último nodo de Hola Hola posibles propietarios debe editarse para que ese nodo se agrega como un propietario posible:

    ![Appendix15][25]

## <a name="additional-resources"></a>Recursos adicionales
* [Almacenamiento Premium de Azure](../../../storage/common/storage-premium-storage.md)
* [Máquinas virtuales](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server en máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
