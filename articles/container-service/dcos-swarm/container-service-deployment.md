---
title: "Implementación de un clúster de contenedores de Docker en Azure | Microsoft Docs"
description: "Implementación de una solución de Kubernetes, DC/OS o Docker Swarm en Azure Container Service mediante Azure Portal o una plantilla de Resource Manager."
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
ms.openlocfilehash: 0ef256537bf095e2a5d582bd345a9c8dcede2095
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-the-azure-portal"></a><span data-ttu-id="15b41-104">Implementación de una solución de hospedaje de contenedor de Docker mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="15b41-104">Deploy a Docker container hosting solution using the Azure portal</span></span>



<span data-ttu-id="15b41-105">El servicio Contenedor de Azure proporciona una rápida implementación de agrupación en clústeres de contenedor de código abierto y soluciones de orquestación populares.</span><span class="sxs-lookup"><span data-stu-id="15b41-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="15b41-106">Este documento es una guía paso a paso para implementar un clúster de Azure Container Service mediante Azure Portal o una plantilla de inicio rápido de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="15b41-106">This document walks you through deploying an Azure Container Service cluster by using the Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="15b41-107">También se puede implementar un clúster de Azure Container Service mediante la [CLI de Azure 2.0](container-service-create-acs-cluster-cli.md) o las API de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="15b41-107">You can also deploy an Azure Container Service cluster by using the [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or the Azure Container Service APIs.</span></span>

<span data-ttu-id="15b41-108">Para más información, consulte [Presentación de Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="15b41-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="15b41-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="15b41-109">Prerequisites</span></span>

* <span data-ttu-id="15b41-110">**Suscripción a Azure:** si no tiene una, suscríbase para una obtener una [evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="15b41-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="15b41-111">En un clúster más grande, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.</span><span class="sxs-lookup"><span data-stu-id="15b41-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15b41-112">El uso de la suscripción de Azure y las [cuotas de recursos](../../azure-subscription-service-limits.md), como las cuotas de núcleos, pueden limitar el tamaño del clúster que se implementa.</span><span class="sxs-lookup"><span data-stu-id="15b41-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit the size of the cluster you deploy.</span></span> <span data-ttu-id="15b41-113">Para solicitar un aumento de cuota, abra una [solicitud de soporte técnico al cliente en línea](../../azure-supportability/how-to-create-azure-support-request.md) sin cargo alguno.</span><span class="sxs-lookup"><span data-stu-id="15b41-113">To request a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="15b41-114">**Clave pública RSA de SSH**: si la implementación se realiza a través del portal o de una de las plantillas de inicio rápido de Azure, es preciso especificar la clave pública para la autenticación con máquinas virtuales de Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="15b41-114">**SSH RSA public key**: When deploying through the portal or one of the Azure quickstart templates, you need to provide the public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="15b41-115">Para crear claves RSA de SSH (Secure Shell), consulte las instrucciones de [OS X y Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o de [Windows](../../virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="15b41-115">To create Secure Shell (SSH) RSA keys, see the [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="15b41-116">**Identificador y secreto de cliente de entidad de servicio** (solo Kubernetes): para más información e instrucciones sobre cómo crear una entidad de servicio de Azure Active Directory, consulte [Acerca de la entidad de servicio de Azure Active Directory para un clúster de Kubernetes en Azure Container Service](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="15b41-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance to create an Azure Active Directory service principal, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-the-azure-portal"></a><span data-ttu-id="15b41-117">Creación de un clúster mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="15b41-117">Create a cluster by using the Azure portal</span></span>
1. <span data-ttu-id="15b41-118">Inicie sesión en Azure Portal, seleccione **Nuevo**, y busque **Azure Container Service** en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="15b41-118">Sign in to the Azure portal, select **New**, and search the Azure Marketplace for **Azure Container Service**.</span></span>

    ![Azure Container Service en Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="15b41-120">Haga clic en **Azure Container Service** y luego en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="15b41-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="15b41-121">En la hoja **Básico**, especifique la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="15b41-121">On the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="15b41-122">**Orquestador**: seleccione uno de los orquestadores de contenedor para implementar en el clúster.</span><span class="sxs-lookup"><span data-stu-id="15b41-122">**Orchestrator**: Select one of the container orchestrators to deploy on the cluster.</span></span>
        * <span data-ttu-id="15b41-123">**DC/OS**: implementa un clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="15b41-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="15b41-124">**Swarm**: implementa un clúster de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="15b41-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="15b41-125">**Kubernetes**: implementa un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="15b41-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="15b41-126">**Suscripción**: seleccione una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="15b41-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="15b41-127">**Grupo de recursos**: escriba el nombre de un nuevo grupo de recursos para la implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-127">**Resource group**: Enter the name of a new resource group for the deployment.</span></span>
    * <span data-ttu-id="15b41-128">**Ubicación**: seleccione una región de Azure para la implementación del servicio Contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="15b41-128">**Location**: Select an Azure region for the Azure Container Service deployment.</span></span> <span data-ttu-id="15b41-129">Para ver la disponibilidad, consulte [Productos disponibles por región](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="15b41-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Configuración básica](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="15b41-131">Haga clic en **Aceptar** cuando esté listo para continuar.</span><span class="sxs-lookup"><span data-stu-id="15b41-131">Click **OK** when you're ready to proceed.</span></span>

4. <span data-ttu-id="15b41-132">En la hoja **Master configuration** (Configuración maestra), especifique la siguiente configuración para los nodos maestros de Linux del clúster (algunos valores de configuración de especifican para cada orquestador):</span><span class="sxs-lookup"><span data-stu-id="15b41-132">On the **Master configuration** blade, enter the following settings for the Linux master node or nodes in the cluster (some settings are specific to each orchestrator):</span></span>

    * <span data-ttu-id="15b41-133">**Master DNS name** (Nombre DNS del maestro): el prefijo usado para crear un nombre de dominio completo (FQDN) para el maestro.</span><span class="sxs-lookup"><span data-stu-id="15b41-133">**Master DNS name**: The prefix used to create a unique fully qualified domain name (FQDN) for the master.</span></span> <span data-ttu-id="15b41-134">El FQDN del maestro tiene el formato *prefijo*mgmt.*ubicación*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="15b41-134">The master FQDN is of the form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="15b41-135">**Nombre de usuario**: el nombre de usuario de una cuenta en cada una de las máquinas virtuales Linux del clúster.</span><span class="sxs-lookup"><span data-stu-id="15b41-135">**User name**: The user name for an account on each of the Linux virtual machines in the cluster.</span></span>
    * <span data-ttu-id="15b41-136">**SSH RSA public key** (Clave pública RSA de SSH): agregue la clave pública que se usará para la autenticación en las máquinas virtuales Linux.</span><span class="sxs-lookup"><span data-stu-id="15b41-136">**SSH RSA public key**: Add the public key to be used for authentication against the Linux virtual machines.</span></span> <span data-ttu-id="15b41-137">Es importante que esta clave no tenga saltos de línea y que incluya el prefijo `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="15b41-137">It is important that this key contains no line breaks, and it includes the `ssh-rsa` prefix.</span></span> <span data-ttu-id="15b41-138">El sufijo `username@domain` es opcional.</span><span class="sxs-lookup"><span data-stu-id="15b41-138">The `username@domain` postfix is optional.</span></span> <span data-ttu-id="15b41-139">La clave debería tener un formato similar al siguiente: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span><span class="sxs-lookup"><span data-stu-id="15b41-139">The key should look something like the following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="15b41-140">**Entidad de servicio**: si seleccionó el orquestador Kubernetes, escriba un **id. de cliente de entidad de servicio** (también llamado appId) de Azure Active Directory y un **secreto de cliente de entidad de servicio** (contraseña).</span><span class="sxs-lookup"><span data-stu-id="15b41-140">**Service principal**: If you selected the Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called the appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="15b41-141">Para más información, consulte [About the Azure Active Directory service principal for a Kubernetes cluster in Azure Container Service](../kubernetes/container-service-kubernetes-service-principal.md) (Acerca de la entidad de servicio de Azure Active Directory para un clúster de Kubernetes de Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="15b41-141">For more information, see [About the service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="15b41-142">**Master count**(Número de patrones): el número de patrones en el clúster.</span><span class="sxs-lookup"><span data-stu-id="15b41-142">**Master count**: The number of masters in the cluster.</span></span>
    * <span data-ttu-id="15b41-143">**VM diagnostics** (Diagnóstico de máquina virtual): en algunos orquestadores, puede habilitar el diagnóstico de máquina virtual en los maestros.</span><span class="sxs-lookup"><span data-stu-id="15b41-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on the masters.</span></span>

    ![Configuración maestra](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="15b41-145">Haga clic en **Aceptar** cuando esté listo para continuar.</span><span class="sxs-lookup"><span data-stu-id="15b41-145">Click **OK** when you're ready to proceed.</span></span>

5. <span data-ttu-id="15b41-146">En la hoja **Configuración del Agente**, escriba la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="15b41-146">On the **Agent configuration** blade, enter the following information:</span></span>

    * <span data-ttu-id="15b41-147">**Número de agentes**: en el caso de Docker Swarm y Kubernetes, este valor es el número inicial de agentes del conjunto de escalado de agentes.</span><span class="sxs-lookup"><span data-stu-id="15b41-147">**Agent count**: For Docker Swarm and Kubernetes, this value is the initial number of agents in the agent scale set.</span></span> <span data-ttu-id="15b41-148">En el caso de DC/OS, se trata del número inicial de agentes de un conjunto de escalado privado.</span><span class="sxs-lookup"><span data-stu-id="15b41-148">For DC/OS, it is the initial number of agents in a private scale set.</span></span> <span data-ttu-id="15b41-149">Además, se crea un conjunto de escalado público para DC/OS, que contiene un número predeterminado de agentes.</span><span class="sxs-lookup"><span data-stu-id="15b41-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="15b41-150">El número de agentes de este conjunto de escalado público lo determina el número de maestros en el clúster: un agente público para un maestro y dos agentes públicos para tres o cinco maestros.</span><span class="sxs-lookup"><span data-stu-id="15b41-150">The number of agents in this public scale set is determined by the number of masters in the cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="15b41-151">**Agent virtual machine size**(Tamaño de máquina virtual de agente): el tamaño de las máquinas virtuales de los agentes.</span><span class="sxs-lookup"><span data-stu-id="15b41-151">**Agent virtual machine size**: The size of the agent virtual machines.</span></span>
    * <span data-ttu-id="15b41-152">**Sistema operativo**: esta opción está actualmente disponible solo si seleccionó el orquestrator Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="15b41-152">**Operating system**: This setting is currently available only if you selected the Kubernetes orchestrator.</span></span> <span data-ttu-id="15b41-153">Elija una distribución de Linux o un sistema operativo de Windows Server para que se ejecute en los agentes.</span><span class="sxs-lookup"><span data-stu-id="15b41-153">Choose either a Linux distribution or a Windows Server operating system to run on the agents.</span></span> <span data-ttu-id="15b41-154">Esta configuración determina si el clúster puede ejecutar aplicaciones de contenedor de Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="15b41-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="15b41-155">La compatibilidad con el contenedor de Windows está en versión preliminar para los clústeres de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="15b41-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="15b41-156">En clústeres de DC/OS y Swarm, actualmente solo se admiten agentes de Linux en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="15b41-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="15b41-157">**Agent credentials** (Credenciales del agente): si seleccionó el sistema operativo Windows, escriba un **nombre de usuario** y una **contraseña** de administrador para las máquinas virtuales del agente.</span><span class="sxs-lookup"><span data-stu-id="15b41-157">**Agent credentials**: If you selected the Windows operating system, enter an administrator **User name** and **Password** for the agent VMs.</span></span> 

    ![Configuración de agente](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="15b41-159">Haga clic en **Aceptar** cuando esté listo para continuar.</span><span class="sxs-lookup"><span data-stu-id="15b41-159">Click **OK** when you're ready to proceed.</span></span>

6. <span data-ttu-id="15b41-160">Una vez finalizada la validación del servicio, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="15b41-160">After service validation finishes, click **OK**.</span></span>

    ![Validación](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="15b41-162">Revise los términos.</span><span class="sxs-lookup"><span data-stu-id="15b41-162">Review the terms.</span></span> <span data-ttu-id="15b41-163">Haga clic en **Crear** para iniciar el proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-163">To start the deployment process, click **Create**.</span></span>

    <span data-ttu-id="15b41-164">Si ha elegido anclar la implementación al Portal de Azure, se verá el estado de la implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-164">If you've elected to pin the deployment to the Azure portal, you can see the deployment status.</span></span>

    ![Estado de implementación](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="15b41-166">La implementación tarda varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="15b41-166">The deployment takes several minutes to complete.</span></span> <span data-ttu-id="15b41-167">Después, el clúster de Azure Container Service estará listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="15b41-167">Then, the Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="15b41-168">Creación de un clúster mediante una plantilla de inicio rápido</span><span class="sxs-lookup"><span data-stu-id="15b41-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="15b41-169">Las plantillas de inicio rápido de Azure permiten implementar un clúster en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="15b41-169">Azure quickstart templates are available to deploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="15b41-170">Las plantillas de inicio rápido que se proporcionan se pueden modificar para que incluyan una configuración de Azure adicional o avanzada.</span><span class="sxs-lookup"><span data-stu-id="15b41-170">The provided quickstart templates can be modified to include additional or advanced Azure configuration.</span></span> <span data-ttu-id="15b41-171">Para crear un clúster de Azure Container Service mediante una plantilla de inicio rápido de Azure, se necesita una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="15b41-171">To create an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="15b41-172">Si no dispone de ninguna, suscríbase para obtener una [evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="15b41-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="15b41-173">Siga estos pasos para implementar un clúster mediante una plantilla y la CLI de Azure 2.0 (consulte las [instrucciones de instalación y configuración ](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="15b41-173">Follow these steps to deploy a cluster using a template and the Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="15b41-174">En un sistema Windows, puede utilizar pasos similares para implementar una plantilla mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15b41-174">If you're on a Windows system, you can use similar steps to deploy a template using Azure PowerShell.</span></span> <span data-ttu-id="15b41-175">En esta misma sección encontrará los pasos necesarios para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="15b41-175">See steps later in this section.</span></span> <span data-ttu-id="15b41-176">Las plantillas también se pueden implementar a través del [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) o mediante otros métodos.</span><span class="sxs-lookup"><span data-stu-id="15b41-176">You can also deploy a template through the [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="15b41-177">Para implementar un clúster de DC/OS, Docker Swarm o Kubernetes, seleccione una de las plantillas de inicio rápido disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="15b41-177">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="15b41-178">Se muestra una lista parcial.</span><span class="sxs-lookup"><span data-stu-id="15b41-178">A partial list follows.</span></span> <span data-ttu-id="15b41-179">Las plantillas de DC/OS y Swarm son las mismas, excepto por la selección del orquestador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="15b41-179">The DC/OS and Swarm templates are the same, except for the default orchestrator selection.</span></span>

    * [<span data-ttu-id="15b41-180">Plantilla de DC/OS</span><span class="sxs-lookup"><span data-stu-id="15b41-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="15b41-181">Plantilla Swarm</span><span class="sxs-lookup"><span data-stu-id="15b41-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="15b41-182">Plantilla de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="15b41-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="15b41-183">Inicie sesión en su cuenta de Azure (`az login`) y asegúrese de que la CLI de Azure está conectada a su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="15b41-183">Log in to your Azure account (`az login`), and make sure that the Azure CLI is connected to your Azure subscription.</span></span> <span data-ttu-id="15b41-184">Para ver la suscripción predeterminada, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="15b41-184">You can see the default subscription by using the following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="15b41-185">Si tiene más de una suscripción y necesita establecer otra suscripción predeterminada, ejecute `az account set --subscription` y especifique el nombre o identificador de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="15b41-185">If you have more than one subscription and need to set a different default subscription, run `az account set --subscription` and specify the subscription ID or name.</span></span>

3. <span data-ttu-id="15b41-186">Como procedimiento recomendado, utilice un grupo de recursos nuevo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-186">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="15b41-187">Para crear un grupo de recursos nuevo, use el comando `az group create` y especifique el nombre y la ubicación del grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="15b41-187">To create a resource group, use the `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="15b41-188">Cree un archivo JSON que contenga los parámetros de plantilla necesarios.</span><span class="sxs-lookup"><span data-stu-id="15b41-188">Create a JSON file containing the required template parameters.</span></span> <span data-ttu-id="15b41-189">Descargue el archivo de parámetros denominado `azuredeploy.parameters.json` que acompaña a la plantilla de Azure Container Service `azuredeploy.json` en GitHub.</span><span class="sxs-lookup"><span data-stu-id="15b41-189">Download the parameters file named `azuredeploy.parameters.json` that accompanies the Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="15b41-190">Especifique los valores de parámetro necesarios para el clúster.</span><span class="sxs-lookup"><span data-stu-id="15b41-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="15b41-191">Por ejemplo, para usar la [plantilla de DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), especifique los valores de parámetro para `dnsNamePrefix` y `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="15b41-191">For example, to use the [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="15b41-192">Vea las descripciones de `azuredeploy.json` y opciones para otros parámetros.</span><span class="sxs-lookup"><span data-stu-id="15b41-192">See the descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="15b41-193">Para crear un clúster de Container Service, use el archivo de parámetros de implementación con el comando siguiente, donde:</span><span class="sxs-lookup"><span data-stu-id="15b41-193">Create a Container Service cluster by passing the deployment parameters file with the following command, where:</span></span>

    * <span data-ttu-id="15b41-194">**RESOURCE_GROUP** es el nombre del grupo de recursos que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="15b41-194">**RESOURCE_GROUP** is the name of the resource group that you created in the previous step.</span></span>
    * <span data-ttu-id="15b41-195">**DEPLOYMENT_NAME** (opcional) es el nombre que se asigna a la implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-195">**DEPLOYMENT_NAME** (optional) is a name you give to the deployment.</span></span>
    * <span data-ttu-id="15b41-196">**TEMPLATE_URI** es la ubicación del archivo de implementación `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="15b41-196">**TEMPLATE_URI** is the location of the deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="15b41-197">Este identificador URI tiene que ser el archivo sin formato, no un puntero a la interfaz de usuario de GitHub.</span><span class="sxs-lookup"><span data-stu-id="15b41-197">This URI must be the Raw file, not a pointer to the GitHub UI.</span></span> <span data-ttu-id="15b41-198">Para buscar el identificador URI, seleccione el archivo `azuredeploy.json` en GitHub y haga clic en el botón **Raw** (Sin formato).</span><span class="sxs-lookup"><span data-stu-id="15b41-198">To find this URI, select the `azuredeploy.json` file in GitHub, and click the **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="15b41-199">Los parámetros también se pueden especificar en forma de cadena con formato JSON en la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="15b41-199">You can also provide parameters as a JSON-formatted string on the command line.</span></span> <span data-ttu-id="15b41-200">Use un comando similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="15b41-200">Use a command similar to the following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="15b41-201">La implementación tarda varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="15b41-201">The deployment takes several minutes to complete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="15b41-202">Comandos de PowerShell equivalentes</span><span class="sxs-lookup"><span data-stu-id="15b41-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="15b41-203">Las plantillas de clúster de Azure Container Service también se pueden implementar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15b41-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="15b41-204">Este documento se basa en la versión 1.0 del [módulo de Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="15b41-204">This document is based on the version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="15b41-205">Para implementar un clúster de DC/OS, Docker Swarm o Kubernetes, seleccione una de las plantillas de inicio rápido disponibles en GitHub.</span><span class="sxs-lookup"><span data-stu-id="15b41-205">To deploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of the available quickstart templates from GitHub.</span></span> <span data-ttu-id="15b41-206">Se muestra una lista parcial.</span><span class="sxs-lookup"><span data-stu-id="15b41-206">A partial list follows.</span></span> <span data-ttu-id="15b41-207">Tenga en cuenta que las plantillas de DC/OS y Swarm son iguales, a excepción de la selección del orquestador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="15b41-207">Note that the DC/OS and Swarm templates are the same, with the exception of the default orchestrator selection.</span></span>

    * [<span data-ttu-id="15b41-208">Plantilla de DC/OS</span><span class="sxs-lookup"><span data-stu-id="15b41-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="15b41-209">Plantilla Swarm</span><span class="sxs-lookup"><span data-stu-id="15b41-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="15b41-210">Plantilla de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="15b41-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="15b41-211">Antes de crear un clúster en su suscripción de Azure, compruebe que la sesión de PowerShell se ha iniciado en Azure.</span><span class="sxs-lookup"><span data-stu-id="15b41-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in to Azure.</span></span> <span data-ttu-id="15b41-212">Para ello, puede usar el comando `Get-AzureRMSubscription` :</span><span class="sxs-lookup"><span data-stu-id="15b41-212">You can do this with the `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="15b41-213">Si tiene que iniciar sesión en Azure, use el comando `Login-AzureRMAccount` :</span><span class="sxs-lookup"><span data-stu-id="15b41-213">If you need to sign in to Azure, use the `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="15b41-214">Como procedimiento recomendado, utilice un grupo de recursos nuevo para la implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-214">As a best practice, use a new resource group for the deployment.</span></span> <span data-ttu-id="15b41-215">Para crear un nuevo grupo de recursos, use el comando `New-AzureRmResourceGroup` y especifique el nombre y la región de destino de dicho grupo:</span><span class="sxs-lookup"><span data-stu-id="15b41-215">To create a resource group, use the `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="15b41-216">Después de crear un grupo de recursos, puede crear el clúster con el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="15b41-216">After you create a resource group, you can create your cluster with the following command.</span></span> <span data-ttu-id="15b41-217">El URI de la plantilla deseada se especifica con el parámetro `-TemplateUri`.</span><span class="sxs-lookup"><span data-stu-id="15b41-217">The URI of the desired template is specified with the `-TemplateUri` parameter.</span></span> <span data-ttu-id="15b41-218">Al ejecutar este comando, PowerShell solicita los valores de los parámetros de implementación.</span><span class="sxs-lookup"><span data-stu-id="15b41-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="15b41-219">Suministro de los parámetros de plantilla</span><span class="sxs-lookup"><span data-stu-id="15b41-219">Provide template parameters</span></span>
<span data-ttu-id="15b41-220">Si está familiarizado con PowerShell, sabe que puede recorrer los parámetros disponibles para un cmdlet; basta con que escriba un signo menos (-) y luego presione la tecla TAB.</span><span class="sxs-lookup"><span data-stu-id="15b41-220">If you're familiar with PowerShell, you know that you can cycle through the available parameters for a cmdlet by typing a minus sign (-) and then pressing the TAB key.</span></span> <span data-ttu-id="15b41-221">Esta misma funcionalidad también sirve para los parámetros que se definen en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="15b41-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="15b41-222">En cuanto escribe el nombre de la plantilla, el cmdlet captura la plantilla, analiza los parámetros y agrega los parámetros de la plantilla al comando de manera dinámica.</span><span class="sxs-lookup"><span data-stu-id="15b41-222">As soon as you type the template name, the cmdlet fetches the template, parses the parameters, and adds the template parameters to the command dynamically.</span></span> <span data-ttu-id="15b41-223">Esto hace que sea fácil especificar los valores de los parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="15b41-223">This makes it easy to specify the template parameter values.</span></span> <span data-ttu-id="15b41-224">Además, si olvida el valor de algún parámetro necesario, PowerShell le pide dicho valor.</span><span class="sxs-lookup"><span data-stu-id="15b41-224">And, if you forget a required parameter value, PowerShell prompts you for the value.</span></span>

<span data-ttu-id="15b41-225">A continuación se muestra el comando completo con parámetros incluidos.</span><span class="sxs-lookup"><span data-stu-id="15b41-225">Here is the full command, with parameters included.</span></span> <span data-ttu-id="15b41-226">Proporcione sus propios valores para los nombres de los recursos.</span><span class="sxs-lookup"><span data-stu-id="15b41-226">Provide your own values for the names of the resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="15b41-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15b41-227">Next steps</span></span>
<span data-ttu-id="15b41-228">Ahora que tiene un clúster funcionando, consulte los siguientes documentos para obtener información detallada sobre conexión y administración:</span><span class="sxs-lookup"><span data-stu-id="15b41-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="15b41-229">Conexión a un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="15b41-229">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="15b41-230">Administración de contenedores con la API de REST</span><span class="sxs-lookup"><span data-stu-id="15b41-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="15b41-231">Administración de contenedores con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="15b41-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="15b41-232">Trabajo con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="15b41-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
