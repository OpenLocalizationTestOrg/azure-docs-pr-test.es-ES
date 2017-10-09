---
title: "clúster de aaaSet la híbrida de HPC Pack en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Microsoft HPC Pack y Azure tooset una copia de seguridad un pequeño, híbrida alto rendimiento informático () clúster de HPC"
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
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="a4346-103">Configuración de un clúster híbrido de informática de alto rendimiento (HPC) con nodos de proceso de Azure a petición y Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="a4346-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="a4346-104">Use Microsoft HPC Pack 2012 R2 y Azure tooset seguridad un pequeño, híbrida informática de alto rendimiento clúster (HPC).</span><span class="sxs-lookup"><span data-stu-id="a4346-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="a4346-105">clúster de Hello mostrado en este artículo está formado por un nodo principal de HPC Pack local y algunos nodos implementar a petición en un Azure servicio en la nube de proceso.</span><span class="sxs-lookup"><span data-stu-id="a4346-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="a4346-106">A continuación, puede ejecutar trabajos de proceso en clúster híbrido de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Clúster híbrido de HPC][Overview] 

<span data-ttu-id="a4346-108">Este tutorial muestra un enfoque suele llamar clúster "ráfaga toohello en la nube," aplicaciones de proceso intensivo de toorun toouse escalable, en la demanda de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="a4346-109">En este tutorial se supone que no cuenta con experiencia previa con los clústeres informáticos o con HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a4346-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="a4346-110">Está previsto toohelp solo implementar un clúster de cálculo híbrido rápidamente con fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="a4346-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="a4346-111">Para las consideraciones y toodeploy pasos clúster HPC Pack híbrido a mayor escala en un entorno de producción o toouse HPC Pack 2016, vea hello [obtener instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a4346-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="a4346-112">Para otros escenarios de HPC Pack, incluida la implementación automatizada de clústeres en máquinas virtuales de Azure, consulte [Opciones de clúster de HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4346-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4346-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a4346-113">Prerequisites</span></span>
* <span data-ttu-id="a4346-114">**Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="a4346-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="a4346-115">**Un equipo local que ejecuta Windows Server 2012 R2 o Windows Server 2012** -usar este equipo como nodo principal de Hola Hola del clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="a4346-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="a4346-116">Si todavía no tiene Windows Server, puede descargar e instalar una [versión de evaluación](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="a4346-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="a4346-117">equipo de Hello debe ser tooan Unidos a un dominio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4346-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="a4346-118">Para fines de prueba, puede configurar el equipo del nodo principal de Hola como un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="a4346-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="a4346-119">tooadd Hola rol de servidor Servicios de dominio de Active Directory y promocionar el equipo del nodo principal Hola como un controlador de dominio, consulte la documentación de Hola para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a4346-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="a4346-120">toosupport HPC Pack, sistema operativo de hello debe instalarse en uno de estos idiomas: inglés, japonés o chino (simplificado).</span><span class="sxs-lookup"><span data-stu-id="a4346-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="a4346-121">Compruebe que estén instaladas las actualizaciones importantes y esenciales.</span><span class="sxs-lookup"><span data-stu-id="a4346-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="a4346-122">**HPC Pack 2012 R2** - [descargar](http://go.microsoft.com/fwlink/p/?linkid=328024) paquete de instalación de hello para la versión más reciente de hello libre de cargo y copia Hola archivos toohello equipo del nodo principal.</span><span class="sxs-lookup"><span data-stu-id="a4346-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="a4346-123">Elija archivos de instalación de hello mismo idioma que la instalación de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a4346-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="a4346-124">Si desea toouse HPC Pack 2016 en lugar de HPC Pack 2012 R2, se necesita configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="a4346-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="a4346-125">Vea hello [obtener instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a4346-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="a4346-126">**Cuenta de dominio** -se debe configurar esta cuenta con permisos de administrador local en el nodo principal de hello tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a4346-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="a4346-127">**Conectividad TCP en el puerto 443** de hello tooAzure de nodo principal.</span><span class="sxs-lookup"><span data-stu-id="a4346-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="a4346-128">Instalar HPC Pack en el nodo principal de Hola</span><span class="sxs-lookup"><span data-stu-id="a4346-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="a4346-129">En primer lugar, debe instalar Microsoft HPC Pack en un equipo local con Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a4346-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="a4346-130">Este equipo se convierte en del nodo principal del clúster de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="a4346-131">Inicie sesión en el nodo principal de toohello con una cuenta de dominio que tenga permisos de administrador local.</span><span class="sxs-lookup"><span data-stu-id="a4346-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="a4346-132">Iniciar Hola Asistente para la instalación de HPC Pack ejecutando Setup.exe desde archivos de instalación de HPC Pack Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="a4346-133">En hello **el programa de instalación de HPC Pack 2012 R2** pantalla, haga clic en **nueva instalación o agregar nuevas características de instalación de existente tooan**.</span><span class="sxs-lookup"><span data-stu-id="a4346-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![Instalación de HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="a4346-135">En hello **página del acuerdo de usuario de Software de Microsoft**, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="a4346-136">En hello **Seleccionar tipo de instalación** página, haga clic en **crear un nuevo clúster HPC mediante la creación de un nodo principal**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="a4346-137">Asistente de Hello ejecuta varias pruebas previas a la instalación.</span><span class="sxs-lookup"><span data-stu-id="a4346-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="a4346-138">Haga clic en **siguiente** en hello **reglas de instalación** página si se superan todas las pruebas.</span><span class="sxs-lookup"><span data-stu-id="a4346-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="a4346-139">En caso contrario, revise la información de hello proporcionada y realice los cambios necesarios en su entorno.</span><span class="sxs-lookup"><span data-stu-id="a4346-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="a4346-140">A continuación, ejecutar pruebas de hello nuevo o si es necesario iniciar Hola Asistente para la instalación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="a4346-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="a4346-141">En hello **configuración de base de datos de HPC** página, asegúrese de que **nodo principal** está seleccionada para todas las bases de datos HPC y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configuración de la base de datos][install_hpc4]

8. <span data-ttu-id="a4346-143">Aceptar selecciones de predeterminado en hello las páginas restantes del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="a4346-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="a4346-144">En hello **instalar los componentes necesarios** página, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Instalación][install_hpc6]

9. <span data-ttu-id="a4346-146">Una vez finalizada la instalación de hello, desactive la opción **iniciar el Administrador de clúster de HPC** y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="a4346-147">(El Administrador de clústeres HPC se inicia en un paso posterior).</span><span class="sxs-lookup"><span data-stu-id="a4346-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Finalizar][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="a4346-149">Preparar Hola suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="a4346-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="a4346-150">Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com) con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="a4346-151">Después de completar estos pasos, puede implementar nodos de Azure desde el nodo principal de hello en local.</span><span class="sxs-lookup"><span data-stu-id="a4346-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="a4346-152">Anote también el Id. de la suscripción de Azure, ya que lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="a4346-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="a4346-153">Encuentra el Id. de hello en **suscripciones** en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="a4346-154">Cargar certificado predeterminado de administración de Hola</span><span class="sxs-lookup"><span data-stu-id="a4346-154">Upload hello default management certificate</span></span>
<span data-ttu-id="a4346-155">HPC Pack se instala un certificado autofirmado en el nodo principal de hello, denominado certificado de administración de Azure de HPC de Microsoft predeterminado hello, que puede cargar como un certificado de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="a4346-156">Este certificado se proporciona para pruebas y conexión de las implementaciones de prueba de concepto toosecure Hola entre hello Azure y el nodo principal.</span><span class="sxs-lookup"><span data-stu-id="a4346-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="a4346-157">Desde el equipo de nodo principal de hello, inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4346-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a4346-158">Haga clic en **Suscripciones** > *nombre_de_la_suscripción*.</span><span class="sxs-lookup"><span data-stu-id="a4346-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="a4346-159">Haga clic en **Certificados de administración** > **Cargar**.4.</span><span class="sxs-lookup"><span data-stu-id="a4346-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="a4346-160">Busque en el nodo principal de Hola para hello archivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="a4346-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="a4346-161">Luego, haga clic en **Cargar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="a4346-162">Hola **administración de Azure de HPC predeterminado** certificado aparece en la lista de Hola de certificados de administración.</span><span class="sxs-lookup"><span data-stu-id="a4346-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="a4346-163">Crear un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="a4346-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="a4346-164">Para obtener el mejor rendimiento, crear servicio en la nube hello y cuenta de almacenamiento de hello (en un paso posterior) en hello misma región geográfica.</span><span class="sxs-lookup"><span data-stu-id="a4346-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="a4346-165">En el portal de hello, haga clic en **servicios (clásico) en la nube** > **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="a4346-166">Escriba un nombre DNS para el servicio de hello, elija un grupo de recursos y una ubicación y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="a4346-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="a4346-167">Creación de una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a4346-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="a4346-168">En el portal de hello, haga clic en **cuentas de almacenamiento (clásica)** > **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="a4346-169">Escriba un nombre para la cuenta de hello y seleccione hello **clásico** modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="a4346-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="a4346-170">Elija un grupo de recursos y una ubicación y deje los valores predeterminados de las demás opciones.</span><span class="sxs-lookup"><span data-stu-id="a4346-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="a4346-171">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a4346-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="a4346-172">Configurar el nodo principal de Hola</span><span class="sxs-lookup"><span data-stu-id="a4346-172">Configure hello head node</span></span>
<span data-ttu-id="a4346-173">Administrador de clústeres HPC toodeploy toouse nodos de Azure y los trabajos de toosubmit, en primer lugar realizar algunos pasos de configuración de clúster necesarios.</span><span class="sxs-lookup"><span data-stu-id="a4346-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="a4346-174">En el nodo principal de hello, inicie el Administrador de clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="a4346-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="a4346-175">Si hello **Seleccionar nodo principal** aparece el cuadro de diálogo, haga clic en **equipo Local**.</span><span class="sxs-lookup"><span data-stu-id="a4346-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="a4346-176">Hola **lista de tareas de implementación** aparece.</span><span class="sxs-lookup"><span data-stu-id="a4346-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="a4346-177">En **Tareas de implementación necesarias**, haga clic en **Configurar la red**.</span><span class="sxs-lookup"><span data-stu-id="a4346-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configuración de la red][config_hpc2]

3. <span data-ttu-id="a4346-179">En el Asistente para configuración de red de hello, seleccione **todos los nodos solo en una red empresarial** (topología 5).</span><span class="sxs-lookup"><span data-stu-id="a4346-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="a4346-180">Esta configuración de red es más sencillo para fines de demostración de hello.</span><span class="sxs-lookup"><span data-stu-id="a4346-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topología 5][config_hpc3]
   
4. <span data-ttu-id="a4346-182">Haga clic en **siguiente** tooaccept valores predeterminados Hola restantes páginas del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="a4346-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="a4346-183">A continuación, en hello **revisión** , haga clic en **configurar** configuración de red de toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="a4346-184">Hola **lista de tareas de implementación**, haga clic en **proporcione las credenciales de instalación**.</span><span class="sxs-lookup"><span data-stu-id="a4346-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="a4346-185">Hola **credenciales de instalación** cuadro de diálogo, escriba hello las credenciales de cuenta de dominio de Hola que usa tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a4346-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="a4346-186">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-186">Then click **OK**.</span></span> 
   
    ![Credenciales de instalación][config_hpc6]
   
7. <span data-ttu-id="a4346-188">Hola **lista de tareas de implementación**, haga clic en **configurar Hola denominación de nuevos nodos**.</span><span class="sxs-lookup"><span data-stu-id="a4346-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="a4346-189">Hola **especificar serie de nombres de nodo** diálogo cuadro, acepte el predeterminado de hello nomenclatura serie y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="a4346-190">Complete este paso, aunque hello nodos de Azure que agregue en este tutorial se asignan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a4346-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Nomenclatura de nodos][config_hpc8]
   
9. <span data-ttu-id="a4346-192">Hola **lista de tareas de implementación**, haga clic en **crear una plantilla de nodo**.</span><span class="sxs-lookup"><span data-stu-id="a4346-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="a4346-193">Más adelante en el tutorial de hello, usar clúster de toohello Hola nodos plantilla tooadd nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="a4346-194">En Hola Asistente Crear plantilla de nodo, haga lo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="a4346-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="a4346-195">a.</span><span class="sxs-lookup"><span data-stu-id="a4346-195">a.</span></span> <span data-ttu-id="a4346-196">En hello **Elegir tipo de plantilla de nodo** página, haga clic en **plantilla de nodo de Windows Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc10]
    
    <span data-ttu-id="a4346-198">b.</span><span class="sxs-lookup"><span data-stu-id="a4346-198">b.</span></span> <span data-ttu-id="a4346-199">Haga clic en **siguiente** nombre de plantilla predeterminado de tooaccept Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="a4346-200">c.</span><span class="sxs-lookup"><span data-stu-id="a4346-200">c.</span></span> <span data-ttu-id="a4346-201">En hello **proporcionan información de suscripción** página, escriba el identificador de suscripción de Azure (está disponible en la información de cuenta de Azure).</span><span class="sxs-lookup"><span data-stu-id="a4346-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="a4346-202">Luego, en **Certificado de administración**, busque **Default Microsoft HPC Azure Management**.</span><span class="sxs-lookup"><span data-stu-id="a4346-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="a4346-203">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-203">Then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc12]
    
    <span data-ttu-id="a4346-205">d.</span><span class="sxs-lookup"><span data-stu-id="a4346-205">d.</span></span> <span data-ttu-id="a4346-206">En hello **proporcionar información del servicio** página, servicio de nube seleccione hello y cuenta de almacenamiento de Hola que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a4346-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="a4346-207">A continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-207">Then click **Next**.</span></span>
    
    ![Plantilla de nodo][config_hpc13]
    
    <span data-ttu-id="a4346-209">e.</span><span class="sxs-lookup"><span data-stu-id="a4346-209">e.</span></span> <span data-ttu-id="a4346-210">Haga clic en **siguiente** tooaccept valores predeterminados Hola restantes páginas del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="a4346-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="a4346-211">A continuación, en hello **revisión** , haga clic en **crear** plantilla de nodo de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a4346-212">De forma predeterminada, Hola nodos de Azure plantilla incluyen la configuración para toostart (aprovisionar) y los nodos de hello detener manualmente, mediante el Administrador de clúster de HPC.</span><span class="sxs-lookup"><span data-stu-id="a4346-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="a4346-213">Opcionalmente, puede configurar una programación toostart y detener Hola automáticamente los nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="a4346-214">Agregar nodos de Azure toohello clúster</span><span class="sxs-lookup"><span data-stu-id="a4346-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="a4346-215">Ahora use clúster de toohello Hola nodos plantilla tooadd nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="a4346-216">Agregar clúster de hello nodos toohello almacena su información de configuración para que pueda iniciar (aprovisionar) usarlas en cualquier momento en el servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="a4346-217">Su suscripción solo obtiene cobra por nodos de Azure después de que se ejecutan instancias de Hola Hola del servicio en nube.</span><span class="sxs-lookup"><span data-stu-id="a4346-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="a4346-218">Siga estos pasos tooadd dos pequeños los nodos.</span><span class="sxs-lookup"><span data-stu-id="a4346-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="a4346-219">En el Administrador de clústeres HPC, haga clic en **Administración de nodos** (llamada **Administración de recursos** en versiones recientes de HPC Pack) > **Agregar nodo**.</span><span class="sxs-lookup"><span data-stu-id="a4346-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Agregar nodo][add_node1]

2. <span data-ttu-id="a4346-221">En Hola Asistente para agregar nodos, en hello **Seleccionar método de implementación** página, haga clic en **nodos de agregar Windows Azure**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Agregar un nodo de Azure][add_node1_1]

3. <span data-ttu-id="a4346-223">En hello **especificar nuevos nodos** página, plantilla de nodo de Azure Hola select que creó anteriormente (llamado de forma predeterminada **plantilla predeterminada de AzureNode**).</span><span class="sxs-lookup"><span data-stu-id="a4346-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="a4346-224">A continuación, especifique **2** nodos de tamaño **pequeño** y, a continuación, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a4346-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Especificar los nodos][add_node2]
   
4. <span data-ttu-id="a4346-226">En hello **finalización Hola Asistente para agregar nodos** página, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="a4346-227">Ahora aparecerán dos nodos llamados **AzureCN-0001** y **AzureCN-0002** en el administrador de clústeres de HPC.</span><span class="sxs-lookup"><span data-stu-id="a4346-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="a4346-228">Ambos están en hello **no implementado** estado.</span><span class="sxs-lookup"><span data-stu-id="a4346-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Nodos agregados][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="a4346-230">Iniciar Hola nodos de Azure</span><span class="sxs-lookup"><span data-stu-id="a4346-230">Start hello Azure nodes</span></span>
<span data-ttu-id="a4346-231">Si desea toouse recursos de clúster de hello en Azure, use el Administrador de clústeres de HPC toostart (aprovisionar) Hola nodos de Azure y ponen en línea.</span><span class="sxs-lookup"><span data-stu-id="a4346-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="a4346-232">Haga clic en Administrador de clústeres de HPC, **administración de nodos** (denominado **administración de recursos** en las versiones actuales de HPC Pack), y seleccione Hola nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="a4346-233">Haga clic en **Inicio** y, luego, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a4346-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Iniciar los nodos][add_node4]
   
    <span data-ttu-id="a4346-235">nodos de Hello transición toohello **Provisioning** estado.</span><span class="sxs-lookup"><span data-stu-id="a4346-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="a4346-236">Hola de vista aprovisionamiento Hola de tootrack registro aprovisionamiento de progreso.</span><span class="sxs-lookup"><span data-stu-id="a4346-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Aprovisionar nodos][add_node6]

3. <span data-ttu-id="a4346-238">Después de unos minutos, hello nodos de Azure finalizar el aprovisionamiento y se encuentran en hello **Offline** estado.</span><span class="sxs-lookup"><span data-stu-id="a4346-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="a4346-239">En este estado, instancias de rol de hello están ejecutando pero aún no pueden aceptar trabajos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a4346-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="a4346-240">tooconfirm que Hola instancias de rol se está ejecutando, Hola portal de Azure, haga clic en **servicios en la nube (clásico)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="a4346-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="a4346-241">Debería ver dos **HpcWorkerRole** instancias (nodos) que se ejecutan en el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="a4346-242">HPC Pack automáticamente también implementa dos **HpcProxy** instancias de comunicación de toohandle (tamaño medio) entre el nodo principal de Hola y Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Instancias en ejecución][view_instances1]

5. <span data-ttu-id="a4346-244">nodos de Azure de hello toobring toorun en línea clúster trabajos, seleccione Hola nodos, menú contextual y, a continuación, haga clic en **poner en conexión**.</span><span class="sxs-lookup"><span data-stu-id="a4346-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nodos desconectados][add_node7]
   
    <span data-ttu-id="a4346-246">Administrador de clústeres HPC indica que los nodos de hello en hello **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="a4346-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="a4346-247">Ejecutar un comando en el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="a4346-247">Run a command across hello cluster</span></span>
<span data-ttu-id="a4346-248">instalación de hello toocheck, use Hola HPC Pack **clusrun** comando toorun un comando o una aplicación en uno o más nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="a4346-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="a4346-249">Como ejemplo sencillo, use **clusrun** tooget configuración de IP Hola Hola nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="a4346-250">En el nodo principal de hello, abra un símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="a4346-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="a4346-251">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a4346-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="a4346-252">Si se le solicita, escriba la contraseña de administrador del clúster.</span><span class="sxs-lookup"><span data-stu-id="a4346-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="a4346-253">Debería ver la salida del comando siguiente de toohello similar.</span><span class="sxs-lookup"><span data-stu-id="a4346-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="a4346-255">Ejecución de un trabajo de prueba</span><span class="sxs-lookup"><span data-stu-id="a4346-255">Run a test job</span></span>
<span data-ttu-id="a4346-256">Ahora, envíe un trabajo de prueba que se ejecuta en el clúster de hello híbrido.</span><span class="sxs-lookup"><span data-stu-id="a4346-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="a4346-257">Este ejemplo es un trabajo simple de barrido paramétrico (un tipo de cálculo intrínsecamente paralelo).</span><span class="sxs-lookup"><span data-stu-id="a4346-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="a4346-258">En este ejemplo se ejecuta subtareas que agregar una tooitself entero mediante hello **establecer /a** comando.</span><span class="sxs-lookup"><span data-stu-id="a4346-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="a4346-259">Todos los nodos Hola Hola clúster contribuyen toofinishing Hola subtareas para números enteros de 1 too100.</span><span class="sxs-lookup"><span data-stu-id="a4346-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="a4346-260">En el Administrador de clústeres HPC, haga clic en **Administración de trabajos** > **Nuevo trabajo de barrido paramétrico**.</span><span class="sxs-lookup"><span data-stu-id="a4346-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nuevo trabajo][test_job1]

2. <span data-ttu-id="a4346-262">Hola **nuevo trabajo de barrido paramétrico** cuadro de diálogo **línea de comandos**, tipo `set /a *+*` (sobrescribiendo la línea de comandos de hello predeterminada que aparece).</span><span class="sxs-lookup"><span data-stu-id="a4346-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="a4346-263">Deje los valores predeterminados para hello restantes de la configuración y, a continuación, haga clic en **enviar** trabajo de hello toosubmit.</span><span class="sxs-lookup"><span data-stu-id="a4346-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Barrido paramétrico][param_sweep1]

3. <span data-ttu-id="a4346-265">Cuando finaliza el trabajo de hello, haga doble clic en hello **mi tarea de barrido** trabajo.</span><span class="sxs-lookup"><span data-stu-id="a4346-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="a4346-266">Haga clic en **tareas vista**y, a continuación, haga clic en una salida de hello calculado tooview subtarea de esa subtarea.</span><span class="sxs-lookup"><span data-stu-id="a4346-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Resultados de la tarea][view_job361]

5. <span data-ttu-id="a4346-268">toosee qué nodo realiza el cálculo de hello esa subtarea, haga clic en **asignar nodos**.</span><span class="sxs-lookup"><span data-stu-id="a4346-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="a4346-269">(Su clúster podría mostrar un nombre de nodo diferente).</span><span class="sxs-lookup"><span data-stu-id="a4346-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultados de la tarea][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="a4346-271">Detener Hola nodos de Azure</span><span class="sxs-lookup"><span data-stu-id="a4346-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="a4346-272">Después de probar clúster hello, detener tooyour cuenta de hello nodos de Azure tooavoid cobros innecesarios.</span><span class="sxs-lookup"><span data-stu-id="a4346-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="a4346-273">Este paso detiene el servicio de nube de Hola y quite instancias de rol de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="a4346-274">En el Administrador de clústeres HPC, en **Administración de nodos** (llamada **Administración de recursos** en versiones anteriores de HPC Pack), seleccione los dos nodos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4346-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="a4346-275">Luego, haga clic en **Detener**.</span><span class="sxs-lookup"><span data-stu-id="a4346-275">Then, click **Stop**.</span></span>
   
    ![Detener los nodos][stop_node1]

2. <span data-ttu-id="a4346-277">Hola **nodos detener Windows Azure** cuadro de diálogo, haga clic en **detener**.</span><span class="sxs-lookup"><span data-stu-id="a4346-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="a4346-278">nodos de Hello transición toohello **detener** estado.</span><span class="sxs-lookup"><span data-stu-id="a4346-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="a4346-279">Después de unos minutos, el Administrador de clústeres de HPC muestra que son nodos de hello **no implementado**.</span><span class="sxs-lookup"><span data-stu-id="a4346-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Nodos no implementados][stop_node4]

4. <span data-ttu-id="a4346-281">Hola a tooconfirm que instancias de rol de hello ya no se ejecutan en Azure, en haga clic en de portal, Azure **servicios (clásico) en la nube** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="a4346-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="a4346-282">No hay instancias se implementan en el entorno de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="a4346-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="a4346-283">Con esto finaliza el tutorial de Hola.</span><span class="sxs-lookup"><span data-stu-id="a4346-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4346-284">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4346-284">Next steps</span></span>
* <span data-ttu-id="a4346-285">Examinar la documentación de Hola para [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="a4346-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="a4346-286">Consulte tooset de una implementación de clúster de HPC Pack a mayor escala, híbrida [tooAzure instancias de rol de trabajo con Microsoft HPC Pack en ráfagas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a4346-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="a4346-287">Para otro toocreate de formas de un clúster de HPC Pack en Azure, incluido con plantillas de Azure Resource Manager, consulte [opciones de clúster HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a4346-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


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
