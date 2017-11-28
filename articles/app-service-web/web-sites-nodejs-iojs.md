---
title: "aaaHow toouse io.js con aplicaciones de Web del servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo una aplicación web en el servicio de aplicación de Azure con io.js toouse."
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="ccc1d-103">Cómo toouse io.js con aplicaciones de Web del servicio de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="ccc1d-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="ccc1d-104">bifurcación de nodo popular de Hello [io.js] características de proyecto de Node.js del tooJoyent de diversas diferencias, incluido un modelo de gobernanza más abierto, un ciclo de versiones más rápido y una adopción más rápida de características de JavaScript de nuevo y experimental.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="ccc1d-105">Aunque Aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tiene muchas las versiones de Node.js preinstaladas, permite binarios de Node.js proporcionados por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="ccc1d-106">En este artículo se describe dos métodos de habilitar el uso de Hola de io.js en las aplicaciones de servicio Web de aplicación: Hola uso de un script de implementación extendida, que configura automáticamente la versión más reciente de io.js disponibles de Azure toouse hello, así como la carga manual de Hola de un archivo binario io.js.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="ccc1d-107">Uso de un script de implementación</span><span class="sxs-lookup"><span data-stu-id="ccc1d-107">Using a Deployment Script</span></span>
<span data-ttu-id="ccc1d-108">Durante la implementación de una aplicación Node.js, las aplicaciones de servicio Web de aplicación se ejecuta una serie de comandos pequeños tooensure que Hola entorno está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="ccc1d-109">Mediante un script de implementación, este proceso puede ser descarga de hello tooinclude personalizada y la configuración de io.js.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="ccc1d-110">Hola [io.js Script de implementación](https://github.com/felixrieseberg/iojs-azure) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="ccc1d-111">tooenable io.js en la aplicación web, simplemente copie **implementación**, **deploy.cmd** y **IISNode.yml** toohello raíz de la carpeta de la aplicación e implementar aplicaciones de tooWeb.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="ccc1d-112">primer archivo Hello, **implementación**, indica a las aplicaciones Web toorun **deploy.cmd** durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="ccc1d-113">Este script ejecuta todos los pasos habituales de Hola para una aplicación Node.js, pero también descarga la versión más reciente de Hola de io.js.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="ccc1d-114">Por último, **IISNode.yml** configura las aplicaciones Web toouse Hola simplemente descargar io.js binario en lugar de un archivo binario de Node.js previamente instalado.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc1d-115">Hola tooupdate usa io.js binario, simplemente vuelva a implementar la aplicación: script de Hola descargará una nueva versión de io.js que se implementa cada aplicación de hello sola vez.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="ccc1d-116">Uso de la instalación manual</span><span class="sxs-lookup"><span data-stu-id="ccc1d-116">Using Manual Installation</span></span>
<span data-ttu-id="ccc1d-117">instalación manual de Hola de una versión personalizada io.js incluye solo dos pasos.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="ccc1d-118">En primer lugar, descargue hello **win-x64** binario directamente desde hello [io.js distribución].</span><span class="sxs-lookup"><span data-stu-id="ccc1d-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="ccc1d-119">Se requieren dos archivos: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="ccc1d-120">Guardar los archivos tooa carpeta dentro de la aplicación web, por ejemplo en **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="ccc1d-121">tooconfigure aplicaciones Web toouse **iojs.exe** en lugar de una versión preinstalada de nodo, cree una **IISNode.yml** de archivos en la raíz de saludo de la aplicación y agregue Hola después de línea.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ccc1d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccc1d-122">Next Steps</span></span>
<span data-ttu-id="ccc1d-123">En este artículo ha aprendido cómo toouse io.js con las aplicaciones Web de aplicación de servicio, utilizando los dos proporcionan los scripts de implementación, así como la instalación manual.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="ccc1d-124">io.js está en pleno desarrollo y se actualiza con más frecuencia que Node.js.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="ccc1d-125">Es posible que varios módulos Node.js no funcionen con io.js (para solucionar el problema, consulte [io.js en GitHub] ).</span><span class="sxs-lookup"><span data-stu-id="ccc1d-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ccc1d-126">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="ccc1d-126">What's changed</span></span>
* <span data-ttu-id="ccc1d-127">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ccc1d-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="ccc1d-128">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ccc1d-129">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="ccc1d-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribución]: https://iojs.org/dist/
[io.js en GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
