---
title: "Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure"
description: "Este tutorial muestra el uso de socket.io en una aplicación web node.js hospedada en Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="e4154-103">Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="e4154-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="e4154-104">Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes con WebSockets.</span><span class="sxs-lookup"><span data-stu-id="e4154-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="e4154-105">También es compatible con la reserva a otros transportes (como el sondeo largo) que funcionan con otros exploradores.</span><span class="sxs-lookup"><span data-stu-id="e4154-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="e4154-106">Este tutorial le guiará por el hospedaje de una aplicación de chat basada en Socket.IO como una aplicación web de Azure, y le mostrará cómo escalar la aplicación con [Caché en Redis de Azure].</span><span class="sxs-lookup"><span data-stu-id="e4154-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="e4154-107">Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="e4154-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="e4154-108">Los procedimientos de esta tarea se aplican a [App Service Web Apps]; para Cloud Services, consulte [Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="e4154-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="e4154-109">Descarga del ejemplo de chat</span><span class="sxs-lookup"><span data-stu-id="e4154-109">Download the chat example</span></span>
<span data-ttu-id="e4154-110">Para este proyecto, usaremos el ejemplo de chat del [repositorio de Socket.IO GitHub](en inglés).</span><span class="sxs-lookup"><span data-stu-id="e4154-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="e4154-111">Realice los siguientes pasos para descargar el ejemplo y agréguelo al proyecto que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e4154-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="e4154-112">Descargue una [versión archivada ZIP o GZ] del proyecto Socket.IO (la versión 1.3.5 se ha utilizado para este documento).</span><span class="sxs-lookup"><span data-stu-id="e4154-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="e4154-113">Extraiga el archivo y copie el directorio **examples\\chat** en una ubicación nueva.</span><span class="sxs-lookup"><span data-stu-id="e4154-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="e4154-114">Por ejemplo, **\\nodo\\chat**.</span><span class="sxs-lookup"><span data-stu-id="e4154-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="e4154-115">Modificación de app.js e instalación de módulos</span><span class="sxs-lookup"><span data-stu-id="e4154-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="e4154-116">Cambie el nombre del archivo **index.js** a **app.js**.</span><span class="sxs-lookup"><span data-stu-id="e4154-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="e4154-117">Esto permite a Azure detectar que se trata de una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="e4154-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="e4154-118">Abra el archivo **app.js** en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e4154-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="e4154-119">Cambie la línea que contiene `var io = require('../..')(server);` como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e4154-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="e4154-120">Abra el archivo **package.json** y agregue una referencia a socket.io en `dependencies`, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e4154-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="e4154-121">En la línea de comandos, cambie al directorio **\\node\\chat** y use npm para instalar los módulos necesarios para esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="e4154-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="e4154-122">Esto instalará los módulos en una subcarpeta denominada **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="e4154-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="e4154-123">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="e4154-123">Create an Azure Web App</span></span>
<span data-ttu-id="e4154-124">Siga estos pasos para crear una aplicación web de Azure, habilite la publicación Git y, a continuación, habilite la compatibilidad de WebSocket para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e4154-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="e4154-125">Para completar este tutorial, deberá tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="e4154-126">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="e4154-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e4154-127">Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="e4154-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="e4154-128">Instale la interfaz de la línea de comandos de Azure (CLI de Azure) y conéctese a su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="e4154-129">Consulte [Instalación y configuración de la interfaz de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e4154-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="e4154-130">Si esta es la primera vez que configura un repositorio en Azure, tendrá que crear unas credenciales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e4154-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="e4154-131">En la CLI de Azure, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4154-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="e4154-132">Cambie al directorio **\\node\chat** y use el siguiente comando para crear una nueva aplicación web de Azure y un repositorio de Git local.</span><span class="sxs-lookup"><span data-stu-id="e4154-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="e4154-133">Este comando también crea un Git remoto llamado "azure".</span><span class="sxs-lookup"><span data-stu-id="e4154-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="e4154-134">Debe reemplazar "mysitename" por un nombre único para su sitio web.</span><span class="sxs-lookup"><span data-stu-id="e4154-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="e4154-135">Confirme los archivos existentes en el repositorio local usando los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e4154-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="e4154-136">Inserte los archivos en el repositorio de la aplicación web de Azure con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4154-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="e4154-137">Cuando se le solicite, escriba las credenciales del paso 2.</span><span class="sxs-lookup"><span data-stu-id="e4154-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="e4154-138">Recibirá mensajes de estado a medida que los módulos se importen en el servidor.</span><span class="sxs-lookup"><span data-stu-id="e4154-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="e4154-139">Después de que se haya completado este proceso, la aplicación se hospedará en su aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4154-140">Durante la instalación de módulos, es posible que aparezcan errores del tipo "No se ha encontrado el proyecto importado...".</span><span class="sxs-lookup"><span data-stu-id="e4154-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="e4154-141">Se pueden ignorar con seguridad.</span><span class="sxs-lookup"><span data-stu-id="e4154-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="e4154-142">Socket.IO usa WebSockets, que no están habilitados de manera predeterminada en Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="e4154-143">Para habilitar los sockets web, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4154-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="e4154-144">Si se solicita, escriba el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="e4154-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4154-145">El comando "azure site set -w" solo funcionará con la versión 0.7.4 o superior de la interfaz de la línea de comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="e4154-146">También puede habilitar la compatibilidad con WebSocket usando el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e4154-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="e4154-147">Para habilitar WebSockets con Azure Portal, haga clic en la aplicación web en la hoja Web Apps, haga clic en **Toda la configuración** > **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="e4154-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="e4154-148">En **Web Sockets**, haga clic en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="e4154-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="e4154-149">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e4154-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="e4154-150">Para ver la aplicación web en Azure, use el siguiente comando para iniciar su explorador web y desplazarse a la aplicación web hospedada:</span><span class="sxs-lookup"><span data-stu-id="e4154-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="e4154-151">Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="e4154-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="e4154-152">Escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="e4154-152">Scale out</span></span>
<span data-ttu-id="e4154-153">Las aplicaciones Socket.IO se pueden escalar horizontalmente con un **adaptador** para distribuir mensajes y eventos entre varias instancias de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e4154-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="e4154-154">Aunque hay varios adaptadores disponibles, el adaptador [socket.io-redis] se puede utilizar fácilmente con la característica de Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="e4154-155">Un requisito adicional para el escalado horizontal de una solución Socket.IO es la compatibilidad con sesiones persistentes.</span><span class="sxs-lookup"><span data-stu-id="e4154-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="e4154-156">Las sesiones persistentes se habilitan de manera predeterminada en las aplicaciones web de Azure con el enrutamiento de solicitudes de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="e4154-157">Para obtener más información, consulte [Afinidad de instancias en Sitios web de Azure].</span><span class="sxs-lookup"><span data-stu-id="e4154-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="e4154-158">Crear una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="e4154-158">Create a Redis cache</span></span>
<span data-ttu-id="e4154-159">Realice los pasos de [Creación de una memoria caché en Caché en Redis de Azure] para crear una caché nueva.</span><span class="sxs-lookup"><span data-stu-id="e4154-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="e4154-160">Guarde el **Nombre de host** y la **Clave principal** de la caché, ya que los necesitará en los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="e4154-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="e4154-161">Agregue los módulos redis y socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="e4154-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="e4154-162">En una línea de comandos, cambie al directorio **\\node\\chat** y use el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="e4154-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="e4154-163">Las versiones indicadas en este comando son la sutilizadas al hacer las pruebas de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e4154-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="e4154-164">Modifique el archivo **app.js** para agregar la siguientes líneas inmediatamente después de `var io = require('socket.io')(server);`.</span><span class="sxs-lookup"><span data-stu-id="e4154-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="e4154-165">Reemplace **redishostname** y **rediskey** por el nombre de host y la clave de la caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="e4154-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="e4154-166">Esto creará un cliente de publicación y suscripción a la caché de Redis creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e4154-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="e4154-167">Entonces los clientes se utilizarán con el adaptador para configurar Socket.IO y utilizar la caché de Redis para pasar mensajes y eventos entre instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4154-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e4154-168">Aunque el adaptador **socket.io-redis** se puede comunicar directamente con Redis, la versión actual no es compatible con la autenticación que requiere Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="e4154-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="e4154-169">Por tanto, la conexión inicial se crea con el módulo **redis**; a continuación, el cliente se pasa al adaptador **socket.io-redis**.</span><span class="sxs-lookup"><span data-stu-id="e4154-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="e4154-170">Aunque la caché de Redis de Azure es compatible con las conexiones seguras que utilizan el puerto 6380, los módulos usados en este ejemplo no son compatibles con las conexiones seguras a partir del 14/07/2014.</span><span class="sxs-lookup"><span data-stu-id="e4154-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="e4154-171">El código anterior utiliza el puerto predeterminado no seguro 6379.</span><span class="sxs-lookup"><span data-stu-id="e4154-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="e4154-172">Guarde el archivo **app.js** modificado</span><span class="sxs-lookup"><span data-stu-id="e4154-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="e4154-173">Confirmar cambios y volver a implementar</span><span class="sxs-lookup"><span data-stu-id="e4154-173">Commit changes and redeploy</span></span>
<span data-ttu-id="e4154-174">En la línea de comandos del directorio **\\node\\chat**, utilice los siguientes comandos para confirmar los cambios y volver a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4154-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="e4154-175">Cuando los cambios se hayan enviado al servidor, puede escalar su sitio por varias instancias con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="e4154-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="e4154-176">Donde **#** es el número de instancias que se van a crear.</span><span class="sxs-lookup"><span data-stu-id="e4154-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="e4154-177">Puede conectarse a la aplicación web desde varios exploradores o equipos para verificar que los mensajes se envían correctamente a todos los clientes.</span><span class="sxs-lookup"><span data-stu-id="e4154-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e4154-178">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e4154-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="e4154-179">Límites de conexión</span><span class="sxs-lookup"><span data-stu-id="e4154-179">Connection limits</span></span>
<span data-ttu-id="e4154-180">Aplicaciones web de Azure está disponible en varios SKU, lo que determina los recursos disponibles en su sitio.</span><span class="sxs-lookup"><span data-stu-id="e4154-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="e4154-181">Esto incluye el número permitido de conexiones WebSocket.</span><span class="sxs-lookup"><span data-stu-id="e4154-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="e4154-182">Para obtener más información, consulte la [página Precios de aplicaciones web].</span><span class="sxs-lookup"><span data-stu-id="e4154-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="e4154-183">No se están enviando los mensajes con WebSockets</span><span class="sxs-lookup"><span data-stu-id="e4154-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="e4154-184">Si los exploradores de los clientes siguen recurriendo al sondeo largo en lugar de utilizar WebSockets, tal vez se deba a uno de estos motivos.</span><span class="sxs-lookup"><span data-stu-id="e4154-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="e4154-185">**Intente limitar el transporte a solo WebSockets**</span><span class="sxs-lookup"><span data-stu-id="e4154-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="e4154-186">Para que Socket.IO utilice WebSockets como transporte de mensajes, tanto el servidor como el cliente deben ser compatibles con WebSockets.</span><span class="sxs-lookup"><span data-stu-id="e4154-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="e4154-187">Si uno o el otro no lo son, Socket.IO negociará otro transporte, como el sondeo largo.</span><span class="sxs-lookup"><span data-stu-id="e4154-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="e4154-188">La lista predeterminada de transportes utilizados por Socket.IO es ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="e4154-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="e4154-189">Puede forzarlo a que solo utilice WebSockets si agrega el siguiente código al archivo **app.js**, después de la línea que contiene `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="e4154-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="e4154-190">Tenga en cuenta que los exploradores más antiguos que no son compatibles con WebSockets no podrán conectarse al sitio, aunque el código anterior esté activo, ya que restringe la comunicación solo a WebSockets.</span><span class="sxs-lookup"><span data-stu-id="e4154-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="e4154-191">**Uso de SSL**</span><span class="sxs-lookup"><span data-stu-id="e4154-191">**Use SSL**</span></span>
  
    <span data-ttu-id="e4154-192">WebSockets depende de algunos encabezados HTTP menos utilizados, como el encabezado **Upgrade** .</span><span class="sxs-lookup"><span data-stu-id="e4154-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="e4154-193">Algunos dispositivos de red intermedios, como los proxy web, pueden quitar estos encabezados.</span><span class="sxs-lookup"><span data-stu-id="e4154-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="e4154-194">Para evitar este problema, puede establecer la conexión WebSocket por SSL.</span><span class="sxs-lookup"><span data-stu-id="e4154-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="e4154-195">Una manera sencilla de conseguirlo es configurar Socket.IO en `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="e4154-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="e4154-196">Esto envía instrucciones a Socket.IO para asegurar la comunicación de WebSockets al igual que la solicitud HTTP/HTTPS original para la página web.</span><span class="sxs-lookup"><span data-stu-id="e4154-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="e4154-197">Si un explorador utiliza una URL HTTPS para visitar su sitio web, las comunicaciones consiguientes de WebSocket a través de Socket.IO se asegurarán con SSL.</span><span class="sxs-lookup"><span data-stu-id="e4154-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="e4154-198">Para modificar este ejemplo y habilitar esta configuración, agregue el siguiente código al archivo **app.js**, después de la línea que contiene `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="e4154-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="e4154-199">**Comprobación de la configuración de web.config**</span><span class="sxs-lookup"><span data-stu-id="e4154-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="e4154-200">Las aplicaciones web de Azure que hospedan aplicaciones Node.js utilizan el archivo **web.config** para enrutar las solicitudes entrantes a la aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="e4154-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="e4154-201">Para que WebSockets funcione correctamente con aplicaciones Node.js, **web.config** debe contener la siguiente entrada.</span><span class="sxs-lookup"><span data-stu-id="e4154-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="e4154-202">Esto deshabilita el módulo WebSockets de IIS, que incluye su propia implementación de WebSockets y entra en conflicto con módulos de WebSocket específicos de Node.js, como Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="e4154-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="e4154-203">Si esta línea no está presente o se establece en `true`, puede ser el motivo por el que el transporte de WebSocket no funciona para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="e4154-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="e4154-204">Normalmente, las aplicaciones Node.js no incluyen un archivo **web.config** , por lo que Sitios web Azure generará automáticamente uno para las aplicaciones Node.js cuando se implementan.</span><span class="sxs-lookup"><span data-stu-id="e4154-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="e4154-205">Como este archivo se genera automáticamente en el servidor, debe utilizar la URL FTP o FTPS en su sitio web para ver este archivo.</span><span class="sxs-lookup"><span data-stu-id="e4154-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="e4154-206">Puede encontrar las direcciones URL FTP y FTPS para su sitio en el Portal clásico si selecciona la aplicación web y después el vínculo **Panel** .</span><span class="sxs-lookup"><span data-stu-id="e4154-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="e4154-207">Las URL se muestran en la sección de **vista rápida** .</span><span class="sxs-lookup"><span data-stu-id="e4154-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e4154-208">Sitios web de Azure solo genera el archivo **web.config** si la aplicación no lo proporciona.</span><span class="sxs-lookup"><span data-stu-id="e4154-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="e4154-209">Si proporciona un archivo **web.config** en la raíz de su proyecto de aplicación, Aplicaciones web de Azure lo utilizará.</span><span class="sxs-lookup"><span data-stu-id="e4154-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="e4154-210">Si la entrada no está presente, o si se ha establecido en el valor de `true`, entonces deberá crear un **web.config** en la raíz de su aplicación Node.js y especificar un valor de `false`.</span><span class="sxs-lookup"><span data-stu-id="e4154-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="e4154-211">Como referencia, a continuación se muestra el **web.config** predeterminado para una aplicación que usa **app.js** como punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="e4154-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="e4154-212">Si la aplicación usa un punto de entrada distinto de **app.js**, debe reemplazar todas las apariciones de **app.js** con el punto de entrada correcto.</span><span class="sxs-lookup"><span data-stu-id="e4154-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="e4154-213">Por ejemplo, reemplazando **app.js** por **server.js**.</span><span class="sxs-lookup"><span data-stu-id="e4154-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="e4154-214">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [App Service], donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e4154-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e4154-215">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="e4154-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e4154-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4154-216">Next steps</span></span>
<span data-ttu-id="e4154-217">En este tutorial aprendió a crear una aplicación de chat hospedada en una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="e4154-218">También puede hospedar esta aplicación como un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e4154-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="e4154-219">Para conocer los pasos para lograr esto, consulte [Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="e4154-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="e4154-220">Para obtener más información, consulte también el [Centro para desarrolladores de Node.js].</span><span class="sxs-lookup"><span data-stu-id="e4154-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e4154-221">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="e4154-221">What's changed</span></span>
* <span data-ttu-id="e4154-222">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes].</span><span class="sxs-lookup"><span data-stu-id="e4154-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="e4154-223">[Caché en Redis de Azure]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="e4154-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="e4154-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="e4154-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="e4154-225">[página Precios de aplicaciones web]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="e4154-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="e4154-226">[Creación de una aplicación de chat Node.js con Socket.IO en Servicio en la nube de Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="e4154-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="e4154-227">[Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="e4154-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="e4154-228">[Centro para desarrolladores de Node.js]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="e4154-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="e4154-229">[App Service]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="e4154-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="e4154-230">[Afinidad de instancias en Sitios web de Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="e4154-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="e4154-231">[Creación de una memoria caché en Caché en Redis de Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="e4154-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="e4154-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="e4154-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="e4154-233">[repositorio de Socket.IO GitHub]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="e4154-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="e4154-234">[versión archivada ZIP o GZ]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="e4154-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
