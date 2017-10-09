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
# <a name="deploy-an-aspnet-container-tooa-remote-docker-host"></a>Implementar un host remoto de Docker ASP.NET contenedor tooa
## <a name="overview"></a>Información general
Docker es un motor ligero de contenedor, similar en algunas máquinas virtuales de tooa de formas, que puede usar toohost aplicaciones y servicios.
Este tutorial le guía a través mediante hello [Visual Studio Tools para Docker](https://docs.microsoft.com/en-us/dotnet/articles/core/docker/visual-studio-tools-for-docker) extensión toodeploy un host de Docker de tooa de aplicación de ASP.NET Core en Azure con PowerShell.

## <a name="prerequisites"></a>Requisitos previos
siguiente Hello es necesario toocomplete este tutorial:

* Crear una máquina virtual de Azure Docker Host como se describe en [cómo máquina docker toouse con Azure](virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Instalar la versión más reciente de Hola de [Visual Studio](https://www.visualstudio.com/downloads/)
* Descargar hello [Microsoft ASP.NET Core 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)
* Instalar [Docker para Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="1-create-an-aspnet-core-web-app"></a>1. Cree una aplicación web ASP.NET Core
Hello pasos siguientes le ayudarán a crear una aplicación de ASP.NET Core básica que se usará en este tutorial.

[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Agregue compatibilidad con Docker
[!INCLUDE [create-aspnet5-app](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-use-hello-dockertaskps1-powershell-script"></a>3. Usar Script de PowerShell DockerTask.ps1 hello
1. Abra un directorio de raíz de PowerShell toohello símbolo del sistema del proyecto. 
   
   ```
   PS C:\Src\WebApplication1>
   ```
2. Validar Hola remoto host se está ejecutando. Debería ver el estado = En ejecución 
   
   ```
   docker-machine ls
   NAME         ACTIVE   DRIVER   STATE     URL                        SWARM   DOCKER    ERRORS
   MyDockerHost -        azure    Running   tcp://xxx.xxx.xxx.xxx:2376         v1.10.3
   ```
   
3. Aplicación Hola de compilación con Hola - parámetro de compilación
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release -Machine mydockerhost
   ```  

   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Build -Environment Release 
   > ```  
   > 
   > 
4. Ejecutar la aplicación hello, utilizando Hola - parámetro de ejecución
   
   ```
   PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release -Machine mydockerhost
   ```
   
   > ```
   > PS C:\Src\WebApplication1> .\Docker\DockerTask.ps1 -Run -Environment Release 
   > ```
   > 
   > 
   
   Una vez completada la docker, debería ver resultados similares toohello siguiente:
   
   ![Vea la aplicación.][3]

[0]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/docker-props-in-solution-explorer.png
[1]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/change-docker-machine-name.png
[2]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/launch-application.png
[3]:./media/vs-azure-tools-docker-hosting-web-apps-in-docker/view-application.png
