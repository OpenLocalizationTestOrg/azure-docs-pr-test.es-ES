---
title: "aaaAzure inicio rápido: crear un Portal de VM de Windows | Documentos de Microsoft"
description: "Inicio rápido de Azure: creación de máquinas virtuales Windows con el Portal"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="f4024-103">Crear una máquina virtual de Windows con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f4024-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="f4024-104">Máquinas virtuales de Azure se pueden crear a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4024-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="f4024-105">Este método proporciona una interfaz de usuario basada en el explorador para crear y configurar máquinas virtuales y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="f4024-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="f4024-106">Este inicio rápido recorre crear una máquina virtual e instalar un servidor Web en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4024-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="f4024-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="f4024-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="f4024-108">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4024-108">Log in tooAzure</span></span>

<span data-ttu-id="f4024-109">Inicie sesión en toohello portal de Azure en http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="f4024-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="f4024-110">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="f4024-110">Create virtual machine</span></span>

1. <span data-ttu-id="f4024-111">Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4024-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="f4024-112">Seleccione **Compute**y, después, seleccione **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="f4024-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="f4024-113">Escriba la información de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4024-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="f4024-114">nombre de usuario de Hello y una contraseña escritos aquí es toolog usado en la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="f4024-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="f4024-115">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-115">When complete, click **OK**.</span></span>

    ![Especificar información básica acerca de la máquina virtual en la hoja de portal de Hola](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="f4024-117">Seleccione un tamaño para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4024-117">Select a size for hello VM.</span></span> <span data-ttu-id="f4024-118">toosee tamaños más, seleccione **todas las ver** o cambiar hello **admite el tipo de disco** filtro.</span><span class="sxs-lookup"><span data-stu-id="f4024-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Captura de pantalla que muestra los tamaños de máquina virtual](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="f4024-120">En la hoja de configuración de hello, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="f4024-121">En la página de resumen de hello, haga clic en **Aceptar** implementación de máquina virtual de toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="f4024-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="f4024-122">Hola VM será toohello anclado Azure panel del portal.</span><span class="sxs-lookup"><span data-stu-id="f4024-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="f4024-123">Cuando haya completado la implementación de hello, hoja de resumen de VM de Hola se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f4024-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="f4024-124">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="f4024-124">Connect toovirtual machine</span></span>

<span data-ttu-id="f4024-125">Crear una máquina virtual de toohello de conexión a Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="f4024-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="f4024-126">Haga clic en hello **conectar** botón de propiedades de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4024-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="f4024-127">Se crea y se descarga un archivo de Protocolo de Escritorio remoto (archivo .rdp).</span><span class="sxs-lookup"><span data-stu-id="f4024-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="f4024-129">tooconnect tooyour máquina virtual, abra Hola descarga archivo RDP.</span><span class="sxs-lookup"><span data-stu-id="f4024-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="f4024-130">Cuando se le solicite, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="f4024-131">En un equipo Mac, necesita un cliente RDP como este [cliente de escritorio remoto](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de hello Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="f4024-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="f4024-132">Escriba el nombre de usuario de Hola y la contraseña que especificó al crear la máquina virtual de hello, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="f4024-133">Recibirá una advertencia de certificado durante el proceso de inicio de sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="f4024-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="f4024-134">Haga clic en **Sí** o **continuar** tooproceed con conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="f4024-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="f4024-135">Instalación de IIS mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4024-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="f4024-136">En la máquina virtual de hello, iniciar una sesión de PowerShell y ejecute hello después comando tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="f4024-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="f4024-137">Cuando haya finalizado, salga de la sesión RDP de Hola y devolver propiedades de la máquina virtual de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4024-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="f4024-138">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="f4024-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="f4024-139">Los grupos de seguridad de red (NSG) protegen el tráfico entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="f4024-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="f4024-140">Cuando se crea una máquina virtual de hello portal de Azure, se crea una regla de entrada en el puerto 3389 para las conexiones RDP.</span><span class="sxs-lookup"><span data-stu-id="f4024-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="f4024-141">Debido a esta máquina virtual hospeda un servidor Web, una regla de NSG necesario toobe creado para el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="f4024-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="f4024-142">En la máquina virtual de hello, haga clic en nombre de Hola de hello **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="f4024-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="f4024-143">Seleccione hello **grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="f4024-143">Select hello **network security group**.</span></span> <span data-ttu-id="f4024-144">Hello NSG puede identificarse mediante el uso hello **tipo** columna.</span><span class="sxs-lookup"><span data-stu-id="f4024-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="f4024-145">En el menú izquierdo de hello, en configuración, haga clic en **reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="f4024-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="f4024-146">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-146">Click on **Add**.</span></span>
5. <span data-ttu-id="f4024-147">En **Nombre**, escriba **http**.</span><span class="sxs-lookup"><span data-stu-id="f4024-147">In **Name**, type **http**.</span></span> <span data-ttu-id="f4024-148">Asegúrese de que **intervalo de puertos** se establece too80 y **acción** se establece demasiado**permitir**.</span><span class="sxs-lookup"><span data-stu-id="f4024-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="f4024-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="f4024-150">Hola de vista Página de bienvenida de IIS</span><span class="sxs-lookup"><span data-stu-id="f4024-150">View hello IIS welcome page</span></span>

<span data-ttu-id="f4024-151">Con IIS instalado y el puerto 80 abra tooyour VM, Hola webserver ahora puede tener acceso desde Hola internet.</span><span class="sxs-lookup"><span data-stu-id="f4024-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="f4024-152">Abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f4024-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="f4024-153">la dirección IP pública Hola puede encontrarse en la hoja de la máquina virtual de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4024-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Sitio predeterminado de IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="f4024-155">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="f4024-155">Clean up resources</span></span>

<span data-ttu-id="f4024-156">Cuando ya no es necesario, eliminar el grupo de recursos de hello, máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f4024-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f4024-157">toodo por lo tanto, seleccione el grupo de recursos de Hola de hoja de la máquina virtual de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f4024-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4024-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4024-158">Next steps</span></span>

<span data-ttu-id="f4024-159">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="f4024-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="f4024-160">toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="f4024-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4024-161">Tutoriales de máquinas virtuales Windows de Azure</span><span class="sxs-lookup"><span data-stu-id="f4024-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
