---
title: "aaaHow tooinstall un servidor de destino maestro de Linux para conmutación por error desde Azure tooon-local | Documentos de Microsoft"
description: "Antes de volver a proteger una máquina virtual Linux, necesita un servidor de destino maestro Linux. Obtenga información acerca de cómo tooinstall uno."
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
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="b5da5-104">Instalación de un servidor de destino maestro Linux</span><span class="sxs-lookup"><span data-stu-id="b5da5-104">Install a Linux master target server</span></span>
<span data-ttu-id="b5da5-105">Después de conmutar las máquinas virtuales, puede producir un error al sitio local toohello Hola atrás máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b5da5-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="b5da5-106">toofail nuevo, deberá tooreprotect Hola virtual máquina desde el sitio de Azure toohello local.</span><span class="sxs-lookup"><span data-stu-id="b5da5-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="b5da5-107">En este proceso, es necesario un tráfico de hello local tooreceive de servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="b5da5-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="b5da5-108">Si la máquina virtual protegida es una máquina virtual Windows, necesitará un destino maestro de Windows.</span><span class="sxs-lookup"><span data-stu-id="b5da5-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="b5da5-109">Para una máquina virtual Linux, se necesita un destino maestro de Linux.</span><span class="sxs-lookup"><span data-stu-id="b5da5-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="b5da5-110">Lectura Hola siguientes pasos le indican toolearn cómo maestro toocreate e instale un Linux de destino.</span><span class="sxs-lookup"><span data-stu-id="b5da5-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5da5-111">A partir de la versión del servidor de destino maestro hello 9.10.0, servidor de destino maestro más reciente de hello puede solo instalarse en un servidor de Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="b5da5-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="b5da5-112">Las nuevas instalaciones no están permitidas en servidores CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="b5da5-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="b5da5-113">Sin embargo, puede seguir tooupgrade los servidores de destino maestra antigua mediante hello 9.10.0 versión.</span><span class="sxs-lookup"><span data-stu-id="b5da5-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="b5da5-114">Información general</span><span class="sxs-lookup"><span data-stu-id="b5da5-114">Overview</span></span>
<span data-ttu-id="b5da5-115">Este artículo proporciona instrucciones para cómo maestro tooinstall una Linux de destino.</span><span class="sxs-lookup"><span data-stu-id="b5da5-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="b5da5-116">Enviar comentarios o preguntas al final de Hola de este artículo o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b5da5-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5da5-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b5da5-117">Prerequisites</span></span>

* <span data-ttu-id="b5da5-118">host de hello toochoose en qué destino maestro de hello toodeploy, determinar si Hola conmutación por recuperación se va toobe tooan locales existentes máquina virtual o una máquina virtual nueva de tooa.</span><span class="sxs-lookup"><span data-stu-id="b5da5-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="b5da5-119">Para una máquina virtual existente, host de hello del destino maestro Hola debe tener acceso a almacenes de datos toohello de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="b5da5-120">Si no existe la máquina virtual de hello en local, máquina virtual de conmutación por recuperación de Hola se crea en Hola mismo host como destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="b5da5-121">Puede elegir cualquier host ESXi destino maestro de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="b5da5-122">destino maestro Hola debe estar en una red que puede comunicarse con el servidor de procesos de Hola y el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="b5da5-123">versión de Hola de destino maestro de Hola debe ser igual tooor anteriores a las versiones de servidor de procesos de Hola y el servidor de configuración de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="b5da5-124">Por ejemplo, si versión Hola Hola del servidor de configuración se 9.4, versión de Hola de destino maestro Hola pueda 9.4 o 9.3 pero no 9,5.</span><span class="sxs-lookup"><span data-stu-id="b5da5-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="b5da5-125">destino maestro Hola solo puede tener una máquina virtual VMware y no un servidor físico.</span><span class="sxs-lookup"><span data-stu-id="b5da5-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="b5da5-126">Crear el destino maestro Hola según toohello directrices de ajuste de tamaño</span><span class="sxs-lookup"><span data-stu-id="b5da5-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="b5da5-127">Crear el destino maestro de hello según Hola siguiendo las directrices de ajuste de tamaño:</span><span class="sxs-lookup"><span data-stu-id="b5da5-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="b5da5-128">**RAM**: 6 GB o más</span><span class="sxs-lookup"><span data-stu-id="b5da5-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="b5da5-129">**Tamaño de disco de SO**: 100 GB o más (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="b5da5-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="b5da5-130">**Tamaño adicional de disco para la unidad de retención**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="b5da5-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="b5da5-131">**Núcleos de CPU**: 4 núcleos o más</span><span class="sxs-lookup"><span data-stu-id="b5da5-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="b5da5-132">siguiente Hola admite Ubuntu kernels son compatibles.</span><span class="sxs-lookup"><span data-stu-id="b5da5-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="b5da5-133">Serie de kernel</span><span class="sxs-lookup"><span data-stu-id="b5da5-133">Kernel Series</span></span>  |<span data-ttu-id="b5da5-134">Admitir hasta demasiado</span><span class="sxs-lookup"><span data-stu-id="b5da5-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="b5da5-135">4.4.</span><span class="sxs-lookup"><span data-stu-id="b5da5-135">4.4</span></span>      |<span data-ttu-id="b5da5-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="b5da5-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="b5da5-137">4.8</span><span class="sxs-lookup"><span data-stu-id="b5da5-137">4.8</span></span>      |<span data-ttu-id="b5da5-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="b5da5-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="b5da5-139">4.10</span><span class="sxs-lookup"><span data-stu-id="b5da5-139">4.10</span></span>     |<span data-ttu-id="b5da5-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="b5da5-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="b5da5-141">Implementar el servidor de destino maestro Hola</span><span class="sxs-lookup"><span data-stu-id="b5da5-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="b5da5-142">Instalación de Ubuntu 16.04.2 mínima</span><span class="sxs-lookup"><span data-stu-id="b5da5-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="b5da5-143">Tomar Hola después de sistema operativo de 64 bits Ubuntu 16.04.2 de hello pasos tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="b5da5-144">**Paso 1:** vaya toohello [vínculo de descarga](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) y elija reflejado más cercano de Hola desde que descargar una imagen de ISO de 64 bits mínima de Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="b5da5-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="b5da5-145">Mantener una imagen de ISO de 64 bits mínima de Ubuntu 16.04.2 en la unidad de DVD de hello e inicie el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="b5da5-146">**Paso 2:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selección de un idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="b5da5-148">**Paso 3:** seleccione **Install Ubuntu Server** (Instalar servidor Ubuntu) y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selección de instalación de servidor Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="b5da5-150">**Paso 4:** seleccione **English** (Inglés) como idioma preferido y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selección de inglés como idioma preferido](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="b5da5-152">**Paso 5:** seleccione Hola opción adecuada de hello **zona horaria** lista de opciones y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Seleccione la zona horaria correcta de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="b5da5-154">**Paso 6:** seleccione **No** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Configurar el teclado de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="b5da5-156">**Paso 7:** seleccione **inglés (Estados Unidos)** como Hola país de origen para el teclado de hello y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Seleccionar Estados Unidos como país Hola de origen](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="b5da5-158">**Paso 8:** seleccione **inglés (Estados Unidos)** como distribución del teclado hello y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Seleccione el inglés de Estados Unidos como la distribución del teclado Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="b5da5-160">**Paso 9:** escriba el nombre de host de hello para el servidor en hello **Hostname** cuadro y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Escriba el nombre de host de hello para el servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="b5da5-162">**Paso 10:** toocreate una cuenta de usuario, escriba el nombre de usuario de hello y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Crea una cuenta de usuario](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="b5da5-164">**Paso 11:** escribir contraseña de hello para la nueva cuenta de usuario de hello y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Escriba la contraseña de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="b5da5-166">**Paso 12:** Confirmar contraseña Hola Hola nuevo usuario y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Confirmar las contraseñas de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="b5da5-168">**Paso 13:** seleccione **No** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Configuración de usuarios y contraseñas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="b5da5-170">**Paso 14:** si la zona horaria de Hola que se muestra es correcto, seleccione **Sí** (hello la opción predeterminada) y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="b5da5-171">tooreconfigure su zona horaria, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-171">tooreconfigure your time zone, select **No**.</span></span>

![Configurar el reloj de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="b5da5-173">**Paso 15:** en hello opciones del método de creación de particiones, seleccione **interactiva - usar todo el disco**y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Seleccione la opción método de creación de particiones de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="b5da5-175">**Paso 16:** seleccione Hola disco adecuado de hello **Seleccionar disco toopartition** opciones y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Seleccione el disco de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="b5da5-177">**Paso 17:** seleccione **Sí** toowrite Hola toodisk de cambios y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Escribir Hola cambios toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="b5da5-179">**Paso 18:** seleccione la opción predeterminada de hello, seleccione **continuar**y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Seleccione la opción predeterminada de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="b5da5-181">**Paso 19:** seleccione Hola la opción adecuada para administrar las actualizaciones en el sistema y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Seleccione cómo se actualiza toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="b5da5-183">Porque el servidor de destino maestro de Azure Site Recovery Hola requiere una versión muy específica de hello Ubuntu, deberá tooensure ese kernel Hola se deshabilitan las actualizaciones para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="b5da5-184">Si están habilitadas, las actualizaciones normales provocar toomalfunction de servidor de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="b5da5-185">Asegúrese de seleccionar hello **ninguna actualización automática** opción.</span><span class="sxs-lookup"><span data-stu-id="b5da5-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="b5da5-186">**Paso 20:** seleccione las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="b5da5-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="b5da5-187">Si desea que openSSH para la conexión de SSH, seleccione hello **server OpenSSH** opción y, a continuación, seleccione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Selección de software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="b5da5-189">**Paso 21:** seleccione **Sí** y luego **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Cargador de arranque GRUB Hola de instalación](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="b5da5-191">**Paso 22:** seleccione Hola dispositivo adecuado para la instalación de cargador de arranque de hello (preferiblemente **/dev/sda**) y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selección de un dispositivo para la instalación del cargador de arranque](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="b5da5-193">**Paso 23:** seleccione **continuar**y, a continuación, seleccione **ENTRAR** instalación de hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="b5da5-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Finalizar la instalación de Hola](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="b5da5-195">Cuando haya finalizado la instalación de hello, inicie sesión en toohello VM con las nuevas credenciales de usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="b5da5-196">(Consulte demasiado**paso 10** para obtener más información.)</span><span class="sxs-lookup"><span data-stu-id="b5da5-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="b5da5-197">Realice los pasos de Hola que se describen en la siguiente captura de pantalla tooset Hola raíz de hello contraseña de usuario.</span><span class="sxs-lookup"><span data-stu-id="b5da5-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="b5da5-198">Luego inicie sesión como usuario raíz.</span><span class="sxs-lookup"><span data-stu-id="b5da5-198">Then sign in as ROOT user.</span></span>

![Contraseña de usuario de conjunto Hola raíz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="b5da5-200">Preparar la máquina de hello para la configuración como un servidor de destino maestro</span><span class="sxs-lookup"><span data-stu-id="b5da5-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="b5da5-201">A continuación, prepare máquina de hello para la configuración como un servidor de destino maestro.</span><span class="sxs-lookup"><span data-stu-id="b5da5-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="b5da5-202">Id. de hello tooget para cada disco duro de SCSI en una máquina virtual de Linux, habilitar hello **disco. EnableUUID = TRUE** parámetro.</span><span class="sxs-lookup"><span data-stu-id="b5da5-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="b5da5-203">tooenable este parámetro, Hola toman siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="b5da5-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="b5da5-204">Apague la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b5da5-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="b5da5-205">Haga clic en la entrada de hello para la máquina virtual de hello en el panel izquierdo de Hola y, a continuación, seleccione **modificar configuración**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="b5da5-206">Seleccione hello **opciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="b5da5-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="b5da5-207">En el panel izquierdo de hello, seleccione **avanzadas** > **General**y, a continuación, seleccione hello **parámetros de configuración** botón en la parte inferior derecha de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="b5da5-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Pestaña de opciones](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="b5da5-209">Hola **parámetros de configuración** opción no está disponible cuando se está ejecutando la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="b5da5-210">toomake esta ficha activa, apagar la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="b5da5-211">Vea si ya existe una fila con **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="b5da5-212">Si el valor de hello existe y está establecido demasiado**False**, cambie el valor de hello demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="b5da5-213">(los valores de hello no distinguen mayúsculas de minúsculas).</span><span class="sxs-lookup"><span data-stu-id="b5da5-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="b5da5-214">Si el valor de hello existe y está establecido demasiado**True**, seleccione **cancelar**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="b5da5-215">Si no existe el valor de hello, seleccione **Agregar fila**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="b5da5-216">En la columna de nombre de hello, agregue **disco. EnableUUID**y, a continuación, establezca el valor de hello demasiado**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Comprobación de si el disk.EnableUUID existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="b5da5-218">Deshabilitación de actualizaciones de kernel</span><span class="sxs-lookup"><span data-stu-id="b5da5-218">Disable kernel upgrades</span></span>

<span data-ttu-id="b5da5-219">Servidor de destino maestro de Azure Site Recovery requiere una versión muy específica de hello Ubuntu, asegúrese de que las actualizaciones de kernel Hola están deshabilitadas para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="b5da5-220">Si están habilitadas las actualizaciones de kernel, las actualizaciones normales provocar toomalfunction de servidor de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="b5da5-221">Descarga e instalación de paquetes adicionales</span><span class="sxs-lookup"><span data-stu-id="b5da5-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="b5da5-222">Asegúrese de que tiene toodownload de conectividad de Internet e instale paquetes adicionales.</span><span class="sxs-lookup"><span data-stu-id="b5da5-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="b5da5-223">Si no tiene conectividad a Internet, necesita toomanually encontrar estos paquetes RPM e instalarlas.</span><span class="sxs-lookup"><span data-stu-id="b5da5-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="b5da5-224">Obtener el instalador de hello para el programa de instalación</span><span class="sxs-lookup"><span data-stu-id="b5da5-224">Get hello installer for setup</span></span>

<span data-ttu-id="b5da5-225">Si el destino maestro tiene conectividad a Internet, puede usar Hola después de instalador de pasos toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="b5da5-226">En caso contrario, puede copiar a instalador Hola Hola servidor de procesos y, a continuación, vuelva a instalarlo.</span><span class="sxs-lookup"><span data-stu-id="b5da5-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="b5da5-227">Descargar los paquetes de instalación de destino maestro Hola</span><span class="sxs-lookup"><span data-stu-id="b5da5-227">Download hello master target installation packages</span></span>

<span data-ttu-id="b5da5-228">[Descargar los bits de instalación de Linux más recientes de hello destino maestro](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="b5da5-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="b5da5-229">toodownload mediante Linux, tipo:</span><span class="sxs-lookup"><span data-stu-id="b5da5-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="b5da5-230">Asegúrese de que se descargue y descomprima al instalador de hello en su directorio particular.</span><span class="sxs-lookup"><span data-stu-id="b5da5-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="b5da5-231">Si se descomprimen demasiado**/usr/Local**, a continuación, se produce un error en la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="b5da5-232">Instalador de Access Hola Hola del servidor de procesos</span><span class="sxs-lookup"><span data-stu-id="b5da5-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="b5da5-233">En el servidor de procesos de Hola y vaya demasiado**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="b5da5-234">Copie el archivo de instalador necesarios de Hola Hola servidor de procesos y guárdelo como **latestlinuxmobsvc.tar.gz** en su directorio particular.</span><span class="sxs-lookup"><span data-stu-id="b5da5-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="b5da5-235">Aplicación de cambios en la configuración personalizada</span><span class="sxs-lookup"><span data-stu-id="b5da5-235">Apply custom configuration changes</span></span>

<span data-ttu-id="b5da5-236">cambios de configuración personalizada de tooapply, usar hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b5da5-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="b5da5-237">Ejecute hello después binario de comando toountar Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de pantalla de hello comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="b5da5-239">Siguiente ejecución Hola comando toogive permiso.</span><span class="sxs-lookup"><span data-stu-id="b5da5-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="b5da5-240">Ejecute hello sigue la secuencia de comandos toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="b5da5-241">Ejecutar script de Hola solo una vez en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="b5da5-242">Apague el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-242">Shut down hello server.</span></span> <span data-ttu-id="b5da5-243">A continuación, reinicie servidor hello después de agregar un disco, como se describe en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="b5da5-244">Agregar una máquina virtual del destino maestro de Linux de retención disco toohello</span><span class="sxs-lookup"><span data-stu-id="b5da5-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="b5da5-245">Usar hello siguiendo los pasos toocreate un disco de retención:</span><span class="sxs-lookup"><span data-stu-id="b5da5-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="b5da5-246">Adjuntar una nueva máquina de virtual de disco de 1 TB toohello Linux destino maestro y, a continuación, inicie el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="b5da5-247">Hola de uso **comando multipath -ll** identificador de comando toolearn Hola múltiples rutas de acceso del disco de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Id. de múltiples rutas de Hello del disco de retención de Hola](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="b5da5-249">Formatear la unidad de hello y, a continuación, cree un sistema de archivos en la nueva unidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Crear un sistema de archivos en la unidad de Hola](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="b5da5-251">Después de crear el sistema de archivos de hello, montar el disco de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retención de Hola de montaje](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="b5da5-253">Crear hello **fstab** unidad de retención de Hola de entrada toomount cada vez que inicia el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="b5da5-254">Seleccione **insertar** toobegin Editar archivo hello.</span><span class="sxs-lookup"><span data-stu-id="b5da5-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="b5da5-255">Crear una nueva línea y, a continuación, insertar Hola después de texto.</span><span class="sxs-lookup"><span data-stu-id="b5da5-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="b5da5-256">Editar Hola disco identificador múltiples rutas de acceso basado en Id. de múltiples rutas de hello resaltado del comando anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="b5da5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="b5da5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="b5da5-258">Seleccione **Esc**y, a continuación, escriba **: wq** (escribir y salir) ventana del editor tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="b5da5-259">Instalar el destino maestro Hola</span><span class="sxs-lookup"><span data-stu-id="b5da5-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5da5-260">versión de Hola Hola maestra del servidor de destino debe ser anterior a las versiones de servidor de procesos de Hola y el servidor de configuración de Hola Hola tooor igual.</span><span class="sxs-lookup"><span data-stu-id="b5da5-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="b5da5-261">Si no se cumple esta condición, la reprotección se realiza correctamente, pero se produce un error en la replicación.</span><span class="sxs-lookup"><span data-stu-id="b5da5-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="b5da5-262">Antes de instalar el servidor de destino maestro de hello, compruebe que hello **/etcetera/hosts** archivo en la máquina virtual de hello contiene entradas que se asignan direcciones IP de toohello de nombre de host local de Hola que están asociadas con todos los adaptadores de red.</span><span class="sxs-lookup"><span data-stu-id="b5da5-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="b5da5-263">Copie la frase de contraseña de Hola de **C:\ProgramData\Microsoft Azure sitio Recovery\private\connection.passphrase** en el servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="b5da5-264">A continuación, guárdelo como **passphrase.txt** Hola mismo directorio local mediante la ejecución de Hola el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b5da5-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="b5da5-265">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b5da5-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="b5da5-266">Anote la dirección IP del servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="b5da5-267">Se necesitará en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="b5da5-268">Ejecute hello siguiente servidor de destino maestro de comando tooinstall hello y registre el servidor de hello con servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="b5da5-269">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b5da5-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="b5da5-270">Espere a que finalice el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-270">Wait until hello script finishes.</span></span> <span data-ttu-id="b5da5-271">Si el destino maestro Hola registra correctamente, destino maestro Hola aparece en hello **infraestructura del sitio de recuperación** página del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="b5da5-272">Instalar el destino maestro hello mediante la instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="b5da5-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="b5da5-273">Ejecute hello siguiendo el destino maestros del comando tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="b5da5-274">Para el rol de agente de hello, elija **destino maestro**.</span><span class="sxs-lookup"><span data-stu-id="b5da5-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="b5da5-275">Elegir ubicación predeterminada de hello para la instalación y, a continuación, seleccione **ENTRAR** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b5da5-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Elección de una ubicación predeterminada para la instalación del destino maestro](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="b5da5-277">Cuando haya finalizado la instalación de hello, registrar el servidor de configuración de hello mediante el uso de la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="b5da5-278">Anote la dirección IP de Hola Hola del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="b5da5-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="b5da5-279">Se necesitará en el paso siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="b5da5-280">Ejecute hello siguiente servidor de destino maestro de comando tooinstall hello y registre el servidor de hello con servidor de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="b5da5-281">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b5da5-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="b5da5-282">Espere a que finalice el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-282">Wait until hello script finishes.</span></span> <span data-ttu-id="b5da5-283">Si el destino maestro de hello está registrado correctamente, destino maestro Hola aparece en hello **infraestructura del sitio de recuperación** página del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="b5da5-284">Actualizar el destino maestro Hola</span><span class="sxs-lookup"><span data-stu-id="b5da5-284">Upgrade hello master target</span></span>

<span data-ttu-id="b5da5-285">Ejecute al instalador de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-285">Run hello installer.</span></span> <span data-ttu-id="b5da5-286">Detecta automáticamente que ese agente Hola está instalado en el destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="b5da5-287">tooupgrade, seleccione **Y**.  Una vez completado el programa de instalación de hello, comprobar la versión de Hola de destino maestro Hola instalado mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="b5da5-288">Puede ver que hello **versión** campo proporciona el número de versión de Hola de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="b5da5-289">Instalar las herramientas de VMware en el servidor de destino maestro Hola</span><span class="sxs-lookup"><span data-stu-id="b5da5-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="b5da5-290">Debe tooinstall las herramientas de VMware en el destino maestro de Hola para que puedan detectar Hola almacenes de datos.</span><span class="sxs-lookup"><span data-stu-id="b5da5-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="b5da5-291">Si no se instalan herramientas de hello, pantalla de bienvenida reprotección no aparece en los almacenes de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="b5da5-292">Tras la instalación de las herramientas de VMware hello, deberá toorestart.</span><span class="sxs-lookup"><span data-stu-id="b5da5-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5da5-293">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b5da5-293">Next steps</span></span>
<span data-ttu-id="b5da5-294">Después de instalación de Hola y el registro de destino maestro hello tiene finsihed, puede ver destino maestro Hola aparecen en hello **destino maestro** sección **infraestructura del sitio de recuperación**, bajo Hola información general del servidor de configuración.</span><span class="sxs-lookup"><span data-stu-id="b5da5-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="b5da5-295">Ahora ya puede continuar con la [reprotección](site-recovery-how-to-reprotect.md), seguido de la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5da5-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="b5da5-296">Problemas comunes</span><span class="sxs-lookup"><span data-stu-id="b5da5-296">Common issues</span></span>

* <span data-ttu-id="b5da5-297">Asegúrese de no activar Storage vMotion en ningún componente de administración como, por ejemplo, un destino maestro.</span><span class="sxs-lookup"><span data-stu-id="b5da5-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="b5da5-298">Si se mueve destino maestro Hola después un reprotección correcta, no se puede desasociar discos de máquina virtual de hello (VMDK).</span><span class="sxs-lookup"><span data-stu-id="b5da5-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="b5da5-299">En este caso se produce un error en la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5da5-299">In this case, failback fails.</span></span>

* <span data-ttu-id="b5da5-300">destino maestro Hello no debería tener todas las instantáneas de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="b5da5-301">Si hay instantáneas, se produce un error en la conmutación por recuperación.</span><span class="sxs-lookup"><span data-stu-id="b5da5-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="b5da5-302">Debido a la configuración de la NIC de personalizada de toosome en algunos clientes, está deshabilitada de interfaz de red de Hola durante el inicio y no se puede inicializar el agente de destino maestro Hola.</span><span class="sxs-lookup"><span data-stu-id="b5da5-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="b5da5-303">Asegúrese de que ese Hola propiedades siguientes se han definido correctamente.</span><span class="sxs-lookup"><span data-stu-id="b5da5-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="b5da5-304">Comprobar /etc/sysconfig/network-scripts/ifcfg del archivo de tarjeta de estas propiedades en hello Ethernet-eth *.</span><span class="sxs-lookup"><span data-stu-id="b5da5-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="b5da5-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="b5da5-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="b5da5-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="b5da5-306">ONBOOT=yes</span></span>
