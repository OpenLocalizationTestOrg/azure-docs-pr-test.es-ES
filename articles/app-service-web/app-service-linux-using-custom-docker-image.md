---
title: "aaaHow toouse una imagen personalizada de Docker para la aplicación Web de Azure en Linux | Documentos de Microsoft"
description: "¿Cómo toouse una Docker personalizada de imágenes para la aplicación Web de Azure en Linux."
keywords: "azure app service, aplicación web, linux, docker, contenedor"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="956cb-104">Uso de una imagen personalizada de Docker para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="956cb-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="956cb-105">App Service proporciona pilas de aplicaciones predefinidas en Linux con compatibilidad para versiones específicas, como PHP 7.0 y Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="956cb-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="956cb-106">Servicio de aplicaciones en Linux utiliza contenedores de Docker toohost estos pregeneradas pilas de aplicación.</span><span class="sxs-lookup"><span data-stu-id="956cb-106">App Service on Linux uses Docker containers toohost these pre-built application stacks.</span></span> <span data-ttu-id="956cb-107">También puede utilizar un toodeploy de imagen de Docker personalizado en el bloque de aplicación de tooan de aplicación web que no se ha definido en Azure.</span><span class="sxs-lookup"><span data-stu-id="956cb-107">You can also use a custom Docker image toodeploy your web app tooan application stack that is not already defined in Azure.</span></span> <span data-ttu-id="956cb-108">Las imágenes de Docker personalizadas se pueden hospedar en un repositorio de Docker público o privado.</span><span class="sxs-lookup"><span data-stu-id="956cb-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="956cb-109">Establecimiento de una imagen de Docker personalizada para una aplicación web</span><span class="sxs-lookup"><span data-stu-id="956cb-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="956cb-110">Puede establecer la imagen de Docker personalizada hello para las nuevas y las aplicaciones Web existentes.</span><span class="sxs-lookup"><span data-stu-id="956cb-110">You can set hello custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="956cb-111">Cuando se crea una aplicación web en Linux en hello [portal de Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), haga clic en **configurar contenedor** tooset una imagen de Docker personalizada:</span><span class="sxs-lookup"><span data-stu-id="956cb-111">When you create a web app on Linux in hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** tooset a custom Docker image:</span></span>

![Imagen de Docker personalizada para una nueva aplicación web en Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="956cb-113">Uso de una imagen personalizada de Docker de Docker Hub</span><span class="sxs-lookup"><span data-stu-id="956cb-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="956cb-114">toouse una imagen personalizada de Docker de Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="956cb-114">toouse a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="956cb-115">Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **contenedor Docker**.</span><span class="sxs-lookup"><span data-stu-id="956cb-115">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="956cb-116">Seleccione **Docker Hub** como hello **origen de la imagen**, a continuación, haga clic en **público** o **privada** tipo hello y **imagen y nombre de etiqueta opcional**, como `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="956cb-116">Select **Docker Hub** as hello **Image source**, then click either **Public** or **Private** and type hello **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="956cb-117">Hola **comando de inicio** se establece automáticamente basándose en la que se define en el archivo de imagen de Docker de hello, pero puede establecer sus propios comandos.</span><span class="sxs-lookup"><span data-stu-id="956cb-117">hello **Startup command** is set automatically based on what is defined in hello Docker image file, but you can set your own commands.</span></span>  

    ![Configuración de la imagen del repositorio público de Docker Hub][2]

    <span data-ttu-id="956cb-119">Cuando la imagen está en un repositorio privado, también necesita credenciales de Docker Hub de hello tooenter como (**nombre de usuario de inicio de sesión** y **contraseña**) para el repositorio de Docker Hub privada Hola.</span><span class="sxs-lookup"><span data-stu-id="956cb-119">When your image is from a private repository, you also need tooenter hello Docker Hub credentials as (**Login username** and **Password**) for hello private Docker Hub repository.</span></span>

    ![Configuración de la imagen del repositorio privado de Docker Hub][3]

3. <span data-ttu-id="956cb-121">Después de haber configurado el contenedor de hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="956cb-121">After you have configured hello container, click **Save**.</span></span>

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="956cb-122">¿Cómo toouse una Docker la imagen de un registro de la imagen privada</span><span class="sxs-lookup"><span data-stu-id="956cb-122">How toouse a Docker image from a private image registry</span></span> ##
<span data-ttu-id="956cb-123">toouse una imagen personalizada de Docker desde un registro de la imagen privada:</span><span class="sxs-lookup"><span data-stu-id="956cb-123">toouse a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="956cb-124">Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **contenedor Docker**.</span><span class="sxs-lookup"><span data-stu-id="956cb-124">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="956cb-125">Haga clic en **registro privada** como hello **origen de la imagen**.</span><span class="sxs-lookup"><span data-stu-id="956cb-125">Click **Private registry** as hello **Image source**.</span></span> <span data-ttu-id="956cb-126">Escriba hello **imagen y el nombre de etiqueta opcional**, **dirección URL del servidor** para hello privada registro, junto con las credenciales de hello (**nombre de usuario de inicio de sesión** y **contraseña** ).</span><span class="sxs-lookup"><span data-stu-id="956cb-126">Enter hello **Image and optional tag name**, **Server URL** for hello private registry, along with hello credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="956cb-127">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="956cb-127">Click **Save**.</span></span>

    ![Configuración de la imagen de Docker del registro privado][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a><span data-ttu-id="956cb-129">Cómo: establecer puerto de hello utilizado por la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="956cb-129">How to: set hello port used by your Docker image</span></span> ##

<span data-ttu-id="956cb-130">Cuando se usa una imagen personalizada de Docker para la aplicación web, puede usar hello `WEBSITES_PORT` variable de entorno en el Dockerfile, que se agrega el contenedor toohello generado.</span><span class="sxs-lookup"><span data-stu-id="956cb-130">When you use a custom Docker image for your web app, you can use hello `WEBSITES_PORT` environment variable in your Dockerfile, which gets added toohello generated container.</span></span> <span data-ttu-id="956cb-131">Considere la posibilidad de hello siguiente ejemplo de un archivo de docker para una aplicación Ruby:</span><span class="sxs-lookup"><span data-stu-id="956cb-131">Consider hello following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="956cb-132">En la última línea de comandos de hello, puede ver que esa variable de entorno WEBSITES_PORT Hola se pasa en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="956cb-132">On last line of hello command, you can see that hello WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="956cb-133">Recuerde que en los comandos se distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="956cb-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="956cb-134">Anteriormente utilizaba plataforma hello `PORT` aplicación establecer, se está planeando toodeprecate Hola use esta configuración de aplicación y mover toousing `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="956cb-134">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="956cb-135">Cuando se usa una imagen de Docker existente creada por otra persona, puede necesitar toospecify un puerto distinto al puerto 80 para aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="956cb-135">When you use an existing Docker image built by someone else, you may need toospecify a port other than port 80 for hello application.</span></span> <span data-ttu-id="956cb-136">tooconfigure Hola puerto, agregue una configuración con nombre de la aplicación `WEBSITES_PORT` con el valor de hello tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="956cb-136">tooconfigure hello port, add an application setting named `WEBSITES_PORT` with hello value as shown below:</span></span>

![Configuración de aplicación PORT para una imagen personalizada de Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a><span data-ttu-id="956cb-138">Cómo: establecer la hora de inicio de hello para la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="956cb-138">How to: set hello startup time for your Docker image</span></span> ##

<span data-ttu-id="956cb-139">De forma predeterminada, si el contenedor no se inicia antes de 230 segundos, plataforma Hola reiniciará su contenedor.</span><span class="sxs-lookup"><span data-stu-id="956cb-139">By default, if your container does not start before 230 seconds, hello platform will restart your container.</span></span> <span data-ttu-id="956cb-140">Si la imagen personalizada de Docker se inicia en más de 230 segundos, puede usar hello `WEBSITES_CONTAINER_START_TIME_LIMIT` aplicación establecer, valor de Hola para esta configuración se encuentra en segundos, esto le permitirá Hola plataforma tenga el contenedor que se ejecuta antes de reiniciarlo.</span><span class="sxs-lookup"><span data-stu-id="956cb-140">If your custom Docker image starts in more than 230 seconds, you can use hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, hello value for this setting is in seconds, this will allow hello platform keep your container running before restarting it.</span></span> <span data-ttu-id="956cb-141">valor predeterminado de Hello es 230 segundos y máximo de hello permitido valor es 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="956cb-141">hello default value is 230 seconds, and hello max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-hello-platform-provided-storage"></a><span data-ttu-id="956cb-142">Cómo: desmontar el almacenamiento de la plataforma proporcionada de Hola</span><span class="sxs-lookup"><span data-stu-id="956cb-142">How to: unmount hello platform provided storage</span></span> ##

<span data-ttu-id="956cb-143">De forma predeterminada, plataforma Hola se puede montar un toohello del recurso compartido de almacenamiento persistente `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="956cb-143">By default, hello platform will mount a persistent storage share toohello `\home\` directory.</span></span> <span data-ttu-id="956cb-144">Si la imagen de contenedor no es necesario un recurso compartido persistente, puede deshabilitar que el almacenamiento de montaje por establecer hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicación establecer demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="956cb-144">If your container image does not need a persistent share, you can disable mounting that storage by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span> <span data-ttu-id="956cb-145">Todavía tendrá acceso toothat almacenamiento del sitio de scm hello y todos los registros de Docker (si está habilitado) se escribirán los archivos de registro de toohello generados por plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="956cb-145">You will still have access toothat storage from hello scm site, and all Docker logs (if enabled) will be written toohello log files generated by hello platform.</span></span>

## <a name="how-to-switch-back-toousing-a-built-in-image"></a><span data-ttu-id="956cb-146">Cómo: hacer que toousing una imagen integrada</span><span class="sxs-lookup"><span data-stu-id="956cb-146">How to: Switch back toousing a built-in image</span></span> ##

<span data-ttu-id="956cb-147">tooswitch del uso de un toousing de imagen personalizada una imagen integrada:</span><span class="sxs-lookup"><span data-stu-id="956cb-147">tooswitch from using a custom image toousing a built-in image:</span></span>

1. <span data-ttu-id="956cb-148">Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **servicio de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="956cb-148">In hello [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="956cb-149">Seleccione el **pila en tiempo de ejecución** toouse para la imagen integrada de hello, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="956cb-149">Select your **Runtime Stack** toouse for hello built-in image, then click **Save**.</span></span> 

![Configuración de una imagen de Docker incorporada][5]


## <a name="troubleshooting"></a><span data-ttu-id="956cb-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="956cb-151">Troubleshooting</span></span> ##

<span data-ttu-id="956cb-152">Cuando la aplicación no consigue toostart con la imagen de Docker personalizada, compruebe hello que docker registra en el directorio LogFiles de Hola.</span><span class="sxs-lookup"><span data-stu-id="956cb-152">When your application fails toostart with your custom Docker image, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="956cb-153">A este directorio se accede a través del sitio SCM o a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="956cb-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="956cb-154">Hola toolog `stdout` y `stderr` desde el contenedor, deberá tooenable **registro de contenedor de Docker** en **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="956cb-154">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitación del registro][8]

![Uso de los registros de Kudu tooview Docker][7]

<span data-ttu-id="956cb-157">Puede tener acceso a sitios SCM Hola de **herramientas avanzadas** en hello **herramientas de desarrollo** menú.</span><span class="sxs-lookup"><span data-stu-id="956cb-157">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="956cb-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="956cb-158">Next Steps</span></span> ##

<span data-ttu-id="956cb-159">Siga Hola después tooget vínculos a trabajar con la aplicación Web en Linux.</span><span class="sxs-lookup"><span data-stu-id="956cb-159">Follow hello following links tooget started with Web App on Linux.</span></span>   

* [<span data-ttu-id="956cb-160">Introducción tooAzure la aplicación Web en Linux</span><span class="sxs-lookup"><span data-stu-id="956cb-160">Introduction tooAzure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="956cb-161">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="956cb-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="956cb-162">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="956cb-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="956cb-163">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="956cb-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
