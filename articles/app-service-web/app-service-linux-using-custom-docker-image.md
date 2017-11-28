---
title: Uso de una imagen personalizada de Docker para Web App on Linux de Azure | Microsoft Docs
description: Uso de una imagen personalizada de Docker para Web App on Linux de Azure
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
ms.openlocfilehash: 1458217a31c4781b28877c030a665f5b22819e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a><span data-ttu-id="fbf7f-104">Uso de una imagen personalizada de Docker para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="fbf7f-104">Using a custom Docker image for Azure Web App on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="fbf7f-105">App Service proporciona pilas de aplicaciones predefinidas en Linux con compatibilidad para versiones específicas, como PHP 7.0 y Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="fbf7f-106">App Service en Linux utiliza contenedores de Docker para hospedar estas pilas de aplicaciones incorporadas.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="fbf7f-107">También puede usar una imagen personalizada de Docker para implementar la aplicación web a una pila de aplicaciones aún sin definir en Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="fbf7f-108">Las imágenes de Docker personalizadas se pueden hospedar en un repositorio de Docker público o privado.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="fbf7f-109">Establecimiento de una imagen de Docker personalizada para una aplicación web</span><span class="sxs-lookup"><span data-stu-id="fbf7f-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="fbf7f-110">Puede establecer la imagen de Docker personalizada para aplicaciones web nuevas y existentes.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="fbf7f-111">Cuando cree una nueva aplicación web en Linux en [Azure Portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), haga clic en **Configurar contenedor** para establecer una imagen de Docker personalizada:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), click **Configure container** to set a custom Docker image:</span></span>

![Imagen de Docker personalizada para una nueva aplicación web en Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="fbf7f-113">Uso de una imagen personalizada de Docker de Docker Hub</span><span class="sxs-lookup"><span data-stu-id="fbf7f-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="fbf7f-114">Para usar una imagen personalizada de Docker de Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="fbf7f-115">En [Azure Portal](https://portal.azure.com), busque la aplicación web en Linux y, en **Configuración**, haga clic en **Contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="fbf7f-116">Seleccione **Docker Hub** como **Origen de imagen**, haga clic en **Pública** o **Privada** y escriba nombre en **Imagen y etiqueta opcional (por ejemplo, 'image:tag')**, como `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="fbf7f-117">El **Comando de inicio** se establece automáticamente basándose en lo que se definió en el archivo de imagen de Docker, pero puede establecer sus propios comandos.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Configuración de la imagen del repositorio público de Docker Hub][2]

    <span data-ttu-id="fbf7f-119">Cuando la imagen pertenece a un repositorio privado, también tendrá que especificar las credenciales de Docker Hub (**nombre de usuario de inicio de sesión** y **contraseña**) para el repositorio de Docker Hub privado.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Configuración de la imagen del repositorio privado de Docker Hub][3]

3. <span data-ttu-id="fbf7f-121">Después de haber configurado el contenedor, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="fbf7f-122">Uso de una imagen de Docker de un registro de imágenes privado</span><span class="sxs-lookup"><span data-stu-id="fbf7f-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="fbf7f-123">Para usar una imagen de Docker de un registro de imágenes privado:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="fbf7f-124">En [Azure Portal](https://portal.azure.com), busque la aplicación web en Linux y, en **Configuración**, haga clic en **Contenedor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="fbf7f-125">Haga clic en **Registro privado** como **Origen de imagen**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="fbf7f-126">Especifique valores para el **nombre de la imagen y la etiqueta opcional** y la **dirección URL del servidor** para el registro privado, junto con las credenciales (**nombre de usuario de inicio de sesión** y **contraseña**).</span><span class="sxs-lookup"><span data-stu-id="fbf7f-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="fbf7f-127">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-127">Click **Save**.</span></span>

    ![Configuración de la imagen de Docker del registro privado][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="fbf7f-129">Establecimiento del puerto que usa la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="fbf7f-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="fbf7f-130">Cuando use una imagen personalizada de Docker para la aplicación web, puede usar la variable de entorno `WEBSITES_PORT` en el Dockerfile, que se agrega al contenedor generado.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-130">When you use a custom Docker image for your web app, you can use the `WEBSITES_PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="fbf7f-131">Tenga en cuenta el siguiente ejemplo de archivo de Docker para una aplicación Ruby:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

<span data-ttu-id="fbf7f-132">En la última línea del comando, puede ver que la variable de entorno de WEBSITES_PORT se pasa en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-132">On last line of the command, you can see that the WEBSITES_PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="fbf7f-133">Recuerde que en los comandos se distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="fbf7f-134">Anteriormente la plataforma utilizaba el parámetro de la aplicación `PORT`. Tenemos previsto dejar de usar este parámetro de la aplicación y usar `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-134">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="fbf7f-135">Al usar una imagen de Docker existente creada por otra persona, para la aplicación debe especificar un puerto distinto al 80.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-135">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="fbf7f-136">Para configurar el puerto, agregue una configuración de la aplicación llamada `WEBSITES_PORT` con el valor tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-136">To configure the port, add an application setting named `WEBSITES_PORT` with the value as shown below:</span></span>

![Configuración de aplicación PORT para una imagen personalizada de Docker][6]

## <a name="how-to-set-the-startup-time-for-your-docker-image"></a><span data-ttu-id="fbf7f-138">Establecimiento de la hora de inicio de la imagen de Docker</span><span class="sxs-lookup"><span data-stu-id="fbf7f-138">How to: set the startup time for your Docker image</span></span> ##

<span data-ttu-id="fbf7f-139">De forma predeterminada, si el contenedor no se inicia antes de 230 segundos, la plataforma reiniciará el contenedor.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-139">By default, if your container does not start before 230 seconds, the platform will restart your container.</span></span> <span data-ttu-id="fbf7f-140">Si la imagen de Docker personalizada se inicia en más de 230 segundos, puede usar el valor de aplicación `WEBSITES_CONTAINER_START_TIME_LIMIT`, el valor de este ajuste está en segundos, lo que va a permitir que la plataforma mantenga el contenedor en funcionamiento antes de reiniciarlo.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-140">If your custom Docker image starts in more than 230 seconds, you can use the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting, the value for this setting is in seconds, this will allow the platform keep your container running before restarting it.</span></span> <span data-ttu-id="fbf7f-141">El valor predeterminado es de 230 segundos y el valor máximo permitido es de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-141">The default value is 230 seconds, and the max allowed value is 600 seconds.</span></span>

## <a name="how-to-unmount-the-platform-provided-storage"></a><span data-ttu-id="fbf7f-142">Desmontaje del almacenamiento proporcionado por la plataforma</span><span class="sxs-lookup"><span data-stu-id="fbf7f-142">How to: unmount the platform provided storage</span></span> ##

<span data-ttu-id="fbf7f-143">De forma predeterminada, la plataforma montará un recurso compartido de almacenamiento persistente en el directorio `\home\`.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-143">By default, the platform will mount a persistent storage share to the `\home\` directory.</span></span> <span data-ttu-id="fbf7f-144">Si la imagen de contenedor no necesita un recurso compartido persistente, puede deshabilitar el montaje de ese almacenamiento estableciendo la configuración de la aplicación `WEBSITES_ENABLE_APP_SERVICE_STORAGE` en `false`.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-144">If your container image does not need a persistent share, you can disable mounting that storage by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span> <span data-ttu-id="fbf7f-145">Todavía seguirá teniendo acceso a ese almacenamiento desde el sitio SCM y todos los registros de Docker (si están habilitados) se escribirán en los archivos de registro generados por la plataforma.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-145">You will still have access to that storage from the scm site, and all Docker logs (if enabled) will be written to the log files generated by the platform.</span></span>

## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="fbf7f-146">Cambio para usar una imagen incorporada</span><span class="sxs-lookup"><span data-stu-id="fbf7f-146">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="fbf7f-147">Para cambiar de una imagen personalizada a una incorporada:</span><span class="sxs-lookup"><span data-stu-id="fbf7f-147">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="fbf7f-148">En [Azure Portal](https://portal.azure.com), busque la aplicación web en Linux y, en **Configuración**, haga clic en **App Service**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-148">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="fbf7f-149">Seleccione la **Pila en tiempo de ejecución** para utilizar para la imagen incorporada y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-149">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Configuración de una imagen de Docker incorporada][5]


## <a name="troubleshooting"></a><span data-ttu-id="fbf7f-151">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="fbf7f-151">Troubleshooting</span></span> ##

<span data-ttu-id="fbf7f-152">Cuando la aplicación no se inicia con la imagen de Docker personalizada, compruebe que el Docker registra en el directorio LogFiles.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-152">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="fbf7f-153">A este directorio se accede a través del sitio SCM o a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-153">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="fbf7f-154">Para registrar `stdout` y `stderr` del contenedor, debe habilitar **Registros de contenedor de Docker** en **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-154">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitación del registro][8]

![Uso de Kudu para ver registros de Docker][7]

<span data-ttu-id="fbf7f-157">Puede acceder al sitio SCM desde **Advanced Tools** (Herramientas avanzadas) en el menú **Herramientas de desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-157">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbf7f-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fbf7f-158">Next Steps</span></span> ##

<span data-ttu-id="fbf7f-159">Siga los siguientes vínculos para empezar a trabajar con Web App on Linux.</span><span class="sxs-lookup"><span data-stu-id="fbf7f-159">Follow the following links to get started with Web App on Linux.</span></span>   

* [<span data-ttu-id="fbf7f-160">Introducción a Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="fbf7f-160">Introduction to Azure Web App on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="fbf7f-161">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="fbf7f-161">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="fbf7f-162">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fbf7f-162">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="fbf7f-163">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="fbf7f-163">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
