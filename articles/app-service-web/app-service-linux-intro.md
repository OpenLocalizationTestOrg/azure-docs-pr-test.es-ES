---
title: "Introducción a Azure Web App on Linux | Microsoft Docs"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="d3363-104">Introducción a Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="d3363-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="d3363-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d3363-105">Overview</span></span>
<span data-ttu-id="d3363-106">Los clientes pueden usar Web App on Linux para hospedar aplicaciones web de forma nativa en Linux para pilas de aplicaciones admitidas.</span><span class="sxs-lookup"><span data-stu-id="d3363-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="d3363-107">En la sección siguiente se muestran las pilas de aplicaciones que son compatibles actualmente.</span><span class="sxs-lookup"><span data-stu-id="d3363-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="d3363-108">Características</span><span class="sxs-lookup"><span data-stu-id="d3363-108">Features</span></span>
<span data-ttu-id="d3363-109">Web App on Linux admite actualmente las siguientes pilas de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="d3363-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="d3363-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="d3363-110">Node.js</span></span>
    * <span data-ttu-id="d3363-111">4.4.</span><span class="sxs-lookup"><span data-stu-id="d3363-111">4.4</span></span>
    * <span data-ttu-id="d3363-112">4.5.</span><span class="sxs-lookup"><span data-stu-id="d3363-112">4.5</span></span>
    * <span data-ttu-id="d3363-113">6.2</span><span class="sxs-lookup"><span data-stu-id="d3363-113">6.2</span></span>
    * <span data-ttu-id="d3363-114">6.6</span><span class="sxs-lookup"><span data-stu-id="d3363-114">6.6</span></span>
    * <span data-ttu-id="d3363-115">6.9</span><span class="sxs-lookup"><span data-stu-id="d3363-115">6.9</span></span>
    * <span data-ttu-id="d3363-116">6.10</span><span class="sxs-lookup"><span data-stu-id="d3363-116">6.10</span></span>
    * <span data-ttu-id="d3363-117">6.11</span><span class="sxs-lookup"><span data-stu-id="d3363-117">6.11</span></span>
    * <span data-ttu-id="d3363-118">8.0</span><span class="sxs-lookup"><span data-stu-id="d3363-118">8.0</span></span>
    * <span data-ttu-id="d3363-119">8.1</span><span class="sxs-lookup"><span data-stu-id="d3363-119">8.1</span></span>
* <span data-ttu-id="d3363-120">PHP</span><span class="sxs-lookup"><span data-stu-id="d3363-120">PHP</span></span>
    * <span data-ttu-id="d3363-121">5.6</span><span class="sxs-lookup"><span data-stu-id="d3363-121">5.6</span></span>
    * <span data-ttu-id="d3363-122">7.0</span><span class="sxs-lookup"><span data-stu-id="d3363-122">7.0</span></span>
* <span data-ttu-id="d3363-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="d3363-123">.Net Core</span></span>
    * <span data-ttu-id="d3363-124">1.0</span><span class="sxs-lookup"><span data-stu-id="d3363-124">1.0</span></span>
    * <span data-ttu-id="d3363-125">1.1</span><span class="sxs-lookup"><span data-stu-id="d3363-125">1.1</span></span>
* <span data-ttu-id="d3363-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="d3363-126">Ruby</span></span>
    * <span data-ttu-id="d3363-127">2.3</span><span class="sxs-lookup"><span data-stu-id="d3363-127">2.3</span></span>

<span data-ttu-id="d3363-128">Los clientes pueden implementar sus aplicaciones mediante:</span><span class="sxs-lookup"><span data-stu-id="d3363-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="d3363-129">FTP</span><span class="sxs-lookup"><span data-stu-id="d3363-129">FTP</span></span>
* <span data-ttu-id="d3363-130">Git local</span><span class="sxs-lookup"><span data-stu-id="d3363-130">Local Git</span></span>
* <span data-ttu-id="d3363-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="d3363-131">GitHub</span></span>
* <span data-ttu-id="d3363-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="d3363-132">Bitbucket</span></span>

<span data-ttu-id="d3363-133">Para el escalado de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="d3363-133">For application scaling:</span></span>

* <span data-ttu-id="d3363-134">Los clientes pueden escalar o reducir aplicaciones web verticalmente mediante la modificación del nivel en su plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="d3363-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="d3363-135">Los clientes pueden escalar horizontalmente aplicaciones y ejecutar varias instancias de la aplicación dentro de los confines de su SKU.</span><span class="sxs-lookup"><span data-stu-id="d3363-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="d3363-136">Para Kudu, parte de la funcionalidad básica funciona con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d3363-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="d3363-137">Entornos</span><span class="sxs-lookup"><span data-stu-id="d3363-137">Environments</span></span>
* <span data-ttu-id="d3363-138">Implementaciones</span><span class="sxs-lookup"><span data-stu-id="d3363-138">Deployments</span></span>
* <span data-ttu-id="d3363-139">Consola básica</span><span class="sxs-lookup"><span data-stu-id="d3363-139">Basic console</span></span>
* <span data-ttu-id="d3363-140">SSH</span><span class="sxs-lookup"><span data-stu-id="d3363-140">SSH</span></span>

<span data-ttu-id="d3363-141">Para DevOps:</span><span class="sxs-lookup"><span data-stu-id="d3363-141">For devops:</span></span>

* <span data-ttu-id="d3363-142">Entornos de ensayo</span><span class="sxs-lookup"><span data-stu-id="d3363-142">Staging environments</span></span>
* <span data-ttu-id="d3363-143">ACR y DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="d3363-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="d3363-144">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="d3363-144">Limitations</span></span>
<span data-ttu-id="d3363-145">Azure Portal solo muestra las características que funcionan actualmente para Web App on Linux y oculta el resto.</span><span class="sxs-lookup"><span data-stu-id="d3363-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="d3363-146">A medida que se habiliten más características, estas aparecerán en el portal.</span><span class="sxs-lookup"><span data-stu-id="d3363-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="d3363-147">Algunas de ellas, como la integración de la red virtual, la autenticación de Azure Active Directory o de terceros o las extensiones de sitio de Kudu, no están aún disponibles.</span><span class="sxs-lookup"><span data-stu-id="d3363-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="d3363-148">Pero cuando lo estén, actualizaremos nuestra documentación y el blog sobre los cambios.</span><span class="sxs-lookup"><span data-stu-id="d3363-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="d3363-149">Esta versión preliminar pública solo está disponible en las siguientes regiones:</span><span class="sxs-lookup"><span data-stu-id="d3363-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="d3363-150">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="d3363-150">West US</span></span>
* <span data-ttu-id="d3363-151">Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="d3363-151">East US</span></span>
* <span data-ttu-id="d3363-152">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="d3363-152">West Europe</span></span>
* <span data-ttu-id="d3363-153">Europa del Norte</span><span class="sxs-lookup"><span data-stu-id="d3363-153">North Europe</span></span>
* <span data-ttu-id="d3363-154">Centro-Sur de EE. UU</span><span class="sxs-lookup"><span data-stu-id="d3363-154">South Central US</span></span>
* <span data-ttu-id="d3363-155">Centro-Norte de EE. UU</span><span class="sxs-lookup"><span data-stu-id="d3363-155">North Central US</span></span>
* <span data-ttu-id="d3363-156">Sudeste asiático</span><span class="sxs-lookup"><span data-stu-id="d3363-156">Southeast Asia</span></span>
* <span data-ttu-id="d3363-157">Asia oriental</span><span class="sxs-lookup"><span data-stu-id="d3363-157">East Asia</span></span>
* <span data-ttu-id="d3363-158">Australia Oriental</span><span class="sxs-lookup"><span data-stu-id="d3363-158">Australia East</span></span>
* <span data-ttu-id="d3363-159">Este de Japón</span><span class="sxs-lookup"><span data-stu-id="d3363-159">Japan East</span></span>
* <span data-ttu-id="d3363-160">Sur de Brasil</span><span class="sxs-lookup"><span data-stu-id="d3363-160">Brazil South</span></span>
* <span data-ttu-id="d3363-161">Sur de la India</span><span class="sxs-lookup"><span data-stu-id="d3363-161">South India</span></span>

<span data-ttu-id="d3363-162">Las aplicaciones web en Linux solo se admiten en planes de App Service dedicados y no tienen un nivel gratuito o compartido.</span><span class="sxs-lookup"><span data-stu-id="d3363-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="d3363-163">Además, los planes de App Service para aplicaciones web normales y de Linux son mutuamente excluyentes, de modo que no puede crear una aplicación web de Linux en un plan de App Service que no sea de Linux.</span><span class="sxs-lookup"><span data-stu-id="d3363-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="d3363-164">Las aplicaciones web de Linux se deben crear en un grupo de recursos que no contenga aplicaciones web que no sean de Linux en la misma región.</span><span class="sxs-lookup"><span data-stu-id="d3363-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d3363-165">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="d3363-165">Troubleshooting</span></span> ##

<span data-ttu-id="d3363-166">Si la aplicación no se inicia o desea comprobar el registro desde la aplicación, compruebe que el Docker realiza el registro en LogFiles.</span><span class="sxs-lookup"><span data-stu-id="d3363-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="d3363-167">A este directorio se accede a través del sitio SCM o a través de FTP.</span><span class="sxs-lookup"><span data-stu-id="d3363-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="d3363-168">Para registrar `stdout` y `stderr` del contenedor, debe habilitar **Registros de contenedor de Docker** en **Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="d3363-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Habilitación del registro][2]

![Uso de Kudu para ver registros de Docker][1]

<span data-ttu-id="d3363-171">Puede acceder al sitio SCM desde **Advanced Tools** (Herramientas avanzadas) en el menú **Herramientas de desarrollo**.</span><span class="sxs-lookup"><span data-stu-id="d3363-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3363-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d3363-172">Next steps</span></span>
<span data-ttu-id="d3363-173">Consulte los vínculos siguientes para empezar a trabajar con App Service en Linux.</span><span class="sxs-lookup"><span data-stu-id="d3363-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="d3363-174">Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="d3363-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="d3363-175">Uso de una imagen personalizada de Docker para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d3363-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="d3363-176">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d3363-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="d3363-177">Uso de .NET Core en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d3363-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="d3363-178">Uso de Ruby en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d3363-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="d3363-179">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d3363-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="d3363-180">Compatibilidad con SSH para Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="d3363-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="d3363-181">Configuración de entornos de ensayo en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d3363-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="d3363-182">Implementación continua de Docker Hub con Azure Web App en Linux</span><span class="sxs-lookup"><span data-stu-id="d3363-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png