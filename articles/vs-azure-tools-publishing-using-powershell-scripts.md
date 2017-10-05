---
title: "Usar scripts de Windows PowerShell para la publicación en entornos de desarrollo y pruebas | Microsoft Docs"
description: Aprenda a utilizar scripts de Windows PowerShell desde Visual Studio para publicar entornos de prueba y desarrollo.
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="e75b3-103">Utilizar scripts de Windows PowerShell para la publicación en entornos de desarrollo y pruebas</span><span class="sxs-lookup"><span data-stu-id="e75b3-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="e75b3-104">Al crear una aplicación web en Visual Studio, puede generar un script de Windows PowerShell que puede usar posteriormente para automatizar la publicación de su sitio Web en Azure como aplicación web en el Servicio de aplicaciones de Azure o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="e75b3-105">Puede editar y ampliar el script de Windows PowerShell en el editor de Visual Studio para adaptarse a sus requisitos o integrar el script con los scripts de compilación, pruebas y publicación existentes.</span><span class="sxs-lookup"><span data-stu-id="e75b3-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="e75b3-106">Mediante estos scripts, puede aprovisionar versiones personalizadas (también conocidos como entornos de desarrollo y pruebas) de su sitio para uso temporal.</span><span class="sxs-lookup"><span data-stu-id="e75b3-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="e75b3-107">Por ejemplo, podría configurar una versión concreta de su sitio web en una máquina virtual de Azure o en la ranura de ensayo de un sitio web para ejecutar un conjunto de pruebas, reproducir un error, probar una corrección de errores, realizar una versión de prueba de un cambio propuesto o configurar un entorno personalizado para una demo o presentación.</span><span class="sxs-lookup"><span data-stu-id="e75b3-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="e75b3-108">Cuando haya creado un script que publique el proyecto, puede volver a crear entornos idénticos volviendo a ejecutar el script según sea necesario, o ejecutar el script con su propia versión de la aplicación web para crear un entorno personalizado para pruebas.</span><span class="sxs-lookup"><span data-stu-id="e75b3-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e75b3-109">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="e75b3-109">What you need</span></span>
* <span data-ttu-id="e75b3-110">SDK de Azure 2.3 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="e75b3-111">Vea [Descargas de Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e75b3-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="e75b3-112">No necesita el SDK de Azure para generar los scripts para proyectos web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="e75b3-113">Esta característica es para proyectos web, no para los roles web de servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="e75b3-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="e75b3-114">Azure PowerShell 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="e75b3-115">Para obtener más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="e75b3-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e75b3-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o posterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="e75b3-117">Herramientas adicionales</span><span class="sxs-lookup"><span data-stu-id="e75b3-117">Additional tools</span></span>
<span data-ttu-id="e75b3-118">Tiene a su disposición herramientas y recursos adicionales para trabajar con PowerShell en Visual Studio para el desarrollo de Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="e75b3-119">Vea [Herramientas de PowerShell para Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="e75b3-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="e75b3-120">Generación de los scripts de publicación</span><span class="sxs-lookup"><span data-stu-id="e75b3-120">Generating the publish scripts</span></span>
<span data-ttu-id="e75b3-121">Puede generar los scripts de publicación para una máquina virtual que hospeda el sitio web al crea un nuevo proyecto siguiendo [estas instrucciones](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e75b3-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e75b3-122">También puede [generar scripts de publicación para aplicaciones web en Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e75b3-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="e75b3-123">Scripts que genera Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e75b3-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="e75b3-124">Visual Studio genera una carpeta de nivel de solución denominada **PublishScripts** que contiene dos archivos de Windows PowerShell, un script de publicación para su máquina virtual o sitio web, y un módulo que contiene funciones que puede usar en los scripts.</span><span class="sxs-lookup"><span data-stu-id="e75b3-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="e75b3-125">Visual Studio también genera un archivo en el formato JSON que especifica los detalles del proyecto que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="e75b3-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="e75b3-126">Script de publicación de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e75b3-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="e75b3-127">El script de publicación contiene pasos de publicación específicos para la implementación en un sitio web o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="e75b3-128">Visual Studio ofrece color de sintaxis para el desarrollo de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e75b3-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="e75b3-129">La Ayuda para las funciones está disponible y puede editar libremente las funciones en el script para satisfacer sus cambiantes requisitos.</span><span class="sxs-lookup"><span data-stu-id="e75b3-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="e75b3-130">Módulo de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e75b3-130">Windows PowerShell module</span></span>
<span data-ttu-id="e75b3-131">El módulo de Windows PowerShell que Visual Studio genera contiene funciones que el script de publicación usa.</span><span class="sxs-lookup"><span data-stu-id="e75b3-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="e75b3-132">Estas son funciones de Azure PowerShell y no están pensadas para modificarse.</span><span class="sxs-lookup"><span data-stu-id="e75b3-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="e75b3-133">Para obtener más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="e75b3-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="e75b3-134">Archivo de configuración de JSON</span><span class="sxs-lookup"><span data-stu-id="e75b3-134">JSON configuration file</span></span>
<span data-ttu-id="e75b3-135">El archivo JSON se crea en la carpeta **Configuraciones** y contiene datos de configuración que especifican exactamente qué recursos se implementarán en Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="e75b3-136">El nombre del archivo que Visual Studio genera es project-name-WAWS-dev.json si ha creado un sitio web o  project name-VM-dev.json, si ha creado una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="e75b3-137">Este es un ejemplo de un archivo de configuración de JSON que se genera al crear un sitio web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="e75b3-138">La mayor parte de los valores se explican por sí solos.</span><span class="sxs-lookup"><span data-stu-id="e75b3-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="e75b3-139">El nombre del sitio web se genera por Azure, por lo que es posible que no coincida con el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="e75b3-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="e75b3-140">Cuando crea una máquina virtual, el archivo de configuración de JSON es similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="e75b3-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="e75b3-141">Tenga en cuenta que se crea un servicio en la nube como un contenedor para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="e75b3-142">La máquina virtual contiene los extremos habituales para el acceso web a través de HTTP y HTTPS, así como extremos para Web Deploy, lo que le permite publicar en el sitio web desde su equipo local, Escritorio remoto y Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e75b3-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="e75b3-143">Puede editar la configuración de JSON para cambiar lo que ocurre al ejecutar los scripts de publicación.</span><span class="sxs-lookup"><span data-stu-id="e75b3-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="e75b3-144">Las secciones `cloudService` y `virtualMachine` son necesarias, pero puede eliminar la sección `databases` si no la necesita.</span><span class="sxs-lookup"><span data-stu-id="e75b3-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="e75b3-145">Las propiedades que están vacías en el archivo de configuración predeterminado que Visual Studio genera son opcionales; se requieren las que tienen valores en el archivo de configuración predeterminado.</span><span class="sxs-lookup"><span data-stu-id="e75b3-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="e75b3-146">Si tiene un sitio web que cuenta con varios entornos de implementación (conocidos como ranuras) en lugar de un único sitio de producción en Azure, puede incluir el nombre de la ranura en el nombre del sitio web en el archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="e75b3-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="e75b3-147">Por ejemplo, si tiene un sitio web llamado **mysite** y una ranura para él llamada **test**, el URI es mysite-test.cloudapp.net, pero el nombre correcto que se usará en el archivo de configuración es mysite(test).</span><span class="sxs-lookup"><span data-stu-id="e75b3-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="e75b3-148">Solo puede hacerlo si el sitio web y las ranuras ya existen en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e75b3-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="e75b3-149">De no ser así, cree el sitio web ejecutando el script sin especificar la ranura y luego créela en el [Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885); después ejecute el script con el nombre del sitio web modificado.</span><span class="sxs-lookup"><span data-stu-id="e75b3-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="e75b3-150">Para más información sobre las ranuras de implementación para las aplicaciones web, consulte [Configuración de entornos de ensayo para aplicaciones web en Azure App Service](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e75b3-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="e75b3-151">Cómo ejecutar los scripts de publicación</span><span class="sxs-lookup"><span data-stu-id="e75b3-151">How to run the publish scripts</span></span>
<span data-ttu-id="e75b3-152">Si nunca ha ejecutado un script de Windows PowerShell antes, debe establecer primero la directiva de ejecución para habilitar la ejecución de los scripts.</span><span class="sxs-lookup"><span data-stu-id="e75b3-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="e75b3-153">Se trata de una característica de seguridad para evitar que los usuarios ejecuten scripts de Windows PowerShell si son vulnerables a malware o virus que implican la ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="e75b3-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="e75b3-154">Ejecute el script</span><span class="sxs-lookup"><span data-stu-id="e75b3-154">Run the script</span></span>
1. <span data-ttu-id="e75b3-155">Cree el paquete de implementación web para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e75b3-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="e75b3-156">Un paquete de Web Deploy es un archivo comprimido (archivo .zip) que contiene archivos que quiere copiar en el sitio web o máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="e75b3-157">Puede crear paquetes de implementación web en Visual Studio para cualquier aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Crear paquete de implementación web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="e75b3-159">Para obtener más información, vea [Cómo crear un paquete de implementación web en Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="e75b3-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="e75b3-160">También puede automatizar la creación de su paquete de Web Deploy, como se describe en la sección **Personalización y ampliación de los scripts de publicación** más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="e75b3-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="e75b3-161">En el **Explorador de soluciones**, abra el menú contextual para el script y luego elija **Abrir con PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="e75b3-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="e75b3-162">Si es la primera vez que ha ejecutado scripts de Windows PowerShell en este equipo, abra una ventana de símbolo del sistema con privilegios de administrador y escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e75b3-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="e75b3-163">Inicie sesión en Azure con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="e75b3-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="e75b3-164">Cuando se le solicite, escriba su nombre de usuario y su contraseña.</span><span class="sxs-lookup"><span data-stu-id="e75b3-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="e75b3-165">Tenga en cuenta que al automatizar el script, este método de ofrecer credenciales de Azure no funcionará.</span><span class="sxs-lookup"><span data-stu-id="e75b3-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="e75b3-166">En su lugar, debe usar el archivo .publishsettings para ofrecer las credenciales.</span><span class="sxs-lookup"><span data-stu-id="e75b3-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="e75b3-167">Una sola vez, use el comando **Get-AzurePublishSettingsFile** para descargar el archivo de Azure y después use **Import-AzurePublishSettingsFile** para importar el archivo.</span><span class="sxs-lookup"><span data-stu-id="e75b3-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="e75b3-168">Para obtener instrucciones detalladas, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e75b3-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="e75b3-169">(Opcional) Si quiere crear recursos de Azure como la máquina virtual, la base de datos y el sitio web sin publicar su aplicación web, use el comando **Publish-WebApplication.ps1** con el argumento **-Configuration** establecido en el archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="e75b3-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="e75b3-170">Esta línea de comandos usa el archivo de configuración de JSON para determinar qué recursos se crearán.</span><span class="sxs-lookup"><span data-stu-id="e75b3-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="e75b3-171">Dado que usa la configuración predeterminada para los demás argumentos de línea de comandos, crea los recursos, pero no publica su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="e75b3-172">La opción –Verbose le ofrece más información sobre lo que ocurre.</span><span class="sxs-lookup"><span data-stu-id="e75b3-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="e75b3-173">Use el comando **Publish-WebApplication.ps1** como se muestra en uno de los ejemplos siguientes para invocar al script y publicar su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="e75b3-174">Si necesita invalidar la configuración predeterminada para cualquiera de los demás argumentos, como el nombre de la suscripción, el nombre del paquete de publicación, las credenciales de máquina virtual o las credenciales de servidor de base de datos, puede especificar esos parámetros.</span><span class="sxs-lookup"><span data-stu-id="e75b3-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="e75b3-175">Use la opción **–Verbose** opción para ver más información sobre el progreso del proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="e75b3-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="e75b3-176">Si está creando una máquina virtual, el comando es similar a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e75b3-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="e75b3-177">En este ejemplo también se muestra cómo especificar las credenciales para varias bases de datos.</span><span class="sxs-lookup"><span data-stu-id="e75b3-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="e75b3-178">Para las máquinas virtuales que se estos scripts crean, el certificado de SSL no procede de una entidad de certificación raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="e75b3-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="e75b3-179">Por lo tanto, debe usar la opción **–AllowUntrusted** .</span><span class="sxs-lookup"><span data-stu-id="e75b3-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="e75b3-180">El script puede crear bases de datos, pero no crea servidores de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="e75b3-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="e75b3-181">Si quiere crear un servidor de base de datos, puede usar la función **New-AzureSqlDatabaseServer** en el módulo de Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="e75b3-182">Personalización y ampliación de los scripts de publicación</span><span class="sxs-lookup"><span data-stu-id="e75b3-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="e75b3-183">Puede personalizar el script de publicación y el archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="e75b3-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="e75b3-184">Las funciones del módulo Windows PowerShell **AzureWebAppPublishModule.psm1** no están pensadas para modificarse.</span><span class="sxs-lookup"><span data-stu-id="e75b3-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="e75b3-185">Si quiere especificar una base de datos diferente o cambiar algunas de las propiedades de la máquina virtual, edite el archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="e75b3-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="e75b3-186">Si quiere ampliar la funcionalidad del script para automatizar la creación y las prueba de su proyecto, puede implementar códigos auxiliares de funciones en **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e75b3-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="e75b3-187">Para automatizar la creación de su proyecto, agregue código que llame a MSBuild en `New-WebDeployPackage` como se muestra en este ejemplo de código.</span><span class="sxs-lookup"><span data-stu-id="e75b3-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="e75b3-188">La ruta de acceso al comando MSBuild es diferente en función de la versión de Visual Studio que ha instalado.</span><span class="sxs-lookup"><span data-stu-id="e75b3-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="e75b3-189">Para obtener la ruta de acceso correcta, puede usar la función **Get-MSBuildCmd**, como se muestra en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e75b3-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="e75b3-190">Para automatizar la creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="e75b3-190">To automate building your project</span></span>
1. <span data-ttu-id="e75b3-191">Agregue el parámetro `$ProjectFile` en la sección de parámetros globales.</span><span class="sxs-lookup"><span data-stu-id="e75b3-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="e75b3-192">Copie la función `Get-MSBuildCmd` en el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="e75b3-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="e75b3-193">Reemplace `New-WebDeployPackage` por el código siguiente y reemplace los marcadores de posición en la construcción de la línea `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="e75b3-194">Este código es para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e75b3-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="e75b3-195">Si está usando Visual Studio 2013, cambie la propiedad **VisualStudioVersion** a continuación a `12.0`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="e75b3-196">Para compilar la aplicación web, utilice MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="e75b3-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="e75b3-197">Para obtener ayuda, consulte la referencia de la línea de comandos de MSBuild en: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="e75b3-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="e75b3-198">Inicio de la ejecución del comando de compilación</span><span class="sxs-lookup"><span data-stu-id="e75b3-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="e75b3-199">Llame a la `New-WebDeployPackage` función antes de esta línea: `$Config = Read-ConfigFile $Configuration` para aplicaciones web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` para máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e75b3-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="e75b3-200">Invoque el script personalizado desde la línea de comandos con el argumento `$Project`, como se muestra en la siguiente línea de comandos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="e75b3-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="e75b3-201">Para automatizar las pruebas de su aplicación, agregue código a `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="e75b3-202">Asegúrese de anular los comentarios de las líneas en **Publish-WebApplication.ps1** donde se llama a estas funciones.</span><span class="sxs-lookup"><span data-stu-id="e75b3-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="e75b3-203">Si no ofrece una implementación, puede crear su proyecto manualmente con Visual Studio y luego ejecute el script de publicación para publicar en Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="e75b3-204">Publicación del resumen de la función</span><span class="sxs-lookup"><span data-stu-id="e75b3-204">Publishing function summary</span></span>
<span data-ttu-id="e75b3-205">Para obtener ayuda para las funciones que puede usar en el símbolo del sistema de Windows PowerShell, use el comando `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="e75b3-206">La ayuda incluye ejemplos y la ayuda de parámetros.</span><span class="sxs-lookup"><span data-stu-id="e75b3-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="e75b3-207">El mismo texto de ayuda también se encuentra en los archivos de origen de script, **AzureWebAppPublishModule.psm1** y **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e75b3-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="e75b3-208">El script y la Ayuda se localizan en su idioma de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e75b3-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="e75b3-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="e75b3-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="e75b3-210">Nombre de función</span><span class="sxs-lookup"><span data-stu-id="e75b3-210">Function name</span></span> | <span data-ttu-id="e75b3-211">Description</span><span class="sxs-lookup"><span data-stu-id="e75b3-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e75b3-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="e75b3-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="e75b3-213">Crea una nueva base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="e75b3-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="e75b3-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="e75b3-215">Crea las bases de datos SQL de Azure a partir de los valores en el archivo de configuración de JSON que Visual Studio genera.</span><span class="sxs-lookup"><span data-stu-id="e75b3-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="e75b3-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e75b3-216">Add-AzureVM</span></span> |<span data-ttu-id="e75b3-217">Crea una máquina virtual de Azure y devuelve la dirección URL de la máquina virtual implementada.</span><span class="sxs-lookup"><span data-stu-id="e75b3-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="e75b3-218">La función configura los requisitos previos y luego llama a la función **New-AzureVM** (módulo de Azure) para crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="e75b3-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="e75b3-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="e75b3-220">Agrega nuevos extremos de entrada a una máquina virtual y devuelve la máquina virtual con el nuevo extremo.</span><span class="sxs-lookup"><span data-stu-id="e75b3-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="e75b3-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e75b3-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="e75b3-222">Crea una nueva cuenta de Almacenamiento de Azure en la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="e75b3-223">El nombre de la cuenta comienza con "devtest" seguido de una cadena alfanumérica única.</span><span class="sxs-lookup"><span data-stu-id="e75b3-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="e75b3-224">La función devuelve el nombre de la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e75b3-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="e75b3-225">Debe especificar una ubicación o un grupo de afinidad para la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e75b3-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="e75b3-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="e75b3-226">Add-AzureWebsite</span></span> |<span data-ttu-id="e75b3-227">Crea un sitio web con el nombre y la ubicación especificados.</span><span class="sxs-lookup"><span data-stu-id="e75b3-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="e75b3-228">Esta función llama a la función **New-AzureWebsite** en el módulo de Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="e75b3-229">Si la suscripción no incluye ya un sitio web con el nombre especificado, esta función crea el sitio web y devuelve un objeto de sitio web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="e75b3-230">De lo contrario, devuelve `$null`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="e75b3-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="e75b3-231">Backup-Subscription</span></span> |<span data-ttu-id="e75b3-232">Guarda la suscripción de Azure actual en la variable `$Script:originalSubscription` en el ámbito de script. Esta función guarda la suscripción de Azure actual (como se obtiene mediante `Get-AzureSubscription -Current`) y su cuenta de almacenamiento, y la suscripción que se cambia por este script (almacenada en la variable `$UserSpecifiedSubscription`) y su cuenta de almacenamiento, en el ámbito de script.</span><span class="sxs-lookup"><span data-stu-id="e75b3-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="e75b3-233">Al guardar los valores, puede usar una función, como `Restore-Subscription`, para restaurar la suscripción actual original y la cuenta de almacenamiento al estado actual si este estado ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="e75b3-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="e75b3-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e75b3-234">Find-AzureVM</span></span> |<span data-ttu-id="e75b3-235">Obtiene la máquina virtual de Azure especificada.</span><span class="sxs-lookup"><span data-stu-id="e75b3-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="e75b3-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="e75b3-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="e75b3-237">Antepone la fecha y la hora a un mensaje.</span><span class="sxs-lookup"><span data-stu-id="e75b3-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="e75b3-238">Esta función está diseñada para mensajes escritos en las secuencias de Error y Detallado.</span><span class="sxs-lookup"><span data-stu-id="e75b3-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="e75b3-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="e75b3-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="e75b3-240">Ensambla una cadena de conexión para conectarse a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b3-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="e75b3-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="e75b3-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="e75b3-242">Devuelve el nombre de la primera cuenta de almacenamiento con el patrón de nombre "devtest*" (no distingue mayúsculas de minúsculas) en la ubicación especificada o el grupo de afinidad. Si la cuenta de almacenamiento "devtest*" no coincide con la ubicación o el grupo de afinidad, la función la omite.</span><span class="sxs-lookup"><span data-stu-id="e75b3-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="e75b3-243">Debe especificar una ubicación o un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="e75b3-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="e75b3-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="e75b3-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="e75b3-245">Devuelve un comando para ejecutar la herramienta MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="e75b3-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="e75b3-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="e75b3-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="e75b3-247">Busca o crea una máquina virtual en la suscripción que coincida con los valores del archivo de configuración de JSON.</span><span class="sxs-lookup"><span data-stu-id="e75b3-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="e75b3-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="e75b3-248">Publish-WebPackage</span></span> |<span data-ttu-id="e75b3-249">Usa MsDeploy.exe y un archivo .zip de paquete de publicación web para implementar recursos en un sitio web.</span><span class="sxs-lookup"><span data-stu-id="e75b3-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="e75b3-250">Esta función no genera ninguna salida.</span><span class="sxs-lookup"><span data-stu-id="e75b3-250">This function doesn't generate any output.</span></span> <span data-ttu-id="e75b3-251">Si se produce un error en la llamada a MSDeploy.exe, la función genera una excepción.</span><span class="sxs-lookup"><span data-stu-id="e75b3-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="e75b3-252">Para obtener una salida más detallada, use la opción **-Verbose** .</span><span class="sxs-lookup"><span data-stu-id="e75b3-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="e75b3-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="e75b3-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="e75b3-254">Comprueba los valores de parámetro y luego llama a la función **Publish-WebPackage** .</span><span class="sxs-lookup"><span data-stu-id="e75b3-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="e75b3-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e75b3-255">Read-ConfigFile</span></span> |<span data-ttu-id="e75b3-256">Valida el archivo de configuración de JSON y devuelve una tabla hash de valores seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e75b3-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="e75b3-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="e75b3-257">Restore-Subscription</span></span> |<span data-ttu-id="e75b3-258">Restablece la suscripción actual a la suscripción original.</span><span class="sxs-lookup"><span data-stu-id="e75b3-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="e75b3-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="e75b3-259">Test-AzureModule</span></span> |<span data-ttu-id="e75b3-260">Devuelve `$true` si la versión del módulo de Azure instalada es 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="e75b3-261">Devuelve `$false` si el módulo no está instalado o es de una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e75b3-262">Esta función no tiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="e75b3-262">This function has no parameters.</span></span> |
| <span data-ttu-id="e75b3-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="e75b3-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="e75b3-264">Devuelve `$true` si la versión del módulo de Azure es 0.7.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="e75b3-265">Devuelve `$false` si el módulo no está instalado o es de una versión anterior.</span><span class="sxs-lookup"><span data-stu-id="e75b3-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="e75b3-266">Esta función no tiene parámetros.</span><span class="sxs-lookup"><span data-stu-id="e75b3-266">This function has no parameters.</span></span> |
| <span data-ttu-id="e75b3-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="e75b3-267">Test-HttpsUrl</span></span> |<span data-ttu-id="e75b3-268">Convierte la URL de entrada en un objeto System.Uri.</span><span class="sxs-lookup"><span data-stu-id="e75b3-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="e75b3-269">Devuelve `$True` si la dirección URL es absoluta y su esquema es https.</span><span class="sxs-lookup"><span data-stu-id="e75b3-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="e75b3-270">Devuelve `$false` si la dirección URL es relativa, su esquema no es HTTPS o no se puede convertir la cadena de entrada a una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e75b3-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="e75b3-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="e75b3-271">Test-Member</span></span> |<span data-ttu-id="e75b3-272">Devuelve `$true` si una propiedad o un método es un miembro del objeto.</span><span class="sxs-lookup"><span data-stu-id="e75b3-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="e75b3-273">De lo contrario, devuelve `$false`.</span><span class="sxs-lookup"><span data-stu-id="e75b3-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="e75b3-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="e75b3-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="e75b3-275">Escribe un mensaje de error precedido por la hora actual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="e75b3-276">Esta función llama a la función **Format-DevTestMessageWithTime** para anteponer la hora antes de escribir el mensaje en la secuencia de error.</span><span class="sxs-lookup"><span data-stu-id="e75b3-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="e75b3-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="e75b3-277">Write-HostWithTime</span></span> |<span data-ttu-id="e75b3-278">Escribe un mensaje en el programa host (**Write-Host**) precedido por la hora actual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="e75b3-279">El efecto de escribir en el programa host varía.</span><span class="sxs-lookup"><span data-stu-id="e75b3-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="e75b3-280">La mayoría de los programas que hospedan Windows PowerShell escribe estos mensajes en la salida estándar.</span><span class="sxs-lookup"><span data-stu-id="e75b3-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="e75b3-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="e75b3-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="e75b3-282">Escribe un mensaje detallado precedido por la hora actual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="e75b3-283">Porque llama a **Write-Verbose**, el mensaje solo aparece cuando el script se ejecuta con el parámetro **Verbose** o cuando la preferencia **VerbosePreference** está establecida en **Continue**.</span><span class="sxs-lookup"><span data-stu-id="e75b3-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="e75b3-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="e75b3-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="e75b3-285">Nombre de función</span><span class="sxs-lookup"><span data-stu-id="e75b3-285">Function name</span></span> | <span data-ttu-id="e75b3-286">Description</span><span class="sxs-lookup"><span data-stu-id="e75b3-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e75b3-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="e75b3-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="e75b3-288">Crea recursos de Azure, como un sitio web o una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e75b3-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="e75b3-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e75b3-289">New-WebDeployPackage</span></span> |<span data-ttu-id="e75b3-290">Esta función no está implementada.</span><span class="sxs-lookup"><span data-stu-id="e75b3-290">This function isn't implemented.</span></span> <span data-ttu-id="e75b3-291">Puede agregar comandos en esta función para generar su proyecto.</span><span class="sxs-lookup"><span data-stu-id="e75b3-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="e75b3-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="e75b3-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="e75b3-293">Publica una aplicación web en Azure</span><span class="sxs-lookup"><span data-stu-id="e75b3-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="e75b3-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e75b3-294">Publish-WebApplication</span></span> |<span data-ttu-id="e75b3-295">Crea e implementa aplicaciones web, máquinas virtuales, bases de datos SQL y cuentas de almacenamiento para un proyecto web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e75b3-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="e75b3-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="e75b3-296">Test-WebApplication</span></span> |<span data-ttu-id="e75b3-297">Esta función no está implementada.</span><span class="sxs-lookup"><span data-stu-id="e75b3-297">This function isn't implemented.</span></span> <span data-ttu-id="e75b3-298">Puede agregar comandos en esta función para probar su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e75b3-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e75b3-299">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e75b3-299">Next steps</span></span>
<span data-ttu-id="e75b3-300">Obtenga más información sobre el scripting de PowerShell leyendo [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) y consulte otros scripts de Azure PowerShell en el [Centro de scripts](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="e75b3-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
