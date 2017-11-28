---
title: "Instalación de un servidor de destino maestro de Linux para realizar una conmutación por error de Azure a un entorno local | Microsoft Docs"
description: "Antes de volver a proteger una máquina virtual Linux, necesita un servidor de destino maestro Linux. Aquí le mostraremos cómo instalar uno."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="d2509-104">Instalación de un servidor de destino maestro Linux</span><span class="sxs-lookup"><span data-stu-id="d2509-104">Install a Linux master target server</span></span>
<span data-ttu-id="d2509-105">Después de conmutar por error las máquinas virtuales, puede conmutarlas por recuperación en el sitio local.</span><span class="sxs-lookup"><span data-stu-id="d2509-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="d2509-106">Para ello, debe volver a proteger la máquina virtual de Azure en el sitio local.</span><span class="sxs-lookup"><span data-stu-id="d2509-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="d2509-107">Para realizar este proceso, necesitará un servidor de destino maestro local que reciba el tráfico.</span><span class="sxs-lookup"><span data-stu-id="d2509-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="d2509-108">Si la máquina virtual protegida es una máquina virtual Windows, necesitará un destino maestro de Windows.</span><span class="sxs-lookup"><span data-stu-id="d2509-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="d2509-109">Para una máquina virtual Linux, se necesita un destino maestro de Linux.</span><span class="sxs-lookup"><span data-stu-id="d2509-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="d2509-110">Lea los pasos siguientes para aprender a crear e instalar un destino maestro de Linux.</span><span class="sxs-lookup"><span data-stu-id="d2509-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2509-111">A partir de la versión 9.10.0 del servidor de destino maestro, el servidor de destino maestro más reciente solo puede instalarse en un servidor Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="d2509-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="d2509-112">Las nuevas instalaciones no están permitidas en servidores CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="d2509-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="d2509-113">Pero puede seguir actualizando los servidores de destino maestros anteriores con la versión 9.10.0.</span><span class="sxs-lookup"><span data-stu-id="d2509-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="d2509-114">Información general</span><span class="sxs-lookup"><span data-stu-id="d2509-114">Overview</span></span>
<span data-ttu-id="d2509-115">En este artículo se proporcionan instrucciones para instalar un destino maestro Linux.</span><span class="sxs-lookup"><span data-stu-id="d2509-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="d2509-116">Publique cualquier comentario o pregunta que tenga al final del artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d2509-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2509-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d2509-117">Prerequisites</span></span>

* <span data-ttu-id="d2509-118">Para elegir el host en el que se va a implementar el destino maestro, determine si la conmutación por recuperación va a ser en una máquina virtual local existente o en una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="d2509-119">En el caso de una máquina virtual existente, el host del destino maestro debe tener acceso a los almacenes de datos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="d2509-120">Si la máquina virtual local no existe, se crea la máquina virtual de conmutación por recuperación en el mismo host que el destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="d2509-121">Puede elegir cualquier host ESXi para instalar el destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="d2509-122">El destino maestro debe estar en una red que pueda comunicarse con el servidor de procesos y el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="d2509-123">La versión del destino maestro debe ser igual o anterior a las versiones del servidor de procesos y el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="d2509-124">Por ejemplo, si la versión del servidor de configuración es 9.4, la versión del destino maestro puede ser 9.4 o 9.3, pero no 9.5.</span><span class="sxs-lookup"><span data-stu-id="d2509-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="d2509-125">El destino maestro solo puede ser una máquina virtual de VMware y no un servidor físico.</span><span class="sxs-lookup"><span data-stu-id="d2509-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="d2509-126">Creación del destino maestro según las directrices de ajuste de tamaño</span><span class="sxs-lookup"><span data-stu-id="d2509-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="d2509-127">Cree el destino maestro conforme a las siguientes directrices de ajuste de tamaño:</span><span class="sxs-lookup"><span data-stu-id="d2509-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="d2509-128">**RAM**: 6 GB o más</span><span class="sxs-lookup"><span data-stu-id="d2509-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="d2509-129">**Tamaño del disco del sistema operativo**: 100 GB o más (para instalar CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="d2509-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="d2509-130">**Tamaño adicional de disco para la unidad de retención**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="d2509-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="d2509-131">**Núcleos de CPU**: 4 núcleos o más</span><span class="sxs-lookup"><span data-stu-id="d2509-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="d2509-132">Se admiten los siguientes kernels de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d2509-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="d2509-133">Serie de kernel</span><span class="sxs-lookup"><span data-stu-id="d2509-133">Kernel Series</span></span>  |<span data-ttu-id="d2509-134">Admite hasta la versión</span><span class="sxs-lookup"><span data-stu-id="d2509-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="d2509-135">4.4.</span><span class="sxs-lookup"><span data-stu-id="d2509-135">4.4</span></span>      |<span data-ttu-id="d2509-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="d2509-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="d2509-137">4.8</span><span class="sxs-lookup"><span data-stu-id="d2509-137">4.8</span></span>      |<span data-ttu-id="d2509-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="d2509-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="d2509-139">4.10</span><span class="sxs-lookup"><span data-stu-id="d2509-139">4.10</span></span>     |<span data-ttu-id="d2509-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="d2509-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="d2509-141">Implementación del servidor de destino maestro</span><span class="sxs-lookup"><span data-stu-id="d2509-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="d2509-142">Instalación de Ubuntu 16.04.2 mínima</span><span class="sxs-lookup"><span data-stu-id="d2509-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="d2509-143">Siga los siguientes pasos para instalar el sistema operativo Ubuntu 16.04.2 de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d2509-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="d2509-144">**Paso 1:** vaya al [vínculo de descarga](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) y elija el reflejo más cercano para descargar una imagen ISO de 64 bits mínima de Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="d2509-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="d2509-145">Coloque una imagen ISO de 64 bits mínima de Ubuntu 16.04.2 en la unidad de DVD e inicie el sistema.</span><span class="sxs-lookup"><span data-stu-id="d2509-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="d2509-146">**Paso 2:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selección de un idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="d2509-148">**Paso 3:** seleccione **Install Ubuntu Server** (Instalar servidor Ubuntu) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selección de instalación de servidor Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="d2509-150">**Paso 4:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selección de inglés como idioma preferido](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="d2509-152">**Paso 5:** seleccione la opción adecuada de la lista de opciones **Time Zone** (Zona horaria) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![Selección de la zona horaria correcta](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="d2509-154">**Paso 6:** seleccione **No** (opción predeterminada) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![Configuración del teclado](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="d2509-156">**Paso 7:** seleccione **English (US)** [Inglés (EE. UU.)] como país de origen para el teclado y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![Selección de EE. UU. como país de origen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="d2509-158">**Paso 8:** seleccione **English (US)** [Inglés (EE. UU.)] como distribución del teclado y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![Selección de inglés de EE. UU. como distribución del teclado](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="d2509-160">**Paso 9:** escriba el nombre de host del servidor en el cuadro **Hostname** (Nombre de host) y luego seleccione **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="d2509-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![Especificación del nombre de host del servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="d2509-162">**Paso 10:** para crear una cuenta de usuario, escriba el nombre de usuario y luego seleccione **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="d2509-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![Crea una cuenta de usuario](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="d2509-164">**Paso 11:** escriba la contraseña de la nueva cuenta de usuario y luego seleccione **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="d2509-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![Especificación de la contraseña](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="d2509-166">**Paso 12:** confirme la contraseña del nuevo usuario y luego seleccione **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="d2509-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![Confirmación de las contraseñas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="d2509-168">**Paso 13:** seleccione **No** (opción predeterminada) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![Configuración de usuarios y contraseñas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="d2509-170">**Paso 14:** si la zona horaria que se muestra es correcta, seleccione **Sí** (opción predeterminada) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="d2509-171">Para volver a configurar la zona horaria, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="d2509-171">To reconfigure your time zone, select **No**.</span></span>

![Configuración del reloj](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="d2509-173">**Paso 15:** en las opciones de método de partición, seleccione **Guided - use entire disk** (Guiado: usar todo el disco) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selección de la opción de método de partición](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="d2509-175">**Paso 16:** seleccione el disco adecuado en las opciones de **Select disk to partition** (Seleccionar disco para la partición) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![Selección del disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="d2509-177">**Paso 17:** seleccione **Sí** para escribir los cambios en el disco y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![Escritura de los cambios en el disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="d2509-179">**Paso 18:** seleccione la opción predeterminada, seleccione **Continue** (Continuar) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![Selección de la opción predeterminada](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="d2509-181">**Paso 19:** seleccione la opción adecuada para administrar las actualizaciones en el sistema y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selección de forma de administrar las actualizaciones](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="d2509-183">Dado que el servidor de destino maestro de Azure Site Recovery exige una versión muy concreta de Ubuntu, tiene que asegurarse de que las actualizaciones del kernel se deshabiliten para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="d2509-184">Si están habilitadas, las actualizaciones normales hacen que el servidor de destino maestro no funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="d2509-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="d2509-185">Asegúrese de seleccionar la opción **No automatic updates** (Sin actualizaciones automáticas).</span><span class="sxs-lookup"><span data-stu-id="d2509-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="d2509-186">**Paso 20:** seleccione las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="d2509-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="d2509-187">Si quiere usar OpenSSH para la conexión SSH, seleccione la opción **OpenSSH server** (Servidor de OpenSSH) y luego **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="d2509-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![Selección de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="d2509-189">**Paso 21:** seleccione **Sí** y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Instalación del cargador de arranque GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="d2509-191">**Paso 22:** seleccione el dispositivo adecuado para la instalación del cargador de arranque (preferiblemente **/dev/sda**) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selección de un dispositivo para la instalación del cargador de arranque](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="d2509-193">**Paso 23:** seleccione **Continue** (Continuar) y luego **Entrar** para finalizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="d2509-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![Fin de la instalación](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="d2509-195">Una vez finalizada la instalación, inicie sesión en la máquina virtual con las credenciales del nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="d2509-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="d2509-196">(Vea el **paso 10** para más información).</span><span class="sxs-lookup"><span data-stu-id="d2509-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="d2509-197">Siga los pasos que se indican en la siguiente captura de pantalla para establecer la contraseña del usuario raíz.</span><span class="sxs-lookup"><span data-stu-id="d2509-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="d2509-198">Luego inicie sesión como usuario raíz.</span><span class="sxs-lookup"><span data-stu-id="d2509-198">Then sign in as ROOT user.</span></span>

![Establecimiento de la contraseña del usuario raíz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="d2509-200">Preparación del equipo para configurarlo como servidor de destino maestro</span><span class="sxs-lookup"><span data-stu-id="d2509-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="d2509-201">Ahora prepare el equipo para configurarlo como servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="d2509-202">Para obtener el identificador de cada disco duro SCSI de una máquina virtual Linux, habilite el parámetro **disk.EnableUUID = TRUE**.</span><span class="sxs-lookup"><span data-stu-id="d2509-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="d2509-203">Para habilitar este parámetro, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d2509-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="d2509-204">Apague la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="d2509-205">Haga clic con el botón derecho en la entrada de la máquina virtual del panel izquierdo y luego seleccione **Editar configuración**.</span><span class="sxs-lookup"><span data-stu-id="d2509-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="d2509-206">Seleccione la pestaña **Opciones**.</span><span class="sxs-lookup"><span data-stu-id="d2509-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="d2509-207">En el panel izquierdo, seleccione **Opciones avanzadas** > **General** y luego el botón **Parámetros de configuración** de la parte inferior derecha de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="d2509-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![Pestaña de opciones](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="d2509-209">La opción **Configuration Parameters** (Parámetros de configuración) no está disponible cuando la máquina está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d2509-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="d2509-210">Para activar esta pestaña, apague la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="d2509-211">Vea si ya existe una fila con **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="d2509-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="d2509-212">Si el valor existe y está establecido en **False**, cámbielo a **True**.</span><span class="sxs-lookup"><span data-stu-id="d2509-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="d2509-213">(Los valores no distinguen mayúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="d2509-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="d2509-214">Si el valor existe y está establecido en **True**, seleccione **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="d2509-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="d2509-215">Si el valor no existe, seleccione **Agregar fila**.</span><span class="sxs-lookup"><span data-stu-id="d2509-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="d2509-216">En la columna de nombre, agregue **disk.EnableUUID** y luego establezca el valor en **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="d2509-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![Comprobación de si el disk.EnableUUID existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="d2509-218">Deshabilitación de actualizaciones de kernel</span><span class="sxs-lookup"><span data-stu-id="d2509-218">Disable kernel upgrades</span></span>

<span data-ttu-id="d2509-219">El servidor de destino maestro de Azure Site Recovery exige una versión muy concreta de Ubuntu, así que asegúrese de que las actualizaciones del kernel se deshabiliten para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="d2509-220">Si están habilitadas, las actualizaciones normales hacen que el servidor de destino maestro no funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="d2509-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="d2509-221">Descarga e instalación de paquetes adicionales</span><span class="sxs-lookup"><span data-stu-id="d2509-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="d2509-222">Asegúrese de que tiene conectividad a Internet para descargar e instalar paquetes adicionales.</span><span class="sxs-lookup"><span data-stu-id="d2509-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="d2509-223">Si no tiene conectividad a Internet, tiene que encontrar manualmente estos paquetes RPM e instalarlos.</span><span class="sxs-lookup"><span data-stu-id="d2509-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="d2509-224">Obtención del instalador para la configuración</span><span class="sxs-lookup"><span data-stu-id="d2509-224">Get the installer for setup</span></span>

<span data-ttu-id="d2509-225">Si el destino maestro tiene conectividad a Internet, puede usar los pasos siguientes para descargar el instalador.</span><span class="sxs-lookup"><span data-stu-id="d2509-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="d2509-226">De lo contrario, puede copiar el instalador del servidor de procesos y luego instalarlo.</span><span class="sxs-lookup"><span data-stu-id="d2509-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="d2509-227">Descarga de los paquetes de instalación del destino maestro</span><span class="sxs-lookup"><span data-stu-id="d2509-227">Download the master target installation packages</span></span>

<span data-ttu-id="d2509-228">[Descargue los bits más recientes de instalación del destino maestro de Linux](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="d2509-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="d2509-229">Para descargarlos mediante Linux, escriba:</span><span class="sxs-lookup"><span data-stu-id="d2509-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="d2509-230">Asegúrese de que descarga y descomprime el instalador en el directorio principal.</span><span class="sxs-lookup"><span data-stu-id="d2509-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="d2509-231">Si lo descomprime en **/usr/Local**, se produce un error en la instalación.</span><span class="sxs-lookup"><span data-stu-id="d2509-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="d2509-232">Acceso al instalador desde el servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="d2509-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="d2509-233">En el servidor de procesos, vaya a **C:\Archivos de programa (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="d2509-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="d2509-234">Copie el archivo necesario del instalador del servidor de procesos y guárdelo como **latestlinuxmobsvc.tar.gz** en el directorio principal.</span><span class="sxs-lookup"><span data-stu-id="d2509-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="d2509-235">Aplicación de cambios en la configuración personalizada</span><span class="sxs-lookup"><span data-stu-id="d2509-235">Apply custom configuration changes</span></span>

<span data-ttu-id="d2509-236">Para aplicar cambios de configuración personalizados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d2509-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="d2509-237">Ejecute el siguiente comando para descomprimir el archivo binario.</span><span class="sxs-lookup"><span data-stu-id="d2509-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de pantalla del comando que se va a ejecutar](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="d2509-239">Ejecute el comando siguiente para conceder permiso.</span><span class="sxs-lookup"><span data-stu-id="d2509-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="d2509-240">Ejecute el siguiente comando para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="d2509-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="d2509-241">Ejecute el script sólo una vez en el servidor.</span><span class="sxs-lookup"><span data-stu-id="d2509-241">Run the script only once on the server.</span></span> <span data-ttu-id="d2509-242">Cierre el servidor.</span><span class="sxs-lookup"><span data-stu-id="d2509-242">Shut down the server.</span></span> <span data-ttu-id="d2509-243">Después de agregar un disco, reinicie el servidor como se explica en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="d2509-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="d2509-244">Adición de un disco de retención a la máquina virtual de destino maestro de Linux</span><span class="sxs-lookup"><span data-stu-id="d2509-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="d2509-245">Use los pasos siguientes para crear un disco de retención:</span><span class="sxs-lookup"><span data-stu-id="d2509-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="d2509-246">Conecte un nuevo disco de 1 TB a la máquina virtual de destino maestro Linux y luego iníciela.</span><span class="sxs-lookup"><span data-stu-id="d2509-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="d2509-247">Use el comando **multipath -ll** para conocer el identificador de múltiples rutas del disco de retención.</span><span class="sxs-lookup"><span data-stu-id="d2509-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![El identificador de múltiples rutas del disco de retención](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="d2509-249">Aplique formato a la unidad y luego cree un sistema de archivos en ella.</span><span class="sxs-lookup"><span data-stu-id="d2509-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Creación de un sistema de archivos en la unidad](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="d2509-251">Después de crear el sistema de archivos, monte el disco de retención.</span><span class="sxs-lookup"><span data-stu-id="d2509-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Montaje del disco de retención](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="d2509-253">Cree la entrada **fstab** para montar la unidad de retención cada vez que se inicie el sistema.</span><span class="sxs-lookup"><span data-stu-id="d2509-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="d2509-254">Seleccione **Insertar** para comenzar a editar el archivo.</span><span class="sxs-lookup"><span data-stu-id="d2509-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="d2509-255">Cree una nueva línea y luego inserte el siguiente texto.</span><span class="sxs-lookup"><span data-stu-id="d2509-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="d2509-256">Edite el identificador de múltiples rutas del disco basándose en el identificador de múltiples rutas resaltado del comando anterior.</span><span class="sxs-lookup"><span data-stu-id="d2509-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="d2509-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="d2509-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="d2509-258">Seleccione **Esc** y luego escriba **:wq** (escribir y salir) para cerrar la ventana del editor.</span><span class="sxs-lookup"><span data-stu-id="d2509-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="d2509-259">Instalación del destino maestro</span><span class="sxs-lookup"><span data-stu-id="d2509-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2509-260">La versión del servidor de destino maestro debe ser igual o anterior a las versiones del servidor de procesos y el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="d2509-261">Si no se cumple esta condición, la reprotección se realiza correctamente, pero se produce un error en la replicación.</span><span class="sxs-lookup"><span data-stu-id="d2509-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="d2509-262">Antes de instalar el servidor de destino maestro, compruebe que el archivo **/etc/hosts** de la máquina virtual contiene entradas que asignan el nombre de host local a las direcciones IP asociadas a todos los adaptadores de red.</span><span class="sxs-lookup"><span data-stu-id="d2509-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="d2509-263">Copie la frase de contraseña de **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** en el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="d2509-264">Luego guarde como **passphrase.txt** en el mismo directorio local al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2509-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="d2509-265">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2509-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="d2509-266">Anote la dirección IP del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="d2509-267">La necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2509-267">You need it in the next step.</span></span>

3. <span data-ttu-id="d2509-268">Ejecute el siguiente comando para instalar el servidor de destino maestro y registre el servidor con el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="d2509-269">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2509-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="d2509-270">Espere a que finalice el script.</span><span class="sxs-lookup"><span data-stu-id="d2509-270">Wait until the script finishes.</span></span> <span data-ttu-id="d2509-271">Si el destino maestro se registra correctamente, aparece en la página **Infraestructura de Site Recovery** del portal.</span><span class="sxs-lookup"><span data-stu-id="d2509-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="d2509-272">Instalación del destino maestro mediante la instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="d2509-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="d2509-273">Ejecute el siguiente comando para instalar el destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-273">Run the following command to install the master target.</span></span> <span data-ttu-id="d2509-274">Para el rol de agente, elija **Destino maestro**.</span><span class="sxs-lookup"><span data-stu-id="d2509-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="d2509-275">Elija la ubicación predeterminada para la instalación y luego seleccione **Entrar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="d2509-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![Elección de una ubicación predeterminada para la instalación del destino maestro](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="d2509-277">Una vez finalizada la instalación, registre el servidor de configuración mediante la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="d2509-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="d2509-278">Anote la dirección IP del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="d2509-279">La necesitará en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2509-279">You need it in the next step.</span></span>

2. <span data-ttu-id="d2509-280">Ejecute el siguiente comando para instalar el servidor de destino maestro y registre el servidor con el servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="d2509-281">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d2509-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="d2509-282">Espere a que finalice el script.</span><span class="sxs-lookup"><span data-stu-id="d2509-282">Wait until the script finishes.</span></span> <span data-ttu-id="d2509-283">Si el destino maestro se ha registrado correctamente, aparece en la página **Infraestructura de Site Recovery** del portal.</span><span class="sxs-lookup"><span data-stu-id="d2509-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="d2509-284">Actualización del destino maestro</span><span class="sxs-lookup"><span data-stu-id="d2509-284">Upgrade the master target</span></span>

<span data-ttu-id="d2509-285">Ejecute al programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="d2509-285">Run the installer.</span></span> <span data-ttu-id="d2509-286">Detecta automáticamente que el agente está instalado en el destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="d2509-287">Para actualizar, seleccione **Y**.  Una vez finalizada la instalación, compruebe la versión del destino maestro instalado mediante el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="d2509-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="d2509-288">Puede ver que el campo **Versión** indica el número de versión del destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="d2509-289">Instale las herramientas de VMware en el servidor de destino principal.</span><span class="sxs-lookup"><span data-stu-id="d2509-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="d2509-290">Debe instalar las herramientas de VMware en el destino maestro para poder detectar los almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="d2509-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="d2509-291">Si las herramientas no están instaladas, la pantalla de reprotección no aparece en los almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="d2509-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="d2509-292">Después de la instalación de las herramientas de VMware, tiene que reiniciar.</span><span class="sxs-lookup"><span data-stu-id="d2509-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2509-293">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2509-293">Next steps</span></span>
<span data-ttu-id="d2509-294">Una vez que han terminado la instalación y el registro del destino maestro, puede ver este en la sección **Destino maestro** de **Infraestructura de Site Recovery**, en la información general del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="d2509-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="d2509-295">Ahora ya puede continuar con la [reprotección](site-recovery-how-to-reprotect.md), seguido de la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="d2509-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="d2509-296">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="d2509-296">Common issues</span></span>

* <span data-ttu-id="d2509-297">Asegúrese de no activar Storage vMotion en ningún componente de administración como, por ejemplo, un destino maestro.</span><span class="sxs-lookup"><span data-stu-id="d2509-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="d2509-298">Si el destino maestro se mueve después de un reprotección correcta, no se pueden desasociar los discos de máquina virtual (VMDK).</span><span class="sxs-lookup"><span data-stu-id="d2509-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="d2509-299">En este caso se produce un error en la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="d2509-299">In this case, failback fails.</span></span>

* <span data-ttu-id="d2509-300">La máquina de destino maestro no debe contener ninguna instantánea en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2509-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="d2509-301">Si hay instantáneas, se produce un error en la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="d2509-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="d2509-302">Debido a ciertas configuraciones de NIC personalizadas en algunos clientes, la interfaz de red está deshabilitada durante el inicio, por lo que el agente del destino maestro no se puede inicializar.</span><span class="sxs-lookup"><span data-stu-id="d2509-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="d2509-303">Asegúrese de que se han definido correctamente las siguientes propiedades.</span><span class="sxs-lookup"><span data-stu-id="d2509-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="d2509-304">Compruebe estas propiedades en /etc/sysconfig/network-scripts/ifcfg-eth* del archivo de la tarjeta Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d2509-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="d2509-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="d2509-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="d2509-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="d2509-306">ONBOOT=yes</span></span>
