---
title: "aaaHPC 2016 de módulo de clúster en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toodeploy una 2016 de HPC Pack en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="c81b4-103">Implementación de un clúster de HPC Pack 2016 en Azure</span><span class="sxs-lookup"><span data-stu-id="c81b4-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="c81b4-104">Siga los pasos de hello en este artículo toodeploy una [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) clúster en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="c81b4-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="c81b4-105">HPC Pack es la solución HPC gratuita de Microsoft que se basa en las tecnologías de Microsoft Azure y Windows Server, y admite cargas de trabajo HPC.</span><span class="sxs-lookup"><span data-stu-id="c81b4-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="c81b4-106">Utilice uno de hello [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) clúster de HPC Pack 2016 hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c81b4-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c81b4-107">Existen varias opciones de topología de clúster con distintos números de nodos principales, y con nodos de proceso Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="c81b4-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c81b4-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c81b4-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="c81b4-109">Certificado PFX</span><span class="sxs-lookup"><span data-stu-id="c81b4-109">PFX certificate</span></span>

<span data-ttu-id="c81b4-110">Un clúster de Microsoft HPC Pack 2016 requiere una comunicación de intercambio de información Personal (PFX) certificado toosecure Hola entre los nodos HPC de Hola.</span><span class="sxs-lookup"><span data-stu-id="c81b4-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="c81b4-111">certificado de Hello debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="c81b4-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="c81b4-112">Debe tener una clave privada con funcionalidad de intercambio de claves.</span><span class="sxs-lookup"><span data-stu-id="c81b4-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="c81b4-113">El uso de la clave incluye firma digital y cifrado de claves.</span><span class="sxs-lookup"><span data-stu-id="c81b4-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="c81b4-114">La clave mejorada incluye autenticación de cliente y autenticación de servidor.</span><span class="sxs-lookup"><span data-stu-id="c81b4-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="c81b4-115">Si ya no tiene un certificado que cumpla estos requisitos, puede solicitar certificado Hola de una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="c81b4-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="c81b4-116">Como alternativa, puede usar Hola después comandos toogenerate Hola autofirmado basada en certificados en el sistema operativo de hello en el que ejecutar el comando de Hola y exportar el certificado con formato PFX Hola con clave privada.</span><span class="sxs-lookup"><span data-stu-id="c81b4-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="c81b4-117">**Para Windows 10 o Windows Server 2016**, ejecute hello integrado **New-SelfSignedCertificate** cmdlet de PowerShell como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c81b4-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="c81b4-118">**Para sistemas operativos anteriores a Windows 10 o Windows Server 2016**, descargar hello [generador certificado autofirmado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de hello Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="c81b4-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="c81b4-119">Extraer su contenido y ejecute hello siguientes comandos en un símbolo del sistema de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c81b4-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="c81b4-120">Cargar certificado tooan almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="c81b4-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="c81b4-121">Antes de implementar el clúster de HPC de hello, cargar Hola certificado tooan [almacén de claves de Azure](../../key-vault/index.md) como un Hola secreto y registro siguiente información para su uso durante la implementación de hello: **nombre del almacén de**,  **Grupo de recursos de almacén**, **dirección URL de certificado**, y **huella digital del certificado**.</span><span class="sxs-lookup"><span data-stu-id="c81b4-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="c81b4-122">A continuación se muestra un certificado de hello ejemplo tooupload de secuencia de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c81b4-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="c81b4-123">Para obtener más información sobre cómo cargar un tooan certificado del almacén de claves de Azure, consulte [empezar a trabajar con el almacén de claves de Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c81b4-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="c81b4-124">Topologías admitidas</span><span class="sxs-lookup"><span data-stu-id="c81b4-124">Supported topologies</span></span>

<span data-ttu-id="c81b4-125">Elija uno de hello [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) clúster de HPC Pack 2016 hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c81b4-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c81b4-126">Las siguientes son arquitecturas de alto nivel de tres topologçias de clúster admitidas.</span><span class="sxs-lookup"><span data-stu-id="c81b4-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="c81b4-127">Las topologías de alta disponibilidad incluyen varios nodos principales de clúster.</span><span class="sxs-lookup"><span data-stu-id="c81b4-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="c81b4-128">Clúster de alta disponibilidad con dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="c81b4-128">High-availability cluster with Active Directory domain</span></span>

    ![Clúster de alta disponibilidad en dominio de AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="c81b4-130">Clúster de alta disponibilidad sin dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="c81b4-130">High-availability cluster without Active Directory domain</span></span>

    ![Clúster de alta disponibilidad sin dominio de AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="c81b4-132">Clúster con un único nodo principal</span><span class="sxs-lookup"><span data-stu-id="c81b4-132">Cluster with a single head node</span></span>

   ![Clúster con un único nodo principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="c81b4-134">Implementación de un clúster</span><span class="sxs-lookup"><span data-stu-id="c81b4-134">Deploy a cluster</span></span>

<span data-ttu-id="c81b4-135">clúster de hello toocreate, elija una plantilla y haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c81b4-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="c81b4-136">Hola [portal de Azure](https://portal.azure.com), especificar parámetros de plantilla de hello como se describe en hello pasos.</span><span class="sxs-lookup"><span data-stu-id="c81b4-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="c81b4-137">Cada plantilla crea todos los recursos de Azure necesarios para la infraestructura de clúster HPC de Hola.</span><span class="sxs-lookup"><span data-stu-id="c81b4-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="c81b4-138">Los recursos incluyen una red virtual de Azure, una dirección IP pública, un equilibrador de carga (solo para un clúster de alta disponibilidad), interfaces de red, conjuntos de disponibilidad, cuentas de almacenamiento y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c81b4-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="c81b4-139">Paso 1: Seleccione la suscripción de hello, la ubicación y el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c81b4-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="c81b4-140">Hola **suscripción** hello y **ubicación** debe ser la misma que especificó cuando se carga el certificado PFX (consulte los requisitos previos).</span><span class="sxs-lookup"><span data-stu-id="c81b4-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="c81b4-141">Le recomendamos que cree una **grupo de recursos** para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c81b4-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="c81b4-142">Paso 2: Especificar la configuración de parámetros de Hola</span><span class="sxs-lookup"><span data-stu-id="c81b4-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="c81b4-143">Escriba o modifique los valores de parámetros de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="c81b4-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="c81b4-144">Haga clic en el parámetro tooeach hello icono siguiente para obtener información de ayuda.</span><span class="sxs-lookup"><span data-stu-id="c81b4-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="c81b4-145">Consulte también las instrucciones de Hola para [tamaños de máquina virtual disponibles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c81b4-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="c81b4-146">Especificar valores de hello registrados en los requisitos previos de Hola para hello parámetros siguientes: **nombre del almacén de**, **grupo de recursos de almacén**, **dirección URL de certificado**y **Huella digital del certificado**.</span><span class="sxs-lookup"><span data-stu-id="c81b4-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="c81b4-147">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="c81b4-147">Step 3.</span></span> <span data-ttu-id="c81b4-148">Revisión de los términos legales y creación</span><span class="sxs-lookup"><span data-stu-id="c81b4-148">Review legal terms and create</span></span>
<span data-ttu-id="c81b4-149">Haga clic en **revisar los términos legales** términos de hello tooreview.</span><span class="sxs-lookup"><span data-stu-id="c81b4-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="c81b4-150">Si los acepta, haga clic en **compra**y, a continuación, haga clic en **crear** implementación de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="c81b4-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="c81b4-151">Conectar el clúster toohello</span><span class="sxs-lookup"><span data-stu-id="c81b4-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="c81b4-152">Después de implementa el clúster de HPC Pack hello, vaya toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c81b4-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c81b4-153">Haga clic en **grupos de recursos**y encontrar el grupo de recursos hello en qué Hola se implementó el clúster.</span><span class="sxs-lookup"><span data-stu-id="c81b4-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="c81b4-154">Puede encontrar Hola máquinas virtuales de nodo principal.</span><span class="sxs-lookup"><span data-stu-id="c81b4-154">You can find hello head node virtual machines.</span></span>

    ![Nodos principales del clúster en el portal de Hola](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="c81b4-156">Haga clic en un nodo principal (en un clúster de alta disponibilidad, haga clic en cualquiera de los nodos principales de hello).</span><span class="sxs-lookup"><span data-stu-id="c81b4-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="c81b4-157">En **Essentials**, puede encontrar la dirección IP pública Hola o nombre DNS completo del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="c81b4-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Configuración de la conexión del clúster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="c81b4-159">Haga clic en **conectar** toolog en tooany de nodos principales hello mediante Escritorio remoto con el nombre de usuario de administrador especificado.</span><span class="sxs-lookup"><span data-stu-id="c81b4-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="c81b4-160">Si el clúster de Hola implementa está en un dominio de Active Directory, nombre de usuario de hello tiene formato de hello <privateDomainName> \<adminUsername > (por ejemplo, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="c81b4-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c81b4-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c81b4-161">Next steps</span></span>
* <span data-ttu-id="c81b4-162">Enviar clúster tooyour de trabajos.</span><span class="sxs-lookup"><span data-stu-id="c81b4-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="c81b4-163">Vea [enviar trabajos tooHPC un clúster de HPC Pack en Azure](hpcpack-cluster-submit-jobs.md) y [administrar un clúster de HPC Pack 2016 en Azure con Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c81b4-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

