---
title: "Clúster de HPC Pack 2016 en Azure | Microsoft Docs"
description: "Aprenda a implementar un clúster de HPC Pack 2016 en Azure."
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
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="2dadf-103">Implementación de un clúster de HPC Pack 2016 en Azure</span><span class="sxs-lookup"><span data-stu-id="2dadf-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="2dadf-104">Siga los pasos de este artículo para implementar un clúster de [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="2dadf-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="2dadf-105">HPC Pack es la solución HPC gratuita de Microsoft que se basa en las tecnologías de Microsoft Azure y Windows Server, y admite cargas de trabajo HPC.</span><span class="sxs-lookup"><span data-stu-id="2dadf-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="2dadf-106">Use una de las [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) para implementar el clúster de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="2dadf-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="2dadf-107">Existen varias opciones de topología de clúster con distintos números de nodos principales, y con nodos de proceso Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="2dadf-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dadf-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2dadf-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="2dadf-109">Certificado PFX</span><span class="sxs-lookup"><span data-stu-id="2dadf-109">PFX certificate</span></span>

<span data-ttu-id="2dadf-110">Un clúster de Microsoft HPC Pack 2016 requiere un certificado de intercambio de información Personal (PFX) para proteger la comunicación entre los nodos HPC.</span><span class="sxs-lookup"><span data-stu-id="2dadf-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="2dadf-111">El certificado debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="2dadf-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="2dadf-112">Debe tener una clave privada con funcionalidad de intercambio de claves.</span><span class="sxs-lookup"><span data-stu-id="2dadf-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="2dadf-113">El uso de la clave incluye firma digital y cifrado de claves.</span><span class="sxs-lookup"><span data-stu-id="2dadf-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="2dadf-114">La clave mejorada incluye autenticación de cliente y autenticación de servidor.</span><span class="sxs-lookup"><span data-stu-id="2dadf-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="2dadf-115">Si aún no cuenta con un certificado que cumpla estos requisitos, puede solicitarlo a una entidad de certificación.</span><span class="sxs-lookup"><span data-stu-id="2dadf-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="2dadf-116">Como alternativa, puede usar los siguientes comandos para generar el certificado autofirmado, en función del sistema operativo en el que se ejecute el comando, y exportar el certificado con formato PFX con una clave privada.</span><span class="sxs-lookup"><span data-stu-id="2dadf-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="2dadf-117">**Para Windows 10 o Windows Server 2016**, ejecute el cmdlet de PowerShell integrado **New-SelfSignedCertificate** como sigue:</span><span class="sxs-lookup"><span data-stu-id="2dadf-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="2dadf-118">**En el caso de sistemas operativos previos a Windows 10 o Windows Server 2016**, descargue el [generador de certificados autofirmados](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) del Centro de scripts de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2dadf-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="2dadf-119">Extraiga su contenido y ejecute los siguientes comandos en un símbolo del sistema de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2dadf-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="2dadf-120">Carga del certificado en una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="2dadf-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="2dadf-121">Antes de implementar el clúster HPC, cargue el certificado en un [almacén de claves de Azure](../../key-vault/index.md) como un secreto y registre la siguiente información para usarla durante la implementación: **nombre del almacén**, **grupo de recursos del almacén**, **dirección URL de certificado** y **huella digital del certificado**.</span><span class="sxs-lookup"><span data-stu-id="2dadf-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="2dadf-122">A continuación se muestra un ejemplo de un script de PowerShell para cargar el certificado.</span><span class="sxs-lookup"><span data-stu-id="2dadf-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="2dadf-123">Para más información sobre cómo cargar un certificado en un almacén de claves de Azure, consulte [Introducción a Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2dadf-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
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
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="2dadf-124">Topologías admitidas</span><span class="sxs-lookup"><span data-stu-id="2dadf-124">Supported topologies</span></span>

<span data-ttu-id="2dadf-125">Elija una de las [plantillas de Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) para implementar el clúster de HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="2dadf-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="2dadf-126">Las siguientes son arquitecturas de alto nivel de tres topologçias de clúster admitidas.</span><span class="sxs-lookup"><span data-stu-id="2dadf-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="2dadf-127">Las topologías de alta disponibilidad incluyen varios nodos principales de clúster.</span><span class="sxs-lookup"><span data-stu-id="2dadf-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="2dadf-128">Clúster de alta disponibilidad con dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dadf-128">High-availability cluster with Active Directory domain</span></span>

    ![Clúster de alta disponibilidad en dominio de AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="2dadf-130">Clúster de alta disponibilidad sin dominio de Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dadf-130">High-availability cluster without Active Directory domain</span></span>

    ![Clúster de alta disponibilidad sin dominio de AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="2dadf-132">Clúster con un único nodo principal</span><span class="sxs-lookup"><span data-stu-id="2dadf-132">Cluster with a single head node</span></span>

   ![Clúster con un único nodo principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="2dadf-134">Implementación de un clúster</span><span class="sxs-lookup"><span data-stu-id="2dadf-134">Deploy a cluster</span></span>

<span data-ttu-id="2dadf-135">Para crear el clúster, elija una plantilla y haga clic en **Implementar en Azure**.</span><span class="sxs-lookup"><span data-stu-id="2dadf-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="2dadf-136">En el [portal de Azure](https://portal.azure.com), especifique para la plantilla los parámetros que se describen en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="2dadf-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="2dadf-137">Cada plantilla crea todos los recursos de Azure necesarios para la infraestructura de clúster HPC.</span><span class="sxs-lookup"><span data-stu-id="2dadf-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="2dadf-138">Los recursos incluyen una red virtual de Azure, una dirección IP pública, un equilibrador de carga (solo para un clúster de alta disponibilidad), interfaces de red, conjuntos de disponibilidad, cuentas de almacenamiento y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2dadf-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="2dadf-139">Paso 1: Selección de la suscripción, la ubicación y el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2dadf-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="2dadf-140">La **suscripción** y la **ubicación** deben ser las mismas que ha especificado al cargar el certificado PFX (consulte los requisitos previos).</span><span class="sxs-lookup"><span data-stu-id="2dadf-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="2dadf-141">Le recomendamos que cree un **grupo de recursos** para la implementación.</span><span class="sxs-lookup"><span data-stu-id="2dadf-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="2dadf-142">Paso 2: Especificación de la configuración de parámetros</span><span class="sxs-lookup"><span data-stu-id="2dadf-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="2dadf-143">Escriba o modifique los valores de los parámetros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="2dadf-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="2dadf-144">Haga clic en el icono junto a cada parámetro para obtener información de ayuda.</span><span class="sxs-lookup"><span data-stu-id="2dadf-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="2dadf-145">Consulte también la guía sobre [tamaños de máquina virtual disponibles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2dadf-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="2dadf-146">Especifique los valores que registró en los requisitos previos para los siguientes parámetros: **Nombre de almacén**, **Vault resource group** (Grupo de recursos de almacén), **Dirección URL del certificado**, y **Huella digital del certificado**.</span><span class="sxs-lookup"><span data-stu-id="2dadf-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="2dadf-147">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="2dadf-147">Step 3.</span></span> <span data-ttu-id="2dadf-148">Revisión de los términos legales y creación</span><span class="sxs-lookup"><span data-stu-id="2dadf-148">Review legal terms and create</span></span>
<span data-ttu-id="2dadf-149">Haga clic en **Revisar los términos legales** para revisar los términos.</span><span class="sxs-lookup"><span data-stu-id="2dadf-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="2dadf-150">Si los acepta, haga clic en **Comprar** y luego en **Crear** para iniciar la implementación.</span><span class="sxs-lookup"><span data-stu-id="2dadf-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="2dadf-151">Conexión al clúster</span><span class="sxs-lookup"><span data-stu-id="2dadf-151">Connect to the cluster</span></span>
1. <span data-ttu-id="2dadf-152">Después de implementar el clúster de HPC Pack, vaya al [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2dadf-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2dadf-153">Haga clic en **Grupos de recursos** y busque el grupo de recursos en el que se implementó el clúster.</span><span class="sxs-lookup"><span data-stu-id="2dadf-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="2dadf-154">Puede encontrar las máquinas virtuales de nodo principal.</span><span class="sxs-lookup"><span data-stu-id="2dadf-154">You can find the head node virtual machines.</span></span>

    ![Nodos principales del clúster en el portal](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="2dadf-156">Haga clic en un nodo principal (en un clúster de alta disponibilidad, haga clic en cualquiera de los nodos principales).</span><span class="sxs-lookup"><span data-stu-id="2dadf-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="2dadf-157">En **Essentials** (Información básica), puede encontrar la dirección IP pública o el nombre DNS completo del clúster.</span><span class="sxs-lookup"><span data-stu-id="2dadf-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Configuración de la conexión del clúster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="2dadf-159">Haga clic en **Conectar** para iniciar sesión en cualquiera de los nodos principales con el nombre de usuario de administrador especificado mediante Escritorio remoto .</span><span class="sxs-lookup"><span data-stu-id="2dadf-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="2dadf-160">Si el clúster implementado está en un dominio de Active Directory, el nombre de usuario tiene el formato <privateDomainName>\<adminUsername > (por ejemplo, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="2dadf-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dadf-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2dadf-161">Next steps</span></span>
* <span data-ttu-id="2dadf-162">Envíe los trabajos al clúster.</span><span class="sxs-lookup"><span data-stu-id="2dadf-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="2dadf-163">Consulte [Envío de trabajos a un clúster de HPC Pack en Azure](hpcpack-cluster-submit-jobs.md) y [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md) (Administración de un clúster de HPC Pack 2016 en Azure mediante Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="2dadf-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

