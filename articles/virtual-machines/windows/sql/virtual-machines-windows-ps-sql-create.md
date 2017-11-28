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
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="8712a-103">Aprovisionamiento de una máquina virtual de SQL mediante Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8712a-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8712a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8712a-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="8712a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8712a-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="8712a-106">Información general</span><span class="sxs-lookup"><span data-stu-id="8712a-106">Overview</span></span>
<span data-ttu-id="8712a-107">Este tutorial muestra cómo toocreate una sola máquina virtual de Azure utilizando Hola **Azure Resource Manager** modelo de implementación mediante cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="8712a-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8712a-108">En este tutorial, creamos una sola máquina virtual con una sola unidad de disco de una imagen en hello Galería de SQL.</span><span class="sxs-lookup"><span data-stu-id="8712a-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="8712a-109">Se creará nuevos proveedores de almacenamiento de hello, red y recursos de proceso que se usará para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="8712a-110">Si ya dispone de proveedores existentes para cualquiera de estos recursos, puede usarlos en su lugar.</span><span class="sxs-lookup"><span data-stu-id="8712a-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="8712a-111">Si necesita hello versión básica de este tema, consulte [aprovisionar una máquina virtual de SQL Server con PowerShell de Azure clásico](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="8712a-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8712a-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8712a-112">Prerequisites</span></span>
<span data-ttu-id="8712a-113">Para este tutorial, necesitará:</span><span class="sxs-lookup"><span data-stu-id="8712a-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="8712a-114">una cuenta de Azure y una suscripción antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="8712a-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="8712a-115">Si no tiene una, suscríbase para [una prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8712a-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8712a-116">[Azure PowerShell](/powershell/azure/overview), versión 1.4.0 (mínima) o posterior (en este tutorial se usa la versión 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="8712a-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="8712a-117">tooretrieve su versión, escriba **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="8712a-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="8712a-118">Configuración de su suscripción</span><span class="sxs-lookup"><span data-stu-id="8712a-118">Configure your subscription</span></span>
<span data-ttu-id="8712a-119">Abra Windows PowerShell y establecer acceso tooyour cuenta de Azure ejecutando el siguiente cmdlet de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="8712a-120">Se le presentará un inicio de sesión en la pantalla tooenter sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="8712a-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="8712a-121">Use Hola mismo correo electrónico y la contraseña que usa toosign en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8712a-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="8712a-122">Tras iniciar sesión correctamente en verá parte de la información en pantalla que incluye SubscriptionId Hola con la que ha iniciado sesión en.</span><span class="sxs-lookup"><span data-stu-id="8712a-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="8712a-123">Se trata de una suscripción de hello en el que se crearán los recursos de Hola para este tutorial a menos que cambie tooa otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="8712a-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="8712a-124">Si tiene varios identificadores de suscripción, ejecute hello siguiente cmdlet tooreturn una lista de todos los identificadores de suscripción:</span><span class="sxs-lookup"><span data-stu-id="8712a-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="8712a-125">toochange tooanother Id. de suscripción, ejecute hello siguiente cmdlet con el Id. de suscripción deseado.</span><span class="sxs-lookup"><span data-stu-id="8712a-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="8712a-126">Definición de variables de imagen</span><span class="sxs-lookup"><span data-stu-id="8712a-126">Define image variables</span></span>
<span data-ttu-id="8712a-127">facilidad de uso de toosimplify y la comprensión del script de Hola completado de este tutorial, se iniciará mediante la definición de una serie de variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="8712a-128">Cambiar los valores de parámetro de hello como considere oportuno, pero tenga cuidado de nomenclatura restricciones relacionadas tooname longitudes y caracteres especiales al modificar los valores de hello proporcionados.</span><span class="sxs-lookup"><span data-stu-id="8712a-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="8712a-129">Ubicación y grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8712a-129">Location and Resource Group</span></span>
<span data-ttu-id="8712a-130">Use dos variables toodefine Hola datos hello y área de grupo de recursos en la que se crearán Hola otros recursos para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="8712a-131">Puede modificarlo como quiera y, a continuación, ejecute hello después cmdlets tooinitialize estas variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="8712a-132">Propiedades de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8712a-132">Storage properties</span></span>
<span data-ttu-id="8712a-133">Usar hello siguientes variables toodefine Hola hello y cuenta de tipo de almacenamiento de toobe de almacenamiento utilizado por la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="8712a-134">Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="8712a-135">Tenga en cuenta que en este ejemplo se usa [Almacenamiento premium](../../../storage/common/storage-premium-storage.md), que es el recomendado para cargas de trabajo de producción.</span><span class="sxs-lookup"><span data-stu-id="8712a-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="8712a-136">Para más información sobre esta guía y para otras recomendaciones, consulte [Prácticas recomendadas para mejorar el rendimiento para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8712a-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="8712a-137">Propiedades de red</span><span class="sxs-lookup"><span data-stu-id="8712a-137">Network properties</span></span>
<span data-ttu-id="8712a-138">Usar hello siguiendo la interfaz de red de las variables toodefine Hola, método de asignación de hello TCP/IP, nombre de red virtual de hello, nombre de subred virtual de hello, Hola intervalo de direcciones IP para la red virtual de hello, Hola intervalo de direcciones IP para la subred de Hola y Hola toobe de etiqueta de nombre de dominio público utilizado por red hello en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="8712a-139">Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="8712a-140">Propiedades de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8712a-140">Virtual machine properties</span></span>
<span data-ttu-id="8712a-141">Usar hello después el nombre de máquina virtual de variables toodefine Hola, nombre de equipo de hello, tamaño de máquina virtual de Hola y nombre del disco de sistema operativo de hello para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="8712a-142">Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="8712a-143">Propiedades de la imagen</span><span class="sxs-lookup"><span data-stu-id="8712a-143">Image properties</span></span>
<span data-ttu-id="8712a-144">Usar hello siguientes variables toodefine Hola imagen toouse para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="8712a-145">En este ejemplo, se utiliza la imagen de SQL Server 2016 Enterprise Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="8712a-146">Puede modificarlo como quiera y, a continuación, ejecute hello siguiente cmdlet tooinitialize estas variables.</span><span class="sxs-lookup"><span data-stu-id="8712a-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="8712a-147">Tenga en cuenta que puede obtener una lista completa de las ofertas de la imagen de SQL Server con el comando Get-AzureRmVMImageOffer hello:</span><span class="sxs-lookup"><span data-stu-id="8712a-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="8712a-148">Y puede ver Hola SKU disponibles para una oferta con el comando Get-AzureRmVMImageSku Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="8712a-149">Hello siguiente comando muestra todas las SKU disponibles para hello **SQL2014SP1 WS2012R2** ofrecen.</span><span class="sxs-lookup"><span data-stu-id="8712a-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="8712a-150">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8712a-150">Create a resource group</span></span>
<span data-ttu-id="8712a-151">Con el modelo de implementación del Administrador de recursos de hello, Hola primer objeto que se crea es grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="8712a-152">Usaremos hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate un grupo de recursos de Azure y sus recursos con recursos de Hola grupo nombre y ubicación definida por las variables de hello inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="8712a-153">Ejecute hello siguiente cmdlet toocreate su nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8712a-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="8712a-154">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8712a-154">Create a storage account</span></span>
<span data-ttu-id="8712a-155">máquina virtual de Hello requiere recursos de almacenamiento para el disco del sistema operativo de Hola y hello datos de SQL Server y los archivos de registro.</span><span class="sxs-lookup"><span data-stu-id="8712a-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="8712a-156">Por motivos de simplicidad, crearemos un único disco para ambos.</span><span class="sxs-lookup"><span data-stu-id="8712a-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="8712a-157">Puede adjuntar discos adicionales posteriormente mediante hello [Azure Agregar disco](/powershell/module/azure/add-azuredisk) cmdlet en orden tooplace los datos de SQL Server y los archivos de registro en discos dedicados.</span><span class="sxs-lookup"><span data-stu-id="8712a-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="8712a-158">Usaremos hello [AzureRmStorageAccount New](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate un almacenamiento estándar de la cuenta en el nuevo grupo de recursos y con nombre de cuenta de almacenamiento de hello, el nombre de Sku de almacenamiento y la ubicación definido mediante variables de Hola que inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8712a-159">Ejecute hello siguiente cmdlet toocreate la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8712a-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="8712a-160">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="8712a-160">Create network resources</span></span>
<span data-ttu-id="8712a-161">máquina virtual de Hello requiere un número de recursos de red para la conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="8712a-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="8712a-162">Cada máquina virtual requiere una red virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="8712a-163">Una red virtual debe tener al menos una subred definida.</span><span class="sxs-lookup"><span data-stu-id="8712a-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="8712a-164">Una interfaz de red debe definirse con una dirección IP privada o pública.</span><span class="sxs-lookup"><span data-stu-id="8712a-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="8712a-165">Creación de una configuración de subred de una red virtual</span><span class="sxs-lookup"><span data-stu-id="8712a-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="8712a-166">Comenzaremos por crear una configuración de subred para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="8712a-167">En nuestro tutorial, se creará una subred de forma predeterminada con hello [AzureRmVirtualNetworkSubnetConfig New](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8712a-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="8712a-168">Nuestra configuración de subred de red virtual se creará con el prefijo de nombre y la dirección de la subred de hello definido mediante las variables de hello inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="8712a-169">Puede definir propiedades adicionales de configuración de subred de red virtual de hello mediante este cmdlet, pero que está más allá del ámbito de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8712a-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="8712a-170">Ejecute hello siguiente cmdlet toocreate la configuración de subred virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="8712a-171">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="8712a-171">Create a virtual network</span></span>
<span data-ttu-id="8712a-172">A continuación, se creará la red virtual con hello [AzureRmVirtualNetwork New](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8712a-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="8712a-173">Se creará la red virtual en el nuevo grupo de recursos con nombre hello, la ubicación y el prefijo de dirección definida mediante variables de Hola que inicializado anteriormente y usar la configuración de subred de Hola que definió en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="8712a-174">Ejecute hello siguiente cmdlet toocreate la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="8712a-175">Crear dirección IP pública de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-175">Create hello public IP address</span></span>
<span data-ttu-id="8712a-176">Ahora que tenemos nuestro red virtual definido, necesitamos tooconfigure una dirección IP para la máquina virtual de toohello de conectividad.</span><span class="sxs-lookup"><span data-stu-id="8712a-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="8712a-177">Para este tutorial, creamos una dirección IP pública mediante toosupport conectividad a Internet de direccionamiento IP dinámica.</span><span class="sxs-lookup"><span data-stu-id="8712a-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="8712a-178">Usaremos hello [AzureRmPublicIpAddress New](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Hola dirección IP pública en hello recursos grupo creado anteriormente y con nombre de hello, ubicación, método de asignación y etiqueta de nombre de dominio DNS definido mediante Hola variables que haya inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="8712a-179">Puede definir propiedades adicionales de la dirección IP pública Hola con este cmdlet, pero que está más allá del ámbito de Hola de este tutorial inicial.</span><span class="sxs-lookup"><span data-stu-id="8712a-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="8712a-180">También puede crear una dirección privada o una dirección con una dirección estática, pero que también sea más allá del ámbito de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8712a-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="8712a-181">Ejecute hello siguiente cmdlet toocreate la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="8712a-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="8712a-182">Crear la interfaz de red de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-182">Create hello network interface</span></span>
<span data-ttu-id="8712a-183">Ahora estamos interfaz de red de hello toocreate preparado que va a usar de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="8712a-184">Usaremos hello [AzureRmNetworkInterface New](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nuestra interfaz de red en grupo de recursos de Hola que creó anteriormente y con nombre de hello, ubicación, subred y la dirección IP pública definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="8712a-185">Ejecute hello siguiente cmdlet toocreate la interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="8712a-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="8712a-186">Configuración de un objeto de VM</span><span class="sxs-lookup"><span data-stu-id="8712a-186">Configure a VM object</span></span>
<span data-ttu-id="8712a-187">Ahora que tenemos los recursos de almacenamiento y de red definidos, estamos listos toodefine los recursos de proceso para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="8712a-188">En nuestro tutorial, se especificará tamaño de máquina virtual de Hola y diversas propiedades de sistema operativo, especificar la interfaz de red de Hola que creamos previamente, definir el almacenamiento de blobs y, a continuación, especifique el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="8712a-189">Crear objeto de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-189">Create hello VM object</span></span>
<span data-ttu-id="8712a-190">Empezaremos especificando el tamaño de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="8712a-191">Para este tutorial, vamos a especificar un DS13.</span><span class="sxs-lookup"><span data-stu-id="8712a-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="8712a-192">Usaremos hello [AzureRmVMConfig New](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate un objeto de máquina virtual puede configurarse con nombre de Hola y el tamaño definido mediante las variables de hello inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8712a-193">Ejecute hello después el objeto de máquina virtual de cmdlet toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="8712a-194">Crear un nombre de credencial objeto toohold hello y una contraseña para las credenciales de administrador local de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="8712a-195">Antes de que podemos establecer las propiedades de sistema operativo de la máquina virtual de Hola Hola, necesitamos sus credenciales de hello toosupply para la cuenta de administrador local de hello como una cadena segura.</span><span class="sxs-lookup"><span data-stu-id="8712a-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="8712a-196">tooaccomplish, usaremos hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8712a-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="8712a-197">Ejecutar el siguiente cmdlet de hello y, en la ventana de solicitud de credenciales de Windows PowerShell de hello, escriba Hola toouse nombre y una contraseña para la cuenta de administrador local de hello en la máquina virtual de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8712a-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="8712a-198">Establecer las propiedades de sistema operativo de hello para la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="8712a-199">Ahora estamos propiedades del sistema operativo preparado tooset hello de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="8712a-200">Usaremos hello [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset Hola tipo de sistema operativo como Windows, requieren hello [agente de máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique ese Hola habilita automáticamente actualizar y establecer nombre de máquina virtual de hello, nombre de equipo de Hola y la credencial de hello mediante las variables de hello inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8712a-201">Ejecute hello después de las propiedades de sistema operativo de cmdlet tooset hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="8712a-202">Agregar una máquina virtual Hola red interfaz toohello</span><span class="sxs-lookup"><span data-stu-id="8712a-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="8712a-203">A continuación, se agregará la interfaz de red de Hola que creamos previamente toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8712a-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="8712a-204">Usaremos hello [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interfaz de red de cmdlet tooadd hello mediante la variable de interfaz de red de Hola que definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="8712a-205">Ejecute hello siguiendo la interfaz de red de cmdlet tooset hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="8712a-206">Establecer ubicación de almacenamiento de blobs de Hola de hello toobe de disco utilizado por la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="8712a-207">A continuación, se establecerá la ubicación de almacenamiento de blobs de Hola de hello toobe de disco utilizado por máquina virtual de hello mediante variables de Hola que definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="8712a-208">Ejecute hello después de la ubicación de almacenamiento de blobs de cmdlet tooset Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="8712a-209">Establecer propiedades de disco de máquina virtual de Hola de sistema operativo de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="8712a-210">A continuación, se establecerá sistema de operativo Hola propiedades de disco de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="8712a-211">Usaremos hello [conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify de cmdlet que Hola de sistema operativo de la máquina virtual de hello procederán de una imagen, tooset tooread solo el almacenamiento en caché (porque se está instalando SQL Server en hello mismo disco) y definir nombre de la máquina virtual de Hola y disco del sistema operativo Hola definido mediante variables de Hola que hemos definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="8712a-212">Ejecute hello siguientes propiedades del disco de sistema operativo cmdlet tooset hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="8712a-213">Especifique la imagen de la plataforma de hello para la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="8712a-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="8712a-214">El último paso de configuración es la imagen de la plataforma toospecify hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="8712a-215">En nuestro tutorial, usamos la imagen de SQL Server 2016 CTP más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="8712a-216">Usaremos hello [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse esta imagen tal como se define mediante variables de Hola que definió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8712a-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="8712a-217">Ejecute hello siguiente cmdlet toospecify la imagen de la plataforma de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="8712a-218">Crear hello VM de SQL</span><span class="sxs-lookup"><span data-stu-id="8712a-218">Create hello SQL VM</span></span>
<span data-ttu-id="8712a-219">Ahora que ha terminado de pasos de configuración de hello, está listo toocreate Hola virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8712a-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="8712a-220">Usaremos hello [AzureRmVM New](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Hola máquina virtual a través variables Hola que hemos definido.</span><span class="sxs-lookup"><span data-stu-id="8712a-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="8712a-221">Ejecute hello siguiente cmdlet toocreate la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8712a-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="8712a-222">se crea la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8712a-222">hello virtual machine is created.</span></span> <span data-ttu-id="8712a-223">Observe que se crea una cuenta de almacenamiento estándar para el diagnóstico de arranque porque Hola la cuenta de almacenamiento para el disco de la máquina virtual Hola especificada es una cuenta de almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="8712a-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="8712a-224">Ahora puede ver esta máquina en hello Azure Portal toosee [su dirección IP pública y su nombre de dominio completo](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8712a-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="8712a-225">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8712a-225">Example script</span></span>
<span data-ttu-id="8712a-226">Hello siguiente secuencia de comandos contiene script de PowerShell de hello completo para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8712a-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="8712a-227">Supone que ya tiene el programa de instalación Hola suscripción de Azure toouse con hello **agregar AzureRmAccount** y **seleccione AzureRmSubscription** comandos.</span><span class="sxs-lookup"><span data-stu-id="8712a-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8712a-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8712a-228">Next steps</span></span>
<span data-ttu-id="8712a-229">Después de crear la máquina virtual de hello, está listo tooconnect toohello máquina con conectividad RDP y el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="8712a-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="8712a-230">Para obtener más información, consulte [conectar tooa Máquina Virtual de SQL Server en Azure (Administrador de recursos)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8712a-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

