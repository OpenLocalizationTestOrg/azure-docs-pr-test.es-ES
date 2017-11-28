---
title: "Entidad de servicio de clúster de Azure Kubernetes | Microsoft Docs"
description: "Cree y administre una entidad de servicio de Azure Active Directory para un clúster de Kubernetes en Azure Container Service"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="87446-103">Configuración de una entidad de servicio de Azure AD para un clúster de Kubernetes en Container Service</span><span class="sxs-lookup"><span data-stu-id="87446-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="87446-104">En Azure Container Service, un clúster de Kubernetes requiere una [entidad de servicio de Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) para interactuar con las API de Azure.</span><span class="sxs-lookup"><span data-stu-id="87446-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="87446-105">La entidad de servicio se necesita para administrar dinámicamente recursos como las [rutas definidas por el usuario](../../virtual-network/virtual-networks-udr-overview.md) y [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) de nivel 4.</span><span class="sxs-lookup"><span data-stu-id="87446-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="87446-106">Este artículo muestra distintas opciones para configurar una entidad de servicio para el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="87446-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="87446-107">Por ejemplo, si instaló y configuró la [CLI de Azure 2.0](/cli/azure/install-az-cli2), puede ejecutar el comando [`az acs create`](/cli/azure/acs#create) para crear el clúster de Kubernetes y la entidad de servicio al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="87446-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="87446-108">Requisitos de la entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="87446-108">Requirements for the service principal</span></span>

<span data-ttu-id="87446-109">Puede usar una entidad de servicio de Azure AD existente que cumpla los requisitos siguientes o crear una.</span><span class="sxs-lookup"><span data-stu-id="87446-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="87446-110">**Ámbito**: el grupo de recursos en la suscripción usada para implementar el clúster de Kubernetes o, de manera menos restrictiva, la suscripción usada para implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="87446-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="87446-111">**Rol**: **colaborador**</span><span class="sxs-lookup"><span data-stu-id="87446-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="87446-112">**Secreto de cliente**: debe ser una contraseña.</span><span class="sxs-lookup"><span data-stu-id="87446-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="87446-113">Actualmente, no se puede usar a una entidad de servicio configurado para la autenticación de certificados.</span><span class="sxs-lookup"><span data-stu-id="87446-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="87446-114">Para crear una entidad de servicio, debe tener permisos suficientes para registrar una aplicación en su inquilino de Azure AD y asignar la aplicación a un rol en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="87446-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="87446-115">Para ver si tiene los permisos necesarios, [compruébelo en el portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="87446-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="87446-116">Opción 1: Creación de una entidad de servicio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="87446-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="87446-117">Si desea crear una entidad de servicio de Azure AD antes de implementar el clúster de Kubernetes, Azure le proporciona varios métodos.</span><span class="sxs-lookup"><span data-stu-id="87446-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="87446-118">Los siguientes comandos de ejemplo muestran cómo hacerlo con la [ CLI de Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="87446-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="87446-119">Como alternativa, puede crear una entidad de servicio mediante [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), el [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md) u otros métodos.</span><span class="sxs-lookup"><span data-stu-id="87446-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="87446-120">Devuelve una salida similar a la siguiente (que se muestra aquí):</span><span class="sxs-lookup"><span data-stu-id="87446-120">Output is similar to the following (shown here redacted):</span></span>

![Creación de una entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="87446-122">Se han resaltado el **identificador de cliente** (`appId`) y el **secreto de cliente** (`password`) que se usan como parámetros de la entidad de servicio para la implementación del clúster.</span><span class="sxs-lookup"><span data-stu-id="87446-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="87446-123">Especificación de la entidad de servicio al crear el clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="87446-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="87446-124">Especifique el **identificador de cliente** (a menudo denominado `appId`, para el identificador de aplicación) y el **secreto de cliente** (`password`) de una entidad de servicio existente como parámetros al crear el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="87446-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="87446-125">Asegúrese de que la entidad de servicio cumpla los requisitos al principio de este artículo.</span><span class="sxs-lookup"><span data-stu-id="87446-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="87446-126">Estos parámetros se pueden especificar al implementar el clúster de Kubernetes desde la [interfaz de la línea de comandos (CLI) de Azure 2.0](container-service-kubernetes-walkthrough.md), [Azure Portal](../dcos-swarm/container-service-deployment.md) u otros métodos.</span><span class="sxs-lookup"><span data-stu-id="87446-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="87446-127">Al especificar el **identificador de cliente**, asegúrese de utilizar `appId`, no `ObjectId`, de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="87446-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="87446-128">En el ejemplo siguiente se muestra una forma de pasar los parámetros con la CLI de Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="87446-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="87446-129">En este ejemplo se utiliza la [plantilla de inicio rápido de Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="87446-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="87446-130">[Descargue](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) el archivo de parámetros de plantilla `azuredeploy.parameters.json` de GitHub.</span><span class="sxs-lookup"><span data-stu-id="87446-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="87446-131">Para especificar la entidad de servicio, especifique los valores de `servicePrincipalClientId` y `servicePrincipalClientSecret` en el archivo.</span><span class="sxs-lookup"><span data-stu-id="87446-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="87446-132">(También tendrá que especificar sus propios valores para `dnsNamePrefix` y `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="87446-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="87446-133">El segundo es la clave pública de SSH para acceder al clúster.) Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="87446-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Pasar los parámetros de la entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="87446-135">Ejecute el siguiente comando y use `--parameters` para establecer la ruta de acceso al archivo azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="87446-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="87446-136">Este comando implementa el clúster en un grupo de recursos que se crea llamado `myResourceGroup` en la región oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="87446-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="87446-137">Opción 2: Generación de una entidad de servicio al crear el clúster con `az acs create`</span><span class="sxs-lookup"><span data-stu-id="87446-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="87446-138">Si ejecuta el comando [`az acs create`](/cli/azure/acs#create) para crear el clúster de Kubernetes, tiene la opción para generar automáticamente una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="87446-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="87446-139">Al igual que sucede con otras opciones de creación de clústeres de Kubernetes, al ejecutar `az acs create` se pueden especificar los parámetros de una entidad de servicio existente.</span><span class="sxs-lookup"><span data-stu-id="87446-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="87446-140">Sin embargo, cuando se omiten estos parámetros, la CLI de Azure crea una automáticamente para usarla con Container Service.</span><span class="sxs-lookup"><span data-stu-id="87446-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="87446-141">Esta operación se realiza de forma transparente durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="87446-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="87446-142">El siguiente comando crea un clúster de Kubernetes y genera tanto las claves de SSH como las credenciales de la entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="87446-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="87446-143">Si su cuenta no tiene los permisos de Azure AD y de suscripción para crear una entidad de servicio, el comando genera un error similar a `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="87446-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="87446-144">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="87446-144">Additional considerations</span></span>

* <span data-ttu-id="87446-145">Si no tiene permisos para crear una entidad de servicio en su suscripción, deberá solicitar al administrador de Azure AD o de su suscripción que se los asigne o pedirle una entidad de servicio que pueda usar con Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="87446-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="87446-146">La entidad de servicio para Kubernetes forma parte de la configuración del clúster.</span><span class="sxs-lookup"><span data-stu-id="87446-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="87446-147">Sin embargo, no use la identidad para implementar el clúster.</span><span class="sxs-lookup"><span data-stu-id="87446-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="87446-148">Cada entidad de servicio está asociada a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87446-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="87446-149">La entidad de servicio de un clúster de Kubernetes puede asociarse con cualquier nombre de aplicación de Azure AD válido (por ejemplo, `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="87446-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="87446-150">La dirección URL de la aplicación no tiene por qué ser un punto de conexión real.</span><span class="sxs-lookup"><span data-stu-id="87446-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="87446-151">Si especifica el valor **Id. de cliente** para la entidad de servicio, puede usar el valor de `appId` (como se muestra en este artículo) o la entidad de servicio correspondiente `name` (por ejemplo, `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="87446-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="87446-152">En las máquinas virtuales principal y del agente en el clúster de Kubernetes, las credenciales de la entidad de servicio se almacenan en el archivo /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="87446-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="87446-153">Cuando use el comando `az acs create` para generar la entidad de servicio automáticamente, sus credenciales se escriben en el archivo ~/.azure/acsServicePrincipal.json de la máquina que se usa para ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="87446-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="87446-154">Cuando use el comando `az acs create` para generar automáticamente la entidad de servicio, esta también se puede autenticar con una [instancia de Azure Container Registry](../../container-registry/container-registry-intro.md) creada en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="87446-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="87446-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87446-155">Next steps</span></span>

* <span data-ttu-id="87446-156">[Introducción a Kubernetes](container-service-kubernetes-walkthrough.md) en el clúster de Container Service.</span><span class="sxs-lookup"><span data-stu-id="87446-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="87446-157">Para solucionar problemas de la entidad de servicio para Kubernetes, consulte la [documentación del motor de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="87446-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


