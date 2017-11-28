---
title: IIS Seguro con certificados SSL en Azure | Microsoft Docs
description: "Aprenda a proteger el servidor web IIS con certificados SSL en una máquina virtual Windows en Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="dc450-103">Protección de un servidor web IIS con certificados SSL en una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="dc450-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="dc450-104">Para proteger los servidores web, se puede utilizar un certificado Capa de sockets seguros (SSL) para cifrar el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="dc450-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="dc450-105">Estos certificados SSL pueden almacenarse en Azure Key Vault y permiten implementaciones seguras de certificados en máquinas virtuales Windows en Azure.</span><span class="sxs-lookup"><span data-stu-id="dc450-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="dc450-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="dc450-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc450-107">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="dc450-108">Generar o cargar un certificado en Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="dc450-109">Creación de una máquina virtual e instalación del servidor web IIS</span><span class="sxs-lookup"><span data-stu-id="dc450-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="dc450-110">Inserción del certificado en la máquina virtual y configuración de IIS con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="dc450-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="dc450-111">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="dc450-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="dc450-112">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="dc450-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="dc450-113">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="dc450-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="dc450-114">Información general</span><span class="sxs-lookup"><span data-stu-id="dc450-114">Overview</span></span>
<span data-ttu-id="dc450-115">Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="dc450-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="dc450-116">Key Vault ayuda a agilizar el proceso de administración de certificados y le permite mantener el control de las claves que acceden a ellos.</span><span class="sxs-lookup"><span data-stu-id="dc450-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="dc450-117">Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.</span><span class="sxs-lookup"><span data-stu-id="dc450-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="dc450-118">En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="dc450-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="dc450-119">Este proceso garantiza que los certificados más actualizados se instalan en un servidor web durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="dc450-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="dc450-120">Si renueva o reemplaza un certificado, no tiene también que crear una nueva imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="dc450-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="dc450-121">Los certificados más recientes se insertan automáticamente a medida que se crean máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="dc450-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="dc450-122">Durante el proceso completo, el certificado nunca deja la plataforma de Azure ni se expone en un script, historial de la línea de comandos o una plantilla.</span><span class="sxs-lookup"><span data-stu-id="dc450-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="dc450-123">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="dc450-124">Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="dc450-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="dc450-125">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en la ubicación *Este de EE. UU.*:</span><span class="sxs-lookup"><span data-stu-id="dc450-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="dc450-126">Después, cree una instancia de Key Vault con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="dc450-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="dc450-127">Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="dc450-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="dc450-128">Reemplace `<mykeyvault>` en el siguiente ejemplo por su propio nombre único de Key Vault:</span><span class="sxs-lookup"><span data-stu-id="dc450-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="dc450-129">Generación de un certificado y almacenamiento en Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="dc450-130">Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="dc450-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="dc450-131">En este tutorial, el ejemplo siguiente muestra cómo puede generar un certificado autofirmado con [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) que usa la directiva de certificado predeterminada de [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="dc450-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="dc450-132">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dc450-132">Create a virtual machine</span></span>
<span data-ttu-id="dc450-133">Establezca un nombre de usuario de administrador y una contraseña para la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="dc450-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="dc450-134">Ahora puede crear la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="dc450-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="dc450-135">En el ejemplo siguiente se crean los componentes de red virtual necesarios, la configuración del sistema operativo y, después, se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="dc450-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="dc450-136">La máquina virtual tarda unos minutos en crearse.</span><span class="sxs-lookup"><span data-stu-id="dc450-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="dc450-137">El último paso usa la extensión Script personalizado de Azure para instalar el servidor web IIS con [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="dc450-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="dc450-138">Incorporación de un certificado a la máquina virtual desde Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="dc450-139">Para agregar el certificado desde Key Vault a una máquina virtual, obtenga el identificador de su certificado con [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="dc450-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="dc450-140">Agregue el certificado a la máquina virtual con [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="dc450-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="dc450-141">Configuración de IIS para utilizar el certificado</span><span class="sxs-lookup"><span data-stu-id="dc450-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="dc450-142">Use la extensión Script personalizado de nuevo con [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para actualizar la configuración de IIS.</span><span class="sxs-lookup"><span data-stu-id="dc450-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="dc450-143">Esta actualización aplica el certificado insertado desde Key Vault a IIS y configura el enlace web:</span><span class="sxs-lookup"><span data-stu-id="dc450-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="dc450-144">Prueba de la aplicación web segura</span><span class="sxs-lookup"><span data-stu-id="dc450-144">Test the secure web app</span></span>
<span data-ttu-id="dc450-145">Obtenga la dirección IP pública de la máquina virtual con [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="dc450-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="dc450-146">En el ejemplo siguiente se obtiene la dirección IP de `myPublicIP` que se ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="dc450-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="dc450-147">Ahora puede abrir un explorador web y escribir `https://<myPublicIP>` en la barra de direcciones.</span><span class="sxs-lookup"><span data-stu-id="dc450-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="dc450-148">Para aceptar la advertencia de seguridad si usó un certificado autofirmado, seleccione **Detalles** y, a continuación, **Acceder a la página web**:</span><span class="sxs-lookup"><span data-stu-id="dc450-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="dc450-150">El sitio web IIS protegido se muestra ahora como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc450-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Visualización del sitio IIS seguro en funcionamiento](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="dc450-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc450-152">Next steps</span></span>

<span data-ttu-id="dc450-153">En este tutorial, protegió un servidor web IIS con un certificado SSL almacenado en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dc450-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="dc450-154">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="dc450-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dc450-155">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="dc450-156">Generar o cargar un certificado en Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc450-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="dc450-157">Creación de una máquina virtual e instalación del servidor web IIS</span><span class="sxs-lookup"><span data-stu-id="dc450-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="dc450-158">Inserción del certificado en la máquina virtual y configuración de IIS con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="dc450-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="dc450-159">Siga este vínculo para ver ejemplos de scripts de máquina virtual creados previamente.</span><span class="sxs-lookup"><span data-stu-id="dc450-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc450-160">Ejemplos de scripts de máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="dc450-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)