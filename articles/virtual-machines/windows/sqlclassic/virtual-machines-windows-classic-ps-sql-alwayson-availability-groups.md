---
title: "aaaConfigure Hola grupo de disponibilidad AlwaysOn en una máquina virtual de Azure mediante PowerShell | Documentos de Microsoft"
description: "Este tutorial utiliza los recursos que se crearon con el modelo de implementación clásica de Hola. Usar PowerShell toocreate un grupo de disponibilidad AlwaysOn en Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="19e20-104">Configurar Hola grupo de disponibilidad AlwaysOn en una máquina virtual de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="19e20-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19e20-105">Portal de Azure clásico: interfaz de usuario</span><span class="sxs-lookup"><span data-stu-id="19e20-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="19e20-106">[Clásico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="19e20-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="19e20-107">Antes de comenzar, considere que ahora puede completar esta tarea en un modelo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="19e20-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="19e20-108">Se recomienda el modelo de Azure Resource Manager para las implementaciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="19e20-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="19e20-109">Consulte [Grupos de disponibilidad de SQL Server AlwaysOn en máquinas virtuales de Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19e20-110">Se recomienda el uso de modelo del Administrador de recursos de hello en implementaciones más nuevas.</span><span class="sxs-lookup"><span data-stu-id="19e20-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="19e20-111">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="19e20-112">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="19e20-113">Máquinas virtuales (VM) Azure puede ayudar a costo de Hola de toolower de los administradores de base de datos de un sistema de SQL Server de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="19e20-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="19e20-114">Este tutorial muestra cómo agrupar tooimplement una disponibilidad mediante el uso de SQL Server Always On-to-end dentro de un entorno de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="19e20-115">Al final de Hola de tutorial de hello, la solución SQL Server Always On en Azure constará de hello siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="19e20-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="19e20-116">Una red virtual que contiene varias subredes, incluida una subred front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="19e20-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="19e20-117">Un controlador de dominio con un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19e20-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="19e20-118">Dos VM de SQL Server que son implementados toohello subred de back-end y toohello Unidos a un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19e20-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="19e20-119">Un clúster de conmutación por error de Windows tres nodos con el modelo de quórum de mayoría de nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="19e20-120">Un grupo de disponibilidad con dos réplicas de confirmación sincrónica de una base de datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="19e20-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="19e20-121">Este escenario es una buena opción debido a su simplicidad en Azure, no por su rentabilidad ni otros factores.</span><span class="sxs-lookup"><span data-stu-id="19e20-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="19e20-122">Por ejemplo, puede minimizar Hola número de máquinas virtuales para una toosave de grupo de disponibilidad de dos réplicas en horas de proceso en Azure mediante el controlador de dominio de hello como testigo de recurso compartido de archivos de hello quórum en un clúster de conmutación por error de dos nodos.</span><span class="sxs-lookup"><span data-stu-id="19e20-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="19e20-123">Este método reduce el recuento VM de hello en uno de Hola por encima de la configuración.</span><span class="sxs-lookup"><span data-stu-id="19e20-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="19e20-124">Este tutorial está concebido tooshow Hola pasos tooset requiere seguridad Hola describe la solución anterior, sin profundizar en los detalles de Hola de cada paso.</span><span class="sxs-lookup"><span data-stu-id="19e20-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="19e20-125">Por lo tanto, en lugar de proporcionar los pasos de configuración Hola GUI, usa scripting tootake de PowerShell se rápidamente a través cada paso.</span><span class="sxs-lookup"><span data-stu-id="19e20-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="19e20-126">Este tutorial se da por supuesto siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="19e20-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="19e20-127">Ya tiene una cuenta de Azure con la suscripción de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="19e20-128">Ha instalado hello [cmdlets de PowerShell de Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="19e20-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="19e20-129">Ya tiene un conocimiento sólido de grupos de disponibilidad AlwaysOn para soluciones locales.</span><span class="sxs-lookup"><span data-stu-id="19e20-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="19e20-130">Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="19e20-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="19e20-131">Conectar tooyour suscripción de Azure y crear red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="19e20-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="19e20-132">En una ventana de PowerShell en el equipo local, importar Hola módulo de Azure, descargue Hola máquina de tooyour del archivo de configuración de publicación y conectar su tooyour de sesión de PowerShell suscripción de Azure importando la configuración de publicación de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="19e20-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="19e20-133">Hola **Get-AzurePublishSettingsFile** comando genera un certificado de administración con Azure automáticamente y descarga tooyour máquina.</span><span class="sxs-lookup"><span data-stu-id="19e20-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="19e20-134">Un explorador se abre automáticamente y le tooenter solicitadas hello las credenciales de cuenta de Microsoft para su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="19e20-135">Hola descargado **.publishsettings** archivo contiene toda la información de Hola que necesita toomanage su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="19e20-136">Después de guardar este directorio local de tooa de archivo, impórtelo mediante el uso de hello **importación-AzurePublishSettingsFile** comando.</span><span class="sxs-lookup"><span data-stu-id="19e20-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19e20-137">archivo .publishsettings de Hello contiene las credenciales (sin codificar) que son utilizado tooadminister sus servicios y suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="19e20-138">práctica recomendada de seguridad de Hola para este archivo es toostore lo temporalmente fuera de los directorios de origen (por ejemplo, en la carpeta bibliotecas\documentos Hola) y, a continuación, eliminarlo una vez ha finalizado la importación de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="19e20-139">Un usuario malintencionado que obtenga el archivo .publishsettings de acceso toohello puede modificar, crear y eliminar los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="19e20-140">Defina una serie de variables que podrá usar toocreate su infraestructura de TI en la nube.</span><span class="sxs-lookup"><span data-stu-id="19e20-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="19e20-141">Pagar toohello atención después tooensure que los comandos se ejecutarán correctamente después:</span><span class="sxs-lookup"><span data-stu-id="19e20-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="19e20-142">Las variables **$storageAccountName** y **$dcServiceName** debe ser único porque se encuentran utilizan tooidentify su cuenta de almacenamiento de nube y servidor de nube, respectivamente, en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="19e20-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="19e20-143">Hola nombres especificados para las variables **$affinityGroupName** y **$virtualNetworkName** se configuran en el documento de configuración de red virtual de Hola que va a utilizar más adelante.</span><span class="sxs-lookup"><span data-stu-id="19e20-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="19e20-144">**$sqlImageName** especifica el nombre de hello actualizado de imagen de máquina virtual de Hola que contiene SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="19e20-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="19e20-145">Para simplificar, **Contoso! 000** es Hola misma contraseña que se utiliza a lo largo de todo el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="19e20-146">Cree un grupo de afinidad.</span><span class="sxs-lookup"><span data-stu-id="19e20-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="19e20-147">Cree una red virtual importando un archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="19e20-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="19e20-148">archivo de configuración de Hello contiene Hola siguiente documento XML.</span><span class="sxs-lookup"><span data-stu-id="19e20-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="19e20-149">En resumen, especifica una red virtual denominada **ContosoNET** en el grupo de afinidad de hello denominado **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="19e20-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="19e20-150">Tiene espacio de direcciones de hello **10.10.0.0/16** y dos subredes, **10.10.1.0/24** y **10.10.2.0/24**, que son subred front-end de Hola y subred back-end, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="19e20-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="19e20-151">subred de front-end de Hello es donde puede colocar las aplicaciones cliente como Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="19e20-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="19e20-152">subred de back-end de Hello es donde colocará la VM de hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="19e20-153">Si cambia hello **$affinityGroupName** y **$virtualNetworkName** variables anteriores, debe cambiar también Hola correspondientes nombres siguientes.</span><span class="sxs-lookup"><span data-stu-id="19e20-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="19e20-154">Cree una cuenta de almacenamiento que esté asociada con el grupo de afinidad de Hola que creó y establézcalo como cuenta de almacenamiento actual de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="19e20-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="19e20-155">Crear servidor de controlador de dominio de hello en conjunto de nube nuevo servicio y la disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="19e20-156">Estos comandos canalizados Hola siguientes cosas:</span><span class="sxs-lookup"><span data-stu-id="19e20-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="19e20-157">**New-AzureVMConfig** crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="19e20-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="19e20-158">**Agregar-AzureProvisioningConfig** proporciona Hola parámetros de configuración de un servidor independiente de Windows.</span><span class="sxs-lookup"><span data-stu-id="19e20-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="19e20-159">**Agregar-AzureDataDisk** agrega Hola disco de datos que va a utilizar para almacenar los datos de Active Directory, con la opción set tooNone el almacenamiento en caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="19e20-160">**New-AzureVM** crea un nuevo servicio de nube y crea Hola nueva máquina virtual de Azure Hola nuevo servicio en nube.</span><span class="sxs-lookup"><span data-stu-id="19e20-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="19e20-161">Espere Hola nueva VM toobe aprovisionado por completo y descargar el directorio de trabajo de tooyour Hola archivo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="19e20-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="19e20-162">Hola como hello nueva máquina virtual de Azure tiene un tooprovision mucho tiempo, `while` bucle continúa toopoll Hola nueva máquina virtual hasta que estén listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="19e20-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="19e20-163">servidor de controlador de dominio de Hello ahora se aprovisionó correctamente.</span><span class="sxs-lookup"><span data-stu-id="19e20-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="19e20-164">A continuación, configurará el dominio de Active Directory de hello en este servidor de controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="19e20-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="19e20-165">Vulnerable la ventana de PowerShell de hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="19e20-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="19e20-166">Se usará nuevo toocreate posterior Hola dos VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="19e20-167">Configurar el controlador de dominio de Hola</span><span class="sxs-lookup"><span data-stu-id="19e20-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="19e20-168">Conectar servidor de controlador de dominio toohello iniciando Hola archivo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="19e20-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="19e20-169">Usar nombre de usuario AzureAdmin y la contraseña del administrador del equipo de hello **Contoso! 000**, que especificó cuando creó Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="19e20-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="19e20-170">Abra una ventana de Azure PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="19e20-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="19e20-171">Ejecute hello siguiente **DCPROMO. EXE** tooset comando seguridad hello **corp.contoso.com** dominio con directorios de datos de hello en la unidad M.</span><span class="sxs-lookup"><span data-stu-id="19e20-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="19e20-172">Cuando finaliza el comando de hello, Hola VM se reinicia automáticamente.</span><span class="sxs-lookup"><span data-stu-id="19e20-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="19e20-173">Conéctese de nuevo servidor de controlador de dominio toohello iniciando Hola archivo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="19e20-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="19e20-174">Esta vez, inicie sesión como **CORP\Administrador**.</span><span class="sxs-lookup"><span data-stu-id="19e20-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="19e20-175">Abra una ventana de PowerShell en modo de administrador e importe el módulo de Active Directory PowerShell de hello mediante el uso de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="19e20-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="19e20-176">Siguiente ejecución Hola comandos tooadd tres usuarios toohello dominio.</span><span class="sxs-lookup"><span data-stu-id="19e20-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="19e20-177">**CORP\Install** es tooconfigure usado todo lo relacionado con toohello instancias de servicio de SQL Server, el clúster de conmutación por error de Hola y el grupo de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="19e20-178">**CORP\SQLSvc1** y **CORP\SQLSvc2** se usan como cuentas de servicio de SQL Server de Hola para hello dos VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="19e20-179">Siguiente Hola de continuación, ejecute comandos toogive **CORP\Install** Hola objetos de equipo de toocreate de permisos en el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="19e20-180">Hola GUID especificado anteriormente es hello GUID para el tipo de objeto de equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="19e20-181">Hola **CORP\Install** cuenta necesita hello **leer todas las propiedades** y **crear objetos de equipo** Hola de permiso toocreate Active directo de objetos para la conmutación por error de Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="19e20-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="19e20-182">Hola **leer todas las propiedades** permiso ya se proporciona tooCORP\Install de forma predeterminada, por lo que no es necesario toogrant lo explícitamente.</span><span class="sxs-lookup"><span data-stu-id="19e20-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="19e20-183">Para obtener más información sobre los permisos que necesita el clúster de conmutación por error de hello toocreate, consulte [guía paso a paso de clúster de conmutación por error: configurar cuentas en Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="19e20-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="19e20-184">Ahora que has terminado de configurar Active Directory y objetos de usuario de hello, creará dos VM de SQL Server y combinarlos toothis dominio.</span><span class="sxs-lookup"><span data-stu-id="19e20-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="19e20-185">Crear máquinas virtuales de hello SQL Server</span><span class="sxs-lookup"><span data-stu-id="19e20-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="19e20-186">Continuar la ventana de PowerShell de hello toouse que está abierto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="19e20-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="19e20-187">Definir Hola siguientes variables adicionales:</span><span class="sxs-lookup"><span data-stu-id="19e20-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="19e20-188">Hola dirección IP **10.10.0.4** normalmente se asigna a toohello primera máquina virtual que cree en hello **10.10.0.0/16** las subredes de la red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="19e20-189">Debe comprobar que se trata Hola dirección de su servidor de controlador de dominio mediante la ejecución de **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="19e20-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="19e20-190">Hola ejecución sigue Hola de comandos canalizados toocreate primero máquina virtual en clúster de conmutación por error de hello, denominado **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="19e20-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="19e20-191">Tenga en cuenta los siguientes de hello sobre Hola comando anterior:</span><span class="sxs-lookup"><span data-stu-id="19e20-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="19e20-192">**New-AzureVMConfig** crea una configuración de máquina virtual con el nombre del conjunto de disponibilidad deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="19e20-193">Hello VM siguientes se creará con hello mismo nombre de conjunto de disponibilidad para que se está unido toohello mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="19e20-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="19e20-194">**Agregar-AzureProvisioningConfig** combinaciones Hola dominio de Active Directory de toohello de máquina virtual que ha creado.</span><span class="sxs-lookup"><span data-stu-id="19e20-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="19e20-195">**Conjunto AzureSubnet** lugares Hola a máquina virtual en la subred back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="19e20-196">**New-AzureVM** crea un nuevo servicio de nube y crea Hola nueva máquina virtual de Azure Hola nuevo servicio en nube.</span><span class="sxs-lookup"><span data-stu-id="19e20-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="19e20-197">Hola **DnsSettings** parámetro especifica el servidor DNS Hola para servidores de servicio de nube nuevo Hola hello tiene dirección IP de hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="19e20-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="19e20-198">Se trata de dirección IP de Hola de servidor de controlador de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="19e20-199">Este parámetro es necesario tooenable Hola nuevas máquinas virtuales en el dominio de Active Directory de toohello toojoin del servicio de la nube Hola correctamente.</span><span class="sxs-lookup"><span data-stu-id="19e20-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="19e20-200">Sin este parámetro, debe establecer manualmente una configuración de IPv4 hello en el servidor de controlador de dominio de máquina virtual toouse hello como servidor DNS principal de hello cuando Hola VM esté aprovisionado y, a continuación, unir el dominio de Active Directory de hello VM toohello.</span><span class="sxs-lookup"><span data-stu-id="19e20-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="19e20-201">Hola ejecución sigue canalizada comandos toocreate hello las máquinas virtuales de SQL Server, denominado **ContosoSQL1** y **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="19e20-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="19e20-202">Tenga en cuenta los siguientes de hello con respecto a los comandos de hello anteriores:</span><span class="sxs-lookup"><span data-stu-id="19e20-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="19e20-203">**New-AzureVMConfig** usa Hola el mismo nombre de conjunto de disponibilidad como servidor de controlador de dominio de Hola y utiliza Hola imagen de SQL Server 2012 Service Pack 1 Enterprise Edition en la Galería de máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="19e20-204">También establece Hola operativo sistema tooread caché de disco sólo (sin caching de escritura).</span><span class="sxs-lookup"><span data-stu-id="19e20-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="19e20-205">Se recomienda que migre Hola base de datos archivos tooa disco de datos independiente que adjuntar toohello máquina virtual y configurarlo con ninguna lectura o la caché de escritura.</span><span class="sxs-lookup"><span data-stu-id="19e20-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="19e20-206">Sin embargo, lo mejor de hello siguiente es tooremove la caché de escritura en disco del sistema operativo Hola porque no se puede quitar lee almacenamiento en caché en el disco del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="19e20-207">**Agregar-AzureProvisioningConfig** combinaciones Hola dominio de Active Directory de toohello de máquina virtual que ha creado.</span><span class="sxs-lookup"><span data-stu-id="19e20-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="19e20-208">**Conjunto AzureSubnet** lugares Hola a máquina virtual en la subred back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="19e20-209">**Agregar-AzureEndpoint** agrega extremos de acceso para que las aplicaciones cliente pueden tener acceso a estas instancias de servicios de SQL Server en hello Internet.</span><span class="sxs-lookup"><span data-stu-id="19e20-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="19e20-210">Se proporcionan puertos diferentes tooContosoSQL1 y ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="19e20-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="19e20-211">**New-AzureVM** crea Hola nueva VM de SQL Server en hello mismo servicio en la nube como ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="19e20-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="19e20-212">Debe colocar las máquinas virtuales de hello en hello mismo servicio en la nube si desea toobe en Hola el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="19e20-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="19e20-213">Espere cada toobe VM aprovisionado por completo y para cada toodownload VM su directorio de trabajo de tooyour de archivo de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="19e20-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="19e20-214">Hola `for` bucle recorre Hola tres nuevas VM y ejecuta comandos Hola dentro de llaves de nivel superior de Hola para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="19e20-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="19e20-215">Hola VM de SQL Server están aprovisionadas y en ejecución, pero está instalado con SQL Server con las opciones predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="19e20-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="19e20-216">Inicializar el clúster de conmutación por error de hello las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="19e20-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="19e20-217">En esta sección, deberá toomodify Hola tres servidores que va a utilizar en la instalación de SQL Server de Hola y clúster de conmutación por error de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="19e20-218">Concretamente:</span><span class="sxs-lookup"><span data-stu-id="19e20-218">Specifically:</span></span>

* <span data-ttu-id="19e20-219">Todos los servidores: necesita hello tooinstall **agrupación en clústeres de conmutación por error** característica.</span><span class="sxs-lookup"><span data-stu-id="19e20-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="19e20-220">Todos los servidores: necesita tooadd **CORP\Install** como máquina de hello **administrador**.</span><span class="sxs-lookup"><span data-stu-id="19e20-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="19e20-221">ContosoSQL1 y ContosoSQL2 únicamente: necesita tooadd **CORP\Install** como un **sysadmin** rol de base de datos de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19e20-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="19e20-222">ContosoSQL1 y ContosoSQL2 únicamente: necesita tooadd **NT AUTHORITY\System** como un inicio de sesión de con hello los siguientes permisos:</span><span class="sxs-lookup"><span data-stu-id="19e20-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="19e20-223">Modificar cualquier grupo de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="19e20-223">Alter any availability group</span></span>
  * <span data-ttu-id="19e20-224">Conectar SQL</span><span class="sxs-lookup"><span data-stu-id="19e20-224">Connect SQL</span></span>
  * <span data-ttu-id="19e20-225">Ver estado del servidor</span><span class="sxs-lookup"><span data-stu-id="19e20-225">View server state</span></span>
* <span data-ttu-id="19e20-226">ContosoSQL1 y ContosoSQL2 únicamente: Hola **TCP** protocolo ya está habilitado en hello VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="19e20-227">Sin embargo, todavía necesita tooopen firewall de hello para el acceso remoto de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="19e20-228">Ahora, está listo toostart.</span><span class="sxs-lookup"><span data-stu-id="19e20-228">Now, you're ready toostart.</span></span> <span data-ttu-id="19e20-229">A partir de **ContosoQuorum**, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="19e20-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="19e20-230">Conectar demasiado**ContosoQuorum** iniciando Hola archivos de escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="19e20-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="19e20-231">Usar nombre de usuario del administrador del equipo de hello **AzureAdmin** y la contraseña **Contoso! 000**, que se especificó cuando creó hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="19e20-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="19e20-232">Compruebe que los equipos de Hola se han unido correctamente demasiado**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="19e20-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="19e20-233">Espere a que toofinish de instalación de SQL Server de hello ejecutar tareas de inicialización de hello automatizada antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="19e20-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="19e20-234">Abra una ventana de Azure PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="19e20-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="19e20-235">Instale la característica de agrupación en clústeres de conmutación por error de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="19e20-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="19e20-236">Agregue **CORP\Install** como administrador local.</span><span class="sxs-lookup"><span data-stu-id="19e20-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="19e20-237">Cierre sesión en ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="19e20-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="19e20-238">Ya está listo con este servidor.</span><span class="sxs-lookup"><span data-stu-id="19e20-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="19e20-239">A continuación, inicialice **ContosoSQL1** y **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="19e20-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="19e20-240">Siga los pasos de hello siguientes, que son idénticos para ambos VM de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="19e20-241">Conéctese toohello dos VM de SQL Server iniciando los archivos de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="19e20-242">Usar nombre de usuario del administrador del equipo de hello **AzureAdmin** y la contraseña **Contoso! 000**, que se especificó cuando creó hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="19e20-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="19e20-243">Compruebe que los equipos de Hola se han unido correctamente demasiado**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="19e20-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="19e20-244">Espere a que toofinish de instalación de SQL Server de hello ejecutar tareas de inicialización de hello automatizada antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="19e20-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="19e20-245">Abra una ventana de Azure PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="19e20-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="19e20-246">Instale la característica de agrupación en clústeres de conmutación por error de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="19e20-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="19e20-247">Agregue **CORP\Install** como administrador local.</span><span class="sxs-lookup"><span data-stu-id="19e20-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="19e20-248">Importar Hola proveedor de PowerShell de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="19e20-249">Agregar **CORP\Install** como sysadmin de hello para la instancia de SQL Server de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19e20-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="19e20-250">Agregar **NT AUTHORITY\System** como un inicio de sesión de con permisos de hello tres se ha descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="19e20-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="19e20-251">Abra firewall de hello para el acceso remoto de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="19e20-252">Cierre sesión en ambas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="19e20-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="19e20-253">Por último, está listo tooconfigure grupo de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="19e20-254">Deberá usar tooperform de SQL Server PowerShell Provider Hola todos Hola funcionan de **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="19e20-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="19e20-255">Configurar grupo de disponibilidad de Hola</span><span class="sxs-lookup"><span data-stu-id="19e20-255">Configure hello availability group</span></span>
1. <span data-ttu-id="19e20-256">Conectar demasiado**ContosoSQL1** nuevo iniciando los archivos de escritorio remoto de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="19e20-257">En lugar de iniciar sesión mediante el uso de la cuenta de equipo de hello, inicie sesión con **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="19e20-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="19e20-258">Abra una ventana de Azure PowerShell en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="19e20-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="19e20-259">Definir Hola siguientes variables:</span><span class="sxs-lookup"><span data-stu-id="19e20-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="19e20-260">Importar Hola proveedor de PowerShell de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e20-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="19e20-261">Cambiar la cuenta de servicio de SQL Server de Hola para ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="19e20-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="19e20-262">Cambiar la cuenta de servicio de SQL Server de Hola para ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="19e20-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="19e20-263">Descargar **CreateAzureFailoverCluster.ps1** de [crear el clúster de conmutación por error para grupos de disponibilidad AlwaysOn en Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello directorio de trabajo local.</span><span class="sxs-lookup"><span data-stu-id="19e20-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="19e20-264">Usará este toohelp de secuencia de comandos crea un clúster de conmutación por error funcional.</span><span class="sxs-lookup"><span data-stu-id="19e20-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="19e20-265">Para obtener información importante sobre cómo interactúa la agrupación en clústeres de conmutación por error de Windows con hello Azure de red, consulte [alta disponibilidad y recuperación ante desastres para SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19e20-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="19e20-266">Cambie el directorio de trabajo tooyour y creación de clúster de conmutación por error de hello con script de Hola descargado.</span><span class="sxs-lookup"><span data-stu-id="19e20-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="19e20-267">Habilitar grupos de disponibilidad AlwaysOn para las instancias de SQL Server predeterminadas de hello en **ContosoSQL1** y **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="19e20-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="19e20-268">Cree un directorio de copia de seguridad y conceder permisos para las cuentas de servicio de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="19e20-269">Usará esta base de datos de disponibilidad de directorio tooprepare hello en la réplica secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="19e20-270">Crear una base de datos en **ContosoSQL1** llama **MyDB1**, realice una copia de seguridad completa y una copia de seguridad de registros y restáurelas en **ContosoSQL2** con hello **WITH NORECOVERY** opción.</span><span class="sxs-lookup"><span data-stu-id="19e20-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="19e20-271">Cree extremos del grupo de disponibilidad de hello en hello VM de SQL Server y establezca los permisos apropiados de hello en los puntos de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="19e20-272">Crear réplicas de disponibilidad, Hola.</span><span class="sxs-lookup"><span data-stu-id="19e20-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="19e20-273">Finalmente, cree el grupo de disponibilidad de Hola y grupo de disponibilidad de toohello de combinación Hola réplica secundaria.</span><span class="sxs-lookup"><span data-stu-id="19e20-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="19e20-274">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19e20-274">Next steps</span></span>
<span data-ttu-id="19e20-275">Ha implementado correctamente SQL Server AlwaysOn mediante la creación de un grupo de disponibilidad en Azure.</span><span class="sxs-lookup"><span data-stu-id="19e20-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="19e20-276">tooconfigure un agente de escucha para este grupo de disponibilidad, consulte [configurar un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="19e20-277">Para más información sobre el uso de SQL Server en Azure, consulte [SQL Server en Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19e20-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
