---
title: aaaUsing entornos de prueba y los Scripts de Windows PowerShell tooPublish tooDev | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Windows PowerShell scripts de entornos de prueba y toodevelopment de toopublish de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="0573a-103">Uso de Windows PowerShell scripts de entornos de prueba y toodev de toopublish</span><span class="sxs-lookup"><span data-stu-id="0573a-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="0573a-104">Cuando crea una aplicación web en Visual Studio, puede generar un script de Windows PowerShell que puede utilizar la publicación de hello tooautomate posterior de su sitio Web tooAzure como una aplicación Web en el servicio de aplicaciones de Azure o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0573a-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="0573a-105">Puede editar y ampliar sus requisitos de script de Windows PowerShell de hello en toosuit de editor de Visual Studio de Hola o integrar script de Hola con compilación existente, prueba y scripts de publicación.</span><span class="sxs-lookup"><span data-stu-id="0573a-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="0573a-106">Mediante estos scripts, puede aprovisionar versiones personalizadas (también conocidos como entornos de desarrollo y pruebas) de su sitio para uso temporal.</span><span class="sxs-lookup"><span data-stu-id="0573a-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="0573a-107">Por ejemplo, podría configurar una versión concreta de su sitio Web en una máquina virtual de Azure o en hello ensayo ranura en un sitio Web toorun un conjunto de pruebas, reproducir un error, realizar una corrección de errores, probar un cambio propuesto o configurar un entorno personalizado para una demostración o presentación.</span><span class="sxs-lookup"><span data-stu-id="0573a-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="0573a-108">Después de crear un script que publique su proyecto, puede volver a crear entornos idénticos volviendo a ejecutar script de Hola según sea necesario, o ejecutar script de Hola con su propia compilación de su toocreate de aplicación web de un entorno de pruebas personalizado.</span><span class="sxs-lookup"><span data-stu-id="0573a-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0573a-109">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="0573a-109">What you need</span></span>
* <span data-ttu-id="0573a-110">SDK de Azure 2.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="0573a-111">Vea [Descargas de Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0573a-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="0573a-112">No es necesario secuencias de comandos de hello Azure SDK toogenerate Hola para proyectos web.</span><span class="sxs-lookup"><span data-stu-id="0573a-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="0573a-113">Esta característica es para proyectos web, no para los roles web de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="0573a-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="0573a-114">Azure PowerShell 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="0573a-115">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0573a-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="0573a-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o posterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="0573a-117">Herramientas adicionales</span><span class="sxs-lookup"><span data-stu-id="0573a-117">Additional tools</span></span>
<span data-ttu-id="0573a-118">Tiene a su disposición herramientas y recursos adicionales para trabajar con PowerShell en Visual Studio para el desarrollo de Azure.</span><span class="sxs-lookup"><span data-stu-id="0573a-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="0573a-119">Vea [Herramientas de PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="0573a-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="0573a-120">Hola de generar scripts de publicación</span><span class="sxs-lookup"><span data-stu-id="0573a-120">Generating hello publish scripts</span></span>
<span data-ttu-id="0573a-121">Puede generar Hola scripts de publicación para una máquina virtual que hospeda el sitio Web cuando se crea un nuevo proyecto siguiendo [estas instrucciones](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0573a-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="0573a-122">También puede [generar scripts de publicación para aplicaciones web en Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0573a-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="0573a-123">Scripts que genera Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0573a-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="0573a-124">Visual Studio genera una carpeta de nivel de solución denominada **PublishScripts** que contiene dos archivos de Windows PowerShell, un script de publicación de la máquina virtual o sitio Web y un módulo que contiene funciones que puede usar en hello secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="0573a-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="0573a-125">Visual Studio también genera un archivo en formato JSON de Hola que especifica los detalles de hello del proyecto de Hola que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="0573a-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="0573a-126">Script de publicación de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0573a-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="0573a-127">script de publicación de Hello contiene específico publicar los pasos para implementar la máquina virtual o sitio Web de tooa.</span><span class="sxs-lookup"><span data-stu-id="0573a-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="0573a-128">Visual Studio ofrece color de sintaxis para el desarrollo de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0573a-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="0573a-129">Ayuda para las funciones hello está disponible y puede editarlas libremente las funciones hello en hello script toosuit sus distintas necesidades.</span><span class="sxs-lookup"><span data-stu-id="0573a-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="0573a-130">Módulo de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0573a-130">Windows PowerShell module</span></span>
<span data-ttu-id="0573a-131">Windows PowerShell módulo que genera Visual Studio contiene funciones que Hola Hola publicar de script se utiliza.</span><span class="sxs-lookup"><span data-stu-id="0573a-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="0573a-132">Estas son funciones de PowerShell de Azure y no son toobe previsto modificado.</span><span class="sxs-lookup"><span data-stu-id="0573a-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="0573a-133">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0573a-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="0573a-134">Archivo de configuración de JSON</span><span class="sxs-lookup"><span data-stu-id="0573a-134">JSON configuration file</span></span>
<span data-ttu-id="0573a-135">se crea el archivo JSON de Hola Hola **configuraciones** carpeta y contiene los datos de configuración que especifica exactamente qué tooAzure toodeploy de recursos.</span><span class="sxs-lookup"><span data-stu-id="0573a-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="0573a-136">Hola de archivo hello que genera Visual Studio se denomina proyecto-nombre-WAWS-dev.json si ha creado un sitio Web o proyecto nombre-VM-dev.json si ha creado una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0573a-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="0573a-137">Este es un ejemplo de un archivo de configuración de JSON que se genera al crear un sitio web.</span><span class="sxs-lookup"><span data-stu-id="0573a-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="0573a-138">La mayoría de los valores de hello es autoexplicativo.</span><span class="sxs-lookup"><span data-stu-id="0573a-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="0573a-139">nombre del sitio Web de Hello lo genera Azure, por lo que quizás no coincida con el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="0573a-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="0573a-140">Cuando se crea una máquina virtual, archivo de configuración de JSON de hello parece similar siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="0573a-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="0573a-141">Tenga en cuenta que un servicio de nube se crea como un contenedor para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="0573a-142">máquina virtual de Hello contiene extremos habituales de hello para el acceso web a través de HTTP y HTTPS, así como los extremos de Web Deploy, que permite publicar el sitio Web de toohello desde el equipo local, escritorio remoto y Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0573a-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="0573a-143">Puede editar Hola JSON configuración toochange lo que sucede al ejecutar Hola scripts de publicación.</span><span class="sxs-lookup"><span data-stu-id="0573a-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="0573a-144">Hola `cloudService` y `virtualMachine` secciones resultan necesarias, pero se puede eliminar hello `databases` sección si no lo necesita.</span><span class="sxs-lookup"><span data-stu-id="0573a-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="0573a-145">propiedades de Hola que están vacías en el archivo de configuración predeterminado de Hola que genera Visual Studio son opcionales; los que tienen valores en el archivo de configuración predeterminado de hello son necesarios.</span><span class="sxs-lookup"><span data-stu-id="0573a-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="0573a-146">Si tiene un sitio Web con varios entornos de implementación (conocidos como espacios) en lugar de un único sitio de producción en Azure, puede incluir nombre de la ranura de hello en nombre de hello del sitio Web de hello en el archivo de configuración de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="0573a-147">Por ejemplo, si tiene un sitio Web que se denomina **misitio** y un espacio llamado **probar** , a continuación, Hola URI es misitio test.cloudapp.net, pero toouse nombre correcto de hello en el archivo de configuración de hello es mysite (Test) .</span><span class="sxs-lookup"><span data-stu-id="0573a-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="0573a-148">Sólo puede hacerlo si las ranuras y sitio Web de hello ya existen en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="0573a-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="0573a-149">Si no existen, crear sitio Web de hello mediante la ejecución de script de Hola sin especificar la ranura de Hola y luego crear ranura Hola Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), y posteriormente, ejecute el script de Hola con el nombre de sitio Web modificado Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="0573a-150">Para más información sobre las ranuras de implementación para las aplicaciones web, consulte [Configuración de entornos de ensayo para aplicaciones web en Azure App Service](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0573a-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="0573a-151">Cómo toorun Hola publicar scripts</span><span class="sxs-lookup"><span data-stu-id="0573a-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="0573a-152">Si nunca ha ejecutado un script de Windows PowerShell antes, debe establecer primero Hola ejecución directiva tooenable scripts toorun.</span><span class="sxs-lookup"><span data-stu-id="0573a-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="0573a-153">Se trata de una seguridad característica tooprevent usuarios ejecuten scripts de Windows PowerShell si son vulnerable toomalware o virus que implican la ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="0573a-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="0573a-154">Ejecutar script de Hola</span><span class="sxs-lookup"><span data-stu-id="0573a-154">Run hello script</span></span>
1. <span data-ttu-id="0573a-155">Crear paquete de Web Deploy de hello para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0573a-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="0573a-156">Un paquete de Web Deploy es un archivo comprimido (.zip) que contienen archivos que desea que sitio Web de tooyour toocopy o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0573a-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="0573a-157">Puede crear paquetes de implementación web en Visual Studio para cualquier aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0573a-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Crear paquete de implementación web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="0573a-159">Para obtener más información, vea [Cómo crear un paquete de implementación web en Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="0573a-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="0573a-160">También puede automatizar la creación de hello de su paquete de Web Deploy, tal y como se describe en la sección de hello **personalizar y extender Hola publican scripts** más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="0573a-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="0573a-161">En **el Explorador de soluciones**, abra el menú contextual de Hola para script de Hola y, a continuación, elija **abrir con PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="0573a-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="0573a-162">Si se trata de hello primera vez que ejecuta scripts de Windows PowerShell en este equipo, abra una ventana de símbolo del sistema con privilegios de administrador y Hola de tipo siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0573a-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="0573a-163">Inicie sesión en tooAzure utilizando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="0573a-164">Cuando se le solicite, escriba su nombre de usuario y su contraseña.</span><span class="sxs-lookup"><span data-stu-id="0573a-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="0573a-165">Tenga en cuenta que cuando automatiza el script de Hola, este método para proporcionar las credenciales de Azure no funcionará.</span><span class="sxs-lookup"><span data-stu-id="0573a-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="0573a-166">En su lugar, debe usar las credenciales de hello .publishsettings archivos tooprovide.</span><span class="sxs-lookup"><span data-stu-id="0573a-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="0573a-167">Una vez únicamente, use comandos de hello **Get-AzurePublishSettingsFile** hello toodownload de archivos de Azure y, posteriormente, use **importación-AzurePublishSettingsFile** archivo de hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="0573a-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="0573a-168">Para obtener instrucciones detalladas, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0573a-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="0573a-169">(Opcional) Si desea que toocreate Azure recursos como Hola virtual machine, base de datos y sitios Web sin publicar la aplicación web, utilizan hello **Publish-WebApplication.ps1** comando con hello **-configuración** establecido toohello archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="0573a-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="0573a-170">Esta línea de comandos usa toodetermine del archivo de configuración de hello JSON que toocreate de recursos.</span><span class="sxs-lookup"><span data-stu-id="0573a-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="0573a-171">Porque utiliza la configuración predeterminada de Hola para otros argumentos de línea de comandos, crea recursos de hello, pero no publica la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0573a-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="0573a-172">Hello: opción detallada proporciona más información sobre lo que está sucediendo.</span><span class="sxs-lookup"><span data-stu-id="0573a-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="0573a-173">Hola de uso **Publish-WebApplication.ps1** comando tal como se muestra en uno de la siguiente secuencia de comandos de ejemplos tooinvoke Hola de Hola y publicar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0573a-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="0573a-174">Si necesita toooverride Hola una configuración predeterminada para cualquiera de Hola otros argumentos, como el nombre de la suscripción de Hola, nombre del paquete, las credenciales de la máquina virtual o las credenciales del servidor de base de datos de publicación, puede especificar esos parámetros.</span><span class="sxs-lookup"><span data-stu-id="0573a-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="0573a-175">Hola de uso **– Verbose** opción toosee obtener más información sobre el progreso de Hola de hello proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="0573a-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="0573a-176">Si va a crear una máquina virtual, comando Hola Hola siguiente aspecto.</span><span class="sxs-lookup"><span data-stu-id="0573a-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="0573a-177">Este ejemplo también muestra cómo toospecify hello las credenciales para varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="0573a-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="0573a-178">Para las máquinas virtuales de Hola que crean estos scripts, certificado SSL de hello no es de una entidad emisora raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="0573a-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="0573a-179">Por lo tanto, debe hello toouse **– AllowUntrusted** opción.</span><span class="sxs-lookup"><span data-stu-id="0573a-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="0573a-180">script de Hola puede crear bases de datos, pero no crea servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="0573a-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="0573a-181">Si desea que toocreate un servidor de base de datos, puede usar hello **New-AzureSqlDatabaseServer** función Hola módulo de Azure.</span><span class="sxs-lookup"><span data-stu-id="0573a-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="0573a-182">Personalizar y ampliar Hola publican scripts</span><span class="sxs-lookup"><span data-stu-id="0573a-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="0573a-183">Puede personalizar Hola publicar script y el archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="0573a-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="0573a-184">Hola funciones de módulo de Windows PowerShell de hello **AzureWebAppPublishModule.psm1** no está previsto toobe modificado.</span><span class="sxs-lookup"><span data-stu-id="0573a-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="0573a-185">Si solo desea toospecify otra base de datos o cambiar algunas de las propiedades de Hola de máquina virtual de hello, edite el archivo de configuración de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="0573a-186">Si desea tooextend Hola de hello script tooautomate compilar y probar el proyecto, puede implementar códigos auxiliares de función en **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0573a-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="0573a-187">tooautomate compilar el proyecto, agregue código que llame a MSBuild demasiado`New-WebDeployPackage` tal y como se muestra en este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="0573a-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="0573a-188">Hola ruta de acceso toohello comando MSBuild es diferente según la versión de Hola de Visual Studio que tenga instalada.</span><span class="sxs-lookup"><span data-stu-id="0573a-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="0573a-189">ruta de acceso correcta de tooget hello, puede usar la función hello **Get-MSBuildCmd**, tal y como se muestra en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0573a-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="0573a-190">tooautomate compilar el proyecto</span><span class="sxs-lookup"><span data-stu-id="0573a-190">tooautomate building your project</span></span>
1. <span data-ttu-id="0573a-191">Agregar hello `$ProjectFile` parámetro en la sección de parámetros globales de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="0573a-192">Copiar función hello `Get-MSBuildCmd` en el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="0573a-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="0573a-193">Reemplace `New-WebDeployPackage` con hello código siguiente y reemplace los marcadores de posición de hello en la creación de la línea de hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="0573a-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="0573a-194">Este código es para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0573a-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="0573a-195">Si está utilizando Visual Studio 2013, cambie hello **VisualStudioVersion** la propiedad siguiente demasiado`12.0`.</span><span class="sxs-lookup"><span data-stu-id="0573a-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="0573a-196">toobuild su aplicación web, use MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="0573a-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="0573a-197">Para obtener ayuda, consulte la referencia de la línea de comandos de MSBuild en: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="0573a-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="0573a-198">Inicia la ejecución del comando de generación de Hola</span><span class="sxs-lookup"><span data-stu-id="0573a-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="0573a-199">Llamar a hello `New-WebDeployPackage` función antes de esta línea: `$Config = Read-ConfigFile $Configuration` para las aplicaciones web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="0573a-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="0573a-200">Invocar el script de Hola personalizado desde la línea de comandos mediante el paso de Hola `$Project` argumento, como en la siguiente línea de comandos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="0573a-201">tooautomate pruebas de la aplicación, agregue código demasiado`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="0573a-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="0573a-202">Estar seguro de toouncomment líneas de hello en **Publish-WebApplication.ps1** donde se llaman a estas funciones.</span><span class="sxs-lookup"><span data-stu-id="0573a-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="0573a-203">Si no proporciona una implementación, puede crear manualmente el proyecto con Visual Studio y, a continuación, ejecución Hola publicar script toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0573a-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="0573a-204">Publicación del resumen de la función</span><span class="sxs-lookup"><span data-stu-id="0573a-204">Publishing function summary</span></span>
<span data-ttu-id="0573a-205">Ayuda de tooget para las funciones que puede usar en línea de comandos de Windows PowerShell de hello, use el comando de hello `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="0573a-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="0573a-206">Ayuda de Hello incluye la ayuda sobre parámetros y ejemplos.</span><span class="sxs-lookup"><span data-stu-id="0573a-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="0573a-207">Hola mismo texto de ayuda también está en archivos de origen de la secuencia de comandos de hello, **AzureWebAppPublishModule.psm1** y **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="0573a-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="0573a-208">Ayuda y script de Hola está localizado en el idioma de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0573a-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="0573a-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="0573a-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="0573a-210">Nombre de función</span><span class="sxs-lookup"><span data-stu-id="0573a-210">Function name</span></span> | <span data-ttu-id="0573a-211">Description</span><span class="sxs-lookup"><span data-stu-id="0573a-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0573a-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="0573a-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="0573a-213">Crea una nueva base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="0573a-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="0573a-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="0573a-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="0573a-215">Crea las bases de datos de SQL Azure a partir de valores de hello en el archivo de configuración de JSON de Hola que genera Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0573a-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="0573a-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="0573a-216">Add-AzureVM</span></span> |<span data-ttu-id="0573a-217">Crea una máquina virtual de Azure y devuelve la que dirección URL de Hola de hello implementa VM.</span><span class="sxs-lookup"><span data-stu-id="0573a-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="0573a-218">Hello función configura los requisitos previos de hello y, a continuación, Hola llamadas **New-AzureVM** función toocreate (módulo de Azure) una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0573a-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="0573a-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="0573a-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="0573a-220">Agrega la nueva máquina virtual de tooa los extremos de entrada y devuelve la máquina virtual de hello con nuevo extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="0573a-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="0573a-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="0573a-222">Crea una nueva cuenta de almacenamiento de Azure en la suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="0573a-223">nombre de Hola de cuenta de hello comienza por "devtest" seguido de una cadena alfanumérica única.</span><span class="sxs-lookup"><span data-stu-id="0573a-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="0573a-224">función Hello devuelve nombre de Hola de hello nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0573a-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="0573a-225">Debe especificar una ubicación o un grupo de afinidad para la nueva cuenta de almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="0573a-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="0573a-226">Add-AzureWebsite</span></span> |<span data-ttu-id="0573a-227">Crea un sitio Web con la ubicación y el nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="0573a-228">Esta función llama hello **New-AzureWebsite** función Hola módulo de Azure.</span><span class="sxs-lookup"><span data-stu-id="0573a-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="0573a-229">Si la suscripción de hello ya no incluye un sitio Web con el nombre especificado de hello, esta función crea el sitio Web de Hola y devuelve un objeto de sitio Web.</span><span class="sxs-lookup"><span data-stu-id="0573a-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="0573a-230">De lo contrario, devuelve `$null`.</span><span class="sxs-lookup"><span data-stu-id="0573a-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="0573a-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="0573a-231">Backup-Subscription</span></span> |<span data-ttu-id="0573a-232">Guarda Hola suscripción de Azure actual en hello `$Script:originalSubscription` variable en el ámbito del script. Esta función guarda la suscripción actual de Azure hello (obtenida por `Get-AzureSubscription -Current`) y su cuenta de almacenamiento y Hola suscripción cambiada por este script (almacenada en la variable de hello `$UserSpecifiedSubscription`) y su cuenta de almacenamiento, en el ámbito del script.</span><span class="sxs-lookup"><span data-stu-id="0573a-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="0573a-233">Al guardar los valores de hello, puede usar una función, como `Restore-Subscription`, toorestore Hola original suscripción y almacenamiento cuenta toocurrent estado actual si ha cambiado el estado actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="0573a-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="0573a-234">Find-AzureVM</span></span> |<span data-ttu-id="0573a-235">Hola obtiene especifica la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="0573a-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="0573a-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="0573a-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="0573a-237">Antepone el mensaje de tooa de fecha y hora de saludo.</span><span class="sxs-lookup"><span data-stu-id="0573a-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="0573a-238">Esta función está diseñada para mensajes escritos toohello flujos de Error y detallado.</span><span class="sxs-lookup"><span data-stu-id="0573a-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="0573a-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="0573a-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="0573a-240">Ensambla una base de datos de SQL Azure de conexión cadena tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="0573a-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="0573a-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="0573a-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="0573a-242">Devuelve Hola nombre de cuenta de almacenamiento primera Hola con patrón de nombre de Hola "devtest*" (entre mayúsculas y minúsculas) Hola ubicación o la afinidad del grupo especificado. Si hello "devtest*" cuenta de almacenamiento no coincide con la ubicación de Hola o el grupo de afinidad, función hello pasa por alto.</span><span class="sxs-lookup"><span data-stu-id="0573a-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="0573a-243">Debe especificar una ubicación o un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="0573a-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="0573a-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="0573a-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="0573a-245">Devuelve una herramienta de comando toorun hello MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="0573a-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="0573a-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="0573a-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="0573a-247">Busca o crea una máquina virtual en la suscripción de Hola que coincide con los valores de hello en el archivo de configuración de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="0573a-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="0573a-248">Publish-WebPackage</span></span> |<span data-ttu-id="0573a-249">Utiliza MsDeploy.exe y un servidor web publican el paquete. ZIP archivo toodeploy recursos tooa el sitio Web.</span><span class="sxs-lookup"><span data-stu-id="0573a-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="0573a-250">Esta función no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="0573a-250">This function doesn't generate any output.</span></span> <span data-ttu-id="0573a-251">Si se produce un error en hello llamada tooMSDeploy.exe, función hello produce una excepción.</span><span class="sxs-lookup"><span data-stu-id="0573a-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="0573a-252">tooget más detallados de salida, use hello **-Verbose** opción.</span><span class="sxs-lookup"><span data-stu-id="0573a-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="0573a-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="0573a-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="0573a-254">Comprueba los valores de parámetro hello y, a continuación, llama a hello **Publish-WebPackage** función.</span><span class="sxs-lookup"><span data-stu-id="0573a-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="0573a-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0573a-255">Read-ConfigFile</span></span> |<span data-ttu-id="0573a-256">Valida el archivo de configuración de JSON de Hola y devuelve una tabla hash de valores seleccionados.</span><span class="sxs-lookup"><span data-stu-id="0573a-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="0573a-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="0573a-257">Restore-Subscription</span></span> |<span data-ttu-id="0573a-258">Restablece la suscripción original de hello actual suscripción toohello.</span><span class="sxs-lookup"><span data-stu-id="0573a-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="0573a-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="0573a-259">Test-AzureModule</span></span> |<span data-ttu-id="0573a-260">Devuelve `$true` si la versión del módulo de Azure de hello instalado es 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="0573a-261">Devuelve `$false` si el módulo de hello no está instalado o tiene una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="0573a-262">Esta función no tiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="0573a-262">This function has no parameters.</span></span> |
| <span data-ttu-id="0573a-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="0573a-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="0573a-264">Devuelve `$true` si la versión de Hola de hello módulo de Azure es 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="0573a-265">Devuelve `$false` si el módulo de hello no está instalado o tiene una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="0573a-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="0573a-266">Esta función no tiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="0573a-266">This function has no parameters.</span></span> |
| <span data-ttu-id="0573a-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="0573a-267">Test-HttpsUrl</span></span> |<span data-ttu-id="0573a-268">Convierte el objeto de hello entrada URL tooa System.Uri.</span><span class="sxs-lookup"><span data-stu-id="0573a-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="0573a-269">Devuelve `$True` si Hola URL es absoluta y su esquema es https.</span><span class="sxs-lookup"><span data-stu-id="0573a-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="0573a-270">Devuelve `$false` si hello es relativa, su esquema no es HTTPS o cadena de entrada de hello no puede ser la dirección URL de tooa convertido.</span><span class="sxs-lookup"><span data-stu-id="0573a-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="0573a-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="0573a-271">Test-Member</span></span> |<span data-ttu-id="0573a-272">Devuelve `$true` si una propiedad o método es un miembro del objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="0573a-273">De lo contrario, devuelve `$false`.</span><span class="sxs-lookup"><span data-stu-id="0573a-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="0573a-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="0573a-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="0573a-275">Escribe un mensaje de error prefijado con hello hora actual.</span><span class="sxs-lookup"><span data-stu-id="0573a-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="0573a-276">Esta función llama hello **Format-DevTestMessageWithTime** tiempo de función tooprepend Hola antes de escribir la secuencia de Error de toohello de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0573a-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="0573a-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="0573a-277">Write-HostWithTime</span></span> |<span data-ttu-id="0573a-278">Escribe un programa de host de mensaje toohello (**Write-Host**) como prefijo Hola hora actual.</span><span class="sxs-lookup"><span data-stu-id="0573a-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="0573a-279">efecto de Hello de la escritura de programa de host toohello varía.</span><span class="sxs-lookup"><span data-stu-id="0573a-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="0573a-280">Mayoría de los programas que hospedan Windows PowerShell escribe estos mensajes toostandard salida.</span><span class="sxs-lookup"><span data-stu-id="0573a-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="0573a-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="0573a-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="0573a-282">Escribe un mensaje detallado prefijado con hello hora actual.</span><span class="sxs-lookup"><span data-stu-id="0573a-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="0573a-283">Dado que llama **Write-Verbose**, mensajes de bienvenida muestra solo cuando se ejecuta el script de Hola con hello **detallado** parámetro o cuando Hola **VerbosePreference** preferencia es establecer demasiado**continuar**.</span><span class="sxs-lookup"><span data-stu-id="0573a-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="0573a-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="0573a-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="0573a-285">Nombre de función</span><span class="sxs-lookup"><span data-stu-id="0573a-285">Function name</span></span> | <span data-ttu-id="0573a-286">Description</span><span class="sxs-lookup"><span data-stu-id="0573a-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0573a-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="0573a-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="0573a-288">Crea recursos de Azure, como un sitio web o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0573a-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="0573a-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="0573a-289">New-WebDeployPackage</span></span> |<span data-ttu-id="0573a-290">Esta función no está implementada.</span><span class="sxs-lookup"><span data-stu-id="0573a-290">This function isn't implemented.</span></span> <span data-ttu-id="0573a-291">Puede agregar comandos en esta función toobuild el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0573a-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="0573a-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="0573a-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="0573a-293">Publica un tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0573a-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="0573a-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="0573a-294">Publish-WebApplication</span></span> |<span data-ttu-id="0573a-295">Crea e implementa aplicaciones web, máquinas virtuales, bases de datos SQL y cuentas de almacenamiento para un proyecto web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0573a-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="0573a-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="0573a-296">Test-WebApplication</span></span> |<span data-ttu-id="0573a-297">Esta función no está implementada.</span><span class="sxs-lookup"><span data-stu-id="0573a-297">This function isn't implemented.</span></span> <span data-ttu-id="0573a-298">Puede agregar comandos en esta tootest de función de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0573a-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0573a-299">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0573a-299">Next steps</span></span>
<span data-ttu-id="0573a-300">Más información acerca de los scripts de PowerShell leyendo [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) y ver otras secuencias de comandos de PowerShell de Azure en hello [centro de scripts de](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="0573a-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
