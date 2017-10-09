---
title: certificados aaaSecure IIS con SSL en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosecure Hola IIS web server con certificados SSL en una máquina virtual de Windows en Azure"
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
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="8f30c-103">Protección de un servidor web IIS con certificados SSL en una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="8f30c-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="8f30c-104">los servidores web toosecure, que puede ser un certificado Secure Sockets más adelante (SSL) utiliza el tráfico web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="8f30c-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="8f30c-105">Estos certificados SSL pueden almacenarse en el almacén de claves de Azure y permiten implementaciones seguras de certificados tooWindows máquinas virtuales (VMs) en Azure.</span><span class="sxs-lookup"><span data-stu-id="8f30c-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="8f30c-106">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8f30c-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f30c-107">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f30c-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8f30c-108">Generar o cargar un almacén de claves de certificado toohello</span><span class="sxs-lookup"><span data-stu-id="8f30c-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="8f30c-109">Crear una máquina virtual e instale el servidor web de IIS de Hola</span><span class="sxs-lookup"><span data-stu-id="8f30c-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="8f30c-110">Insertar certificado de hello en hello VM y configurar IIS con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="8f30c-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="8f30c-111">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="8f30c-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8f30c-112">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f30c-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="8f30c-113">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8f30c-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="8f30c-114">Información general</span><span class="sxs-lookup"><span data-stu-id="8f30c-114">Overview</span></span>
<span data-ttu-id="8f30c-115">Azure Key Vault protege claves y secretos criptográficos, como certificados y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="8f30c-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="8f30c-116">El almacén de claves ayuda a simplificar el proceso de administración de certificados de Hola y permite toomaintain control de claves que tienen acceso a dichos certificados.</span><span class="sxs-lookup"><span data-stu-id="8f30c-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="8f30c-117">Puede crear un certificado autofirmado en Key Vault o cargar un certificado de confianza existente que ya posea.</span><span class="sxs-lookup"><span data-stu-id="8f30c-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="8f30c-118">En lugar de usar una imagen de máquina virtual personalizada que incluya los certificados preparados, inserta los certificados en una máquina virtual en ejecución.</span><span class="sxs-lookup"><span data-stu-id="8f30c-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="8f30c-119">Este proceso garantiza que los certificados más actualizados de hello están instalados en un servidor web durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="8f30c-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="8f30c-120">Si renovar o reemplazar un certificado, no tendrá también toocreate una nueva imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="8f30c-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="8f30c-121">los certificados más recientes de Hola se insertan automáticamente a medida que cree máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="8f30c-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="8f30c-122">Durante el proceso completo de hello, certificados de hello nunca deje Hola plataforma Windows Azure o se exponen en un script, el historial de la línea de comandos o la plantilla.</span><span class="sxs-lookup"><span data-stu-id="8f30c-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="8f30c-123">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f30c-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="8f30c-124">Para poder crear una instancia de Key Vault y certificados, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8f30c-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8f30c-125">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupSecureWeb* en hello *UU* ubicación:</span><span class="sxs-lookup"><span data-stu-id="8f30c-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="8f30c-126">Después, cree una instancia de Key Vault con [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="8f30c-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="8f30c-127">Cada instancia de Key Vault requiere un nombre único, que debe estar todo en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8f30c-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="8f30c-128">Reemplace `<mykeyvault>` en el siguiente ejemplo con su propio nombre de almacén de claves único de hello:</span><span class="sxs-lookup"><span data-stu-id="8f30c-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="8f30c-129">Generación de un certificado y almacenamiento en Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f30c-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="8f30c-130">Para usarlo en producción, debe importar un certificado válido firmado por un proveedor de confianza con [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="8f30c-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="8f30c-131">Para este tutorial, hello en el ejemplo siguiente se muestra cómo puede generar un certificado autofirmado con [agregar AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) que usa Hola directiva de certificado predeterminada de [ Nueva AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="8f30c-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="8f30c-132">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f30c-132">Create a virtual machine</span></span>
<span data-ttu-id="8f30c-133">Hola a máquina virtual con un nombre de usuario de administrador y una contraseña para el conjunto [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="8f30c-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8f30c-134">Ahora puede crear Hola VM con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8f30c-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="8f30c-135">Hello ejemplo siguiente crea componentes de red virtual Hola necesario, configuración de hello SO y, a continuación, crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="8f30c-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="8f30c-136">Se tarda unos minutos para hello VM toobe creado.</span><span class="sxs-lookup"><span data-stu-id="8f30c-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="8f30c-137">último paso Hello usa Hola extensión de Script personalizado de Azure tooinstall Hola IIS web server con [AzureRmVmExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="8f30c-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="8f30c-138">Agregar un tooVM certificado desde el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="8f30c-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="8f30c-139">certificado de hello tooadd de tooa de almacén de claves de máquina virtual, obtener Id. de hello del certificado con [AzureKeyVaultSecret Get](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="8f30c-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="8f30c-140">Agregar Hola certificado toohello VM con [AzureRmVMSecret agregar](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="8f30c-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="8f30c-141">Configurar IIS toouse Hola certificado</span><span class="sxs-lookup"><span data-stu-id="8f30c-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="8f30c-142">Use Hola extensión de Script personalizado nuevo con [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) configuración de IIS de tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="8f30c-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="8f30c-143">Esta actualización aplica a certificados de hello insertado desde el almacén de claves tooIIS y configura el enlace de hello web:</span><span class="sxs-lookup"><span data-stu-id="8f30c-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

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


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="8f30c-144">Aplicación de prueba hello web segura</span><span class="sxs-lookup"><span data-stu-id="8f30c-144">Test hello secure web app</span></span>
<span data-ttu-id="8f30c-145">Obtener dirección IP pública de saludo de la máquina virtual con [AzureRmPublicIPAddress Get](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="8f30c-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="8f30c-146">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para `myPublicIP` creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8f30c-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="8f30c-147">Ahora puede abrir un explorador web y escriba `https://<myPublicIP>` en la barra de direcciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f30c-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="8f30c-148">Advertencia de seguridad de hello tooaccept si usa un certificado autofirmado, seleccione **detalles** y, a continuación, **ir en la página Web toohello**:</span><span class="sxs-lookup"><span data-stu-id="8f30c-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Aceptar la advertencia de seguridad del explorador web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="8f30c-150">El sitio Web IIS seguro, a continuación, se muestra como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="8f30c-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Visualización del sitio IIS seguro en funcionamiento](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="8f30c-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f30c-152">Next steps</span></span>

<span data-ttu-id="8f30c-153">En este tutorial, protegió un servidor web IIS con un certificado SSL almacenado en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8f30c-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="8f30c-154">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="8f30c-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f30c-155">Crear una instancia de Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="8f30c-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="8f30c-156">Generar o cargar un almacén de claves de certificado toohello</span><span class="sxs-lookup"><span data-stu-id="8f30c-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="8f30c-157">Crear una máquina virtual e instale el servidor web de IIS de Hola</span><span class="sxs-lookup"><span data-stu-id="8f30c-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="8f30c-158">Insertar certificado de hello en hello VM y configurar IIS con un enlace SSL</span><span class="sxs-lookup"><span data-stu-id="8f30c-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="8f30c-159">Siga este toosee vínculo pregeneradas ejemplos de script de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f30c-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f30c-160">Ejemplos de scripts de máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="8f30c-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)