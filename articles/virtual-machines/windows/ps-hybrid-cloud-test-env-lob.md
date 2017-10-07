---
title: "entorno de prueba de aplicación aaaLOB | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate basada en web, línea de aplicaciones empresariales en un híbrido en la nube de entorno de TI pro o las pruebas de desarrollo."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="dcb1f-103">Configuración de una aplicación de LOB basada en web en una nube híbrida para pruebas</span><span class="sxs-lookup"><span data-stu-id="dcb1f-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="dcb1f-104">En este tema se le guiará en el proceso de creación de un entorno de nube híbrida simulada para probar una aplicación de línea de negocio (LOB) basada en web hospedada en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="dcb1f-105">Esta es la configuración resultante de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="dcb1f-106">Esta configuración consta de:</span><span class="sxs-lookup"><span data-stu-id="dcb1f-106">This configuration consists of:</span></span>

* <span data-ttu-id="dcb1f-107">Una red de simulada en entornos hospedada en Azure (Hola TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="dcb1f-108">Una red virtual entre locales hospedada en Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="dcb1f-109">Una conexión VPN de red virtual a red virtual.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="dcb1f-110">Un servidor LOB basado en web, SQL server y el controlador de dominio secundario en la red virtual de hello TestVNET.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="dcb1f-111">Esta configuración proporciona una base y un punto de partida común desde el que puede:</span><span class="sxs-lookup"><span data-stu-id="dcb1f-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="dcb1f-112">Desarrollar y probar aplicaciones de LOB hospedadas en Internet Information Services (IIS) con un back-end de base de datos de SQL Server 2014 en Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="dcb1f-113">Realizar pruebas de esta carga de trabajo de TI basada en la nube híbrida simulada.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="dcb1f-114">Hay tres toosetting fases principales en este entorno de prueba de nube híbrida:</span><span class="sxs-lookup"><span data-stu-id="dcb1f-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="dcb1f-115">Configurar el entorno de nube híbrida simulada Hola.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="dcb1f-116">Configurar el equipo con hello SQL server (SQL1).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="dcb1f-117">Configurar servidor LOB de hello (LOB1).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="dcb1f-118">Esta carga de trabajo requiere una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="dcb1f-119">Si tiene una suscripción de MSDN o de Visual Studio, consulte [Crédito mensual de Azure para suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="dcb1f-120">Para obtener un ejemplo de una aplicación LOB hospedada en Azure de producción, vea hello **línea de aplicaciones empresariales** plano técnico de arquitectura en [diagramas de arquitectura de Software de Microsoft y planos](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="dcb1f-121">Fase 1: Configurar el entorno de nube híbrida simulada Hola</span><span class="sxs-lookup"><span data-stu-id="dcb1f-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="dcb1f-122">Crear hello [entorno de prueba de nube híbrida simulada](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dcb1f-123">Dado que este entorno de prueba no requiere la presencia de Hola de servidor hello APP1 en la subred Corpnet de hello, puede cerrarlo por ahora.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="dcb1f-124">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="dcb1f-125">Fase 2: Configurar el equipo con hello SQL server (SQL1)</span><span class="sxs-lookup"><span data-stu-id="dcb1f-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="dcb1f-126">Empezar desde Hola portal de Azure, equipo de DC2 Hola si es necesario.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="dcb1f-127">Después, cree una máquina virtual para SQL1 con estos comandos en un símbolo del sistema de Azure PowerShell en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="dcb1f-128">Toorunning anterior estos comandos, rellene Hola valores de las variables y quitar Hola < y > caracteres.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="dcb1f-129">Usar hello Azure tooconnect portal tooSQL1 con cuenta de administrador local de Hola de SQL1.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="dcb1f-130">A continuación, configure la conectividad básica pruebas de tooallow de reglas de Firewall de Windows y el tráfico de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="dcb1f-131">Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en SQL1, ejecute estos comandos.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="dcb1f-132">comando ping de Hello debe producir cuatro respuestas correcta de la dirección IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="dcb1f-133">A continuación, agregue Hola disco de datos adicionales en SQL1 como un volumen nuevo con una letra de unidad de hello F:.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="dcb1f-134">En el panel izquierdo del administrador del servidor de hello, haga clic en **File and Storage Services**y, a continuación, haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="dcb1f-135">En panel de contenido de hello, Hola **discos** grupo, haga clic en **disco 2** (con hello **partición** establecido demasiado**desconocido**).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="dcb1f-136">Haga clic en **Tareas** y luego haga clic en **Nuevo volumen**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="dcb1f-137">En hello antes de comenzar la página del Asistente para nuevo volumen hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="dcb1f-138">En el servidor seleccione Hola de Hola y página de disco, haga clic en **disco 2**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="dcb1f-139">Cuando se le solicite, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="dcb1f-140">En especificar el tamaño de Hola de página de volumen de Hola Hola, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="dcb1f-141">En hello asignar tooa unidad carpeta o letra de página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="dcb1f-142">En la página Configuración del sistema seleccione archivo hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="dcb1f-143">En la página Confirmar selecciones de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="dcb1f-144">Cuando haya terminado, haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-144">When complete, click **Close**.</span></span>

<span data-ttu-id="dcb1f-145">Ejecute estos comandos en línea de comandos de Windows PowerShell de hello en SQL1:</span><span class="sxs-lookup"><span data-stu-id="dcb1f-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="dcb1f-146">A continuación, unirse a dominio de CORP Windows Server Active Directory de toohello SQL1 con estos comandos en el símbolo del sistema de Windows PowerShell de hello en SQL1.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="dcb1f-147">Usar cuenta de hello CORP\User1 cuando se le solicite credenciales de cuenta de dominio toosupply de hello **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="dcb1f-148">Después de reiniciar, use hello Azure tooconnect portal tooSQL1 *con la cuenta de administrador local de Hola de SQL1*.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="dcb1f-149">A continuación, configure SQL Server 2014 toouse Hola la unidad F: para nuevas bases de datos y de los permisos de cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="dcb1f-150">En la pantalla de inicio de bienvenida, escriba **administración de SQL Server**y, a continuación, haga clic en **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="dcb1f-151">En **conectar tooServer**, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="dcb1f-152">En el panel de árbol del explorador de objetos de hello, haga clic en **SQL1**y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="dcb1f-153">Hola **propiedades del servidor** ventana, haga clic en **configuración de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="dcb1f-154">Busque hello **ubicaciones predeterminadas de la base de datos** y establecer estos valores:</span><span class="sxs-lookup"><span data-stu-id="dcb1f-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="dcb1f-155">Para **datos**, ruta de acceso del tipo hello **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="dcb1f-156">Para **registro**, ruta de acceso del tipo hello **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="dcb1f-157">Para **copia de seguridad**, ruta de acceso del tipo hello **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="dcb1f-158">Nota: Solo las bases de datos nuevas utilizan estas ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="dcb1f-159">Haga clic en hello **Aceptar** ventana de hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="dcb1f-160">Hola **Explorador de objetos** panel del árbol, abra **seguridad**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="dcb1f-161">Haga clic con el botón derecho en **Inicios de sesión** y luego haga clic en **Nuevo inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="dcb1f-162">En **Nombre de inicio de sesión**, escriba **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="dcb1f-163">En hello **Roles de servidor** página, haga clic en **sysadmin**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="dcb1f-164">Cierre Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="dcb1f-165">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="dcb1f-166">Fase 3: Configurar el servidor LOB de hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="dcb1f-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="dcb1f-167">Primero, cree una máquina virtual para LOB1 con estos comandos en línea de comandos de PowerShell de Azure de hello en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="dcb1f-168">A continuación, use hello Azure tooconnect portal tooLOB1 con credenciales de Hola de cuenta de administrador local de Hola de LOB1.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="dcb1f-169">A continuación, configure un tráfico de tooallow de regla de Firewall de Windows para probar la conectividad básica.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="dcb1f-170">Desde un símbolo del sistema de Windows PowerShell con nivel de administrador en LOB1, ejecute estos comandos.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="dcb1f-171">comando ping de Hello debe producir cuatro respuestas correcta de la dirección IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="dcb1f-172">A continuación, unirse a dominio de Active Directory de CORP toohello de LOB1 con estos comandos en el símbolo del sistema de hello Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="dcb1f-173">Usar cuenta de hello CORP\User1 cuando se le solicite credenciales de cuenta de dominio toosupply de hello **Add-Computer** comando.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="dcb1f-174">Después de reiniciar, use hello Azure tooconnect portal tooLOB1 con hello CORP\User1 cuentas y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="dcb1f-175">A continuación, configure LOB1 para IIS y pruebe el acceso desde CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="dcb1f-176">En Administrador del servidor, haga clic en **Agregar roles y características**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="dcb1f-177">En hello **antes de comenzar** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="dcb1f-178">En hello **Seleccionar tipo de instalación** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="dcb1f-179">En hello **Seleccionar servidor de destino** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="dcb1f-180">En hello **roles de servidor** página, haga clic en **servidor Web (IIS)** en la lista de Hola de **Roles**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="dcb1f-181">Cuando se le solicite, haga clic en **Agregar características** y después en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="dcb1f-182">En hello **seleccionar características** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="dcb1f-183">En hello **servidor Web (IIS)** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="dcb1f-184">En hello **seleccionar servicios de rol** , seleccione o desactive casillas de verificación de Hola para servicios de Hola que necesita para probar la aplicación de LOB y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="dcb1f-185">En hello **Confirmar selecciones de instalación** página, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="dcb1f-186">Espere hasta que haya completado la instalación de Hola de componentes y, a continuación, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="dcb1f-187">Desde Hola portal de Azure, conectar toohello CLIENT1 equipo con las credenciales de cuenta de hello CORP\User1 y, a continuación, inicie Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="dcb1f-188">En la barra de direcciones de hello, escriba **http://lob1/** y, a continuación, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="dcb1f-189">Debería ver la página web de hello predeterminada IIS 8.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="dcb1f-190">Se trata de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="dcb1f-191">Este entorno es ahora está listo para que se toodeploy su aplicación web sobre las funciones LOB1 y prueba de CLIENT1 en la subred Corpnet de Hola.</span><span class="sxs-lookup"><span data-stu-id="dcb1f-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="dcb1f-192">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="dcb1f-192">Next step</span></span>
* <span data-ttu-id="dcb1f-193">Agregar una nueva máquina virtual con hello [portal de Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dcb1f-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

