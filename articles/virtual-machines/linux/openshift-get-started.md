---
title: aaaDeploy origen OpenShift tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de las máquinas virtuales tooAzure toodeploy OpenShift origen."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="56286-103">Implementar OpenShift origen tooAzure máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="56286-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="56286-104">[OpenShift Origin](https://www.openshift.org/) es una plataforma de contenedor de código abierto basada en [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="56286-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="56286-105">Simplifica el proceso de Hola de implementar, ajuste de escala y utilizar aplicaciones de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="56286-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="56286-106">Esta guía describe cómo toodeploy OpenShift origen sobre el uso de máquinas virtuales de Azure Hola CLI de Azure y las plantillas de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="56286-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="56286-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56286-108">Crear un toomanage KeyVault claves SSH para clúster de OpenShift Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="56286-109">Implementar un clúster de OpenShift en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="56286-110">Instalar y configurar hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) clúster de hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="56286-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="56286-111">Personalizar la implementación de OpenShift Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="56286-112">Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="56286-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="56286-113">Este inicio rápido requiere hello Azure CLI versión 2.0.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="56286-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="56286-114">versión de hello toofind, ejecute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="56286-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="56286-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="56286-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="56286-116">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="56286-116">Log in tooAzure</span></span> 
<span data-ttu-id="56286-117">Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones o haga clic en **Pruébelo** toouse Shell en la nube.</span><span class="sxs-lookup"><span data-stu-id="56286-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="56286-118">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="56286-118">Create a resource group</span></span>

<span data-ttu-id="56286-119">Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="56286-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="56286-120">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="56286-121">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="56286-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="56286-122">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="56286-122">Create a Key Vault</span></span>
<span data-ttu-id="56286-123">Crear un Hola de toostore KeyVault claves SSH para clúster Hola con hello [crear az keyvault](/cli/azure/keyvault#create) comando.</span><span class="sxs-lookup"><span data-stu-id="56286-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="56286-124">Creación de una clave SSH</span><span class="sxs-lookup"><span data-stu-id="56286-124">Create an SSH key</span></span> 
<span data-ttu-id="56286-125">Una clave SSH es necesario toosecure acceso toohello clúster OpenShift origen.</span><span class="sxs-lookup"><span data-stu-id="56286-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="56286-126">Crear un par de claves SSH con hello `ssh-keygen` comando.</span><span class="sxs-lookup"><span data-stu-id="56286-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="56286-127">Hola par de claves SSH que cree no debe tener una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="56286-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="56286-128">Para obtener más información sobre las claves SSH en Windows, [cómo toocreate SSH teclas Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="56286-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="56286-129">Almacenamiento de la clave privada de SSH en Key Vault</span><span class="sxs-lookup"><span data-stu-id="56286-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="56286-130">Hola OpenShift implementación utiliza la clave SSH de hello creaste acceso toosecure toohello OpenShift master.</span><span class="sxs-lookup"><span data-stu-id="56286-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="56286-131">tooenable Hola implementación toosecurely recuperar la clave SSH hello, almacenar la clave de hello en el almacén de claves mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="56286-132">Habilitación para la implementación de plantilla</span><span class="sxs-lookup"><span data-stu-id="56286-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="56286-133">Creación de una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="56286-133">Create a service principal</span></span> 
<span data-ttu-id="56286-134">OpenShift se comunica con Azure mediante un nombre de usuario y una contraseña, o a través de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="56286-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="56286-135">Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como OpenShift.</span><span class="sxs-lookup"><span data-stu-id="56286-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="56286-136">Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="56286-137">tooimprove seguridad a través de la que se proporcionen un nombre de usuario y una contraseña, este ejemplo crea un servicio básico principal.</span><span class="sxs-lookup"><span data-stu-id="56286-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="56286-138">Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita OpenShift:</span><span class="sxs-lookup"><span data-stu-id="56286-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="56286-139">Tome nota de la propiedad de appId Hola devuelta por el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-139">Take note of hello appId property returned from hello command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="56286-140">No cree una contraseña que no sea segura.</span><span class="sxs-lookup"><span data-stu-id="56286-140">Don't create an insecure password.</span></span>  <span data-ttu-id="56286-141">Siga la guía de las [restricciones y reglas de contraseña de Azure AD](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="56286-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="56286-142">Para más información, sobre las entidades de servicio, consulte [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="56286-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="56286-143">Implementar la plantilla de origen de OpenShift Hola</span><span class="sxs-lookup"><span data-stu-id="56286-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="56286-144">A continuación implemente OpenShift Origin mediante una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="56286-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="56286-145">el comando siguiente Hello requiere az CLI 2.0.8 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="56286-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="56286-146">Puede comprobar Hola az CLI versión con hello `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="56286-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="56286-147">Hola tooupdate versión CLI, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="56286-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="56286-148">Hola de uso `appId` valor de entidad de seguridad de servicio de Hola que creó anteriormente para hello `aadClientId` parámetro.</span><span class="sxs-lookup"><span data-stu-id="56286-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="56286-149">implementación de Hello puede tardar too20 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="56286-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="56286-150">Hello dirección URL de la consola de OpenShift de Hola y el nombre DNS de hello OpenShift maestro está imprime toohello terminal cuando se completa la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="56286-151">Conectar toohello OpenShift clúster</span><span class="sxs-lookup"><span data-stu-id="56286-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="56286-152">Cuando se haya completado la implementación de hello, conectar la consola de OpenShift toohello mediante explorador hello mediante hello `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="56286-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="56286-153">O bien, puede conectarse a toohello OpenShift maestra mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="56286-154">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="56286-154">Clean up resources</span></span>
<span data-ttu-id="56286-155">Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, OpenShift clúster y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="56286-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="56286-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56286-156">Next steps</span></span>

<span data-ttu-id="56286-157">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="56286-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="56286-158">Crear un toomanage KeyVault claves SSH para clúster de OpenShift Hola.</span><span class="sxs-lookup"><span data-stu-id="56286-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="56286-159">Implementar un clúster de OpenShift en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="56286-160">Instalar y configurar hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) clúster de hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="56286-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="56286-161">Ahora el clúster de OpenShift Origin está implementado.</span><span class="sxs-lookup"><span data-stu-id="56286-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="56286-162">Puede seguir OpenShift tutoriales toolearn cómo toodeploy su primera aplicación y utilice Hola OpenShift herramientas.</span><span class="sxs-lookup"><span data-stu-id="56286-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="56286-163">Vea [introducción con el origen de OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="56286-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
