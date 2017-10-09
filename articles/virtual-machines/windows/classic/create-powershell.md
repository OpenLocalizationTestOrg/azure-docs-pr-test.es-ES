---
title: aaaCreate una VM de Windows con PowerShell | Documentos de Microsoft
description: "Crear máquinas virtuales de Windows con PowerShell de Azure y modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="86a4a-103">Crear una máquina virtual de Windows con el modelo de implementación clásica de hello y PowerShell</span><span class="sxs-lookup"><span data-stu-id="86a4a-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86a4a-104">Azure Portal - Windows</span><span class="sxs-lookup"><span data-stu-id="86a4a-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="86a4a-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="86a4a-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="86a4a-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="86a4a-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="86a4a-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="86a4a-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="86a4a-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="86a4a-109">Obtenga información acerca de cómo demasiado[realizar estos pasos con el modelo del Administrador de recursos de hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86a4a-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="86a4a-110">Estos pasos muestra cómo toocustomize un conjunto de Azure PowerShell comandos que crear y preconfigurar una máquina virtual de Azure basado en Windows mediante un enfoque de bloque de creación.</span><span class="sxs-lookup"><span data-stu-id="86a4a-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="86a4a-111">Puede utilizar este proceso tooquickly crear un conjunto de comandos para una nueva máquina virtual basada en Windows y expandir una implementación existente o crear una personalizada para desarrollo y pruebas o el entorno profesional de TI toocreate varios comandos que establece rápidamente.</span><span class="sxs-lookup"><span data-stu-id="86a4a-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="86a4a-112">En estos pasos se sigue un enfoque consistente en atar cabos para crear conjuntos de comandos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86a4a-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="86a4a-113">Este enfoque puede ser útil si está tooPowerShell nueva o simplemente desea tooknow qué toospecify valores para una configuración correcta.</span><span class="sxs-lookup"><span data-stu-id="86a4a-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="86a4a-114">Los usuarios avanzados de PowerShell pueden tomar los comandos de Hola y sustituir sus propios valores para las variables de hello (líneas de hello comenzar con "$").</span><span class="sxs-lookup"><span data-stu-id="86a4a-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="86a4a-115">Si aún no lo ha no lo ha hecho, use las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="86a4a-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="86a4a-116">Después, abra el símbolo del sistema de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86a4a-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="86a4a-117">Paso 1: agregar la cuenta</span><span class="sxs-lookup"><span data-stu-id="86a4a-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="86a4a-118">En el símbolo del sistema de PowerShell hello, escriba **Add-AzureAccount** y haga clic en **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="86a4a-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="86a4a-119">Escriba Hola dirección de correo electrónico asociada a su suscripción de Azure y haga clic en **continuar**.</span><span class="sxs-lookup"><span data-stu-id="86a4a-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="86a4a-120">Escribir contraseña de Hola para su cuenta.</span><span class="sxs-lookup"><span data-stu-id="86a4a-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="86a4a-121">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="86a4a-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="86a4a-122">Paso 2: establecimiento de la cuenta de suscripción y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="86a4a-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="86a4a-123">Establecer la suscripción de Azure y la cuenta de almacenamiento mediante la ejecución de estos comandos en línea de comandos de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="86a4a-124">Reemplace todo el contenido de las comillas de hello, incluidos Hola < y > caracteres, con los nombres correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="86a4a-125">Puede obtener nombre de la suscripción correcta de Hola de hello SubscriptionName propiedad de salida de hello de hello **Get-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="86a4a-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="86a4a-126">Puede obtener nombre de cuenta de almacenamiento correcta de Hola de hello propiedad Label de salida de hello de hello **Get AzureStorageAccount** comando después de ejecutar hello **Select-AzureSubscription** comando.</span><span class="sxs-lookup"><span data-stu-id="86a4a-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="86a4a-127">Paso 3: Determinar hello ImageFamily</span><span class="sxs-lookup"><span data-stu-id="86a4a-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="86a4a-128">A continuación, necesita toodetermine Hola ImageFamily o valor de etiqueta para hello imagen específica correspondiente toohello máquina virtual de Azure que desee toocreate.</span><span class="sxs-lookup"><span data-stu-id="86a4a-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="86a4a-129">Puede obtener Hola lista de valores disponibles de ImageFamily con este comando.</span><span class="sxs-lookup"><span data-stu-id="86a4a-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="86a4a-130">A continuación, se muestran algunos ejemplos de valores de ImageFamily para equipos basados en Windows:</span><span class="sxs-lookup"><span data-stu-id="86a4a-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="86a4a-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="86a4a-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="86a4a-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="86a4a-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="86a4a-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="86a4a-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="86a4a-134">SQL Server 2012 SP1 Enterprise en Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="86a4a-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="86a4a-135">Si encuentra la imagen de Hola que está buscando, abra una nueva instancia del editor de texto hello de su elección u Hola PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="86a4a-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="86a4a-136">Copie Hola siguiente en el nuevo archivo de texto de Hola o hello PowerShell ISE, sustituyendo el valor de ImageFamily Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="86a4a-137">En algunos casos, nombre de la imagen de hello es Hola propiedad de etiqueta en lugar de hello ImageFamily valor.</span><span class="sxs-lookup"><span data-stu-id="86a4a-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="86a4a-138">Si no encontró la imagen de Hola que desea para el uso de la propiedad ImageFamily hello, una lista de imágenes de Hola por su propiedad de etiqueta con este comando.</span><span class="sxs-lookup"><span data-stu-id="86a4a-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="86a4a-139">Si encuentra la imagen de la derecha Hola con este comando, abra una nueva instancia del editor de texto hello de su elección u Hola PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="86a4a-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="86a4a-140">Copie Hola siguiente en el nuevo archivo de texto de Hola o hello PowerShell ISE, sustituyendo el valor de la etiqueta de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="86a4a-141">Paso 4: Creación del conjunto de comandos</span><span class="sxs-lookup"><span data-stu-id="86a4a-141">Step 4: Build your command set</span></span>
<span data-ttu-id="86a4a-142">Construir el resto de hello del comando establecer copiando el conjunto adecuado de Hola de bloques a continuación en el nuevo archivo de texto u Hola ISE y, a continuación, rellena los valores de variable de Hola y quitando Hola < y > caracteres.</span><span class="sxs-lookup"><span data-stu-id="86a4a-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="86a4a-143">Vea Hola dos [ejemplos](#examples) final Hola de este artículo para obtener una idea del resultado final de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="86a4a-144">Inicie el conjunto de comandos eligiendo uno de estos dos bloques de comandos (obligatorio).</span><span class="sxs-lookup"><span data-stu-id="86a4a-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="86a4a-145">Opción 1: Especificación de un nombre de máquina virtual y un tamaño.</span><span class="sxs-lookup"><span data-stu-id="86a4a-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="86a4a-146">Opción 2: Especificación de un nombre, un tamaño y un nombre del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="86a4a-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="86a4a-147">Para los valores de InstanceSize Hola D, DS o máquinas virtuales de serie G, vea [Máquina Virtual y tamaños de servicio de nube de Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="86a4a-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="86a4a-148">Si tiene un contrato Enterprise con Software Assurance y piensa tootake aprovechar Hola Windows Server [ventaja del uso de híbrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/), agregar el **- LicenseType** toohello parámetro  **New-AzureVMConfig** cmdlet, se pasa el valor de hello **Windows_Server** para hello típico caso de usuario.</span><span class="sxs-lookup"><span data-stu-id="86a4a-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="86a4a-149">Asegúrese de que usa una imagen que ha cargado; no se puede usar una imagen estándar de hello galería con hello híbrida ventaja de usar.</span><span class="sxs-lookup"><span data-stu-id="86a4a-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="86a4a-150">Si lo desea, para un equipo de Windows independiente, especifique cuentas de administrador local de Hola y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="86a4a-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="86a4a-151">Elija una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="86a4a-151">Choose a strong password.</span></span> <span data-ttu-id="86a4a-152">toocheck su nivel de seguridad, consulte [Comprobador de contraseñas: uso de contraseñas seguras](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="86a4a-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="86a4a-153">Si lo desea, tooadd Hola Windows equipo tooan dominio de Active Directory, especifique la cuenta de administrador local de Hola y contraseña, dominio hello y nombre de Hola y la contraseña de una cuenta de dominio.</span><span class="sxs-lookup"><span data-stu-id="86a4a-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="86a4a-154">Para opciones de configuración previa adicionales para máquinas virtuales basadas en Windows, vea la sintaxis de Hola para hello **Windows** y **WindowsDomain** parámetro se establece [ Agregar-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="86a4a-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="86a4a-155">Opcionalmente, asigne máquina virtual de hello una dirección IP específica, conocida como una DIP estática.</span><span class="sxs-lookup"><span data-stu-id="86a4a-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="86a4a-156">Puede comprobar que una dirección IP concreta está disponible con:</span><span class="sxs-lookup"><span data-stu-id="86a4a-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="86a4a-157">Opcionalmente, asigne tooa de subred específica en una red virtual para la máquina virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="86a4a-158">Opcionalmente, agregue una máquina virtual de datos único disco toohello.</span><span class="sxs-lookup"><span data-stu-id="86a4a-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="86a4a-159">Para un controlador de dominio de Active Directory, establezca $hcaching demasiado "None".</span><span class="sxs-lookup"><span data-stu-id="86a4a-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="86a4a-160">Opcionalmente, agregue Hola máquina virtual tooan existente conjunto de carga equilibrada para tráfico externo.</span><span class="sxs-lookup"><span data-stu-id="86a4a-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="86a4a-161">Por último, elija uno de estos bloques de comandos necesarios para crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="86a4a-162">Opción 1: Crear la máquina virtual de Hola en un servicio de nube existente.</span><span class="sxs-lookup"><span data-stu-id="86a4a-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="86a4a-163">nombre corto de Hello del servicio de nube de hello es nombre de Hola que aparece en la lista de servicios en la nube Hola Hola portal de Azure o en la lista de Hola de grupos de recursos en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a4a-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="86a4a-164">Opción 2: Crear máquina virtual de hello en un servicio en la nube y una red virtual.</span><span class="sxs-lookup"><span data-stu-id="86a4a-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="86a4a-165">Paso 5: Ejecución del conjunto de comandos</span><span class="sxs-lookup"><span data-stu-id="86a4a-165">Step 5: Run your command set</span></span>
<span data-ttu-id="86a4a-166">Revise el conjunto de comandos de PowerShell de Azure Hola creado en el editor de texto u Hola PowerShell ISE que consta de varios bloques de comandos del paso 4.</span><span class="sxs-lookup"><span data-stu-id="86a4a-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="86a4a-167">Asegúrese de que ha especificado todas las variables de hello necesitado y que tengan valores correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="86a4a-168">Además, asegúrese de que se han quitado todos los Hola < y > caracteres.</span><span class="sxs-lookup"><span data-stu-id="86a4a-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="86a4a-169">Si está utilizando un editor de texto, copia Hola comando establezca toohello Portapapeles y, a continuación, haga clic en el símbolo del sistema de abrir Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86a4a-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="86a4a-170">Esto emitirá el conjunto de comandos de hello como una serie de comandos de PowerShell y crear la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a4a-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="86a4a-171">Como alternativa, ejecutar comandos de hello establecido en hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="86a4a-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="86a4a-172">Si va a crear esta máquina virtual de nuevo o una similar, puede:</span><span class="sxs-lookup"><span data-stu-id="86a4a-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="86a4a-173">Guardar este conjunto de comandos como archivo de script de PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="86a4a-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="86a4a-174">Guardar este comando establece como un runbook de automatización de Azure en hello **cuentas de automatización** sección de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a4a-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="86a4a-175"><a id="examples"></a>Ejemplos</span><span class="sxs-lookup"><span data-stu-id="86a4a-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="86a4a-176">Presentamos dos ejemplos del uso de pasos de hello anteriores conjuntos de comandos de PowerShell de Azure toobuild que creación máquinas virtuales Azure basadas en Windows.</span><span class="sxs-lookup"><span data-stu-id="86a4a-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="86a4a-177">Ejemplo 1</span><span class="sxs-lookup"><span data-stu-id="86a4a-177">Example 1</span></span>
<span data-ttu-id="86a4a-178">Se necesita un PowerShell comando establecer máquina virtual toocreate Hola inicial para un controlador de dominio de Active Directory:</span><span class="sxs-lookup"><span data-stu-id="86a4a-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="86a4a-179">Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="86a4a-180">Tiene el nombre de hello AZDC1.</span><span class="sxs-lookup"><span data-stu-id="86a4a-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="86a4a-181">Sea un equipo independiente.</span><span class="sxs-lookup"><span data-stu-id="86a4a-181">Is a standalone computer.</span></span>
* <span data-ttu-id="86a4a-182">Tenga un disco de datos adicional de 20 GB.</span><span class="sxs-lookup"><span data-stu-id="86a4a-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="86a4a-183">No tiene dirección IP estática de hello 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="86a4a-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="86a4a-184">Está en la subred de back-end de Hola de red virtual de hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="86a4a-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="86a4a-185">Está en servicio de nube de hello TailspinToys de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a4a-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="86a4a-186">Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual, con líneas en blanco entre cada bloque para mejorar la legibilidad.</span><span class="sxs-lookup"><span data-stu-id="86a4a-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="86a4a-187">Ejemplo 2</span><span class="sxs-lookup"><span data-stu-id="86a4a-187">Example 2</span></span>
<span data-ttu-id="86a4a-188">Se necesita un PowerShell comando establecer toocreate una máquina virtual para un servidor de línea de negocio que:</span><span class="sxs-lookup"><span data-stu-id="86a4a-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="86a4a-189">Utiliza la imagen de Windows Server 2012 R2 Datacenter Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="86a4a-190">Tiene el nombre de hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="86a4a-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="86a4a-191">Es un miembro de dominio de corp.contoso.com Hola.</span><span class="sxs-lookup"><span data-stu-id="86a4a-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="86a4a-192">Tenga un disco de datos adicional de 200 GB.</span><span class="sxs-lookup"><span data-stu-id="86a4a-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="86a4a-193">Está en la subred de front-end de Hola de red virtual de hello AZDatacenter.</span><span class="sxs-lookup"><span data-stu-id="86a4a-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="86a4a-194">Está en servicio de nube de hello TailspinToys de Azure.</span><span class="sxs-lookup"><span data-stu-id="86a4a-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="86a4a-195">Aquí es Hola correspondiente Azure PowerShell comando conjunto toocreate esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86a4a-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="86a4a-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86a4a-196">Next steps</span></span>
<span data-ttu-id="86a4a-197">Si necesita un disco del SO que es mayor que 127 GB, puede [expanda la unidad de hello OS](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="86a4a-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

