---
title: "Preguntas más frecuentes sobre Web App on Linux de Azure App Service | Microsoft Docs"
description: "Este artículo trata sobre las preguntas más frecuentes sobre Web App on Linux de Azure App Service."
keywords: "azure app service, web app, preguntas más frecuentes, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 6122f28b35d143ec26a379ae9aa8aee9bdaaff9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="236d7-104">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="236d7-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="236d7-105">Con el lanzamiento de Web App en Linux, estamos trabajando en incorporar características y realizar mejoras en nuestra plataforma.</span><span class="sxs-lookup"><span data-stu-id="236d7-105">With the release of Web App on Linux, we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="236d7-106">A continuación encontrará una serie de preguntas más frecuentes que nuestros clientes nos han formulado durante los últimos meses.</span><span class="sxs-lookup"><span data-stu-id="236d7-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="236d7-107">Si tiene alguna pregunta, comente el artículo y le responderemos en cuanto sea posible.</span><span class="sxs-lookup"><span data-stu-id="236d7-107">If you have a question, comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="236d7-108">Imágenes integradas</span><span class="sxs-lookup"><span data-stu-id="236d7-108">Built-in images</span></span>

<span data-ttu-id="236d7-109">**P:** Quiero bifurcar los contenedores de Docker integrados que ofrece la plataforma.</span><span class="sxs-lookup"><span data-stu-id="236d7-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="236d7-110">¿Dónde puedo encontrar esos archivos?</span><span class="sxs-lookup"><span data-stu-id="236d7-110">Where can I find those files?</span></span>

<span data-ttu-id="236d7-111">**R.:** Encontrará todos los archivos de Docker en [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="236d7-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="236d7-112">Puede encontrar todos los contenedores de Docker en [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="236d7-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="236d7-113">**P.:** ¿Cuál es el valor previsible para la sección del archivo de inicio cuando se configura la pila en tiempo de ejecución?</span><span class="sxs-lookup"><span data-stu-id="236d7-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="236d7-114">**R.:** Para Node.Js, puede especificar el archivo de configuración de PM2 o el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="236d7-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="236d7-115">Para .Net Core, debe especificar el nombre del archivo DLL compilado.</span><span class="sxs-lookup"><span data-stu-id="236d7-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="236d7-116">Para Ruby, puede especificar un script de Ruby con el que quiera inicializar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="236d7-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="236d7-117">Administración</span><span class="sxs-lookup"><span data-stu-id="236d7-117">Management</span></span>

<span data-ttu-id="236d7-118">**P.**: ¿Qué ocurre al hacer clic en botón de reinicio de Azure Portal?</span><span class="sxs-lookup"><span data-stu-id="236d7-118">**Q:** What happens when I press the restart button in the Azure portal?</span></span>

<span data-ttu-id="236d7-119">**R.**: Es el equivalente del reinicio de Docker.</span><span class="sxs-lookup"><span data-stu-id="236d7-119">**A:** This is the equivalent of Docker restart.</span></span>

<span data-ttu-id="236d7-120">**P.:** ¿Puedo usar Secure Shell (SSH) para conectarme a la máquina virtual de contenedor de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="236d7-120">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="236d7-121">**R.**: Sí, puede hacerlo a través del sitio SCM. Consulte el artículo siguiente para obtener más información: [Compatibilidad con SSH para Web App en Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="236d7-121">**A:** Yes, you can do that through the SCM site, check the following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="236d7-122">**P:** Deseo crear un plano de Linux App Service mediante SDK o una plantilla de ARM, ¿cómo puedo hacerlo?</span><span class="sxs-lookup"><span data-stu-id="236d7-122">**Q:** I want to create a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="236d7-123">**R:** Debe establecer el campo `reserved` del servicio de aplicaciones en `true`.</span><span class="sxs-lookup"><span data-stu-id="236d7-123">**A:** You need to set the `reserved` field of the app service to `true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="236d7-124">Integración e implementación continuas</span><span class="sxs-lookup"><span data-stu-id="236d7-124">Continuous integration/deployment</span></span>

<span data-ttu-id="236d7-125">**P:** ¿Mi aplicación web sigue usando una imagen de contenedor de Docker antigua después de actualizar la imagen en DockerHub?</span><span class="sxs-lookup"><span data-stu-id="236d7-125">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="236d7-126">¿Se admite la integración e implementación continuas de contenedores personalizados?</span><span class="sxs-lookup"><span data-stu-id="236d7-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="236d7-127">**R.**: Para configurar la integración e implementación continua de las imágenes de Azure Container Registry o Docker Hub consulte el siguiente artículo: [Implementación continua con Azure Web App en Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="236d7-127">**A:** To set up continuous integration/deployment for Azure Container Registry or DockerHub images by check the following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="236d7-128">Para registros privados, puede actualizar el contenedor deteniendo y, luego, iniciando la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="236d7-128">For private registries, you can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="236d7-129">También puede cambiar o agregar una configuración de aplicación ficticia para forzar una actualización del contenedor.</span><span class="sxs-lookup"><span data-stu-id="236d7-129">Or you can change or add a dummy application setting to force a refresh of your container.</span></span>

<span data-ttu-id="236d7-130">**P.**: ¿Los entornos de ensayo son compatibles?</span><span class="sxs-lookup"><span data-stu-id="236d7-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="236d7-131">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="236d7-131">**A:** Yes.</span></span>

<span data-ttu-id="236d7-132">**P:** ¿Puedo usar **Web Deploy** para implementar mi aplicación web?</span><span class="sxs-lookup"><span data-stu-id="236d7-132">**Q:** Can I use **web deploy** to deploy my web app?</span></span>

<span data-ttu-id="236d7-133">**R:** Sí, tiene que establecer una configuración de aplicación denominada `WEBSITE_WEBDEPLOY_USE_SCM` en `false`.</span><span class="sxs-lookup"><span data-stu-id="236d7-133">**A:** Yes, you need to set an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` to `false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="236d7-134">Compatibilidad con idiomas</span><span class="sxs-lookup"><span data-stu-id="236d7-134">Language support</span></span>

<span data-ttu-id="236d7-135">**P.:** ¿Se admiten aplicaciones de .NET Core sin compilar?</span><span class="sxs-lookup"><span data-stu-id="236d7-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="236d7-136">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="236d7-136">**A:** Yes.</span></span>

<span data-ttu-id="236d7-137">**P.:** ¿Admite un compositor como un administrador de dependencias para aplicaciones PHP?</span><span class="sxs-lookup"><span data-stu-id="236d7-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="236d7-138">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="236d7-138">**A:** Yes.</span></span> <span data-ttu-id="236d7-139">Durante una implementación de Git, Kudu debe detectar que va a implementar una aplicación PHP (gracias a la presencia de un archivo composer.json) y que se va a desencadenar una instalación de compositor automáticamente.</span><span class="sxs-lookup"><span data-stu-id="236d7-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks to the presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="236d7-140">Contenedores personalizados</span><span class="sxs-lookup"><span data-stu-id="236d7-140">Custom containers</span></span>

<span data-ttu-id="236d7-141">**P.:** Utilizo mi propio contenedor personalizado.</span><span class="sxs-lookup"><span data-stu-id="236d7-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="236d7-142">Mi aplicación reside en el directorio `\home\`, pero no puedo encontrar mis archivos al examinar el contenido mediante el [sitio SCM](https://github.com/projectkudu/kudu) o un cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="236d7-142">My app resides in the `\home\` directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="236d7-143">¿Dónde están mis archivos?</span><span class="sxs-lookup"><span data-stu-id="236d7-143">Where are my files?</span></span>

<span data-ttu-id="236d7-144">**R.**: Montamos un recurso compartido SMB en el directorio `\home\`.</span><span class="sxs-lookup"><span data-stu-id="236d7-144">**A:** We mount an SMB share to the `\home\` directory.</span></span> <span data-ttu-id="236d7-145">Esto invalida cualquier contenido de dicho directorio.</span><span class="sxs-lookup"><span data-stu-id="236d7-145">This will override any content that's there.</span></span>

<span data-ttu-id="236d7-146">**P.:** Utilizo mi propio contenedor personalizado.</span><span class="sxs-lookup"><span data-stu-id="236d7-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="236d7-147">No deseo que la plataforma monte un recurso compartido de SMB en `\home\`.</span><span class="sxs-lookup"><span data-stu-id="236d7-147">I don't want the platform to mount an SMB share to the `\home\`.</span></span>

<span data-ttu-id="236d7-148">**R:** Puede hacerlo estableciendo la configuración `WEBSITES_ENABLE_APP_SERVICE_STORAGE` de la aplicación en `false`.</span><span class="sxs-lookup"><span data-stu-id="236d7-148">**A:** You can do that by setting the `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting to `false`.</span></span>

<span data-ttu-id="236d7-149">**P:** Mi contenedor personalizado tarda mucho tiempo en iniciarse y la plataforma reinicia el contenedor antes de que finalice el inicio.</span><span class="sxs-lookup"><span data-stu-id="236d7-149">**Q:** My custom container takes a long time to start, and the platform restart the container before it finishes starting up.</span></span>

<span data-ttu-id="236d7-150">**R:** Puede configurar el tiempo que va a esperar la plataforma antes de reiniciar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="236d7-150">**A:** You can configure the time the platform will wait before restarting your container.</span></span> <span data-ttu-id="236d7-151">Puede hacerlo estableciendo la configuración `WEBSITES_CONTAINER_START_TIME_LIMIT` de la aplicación en el valor en segundos que desee.</span><span class="sxs-lookup"><span data-stu-id="236d7-151">This can be done by setting the `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting to the desired value in seconds.</span></span> <span data-ttu-id="236d7-152">El valor predeterminado es de 230 segundos y el valor máximo es de 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="236d7-152">The default is 230 seconds, and the max is 600 seconds.</span></span>

<span data-ttu-id="236d7-153">**P:** ¿Cuál es el formato de la dirección URL del servidor del Registro privado?</span><span class="sxs-lookup"><span data-stu-id="236d7-153">**Q:** What is the format for private registry server url?</span></span>

<span data-ttu-id="236d7-154">**R.**: Tiene que escribir la dirección URL completa del registro, incluidos `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="236d7-154">**A:** You need to provide the full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="236d7-155">**P:** ¿Cuál es el formato del nombre de la imagen en la opción del Registro privado?</span><span class="sxs-lookup"><span data-stu-id="236d7-155">**Q:** What is the format for the image name in private registry option?</span></span>

<span data-ttu-id="236d7-156">**R:** Debe agregar el nombre completo de la imagen, incluida la dirección URL del Registro privado (p. ej.</span><span class="sxs-lookup"><span data-stu-id="236d7-156">**A:** You need to add the full image name including the private registry url (eg.</span></span> <span data-ttu-id="236d7-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="236d7-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="236d7-158">**P:** Quiero exponer más de un puerto en mi imagen de contenedor personalizado.</span><span class="sxs-lookup"><span data-stu-id="236d7-158">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="236d7-159">¿Es posible?</span><span class="sxs-lookup"><span data-stu-id="236d7-159">Is that possible?</span></span>

<span data-ttu-id="236d7-160">**R.:** Actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="236d7-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="236d7-161">**P:** ¿Puedo traer mi propio almacenamiento?</span><span class="sxs-lookup"><span data-stu-id="236d7-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="236d7-162">**R.:** Actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="236d7-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="236d7-163">**P:** No puedo examinar el sistema de archivos de mi contenedor personalizado o ejecutar procesos desde el sitio SCM.</span><span class="sxs-lookup"><span data-stu-id="236d7-163">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="236d7-164">¿Por qué ocurre esto?</span><span class="sxs-lookup"><span data-stu-id="236d7-164">Why is that?</span></span>

<span data-ttu-id="236d7-165">**R.:** El sitio SCM se ejecuta en un contenedor independiente;</span><span class="sxs-lookup"><span data-stu-id="236d7-165">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="236d7-166">no puede comprobar el sistema de archivos o los procesos en ejecución del contenedor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="236d7-166">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="236d7-167">**P.:** Mi contenedor personalizado escucha a un puerto distinto al puerto 80.</span><span class="sxs-lookup"><span data-stu-id="236d7-167">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="236d7-168">¿Cómo puedo configurar mi aplicación para enrutar las solicitudes hacia ese puerto?</span><span class="sxs-lookup"><span data-stu-id="236d7-168">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="236d7-169">**R.**: Ofrecemos detección de puertos automática, pero también puede especificar un parámetro de la aplicación llamado **WEBSITES_PORT** y asignarle el valor del número de puerto esperado.</span><span class="sxs-lookup"><span data-stu-id="236d7-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it the value of the expected port number.</span></span> <span data-ttu-id="236d7-170">Anteriormente la plataforma utilizaba el parámetro de la aplicación `PORT`. Tenemos previsto dejar de usar este parámetro de la aplicación y usar `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="236d7-170">Previously the platform was using `PORT` app setting, we are planning to deprecate the use this app setting and move to using `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="236d7-171">**P:** ¿Es necesario implementar HTTPS en mi contenedor personalizado?</span><span class="sxs-lookup"><span data-stu-id="236d7-171">**Q:** Do I need to implement HTTPS in my custom container.</span></span>

<span data-ttu-id="236d7-172">**R:** No, la plataforma controla la terminación HTTPS en los front-end compartidos.</span><span class="sxs-lookup"><span data-stu-id="236d7-172">**A:** No, the platform handles HTTPS termination at the shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="236d7-173">Precios y contrato de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="236d7-173">Pricing and SLA</span></span>

<span data-ttu-id="236d7-174">**P.:** ¿Qué precios tiene usar la versión preliminar pública?</span><span class="sxs-lookup"><span data-stu-id="236d7-174">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="236d7-175">**R.**: Se le cobrará la mitad del número de horas que se ejecute la aplicación, con los precios normales de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="236d7-175">**A:** You are charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="236d7-176">Esto significa que hay un descuento del 50 por ciento en los precios normales de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="236d7-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="236d7-177">Otros</span><span class="sxs-lookup"><span data-stu-id="236d7-177">Other</span></span>

<span data-ttu-id="236d7-178">**P:** ¿Cuáles son los caracteres admitidos en los nombres de configuración de aplicación?</span><span class="sxs-lookup"><span data-stu-id="236d7-178">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="236d7-179">**R.:** Solo puede utilizar A-z, a-z, 0-9 y caracteres de subrayado para la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="236d7-179">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="236d7-180">**P:** ¿Dónde puedo solicitar nuevas características?</span><span class="sxs-lookup"><span data-stu-id="236d7-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="236d7-181">**R.:** Puede enviar su idea en el [foro de comentarios de Web Apps](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="236d7-181">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="236d7-182">Agregue [Linux] en el título de la idea.</span><span class="sxs-lookup"><span data-stu-id="236d7-182">Add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="236d7-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="236d7-183">Next steps</span></span>
* [<span data-ttu-id="236d7-184">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="236d7-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="236d7-185">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="236d7-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="236d7-186">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="236d7-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="236d7-187">Implementación continua con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="236d7-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
