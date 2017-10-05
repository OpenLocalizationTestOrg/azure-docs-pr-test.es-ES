---
title: "Configuración de un host de Docker con VirtualBox | Microsoft Docs"
description: "Instrucciones paso a paso para configurar una instancia de Docker predeterminada con la máquina de Docker y VirtualBox"
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
ms.openlocfilehash: e9465afb560a73d74f853c19094b3ee75b8c470c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-docker-host-with-virtualbox"></a><span data-ttu-id="fd013-103">Configuración de un host de Docker con VirtualBox</span><span class="sxs-lookup"><span data-stu-id="fd013-103">Configure a Docker Host with VirtualBox</span></span>
## <a name="overview"></a><span data-ttu-id="fd013-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fd013-104">Overview</span></span>
<span data-ttu-id="fd013-105">Este artículo le guiará por el proceso de configuración de una instancia de Docker predeterminada con la máquina de Docker y VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="fd013-105">This article guides you through configuring a default Docker instance using Docker Machine and VirtualBox.</span></span> <span data-ttu-id="fd013-106">Si utiliza [Docker para Windows beta](http://beta.docker.com/), esta configuración no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="fd013-106">If you’re using the [Docker for Windows beta](http://beta.docker.com/), this configuration is not necessary.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd013-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd013-107">Prerequisites</span></span>
<span data-ttu-id="fd013-108">Es necesario instalar las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="fd013-108">The following tools need to be installed.</span></span>

* [<span data-ttu-id="fd013-109">Docker Toolbox</span><span class="sxs-lookup"><span data-stu-id="fd013-109">Docker Toolbox</span></span>](https://www.docker.com/products/overview#/docker_toolbox)

## <a name="configuring-the-docker-client-with-windows-powershell"></a><span data-ttu-id="fd013-110">Configuración del cliente de Docker con Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd013-110">Configuring the Docker client with Windows PowerShell</span></span>
<span data-ttu-id="fd013-111">Para configurar a un cliente de Docker, simplemente abra Windows PowerShell y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd013-111">To configure a Docker client, simply open Windows PowerShell, and perform the following steps:</span></span>

1. <span data-ttu-id="fd013-112">Cree una instancia de host de docker predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fd013-112">Create a default docker host instance.</span></span>
   
    ```PowerShell
    docker-machine create --driver virtualbox default
    ```
2. <span data-ttu-id="fd013-113">Compruebe que la instancia predeterminada está configurada y en ejecución.</span><span class="sxs-lookup"><span data-stu-id="fd013-113">Verify the default instance is configured and running.</span></span> <span data-ttu-id="fd013-114">(Verá que se ejecuta una instancia denominada 'predeterminada'.</span><span class="sxs-lookup"><span data-stu-id="fd013-114">(You should see an instance named \`default' running.</span></span>
   
    ```PowerShell
    docker-machine ls 
    ```
   
    ![salida de docker-machine ls][0]
3. <span data-ttu-id="fd013-116">Establezca el host actual como predeterminado y configure el shell.</span><span class="sxs-lookup"><span data-stu-id="fd013-116">Set default as the current host, and configure your shell.</span></span>
   
    ```PowerShell
    docker-machine env default | Invoke-Expression
    ```
4. <span data-ttu-id="fd013-117">Vea los contenedores de Docker activos.</span><span class="sxs-lookup"><span data-stu-id="fd013-117">Display the active Docker containers.</span></span> <span data-ttu-id="fd013-118">La lista debe estar vacía.</span><span class="sxs-lookup"><span data-stu-id="fd013-118">The list should be empty.</span></span>
   
    ```PowerShell
    docker ps
    ```
   
    ![salida de docker ps][1]

> [!NOTE]
> <span data-ttu-id="fd013-120">Cada vez que reinicie el equipo de desarrollo, deberá reiniciar el host de Docker local.</span><span class="sxs-lookup"><span data-stu-id="fd013-120">Each time you reboot your development machine, you’ll need to restart your local docker host.</span></span>
> <span data-ttu-id="fd013-121">Para ello, emita el siguiente comando en un símbolo del sistema: `docker-machine start default`.</span><span class="sxs-lookup"><span data-stu-id="fd013-121">To do this, issue the following command at a command prompt: `docker-machine start default`.</span></span>
> 
> 

[0]: ./media/vs-azure-tools-docker-setup/docker-machine-ls.png
[1]: ./media/vs-azure-tools-docker-setup/docker-ps.png
