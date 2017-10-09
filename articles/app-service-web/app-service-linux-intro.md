---
title: aaaIntroduction tooAzure Web App en Linux | Documentos de Microsoft
description: "Obtenga información sobre Azure Web App en Linux."
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="fc37d-104">Introducción tooAzure la aplicación Web en Linux</span><span class="sxs-lookup"><span data-stu-id="fc37d-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="fc37d-105">Información general</span><span class="sxs-lookup"><span data-stu-id="fc37d-105">Overview</span></span>
<span data-ttu-id="fc37d-106">Los clientes pueden usar la aplicación Web en aplicaciones de Linux toohost web de forma nativa en Linux pilas de aplicación compatibles de.</span><span class="sxs-lookup"><span data-stu-id="fc37d-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="fc37d-107">Hello siguiente sección enumeran pilas de aplicación Hola que son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="fc37d-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="fc37d-108">Características</span><span class="sxs-lookup"><span data-stu-id="fc37d-108">Features</span></span>
<span data-ttu-id="fc37d-109">Web App en Linux admite actualmente Hola después de pilas de aplicación:</span><span class="sxs-lookup"><span data-stu-id="fc37d-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="fc37d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="fc37d-110">Node.js</span></span>
    * <span data-ttu-id="fc37d-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="fc37d-111">4.4</span></span>
    * <span data-ttu-id="fc37d-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="fc37d-112">4.5</span></span>
    * <span data-ttu-id="fc37d-113">6.2</span><span class="sxs-lookup"><span data-stu-id="fc37d-113">6.2</span></span>
    * <span data-ttu-id="fc37d-114">6.6</span><span class="sxs-lookup"><span data-stu-id="fc37d-114">6.6</span></span>
    * <span data-ttu-id="fc37d-115">6.9</span><span class="sxs-lookup"><span data-stu-id="fc37d-115">6.9</span></span>
    * <span data-ttu-id="fc37d-116">6.10</span><span class="sxs-lookup"><span data-stu-id="fc37d-116">6.10</span></span>
    * <span data-ttu-id="fc37d-117">6.11</span><span class="sxs-lookup"><span data-stu-id="fc37d-117">6.11</span></span>
    * <span data-ttu-id="fc37d-118">8.0</span><span class="sxs-lookup"><span data-stu-id="fc37d-118">8.0</span></span>
    * <span data-ttu-id="fc37d-119">8.1</span><span class="sxs-lookup"><span data-stu-id="fc37d-119">8.1</span></span>
* <span data-ttu-id="fc37d-120">PHP</span><span class="sxs-lookup"><span data-stu-id="fc37d-120">PHP</span></span>
    * <span data-ttu-id="fc37d-121">5.6</span><span class="sxs-lookup"><span data-stu-id="fc37d-121">5.6</span></span>
    * <span data-ttu-id="fc37d-122">7.0</span><span class="sxs-lookup"><span data-stu-id="fc37d-122">7.0</span></span>
* <span data-ttu-id="fc37d-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="fc37d-123">.Net Core</span></span>
    * <span data-ttu-id="fc37d-124">1.0</span><span class="sxs-lookup"><span data-stu-id="fc37d-124">1.0</span></span>
    * <span data-ttu-id="fc37d-125">1.1</span><span class="sxs-lookup"><span data-stu-id="fc37d-125">1.1</span></span>
* <span data-ttu-id="fc37d-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="fc37d-126">Ruby</span></span>
    * <span data-ttu-id="fc37d-127">2.3</span><span class="sxs-lookup"><span data-stu-id="fc37d-127">2.3</span></span>

<span data-ttu-id="fc37d-128">Los clientes pueden implementar sus aplicaciones mediante:</span><span class="sxs-lookup"><span data-stu-id="fc37d-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="fc37d-129">FTP</span><span class="sxs-lookup"><span data-stu-id="fc37d-129">FTP</span></span>
* <span data-ttu-id="fc37d-130">Git local</span><span class="sxs-lookup"><span data-stu-id="fc37d-130">Local Git</span></span>
* <span data-ttu-id="fc37d-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="fc37d-131">GitHub</span></span>
* <span data-ttu-id="fc37d-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="fc37d-132">Bitbucket</span></span>

<span data-ttu-id="fc37d-133">Para el escalado de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="fc37d-133">For application scaling:</span></span>

* <span data-ttu-id="fc37d-134">Los clientes pueden escalar aplicaciones web de arriba y abajo cambiando el nivel de Hola de su plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fc37d-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="fc37d-135">Los clientes pueden escalar horizontalmente aplicaciones y ejecutar varias instancias de aplicación dentro de los confines de Hola de su SKU</span><span class="sxs-lookup"><span data-stu-id="fc37d-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="fc37d-136">Para Kudu, algunas de las funciones básicas de hello:</span><span class="sxs-lookup"><span data-stu-id="fc37d-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="fc37d-137">Entornos</span><span class="sxs-lookup"><span data-stu-id="fc37d-137">Environments</span></span>
* <span data-ttu-id="fc37d-138">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="fc37d-138">Deployments</span></span>
* <span data-ttu-id="fc37d-139">Consola básica</span><span class="sxs-lookup"><span data-stu-id="fc37d-139">Basic console</span></span>
* <span data-ttu-id="fc37d-140">SSH</span><span class="sxs-lookup"><span data-stu-id="fc37d-140">SSH</span></span>

<span data-ttu-id="fc37d-141">Para DevOps:</span><span class="sxs-lookup"><span data-stu-id="fc37d-141">For devops:</span></span>

* <span data-ttu-id="fc37d-142">Entornos de ensayo</span><span class="sxs-lookup"><span data-stu-id="fc37d-142">Staging environments</span></span>
* <span data-ttu-id="fc37d-143">ACR y DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="fc37d-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="fc37d-144">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="fc37d-144">Limitations</span></span>
<span data-ttu-id="fc37d-145">Hello portal de Azure únicas características que funcionan actualmente para la aplicación Web en Linux muestra y oculta resto Hola.</span><span class="sxs-lookup"><span data-stu-id="fc37d-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="fc37d-146">Tal y como se habilita más características, serán visibles en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc37d-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="fc37d-147">Algunas de ellas, como la integración de la red virtual, la autenticación de Azure Active Directory o de terceros o las extensiones de sitio de Kudu, no están aún disponibles.</span><span class="sxs-lookup"><span data-stu-id="fc37d-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="fc37d-148">Una vez que estas características están disponibles, se actualizará en nuestro blog sobre los cambios de Hola y documentación.</span><span class="sxs-lookup"><span data-stu-id="fc37d-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="fc37d-149">Esta vista previa pública actualmente solo está disponible en hello siguientes regiones:</span><span class="sxs-lookup"><span data-stu-id="fc37d-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="fc37d-150">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="fc37d-150">West US</span></span>
* <span data-ttu-id="fc37d-151">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="fc37d-151">East US</span></span>
* <span data-ttu-id="fc37d-152">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="fc37d-152">West Europe</span></span>
* <span data-ttu-id="fc37d-153">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="fc37d-153">North Europe</span></span>
* <span data-ttu-id="fc37d-154">Centro-Sur de EE. UU</span><span class="sxs-lookup"><span data-stu-id="fc37d-154">South Central US</span></span>
* <span data-ttu-id="fc37d-155">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="fc37d-155">North Central US</span></span>
* <span data-ttu-id="fc37d-156">Sudeste asiático</span><span class="sxs-lookup"><span data-stu-id="fc37d-156">Southeast Asia</span></span>
* <span data-ttu-id="fc37d-157">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="fc37d-157">East Asia</span></span>
* <span data-ttu-id="fc37d-158">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="fc37d-158">Australia East</span></span>
* <span data-ttu-id="fc37d-159">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="fc37d-159">Japan East</span></span>
* <span data-ttu-id="fc37d-160">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="fc37d-160">Brazil South</span></span>
* <span data-ttu-id="fc37d-161">Sur de la India</span><span class="sxs-lookup"><span data-stu-id="fc37d-161">South India</span></span>

<span data-ttu-id="fc37d-162">Aplicaciones en Linux Web solo se admiten en planes de servicio de aplicaciones dedicado de hello y no tiene un nivel gratuito o compartido.</span><span class="sxs-lookup"><span data-stu-id="fc37d-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="fc37d-163">Además, los planes de App Service para aplicaciones web normales y de Linux son mutuamente excluyentes, de modo que no puede crear una aplicación web de Linux en un plan de App Service que no sea de Linux.</span><span class="sxs-lookup"><span data-stu-id="fc37d-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="fc37d-164">Aplicaciones en Linux Web deben crearse en un grupo de recursos que no contenga las aplicaciones web no Linux Hola misma región.</span><span class="sxs-lookup"><span data-stu-id="fc37d-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fc37d-165">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="fc37d-165">Troubleshooting</span></span> ##

<span data-ttu-id="fc37d-166">Cuando se produce un error en la aplicación toostart o si desea el registro de hello toocheck desde la aplicación, compruebe hello que docker registra en el directorio LogFiles de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc37d-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="fc37d-167">A este directorio se accede a través del sitio SCM o a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="fc37d-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="fc37d-168">Hola toolog `stdout` y `stderr` desde el contenedor, deberá tooenable **registro de contenedor de Docker** en **registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="fc37d-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitación del registro][2]

![Uso de los registros de Kudu tooview Docker][1]

<span data-ttu-id="fc37d-171">Puede tener acceso a sitios SCM Hola de **herramientas avanzadas** en hello **herramientas de desarrollo** menú.</span><span class="sxs-lookup"><span data-stu-id="fc37d-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc37d-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fc37d-172">Next steps</span></span>
<span data-ttu-id="fc37d-173">Vea Hola después tooget de vínculos que se inició con el servicio de aplicación en Linux.</span><span class="sxs-lookup"><span data-stu-id="fc37d-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="fc37d-174">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="fc37d-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="fc37d-175">Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="fc37d-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="fc37d-176">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="fc37d-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="fc37d-177">Uso de .NET Core en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fc37d-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="fc37d-178">Uso de Ruby en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fc37d-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="fc37d-179">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fc37d-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="fc37d-180">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="fc37d-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="fc37d-181">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fc37d-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="fc37d-182">Implementación continua de Docker Hub con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="fc37d-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png