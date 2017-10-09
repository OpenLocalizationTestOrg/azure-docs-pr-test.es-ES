---
title: "aaaDeploy su primer tooCloud de aplicación Foundry en Microsoft Azure | Documentos de Microsoft"
description: "Implementar un tooCloud aplicación Foundry en Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="df0df-103">Implementar su primer tooCloud de aplicación Foundry en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="df0df-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="df0df-104">[Cloud Foundry](http://cloudfoundry.org) es una popular plataforma de aplicaciones de código abierto disponible en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="df0df-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="df0df-105">En este artículo, le mostramos cómo toodeploy y administrar una aplicación en nube Foundry en un entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="df0df-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="df0df-106">Creación de un entorno de Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="df0df-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="df0df-107">Hay varias opciones para crear un entorno de Cloud Foundry en Azure:</span><span class="sxs-lookup"><span data-stu-id="df0df-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="df0df-108">Hola de uso [oferta esencial Foundry nube] [ pcf-azuremarketplace] en hello Azure Marketplace toocreate un entorno estándar que incluye hello Azure Service Broker y PCF Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="df0df-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="df0df-109">Puede encontrar [completar instrucciones] [ pcf-azuremarketplace-pivotaldocs] para la implementación de marketplace de hello ofrecen Hola documentación esencial.</span><span class="sxs-lookup"><span data-stu-id="df0df-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="df0df-110">Crear un entorno personalizado mediante la [implementación manual de Pivotal Cloud Foundry][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="df0df-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="df0df-111">[Implementar paquetes de nube Foundry de código abierto de hello directamente] [ oss-cf-bosh] mediante la configuración de un [BOSH](http://bosh.io) director, una máquina virtual que coordina la implementación de hello del entorno de nube Foundry de Hola.</span><span class="sxs-lookup"><span data-stu-id="df0df-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="df0df-112">Si va a implementar PCF de hello Azure Marketplace, tome nota de hello SYSTEMDOMAINURL y credenciales de administrador de hello necesitan tooaccess Hola esencial el Administrador de aplicaciones, los cuales se describen en la Guía de implementación de marketplace de Hola.</span><span class="sxs-lookup"><span data-stu-id="df0df-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="df0df-113">Únicamente es necesario toocomplete este tutorial.</span><span class="sxs-lookup"><span data-stu-id="df0df-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="df0df-114">Para las implementaciones de marketplace, hello SYSTEMDOMAINURL está en hello formulario https://system. *dirección ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="df0df-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="df0df-115">Conectar toohello controlador de nube</span><span class="sxs-lookup"><span data-stu-id="df0df-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="df0df-116">Hola controlador de nube es el entorno de Foundry en la nube de tooa de punto de entrada principal de Hola para implementar y administrar aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="df0df-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="df0df-117">Hola core API de controlador de nube (CCAPI) es una API de REST, pero es accesible a través de varias herramientas.</span><span class="sxs-lookup"><span data-stu-id="df0df-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="df0df-118">En este caso, se interactuar con él a través de hello [nube Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="df0df-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="df0df-119">Puede instalar Hola CLI en Linux, Mac OS o Windows, pero si prefiere no tooinstall en absoluto, está disponible preinstalado en hello [Shell en la nube de Azure][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="df0df-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="df0df-120">anteponer toolog, `api` toohello SYSTEMDOMAINURL que obtuvo de la implementación de marketplace de Hola.</span><span class="sxs-lookup"><span data-stu-id="df0df-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="df0df-121">Puesto que la implementación predeterminada de hello usa un certificado autofirmado, también debe incluir hello `skip-ssl-validation` cambiar.</span><span class="sxs-lookup"><span data-stu-id="df0df-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="df0df-122">Son toolog solicitada en toohello controlador de nube.</span><span class="sxs-lookup"><span data-stu-id="df0df-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="df0df-123">Usar credenciales de cuenta de administrador de Hola que adquirió de pasos de implementación de hello marketplace.</span><span class="sxs-lookup"><span data-stu-id="df0df-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="df0df-124">En la nube Foundry proporciona *organizaciones* y *espacios* como los equipos de los espacios de nombres tooisolate hello y entornos dentro de una implementación compartida.</span><span class="sxs-lookup"><span data-stu-id="df0df-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="df0df-125">Hola implementación de marketplace PCF incluye predeterminado hello *system* org y un conjunto de espacios crean toocontain componentes básicos de hello, como servicio de escalado automático de Hola y Hola Azure service broker.</span><span class="sxs-lookup"><span data-stu-id="df0df-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="df0df-126">Por ahora, elija hello *system* espacio.</span><span class="sxs-lookup"><span data-stu-id="df0df-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="df0df-127">Creación de una organización y un espacio</span><span class="sxs-lookup"><span data-stu-id="df0df-127">Create an org and space</span></span>

<span data-ttu-id="df0df-128">Si escribe `cf apps`, verá un conjunto de aplicaciones de sistema que se han implementado en el espacio de sistema de hello en hello sistema org</span><span class="sxs-lookup"><span data-stu-id="df0df-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="df0df-129">Debe mantener hello *system* org reservado para las aplicaciones del sistema, por lo que crear un toohouse de organización y el espacio de nuestra aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="df0df-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="df0df-130">Use Hola destino comando tooswitch toohello nueva organización y el espacio:</span><span class="sxs-lookup"><span data-stu-id="df0df-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="df0df-131">Ahora, cuando se implementa una aplicación, se crea automáticamente en el espacio y Hola nueva organización.</span><span class="sxs-lookup"><span data-stu-id="df0df-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="df0df-132">tooconfirm que actualmente no hay ninguna aplicación en hello nuevo org/espacio, escriba `cf apps` nuevo.</span><span class="sxs-lookup"><span data-stu-id="df0df-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="df0df-133">Para obtener más información acerca de organizaciones y espacios, y cómo se puede usar para el control de acceso basado en roles (RBAC), vea hello [documentación de nube Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="df0df-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="df0df-134">Implementar una aplicación</span><span class="sxs-lookup"><span data-stu-id="df0df-134">Deploy an application</span></span>

<span data-ttu-id="df0df-135">Vamos a usar una aplicación de nube Foundry de ejemplo denominada Hola Spring en la nube, que está escrito en Java y se basa en hello [Spring Framework](http://spring.io) y [Spring arranque](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="df0df-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="df0df-136">Clonar el repositorio de nube de primavera de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="df0df-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="df0df-137">Hola aplicación de ejemplo de Hola Spring nube está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="df0df-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="df0df-138">Clonar tooyour entorno y cambie al directorio nuevo hello:</span><span class="sxs-lookup"><span data-stu-id="df0df-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="df0df-139">Compilar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="df0df-139">Build hello application</span></span>

<span data-ttu-id="df0df-140">Aplicación Hola de compilación con [Maven Apache](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="df0df-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="df0df-141">Implementar la aplicación hello con inserción cf</span><span class="sxs-lookup"><span data-stu-id="df0df-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="df0df-142">Puede implementar la mayoría de las aplicaciones tooCloud Foundry con hello `push` comando:</span><span class="sxs-lookup"><span data-stu-id="df0df-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="df0df-143">Cuando se *inserción* una aplicación, en la nube Foundry detecta el tipo de saludo de la aplicación (en este caso, una aplicación de Java) e identifica sus dependencias (en este caso, Hola Spring marco de trabajo).</span><span class="sxs-lookup"><span data-stu-id="df0df-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="df0df-144">A continuación, empaqueta todos los elementos requeridos toorun el código en una imagen de contenedor independiente, que se conoce como un *droplet*.</span><span class="sxs-lookup"><span data-stu-id="df0df-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="df0df-145">Por último, programaciones de nube Foundry Hola aplicación en uno de hello equipos disponibles en su entorno y crea una dirección URL donde se puede llegar a él, que está disponible en la salida de hello de comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="df0df-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Salida de comando cf push][cf-push-output]

<span data-ttu-id="df0df-147">aplicación hello-spring-cloud toosee hello, URL Abrir Hola proporcionado en el explorador:</span><span class="sxs-lookup"><span data-stu-id="df0df-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Interfaz de usuario predeterminada de Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="df0df-149">toolearn más sobre lo que ocurre durante `cf push`, consulte [cómo se almacenan las aplicaciones] [ cf-push-docs] Hola documentación Foundry en la nube.</span><span class="sxs-lookup"><span data-stu-id="df0df-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="df0df-150">Visualización de registros de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="df0df-150">View application logs</span></span>

<span data-ttu-id="df0df-151">Puede usar los registros de tooview de nube Foundry CLI de Hola para una aplicación por su nombre:</span><span class="sxs-lookup"><span data-stu-id="df0df-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="df0df-152">De forma predeterminada, Hola registra el comando usa *final*, que muestra nuevos registros, tal y como se escriben.</span><span class="sxs-lookup"><span data-stu-id="df0df-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="df0df-153">aparecen toosee nuevos registros, actualizar la aplicación de nube de primavera de Hola de hello en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="df0df-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="df0df-154">registros de tooview que ya se han escrito, agregar hello `recent` cambiar:</span><span class="sxs-lookup"><span data-stu-id="df0df-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="df0df-155">Aplicación Hola a escala</span><span class="sxs-lookup"><span data-stu-id="df0df-155">Scale hello application</span></span>

<span data-ttu-id="df0df-156">De forma predeterminada, `cf push` solo crea una instancia individual de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="df0df-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="df0df-157">tooensure alta disponibilidad y escalado habilitar un mayor rendimiento, por lo general desea toorun más de una instancia de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="df0df-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="df0df-158">Puede escalar fácilmente las aplicaciones ya implementadas mediante hello `scale` comando:</span><span class="sxs-lookup"><span data-stu-id="df0df-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="df0df-159">Hola ejecución `cf app` comando en la aplicación hello muestra que en la nube Foundry crea otra instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="df0df-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="df0df-160">Cuando se inicia la aplicación hello, en la nube Foundry inicia automáticamente tooit de tráfico de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="df0df-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="df0df-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="df0df-161">Next steps</span></span>

- <span data-ttu-id="df0df-162">[Hola de lectura documentación Foundry en la nube][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="df0df-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="df0df-163">[Configurar el complemento de Visual Studio Team Services Hola para Foundry en la nube][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="df0df-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="df0df-164">[Configurar Hola inyectores de análisis de registro de Microsoft para la nube Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="df0df-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png