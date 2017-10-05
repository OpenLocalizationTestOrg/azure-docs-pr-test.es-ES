---
title: "Estimación de la capacidad de replicación en Azure | Microsoft Docs"
description: "Use este artículo para hacer estimaciones cuando se realizan replicaciones con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: 134e17ebda3105be2b53d072fdef7aeda4a98bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="plan-capacity-for-protecting-virtual-machines-and-physical-servers-in-azure-site-recovery"></a><span data-ttu-id="388d1-103">Planeación de la capacidad para la protección de máquinas virtuales y de los servidores físicos en Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="388d1-103">Plan capacity for protecting virtual machines and physical servers in Azure Site Recovery</span></span>

<span data-ttu-id="388d1-104">La herramienta Azure Site Recovery Capacity Planner lo ayuda a determinar los requisitos de capacidad para replicar máquinas virtuales de Hyper-V, máquinas virtuales de VMware y servidores físicos de Windows/Linux con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="388d1-104">The Azure Site Recovery Capacity Planner tool helps you to figure out your capacity requirements when replicating Hyper-V VMs, VMware VMs, and Windows/Linux physical servers, with Azure Site Recovery.</span></span>

<span data-ttu-id="388d1-105">Use Capacity Planner de Site Recovery para analizar el entorno de origen y las cargas de trabajo, calcular las necesidades de ancho de banda, los recursos de servidor que necesita en la ubicación de origen y los recursos (máquinas virtuales y almacenamiento, etc.) que necesitará en su ubicación de destino.</span><span class="sxs-lookup"><span data-stu-id="388d1-105">Use the Site Recovery Capacity Planner to analyze your source environment and workloads, estimate bandwidth needs and server resources you'll need for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span>

<span data-ttu-id="388d1-106">Puede ejecutar la herramienta de dos modos distintos:</span><span class="sxs-lookup"><span data-stu-id="388d1-106">You can run the tool in a couple of modes:</span></span>

* <span data-ttu-id="388d1-107">**Planeación rápida**: ejecute la herramienta en este modo para obtener las proyecciones de la red y del servidor según el promedio de las máquinas virtuales, discos, almacenamiento y tasa de cambio.</span><span class="sxs-lookup"><span data-stu-id="388d1-107">**Quick planning**: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
* <span data-ttu-id="388d1-108">**Planeación detallada**: ejecute la herramienta en este modo y proporcione detalles de cada carga de trabajo en el nivel de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="388d1-108">**Detailed planning**: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="388d1-109">Analice la compatibilidad de la máquina virtual y obtenga proyecciones de red y del servidor.</span><span class="sxs-lookup"><span data-stu-id="388d1-109">Analyze VM compatibility and get network and server projections.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="388d1-110">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="388d1-110">Before you start</span></span>


1. <span data-ttu-id="388d1-111">Recopile información sobre su entorno, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.</span><span class="sxs-lookup"><span data-stu-id="388d1-111">Gather information about your environment, including VMs, disks per VM, storage per disk.</span></span>
2. <span data-ttu-id="388d1-112">Identifique la tasa de cambio (renovación) diaria para los datos replicados.</span><span class="sxs-lookup"><span data-stu-id="388d1-112">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="388d1-113">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="388d1-113">To do this:</span></span>

   * <span data-ttu-id="388d1-114">Si está replicando máquinas virtuales de Hyper-V, descargue la [herramienta de planeamiento de capacidad de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) para obtener la tasa de cambio.</span><span class="sxs-lookup"><span data-stu-id="388d1-114">If you're replicating Hyper-V VMs, then download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="388d1-115">[Más información](site-recovery-capacity-planning-for-hyper-v-replication.md) sobre esta herramienta.</span><span class="sxs-lookup"><span data-stu-id="388d1-115">[Learn more](site-recovery-capacity-planning-for-hyper-v-replication.md) about this tool.</span></span> <span data-ttu-id="388d1-116">Se recomienda ejecutar esta herramienta durante una semana para capturar los promedios.</span><span class="sxs-lookup"><span data-stu-id="388d1-116">We recommend you run this tool over a week to capture averages.</span></span>
   * <span data-ttu-id="388d1-117">Si va a replicar máquinas virtuales de VMware, use [Azure Site Recovery Deployment Planner](./site-recovery-deployment-planner.md) para calcular la frecuencia de renovación.</span><span class="sxs-lookup"><span data-stu-id="388d1-117">If you're replicating VMware virtual machines, use the [Azure Site Recovery Deployment Planner](./site-recovery-deployment-planner.md) to figure out the churn rate.</span></span>
   * <span data-ttu-id="388d1-118">Si está replicando servidores físicos, debe realizar los cálculos manualmente.</span><span class="sxs-lookup"><span data-stu-id="388d1-118">If you're replicating physical servers, you need to estimate manually.</span></span>

## <a name="run-the-quick-planner"></a><span data-ttu-id="388d1-119">Ejecución de Quick Planner</span><span class="sxs-lookup"><span data-stu-id="388d1-119">Run the Quick Planner</span></span>
1. <span data-ttu-id="388d1-120">Descargue la herramienta [Capacity Planner de Azure Site Recovery](http://aka.ms/asr-capacity-planner-excel) y ábrala.</span><span class="sxs-lookup"><span data-stu-id="388d1-120">Download and open the [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) tool.</span></span> <span data-ttu-id="388d1-121">Como debe ejecutar macros, seleccione las opciones de permitir la edición y de habilitar el contenido cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="388d1-121">You need to run macros, so select to enable editing and enable content when prompted.</span></span>
2. <span data-ttu-id="388d1-122">En **Select a planner type** (Seleccione un tipo de planeador), seleccione **Quick Planner** (Planificador rápido) en el cuadro de lista.</span><span class="sxs-lookup"><span data-stu-id="388d1-122">In **Select a planner type** select **Quick Planner** from the list box.</span></span>

   ![Introducción](./media/site-recovery-capacity-planner/getting-started.png)
3. <span data-ttu-id="388d1-124">En la hoja de cálculo **Capacity Planner** , escriba la información que necesite.</span><span class="sxs-lookup"><span data-stu-id="388d1-124">In the **Capacity Planner** worksheet, enter the required information.</span></span> <span data-ttu-id="388d1-125">Debe rellenar todos los campos rodeados por un círculo rojo de la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="388d1-125">You must fill in all the fields circled in red in the screenshot below.</span></span>

   * <span data-ttu-id="388d1-126">En **Select your scenario** (Seleccionar escenario) elija **Hyper-V to Azure** (Hyper-V a Azure) o **VMware/Physical to Azure** (VMWare/Físico a Azure).</span><span class="sxs-lookup"><span data-stu-id="388d1-126">In **Select your scenario**, choose **Hyper-V to Azure** or **VMware/Physical to Azure**.</span></span>
   * <span data-ttu-id="388d1-127">En **Average daily data change rate (%)** [Tasa media diaria de cambio de datos (%)], agregue la información que ha recopilado con la [herramienta de planeamiento de capacidad de Hyper-V](site-recovery-capacity-planning-for-hyper-v-replication.md) o con [Azure Site Recovery Deployment Planner](./site-recovery-deployment-planner.md).</span><span class="sxs-lookup"><span data-stu-id="388d1-127">In **Average daily data change rate (%)**, put in the information you gather using the [Hyper-V capacity planning tool](site-recovery-capacity-planning-for-hyper-v-replication.md) or the [Azure Site Recovery Deployment Planner](./site-recovery-deployment-planner.md).</span></span>  
   * <span data-ttu-id="388d1-128">**Compresión** solo se aplica a la compresión que se ofrece al replicar máquinas virtuales de VMware o servidores físicos en Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-128">**Compression** only applies to compression offered when replicating VMware VMs or physical servers to Azure.</span></span> <span data-ttu-id="388d1-129">Consideramos que es del 30 % o más, pero el valor se puede modificar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="388d1-129">We estimate 30% or more, but you can modify the setting as required.</span></span> <span data-ttu-id="388d1-130">Para la replicación de máquinas virtuales de Hyper-V a la compresión de Azure puede usar un dispositivo de terceros, como Riverbed.</span><span class="sxs-lookup"><span data-stu-id="388d1-130">For replicating Hyper-V VMs to Azure compression, you can use a third-party appliance such as Riverbed.</span></span>
   * <span data-ttu-id="388d1-131">En **Entradas de retención** especifique durante cuánto tiempo hay que conservar las réplicas.</span><span class="sxs-lookup"><span data-stu-id="388d1-131">In **Retention Inputs**, specify how long replicas should be retained.</span></span> <span data-ttu-id="388d1-132">Si está replicando VMware o servidores físicos, especifique un valor en días.</span><span class="sxs-lookup"><span data-stu-id="388d1-132">If you're replicating VMware or physical servers, input the value in days.</span></span> <span data-ttu-id="388d1-133">Si está replicando Hyper-V, especifique el tiempo en horas.</span><span class="sxs-lookup"><span data-stu-id="388d1-133">If you're replicating Hyper-V, specify the time in hours.</span></span>
   * <span data-ttu-id="388d1-134">En **Number of hours in which initial replication for the batch of virtual machines should complete** (Número de horas en las que debe completarse la replicación inicial para el lote de máquinas virtuales) y **Number of virtual machines per initial replication batch** (Número de máquinas virtuales por lote de replicación inicial) hay que especificar la configuración que se ha usado para procesar los requisitos de replicación iniciales.</span><span class="sxs-lookup"><span data-stu-id="388d1-134">In **Number of hours in which initial replication for the batch of virtual machines should complete** and **Number of virtual machines per initial replication batch**, you input settings that are used to compute initial replication requirements.</span></span>  <span data-ttu-id="388d1-135">Cuando se implementa Site Recovery, se debe cargar el conjunto de datos inicial completo.</span><span class="sxs-lookup"><span data-stu-id="388d1-135">When Site Recovery is deployed, the entire initial data set should be uploaded.</span></span>

   ![Entradas](./media/site-recovery-capacity-planner/inputs.png)
4. <span data-ttu-id="388d1-137">Después de haber especificado los valores para el entorno de origen, la salida mostrada incluye:</span><span class="sxs-lookup"><span data-stu-id="388d1-137">After you've put in the values for the source environment, displayed output includes:</span></span>

   * <span data-ttu-id="388d1-138">**Ancho de banda necesario para la replicación diferencial** (MB/s).</span><span class="sxs-lookup"><span data-stu-id="388d1-138">**Bandwidth required for delta replication** (MB/sec).</span></span> <span data-ttu-id="388d1-139">El ancho de banda de red necesario para la replicación diferencial se calcula según la tasa media diaria de cambio de datos.</span><span class="sxs-lookup"><span data-stu-id="388d1-139">Network bandwidth for delta replication is calculated on the average daily data change rate.</span></span>
   * <span data-ttu-id="388d1-140">**Ancho de banda necesario para la replicación inicial** (MB/s).</span><span class="sxs-lookup"><span data-stu-id="388d1-140">**Bandwidth required for initial replication** (MB/sec).</span></span> <span data-ttu-id="388d1-141">El ancho de banda de red para la replicación inicial se calcula según los valores de replicación inicial establecidos.</span><span class="sxs-lookup"><span data-stu-id="388d1-141">Network bandwidth for initial replication is calculated on the initial replication values you put in.</span></span>
   * <span data-ttu-id="388d1-142">**Almacenamiento necesario (en GB)** es el almacenamiento total requerido en Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-142">**Storage required (in GBs)** is the total Azure storage required.</span></span>
   * <span data-ttu-id="388d1-143">**IOPS totales en cuentas de almacenamiento estándar** se calcula en función de un tamaño de unidad IOPS de 8 K en las cuentas de almacenamiento estándar totales.</span><span class="sxs-lookup"><span data-stu-id="388d1-143">**Total IOPS on standard storage accounts** is calculated based on 8K IOPS unit size on the total standard storage accounts.</span></span>  <span data-ttu-id="388d1-144">Para Quick Planner, el número se calcula en función de todos los discos de máquinas virtuales de origen y la tasa de cambio de los datos diarios.</span><span class="sxs-lookup"><span data-stu-id="388d1-144">For the Quick Planner, the number is calculated based on all the source VMs disks and daily data change rate.</span></span> <span data-ttu-id="388d1-145">Para Detailed Planner el número se calcula en función del número total de máquinas virtuales que se asignan a las máquinas virtuales estándar de Azure y a la tasa de cambio de los datos en dichas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="388d1-145">For the Detailed Planner, the number is calculated based on total number of VMs that are mapped to standard Azure VMs, and data change rate on those VMs.</span></span>
   * <span data-ttu-id="388d1-146">**Número de cuentas de almacenamiento estándar** proporciona el número total de cuentas de almacenamiento estándar necesarias para proteger las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="388d1-146">**Number of standard storage accounts** provides the total number of standard storage accounts needed to protect the VMs.</span></span> <span data-ttu-id="388d1-147">Una cuenta de almacenamiento estándar puede contener hasta 20 000 IOPS en todas las máquinas virtuales de un almacenamiento estándar y admite un máximo de 500 IOPS por disco.</span><span class="sxs-lookup"><span data-stu-id="388d1-147">A standard storage account can hold up to 20000 IOPS across all the VMs in a standard storage, and a maximum of 500 IOPS is supported per disk.</span></span>
   * <span data-ttu-id="388d1-148">**Número de discos blob necesarios** proporciona el número de discos que se crearán en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-148">**Number of blob disks required** gives the number of disks that will be created on Azure storage.</span></span>
   * <span data-ttu-id="388d1-149">**Número de cuentas de almacenamiento premium necesarias** proporciona el número total de cuentas de almacenamiento premium necesarias para proteger las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="388d1-149">**Number of premium storage accounts required** provides the total number of premium storage accounts needed to protect the VMs.</span></span> <span data-ttu-id="388d1-150">Una máquina virtual de origen con una IOPS elevada (más de 20000) necesita una cuenta de Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="388d1-150">A source VM with high IOPS (greater than 20000) needs  a premium storage account.</span></span> <span data-ttu-id="388d1-151">Una cuenta de almacenamiento premium puede contener hasta 80 000 IOPS.</span><span class="sxs-lookup"><span data-stu-id="388d1-151">A premium storage account can hold up to 80000 IOPS.</span></span>
   * <span data-ttu-id="388d1-152">**IOPS totales en cuentas de almacenamiento premium** se calcula en función de un tamaño de unidad IOPS de 256 K en las cuentas de almacenamiento premium totales.</span><span class="sxs-lookup"><span data-stu-id="388d1-152">**Total IOPS on premium storage** is calculated based on 256K IOPS unit size on the total premium storage accounts.</span></span>  <span data-ttu-id="388d1-153">Para Quick Planner, el número se calcula en función de todos los discos de máquinas virtuales de origen y la tasa de cambio de los datos diarios.</span><span class="sxs-lookup"><span data-stu-id="388d1-153">For the Quick Planner, the number is calculated based on all the source VMs disks and daily data change rate.</span></span> <span data-ttu-id="388d1-154">Para Detailed Planner el número se calcula en función del número total de máquinas virtuales que se asignan a las máquinas virtuales premium de Azure (serie DS y GS) y a la tasa de cambio de los datos en dichas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="388d1-154">For the Detailed Planner, the number is calculated based on the total number of VMs that are mapped to premium Azure VM (DS and GS series), and the data change rate on those VMs.</span></span>
   * <span data-ttu-id="388d1-155">**Número de servidores de configuración necesarios** muestra cuántos servidores de configuración son necesarios para la implementación.</span><span class="sxs-lookup"><span data-stu-id="388d1-155">**Number of configuration servers required** shows how many configuration servers are required for the deployment.</span></span>
   * <span data-ttu-id="388d1-156">**Número de servidores de procesos adicionales necesarios** muestra si se requieren servidores de procesos adicionales, además del servidor de proceso configurado en el servidor de configuración de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="388d1-156">**Number of additional process servers required** shows whether additional process servers are required, in addition to the process server that's running on the configuration server by default.</span></span>
   * <span data-ttu-id="388d1-157">**100 % de almacenamiento adicional en origen** muestra si se necesita almacenamiento adicional en la ubicación de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-157">**100% additional storage on the source** shows whether additional storage is required in the source location.</span></span>

   ![Salida](./media/site-recovery-capacity-planner/output.png)

## <a name="run-the-detailed-planner"></a><span data-ttu-id="388d1-159">Ejecución de Detailed Planner</span><span class="sxs-lookup"><span data-stu-id="388d1-159">Run the Detailed Planner</span></span>

1. <span data-ttu-id="388d1-160">Descargue la herramienta [Capacity Planner de Azure Site Recovery](http://aka.ms/asr-capacity-planner-excel) y ábrala.</span><span class="sxs-lookup"><span data-stu-id="388d1-160">Download and open the [Azure Site Recovery Capacity Planner](http://aka.ms/asr-capacity-planner-excel) tool.</span></span> <span data-ttu-id="388d1-161">Como debe ejecutar macros, seleccione las opciones de permitir la edición y de habilitar el contenido cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="388d1-161">You need to run macros, so select to enable editing and enable content when prompted.</span></span>
2. <span data-ttu-id="388d1-162">En **Seleccionar un tipo de planificador**, elija **Planificador detallado** en el cuadro de lista.</span><span class="sxs-lookup"><span data-stu-id="388d1-162">In **Select a planner type**, select **Detailed Planner** from the list box.</span></span>

   ![Introducción](./media/site-recovery-capacity-planner/getting-started-2.png)
3. <span data-ttu-id="388d1-164">En la hoja de cálculo **Workload Qualification** , escriba la información necesaria.</span><span class="sxs-lookup"><span data-stu-id="388d1-164">In the **Workload Qualification** worksheet, enter the required information.</span></span> <span data-ttu-id="388d1-165">Debe rellenar todos los campos marcados.</span><span class="sxs-lookup"><span data-stu-id="388d1-165">You must fill in all the marked fields.</span></span>

   * <span data-ttu-id="388d1-166">En **Núcleos de procesador**, especifique el número total de núcleos de un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-166">In **Processor cores**, specify the total number of cores on a source server.</span></span>
   * <span data-ttu-id="388d1-167">En **Asignación de memoria en MB**, especifique el tamaño de la RAM de un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-167">In **Memory allocation in MB**, specify the RAM size of a source server.</span></span>
   * <span data-ttu-id="388d1-168">El valor **Número de NIC** especifica el número de adaptadores de red de un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-168">The **Number of NICs**, specify the number of network adapters on a source server.</span></span>
   * <span data-ttu-id="388d1-169">En **Almacenamiento total (en GB)**, especifique el tamaño total del almacenamiento de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="388d1-169">In **Total storage (in GB)**, specify the total size of the VM storage.</span></span> <span data-ttu-id="388d1-170">Por ejemplo, si el servidor de origen tiene 3 discos con 500 GB cada uno, el tamaño de almacenamiento total es de 1500 GB.</span><span class="sxs-lookup"><span data-stu-id="388d1-170">For example, if the source server has 3 disks with 500 GB each, then total storage size is 1500 GB.</span></span>
   * <span data-ttu-id="388d1-171">En **Número de discos conectados**, especifique el número total de discos de un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-171">In **Number of disks attached**, specify the total number of disks of a source server.</span></span>
   * <span data-ttu-id="388d1-172">En **Utilización de la capacidad de disco**, especifique el promedio de uso.</span><span class="sxs-lookup"><span data-stu-id="388d1-172">In **Disk capacity utilization**, specify the average utilization.</span></span>
   * <span data-ttu-id="388d1-173">En **Tasa de cambios diaria (%)**, especifique la tasa de cambios de datos diaria de un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-173">In **Daily change rate (%)**, specify the daily data change rate of a source server.</span></span>
   * <span data-ttu-id="388d1-174">En **Tamaño de asignación de Azure**, escriba el tamaño de la máquina virtual de Azure que desea asignar.</span><span class="sxs-lookup"><span data-stu-id="388d1-174">In **Mapping Azure size**, enter the Azure VM size that you want to map.</span></span> <span data-ttu-id="388d1-175">Si no quiere hacerlo manualmente, haga clic en **Compute IaaS VMs** (Calcular máquinas virtuales IaaS). Si especifica un valor de configuración manual y hace clic en Procesar máquinas virtuales de IaaS, puede que se sobrescriba la configuración manual, ya que el proceso identifica automáticamente la mejor coincidencia de tamaño de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-175">If you don't want to do this manually, click **Compute IaaS VMs**.If you input a manual setting, and then click Compute IaaS VMs, the manual setting might be overwritten because the compute process automatically identifies the best match on Azure VM size.</span></span>

   ![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification.png)
4. <span data-ttu-id="388d1-177">Al hacer clic en **Procesar máquinas virtuales de IaaS** :</span><span class="sxs-lookup"><span data-stu-id="388d1-177">If you click **Compute IaaS VMs** here's what it does:</span></span>

   * <span data-ttu-id="388d1-178">Se validan las entradas obligatorias.</span><span class="sxs-lookup"><span data-stu-id="388d1-178">Validates the mandatory inputs.</span></span>
   * <span data-ttu-id="388d1-179">Se calculan las IOPS y se sugiere la mejor coincidencia de tamaño de máquina virtual de Azure para cada máquina virtual apta para la replicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-179">Calculates IOPS and suggests the best Azure VM aize match for each VMs that's eligible for replication to Azure.</span></span> <span data-ttu-id="388d1-180">Se produce un error si no se detecta un tamaño adecuado para la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-180">If an appropriate size of Azure VM can't be detected an error is issued.</span></span> <span data-ttu-id="388d1-181">Por ejemplo, si el número de discos conectados es 65, se produce un error ya que el tamaño máximo de una máquina virtual de Azure es 64.</span><span class="sxs-lookup"><span data-stu-id="388d1-181">For example, if the number of disks attached in 65, an error is issued because the highest size Azure VM is 64.</span></span>
   * <span data-ttu-id="388d1-182">Sugiere una cuenta de almacenamiento que puede usar para una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-182">Suggests a storage account that can be used for an Azure VM.</span></span>
   * <span data-ttu-id="388d1-183">Calcula el número total de cuentas de almacenamiento estándar y de cuentas de almacenamiento premium que son necesarias para la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="388d1-183">Calculates the total number of standard storage accounts and premium storage accounts required for the workload.</span></span> <span data-ttu-id="388d1-184">Desplácese hacia abajo para ver el tipo de almacenamiento de Azure y la cuenta de almacenamiento que puede usar para un servidor de origen.</span><span class="sxs-lookup"><span data-stu-id="388d1-184">Scroll down to view the Azure storage type, and the storage account that can be used for a source server.</span></span>
   * <span data-ttu-id="388d1-185">Completa y ordena el resto de la tabla basándose en el tipo de almacenamiento necesario (estándar o premium) asignado a una máquina virtual y el número de discos conectados.</span><span class="sxs-lookup"><span data-stu-id="388d1-185">Completes and sorts the rest of the table based on required storage type (standard or premium) assigned for a VM, and the number of disks attached.</span></span> <span data-ttu-id="388d1-186">En todas las máquinas virtuales que cumplen los requisitos de Azure, la columna **Is VM qualified?** (¿Está calificada la máquina virtual?) muestra **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="388d1-186">For all VMs that meet the requirements for Azure, the column **Is VM qualified?** shows **Yes**.</span></span> <span data-ttu-id="388d1-187">Si no se puede realizar una copia de seguridad de la máquina virtual en Azure, se muestra un error.</span><span class="sxs-lookup"><span data-stu-id="388d1-187">If a VM can't be backed up to Azure, an error is shown.</span></span>

<span data-ttu-id="388d1-188">Las columnas AA hasta AE muestran los resultados y proporcionan información de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="388d1-188">Columns AA to AE are output, and provide information for each VM.</span></span>

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-2.png)

### <a name="example"></a><span data-ttu-id="388d1-190">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="388d1-190">Example</span></span>
<span data-ttu-id="388d1-191">Como ejemplo, para seis máquinas virtuales con los valores que se muestran en la tabla, la herramienta calcula y asigna la mejor coincidencia de máquina virtual de Azure y los requisitos de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="388d1-191">As an example, for six VMs with the values shown in the table, the tool calculates and assigns the best Azure VM match, and the Azure storage requirements.</span></span>

![Workload Qualification](./media/site-recovery-capacity-planner/workload-qualification-3.png)

* <span data-ttu-id="388d1-193">En el resultado del ejemplo, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="388d1-193">In the example output, note the following:</span></span>

  * <span data-ttu-id="388d1-194">La primera columna es una columna de validación para las máquinas virtuales, discos y renovación.</span><span class="sxs-lookup"><span data-stu-id="388d1-194">The first column is a validation column for the VMs, disks and churn.</span></span>
  * <span data-ttu-id="388d1-195">Se requieren dos cuentas de almacenamiento estándar y una cuenta de almacenamiento premium para las cinco máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="388d1-195">Two standard storage accounts and one premium storage account are needed for five VMs.</span></span>
  * <span data-ttu-id="388d1-196">VM3 no cumple los requisitos para la protección porque uno o más discos tienen más de 1 TB.</span><span class="sxs-lookup"><span data-stu-id="388d1-196">VM3 doesn't qualify for protection, because one or more disks are more than 1 TB.</span></span>
  * <span data-ttu-id="388d1-197">VM1 y VM2 pueden usar la primera cuenta de almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="388d1-197">VM1 and VM2 can use the first standard storage account</span></span>
  * <span data-ttu-id="388d1-198">VM4 puede usar la segunda cuenta de almacenamiento estándar</span><span class="sxs-lookup"><span data-stu-id="388d1-198">VM4 can use the second standard storage account.</span></span>
  * <span data-ttu-id="388d1-199">VM5 y VM6 necesitan una cuenta de Premium Storage y ambas pueden usar una única cuenta.</span><span class="sxs-lookup"><span data-stu-id="388d1-199">VM5 and VM6 need a premium storage account, and can both use a single account.</span></span>

    > [!NOTE]
    > <span data-ttu-id="388d1-200">Las IOPS de almacenamiento estándar y premium se calculan en el nivel de máquina virtual y no en el nivel de disco.</span><span class="sxs-lookup"><span data-stu-id="388d1-200">IOPS on standard and premium storage are calculated at the VM level, and not at disk level.</span></span> <span data-ttu-id="388d1-201">Una máquina virtual estándar puede controlar hasta 500 IOPS por disco.</span><span class="sxs-lookup"><span data-stu-id="388d1-201">A standard virtual machine can handle up to 500 IOPS per disk.</span></span> <span data-ttu-id="388d1-202">Si las IOPS de un disco son más de 500, necesitará Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="388d1-202">If IOPS for a disk are greater than 500, you need premium storage.</span></span> <span data-ttu-id="388d1-203">Sin embargo, si las IOPS de un disco son más de 500, pero las IOPS de todos los discos de máquina virtual están dentro de los límites admitidos para máquinas virtuales de Azure estándar (tamaño de máquina virtual, número de discos, número de adaptadores, CPU, memoria), el planificador elige una máquina virtual estándar en lugar de la serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="388d1-203">However, if IOPS for a disk are more than 500, but IOPS for the total VM disks are within the support standard Azure VM limits (VM size, number of disks, number of adapters, CPU, memory), then the planner picks a standard VM and not the DS or GS series.</span></span> <span data-ttu-id="388d1-204">El usuario debe actualizar manualmente la asignación de la celda de tamaño de Azure con la máquina virtual de serie DS o GS correspondiente.</span><span class="sxs-lookup"><span data-stu-id="388d1-204">You need to manually update the mapping Azure size cell with appropriate DS or GS series VM.</span></span>


<span data-ttu-id="388d1-205">Cuando toda la información esté definida, haga clic en **Enviar datos a la herramienta del planificador** para abrir la herramienta**Capacity Planner**. Las cargas de trabajo se resaltan para mostrar si cumplen los requisitos para la protección.</span><span class="sxs-lookup"><span data-stu-id="388d1-205">After all the details are in place, click **Submit data to the planner tool** to open the **Capacity Planner** Workloads are highlighted, to show whether they're eligible for protection or not.</span></span>

### <a name="submit-data-in-the-capacity-planner"></a><span data-ttu-id="388d1-206">Enviar datos en Capacity Planner</span><span class="sxs-lookup"><span data-stu-id="388d1-206">Submit data in the Capacity Planner</span></span>
1. <span data-ttu-id="388d1-207">Cuando se abre la hoja de datos **Capacity Planner** , esta se rellena en función de la configuración que haya especificado.</span><span class="sxs-lookup"><span data-stu-id="388d1-207">When you open the **Capacity Planner** worksheet it's populated based on the settings you've specified.</span></span> <span data-ttu-id="388d1-208">La palabra «Workload» aparece en la celda **Origen de entradas de infraestructura** para mostrar la entrada de la hoja de cálculo **Workload Qualification**.</span><span class="sxs-lookup"><span data-stu-id="388d1-208">The word 'Workload' appears in the **Infra inputs source** cell, to show that the input is the **Workload Qualification** worksheet.</span></span>
2. <span data-ttu-id="388d1-209">Si desea realizar cambios, deberá modificar la hoja de cálculo **Workload Qualification** y hacer clic de nuevo en **Enviar datos a la herramienta del planificador**.</span><span class="sxs-lookup"><span data-stu-id="388d1-209">If you want to make changes, you need to modify the **Workload Qualification** worksheet, and click **Submit data to the planner tool** again.</span></span>  

   ![Capacity Planner](./media/site-recovery-capacity-planner/capacity-planner.png)