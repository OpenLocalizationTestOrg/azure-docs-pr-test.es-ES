---
title: 'Azure Active Directory Domain Services: Unirse a un dominio administrado de RHEL VM tooa | Documentos de Microsoft'
description: "Unir una máquina virtual de Red Hat Enterprise Linux tooAzure AD los servicios de dominio"
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
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="98a03-103">Unirse a un dominio administrado de Red Hat Enterprise Linux 7 máquina virtual tooa</span><span class="sxs-lookup"><span data-stu-id="98a03-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="98a03-104">Este artículo muestra cómo toojoin una tooan de máquina virtual de Red Hat Enterprise Linux (RHEL) 7 Servicios de dominio de Azure AD administra el dominio.</span><span class="sxs-lookup"><span data-stu-id="98a03-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="98a03-105">Aprovisionamiento de una máquina virtual de Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="98a03-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="98a03-106">Realizar Hola después de la máquina virtual pasos tooprovision un RHEL 7 a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="98a03-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="98a03-107">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="98a03-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Panel de Portal de Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="98a03-109">Haga clic en **New** en hello dejado panel y escriba **Red Hat** en la barra de búsqueda de hello tal y como se muestra en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="98a03-110">Las entradas para Red Hat Enterprise Linux aparezcan en resultados de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="98a03-111">Haga clic en **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="98a03-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="98a03-113">resultados de búsqueda de Hello en hello **todo** panel debe enumerar imagen Hola Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="98a03-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="98a03-114">Haga clic en **Red Hat Enterprise Linux 7.2** tooview obtener más información acerca de la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Seleccionar RHEL en resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="98a03-116">Hola **Red Hat Enterprise Linux 7.2** panel, debería ver más información acerca de la imagen de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="98a03-117">Hola **seleccionar un modelo de implementación** lista desplegable, seleccione **clásico**.</span><span class="sxs-lookup"><span data-stu-id="98a03-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="98a03-118">A continuación, haga clic en hello **crear** botón.</span><span class="sxs-lookup"><span data-stu-id="98a03-118">Then click hello **Create** button.</span></span>

    ![Ver detalles de la imagen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="98a03-120">Hola **conceptos básicos de** página de hello **crear máquina virtual** asistente, escriba Hola **nombre de Host** para la máquina virtual nueva de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="98a03-121">Especificar un nombre de usuario de administrador local en hello **nombre de usuario** campo y un **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="98a03-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="98a03-122">También puede elegir toouse un usuario de administrador local de Hola de tooauthenticate clave SSH.</span><span class="sxs-lookup"><span data-stu-id="98a03-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="98a03-123">Seleccionar una **tarifa** para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Crear máquina virtual: página de aspectos básicos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="98a03-125">Hola **tamaño** página de hello **crear máquina virtual** tamaño Hola asistente, seleccione para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Crear máquina virtual: seleccionar tamaño](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="98a03-127">Hola **configuración** página de hello **crear máquina virtual** cuenta de almacenamiento de saludo del asistente, seleccione para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="98a03-128">Haga clic en **red Virtual** tooselect Hola Hola de toowhich de red virtual se deben implementar la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="98a03-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="98a03-129">Hola **red Virtual** hoja, red virtual seleccione hello en el que los servicios de dominio de Azure AD está disponible.</span><span class="sxs-lookup"><span data-stu-id="98a03-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="98a03-130">En este ejemplo, hemos elegido red virtual de hello 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="98a03-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Crear máquina virtual: seleccionar la red virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="98a03-132">En hello **resumen** página de hello **crear máquina virtual** Hola asistente, revise y haga clic en **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="98a03-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Crear máquina virtual: red virtual seleccionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="98a03-134">Debe iniciar la implementación de hello nueva máquina virtual basada en imagen de hello RHEL 7.2.</span><span class="sxs-lookup"><span data-stu-id="98a03-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Crear máquina virtual: implementación iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="98a03-136">Después de unos minutos, máquina virtual de hello debe ser implementada correctamente y está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="98a03-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Crear máquina virtual: implementado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="98a03-138">Conectar la máquina virtual de Linux toohello recién aprovisionado de forma remota</span><span class="sxs-lookup"><span data-stu-id="98a03-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="98a03-139">máquina virtual de Hello RHEL 7.2 se haya aprovisionado en Azure.</span><span class="sxs-lookup"><span data-stu-id="98a03-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="98a03-140">Hola siguiente tarea es tooconnect de forma remota máquinas virtuales de toohello.</span><span class="sxs-lookup"><span data-stu-id="98a03-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="98a03-141">**Conectar máquina virtual de toohello RHEL 7.2** siga las instrucciones de hello en el artículo hello [cómo toolog en la máquina virtual de tooa ejecutan Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98a03-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="98a03-142">resto de Hola de pasos de hello supongamos que se usa Hola PuTTY SSH cliente tooconnect toohello RHEL máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="98a03-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="98a03-143">Para obtener más información, vea hello [página de descargas de PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="98a03-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="98a03-144">Abra Hola PuTTY programa.</span><span class="sxs-lookup"><span data-stu-id="98a03-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="98a03-145">Escriba hello **nombre de Host** para hello recién creado la máquina virtual RHEL.</span><span class="sxs-lookup"><span data-stu-id="98a03-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="98a03-146">En este ejemplo, de la máquina virtual tiene el nombre de host de hello 'contoso rhel.cloudapp .net'.</span><span class="sxs-lookup"><span data-stu-id="98a03-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="98a03-147">Si no está seguro del nombre de host de saludo de la máquina virtual, consulte toohello panel de máquinas virtuales en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="98a03-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Conexión a PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="98a03-149">Inicie sesión en la máquina virtual de toohello con credenciales de administrador local de Hola que especificó cuando creó la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="98a03-150">En este ejemplo, se utiliza la cuenta de administrador local de Hola "mahesh".</span><span class="sxs-lookup"><span data-stu-id="98a03-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Inicio de sesión de PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="98a03-152">Instalar los paquetes necesarios en la máquina virtual de Linux de Hola</span><span class="sxs-lookup"><span data-stu-id="98a03-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="98a03-153">Después de la máquina virtual en conexión toohello Hola siguiente tarea es paquetes tooinstall necesarios para unirse a un dominio en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="98a03-154">Lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="98a03-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="98a03-155">**Instalar realmd:** paquete de hello realmd se usa para unirse a un dominio.</span><span class="sxs-lookup"><span data-stu-id="98a03-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="98a03-156">En el terminal PuTTY, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98a03-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="98a03-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="98a03-157">sudo yum install realmd</span></span>

    ![Instalar realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="98a03-159">Después de unos minutos, paquete de hello realmd debe se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="98a03-161">**Instalar sssd:** hello realmd paquete dependiente sssd tooperform las operaciones de combinación de dominio.</span><span class="sxs-lookup"><span data-stu-id="98a03-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="98a03-162">En el terminal PuTTY, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98a03-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="98a03-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="98a03-163">sudo yum install sssd</span></span>

    ![Instalar sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="98a03-165">Después de unos minutos, paquete de hello sssd debe se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="98a03-167">**Instalar kerberos:** de su terminal PuTTY, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98a03-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="98a03-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="98a03-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalar kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="98a03-170">Después de unos minutos, paquete de hello realmd debe se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="98a03-172">Unirse a dominio administrado del toohello de máquina virtual Linux Hola</span><span class="sxs-lookup"><span data-stu-id="98a03-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="98a03-173">Ahora que los paquetes de saludo necesario están instalados en la máquina virtual de Linux de hello, Hola siguiente tarea es dominio administrado del toohello toojoin Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="98a03-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="98a03-174">Detectar el dominio administrado de los servicios de dominio de AAD Hola.</span><span class="sxs-lookup"><span data-stu-id="98a03-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="98a03-175">En el terminal PuTTY, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98a03-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="98a03-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="98a03-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="98a03-178">Si **territorio detectar** es no se puede toofind el dominio administrado, asegúrese de ese dominio hello es accesible desde la máquina virtual de hello (try ping).</span><span class="sxs-lookup"><span data-stu-id="98a03-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="98a03-179">Asegúrese también de que la máquina virtual Hola realmente ha sido implementado toohello misma red virtual en qué Hola dominio administrado está disponible.</span><span class="sxs-lookup"><span data-stu-id="98a03-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="98a03-180">Inicialice kerberos.</span><span class="sxs-lookup"><span data-stu-id="98a03-180">Initialize kerberos.</span></span> <span data-ttu-id="98a03-181">En el terminal PuTTY, escriba Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="98a03-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="98a03-182">Asegúrese de especificar un usuario que pertenece el grupo toohello 'AAD DC administradores'.</span><span class="sxs-lookup"><span data-stu-id="98a03-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="98a03-183">Solo estos usuarios pueden unirse a dominio administrado de equipos toohello.</span><span class="sxs-lookup"><span data-stu-id="98a03-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="98a03-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="98a03-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="98a03-186">Asegurarse de que se especifique el nombre de dominio de hello en letras mayúsculas, kinit else se produce un error.</span><span class="sxs-lookup"><span data-stu-id="98a03-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="98a03-187">Unirse a dominio de hello máquina toohello.</span><span class="sxs-lookup"><span data-stu-id="98a03-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="98a03-188">En el terminal PuTTY, escriba Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="98a03-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="98a03-189">Especificar Hola mismo usuario que especificó en hello anterior paso ('kinit').</span><span class="sxs-lookup"><span data-stu-id="98a03-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="98a03-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="98a03-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Unión a dominio kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="98a03-192">Debe obtener un mensaje ("se inscribió correctamente máquina en el dominio Kerberos") cuando la máquina de hello es dominio administrado toohello se unió correctamente.</span><span class="sxs-lookup"><span data-stu-id="98a03-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="98a03-193">Verificación de la unión a un dominio</span><span class="sxs-lookup"><span data-stu-id="98a03-193">Verify domain join</span></span>
<span data-ttu-id="98a03-194">Para comprobar rápidamente si máquina Hola ha sido el dominio administrado toohello se unió correctamente.</span><span class="sxs-lookup"><span data-stu-id="98a03-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="98a03-195">Conectar toohello recién Unidos a un dominio RHEL VM con SSH y una cuenta de usuario de dominio y, a continuación, toosee de comprobación si la cuenta de usuario de Hola se resuelve correctamente.</span><span class="sxs-lookup"><span data-stu-id="98a03-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="98a03-196">En el terminal, PuTTY Hola de tipo siguientes comando tooconnect toohello recién Unidos RHEL virtual máquina mediante SSH a un dominio.</span><span class="sxs-lookup"><span data-stu-id="98a03-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="98a03-197">Usar una cuenta de dominio que pertenece el dominio administrado toohello (por ejemplo, 'bob@CONTOSO100.COM' en este caso.)</span><span class="sxs-lookup"><span data-stu-id="98a03-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="98a03-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="98a03-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="98a03-199">En el terminal PuTTY, escriba Hola después toosee comando si el directorio particular de Hola se inicializó correctamente.</span><span class="sxs-lookup"><span data-stu-id="98a03-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="98a03-200">pwd</span><span class="sxs-lookup"><span data-stu-id="98a03-200">pwd</span></span>
3. <span data-ttu-id="98a03-201">En el terminal PuTTY, escriba Hola después toosee comando si se están resolviendo las pertenencias a grupos de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="98a03-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="98a03-202">id</span><span class="sxs-lookup"><span data-stu-id="98a03-202">id</span></span>

<span data-ttu-id="98a03-203">Este es un ejemplo de los resultados de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="98a03-203">A sample output of these commands follows:</span></span>

![Verificación de la unión a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="98a03-205">Solución de problemas de unión al dominio</span><span class="sxs-lookup"><span data-stu-id="98a03-205">Troubleshooting domain join</span></span>
<span data-ttu-id="98a03-206">Consulte toohello [unión al dominio de solución de problemas](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artículo.</span><span class="sxs-lookup"><span data-stu-id="98a03-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="98a03-207">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="98a03-207">Related Content</span></span>
* [<span data-ttu-id="98a03-208">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="98a03-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="98a03-209">Unirse a un dominio administrado de Windows Server máquina virtual tooan servicios de dominio de AD de Azure</span><span class="sxs-lookup"><span data-stu-id="98a03-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="98a03-210">[¿Cómo toolog en la máquina virtual de tooa ejecutan Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98a03-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="98a03-211">Installing Kerberos (Instalación de Kerberos)</span><span class="sxs-lookup"><span data-stu-id="98a03-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="98a03-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: guía de integración de Windows)</span><span class="sxs-lookup"><span data-stu-id="98a03-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
