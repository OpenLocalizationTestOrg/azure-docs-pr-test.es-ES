---
title: "las imágenes de aaaCreate y carga una VM FreeBSD | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate y cargar un disco duro virtual (VHD) que contiene toocreate de sistema operativo de hello FreeBSD máquinas virtuales de Azure"
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
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="4028f-103">Crear y cargar un tooAzure FreeBSD VHD</span><span class="sxs-lookup"><span data-stu-id="4028f-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="4028f-104">Este artículo muestra cómo toocreate y cargar un disco duro virtual (VHD) que contiene Hola sistema de operativo FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="4028f-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="4028f-105">Después de cargarlo, puede usarlo como su propia toocreate imagen una máquina virtual (VM) en Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4028f-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4028f-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4028f-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="4028f-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4028f-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4028f-109">Para obtener información sobre cómo cargar un VHD con el modelo del Administrador de recursos de hello, consulte [aquí](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4028f-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4028f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4028f-110">Prerequisites</span></span>
<span data-ttu-id="4028f-111">Este artículo se supone que dispone de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="4028f-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="4028f-112">**Una suscripción de Azure**: si no tiene una cuenta, puede crear una en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="4028f-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="4028f-113">Si tiene una suscripción a MSDN, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="4028f-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="4028f-114">De lo contrario, obtenga información acerca de cómo demasiado[crear una cuenta de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4028f-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="4028f-115">**Herramientas de Azure PowerShell**: módulo de Azure PowerShell Hola debe estar instalado y configurado toouse su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="4028f-116">módulo de hello toodownload, consulte [descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4028f-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="4028f-117">Un tutorial que describe cómo tooinstall y configurar el módulo de hello está disponible aquí.</span><span class="sxs-lookup"><span data-stu-id="4028f-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="4028f-118">Hola de uso [descargas de Azure](https://azure.microsoft.com/downloads/) Hola de cmdlet tooupload disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="4028f-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="4028f-119">**Sistema de operativo FreeBSD instalado en un archivo .vhd**--un sistema de operativo FreeBSD compatible debe ser tooa disco duro instalado.</span><span class="sxs-lookup"><span data-stu-id="4028f-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="4028f-120">Varias herramientas existen archivos .vhd de toocreate.</span><span class="sxs-lookup"><span data-stu-id="4028f-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="4028f-121">Por ejemplo, puede usar una solución de virtualización como archivo .vhd de Hyper-V toocreate Hola e instalar sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="4028f-122">Para obtener instrucciones sobre cómo tooinstall y usar Hyper-V, vea [instalar Hyper-V y crear una máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="4028f-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4028f-123">no se admite el formato VHDX más reciente de Hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="4028f-124">Puede convertir el formato de tooVHD de disco de hello mediante el Administrador de Hyper-V u Hola cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="4028f-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="4028f-125">Además, hay un [tutorial de MSDN acerca de cómo toouse FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="4028f-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="4028f-126">Esta tarea incluye Hola siguiendo cinco pasos:</span><span class="sxs-lookup"><span data-stu-id="4028f-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="4028f-127">Paso 1: Preparar la imagen de hello para la carga</span><span class="sxs-lookup"><span data-stu-id="4028f-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="4028f-128">En máquina virtual de Hola donde instaló el sistema operativo de hello FreeBSD, complete Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4028f-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="4028f-129">Habilite DHCP.</span><span class="sxs-lookup"><span data-stu-id="4028f-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="4028f-130">Habilite SSH.</span><span class="sxs-lookup"><span data-stu-id="4028f-130">Enable SSH.</span></span>

    <span data-ttu-id="4028f-131">Asegúrese de que el servidor SSH Hola se instala y configura toostart al arrancar el sistema.</span><span class="sxs-lookup"><span data-stu-id="4028f-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="4028f-132">De forma predeterminada, se habilita después de la instalación desde el disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="4028f-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="4028f-133">Configure la consola de serie.</span><span class="sxs-lookup"><span data-stu-id="4028f-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="4028f-134">Instale sudo.</span><span class="sxs-lookup"><span data-stu-id="4028f-134">Install sudo.</span></span>

    <span data-ttu-id="4028f-135">cuenta de Hello raíz está deshabilitada en Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="4028f-136">Esto significa que necesita tooutilize sudo desde un comandos toorun de usuario sin privilegios con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="4028f-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="4028f-137">Requisitos previos del agente de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="4028f-138">Instale el agente de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-138">Install Azure Agent.</span></span>

    <span data-ttu-id="4028f-139">Hello versión más reciente de hello agente de Azure siempre se encuentra en [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="4028f-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="4028f-140">Hola versión 2.0.10 + admita oficialmente FreeBSD 10 & 10.1 y esta versión de Hola 2.1.4 + (incluidos 2.2) admite oficialmente 10.2 FreeBSD y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="4028f-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="4028f-141">Para 2.0, usaremos la 2.0.16 como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4028f-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="4028f-142">Para 2.1, utilizaremos la 2.1.4 como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4028f-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="4028f-143">Después de instalar al agente de Azure, es un tooverify buena idea que se está ejecutando:</span><span class="sxs-lookup"><span data-stu-id="4028f-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="4028f-144">Desaprovisionar sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-144">Deprovision hello system.</span></span>

    <span data-ttu-id="4028f-145">Desaprovisionamiento Hola tooclean del sistema y asegúrese de que adecuado para reaprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="4028f-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="4028f-146">Hello siguiente comando también elimina última cuenta de usuario aprovisionado Hola y Hola asociado datos:</span><span class="sxs-lookup"><span data-stu-id="4028f-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="4028f-147">Ahora ya puede apagar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4028f-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="4028f-148">Paso 2: Creación de una cuenta de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="4028f-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="4028f-149">Se necesita una cuenta de almacenamiento en un archivo .vhd de Azure tooupload por lo que puede ser usado toocreate una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4028f-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="4028f-150">Puede usar hello toocreate portal clásico una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="4028f-151">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4028f-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4028f-152">En la barra de comandos de hello, seleccione **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="4028f-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="4028f-153">Seleccione **Data Services** > **Storage** > **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="4028f-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Crear rápidamente una cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="4028f-155">Rellene los campos de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="4028f-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="4028f-156">Hola **dirección URL** , escriba un toouse de nombre de subdominio en hello URL de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4028f-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="4028f-157">entrada de Hello puede contener entre 3 y 24 números y letras en minúscula.</span><span class="sxs-lookup"><span data-stu-id="4028f-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="4028f-158">Este nombre se convierte en el nombre de host de hello dentro de dirección URL de hello tooaddress usa almacenamiento de blobs de Azure, almacenamiento en la cola de Azure o recursos de almacenamiento de tabla de Azure para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="4028f-159">Hola **ubicación/grupo de afinidad** menú desplegable, elija hello **ubicación o grupo de afinidad** Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4028f-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="4028f-160">Un grupo de afinidad le permite colocar los servicios en la nube y el almacenamiento en hello mismo centro de datos.</span><span class="sxs-lookup"><span data-stu-id="4028f-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="4028f-161">Hola **replicación** , a continuación, decidir si toouse **con redundancia geográfica** replicación Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4028f-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="4028f-162">La replicación geográfica está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4028f-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="4028f-163">Esta opción replica la tooa secundaria ubicación de datos, en ningún tooyou de costo, para que el almacenamiento se conmuta toothat ubicación si un error grave, se produce en la ubicación principal Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="4028f-164">ubicación secundaria Hola se asigna automáticamente y no se puede cambiar.</span><span class="sxs-lookup"><span data-stu-id="4028f-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="4028f-165">Si necesita más control sobre la ubicación de Hola de su almacenamiento en la nube debido a los requisitos de toolegal o directiva organizativa, puede desactivar la replicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="4028f-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="4028f-166">Sin embargo, tenga presente que si más adelante activar la replicación geográfica, se le cobrará una sola vez tooreplicate de cuota de transferencia de datos la ubicación secundaria de toohello de datos existente.</span><span class="sxs-lookup"><span data-stu-id="4028f-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="4028f-167">Los servicios de almacenamiento sin replicación geográfica se ofrecen con descuento.</span><span class="sxs-lookup"><span data-stu-id="4028f-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="4028f-168">Puede encontrar más información sobre la administración de la replicación geográfica de cuentas de almacenamiento aquí: [Replicación de Azure Storage](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="4028f-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Escribir los detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="4028f-170">Haga clic en **Crear cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4028f-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="4028f-171">Hello cuenta aparece ahora en **almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="4028f-171">hello account now appears under **storage**.</span></span>

    ![Cuenta de almacenamiento creada correctamente](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="4028f-173">Después, cree un contenedor para los archivos .vhd que ha cargado.</span><span class="sxs-lookup"><span data-stu-id="4028f-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="4028f-174">Seleccione el nombre de cuenta de almacenamiento de hello y, a continuación, seleccione **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="4028f-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="4028f-176">Seleccione **Crear un contenedor**.</span><span class="sxs-lookup"><span data-stu-id="4028f-176">Select **Create a Container**.</span></span>

    ![Detalles de la cuenta de almacenamiento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="4028f-178">Hola **nombre** , escriba un nombre para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="4028f-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="4028f-179">A continuación, en hello **acceso** menú de lista desplegable, seleccione el tipo de directiva de acceso que desee.</span><span class="sxs-lookup"><span data-stu-id="4028f-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nombre del contenedor](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="4028f-181">De forma predeterminada, el contenedor de hello es privado y sólo pueden obtener acceso el propietario de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="4028f-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="4028f-182">tooallow acceso de lectura público toohello blobs en el contenedor de hello, pero no las propiedades de contenedor toohello y metadatos, utilice hello **Blob público** opción.</span><span class="sxs-lookup"><span data-stu-id="4028f-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="4028f-183">acceso de lectura público completo tooallow hello contenedor y blobs, use hello **contenedor público** opción.</span><span class="sxs-lookup"><span data-stu-id="4028f-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="4028f-184">Paso 3: Preparar Hola conexión tooAzure</span><span class="sxs-lookup"><span data-stu-id="4028f-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="4028f-185">Antes de poder cargar un archivo .vhd, debe tooestablish una conexión segura entre el equipo y su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="4028f-186">Puede usar el método de hello Azure Active Directory (Azure AD) u Hola certificado método toodo.</span><span class="sxs-lookup"><span data-stu-id="4028f-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="4028f-187">Usar tooupload de método hello Azure AD un archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="4028f-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="4028f-188">Consola de Azure PowerShell Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="4028f-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="4028f-189">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4028f-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="4028f-190">Este comando abre una ventana de inicio de sesión donde podrá iniciar sesión con su cuenta profesional o educativa.</span><span class="sxs-lookup"><span data-stu-id="4028f-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Ventana de PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="4028f-192">Azure se autentica y guarda la información de credenciales de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="4028f-193">A continuación, cierra la ventana hello.</span><span class="sxs-lookup"><span data-stu-id="4028f-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="4028f-194">Usar tooupload de método hello certificado un archivo .vhd</span><span class="sxs-lookup"><span data-stu-id="4028f-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="4028f-195">Consola de Azure PowerShell Hola abierto.</span><span class="sxs-lookup"><span data-stu-id="4028f-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="4028f-196">Escriba: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="4028f-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="4028f-197">Una ventana del explorador se abre y se le pide toodownload Hola archivo .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="4028f-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="4028f-198">Este archivo contiene información y un certificado para su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Página de descarga del explorador](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="4028f-200">Guarde el archivo .publishsettings de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="4028f-201">Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, donde `<PathToFile>` es el archivo .publishsettings de hello ruta de acceso completa toohello.</span><span class="sxs-lookup"><span data-stu-id="4028f-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="4028f-202">Para obtener información, consulte [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx)(Introducción a los cmdlets de Azure).</span><span class="sxs-lookup"><span data-stu-id="4028f-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="4028f-203">Para obtener más información sobre la instalación y configuración de PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4028f-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="4028f-204">Paso 4: Cargar archivo .vhd de hello</span><span class="sxs-lookup"><span data-stu-id="4028f-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="4028f-205">Cuando se carga el archivo .vhd de hello, puede colocarlo en cualquier lugar dentro de su almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="4028f-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="4028f-206">Estos son algunos de los términos que se utilizará al cargar el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="4028f-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="4028f-207">**BlobStorageURL** es la dirección URL de Hola Hola cuenta de almacenamiento que creó en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="4028f-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="4028f-208">**YourImagesFolder** esté contenedor Hola dentro del almacenamiento de blobs donde desee toostore las imágenes.</span><span class="sxs-lookup"><span data-stu-id="4028f-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="4028f-209">**VHDName** es Hola etiqueta que aparece en el disco de duro virtual de hello Azure tooidentify portal clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="4028f-210">**PathToVHDFile** es la ruta de acceso completa de Hola y el nombre de archivo .vhd de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="4028f-211">Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="4028f-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="4028f-212">Paso 5: Crear una máquina virtual con archivo .vhd cargado de hello</span><span class="sxs-lookup"><span data-stu-id="4028f-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="4028f-213">Después de cargar el archivo .vhd de hello, puede agregarlo como una lista de toohello de imagen de imágenes personalizadas que están asociados a su suscripción y crear una máquina virtual con esta imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="4028f-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="4028f-214">Desde la ventana de PowerShell de Azure de hello utilizada en el paso anterior de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="4028f-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="4028f-215">Usar Linux como tipo de sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="4028f-216">versión actual de PowerShell de Azure de Hello acepta solo "Linux" o "Windows" como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="4028f-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="4028f-217">Después de completar los pasos anteriores de hello, nueva imagen de hello aparece cuando se elige hello **imágenes** ficha en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="4028f-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Elija una imagen](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="4028f-219">Crear una máquina virtual desde la Galería de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="4028f-220">Esta nueva imagen ahora está disponible en **Mis imágenes**.</span><span class="sxs-lookup"><span data-stu-id="4028f-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="4028f-221">Seleccione la nueva imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="4028f-221">Select hello new image.</span></span> <span data-ttu-id="4028f-222">A continuación, vaya a través de hello solicita tooset un nombre de host, contraseña, clave SSH, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="4028f-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Imagen personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="4028f-224">Después de completar el aprovisionamiento de hello, verá la VM de FreeBSD ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="4028f-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Imagen de FreeBSD en Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
