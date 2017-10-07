---
title: aaaConnect tooAzure pila con CLI | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola toomanage multiplataforma interfaz de línea de comandos (CLI) e implementar recursos en la pila de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: sngun
ms.openlocfilehash: ffb1ffd2b7784e188487bef98fe5b2add8e96784
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a><span data-ttu-id="47351-103">Instalar y configurar la CLI para su uso con Azure Stack</span><span class="sxs-lookup"><span data-stu-id="47351-103">Install and configure CLI for use with Azure Stack</span></span>

<span data-ttu-id="47351-104">En este documento, se dirigirá en proceso de Hola de uso de recursos de interfaz de línea de comandos (CLI) de Azure toomanage Kit de desarrollo de pila de Azure entre plataformas de cliente de Linux y Mac.</span><span class="sxs-lookup"><span data-stu-id="47351-104">In this document, we guide you through hello process of using Azure Command-line Interface (CLI) toomanage Azure Stack Development Kit resources from Linux and Mac client platforms.</span></span> 

## <a name="export-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="47351-105">Exportar el certificado de raíz de hello entidad emisora de certificados de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="47351-105">Export hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="47351-106">Si está usando CLI desde una máquina virtual que se está ejecutando en el entorno del Kit de desarrollo de Azure pila hello, certificado de raíz de hello Azure pila ya está instalado dentro de la máquina virtual de Hola para que pueda recuperar directamente.</span><span class="sxs-lookup"><span data-stu-id="47351-106">If you are using CLI from a virtual machine that is running within hello Azure Stack Development Kit environment, hello Azure Stack root certificate is already installed within hello virtual machine so you can directly retrieve.</span></span> <span data-ttu-id="47351-107">Mientras que si se usa la CLI desde una estación de trabajo fuera de kit de desarrollo de hello, debe exportar el certificado de raíz de hello entidad emisora de certificados de la pila de Azure del kit de desarrollo de Hola y agregarlo toohello Python almacén de la estación de trabajo de desarrollo (externo Linux o Mac plataforma de certificados ).</span><span class="sxs-lookup"><span data-stu-id="47351-107">Whereas if you are use CLI from a workstation outside hello development kit, you must export hello Azure Stack CA root certificate from hello development kit and add it toohello Python certificate store of your development workstation(external Linux or Mac platform).</span></span> 

<span data-ttu-id="47351-108">Inicie sesión en el kit de desarrollo de tooyour y ejecute hello sigue la secuencia de comandos tooexport hello Azure pila certificado raíz en formato PEM:</span><span class="sxs-lookup"><span data-stu-id="47351-108">Sign in tooyour development kit and run hello following script tooexport hello Azure Stack root certificate in PEM format:</span></span>

```powershell
   $label = "AzureStackSelfSignedRootCert"
   Write-Host "Getting certificate from hello current user trusted store with subject CN=$label"
   $root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
   if (-not $root)
   {
       Log-Error "Cerficate with subject CN=$label not found"
       return
   }

   Write-Host "Exporting certificate"
   Export-Certificate -Type CERT -FilePath root.cer -Cert $root

   Write-Host "Converting certificate tooPEM format"
   certutil -encode root.cer root.pem
```

## <a name="install-cli"></a><span data-ttu-id="47351-109">Instalar la CLI</span><span class="sxs-lookup"><span data-stu-id="47351-109">Install CLI</span></span>

<span data-ttu-id="47351-110">A continuación debe iniciar sesión en la estación de trabajo de desarrollo de tooyour e instalar la CLI.</span><span class="sxs-lookup"><span data-stu-id="47351-110">Next you should sign in tooyour development workstation and install CLI.</span></span> <span data-ttu-id="47351-111">Pila de Azure requiere la versión de Hola 2.0 de CLI de Azure, que se puede instalar mediante el uso de pasos de hello descritos en hello [instalar Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) artículo.</span><span class="sxs-lookup"><span data-stu-id="47351-111">Azure Stack requires hello 2.0 version of Azure CLI, which you can install by using hello steps described in hello [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) article.</span></span> <span data-ttu-id="47351-112">tooverify si la instalación de hello fue correcta, abra un terminal o una ventana de símbolo del sistema y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47351-112">tooverify if hello installation was successful, open a terminal or a command prompt window and run hello following command:</span></span>

```azurecli
az --version
```

<span data-ttu-id="47351-113">Debería ver la versión de Hola de CLI de Azure y otras bibliotecas dependientes que están instalados en su equipo.</span><span class="sxs-lookup"><span data-stu-id="47351-113">You should see hello version of Azure CLI and other dependent libraries that are installed on your computer.</span></span>

## <a name="trust-hello-azure-stack-ca-root-certificate"></a><span data-ttu-id="47351-114">Confiar en certificado de raíz de hello entidad emisora de certificados de la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="47351-114">Trust hello Azure Stack CA root certificate</span></span>

<span data-ttu-id="47351-115">tootrust Hola certificado de Azure de pila de CA raíz, también debe agregar certificado de python existente toohello.</span><span class="sxs-lookup"><span data-stu-id="47351-115">tootrust hello Azure Stack CA root certificate, you should append it toohello existing python certificate.</span></span> <span data-ttu-id="47351-116">Si está ejecutando CLI desde un equipo de Linux que se crea dentro del entorno de Azure pila hello, siguiente ejecución Hola bash comando:</span><span class="sxs-lookup"><span data-stu-id="47351-116">If you are running CLI from a Linux machine that is created within hello Azure Stack environment, run hello following bash command:</span></span>

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

<span data-ttu-id="47351-117">Si está ejecutando CLI desde un equipo fuera de entorno de Azure Sack hello, primero debe configurar [tooAzure de conectividad VPN pila](azure-stack-connect-azure-stack.md).</span><span class="sxs-lookup"><span data-stu-id="47351-117">If you are running CLI from a machine outside hello Azure Sack environment, you must first set up [VPN connectivity tooAzure Stack](azure-stack-connect-azure-stack.md).</span></span> <span data-ttu-id="47351-118">Ahora copie Hola PEM certificado que exportó anteriormente en la estación de trabajo de desarrollo y ejecute hello siguientes comandos en función del sistema operativo de su desarrollo de estación de trabajo:</span><span class="sxs-lookup"><span data-stu-id="47351-118">Now copy hello PEM certificate that you exported earlier onto your development workstation and run hello following commands depending on your development workstation's OS,:</span></span>

### <a name="linux"></a><span data-ttu-id="47351-119">Linux</span><span class="sxs-lookup"><span data-stu-id="47351-119">Linux</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a><span data-ttu-id="47351-120">macOS</span><span class="sxs-lookup"><span data-stu-id="47351-120">macOS</span></span>

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a><span data-ttu-id="47351-121">Windows</span><span class="sxs-lookup"><span data-stu-id="47351-121">Windows</span></span>

```powershell
$pemFile = "<Fully qualified path toohello PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from hello cert file"
$md5Hash=(Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash=(Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash=(Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry  = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path root.pem -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding hello certificate content tooPython Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing hello azure stack CA root certificate"
```

## <a name="set-up-hello-virtual-machine-aliases-endpoint"></a><span data-ttu-id="47351-122">Establecer el punto de conexión de alias de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="47351-122">Set up hello virtual machine aliases endpoint</span></span>

<span data-ttu-id="47351-123">Antes de que los usuarios pueden crear máquinas virtuales mediante el uso de CLI, Administrador de la nube de hello debe configurar un extremo accesible públicamente que contiene el alias de la imagen de máquina virtual y registre este punto de conexión con la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="47351-123">Before users can create virtual machines by using CLI, hello cloud administrator should set up a publicly accessible endpoint that contains virtual machine image aliases and register this endpoint with hello cloud.</span></span> <span data-ttu-id="47351-124">Hola `endpoint-vm-image-alias-doc` parámetro Hola `az cloud register` comando se usa para este propósito.</span><span class="sxs-lookup"><span data-stu-id="47351-124">hello `endpoint-vm-image-alias-doc` parameter in hello `az cloud register` command is used for this purpose.</span></span> <span data-ttu-id="47351-125">Los administradores de nube deben descargar marketplace de pila de Azure de hello imagen toohello antes de que agregan el punto de conexión de tooimage alias.</span><span class="sxs-lookup"><span data-stu-id="47351-125">Cloud administrators must download hello image toohello Azure Stack marketplace before they add it tooimage aliases endpoint.</span></span>
   
<span data-ttu-id="47351-126">Por ejemplo, el contenido de Azure usa el URI siguiente: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span><span class="sxs-lookup"><span data-stu-id="47351-126">For example, Azure contains uses following URI: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json.</span></span> <span data-ttu-id="47351-127">Hola nube administrador debe configurar un punto de conexión similar para la pila de Azure con imágenes de Hola que están disponibles en el marketplace de Azure pila Hola.</span><span class="sxs-lookup"><span data-stu-id="47351-127">hello cloud administrator should set up a similar endpoint for Azure Stack with hello images that are available in hello Azure Stack marketplace.</span></span>

## <a name="connect-tooazure-stack"></a><span data-ttu-id="47351-128">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="47351-128">Connect tooAzure Stack</span></span>

<span data-ttu-id="47351-129">Usar hello siguiendo los pasos tooconnect tooAzure pila:</span><span class="sxs-lookup"><span data-stu-id="47351-129">Use hello following steps tooconnect tooAzure Stack:</span></span>

1. <span data-ttu-id="47351-130">Registrar su entorno de pila de Azure mediante la ejecución de comando de registro de hello az en la nube.</span><span class="sxs-lookup"><span data-stu-id="47351-130">Register your Azure Stack environment by running hello az cloud register command.</span></span>
   
   <span data-ttu-id="47351-131">a.</span><span class="sxs-lookup"><span data-stu-id="47351-131">a.</span></span> <span data-ttu-id="47351-132">Hola tooregister **nube administrativa** entorno, use:</span><span class="sxs-lookup"><span data-stu-id="47351-132">tooregister hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackAdmin \ 
     --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

   <span data-ttu-id="47351-133">b.</span><span class="sxs-lookup"><span data-stu-id="47351-133">b.</span></span> <span data-ttu-id="47351-134">Hola tooregister **usuario** entorno, use:</span><span class="sxs-lookup"><span data-stu-id="47351-134">tooregister hello **user** environment, use:</span></span>

   ```azurecli
   az cloud register \ 
     -n AzureStackUser \ 
     --endpoint-resource-manager "https://management.local.azurestack.external" \ 
     --suffix-storage-endpoint "local.azurestack.external" \ 
     --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
     --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
     --endpoint-vm-image-alias-doc <URI of hello document which contains virtual machine image aliases>
   ```

2. <span data-ttu-id="47351-135">Establecer entorno activo de hello mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="47351-135">Set hello active environment by using hello following commands:</span></span>

   <span data-ttu-id="47351-136">a.</span><span class="sxs-lookup"><span data-stu-id="47351-136">a.</span></span> <span data-ttu-id="47351-137">Para hello **nube administrativa** entorno, use:</span><span class="sxs-lookup"><span data-stu-id="47351-137">For hello **cloud administrative** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackAdmin
   ```

   <span data-ttu-id="47351-138">b.</span><span class="sxs-lookup"><span data-stu-id="47351-138">b.</span></span> <span data-ttu-id="47351-139">Para hello **usuario** entorno, use:</span><span class="sxs-lookup"><span data-stu-id="47351-139">For hello **user** environment, use:</span></span>

   ```azurecli
   az cloud set \
     -n AzureStackUser
   ```

3. <span data-ttu-id="47351-140">Actualice su hello toouse de configuración de entorno perfil de versión de API específica de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="47351-140">Update your environment configuration toouse hello Azure Stack specific API version profile.</span></span> <span data-ttu-id="47351-141">configuración de hello tooupdate, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="47351-141">tooupdate hello configuration, run hello following command:</span></span>

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. <span data-ttu-id="47351-142">Inicie sesión en el entorno de Azure pila tooyour mediante hello **inicio de sesión de az** comando.</span><span class="sxs-lookup"><span data-stu-id="47351-142">Sign in tooyour Azure Stack environment by using hello **az login** command.</span></span> <span data-ttu-id="47351-143">Puede iniciar sesión en el entorno de Azure pila toohello como un usuario o un [entidad de servicio](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="47351-143">You can sign in toohello Azure Stack environment either as a user or as a [service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects).</span></span> 

   * <span data-ttu-id="47351-144">Inicie sesión como un **usuario**: puede especificar Hola username y password directamente dentro de comando de inicio de sesión de hello az o autenticarse mediante un explorador.</span><span class="sxs-lookup"><span data-stu-id="47351-144">Sign in as a **user**: You can either specify hello username and password directly within hello az login command or authenticate using a browser.</span></span> <span data-ttu-id="47351-145">Deberá toodo Hola último caso, si la cuenta tiene habilitada la autenticación multifactor.</span><span class="sxs-lookup"><span data-stu-id="47351-145">You would have toodo hello latter, if your account has multi-factor authentication enabled.</span></span>

   ```azurecli
   az login \
     -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
   ```

   > [!NOTE]
   > <span data-ttu-id="47351-146">Si su cuenta de usuario tiene la autenticación multifactor habilitada, puede usar el comando de inicio de sesión de hello az sin proporcionar el parámetro de hello -u.</span><span class="sxs-lookup"><span data-stu-id="47351-146">If your user account has Multi factor authentication enabled, you can use hello az login command without providing hello -u parameter.</span></span> <span data-ttu-id="47351-147">Ejecutar comando hello proporciona una dirección URL y un código que debe usar tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="47351-147">Running hello command gives you a URL and a code that you must use tooauthenticate.</span></span>
   
   * <span data-ttu-id="47351-148">Inicie sesión como un **entidad de servicio**: antes de iniciar sesión, [crear una entidad de servicio a través del portal de Azure de hello](azure-stack-create-service-principals.md) o CLI y asigna a una función.</span><span class="sxs-lookup"><span data-stu-id="47351-148">Sign in as a **service principal**: Before you sign in, [Create a service principal through hello Azure portal](azure-stack-create-service-principals.md) or CLI and assign it a role.</span></span> <span data-ttu-id="47351-149">Ahora, inicie sesión con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47351-149">Now, log in by using hello following command:</span></span>

   ```azurecli
   az login \
     --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
     --service-principal \
     -u <Application Id of hello Service Principal> \
     -p <Key generated for hello Service Principal>
   ```

## <a name="test-hello-connectivity"></a><span data-ttu-id="47351-150">Probar la conectividad de Hola</span><span class="sxs-lookup"><span data-stu-id="47351-150">Test hello connectivity</span></span>

<span data-ttu-id="47351-151">Ahora que tenemos todo lo que el programa de instalación, vamos a usar recursos CLI toocreate dentro de la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="47351-151">Now that we've got everything setup, let's use CLI toocreate resources within Azure Stack.</span></span> <span data-ttu-id="47351-152">Por ejemplo, puede crear un grupo de recursos para una aplicación y agregar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47351-152">For example, you can create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="47351-153">Hola use después el comando toocreate un grupo de recursos denominado "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="47351-153">Use hello following command toocreate a resource group named "MyResourceGroup":</span></span>

```azurecli
az group create \
  -n MyResourceGroup -l local
```

<span data-ttu-id="47351-154">Si se crea correctamente el grupo de recursos de hello, Hola anterior comando da como resultado Hola propiedades del recurso de hello recién creado siguientes:</span><span class="sxs-lookup"><span data-stu-id="47351-154">If hello resource group is created successfully, hello previous command outputs hello following properties of hello newly created resource:</span></span>

![resultado de creación del grupo de recursos](media/azure-stack-connect-cli/image1.png)

<span data-ttu-id="47351-156">Hay algunos problemas conocidos al usar CLI 2.0 en Azure pila, toolearn acerca de estos problemas, vea hello [problemas conocidos de Azure pila CLI](azure-stack-troubleshooting.md#cli) tema.</span><span class="sxs-lookup"><span data-stu-id="47351-156">There are some known issues when using CLI 2.0 in Azure Stack, toolearn about these issues, see hello [Known issues in Azure Stack CLI](azure-stack-troubleshooting.md#cli) topic.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="47351-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47351-157">Next steps</span></span>

[<span data-ttu-id="47351-158">Implementación de plantillas con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="47351-158">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="47351-159">Conexión con PowerShell</span><span class="sxs-lookup"><span data-stu-id="47351-159">Connect with PowerShell</span></span>](azure-stack-connect-powershell.md)

[<span data-ttu-id="47351-160">Administración de permisos de usuario</span><span class="sxs-lookup"><span data-stu-id="47351-160">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

