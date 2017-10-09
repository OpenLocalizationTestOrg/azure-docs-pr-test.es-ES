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
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="c2187-103">Configuración de un host de Docker con VirtualBox</span><span class="sxs-lookup"><span data-stu-id="c2187-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="c2187-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c2187-104">Overview</span></span>
<span data-ttu-id="c2187-105">Este artículo le guiará por el proceso de configuración de una instancia de Docker predeterminada con la máquina de Docker y VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="c2187-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="c2187-106">Si usas hello [beta de Docker para Windows](http://beta.docker.com/), esta configuración no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="c2187-106">If you’re using hello [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2187-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c2187-107">Prerequisites</span></span>
<span data-ttu-id="c2187-108">Hello siguientes herramientas necesitan toobe instalado.</span><span class="sxs-lookup"><span data-stu-id="c2187-108">hello following tools need toobe installed.</span></span>

* [<span data-ttu-id="c2187-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="c2187-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-hello-docker-client-with-windows-powershell"></a><span data-ttu-id="c2187-110">Configuración de cliente hello con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2187-110">Configuring hello Docker client with Windows PowerShell</span></span>
<span data-ttu-id="c2187-111">tooconfigure un cliente de Docker, simplemente abra Windows PowerShell y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c2187-111">tooconfigure a Docker client, simply open Windows PowerShell, and perform hello following steps:</span></span>

1. <span data-ttu-id="c2187-112">Cree una instancia de host de docker predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c2187-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="c2187-113">Compruebe la instancia predeterminada de hello está configurado y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="c2187-113">Verify hello default instance is configured and running.</span></span> <span data-ttu-id="c2187-114">(Verá que se ejecuta una instancia denominada 'predeterminada'.</span><span class="sxs-lookup"><span data-stu-id="c2187-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![salida de docker-machine ls][0]
3. <span data-ttu-id="c2187-116">Establezca el valor predeterminado como host actual de Hola y configurar el shell.</span><span class="sxs-lookup"><span data-stu-id="c2187-116">Set default as hello current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="c2187-117">Mostrar contenedores de Docker active Hola.</span><span class="sxs-lookup"><span data-stu-id="c2187-117">Display hello active Docker containers.</span></span> <span data-ttu-id="c2187-118">lista de Hello debe estar vacío.</span><span class="sxs-lookup"><span data-stu-id="c2187-118">hello list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![salida de docker ps][1]

> [!NOTE]
> <span data-ttu-id="c2187-120">Cada vez que se reinicie el equipo de desarrollo, necesitará toorestart host docker local.</span><span class="sxs-lookup"><span data-stu-id="c2187-120">Each time you reboot your development machine, you’ll need toorestart your local docker host.</span></span>
> <span data-ttu-id="c2187-121">toodo, Hola problema siguiente comando en un símbolo del sistema: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="c2187-121">toodo this, issue hello following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
