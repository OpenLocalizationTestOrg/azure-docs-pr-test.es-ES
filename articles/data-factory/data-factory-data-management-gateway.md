---
title: "puerta de enlace de administración de factoría de datos aaaData | Documentos de Microsoft"
description: Configurar una puerta de enlace de datos toomove datos entre hello y local en la nube. Utilice Data Management Gateway en toomove Data Factory de Azure los datos.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="4dc69-104">Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="4dc69-104">Data Management Gateway</span></span>
<span data-ttu-id="4dc69-105">Hola Data management gateway es un agente de cliente que debe instalar en los datos de toocopy del entorno local entre los almacenes de datos en la nube y locales.</span><span class="sxs-lookup"><span data-stu-id="4dc69-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="4dc69-106">Hola de datos locales almacenes compatibles con factoría de datos se muestran en hello [admite orígenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sección.</span><span class="sxs-lookup"><span data-stu-id="4dc69-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="4dc69-107">En este artículo complementa tutorial Hola Hola [mover datos entre local y nube almacenes de datos](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="4dc69-108">En el tutorial de hello, crear una canalización que utiliza datos de toomove de puerta de enlace de Hola de una base de datos de SQL Server local tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="4dc69-109">Este artículo proporciona detallada información detallada acerca de la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="4dc69-110">Puede escalar horizontalmente una puerta de enlace de administración de datos mediante la asociación de varios máquinas locales con puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="4dc69-111">Puede escalar verticalmente aumentando el número de trabajos de movimiento de datos que pueden ejecutarse simultáneamente en un nodo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="4dc69-112">Esta característica también está disponible para una puerta de enlace lógica con un único nodo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="4dc69-113">Consulte el artículo [Escalado en Data Management Gateway en Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="4dc69-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc69-114">Actualmente, la puerta de enlace admite solo la actividad de copia de Hola y la actividad de procedimiento almacenado de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="4dc69-115">No es puerta de enlace de posibles toouse Hola una actividad personalizada tooaccess local orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="4dc69-116">Información general</span><span class="sxs-lookup"><span data-stu-id="4dc69-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="4dc69-117">Funcionalidades de Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="4dc69-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="4dc69-118">Puerta de enlace de administración de datos proporciona Hola siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="4dc69-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="4dc69-119">Modelo de orígenes de datos locales y los orígenes de datos en la nube dentro Hola misma factoría de datos y moverán los datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="4dc69-120">Tener un solo panel de vidrio para la supervisión y administración con la visibilidad del estado de la puerta de enlace desde la página de la factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="4dc69-121">Administrar orígenes de datos de access tooon local de forma segura.</span><span class="sxs-lookup"><span data-stu-id="4dc69-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="4dc69-122">Toocorporate firewall requiere ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="4dc69-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="4dc69-123">Puerta de enlace solo realiza conexiones basadas en HTTP salientes tooopen internet.</span><span class="sxs-lookup"><span data-stu-id="4dc69-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="4dc69-124">Cifrar las credenciales de los almacenes de datos locales con su certificado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="4dc69-125">Mover datos de manera eficaz: problemas de red toointermittent paralela y resistente con lógica de reintento automático de los datos se transfieren.</span><span class="sxs-lookup"><span data-stu-id="4dc69-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="4dc69-126">Flujo de comandos y flujo de datos</span><span class="sxs-lookup"><span data-stu-id="4dc69-126">Command flow and data flow</span></span>
<span data-ttu-id="4dc69-127">Al utilizar toocopy de actividad copiar datos entre local y en la nube, actividad hello usa datos tootransfer puerta de enlace de toocloud de origen de datos local y viceversa.</span><span class="sxs-lookup"><span data-stu-id="4dc69-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="4dc69-128">Este es flujo de datos de alto nivel hello y resumen de pasos para copiar con puerta de enlace de datos: ![flujo de datos mediante la puerta de enlace](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="4dc69-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="4dc69-129">Desarrollador de datos crea una puerta de enlace de una factoría de datos de Azure mediante cualquier hello [portal de Azure](https://portal.azure.com) o [Cmdlet de PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="4dc69-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="4dc69-130">Desarrollador de datos crea un servicio vinculado para un almacén de datos local mediante la especificación de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="4dc69-131">Como parte de la configuración de hello servicio vinculado, el programador de datos utiliza las credenciales y tipos de autenticación de hello establecer credenciales aplicación toospecify.</span><span class="sxs-lookup"><span data-stu-id="4dc69-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="4dc69-132">cuadro de diálogo aplicación se comunica con los datos de Hola Hola establecer credenciales almacenar tootest hello y conexión de puerta de enlace toosave las credenciales.</span><span class="sxs-lookup"><span data-stu-id="4dc69-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="4dc69-133">Puerta de enlace cifra las credenciales de hello con certificado de hello asociado con la puerta de enlace de hello (proporcionado por el desarrollador de datos), antes de guardar las credenciales de hello en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="4dc69-134">Servicio de factoría de datos se comunica con la puerta de enlace de hello para la programación y administración de trabajos a través de un canal de control que utiliza una cola de bus de servicio compartido de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="4dc69-135">Cuando un trabajo de copia de la actividad necesita toobe iniciado, factoría de datos se pone en cola con solicitud de hello junto con información de credenciales.</span><span class="sxs-lookup"><span data-stu-id="4dc69-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="4dc69-136">Puerta de enlace inicia el trabajo de hello después de sondear la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="4dc69-137">puerta de enlace de Hola descifra las credenciales de hello con hello mismo certificado y, a continuación, conecta a un almacén de datos local toohello con las credenciales y el tipo de autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="4dc69-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="4dc69-138">puerta de enlace de Hello copia los datos desde un almacenamiento de nube local tooa de almacén, o viceversa según cómo esté configurada Hola actividad de copia en la canalización de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="4dc69-139">Para este paso, puerta de enlace de Hola se comunica directamente con los servicios de almacenamiento en la nube como almacenamiento de blobs de Azure por un canal seguro (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="4dc69-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="4dc69-140">Consideraciones a la hora de usar la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="4dc69-140">Considerations for using gateway</span></span>
* <span data-ttu-id="4dc69-141">Se puede utilizar una sola instancia de Data Management Gateway para varios orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="4dc69-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="4dc69-142">Sin embargo, **una instancia única de la puerta de enlace es un generador de datos de Azure relacionados tooonly** y no puede compartirse con otro generador de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="4dc69-143">**Solo puede haber una instancia de Data Management Gateway** instalada en un equipo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="4dc69-144">Imagine que tiene dos generadores de datos que necesitan tooaccess los orígenes de datos local, necesita puertas de enlace de tooinstall en equipos locales en dos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="4dc69-145">En otras palabras, una puerta de enlace es factoría de datos específica de tooa relacionados</span><span class="sxs-lookup"><span data-stu-id="4dc69-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="4dc69-146">Hola **puerta de enlace no es necesario toobe en hello mismo equipo como origen de datos de hello**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="4dc69-147">Sin embargo, con el origen de datos de toohello más de cerca de puerta de enlace reduce el tiempo Hola Hola puerta de enlace tooconnect toohello origen de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="4dc69-148">Se recomienda que instale la puerta de enlace de hello en un equipo que es diferente de hello uno ese origen de datos de hosts local.</span><span class="sxs-lookup"><span data-stu-id="4dc69-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="4dc69-149">Cuando el origen de datos y la puerta de enlace de hello están en equipos diferentes, puerta de enlace de hello no compiten por los recursos con el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="4dc69-150">Puede tener **varias puertas de enlace en distintos equipos conectarse toohello mismo origen de datos local**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="4dc69-151">Por ejemplo, puede tener dos puertas de enlace que sirve al factorías de dos datos pero Hola mismo origen de datos local se registra con ambos factorías de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="4dc69-152">Si ya tiene una puerta de enlace instalada en el equipo que atiende a un escenario de **Power BI**, instale una **puerta de enlace independiente para Azure Data Factory** en otra máquina.</span><span class="sxs-lookup"><span data-stu-id="4dc69-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="4dc69-153">Debe usar la puerta de enlace, incluso cuando utilice **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="4dc69-154">Considere el origen de datos como uno de tipo local (que está detrás de un firewall), aunque utilice **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="4dc69-155">Usar la conectividad de tooestablish de puerta de enlace de hello entre el servicio de Hola y el origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="4dc69-156">Debe **usar puerta de enlace de hello** aunque Hola almacén de datos está en la nube de hello en un **VM de IaaS de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="4dc69-157">Instalación</span><span class="sxs-lookup"><span data-stu-id="4dc69-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="4dc69-158">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4dc69-158">Prerequisites</span></span>
* <span data-ttu-id="4dc69-159">Hola admitida **sistema operativo** versiones son Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="4dc69-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="4dc69-160">Instalación de data management gateway de hello en un controlador de dominio no se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="4dc69-161">Es necesario .NET Framework 4.5.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4dc69-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="4dc69-162">Si está instalando la puerta de enlace en una máquina con Windows 7, instale .NET Framework 4.5 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4dc69-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="4dc69-163">Consulte [Requisitos de sistema de .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="4dc69-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="4dc69-164">Hola recomendada **configuración** de máquina de puerta de enlace de hello es al menos 2 GHz, 4 núcleos, 8 GB de RAM y disco de 80 GB.</span><span class="sxs-lookup"><span data-stu-id="4dc69-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="4dc69-165">Si el equipo host de hello hiberna, puerta de enlace de hello no responde toodata solicitudes.</span><span class="sxs-lookup"><span data-stu-id="4dc69-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="4dc69-166">Por lo tanto, configure una adecuada **plan de energía** en equipo Hola antes de instalar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="4dc69-167">Si se utiliza una máquina de hello toohibernate configurado, instalación de puerta de enlace de hello pide un mensaje.</span><span class="sxs-lookup"><span data-stu-id="4dc69-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="4dc69-168">Debe ser un administrador en hello máquina tooinstall y configurar correctamente la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="4dc69-169">Puede agregar usuarios adicionales toohello **puerta de enlace de administración de datos a los usuarios** grupo local de Windows.</span><span class="sxs-lookup"><span data-stu-id="4dc69-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="4dc69-170">los miembros de Hola de este grupo son toouse capaz de hello **Administrador de configuración de Data Management Gateway** puerta de enlace de herramienta tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="4dc69-171">Como copiar conseguirlo ejecuciones de actividad en una frecuencia determinada, hello uso de recursos (CPU, memoria) en la máquina de hello también sigue Hola mismo patrón con las horas punta y tiempos de inactividad.</span><span class="sxs-lookup"><span data-stu-id="4dc69-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="4dc69-172">Utilización de recursos también depende en gran medida cantidad Hola de datos que se mueven.</span><span class="sxs-lookup"><span data-stu-id="4dc69-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="4dc69-173">Cuando hay varios trabajos de copia en curso, puede ver que el uso de los recursos aumenta durante las horas pico.</span><span class="sxs-lookup"><span data-stu-id="4dc69-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="4dc69-174">Opciones de instalación</span><span class="sxs-lookup"><span data-stu-id="4dc69-174">Installation options</span></span>
<span data-ttu-id="4dc69-175">Puerta de enlace de administración de datos puede instalarse en hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="4dc69-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="4dc69-176">Al descargar un paquete de instalación MSI de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="4dc69-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="4dc69-177">Hola MSI también puede ser utilizados tooupgrade existente datos administración puerta de enlace toohello versión más reciente, con todas las opciones que se conservan.</span><span class="sxs-lookup"><span data-stu-id="4dc69-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="4dc69-178">Haciendo clic en el vínculo **Descargar e instalar la puerta de enlace de datos** en INSTALACIÓN MANUAL o en la opción **Instalar directamente en este equipo** en CONFIGURACIÓN RÁPIDA.</span><span class="sxs-lookup"><span data-stu-id="4dc69-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="4dc69-179">Consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obtener instrucciones detalladas sobre cómo usar la configuración rápida.</span><span class="sxs-lookup"><span data-stu-id="4dc69-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="4dc69-180">paso manual Hola le toohello centro de descarga.</span><span class="sxs-lookup"><span data-stu-id="4dc69-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="4dc69-181">las instrucciones de Hola para descargar e instalar la puerta de enlace de Hola desde el centro de descarga están en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="4dc69-182">Procedimientos recomendados de instalación:</span><span class="sxs-lookup"><span data-stu-id="4dc69-182">Installation best practices:</span></span>
1. <span data-ttu-id="4dc69-183">Configurar el plan de energía en la máquina de host de Hola para puerta de enlace de Hola para que hello máquina no hibernación.</span><span class="sxs-lookup"><span data-stu-id="4dc69-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="4dc69-184">Si el equipo host de hello hiberna, puerta de enlace de hello no responde toodata solicitudes.</span><span class="sxs-lookup"><span data-stu-id="4dc69-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="4dc69-185">Copia de seguridad asociado a la puerta de enlace de Hola de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="4dc69-186">Instale la puerta de enlace de Hola desde el centro de descarga</span><span class="sxs-lookup"><span data-stu-id="4dc69-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="4dc69-187">Navegue demasiado[página de descarga de Microsoft Data Management Gateway](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="4dc69-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="4dc69-188">Haga clic en **descargar**, seleccione Hola versión adecuada (**32-bit** vs. **64 bits**) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="4dc69-189">Ejecute hello **MSI** directamente o guárdelo en disco duro de tooyour y ejecutar.</span><span class="sxs-lookup"><span data-stu-id="4dc69-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="4dc69-190">En hello **bienvenida** página, seleccione un **lenguaje** haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="4dc69-191">**Aceptar** Hola contrato de licencia de usuario final y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="4dc69-192">Seleccione **carpeta** tooinstall Hola puerta de enlace y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="4dc69-193">En hello **tooinstall listo** página, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="4dc69-194">Haga clic en **finalizar** toocomplete instalación.</span><span class="sxs-lookup"><span data-stu-id="4dc69-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="4dc69-195">Obtener clave de Hola de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="4dc69-196">Vea la siguiente sección de Hola para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="4dc69-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="4dc69-197">En hello **puerta de enlace de registro** página de **Administrador de configuración de Data Management Gateway** ejecutando en el equipo, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4dc69-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="4dc69-198">Pegue la clave de hello en texto hello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="4dc69-199">Si lo desea, haga clic en **clave de puerta de enlace de mostrar** texto de la tecla toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="4dc69-200">Haga clic en **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="4dc69-201">Registro de la puerta de enlace mediante una clave</span><span class="sxs-lookup"><span data-stu-id="4dc69-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="4dc69-202">Si aún no ha creado una puerta de enlace lógico en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="4dc69-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="4dc69-203">una puerta de enlace de clave de hello portal y get hello de hello toocreate **configurar** página, siga los pasos del tutorial Hola [mover datos entre local y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="4dc69-204">Si ya ha creado la puerta de enlace lógica de Hola en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="4dc69-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="4dc69-205">En el portal de Azure, navegue toohello **factoría de datos** página y haga clic en **servicios vinculados** icono.</span><span class="sxs-lookup"><span data-stu-id="4dc69-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Página Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="4dc69-207">Hola **servicios vinculados** página, seleccione Hola lógico **puerta de enlace** que creó en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![puerta de enlace lógica](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="4dc69-209">Hola **puerta de enlace de datos** página, haga clic en **descargar e instalar la puerta de enlace de datos**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Descargar vínculo en el portal de Hola](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="4dc69-211">Hola **configurar** página, haga clic en **vuelva a crear clave**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="4dc69-212">Haga clic en Sí en el mensaje de advertencia de hello después de leerlo detenidamente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Volver a crear clave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="4dc69-214">Haga clic en siguiente toohello tecla del botón Copiar.</span><span class="sxs-lookup"><span data-stu-id="4dc69-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="4dc69-215">clave de Hello es copiada toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="4dc69-215">hello key is copied toohello clipboard.</span></span>

    ![Copiar clave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="4dc69-217">Notificaciones/iconos de la bandeja del sistema</span><span class="sxs-lookup"><span data-stu-id="4dc69-217">System tray icons/ notifications</span></span>
<span data-ttu-id="4dc69-218">Hello imagen siguiente muestra algunas de hello iconos de la bandeja que se ven.</span><span class="sxs-lookup"><span data-stu-id="4dc69-218">hello following image shows some of hello tray icons that you see.</span></span>

![Iconos de la bandeja del sistema](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="4dc69-220">Si mueve el cursor sobre el mensaje de notificación/icono de bandeja de sistema hello, puede ver detalles acerca del estado de Hola de operación de puerta de enlace o actualizar hello en una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="4dc69-221">Puertos y firewall</span><span class="sxs-lookup"><span data-stu-id="4dc69-221">Ports and firewall</span></span>
<span data-ttu-id="4dc69-222">Hay dos firewalls necesita tooconsider: **firewall corporativo** ejecuta en hello enrutador central de la organización de hello, y **firewall de Windows** configurado como un demonio en el equipo local de Hola donde hello puerta de enlace está instalado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![Firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="4dc69-224">En el nivel de firewall corporativo, debe configurar siguiente Hola dominios y los puertos de salida:</span><span class="sxs-lookup"><span data-stu-id="4dc69-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="4dc69-225">Nombres de dominio</span><span class="sxs-lookup"><span data-stu-id="4dc69-225">Domain names</span></span> | <span data-ttu-id="4dc69-226">Puertos</span><span class="sxs-lookup"><span data-stu-id="4dc69-226">Ports</span></span> | <span data-ttu-id="4dc69-227">Descripción</span><span class="sxs-lookup"><span data-stu-id="4dc69-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4dc69-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="4dc69-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="4dc69-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="4dc69-229">443, 80</span></span> |<span data-ttu-id="4dc69-230">Usado para la comunicación con el back-end del servicio de movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="4dc69-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="4dc69-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4dc69-231">*.core.windows.net</span></span> |<span data-ttu-id="4dc69-232">443</span><span class="sxs-lookup"><span data-stu-id="4dc69-232">443</span></span> |<span data-ttu-id="4dc69-233">Usado para la copia de almacenamiento provisional que usa el blob de Azure (si está configurado)</span><span class="sxs-lookup"><span data-stu-id="4dc69-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="4dc69-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="4dc69-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="4dc69-235">443</span><span class="sxs-lookup"><span data-stu-id="4dc69-235">443</span></span> |<span data-ttu-id="4dc69-236">Usado para la comunicación con el back-end del servicio de movimiento de datos</span><span class="sxs-lookup"><span data-stu-id="4dc69-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="4dc69-237">En el nivel de Firewall de Windows, normalmente se habilitan estos puertos de salida.</span><span class="sxs-lookup"><span data-stu-id="4dc69-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="4dc69-238">Si no es así, puede configurar dominios de Hola y puertos según corresponda en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4dc69-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="4dc69-239">En función de su origen / receptores, puede tener dominios adicionales toowhitelist y puertos de salida en el firewall corporativo/Windows.</span><span class="sxs-lookup"><span data-stu-id="4dc69-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="4dc69-240">Para algunas bases de datos en la nube (por ejemplo: [base de datos de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), deberá toowhitelist dirección IP de la máquina de puerta de enlace en su configuración de firewall.</span><span class="sxs-lookup"><span data-stu-id="4dc69-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="4dc69-241">Copiar datos desde un almacén de datos de origen datos almacén tooa receptor</span><span class="sxs-lookup"><span data-stu-id="4dc69-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="4dc69-242">Asegúrese de que las reglas de firewall de hello están habilitadas correctamente en el firewall corporativo hello, firewall de Windows en la máquina de puerta de enlace de hello, y del almacén de datos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="4dc69-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="4dc69-243">Al habilitar estas reglas permite Hola origen de puerta de enlace tooconnect tooboth y receptor correctamente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="4dc69-244">Habilitar reglas para cada almacén de datos que están implicados en la operación de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="4dc69-245">Por ejemplo, toocopy de **un receptor de base de datos de SQL Azure local tooan de almacén de datos o un receptor de almacenamiento de datos de SQL Azure**, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4dc69-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="4dc69-246">Permita la comunicación **TCP** saliente en el puerto **1433** para el Firewall de Windows y el corporativo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="4dc69-247">La configuración de firewall Hola de SQL Azure tooadd Hola dirección IP del servidor lista de toohello máquina Hola de puerta de enlace de direcciones IP permitidas.</span><span class="sxs-lookup"><span data-stu-id="4dc69-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc69-248">Si el firewall no permite el puerto de salida 1433, la puerta de enlace no podrá tener acceso directamente a Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4dc69-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="4dc69-249">En este caso, puede usar [copia provisionalmente](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL base de datos de Azure y almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="4dc69-250">En este escenario, sólo requeriría HTTPS (puerto 443) para el movimiento de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="4dc69-251">Consideraciones acerca del servidor proxy</span><span class="sxs-lookup"><span data-stu-id="4dc69-251">Proxy server considerations</span></span>
<span data-ttu-id="4dc69-252">Si su entorno de red corporativa usa un proxy de servidor tooaccess Hola internet, configure la configuración de proxy apropiada de toouse de puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="4dc69-253">Puede establecer el proxy de Hola durante la fase de registro inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-253">You can set hello proxy during hello initial registration phase.</span></span>

![Configuración del proxy durante el registro](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="4dc69-255">Puerta de enlace usa el servicio de nube de hello proxy server tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="4dc69-256">Haga clic en el vínculo **Cambiar** durante la configuración inicial.</span><span class="sxs-lookup"><span data-stu-id="4dc69-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="4dc69-257">Vea hello **la configuración de proxy** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-257">You see hello **proxy setting** dialog.</span></span>

![Configuración del proxy mediante el Administrador de configuración](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="4dc69-259">Hay tres opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="4dc69-259">There are three configuration options:</span></span>

* <span data-ttu-id="4dc69-260">**No utilice el proxy**: puerta de enlace no utiliza los servicios de proxy tooconnect toocloud explícitamente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="4dc69-261">**Utilice el proxy de sistema**: puerta de enlace utiliza la configuración que es configurado en diahost.exe.config y diawp.exe.config de proxy de Hola.  Si no hay ningún proxy está configurado en diahost.exe.config y diawp.exe.config, puerta de enlace conecta toocloud servicio directamente sin tener que pasar a través de proxy.</span><span class="sxs-lookup"><span data-stu-id="4dc69-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="4dc69-262">**Usar proxy personalizado**: configurar Hola HTTP toouse de configuración de proxy para la puerta de enlace, en lugar de utilizar las configuraciones de diahost.exe.config y diawp.exe.config.  La dirección y el puerto son obligatorios.</span><span class="sxs-lookup"><span data-stu-id="4dc69-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="4dc69-263">El nombre de usuario y la contraseña son opcionales según la configuración de autenticación del proxy.</span><span class="sxs-lookup"><span data-stu-id="4dc69-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="4dc69-264">Todos los valores son cifrados con el certificado de credencial de Hola de puerta de enlace de Hola y almacenados localmente en el equipo de host de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="4dc69-265">puerta de enlace de administración de datos de Hello servicio de Host se reiniciará automáticamente después de guardar la configuración de proxy de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="4dc69-266">Después de puerta de enlace se ha registrado correctamente, si desea que tooview o actualizar la configuración de proxy, use el Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4dc69-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="4dc69-267">Inicie el **Administrador de configuración de Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="4dc69-268">Cambiar toohello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="4dc69-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="4dc69-269">Haga clic en **cambio** vincular en **HTTP Proxy** Hola de sección toolaunch **establecer Proxy HTTP** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="4dc69-270">Tras hacer clic en hello **siguiente** botón, verá un cuadro de diálogo de advertencia que pregunta para el permiso toosave Hola configuración del servidor proxy y reinicie el servicio de Host de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="4dc69-271">Puede ver y actualizar el proxy HTTP mediante la herramienta Administrador de configuración.</span><span class="sxs-lookup"><span data-stu-id="4dc69-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Configuración del proxy mediante el Administrador de configuración](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="4dc69-273">Si configura un servidor proxy con la autenticación NTLM, servicio de Host de puerta de enlace se ejecuta bajo la cuenta de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="4dc69-274">Si cambia Hola contraseña de cuenta de dominio de hello más tarde, recuerde tooupdate valores de configuración para el servicio de Hola y reiniciarlo en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="4dc69-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="4dc69-275">Pagar toothis requisito, se recomienda que usar un servidor proxy de dominio dedicada cuenta tooaccess Hola que no requiere la contraseña de hello tooupdate con frecuencia.</span><span class="sxs-lookup"><span data-stu-id="4dc69-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="4dc69-276">Configuración de un servidor proxy</span><span class="sxs-lookup"><span data-stu-id="4dc69-276">Configure proxy server settings</span></span>
<span data-ttu-id="4dc69-277">Si selecciona **usar el proxy de sistema** establecer para el proxy HTTP de hello, puerta de enlace usa Hola configuración del proxy de diahost.exe.config y diawp.exe.config.  Si no se especifica ningún proxy en diahost.exe.config y diawp.exe.config, puerta de enlace conecta toocloud servicio directamente sin tener que pasar a través de proxy.</span><span class="sxs-lookup"><span data-stu-id="4dc69-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="4dc69-278">Hello siguiente procedimiento proporciona instrucciones para actualizar el archivo de hello diahost.exe.config.</span><span class="sxs-lookup"><span data-stu-id="4dc69-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="4dc69-279">En el Explorador de archivos, constituyen una copia de seguridad del C:\Program Files\Microsoft datos administración Gateway\2.0\Shared\diahost.exe.config tooback archivo original de hello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="4dc69-280">Inicie Notepad.exe como administrador y abra el archivo de texto C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Buscar etiqueta predeterminada de Hola para system.net tal y como se muestra en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="4dc69-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="4dc69-281">A continuación, puede agregar detalles del servidor proxy como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4dc69-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="4dc69-282">Propiedades adicionales se permiten dentro de hello etiqueta toospecify Hola requerido configuración del proxy como scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="4dc69-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="4dc69-283">Consulte demasiado[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) acerca de la sintaxis.</span><span class="sxs-lookup"><span data-stu-id="4dc69-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="4dc69-284">Guarde el archivo de configuración de hello en ubicación original de hello, a continuación, reinicie el servicio de Host de puerta de enlace de administración de datos, que recoge el cambio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="4dc69-285">servicio de Hola toorestart: usar servicios applet de panel de control de Hola o de hello **Administrador de configuración de Data Management Gateway** > haga clic en hello **detener el servicio** , a continuación, haga clic en hello **Iniciar el servicio**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="4dc69-286">Si no se inicia el servicio de hello, es probable que se ha agregado una sintaxis de etiqueta XML incorrecta en el archivo de configuración de aplicación Hola que se ha editado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4dc69-287">No olvide tooupdate **ambos** diahost.exe.config y diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="4dc69-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="4dc69-288">Además puntos toothese, también necesitará toomake seguro de que Microsoft Azure está en la lista blanca de direcciones de su empresa.</span><span class="sxs-lookup"><span data-stu-id="4dc69-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="4dc69-289">lista de Hola de direcciones IP de Microsoft Azure puede descargarse desde hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="4dc69-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="4dc69-290">Posibles síntomas de problemas relacionados con el firewall y el servidor proxy</span><span class="sxs-lookup"><span data-stu-id="4dc69-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="4dc69-291">Si encuentra errores toohello similar los siguiendo, es probable debido tooimproper configuración de servidor hello proxy o firewall que bloquea la puerta de enlace de conexión tooauthenticate de fábrica de tooData propio.</span><span class="sxs-lookup"><span data-stu-id="4dc69-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="4dc69-292">Consulte tooprevious sección tooensure el servidor proxy y firewall se han configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="4dc69-293">Al tratar de puerta de enlace de tooregister hello, recibirá Hola siguiente error: "clave de puerta de enlace de error tooregister Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="4dc69-294">Antes de intentar clave de puerta de enlace de tooregister Hola de nuevo, confirme que hello data management gateway está en estado conectado y Hola servicio de Host de Data Management Gateway se ha iniciado."</span><span class="sxs-lookup"><span data-stu-id="4dc69-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="4dc69-295">Al abrir el Administrador de configuración, verá el estado Desconectado o Conectando.</span><span class="sxs-lookup"><span data-stu-id="4dc69-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="4dc69-296">Al ver los registros de eventos de Windows, en "Visor de eventos" > "Registros de aplicaciones y servicios" > "Data Management Gateway", aparecen mensajes de error como Hola siguiente error:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="4dc69-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="4dc69-297">Apertura del puerto 8050 para el cifrado de credenciales</span><span class="sxs-lookup"><span data-stu-id="4dc69-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="4dc69-298">Hola **establecer credenciales** aplicación usa Hola puerto de entrada **8050** servicio Hola portal de Azure vinculado de puerta de enlace de toorelay credenciales toohello al configurar una implementación local.</span><span class="sxs-lookup"><span data-stu-id="4dc69-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="4dc69-299">Durante la instalación de puerta de enlace, de forma predeterminada, instalación de puerta de enlace de hello lo abre en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="4dc69-300">Si estás usando un firewall de terceros, puede abrir manualmente el puerto de hello 8050.</span><span class="sxs-lookup"><span data-stu-id="4dc69-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="4dc69-301">Si experimenta el problema de firewall durante la instalación de puerta de enlace, también puede intentar usar Hola después de puerta de enlace de comando tooinstall Hola sin configurar firewall de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="4dc69-302">Si decide no tooopen puerto hello 8050 en la máquina de puerta de enlace de hello, use mecanismos que no sea hello **establecer credenciales** credenciales de almacén de datos de tooconfigure de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4dc69-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="4dc69-303">Por ejemplo, puede usar el cmdlet de PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4dc69-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="4dc69-304">Consulte la sección [Configuración de credenciales y seguridad](#set-credentials-and-securityy) para más información sobre cómo configurar las credenciales del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="4dc69-305">Actualizar</span><span class="sxs-lookup"><span data-stu-id="4dc69-305">Update</span></span>
<span data-ttu-id="4dc69-306">De forma predeterminada, la puerta de enlace de administración de datos se actualiza automáticamente cuando hay disponible una versión más reciente de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="4dc69-307">puerta de enlace de Hello no se actualiza hasta que se realizan todas las tareas de hello programado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="4dc69-308">No hay otras tareas se procesan por puerta de enlace de hello hasta que se complete la operación de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="4dc69-309">Si se produce un error en la actualización de hello, puerta de enlace se revierte toohello una versión antigua.</span><span class="sxs-lookup"><span data-stu-id="4dc69-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="4dc69-310">Consulte hora de la actualización de hello programado en hello siguientes lugares:</span><span class="sxs-lookup"><span data-stu-id="4dc69-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="4dc69-311">página de propiedades de puerta de enlace de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="4dc69-312">Página principal del programa Hola a Administrador de configuración de Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="4dc69-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="4dc69-313">En un mensaje de notificación de la bandeja del sistema</span><span class="sxs-lookup"><span data-stu-id="4dc69-313">System tray notification message.</span></span>

<span data-ttu-id="4dc69-314">pestaña de inicio de Hola de hello Administrador de configuración de Data Management Gateway muestra la programación de actualización de Hola y puerta de enlace de hello última hora Hola se ha instalado o actualizar.</span><span class="sxs-lookup"><span data-stu-id="4dc69-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Programar actualizaciones](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="4dc69-316">Puede instalar la actualización de hello inmediatamente o esperar toobe de puerta de enlace de hello actualizado automáticamente en el momento de hello programado.</span><span class="sxs-lookup"><span data-stu-id="4dc69-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="4dc69-317">Por ejemplo, hello siguiente imagen muestra Hola se muestra en hello puerta de enlace de Configuration Manager junto con el botón de actualización de Hola que puede hacer clic en tooinstall se inmediatamente el mensaje de notificación.</span><span class="sxs-lookup"><span data-stu-id="4dc69-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Actualización en el Administrador de configuración de Data Management Gateway](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="4dc69-319">mensaje de notificación de Hello en bandeja del sistema Hola sería como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="4dc69-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Mensaje de la bandeja del sistema](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="4dc69-321">Vea Estado Hola de operación de actualización en la bandeja del sistema hello (manual o automática).</span><span class="sxs-lookup"><span data-stu-id="4dc69-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="4dc69-322">Al iniciar el Administrador de configuración de puerta de enlace próxima vez, verá un mensaje en la notificación de hello barra esa puerta de enlace de Hola se ha actualizado junto con un vínculo demasiado[¿qué es el nuevo tema](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="4dc69-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="4dc69-323">característica de toodisable/Habilitar actualización automática</span><span class="sxs-lookup"><span data-stu-id="4dc69-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="4dc69-324">Se puede deshabilitar/Habilitar característica de actualización automática de hello haciendo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4dc69-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="4dc69-325">[Para puerta de enlace de nodo único]</span><span class="sxs-lookup"><span data-stu-id="4dc69-325">[For single node gateway]</span></span>
1. <span data-ttu-id="4dc69-326">Inicie Windows PowerShell en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="4dc69-327">Cambie la carpeta C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript de toohello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="4dc69-328">Hola ejecución después de comando tooturn Hola la actualización automática de características desactivar (deshabilitar).</span><span class="sxs-lookup"><span data-stu-id="4dc69-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="4dc69-329">tooturn vuelve a activar:</span><span class="sxs-lookup"><span data-stu-id="4dc69-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="4dc69-330">[[Para puerta de enlace escalable y altamente disponible de varios nodos (versión preliminar)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="4dc69-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="4dc69-331">Inicie Windows PowerShell en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="4dc69-332">Cambie la carpeta C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript de toohello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="4dc69-333">Hola ejecución después de comando tooturn Hola la actualización automática de características desactivar (deshabilitar).</span><span class="sxs-lookup"><span data-stu-id="4dc69-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="4dc69-334">Se requiere un parámetro AuthKey adicional para la característica de puerta de enlace con alta disponibilidad (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="4dc69-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="4dc69-335">tooturn vuelve a activar:</span><span class="sxs-lookup"><span data-stu-id="4dc69-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="4dc69-336">Si tiene acceso a portal de Hola desde un equipo que es diferente de la máquina de puerta de enlace de hello, debe asegurarse de que aplicación de administrador de credenciales de hello puede conectarse toohello máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4dc69-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="4dc69-337">Si la aplicación hello no puede llegar a la máquina de puerta de enlace de hello, no permite también tooset credenciales para el origen de datos de Hola y el origen de datos de tootest conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="4dc69-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="4dc69-338">Cuando usas hello **establecer credenciales** aplicación, portal de Hola cifra las credenciales de Hola con certificado de hello especificado en hello **certificado** ficha de hello **puerta de enlace Administrador de configuración de** en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="4dc69-339">Si desea obtener un enfoque basado en la API para cifrar las credenciales de hello, puede usar hello [AzureRmDataFactoryEncryptValue nuevo](https://msdn.microsoft.com/library/mt603802.aspx) las credenciales de tooencrypt de cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4dc69-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="4dc69-340">Hola cmdlet utiliza esa puerta de enlace está configurado toouse tooencrypt Hola credenciales de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="4dc69-341">Agregue las credenciales cifradas toohello **EncryptedCredential** elemento de hello **connectionString** Hola JSON.</span><span class="sxs-lookup"><span data-stu-id="4dc69-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="4dc69-342">Usar hello JSON con hello [AzureRmDataFactoryLinkedService New](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet u Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="4dc69-343">Hay otro enfoque para establecer las credenciales mediante el Editor de la Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="4dc69-344">Si crea un servidor SQL Server vinculado servicio mediante el editor de Hola y escriba las credenciales en texto sin formato, las credenciales de Hola se cifran mediante un certificado que posee el servicio Data Factory de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="4dc69-345">NO utiliza certificados de hello que esa puerta de enlace está configurado toouse.</span><span class="sxs-lookup"><span data-stu-id="4dc69-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="4dc69-346">Aunque este enfoque puede resultar un poco más rápido, en algunos casos es menos seguro.</span><span class="sxs-lookup"><span data-stu-id="4dc69-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="4dc69-347">Por lo tanto, se recomienda seguir este enfoque solo para fines de desarrollo y pruebas.</span><span class="sxs-lookup"><span data-stu-id="4dc69-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="4dc69-348">Cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc69-348">PowerShell cmdlets</span></span>
<span data-ttu-id="4dc69-349">Esta sección se describe cómo toocreate y registrar una puerta de enlace mediante cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="4dc69-350">Inicie **Azure PowerShell** en modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="4dc69-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="4dc69-351">Inicie sesión en tooyour cuenta de Azure mediante la ejecución de hello siguiente comando y escriba sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="4dc69-352">Hola de uso **AzureRmDataFactoryGateway New** cmdlet toocreate una puerta de enlace lógico como sigue:</span><span class="sxs-lookup"><span data-stu-id="4dc69-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="4dc69-353">**Ejemplo de comando y salida**:</span><span class="sxs-lookup"><span data-stu-id="4dc69-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="4dc69-354">En Azure PowerShell, cambie la carpeta toohello: **C:\Program Files\Microsoft datos administración Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="4dc69-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="4dc69-355">Ejecutar **RegisterGateway.ps1** asociado a la variable local de hello **$Key** tal y como se muestra en el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4dc69-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="4dc69-356">Este script registra el agente de cliente de hello instalado en su equipo con puerta de enlace de lógica Hola que crear anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4dc69-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="4dc69-357">Puede registrar la puerta de enlace de hello en un equipo remoto mediante hello IsRegisterOnRemoteMachine parámetro.</span><span class="sxs-lookup"><span data-stu-id="4dc69-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="4dc69-358">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4dc69-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="4dc69-359">Puede usar hello **AzureRmDataFactoryGateway Get** lista de cmdlets tooget Hola de puertas de enlace de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="4dc69-360">Cuando Hola **estado** muestra **en línea**, significa que la puerta de enlace es toouse listo.</span><span class="sxs-lookup"><span data-stu-id="4dc69-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="4dc69-361">Puede quitar una puerta de enlace con hello **Remove-AzureRmDataFactoryGateway** descripción de cmdlet y actualización de una puerta de enlace con hello **AzureRmDataFactoryGateway conjunto** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4dc69-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="4dc69-362">Para ver la sintaxis y otros detalles de estos cmdlets, consulte la documentación de referencia de los cmdlets de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="4dc69-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="4dc69-363">Enumeración de puertas de enlace con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc69-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="4dc69-364">Eliminación de puerta de enlace con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc69-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="4dc69-365">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4dc69-365">Next steps</span></span>
* <span data-ttu-id="4dc69-366">Para más información, consulte el artículo [Movimiento de datos entre orígenes locales y la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="4dc69-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="4dc69-367">En el tutorial de hello, crear una canalización que utiliza datos de toomove de puerta de enlace de Hola de una base de datos de SQL Server local tooan blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc69-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
