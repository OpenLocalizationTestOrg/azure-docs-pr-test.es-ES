---
title: "Instalación de IIS en la primera máquina virtual Windows | Microsoft Docs"
description: "Experimente con la primera máquina virtual de Windows al instalar IIS y abrir el puerto 80 mediante Azure Portal."
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
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="d01ac-103">Experimentación con la instalación de un rol en la máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="d01ac-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="d01ac-104">Con la primera máquina virtual activa y en funcionamiento, puede pasar a instalar el software y los servicios.</span><span class="sxs-lookup"><span data-stu-id="d01ac-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="d01ac-105">Para este tutorial, vamos a utilizar el administrador del servidor en la máquina virtual de Windows Server para instalar IIS.</span><span class="sxs-lookup"><span data-stu-id="d01ac-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="d01ac-106">A continuación, se crea un grupo de seguridad de red (NSG) mediante Azure Portal para abrir el puerto 80 al tráfico IIS.</span><span class="sxs-lookup"><span data-stu-id="d01ac-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="d01ac-107">Si aún no ha creado su primera máquina virtual, debe volver a [Creación de la primera máquina virtual Windows en Azure Portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar con este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d01ac-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="d01ac-108">Asegúrese de que está ejecutando la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d01ac-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="d01ac-109">Abra el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d01ac-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d01ac-110">En el menú central, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="d01ac-111">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="d01ac-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="d01ac-112">Si el estado es **Detenido (desasignado)**, haga clic en el botón **Iniciar** de la hoja **Essentials** (Información básica) de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="d01ac-113">Si el estado es **En ejecución**, puede continuar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="d01ac-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="d01ac-114">Conexión a la máquina virtual e inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="d01ac-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="d01ac-115">En el menú central, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="d01ac-116">Seleccione la máquina virtual en la lista.</span><span class="sxs-lookup"><span data-stu-id="d01ac-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="d01ac-117">En la hoja de la máquina virtual, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="d01ac-118">Así se crea y se descarga un archivo de protocolo de escritorio remoto (archivo.rdp), que es como un acceso directo de conexión a la máquina.</span><span class="sxs-lookup"><span data-stu-id="d01ac-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="d01ac-119">Puede guardar el archivo en el escritorio para facilitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="d01ac-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="d01ac-120">**Abra** este archivo para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-120">**Open** this file to connect to your VM.</span></span>
   
    ![Captura de pantalla del portal de Azure que muestra cómo conectarse a la máquina virtual](./media/hero-role/connect.png)
3. <span data-ttu-id="d01ac-122">Aparece una advertencia que indica que el archivo .rdp procede de un editor desconocido.</span><span class="sxs-lookup"><span data-stu-id="d01ac-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="d01ac-123">Esto es normal.</span><span class="sxs-lookup"><span data-stu-id="d01ac-123">This is normal.</span></span> <span data-ttu-id="d01ac-124">En la ventana de Escritorio remoto, haga clic en **Conectar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="d01ac-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Captura de pantalla de una advertencia sobre un editor desconocido](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="d01ac-126">En la ventana de seguridad de Windows, escriba el nombre de usuario y la contraseña de la cuenta local que generó al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="d01ac-127">El nombre de usuario se escribe como *nombreDeMáquinaVirtual*&#92;*nombreDeUsuario*; después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Captura de pantalla de la escritura del nombre de la máquina virtual, el nombre de usuario y la contraseña](./media/hero-role/credentials.png)
5. <span data-ttu-id="d01ac-129">Aparece una advertencia que indica que no se puede comprobar el certificado.</span><span class="sxs-lookup"><span data-stu-id="d01ac-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="d01ac-130">Esto es normal.</span><span class="sxs-lookup"><span data-stu-id="d01ac-130">This is normal.</span></span> <span data-ttu-id="d01ac-131">Haga clic en **Sí** para comprobar la identidad de la máquina virtual y finalizar el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="d01ac-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Captura de pantalla que muestra un mensaje sobre la comprobación de la identidad de la máquina virtual](./media/hero-role/cert-warning.png)

<span data-ttu-id="d01ac-133">Si surgen problemas al intentar conectarse, consulte [Solución de problemas de conexiones del Escritorio remoto a una máquina virtual de Azure con Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d01ac-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="d01ac-134">Instalación de IIS en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d01ac-134">Install IIS on your VM</span></span>
<span data-ttu-id="d01ac-135">Ahora que ha iniciado sesión en la máquina virtual, se instalará un rol de servidor para que pueda realizar más experimentos.</span><span class="sxs-lookup"><span data-stu-id="d01ac-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="d01ac-136">Abra el **Administrador del servidor** si aún no está abierto.</span><span class="sxs-lookup"><span data-stu-id="d01ac-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="d01ac-137">Haga clic en el menú **Inicio** y en **Administrador del servidor**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="d01ac-138">En **Administrador del servidor**, seleccione **Servidor local** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="d01ac-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="d01ac-139">En el menú, seleccione **Administrar** > **Agregar roles y características**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="d01ac-140">En el Asistente para agregar roles y características, en la página **Tipo de instalación**, elija **Instalación basada en características o en roles** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Captura de pantalla que muestra la pestaña del Asistente para agregar roles y características para Tipo de instalación](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="d01ac-142">Seleccione la máquina virtual del grupo de servidores y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="d01ac-143">En la página **Roles de servidor**, seleccione **Servidor web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Captura de pantalla que muestra la pestaña del Asistente para agregar roles y características para Roles de servidor](./media/hero-role/add-iis.png)
7. <span data-ttu-id="d01ac-145">En el menú emergente acerca de cómo agregar características necesarias para IIS, asegúrese de que la opción **Incluir herramientas de administración** está seleccionada y, a continuación, haga clic en **Agregar características**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="d01ac-146">Cuando se cierre el elemento emergente, haga clic en **Siguiente** en el asistente.</span><span class="sxs-lookup"><span data-stu-id="d01ac-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Captura de pantalla que muestra un elemento emergente para confirmar la adición del rol de IIS](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="d01ac-148">En la página de características, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="d01ac-149">En la página **Rol de servidor web (IIS)**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="d01ac-150">En la página **Servicios de rol**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="d01ac-151">En la página **Confirmación**, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="d01ac-152">Una vez completada la instalación, haga clic en **Cerrar** en el asistente.</span><span class="sxs-lookup"><span data-stu-id="d01ac-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="d01ac-153">Apertura del puerto 80</span><span class="sxs-lookup"><span data-stu-id="d01ac-153">Open port 80</span></span>
<span data-ttu-id="d01ac-154">Para que la máquina virtual acepte tráfico entrante en el puerto 80, debe agregar una regla de entrada al grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="d01ac-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="d01ac-155">Abra el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d01ac-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d01ac-156">En **Máquinas virtuales** , seleccione la máquina virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="d01ac-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="d01ac-157">En la configuración de las máquinas virtuales, seleccione **Interfaces de red** y la interfaz de red existente.</span><span class="sxs-lookup"><span data-stu-id="d01ac-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Captura de pantalla que muestra la configuración de máquina virtual para las interfaces de red](./media/hero-role/network-interface.png)
4. <span data-ttu-id="d01ac-159">En **Essentials** (Información básica) de la interfaz de red, haga clic en el **grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Captura de pantalla que muestra la sección Essentials para la interfaz de red](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="d01ac-161">En la hoja **Essentials** (Información básica) del NSG, debe tener una regla de entrada predeterminada existente para **default-allow-rdp** que le permita iniciar sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="d01ac-162">Ahora, va a agregar otra regla de entrada para permitir el tráfico IIS.</span><span class="sxs-lookup"><span data-stu-id="d01ac-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="d01ac-163">Haga clic en **Regla de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-163">Click **Inbound security rule**.</span></span>
   
    ![Captura de pantalla que muestra la sección Essentials para el NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="d01ac-165">En **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Captura de pantalla que muestra el botón para agregar una regla de seguridad](./media/hero-role/add-rule.png)
7. <span data-ttu-id="d01ac-167">En **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="d01ac-168">Escriba **80** en el intervalo de puertos y asegúrese de que la opción **Permitir** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="d01ac-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="d01ac-169">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-169">When you are done, click **OK**.</span></span>
   
    ![Captura de pantalla que muestra el botón para agregar una regla de seguridad](./media/hero-role/port-80.png)

<span data-ttu-id="d01ac-171">Para más información sobre los NSG y las reglas de entrada y de salida, consulte [Permitir el acceso externo a la máquina virtual mediante Azure Portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d01ac-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="d01ac-172">Conexión al sitio web predeterminado de IIS</span><span class="sxs-lookup"><span data-stu-id="d01ac-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="d01ac-173">En el Portal de Azure, haga clic en **Máquinas virtuales** y, luego, seleccione la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="d01ac-174">En la hoja **Essentials** (Información básica), copie su **dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="d01ac-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Captura de pantalla que muestra dónde encontrar la dirección IP pública de la máquina virtual](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="d01ac-176">Abra un explorador y, en la barra de direcciones, escriba la dirección IP pública así: http://<publicIPaddress> y haga clic en **Entrar** para ir a esa dirección.</span><span class="sxs-lookup"><span data-stu-id="d01ac-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="d01ac-177">El explorador debe abrir la página web IIS predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d01ac-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="d01ac-178">Se parece a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d01ac-178">It looks something like this:</span></span>
   
    ![Captura de pantalla que muestra el aspecto de la página predeterminada de IIS en un explorador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="d01ac-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d01ac-180">Next steps</span></span>
* <span data-ttu-id="d01ac-181">También puede probar a [conectar un disco de datos](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="d01ac-182">Los discos de datos proporcionan más espacio de almacenamiento para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d01ac-182">Data disks provide more storage for your virtual machine.</span></span>

