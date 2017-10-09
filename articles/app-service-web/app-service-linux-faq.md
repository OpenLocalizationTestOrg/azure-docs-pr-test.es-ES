---
title: "aaaAzure aplicación servicio de aplicaciones Web de preguntas más frecuentes de Linux | Documentos de Microsoft"
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
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a><span data-ttu-id="b0d32-104">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b0d32-104">Azure App Service Web App on Linux FAQ</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="b0d32-105">Con la versión de Hola de aplicación Web en Linux, estamos trabajando para agregar características y realizar la plataforma de tooour de mejoras.</span><span class="sxs-lookup"><span data-stu-id="b0d32-105">With hello release of Web App on Linux, we're working on adding features and making improvements tooour platform.</span></span> <span data-ttu-id="b0d32-106">Aquí son algunas preguntas frecuentes (P+F) que nuestros clientes han estado solicitando a nosotros a través de Hola últimos meses.</span><span class="sxs-lookup"><span data-stu-id="b0d32-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over hello last months.</span></span>
<span data-ttu-id="b0d32-107">Si tiene alguna pregunta, el comentario de artículo de hello y, responderemos tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="b0d32-107">If you have a question, comment on hello article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="b0d32-108">Imágenes integradas</span><span class="sxs-lookup"><span data-stu-id="b0d32-108">Built-in images</span></span>

<span data-ttu-id="b0d32-109">**P: ¿** quiero toofork hello Docker contenedores integrados que Hola plataforma proporciona.</span><span class="sxs-lookup"><span data-stu-id="b0d32-109">**Q:** I want toofork hello built-in Docker containers that hello platform provides.</span></span> <span data-ttu-id="b0d32-110">¿Dónde puedo encontrar esos archivos?</span><span class="sxs-lookup"><span data-stu-id="b0d32-110">Where can I find those files?</span></span>

<span data-ttu-id="b0d32-111">**R.:** Encontrará todos los archivos de Docker en [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="b0d32-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="b0d32-112">Puede encontrar todos los contenedores de Docker en [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="b0d32-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="b0d32-113">**P: ¿** ¿cuáles son valores esperados de Hola para hello sección del archivo de inicio al configurar la pila de tiempo de ejecución de Hola?</span><span class="sxs-lookup"><span data-stu-id="b0d32-113">**Q:** What are hello expected values for hello Startup File section when I configure hello runtime stack?</span></span>

<span data-ttu-id="b0d32-114">**R:** para Node.Js, especifique el archivo de configuración de hello PM2 o el archivo de script.</span><span class="sxs-lookup"><span data-stu-id="b0d32-114">**A:** For Node.Js, you specify hello PM2 configuration file or your script file.</span></span> <span data-ttu-id="b0d32-115">Para .Net Core, debe especificar el nombre del archivo DLL compilado.</span><span class="sxs-lookup"><span data-stu-id="b0d32-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="b0d32-116">Para Ruby, puede especificar Hola Ruby script que quiere que tooinitialize su aplicación con.</span><span class="sxs-lookup"><span data-stu-id="b0d32-116">For Ruby, you can specify hello Ruby script that you want tooinitialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="b0d32-117">Administración</span><span class="sxs-lookup"><span data-stu-id="b0d32-117">Management</span></span>

<span data-ttu-id="b0d32-118">**P: ¿** ¿qué ocurre cuando presione el botón de reinicio de Hola Hola portal de Azure?</span><span class="sxs-lookup"><span data-stu-id="b0d32-118">**Q:** What happens when I press hello restart button in hello Azure portal?</span></span>

<span data-ttu-id="b0d32-119">**R:** esto es Hola equivalente del reinicio de Docker.</span><span class="sxs-lookup"><span data-stu-id="b0d32-119">**A:** This is hello equivalent of Docker restart.</span></span>

<span data-ttu-id="b0d32-120">**P: ¿** ¿se puede usar la máquina virtual (VM) del contenedor de aplicación de toohello Shell seguro (SSH), tooconnect?</span><span class="sxs-lookup"><span data-stu-id="b0d32-120">**Q:** Can I use Secure Shell (SSH) tooconnect toohello app container virtual machine (VM)?</span></span>

<span data-ttu-id="b0d32-121">**R:** Sí, puede hacer que a través del sitio SCM hello, artículo comprobación Hola siguiente para obtener más información [compatibilidad SSH para la aplicación Web en Linux](./app-service-linux-ssh-support.md)</span><span class="sxs-lookup"><span data-stu-id="b0d32-121">**A:** Yes, you can do that through hello SCM site, check hello following article for more information [SSH support for Web App on Linux](./app-service-linux-ssh-support.md)</span></span>

<span data-ttu-id="b0d32-122">**P: ¿** quiero toocreate un plano Linux App Service enviada mediante SDK o una plantilla de ARM, ¿cómo puedo lograr esto?</span><span class="sxs-lookup"><span data-stu-id="b0d32-122">**Q:** I want toocreate a Linux App Service plane through SDK or an ARM template, how can I achieve this?</span></span>

<span data-ttu-id="b0d32-123">**R:** necesita hello tooset `reserved` campo de la aplicación hello servicio demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="b0d32-123">**A:** You need tooset hello `reserved` field of hello app service too`true`.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="b0d32-124">Integración e implementación continuas</span><span class="sxs-lookup"><span data-stu-id="b0d32-124">Continuous integration/deployment</span></span>

<span data-ttu-id="b0d32-125">**P: ¿** mi aplicación web sigue usando una imagen de contenedor de Docker antigua después de actualizar la imagen de hello en Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="b0d32-125">**Q:** My web app still uses an old Docker container image after I've updated hello image on Docker Hub.</span></span> <span data-ttu-id="b0d32-126">¿Se admite la integración e implementación continuas de contenedores personalizados?</span><span class="sxs-lookup"><span data-stu-id="b0d32-126">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="b0d32-127">**R:** tooset la implementación/integración continua para las imágenes del registro de contenedor de Azure o DockerHub por Hola de verificación artículo siguiente [implementación continua con la aplicación Web de Azure en Linux](./app-service-linux-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="b0d32-127">**A:** tooset up continuous integration/deployment for Azure Container Registry or DockerHub images by check hello following article [Continuous Deployment with Azure Web App on Linux](./app-service-linux-ci-cd.md).</span></span> <span data-ttu-id="b0d32-128">Para registros privados, puede actualizar el contenedor de hello deteniendo y, a continuación, iniciar la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b0d32-128">For private registries, you can refresh hello container by stopping and then starting your web app.</span></span> <span data-ttu-id="b0d32-129">O bien, puede cambiar o agregar una aplicación ficticia establecer tooforce una actualización del contenedor.</span><span class="sxs-lookup"><span data-stu-id="b0d32-129">Or you can change or add a dummy application setting tooforce a refresh of your container.</span></span>

<span data-ttu-id="b0d32-130">**P.**: ¿Los entornos de ensayo son compatibles?</span><span class="sxs-lookup"><span data-stu-id="b0d32-130">**Q:** Do you support staging environments?</span></span>

<span data-ttu-id="b0d32-131">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="b0d32-131">**A:** Yes.</span></span>

<span data-ttu-id="b0d32-132">**P: ¿** puedo usar **WebDeploy** toodeploy mi aplicación web?</span><span class="sxs-lookup"><span data-stu-id="b0d32-132">**Q:** Can I use **web deploy** toodeploy my web app?</span></span>

<span data-ttu-id="b0d32-133">**R:** Sí, necesita una aplicación llamada tooset `WEBSITE_WEBDEPLOY_USE_SCM` demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="b0d32-133">**A:** Yes, you need tooset an app setting called `WEBSITE_WEBDEPLOY_USE_SCM` too`false`.</span></span>

## <a name="language-support"></a><span data-ttu-id="b0d32-134">Compatibilidad con idiomas</span><span class="sxs-lookup"><span data-stu-id="b0d32-134">Language support</span></span>

<span data-ttu-id="b0d32-135">**P.:** ¿Se admiten aplicaciones de .NET Core sin compilar?</span><span class="sxs-lookup"><span data-stu-id="b0d32-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="b0d32-136">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="b0d32-136">**A:** Yes.</span></span>

<span data-ttu-id="b0d32-137">**P.:** ¿Admite un compositor como un administrador de dependencias para aplicaciones PHP?</span><span class="sxs-lookup"><span data-stu-id="b0d32-137">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="b0d32-138">**R:** Sí.</span><span class="sxs-lookup"><span data-stu-id="b0d32-138">**A:** Yes.</span></span> <span data-ttu-id="b0d32-139">Durante una implementación de Git, Kudu debería detectar que va a implementar una aplicación PHP (gracias toohello presencia de un archivo composer.json) y desencadenará una instalación de compositor automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b0d32-139">During a Git deployment, Kudu should detect that you are deploying a PHP application (thanks toohello presence of a composer.json file) and will trigger a composer install for you.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="b0d32-140">Contenedores personalizados</span><span class="sxs-lookup"><span data-stu-id="b0d32-140">Custom containers</span></span>

<span data-ttu-id="b0d32-141">**P.:** Utilizo mi propio contenedor personalizado.</span><span class="sxs-lookup"><span data-stu-id="b0d32-141">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="b0d32-142">Mi aplicación reside en hello `\home\` directorio, pero no podemos encontrar Mis archivos al examinar el contenido de hello mediante el uso de hello [sitio SCM](https://github.com/projectkudu/kudu) o un cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="b0d32-142">My app resides in hello `\home\` directory, but I can't find my files when I browse hello content by using hello [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="b0d32-143">¿Dónde están mis archivos?</span><span class="sxs-lookup"><span data-stu-id="b0d32-143">Where are my files?</span></span>

<span data-ttu-id="b0d32-144">**R:** montamos un toohello del recurso compartido SMB `\home\` directory.</span><span class="sxs-lookup"><span data-stu-id="b0d32-144">**A:** We mount an SMB share toohello `\home\` directory.</span></span> <span data-ttu-id="b0d32-145">Esto invalida cualquier contenido de dicho directorio.</span><span class="sxs-lookup"><span data-stu-id="b0d32-145">This will override any content that's there.</span></span>

<span data-ttu-id="b0d32-146">**P.:** Utilizo mi propio contenedor personalizado.</span><span class="sxs-lookup"><span data-stu-id="b0d32-146">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="b0d32-147">No deseo Hola plataforma toomount un toohello de recurso compartido SMB `\home\`.</span><span class="sxs-lookup"><span data-stu-id="b0d32-147">I don't want hello platform toomount an SMB share toohello `\home\`.</span></span>

<span data-ttu-id="b0d32-148">**R:** para hacer que debe establecer hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicación establecer demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="b0d32-148">**A:** You can do that by setting hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` app setting too`false`.</span></span>

<span data-ttu-id="b0d32-149">**P: ¿** mi contenedor personalizado toma un toostart mucho tiempo y finalice de contenedor de Hola de reinicio de hello plataforma antes de que iniciarse.</span><span class="sxs-lookup"><span data-stu-id="b0d32-149">**Q:** My custom container takes a long time toostart, and hello platform restart hello container before it finishes starting up.</span></span>

<span data-ttu-id="b0d32-150">**R:** puede configurar tiempo de hello plataforma Hola esperará antes de reiniciar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="b0d32-150">**A:** You can configure hello time hello platform will wait before restarting your container.</span></span> <span data-ttu-id="b0d32-151">Esto puede hacerse por establecer hello `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de configuración de aplicación el valor deseado en segundos.</span><span class="sxs-lookup"><span data-stu-id="b0d32-151">This can be done by setting hello `WEBSITES_CONTAINER_START_TIME_LIMIT` app setting toohello desired value in seconds.</span></span> <span data-ttu-id="b0d32-152">valor predeterminado de Hello es 230 segundos y Hola max es 600 segundos.</span><span class="sxs-lookup"><span data-stu-id="b0d32-152">hello default is 230 seconds, and hello max is 600 seconds.</span></span>

<span data-ttu-id="b0d32-153">**P: ¿** ¿qué es el formato de hello para la dirección url del servidor de registro privada?</span><span class="sxs-lookup"><span data-stu-id="b0d32-153">**Q:** What is hello format for private registry server url?</span></span>

<span data-ttu-id="b0d32-154">**R:** que debe tooprovide Hola completo registro dirección url como `http://` o `https://`.</span><span class="sxs-lookup"><span data-stu-id="b0d32-154">**A:** You need tooprovide hello full registry url including `http://` or `https://`.</span></span>

<span data-ttu-id="b0d32-155">**P: ¿** ¿qué es el formato de hello para el nombre de la imagen de hello en la opción de registro privada?</span><span class="sxs-lookup"><span data-stu-id="b0d32-155">**Q:** What is hello format for hello image name in private registry option?</span></span>

<span data-ttu-id="b0d32-156">**R:** necesita nombre de la imagen completa de hello tooadd incluida (p. ej dirección url de registro privada de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0d32-156">**A:** You need tooadd hello full image name including hello private registry url (eg.</span></span> <span data-ttu-id="b0d32-157">myacr.azurecr.io/dotnet:latest)</span><span class="sxs-lookup"><span data-stu-id="b0d32-157">myacr.azurecr.io/dotnet:latest)</span></span>

<span data-ttu-id="b0d32-158">**P: ¿** deseo tooexpose más de un puerto en mi imagen de contenedor personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b0d32-158">**Q:** I want tooexpose more than one port on my custom container image.</span></span> <span data-ttu-id="b0d32-159">¿Es posible?</span><span class="sxs-lookup"><span data-stu-id="b0d32-159">Is that possible?</span></span>

<span data-ttu-id="b0d32-160">**R.:** Actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="b0d32-160">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="b0d32-161">**P:** ¿Puedo traer mi propio almacenamiento?</span><span class="sxs-lookup"><span data-stu-id="b0d32-161">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="b0d32-162">**R.:** Actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="b0d32-162">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="b0d32-163">**P: ¿** no se puede examinar los procesos de sistema o de ejecución de archivos de mi contenedor personalizado desde el sitio SCM Hola.</span><span class="sxs-lookup"><span data-stu-id="b0d32-163">**Q:** I can't browse my custom container's file system or running processes from hello SCM site.</span></span> <span data-ttu-id="b0d32-164">¿Por qué ocurre esto?</span><span class="sxs-lookup"><span data-stu-id="b0d32-164">Why is that?</span></span>

<span data-ttu-id="b0d32-165">**R:** sitio SCM Hola se ejecuta en un contenedor independiente.</span><span class="sxs-lookup"><span data-stu-id="b0d32-165">**A:** hello SCM site runs in a separate container.</span></span> <span data-ttu-id="b0d32-166">No se pueden comprobar sistema de archivos de Hola o procesos de contenedor de la aplicación hello en ejecución.</span><span class="sxs-lookup"><span data-stu-id="b0d32-166">You can't check hello file system or running processes of hello app container.</span></span>

<span data-ttu-id="b0d32-167">**P: ¿** mi contenedor personalizado escucha tooa puerto distinto al puerto 80.</span><span class="sxs-lookup"><span data-stu-id="b0d32-167">**Q:** My custom container listens tooa port other than port 80.</span></span> <span data-ttu-id="b0d32-168">¿Cómo puedo configurar mi puerto aplicación tooroute Hola solicitudes toothat?</span><span class="sxs-lookup"><span data-stu-id="b0d32-168">How can I configure my app tooroute hello requests toothat port?</span></span>

<span data-ttu-id="b0d32-169">**R:** contamos con detección automática del puerto, también puede especificar una aplicación llamada **WEBSITES_PORT**y asígnele el valor de Hola Hola esperada número de puerto.</span><span class="sxs-lookup"><span data-stu-id="b0d32-169">**A:** We have auto port detection, also you can specify an application setting called **WEBSITES_PORT**, and give it hello value of hello expected port number.</span></span> <span data-ttu-id="b0d32-170">Anteriormente utilizaba plataforma hello `PORT` aplicación establecer, se está planeando toodeprecate Hola use esta configuración de aplicación y mover toousing `WEBSITES_PORT` exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="b0d32-170">Previously hello platform was using `PORT` app setting, we are planning toodeprecate hello use this app setting and move toousing `WEBSITES_PORT` exclusively.</span></span>

<span data-ttu-id="b0d32-171">**P: ¿** es necesario tooimplement HTTPS en mi contenedor personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b0d32-171">**Q:** Do I need tooimplement HTTPS in my custom container.</span></span>

<span data-ttu-id="b0d32-172">**R:** No, plataforma Hola controla la terminación HTTPS en hello compartido front-ends.</span><span class="sxs-lookup"><span data-stu-id="b0d32-172">**A:** No, hello platform handles HTTPS termination at hello shared frontends.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="b0d32-173">Precios y contrato de nivel de servicio</span><span class="sxs-lookup"><span data-stu-id="b0d32-173">Pricing and SLA</span></span>

<span data-ttu-id="b0d32-174">**P: ¿** ¿qué es Hola precios mientras utiliza la versión preliminar pública de hello?</span><span class="sxs-lookup"><span data-stu-id="b0d32-174">**Q:** What's hello pricing while you're using hello public preview?</span></span>

<span data-ttu-id="b0d32-175">**R:** se le cobrará la mitad el número de Hola de horas que se ejecuta la aplicación, con hello precios normal del servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="b0d32-175">**A:** You are charged half hello number of hours that your app runs, with hello normal Azure App Service pricing.</span></span> <span data-ttu-id="b0d32-176">Esto significa que hay un descuento del 50 por ciento en los precios normales de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b0d32-176">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="b0d32-177">Otros</span><span class="sxs-lookup"><span data-stu-id="b0d32-177">Other</span></span>

<span data-ttu-id="b0d32-178">**P: ¿** ¿qué son Hola admitida caracteres en nombres de configuración de aplicación?</span><span class="sxs-lookup"><span data-stu-id="b0d32-178">**Q:** What are hello supported characters in application settings names?</span></span>

<span data-ttu-id="b0d32-179">**R:** solo puede usar A-z, a-z, 0-9 y Hola guión bajo Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0d32-179">**A:** You can only use A-Z, a-z, 0-9, and hello underscore for application settings.</span></span>

<span data-ttu-id="b0d32-180">**P:**  ¿Dónde puedo solicitar nuevas características?</span><span class="sxs-lookup"><span data-stu-id="b0d32-180">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="b0d32-181">**R:** puede enviar su idea en hello [foro de comentarios de las aplicaciones Web](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="b0d32-181">**A:** You can submit your idea at hello [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="b0d32-182">Agregar un título de toohello "[Linux]" de su idea.</span><span class="sxs-lookup"><span data-stu-id="b0d32-182">Add "[Linux]" toohello title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0d32-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0d32-183">Next steps</span></span>
* [<span data-ttu-id="b0d32-184">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="b0d32-184">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b0d32-185">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="b0d32-185">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="b0d32-186">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b0d32-186">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="b0d32-187">Implementación continua con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="b0d32-187">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
