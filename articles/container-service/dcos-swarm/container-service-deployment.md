---
title: "clúster de aaaDeploy un contenedor de Docker en Azure | Documentos de Microsoft"
description: "Implementar una solución Kubernetes, DC/OS o Docker Swarm en el servicio de contenedor de Azure mediante Hola portal de Azure o una plantilla de administrador de recursos."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="5e532-104">Implementar un contenedor de Docker con hello Azure portal de solución de hospedaje</span><span class="sxs-lookup"><span data-stu-id="5e532-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="5e532-105">El servicio Contenedor de Azure proporciona una rápida implementación de agrupación en clústeres de contenedor de código abierto y soluciones de orquestación populares.</span><span class="sxs-lookup"><span data-stu-id="5e532-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="5e532-106">Este documento le guía a través de la implementación de un clúster de servicio de contenedor de Azure mediante Hola portal de Azure o una plantilla de inicio rápido de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5e532-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="5e532-107">También puede implementar un clúster de servicio de contenedor de Azure mediante el uso de hello [CLI de Azure 2.0](container-service-create-acs-cluster-cli.md) u Hola API de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="5e532-108">Para más información, consulte [Presentación de Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5e532-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5e532-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5e532-109">Prerequisites</span></span>

* <span data-ttu-id="5e532-110">**Suscripción a Azure:** si no tiene una, suscríbase para una obtener una [evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="5e532-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="5e532-111">En un clúster más grande, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.</span><span class="sxs-lookup"><span data-stu-id="5e532-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e532-112">El uso de la suscripción de Azure y [cuotas de recursos](../../azure-subscription-service-limits.md), como las cuotas de núcleos, puede limitar tamaño de Hola de implementar el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="5e532-113">toorequest un aumento de la cuota, abra un [solicitud de soporte técnico al cliente en línea](../../azure-supportability/how-to-create-azure-support-request.md) sin cargo.</span><span class="sxs-lookup"><span data-stu-id="5e532-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="5e532-114">**Clave pública SSH RSA**: cuando se implementa a través del portal de Hola o de plantillas de inicio rápido de Azure de hello, necesita clave pública de tooprovide hello para la autenticación con máquinas virtuales de servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="5e532-115">claves RSA de Shell seguro (SSH) toocreate, vea hello [OS X y Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../../virtual-machines/linux/ssh-from-windows.md) instrucciones.</span><span class="sxs-lookup"><span data-stu-id="5e532-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="5e532-116">**Id. de entidad de seguridad de cliente y el secreto del servicio** (sólo Kubernetes): para más información e instrucciones toocreate una entidad de seguridad de servicio de Azure Active Directory, vea [acerca de la entidad de seguridad de servicio de Hola para un clúster de Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5e532-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="5e532-117">Crear un clúster mediante el uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5e532-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="5e532-118">Seleccione inicio de sesión en el portal de Azure, toohello **New**y busque hello Azure Marketplace para **servicio de contenedor de Azure**.</span><span class="sxs-lookup"><span data-stu-id="5e532-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Azure Container Service en Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="5e532-120">Haga clic en **Azure Container Service** y luego en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5e532-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="5e532-121">En hello **Fundamentos** hoja, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5e532-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="5e532-122">**Orchestrator**: seleccione uno de hello contenedor orchestrators toodeploy en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="5e532-123">**DC/OS**: implementa un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5e532-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="5e532-124">**Swarm**: implementa un clúster de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="5e532-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="5e532-125">**Kubernetes**: implementa un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5e532-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="5e532-126">**Suscripción**: seleccione una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="5e532-127">**Grupo de recursos**: escriba Hola nombre de un nuevo grupo de recursos para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="5e532-128">**Ubicación**: seleccione una región de Azure para la implementación del servicio de contenedor de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="5e532-129">Para ver la disponibilidad, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="5e532-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Configuración básica](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="5e532-131">Haga clic en **Aceptar** cuando esté listo tooproceed.</span><span class="sxs-lookup"><span data-stu-id="5e532-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="5e532-132">En hello **maestro configuración** hoja, escriba Hola después de la configuración de nodo maestro de Linux de Hola o nodos de clúster de hello (algunas opciones de configuración son específicos tooeach orchestrator):</span><span class="sxs-lookup"><span data-stu-id="5e532-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="5e532-133">**Nombre DNS del maestro**: hello toocreate de prefijo que se usa un único completo de nombre de dominio (FQDN) para el patrón de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="5e532-134">Hola FQDN maestro tiene el formato de hello *prefijo*Admin.*ubicación*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="5e532-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="5e532-135">**Nombre de usuario**: nombre de usuario de Hola para una cuenta en cada una de las máquinas virtuales de Linux hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="5e532-136">**Clave pública SSH RSA**: agregar hello toobe de clave pública utilizado para la autenticación frente a máquinas virtuales Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="5e532-137">Es importante que esta clave no contiene saltos de línea, e incluye hello `ssh-rsa` prefijo.</span><span class="sxs-lookup"><span data-stu-id="5e532-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="5e532-138">Hola `username@domain` postfijo es opcional.</span><span class="sxs-lookup"><span data-stu-id="5e532-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="5e532-139">Hello clave debería parecerse al siguiente hello: **ssh-rsa AAAAB3Nz... <> …... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="5e532-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="5e532-140">**Entidad de servicio**: si ha seleccionado orchestrator Kubernetes de hello, escriba un Azure Active Directory **Id. de cliente principal de servicio** (también denominada Hola appId) y **secreto de cliente principal de servicio** (contraseña).</span><span class="sxs-lookup"><span data-stu-id="5e532-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="5e532-141">Para obtener más información, consulte [acerca de la entidad de seguridad de servicio de Hola para un clúster de Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="5e532-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="5e532-142">**Maestro de recuento**: Hola de patrones en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="5e532-143">**Diagnóstico de máquina virtual**: para algunos orchestrators, puede habilitar el diagnóstico de máquina virtual de las páginas maestras Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Configuración maestra](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="5e532-145">Haga clic en **Aceptar** cuando esté listo tooproceed.</span><span class="sxs-lookup"><span data-stu-id="5e532-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="5e532-146">En hello **configuración del agente** hoja, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5e532-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="5e532-147">**Número de agentes**: para el conjunto de Docker y Kubernetes, este valor es el número inicial de Hola de agentes en el conjunto de escalas de agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="5e532-148">Para el controlador de dominio/OS, es Hola número inicial de agentes en un conjunto de escala privada.</span><span class="sxs-lookup"><span data-stu-id="5e532-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="5e532-149">Además, se crea un conjunto de escalado público para DC/OS, que contiene un número predeterminado de agentes.</span><span class="sxs-lookup"><span data-stu-id="5e532-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="5e532-150">número de agentes en este conjunto de escala pública Hello se determina una por número de Hola de patrones en clúster de hello: un agente público para un patrón y los dos agentes públicos para patrones de tres o cinco.</span><span class="sxs-lookup"><span data-stu-id="5e532-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="5e532-151">**Tamaño de la máquina virtual de agente**: Hola tamaño de máquinas virtuales de hello agente.</span><span class="sxs-lookup"><span data-stu-id="5e532-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="5e532-152">**Sistema operativo**: esta opción está actualmente disponible sólo si seleccionó orchestrator Kubernetes de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="5e532-153">Elija una distribución de Linux o un toorun de sistema operativo Windows Server en los agentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="5e532-154">Esta configuración determina si el clúster puede ejecutar aplicaciones de contenedor de Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="5e532-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="5e532-155">La compatibilidad con el contenedor de Windows está en versión preliminar para los clústeres de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5e532-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="5e532-156">En clústeres de DC/OS y Swarm, actualmente solo se admiten agentes de Linux en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="5e532-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="5e532-157">**Las credenciales del agente**: si ha seleccionado el sistema operativo de Windows hello, escriba administrador **nombre de usuario** y **contraseña** para agente de hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="5e532-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Configuración de agente](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="5e532-159">Haga clic en **Aceptar** cuando esté listo tooproceed.</span><span class="sxs-lookup"><span data-stu-id="5e532-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="5e532-160">Una vez finalizada la validación del servicio, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5e532-160">After service validation finishes, click **OK**.</span></span>

    ![Validación](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="5e532-162">Revise los términos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-162">Review hello terms.</span></span> <span data-ttu-id="5e532-163">proceso de implementación de hello toostart, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="5e532-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="5e532-164">Si ha elegido toopin Hola implementación toohello portal de Azure, puede ver el estado de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Estado de implementación](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="5e532-166">implementación de Hello toma toocomplete de varios minutos.</span><span class="sxs-lookup"><span data-stu-id="5e532-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="5e532-167">A continuación, clúster de servicio de contenedor de Azure Hola está listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="5e532-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="5e532-168">Creación de un clúster mediante una plantilla de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="5e532-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="5e532-169">Plantillas de inicio rápido de Azure están disponible toodeploy un clúster en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="5e532-170">Hola proporciona plantillas de inicio rápido pueden ser modificado tooinclude adicionales o avanzados configuración de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="5e532-171">toocreate un clúster de servicio de contenedor de Azure mediante una plantilla de inicio rápido de Azure, se necesita una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="5e532-172">Si no dispone de ninguna, suscríbase para obtener una [evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="5e532-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="5e532-173">Siga estos pasos toodeploy un clúster con una plantilla y Hola CLI de Azure 2.0 (vea [instrucciones de instalación y](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="5e532-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="5e532-174">Si está en un sistema de Windows, puede usar toodeploy de pasos similares una plantilla con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e532-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="5e532-175">En esta misma sección encontrará los pasos necesarios para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="5e532-175">See steps later in this section.</span></span> <span data-ttu-id="5e532-176">También puede implementar una plantilla a través de hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) u otros métodos.</span><span class="sxs-lookup"><span data-stu-id="5e532-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="5e532-177">toodeploy un clúster DC/OS, Docker Swarm o Kubernetes, seleccione uno de plantillas de hello quickstart disponibles desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e532-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="5e532-178">Se muestra una lista parcial.</span><span class="sxs-lookup"><span data-stu-id="5e532-178">A partial list follows.</span></span> <span data-ttu-id="5e532-179">Hola DC/OS y plantillas de conjunto se Hola mismo, excepto la selección de orchestrator de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5e532-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="5e532-180">Plantilla de DC/OS</span><span class="sxs-lookup"><span data-stu-id="5e532-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="5e532-181">Plantilla Swarm</span><span class="sxs-lookup"><span data-stu-id="5e532-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="5e532-182">Plantilla de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5e532-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="5e532-183">Inicie sesión en tooyour cuenta de Azure (`az login`) y asegúrese de que ese Hola CLI de Azure está conectado tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5e532-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="5e532-184">Puede ver suscripción predeterminada de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5e532-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="5e532-185">Si tiene más de un tooset de suscripción y la necesidad de una suscripción predeterminados diferentes, ejecute `az account set --subscription` y especifique un identificador de suscripción de Hola o nombre.</span><span class="sxs-lookup"><span data-stu-id="5e532-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="5e532-186">Como práctica recomendada, utilice un nuevo grupo de recursos para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="5e532-187">toocreate un grupo de recursos, utilice hello `az group create` comando especifica un nombre de grupo de recursos y la ubicación:</span><span class="sxs-lookup"><span data-stu-id="5e532-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="5e532-188">Crear una JSON archivo contenedor Hola necesaria plantilla parámetros.</span><span class="sxs-lookup"><span data-stu-id="5e532-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="5e532-189">Archivo de parámetros de hello descarga denominado `azuredeploy.parameters.json` que acompaña a la plantilla de servicio de contenedor de Azure de hello `azuredeploy.json` en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e532-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="5e532-190">Especifique los valores de parámetro necesarios para el clúster.</span><span class="sxs-lookup"><span data-stu-id="5e532-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="5e532-191">Por ejemplo, toouse hello [plantilla DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), proporcionar valores de parámetro para `dnsNamePrefix` y `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="5e532-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="5e532-192">Ver una descripción de hello en `azuredeploy.json` y opciones para otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="5e532-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="5e532-193">Crear un clúster de servicio de contenedor al pasar el archivo de parámetros de implementación de hello con hello siguiente comando, donde:</span><span class="sxs-lookup"><span data-stu-id="5e532-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="5e532-194">**RESOURCE_GROUP** es nombre Hola Hola del grupo de recursos que creó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="5e532-195">**DEPLOYMENT_NAME** (opcional) es un nombre que le asigne toohello implementación.</span><span class="sxs-lookup"><span data-stu-id="5e532-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="5e532-196">**TEMPLATE_URI** es Hola ubicación del archivo de implementación de hello `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="5e532-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="5e532-197">Este identificador URI debe ser el archivo sin formato hello, no toohello puntero GitHub UI.</span><span class="sxs-lookup"><span data-stu-id="5e532-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="5e532-198">toofind este URI, seleccione hello `azuredeploy.json` en GitHub el archivo y haga clic en hello **Raw** botón.</span><span class="sxs-lookup"><span data-stu-id="5e532-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="5e532-199">También puede proporcionar parámetros como una cadena con formato JSON en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="5e532-200">Utilice un siguiente toohello similar de comando:</span><span class="sxs-lookup"><span data-stu-id="5e532-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="5e532-201">implementación de Hello toma toocomplete de varios minutos.</span><span class="sxs-lookup"><span data-stu-id="5e532-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="5e532-202">Comandos de PowerShell equivalentes</span><span class="sxs-lookup"><span data-stu-id="5e532-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="5e532-203">Las plantillas de clúster de Azure Container Service también se pueden implementar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e532-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="5e532-204">Este documento se basa en la versión 1.0 de hello [módulo Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="5e532-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="5e532-205">toodeploy un clúster DC/OS, Docker Swarm o Kubernetes, seleccione uno de plantillas de hello quickstart disponibles desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="5e532-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="5e532-206">Se muestra una lista parcial.</span><span class="sxs-lookup"><span data-stu-id="5e532-206">A partial list follows.</span></span> <span data-ttu-id="5e532-207">Tenga en cuenta que Hola DC/OS y plantillas de conjunto se Hola igual, con excepción de Hola de selección de orchestrator de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5e532-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="5e532-208">Plantilla de DC/OS</span><span class="sxs-lookup"><span data-stu-id="5e532-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="5e532-209">Plantilla Swarm</span><span class="sxs-lookup"><span data-stu-id="5e532-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="5e532-210">Plantilla de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5e532-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="5e532-211">Antes de crear un clúster en su suscripción de Azure, compruebe que se ha suscrito a la sesión de PowerShell en tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5e532-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="5e532-212">Puede hacerlo con hello `Get-AzureRMSubscription` comando:</span><span class="sxs-lookup"><span data-stu-id="5e532-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="5e532-213">Si necesita toosign en tooAzure, usar hello `Login-AzureRMAccount` comando:</span><span class="sxs-lookup"><span data-stu-id="5e532-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="5e532-214">Como práctica recomendada, utilice un nuevo grupo de recursos para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="5e532-215">toocreate un grupo de recursos, utilice hello `New-AzureRmResourceGroup` comando y especifique una región de nombre y el destino de grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="5e532-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="5e532-216">Después de crear un grupo de recursos, puede crear el clúster con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="5e532-217">URI de Hola Hola deseado se especificó una plantilla con hello `-TemplateUri` parámetro.</span><span class="sxs-lookup"><span data-stu-id="5e532-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="5e532-218">Al ejecutar este comando, PowerShell solicita los valores de los parámetros de implementación.</span><span class="sxs-lookup"><span data-stu-id="5e532-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="5e532-219">Suministro de los parámetros de plantilla</span><span class="sxs-lookup"><span data-stu-id="5e532-219">Provide template parameters</span></span>
<span data-ttu-id="5e532-220">Si está familiarizado con PowerShell, sabrá que puede recorrer parámetros disponibles de Hola para un cmdlet, escriba un signo menos (-) y, a continuación, presionando la tecla TAB de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="5e532-221">Esta misma funcionalidad también sirve para los parámetros que se definen en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="5e532-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="5e532-222">En cuanto escriba el nombre de la plantilla de hello, Hola cmdlet captura plantilla hello, analiza los parámetros de Hola y agrega comandos de toohello de parámetros de plantilla de hello dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="5e532-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="5e532-223">Esto facilita valores de parámetro de plantilla toospecify fácil Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="5e532-224">Y, si se olvida de un valor de parámetro necesario, PowerShell le pide el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="5e532-225">Aquí es el comando completo Hola con los parámetros incluidos.</span><span class="sxs-lookup"><span data-stu-id="5e532-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="5e532-226">Proporcionar sus propios valores para los nombres de Hola de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5e532-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="5e532-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e532-227">Next steps</span></span>
<span data-ttu-id="5e532-228">Ahora que tiene un clúster funcionando, consulte los siguientes documentos para obtener información detallada sobre conexión y administración:</span><span class="sxs-lookup"><span data-stu-id="5e532-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="5e532-229">Conectar el clúster del servicio de contenedor de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="5e532-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="5e532-230">Administración de contenedores con la API de REST</span><span class="sxs-lookup"><span data-stu-id="5e532-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="5e532-231">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="5e532-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="5e532-232">Trabajo con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5e532-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
