---
title: "entidad de seguridad de aaaService de clúster de Azure Kubernetes | Documentos de Microsoft"
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
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="8d4cf-103">Configuración de una entidad de servicio de Azure AD para un clúster de Kubernetes en Container Service</span><span class="sxs-lookup"><span data-stu-id="8d4cf-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="8d4cf-104">En el servicio de contenedor de Azure, se requiere un clúster de Kubernetes una [entidad de servicio de Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract con las API de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="8d4cf-105">Hello entidad de servicio es necesario toodynamically administran recursos como [rutas definidas por el usuario](../../virtual-network/virtual-networks-udr-overview.md) hello y [equilibrador de carga de Azure de capa 4](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="8d4cf-106">Este artículo muestra diferentes opciones tooset configurar un servicio principal para el clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="8d4cf-107">Por ejemplo, si instalado y configurado hello [CLI de Azure 2.0](/cli/azure/install-az-cli2), puede ejecutar hello [ `az acs create` ](/cli/azure/acs#create) comando toocreate hello Kubernetes hello y clúster de entidad de servicio en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="8d4cf-108">Requisitos para la entidad de servicio de Hola</span><span class="sxs-lookup"><span data-stu-id="8d4cf-108">Requirements for hello service principal</span></span>

<span data-ttu-id="8d4cf-109">Puede usar a una entidad de servicio de Azure AD existente que cumpla Hola según los requisitos, o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="8d4cf-110">**Ámbito**: grupo de recursos de hello en la suscripción de hello usa clúster de toodeploy hello Kubernetes o (menos de manera restrictiva) suscripción Hola clúster de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="8d4cf-111">**Rol**: **colaborador**</span><span class="sxs-lookup"><span data-stu-id="8d4cf-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="8d4cf-112">**Secreto de cliente**: debe ser una contraseña.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="8d4cf-113">Actualmente, no se puede usar a una entidad de servicio configurado para la autenticación de certificados.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8d4cf-114">toocreate una entidad de servicio, debe tener permisos tooregister una aplicación con el inquilino de Azure AD y rol de tooassign Hola aplicación tooa en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="8d4cf-115">toosee si tiene los permisos necesario de hello, [comprobar Hola Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="8d4cf-116">Opción 1: Creación de una entidad de servicio en Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d4cf-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="8d4cf-117">Si desea toocreate una entidad de seguridad de servicio de Azure AD antes de implementar el clúster Kubernetes, Azure proporciona varios métodos.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="8d4cf-118">Hola después de comandos de ejemplo muestra cómo toodo esto con hello [CLI de Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="8d4cf-119">O bien puede crear una entidad de seguridad de servicio mediante [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), u otros métodos.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="8d4cf-120">Salida es similar toohello siguiente (mostrado aquí redactado):</span><span class="sxs-lookup"><span data-stu-id="8d4cf-120">Output is similar toohello following (shown here redacted):</span></span>

![Creación de una entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="8d4cf-122">Resalta son hello **Id. de cliente** (`appId`) hello y **secreto de cliente** (`password`) que se usan como parámetros de entidad de seguridad de servicio para la implementación del clúster.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="8d4cf-123">Especifique la entidad de servicio al crear el clúster de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8d4cf-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="8d4cf-124">Proporcionar hello **Id. de cliente** (también llamado hello `appId`, para el Id. de aplicación) y **secreto de cliente** (`password`) de una entidad como parámetros al crear Hola de servicio existente Clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="8d4cf-125">Asegúrese de entidad de servicio de hello cumple los requisitos de hello en hello partir de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="8d4cf-126">Puede especificar estos parámetros al implementar el clúster de hello Kubernetes con hello [interfaz de línea de comandos (CLI) 2.0 de Azure](container-service-kubernetes-walkthrough.md), [portal de Azure](../dcos-swarm/container-service-deployment.md), u otros métodos.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="8d4cf-127">Al especificar hello **Id. de cliente**, estar seguro de hello toouse `appId`, no Hola `ObjectId`, de entidad de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="8d4cf-128">Hello en el ejemplo siguiente se muestra toopass unidireccional Hola parámetros con hello 2.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8d4cf-129">Este ejemplo utiliza hello [plantilla de inicio rápido de Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="8d4cf-130">[Descargar](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) archivo de parámetros de plantilla de hello `azuredeploy.parameters.json` desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="8d4cf-131">servicio de hello toospecify principal, especifique los valores de `servicePrincipalClientId` y `servicePrincipalClientSecret` en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="8d4cf-132">(También necesita tooprovide sus propios valores para `dnsNamePrefix` y `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="8d4cf-133">Hola este último es clúster Hola de hello SSH tooaccess de clave pública). Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Pasar los parámetros de la entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="8d4cf-135">Hola ejecución siguiente comando, usando `--parameters` tooset Hola ruta toohello azuredeploy.parameters.json al archivo.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="8d4cf-136">Este comando implementa el clúster de hello en un grupo de recursos que se haya creado llamado `myResourceGroup` en la región del oeste de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="8d4cf-137">Opción 2: Generar a una entidad de servicio al crear el clúster de hello con`az acs create`</span><span class="sxs-lookup"><span data-stu-id="8d4cf-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="8d4cf-138">Si ejecuta hello [ `az acs create` ](/cli/azure/acs#create) toocreate comando Hola Kubernetes clúster, tienes Hola opción toogenerate una entidad de servicio automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="8d4cf-139">Al igual que sucede con otras opciones de creación de clústeres de Kubernetes, al ejecutar `az acs create` se pueden especificar los parámetros de una entidad de servicio existente.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="8d4cf-140">Sin embargo, si se omiten estos parámetros, Hola CLI de Azure crea una automáticamente para su uso con el servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="8d4cf-141">Esto tiene lugar de forma transparente durante la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="8d4cf-142">Hello comando siguiente crea un clúster Kubernetes y genera claves de SSH y las credenciales de servicio principal:</span><span class="sxs-lookup"><span data-stu-id="8d4cf-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="8d4cf-143">Si su cuenta no tiene hello Azure AD y toocreate de permisos de suscripción en una entidad de servicio, el comando de hello genera un error similar demasiado`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="8d4cf-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="8d4cf-144">Consideraciones adicionales</span><span class="sxs-lookup"><span data-stu-id="8d4cf-144">Additional considerations</span></span>

* <span data-ttu-id="8d4cf-145">Si no tiene permisos toocreate una entidad de servicio en su suscripción, puede que tenga tooask Azure AD o suscripción administrador tooassign Hola permisos necesarios o pídale una toouse principal de servicio con el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="8d4cf-146">entidad de servicio Hola para Kubernetes es un elemento de configuración del clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="8d4cf-147">Sin embargo, no use clústeres de hello identidad toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="8d4cf-148">Cada entidad de servicio está asociada a una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="8d4cf-149">Hello entidad de servicio para un clúster de Kubernetes puede asociarse con cualquier Azure válida nombre de la aplicación de AD (por ejemplo: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="8d4cf-150">dirección URL de Hello para la aplicación hello no tiene toobe un punto de conexión real.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="8d4cf-151">Cuando especifica la entidad de servicio de hello **Id. de cliente**, se puede utilizar el valor de Hola de hello `appId` (como se muestra en este artículo) o entidad de servicio correspondiente hello `name` (por ejemplo,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="8d4cf-152">En master de Hola y el agente máquinas virtuales en clúster de Kubernetes Hola, credenciales de entidad de seguridad de servicio de Hola se almacenan en hello archivo /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="8d4cf-153">Cuando usas hello `az acs create` comando entidad de servicio de hello toogenerate automáticamente, se escriben las credenciales de entidad de seguridad de servicio de hello toohello archivo ~/.azure/acsServicePrincipal.json en la máquina de hello usa comandos de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="8d4cf-154">Cuando usas hello `az acs create` comando entidad de servicio de hello toogenerate automáticamente, también puede autenticar la entidad de servicio de Hola con un [registro de contenedor de Azure](../../container-registry/container-registry-intro.md) creadas en hello mismo suscripción.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="8d4cf-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8d4cf-155">Next steps</span></span>

* <span data-ttu-id="8d4cf-156">[Introducción a Kubernetes](container-service-kubernetes-walkthrough.md) en el clúster de Container Service.</span><span class="sxs-lookup"><span data-stu-id="8d4cf-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="8d4cf-157">entidad de servicio de tootroubleshoot Hola para Kubernetes, vea hello [documentación del motor de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="8d4cf-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


