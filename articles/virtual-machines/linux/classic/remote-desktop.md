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
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Usar Escritorio remoto tooconnect tooa VM de Linux de Microsoft Azure
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para hello actualizado a la versión del Administrador de recursos de este artículo, consulte [aquí](../use-remote-desktop.md).

## <a name="overview"></a>Información general
RDP (protocolo de escritorio remoto) es un protocolo propietario que se usa para Windows. ¿Cómo podemos usar RDP tooconnect tooa Linux VM (máquina virtual de) forma remota?

Esta guía le proporcionará Hola respuesta! Le servirá de ayuda xrdp tooinstall y config en su máquina virtual Linux de Microsoft Azure, que le permite conectarse tooit con Escritorio remoto desde un equipo Windows. Se usará la VM de Linux ejecutando Ubuntu o OpenSUSE como ejemplo de Hola en esta guía.

herramienta de Hello xrdp es servidor RDP que podrá tooconnect origen abierto el servidor Linux con Escritorio remoto desde un equipo Windows. El rendimiento de RDP es superior al de VNC (Virtual Network Computing). VNC representa con gráficos de calidad JPEG y puede ser lento, mientras que RDP ofrece rapidez y nitidez.

> [!NOTE]
> Ya debe tener una VM de Microsoft Azure que ejecuta Linux. toocreate y configurar una VM de Linux, vea hello [tutorial de la máquina virtual de Linux de Azure](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Creación de un punto de conexión para Escritorio remoto
Usaremos punto de conexión de hello predeterminado 3389 para escritorio remoto en este documento. Establecer el punto de conexión 3389 como `Remote Desktop` tooyour VM de Linux como las siguientes:

![imagen](./media/remote-desktop/endpoint-for-linux-server.png)

Si no sabe cómo tooset un extremo para la máquina virtual, consulte [esta guía](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Instalar Gnome Desktop
Conectar tooyour VM de Linux a través de `putty`e instalar `Gnome Desktop`.

Para Ubuntu, use:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Para OpenSUSE, use:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Instalación de xrdp
Para Ubuntu, use:

    #sudo apt-get install xrdp

Para OpenSUSE, use:

> [!NOTE]
> Actualizar versión de hello OpenSUSE con la versión de Hola que utilizas en el siguiente comando de Hola. ejemplo de Hola siguiente es para `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Iniciar xrdp y establecer el servicio xdrp durante el arranque
Para OpenSUSE, use:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Para Ubuntu, se iniciará y habilitará xrdp durante el arranque automáticamente después de la instalación.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Uso de xfce si utiliza una versión de Ubuntu posterior a Ubuntu 12.04LTS
Hola actual versión de xrdp no son compatibles con escritorio Gnome para Ubuntu versiones posterior a Ubuntu 12.04LTS, usaremos `xfce` escritorio en su lugar.

tooinstall `xfce`, use este comando:

    #sudo apt-get install xubuntu-desktop

A continuación, habilite `xfce` con este comando:

    #echo xfce4-session >~/.xsession

Editar el archivo de configuración de Hola `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Agregue la línea hello `xfce4-session` antes de la línea hello `/etc/X11/Xsession`.

toorestart Hola xrdp servicio, utilice esto:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Conexión de su VM Linux desde un equipo de Windows
En un equipo Windows, inicie el cliente de escritorio remoto de Hola y el nombre DNS de la máquina virtual de Linux de entrada. O vaya toohello panel de la máquina virtual en hello portal de Azure y haga clic en `Connect` tooconnect la VM de Linux. En ese caso, verá la ventana de inicio de sesión de hello:

![imagen](./media/remote-desktop/no2.png)

Inicie sesión con el nombre de usuario de Hola y la contraseña de la VM de Linux.

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre el uso de xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).
