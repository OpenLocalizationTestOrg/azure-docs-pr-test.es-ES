---
title: "aaaCreate una aplicación de chat de Node.js con Socket.IO en el servicio de aplicación de Azure"
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="443b9-103">Creación de una aplicación de chat Node.js con Socket.IO en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="443b9-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="443b9-104">Socket.IO proporciona comunicación en tiempo real entre su servidor node.js y los clientes con WebSockets.</span><span class="sxs-lookup"><span data-stu-id="443b9-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="443b9-105">También es compatible con los transportes de reserva tooother (por ejemplo, el sondeo prolongado) que funcionan con los exploradores más antiguos.</span><span class="sxs-lookup"><span data-stu-id="443b9-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="443b9-106">Este tutorial se le guían a través de aloja una aplicación de chat Socket.IO según como una aplicación web de Azure y le muestran cómo tooscale Hola aplicación usando [Azure Redis Cache].</span><span class="sxs-lookup"><span data-stu-id="443b9-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="443b9-107">Para obtener más información sobre Socket.IO, consulte <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="443b9-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="443b9-108">procedimientos de Hello en esta tarea se aplican demasiado[aplicación del servicio de aplicaciones Web]; para servicios en la nube, consulte [compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="443b9-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="443b9-109">Descargar el ejemplo de Hola chat</span><span class="sxs-lookup"><span data-stu-id="443b9-109">Download hello chat example</span></span>
<span data-ttu-id="443b9-110">Para este proyecto, usaremos hello (ejemplo) chat de hello [repositorio de Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="443b9-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="443b9-111">Realizar Hola siguiente ejemplo de Hola toodownload de pasos y Agregar proyecto toohello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="443b9-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="443b9-112">Descargar un [ZIP o GZ archivado versión] del proyecto de hello Socket.IO (versión 1.3.5 se utilizó para este documento)</span><span class="sxs-lookup"><span data-stu-id="443b9-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="443b9-113">Extraer Hola Hola de archivo y copia **ejemplos\\chat** tooa nueva ubicación de directorio.</span><span class="sxs-lookup"><span data-stu-id="443b9-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="443b9-114">Por ejemplo, **\\nodo\\chat**.</span><span class="sxs-lookup"><span data-stu-id="443b9-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="443b9-115">Modificación de app.js e instalación de módulos</span><span class="sxs-lookup"><span data-stu-id="443b9-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="443b9-116">Cambiar el nombre de hello **index.js** archivo demasiado**app.js**.</span><span class="sxs-lookup"><span data-stu-id="443b9-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="443b9-117">Esto permite que toodetect de Azure que se trata de una aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="443b9-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="443b9-118">Abra hello **app.js** archivo en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="443b9-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="443b9-119">Que contiene la línea de saludo de cambio `var io = require('../..')(server);` tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="443b9-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="443b9-120">Abra hello **package.json** de archivos y agregue un toosocket.io de referencia en `dependencies`, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="443b9-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="443b9-121">Desde la línea de comandos de hello, cambiar toohello  **\\nodo\\chat** directorio y uso tooinstall Hola módulos npm requeridos por la aplicación:</span><span class="sxs-lookup"><span data-stu-id="443b9-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="443b9-122">Este modo se instalará módulos hello en una subcarpeta denominada **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="443b9-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="443b9-123">Creación de una aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="443b9-123">Create an Azure Web App</span></span>
<span data-ttu-id="443b9-124">Siga estos toocreate pasos una aplicación web de Azure, habilitar la publicación de Git y, a continuación, habilitar la compatibilidad de WebSocket para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="443b9-125">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="443b9-126">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="443b9-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="443b9-127">Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="443b9-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="443b9-128">Instale hello Azure interfaz de línea de comandos (CLI de Azure) y conecte tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="443b9-129">Vea [instalar y configurar hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="443b9-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="443b9-130">Si se trata de la primera configuración de tiempo de un repositorio de Azure, necesita credenciales de inicio de sesión de toocreate.</span><span class="sxs-lookup"><span data-stu-id="443b9-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="443b9-131">En el saludo CLI de Azure, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="443b9-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="443b9-132">Cambiar toohello  **\\node\chat** directorio y siguientes de Hola de uso de comandos toocreate una nueva aplicación web de Azure y un repositorio Git local.</span><span class="sxs-lookup"><span data-stu-id="443b9-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="443b9-133">Este comando también crea un Git remoto llamado "azure".</span><span class="sxs-lookup"><span data-stu-id="443b9-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="443b9-134">Debe reemplazar "mysitename" por un nombre único para su sitio web.</span><span class="sxs-lookup"><span data-stu-id="443b9-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="443b9-135">Confirmar repositorio local de hello existente archivos toohello mediante el uso de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="443b9-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="443b9-136">Insertar repositorio de aplicaciones Web de Azure de hello archivos toohello con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="443b9-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="443b9-137">Cuando se le solicite, escriba las credenciales del paso 2.</span><span class="sxs-lookup"><span data-stu-id="443b9-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="443b9-138">Recibirá mensajes de estado de los módulos se importan en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="443b9-139">Cuando haya completado este proceso, la aplicación hello se hospedará en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="443b9-140">Durante la instalación del módulo, es podrán que encuentre errores que ' hello proyecto importado... no se encontró '.</span><span class="sxs-lookup"><span data-stu-id="443b9-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="443b9-141">Se pueden ignorar con seguridad.</span><span class="sxs-lookup"><span data-stu-id="443b9-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="443b9-142">Socket.IO usa WebSockets, que no están habilitados de manera predeterminada en Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="443b9-143">tooenable web sockets, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="443b9-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="443b9-144">Si se le pide, escriba el nombre de Hola de aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="443b9-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="443b9-145">Hola will de comando 'sitio de azure set -w' sólo funcionan con la versión 0.7.4 o posterior del programa Hola a la interfaz de línea de comandos de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="443b9-146">También puede habilitar la compatibilidad de WebSocket con hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="443b9-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="443b9-147">uso de WebSockets de tooenable Hola Portal de Azure, haga clic en la aplicación web de hello de hoja de aplicaciones Web de hello, haga clic en **toda la configuración de** > **configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="443b9-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="443b9-148">En **Web Sockets**, haga clic en **Activado**.</span><span class="sxs-lookup"><span data-stu-id="443b9-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="443b9-149">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="443b9-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="443b9-150">tooview hello web aplicación en Azure, use a continuación Hola comando toolaunch el explorador web y navegar por la aplicación web de toohello hospedado:</span><span class="sxs-lookup"><span data-stu-id="443b9-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="443b9-151">Su aplicación se está ejecutando ahora en Azure y puede retransmitir los mensajes de chat entre los diferentes clientes que usan Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="443b9-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="443b9-152">Escalado horizontal</span><span class="sxs-lookup"><span data-stu-id="443b9-152">Scale out</span></span>
<span data-ttu-id="443b9-153">Aplicaciones de Socket.IO se pueden escalar horizontalmente mediante el uso de un **adaptador** toodistribute mensajes y eventos entre varias instancias de aplicación.</span><span class="sxs-lookup"><span data-stu-id="443b9-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="443b9-154">Aunque hay varios adaptadores, Hola [socket.io redis] adaptador se puede usar fácilmente con la característica de caché en Redis de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="443b9-155">Un requisito adicional para el escalado horizontal de una solución Socket.IO es la compatibilidad con sesiones persistentes.</span><span class="sxs-lookup"><span data-stu-id="443b9-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="443b9-156">Las sesiones persistentes se habilitan de manera predeterminada en las aplicaciones web de Azure con el enrutamiento de solicitudes de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="443b9-157">Para obtener más información, consulte [Afinidad de instancias en Sitios web de Azure].</span><span class="sxs-lookup"><span data-stu-id="443b9-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="443b9-158">Crear una caché de Redis</span><span class="sxs-lookup"><span data-stu-id="443b9-158">Create a Redis cache</span></span>
<span data-ttu-id="443b9-159">Realice los pasos de Hola de [crear una memoria caché en Redis de Azure] toocreate una nueva memoria caché.</span><span class="sxs-lookup"><span data-stu-id="443b9-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="443b9-160">Guardar hello **nombre de Host** y **clave principal** para la memoria caché, como estas se necesitará en Hola pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="443b9-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="443b9-161">Agregar redis hello y módulos socket.io redis</span><span class="sxs-lookup"><span data-stu-id="443b9-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="443b9-162">Desde una línea de comandos, cambiar toohello  **\\nodo\\chat** Hola de directorio y el uso siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="443b9-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="443b9-163">versiones de Hello especificadas en este comando son versiones de hello utilizadas al probar este artículo.</span><span class="sxs-lookup"><span data-stu-id="443b9-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="443b9-164">Modificar hello **app.js** siguientes de Hola de archivo tooadd líneas inmediatamente después de`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="443b9-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="443b9-165">Reemplace **redishostname** y **rediskey** con nombre de host de Hola y la clave de la memoria caché de Redis.</span><span class="sxs-lookup"><span data-stu-id="443b9-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="443b9-166">Esto creará una publicación y suscripción cliente toohello caché en Redis creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="443b9-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="443b9-167">los clientes de Hello, a continuación, se usan con hello adaptador tooconfigure caché en Redis hello Socket.IO toouse para pasar mensajes y eventos entre instancias de la aplicación</span><span class="sxs-lookup"><span data-stu-id="443b9-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="443b9-168">Mientras hello **socket.io redis** adaptador puede comunicarse directamente tooRedis, versión actual de hello no admite la autenticación de hello requerida por la caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="443b9-169">Por lo que la conexión inicial Hola se crea utilizando hello **redis** módulo, el cliente de hello, a continuación, se pasa toohello **socket.io redis** adaptador.</span><span class="sxs-lookup"><span data-stu-id="443b9-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="443b9-170">Mientras que caché en Redis de Azure admite conexiones seguras mediante el puerto 6380, módulos de hello usados en este ejemplo no admiten conexiones seguras a partir de 7/14/2014.</span><span class="sxs-lookup"><span data-stu-id="443b9-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="443b9-171">Hola por encima de código usa Hola de forma predeterminada, el puerto no seguro de 6379.</span><span class="sxs-lookup"><span data-stu-id="443b9-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="443b9-172">Hola guardar modificado **app.js**</span><span class="sxs-lookup"><span data-stu-id="443b9-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="443b9-173">Confirmar cambios y volver a implementar</span><span class="sxs-lookup"><span data-stu-id="443b9-173">Commit changes and redeploy</span></span>
<span data-ttu-id="443b9-174">Desde la línea de comandos en Hola Hola  **\\nodo\\chat** directorio, use Hola siguientes comandos toocommit cambios y volver a implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="443b9-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="443b9-175">Una vez que se hayan insertado cambios hello toohello server, puede escalar el sitio en varias instancias utilizando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="443b9-176">Donde  **#**  es Hola número de instancias toocreate.</span><span class="sxs-lookup"><span data-stu-id="443b9-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="443b9-177">Puede conectarse tooyour web app desde varios tooverify exploradores o equipos que los mensajes se envían correctamente los clientes de tooall.</span><span class="sxs-lookup"><span data-stu-id="443b9-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="443b9-178">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="443b9-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="443b9-179">Límites de conexión</span><span class="sxs-lookup"><span data-stu-id="443b9-179">Connection limits</span></span>
<span data-ttu-id="443b9-180">Las aplicaciones Web de Azure está disponible en varias SKU, que determinan el sitio de hello recursos tooyour disponible.</span><span class="sxs-lookup"><span data-stu-id="443b9-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="443b9-181">Esto incluye Hola número de conexiones permitidas de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="443b9-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="443b9-182">Para obtener más información, vea hello [página de precios de las aplicaciones Web].</span><span class="sxs-lookup"><span data-stu-id="443b9-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="443b9-183">No se están enviando los mensajes con WebSockets</span><span class="sxs-lookup"><span data-stu-id="443b9-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="443b9-184">Si los exploradores de cliente mantengan revirtiendo toolong sondeo en lugar de usar WebSockets, puede ser debido a uno de los siguientes Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="443b9-185">**Pruebe a limitar Hola transporte toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="443b9-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="443b9-186">Para Socket.IO toouse WebSockets como Hola transporte de mensajería, servidor hello y del cliente deben admitir WebSockets.</span><span class="sxs-lookup"><span data-stu-id="443b9-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="443b9-187">Si uno o hello otro no es así, Socket.IO negociará otro transporte, como el sondeo largo.</span><span class="sxs-lookup"><span data-stu-id="443b9-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="443b9-188">lista predeterminada de Hola de transportes utilizados por Socket.IO es ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="443b9-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="443b9-189">Puede forzar la tooonly use WebSockets agregando Hola después código toohello **app.js** archivo, después de la línea que contiene de hello `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="443b9-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="443b9-190">Observe que exploradores más antiguos que no admiten WebSockets no será capaz de tooconnect toohello sitio mientras Hola por encima del código está activa, tal y como se restringe únicamente tooWebSockets de comunicación.</span><span class="sxs-lookup"><span data-stu-id="443b9-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="443b9-191">**Uso de SSL**</span><span class="sxs-lookup"><span data-stu-id="443b9-191">**Use SSL**</span></span>
  
    <span data-ttu-id="443b9-192">WebSockets se basa en algunos encabezados HTTP menor uso, como Hola **actualizar** encabezado.</span><span class="sxs-lookup"><span data-stu-id="443b9-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="443b9-193">Algunos dispositivos de red intermedios, como los proxy web, pueden quitar estos encabezados.</span><span class="sxs-lookup"><span data-stu-id="443b9-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="443b9-194">tooavoid este problema, puede establecer la conexión de WebSocket de Hola a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="443b9-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="443b9-195">Una manera sencilla de tooaccomplish es demasiado tooconfigure Socket.IO`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="443b9-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="443b9-196">Esto indica a Hola de comunicación de WebSockets Socket.IO toosecure igual Hola HTTP/HTTPS que se originan de solicitud para la página web de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="443b9-197">Si un explorador utiliza una dirección URL HTTPS toovisit su sitio Web, se protegerán posteriores WebSocket las comunicaciones a través Socket.IO a través de SSL.</span><span class="sxs-lookup"><span data-stu-id="443b9-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="443b9-198">toomodify este tooenable ejemplo esta configuración, agregar Hola después código toohello **app.js** archivo después de la línea que contiene de hello `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="443b9-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="443b9-199">**Comprobación de la configuración de web.config**</span><span class="sxs-lookup"><span data-stu-id="443b9-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="443b9-200">Aplicaciones web de Azure que hospedan aplicaciones Node.js usan hello **web.config** tooroute archivo entrante solicita toohello Node.js aplicación.</span><span class="sxs-lookup"><span data-stu-id="443b9-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="443b9-201">Para WebSockets toofunction correctamente con aplicaciones Node.js, Hola **web.config** debe contener la siguiente entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="443b9-202">Esto deshabilita el módulo WebSockets de IIS de hello, que incluye su propia implementación de WebSockets y entra en conflicto con los módulos de WebSocket específicos de Node.js como Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="443b9-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="443b9-203">Si esta línea no está presente o se establece demasiado`true`, esto puede ser motivo de Hola que transporte de WebSocket de hello no funciona para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="443b9-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="443b9-204">Normalmente, las aplicaciones Node.js no incluyen un archivo **web.config** , por lo que Sitios web Azure generará automáticamente uno para las aplicaciones Node.js cuando se implementan.</span><span class="sxs-lookup"><span data-stu-id="443b9-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="443b9-205">Puesto que este archivo se genera automáticamente en el servidor de hello, debe usar Hola FTP o FTPS dirección URL para el sitio Web tooview este archivo.</span><span class="sxs-lookup"><span data-stu-id="443b9-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="443b9-206">Puede encontrar Hola FTP y FTPS direcciones URL para el sitio en el portal clásico de hello seleccionando la aplicación web y Hola, a continuación, **panel** vínculo.</span><span class="sxs-lookup"><span data-stu-id="443b9-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="443b9-207">Hello las direcciones URL aparecen en hello **vista rápida** sección.</span><span class="sxs-lookup"><span data-stu-id="443b9-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="443b9-208">Hola **web.config** archivo solo se genera por los sitios Web de Azure si la aplicación no proporciona uno.</span><span class="sxs-lookup"><span data-stu-id="443b9-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="443b9-209">Si proporciona un **web.config** archivo en la raíz de Hola de su proyecto de aplicación, se utilizará por aplicaciones Web de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="443b9-210">Si entrada hello no está presente o se establece el valor de tooa de `true`, a continuación, debe crear un **web.config** en Hola raíz de la aplicación Node.js y especifique un valor de `false`.</span><span class="sxs-lookup"><span data-stu-id="443b9-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="443b9-211">Como referencia, Hola siguiente es un valor predeterminado **web.config** para una aplicación que utiliza **app.js** como punto de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="443b9-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="443b9-212">Si la aplicación utiliza un punto de entrada distinto de **app.js**, debe reemplazar todas las apariciones de **app.js** con hello corregir el punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="443b9-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="443b9-213">Por ejemplo, reemplazando **app.js** por **server.js**.</span><span class="sxs-lookup"><span data-stu-id="443b9-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="443b9-214">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones], donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="443b9-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="443b9-215">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="443b9-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="443b9-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="443b9-216">Next steps</span></span>
<span data-ttu-id="443b9-217">En este tutorial ha aprendido cómo toocreate una aplicación de chat hospedada en una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="443b9-218">También puede hospedar esta aplicación como un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="443b9-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="443b9-219">Para conocer los pasos sobre cómo tooaccomplish, vea [compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="443b9-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="443b9-220">Para obtener más información, vea también hello [Centro para desarrolladores de Node.js].</span><span class="sxs-lookup"><span data-stu-id="443b9-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="443b9-221">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="443b9-221">What's changed</span></span>
* <span data-ttu-id="443b9-222">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente].</span><span class="sxs-lookup"><span data-stu-id="443b9-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[aplicación del servicio de aplicaciones Web]: http://go.microsoft.com/fwlink/?LinkId=529714
[página de precios de las aplicaciones Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[compilar una aplicación de Chat de Node.js con Socket.IO en un servicio de nube de Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro para desarrolladores de Node.js]: /develop/nodejs/
[pruebe el servicio de aplicaciones]: https://azure.microsoft.com/try/app-service/
[Afinidad de instancias en Sitios web de Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[crear una memoria caché en Redis de Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[repositorio de Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP o GZ archivado versión]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
