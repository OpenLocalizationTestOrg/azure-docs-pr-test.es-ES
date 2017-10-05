---
title: "Active Directory Domain Services: guía de administración | Microsoft Docs"
description: "Una la máquina virtual de Windows a un dominio administrado con Azure PowerShell y el modelo de implementación clásica."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="be390-103">Unión de una máquina virtual con Windows Server a un dominio administrado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="be390-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be390-104">Portal de Azure clásico - Windows</span><span class="sxs-lookup"><span data-stu-id="be390-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="be390-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="be390-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="be390-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="be390-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="be390-107">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="be390-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="be390-108">Servicios de dominio de Azure AD no admite actualmente el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="be390-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="be390-109">En estos pasos se muestra cómo personalizar un conjunto de comandos de Azure PowerShell que creen y preconfiguren una máquina virtual de Azure basada en Windows mediante el uso de un enfoque de bloque de creación.</span><span class="sxs-lookup"><span data-stu-id="be390-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="be390-110">Estos pasos ayudan a crear una máquina virtual de Azure basada en Windows y unirla a un dominio administrado de Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be390-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="be390-111">En estos pasos se sigue un enfoque consistente en atar cabos para crear conjuntos de comandos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be390-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="be390-112">Este enfoque puede ser útil si es la primera vez que se usa PowerShell o se desea saber qué valores se deben especificar para una configuración correcta.</span><span class="sxs-lookup"><span data-stu-id="be390-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="be390-113">Los usuarios avanzados de PowerShell pueden tomar los comandos y sustituir sus propios valores de las variables (las líneas que comienzan con "$").</span><span class="sxs-lookup"><span data-stu-id="be390-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="be390-114">Si aún no lo ha hecho, siga las instrucciones de [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) para instalar Azure PowerShell en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="be390-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="be390-115">Después, abra el símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be390-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="be390-116">Paso 1: agregar la cuenta</span><span class="sxs-lookup"><span data-stu-id="be390-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="be390-117">En el símbolo del sistema de Powershell, escriba **Add-AzureAccount** y haga clic en **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="be390-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="be390-118">Escriba la dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="be390-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="be390-119">Escriba la contraseña de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="be390-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="be390-120">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="be390-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="be390-121">Paso 2: establecimiento de la cuenta de suscripción y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="be390-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="be390-122">Para establecer su cuenta de suscripción y almacenamiento de Azure, ejecute estos comandos en el símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be390-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="be390-123">Reemplace todo el contenido dentro de las comillas, incluidos los caracteres < y >, por los nombres correctos.</span><span class="sxs-lookup"><span data-stu-id="be390-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="be390-124">El nombre de suscripción correcto se puede obtener de la propiedad SubscriptionName de la salida del comando **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="be390-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="be390-125">Puede obtener el nombre de cuenta de almacenamiento correcto de la propiedad Label de la salida del comando **Get-AzureStorageAccount**, una vez haya ejecutado el comando **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="be390-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="be390-126">Paso 3: Tutorial paso a paso - Aprovisionamiento de la máquina virtual y unión al dominio administrado</span><span class="sxs-lookup"><span data-stu-id="be390-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="be390-127">Este es el comando de Azure PowerShell correspondiente para crear esta máquina virtual, con líneas en blanco entre cada bloque para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="be390-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="be390-128">Especifique la información sobre la máquina virtual de Windows que desea aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="be390-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="be390-129">Para los valores de InstanceSize de las máquinas virtuales de las series D, DS o G, consulte [Máquina virtual y tamaños de servicios en la nube de Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="be390-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="be390-130">Proporcione información sobre el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="be390-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="be390-131">Especifique el nombre del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="be390-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="be390-132">Especifique el nombre de la red virtual a la que se debe unir la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be390-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="be390-133">Asegúrese de que el dominio administrado de Servicios de dominio de Azure AD está disponible en esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="be390-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="be390-134">Seleccione la imagen de máquina virtual que se usará para aprovisionar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be390-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="be390-135">Configure la máquina virtual: nombre del conjunto de máquina virtual, tamaño de instancia e imagen que se usará.</span><span class="sxs-lookup"><span data-stu-id="be390-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="be390-136">Obtenga las credenciales de administrador local para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be390-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="be390-137">Elija una contraseña segura de administrador local.</span><span class="sxs-lookup"><span data-stu-id="be390-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="be390-138">Obtenga las credenciales para una cuenta de usuario que pertenezca al grupo de administradores de controlador de dominio de AAD para unir la máquina virtual al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="be390-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="be390-139">No especifique el nombre de dominio; fíjese en nuestro ejemplo, donde "bob" es el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="be390-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="be390-140">Configure la máquina virtual: especifique el requisito de la unión a dominio y las credenciales necesarias.</span><span class="sxs-lookup"><span data-stu-id="be390-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="be390-141">Establezca una subred para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="be390-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="be390-142">Opcional: señale a la dirección IP del dominio.</span><span class="sxs-lookup"><span data-stu-id="be390-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="be390-143">Si establece las direcciones IP del dominio administrado de Servicios de dominio de Azure AD para que sean los servidores DNS de la red virtual, este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="be390-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="be390-144">Ahora, aprovisione la máquina virtual de Windows unida a un dominio.</span><span class="sxs-lookup"><span data-stu-id="be390-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="be390-145">Script para aprovisionar una máquina virtual de Windows y unirla automáticamente a un dominio administrado de Servicios de dominio de AAD</span><span class="sxs-lookup"><span data-stu-id="be390-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="be390-146">Este conjunto de comandos de PowerShell crea una máquina virtual para un servidor de línea de negocio que:</span><span class="sxs-lookup"><span data-stu-id="be390-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="be390-147">Utilice la imagen de Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="be390-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="be390-148">Es una máquina virtual extra pequeña.</span><span class="sxs-lookup"><span data-stu-id="be390-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="be390-149">Tiene el nombre Contoso100-test.</span><span class="sxs-lookup"><span data-stu-id="be390-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="be390-150">Se une automáticamente al dominio administrado contoso100.</span><span class="sxs-lookup"><span data-stu-id="be390-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="be390-151">Se agrega a la misma red virtual que el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="be390-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="be390-152">Ese es el script de ejemplo completo para crear la máquina virtual de Windows y unirla automáticamente al dominio administrado de Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be390-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="be390-153">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="be390-153">Related Content</span></span>
* [<span data-ttu-id="be390-154">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="be390-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="be390-155">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="be390-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
