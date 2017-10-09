---
title: un host remoto de Docker de ASP.NET Core Linux Docker contenedor tooa aaaDeploy | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Visual Studio Tools para Docker toodeploy un núcleo de ASP.NET web app tooa Docker que se ejecutan en una máquina virtual Linux de Host de Azure Docker"
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
ms.openlocfilehash: 27b0c6420628c73220200bc071b47a4cd89fff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a><span data-ttu-id="ded9a-103">Implementar un host remoto de Docker ASP.NET contenedor tooa</span><span class="sxs-lookup"><span data-stu-id="ded9a-103">Deploy an ASP.NET container tooa remote Docker host</span></span>
## <a name="overview"></a><span data-ttu-id="ded9a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ded9a-104">Overview</span></span>
<span data-ttu-id="ded9a-105">Docker es un motor ligero de contenedor, similar en algunas máquinas virtuales de tooa de formas, que puede usar toohost aplicaciones y servicios.</span><span class="sxs-lookup"><span data-stu-id="ded9a-105">Docker is a lightweight container engine, similar in some ways tooa virtual machine, which you can use toohost applications and services.</span></span>
<span data-ttu-id="ded9a-106">Este tutorial le guía a través mediante hello [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensión toodeploy un host de Docker de tooa de aplicación de ASP.NET Core en Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ded9a-106">This tutorial walks you through using hello [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extension toodeploy an ASP.NET Core app tooa Docker host on Azure using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ded9a-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ded9a-107">Prerequisites</span></span>
<span data-ttu-id="ded9a-108">siguiente Hello es necesario toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="ded9a-108">hello following is required toocomplete this tutorial:</span></span>

* <span data-ttu-id="ded9a-109">Crear una máquina virtual de Azure Docker Host como se describe en [cómo máquina docker toouse con Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ded9a-109">Create an Azure Docker Host VM as described in [How toouse docker-machine with Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="ded9a-110">Instalar la versión más reciente de Hola de [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ded9a-110">Install hello latest version of [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
* <span data-ttu-id="ded9a-111">Descargar hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span><span class="sxs-lookup"><span data-stu-id="ded9a-111">Download hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)</span></span>
* <span data-ttu-id="ded9a-112">Instalar [Docker para Windows](https://docs.docker.com/docker-for-windows/install/)</span><span class="sxs-lookup"><span data-stu-id="ded9a-112">Install [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)</span></span>

## <a name="1-create-an-aspnet-core-web-app"></a><span data-ttu-id="ded9a-113">1. Cree una aplicación web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ded9a-113">1. Create an ASP.NET Core web app</span></span>
<span data-ttu-id="ded9a-114">Hello pasos siguientes le ayudarán a crear una aplicación de ASP.NET Core básica que se usará en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ded9a-114">hello following steps guide you through creating a basic ASP.NET Core app that will be used in this tutorial.</span></span>

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="ded9a-115">2. Agregue compatibilidad con Docker</span><span class="sxs-lookup"><span data-stu-id="ded9a-115">2. Add Docker support</span></span>
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a><span data-ttu-id="ded9a-116">3. Usar Script de PowerShell DockerTask.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="ded9a-116">3. Use hello DockerTask.ps1 PowerShell Script</span></span>
1. <span data-ttu-id="ded9a-117">Abra un directorio de raíz de PowerShell toohello símbolo del sistema del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ded9a-117">Open a PowerShell prompt toohello root directory of your project.</span></span> 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. <span data-ttu-id="ded9a-118">Validar Hola remoto host se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="ded9a-118">Validate hello remote host is running.</span></span> <span data-ttu-id="ded9a-119">Debería ver el estado = En ejecución</span><span class="sxs-lookup"><span data-stu-id="ded9a-119">You should see state = Running</span></span> 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. <span data-ttu-id="ded9a-120">Aplicación Hola de compilación con Hola - parámetro de compilación</span><span class="sxs-lookup"><span data-stu-id="ded9a-120">Build hello app using hello -Build parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. <span data-ttu-id="ded9a-121">Ejecutar la aplicación hello, utilizando Hola - parámetro de ejecución</span><span class="sxs-lookup"><span data-stu-id="ded9a-121">Run hello app, using hello -Run parameter</span></span>
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   <span data-ttu-id="ded9a-122">Una vez completada la docker, debería ver resultados similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="ded9a-122">Once docker completes, you should see results similar toohello following:</span></span>
   
   ![Vea la aplicación.][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
