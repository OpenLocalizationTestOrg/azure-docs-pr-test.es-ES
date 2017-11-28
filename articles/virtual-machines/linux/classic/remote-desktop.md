---
title: aaaRemote escritorio tooa VM de Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall y configurar Escritorio remoto tooconnect tooa VM de Linux de Microsoft Azure para el modelo de implementación de hello clásico"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="83c84-103">Usar Escritorio remoto tooconnect tooa VM de Linux de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="83c84-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="83c84-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="83c84-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="83c84-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="83c84-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="83c84-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="83c84-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="83c84-107">Para hello actualizado a la versión del Administrador de recursos de este artículo, consulte [aquí](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="83c84-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="83c84-108">Información general</span><span class="sxs-lookup"><span data-stu-id="83c84-108">Overview</span></span>
<span data-ttu-id="83c84-109">RDP (protocolo de escritorio remoto) es un protocolo propietario que se usa para Windows.</span><span class="sxs-lookup"><span data-stu-id="83c84-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="83c84-110">¿Cómo podemos usar RDP tooconnect tooa Linux VM (máquina virtual de) forma remota?</span><span class="sxs-lookup"><span data-stu-id="83c84-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="83c84-111">Esta guía le proporcionará Hola respuesta!</span><span class="sxs-lookup"><span data-stu-id="83c84-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="83c84-112">Le servirá de ayuda xrdp tooinstall y config en su máquina virtual Linux de Microsoft Azure, que le permite conectarse tooit con Escritorio remoto desde un equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="83c84-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="83c84-113">Se usará la VM de Linux ejecutando Ubuntu o OpenSUSE como ejemplo de Hola en esta guía.</span><span class="sxs-lookup"><span data-stu-id="83c84-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="83c84-114">herramienta de Hello xrdp es servidor RDP que podrá tooconnect origen abierto el servidor Linux con Escritorio remoto desde un equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="83c84-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="83c84-115">El rendimiento de RDP es superior al de VNC (Virtual Network Computing).</span><span class="sxs-lookup"><span data-stu-id="83c84-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="83c84-116">VNC representa con gráficos de calidad JPEG y puede ser lento, mientras que RDP ofrece rapidez y nitidez.</span><span class="sxs-lookup"><span data-stu-id="83c84-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="83c84-117">Ya debe tener una VM de Microsoft Azure que ejecuta Linux.</span><span class="sxs-lookup"><span data-stu-id="83c84-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="83c84-118">toocreate y configurar una VM de Linux, vea hello [tutorial de la máquina virtual de Linux de Azure](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="83c84-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="83c84-119">Creación de un punto de conexión para Escritorio remoto</span><span class="sxs-lookup"><span data-stu-id="83c84-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="83c84-120">Usaremos punto de conexión de hello predeterminado 3389 para escritorio remoto en este documento. Establecer el punto de conexión 3389 como `Remote Desktop` tooyour VM de Linux como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="83c84-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![imagen](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="83c84-122">Si no sabe cómo tooset un extremo para la máquina virtual, consulte [esta guía](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="83c84-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="83c84-123">Instalar Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="83c84-123">Install Gnome Desktop</span></span>
<span data-ttu-id="83c84-124">Conectar tooyour VM de Linux a través de `putty`e instalar `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="83c84-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="83c84-125">Para Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="83c84-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="83c84-126">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="83c84-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="83c84-127">Instalación de xrdp</span><span class="sxs-lookup"><span data-stu-id="83c84-127">Install xrdp</span></span>
<span data-ttu-id="83c84-128">Para Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="83c84-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="83c84-129">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="83c84-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="83c84-130">Actualizar versión de hello OpenSUSE con la versión de Hola que utilizas en el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="83c84-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="83c84-131">ejemplo de Hola siguiente es para `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="83c84-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="83c84-132">Iniciar xrdp y establecer el servicio xdrp durante el arranque</span><span class="sxs-lookup"><span data-stu-id="83c84-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="83c84-133">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="83c84-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="83c84-134">Para Ubuntu, se iniciará y habilitará xrdp durante el arranque automáticamente después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="83c84-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="83c84-135">Uso de xfce si utiliza una versión de Ubuntu posterior a Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="83c84-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="83c84-136">Hola actual versión de xrdp no son compatibles con escritorio Gnome para Ubuntu versiones posterior a Ubuntu 12.04LTS, usaremos `xfce` escritorio en su lugar.</span><span class="sxs-lookup"><span data-stu-id="83c84-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="83c84-137">tooinstall `xfce`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="83c84-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="83c84-138">A continuación, habilite `xfce` con este comando:</span><span class="sxs-lookup"><span data-stu-id="83c84-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="83c84-139">Editar el archivo de configuración de Hola `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="83c84-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="83c84-140">Agregue la línea hello `xfce4-session` antes de la línea hello `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="83c84-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="83c84-141">toorestart Hola xrdp servicio, utilice esto:</span><span class="sxs-lookup"><span data-stu-id="83c84-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="83c84-142">Conexión de su VM Linux desde un equipo de Windows</span><span class="sxs-lookup"><span data-stu-id="83c84-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="83c84-143">En un equipo Windows, inicie el cliente de escritorio remoto de Hola y el nombre DNS de la máquina virtual de Linux de entrada.</span><span class="sxs-lookup"><span data-stu-id="83c84-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="83c84-144">O vaya toohello panel de la máquina virtual en hello portal de Azure y haga clic en `Connect` tooconnect la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="83c84-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="83c84-145">En ese caso, verá la ventana de inicio de sesión de hello:</span><span class="sxs-lookup"><span data-stu-id="83c84-145">In that case, you see hello login window:</span></span>

![imagen](./media/remote-desktop/no2.png)

<span data-ttu-id="83c84-147">Inicie sesión con el nombre de usuario de Hola y la contraseña de la VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="83c84-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83c84-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="83c84-148">Next steps</span></span>
<span data-ttu-id="83c84-149">Para más información sobre el uso de xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="83c84-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
