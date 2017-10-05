---
title: Uso de io.js con aplicaciones web del Servicio de aplicaciones de Azure
description: "Aprenda a usar una aplicación web en el Servicio de aplicaciones de Azure con io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="585d5-103">Uso de io.js con aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="585d5-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="585d5-104">La popular bifurcación de nodo [io.js] tiene varias diferencias con el proyecto Node.js de Joyent, entre las que se incluyen un modelo de gobernanza más abierto, un ciclo de versiones más rápido y una adopción más rápida de características de JavaScript nuevas y experimentales.</span><span class="sxs-lookup"><span data-stu-id="585d5-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="585d5-105">Aunque Aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tiene muchas las versiones de Node.js preinstaladas, permite binarios de Node.js proporcionados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="585d5-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="585d5-106">Este artículo analiza dos métodos que habilitan el uso de io.js en Aplicaciones web del Servicio de aplicaciones: el uso de un script de implementación extendido, que configura automáticamente Azure para que use la versión de io.js más reciente disponible, así como la carga manual de un binario de io.js.</span><span class="sxs-lookup"><span data-stu-id="585d5-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="585d5-107">Uso de un script de implementación</span><span class="sxs-lookup"><span data-stu-id="585d5-107">Using a Deployment Script</span></span>
<span data-ttu-id="585d5-108">Tras la implementación de una aplicación de Node.js, Aplicaciones web del Servicio de aplicaciones ejecuta varios comandos pequeños para asegurarse de que el entorno está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="585d5-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="585d5-109">Mediante un script de implementación, este proceso se puede personalizar para que incluya la descarga y configuración de io.js.</span><span class="sxs-lookup"><span data-stu-id="585d5-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="585d5-110">El [script de implementación de io.js](https://github.com/felixrieseberg/iojs-azure) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="585d5-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="585d5-111">Para habilitar io.js en una aplicación web, solo es preciso copiar **.deployment**, **deploy.cmd** y **IISNode.yml** en la raíz de la carpeta de aplicaciones e implementarlos en Web Apps.</span><span class="sxs-lookup"><span data-stu-id="585d5-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="585d5-112">El primer archivo, **.deployment**, indica a Web Apps que ejecute **deploy.cmd** tras la implementación.</span><span class="sxs-lookup"><span data-stu-id="585d5-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="585d5-113">Este script ejecuta todos los pasos habituales de una aplicación de Node.js, pero también descarga la versión más reciente de io.js.</span><span class="sxs-lookup"><span data-stu-id="585d5-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="585d5-114">Por último, **IISNode.yml** configura Aplicaciones Web para que utilice el binario de io.js que se acaba de descargar, en lugar de un binario de Node.js preinstalado.</span><span class="sxs-lookup"><span data-stu-id="585d5-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="585d5-115">Para actualizar el binario de io.js utilizado, solo es preciso volver a implementar la aplicación (el script descargará una nueva versión de io.js cada vez que se implemente la aplicación).</span><span class="sxs-lookup"><span data-stu-id="585d5-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="585d5-116">Uso de la instalación manual</span><span class="sxs-lookup"><span data-stu-id="585d5-116">Using Manual Installation</span></span>
<span data-ttu-id="585d5-117">La instalación manual de una versión personalizada de io.js incluye solo dos pasos.</span><span class="sxs-lookup"><span data-stu-id="585d5-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="585d5-118">En primer lugar, descargue el binario **win-x64** directamente desde la [distribución de io.js].</span><span class="sxs-lookup"><span data-stu-id="585d5-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="585d5-119">Se requieren dos archivos: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="585d5-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="585d5-120">Guarde ambos archivos en una carpeta de la aplicación web, por ejemplo en **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="585d5-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="585d5-121">Para configurar Web Apps para que use **iojs.exe**, en lugar de una versión preinstalada de Node.js, cree un archivo **IISNode.yml** en la raíz de la aplicación y agregue la siguiente línea.</span><span class="sxs-lookup"><span data-stu-id="585d5-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="585d5-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="585d5-122">Next Steps</span></span>
<span data-ttu-id="585d5-123">En este artículo ha aprendido a usar io.js con Aplicaciones web del Servicio de aplicaciones utilizando tanto los scripts de implementación que se proporcionan como la instalación.</span><span class="sxs-lookup"><span data-stu-id="585d5-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="585d5-124">io.js está en pleno desarrollo y se actualiza con más frecuencia que Node.js.</span><span class="sxs-lookup"><span data-stu-id="585d5-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="585d5-125">Es posible que varios módulos Node.js no funcionen con io.js (para solucionar el problema, consulte [io.js en GitHub] ).</span><span class="sxs-lookup"><span data-stu-id="585d5-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="585d5-126">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="585d5-126">What's changed</span></span>
* <span data-ttu-id="585d5-127">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="585d5-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="585d5-128">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="585d5-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="585d5-129">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="585d5-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="585d5-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="585d5-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="585d5-131">[distribución de io.js]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="585d5-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="585d5-132">[io.js en GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="585d5-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
