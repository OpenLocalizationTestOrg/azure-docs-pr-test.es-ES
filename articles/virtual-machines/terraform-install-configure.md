---
title: "aaaInstall o configurar las máquinas virtuales de Terraform tooprovision y otras infraestructuras de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configurar Terraform toocreate Azure recursos"
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
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="54631-103">Instalar y configurar las máquinas virtuales de Terraform tooprovision y otras infraestructuras en Azure</span><span class="sxs-lookup"><span data-stu-id="54631-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="54631-104">Este artículo describe tooinstall de pasos necesarios de Hola y configure Terraform tooprovision recursos como máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="54631-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="54631-105">Obtendrá información sobre cómo toocreate y use Azure credenciales tooenable Terraform tooprovision recursos en la nube de forma segura.</span><span class="sxs-lookup"><span data-stu-id="54631-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="54631-106">HashiCorp Terraform proporciona una manera sencilla de toodefine e implementar la infraestructura de nube mediante un lenguaje de plantillas personalizadas denominado lenguaje de configuración de HashiCorp (HCL).</span><span class="sxs-lookup"><span data-stu-id="54631-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="54631-107">Este lenguaje personalizado es [toowrite sencillo y fácil toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="54631-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="54631-108">Además, mediante el uso de hello `terraform plan` de comandos, puede visualizar tooyour infraestructura de hello cambios antes de confirmarlos.</span><span class="sxs-lookup"><span data-stu-id="54631-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="54631-109">Siga estos toostart pasos mediante Terraform con Azure.</span><span class="sxs-lookup"><span data-stu-id="54631-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="54631-110">Instalar Terraform</span><span class="sxs-lookup"><span data-stu-id="54631-110">Install Terraform</span></span>
<span data-ttu-id="54631-111">tooinstall Terraform, [descargar](https://www.terraform.io/downloads.html) paquete Hola adecuado para su sistema operativo en un directorio de instalación independiente.</span><span class="sxs-lookup"><span data-stu-id="54631-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="54631-112">descarga de Hello contiene un solo archivo ejecutable para el que también debe definir una ruta de acceso global.</span><span class="sxs-lookup"><span data-stu-id="54631-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="54631-113">Para obtener instrucciones sobre cómo tooset Hola ruta de acceso en Linux y Mac, vaya demasiado[esta página Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="54631-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="54631-114">Para obtener instrucciones sobre cómo tooset Hola ruta de acceso en Windows, vaya demasiado[esta página Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="54631-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="54631-115">tooverify la instalación, ejecute hello `terraform` comando.</span><span class="sxs-lookup"><span data-stu-id="54631-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="54631-116">Debería ver una lista de opciones disponibles de Terraform como salida.</span><span class="sxs-lookup"><span data-stu-id="54631-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="54631-117">A continuación, deberá tooallow Terraform acceso tooyour suscripción de Azure tooperform aprovisionamiento de la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="54631-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="54631-118">Configurar Terraform acceso tooAzure</span><span class="sxs-lookup"><span data-stu-id="54631-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="54631-119">tooenable Terraform tooprovision recursos en Azure, necesita toocreate dos entidades en Azure Active Directory (Azure AD): una aplicación de Azure AD y una entidad de seguridad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54631-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="54631-120">Seguidamente, los identificadores de estas entidades se usan en los scripts de Terraform.</span><span class="sxs-lookup"><span data-stu-id="54631-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="54631-121">La entidad de servicio es una instancia local de una aplicación de Azure AD global.</span><span class="sxs-lookup"><span data-stu-id="54631-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="54631-122">Una entidad de servicio permite recursos de tooglobal de control de acceso local específico.</span><span class="sxs-lookup"><span data-stu-id="54631-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="54631-123">Hay varias toocreate formas una aplicación de Azure AD y una entidad de seguridad de servicio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54631-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="54631-124">Hola más rápido y sencillo cierto hoy en día es toouse 2.0 de CLI de Azure, que [puede descargar e instalar en Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54631-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="54631-125">También puede utilizar la infraestructura de seguridad necesarios de hello toocreate PowerShell o CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="54631-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="54631-126">instrucciones de Hello siguientes muestran cómo tooconfigure Terraform de Azure mediante el uso de todos estos enfoques.</span><span class="sxs-lookup"><span data-stu-id="54631-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="54631-127">Usar la CLI de Azure 2.0 (para usuarios de Windows, Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="54631-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="54631-128">Después de descargar e instalar hello [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), inicie sesión en tooadminister su suscripción de Azure mediante la emisión de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="54631-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="54631-129">Si usas Hola China, Azure en Alemania o nubes de Azure Government, necesita toofirst configurar hello Azure CLI toowork con esa nube.</span><span class="sxs-lookup"><span data-stu-id="54631-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="54631-130">Puede hacerlo ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="54631-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="54631-131">Si tiene varias suscripciones de Azure, se devuelven sus detalles por hello `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="54631-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="54631-132">Conjunto hello `SUBSCRIPTION_ID` devuelve el valor de hello toohold variables de entorno del programa Hola a `id` campo de la suscripción de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="54631-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="54631-133">Establecer la suscripción de Hola que quiere toouse de esta sesión.</span><span class="sxs-lookup"><span data-stu-id="54631-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="54631-134">Id. de suscripción de hello cuenta tooget Hola de consulta y valores de Id. de inquilino.</span><span class="sxs-lookup"><span data-stu-id="54631-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="54631-135">A continuación, cree credenciales separadas para Terraform.</span><span class="sxs-lookup"><span data-stu-id="54631-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="54631-136">Se devuelven el valor de appId, password, sp_name y tenant.</span><span class="sxs-lookup"><span data-stu-id="54631-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="54631-137">Tome nota de appId de hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="54631-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="54631-138">tooconfirm sus credenciales (entidad de servicio), abra un nuevo shell y ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="54631-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="54631-139">Hola de sustitución devuelve valores para sp_name, la contraseña y el inquilino:</span><span class="sxs-lookup"><span data-stu-id="54631-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="54631-140">Usar PowerShell (para usuarios de Windows)</span><span class="sxs-lookup"><span data-stu-id="54631-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="54631-141">toouse Windows toowrite del equipo y ejecutar su Terraform secuencias de comandos y toouse PowerShell para tareas de configuración, configurar la máquina con herramientas de PowerShell de hello adecuadas.</span><span class="sxs-lookup"><span data-stu-id="54631-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="54631-142">Instalar herramientas de PowerShell siguiendo los pasos de hello en [instalar y configurar Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="54631-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="54631-143">Descargar y ejecutar hello [secuencia de comandos de azure setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) desde la consola de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="54631-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="54631-144">secuencia de comandos toorun hello setup.ps1 de azure, descargarla y ejecutar hello `./azure-setup.ps1 setup` comando desde la consola de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="54631-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="54631-145">A continuación, inicie sesión en tooyour suscripción de Azure con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="54631-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="54631-146">Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="54631-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="54631-147">Opcionalmente, proporcione una contraseña segura cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="54631-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="54631-148">Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.</span><span class="sxs-lookup"><span data-stu-id="54631-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="54631-149">Usar la CLI de Azure 1.0 (para usuarios de Linux o Mac)</span><span class="sxs-lookup"><span data-stu-id="54631-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="54631-150">tooget iniciados con Terraform en máquinas de Linux o Mac con 1.0 de CLI de Azure, instale Hola bibliotecas adecuadas en su equipo.</span><span class="sxs-lookup"><span data-stu-id="54631-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="54631-151">Instalar las herramientas CLI de Azure xPlat siguiendo los pasos de hello en [instalar Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54631-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="54631-152">Descargar e instalar un procesador JSON siguiendo las instrucciones de hello en [descargar jq](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="54631-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="54631-153">Descargar y ejecutar hello [secuencia de comandos de azure setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script desde la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="54631-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="54631-154">secuencia de comandos toorun hello setup.sh de azure, descargarla y ejecutar hello `./azure-setup setup` comando desde la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="54631-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="54631-155">A continuación, inicie sesión en tooyour suscripción de Azure con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="54631-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="54631-156">Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="54631-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="54631-157">Opcionalmente, proporcione una contraseña segura cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="54631-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="54631-158">Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.</span><span class="sxs-lookup"><span data-stu-id="54631-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="54631-159">Todos los scripts anteriores Hola crean una aplicación de Azure AD y el servicio principal.</span><span class="sxs-lookup"><span data-stu-id="54631-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="54631-160">Hola service principal obtiene un colaborador o acceso de nivel de propietario de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="54631-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="54631-161">Debido a Hola alto nivel de acceso concedido, siempre debería proteger la información de seguridad de hello generado por los scripts.</span><span class="sxs-lookup"><span data-stu-id="54631-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="54631-162">Anote los cuatro elementos de información de seguridad que proporcionan los scripts: appId, password, subscription_id y tenant_id.</span><span class="sxs-lookup"><span data-stu-id="54631-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="54631-163">Establecimiento de variables de entorno</span><span class="sxs-lookup"><span data-stu-id="54631-163">Set environment variables</span></span>
<span data-ttu-id="54631-164">Después de crear y configurar una entidad de seguridad de servicio de Azure AD, necesita toolet Terraform saber Id. de inquilino de hello, Id. de suscripción, Id. de cliente y toouse secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="54631-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="54631-165">Para ello, inserte esos valores en los scripts de Terraform, tal y como se describe en [Creación de una infraestructura básica de Azure mediante Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="54631-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="54631-166">Como alternativa, puede establecer Hola después de las variables de entorno (y, por tanto, evitar accidentalmente proteger o compartir sus credenciales):</span><span class="sxs-lookup"><span data-stu-id="54631-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="54631-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="54631-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="54631-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="54631-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="54631-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="54631-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="54631-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="54631-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="54631-171">Puede usar este tooset de secuencia de comandos de shell de ejemplo esas variables:</span><span class="sxs-lookup"><span data-stu-id="54631-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="54631-172">Además, si utiliza Terraform con Azure en China, o bien administración pública de Azure o Azure en Alemania, deberá variable de entorno tooset Hola adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="54631-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54631-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54631-173">Next steps</span></span>
<span data-ttu-id="54631-174">Ya ha instalado Terraform y configurado las credenciales de Azure para poder iniciar la implementación de la infraestructura en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="54631-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="54631-175">A continuación, obtenga información acerca de cómo demasiado[crear infraestructura con Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="54631-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>
