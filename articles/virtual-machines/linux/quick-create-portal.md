---
title: "aaaAzure inicio rápido: crear VM Portal | Documentos de Microsoft"
description: "Inicio rápido de Azure: creación de máquinas virtuales con el Portal"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="037c3-103">Crear una máquina virtual Linux con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="037c3-103">Create a Linux virtual machine with hello Azure portal</span></span>

<span data-ttu-id="037c3-104">Máquinas virtuales de Azure se pueden crear a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c3-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="037c3-105">Este método proporciona una interfaz de usuario basada en el explorador para crear y configurar máquinas virtuales y todos los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="037c3-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="037c3-106">Este inicio rápido recorre crear una máquina virtual e instalar un servidor Web en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="037c3-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="037c3-107">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="037c3-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="037c3-108">Creación del par de claves SSH</span><span class="sxs-lookup"><span data-stu-id="037c3-108">Create SSH key pair</span></span>

<span data-ttu-id="037c3-109">Es necesario un toocomplete de par de claves SSH este inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="037c3-109">You need an SSH key pair toocomplete this quick start.</span></span> <span data-ttu-id="037c3-110">Si ya tiene un par de claves SSH, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="037c3-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="037c3-111">Desde un shell de Bash, ejecute este comando y siga hello en pantalla direcciones.</span><span class="sxs-lookup"><span data-stu-id="037c3-111">From a Bash shell, run this command and follow hello on-screen directions.</span></span> <span data-ttu-id="037c3-112">resultado del comando Hello incluye nombre hello del archivo de clave pública Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-112">hello command output includes hello file name of hello public key file.</span></span> <span data-ttu-id="037c3-113">Copie el contenido de hello del Portapapeles de toohello del archivo de clave pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-113">Copy hello contents of hello public key file toohello clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a><span data-ttu-id="037c3-114">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="037c3-114">Log in tooAzure</span></span> 

<span data-ttu-id="037c3-115">Inicie sesión en toohello portal de Azure en http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="037c3-115">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="037c3-116">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="037c3-116">Create virtual machine</span></span>

1. <span data-ttu-id="037c3-117">Haga clic en hello **New** encontró el botón en la esquina izquierda superior de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c3-117">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="037c3-118">Seleccione **Compute**y, después, seleccione **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="037c3-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="037c3-119">Escriba la información de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-119">Enter hello virtual machine information.</span></span> <span data-ttu-id="037c3-120">En **Tipo de autenticación**, seleccione **Clave pública SSH**.</span><span class="sxs-lookup"><span data-stu-id="037c3-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="037c3-121">Al pegar en su clave pública SSH, procure tooremove los espacios en blanco iniciales ni finales.</span><span class="sxs-lookup"><span data-stu-id="037c3-121">When pasting in your SSH public key, take care tooremove any leading or trailing white space.</span></span> <span data-ttu-id="037c3-122">Cuando haya terminado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="037c3-122">When complete, click **OK**.</span></span>

    ![Especificar información básica acerca de la máquina virtual en la hoja de portal de Hola](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="037c3-124">Seleccione un tamaño para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="037c3-124">Select a size for hello VM.</span></span> <span data-ttu-id="037c3-125">toosee tamaños más, seleccione **todas las ver** o cambiar hello **admite el tipo de disco** filtro.</span><span class="sxs-lookup"><span data-stu-id="037c3-125">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Captura de pantalla que muestra los tamaños de máquina virtual](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="037c3-127">En la hoja de configuración de hello, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="037c3-127">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="037c3-128">En la página de resumen de hello, haga clic en **Aceptar** implementación de máquina virtual de toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-128">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="037c3-129">Hola VM será toohello anclado Azure panel del portal.</span><span class="sxs-lookup"><span data-stu-id="037c3-129">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="037c3-130">Cuando haya completado la implementación de hello, hoja de resumen de VM de Hola se abre automáticamente.</span><span class="sxs-lookup"><span data-stu-id="037c3-130">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="037c3-131">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="037c3-131">Connect toovirtual machine</span></span>

<span data-ttu-id="037c3-132">Crear una conexión SSH con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-132">Create an SSH connection with hello virtual machine.</span></span>

1. <span data-ttu-id="037c3-133">Haga clic en hello **conectar** botón en la hoja de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-133">Click hello **Connect** button on hello virtual machine blade.</span></span> <span data-ttu-id="037c3-134">Hola conectarse botón muestra una cadena de conexión de SSH que puede ser utilizados tooconnect toohello virtual máquina.</span><span class="sxs-lookup"><span data-stu-id="037c3-134">hello connect button displays an SSH connection string that can be used tooconnect toohello virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="037c3-136">Siguiente ejecución Hola comando toocreate una sesión SSH.</span><span class="sxs-lookup"><span data-stu-id="037c3-136">Run hello following command toocreate an SSH session.</span></span> <span data-ttu-id="037c3-137">Reemplace la cadena de conexión de hello con hello uno que copió de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c3-137">Replace hello connection string with hello one you copied from hello Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="037c3-138">Instalación de NGINX</span><span class="sxs-lookup"><span data-stu-id="037c3-138">Install NGINX</span></span>

<span data-ttu-id="037c3-139">Hola a uso continuación bash orígenes de paquetes de secuencia de comandos tooupdate e instala paquete NGINX más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="037c3-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="037c3-140">Cuando haya finalizado, salga de sesión SSH de Hola y devolver propiedades de la máquina virtual de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c3-140">When done, exit hello SSH session and return hello VM properties in hello Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="037c3-141">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="037c3-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="037c3-142">Los grupos de seguridad de red (NSG) protegen el tráfico entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="037c3-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="037c3-143">Cuando se crea una máquina virtual de hello portal de Azure, se crea una regla de entrada en el puerto 22 para las conexiones SSH.</span><span class="sxs-lookup"><span data-stu-id="037c3-143">When a VM is created from hello Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="037c3-144">Debido a esta máquina virtual hospeda un servidor Web, una regla de NSG necesario toobe creado para el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="037c3-144">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="037c3-145">En la máquina virtual de hello, haga clic en nombre de Hola de hello **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="037c3-145">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="037c3-146">Seleccione hello **grupo de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="037c3-146">Select hello **network security group**.</span></span> <span data-ttu-id="037c3-147">Hello NSG puede identificarse mediante el uso hello **tipo** columna.</span><span class="sxs-lookup"><span data-stu-id="037c3-147">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="037c3-148">En el menú izquierdo de hello, en configuración, haga clic en **reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="037c3-148">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="037c3-149">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="037c3-149">Click on **Add**.</span></span>
5. <span data-ttu-id="037c3-150">En **Nombre**, escriba **http**.</span><span class="sxs-lookup"><span data-stu-id="037c3-150">In **Name**, type **http**.</span></span> <span data-ttu-id="037c3-151">Asegúrese de que **intervalo de puertos** se establece too80 y **acción** se establece demasiado**permitir**.</span><span class="sxs-lookup"><span data-stu-id="037c3-151">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="037c3-152">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="037c3-152">Click **OK**.</span></span>


## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="037c3-153">Página de bienvenida de vista hello NGINX</span><span class="sxs-lookup"><span data-stu-id="037c3-153">View hello NGINX welcome page</span></span>

<span data-ttu-id="037c3-154">Con NGINX instalada y el puerto 80 abra tooyour VM, servidor Web Hola ahora puede tener acceso desde Hola internet.</span><span class="sxs-lookup"><span data-stu-id="037c3-154">With NGINX installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="037c3-155">Abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="037c3-155">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="037c3-156">la dirección IP pública Hola puede encontrarse en la hoja de la máquina virtual de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="037c3-156">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Sitio predeterminado de NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="037c3-158">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="037c3-158">Clean up resources</span></span>

<span data-ttu-id="037c3-159">Cuando ya no es necesario, eliminar el grupo de recursos de hello, máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="037c3-159">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="037c3-160">toodo por lo tanto, seleccione el grupo de recursos de Hola de hoja de la máquina virtual de Hola y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="037c3-160">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="037c3-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="037c3-161">Next steps</span></span>

<span data-ttu-id="037c3-162">En esta guía de inicio rápido, ha implementado una máquina virtual simple y una regla de grupo de seguridad de red, y ha instalado un servidor web.</span><span class="sxs-lookup"><span data-stu-id="037c3-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="037c3-163">toolearn más información acerca de máquinas virtuales de Azure, continuar con tutorial toohello para máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="037c3-163">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="037c3-164">Tutoriales de máquinas virtuales Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="037c3-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
