---
title: "implementación de máquina virtual de aaaAzure con Chef | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Chef toodo automatiza la implementación de máquina virtual y la configuración en Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="04e23-103">Automatización de la implementación de la máquina virtual de Azure con Chef</span><span class="sxs-lookup"><span data-stu-id="04e23-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="04e23-104">Chef es una fantástica herramienta para ofrecer automatización y las configuraciones de estado que desee.</span><span class="sxs-lookup"><span data-stu-id="04e23-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="04e23-105">Con la versión más reciente de api de la nube, Chef proporciona una perfecta integración con Azure, lo que le ofrece Hola tooprovision de capacidad e implementar los Estados de configuración a través de un solo comando.</span><span class="sxs-lookup"><span data-stu-id="04e23-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="04e23-106">En este artículo, mostraré cómo tooset seguridad su tooprovision de entorno virtual de Azure de Chef máquinas y le guían en la creación de una directiva o un "Libro de cocina" y, a continuación, implementar esta máquina virtual de Azure tooan de libro de cocina.</span><span class="sxs-lookup"><span data-stu-id="04e23-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="04e23-107">Vamos a comenzar</span><span class="sxs-lookup"><span data-stu-id="04e23-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="04e23-108">Conceptos básicos de Chef</span><span class="sxs-lookup"><span data-stu-id="04e23-108">Chef basics</span></span>
<span data-ttu-id="04e23-109">Antes de comenzar, le sugiero que revise los conceptos básicos de Hola de Chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="04e23-110">Hay gran material <a href="http://www.chef.io/chef" target="_blank">aquí</a> y recomiendo una lectura rápida antes de realizar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="04e23-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="04e23-111">Sin embargo se resumen de conceptos básicos de hello antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="04e23-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="04e23-112">Hola siguiente diagrama muestra la arquitectura de Chef de alto nivel de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="04e23-113">Chef tiene tres componentes de arquitectura principales: servidor de Chef, cliente de Chef (nodo) y estación de trabajo de Chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="04e23-114">Hola el servidor de Chef es el punto de administración y hay dos opciones para el servidor de Chef hello: una solución hospedada o una solución local.</span><span class="sxs-lookup"><span data-stu-id="04e23-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="04e23-115">Vamos a usar una solución hospedada.</span><span class="sxs-lookup"><span data-stu-id="04e23-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="04e23-116">Cliente de Chef Hello (nodo) es agente de Hola que se ubica en los servidores de hello que está administrando.</span><span class="sxs-lookup"><span data-stu-id="04e23-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="04e23-117">Hola la estación de trabajo es nuestra estación de trabajo de administración donde se crean nuestras directivas y ejecutan los comandos de la administración.</span><span class="sxs-lookup"><span data-stu-id="04e23-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="04e23-118">Ejecutamos hello **knife** nuestra infraestructura de comandos de hello toomanage de la estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="04e23-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="04e23-119">También hay concepto de Hola de "Cocina" y "Recetas".</span><span class="sxs-lookup"><span data-stu-id="04e23-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="04e23-120">Estas son las directivas de Hola se defina y aplican tooour servidores.</span><span class="sxs-lookup"><span data-stu-id="04e23-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="04e23-121">Preparar la estación de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="04e23-121">Preparing hello workstation</span></span>
<span data-ttu-id="04e23-122">En primer lugar, permite la estación de trabajo de preparación Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="04e23-123">Estoy usando una estación de trabajo de Windows estándar.</span><span class="sxs-lookup"><span data-stu-id="04e23-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="04e23-124">Necesitamos toocreate un toostore directory nuestros archivos de configuración y los libros de cocina.</span><span class="sxs-lookup"><span data-stu-id="04e23-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="04e23-125">En primer lugar, cree un directorio denominado C:\chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="04e23-126">A continuación, cree un segundo directorio denominado c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="04e23-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="04e23-127">Ahora necesitamos toodownload nuestro archivo de configuración de Azure para que Chef pueda comunicarse con nuestra suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="04e23-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="04e23-128">Descargar su configuración mediante hello PowerShell Azure de publicación [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) comando.</span><span class="sxs-lookup"><span data-stu-id="04e23-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="04e23-129">Guardar Hola publicar el archivo de configuración en C:\chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="04e23-130">Crear una cuenta de Chef administrada</span><span class="sxs-lookup"><span data-stu-id="04e23-130">Creating a managed Chef account</span></span>
<span data-ttu-id="04e23-131">Regístrese para una cuenta de Chef hospedada [aquí](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="04e23-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="04e23-132">Durante el proceso de registro de hello, estará más frecuentes toocreate una nueva organización.</span><span class="sxs-lookup"><span data-stu-id="04e23-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="04e23-133">Una vez creada la organización, descargue el starter kit de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="04e23-134">Si recibe un mensaje que le advierte de que las claves se restablecerá, es aceptar tooproceed tal y como se dispone de ninguna infraestructura configurada todavía.</span><span class="sxs-lookup"><span data-stu-id="04e23-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="04e23-135">El archivo zip del starter kit contiene sus claves y archivos de configuración de la organización.</span><span class="sxs-lookup"><span data-stu-id="04e23-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="04e23-136">Configurar la estación de trabajo de Chef Hola</span><span class="sxs-lookup"><span data-stu-id="04e23-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="04e23-137">Extraer contenido de Hola de hello chef starter.zip tooC:\chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="04e23-138">Copie todos los archivos en el repositorio de chef starter\chef\.chef tooyour c:\chef directory.</span><span class="sxs-lookup"><span data-stu-id="04e23-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="04e23-139">El directorio debe ser ahora algo parecido a Hola siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="04e23-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="04e23-140">Ahora debería tener cuatro archivos incluidos Hola archivo de publicación de Azure en la raíz de Hola de c:\chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="04e23-141">archivos PEM de Hello contienen la organización y administración de claves privadas para la comunicación al archivo de hello knife.rb contiene la configuración de knife.</span><span class="sxs-lookup"><span data-stu-id="04e23-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="04e23-142">Necesitamos archivo knife.rb de tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="04e23-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="04e23-143">Abra el archivo hello en el editor que prefiera y modificar cookbook_path"hello" mediante la eliminación de Hola /... / desde la ruta de acceso de Hola por lo que parece tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="04e23-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="04e23-144">Agregar siguiente Hola línea reflejan nombre Hola de Azure publicar el archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="04e23-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="04e23-145">El archivo knife.rb debe ser ahora similar toohello siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="04e23-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="04e23-146">Estas líneas garantizará que hace referencia a directorio de guías de hello en c:\chef\cookbooks Knife y también usa el archivo de configuración de publicación de Azure durante las operaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="04e23-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="04e23-147">Hola Chef Development Kit de instalación</span><span class="sxs-lookup"><span data-stu-id="04e23-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="04e23-148">Siguiente [descargar e instalar](http://downloads.getchef.com/chef-dk/windows) Hola tooset ChefDK (Chef Development Kit) de la estación de trabajo de Chef.</span><span class="sxs-lookup"><span data-stu-id="04e23-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="04e23-149">Instalar en la ubicación predeterminada de Hola de c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="04e23-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="04e23-150">Esta instalación tardará unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="04e23-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="04e23-151">Confirme que la variable PATH contiene entradas para C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="04e23-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="04e23-152">Si no están ahí, asegúrese de agregar estas rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="04e23-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="04e23-153">*Tenga en cuenta Hola orden de Hola ruta de acceso es importante.*</span><span class="sxs-lookup"><span data-stu-id="04e23-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="04e23-154">Si las rutas de acceso de opscode no están en orden correcto de hello tendrán problemas.</span><span class="sxs-lookup"><span data-stu-id="04e23-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="04e23-155">Reinicie la estación de trabajo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="04e23-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="04e23-156">A continuación, se instalará la extensión de Azure de Knife Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="04e23-157">Esto proporciona cuchilla con hello "Complemento de Azure".</span><span class="sxs-lookup"><span data-stu-id="04e23-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="04e23-158">Ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="04e23-159">argumento de Hello – pre garantiza que recibe la versión más reciente de RC Hola de hello complemento de Azure de Knife que proporciona acceso toohello último conjunto de API.</span><span class="sxs-lookup"><span data-stu-id="04e23-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="04e23-160">Es probable que también se instala un número de dependencias en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="04e23-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="04e23-161">tooensure que todo está configurado correctamente, Hola ejecución siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="04e23-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="04e23-162">Si todo está configurado correctamente, verá una lista de imágenes de Azure disponibles en desplazamiento.</span><span class="sxs-lookup"><span data-stu-id="04e23-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="04e23-163">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="04e23-163">Congratulations.</span></span> <span data-ttu-id="04e23-164">¡se configura la estación de trabajo de Hola!</span><span class="sxs-lookup"><span data-stu-id="04e23-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="04e23-165">Crear una guía</span><span class="sxs-lookup"><span data-stu-id="04e23-165">Creating a Cookbook</span></span>
<span data-ttu-id="04e23-166">Se utiliza un libro de cocina por Chef toodefine un conjunto de comandos que desea tooexecute en el cliente administrado.</span><span class="sxs-lookup"><span data-stu-id="04e23-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="04e23-167">Crear un libro de cocina es sencillo y usamos hello **chef generar el libro de cocina** comando toogenerate la plantilla de libro de cocina.</span><span class="sxs-lookup"><span data-stu-id="04e23-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="04e23-168">Llamaré a mi servidor web de Cookbook ya que me gustaría una directiva que implemente IIS automáticamente.</span><span class="sxs-lookup"><span data-stu-id="04e23-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="04e23-169">En el directorio C:\Chef ejecute hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="04e23-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="04e23-170">Esto generará un conjunto de archivos en el directorio de hello C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="04e23-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="04e23-171">Ahora necesitamos conjunto de hello toodefine de comandos que nos gustaría nuestro tooexecute de cliente de Chef en la máquina virtual administrado.</span><span class="sxs-lookup"><span data-stu-id="04e23-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="04e23-172">comandos de Hola se almacenan en hello archivo default.rb.</span><span class="sxs-lookup"><span data-stu-id="04e23-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="04e23-173">En este archivo, podrá definir un conjunto de comandos que se instala IIS, IIS se inicia y se copia una carpeta de plantilla archivo toohello wwwroot.</span><span class="sxs-lookup"><span data-stu-id="04e23-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="04e23-174">Modificar el archivo de C:\chef\cookbooks\webserver\recipes\default.rb hello y agregue Hola siguiendo las líneas.</span><span class="sxs-lookup"><span data-stu-id="04e23-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="04e23-175">Guarde el archivo hello cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="04e23-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="04e23-176">Crear una plantilla</span><span class="sxs-lookup"><span data-stu-id="04e23-176">Creating a template</span></span>
<span data-ttu-id="04e23-177">Como mencionamos anteriormente, necesitamos toogenerate un archivo de plantilla que se usará como nuestra página de default.html.</span><span class="sxs-lookup"><span data-stu-id="04e23-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="04e23-178">Ejecute hello después de la plantilla del comando toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="04e23-179">Ahora, explore toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb archivo.</span><span class="sxs-lookup"><span data-stu-id="04e23-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="04e23-180">Editar archivo hello agregando código HTML "Hello World" simple y, a continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="04e23-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="04e23-181">Cargar Hola libro de cocina toohello el servidor de Chef</span><span class="sxs-lookup"><span data-stu-id="04e23-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="04e23-182">En este paso, estamos teniendo una copia del programa Hola libro de cocina que hemos creado en el equipo local y cargarlo toohello el servidor de Chef hospedada.</span><span class="sxs-lookup"><span data-stu-id="04e23-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="04e23-183">Una vez cargado, Hola libro de cocina aparecerá en hello **directiva** ficha.</span><span class="sxs-lookup"><span data-stu-id="04e23-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="04e23-184">Implementar una máquina virtual con Knife Azure</span><span class="sxs-lookup"><span data-stu-id="04e23-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="04e23-185">Ahora agregaremos implementar una máquina virtual de Azure y aplicar Hola libro de cocina "Webserver" que se instalará nuestra página de web IIS web predeterminada y el servicio.</span><span class="sxs-lookup"><span data-stu-id="04e23-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="04e23-186">En el orden toodo esto, usar hello **crear servidor de azure de knife** comando.</span><span class="sxs-lookup"><span data-stu-id="04e23-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="04e23-187">Estoy de ejemplo de Hola comando aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="04e23-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="04e23-188">parámetros de Hello son autoexplicativos.</span><span class="sxs-lookup"><span data-stu-id="04e23-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="04e23-189">Sustituir sus variables concretas y ejecutar.</span><span class="sxs-lookup"><span data-stu-id="04e23-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="04e23-190">A través de la línea de comandos de Hola Hola, estoy automatizar mis reglas de filtro de red de punto de conexión mediante el uso de parámetros de los puntos de conexión de tcp: Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="04e23-191">He abierto los puertos 80 y 3389 tooprovide acceso toomy web página y sesión RDP.</span><span class="sxs-lookup"><span data-stu-id="04e23-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="04e23-192">Una vez que ejecute el comando hello, vaya toohello Azure portal y verá su equipo empezar tooprovision.</span><span class="sxs-lookup"><span data-stu-id="04e23-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="04e23-193">símbolo de Hello aparece a continuación.</span><span class="sxs-lookup"><span data-stu-id="04e23-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="04e23-194">Una vez completada la implementación de hello, deberíamos estar servicio web de tooconnect puede toohello en el puerto 80 tal y como se hubiera abierto el puerto de hello cuando se aprovisiona máquina virtual de hello con hello comando Knife de Azure.</span><span class="sxs-lookup"><span data-stu-id="04e23-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="04e23-195">Puesto que esta máquina virtual es Hola de máquina virtual solo en mi servicio de nube, conectará con la dirección url del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="04e23-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="04e23-196">Como puede observar, me ha entrado la creatividad con mi código HTML.</span><span class="sxs-lookup"><span data-stu-id="04e23-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="04e23-197">No olvide que también podemos conectarnos a través de una sesión RDP de hello portal de Azure en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="04e23-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="04e23-198">Espero que esto les haya resultado útil.</span><span class="sxs-lookup"><span data-stu-id="04e23-198">I hope this has been helpful!</span></span> <span data-ttu-id="04e23-199">Empiece hoy su viaje de su infraestructura como código con Azure.</span><span class="sxs-lookup"><span data-stu-id="04e23-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
