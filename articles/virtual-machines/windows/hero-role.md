---
title: aaaInstall IIS en su primera VM de Windows | Documentos de Microsoft
description: "Experimentar con la primera máquina virtual de Windows mediante la instalación de IIS y abrir el puerto 80 mediante Hola portal de Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="cfda4-103">Experimentación con la instalación de un rol en la máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="cfda4-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="cfda4-104">Una vez que la máquina virtual (VM) la primera y en ejecución, puede mover en tooinstalling software y los servicios.</span><span class="sxs-lookup"><span data-stu-id="cfda4-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="cfda4-105">Para este tutorial, vamos toouse administrador del servidor en VM de Windows Server de hello tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="cfda4-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="cfda4-106">A continuación, se creará un grupo de seguridad de red (NSG) mediante el puerto 80 tooIIS tráfico de hello tooopen de portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cfda4-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="cfda4-107">Si aún no ha creado su primera máquina virtual, debe volver atrás demasiado[crear la primera máquina virtual de Windows en el portal de Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar con este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfda4-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="cfda4-108">Asegúrese de Hola que está ejecutando la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cfda4-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="cfda4-109">Abra hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfda4-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cfda4-110">En el menú del concentrador hello, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="cfda4-111">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="cfda4-112">Si el estado de hello es **detenido (desasignado)**, haga clic en hello **iniciar** botón en hello **Essentials** hoja de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="cfda4-113">Si el estado de hello es **ejecuta**, puede mover en toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="cfda4-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="cfda4-114">Conectar máquina virtual de toohello e inicie sesión en</span><span class="sxs-lookup"><span data-stu-id="cfda4-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="cfda4-115">En el menú del concentrador hello, haga clic en **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="cfda4-116">Seleccione la máquina virtual de Hola de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="cfda4-117">En la hoja de hello para la máquina virtual de hello, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="cfda4-118">Esto crea y descarga un archivo de protocolo de escritorio remoto (archivo .rdp) que es similar a una máquina de tooyour tooconnect de método abreviado.</span><span class="sxs-lookup"><span data-stu-id="cfda4-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="cfda4-119">Podría desea toosave Hola archivo tooyour escritorio para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="cfda4-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="cfda4-120">**Abra** esta tooyour de tooconnect archivo máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Captura de pantalla de hello Azure portal que se muestra cómo tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="cfda4-122">Obtendrá una advertencia que .rdp hello es de un publicador desconocido.</span><span class="sxs-lookup"><span data-stu-id="cfda4-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="cfda4-123">Esto es normal.</span><span class="sxs-lookup"><span data-stu-id="cfda4-123">This is normal.</span></span> <span data-ttu-id="cfda4-124">En la ventana de escritorio remoto de hello, haga clic en **conectar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="cfda4-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Captura de pantalla de una advertencia sobre un editor desconocido](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="cfda4-126">En la ventana de la seguridad de Windows hello, el nombre de usuario de tipo hello y la contraseña de cuenta local de Hola que creó al crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="cfda4-127">se ha introducido el nombre de usuario de Hello *vmname*&#92; *nombre de usuario*, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Captura de pantalla de escribir el nombre de la máquina virtual de hello, nombre de usuario y contraseña](./media/hero-role/credentials.png)
5. <span data-ttu-id="cfda4-129">Obtendrá una advertencia no se puede comprobar que el certificado Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="cfda4-130">Esto es normal.</span><span class="sxs-lookup"><span data-stu-id="cfda4-130">This is normal.</span></span> <span data-ttu-id="cfda4-131">Haga clic en **Sí** tooverify Hola identidad de máquina virtual de Hola y finalizar la sesión.</span><span class="sxs-lookup"><span data-stu-id="cfda4-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Captura de pantalla muestra un mensaje acerca de la verificación de identidad de Hola de hello VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="cfda4-133">Si se ejecuta en tootrouble cuando intente tooconnect, consulte [tooa de conexiones de escritorio remoto solucionar problemas de máquina Virtual de Azure basado en Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cfda4-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="cfda4-134">Instalación de IIS en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cfda4-134">Install IIS on your VM</span></span>
<span data-ttu-id="cfda4-135">Ahora que ha iniciado sesión toohello VM, se instalará un rol de servidor para que pueda experimentar más.</span><span class="sxs-lookup"><span data-stu-id="cfda4-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="cfda4-136">Abra el **Administrador del servidor** si aún no está abierto.</span><span class="sxs-lookup"><span data-stu-id="cfda4-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="cfda4-137">Haga clic en hello **iniciar** menú y, a continuación, haga clic en **el administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="cfda4-138">En **el administrador del servidor**, seleccione **servidor Local** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="cfda4-139">En el menú de hello, seleccione **administrar** > **agregar Roles y características**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="cfda4-140">En Administrador de hello agregar Roles y características, en hello **tipo de instalación** página, elija **instalación basada en roles o basada en características**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Pestaña captura de pantalla que muestra hello Agregar administrador de Roles y características de tipo de instalación](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="cfda4-142">Seleccione Hola VM Hola grupo de servidores y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="cfda4-143">En hello **Roles de servidor** página, seleccione **servidor Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Pestaña captura de pantalla que muestra hello agregar Roles y características Asistente para Roles de servidor](./media/hero-role/add-iis.png)
7. <span data-ttu-id="cfda4-145">Hola emergente acerca de cómo agregar características necesarias para IIS, asegúrese de que **incluir herramientas de administración** está seleccionada y, a continuación, haga clic en **agregar características**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="cfda4-146">Cuando se cierra Hola emergente, haga clic en **siguiente** Asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Captura de pantalla muestra tooconfirm emergente Agregar rol IIS de Hola](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="cfda4-148">En la página de características de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="cfda4-149">En hello **rol de servidor Web (IIS)** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="cfda4-150">En hello **servicios de rol** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="cfda4-151">En hello **confirmación** página, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="cfda4-152">Una vez completada la instalación de hello, haga clic en **cerrar** Asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="cfda4-153">Apertura del puerto 80</span><span class="sxs-lookup"><span data-stu-id="cfda4-153">Open port 80</span></span>
<span data-ttu-id="cfda4-154">En orden para la máquina virtual tooaccept el tráfico entrante en el puerto 80, deberá tooadd un grupo de seguridad de red de toohello de regla de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfda4-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="cfda4-155">Abra hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfda4-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cfda4-156">En **máquinas virtuales** seleccione Hola máquina virtual que ha creado.</span><span class="sxs-lookup"><span data-stu-id="cfda4-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="cfda4-157">En configuración de máquinas virtuales de hello, seleccione **interfaces de red** y, a continuación, seleccione Hola interfaz de red existente.</span><span class="sxs-lookup"><span data-stu-id="cfda4-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Captura de pantalla muestra a la configuración de máquina virtual de Hola para hello interfaces de red](./media/hero-role/network-interface.png)
4. <span data-ttu-id="cfda4-159">En **Essentials** de interfaz de red de hello, haga clic en hello **grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Captura de pantalla muestra la sección de Essentials Hola de interfaz de red de Hola](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="cfda4-161">Hola **Essentials** hoja para hello NSG, debe tener un valor predeterminado existente regla de entrada de **rdp permitir predeterminado** que permite toolog en toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="cfda4-162">Va a agregar otro tráfico IIS de tooallow de regla de entrada.</span><span class="sxs-lookup"><span data-stu-id="cfda4-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="cfda4-163">Haga clic en **Regla de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-163">Click **Inbound security rule**.</span></span>
   
    ![Captura de pantalla muestra la sección de Essentials de Hola para hello NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="cfda4-165">En **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Captura de pantalla muestra hello botón tooadd una regla de seguridad](./media/hero-role/add-rule.png)
7. <span data-ttu-id="cfda4-167">En **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="cfda4-168">Tipo de **80** en Hola intervalo de puertos y asegúrese de que **permitir** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="cfda4-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="cfda4-169">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-169">When you are done, click **OK**.</span></span>
   
    ![Captura de pantalla muestra hello botón tooadd una regla de seguridad](./media/hero-role/port-80.png)

<span data-ttu-id="cfda4-171">Para obtener más información acerca de los NSG, las reglas entrantes y salientes, vea [permitir acceso externo tooyour VM con Hola portal de Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="cfda4-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="cfda4-172">Conectar el sitio Web IIS de toohello predeterminado</span><span class="sxs-lookup"><span data-stu-id="cfda4-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="cfda4-173">Hola portal de Azure, haga clic en **máquinas virtuales** y, a continuación, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="cfda4-174">Hola **Essentials** hoja, copie su **dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="cfda4-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Captura de pantalla muestra donde toofind Hola dirección IP pública de la máquina virtual](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="cfda4-176">Abra un explorador y en la barra de direcciones de hello, escriba la dirección IP pública similar al siguiente: http://<publicIPaddress> y haga clic en **ENTRAR** toogo toothat dirección.</span><span class="sxs-lookup"><span data-stu-id="cfda4-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="cfda4-177">El explorador debe abrir la página de web IIS predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="cfda4-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="cfda4-178">Se parece a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cfda4-178">It looks something like this:</span></span>
   
    ![Captura de pantalla muestra qué página IIS predeterminada Hola aspecto en un explorador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="cfda4-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cfda4-180">Next steps</span></span>
* <span data-ttu-id="cfda4-181">También puede experimentar con [adjuntar un disco de datos](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cfda4-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="cfda4-182">Los discos de datos proporcionan más espacio de almacenamiento para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cfda4-182">Data disks provide more storage for your virtual machine.</span></span>

