---
title: "aplicación de aaaNode.js con Socket.io | Documentos de Microsoft"
description: "Obtenga información acerca de cómo alojar toouse socket.io en una aplicación node.js en Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="08a9a-103">Creación de una aplicación de chat Node.js con Socket.IO en un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="08a9a-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="08a9a-104">Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes.</span><span class="sxs-lookup"><span data-stu-id="08a9a-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="08a9a-105">Este tutorial le llevara por el hospedaje de una aplicación de chat basada en socket.IO en Azure.</span><span class="sxs-lookup"><span data-stu-id="08a9a-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="08a9a-106">Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="08a9a-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="08a9a-107">Una captura de pantalla de la aplicación hello completado es menor que:</span><span class="sxs-lookup"><span data-stu-id="08a9a-107">A screenshot of hello completed application is below:</span></span>

![Una ventana del explorador mostrar servicio Hola hospedado en Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="08a9a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="08a9a-109">Prerequisites</span></span>
<span data-ttu-id="08a9a-110">Asegúrese de que Hola siguientes productos y versiones son ejemplo de Hola completa toosuccessfully instalada en este artículo:</span><span class="sxs-lookup"><span data-stu-id="08a9a-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="08a9a-111">Instalar [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="08a9a-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="08a9a-112">Instalar [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="08a9a-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="08a9a-113">Instalar [Python versión 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="08a9a-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="08a9a-114">Creación de un proyecto de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="08a9a-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="08a9a-115">Hello pasos siguientes crean proyecto de servicio de nube de Hola que hospedará la aplicación de hello Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="08a9a-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="08a9a-116">De hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="08a9a-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="08a9a-117">Finalmente, haga clic con el botón derecho en **Windows PowerShell** y seleccione **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="08a9a-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icono de Azure PowerShell][powershell-menu]
2. <span data-ttu-id="08a9a-119">Cree un directorio denominado **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="08a9a-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="08a9a-120">Cambie los directorios toohello **c:\\nodo** directory</span><span class="sxs-lookup"><span data-stu-id="08a9a-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="08a9a-121">Escriba Hola después comandos toocreate una nueva solución denominada **chatapp** y un rol de trabajo denominado **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="08a9a-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="08a9a-122">Verá Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="08a9a-122">You will see hello following response:</span></span>
   
    ![salida de Hello de hello nueva-azureservice y azurenodeworkerrolecmdlets agregar](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="08a9a-124">Descargar Hola ejemplo Chat</span><span class="sxs-lookup"><span data-stu-id="08a9a-124">Download hello Chat Example</span></span>
<span data-ttu-id="08a9a-125">Para este proyecto, usaremos hello (ejemplo) chat de hello [repositorio de Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="08a9a-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="08a9a-126">Realizar Hola siguiente ejemplo de Hola toodownload de pasos y Agregar proyecto toohello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="08a9a-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="08a9a-127">Crear una copia local del repositorio de hello mediante hello **clon** botón.</span><span class="sxs-lookup"><span data-stu-id="08a9a-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="08a9a-128">También puede usar hello **código postal** proyecto de botón toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="08a9a-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Una ventana del explorador ven https://github.com/LearnBoost/socket.io/tree/master/examples/chat, con el icono de descarga de hello ZIP resaltado][chat-example-view]
2. <span data-ttu-id="08a9a-130">Explorar la estructura de directorios de hello del repositorio local Hola hasta que llegue al hello **ejemplos\\chat** directory.</span><span class="sxs-lookup"><span data-stu-id="08a9a-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="08a9a-131">Copie el contenido de Hola de este directorio toothe **C:\\nodo\\chatapp\\WorkerRole1** directorio creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="08a9a-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![El explorador, mostrar contenido de Hola de ejemplos de hello\\directorio chat extraído del archivo Hola][chat-contents]
   
   <span data-ttu-id="08a9a-133">los elementos resaltados en la captura de pantalla de hello anterior Hello son archivos de hello copiados de hello **ejemplos\\chat** directory</span><span class="sxs-lookup"><span data-stu-id="08a9a-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="08a9a-134">Hola **C:\\nodo\\chatapp\\WorkerRole1** directorio, delete hello **server.js** de archivos y, a continuación, cambie el nombre hello **app.js**archivo demasiado**server.js**.</span><span class="sxs-lookup"><span data-stu-id="08a9a-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="08a9a-135">Esto quita el valor predeterminado de hello **server.js** archivo creado anteriormente por hello **Add-AzureNodeWorkerRole** cmdlet y los reemplaza con la aplicación hello de archivos de ejemplo de chat de Hola.</span><span class="sxs-lookup"><span data-stu-id="08a9a-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="08a9a-136">Modificar el archivo server.js e instalar los módulos</span><span class="sxs-lookup"><span data-stu-id="08a9a-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="08a9a-137">Antes de la aplicación de prueba Hola Hola emulador de Azure, debemos hacer algunas modificaciones menores.</span><span class="sxs-lookup"><span data-stu-id="08a9a-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="08a9a-138">Lleve a cabo Hola pasos toothe server.js archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="08a9a-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="08a9a-139">Abra hello **server.js** archivo en Visual Studio o en cualquier editor de texto.</span><span class="sxs-lookup"><span data-stu-id="08a9a-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="08a9a-140">Buscar hello **las dependencias del módulo** sección al principio de Hola de server.js y cambiar Hola línea que contiene **sio = require('.. //.. lib//Socket.IO')** demasiado**sio = require('socket.io')** tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="08a9a-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="08a9a-141">aplicación de hello tooensure escucha en el puerto correcto de hello, abra server.js en el Bloc de notas o su editor favorito y, a continuación, cambie la siguiente línea reemplazando **3000** con **process.env.port** tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="08a9a-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="08a9a-142">Después de guardar los cambios de hello demasiado**server.js**usar hello siguiendo los pasos para instalar los módulos necesarios y, a continuación, pruebe la aplicación hello en el emulador de Azure:</span><span class="sxs-lookup"><span data-stu-id="08a9a-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="08a9a-143">Usando **Azure PowerShell**, cambie los directorios toohello **C:\\nodo\\chatapp\\WorkerRole1** Hola de directorio y el uso después de comando tooinstall hello módulos requeridos por la aplicación:</span><span class="sxs-lookup"><span data-stu-id="08a9a-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="08a9a-144">Este modo se instalará módulos de hello enumerados en el archivo de hello package.json.</span><span class="sxs-lookup"><span data-stu-id="08a9a-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="08a9a-145">Una vez completado el comando de hello, debería ver resultados similares toothe siguiente:</span><span class="sxs-lookup"><span data-stu-id="08a9a-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![comando de instalación de la salida de Hello de hello npm][The-output-of-the-npm-install-command]
2. <span data-ttu-id="08a9a-147">Dado que este ejemplo originalmente formaba parte del repositorio de Socket.IO GitHub de Hola y hace referencia directamente a biblioteca de hello Socket.IO ruta de acceso relativa, Socket.IO no se hace referencia en el archivo de package.json hello, por lo que debemos instalarlo mediante la emisión de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="08a9a-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="08a9a-148">Prueba e implementación</span><span class="sxs-lookup"><span data-stu-id="08a9a-148">Test and Deploy</span></span>
1. <span data-ttu-id="08a9a-149">Inicie el emulador de hello emitiendo Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="08a9a-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="08a9a-150">Si tiene algún problema con el emulador de inicio, por ejemplo; Start-AzureEmulator : Error inesperado.</span><span class="sxs-lookup"><span data-stu-id="08a9a-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="08a9a-151">Detalles: Se encontró un error inesperado Hola comunicación objeto, System.ServiceModel.Channels.ServiceChannel, no puede utilizarse para la comunicación porque está en estado Faulted de hello.</span><span class="sxs-lookup"><span data-stu-id="08a9a-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="08a9a-152">Vuelva a instalar AzureAuthoringTools v 2.7.1 y AzureComputeEmulator v 2.7. Asegúrese de que coincida con esa versión.</span><span class="sxs-lookup"><span data-stu-id="08a9a-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="08a9a-153">Abra un explorador y navegue demasiado**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="08a9a-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="08a9a-154">Cuando se abre la ventana del explorador de hello, escriba un alias y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="08a9a-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="08a9a-155">Esto le permitirá toopost mensajes como un alias específico.</span><span class="sxs-lookup"><span data-stu-id="08a9a-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="08a9a-156">funcionalidad de varios usuarios tootest, abrir ventanas adicionales del explorador utilizando la misma dirección URL y escriba los alias diferentes.</span><span class="sxs-lookup"><span data-stu-id="08a9a-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Dos ventanas de explorador que muestran mensajes de chat de User1 y User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="08a9a-158">Después de la aplicación de prueba hello, detener el emulador de hello emitiendo el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="08a9a-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="08a9a-159">toodeploy Hola aplicación tooAzure, use la **AzureServiceProject publicar** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08a9a-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="08a9a-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="08a9a-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="08a9a-161">Ser un nombre único de toouse seguro, en caso contrario Hola publicar proceso producirá un error.</span><span class="sxs-lookup"><span data-stu-id="08a9a-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="08a9a-162">Una vez finalizada la implementación de hello, Explorador de Hola se abrirá y navegue toohello implementado service.</span><span class="sxs-lookup"><span data-stu-id="08a9a-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="08a9a-163">Si recibe un error que indica que ese Hola proporcionado nombre de la suscripción no existe en hello importar perfil de publicación, debe descargar e importar el perfil de publicación de Hola para su suscripción antes de implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="08a9a-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="08a9a-164">Vea hello **implementar Hola aplicación tooAzure** sección de [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="08a9a-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Una ventana del explorador mostrar servicio Hola hospedado en Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="08a9a-166">Si recibe un error que indica que ese Hola proporcionado nombre de la suscripción no existe en hello importar perfil de publicación, debe descargar e importar el perfil de publicación de Hola para su suscripción antes de implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="08a9a-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="08a9a-167">Vea hello **implementar Hola aplicación tooAzure** sección de [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="08a9a-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="08a9a-168">Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="08a9a-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="08a9a-169">Para simplificar, este ejemplo es toochatting limitado entre los usuarios conectados toohello misma instancia.</span><span class="sxs-lookup"><span data-stu-id="08a9a-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="08a9a-170">Esto significa que si el servicio en la nube Hola crea dos instancias de rol de trabajo, los usuarios solo podrán toochat con otros usuarios conectados toohello misma instancia de rol de trabajo.</span><span class="sxs-lookup"><span data-stu-id="08a9a-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="08a9a-171">tooscale hello toowork de aplicación con varias instancias de rol, podría utilizar una tecnología como Service Bus tooshare hello Socket.IO almacenar el estado en todas las instancias.</span><span class="sxs-lookup"><span data-stu-id="08a9a-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="08a9a-172">Para obtener ejemplos, vea ejemplos de uso de hello temas y colas de Bus de servicio en hello [Azure SDK para el repositorio de Node.js GitHub](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="08a9a-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="08a9a-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08a9a-173">Next steps</span></span>
<span data-ttu-id="08a9a-174">En este tutorial ha aprendido cómo toocreate una aplicación básica de chat hospedada en un servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="08a9a-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="08a9a-175">toolearn toohost esta aplicación en un sitio Web de Azure, vea [compilar una aplicación de Chat de Node.js con Socket.IO en un sitio Web de Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="08a9a-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="08a9a-176">Para obtener más información, vea también hello [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="08a9a-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repositorio de Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


