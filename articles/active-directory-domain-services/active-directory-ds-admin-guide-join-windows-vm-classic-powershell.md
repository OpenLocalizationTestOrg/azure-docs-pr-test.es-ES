---
title: "Active Directory Domain Services: guía de administración | Microsoft Docs"
description: "Unir un máquina virtual tooa administrado dominio de Windows con PowerShell de Azure y modelo de implementación clásica de Hola."
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
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="7e87a-103">Unirse a un máquina virtual tooa administrado dominio de Windows Server con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e87a-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7e87a-104">Portal de Azure clásico - Windows</span><span class="sxs-lookup"><span data-stu-id="7e87a-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="7e87a-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="7e87a-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="7e87a-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7e87a-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7e87a-107">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7e87a-108">Servicios de dominio de Azure AD no admite actualmente el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="7e87a-109">Estos pasos muestra cómo toocustomize un conjunto de Azure PowerShell comandos que crear y preconfigurar una máquina virtual de Azure basado en Windows mediante un enfoque de bloque de creación.</span><span class="sxs-lookup"><span data-stu-id="7e87a-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="7e87a-110">Estos pasos le permiten crear una máquina virtual de Azure basado en Windows y unirse a dominio administrado de tooan servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e87a-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="7e87a-111">En estos pasos se sigue un enfoque consistente en atar cabos para crear conjuntos de comandos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e87a-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="7e87a-112">Este enfoque puede ser útil si es nuevo tooPowerShell o desea tooknow qué toospecify valores para una configuración correcta.</span><span class="sxs-lookup"><span data-stu-id="7e87a-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="7e87a-113">Los usuarios avanzados de PowerShell pueden tomar los comandos de Hola y sustituir sus propios valores para las variables de hello (líneas de hello comenzar con "$").</span><span class="sxs-lookup"><span data-stu-id="7e87a-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="7e87a-114">Si aún no lo ha no lo ha hecho, use las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="7e87a-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="7e87a-115">Después, abra el símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e87a-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="7e87a-116">Paso 1: agregar la cuenta</span><span class="sxs-lookup"><span data-stu-id="7e87a-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="7e87a-117">En el símbolo del sistema de PowerShell hello, escriba **Add-AzureAccount** y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="7e87a-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="7e87a-118">Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="7e87a-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="7e87a-119">Escribir contraseña de Hola para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="7e87a-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="7e87a-120">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="7e87a-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="7e87a-121">Paso 2: establecimiento de la cuenta de suscripción y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="7e87a-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="7e87a-122">Establecer la suscripción de Azure y la cuenta de almacenamiento mediante la ejecución de estos comandos en línea de comandos de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="7e87a-123">Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con los nombres correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="7e87a-124">Puede obtener nombre de la suscripción correcta de Hola de hello SubscriptionName propiedad de salida de hello de hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="7e87a-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="7e87a-125">Puede obtener nombre de cuenta de almacenamiento correcta de Hola de hello propiedad Label de salida de hello de hello **Get AzureStorageAccount** comando después de ejecutar hello **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="7e87a-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="7e87a-126">Paso 3: Tutorial paso a paso: aprovisionar la máquina virtual de Hola y unirse a dominio administrados toohello</span><span class="sxs-lookup"><span data-stu-id="7e87a-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="7e87a-127">Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual, con líneas en blanco entre cada bloque para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="7e87a-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="7e87a-128">Especifique la información sobre toobe de máquina virtual de Windows hello aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="7e87a-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="7e87a-129">Para los valores de InstanceSize Hola D, DS o máquinas virtuales de serie G, vea [Máquina Virtual y tamaños de servicio de nube de Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e87a-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="7e87a-130">Proporciona información sobre el dominio administrado Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="7e87a-131">Especifique el nombre de hello del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="7e87a-132">Especificar nombre de Hola de Hola Hola de toowhich de red virtual que debe estar unida la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7e87a-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="7e87a-133">Asegúrese de que ese dominio de AAD-DS administrados Hola está disponible en esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="7e87a-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="7e87a-134">Seleccione Hola VM imagen toobe utiliza tooprovision Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7e87a-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="7e87a-135">Configurar Hola VM - nombre de la máquina virtual de conjunto, toobe & imagen de tamaño de instancia utiliza.</span><span class="sxs-lookup"><span data-stu-id="7e87a-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="7e87a-136">Obtener credenciales de administrador local para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7e87a-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="7e87a-137">Elija una contraseña segura de administrador local.</span><span class="sxs-lookup"><span data-stu-id="7e87a-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="7e87a-138">Obtener credenciales para una cuenta de usuario que pertenecen a toojoin VM toohello administrado dominio del grupo los administradores de controlador de dominio de too'AAD de.</span><span class="sxs-lookup"><span data-stu-id="7e87a-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="7e87a-139">No especificar nombre de dominio de hello - de instancia, en nuestro ejemplo, especificamos 'bob' como nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="7e87a-140">Configure Hola VM: especifique el requisito de unión de dominio y las credenciales necesarias.</span><span class="sxs-lookup"><span data-stu-id="7e87a-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="7e87a-141">Establecer una subred de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="7e87a-142">Opcional: La dirección IP de toohello de punto de dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="7e87a-143">Si establece las direcciones IP Hola de Hola Hola de toobe de dominio administrados de servicios de dominio de AD de Azure servidores DNS para la red virtual de hello, este paso no es necesario.</span><span class="sxs-lookup"><span data-stu-id="7e87a-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="7e87a-144">Ahora, Hola aprovisionar Unidos al dominio VM de Windows.</span><span class="sxs-lookup"><span data-stu-id="7e87a-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="7e87a-145">Script tooprovision una VM de Windows y automáticamente unirse a dominio administrado de los servicios de dominio de AAD de tooan</span><span class="sxs-lookup"><span data-stu-id="7e87a-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="7e87a-146">Este conjunto de comandos de PowerShell crea una máquina virtual para un servidor de línea de negocio que:</span><span class="sxs-lookup"><span data-stu-id="7e87a-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="7e87a-147">Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.</span><span class="sxs-lookup"><span data-stu-id="7e87a-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="7e87a-148">Es una máquina virtual extra pequeña.</span><span class="sxs-lookup"><span data-stu-id="7e87a-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="7e87a-149">Tiene el nombre de hello Contoso100-prueba.</span><span class="sxs-lookup"><span data-stu-id="7e87a-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="7e87a-150">Es automáticamente toohello Unidos a un dominio contoso100 el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="7e87a-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="7e87a-151">Se agrega toohello misma red virtual que Hola administrados dominio.</span><span class="sxs-lookup"><span data-stu-id="7e87a-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="7e87a-152">Este es Hola máquina de virtual de Windows de ejemplo completo script toocreate hello y automáticamente unirse a dominio administrado de toohello servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="7e87a-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="7e87a-153">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="7e87a-153">Related Content</span></span>
* [<span data-ttu-id="7e87a-154">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="7e87a-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="7e87a-155">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="7e87a-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
