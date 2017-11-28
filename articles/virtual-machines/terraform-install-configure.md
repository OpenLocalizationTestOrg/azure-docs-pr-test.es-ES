---
title: "Instalación y configuración de Terraform para aprovisionar máquinas virtuales y otras infraestructuras en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo instalar y configurar Terraform para crear recursos de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 1f26bccf279ebb61fbf77767186d0435e4f4ba40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-configure-terraform-to-provision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="53cd7-103">Instalación y configuración de Terraform para aprovisionar máquinas virtuales y otras infraestructuras en Azure</span><span class="sxs-lookup"><span data-stu-id="53cd7-103">Install and configure Terraform to provision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="53cd7-104">En este artículo se describen los pasos necesarios para instalar y configurar Terraform para aprovisionar recursos, tales como máquinas virtuales, en Azure.</span><span class="sxs-lookup"><span data-stu-id="53cd7-104">This article describes the necessary steps to install and configure Terraform to provision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="53cd7-105">Obtendrá información sobre cómo crear y usar credenciales de Azure para habilitar Terraform para aprovisionar recursos en la nube de forma segura.</span><span class="sxs-lookup"><span data-stu-id="53cd7-105">You will learn how to create and use Azure credentials to enable Terraform to provision cloud resources in a secure manner.</span></span>

<span data-ttu-id="53cd7-106">HashiCorp Terraform proporciona una manera fácil de definir e implementar infraestructura en la nube mediante un lenguaje de plantillas personalizadas denominado lenguaje de configuración de HashiCorp (HCL).</span><span class="sxs-lookup"><span data-stu-id="53cd7-106">HashiCorp Terraform provides an easy way to define and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="53cd7-107">Este lenguaje personalizado es [fácil de escribir y fácil de entender](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="53cd7-107">This custom language is [easy to write and easy to understand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="53cd7-108">Además, mediante el comando `terraform plan`, puede visualizar los cambios en la infraestructura antes de confirmarlos.</span><span class="sxs-lookup"><span data-stu-id="53cd7-108">Additionally, by using the `terraform plan` command, you can visualize the changes to your infrastructure before you commit them.</span></span> <span data-ttu-id="53cd7-109">Siga estos pasos para empezar a usar Terraform con Azure.</span><span class="sxs-lookup"><span data-stu-id="53cd7-109">Follow these steps to start using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="53cd7-110">Instalar Terraform</span><span class="sxs-lookup"><span data-stu-id="53cd7-110">Install Terraform</span></span>
<span data-ttu-id="53cd7-111">Para instalar Terraform, [descargue](https://www.terraform.io/downloads.html) el paquete apropiado para su sistema operativo en un directorio de instalación independiente.</span><span class="sxs-lookup"><span data-stu-id="53cd7-111">To install Terraform, [download](https://www.terraform.io/downloads.html) the package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="53cd7-112">La descarga contiene un único archivo ejecutable, para el que también debe definir una ruta de acceso global.</span><span class="sxs-lookup"><span data-stu-id="53cd7-112">The download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="53cd7-113">Para obtener instrucciones sobre cómo establecer la ruta de acceso en Linux y Mac, vaya a [esta página web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="53cd7-113">For instructions on how to set the path on Linux and Mac, go to [this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="53cd7-114">Para obtener instrucciones sobre cómo establecer la ruta de acceso en Windows, vaya a [esta página web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="53cd7-114">For instructions on how to set the path on Windows, go to [this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="53cd7-115">Para comprobar la instalación, ejecute el comando `terraform`.</span><span class="sxs-lookup"><span data-stu-id="53cd7-115">To verify your installation, run the `terraform` command.</span></span> <span data-ttu-id="53cd7-116">Debería ver una lista de opciones disponibles de Terraform como salida.</span><span class="sxs-lookup"><span data-stu-id="53cd7-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="53cd7-117">A continuación, debe permitir el acceso de Terraform a su suscripción de Azure para realizar el aprovisionamiento de infraestructuras.</span><span class="sxs-lookup"><span data-stu-id="53cd7-117">Next, you need to allow Terraform access to your Azure subscription to perform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-to-azure"></a><span data-ttu-id="53cd7-118">Configurar el acceso de Terraform a Azure</span><span class="sxs-lookup"><span data-stu-id="53cd7-118">Set up Terraform access to Azure</span></span>
<span data-ttu-id="53cd7-119">Para habilitar Terraform para aprovisionar recursos en Azure, debe crear dos entidades en Azure Active Directory (Azure AD): una aplicación de Azure AD y una entidad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cd7-119">To enable Terraform to provision resources into Azure, you need to create two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="53cd7-120">Seguidamente, los identificadores de estas entidades se usan en los scripts de Terraform.</span><span class="sxs-lookup"><span data-stu-id="53cd7-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="53cd7-121">La entidad de servicio es una instancia local de una aplicación de Azure AD global.</span><span class="sxs-lookup"><span data-stu-id="53cd7-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="53cd7-122">Una entidad de servicio permite el control de acceso local granular a los recursos globales.</span><span class="sxs-lookup"><span data-stu-id="53cd7-122">A service principal allows granular local access control to global resources.</span></span>

<span data-ttu-id="53cd7-123">Hay varias maneras de crear una aplicación de Azure AD y una entidad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cd7-123">There are several ways to create an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="53cd7-124">La forma más sencilla y rápida hoy en día es usar la CLI de Azure 2.0, que [puede descargar e instalar en Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53cd7-124">The easiest and fastest way today is to use Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="53cd7-125">También puede usar PowerShell o la CLI de Azure 1.0 para crear la infraestructura de seguridad necesaria.</span><span class="sxs-lookup"><span data-stu-id="53cd7-125">You also can use PowerShell or Azure CLI 1.0 to create the necessary security infrastructure.</span></span> <span data-ttu-id="53cd7-126">Las instrucciones siguientes muestran cómo configurar Terraform para Azure mediante el uso de todos estos métodos.</span><span class="sxs-lookup"><span data-stu-id="53cd7-126">The instructions that follow show you how to configure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="53cd7-127">Usar la CLI de Azure 2.0 (para usuarios de Windows, Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="53cd7-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="53cd7-128">Después de descargar e instalar la [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), inicie sesión para administrar su suscripción de Azure con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="53cd7-128">After you download and install the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in to administer your Azure subscription by issuing the following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="53cd7-129">Si usa las nubes de China, Alemania o Government, primero debe configurar la CLI de Azure para trabajar con dicha nube.</span><span class="sxs-lookup"><span data-stu-id="53cd7-129">If you use the China, Azure Germany, or Azure Government clouds, you need to first configure the Azure CLI to work with that cloud.</span></span> <span data-ttu-id="53cd7-130">Para ello, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="53cd7-130">You can do this by running the following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="53cd7-131">Si tiene varias suscripciones de Azure, se devuelven sus detalles mediante el comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="53cd7-131">If you have multiple Azure subscriptions, their details are returned by the `az login` command.</span></span> <span data-ttu-id="53cd7-132">Establezca la variable de entorno `SUBSCRIPTION_ID` para almacenar el valor devuelto del campo `id` de la suscripción que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="53cd7-132">Set the `SUBSCRIPTION_ID` environment variable to hold the value of the returned `id` field from the subscription you want to use.</span></span> 

<span data-ttu-id="53cd7-133">Establezca la suscripción que quiere usar para esta sesión.</span><span class="sxs-lookup"><span data-stu-id="53cd7-133">Set the subscription that you want to use for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="53cd7-134">Consulte la cuenta para obtener los valores de los identificadores de suscripción e inquilino.</span><span class="sxs-lookup"><span data-stu-id="53cd7-134">Query the account to get the subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="53cd7-135">A continuación, cree credenciales separadas para Terraform.</span><span class="sxs-lookup"><span data-stu-id="53cd7-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="53cd7-136">Se devuelven el valor de appId, password, sp_name y tenant.</span><span class="sxs-lookup"><span data-stu-id="53cd7-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="53cd7-137">Anote el valor de appId y password.</span><span class="sxs-lookup"><span data-stu-id="53cd7-137">Make a note of the appId and password.</span></span>

<span data-ttu-id="53cd7-138">Para confirmar las credenciales (la entidad de servicio), abra un nuevo shell y ejecute los comandos siguientes.</span><span class="sxs-lookup"><span data-stu-id="53cd7-138">To confirm your credentials (service principal), open a new shell and run the following commands.</span></span> <span data-ttu-id="53cd7-139">Sustituya los valores devueltos de sp_name, password y tenant:</span><span class="sxs-lookup"><span data-stu-id="53cd7-139">Substitute the returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="53cd7-140">Usar PowerShell (para usuarios de Windows)</span><span class="sxs-lookup"><span data-stu-id="53cd7-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="53cd7-141">Para usar un equipo Windows para escribir y ejecutar los scripts de Terraform, y usar PowerShell para las tareas de configuración, configure el equipo con las herramientas adecuadas de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53cd7-141">To use a Windows machine to write and execute your Terraform scripts and to use PowerShell for configuration tasks, configure your machine with the right PowerShell tools.</span></span> 

1. <span data-ttu-id="53cd7-142">Instale las herramientas de PowerShell siguiendo los pasos descritos en [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps) (Instalar y configurar Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="53cd7-142">Install PowerShell tools by following the steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="53cd7-143">Descargue y ejecute el script [azure-setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) desde la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53cd7-143">Download and execute the [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from the PowerShell console.</span></span>

3. <span data-ttu-id="53cd7-144">Para ejecutar el script azure-setup.ps1, descárguelo y ejecute el comando `./azure-setup.ps1 setup` desde la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53cd7-144">To run the azure-setup.ps1 script, download it and execute the `./azure-setup.ps1 setup` command from the PowerShell console.</span></span> <span data-ttu-id="53cd7-145">Después, inicie sesión con su suscripción de Azure con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="53cd7-145">Then sign in to your Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="53cd7-146">Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="53cd7-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="53cd7-147">Opcionalmente, proporcione una contraseña segura cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="53cd7-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="53cd7-148">Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.</span><span class="sxs-lookup"><span data-stu-id="53cd7-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="53cd7-149">Usar la CLI de Azure 1.0 (para usuarios de Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="53cd7-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="53cd7-150">Para empezar a trabajar con Terraform en equipos Linux o Mac con la CLI de Azure 1.0, instale las bibliotecas adecuadas en el equipo.</span><span class="sxs-lookup"><span data-stu-id="53cd7-150">To get started with Terraform on Linux machines or Macs with Azure CLI 1.0, install the proper libraries on your machine.</span></span>  

1. <span data-ttu-id="53cd7-151">Instale las herramientas xPlat de la CLI de Azure siguiendo los pasos descritos en [Instalación de la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53cd7-151">Install Azure xPlat CLI tools by following the steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="53cd7-152">Descargue e instale un procesador JSON siguiendo las instrucciones de [Download jq](https://stedolan.github.io/jq/download/) (Descargar jq).</span><span class="sxs-lookup"><span data-stu-id="53cd7-152">Download and install a JSON processor by following the instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="53cd7-153">Descargue y ejecute el script de Bash [azure-setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) desde la consola.</span><span class="sxs-lookup"><span data-stu-id="53cd7-153">Download and execute the [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from the console.</span></span>

4. <span data-ttu-id="53cd7-154">Para ejecutar el script azure-setup.sh, descárguelo y ejecute el comando `./azure-setup setup` desde la consola.</span><span class="sxs-lookup"><span data-stu-id="53cd7-154">To run the azure-setup.sh script, download it and execute the `./azure-setup setup` command from the console.</span></span> <span data-ttu-id="53cd7-155">Después, inicie sesión con su suscripción de Azure con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="53cd7-155">Then sign in to your Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="53cd7-156">Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="53cd7-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="53cd7-157">Opcionalmente, proporcione una contraseña segura cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="53cd7-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="53cd7-158">Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.</span><span class="sxs-lookup"><span data-stu-id="53cd7-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="53cd7-159">Todos los scripts anteriores crean una aplicación y una entidad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cd7-159">All the previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="53cd7-160">La entidad de servicio obtiene acceso de nivel de colaborador o propietario en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="53cd7-160">The service principal gets a contributor or owner-level access on the subscription.</span></span> <span data-ttu-id="53cd7-161">Debido al nivel alto de acceso concedido, debe proteger siempre la información de seguridad generada por los scripts.</span><span class="sxs-lookup"><span data-stu-id="53cd7-161">Because of the high level of access granted, you should always protect the security information generated by those scripts.</span></span> <span data-ttu-id="53cd7-162">Anote los cuatro elementos de información de seguridad que proporcionan los scripts: appId, password, subscription_id y tenant_id.</span><span class="sxs-lookup"><span data-stu-id="53cd7-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="53cd7-163">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="53cd7-163">Set environment variables</span></span>
<span data-ttu-id="53cd7-164">Después de crear y configurar una entidad de servicio de Azure AD, debe notificar a Terraform el identificador de inquilino, identificador de suscripción, identificador de cliente y secreto de cliente que se van a usar.</span><span class="sxs-lookup"><span data-stu-id="53cd7-164">After you create and configure an Azure AD service principal, you need to let Terraform know the tenant ID, subscription ID, client ID, and client secret to use.</span></span> <span data-ttu-id="53cd7-165">Para ello, inserte esos valores en los scripts de Terraform, tal y como se describe en [Creación de una infraestructura básica de Azure mediante Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="53cd7-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="53cd7-166">Como alternativa, puede establecer las siguientes variables de entorno (y así evitar insertar en el repositorio o compartir las credenciales accidentalmente):</span><span class="sxs-lookup"><span data-stu-id="53cd7-166">Alternately, you can set the following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="53cd7-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="53cd7-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="53cd7-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="53cd7-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="53cd7-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="53cd7-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="53cd7-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="53cd7-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="53cd7-171">Puede usar este script de shell de ejemplo para establecer esas variables:</span><span class="sxs-lookup"><span data-stu-id="53cd7-171">You can use this sample shell script to set those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="53cd7-172">Además, si usa Terraform con Azure Government, Azure Alemania o Azure China, debe establecer la variable de entorno adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="53cd7-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need to set the environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53cd7-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53cd7-173">Next steps</span></span>
<span data-ttu-id="53cd7-174">Ya ha instalado Terraform y configurado las credenciales de Azure para poder iniciar la implementación de la infraestructura en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="53cd7-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="53cd7-175">Ahora, obtenga información acerca de cómo [Crear infraestructura con Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="53cd7-175">Next, learn how to [create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
