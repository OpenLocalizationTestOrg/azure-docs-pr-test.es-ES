---
title: "Implementación de un contenedor de Docker de ASP.NET Core para Linux en un host remoto de Docker | Microsoft Docs"
description: "Aprenda a usar Visual Studio Tools para Docker para implementar una aplicación web de ASP.NET Core en un contenedor de Docker que se ejecute en una máquina virtual Linux de host de Docker de Azure"
services: azure-container-service
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.service: azure-container-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 4a87ee69f23779bf4f6f5db40bc05edbcfc7668d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-aspnet-container-to-a-remote-docker-host"></a><span data-ttu-id="d11f4-103">Implementación de un contenedor ASP.NET en un host remoto de Docker</span><span class="sxs-lookup"><span data-stu-id="d11f4-103">Deploy an ASP.NET container to a remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="d11f4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d11f4-104">Overview</span></span>
<span data-ttu-id="d11f4-105">Docker es un motor de contenedor ligero, semejante de alguna manera a una máquina virtual, que puede utilizar para hospedar aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="d11f4-105">Docker is a lightweight container engine, similar in some ways to a virtual machine, which you can use to host applications and services.</span></span>
<span data-ttu-id="d11f4-106">Este tutorial le guiará a través del uso de la extensión de [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) para implementar una aplicación ASP.NET Core en un host de Docker en Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d11f4-106">This tutorial walks you through using the [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension to deploy an ASP.NET Core app to a Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d11f4-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d11f4-107">Prerequisites</span></span>
<span data-ttu-id="d11f4-108">El siguiente requisito es necesario para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="d11f4-108">The following is required to complete this tutorial:</span></span>

* <span data-ttu-id="d11f4-109">Crear una VM de host de Docker de Azure tal y como se describe en [Uso de una máquina de Docker con el controlador de Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d11f4-109">Create an Azure Docker Host VM as described in [How to use docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="d11f4-110">Instalar la versión más reciente de [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="d11f4-110">Install the latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="d11f4-111">Descargar [SDK de Microsoft ASP.NET Core 1.0](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="d11f4-111">Download the [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="d11f4-112">Instalar [Docker para Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="d11f4-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="d11f4-113">1. Cree una aplicación web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d11f4-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="d11f4-114">Los siguientes pasos le guían en el proceso de creación de una aplicación ASP.NET Core básica que se usará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d11f4-114">The following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="d11f4-115">2. Agregue compatibilidad con Docker</span><span class="sxs-lookup"><span data-stu-id="d11f4-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-the-dockertaskps1-powershell-script"></a><span data-ttu-id="d11f4-116">3. Use el script de PowerShell DockerTask.ps1</span><span class="sxs-lookup"><span data-stu-id="d11f4-116">3. Use the DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="d11f4-117">Abra un símbolo del sistema de PowerShell en el directorio raíz del proyecto.</span><span class="sxs-lookup"><span data-stu-id="d11f4-117">Open a PowerShell prompt to the root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="d11f4-118">Asegúrese de que el host remoto se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="d11f4-118">Validate the remote host is running.</span></span> <span data-ttu-id="d11f4-119">Debería ver el estado = En ejecución</span><span class="sxs-lookup"><span data-stu-id="d11f4-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="d11f4-120">Compile la aplicación con el parámetro -Build</span><span class="sxs-lookup"><span data-stu-id="d11f4-120">Build the app using the -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="d11f4-121">Ejecute la aplicación mediante el parámetro -Run</span><span class="sxs-lookup"><span data-stu-id="d11f4-121">Run the app, using the -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="d11f4-122">Una vez que Docker termina, debería ver resultados similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d11f4-122">Once docker completes, you should see results similar to the following:</span></span>
   
   ![Vea la aplicación.][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
