---
title: "aaaSpecifying una Node.js versión"
description: "Obtenga información acerca de cómo toospecify Hola versión de Node.js utilizado por los sitios Web y servicios en la nube"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="db582-103">Especificación de una versión de Node.js en una aplicación Azure</span><span class="sxs-lookup"><span data-stu-id="db582-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="db582-104">Al hospedar una aplicación Node.js, puede que desee tooensure que la aplicación usa una versión específica de Node.js.</span><span class="sxs-lookup"><span data-stu-id="db582-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="db582-105">Hay varias tooaccomplish formas esto para las aplicaciones hospedadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="db582-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="db582-106">Versiones predeterminadas</span><span class="sxs-lookup"><span data-stu-id="db582-106">Default versions</span></span>
<span data-ttu-id="db582-107">versiones de Node.js Hola proporcionadas por Azure se actualizan constantemente.</span><span class="sxs-lookup"><span data-stu-id="db582-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="db582-108">A menos que se especifique lo contrario, Hola versión predeterminada que se especifica en hello `WEBSITE_NODE_DEFAULT_VERSION` se usará la variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="db582-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="db582-109">toooverride este valor predeterminado, siga los pasos de hello en las secciones siguientes de este artículo</span><span class="sxs-lookup"><span data-stu-id="db582-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="db582-110">Si se hospeda la aplicación en un servicio de nube de Azure (rol web o de trabajo) y es Hola primera vez que se ha implementado la aplicación hello, Azure intentará toouse Hola la misma versión de Node.js tal y como se ha instalado en el entorno de desarrollo si se coincide con uno de versiones predeterminadas de hello disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="db582-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="db582-111">Control de versiones con package.json</span><span class="sxs-lookup"><span data-stu-id="db582-111">Versioning with package.json</span></span>
<span data-ttu-id="db582-112">Puede especificar la versión de Hola de toobe de Node.js usa agregando Hola después tooyour **package.json** archivo:</span><span class="sxs-lookup"><span data-stu-id="db582-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="db582-113">Donde *versión* es toouse de número de versión específica de Hola.</span><span class="sxs-lookup"><span data-stu-id="db582-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="db582-114">Puede especificar condiciones más complejas para la versión, como:</span><span class="sxs-lookup"><span data-stu-id="db582-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="db582-115">Puesto que 0.6.22 no es uno de las versiones de hello disponibles en el entorno de hospedaje de hello, hello versión más reciente de hello 0,8 serie en la que está disponible será usa en su lugar - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="db582-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="db582-116">Control de versiones de sitios web con configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="db582-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="db582-117">Si hospeda la aplicación hello en un sitio Web, puede establecer la variable de entorno de hello **WEBSITE_NODE_DEFAULT_VERSION** toohello versión que desee.</span><span class="sxs-lookup"><span data-stu-id="db582-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="db582-118">Control de versiones de Servicios en la nube con PowerShell</span><span class="sxs-lookup"><span data-stu-id="db582-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="db582-119">Si hospeda la aplicación hello en un servicio de nube y a implementar la aplicación hello mediante Azure PowerShell, puede invalidar versión Node.js de hello predeterminada mediante el uso de hello **AzureServiceProjectRole conjunto** cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="db582-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="db582-120">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="db582-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="db582-121">Parámetros de nota Hola Hola encima de instrucción distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="db582-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="db582-122">Puede comprobar la versión correcta de Hola de Node.js se ha seleccionado mediante la comprobación de hello **motores** propiedad en su rol **package.json**.</span><span class="sxs-lookup"><span data-stu-id="db582-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="db582-123">También puede usar hello **AzureServiceProjectRoleRuntime Get** tooretrieve una lista de versiones de Node.js disponibles para las aplicaciones hospedadas como un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="db582-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="db582-124">Compruebe siempre la versión de Hola de Node.js que depende su proyecto está en esta lista.</span><span class="sxs-lookup"><span data-stu-id="db582-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="db582-125">Uso de una versión personalizada con Sitios web Azure</span><span class="sxs-lookup"><span data-stu-id="db582-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="db582-126">Aunque Azure proporciona varias versiones predeterminadas de Node.js, puede querer toouse una versión que no se proporciona de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="db582-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="db582-127">Si la aplicación se hospeda como un sitio Web de Azure, puede hacerlo mediante el uso de hello **iisnode.yml** archivo.</span><span class="sxs-lookup"><span data-stu-id="db582-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="db582-128">Hello pasos siguientes guiarán a través del proceso de Hola de uso de una versión personalizada de Node.Js con un sitio Web de Azure:</span><span class="sxs-lookup"><span data-stu-id="db582-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="db582-129">Crear un nuevo directorio y, a continuación, cree un **server.js** archivo dentro del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="db582-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="db582-130">Hola **server.js** archivo debe contener la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="db582-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="db582-131">Se mostrará la versión de Node.js de Hola que se va a utilizar al examinar el sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="db582-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="db582-132">Crear un nuevo sitio Web y un nombre de hello nota del sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="db582-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="db582-133">Por ejemplo, la siguiente hello usa hello [herramientas de línea de comandos de Azure] toocreate un nuevo sitio Web de Azure denominado **MiSitioWeb**y, a continuación, habilitar un repositorio Git del sitio Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="db582-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="db582-134">Crear un nuevo directorio denominado **bin** como un elemento secundario del directorio de Hola que contiene hello **server.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="db582-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="db582-135">Descargar la versión específica de Hola de **node.exe** (versión de Windows hello) que desea toouse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db582-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="db582-136">Por ejemplo, Hola después usa **curl** versión toodownload 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="db582-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="db582-137">Guardar hello **node.exe** archivo en hello **bin** carpeta creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="db582-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="db582-138">Crear un **iisnode.yml** en el archivo hello mismo directorio como hello **server.js** de archivos y después agregue Hola después toohello contenido **iisnode.yml** archivo:</span><span class="sxs-lookup"><span data-stu-id="db582-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="db582-139">Esta ruta de acceso es donde hello **node.exe** archivo dentro del proyecto se ubicarán después de publicar el sitio Web de Azure toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="db582-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="db582-140">Publique la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db582-140">Publish your application.</span></span> <span data-ttu-id="db582-141">Por ejemplo, puesto que he creado un nuevo sitio Web anteriormente con el parámetro de git: Hola, hello siguientes comandos se Agregar repositorio de Git local de hello aplicación archivos toomy e insertarlas repositorio del sitio Web de toohello:</span><span class="sxs-lookup"><span data-stu-id="db582-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="db582-142">Después de que ha publicado la aplicación hello, abrir sitio Web de hello en un explorador.</span><span class="sxs-lookup"><span data-stu-id="db582-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="db582-143">Debe aparecer un mensaje que diga "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="db582-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="db582-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db582-144">Next Steps</span></span>
<span data-ttu-id="db582-145">Ahora que sabe cómo utiliza la versión de Hola de toospecify de Node.js por la aplicación, obtenga información acerca de cómo demasiado[trabajar con módulos], [compilar e implementar un sitio Web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), y [cómo toouse hello Azure Herramientas de línea de comandos para Mac y Linux].</span><span class="sxs-lookup"><span data-stu-id="db582-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="db582-146">Para obtener más información, vea hello [Centro para desarrolladores de Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="db582-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[cómo toouse hello Azure Herramientas de línea de comandos para Mac y Linux]:cli-install-nodejs.md
[herramientas de línea de comandos de Azure]:cli-install-nodejs.md
[trabajar con módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
