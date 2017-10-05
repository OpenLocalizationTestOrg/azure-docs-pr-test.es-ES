---
title: "Creación y carga de una imagen de máquina virtual de FreeBSD | Microsoft Docs"
description: "Aprenda a crear y cargar un disco duro virtual (VHD) que contenga el sistema operativo FreeBSD para crear una máquina virtual de Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="f8152-103">Creación y carga de un VHD de FreeBSD en Azure</span><span class="sxs-lookup"><span data-stu-id="f8152-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="f8152-104">En este artículo se muestra cómo crear y cargar un disco duro virtual (VHD) que contenga el sistema operativo FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="f8152-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="f8152-105">Después de cargarlo, puede utilizarlo como su propia imagen para crear una máquina virtual (VM) en Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f8152-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8152-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f8152-107">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="f8152-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f8152-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="f8152-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f8152-109">Para más información sobre cómo cargar un VHD con el modelo de Resource Manager, consulte [aquí](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8152-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8152-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f8152-110">Prerequisites</span></span>
<span data-ttu-id="f8152-111">En este artículo se supone que tiene los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f8152-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="f8152-112">**Una suscripción de Azure**: si no tiene una cuenta, puede crear una en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="f8152-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="f8152-113">Si tiene una suscripción a MSDN, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="f8152-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="f8152-114">De lo contrario, obtenga información sobre cómo [crear una cuenta de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8152-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="f8152-115">**Herramientas de Azure PowerShell**: el módulo Azure PowerShell debe estar instalado y configurado para utilizar su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="f8152-116">Para descargar el módulo, consulte la página de [descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f8152-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="f8152-117">Hay disponible aquí un tutorial que describe cómo instalar y configurar el módulo.</span><span class="sxs-lookup"><span data-stu-id="f8152-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="f8152-118">Use el cmdlet de [descargas de Azure](https://azure.microsoft.com/downloads/) para cargar el VHD.</span><span class="sxs-lookup"><span data-stu-id="f8152-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="f8152-119">**Sistema operativo FreeBSD instalado en un archivo .vhd**: se debe instalar un sistema operativo FreeBSD compatible en un disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f8152-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="f8152-120">Existen varias herramientas para crear archivos .vhd.</span><span class="sxs-lookup"><span data-stu-id="f8152-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="f8152-121">Por ejemplo, puede utilizar una solución de virtualización como Hyper-V para crear el archivo .vhd e instalar el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f8152-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="f8152-122">Para obtener instrucciones sobre cómo instalar y utilizar Hyper-V, consulte [Instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8152-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f8152-123">el reciente formato VHDX no se admite en Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="f8152-124">Puede convertir el disco al formato VHD mediante el Administrador de Hyper-V o el cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8152-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="f8152-125">Además, hay un [tutorial en MSDN sobre cómo utilizar FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8152-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="f8152-126">Esta tarea incluye los cinco pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8152-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="f8152-127">Paso 1: Preparación de la imagen que se va a cargar</span><span class="sxs-lookup"><span data-stu-id="f8152-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="f8152-128">En la máquina virtual en la que se instaló el sistema operativo FreeBSD, realice los procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f8152-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="f8152-129">Habilite DHCP.</span><span class="sxs-lookup"><span data-stu-id="f8152-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="f8152-130">Habilite SSH.</span><span class="sxs-lookup"><span data-stu-id="f8152-130">Enable SSH.</span></span>

    <span data-ttu-id="f8152-131">Asegúrese de que el servidor SSH se haya instalado y configurado para iniciarse en el tiempo de arranque.</span><span class="sxs-lookup"><span data-stu-id="f8152-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="f8152-132">De forma predeterminada, se habilita después de la instalación desde el disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="f8152-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="f8152-133">Configure la consola de serie.</span><span class="sxs-lookup"><span data-stu-id="f8152-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="f8152-134">Instale sudo.</span><span class="sxs-lookup"><span data-stu-id="f8152-134">Install sudo.</span></span>

    <span data-ttu-id="f8152-135">La cuenta raíz está deshabilitada en Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="f8152-136">Esto significa que deberá usar sudo con un usuario sin privilegios para ejecutar comandos con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="f8152-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="f8152-137">Requisitos previos del agente de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="f8152-138">Instale el agente de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-138">Install Azure Agent.</span></span>

    <span data-ttu-id="f8152-139">Siempre puede encontrar la versión más reciente del agente de Azure en [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="f8152-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="f8152-140">La versión 2.0.10 + admite oficialmente FreeBSD 10 y 10.1 y la versión 2.1.4 (incluida la 2.2.x) admite oficialmente FreeBSD 10.2 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="f8152-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="f8152-141">Para 2.0, usaremos la 2.0.16 como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8152-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="f8152-142">Para 2.1, utilizaremos la 2.1.4 como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f8152-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="f8152-143">Después de instalar el agente de Azure, es recomendable comprobar que está ejecutándose:</span><span class="sxs-lookup"><span data-stu-id="f8152-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="f8152-144">Desaprovisione el sistema.</span><span class="sxs-lookup"><span data-stu-id="f8152-144">Deprovision the system.</span></span>

    <span data-ttu-id="f8152-145">Desaprovisione el sistema para limpiarlo y dejarlo adecuado para el reaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="f8152-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="f8152-146">El comando siguiente también elimina la última cuenta de usuario aprovisionada y los datos asociados:</span><span class="sxs-lookup"><span data-stu-id="f8152-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="f8152-147">Ahora ya puede apagar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8152-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="f8152-148">Paso 2: Creación de una cuenta de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="f8152-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="f8152-149">Necesita una cuenta de almacenamiento de Azure para cargar un archivo .vhd, que se puede usar para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8152-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="f8152-150">Puede utilizar el portal clásico de Azure para crear una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8152-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="f8152-151">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f8152-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f8152-152">En la barra de comandos, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="f8152-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="f8152-153">Seleccione **Data Services** > **Storage** > **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="f8152-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Crear rápidamente una cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="f8152-155">Rellene los campos de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8152-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="f8152-156">En el campo **URL** , escriba un nombre de subdominio que vaya a usar en la URL de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8152-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="f8152-157">Esta entrada puede contener de 3 a 24 números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f8152-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="f8152-158">Este nombre se convierte en el nombre del host dentro de la dirección URL que se usó para direccionar el Almacenamiento de blobs de Azure, el Almacenamiento en cola de Azure o los recursos de Almacenamiento de tablas de Azure de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f8152-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="f8152-159">En la lista desplegable **Ubicación/grupo de afinidad**, seleccione una **ubicación o grupo de afinidad** para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8152-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="f8152-160">Un grupo de afinidad le permite colocar sus servicios y almacenamiento en la nube en el mismo centro de datos.</span><span class="sxs-lookup"><span data-stu-id="f8152-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="f8152-161">En el campo **Replicación**, decida si va a usar la replicación **Redundancia geográfica** para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f8152-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="f8152-162">La replicación geográfica está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f8152-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="f8152-163">Esta opción replica los datos en una ubicación secundaria, sin coste, por lo que su almacenamiento conmuta por error a esa ubicación si se produce un error importante en la ubicación principal.</span><span class="sxs-lookup"><span data-stu-id="f8152-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="f8152-164">La ubicación secundaria se asigna automáticamente y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="f8152-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="f8152-165">Si necesita más control sobre la ubicación del almacenamiento en la nube debido a requisitos legales o las directivas de su organización, puede desactivar la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="f8152-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="f8152-166">Sin embargo, tenga en cuenta que si más tarde activa la replicación geográfica, deberá pagar una cuota de transferencia de datos puntual para replicar los datos existentes en la ubicación secundaria.</span><span class="sxs-lookup"><span data-stu-id="f8152-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="f8152-167">Los servicios de almacenamiento sin replicación geográfica se ofrecen con descuento.</span><span class="sxs-lookup"><span data-stu-id="f8152-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="f8152-168">Puede encontrar más información sobre la administración de la replicación geográfica de cuentas de almacenamiento aquí: [Replicación de Azure Storage](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="f8152-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Escribir los detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="f8152-170">Haga clic en **Crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="f8152-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="f8152-171">La cuenta aparece ahora en **Almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="f8152-171">The account now appears under **storage**.</span></span>

    ![Cuenta de almacenamiento creada correctamente](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="f8152-173">Después, cree un contenedor para los archivos .vhd que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="f8152-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="f8152-174">Seleccione el nombre de la cuenta de almacenamiento y, a continuación, elija **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="f8152-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="f8152-176">Seleccione **Crear un contenedor**.</span><span class="sxs-lookup"><span data-stu-id="f8152-176">Select **Create a Container**.</span></span>

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="f8152-178">En el campo **Nombre** , escriba un nombre para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="f8152-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="f8152-179">A continuación, en el menú desplegable **Acceso** , seleccione el tipo de directiva de acceso que desee.</span><span class="sxs-lookup"><span data-stu-id="f8152-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nombre del contenedor](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="f8152-181">De manera predeterminada, el contenedor es privado y solo puede acceder a él el propietario de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="f8152-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="f8152-182">Para permitir el acceso de lectura público a los blobs del contenedor, pero no a las propiedades y metadatos del contenedor, use la opción **Blob público** .</span><span class="sxs-lookup"><span data-stu-id="f8152-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="f8152-183">Para permitir el acceso de lectura público completo para el contenedor y los blobs, utilice la opción **Contenedor público** .</span><span class="sxs-lookup"><span data-stu-id="f8152-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="f8152-184">Paso 3: Preparación de la conexión a Azure</span><span class="sxs-lookup"><span data-stu-id="f8152-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="f8152-185">Antes de cargar el archivo .vhd, debe establecer una conexión segura entre el equipo y la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="f8152-186">Para ello, puede usar el método de Azure Active Directory (Azure AD) o el método del certificado.</span><span class="sxs-lookup"><span data-stu-id="f8152-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="f8152-187">Uso del método de Azure AD para cargar un archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="f8152-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="f8152-188">Abra la consola de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8152-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="f8152-189">Escriba el siguiente comando: </span><span class="sxs-lookup"><span data-stu-id="f8152-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="f8152-190">Este comando abre una ventana de inicio de sesión donde podrá iniciar sesión con su cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="f8152-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Ventana de PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="f8152-192">Azure autentica y guarda las credenciales.</span><span class="sxs-lookup"><span data-stu-id="f8152-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="f8152-193">A continuación, cierra la ventana.</span><span class="sxs-lookup"><span data-stu-id="f8152-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="f8152-194">Uso del método del certificado para cargar un archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="f8152-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="f8152-195">Abra la consola de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8152-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="f8152-196">Escriba: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="f8152-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="f8152-197">Se abre una ventana del explorador que le solicita que descargue el archivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="f8152-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="f8152-198">Este archivo contiene información y un certificado para su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Página de descarga del explorador](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="f8152-200">Guarde el archivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="f8152-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="f8152-201">Escriba: `Import-AzurePublishSettingsFile <PathToFile>`, donde `<PathToFile>` es la ruta de acceso completa al archivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="f8152-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="f8152-202">Para obtener información, consulte [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)(Introducción a los cmdlets de Azure).</span><span class="sxs-lookup"><span data-stu-id="f8152-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="f8152-203">Para más información sobre cómo instalar Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f8152-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="f8152-204">Paso 4: Carga del archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="f8152-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="f8152-205">Cuando carga el archivo .vhd, puede colocarlo en cualquier parte del Almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f8152-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="f8152-206">A continuación se muestran algunos términos que se van a usar al cargar el archivo:</span><span class="sxs-lookup"><span data-stu-id="f8152-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="f8152-207">**URLAlmacenamientoDeBlobs** es la dirección URL de la cuenta de almacenamiento que ha creado en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="f8152-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="f8152-208">**SuCarpetaDeImágenes** es el contenedor de Almacenamiento de blobs en el que desea almacenar las imágenes.</span><span class="sxs-lookup"><span data-stu-id="f8152-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="f8152-209">**VHDName** es la etiqueta que aparece en el Portal de Azure clásico para identificar el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f8152-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="f8152-210">**PathToVHDFile** es la ruta de acceso completa y el nombre del archivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="f8152-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="f8152-211">Desde la ventana de Azure PowerShell que ha usado en el paso anterior, escriba:</span><span class="sxs-lookup"><span data-stu-id="f8152-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="f8152-212">Paso 5: Creación de una máquina virtual con el archivo .vhd cargado</span><span class="sxs-lookup"><span data-stu-id="f8152-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="f8152-213">Después de cargar el archivo .vhd, puede agregarlo como imagen a la lista de imágenes personalizadas que están asociadas con su suscripción y crear una máquina virtual con esta imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="f8152-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="f8152-214">Desde la ventana de Azure PowerShell que ha usado en el paso anterior, escriba:</span><span class="sxs-lookup"><span data-stu-id="f8152-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="f8152-215">Utilice Linux como tipo de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f8152-215">Use Linux as the OS type.</span></span> <span data-ttu-id="f8152-216">La versión actual de Azure PowerShell acepta solo "Linux" o "Windows" como parámetro.</span><span class="sxs-lookup"><span data-stu-id="f8152-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="f8152-217">Tras completar los pasos anteriores, la nueva imagen aparecerá en la lista cuando elija la pestaña **Imágenes** en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="f8152-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Elija una imagen](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="f8152-219">Cree una máquina virtual desde la galería.</span><span class="sxs-lookup"><span data-stu-id="f8152-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="f8152-220">Esta nueva imagen ahora está disponible en **Mis imágenes**.</span><span class="sxs-lookup"><span data-stu-id="f8152-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="f8152-221">Seleccione la nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="f8152-221">Select the new image.</span></span> <span data-ttu-id="f8152-222">Siga las indicaciones para configurar un nombre de host, una contraseña, una clave SSH, etc.</span><span class="sxs-lookup"><span data-stu-id="f8152-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Imagen personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="f8152-224">Una vez completado el aprovisionamiento, verá que la máquina virtual de FreeBSD se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="f8152-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Imagen de FreeBSD en Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
