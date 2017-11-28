---
title: "Configuración de un clúster híbrido de HPC Pack en Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo usar Microsoft HPC Pack y Azure para configurar un pequeño clúster híbrido de informática de alto rendimiento (HPC)"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="a3506-103">Configuración de un clúster híbrido de informática de alto rendimiento (HPC) con nodos de proceso de Azure a petición y Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="a3506-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="a3506-104">Use Microsoft HPC Pack 2012 R2 y Azure para configurar un pequeño clúster híbrido de informática de alto rendimiento (HPC).</span><span class="sxs-lookup"><span data-stu-id="a3506-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="a3506-105">El clúster que se muestra en el artículo consta del nodo principal de un HPC Pack local y algunos nodos de ejecución que se implementan a petición en un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="a3506-106">A continuación, podrá ejecutar trabajos informáticos en el clúster híbrido.</span><span class="sxs-lookup"><span data-stu-id="a3506-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Clúster híbrido de HPC][Overview] 

<span data-ttu-id="a3506-108">Este tutorial muestra un enfoque, en ocasiones denominado clúster "ráfaga en la nube", para usar recursos de escalables y a petición a fin de ejecutar aplicaciones informáticas que consumen numerosos recursos.</span><span class="sxs-lookup"><span data-stu-id="a3506-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="a3506-109">En este tutorial se supone que no cuenta con experiencia previa con los clústeres informáticos o con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a3506-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="a3506-110">Únicamente está destinado a ayudarle a implementar un clúster de proceso híbrido rápidamente con fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="a3506-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="a3506-111">Para más información y conocer los pasos que se deben dar para implementar un clúster de HPC Pack híbrido a gran escala en un entorno de producción o para usar HPC Pack 2016, consulte las [instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a3506-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="a3506-112">Para otros escenarios de HPC Pack, incluida la implementación automatizada de clústeres en máquinas virtuales de Azure, consulte [Opciones de clúster de HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3506-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3506-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3506-113">Prerequisites</span></span>
* <span data-ttu-id="a3506-114">**Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="a3506-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="a3506-115">**Un equipo local que ejecute Windows Server 2012 R2 o Windows Server 2012**. Use este equipo como el nodo principal del clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="a3506-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="a3506-116">Si todavía no tiene Windows Server, puede descargar e instalar una [versión de evaluación](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="a3506-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="a3506-117">El equipo debe estar unido a un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a3506-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="a3506-118">Para realizar pruebas, puede configurar el equipo del nodo principal como controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="a3506-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="a3506-119">Para agregar el rol del servidor de Active Directory Domain Services y promover el equipo del nodo principal como controlador de dominio, consulte la documentación de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3506-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="a3506-120">Para admitir HPC Pack, el sistema operativo debe estar instalado en uno de estos idiomas: inglés, japonés o chino (simplificado).</span><span class="sxs-lookup"><span data-stu-id="a3506-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="a3506-121">Compruebe que estén instaladas las actualizaciones importantes y esenciales.</span><span class="sxs-lookup"><span data-stu-id="a3506-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="a3506-122">**HPC Pack 2012 R2** - [Descargue](http://go.microsoft.com/fwlink/p/?linkid=328024) el paquete de instalación completo de la última versión gratis y copie los archivos en el equipo del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="a3506-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="a3506-123">Elija los archivos de instalación que tengan el mismo idioma que su instalación de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3506-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="a3506-124">Si desea usar HPC Pack 2016, en lugar de HPC Pack 2012 R2, se necesita configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="a3506-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="a3506-125">Consulte las [instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a3506-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="a3506-126">**Cuenta de dominio**. Esta cuenta se debe configurar con permisos de administrador local en el nodo principal para instalar HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a3506-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="a3506-127">**Conectividad TCP en el puerto 443** desde el nodo principal a Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="a3506-128">Instalación de HPC Pack en el nodo principal</span><span class="sxs-lookup"><span data-stu-id="a3506-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="a3506-129">En primer lugar, debe instalar Microsoft HPC Pack en un equipo local con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a3506-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="a3506-130">Este equipo se convierte en el nodo principal del clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="a3506-131">Inicie sesión en el nodo principal usando una cuenta de dominio que tenga permisos de administrador local.</span><span class="sxs-lookup"><span data-stu-id="a3506-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="a3506-132">Inicie el asistente de instalación de HPC Pack ejecutando el archivo Setup.exe desde los archivos de instalación de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a3506-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="a3506-133">En la pantalla de **instalación de HPC Pack 2012 R2**, haga clic en **Nueva instalación o agregar características a una instalación existente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![Instalación de HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="a3506-135">En la página **Contrato de usuario de software de Microsoft**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="a3506-136">En la página **Seleccionar tipo de instalación**, haga clic en **Crear un clúster de HPC creando un nodo principal** y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="a3506-137">El asistente ejecuta varias pruebas de preinstalación.</span><span class="sxs-lookup"><span data-stu-id="a3506-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="a3506-138">Haga clic en **Siguiente** on the **Installation Rules** si se pasan todas las pruebas.</span><span class="sxs-lookup"><span data-stu-id="a3506-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="a3506-139">Si no, revise la información proporcionada y realice los cambios necesarios en su entorno.</span><span class="sxs-lookup"><span data-stu-id="a3506-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="a3506-140">A continuación, ejecute las pruebas de nuevo o, si fuera necesario, vuelva a iniciar el asistente de instalación.</span><span class="sxs-lookup"><span data-stu-id="a3506-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="a3506-141">En la página **Configuración de la base de datos de HPC**, asegúrese de haber seleccionado **Nodo principal** en todas las bases de datos de HPC y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configuración de la base de datos][install_hpc4]

8. <span data-ttu-id="a3506-143">Acepte las opciones seleccionadas de forma predeterminada en las páginas restantes del asistente.</span><span class="sxs-lookup"><span data-stu-id="a3506-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="a3506-144">En la página **Instalar componentes** requeridos, haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Instalar][install_hpc6]

9. <span data-ttu-id="a3506-146">Cuando finalice la instalación, desactive **Iniciar Administrador de clústeres de HPC** y, a continuación, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="a3506-147">(El Administrador de clústeres HPC se inicia en un paso posterior).</span><span class="sxs-lookup"><span data-stu-id="a3506-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finalizar][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="a3506-149">Preparación de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="a3506-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="a3506-150">Lleve a cabo estos pasos en [Azure Portal](https://portal.azure.com) con la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="a3506-151">Una vez que complete estos pasos, puede implementar los nodos de Azure desde el nodo principal local.</span><span class="sxs-lookup"><span data-stu-id="a3506-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="a3506-152">Anote también el Id. de la suscripción de Azure, ya que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="a3506-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="a3506-153">Busque el identificador en las **suscripciones** del portal.</span><span class="sxs-lookup"><span data-stu-id="a3506-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="a3506-154">Cargar el certificado de administración predeterminado</span><span class="sxs-lookup"><span data-stu-id="a3506-154">Upload the default management certificate</span></span>
<span data-ttu-id="a3506-155">HPC Pack instala un certificado autofirmado en el nodo principal, llamado Default Microsoft HPC Azure Management, que podrá cargar como certificado de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="a3506-156">Este certificado se proporciona para pruebas y las implementaciones de prueba de concepto para proteger la conexión entre el nodo principal y Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="a3506-157">En el equipo del nodo principal, inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3506-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a3506-158">Haga clic en **Suscripciones** > *nombre_de_la_suscripción*.</span><span class="sxs-lookup"><span data-stu-id="a3506-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="a3506-159">Haga clic en **Certificados de administración** > **Cargar**.4.</span><span class="sxs-lookup"><span data-stu-id="a3506-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="a3506-160">Busque el archivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer en el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="a3506-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="a3506-161">Luego, haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="a3506-162">El certificado **Administración de HPC de Azure predeterminado** aparece en la lista de certificados de administración.</span><span class="sxs-lookup"><span data-stu-id="a3506-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="a3506-163">Crear un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="a3506-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="a3506-164">Para conseguir un mejor rendimiento, cree el servicio en la nube y (en un paso posterior) la cuenta de almacenamiento en la misma región geográfica.</span><span class="sxs-lookup"><span data-stu-id="a3506-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="a3506-165">En el portal, haga clic en **Servicios en la nube (clásico)** > **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="a3506-166">Escriba un nombre DNS para el servicio, elija un grupo de recursos y una ubicación y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a3506-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="a3506-167">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a3506-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="a3506-168">En el portal, haga clic en **Cuentas de almacenamiento (clásico)** > **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="a3506-169">Escriba un nombre para la cuenta y seleccione el modelo de implementación **clásica**.</span><span class="sxs-lookup"><span data-stu-id="a3506-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="a3506-170">Elija un grupo de recursos y una ubicación y deje los valores predeterminados de las demás opciones.</span><span class="sxs-lookup"><span data-stu-id="a3506-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="a3506-171">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a3506-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="a3506-172">Configuración del nodo principal</span><span class="sxs-lookup"><span data-stu-id="a3506-172">Configure the head node</span></span>
<span data-ttu-id="a3506-173">Para usar el administrador de clústeres de HPC para implementar nodos de Azure y enviar trabajos, primero debe seguir los pasos necesarios para configurar el clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="a3506-174">En el nodo principal, inicie el administrador de clústeres de HPC.</span><span class="sxs-lookup"><span data-stu-id="a3506-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="a3506-175">Si aparece el cuadro de diálogo **Select Head Node** (Seleccionar nodo principal), haga clic en **Local Computer** (Equipo local).</span><span class="sxs-lookup"><span data-stu-id="a3506-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="a3506-176">Aparecerá la **lista de tareas pendientes de implementación** .</span><span class="sxs-lookup"><span data-stu-id="a3506-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="a3506-177">En **Tareas de implementación necesarias**, haga clic en **Configurar la red**.</span><span class="sxs-lookup"><span data-stu-id="a3506-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configuración de la red][config_hpc2]

3. <span data-ttu-id="a3506-179">En el Asistente para configuración de red, seleccione **Todos los nodos solo en una red empresarial** (topología 5).</span><span class="sxs-lookup"><span data-stu-id="a3506-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="a3506-180">Esta configuración de red es la más sencilla para fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="a3506-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topología 5][config_hpc3]
   
4. <span data-ttu-id="a3506-182">Haga clic en **Siguiente** para aceptar los valores predeterminados de las páginas restantes del asistente.</span><span class="sxs-lookup"><span data-stu-id="a3506-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="a3506-183">A continuación, en la pestaña **Revisar**, haga clic en **Configurar** para completar la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="a3506-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="a3506-184">En la **lista de tareas pendientes de implementación**, haga clic en **Proporcionar credenciales de instalación**.</span><span class="sxs-lookup"><span data-stu-id="a3506-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="a3506-185">En el cuadro de diálogo **Credenciales de instalación** , escriba las credenciales de la cuenta de dominio que ha usado para instalar HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a3506-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="a3506-186">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-186">Then click **OK**.</span></span> 
   
    ![Credenciales de instalación][config_hpc6]
   
7. <span data-ttu-id="a3506-188">En la **lista de tareas pendientes de implementación**, haga clic en **Configurar la nomenclatura de los nuevos nodos**.</span><span class="sxs-lookup"><span data-stu-id="a3506-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="a3506-189">En el cuadro de diálogo **Especificar serie de nomenclatura de nodos**, acepte la serie de nomenclatura predeterminada y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="a3506-190">Complete este paso incluso si se asigna automáticamente un nombre a los nodos de Azure que agrega en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3506-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Nomenclatura de nodos][config_hpc8]
   
9. <span data-ttu-id="a3506-192">En la **lista de tareas pendientes de implementación**, haga clic en **Crear una plantilla de nodo**.</span><span class="sxs-lookup"><span data-stu-id="a3506-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="a3506-193">Más adelante en el tutorial usará la plantilla de nodo para agregar nodos de Azure al clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="a3506-194">En el asistente de creación de plantillas de nodo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a3506-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="a3506-195">a.</span><span class="sxs-lookup"><span data-stu-id="a3506-195">a.</span></span> <span data-ttu-id="a3506-196">En la página **Elegir el tipo de plantilla de nodo**, haga clic en la **plantilla de nodo de Microsoft Azure** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc10]
    
    <span data-ttu-id="a3506-198">b.</span><span class="sxs-lookup"><span data-stu-id="a3506-198">b.</span></span> <span data-ttu-id="a3506-199">Haga clic en **Siguiente** para aceptar el nombre de plantilla predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a3506-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="a3506-200">c.</span><span class="sxs-lookup"><span data-stu-id="a3506-200">c.</span></span> <span data-ttu-id="a3506-201">En la página **Proporcionar información de suscripción** , especifique su identificador de suscripción de Azure (disponible en la información de cuenta de Azure).</span><span class="sxs-lookup"><span data-stu-id="a3506-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="a3506-202">Luego, en **Certificado de administración**, busque **Default Microsoft HPC Azure Management**.</span><span class="sxs-lookup"><span data-stu-id="a3506-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="a3506-203">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-203">Then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc12]
    
    <span data-ttu-id="a3506-205">d.</span><span class="sxs-lookup"><span data-stu-id="a3506-205">d.</span></span> <span data-ttu-id="a3506-206">En la pagina **Proporcionar información del servicio** , seleccione el servicio en la nube y la cuenta de almacenamiento que ha creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a3506-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="a3506-207">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-207">Then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc13]
    
    <span data-ttu-id="a3506-209">e.</span><span class="sxs-lookup"><span data-stu-id="a3506-209">e.</span></span> <span data-ttu-id="a3506-210">Haga clic en **Siguiente** para aceptar los valores predeterminados de las páginas restantes del asistente.</span><span class="sxs-lookup"><span data-stu-id="a3506-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="a3506-211">A continuación, en la pestaña **Revisar**, haga clic en **Crear** para crear la plantilla de nodo.</span><span class="sxs-lookup"><span data-stu-id="a3506-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a3506-212">De forma predeterminada, la plantilla de nodo de Azure incluye la configuración para que pueda iniciar (aprovisionar) y detener los nodos manualmente con el Administrador de clústeres HPC.</span><span class="sxs-lookup"><span data-stu-id="a3506-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="a3506-213">También puede configurar una programación para iniciar y detener los nodos de Azure automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a3506-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="a3506-214">Incorporación de nodos de Azure al clúster</span><span class="sxs-lookup"><span data-stu-id="a3506-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="a3506-215">Ahora use la plantilla de nodo para agregar nodos de Azure al clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="a3506-216">Al agregar los nodos al clúster, su información de configuración se almacena para que pueda iniciarlos (aprovisionarlos) en cualquier momento en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a3506-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="a3506-217">Su suscripción solo se carga para los nodos de Azure después de que las instancias se ejecuten en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a3506-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="a3506-218">Siga estos pasos para agregar dos nodos pequeños.</span><span class="sxs-lookup"><span data-stu-id="a3506-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="a3506-219">En el Administrador de clústeres HPC, haga clic en **Administración de nodos** (llamada **Administración de recursos** en versiones recientes de HPC Pack) > **Agregar nodo**.</span><span class="sxs-lookup"><span data-stu-id="a3506-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Agregar nodo][add_node1]

2. <span data-ttu-id="a3506-221">En el Asistente para agregar nodo, en la página **Select Deployment Method** (Seleccionar método de implementación), haga clic en **Add Windows Azure nodes** (Agregar nodos de Microsoft Azure) y, a continuación, en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Agregar un nodo de Azure][add_node1_1]

3. <span data-ttu-id="a3506-223">En la página **Especificar nodos nuevos**, seleccione la plantilla de nodo de Azure que creó anteriormente (llamada de manera predeterminada **Default AzureNode Template**).</span><span class="sxs-lookup"><span data-stu-id="a3506-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="a3506-224">A continuación, especifique **2** nodos de tamaño **pequeño** y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a3506-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Especificar los nodos][add_node2]
   
4. <span data-ttu-id="a3506-226">En la página **Finalización del asistente para agregar nodos**, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="a3506-227">Ahora aparecerán dos nodos llamados **AzureCN-0001** y **AzureCN-0002** en el administrador de clústeres de HPC.</span><span class="sxs-lookup"><span data-stu-id="a3506-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="a3506-228">Ambos tienen el estado **No implementado** .</span><span class="sxs-lookup"><span data-stu-id="a3506-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Nodos agregados][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="a3506-230">Inicio de los nodos de Azure</span><span class="sxs-lookup"><span data-stu-id="a3506-230">Start the Azure nodes</span></span>
<span data-ttu-id="a3506-231">Cuando quiera usar los recursos del clúster de Azure, use el administrador de clústeres de HPC para iniciar (aprovisionar) los nodos de Azure y conectarlos a la red.</span><span class="sxs-lookup"><span data-stu-id="a3506-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="a3506-232">En el Administrador de clústeres HPC, haga clic en **Administración de nodos** (llamada **Administración de recursos** en versiones recientes de HPC Pack) y seleccione los nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="a3506-233">Haga clic en **Inicio** y, luego, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a3506-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Iniciar los nodos][add_node4]
   
    <span data-ttu-id="a3506-235">Los nodos pasan al estado **Aprovisionamiento** .</span><span class="sxs-lookup"><span data-stu-id="a3506-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="a3506-236">Consulte el registro de aprovisionamiento para realizar el seguimiento del progreso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="a3506-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Aprovisionar nodos][add_node6]

3. <span data-ttu-id="a3506-238">Después de unos minutos, los nodos de Azure terminan de aprovisionarse y pasan al estado **Sin conexión** .</span><span class="sxs-lookup"><span data-stu-id="a3506-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="a3506-239">En este estado, las instancias de rol se ejecutan pero todavía no pueden aceptar trabajos de clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="a3506-240">Para confirmar que las instancias de rol se ejecutan, en Azure Portal, haga clic en **Servicios en la nube (clásico)** > *nombre_del_servicio_en_la_nube*.</span><span class="sxs-lookup"><span data-stu-id="a3506-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="a3506-241">Debería ver dos instancias (nodos) de **HpcWorkerRole** en ejecución en el servicio.</span><span class="sxs-lookup"><span data-stu-id="a3506-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="a3506-242">HPC Pack también implementa automáticamente dos instancias **HpcProxy** (tamaño medio) para controlar la comunicación entre el nodo principal y Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Instancias en ejecución][view_instances1]

5. <span data-ttu-id="a3506-244">Para conectar los nodos de Azure y que ejecuten los trabajos de clúster, seleccione los nodos, haga clic con el botón secundario y, a continuación, haga clic en **Poner en línea**.</span><span class="sxs-lookup"><span data-stu-id="a3506-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nodos desconectados][add_node7]
   
    <span data-ttu-id="a3506-246">El administrador de clústeres de HPC indica que los nodos están en estado **En línea** .</span><span class="sxs-lookup"><span data-stu-id="a3506-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="a3506-247">Ejecución de un comando en el clúster</span><span class="sxs-lookup"><span data-stu-id="a3506-247">Run a command across the cluster</span></span>
<span data-ttu-id="a3506-248">Para comprobar la instalación, use el comando **clusrun** de HPC Pack para ejecutar un comando o una aplicación en uno o varios nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="a3506-249">Por ejemplo, use **clusrun** para obtener la configuración IP de los nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="a3506-250">En el nodo principal, abra un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="a3506-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="a3506-251">Escriba el siguiente comando: </span><span class="sxs-lookup"><span data-stu-id="a3506-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="a3506-252">Si se le solicita, escriba la contraseña de administrador del clúster.</span><span class="sxs-lookup"><span data-stu-id="a3506-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="a3506-253">Debería ver un resultado del comando similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="a3506-253">You should see command output similar to the following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="a3506-255">Ejecución de un trabajo de prueba</span><span class="sxs-lookup"><span data-stu-id="a3506-255">Run a test job</span></span>
<span data-ttu-id="a3506-256">Ahora, envíe un trabajo de prueba que se ejecute en el clúster híbrido.</span><span class="sxs-lookup"><span data-stu-id="a3506-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="a3506-257">Este ejemplo es un trabajo simple de barrido paramétrico (un tipo de cálculo intrínsecamente paralelo).</span><span class="sxs-lookup"><span data-stu-id="a3506-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="a3506-258">En este ejemplo se ejecutan subtareas que agregan un entero a sí mismo con el comando **set /a** .</span><span class="sxs-lookup"><span data-stu-id="a3506-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="a3506-259">Todos los nodos del clúster contribuyen a finalizar las subtareas para enteros del 1 al 100.</span><span class="sxs-lookup"><span data-stu-id="a3506-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="a3506-260">En el Administrador de clústeres HPC, haga clic en **Administración de trabajos** > **Nuevo trabajo de barrido paramétrico**.</span><span class="sxs-lookup"><span data-stu-id="a3506-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nuevo trabajo][test_job1]

2. <span data-ttu-id="a3506-262">En el cuadro de diálogo **Nuevo trabajo de barrido paramétrico**, en la **línea de comandos**, escriba `set /a *+*` (sobrescribiendo la línea de comandos predeterminada que aparezca).</span><span class="sxs-lookup"><span data-stu-id="a3506-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="a3506-263">Deje los valores predeterminados para el resto de la configuración y, a continuación, haga clic en **Enviar** para enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="a3506-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Barrido paramétrico][param_sweep1]

3. <span data-ttu-id="a3506-265">Cuando termine el trabajo, haga doble clic en el trabajo **Mi tarea de barrido** .</span><span class="sxs-lookup"><span data-stu-id="a3506-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="a3506-266">Haga clic en **Ver tareas**y, a continuación, haga clic en una subtarea para ver la salida calculada de dicha subtarea.</span><span class="sxs-lookup"><span data-stu-id="a3506-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Resultados de la tarea][view_job361]

5. <span data-ttu-id="a3506-268">Para ver qué nodo ha realizado el cálculo en esa subtarea, haga clic en **Nodos asignados**.</span><span class="sxs-lookup"><span data-stu-id="a3506-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="a3506-269">(Su clúster podría mostrar un nombre de nodo diferente).</span><span class="sxs-lookup"><span data-stu-id="a3506-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultados de la tarea][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="a3506-271">Detención de los nodos de Azure</span><span class="sxs-lookup"><span data-stu-id="a3506-271">Stop the Azure nodes</span></span>
<span data-ttu-id="a3506-272">Después de probar el clúster, detenga los nodos de Azure e impida que se produzcan cargas innecesarias en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="a3506-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="a3506-273">Este paso detiene el servicio en la nube y quitan las instancias de rol de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="a3506-274">En el Administrador de clústeres HPC, en **Administración de nodos** (llamada **Administración de recursos** en versiones anteriores de HPC Pack), seleccione los dos nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3506-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="a3506-275">Luego, haga clic en **Detener**.</span><span class="sxs-lookup"><span data-stu-id="a3506-275">Then, click **Stop**.</span></span>
   
    ![Detener los nodos][stop_node1]

2. <span data-ttu-id="a3506-277">En el cuadro de diálogo **Stop Windows Azure nodes** (Detener nodos de Microsoft Azure), haga clic en **Detener**.</span><span class="sxs-lookup"><span data-stu-id="a3506-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="a3506-278">Los nodos pasan al estado **En detención** .</span><span class="sxs-lookup"><span data-stu-id="a3506-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="a3506-279">Después de unos minutos, el administrador de clústeres de HPC indica que los nodos tienen el estado **No implementado**.</span><span class="sxs-lookup"><span data-stu-id="a3506-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Nodos no implementados][stop_node4]

4. <span data-ttu-id="a3506-281">Para confirmar que las instancias de rol ya no se ejecutan en Azure, en Azure Portal, haga clic en **Servicios en la nube (clásico)** > *nombre_del_servicio_en_la_nube*.</span><span class="sxs-lookup"><span data-stu-id="a3506-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="a3506-282">No se implementa instancias en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a3506-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="a3506-283">Con esto finaliza el tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3506-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3506-284">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a3506-284">Next steps</span></span>
* <span data-ttu-id="a3506-285">Explore la documentación correspondiente a [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="a3506-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="a3506-286">Para configurar una implementación híbrida de clústeres HPC Pack a mayor escala, consulte [Irrupción en instancias de rol de trabajo de Azure con Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a3506-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="a3506-287">Para ver otras formas de crear un clúster HPC Pack en Azure como, por ejemplo, el uso de plantillas de Azure Resource Manager, consulte [Opciones de clúster HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3506-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
