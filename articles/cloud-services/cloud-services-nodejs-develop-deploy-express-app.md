---
title: "aaaWeb aplicación con Express (Node.js) | Documentos de Microsoft"
description: "Un tutorial que se basa en el tutorial de servicio de nube de Hola y muestra cómo toouse Hola módulo Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="7aa44-103">Compilación de una aplicación web Node.js mediante Express en un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="7aa44-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="7aa44-104">Node.js incluye un conjunto mínimo de funcionalidad en tiempo de ejecución de hello core.</span><span class="sxs-lookup"><span data-stu-id="7aa44-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="7aa44-105">Los desarrolladores suelen utilizar 3rd funcionalidad adicional de entidad módulos tooprovide al desarrollar una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="7aa44-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="7aa44-106">En este tutorial creará una nueva aplicación mediante hello [Express] [ Express] módulo, que proporciona un marco MVC para crear aplicaciones web de Node.js.</span><span class="sxs-lookup"><span data-stu-id="7aa44-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="7aa44-107">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="7aa44-107">A screenshot of hello completed application is below:</span></span>

![Un explorador web mostrar tooExpress bienvenida en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="7aa44-109">Creación de un proyecto de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="7aa44-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="7aa44-110">Realizar Hola siguientes pasos toocreate un nuevo proyecto de servicio de nube con el nombre 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="7aa44-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="7aa44-111">De hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7aa44-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="7aa44-112">Finalmente, haga clic con el botón derecho en **Windows PowerShell** y seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="7aa44-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icono de Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="7aa44-114">Cambie los directorios toohello **c:\\nodo** directorio y, a continuación, escriba Hola después comandos toocreate una nueva solución denominada **expressapp** y un rol web denominado **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="7aa44-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="7aa44-115">De forma predeterminada, **Add-AzureNodeWebRole** usa una versión anterior de Node.js.</span><span class="sxs-lookup"><span data-stu-id="7aa44-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="7aa44-116">Hola **AzureServiceProjectRole conjunto** instrucción anterior indica a Azure toouse v0.10.21 del nodo.</span><span class="sxs-lookup"><span data-stu-id="7aa44-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="7aa44-117">Tenga en cuenta los parámetros de hello distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="7aa44-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="7aa44-118">Puede comprobar la versión correcta de Hola de Node.js se ha seleccionado mediante la comprobación de hello **motores** propiedad en **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="7aa44-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="7aa44-119">Instalación de Express</span><span class="sxs-lookup"><span data-stu-id="7aa44-119">Install Express</span></span>
1. <span data-ttu-id="7aa44-120">Instalar generador de Express Hola emitiendo Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7aa44-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="7aa44-121">resultado de Hello de comando de npm Hola debería ser resultado de toohello similar a continuación.</span><span class="sxs-lookup"><span data-stu-id="7aa44-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Comando rápida de instalación de Windows PowerShell mostrar salida de hello de hello npm.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="7aa44-123">Cambie los directorios toohello **WebRole1** directorio y uso Hola comando express toogenerate una nueva aplicación:</span><span class="sxs-lookup"><span data-stu-id="7aa44-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="7aa44-124">También será toooverwrite solicitada su aplicación anterior.</span><span class="sxs-lookup"><span data-stu-id="7aa44-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="7aa44-125">Escriba **y** o **Sí** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7aa44-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="7aa44-126">Express generará el archivo de app.js hello y una estructura de carpetas para la creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7aa44-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![salida de Hello de comando express Hola](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="7aa44-128">dependencias adicionales tooinstall definidas en el archivo de package.json hello, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7aa44-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalación de la salida de Hello de hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="7aa44-130">Siguiente Hola de uso del comando hello toocopy **bin/www** archivo demasiado**server.js**.</span><span class="sxs-lookup"><span data-stu-id="7aa44-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="7aa44-131">Esto es para que servicio de nube de hello pueda encontrar el punto de entrada de Hola para esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="7aa44-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="7aa44-132">Una vez completado este comando, debe tener un **server.js** archivo hello WebRole1 directorio.</span><span class="sxs-lookup"><span data-stu-id="7aa44-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="7aa44-133">Modificar hello **server.js** tooremove uno de hello '.' caracteres de hello después de línea.</span><span class="sxs-lookup"><span data-stu-id="7aa44-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="7aa44-134">Después de realizar esta modificación, la línea hello debería aparecer como sigue.</span><span class="sxs-lookup"><span data-stu-id="7aa44-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="7aa44-135">Este cambio es necesario puesto que se movió el archivo hello (anteriormente **bin/www**,) toohello mismo directorio que el archivo de aplicación hello que se requiere.</span><span class="sxs-lookup"><span data-stu-id="7aa44-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="7aa44-136">Después de realizar este cambio, guardar hello **server.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="7aa44-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="7aa44-137">Usar hello tras la aplicación de comando toorun Hola Hola emulador de Azure:</span><span class="sxs-lookup"><span data-stu-id="7aa44-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Una página web que contiene tooexpress bienvenida.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="7aa44-139">Hola Modificar vista</span><span class="sxs-lookup"><span data-stu-id="7aa44-139">Modifying hello View</span></span>
<span data-ttu-id="7aa44-140">Ahora modificar Hola ver toodisplay Hola mensaje "Bienvenida tooExpress en Azure".</span><span class="sxs-lookup"><span data-stu-id="7aa44-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="7aa44-141">Escriba Hola comando tooopen hello index.jade archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7aa44-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Hola contenido de hello index.jade archivo.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="7aa44-143">Jade es el motor de vistas de hello predeterminado utilizado por las aplicaciones de Express.</span><span class="sxs-lookup"><span data-stu-id="7aa44-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="7aa44-144">Para obtener más información sobre el motor de vista Jade hello, consulte [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="7aa44-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="7aa44-145">Modificar la última línea de texto de hello anexando **en Azure**.</span><span class="sxs-lookup"><span data-stu-id="7aa44-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![archivo de index.jade Hello, última línea de hello lee: p Bienvenido demasiado\#{título} en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="7aa44-147">Guarde el archivo hello y salga el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="7aa44-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="7aa44-148">Actualice el explorador para ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="7aa44-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Una ventana del explorador, la página de hello contiene tooExpress bienvenida en Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="7aa44-150">Después de la aplicación de prueba hello, usar hello **AzureEmulator Stop** emulador de cmdlet toostop Hola.</span><span class="sxs-lookup"><span data-stu-id="7aa44-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="7aa44-151">Publicación tooAzure de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="7aa44-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="7aa44-152">En la ventana de PowerShell de Azure de hello, usar hello **AzureServiceProject publicar** servicio de nube de cmdlet toodeploy Hola aplicación tooa</span><span class="sxs-lookup"><span data-stu-id="7aa44-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="7aa44-153">Una vez completada la operación de implementación de hello, el explorador abrirá y mostrar la página web de Hola.</span><span class="sxs-lookup"><span data-stu-id="7aa44-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Un explorador web mostrar hello Express página.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="7aa44-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7aa44-156">Next steps</span></span>
<span data-ttu-id="7aa44-157">Para obtener más información, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="7aa44-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


