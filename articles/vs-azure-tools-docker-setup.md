---
title: un Host de Docker con VirtualBox aaaConfigure | Documentos de Microsoft
description: "Instancia de un valor predeterminado de Docker mediante máquina Docker y VirtualBox de tooconfigure de instrucciones paso a paso"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 0b1335a2-7720-42a8-8260-4e06fc00c9f6
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 1df2da4482444a803d05e413e019edcc57269062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a>Configuración de un host de Docker con VirtualBox
## <a name="overview"></a>Información general
Este artículo le guiará por el proceso de configuración de una instancia de Docker predeterminada con la máquina de Docker y VirtualBox. Si usas hello [beta de Docker para Windows](http://beta.docker.com/), esta configuración no es necesaria.

## <a name="prerequisites"></a>Requisitos previos
Hello siguientes herramientas necesitan toobe instalado.

* [Docker Toolbox](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a>Configuración de cliente hello con Windows PowerShell
tooconfigure un cliente de Docker, simplemente abra Windows PowerShell y realizar Hola pasos:

1. Cree una instancia de host de docker predeterminada.
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. Compruebe la instancia predeterminada de hello está configurado y en ejecución. (Verá que se ejecuta una instancia denominada 'predeterminada'.
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![salida de docker-machine ls][0]
3. Establezca el valor predeterminado como host actual de Hola y configurar el shell.
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. Mostrar contenedores de Docker active Hola. lista de Hello debe estar vacío.
   
    ```PowerShell
    docker ps
    ```
   
    ![salida de docker ps][1]

> [!NOTE]
> Cada vez que se reinicie el equipo de desarrollo, necesitará toorestart host docker local.
> toodo, Hola problema siguiente comando en un símbolo del sistema: `docker-machine start default`.
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
