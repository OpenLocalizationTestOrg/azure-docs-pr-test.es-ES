---
title: "Azure Active Directory Domain Services: Unión de una máquina virtual de Red Hat Enterprise Linux a un dominio administrado | Microsoft Docs"
description: "Unión de una máquina virtual Red Hat Enterprise Linux a un dominio administrado de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="fe90f-103">Unión de una máquina virtual de Red Hat Enterprise Linux 7 a un dominio administrado</span><span class="sxs-lookup"><span data-stu-id="fe90f-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="fe90f-104">Este artículo muestra cómo unir una máquina virtual de Red Hat Enterprise Linux (RHEL) 7 a un dominio administrado con Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe90f-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="fe90f-105">Aprovisionamiento de una máquina virtual de Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="fe90f-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="fe90f-106">Realice los pasos siguientes para aprovisionar una máquina virtual de RHEL 7 mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe90f-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="fe90f-107">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fe90f-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Panel de Portal de Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="fe90f-109">Haga clic en **Nuevo** en el panel izquierdo y escriba **Red Hat** en la barra de búsqueda, como se muestra en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="fe90f-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="fe90f-110">Las entradas para Red Hat Enterprise Linux en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="fe90f-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="fe90f-111">Haga clic en **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="fe90f-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="fe90f-113">En los resultados de búsqueda del panel **Todo** se debe mostrar la imagen de Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="fe90f-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="fe90f-114">Haga clic en **Red Hat Enterprise Linux 7.2** para obtener más información sobre la imagen de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="fe90f-116">En el panel **Red Hat Enterprise Linux 7.2** debería ver más información sobre la imagen de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="fe90f-117">En el menú desplegable **Seleccionar un modelo de implementación**, seleccione **Clásico**.</span><span class="sxs-lookup"><span data-stu-id="fe90f-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="fe90f-118">Después, haga clic en el botón **Crear** .</span><span class="sxs-lookup"><span data-stu-id="fe90f-118">Then click the **Create** button.</span></span>

    ![Ver detalles de la imagen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="fe90f-120">En la página **Aspectos básicos** del Asistente para **crear máquina virtual**, escriba el **nombre de host** para la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="fe90f-121">Especifique también un nombre de usuario de administrador local en el campo **Nombre de usuario** y una **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fe90f-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="fe90f-122">También puede decidir utilizar una clave SSH para autenticar al usuario de administrador local.</span><span class="sxs-lookup"><span data-stu-id="fe90f-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="fe90f-123">Seleccione también un **Plan de tarifa** para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Crear máquina virtual: página de aspectos básicos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="fe90f-125">En la página **Tamaño** del Asistente para **crear máquina virtual**, seleccione el tamaño de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Crear máquina virtual: seleccionar tamaño](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="fe90f-127">En la página **Configuración** del Asistente para **crear máquina virtual**, seleccione la cuenta de almacenamiento para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="fe90f-128">Haga clic en **Red virtual** para seleccionar la red virtual en la que se debe implementar la máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="fe90f-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="fe90f-129">En la hoja **Red virtual**, seleccione la red virtual en la que Azure AD Domain Services estará disponible.</span><span class="sxs-lookup"><span data-stu-id="fe90f-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="fe90f-130">En este ejemplo, se ha elegido la red virtual "MyPreviewVNet".</span><span class="sxs-lookup"><span data-stu-id="fe90f-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Crear máquina virtual: seleccionar la red virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="fe90f-132">En la página **Resumen** del Asistente para **crear máquina virtual**, revise y haga clic en el botón **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fe90f-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Crear máquina virtual: red virtual seleccionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="fe90f-134">Debe comenzar la implementación de la nueva máquina virtual basada en la imagen de RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="fe90f-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Crear máquina virtual: implementación iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="fe90f-136">Después de unos minutos, la máquina virtual se debe implementar correctamente y estar lista para su uso.</span><span class="sxs-lookup"><span data-stu-id="fe90f-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Crear máquina virtual: implementado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="fe90f-138">Conexión remota a la máquina virtual de Linux recién aprovisionada</span><span class="sxs-lookup"><span data-stu-id="fe90f-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="fe90f-139">Se ha aprovisionado la máquina virtual de RHEL 7.2 en Azure.</span><span class="sxs-lookup"><span data-stu-id="fe90f-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="fe90f-140">La siguiente tarea es conectarse de forma remota a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="fe90f-141">**Conectarse a la máquina virtual de RHEL 7.2** Siga las instrucciones del artículo [Inicio de sesión en una máquina virtual con Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe90f-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="fe90f-142">En el resto de los pasos se supone que usa el cliente de SSH PuTTY para conectarse a la máquina virtual de RHEL.</span><span class="sxs-lookup"><span data-stu-id="fe90f-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="fe90f-143">Para más información, consulte la página [PuTTY Download Page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)(Página de descarga de PuTTY).</span><span class="sxs-lookup"><span data-stu-id="fe90f-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="fe90f-144">Abra el programa PuTTY.</span><span class="sxs-lookup"><span data-stu-id="fe90f-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="fe90f-145">Escriba el **Nombre de host** para la máquina virtual de RHEL recién creada.</span><span class="sxs-lookup"><span data-stu-id="fe90f-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="fe90f-146">En este ejemplo, la máquina virtual tiene el nombre de host "contoso rhel.cloudapp .net".</span><span class="sxs-lookup"><span data-stu-id="fe90f-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="fe90f-147">Si no está seguro del nombre de host de su máquina virtual, consulte el panel de máquinas virtuales en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe90f-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![Conexión a PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="fe90f-149">Inicie sesión en la máquina virtual con las credenciales de administrador local que ha especificado al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="fe90f-150">En este ejemplo, se usa la cuenta de administrador local "mahesh".</span><span class="sxs-lookup"><span data-stu-id="fe90f-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![Inicio de sesión de PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="fe90f-152">Instalación de los paquetes necesarios en la máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="fe90f-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="fe90f-153">Después de conectarse a la máquina virtual, la siguiente tarea es instalar los paquetes necesarios para unir un dominio a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="fe90f-154">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="fe90f-154">Perform the following steps:</span></span>

1. <span data-ttu-id="fe90f-155">**Instale realmd** : el paquete realmd se utiliza para unirse a un dominio.</span><span class="sxs-lookup"><span data-stu-id="fe90f-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="fe90f-156">En el terminal PuTTY, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe90f-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="fe90f-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="fe90f-157">sudo yum install realmd</span></span>

    ![Instalar realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="fe90f-159">Después de unos minutos, el paquete realmd debe estar instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="fe90f-161">**Instale sssd** : el paquete realmd depende de SSSD para realizar las operaciones de unión al dominio.</span><span class="sxs-lookup"><span data-stu-id="fe90f-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="fe90f-162">En el terminal PuTTY, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe90f-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="fe90f-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="fe90f-163">sudo yum install sssd</span></span>

    ![Instalar sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="fe90f-165">Después de unos minutos, el paquete sssd debe estar instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="fe90f-167">**Instale Kerberos**: en el terminal PuTTY, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe90f-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="fe90f-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="fe90f-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalar kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="fe90f-170">Después de unos minutos, el paquete realmd debe estar instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe90f-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="fe90f-172">Unión de la máquina virtual de Linux al dominio administrado</span><span class="sxs-lookup"><span data-stu-id="fe90f-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="fe90f-173">Ahora que los paquetes necesarios están instalados en la máquina virtual de Linux, la siguiente tarea es unir la máquina virtual al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="fe90f-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="fe90f-174">Detecte el dominio administrado con Servicios de dominio de AAD.</span><span class="sxs-lookup"><span data-stu-id="fe90f-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="fe90f-175">En el terminal PuTTY, escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe90f-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="fe90f-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="fe90f-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="fe90f-178">Si **realm discover** no puede encontrar el dominio administrado, asegúrese de que se puede acceder al dominio desde la máquina virtual (pruebe con ping).</span><span class="sxs-lookup"><span data-stu-id="fe90f-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="fe90f-179">Asegúrese de que la máquina virtual se ha implementado realmente en la misma red virtual en la que el dominio administrado está disponible.</span><span class="sxs-lookup"><span data-stu-id="fe90f-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="fe90f-180">Inicialice kerberos.</span><span class="sxs-lookup"><span data-stu-id="fe90f-180">Initialize kerberos.</span></span> <span data-ttu-id="fe90f-181">En el terminal PuTTY, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe90f-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="fe90f-182">Asegúrese de especificar un usuario que pertenezca al grupo "Administradores del controlador de dominio de AAD".</span><span class="sxs-lookup"><span data-stu-id="fe90f-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="fe90f-183">Solo estos usuarios pueden unir equipos al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="fe90f-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="fe90f-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="fe90f-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="fe90f-186">Asegúrese de especificar el nombre de dominio en mayúsculas o kinit generará un error.</span><span class="sxs-lookup"><span data-stu-id="fe90f-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="fe90f-187">Una la máquina al dominio.</span><span class="sxs-lookup"><span data-stu-id="fe90f-187">Join the machine to the domain.</span></span> <span data-ttu-id="fe90f-188">En el terminal PuTTY, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe90f-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="fe90f-189">Especifique el mismo usuario que ha especificado el paso anterior ("kinit").</span><span class="sxs-lookup"><span data-stu-id="fe90f-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="fe90f-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="fe90f-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Unión a dominio kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="fe90f-192">Debe obtener un mensaje (Máquina inscrita correctamente en el dominio kerberos) cuando la máquina está unida correctamente al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="fe90f-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="fe90f-193">Verificación de la unión a un dominio</span><span class="sxs-lookup"><span data-stu-id="fe90f-193">Verify domain join</span></span>
<span data-ttu-id="fe90f-194">Puede verificar rápidamente si el equipo se ha unido correctamente al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="fe90f-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="fe90f-195">Conecte a la máquina virtual de RHEL recién unida al dominio con SSH y una cuenta de usuario del dominio y, después,compruebe si la cuenta de usuario se ha resuelto correctamente.</span><span class="sxs-lookup"><span data-stu-id="fe90f-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="fe90f-196">En el terminal PuTTY, escriba el comando siguiente para conectarse a la nueva máquina virtual de RHEL recién unida al dominio con SSH.</span><span class="sxs-lookup"><span data-stu-id="fe90f-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="fe90f-197">Use una cuenta de dominio que pertenezca al dominio administrado (por ejemplo, "bob@CONTOSO100.COM" en este caso).</span><span class="sxs-lookup"><span data-stu-id="fe90f-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="fe90f-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="fe90f-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="fe90f-199">En el terminal PuTTY, escriba el comando siguiente para ver si el directorio principal se ha inicializado correctamente.</span><span class="sxs-lookup"><span data-stu-id="fe90f-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="fe90f-200">pwd</span><span class="sxs-lookup"><span data-stu-id="fe90f-200">pwd</span></span>
3. <span data-ttu-id="fe90f-201">En el terminal PuTTY, escriba el comando siguiente para ver si los miembros del grupo se está resolviendo correctamente.</span><span class="sxs-lookup"><span data-stu-id="fe90f-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="fe90f-202">id</span><span class="sxs-lookup"><span data-stu-id="fe90f-202">id</span></span>

<span data-ttu-id="fe90f-203">Este es un ejemplo de los resultados de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="fe90f-203">A sample output of these commands follows:</span></span>

![Verificación de la unión a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="fe90f-205">Solución de problemas de unión al dominio</span><span class="sxs-lookup"><span data-stu-id="fe90f-205">Troubleshooting domain join</span></span>
<span data-ttu-id="fe90f-206">Consulte el artículo [Solución de problemas de unión al dominio](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) .</span><span class="sxs-lookup"><span data-stu-id="fe90f-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="fe90f-207">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="fe90f-207">Related Content</span></span>
* [<span data-ttu-id="fe90f-208">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="fe90f-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="fe90f-209">Unión de una máquina virtual de Windows Server a un dominio administrado</span><span class="sxs-lookup"><span data-stu-id="fe90f-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="fe90f-210">[Inicio de sesión en una máquina virtual con Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe90f-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="fe90f-211">Installing Kerberos (Instalación de Kerberos)</span><span class="sxs-lookup"><span data-stu-id="fe90f-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="fe90f-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: guía de integración de Windows)</span><span class="sxs-lookup"><span data-stu-id="fe90f-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
